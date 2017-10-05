---
title: Gegevens verplaatsen naar/van Azure DB die Cosmos | Microsoft Docs
description: Meer informatie over hoe gegevens worden verplaatst naar/van Azure DB die Cosmos-verzameling met behulp van Azure Data Factory
services: data-factory, cosmosdb
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c9297b71-1bb4-4b29-ba3c-4cf1f5575fac
ms.service: multiple
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 7a11c6ade0325b08ad520448bbf82d64a0a555f3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-to-and-from-azure-cosmos-db-using-azure-data-factory"></a><span data-ttu-id="8fe94-103">Gegevens verplaatsen en naar Azure Cosmos DB met Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="8fe94-103">Move data to and from Azure Cosmos DB using Azure Data Factory</span></span>
<span data-ttu-id="8fe94-104">In dit artikel wordt uitgelegd hoe u met de Kopieeractiviteit in Azure Data Factory te verplaatsen van gegevens uit Azure Cosmos-DB (DocumentDB-API).</span><span class="sxs-lookup"><span data-stu-id="8fe94-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure Cosmos DB (DocumentDB API).</span></span> <span data-ttu-id="8fe94-105">Dit is gebaseerd op de [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, hetgeen een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit toont.</span><span class="sxs-lookup"><span data-stu-id="8fe94-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

