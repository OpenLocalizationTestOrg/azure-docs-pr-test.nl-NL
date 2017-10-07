---
title: aaaMove gegevens van/naar Azure Table | Microsoft Docs
description: Meer informatie over hoe toomove gegevens van/naar Azure Table Storage met Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 07b046b1-7884-4e57-a613-337292416319
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 3dc3da6d88854674a9108b600534bc5d07575f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-table-using-azure-data-factory"></a><span data-ttu-id="e2aa3-103">Verplaatsen van gegevens tooand van Azure-tabel met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="e2aa3-103">Move data tooand from Azure Table using Azure Data Factory</span></span>
<span data-ttu-id="e2aa3-104">Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit Hallo in Azure Data Factory toomove gegevens uit Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from Azure Table Storage.</span></span> <span data-ttu-id="e2aa3-105">Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

<span data-ttu-id="e2aa3-106">U kunt gegevens kopiëren van een ondersteunde bron gegevens opslaan tooAzure Table Storage of Azure Table Storage tooany ondersteund sink gegevens opslaan.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-106">You can copy data from any supported source data store tooAzure Table Storage or from Azure Table Storage tooany supported sink data store.</span></span> <span data-ttu-id="e2aa3-107">Zie voor een lijst van gegevensarchieven als bronnen of PUT wordt ondersteund door kopieeractiviteit Hallo Hallo [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-107">For a list of data stores supported as sources or sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="e2aa3-108">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="e2aa3-108">Getting started</span></span>
<span data-ttu-id="e2aa3-109">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens uit een Azure-tabelopslag verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-109">You can create a pipeline with a copy activity that moves data to/from an Azure Table Storage by using different tools/APIs.</span></span>

<span data-ttu-id="e2aa3-110">Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-110">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="e2aa3-111">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-111">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="e2aa3-112">U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-112">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="e2aa3-113">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-113">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="e2aa3-114">Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="e2aa3-114">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="e2aa3-115">Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-115">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="e2aa3-116">Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-116">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="e2aa3-117">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-117">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="e2aa3-118">Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-118">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="e2aa3-119">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-119">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="e2aa3-120">Zie voor voorbeelden met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens van/naar een Azure-tabelopslag zijn [JSON voorbeelden](#json-examples) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-120">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure Table Storage, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="e2aa3-121">Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooAzure Table Storage zijn:</span><span class="sxs-lookup"><span data-stu-id="e2aa3-121">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure Table Storage:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="e2aa3-122">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="e2aa3-122">Linked service properties</span></span>
<span data-ttu-id="e2aa3-123">Er zijn twee typen van de gekoppelde services kunt u een Azure blob storage tooan Azure data factory toolink.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-123">There are two types of linked services you can use toolink an Azure blob storage tooan Azure data factory.</span></span> <span data-ttu-id="e2aa3-124">Ze zijn: **AzureStorage** gekoppelde service en **AzureStorageSas** gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-124">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="e2aa3-125">Hallo gekoppelde Azure Storage-service biedt Hallo data factory met globale toegang toohello Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-125">hello Azure Storage linked service provides hello data factory with global access toohello Azure Storage.</span></span> <span data-ttu-id="e2aa3-126">Terwijl hello Azure Storage SAS (Shared Access Signature) gekoppelde biedt service Hallo gegevensfactory met de toegang beperkt/tijdsgebonden toohello Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-126">Whereas, hello Azure Storage SAS (Shared Access Signature) linked service provides hello data factory with restricted/time-bound access toohello Azure Storage.</span></span> <span data-ttu-id="e2aa3-127">Er zijn geen andere verschillen tussen deze twee gekoppelde services.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-127">There are no other differences between these two linked services.</span></span> <span data-ttu-id="e2aa3-128">Kies Hallo gekoppelde service die bij uw behoeften past.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-128">Choose hello linked service that suits your needs.</span></span> <span data-ttu-id="e2aa3-129">Hallo vindt volgende secties u meer informatie over deze twee gekoppelde services.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-129">hello following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="e2aa3-130">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="e2aa3-130">Dataset properties</span></span>
<span data-ttu-id="e2aa3-131">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-131">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="e2aa3-132">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).</span><span class="sxs-lookup"><span data-stu-id="e2aa3-132">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="e2aa3-133">Hallo typeProperties sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-133">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="e2aa3-134">Hallo **typeProperties** sectie voor Hallo gegevensset van het type **AzureTable** Hallo volgende eigenschappen heeft.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-134">hello **typeProperties** section for hello dataset of type **AzureTable** has hello following properties.</span></span>

