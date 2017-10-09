---
title: aaaMove gegevens van/naar Azure Cosmos DB | Microsoft Docs
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
ms.openlocfilehash: bd23ce4e004a972ce6f3e4165cfdea4f0c18fecc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-cosmos-db-using-azure-data-factory"></a><span data-ttu-id="e2a59-103">Verplaatsen van gegevens tooand van Azure Cosmos DB met Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="e2a59-103">Move data tooand from Azure Cosmos DB using Azure Data Factory</span></span>
<span data-ttu-id="e2a59-104">Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit Hallo in Azure Data Factory toomove gegevens uit Azure Cosmos-DB (DocumentDB-API).</span><span class="sxs-lookup"><span data-stu-id="e2a59-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from Azure Cosmos DB (DocumentDB API).</span></span> <span data-ttu-id="e2a59-105">Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.</span><span class="sxs-lookup"><span data-stu-id="e2a59-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

<span data-ttu-id="e2a59-106">U kunt gegevens kopiëren van een ondersteunde bron gegevens tooAzure Cosmos DB opslaan of opslaan van gegevens van Azure DB die Cosmos tooany ondersteund sink.</span><span class="sxs-lookup"><span data-stu-id="e2a59-106">You can copy data from any supported source data store tooAzure Cosmos DB or from Azure Cosmos DB tooany supported sink data store.</span></span> <span data-ttu-id="e2a59-107">Zie voor een lijst van gegevensarchieven als bronnen of PUT wordt ondersteund door kopieeractiviteit Hallo Hallo [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel.</span><span class="sxs-lookup"><span data-stu-id="e2a59-107">For a list of data stores supported as sources or sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="e2a59-108">DocumentDB-API wordt alleen ondersteund door Azure DB Cosmos-connector.</span><span class="sxs-lookup"><span data-stu-id="e2a59-108">Azure Cosmos DB connector only support DocumentDB API.</span></span>

<span data-ttu-id="e2a59-109">gegevens als toocopy-is naar/van de JSON-bestanden of een andere verzameling van de Cosmos-DB, Zie [voor importeren/exporteren JSON-documenten](#importexport-json-documents).</span><span class="sxs-lookup"><span data-stu-id="e2a59-109">toocopy data as-is to/from JSON files or another Cosmos DB collection, see [Import/Export JSON documents](#importexport-json-documents).</span></span>

## <a name="getting-started"></a><span data-ttu-id="e2a59-110">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="e2a59-110">Getting started</span></span>
<span data-ttu-id="e2a59-111">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens uit Azure Cosmos DB verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="e2a59-111">You can create a pipeline with a copy activity that moves data to/from Azure Cosmos DB by using different tools/APIs.</span></span>

<span data-ttu-id="e2a59-112">Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="e2a59-112">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="e2a59-113">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="e2a59-113">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="e2a59-114">U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="e2a59-114">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="e2a59-115">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="e2a59-115">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="e2a59-116">Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="e2a59-116">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="e2a59-117">Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="e2a59-117">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="e2a59-118">Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="e2a59-118">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="e2a59-119">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="e2a59-119">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="e2a59-120">Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e2a59-120">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="e2a59-121">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="e2a59-121">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="e2a59-122">Zie voor voorbeelden met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens van/naar Cosmos DB zijn, [JSON voorbeelden](#json-examples) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="e2a59-122">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from Cosmos DB, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="e2a59-123">Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooCosmos DB zijn:</span><span class="sxs-lookup"><span data-stu-id="e2a59-123">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooCosmos DB:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="e2a59-124">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="e2a59-124">Linked service properties</span></span>
<span data-ttu-id="e2a59-125">Hallo volgende tabel bevat een beschrijving voor JSON-elementen specifieke tooAzure Cosmos DB gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="e2a59-125">hello following table provides description for JSON elements specific tooAzure Cosmos DB linked service.</span></span>

| <span data-ttu-id="e2a59-126">**Eigenschap**</span><span class="sxs-lookup"><span data-stu-id="e2a59-126">**Property**</span></span> | <span data-ttu-id="e2a59-127">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="e2a59-127">**Description**</span></span> | <span data-ttu-id="e2a59-128">**Vereist**</span><span class="sxs-lookup"><span data-stu-id="e2a59-128">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e2a59-129">type</span><span class="sxs-lookup"><span data-stu-id="e2a59-129">type</span></span> |<span data-ttu-id="e2a59-130">Hallo type eigenschap moet worden ingesteld op: **DocumentDb**</span><span class="sxs-lookup"><span data-stu-id="e2a59-130">hello type property must be set to: **DocumentDb**</span></span> |<span data-ttu-id="e2a59-131">Ja</span><span class="sxs-lookup"><span data-stu-id="e2a59-131">Yes</span></span> |
| <span data-ttu-id="e2a59-132">connectionString</span><span class="sxs-lookup"><span data-stu-id="e2a59-132">connectionString</span></span> |<span data-ttu-id="e2a59-133">Geef informatie nodig tooconnect tooAzure Cosmos-DB-database.</span><span class="sxs-lookup"><span data-stu-id="e2a59-133">Specify information needed tooconnect tooAzure Cosmos DB database.</span></span> |<span data-ttu-id="e2a59-134">Ja</span><span class="sxs-lookup"><span data-stu-id="e2a59-134">Yes</span></span> |

<span data-ttu-id="e2a59-135">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e2a59-135">Example:</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="e2a59-136">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="e2a59-136">Dataset properties</span></span>
<span data-ttu-id="e2a59-137">Raadpleeg voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van toohello [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="e2a59-137">For a full list of sections & properties available for defining datasets please refer toohello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="e2a59-138">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).</span><span class="sxs-lookup"><span data-stu-id="e2a59-138">Sections like structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="e2a59-139">Hallo typeProperties sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="e2a59-139">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="e2a59-140">Hallo typeProperties sectie voor de gegevensset Hallo van het type **DocumentDbCollection** Hallo volgende eigenschappen heeft.</span><span class="sxs-lookup"><span data-stu-id="e2a59-140">hello typeProperties section for hello dataset of type **DocumentDbCollection** has hello following properties.</span></span>

| <span data-ttu-id="e2a59-141">**Eigenschap**</span><span class="sxs-lookup"><span data-stu-id="e2a59-141">**Property**</span></span> | <span data-ttu-id="e2a59-142">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="e2a59-142">**Description**</span></span> | <span data-ttu-id="e2a59-143">**Vereist**</span><span class="sxs-lookup"><span data-stu-id="e2a59-143">**Required**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e2a59-144">CollectionName</span><span class="sxs-lookup"><span data-stu-id="e2a59-144">collectionName</span></span> |<span data-ttu-id="e2a59-145">Naam van Hallo documentverzameling Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e2a59-145">Name of hello Cosmos DB document collection.</span></span> |<span data-ttu-id="e2a59-146">Ja</span><span class="sxs-lookup"><span data-stu-id="e2a59-146">Yes</span></span> |

<span data-ttu-id="e2a59-147">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e2a59-147">Example:</span></span>

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
### <a name="schema-by-data-factory"></a><span data-ttu-id="e2a59-148">Schema door Data Factory</span><span class="sxs-lookup"><span data-stu-id="e2a59-148">Schema by Data Factory</span></span>
<span data-ttu-id="e2a59-149">Voor gegevens zonder schema winkels zoals Azure Cosmos DB afleidt Hallo Data Factory-service Hallo schema in een van de volgende manieren Hallo:</span><span class="sxs-lookup"><span data-stu-id="e2a59-149">For schema-free data stores such as Azure Cosmos DB, hello Data Factory service infers hello schema in one of hello following ways:</span></span>  

1. <span data-ttu-id="e2a59-150">Als u Hallo-structuur van gegevens opgeeft met behulp van Hallo **structuur** eigenschap in de gegevenssetdefinitie hello, Hallo Data Factory-service zich houdt aan deze structuur als Hallo schema.</span><span class="sxs-lookup"><span data-stu-id="e2a59-150">If you specify hello structure of data by using hello **structure** property in hello dataset definition, hello Data Factory service honors this structure as hello schema.</span></span> <span data-ttu-id="e2a59-151">Als een rij geen waarde voor een kolom bevat, wordt in dit geval een null-waarde opgegeven voor deze.</span><span class="sxs-lookup"><span data-stu-id="e2a59-151">In this case, if a row does not contain a value for a column, a null value will be provided for it.</span></span>
2. <span data-ttu-id="e2a59-152">Als u niet Hallo-structuur van gegevens opgeeft met behulp van Hallo **structuur** eigenschap in de gegevenssetdefinitie hello, Hallo Data Factory-service Hallo schema afleidt met behulp van de eerste rij Hallo in Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="e2a59-152">If you do not specify hello structure of data by using hello **structure** property in hello dataset definition, hello Data Factory service infers hello schema by using hello first row in hello data.</span></span> <span data-ttu-id="e2a59-153">In dit geval als de eerste rij Hallo bevat geen volledige schema hello, sommige kolommen worden ontbreekt in Hallo resultaat van de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="e2a59-153">In this case, if hello first row does not contain hello full schema, some columns will be missing in hello result of copy operation.</span></span>

<span data-ttu-id="e2a59-154">Voor gegevensbronnen zonder schema, Hallo aanbevolen procedure is daarom toospecify Hallo structuur van gegevens met behulp van Hallo **structuur** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="e2a59-154">Therefore, for schema-free data sources, hello best practice is toospecify hello structure of data using hello **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="e2a59-155">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="e2a59-155">Copy activity properties</span></span>
<span data-ttu-id="e2a59-156">Raadpleeg voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten toohello [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="e2a59-156">For a full list of sections & properties available for defining activities please refer toohello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="e2a59-157">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en -beleid zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="e2a59-157">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="e2a59-158">Hallo Kopieeractiviteit slechts één invoer en slechts één uitvoer produceert.</span><span class="sxs-lookup"><span data-stu-id="e2a59-158">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="e2a59-159">Eigenschappen beschikbaar zijn in Hallo typeProperties sectie Hallo-activiteit op Hallo anderzijds met elk activiteitstype en variëren in geval van een kopieeractiviteit afhankelijk van Hallo soorten gegevensbronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="e2a59-159">Properties available in hello typeProperties section of hello activity on hello other hand vary with each activity type and in case of Copy activity they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="e2a59-160">In geval van een kopieeractiviteit wanneer de bron van het type **DocumentDbCollectionSource** Hallo volgende eigenschappen beschikbaar zijn in **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="e2a59-160">In case of Copy activity when source is of type **DocumentDbCollectionSource** hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="e2a59-161">**Eigenschap**</span><span class="sxs-lookup"><span data-stu-id="e2a59-161">**Property**</span></span> | <span data-ttu-id="e2a59-162">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="e2a59-162">**Description**</span></span> | <span data-ttu-id="e2a59-163">**Toegestane waarden**</span><span class="sxs-lookup"><span data-stu-id="e2a59-163">**Allowed values**</span></span> | <span data-ttu-id="e2a59-164">**Vereist**</span><span class="sxs-lookup"><span data-stu-id="e2a59-164">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e2a59-165">query</span><span class="sxs-lookup"><span data-stu-id="e2a59-165">query</span></span> |<span data-ttu-id="e2a59-166">Geef gegevens op Hallo query tooread.</span><span class="sxs-lookup"><span data-stu-id="e2a59-166">Specify hello query tooread data.</span></span> |<span data-ttu-id="e2a59-167">Queryreeks wordt ondersteund door Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e2a59-167">Query string supported by Azure Cosmos DB.</span></span> <br/><br/><span data-ttu-id="e2a59-168">Voorbeeld:`SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span><span class="sxs-lookup"><span data-stu-id="e2a59-168">Example: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"`</span></span> |<span data-ttu-id="e2a59-169">Nee</span><span class="sxs-lookup"><span data-stu-id="e2a59-169">No</span></span> <br/><br/><span data-ttu-id="e2a59-170">Als niet wordt opgegeven, Hallo SQL-instructie die is uitgevoerd:`select <columns defined in structure> from mycollection`</span><span class="sxs-lookup"><span data-stu-id="e2a59-170">If not specified, hello SQL statement that is executed: `select <columns defined in structure> from mycollection`</span></span> |
| <span data-ttu-id="e2a59-171">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="e2a59-171">nestingSeparator</span></span> |<span data-ttu-id="e2a59-172">Speciaal teken tooindicate dat document Hallo is genest</span><span class="sxs-lookup"><span data-stu-id="e2a59-172">Special character tooindicate that hello document is nested</span></span> |<span data-ttu-id="e2a59-173">Willekeurig teken.</span><span class="sxs-lookup"><span data-stu-id="e2a59-173">Any character.</span></span> <br/><br/><span data-ttu-id="e2a59-174">Azure Cosmos-database is een NoSQL-opslagplaats voor JSON-documenten, waarbij geneste structuren zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="e2a59-174">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="e2a59-175">Azure Data Factory kunt toodenote gebruikershiërarchie via nestingSeparator die "."</span><span class="sxs-lookup"><span data-stu-id="e2a59-175">Azure Data Factory enables user toodenote hierarchy via nestingSeparator, which is “.”</span></span> <span data-ttu-id="e2a59-176">in hello bovenstaande voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="e2a59-176">in hello above examples.</span></span> <span data-ttu-id="e2a59-177">Met Hallo scheidingsteken, genereert kopieeractiviteit Hallo Hallo "Name" object met drie onderliggende elementen eerste, middelste en laatste, volgens too"Name.First ', 'Name.Middle' en 'Name.Last' in hello tabeldefinitie.</span><span class="sxs-lookup"><span data-stu-id="e2a59-177">With hello separator, hello copy activity will generate hello “Name” object with three children elements First, Middle and Last, according too“Name.First”, “Name.Middle” and “Name.Last” in hello table definition.</span></span> |<span data-ttu-id="e2a59-178">Nee</span><span class="sxs-lookup"><span data-stu-id="e2a59-178">No</span></span> |

<span data-ttu-id="e2a59-179">**DocumentDbCollectionSink** ondersteunt Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="e2a59-179">**DocumentDbCollectionSink** supports hello following properties:</span></span>

| <span data-ttu-id="e2a59-180">**Eigenschap**</span><span class="sxs-lookup"><span data-stu-id="e2a59-180">**Property**</span></span> | <span data-ttu-id="e2a59-181">**Beschrijving**</span><span class="sxs-lookup"><span data-stu-id="e2a59-181">**Description**</span></span> | <span data-ttu-id="e2a59-182">**Toegestane waarden**</span><span class="sxs-lookup"><span data-stu-id="e2a59-182">**Allowed values**</span></span> | <span data-ttu-id="e2a59-183">**Vereist**</span><span class="sxs-lookup"><span data-stu-id="e2a59-183">**Required**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e2a59-184">nestingSeparator</span><span class="sxs-lookup"><span data-stu-id="e2a59-184">nestingSeparator</span></span> |<span data-ttu-id="e2a59-185">Er is een speciaal teken in Hallo bron kolom naam tooindicate dat document genest nodig.</span><span class="sxs-lookup"><span data-stu-id="e2a59-185">A special character in hello source column name tooindicate that nested document is needed.</span></span> <br/><br/><span data-ttu-id="e2a59-186">Zoals hierboven: `Name.First` in Hallo-uitvoer produceert tabel Hallo JSON-structuur in Hallo Cosmos DB document te volgen:</span><span class="sxs-lookup"><span data-stu-id="e2a59-186">For example above: `Name.First` in hello output table produces hello following JSON structure in hello Cosmos DB document:</span></span><br/><br/><span data-ttu-id="e2a59-187">"Name": {</span><span class="sxs-lookup"><span data-stu-id="e2a59-187">"Name": {</span></span><br/>    <span data-ttu-id="e2a59-188">' First ': 'John'</span><span class="sxs-lookup"><span data-stu-id="e2a59-188">"First": "John"</span></span><br/><span data-ttu-id="e2a59-189">},</span><span class="sxs-lookup"><span data-stu-id="e2a59-189">},</span></span> |<span data-ttu-id="e2a59-190">Teken gebruikte tooseparate aantal geneste niveaus.</span><span class="sxs-lookup"><span data-stu-id="e2a59-190">Character that is used tooseparate nesting levels.</span></span><br/><br/><span data-ttu-id="e2a59-191">Standaardwaarde is `.` (punt).</span><span class="sxs-lookup"><span data-stu-id="e2a59-191">Default value is `.` (dot).</span></span> |<span data-ttu-id="e2a59-192">Teken gebruikte tooseparate aantal geneste niveaus.</span><span class="sxs-lookup"><span data-stu-id="e2a59-192">Character that is used tooseparate nesting levels.</span></span> <br/><br/><span data-ttu-id="e2a59-193">Standaardwaarde is `.` (punt).</span><span class="sxs-lookup"><span data-stu-id="e2a59-193">Default value is `.` (dot).</span></span> |
| <span data-ttu-id="e2a59-194">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="e2a59-194">writeBatchSize</span></span> |<span data-ttu-id="e2a59-195">Aantal parallelle aanvragen tooAzure Cosmos DB service toocreate documenten.</span><span class="sxs-lookup"><span data-stu-id="e2a59-195">Number of parallel requests tooAzure Cosmos DB service toocreate documents.</span></span><br/><br/><span data-ttu-id="e2a59-196">Bij het kopiëren van gegevens van Cosmos-database met behulp van deze eigenschap kunt u de prestaties van Hallo verfijnen.</span><span class="sxs-lookup"><span data-stu-id="e2a59-196">You can fine-tune hello performance when copying data to/from Cosmos DB by using this property.</span></span> <span data-ttu-id="e2a59-197">U kunt een betere prestaties verwachten wanneer u writeBatchSize verhogen omdat meer parallelle aanvragen tooCosmos DB worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="e2a59-197">You can expect a better performance when you increase writeBatchSize because more parallel requests tooCosmos DB are sent.</span></span> <span data-ttu-id="e2a59-198">Maar u moet tooavoid beperking die kunnen genereert fout het Hallo-bericht: 'Vragen snelheid is groot'.</span><span class="sxs-lookup"><span data-stu-id="e2a59-198">However you’ll need tooavoid throttling that can throw hello error message: "Request rate is large".</span></span><br/><br/><span data-ttu-id="e2a59-199">Beperking wordt bepaald door een aantal factoren, onder andere de grootte van documenten, aantal termen in documenten, indexeren beleid van de doelverzameling, enzovoort. Voor het kopiëren van, kunt u een betere verzameling (bijvoorbeeld S3) toohave Hallo meeste doorvoer beschikbaar (2500 aanvragen eenheden/seconde).</span><span class="sxs-lookup"><span data-stu-id="e2a59-199">Throttling is decided by a number of factors, including size of documents, number of terms in documents, indexing policy of target collection, etc. For copy operations, you can use a better collection (e.g. S3) toohave hello most throughput available (2,500 request units/second).</span></span> |<span data-ttu-id="e2a59-200">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="e2a59-200">Integer</span></span> |<span data-ttu-id="e2a59-201">Nee (standaard: 5)</span><span class="sxs-lookup"><span data-stu-id="e2a59-201">No (default: 5)</span></span> |
| <span data-ttu-id="e2a59-202">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="e2a59-202">writeBatchTimeout</span></span> |<span data-ttu-id="e2a59-203">Wachttijd voor Hallo bewerking toocomplete voordat een time-out optreedt.</span><span class="sxs-lookup"><span data-stu-id="e2a59-203">Wait time for hello operation toocomplete before it times out.</span></span> |<span data-ttu-id="e2a59-204">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e2a59-204">timespan</span></span><br/><br/> <span data-ttu-id="e2a59-205">Voorbeeld: "00: 30:00 ' (30 minuten).</span><span class="sxs-lookup"><span data-stu-id="e2a59-205">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="e2a59-206">Nee</span><span class="sxs-lookup"><span data-stu-id="e2a59-206">No</span></span> |

## <a name="importexport-json-documents"></a><span data-ttu-id="e2a59-207">Import/Export JSON-documenten</span><span class="sxs-lookup"><span data-stu-id="e2a59-207">Import/Export JSON documents</span></span>
<span data-ttu-id="e2a59-208">Met deze Cosmos-DB-connector kunt u eenvoudig</span><span class="sxs-lookup"><span data-stu-id="e2a59-208">Using this Cosmos DB connector, you can easily</span></span>

* <span data-ttu-id="e2a59-209">JSON-documenten importeren uit diverse bronnen in Cosmos-DB, met inbegrip van Azure Blob Azure Data Lake, on-premises bestandssysteem of andere winkels op basis van bestanden die door Azure Data Factory worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="e2a59-209">Import JSON documents from various sources into Cosmos DB, including Azure Blob, Azure Data Lake, on-premises File System or other file-based stores supported by Azure Data Factory.</span></span>
* <span data-ttu-id="e2a59-210">JSON-documenten uit Cosmos DB gewijzigd exporteren in verschillende winkels op basis van bestanden.</span><span class="sxs-lookup"><span data-stu-id="e2a59-210">Export JSON documents from Cosmos DB collecton into various file-based stores.</span></span>
* <span data-ttu-id="e2a59-211">Gegevens migreren tussen twee Cosmos DB verzamelingen op als-is.</span><span class="sxs-lookup"><span data-stu-id="e2a59-211">Migrate data between two Cosmos DB collections as-is.</span></span>

<span data-ttu-id="e2a59-212">tooachieve dergelijke schema-networkdirect kopiëren</span><span class="sxs-lookup"><span data-stu-id="e2a59-212">tooachieve such schema-agnostic copy,</span></span> 
* <span data-ttu-id="e2a59-213">Als u de wizard kopiëren, moet u Hallo **' exporteren als-tooJSON bestanden of Cosmos DB verzameling '** optie.</span><span class="sxs-lookup"><span data-stu-id="e2a59-213">When using copy wizard, check hello **"Export as-is tooJSON files or Cosmos DB collection"** option.</span></span>
* <span data-ttu-id="e2a59-214">Wanneer met behulp van JSON bewerkt, geen Hallo "structuur" sectie opgeven in Cosmos DB gegevensset (s) noch de eigenschap 'nestingSeparator' op Cosmos DB bron/sink in de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="e2a59-214">When using JSON editing, do not specify hello "structure" section in Cosmos DB dataset(s) nor "nestingSeparator" property on Cosmos DB source/sink in copy activity.</span></span> <span data-ttu-id="e2a59-215">tooimport van / exportbestanden tooJSON, notatietype in Hallo bestand store gegevensset opgeven als 'JsonFormat', 'filePattern' config en overslaan Hallo rest indelingsinstellingen, Zie [JSON-indeling](data-factory-supported-file-and-compression-formats.md#json-format) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e2a59-215">tooimport from/export tooJSON files, in hello file store dataset specify format type as "JsonFormat", config "filePattern" and skip hello rest format settings, see [JSON format](data-factory-supported-file-and-compression-formats.md#json-format) section on details.</span></span>

## <a name="json-examples"></a><span data-ttu-id="e2a59-216">JSON-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="e2a59-216">JSON examples</span></span>
<span data-ttu-id="e2a59-217">Hallo volgende voorbeelden geven voorbeeld JSON definities waarmee u een pijplijn toocreate kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e2a59-217">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="e2a59-218">Ze geven weer hoe toocopy gegevens tooand van Azure DB die Cosmos en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="e2a59-218">They show how toocopy data tooand from Azure Cosmos DB and Azure Blob Storage.</span></span> <span data-ttu-id="e2a59-219">Echter gegevens kunnen worden gekopieerd **rechtstreeks** vanaf elke Hallo bronnen tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="e2a59-219">However, data can be copied **directly** from any of hello sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

## <a name="example-copy-data-from-azure-cosmos-db-tooazure-blob"></a><span data-ttu-id="e2a59-220">Voorbeeld: Gegevens kopiëren van Azure DB die Cosmos tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="e2a59-220">Example: Copy data from Azure Cosmos DB tooAzure Blob</span></span>
<span data-ttu-id="e2a59-221">Hallo voorbeeld hieronder wordt:</span><span class="sxs-lookup"><span data-stu-id="e2a59-221">hello sample below shows:</span></span>

1. <span data-ttu-id="e2a59-222">Een gekoppelde service van het type [DocumentDb](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e2a59-222">A linked service of type [DocumentDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="e2a59-223">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e2a59-223">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="e2a59-224">Invoer [gegevensset](data-factory-create-datasets.md) van het type [DocumentDbCollection](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e2a59-224">An input [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="e2a59-225">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e2a59-225">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="e2a59-226">Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [DocumentDbCollectionSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="e2a59-226">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [DocumentDbCollectionSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="e2a59-227">Hallo voorbeeld kopieert de gegevens in Azure Cosmos DB tooAzure Blob.</span><span class="sxs-lookup"><span data-stu-id="e2a59-227">hello sample copies data in Azure Cosmos DB tooAzure Blob.</span></span> <span data-ttu-id="e2a59-228">Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="e2a59-228">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="e2a59-229">**Azure Cosmos DB gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="e2a59-229">**Azure Cosmos DB linked service:**</span></span>

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
<span data-ttu-id="e2a59-230">**Azure Blob-opslag gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="e2a59-230">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="e2a59-231">**Invoergegevensset van Azure Document database:**</span><span class="sxs-lookup"><span data-stu-id="e2a59-231">**Azure Document DB input dataset:**</span></span>

<span data-ttu-id="e2a59-232">Hallo-voorbeeld wordt ervan uitgegaan dat u hebt een verzameling met de naam **persoon** in een Azure DB die Cosmos-database.</span><span class="sxs-lookup"><span data-stu-id="e2a59-232">hello sample assumes you have a collection named **Person** in an Azure Cosmos DB database.</span></span>

<span data-ttu-id="e2a59-233">Instelling 'extern': 'true' en externalData geven beleidsgegevens hello Azure Data Factory-service die tabel Hallo externe toohello data factory is en niet wordt geproduceerd door een activiteit in de gegevensfactory Hallo.</span><span class="sxs-lookup"><span data-stu-id="e2a59-233">Setting “external”: ”true” and specifying externalData policy information hello Azure Data Factory service that hello table is external toohello data factory and not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="e2a59-234">**Azure Blob-uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="e2a59-234">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="e2a59-235">Gegevens zijn gekopieerde tooa nieuwe blob elk uur met Hallo pad voor Hallo blob opgetreden bij het Hallo specifieke datetime weergeven met een granulatie uur.</span><span class="sxs-lookup"><span data-stu-id="e2a59-235">Data is copied tooa new blob every hour with hello path for hello blob reflecting hello specific datetime with hour granularity.</span></span>

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
<span data-ttu-id="e2a59-236">Voorbeeld JSON-document in Hallo persoon verzameling in een Cosmos-DB-database:</span><span class="sxs-lookup"><span data-stu-id="e2a59-236">Sample JSON document in hello Person collection in a Cosmos DB database:</span></span>

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
<span data-ttu-id="e2a59-237">Cosmos DB biedt ondersteuning voor documentquery's die gebruikmaken van een SQL zoals syntaxis via hiërarchische JSON-documenten.</span><span class="sxs-lookup"><span data-stu-id="e2a59-237">Cosmos DB supports querying documents using a SQL like syntax over hierarchical JSON documents.</span></span>

<span data-ttu-id="e2a59-238">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="e2a59-238">Example:</span></span> 

```sql
SELECT Person.PersonId, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person
```

<span data-ttu-id="e2a59-239">Hallo volgende pijplijn kopieert gegevens van Hallo persoon verzameling in hello Azure Cosmos DB database tooan Azure-blob.</span><span class="sxs-lookup"><span data-stu-id="e2a59-239">hello following pipeline copies data from hello Person collection in hello Azure Cosmos DB database tooan Azure blob.</span></span> <span data-ttu-id="e2a59-240">Als onderdeel van Hallo kopie activiteit Hallo zijn invoer- en uitvoergegevenssets opgegeven.</span><span class="sxs-lookup"><span data-stu-id="e2a59-240">As part of hello copy activity hello input and output datasets have been specified.</span></span>  

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
## <a name="example-copy-data-from-azure-blob-tooazure-cosmos-db"></a><span data-ttu-id="e2a59-241">Voorbeeld: Gegevens kopiëren van Azure Blob-tooAzure Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="e2a59-241">Example: Copy data from Azure Blob tooAzure Cosmos DB</span></span> 
<span data-ttu-id="e2a59-242">Hallo voorbeeld hieronder wordt:</span><span class="sxs-lookup"><span data-stu-id="e2a59-242">hello sample below shows:</span></span>

1. <span data-ttu-id="e2a59-243">Een gekoppelde service van het type [DocumentDb](#azure-documentdb-linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e2a59-243">A linked service of type [DocumentDb](#azure-documentdb-linked-service-properties).</span></span>
2. <span data-ttu-id="e2a59-244">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="e2a59-244">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="e2a59-245">Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e2a59-245">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="e2a59-246">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span><span class="sxs-lookup"><span data-stu-id="e2a59-246">An output [dataset](data-factory-create-datasets.md) of type [DocumentDbCollection](#azure-documentdb-dataset-type-properties).</span></span>
5. <span data-ttu-id="e2a59-247">Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) en [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="e2a59-247">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).</span></span>

<span data-ttu-id="e2a59-248">Hallo voorbeeld kopieert gegevens van Azure blob-tooAzure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e2a59-248">hello sample copies data from Azure blob tooAzure Cosmos DB.</span></span> <span data-ttu-id="e2a59-249">Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="e2a59-249">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="e2a59-250">**Azure Blob-opslag gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="e2a59-250">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="e2a59-251">**Azure Cosmos DB gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="e2a59-251">**Azure Cosmos DB linked service:**</span></span>

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
<span data-ttu-id="e2a59-252">**Azure Blob invoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="e2a59-252">**Azure Blob input dataset:**</span></span>

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
<span data-ttu-id="e2a59-253">**Azure Cosmos DB uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="e2a59-253">**Azure Cosmos DB output dataset:**</span></span>

<span data-ttu-id="e2a59-254">Hallo voorbeeld kopieert tooa verzamelen van gegevens met de naam 'Persoon'.</span><span class="sxs-lookup"><span data-stu-id="e2a59-254">hello sample copies data tooa collection named “Person”.</span></span>

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
<span data-ttu-id="e2a59-255">Hallo volgende pijplijn kopieert gegevens van Azure Blob-toohello persoon verzameling in hello Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e2a59-255">hello following pipeline copies data from Azure Blob toohello Person collection in hello Cosmos DB.</span></span> <span data-ttu-id="e2a59-256">Als onderdeel van Hallo kopie activiteit Hallo zijn invoer- en uitvoergegevenssets opgegeven.</span><span class="sxs-lookup"><span data-stu-id="e2a59-256">As part of hello copy activity hello input and output datasets have been specified.</span></span>

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
              "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix, EmailPromotion: EmailPromotion, rowguid: rowguid, ModifiedDate: ModifiedDate"
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
<span data-ttu-id="e2a59-257">Als de Voorbeeldinvoer blob Hallo als</span><span class="sxs-lookup"><span data-stu-id="e2a59-257">If hello sample blob input is as</span></span>

```
1,John,,Doe
```
<span data-ttu-id="e2a59-258">Vervolgens zal Hallo uitvoer JSON in Cosmos-database zijn:</span><span class="sxs-lookup"><span data-stu-id="e2a59-258">Then hello output JSON in Cosmos DB will be as:</span></span>

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
<span data-ttu-id="e2a59-259">Azure Cosmos-database is een NoSQL-opslagplaats voor JSON-documenten, waarbij geneste structuren zijn toegestaan.</span><span class="sxs-lookup"><span data-stu-id="e2a59-259">Azure Cosmos DB is a NoSQL store for JSON documents, where nested structures are allowed.</span></span> <span data-ttu-id="e2a59-260">Azure Data Factory kunt toodenote gebruikershiërarchie via **nestingSeparator**, namelijk '. '</span><span class="sxs-lookup"><span data-stu-id="e2a59-260">Azure Data Factory enables user toodenote hierarchy via **nestingSeparator**, which is “.”</span></span> <span data-ttu-id="e2a59-261">in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="e2a59-261">in this example.</span></span> <span data-ttu-id="e2a59-262">Met Hallo scheidingsteken, genereert kopieeractiviteit Hallo Hallo "Name" object met drie onderliggende elementen eerste, middelste en laatste, volgens too"Name.First ', 'Name.Middle' en 'Name.Last' in hello tabeldefinitie.</span><span class="sxs-lookup"><span data-stu-id="e2a59-262">With hello separator, hello copy activity will generate hello “Name” object with three children elements First, Middle and Last, according too“Name.First”, “Name.Middle” and “Name.Last” in hello table definition.</span></span>

## <a name="appendix"></a><span data-ttu-id="e2a59-263">Bijlage</span><span class="sxs-lookup"><span data-stu-id="e2a59-263">Appendix</span></span>
1. <span data-ttu-id="e2a59-264">**Vraag:** Kopieeractiviteit update voor de ondersteuning van bestaande records Hallo?</span><span class="sxs-lookup"><span data-stu-id="e2a59-264">**Question:** Does hello Copy Activity support update of existing records?</span></span>

    <span data-ttu-id="e2a59-265">**Antwoord:** Nee.</span><span class="sxs-lookup"><span data-stu-id="e2a59-265">**Answer:** No.</span></span>
2. <span data-ttu-id="e2a59-266">**Vraag:** records hoe een nieuwe poging van een kopie tooAzure Cosmos DB behandelen al is gekopieerd?</span><span class="sxs-lookup"><span data-stu-id="e2a59-266">**Question:** How does a retry of a copy tooAzure Cosmos DB deal with already copied records?</span></span>

    <span data-ttu-id="e2a59-267">**Antwoord:** als records een veld 'ID hebben' en Hallo kopieerbewerking een record met Hallo tooinsert probeert dezelfde ID, de kopieerbewerking Hallo een fout genereert.</span><span class="sxs-lookup"><span data-stu-id="e2a59-267">**Answer:** If records have an "ID" field and hello copy operation tries tooinsert a record with hello same ID, hello copy operation throws an error.</span></span>  
3. <span data-ttu-id="e2a59-268">**Vraag:** biedt ondersteuning voor Data Factory [bereik of de gegevens op basis van het hash-partitionering](../documentdb/documentdb-partition-data.md)?</span><span class="sxs-lookup"><span data-stu-id="e2a59-268">**Question:** Does Data Factory support [range or hash-based data partitioning](../documentdb/documentdb-partition-data.md)?</span></span>

    <span data-ttu-id="e2a59-269">**Antwoord:** Nee.</span><span class="sxs-lookup"><span data-stu-id="e2a59-269">**Answer:** No.</span></span>
4. <span data-ttu-id="e2a59-270">**Vraag:** kan ik meer dan één Azure Cosmos DB verzameling voor een tabel opgeven?</span><span class="sxs-lookup"><span data-stu-id="e2a59-270">**Question:** Can I specify more than one Azure Cosmos DB collection for a table?</span></span>

    <span data-ttu-id="e2a59-271">**Antwoord:** Nee.</span><span class="sxs-lookup"><span data-stu-id="e2a59-271">**Answer:** No.</span></span> <span data-ttu-id="e2a59-272">Slechts één verzameling kan op dit moment worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="e2a59-272">Only one collection can be specified at this time.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="e2a59-273">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="e2a59-273">Performance and Tuning</span></span>
<span data-ttu-id="e2a59-274">Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.</span><span class="sxs-lookup"><span data-stu-id="e2a59-274">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