<span data-ttu-id="8fe94-106">U kunt gegevens kopiëren vanuit een ondersteunde brongegevensarchief bij Azure Cosmos DB of vanuit Azure Cosmos-database moet een ondersteunde sink-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="8fe94-106">You can copy data from any supported source data store to Azure Cosmos DB or from Azure Cosmos DB to any supported sink data store.</span></span> <span data-ttu-id="8fe94-107">Zie voor een lijst met gegevensarchieven als bronnen of PUT wordt ondersteund door de kopieeractiviteit, de [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel.</span><span class="sxs-lookup"><span data-stu-id="8fe94-107">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="8fe94-108">DocumentDB-API wordt alleen ondersteund door Azure DB Cosmos-connector.</span><span class="sxs-lookup"><span data-stu-id="8fe94-108">Azure Cosmos DB connector only support DocumentDB API.</span></span>

<span data-ttu-id="8fe94-109">Gegevens kopiëren-is naar/van de JSON-bestanden of een andere verzameling van de Cosmos-DB, Zie [voor importeren/exporteren JSON-documenten](#importexport-json-documents).</span><span class="sxs-lookup"><span data-stu-id="8fe94-109">To copy data as-is to/from JSON files or another Cosmos DB collection, see [Import/Export JSON documents](#importexport-json-documents).</span></span>

## <a name="getting-started"></a><span data-ttu-id="8fe94-110">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="8fe94-110">Getting started</span></span>
<span data-ttu-id="8fe94-111">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens uit Azure Cosmos DB verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="8fe94-111">You can create a pipeline with a copy activity that moves data to/from Azure Cosmos DB by using different tools/APIs.</span></span>

<span data-ttu-id="8fe94-112">De eenvoudigste manier om een pijplijn maken is met de **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="8fe94-112">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="8fe94-113">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met de wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="8fe94-113">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="8fe94-114">U kunt ook de volgende hulpprogramma's gebruiken voor het maken van een pijplijn: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon**, **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="8fe94-114">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="8fe94-115">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies voor een pijplijn maken met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="8fe94-115">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="8fe94-116">Of u de hulpprogramma's of API's gebruiken, moet u de volgende stappen voor het maken van een pijplijn die de gegevens vanuit een brongegevensarchief naar een gegevensarchief sink verplaatst uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="8fe94-116">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="8fe94-117">Maak **gekoppelde services** slaat om invoer- en gegevens te koppelen aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="8fe94-117">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="8fe94-118">Maak **gegevenssets** vertegenwoordigt de invoer- en -gegevens voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="8fe94-118">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="8fe94-119">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="8fe94-119">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="8fe94-120">Wanneer u de wizard gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8fe94-120">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="8fe94-121">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van de JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="8fe94-121">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="8fe94-122">Zie voor voorbeelden met JSON-definities voor Data Factory-entiteiten die worden gebruikt om gegevens te kopiëren naar/van de Cosmos-DB, [JSON voorbeelden](#json-examples) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="8fe94-122">For samples with JSON definitions for Data Factory entities that are used to copy data to/from Cosmos DB, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="8fe94-123">De volgende secties bevatten informatie over de JSON-eigenschappen die worden gebruikt voor het definiëren van Data Factory-entiteiten specifieke aan de Cosmos-database:</span><span class="sxs-lookup"><span data-stu-id="8fe94-123">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Cosmos DB:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="8fe94-124">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="8fe94-124">Linked service properties</span></span>
<span data-ttu-id="8fe94-125">De volgende tabel bevat een beschrijving voor JSON-elementen die specifiek zijn voor de service Azure Cosmos DB gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="8fe94-125">The following table provides description for JSON elements specific to Azure Cosmos DB linked service.</span></span>

| <span data-ttu-id="8fe94-126">**Eigenschap**</span><span class="sxs-lookup"><span data-stu-id="8fe94-126">**Property**</span></span> | <span data-ttu-id="8fe94-127">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="8fe94-127">**Description**</span></span> | <span data-ttu-id="8fe94-128">**Vereist**</span><span class="sxs-lookup"><span data-stu-id="8fe94-128">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8fe94-129">type</span><span class="sxs-lookup"><span data-stu-id="8fe94-129">type</span></span> |<span data-ttu-id="8fe94-130">De eigenschap type moet worden ingesteld op: **DocumentDb**</span><span class="sxs-lookup"><span data-stu-id="8fe94-130">The type property must be set to: **DocumentDb**</span></span> |<span data-ttu-id="8fe94-131">Ja</span><span class="sxs-lookup"><span data-stu-id="8fe94-131">Yes</span></span> |
| <span data-ttu-id="8fe94-132">connectionString</span><span class="sxs-lookup"><span data-stu-id="8fe94-132">connectionString</span></span> |<span data-ttu-id="8fe94-133">Geef informatie op die nodig zijn voor het verbinding maken met Azure DB die Cosmos-database.</span><span class="sxs-lookup"><span data-stu-id="8fe94-133">Specify information needed to connect to Azure Cosmos DB database.</span></span> |<span data-ttu-id="8fe94-134">Ja</span><span class="sxs-lookup"><span data-stu-id="8fe94-134">Yes</span></span> |

<span data-ttu-id="8fe94-135">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8fe94-135">Example:</span></span>

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="8fe94-136">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="8fe94-136">Dataset properties</span></span>
<span data-ttu-id="8fe94-137">Raadpleeg voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van de [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="8fe94-137">For a full list of sections & properties available for defining datasets please refer to the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="8fe94-138">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).</span><span class="sxs-lookup"><span data-stu-id="8fe94-138">Sections like structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="8fe94-139">De sectie typeProperties verschilt voor elk type gegevensset en bevat informatie over de locatie van de gegevens in het gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="8fe94-139">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="8fe94-140">De typeProperties sectie voor de gegevensset van het type **DocumentDbCollection** heeft de volgende eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="8fe94-140">The typeProperties section for the dataset of type **DocumentDbCollection** has the following properties.</span></span>

| <span data-ttu-id="8fe94-141">**Eigenschap**</span><span class="sxs-lookup"><span data-stu-id="8fe94-141">**Property**</span></span> | <span data-ttu-id="8fe94-142">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="8fe94-142">**Description**</span></span> | <span data-ttu-id="8fe94-143">**Vereist**</span><span class="sxs-lookup"><span data-stu-id="8fe94-143">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8fe94-144">CollectionName</span><span class="sxs-lookup"><span data-stu-id="8fe94-144">collectionName</span></span> |<span data-ttu-id="8fe94-145">De naam van de Cosmos-DB-document-verzameling.</span><span class="sxs-lookup"><span data-stu-id="8fe94-145">Name of the Cosmos DB document collection.</span></span> |<span data-ttu-id="8fe94-146">Ja</span><span class="sxs-lookup"><span data-stu-id="8fe94-146">Yes</span></span> |

<span data-ttu-id="8fe94-147">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8fe94-147">Example:</span></span>

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
### <a name="schema-by-data-factory"></a><span data-ttu-id="8fe94-148">Schema door Data Factory</span><span class="sxs-lookup"><span data-stu-id="8fe94-148">Schema by Data Factory</span></span>
<span data-ttu-id="8fe94-149">Voor gegevens zonder schema winkels zoals Azure Cosmos DB afleidt de Data Factory-service het schema in een van de volgende manieren:</span><span class="sxs-lookup"><span data-stu-id="8fe94-149">For schema-free data stores such as Azure Cosmos DB, the Data Factory service infers the schema in one of the following ways:</span></span>  

1. <span data-ttu-id="8fe94-150">Als u de structuur van gegevens met behulp van opgeven de **structuur** eigenschap in de definitie van de gegevensset, de Data Factory-service zich houdt aan deze structuur als het schema.</span><span class="sxs-lookup"><span data-stu-id="8fe94-150">If you specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service honors this structure as the schema.</span></span> <span data-ttu-id="8fe94-151">Als een rij geen waarde voor een kolom bevat, wordt in dit geval een null-waarde opgegeven voor deze.</span><span class="sxs-lookup"><span data-stu-id="8fe94-151">In this case, if a row does not contain a value for a column, a null value will be provided for it.</span></span>
2. <span data-ttu-id="8fe94-152">Als u de structuur van gegevens niet via opgeeft de **structuur** eigenschap in de definitie van de gegevensset, de Data Factory-service infereert het schema met behulp van de eerste rij in de gegevens.</span><span class="sxs-lookup"><span data-stu-id="8fe94-152">If you do not specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service infers the schema by using the first row in the data.</span></span> <span data-ttu-id="8fe94-153">In dit geval als de eerste rij niet het volledige schema bevat, sommige kolommen worden ontbreekt in het resultaat van de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="8fe94-153">In this case, if the first row does not contain the full schema, some columns will be missing in the result of copy operation.</span></span>

<span data-ttu-id="8fe94-154">Daarom voor gegevensbronnen zonder schema, de aanbevolen procedure is om op te geven van de structuur van gegevens met de **structuur** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="8fe94-154">Therefore, for schema-free data sources, the best practice is to specify the structure of data using the **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="8fe94-155">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="8fe94-155">Copy activity properties</span></span>
<span data-ttu-id="8fe94-156">Raadpleeg voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van activiteiten van de [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="8fe94-156">For a full list of sections & properties available for defining activities please refer to the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="8fe94-157">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en -beleid zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="8fe94-157">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="8fe94-158">De Kopieeractiviteit slechts één invoer en slechts één uitvoer produceert.</span><span class="sxs-lookup"><span data-stu-id="8fe94-158">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="8fe94-159">Eigenschappen die beschikbaar zijn in de sectie typeProperties van de activiteit aan de andere kant afwijken met elk activiteitstype en in geval van een kopieeractiviteit ze afhankelijk van de typen van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="8fe94-159">Properties available in the typeProperties section of the activity on the other hand vary with each activity type and in case of Copy activity they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="8fe94-160">In geval van een kopieeractiviteit wanneer de bron van het type **DocumentDbCollectionSource** de volgende eigenschappen beschikbaar zijn in **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="8fe94-160">In case of Copy activity when source is of type **DocumentDbCollectionSource** the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="8fe94-161">**Eigenschap**</span><span class="sxs-lookup"><span data-stu-id="8fe94-161">**Property**</span></span> | <span data-ttu-id="8fe94-162">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="8fe94-162">**Description**</span></span> | <span data-ttu-id="8fe94-163">**Toegestane waarden**</span><span class="sxs-lookup"><span data-stu-id="8fe94-163">**Allowed values**</span></span> | <span data-ttu-id="8fe94-164">**Vereist**</span><span class="sxs-lookup"><span data-stu-id="8fe94-164">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8fe94-165">query</span><span class="sxs-lookup"><span data-stu-id="8fe94-165">query</span></span> |<span data-ttu-id="8fe94-166">Specificeer de query voor het lezen van gegevens.</span><span class="sxs-lookup"><span data-stu-id="8fe94-166">Specify the query to read data.</span></span> |<span data-ttu-id="8fe94-167">Queryreeks wordt ondersteund door Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8fe94-167">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="8fe94-168">Voorbeeld:`SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="8fe94-168">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="8fe94-169">Nee</span><span class="sxs-lookup"><span data-stu-id="8fe94-169">No</span></span> <br/><br/><span data-ttu-id="8fe94-170">Als niet wordt opgegeven, de SQL-instructie die is uitgevoerd:`select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="8fe94-170">If not specified, the SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="8fe94-171">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="8fe94-171">nestingSeparator</span></span> |<span data-ttu-id="8fe94-172">Speciaal teken om aan te geven dat het document is genest</span><span class="sxs-lookup"><span data-stu-id="8fe94-172">Special character to indicate that the document is nested</span></span> |<span data-ttu-id="8fe94-173">Willekeurig teken.</span><span class="sxs-lookup"><span data-stu-id="8fe94-173">Any character.</span></span> <br/><br/><span data-ttu-id="8fe94-174">Azure Cosmos-database is een NoSQL-opslagplaats voor JSON-documenten, waarbij geneste structuren zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="8fe94-174">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="8fe94-175">Azure Data Factory kan gebruiker duiden hiërarchie via nestingSeparator die "."</span><span class="sxs-lookup"><span data-stu-id="8fe94-175">Azure Data Factory enables user to denote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="8fe94-176">in de bovenstaande voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="8fe94-176">in the above examples.</span></span> <span data-ttu-id="8fe94-177">Met het scheidingsteken, met de kopieerbewerking genereert het object "Name" met de drie onderliggende elementen eerst middelste en de laatste volgens 'Name.First', 'Name.Middle' en 'Name.Last' in de tabeldefinitie.</span><span class="sxs-lookup"><span data-stu-id="8fe94-177">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span></span> |<span data-ttu-id="8fe94-178">Nee</span><span class="sxs-lookup"><span data-stu-id="8fe94-178">No</span></span> |

<span data-ttu-id="8fe94-179">**DocumentDbCollectionSink** ondersteunt de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="8fe94-179">**DocumentDbCollectionSink** supports the following properties:</span></span>

| <span data-ttu-id="8fe94-180">**Eigenschap**</span><span class="sxs-lookup"><span data-stu-id="8fe94-180">**Property**</span></span> | <span data-ttu-id="8fe94-181">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="8fe94-181">**Description**</span></span> | <span data-ttu-id="8fe94-182">**Toegestane waarden**</span><span class="sxs-lookup"><span data-stu-id="8fe94-182">**Allowed values**</span></span> | <span data-ttu-id="8fe94-183">**Vereist**</span><span class="sxs-lookup"><span data-stu-id="8fe94-183">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="8fe94-184">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="8fe94-184">nestingSeparator</span></span> |<span data-ttu-id="8fe94-185">Er is een speciaal teken in naam van de bronkolom om aan te geven dat geneste document nodig.</span><span class="sxs-lookup"><span data-stu-id="8fe94-185">A special character in the source column name to indicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="8fe94-186">Zoals hierboven: `Name.First` in de uitvoer van de tabel de volgende JSON-structuur in het document Cosmos DB produceert:</span><span class="sxs-lookup"><span data-stu-id="8fe94-186">For example above: `Name.First` in the output table produces the following JSON structure in the Cosmos DB document:</span></span><br/><br/><span data-ttu-id="8fe94-187">"Name": {</span><span class="sxs-lookup"><span data-stu-id="8fe94-187">"Name": {</span></span><br/>    <span data-ttu-id="8fe94-188">' First ': 'John'</span><span class="sxs-lookup"><span data-stu-id="8fe94-188">"First": "John"</span></span><br/><span data-ttu-id="8fe94-189">},</span><span class="sxs-lookup"><span data-stu-id="8fe94-189">},</span></span> |<span data-ttu-id="8fe94-190">Teken dat wordt gebruikt voor het scheiden van geneste niveaus.</span><span class="sxs-lookup"><span data-stu-id="8fe94-190">Character that is used to separate nesting levels.</span></span><br/><br/><span data-ttu-id="8fe94-191">Standaardwaarde is `.` (punt).</span><span class="sxs-lookup"><span data-stu-id="8fe94-191">Default value is `.` (dot).</span></span> |<span data-ttu-id="8fe94-192">Teken dat wordt gebruikt voor het scheiden van geneste niveaus.</span><span class="sxs-lookup"><span data-stu-id="8fe94-192">Character that is used to separate nesting levels.</span></span> <br/><br/><span data-ttu-id="8fe94-193">Standaardwaarde is `.` (punt).</span><span class="sxs-lookup"><span data-stu-id="8fe94-193">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="8fe94-194">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="8fe94-194">writeBatchSize</span></span> |<span data-ttu-id="8fe94-195">Het aantal parallelle aanvragen voor Azure DB die Cosmos-service om documenten te maken.</span><span class="sxs-lookup"><span data-stu-id="8fe94-195">Number of parallel requests to Azure Cosmos DB service to create documents.</span></span><br/><br/><span data-ttu-id="8fe94-196">U kunt de prestaties aanpassen bij het kopiëren van gegevens van Cosmos-database met behulp van deze eigenschap.</span><span class="sxs-lookup"><span data-stu-id="8fe94-196">You can fine-tune the performance when copying data to/from Cosmos DB by using this property.</span></span> <span data-ttu-id="8fe94-197">U kunt een betere prestaties verwachten wanneer u writeBatchSize verhogen omdat meer parallelle aanvragen aan de Cosmos-database worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="8fe94-197">You can expect a better performance when you increase writeBatchSize because more parallel requests to Cosmos DB are sent.</span></span> <span data-ttu-id="8fe94-198">Moet u echter om te voorkomen dat beperking kunnen genereert het foutbericht weergegeven: 'Vragen snelheid is groot'.</span><span class="sxs-lookup"><span data-stu-id="8fe94-198">However you’ll need to avoid throttling that can throw the error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="8fe94-199">Beperking wordt bepaald door een aantal factoren, onder andere de grootte van documenten, aantal termen in documenten, indexeren beleid van de doelverzameling, enzovoort. Voor het kopiëren van, kunt u een betere verzameling (bijvoorbeeld S3) hebben de meeste beschikbare doorvoer (2500 aanvragen eenheden/seconde).</span><span class="sxs-lookup"><span data-stu-id="8fe94-199">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (e.g. S3) to have the most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="8fe94-200">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="8fe94-200">Integer</span></span> |<span data-ttu-id="8fe94-201">Nee (standaard: 5)</span><span class="sxs-lookup"><span data-stu-id="8fe94-201">No (default: 5)</span></span> |
| <span data-ttu-id="8fe94-202">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="8fe94-202">writeBatchTimeout</span></span> |<span data-ttu-id="8fe94-203">Wachttijd voor de bewerking te voltooien voordat er een optreedt time-out.</span><span class="sxs-lookup"><span data-stu-id="8fe94-203">Wait time for the operation to complete before it times out.</span></span> |<span data-ttu-id="8fe94-204">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="8fe94-204">timespan</span></span><br/><br/> <span data-ttu-id="8fe94-205">Voorbeeld: "00: 30:00 ' (30 minuten).</span><span class="sxs-lookup"><span data-stu-id="8fe94-205">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="8fe94-206">Nee</span><span class="sxs-lookup"><span data-stu-id="8fe94-206">No</span></span> |

## <a name="importexport-json-documents"></a><span data-ttu-id="8fe94-207">Import/Export JSON-documenten</span><span class="sxs-lookup"><span data-stu-id="8fe94-207">Import/Export JSON documents</span></span>
<span data-ttu-id="8fe94-208">Met deze Cosmos-DB-connector kunt u eenvoudig</span><span class="sxs-lookup"><span data-stu-id="8fe94-208">Using this Cosmos DB connector, you can easily</span></span>

* <span data-ttu-id="8fe94-209">JSON-documenten importeren uit diverse bronnen in Cosmos-DB, met inbegrip van Azure Blob Azure Data Lake, on-premises bestandssysteem of andere winkels op basis van bestanden die door Azure Data Factory worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="8fe94-209">Import JSON documents from various sources into Cosmos DB, including Azure Blob, Azure Data Lake, on-premises File System or other file-based stores supported by Azure Data Factory.</span></span>
* <span data-ttu-id="8fe94-210">JSON-documenten uit Cosmos DB gewijzigd exporteren in verschillende winkels op basis van bestanden.</span><span class="sxs-lookup"><span data-stu-id="8fe94-210">Export JSON documents from Cosmos DB collecton into various file-based stores.</span></span>
* <span data-ttu-id="8fe94-211">Gegevens migreren tussen twee Cosmos DB verzamelingen op als-is.</span><span class="sxs-lookup"><span data-stu-id="8fe94-211">Migrate data between two Cosmos DB collections as-is.</span></span>

<span data-ttu-id="8fe94-212">Als u dit schema networkdirect-exemplaar</span><span class="sxs-lookup"><span data-stu-id="8fe94-212">To achieve such schema-agnostic copy,</span></span> 
* <span data-ttu-id="8fe94-213">Als u de wizard kopiëren, moet u de **' exporteren als-JSON-bestanden of Cosmos DB verzameling '** optie.</span><span class="sxs-lookup"><span data-stu-id="8fe94-213">When using copy wizard, check the **"Export as-is to JSON files or Cosmos DB collection"** option.</span></span>
* <span data-ttu-id="8fe94-214">Wanneer met behulp van JSON bewerkt, geen de sectie 'structuur' opgeven in Cosmos DB gegevensset (s) en ook 'nestingSeparator'-eigenschap op Cosmos DB bron/sink in de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="8fe94-214">When using JSON editing, do not specify the "structure" section in Cosmos DB dataset(s) nor "nestingSeparator" property on Cosmos DB source/sink in copy activity.</span></span> <span data-ttu-id="8fe94-215">Als u wilt van importeren / exporteren naar JSON-bestanden, notatietype in de store-gegevensset bestand opgeven als 'JsonFormat', 'filePattern' config en overslaan van de instellingen van de rest-indeling, Zie [JSON-indeling](data-factory-supported-file-and-compression-formats.md#json-format) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8fe94-215">To import from/export to JSON files, in the file store dataset specify format type as "JsonFormat", config "filePattern" and skip the rest format settings, see [JSON format](data-factory-supported-file-and-compression-formats.md#json-format) section on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="8fe94-216">JSON-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="8fe94-216">JSON examples</span></span>
<span data-ttu-id="8fe94-217">De volgende voorbeelden geven voorbeeld JSON definities die u een pijplijn maken kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="8fe94-217">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="8fe94-218">Ze laten zien hoe om gegevens te kopiëren naar en van Azure DB die Cosmos en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="8fe94-218">They show how to copy data to and from Azure Cosmos DB and Azure Blob Storage.</span></span> <span data-ttu-id="8fe94-219">Echter, de gegevens kunnen worden gekopieerd **rechtstreeks** uit een van de bronnen aan een van de PUT vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van de Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="8fe94-219">However, data can be copied **directly** from any of the sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

## <a name="example-copy-data-from-azure-cosmos-db-to-azure-blob"></a><span data-ttu-id="8fe94-220">Voorbeeld: Gegevens kopiëren van Azure DB die Cosmos naar Azure Blob</span><span class="sxs-lookup"><span data-stu-id="8fe94-220">Example: Copy data from Azure Cosmos DB to Azure Blob</span></span>
<span data-ttu-id="8fe94-221">Het voorbeeld hieronder ziet:</span><span class="sxs-lookup"><span data-stu-id="8fe94-221">The sample below shows:</span></span>

1. <span data-ttu-id="8fe94-222">Een gekoppelde service van het type [DocumentDb](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8fe94-222">A linked service of type [DocumentDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="8fe94-223">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8fe94-223">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="8fe94-224">Invoer [gegevensset](data-factory-create-datasets.md) van het type [DocumentDbCollection](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8fe94-224">An input [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="8fe94-225">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8fe94-225">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="8fe94-226">Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [DocumentDbCollectionSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8fe94-226">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [DocumentDbCollectionSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="8fe94-227">Het voorbeeld worden gegevens in Azure Cosmos DB gekopieerd naar Azure-Blob.</span><span class="sxs-lookup"><span data-stu-id="8fe94-227">The sample copies data in Azure Cosmos DB to Azure Blob.</span></span> <span data-ttu-id="8fe94-228">De JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na de voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="8fe94-228">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="8fe94-229">**Azure Cosmos DB gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="8fe94-229">**Azure Cosmos DB linked service:**</span></span>

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
<span data-ttu-id="8fe94-230">**Azure Blob-opslag gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="8fe94-230">**Azure Blob storage linked service:**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="8fe94-231">**Invoergegevensset van Azure Document database:**</span><span class="sxs-lookup"><span data-stu-id="8fe94-231">**Azure Document DB input dataset:**</span></span>

<span data-ttu-id="8fe94-232">Het voorbeeld wordt ervan uitgegaan dat u hebt een verzameling met de naam **persoon** in een Azure DB die Cosmos-database.</span><span class="sxs-lookup"><span data-stu-id="8fe94-232">The sample assumes you have a collection named **Person** in an Azure Cosmos DB database.</span></span>

<span data-ttu-id="8fe94-233">Instelling 'extern': 'true' en externalData beleid gegevens over de Azure Data Factory-service die de tabel extern is aan de gegevensfactory en niet wordt geproduceerd door een activiteit in de gegevensfactory op te geven.</span><span class="sxs-lookup"><span data-stu-id="8fe94-233">Setting “external”: ”true” and specifying externalData policy information the Azure Data Factory service that the table is external to the data factory and not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="8fe94-234">**Azure Blob-uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="8fe94-234">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="8fe94-235">Gegevens worden gekopieerd naar een nieuwe blob elk uur met het pad voor de blob als gevolg van de specifieke datum/tijd met uur granulatie.</span><span class="sxs-lookup"><span data-stu-id="8fe94-235">Data is copied to a new blob every hour with the path for the blob reflecting the specific datetime with hour granularity.</span></span>

```JSON
{
  "name": "PersonBlobTableOut",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="8fe94-236">Voorbeeld JSON-document in de verzameling persoon in een Cosmos-DB-database:</span><span class="sxs-lookup"><span data-stu-id="8fe94-236">Sample JSON document in the Person collection in a Cosmos DB database:</span></span>

```JSON
{
  "PersonId": 2,
  "Name": {
    "First": "Jane",
    "Middle": "",
    "Last": "Doe"
  }
}
```
<span data-ttu-id="8fe94-237">Cosmos DB biedt ondersteuning voor documentquery's die gebruikmaken van een SQL zoals syntaxis via hiërarchische JSON-documenten.</span><span class="sxs-lookup"><span data-stu-id="8fe94-237">Cosmos DB supports querying documents using a SQL like syntax over hierarchical JSON documents.</span></span>

<span data-ttu-id="8fe94-238">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="8fe94-238">Example:</span></span> 

```sql
SELECT Person.PersonId, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person
```

<span data-ttu-id="8fe94-239">De volgende pijplijn kopieert invoergegevens uit de verzameling persoon in de Azure DB die Cosmos-database naar een Azure-blob.</span><span class="sxs-lookup"><span data-stu-id="8fe94-239">The following pipeline copies data from the Person collection in the Azure Cosmos DB database to an Azure blob.</span></span> <span data-ttu-id="8fe94-240">Als onderdeel van de kopieeractiviteit de invoer en uitvoer zijn gegevenssets opgegeven.</span><span class="sxs-lookup"><span data-stu-id="8fe94-240">As part of the copy activity the input and output datasets have been specified.</span></span>  

```JSON
{
  "name": "DocDbToBlobPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "DocumentDbCollectionSource",
            "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
            "nestingSeparator": "."
          },
          "sink": {
            "type": "BlobSink",
            "blobWriterAddHeader": true,
            "writeBatchSize": 1000,
            "writeBatchTimeout": "00:00:59"
          }
        },
        "inputs": [
          {
            "name": "PersonCosmosDbTable"
          }
        ],
        "outputs": [
          {
            "name": "PersonBlobTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromDocDbToBlob"
      }
    ],
    "start": "2015-04-01T00:00:00Z",
    "end": "2015-04-02T00:00:00Z"
  }
}
```
## <a name="example-copy-data-from-azure-blob-to-azure-cosmos-db"></a><span data-ttu-id="8fe94-241">Voorbeeld: Gegevens kopiëren van Azure-Blob naar Azure Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="8fe94-241">Example: Copy data from Azure Blob to Azure Cosmos DB</span></span> 
<span data-ttu-id="8fe94-242">Het voorbeeld hieronder ziet:</span><span class="sxs-lookup"><span data-stu-id="8fe94-242">The sample below shows:</span></span>

1. <span data-ttu-id="8fe94-243">Een gekoppelde service van het type [DocumentDb](#azure-documentdb-linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8fe94-243">A linked service of type [DocumentDb](#azure-documentdb-linked-service-properties).</span></span>
2. <span data-ttu-id="8fe94-244">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8fe94-244">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="8fe94-245">Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8fe94-245">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="8fe94-246">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span><span class="sxs-lookup"><span data-stu-id="8fe94-246">An output [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span></span>
5. <span data-ttu-id="8fe94-247">Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) en [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="8fe94-247">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span></span>

<span data-ttu-id="8fe94-248">Het voorbeeld kopieert gegevens van Azure blob naar Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="8fe94-248">The sample copies data from Azure blob to Azure Cosmos DB.</span></span> <span data-ttu-id="8fe94-249">De JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na de voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="8fe94-249">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="8fe94-250">**Azure Blob-opslag gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="8fe94-250">**Azure Blob storage linked service:**</span></span>

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="8fe94-251">**Azure Cosmos DB gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="8fe94-251">**Azure Cosmos DB linked service:**</span></span>

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
<span data-ttu-id="8fe94-252">**Azure Blob invoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="8fe94-252">**Azure Blob input dataset:**</span></span>

```JSON
{
  "name": "PersonBlobTableIn",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "MiddleName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "fileName": "input.csv",
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
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
<span data-ttu-id="8fe94-253">**Azure Cosmos DB uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="8fe94-253">**Azure Cosmos DB output dataset:**</span></span>

<span data-ttu-id="8fe94-254">Het voorbeeld worden gegevens gekopieerd naar een verzameling met de naam 'Persoon'.</span><span class="sxs-lookup"><span data-stu-id="8fe94-254">The sample copies data to a collection named “Person”.</span></span>

```JSON
{
  "name": "PersonCosmosDbTableOut",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "Name.First",
        "type": "String"
      },
      {
        "name": "Name.Middle",
        "type": "String"
      },
      {
        "name": "Name.Last",
        "type": "String"
      }
    ],
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="8fe94-255">De volgende pijplijn kopieert invoergegevens uit Azure Blob aan de verzameling persoon in de Cosmos-database.</span><span class="sxs-lookup"><span data-stu-id="8fe94-255">The following pipeline copies data from Azure Blob to the Person collection in the Cosmos DB.</span></span> <span data-ttu-id="8fe94-256">Als onderdeel van de kopieeractiviteit de invoer en uitvoer zijn gegevenssets opgegeven.</span><span class="sxs-lookup"><span data-stu-id="8fe94-256">As part of the copy activity the input and output datasets have been specified.</span></span>

```JSON
{
  "name": "BlobToDocDbPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "DocumentDbCollectionSink",
            "nestingSeparator": ".",
            "writeBatchSize": 2,
            "writeBatchTimeout": "00:00:00"
          }
          "translator": {
              "type": "TabularTranslator",
              "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, Title: Title, Suffix: Suffix, EmailPromotion: EmailPromotion, rowguid: rowguid, ModifiedDate: ModifiedDate"
          }
        },
        "inputs": [
          {
            "name": "PersonBlobTableIn"
          }
        ],
        "outputs": [
          {
            "name": "PersonCosmosDbTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromBlobToDocDb"
      }
    ],
    "start": "2015-04-14T00:00:00Z",
    "end": "2015-04-15T00:00:00Z"
  }
}
```
<span data-ttu-id="8fe94-257">Als de invoer van de blob voorbeeld als</span><span class="sxs-lookup"><span data-stu-id="8fe94-257">If the sample blob input is as</span></span>

```
1,John,,Doe
```
<span data-ttu-id="8fe94-258">Vervolgens wordt de uitvoer van de JSON-code in Cosmos-DB worden als:</span><span class="sxs-lookup"><span data-stu-id="8fe94-258">Then the output JSON in Cosmos DB will be as:</span></span>

```JSON
{
  "Id": 1,
  "Name": {
    "First": "John",
    "Middle": null,
    "Last": "Doe"
  },
  "id": "a5e8595c-62ec-4554-a118-3940f4ff70b6"
}
```
<span data-ttu-id="8fe94-259">Azure Cosmos-database is een NoSQL-opslagplaats voor JSON-documenten, waarbij geneste structuren zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="8fe94-259">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="8fe94-260">Azure Data Factory kan gebruiker duiden hiërarchie via **nestingSeparator**, namelijk '. '</span><span class="sxs-lookup"><span data-stu-id="8fe94-260">Azure Data Factory enables user to denote hierarchy via **nestingSeparator**, which is “.”</span></span> <span data-ttu-id="8fe94-261">in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="8fe94-261">in this example.</span></span> <span data-ttu-id="8fe94-262">Met het scheidingsteken, met de kopieerbewerking genereert het object "Name" met de drie onderliggende elementen eerst middelste en de laatste volgens 'Name.First', 'Name.Middle' en 'Name.Last' in de tabeldefinitie.</span><span class="sxs-lookup"><span data-stu-id="8fe94-262">With the separator, the copy activity will generate the “Name” object with three children elements First, Middle and Last, according to “Name.First”, “Name.Middle” and “Name.Last” in the table definition.</span></span>

## <a name="appendix"></a><span data-ttu-id="8fe94-263">Bijlage</span><span class="sxs-lookup"><span data-stu-id="8fe94-263">Appendix</span></span>
1. <span data-ttu-id="8fe94-264">**Vraag:** heeft de update voor de Kopieeractiviteit ondersteuning van bestaande records?</span><span class="sxs-lookup"><span data-stu-id="8fe94-264">**Question:** Does the Copy Activity support update of existing records?</span></span>

    <span data-ttu-id="8fe94-265">**Antwoord:** Nee.</span><span class="sxs-lookup"><span data-stu-id="8fe94-265">**Answer:** No.</span></span>
2. <span data-ttu-id="8fe94-266">**Vraag:** records hoe al biedt een nieuwe poging van een kopie te behandelen Azure Cosmos DB gekopieerd?</span><span class="sxs-lookup"><span data-stu-id="8fe94-266">**Question:** How does a retry of a copy to Azure Cosmos DB deal with already copied records?</span></span>

    <span data-ttu-id="8fe94-267">**Antwoord:** als records een veld 'ID hebben' en de kopieerbewerking wordt geprobeerd een record met dezelfde ID in te voegen, de kopieerbewerking een fout genereert.</span><span class="sxs-lookup"><span data-stu-id="8fe94-267">**Answer:** If records have an "ID" field and the copy operation tries to insert a record with the same ID, the copy operation throws an error.</span></span>  
3. <span data-ttu-id="8fe94-268">**Vraag:** biedt ondersteuning voor Data Factory [bereik of de gegevens op basis van het hash-partitionering](../documentdb/documentdb-partition-data.md)?</span><span class="sxs-lookup"><span data-stu-id="8fe94-268">**Question:** Does Data Factory support [range or hash-based data partitioning](../documentdb/documentdb-partition-data.md)?</span></span>

    <span data-ttu-id="8fe94-269">**Antwoord:** Nee.</span><span class="sxs-lookup"><span data-stu-id="8fe94-269">**Answer:** No.</span></span>
4. <span data-ttu-id="8fe94-270">**Vraag:** kan ik meer dan één Azure Cosmos DB verzameling voor een tabel opgeven?</span><span class="sxs-lookup"><span data-stu-id="8fe94-270">**Question:** Can I specify more than one Azure Cosmos DB collection for a table?</span></span>

    <span data-ttu-id="8fe94-271">**Antwoord:** Nee.</span><span class="sxs-lookup"><span data-stu-id="8fe94-271">**Answer:** No.</span></span> <span data-ttu-id="8fe94-272">Slechts één verzameling kan op dit moment worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="8fe94-272">Only one collection can be specified at this time.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="8fe94-273">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="8fe94-273">Performance and Tuning</span></span>
<span data-ttu-id="8fe94-274">Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) voor meer informatie over de belangrijkste factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren om te optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="8fe94-274">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