| <span data-ttu-id="e2aa3-135">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="e2aa3-135">Property</span></span> | <span data-ttu-id="e2aa3-136">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e2aa3-136">Description</span></span> | <span data-ttu-id="e2aa3-137">Vereist</span><span class="sxs-lookup"><span data-stu-id="e2aa3-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e2aa3-138">tableName</span><span class="sxs-lookup"><span data-stu-id="e2aa3-138">tableName</span></span> |<span data-ttu-id="e2aa3-139">De naam van de tabel Hallo in hello Azure Table-Database-instantie waarnaar de gekoppelde service verwijst.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-139">Name of hello table in hello Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="e2aa3-140">Ja.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-140">Yes.</span></span> <span data-ttu-id="e2aa3-141">Wanneer een tabelnaam is opgegeven zonder een azureTableSourceQuery, worden alle records uit de tabel Hallo gekopieerde toohello bestemming.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-141">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="e2aa3-142">Als een azureTableSourceQuery ook is opgegeven, worden records uit de tabel Hallo die voldoet aan de query Hallo gekopieerde toohello bestemming.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-142">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |

### <a name="schema-by-data-factory"></a><span data-ttu-id="e2aa3-143">Schema door Data Factory</span><span class="sxs-lookup"><span data-stu-id="e2aa3-143">Schema by Data Factory</span></span>
<span data-ttu-id="e2aa3-144">Voor gegevens zonder schema winkels zoals Azure Table afleidt Hallo Data Factory-service Hallo schema in een van de volgende manieren Hallo:</span><span class="sxs-lookup"><span data-stu-id="e2aa3-144">For schema-free data stores such as Azure Table, hello Data Factory service infers hello schema in one of hello following ways:</span></span>

1. <span data-ttu-id="e2aa3-145">Als u Hallo-structuur van gegevens opgeeft met behulp van Hallo **structuur** eigenschap in de gegevenssetdefinitie hello, Hallo Data Factory-service zich houdt aan deze structuur als Hallo schema.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-145">If you specify hello structure of data by using hello **structure** property in hello dataset definition, hello Data Factory service honors this structure as hello schema.</span></span> <span data-ttu-id="e2aa3-146">Als een rij geen waarde voor een kolom bevat, wordt in dit geval een null-waarde opgegeven voor deze.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-146">In this case, if a row does not contain a value for a column, a null value is provided for it.</span></span>
2. <span data-ttu-id="e2aa3-147">Als u geen Hallo-structuur van gegevens opgeeft met behulp van Hallo **structuur** eigenschap in de gegevenssetdefinitie hello, Data Factory Hallo schema afleidt met behulp van de eerste rij Hallo in Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-147">If you don't specify hello structure of data by using hello **structure** property in hello dataset definition, Data Factory infers hello schema by using hello first row in hello data.</span></span> <span data-ttu-id="e2aa3-148">Als de eerste rij Hallo bevat geen volledige schema hello, worden sommige kolommen in dit geval gemist in Hallo resultaat van de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-148">In this case, if hello first row does not contain hello full schema, some columns are missed in hello result of copy operation.</span></span>

<span data-ttu-id="e2aa3-149">Voor gegevensbronnen zonder schema, Hallo aanbevolen procedure is daarom toospecify Hallo structuur van gegevens met behulp van Hallo **structuur** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-149">Therefore, for schema-free data sources, hello best practice is toospecify hello structure of data using hello **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="e2aa3-150">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="e2aa3-150">Copy activity properties</span></span>
<span data-ttu-id="e2aa3-151">Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-151">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="e2aa3-152">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer gegevenssets en beleidsregels zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-152">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span>

<span data-ttu-id="e2aa3-153">Eigenschappen beschikbaar zijn in Hallo typeProperties sectie Hallo-activiteit op Hallo daarentegen variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-153">Properties available in hello typeProperties section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="e2aa3-154">Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-154">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="e2aa3-155">**AzureTableSource** ondersteunt de volgende eigenschappen in de sectie typeProperties Hallo:</span><span class="sxs-lookup"><span data-stu-id="e2aa3-155">**AzureTableSource** supports hello following properties in typeProperties section:</span></span>

| <span data-ttu-id="e2aa3-156">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="e2aa3-156">Property</span></span> | <span data-ttu-id="e2aa3-157">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e2aa3-157">Description</span></span> | <span data-ttu-id="e2aa3-158">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="e2aa3-158">Allowed values</span></span> | <span data-ttu-id="e2aa3-159">Vereist</span><span class="sxs-lookup"><span data-stu-id="e2aa3-159">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e2aa3-160">azureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="e2aa3-160">azureTableSourceQuery</span></span> |<span data-ttu-id="e2aa3-161">Hallo aangepaste query tooread gegevens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-161">Use hello custom query tooread data.</span></span> |<span data-ttu-id="e2aa3-162">Azure-tabel queryreeks.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-162">Azure table query string.</span></span> <span data-ttu-id="e2aa3-163">Zie de voorbeelden in de volgende sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-163">See examples in hello next section.</span></span> |<span data-ttu-id="e2aa3-164">Nee.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-164">No.</span></span> <span data-ttu-id="e2aa3-165">Wanneer een tabelnaam is opgegeven zonder een azureTableSourceQuery, worden alle records uit de tabel Hallo gekopieerde toohello bestemming.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-165">When a tableName is specified without an azureTableSourceQuery, all records from hello table are copied toohello destination.</span></span> <span data-ttu-id="e2aa3-166">Als een azureTableSourceQuery ook is opgegeven, worden records uit de tabel Hallo die voldoet aan de query Hallo gekopieerde toohello bestemming.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-166">If an azureTableSourceQuery is also specified, records from hello table that satisfies hello query are copied toohello destination.</span></span> |
| <span data-ttu-id="e2aa3-167">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="e2aa3-167">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="e2aa3-168">Geef aan of slikken Hallo uitzondering van de tabel niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-168">Indicate whether swallow hello exception of table not exist.</span></span> |<span data-ttu-id="e2aa3-169">DE WAARDE TRUE</span><span class="sxs-lookup"><span data-stu-id="e2aa3-169">TRUE</span></span><br/><span data-ttu-id="e2aa3-170">DE WAARDE FALSE</span><span class="sxs-lookup"><span data-stu-id="e2aa3-170">FALSE</span></span> |<span data-ttu-id="e2aa3-171">Nee</span><span class="sxs-lookup"><span data-stu-id="e2aa3-171">No</span></span> |

