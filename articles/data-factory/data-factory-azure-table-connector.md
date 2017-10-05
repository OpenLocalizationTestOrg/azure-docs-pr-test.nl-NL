---
title: Gegevens verplaatsen naar/van Azure Table | Microsoft Docs
description: Informatie over het verplaatsen van gegevens van Azure Table Storage met Azure Data Factory.
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
ms.openlocfilehash: 792a551ae3dae46c503e5f0dda74cd0ac3a69c3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-to-and-from-azure-table-using-azure-data-factory"></a><span data-ttu-id="1b89b-103">Gegevens verplaatsen en naar Azure Table met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="1b89b-103">Move data to and from Azure Table using Azure Data Factory</span></span>
<span data-ttu-id="1b89b-104">Dit artikel wordt uitgelegd dat het gebruik van de Kopieeractiviteit in Azure Data Factory om gegevens uit Azure Table Storage te verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="1b89b-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure Table Storage.</span></span> <span data-ttu-id="1b89b-105">Dit is gebaseerd op de [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, hetgeen een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit toont.</span><span class="sxs-lookup"><span data-stu-id="1b89b-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

<span data-ttu-id="1b89b-106">U kunt gegevens kopiëren van een ondersteunde brongegevensarchief naar Azure Table Storage of Azure Table Storage met alle ondersteunde sink-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="1b89b-106">You can copy data from any supported source data store to Azure Table Storage or from Azure Table Storage to any supported sink data store.</span></span> <span data-ttu-id="1b89b-107">Zie voor een lijst met gegevensarchieven als bronnen of PUT wordt ondersteund door de kopieeractiviteit, de [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel.</span><span class="sxs-lookup"><span data-stu-id="1b89b-107">For a list of data stores supported as sources or sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="1b89b-108">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="1b89b-108">Getting started</span></span>
<span data-ttu-id="1b89b-109">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens uit een Azure-tabelopslag verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="1b89b-109">You can create a pipeline with a copy activity that moves data to/from an Azure Table Storage by using different tools/APIs.</span></span>

<span data-ttu-id="1b89b-110">De eenvoudigste manier om een pijplijn maken is met de **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="1b89b-110">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="1b89b-111">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met de wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="1b89b-111">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="1b89b-112">U kunt ook de volgende hulpprogramma's gebruiken voor het maken van een pijplijn: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon**, **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="1b89b-112">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="1b89b-113">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies voor een pijplijn maken met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="1b89b-113">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="1b89b-114">Of u de hulpprogramma's of API's gebruiken, moet u de volgende stappen voor het maken van een pijplijn die de gegevens vanuit een brongegevensarchief naar een gegevensarchief sink verplaatst uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="1b89b-114">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="1b89b-115">Maak **gekoppelde services** slaat om invoer- en gegevens te koppelen aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="1b89b-115">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="1b89b-116">Maak **gegevenssets** vertegenwoordigt de invoer- en -gegevens voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="1b89b-116">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="1b89b-117">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="1b89b-117">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="1b89b-118">Wanneer u de wizard gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1b89b-118">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="1b89b-119">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van de JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="1b89b-119">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="1b89b-120">Zie voor voorbeelden met JSON-definities voor Data Factory-entiteiten die worden gebruikt om gegevens te kopiëren naar/van een Azure-tabelopslag [JSON voorbeelden](#json-examples) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="1b89b-120">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Table Storage, see [JSON examples](#json-examples) section of this article.</span></span> 

<span data-ttu-id="1b89b-121">De volgende secties bevatten informatie over de JSON-eigenschappen die worden gebruikt voor het definiëren van Data Factory-entiteiten specifieke naar Azure Table Storage:</span><span class="sxs-lookup"><span data-stu-id="1b89b-121">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Table Storage:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="1b89b-122">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="1b89b-122">Linked service properties</span></span>
<span data-ttu-id="1b89b-123">Er zijn twee soorten gekoppelde services die kunt u een Azure blob storage koppelen aan een Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="1b89b-123">There are two types of linked services you can use to link an Azure blob storage to an Azure data factory.</span></span> <span data-ttu-id="1b89b-124">Ze zijn: **AzureStorage** gekoppelde service en **AzureStorageSas** gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="1b89b-124">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="1b89b-125">De gekoppelde Azure Storage-service biedt de gegevensfactory met globale toegang tot Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="1b89b-125">The Azure Storage linked service provides the data factory with global access to the Azure Storage.</span></span> <span data-ttu-id="1b89b-126">Terwijl de Azure Storage SAS (Shared Access Signature) gekoppelde biedt service de gegevensfactory met de toegang beperkt/tijdsgebonden naar Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="1b89b-126">Whereas, The Azure Storage SAS (Shared Access Signature) linked service provides the data factory with restricted/time-bound access to the Azure Storage.</span></span> <span data-ttu-id="1b89b-127">Er zijn geen andere verschillen tussen deze twee gekoppelde services.</span><span class="sxs-lookup"><span data-stu-id="1b89b-127">There are no other differences between these two linked services.</span></span> <span data-ttu-id="1b89b-128">Kies de gekoppelde service die bij uw behoeften past.</span><span class="sxs-lookup"><span data-stu-id="1b89b-128">Choose the linked service that suits your needs.</span></span> <span data-ttu-id="1b89b-129">De volgende secties bevatten meer details over deze twee gekoppelde services.</span><span class="sxs-lookup"><span data-stu-id="1b89b-129">The following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="1b89b-130">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="1b89b-130">Dataset properties</span></span>
<span data-ttu-id="1b89b-131">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van de [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="1b89b-131">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="1b89b-132">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).</span><span class="sxs-lookup"><span data-stu-id="1b89b-132">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="1b89b-133">De sectie typeProperties verschilt voor elk type gegevensset en bevat informatie over de locatie van de gegevens in het gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="1b89b-133">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="1b89b-134">De **typeProperties** sectie voor de gegevensset van het type **AzureTable** heeft de volgende eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="1b89b-134">The **typeProperties** section for the dataset of type **AzureTable** has the following properties.</span></span>

| <span data-ttu-id="1b89b-135">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="1b89b-135">Property</span></span> | <span data-ttu-id="1b89b-136">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="1b89b-136">Description</span></span> | <span data-ttu-id="1b89b-137">Vereist</span><span class="sxs-lookup"><span data-stu-id="1b89b-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1b89b-138">tableName</span><span class="sxs-lookup"><span data-stu-id="1b89b-138">tableName</span></span> |<span data-ttu-id="1b89b-139">De naam van de tabel in de Azure-tabel Database-instantie waarnaar de gekoppelde service verwijst.</span><span class="sxs-lookup"><span data-stu-id="1b89b-139">Name of the table in the Azure Table Database instance that linked service refers to.</span></span> |<span data-ttu-id="1b89b-140">Ja.</span><span class="sxs-lookup"><span data-stu-id="1b89b-140">Yes.</span></span> <span data-ttu-id="1b89b-141">Wanneer een tabelnaam is opgegeven zonder een azureTableSourceQuery, worden alle records uit de tabel worden gekopieerd naar de bestemming.</span><span class="sxs-lookup"><span data-stu-id="1b89b-141">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="1b89b-142">Als een azureTableSourceQuery ook is opgegeven, worden de records uit de tabel die voldoet aan de query gekopieerd naar de bestemming.</span><span class="sxs-lookup"><span data-stu-id="1b89b-142">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |

### <a name="schema-by-data-factory"></a><span data-ttu-id="1b89b-143">Schema door Data Factory</span><span class="sxs-lookup"><span data-stu-id="1b89b-143">Schema by Data Factory</span></span>
<span data-ttu-id="1b89b-144">Voor gegevens zonder schema winkels zoals Azure Table afleidt de Data Factory-service het schema in een van de volgende manieren:</span><span class="sxs-lookup"><span data-stu-id="1b89b-144">For schema-free data stores such as Azure Table, the Data Factory service infers the schema in one of the following ways:</span></span>

1. <span data-ttu-id="1b89b-145">Als u de structuur van gegevens met behulp van opgeven de **structuur** eigenschap in de definitie van de gegevensset, de Data Factory-service zich houdt aan deze structuur als het schema.</span><span class="sxs-lookup"><span data-stu-id="1b89b-145">If you specify the structure of data by using the **structure** property in the dataset definition, the Data Factory service honors this structure as the schema.</span></span> <span data-ttu-id="1b89b-146">Als een rij geen waarde voor een kolom bevat, wordt in dit geval een null-waarde opgegeven voor deze.</span><span class="sxs-lookup"><span data-stu-id="1b89b-146">In this case, if a row does not contain a value for a column, a null value is provided for it.</span></span>
2. <span data-ttu-id="1b89b-147">Als u de structuur van gegevens niet via opgeeft de **structuur** het schema-eigenschap in de definitie van de gegevensset, Data Factory afleidt met behulp van de eerste rij in de gegevens.</span><span class="sxs-lookup"><span data-stu-id="1b89b-147">If you don't specify the structure of data by using the **structure** property in the dataset definition, Data Factory infers the schema by using the first row in the data.</span></span> <span data-ttu-id="1b89b-148">Als de eerste rij niet het volledige schema bevat, worden sommige kolommen in dit geval wordt opgehaald in het resultaat van de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="1b89b-148">In this case, if the first row does not contain the full schema, some columns are missed in the result of copy operation.</span></span>

<span data-ttu-id="1b89b-149">Daarom voor gegevensbronnen zonder schema, de aanbevolen procedure is om op te geven van de structuur van gegevens met de **structuur** eigenschap.</span><span class="sxs-lookup"><span data-stu-id="1b89b-149">Therefore, for schema-free data sources, the best practice is to specify the structure of data using the **structure** property.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="1b89b-150">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="1b89b-150">Copy activity properties</span></span>
<span data-ttu-id="1b89b-151">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van activiteiten van de [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="1b89b-151">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="1b89b-152">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer gegevenssets en beleidsregels zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="1b89b-152">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span>

<span data-ttu-id="1b89b-153">Eigenschappen die beschikbaar zijn in de sectie typeProperties van de activiteit wordt aan de andere kant variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="1b89b-153">Properties available in the typeProperties section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="1b89b-154">Voor de kopieeractiviteit variëren ze, afhankelijk van de typen van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="1b89b-154">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="1b89b-155">**AzureTableSource** ondersteunt de volgende eigenschappen in de sectie typeProperties:</span><span class="sxs-lookup"><span data-stu-id="1b89b-155">**AzureTableSource** supports the following properties in typeProperties section:</span></span>

| <span data-ttu-id="1b89b-156">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="1b89b-156">Property</span></span> | <span data-ttu-id="1b89b-157">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="1b89b-157">Description</span></span> | <span data-ttu-id="1b89b-158">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="1b89b-158">Allowed values</span></span> | <span data-ttu-id="1b89b-159">Vereist</span><span class="sxs-lookup"><span data-stu-id="1b89b-159">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1b89b-160">azureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="1b89b-160">azureTableSourceQuery</span></span> |<span data-ttu-id="1b89b-161">Gebruik de aangepaste query om gegevens te lezen.</span><span class="sxs-lookup"><span data-stu-id="1b89b-161">Use the custom query to read data.</span></span> |<span data-ttu-id="1b89b-162">Azure-tabel queryreeks.</span><span class="sxs-lookup"><span data-stu-id="1b89b-162">Azure table query string.</span></span> <span data-ttu-id="1b89b-163">Zie de voorbeelden in de volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="1b89b-163">See examples in the next section.</span></span> |<span data-ttu-id="1b89b-164">Nee.</span><span class="sxs-lookup"><span data-stu-id="1b89b-164">No.</span></span> <span data-ttu-id="1b89b-165">Wanneer een tabelnaam is opgegeven zonder een azureTableSourceQuery, worden alle records uit de tabel worden gekopieerd naar de bestemming.</span><span class="sxs-lookup"><span data-stu-id="1b89b-165">When a tableName is specified without an azureTableSourceQuery, all records from the table are copied to the destination.</span></span> <span data-ttu-id="1b89b-166">Als een azureTableSourceQuery ook is opgegeven, worden de records uit de tabel die voldoet aan de query gekopieerd naar de bestemming.</span><span class="sxs-lookup"><span data-stu-id="1b89b-166">If an azureTableSourceQuery is also specified, records from the table that satisfies the query are copied to the destination.</span></span> |
| <span data-ttu-id="1b89b-167">azureTableSourceIgnoreTableNotFound</span><span class="sxs-lookup"><span data-stu-id="1b89b-167">azureTableSourceIgnoreTableNotFound</span></span> |<span data-ttu-id="1b89b-168">Geef aan of de uitzondering van de tabel slikken bestaat niet.</span><span class="sxs-lookup"><span data-stu-id="1b89b-168">Indicate whether swallow the exception of table not exist.</span></span> |<span data-ttu-id="1b89b-169">DE WAARDE TRUE</span><span class="sxs-lookup"><span data-stu-id="1b89b-169">TRUE</span></span><br/><span data-ttu-id="1b89b-170">DE WAARDE FALSE</span><span class="sxs-lookup"><span data-stu-id="1b89b-170">FALSE</span></span> |<span data-ttu-id="1b89b-171">Nee</span><span class="sxs-lookup"><span data-stu-id="1b89b-171">No</span></span> |

### <a name="azuretablesourcequery-examples"></a><span data-ttu-id="1b89b-172">Voorbeelden van azureTableSourceQuery</span><span class="sxs-lookup"><span data-stu-id="1b89b-172">azureTableSourceQuery examples</span></span>
<span data-ttu-id="1b89b-173">Als Azure Table-kolom van het tekenreekstype:</span><span class="sxs-lookup"><span data-stu-id="1b89b-173">If Azure Table column is of string type:</span></span>

```JSON
azureTableSourceQuery": "$$Text.Format('PartitionKey ge \\'{0:yyyyMMddHH00_0000}\\' and PartitionKey le \\'{0:yyyyMMddHH00_9999}\\'', SliceStart)"
```

<span data-ttu-id="1b89b-174">Als Azure Table-kolom van het type datetime:</span><span class="sxs-lookup"><span data-stu-id="1b89b-174">If Azure Table column is of datetime type:</span></span>

```JSON
"azureTableSourceQuery": "$$Text.Format('DeploymentEndTime gt datetime\\'{0:yyyy-MM-ddTHH:mm:ssZ}\\' and DeploymentEndTime le datetime\\'{1:yyyy-MM-ddTHH:mm:ssZ}\\'', SliceStart, SliceEnd)"
```

<span data-ttu-id="1b89b-175">**AzureTableSink** ondersteunt de volgende eigenschappen in de sectie typeProperties:</span><span class="sxs-lookup"><span data-stu-id="1b89b-175">**AzureTableSink** supports the following properties in typeProperties section:</span></span>

| <span data-ttu-id="1b89b-176">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="1b89b-176">Property</span></span> | <span data-ttu-id="1b89b-177">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="1b89b-177">Description</span></span> | <span data-ttu-id="1b89b-178">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="1b89b-178">Allowed values</span></span> | <span data-ttu-id="1b89b-179">Vereist</span><span class="sxs-lookup"><span data-stu-id="1b89b-179">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1b89b-180">azureTableDefaultPartitionKeyValue</span><span class="sxs-lookup"><span data-stu-id="1b89b-180">azureTableDefaultPartitionKeyValue</span></span> |<span data-ttu-id="1b89b-181">Standaardwaarde voor de partitiesleutel die kan worden gebruikt door de sink.</span><span class="sxs-lookup"><span data-stu-id="1b89b-181">Default partition key value that can be used by the sink.</span></span> |<span data-ttu-id="1b89b-182">Een string-waarde.</span><span class="sxs-lookup"><span data-stu-id="1b89b-182">A string value.</span></span> |<span data-ttu-id="1b89b-183">Nee</span><span class="sxs-lookup"><span data-stu-id="1b89b-183">No</span></span> |
| <span data-ttu-id="1b89b-184">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="1b89b-184">azureTablePartitionKeyName</span></span> |<span data-ttu-id="1b89b-185">Geef de naam van de kolom waarvan de waarden worden gebruikt als partitiesleutels.</span><span class="sxs-lookup"><span data-stu-id="1b89b-185">Specify name of the column whose values are used as partition keys.</span></span> <span data-ttu-id="1b89b-186">Als niet wordt opgegeven, wordt AzureTableDefaultPartitionKeyValue gebruikt als de partitiesleutel.</span><span class="sxs-lookup"><span data-stu-id="1b89b-186">If not specified, AzureTableDefaultPartitionKeyValue is used as the partition key.</span></span> |<span data-ttu-id="1b89b-187">De naam van een kolom.</span><span class="sxs-lookup"><span data-stu-id="1b89b-187">A column name.</span></span> |<span data-ttu-id="1b89b-188">Nee</span><span class="sxs-lookup"><span data-stu-id="1b89b-188">No</span></span> |
| <span data-ttu-id="1b89b-189">azureTableRowKeyName</span><span class="sxs-lookup"><span data-stu-id="1b89b-189">azureTableRowKeyName</span></span> |<span data-ttu-id="1b89b-190">Geef de naam van de kolom waarvan de kolomwaarden worden gebruikt als de rijsleutel.</span><span class="sxs-lookup"><span data-stu-id="1b89b-190">Specify name of the column whose column values are used as row key.</span></span> <span data-ttu-id="1b89b-191">Als niet wordt opgegeven, gebruikt u een GUID voor elke rij.</span><span class="sxs-lookup"><span data-stu-id="1b89b-191">If not specified, use a GUID for each row.</span></span> |<span data-ttu-id="1b89b-192">De naam van een kolom.</span><span class="sxs-lookup"><span data-stu-id="1b89b-192">A column name.</span></span> |<span data-ttu-id="1b89b-193">Nee</span><span class="sxs-lookup"><span data-stu-id="1b89b-193">No</span></span> |
| <span data-ttu-id="1b89b-194">azureTableInsertType</span><span class="sxs-lookup"><span data-stu-id="1b89b-194">azureTableInsertType</span></span> |<span data-ttu-id="1b89b-195">De modus voor gegevens in Azure-tabel invoegen.</span><span class="sxs-lookup"><span data-stu-id="1b89b-195">The mode to insert data into Azure table.</span></span><br/><br/><span data-ttu-id="1b89b-196">Deze eigenschap bepaalt of bestaande rijen in de uitvoertabel met partitie-als rijsleutels die overeenkomt met de waarden vervangen of samenvoegen van hebben.</span><span class="sxs-lookup"><span data-stu-id="1b89b-196">This property controls whether existing rows in the output table with matching partition and row keys have their values replaced or merged.</span></span> <br/><br/><span data-ttu-id="1b89b-197">Zie voor meer informatie over de werking van deze instellingen (merge en vervangen), [invoegen of Merge entiteit](https://msdn.microsoft.com/library/azure/hh452241.aspx) en [invoegen of vervangen entiteit](https://msdn.microsoft.com/library/azure/hh452242.aspx) onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="1b89b-197">To learn about how these settings (merge and replace) work, see [Insert or Merge Entity](https://msdn.microsoft.com/library/azure/hh452241.aspx) and [Insert or Replace Entity](https://msdn.microsoft.com/library/azure/hh452242.aspx) topics.</span></span> <br/><br> <span data-ttu-id="1b89b-198">Deze instelling is van toepassing op het rijniveau van niet tabelniveau, en geen van beide optie worden de rijen in de uitvoertabel die niet bestaan in de invoer verwijderd.</span><span class="sxs-lookup"><span data-stu-id="1b89b-198">This setting applies at the row level, not the table level, and neither option deletes rows in the output table that do not exist in the input.</span></span> |<span data-ttu-id="1b89b-199">samenvoegen (standaard)</span><span class="sxs-lookup"><span data-stu-id="1b89b-199">merge (default)</span></span><br/><span data-ttu-id="1b89b-200">vervangen</span><span class="sxs-lookup"><span data-stu-id="1b89b-200">replace</span></span> |<span data-ttu-id="1b89b-201">Nee</span><span class="sxs-lookup"><span data-stu-id="1b89b-201">No</span></span> |
| <span data-ttu-id="1b89b-202">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="1b89b-202">writeBatchSize</span></span> |<span data-ttu-id="1b89b-203">Voegt de gegevens in de Azure-tabel wanneer de writeBatchSize of writeBatchTimeout is bereikt.</span><span class="sxs-lookup"><span data-stu-id="1b89b-203">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit.</span></span> |<span data-ttu-id="1b89b-204">Geheel getal (aantal rijen)</span><span class="sxs-lookup"><span data-stu-id="1b89b-204">Integer (number of rows)</span></span> |<span data-ttu-id="1b89b-205">Nee (standaard: 10000)</span><span class="sxs-lookup"><span data-stu-id="1b89b-205">No (default: 10000)</span></span> |
| <span data-ttu-id="1b89b-206">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="1b89b-206">writeBatchTimeout</span></span> |<span data-ttu-id="1b89b-207">Voegt de gegevens in de Azure-tabel wanneer de writeBatchSize of writeBatchTimeout is bereikt.</span><span class="sxs-lookup"><span data-stu-id="1b89b-207">Inserts data into the Azure table when the writeBatchSize or writeBatchTimeout is hit</span></span> |<span data-ttu-id="1b89b-208">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="1b89b-208">timespan</span></span><br/><br/><span data-ttu-id="1b89b-209">Voorbeeld: "00: 20:00 ' (20 minuten)</span><span class="sxs-lookup"><span data-stu-id="1b89b-209">Example: “00:20:00” (20 minutes)</span></span> |<span data-ttu-id="1b89b-210">Nee (voor opslag client standaardtime-out standaardwaarde is 90 sec)</span><span class="sxs-lookup"><span data-stu-id="1b89b-210">No (Default to storage client default timeout value 90 sec)</span></span> |

### <a name="azuretablepartitionkeyname"></a><span data-ttu-id="1b89b-211">azureTablePartitionKeyName</span><span class="sxs-lookup"><span data-stu-id="1b89b-211">azureTablePartitionKeyName</span></span>
<span data-ttu-id="1b89b-212">Een bronkolom worden toegewezen aan een doelkolom met behulp van de vertaler JSON-eigenschap voordat u de doelkolom als de azureTablePartitionKeyName gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="1b89b-212">Map a source column to a destination column using the translator JSON property before you can use the destination column as the azureTablePartitionKeyName.</span></span>

<span data-ttu-id="1b89b-213">In het volgende voorbeeld bronkolom DivisionID is toegewezen aan de doelkolom: DivisionID.</span><span class="sxs-lookup"><span data-stu-id="1b89b-213">In the following example, source column DivisionID is mapped to the destination column: DivisionID.</span></span>  

```JSON
"translator": {
    "type": "TabularTranslator",
    "columnMappings": "DivisionID: DivisionID, FirstName: FirstName, LastName: LastName"
}
```
<span data-ttu-id="1b89b-214">De DivisionID is opgegeven als de partitiesleutel.</span><span class="sxs-lookup"><span data-stu-id="1b89b-214">The DivisionID is specified as the partition key.</span></span>

```JSON
"sink": {
    "type": "AzureTableSink",
    "azureTablePartitionKeyName": "DivisionID",
    "writeBatchSize": 100,
    "writeBatchTimeout": "01:00:00"
}
```
## <a name="json-examples"></a><span data-ttu-id="1b89b-215">JSON-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="1b89b-215">JSON examples</span></span>
<span data-ttu-id="1b89b-216">De volgende voorbeelden geven voorbeeld JSON definities die u een pijplijn maken kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="1b89b-216">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="1b89b-217">Ze laten zien hoe om gegevens te kopiëren en naar Azure Table Storage en Azure Blob-Database.</span><span class="sxs-lookup"><span data-stu-id="1b89b-217">They show how to copy data to and from Azure Table Storage and Azure Blob Database.</span></span> <span data-ttu-id="1b89b-218">Echter, de gegevens kunnen worden gekopieerd **rechtstreeks** uit een van de bronnen aan een van de ondersteunde Put.</span><span class="sxs-lookup"><span data-stu-id="1b89b-218">However, data can be copied **directly** from any of the sources to any of the supported sinks.</span></span> <span data-ttu-id="1b89b-219">Zie voor meer informatie de sectie 'ondersteunde gegevensarchieven en indelingen' in [verplaatsen van gegevens met behulp van de Kopieeractiviteit](data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="1b89b-219">For more information, see the section "Supported data stores and formats" in [Move data by using Copy Activity](data-factory-data-movement-activities.md).</span></span>

## <a name="example-copy-data-from-azure-table-to-azure-blob"></a><span data-ttu-id="1b89b-220">Voorbeeld: Gegevens kopiëren van Azure Table naar Azure Blob</span><span class="sxs-lookup"><span data-stu-id="1b89b-220">Example: Copy data from Azure Table to Azure Blob</span></span>
<span data-ttu-id="1b89b-221">Het volgende voorbeeld toont:</span><span class="sxs-lookup"><span data-stu-id="1b89b-221">The following sample shows:</span></span>

1. <span data-ttu-id="1b89b-222">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (gebruikt voor blob & tabel).</span><span class="sxs-lookup"><span data-stu-id="1b89b-222">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob).</span></span>
2. <span data-ttu-id="1b89b-223">Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1b89b-223">An input [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
3. <span data-ttu-id="1b89b-224">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1b89b-224">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="1b89b-225">De [pijplijn](data-factory-create-pipelines.md) met de kopieeractiviteit die gebruikmaakt van [AzureTableSource](#activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1b89b-225">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [AzureTableSource](#activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="1b89b-226">Het voorbeeld kopieert de gegevens die behoren tot de standaardpartitie in een Azure-tabel naar een blob elk uur.</span><span class="sxs-lookup"><span data-stu-id="1b89b-226">The sample copies data belonging to the default partition in an Azure Table to a blob every hour.</span></span> <span data-ttu-id="1b89b-227">De JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na de voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="1b89b-227">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="1b89b-228">**Gekoppelde Azure storage-service:**</span><span class="sxs-lookup"><span data-stu-id="1b89b-228">**Azure storage linked service:**</span></span>

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
<span data-ttu-id="1b89b-229">Azure Data Factory ondersteunt twee soorten gekoppelde Azure Storage-services: **AzureStorage** en **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="1b89b-229">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="1b89b-230">U de verbindingsreeks met de sleutel van de account opgeven voor de eerste en voor de latere, geeft u de Shared Access Signature (SAS)-Uri.</span><span class="sxs-lookup"><span data-stu-id="1b89b-230">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="1b89b-231">Zie [gekoppelde Services](#linked-service-properties) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="1b89b-231">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="1b89b-232">**Azure Table invoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="1b89b-232">**Azure Table input dataset:**</span></span>

<span data-ttu-id="1b89b-233">Het voorbeeld wordt ervan uitgegaan dat u een tabel "MijnTabel" hebt gemaakt in Azure-tabel.</span><span class="sxs-lookup"><span data-stu-id="1b89b-233">The sample assumes you have created a table “MyTable” in Azure Table.</span></span>

<span data-ttu-id="1b89b-234">Instelling 'extern': 'true' informeert de Data Factory-service dat de dataset extern is aan de gegevensfactory en niet wordt geproduceerd door een activiteit in de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="1b89b-234">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="1b89b-235">**Azure Blob-uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="1b89b-235">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="1b89b-236">Gegevens worden geschreven naar een nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="1b89b-236">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="1b89b-237">Het pad naar de blob wordt dynamisch geëvalueerd op basis van de begintijd van het segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="1b89b-237">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="1b89b-238">Het mappad maakt gebruik van jaar, maand, dag en uur delen van de begintijd.</span><span class="sxs-lookup"><span data-stu-id="1b89b-238">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="1b89b-239">**De kopieeractiviteit in een pijplijn met AzureTableSource en BlobSink:**</span><span class="sxs-lookup"><span data-stu-id="1b89b-239">**Copy activity in a pipeline with AzureTableSource and BlobSink:**</span></span>

<span data-ttu-id="1b89b-240">De pijplijn bevat een Kopieeractiviteit die is geconfigureerd voor gebruik van de invoer- en uitvoergegevenssets en elk uur is gepland.</span><span class="sxs-lookup"><span data-stu-id="1b89b-240">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="1b89b-241">In de pijplijn-JSON-definitie de **bron** type is ingesteld op **AzureTableSource** en **sink** type is ingesteld op **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="1b89b-241">In the pipeline JSON definition, the **source** type is set to **AzureTableSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="1b89b-242">De SQL-query opgegeven met **AzureTableSourceQuery** eigenschap selecteert de gegevens uit de standaardpartitie elk uur te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="1b89b-242">The SQL query specified with **AzureTableSourceQuery** property selects the data from the default partition every hour to copy.</span></span>

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

## <a name="example-copy-data-from-azure-blob-to-azure-table"></a><span data-ttu-id="1b89b-243">Voorbeeld: Gegevens kopiëren van Azure-Blob naar Azure Table</span><span class="sxs-lookup"><span data-stu-id="1b89b-243">Example: Copy data from Azure Blob to Azure Table</span></span>
<span data-ttu-id="1b89b-244">Het volgende voorbeeld toont:</span><span class="sxs-lookup"><span data-stu-id="1b89b-244">The following sample shows:</span></span>

1. <span data-ttu-id="1b89b-245">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (gebruikt voor blob & tabel)</span><span class="sxs-lookup"><span data-stu-id="1b89b-245">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (used for both table & blob)</span></span>
2. <span data-ttu-id="1b89b-246">Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1b89b-246">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
3. <span data-ttu-id="1b89b-247">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1b89b-247">An output [dataset](data-factory-create-datasets.md) of type [AzureTable](#dataset-properties).</span></span>
4. <span data-ttu-id="1b89b-248">De [pijplijn](data-factory-create-pipelines.md) met de kopieeractiviteit die gebruikmaakt van [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) en [AzureTableSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1b89b-248">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureTableSink](#copy-activity-properties).</span></span>

<span data-ttu-id="1b89b-249">De voorbeeld-kopieën timeseries gegevens van een Azure-blob naar een Azure tabel per uur.</span><span class="sxs-lookup"><span data-stu-id="1b89b-249">The sample copies time-series data from an Azure blob to an Azure table hourly.</span></span> <span data-ttu-id="1b89b-250">De JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na de voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="1b89b-250">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="1b89b-251">**Gekoppelde Azure storage (voor Azure Table & Blob)-service:**</span><span class="sxs-lookup"><span data-stu-id="1b89b-251">**Azure storage (for both Azure Table & Blob) linked service:**</span></span>

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

<span data-ttu-id="1b89b-252">Azure Data Factory ondersteunt twee soorten gekoppelde Azure Storage-services: **AzureStorage** en **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="1b89b-252">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="1b89b-253">U de verbindingsreeks met de sleutel van de account opgeven voor de eerste en voor de latere, geeft u de Shared Access Signature (SAS)-Uri.</span><span class="sxs-lookup"><span data-stu-id="1b89b-253">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="1b89b-254">Zie [gekoppelde Services](#linked-service-properties) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="1b89b-254">See [Linked Services](#linked-service-properties) section for details.</span></span>

<span data-ttu-id="1b89b-255">**Azure Blob invoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="1b89b-255">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="1b89b-256">Gegevens wordt opgehaald uit een nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="1b89b-256">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="1b89b-257">Pad en naam van de map voor de blob worden dynamisch geëvalueerd op basis van de begintijd van het segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="1b89b-257">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="1b89b-258">Het mappad gebruikt jaar, maand en dag deel uit van de begintijd en de bestandsnaam wordt gebruikt voor het uur deel van de begintijd.</span><span class="sxs-lookup"><span data-stu-id="1b89b-258">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="1b89b-259">"extern": "true" instelling informeert de Data Factory-service dat de dataset extern is aan de gegevensfactory en niet wordt geproduceerd door een activiteit in de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="1b89b-259">“external”: “true” setting informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="1b89b-260">**Azure-tabel uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="1b89b-260">**Azure Table output dataset:**</span></span>

<span data-ttu-id="1b89b-261">Het voorbeeld worden gegevens gekopieerd naar een tabel met de naam "MijnTabel" in de Azure-tabel.</span><span class="sxs-lookup"><span data-stu-id="1b89b-261">The sample copies data to a table named “MyTable” in Azure Table.</span></span> <span data-ttu-id="1b89b-262">Maak een Azure-tabel met hetzelfde aantal kolommen, zoals u verwacht dat de Blob-CSV-bestand bevatten.</span><span class="sxs-lookup"><span data-stu-id="1b89b-262">Create an Azure table with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="1b89b-263">Nieuwe rijen worden toegevoegd aan de tabel om het uur.</span><span class="sxs-lookup"><span data-stu-id="1b89b-263">New rows are added to the table every hour.</span></span>

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

<span data-ttu-id="1b89b-264">**De kopieeractiviteit in een pijplijn met BlobSource en AzureTableSink:**</span><span class="sxs-lookup"><span data-stu-id="1b89b-264">**Copy activity in a pipeline with BlobSource and AzureTableSink:**</span></span>

<span data-ttu-id="1b89b-265">De pijplijn bevat een Kopieeractiviteit die is geconfigureerd voor gebruik van de invoer- en uitvoergegevenssets en elk uur is gepland.</span><span class="sxs-lookup"><span data-stu-id="1b89b-265">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="1b89b-266">In de pijplijn-JSON-definitie de **bron** type is ingesteld op **BlobSource** en **sink** type is ingesteld op **AzureTableSink**.</span><span class="sxs-lookup"><span data-stu-id="1b89b-266">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **AzureTableSink**.</span></span>

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
## <a name="type-mapping-for-azure-table"></a><span data-ttu-id="1b89b-267">Toewijzing van het type voor Azure-tabel</span><span class="sxs-lookup"><span data-stu-id="1b89b-267">Type Mapping for Azure Table</span></span>
<span data-ttu-id="1b89b-268">Zoals vermeld in de [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel kopieerbewerking wordt automatische typeconversies van brontypen opvangen typen met de volgende benadering voor in twee stappen uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1b89b-268">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach.</span></span>

1. <span data-ttu-id="1b89b-269">Systeemeigen brontypen converteren naar .NET-type</span><span class="sxs-lookup"><span data-stu-id="1b89b-269">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="1b89b-270">Converteren van .NET-type naar systeemeigen sink-type</span><span class="sxs-lookup"><span data-stu-id="1b89b-270">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="1b89b-271">Wanneer u gegevens verplaatst naar & van Azure-tabel, de volgende [toewijzingen die zijn gedefinieerd door de service Azure Table](https://msdn.microsoft.com/library/azure/dd179338.aspx) worden gebruikt vanuit Azure tabel OData-typen aan .NET-type en vice versa.</span><span class="sxs-lookup"><span data-stu-id="1b89b-271">When moving data to & from Azure Table, the following [mappings defined by Azure Table service](https://msdn.microsoft.com/library/azure/dd179338.aspx) are used from Azure Table OData types to .NET type and vice versa.</span></span>

| <span data-ttu-id="1b89b-272">OData-gegevenstype</span><span class="sxs-lookup"><span data-stu-id="1b89b-272">OData Data Type</span></span> | <span data-ttu-id="1b89b-273">.NET-type</span><span class="sxs-lookup"><span data-stu-id="1b89b-273">.NET Type</span></span> | <span data-ttu-id="1b89b-274">Details</span><span class="sxs-lookup"><span data-stu-id="1b89b-274">Details</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1b89b-275">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="1b89b-275">Edm.Binary</span></span> |<span data-ttu-id="1b89b-276">Byte]</span><span class="sxs-lookup"><span data-stu-id="1b89b-276">byte[]</span></span> |<span data-ttu-id="1b89b-277">Een matrix met bytes maximaal 64 KB.</span><span class="sxs-lookup"><span data-stu-id="1b89b-277">An array of bytes up to 64 KB.</span></span> |
| <span data-ttu-id="1b89b-278">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="1b89b-278">Edm.Boolean</span></span> |<span data-ttu-id="1b89b-279">BOOL</span><span class="sxs-lookup"><span data-stu-id="1b89b-279">bool</span></span> |<span data-ttu-id="1b89b-280">Een Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="1b89b-280">A Boolean value.</span></span> |
| <span data-ttu-id="1b89b-281">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="1b89b-281">Edm.DateTime</span></span> |<span data-ttu-id="1b89b-282">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="1b89b-282">DateTime</span></span> |<span data-ttu-id="1b89b-283">Een 64-bits waarde wordt uitgedrukt als Coordinated Universal Time (UTC).</span><span class="sxs-lookup"><span data-stu-id="1b89b-283">A 64-bit value expressed as Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="1b89b-284">Het ondersteunde bereik van de datum-/ begint vanaf 12:00 middernacht, 1 januari 1601 A.D.</span><span class="sxs-lookup"><span data-stu-id="1b89b-284">The supported DateTime range begins from 12:00 midnight, January 1, 1601 A.D.</span></span> <span data-ttu-id="1b89b-285">(C.E.) UTC.</span><span class="sxs-lookup"><span data-stu-id="1b89b-285">(C.E.), UTC.</span></span> <span data-ttu-id="1b89b-286">Het bereik eindigt op 31 December 9999.</span><span class="sxs-lookup"><span data-stu-id="1b89b-286">The range ends at December 31, 9999.</span></span> |
| <span data-ttu-id="1b89b-287">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="1b89b-287">Edm.Double</span></span> |<span data-ttu-id="1b89b-288">dubbele</span><span class="sxs-lookup"><span data-stu-id="1b89b-288">double</span></span> |<span data-ttu-id="1b89b-289">Een 64-bits drijvende-kommawaarde.</span><span class="sxs-lookup"><span data-stu-id="1b89b-289">A 64-bit floating point value.</span></span> |
| <span data-ttu-id="1b89b-290">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="1b89b-290">Edm.Guid</span></span> |<span data-ttu-id="1b89b-291">GUID</span><span class="sxs-lookup"><span data-stu-id="1b89b-291">Guid</span></span> |<span data-ttu-id="1b89b-292">Een globally unique identifier van 128-bits.</span><span class="sxs-lookup"><span data-stu-id="1b89b-292">A 128-bit globally unique identifier.</span></span> |
| <span data-ttu-id="1b89b-293">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="1b89b-293">Edm.Int32</span></span> |<span data-ttu-id="1b89b-294">Int32</span><span class="sxs-lookup"><span data-stu-id="1b89b-294">Int32</span></span> |<span data-ttu-id="1b89b-295">Een 32-bits geheel getal.</span><span class="sxs-lookup"><span data-stu-id="1b89b-295">A 32-bit integer.</span></span> |
| <span data-ttu-id="1b89b-296">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="1b89b-296">Edm.Int64</span></span> |<span data-ttu-id="1b89b-297">Int64</span><span class="sxs-lookup"><span data-stu-id="1b89b-297">Int64</span></span> |<span data-ttu-id="1b89b-298">Een 64-bits geheel getal.</span><span class="sxs-lookup"><span data-stu-id="1b89b-298">A 64-bit integer.</span></span> |
| <span data-ttu-id="1b89b-299">Edm.String</span><span class="sxs-lookup"><span data-stu-id="1b89b-299">Edm.String</span></span> |<span data-ttu-id="1b89b-300">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="1b89b-300">String</span></span> |<span data-ttu-id="1b89b-301">Een waarde UTF-16-codering.</span><span class="sxs-lookup"><span data-stu-id="1b89b-301">A UTF-16-encoded value.</span></span> <span data-ttu-id="1b89b-302">Tekenreekswaarden mogelijk maximaal 64 KB.</span><span class="sxs-lookup"><span data-stu-id="1b89b-302">String values may be up to 64 KB.</span></span> |

### <a name="type-conversion-sample"></a><span data-ttu-id="1b89b-303">Type conversie voorbeeld</span><span class="sxs-lookup"><span data-stu-id="1b89b-303">Type Conversion Sample</span></span>
<span data-ttu-id="1b89b-304">Het volgende voorbeeld is voor het kopiëren van gegevens van een Azure-Blob naar Azure Table met typeconversies.</span><span class="sxs-lookup"><span data-stu-id="1b89b-304">The following sample is for copying data from an Azure Blob to Azure Table with type conversions.</span></span>

<span data-ttu-id="1b89b-305">Stel dat de Blob-gegevensset is CSV-indeling en drie kolommen bevat.</span><span class="sxs-lookup"><span data-stu-id="1b89b-305">Suppose the Blob dataset is in CSV format and contains three columns.</span></span> <span data-ttu-id="1b89b-306">Een van beide is een datetime-kolom met een aangepaste datum / tijdindeling met behulp van Franse afkortingen voor dag van de week.</span><span class="sxs-lookup"><span data-stu-id="1b89b-306">One of them is a datetime column with a custom datetime format using abbreviated French names for day of the week.</span></span>

<span data-ttu-id="1b89b-307">Definieer de bron van de Blob-gegevensset als volgt samen met de definities voor de kolommen.</span><span class="sxs-lookup"><span data-stu-id="1b89b-307">Define the Blob Source dataset as follows along with type definitions for the columns.</span></span>

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
<span data-ttu-id="1b89b-308">Toewijzing van het type van Azure Table OData-type opgegeven voor .NET-type, zou u de tabel definiëren in Azure-tabel met het volgende schema.</span><span class="sxs-lookup"><span data-stu-id="1b89b-308">Given the type mapping from Azure Table OData type to .NET type, you would define the table in Azure Table with the following schema.</span></span>

<span data-ttu-id="1b89b-309">**Azure tabelschema:**</span><span class="sxs-lookup"><span data-stu-id="1b89b-309">**Azure Table schema:**</span></span>

| <span data-ttu-id="1b89b-310">Kolomnaam</span><span class="sxs-lookup"><span data-stu-id="1b89b-310">Column name</span></span> | <span data-ttu-id="1b89b-311">Type</span><span class="sxs-lookup"><span data-stu-id="1b89b-311">Type</span></span> |
| --- | --- |
| <span data-ttu-id="1b89b-312">gebruikers-id</span><span class="sxs-lookup"><span data-stu-id="1b89b-312">userid</span></span> |<span data-ttu-id="1b89b-313">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="1b89b-313">Edm.Int64</span></span> |
| <span data-ttu-id="1b89b-314">naam</span><span class="sxs-lookup"><span data-stu-id="1b89b-314">name</span></span> |<span data-ttu-id="1b89b-315">Edm.String</span><span class="sxs-lookup"><span data-stu-id="1b89b-315">Edm.String</span></span> |
| <span data-ttu-id="1b89b-316">lastlogindate</span><span class="sxs-lookup"><span data-stu-id="1b89b-316">lastlogindate</span></span> |<span data-ttu-id="1b89b-317">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="1b89b-317">Edm.DateTime</span></span> |

<span data-ttu-id="1b89b-318">Definieer vervolgens als volgt de Azure Table-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="1b89b-318">Next, define the Azure Table dataset as follows.</span></span> <span data-ttu-id="1b89b-319">U hoeft niet "structuur" sectie met de type-informatie opgeven omdat de type-informatie al in het onderliggende gegevensarchief opgegeven is.</span><span class="sxs-lookup"><span data-stu-id="1b89b-319">You do not need to specify “structure” section with the type information since the type information is already specified in the underlying data store.</span></span>

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

<span data-ttu-id="1b89b-320">In dit geval Data Factory automatisch gegevenstypeconversies met inbegrip van de Datetime-veld met de aangepaste datum / tijdindeling met behulp van de cultuur "fr-fr" bij het verplaatsen van gegevens uit Blob naar Azure Table.</span><span class="sxs-lookup"><span data-stu-id="1b89b-320">In this case, Data Factory automatically does type conversions including the Datetime field with the custom datetime format using the "fr-fr" culture when moving data from Blob to Azure Table.</span></span>

> [!NOTE]
> <span data-ttu-id="1b89b-321">Zie het toewijzen van kolommen uit de bron-gegevensset naar kolommen uit de dataset sink [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="1b89b-321">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="1b89b-322">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="1b89b-322">Performance and Tuning</span></span>
<span data-ttu-id="1b89b-323">Zie voor meer informatie over de belangrijkste factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren om te optimaliseren, [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="1b89b-323">To learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it, see [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md).</span></span>