### <a name="azuretablesourcequery-examples"></a><span data-ttu-id="e2aa3-172">Voorbeelden van azureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="e2aa3-172">azureTableSourceQuery examples</span></span>
<span data-ttu-id="e2aa3-173">Als Azure Table-kolom van het tekenreekstype:</span><span class="sxs-lookup"><span data-stu-id="e2aa3-173">If Azure Table column is of string type:</span></span>

```JSON
azureTableSourceQuery": "$$Text.Format('PartitionKey ge \\'{0:yyyyMMddHH00_0000}\\' and PartitionKey le \\'{0:yyyyMMddHH00_9999}\\'', SliceStart)"
```

<span data-ttu-id="e2aa3-174">Als Azure Table-kolom van het type datetime:</span><span class="sxs-lookup"><span data-stu-id="e2aa3-174">If Azure Table column is of datetime type:</span></span>

```JSON
"azureTableSourceQuery": "$$Text.Format('DeploymentEndTime gt datetime\\'{0:yyyy-MM-ddTHH:mm:ssZ}\\' and DeploymentEndTime le datetime\\'{1:yyyy-MM-ddTHH:mm:ssZ}\\'', SliceStart, SliceEnd)"
```

<span data-ttu-id="e2aa3-175">**AzureTableSink** ondersteunt de volgende eigenschappen in de sectie typeProperties Hallo:</span><span class="sxs-lookup"><span data-stu-id="e2aa3-175">**AzureTableSink** supports hello following properties in typeProperties section:</span></span>

| <span data-ttu-id="e2aa3-176">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="e2aa3-176">Property</span></span> | <span data-ttu-id="e2aa3-177">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="e2aa3-177">Description</span></span> | <span data-ttu-id="e2aa3-178">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="e2aa3-178">Allowed values</span></span> | <span data-ttu-id="e2aa3-179">Vereist</span><span class="sxs-lookup"><span data-stu-id="e2aa3-179">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e2aa3-180">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="e2aa3-180">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="e2aa3-181">Standaardwaarde voor de partitiesleutel die kan worden gebruikt door Hallo sink.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-181">Default partition key value that can be used by hello sink.</span></span> |<span data-ttu-id="e2aa3-182">Een string-waarde.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-182">A string value.</span></span> |<span data-ttu-id="e2aa3-183">Nee</span><span class="sxs-lookup"><span data-stu-id="e2aa3-183">No</span></span> |
| <span data-ttu-id="e2aa3-184">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="e2aa3-184">azureTablePartitionKeyName</span></span> |<span data-ttu-id="e2aa3-185">Naam van het Hallo-kolom waarvan de waarden worden gebruikt als partitiesleutels opgeven.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-185">Specify name of hello column whose values are used as partition keys.</span></span> <span data-ttu-id="e2aa3-186">Als niet wordt opgegeven, wordt AzureTableDefaultPartitionKeyValue gebruikt als partitiesleutel Hallo.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-186">If not specified, AzureTableDefaultPartitionKeyValue is used as hello partition key.</span></span> |<span data-ttu-id="e2aa3-187">De naam van een kolom.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-187">A column name.</span></span> |<span data-ttu-id="e2aa3-188">Nee</span><span class="sxs-lookup"><span data-stu-id="e2aa3-188">No</span></span> |
| <span data-ttu-id="e2aa3-189">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="e2aa3-189">azureTableRowKeyName</span></span> |<span data-ttu-id="e2aa3-190">Naam van het Hallo-kolom waarvan de kolomwaarden worden gebruikt als de rijsleutel opgeven.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-190">Specify name of hello column whose column values are used as row key.</span></span> <span data-ttu-id="e2aa3-191">Als niet wordt opgegeven, gebruikt u een GUID voor elke rij.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-191">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="e2aa3-192">De naam van een kolom.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-192">A column name.</span></span> |<span data-ttu-id="e2aa3-193">Nee</span><span class="sxs-lookup"><span data-stu-id="e2aa3-193">No</span></span> |
| <span data-ttu-id="e2aa3-194">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="e2aa3-194">azureTableInsertType</span></span> |<span data-ttu-id="e2aa3-195">Hallo modus tooinsert gegevens in Azure-tabel.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-195">hello mode tooinsert data into Azure table.</span></span><br/><br/><span data-ttu-id="e2aa3-196">Deze eigenschap bepaalt of bestaande rijen in de uitvoertabel Hallo met partitie-als rijsleutels die overeenkomt met de waarden vervangen of samenvoegen van hebben.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-196">This property controls whether existing rows in hello output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="e2aa3-197">toolearn over hoe deze instellingen (merge en vervangen) werken, Zie [invoegen of Merge entiteit](https://msdn.microsoft.com/library/azure/hh452241.aspx) en [invoegen of vervangen entiteit](https://msdn.microsoft.com/library/azure/hh452242.aspx) onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-197">toolearn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="e2aa3-198">Deze instelling is van toepassing op Hallo rijniveau niet Hallo-tabelniveau, en geen van beide optie worden de rijen in de uitvoertabel Hallo die niet bestaan in de invoer Hallo verwijderd.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-198">This setting applies at hello row level, not hello table level, and neither option deletes rows in hello output table that do not exist in hello input.</span></span> |<span data-ttu-id="e2aa3-199">samenvoegen (standaard)</span><span class="sxs-lookup"><span data-stu-id="e2aa3-199">merge (default)</span></span><br/><span data-ttu-id="e2aa3-200">vervangen</span><span class="sxs-lookup"><span data-stu-id="e2aa3-200">replace</span></span> |<span data-ttu-id="e2aa3-201">Nee</span><span class="sxs-lookup"><span data-stu-id="e2aa3-201">No</span></span> |
| <span data-ttu-id="e2aa3-202">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="e2aa3-202">writeBatchSize</span></span> |<span data-ttu-id="e2aa3-203">Voegt de gegevens in hello Azure-tabel wanneer Hallo writeBatchSize of writeBatchTimeout is bereikt.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-203">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="e2aa3-204">Geheel getal (aantal rijen)</span><span class="sxs-lookup"><span data-stu-id="e2aa3-204">Integer (number of rows)</span></span> |<span data-ttu-id="e2aa3-205">Nee (standaard: 10000)</span><span class="sxs-lookup"><span data-stu-id="e2aa3-205">No (default: 10000)</span></span> |
| <span data-ttu-id="e2aa3-206">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="e2aa3-206">writeBatchTimeout</span></span> |<span data-ttu-id="e2aa3-207">Voegt de gegevens in hello Azure-tabel wanneer Hallo writeBatchSize of writeBatchTimeout is bereikt.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-207">Inserts data into hello Azure table when hello writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="e2aa3-208">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="e2aa3-208">timespan</span></span><br/><br/><span data-ttu-id="e2aa3-209">Voorbeeld: "00: 20:00 ' (20 minuten)</span><span class="sxs-lookup"><span data-stu-id="e2aa3-209">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="e2aa3-210">Nee (standaard toostorage client standaardtime-out waarde 90 sec)</span><span class="sxs-lookup"><span data-stu-id="e2aa3-210">No (Default toostorage client default timeout value 90 sec)</span></span> |

### <a name="azuretablepartitionkeyname"></a><span data-ttu-id="e2aa3-211">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="e2aa3-211">azureTablePartitionKeyName</span></span>
<span data-ttu-id="e2aa3-212">Een kolom tooa bestemming bronkolom met Hallo conversieprogramma JSON eigenschap voordat u de doelkolom Hallo kunt zoals Hallo azureTablePartitionKeyName worden toegewezen.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-212">Map a source column tooa destination column using hello translator JSON property before you can use hello destination column as hello azureTablePartitionKeyName.</span></span>

<span data-ttu-id="e2aa3-213">In de Hallo voorbeeld te volgen, bronkolom DivisionID is toegewezen toohello doelkolom: DivisionID.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-213">In hello following example, source column DivisionID is mapped toohello destination column: DivisionID.</span></span>  

```JSON
"translator": {
    "type": "TabularTranslator",
    "columnMappings": "DivisionID: DivisionID, FirstName: FirstName, LastName: LastName"
}
```
<span data-ttu-id="e2aa3-214">Hallo DivisionID is opgegeven als partitiesleutel Hallo.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-214">hello DivisionID is specified as hello partition key.</span></span>

```JSON
"sink": {
    "type": "AzureTableSink",
    "azureTablePartitionKeyName": "DivisionID",
    "writeBatchSize": 100,
    "writeBatchTimeout": "01:00:00"
}
```
## <a name="json-examples"></a><span data-ttu-id="e2aa3-215">JSON-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="e2aa3-215">JSON examples</span></span>
<span data-ttu-id="e2aa3-216">Hallo volgende voorbeelden geven voorbeeld JSON definities waarmee u een pijplijn toocreate kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="e2aa3-216">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="e2aa3-217">Ze geven weer hoe toocopy gegevens tooand van Azure Table Storage en Azure Blob-Database.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-217">They show how toocopy data tooand from Azure Table Storage and Azure Blob Database.</span></span> <span data-ttu-id="e2aa3-218">Echter, de gegevens kunnen worden gekopieerd **rechtstreeks** vanaf elke Hallo bronnen tooany van Hallo ondersteund Put.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-218">However, data can be copied **directly** from any of hello sources tooany of hello supported sinks.</span></span> <span data-ttu-id="e2aa3-219">Zie voor meer informatie Hallo sectie 'ondersteunde gegevensarchieven en indelingen' in [verplaatsen van gegevens met behulp van de Kopieeractiviteit](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="e2aa3-219">For more information, see hello section "Supported data stores and formats" in [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>

## <a name="example-copy-data-from-azure-table-tooazure-blob"></a><span data-ttu-id="e2aa3-220">Voorbeeld: Gegevens kopiëren van Azure Table tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="e2aa3-220">Example: Copy data from Azure Table tooAzure Blob</span></span>
<span data-ttu-id="e2aa3-221">Hallo volgende ziet:</span><span class="sxs-lookup"><span data-stu-id="e2aa3-221">hello following sample shows:</span></span>

1. <span data-ttu-id="e2aa3-222">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (gebruikt voor blob & tabel).</span><span class="sxs-lookup"><span data-stu-id="e2aa3-222">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob).</span></span>
2. <span data-ttu-id="e2aa3-223">Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e2aa3-223">An input [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
3. <span data-ttu-id="e2aa3-224">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e2aa3-224">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="e2aa3-225">Hallo [pijplijn](data-factory-create-pipelines.md) met de kopieeractiviteit die gebruikmaakt van [AzureTableSource](#activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="e2aa3-225">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [AzureTableSource](#activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="e2aa3-226">Hallo voorbeeld kopieert de gegevens die behoren toohello standaardpartitie in een blob van Azure Table tooa elk uur.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-226">hello sample copies data belonging toohello default partition in an Azure Table tooa blob every hour.</span></span> <span data-ttu-id="e2aa3-227">Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-227">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="e2aa3-228">**Gekoppelde Azure storage-service:**</span><span class="sxs-lookup"><span data-stu-id="e2aa3-228">**Azure storage linked service:**</span></span>

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
<span data-ttu-id="e2aa3-229">Azure Data Factory ondersteunt twee soorten gekoppelde Azure Storage-services: **AzureStorage** en **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-229">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="e2aa3-230">Hallo voor eerste, u Hallo verbindingsreeks met Hallo accountsleutel opgeven en voor latere Hallo, u Hallo Shared Access Signature (SAS)-Uri opgeven.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-230">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="e2aa3-231">Zie [gekoppelde Services](#linked-service-properties) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-231">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="e2aa3-232">**Azure Table invoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="e2aa3-232">**Azure Table input dataset:**</span></span>

<span data-ttu-id="e2aa3-233">Hallo-voorbeeld wordt ervan uitgegaan dat u een tabel "MijnTabel" hebt gemaakt in Azure-tabel.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-233">hello sample assumes you have created a table “MyTable” in Azure Table.</span></span>

<span data-ttu-id="e2aa3-234">Instelling 'extern': 'true' informeert Hallo Data Factory-service die gegevensset Hallo externe toohello data factory is en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-234">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureTableInput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

<span data-ttu-id="e2aa3-235">**Azure Blob-uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="e2aa3-235">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="e2aa3-236">Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="e2aa3-236">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="e2aa3-237">pad naar map voor blob Hallo Hallo wordt dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-237">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="e2aa3-238">Hallo mappad jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-238">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="e2aa3-239">**De kopieeractiviteit in een pijplijn met AzureTableSource en BlobSink:**</span><span class="sxs-lookup"><span data-stu-id="e2aa3-239">**Copy activity in a pipeline with AzureTableSource and BlobSink:**</span></span>

<span data-ttu-id="e2aa3-240">Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-240">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="e2aa3-241">Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**AzureTableSource** en **sink** type is ingesteld, te**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-241">In hello pipeline JSON definition, hello **source** type is set too**AzureTableSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="e2aa3-242">Hallo SQL-query is opgegeven met **AzureTableSourceQuery** eigenschap selecteert Hallo gegevens uit Hallo standaardpartitie elke toocopy uur.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-242">hello SQL query specified with **AzureTableSourceQuery** property selects hello data from hello default partition every hour toocopy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "AzureTabletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                      {
                        "name": "AzureTableInput"
                    }
                ],
                "outputs": [
                      {
                            "name": "AzureBlobOutput"
                      }
                ],
                "typeProperties": {
                      "source": {
                        "type": "AzureTableSource",
                        "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
                      },
                      "sink": {
                        "type": "BlobSink"
                      }
                },
                "scheduler": {
                      "frequency": "Hour",
                      "interval": 1
                },                
                "policy": {
                      "concurrency": 1,
                      "executionPriorityOrder": "OldestFirst",
                      "retry": 0,
                      "timeout": "01:00:00"
                }
            }
         ]    
    }
}
```

## <a name="example-copy-data-from-azure-blob-tooazure-table"></a><span data-ttu-id="e2aa3-243">Voorbeeld: Gegevens kopiëren van Azure Blob-tooAzure tabel</span><span class="sxs-lookup"><span data-stu-id="e2aa3-243">Example: Copy data from Azure Blob tooAzure Table</span></span>
<span data-ttu-id="e2aa3-244">Hallo volgende ziet:</span><span class="sxs-lookup"><span data-stu-id="e2aa3-244">hello following sample shows:</span></span>

1. <span data-ttu-id="e2aa3-245">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (gebruikt voor blob & tabel)</span><span class="sxs-lookup"><span data-stu-id="e2aa3-245">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob)</span></span>
2. <span data-ttu-id="e2aa3-246">Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e2aa3-246">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="e2aa3-247">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="e2aa3-247">An output [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
4. <span data-ttu-id="e2aa3-248">Hallo [pijplijn](data-factory-create-pipelines.md) met de kopieeractiviteit die gebruikmaakt van [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) en [AzureTableSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="e2aa3-248">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureTableSink](#copy-activity-properties).</span></span>

<span data-ttu-id="e2aa3-249">Hallo voorbeeld kopieert timeseries gegevens van een Azure blob-tooan Azure-tabel per uur.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-249">hello sample copies time-series data from an Azure blob tooan Azure table hourly.</span></span> <span data-ttu-id="e2aa3-250">Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-250">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="e2aa3-251">**Gekoppelde Azure storage (voor Azure Table & Blob)-service:**</span><span class="sxs-lookup"><span data-stu-id="e2aa3-251">**Azure storage (for both Azure Table & Blob) linked service:**</span></span>

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

<span data-ttu-id="e2aa3-252">Azure Data Factory ondersteunt twee soorten gekoppelde Azure Storage-services: **AzureStorage** en **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-252">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="e2aa3-253">Hallo voor eerste, u Hallo verbindingsreeks met Hallo accountsleutel opgeven en voor latere Hallo, u Hallo Shared Access Signature (SAS)-Uri opgeven.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-253">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="e2aa3-254">Zie [gekoppelde Services](#linked-service-properties) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-254">See [Linked Services](#linked-service-properties) section for details.</span></span>

<span data-ttu-id="e2aa3-255">**Azure Blob invoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="e2aa3-255">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="e2aa3-256">Gegevens wordt opgehaald uit een nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="e2aa3-256">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="e2aa3-257">Hallo map pad en de naam voor de blob Hallo worden dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-257">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="e2aa3-258">Hallo mappad jaar, maand en dag deel uit van de begintijd Hallo en bestandsnaam gebruikt Hallo uur deel uit van de begintijd Hallo.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-258">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="e2aa3-259">"extern": "true" instelling informeert Hallo Data Factory-service die gegevensset Hallo externe toohello data factory is en niet wordt geproduceerd door een activiteit in de gegevensfactory Hallo.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-259">“external”: “true” setting informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

<span data-ttu-id="e2aa3-260">**Azure-tabel uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="e2aa3-260">**Azure Table output dataset:**</span></span>

<span data-ttu-id="e2aa3-261">Hallo voorbeeld kopieert gegevens tooa tabel "MijnTabel" in de Azure-tabel.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-261">hello sample copies data tooa table named “MyTable” in Azure Table.</span></span> <span data-ttu-id="e2aa3-262">Maken van een Azure-tabel met hetzelfde aantal kolommen Hallo zoals Hallo Blob CSV-bestand toocontain verwacht.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-262">Create an Azure table with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="e2aa3-263">Nieuwe rijen worden toohello tabel toegevoegd om het uur.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-263">New rows are added toohello table every hour.</span></span>

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="e2aa3-264">**De kopieeractiviteit in een pijplijn met BlobSource en AzureTableSink:**</span><span class="sxs-lookup"><span data-stu-id="e2aa3-264">**Copy activity in a pipeline with BlobSource and AzureTableSink:**</span></span>

<span data-ttu-id="e2aa3-265">Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-265">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="e2aa3-266">Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**BlobSource** en **sink** type is ingesteld, te**AzureTableSink**.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-266">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**AzureTableSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoTable",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureTableOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "AzureTableSink",
            "writeBatchSize": 100,
            "writeBatchTimeout": "01:00:00"
          }
        },
        "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },                        
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```
## <a name="type-mapping-for-azure-table"></a><span data-ttu-id="e2aa3-267">Toewijzing van het type voor Azure-tabel</span><span class="sxs-lookup"><span data-stu-id="e2aa3-267">Type Mapping for Azure Table</span></span>
<span data-ttu-id="e2aa3-268">Zoals vermeld in Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel kopieeractiviteit voert automatische typeconversies van brontypen typen toosink Hello benadering in twee stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-268">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach.</span></span>

1. <span data-ttu-id="e2aa3-269">Systeemeigen bron typen too.NET type converteren</span><span class="sxs-lookup"><span data-stu-id="e2aa3-269">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="e2aa3-270">Converteren van .NET-type toonative sink-type</span><span class="sxs-lookup"><span data-stu-id="e2aa3-270">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="e2aa3-271">Bij het verplaatsen van gegevens te & van Azure Table Hallo na [toewijzingen die zijn gedefinieerd door de service Azure Table](https://msdn.microsoft.com/library/azure/dd179338.aspx) worden gebruikt vanuit Azure tabel OData typen too.NET type en vice versa.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-271">When moving data too& from Azure Table, hello following [mappings defined by Azure Table service](https://msdn.microsoft.com/library/azure/dd179338.aspx) are used from Azure Table OData types too.NET type and vice versa.</span></span>

| <span data-ttu-id="e2aa3-272">OData-gegevenstype</span><span class="sxs-lookup"><span data-stu-id="e2aa3-272">OData Data Type</span></span> | <span data-ttu-id="e2aa3-273">.NET-type</span><span class="sxs-lookup"><span data-stu-id="e2aa3-273">.NET Type</span></span> | <span data-ttu-id="e2aa3-274">Details</span><span class="sxs-lookup"><span data-stu-id="e2aa3-274">Details</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e2aa3-275">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="e2aa3-275">Edm.Binary</span></span> |<span data-ttu-id="e2aa3-276">Byte]</span><span class="sxs-lookup"><span data-stu-id="e2aa3-276">byte[]</span></span> |<span data-ttu-id="e2aa3-277">Een matrix met bytes up too64 KB.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-277">An array of bytes up too64 KB.</span></span> |
| <span data-ttu-id="e2aa3-278">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="e2aa3-278">Edm.Boolean</span></span> |<span data-ttu-id="e2aa3-279">BOOL</span><span class="sxs-lookup"><span data-stu-id="e2aa3-279">bool</span></span> |<span data-ttu-id="e2aa3-280">Een Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-280">A Boolean value.</span></span> |
| <span data-ttu-id="e2aa3-281">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="e2aa3-281">Edm.DateTime</span></span> |<span data-ttu-id="e2aa3-282">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="e2aa3-282">DateTime</span></span> |<span data-ttu-id="e2aa3-283">Een 64-bits waarde wordt uitgedrukt als Coordinated Universal Time (UTC).</span><span class="sxs-lookup"><span data-stu-id="e2aa3-283">A 64-bit value expressed as Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="e2aa3-284">Hallo ondersteund DateTime bereik van 12:00 middernacht, 1 januari 1601 A.D. begint</span><span class="sxs-lookup"><span data-stu-id="e2aa3-284">hello supported DateTime range begins from 12:00 midnight, January 1, 1601 A.D.</span></span> <span data-ttu-id="e2aa3-285">(C.E.) UTC.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-285">(C.E.), UTC.</span></span> <span data-ttu-id="e2aa3-286">Hallo bereik eindigt op 31 December 9999.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-286">hello range ends at December 31, 9999.</span></span> |
| <span data-ttu-id="e2aa3-287">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="e2aa3-287">Edm.Double</span></span> |<span data-ttu-id="e2aa3-288">dubbele</span><span class="sxs-lookup"><span data-stu-id="e2aa3-288">double</span></span> |<span data-ttu-id="e2aa3-289">Een 64-bits drijvende-kommawaarde.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-289">A 64-bit floating point value.</span></span> |
| <span data-ttu-id="e2aa3-290">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="e2aa3-290">Edm.Guid</span></span> |<span data-ttu-id="e2aa3-291">GUID</span><span class="sxs-lookup"><span data-stu-id="e2aa3-291">Guid</span></span> |<span data-ttu-id="e2aa3-292">Een globally unique identifier van 128-bits.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-292">A 128-bit globally unique identifier.</span></span> |
| <span data-ttu-id="e2aa3-293">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="e2aa3-293">Edm.Int32</span></span> |<span data-ttu-id="e2aa3-294">Int32</span><span class="sxs-lookup"><span data-stu-id="e2aa3-294">Int32</span></span> |<span data-ttu-id="e2aa3-295">Een 32-bits geheel getal.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-295">A 32-bit integer.</span></span> |
| <span data-ttu-id="e2aa3-296">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="e2aa3-296">Edm.Int64</span></span> |<span data-ttu-id="e2aa3-297">Int64</span><span class="sxs-lookup"><span data-stu-id="e2aa3-297">Int64</span></span> |<span data-ttu-id="e2aa3-298">Een 64-bits geheel getal.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-298">A 64-bit integer.</span></span> |
| <span data-ttu-id="e2aa3-299">Edm.String</span><span class="sxs-lookup"><span data-stu-id="e2aa3-299">Edm.String</span></span> |<span data-ttu-id="e2aa3-300">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="e2aa3-300">String</span></span> |<span data-ttu-id="e2aa3-301">Een waarde UTF-16-codering.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-301">A UTF-16-encoded value.</span></span> <span data-ttu-id="e2aa3-302">Tekenreekswaarden mogelijk up too64 KB.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-302">String values may be up too64 KB.</span></span> |

### <a name="type-conversion-sample"></a><span data-ttu-id="e2aa3-303">Type conversie voorbeeld</span><span class="sxs-lookup"><span data-stu-id="e2aa3-303">Type Conversion Sample</span></span>
<span data-ttu-id="e2aa3-304">Hallo volgende voorbeeld is voor het kopiëren van gegevens uit een Azure Blob-tooAzure tabel met typeconversies.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-304">hello following sample is for copying data from an Azure Blob tooAzure Table with type conversions.</span></span>

<span data-ttu-id="e2aa3-305">Stel Hallo Blob-gegevenssets is CSV-indeling en drie kolommen bevat.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-305">Suppose hello Blob dataset is in CSV format and contains three columns.</span></span> <span data-ttu-id="e2aa3-306">Een van deze is een datetime-kolom met een aangepaste datum / tijdindeling met behulp van Franse afkortingen voor dag van week Hallo.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-306">One of them is a datetime column with a custom datetime format using abbreviated French names for day of hello week.</span></span>

<span data-ttu-id="e2aa3-307">Bron van de Blob-gegevensset Hallo als volgt samen met de definities voor Hallo kolommen definiëren.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-307">Define hello Blob Source dataset as follows along with type definitions for hello columns.</span></span>

```JSON
{
    "name": " AzureBlobInput",
    "properties":
    {
         "structure":
          [
                { "name": "userid", "type": "Int64"},
                { "name": "name", "type": "String"},
                { "name": "lastlogindate", "type": "Datetime", "culture": "fr-fr", "format": "ddd-MM-YYYY"}
          ],
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder",
            "fileName":"myfile.csv",
            "format":
            {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "external": true,
        "availability":
        {
            "frequency": "Hour",
            "interval": 1,
        },
        "policy": {
            "externalData": {
                "retryInterval": "00:01:00",
                "retryTimeout": "00:10:00",
                "maximumRetry": 3
            }
        }
    }
}
```
<span data-ttu-id="e2aa3-308">Toewijzing van het type Hallo van Azure Table OData type too.NET type gezien, zou u Hallo tabel definiëren in Azure Table Hello schema te volgen.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-308">Given hello type mapping from Azure Table OData type too.NET type, you would define hello table in Azure Table with hello following schema.</span></span>

<span data-ttu-id="e2aa3-309">**Azure tabelschema:**</span><span class="sxs-lookup"><span data-stu-id="e2aa3-309">**Azure Table schema:**</span></span>

| <span data-ttu-id="e2aa3-310">Kolomnaam</span><span class="sxs-lookup"><span data-stu-id="e2aa3-310">Column name</span></span> | <span data-ttu-id="e2aa3-311">Type</span><span class="sxs-lookup"><span data-stu-id="e2aa3-311">Type</span></span> |
| --- | --- |
| <span data-ttu-id="e2aa3-312">gebruikers-id</span><span class="sxs-lookup"><span data-stu-id="e2aa3-312">userid</span></span> |<span data-ttu-id="e2aa3-313">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="e2aa3-313">Edm.Int64</span></span> |
| <span data-ttu-id="e2aa3-314">naam</span><span class="sxs-lookup"><span data-stu-id="e2aa3-314">name</span></span> |<span data-ttu-id="e2aa3-315">Edm.String</span><span class="sxs-lookup"><span data-stu-id="e2aa3-315">Edm.String</span></span> |
| <span data-ttu-id="e2aa3-316">lastlogindate</span><span class="sxs-lookup"><span data-stu-id="e2aa3-316">lastlogindate</span></span> |<span data-ttu-id="e2aa3-317">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="e2aa3-317">Edm.DateTime</span></span> |

<span data-ttu-id="e2aa3-318">Definieer vervolgens als volgt hello Azure Table-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-318">Next, define hello Azure Table dataset as follows.</span></span> <span data-ttu-id="e2aa3-319">U hoeft niet toospecify "structuur" sectie met informatie over Hallo omdat Hallo-informatie is al opgegeven in Hallo onderliggende gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-319">You do not need toospecify “structure” section with hello type information since hello type information is already specified in hello underlying data store.</span></span>

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

<span data-ttu-id="e2aa3-320">In dit geval Data Factory automatisch gegevenstypeconversies inclusief Hallo Datetime-veld met de Hallo aangepaste datum/tijd-indeling met behulp van 'fr-fr' hello cultuur, bij het verplaatsen van gegevens uit Blob tooAzure tabel.</span><span class="sxs-lookup"><span data-stu-id="e2aa3-320">In this case, Data Factory automatically does type conversions including hello Datetime field with hello custom datetime format using hello "fr-fr" culture when moving data from Blob tooAzure Table.</span></span>

> [!NOTE]
> <span data-ttu-id="e2aa3-321">toomap kolommen uit de bron gegevensset toocolumns uit sink gegevensset, Zie [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="e2aa3-321">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="e2aa3-322">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="e2aa3-322">Performance and Tuning</span></span>
<span data-ttu-id="e2aa3-323">toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize, Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="e2aa3-323">toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it, see [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md).</span></span>
