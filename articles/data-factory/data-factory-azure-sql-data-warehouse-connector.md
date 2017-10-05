---
title: "Gegevens kopiëren naar/van Azure SQL Data Warehouse | Microsoft Docs"
description: "Informatie over het kopiëren van gegevens van Azure SQL Data Warehouse met behulp van Azure Data Factory"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: d90fa9bd-4b79-458a-8d40-e896835cfd4a
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 8cba89e0947646b498af07aa484511bf07bf7b0e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="copy-data-to-and-from-azure-sql-data-warehouse-using-azure-data-factory"></a><span data-ttu-id="ef565-103">Gegevens kopiëren van en naar Azure SQL Data Warehouse met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="ef565-103">Copy data to and from Azure SQL Data Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="ef565-104">Dit artikel wordt uitgelegd hoe u de Kopieeractiviteit in Azure Data Factory om gegevens te verplaatsen van Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ef565-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from Azure SQL Data Warehouse.</span></span> <span data-ttu-id="ef565-105">Dit is gebaseerd op de [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, hetgeen een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit toont.</span><span class="sxs-lookup"><span data-stu-id="ef565-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>  

> [!TIP]
> <span data-ttu-id="ef565-106">Gebruik PolyBase gegevens laadt in Azure SQL Data Warehouse zodat de beste prestaties.</span><span class="sxs-lookup"><span data-stu-id="ef565-106">To achieve best performance, use PolyBase to load data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="ef565-107">De [gebruik PolyBase gegevens laadt in Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) sectie bevat informatie.</span><span class="sxs-lookup"><span data-stu-id="ef565-107">The [Use PolyBase to load data into Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) section has details.</span></span> <span data-ttu-id="ef565-108">Zie voor een overzicht met een gebruiksvoorbeeld [1 TB laden in Azure SQL Data Warehouse onder 15 minuten met Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span><span class="sxs-lookup"><span data-stu-id="ef565-108">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="ef565-109">Ondersteunde scenario 's</span><span class="sxs-lookup"><span data-stu-id="ef565-109">Supported scenarios</span></span>
<span data-ttu-id="ef565-110">U kunt gegevens kopiëren **van Azure SQL Data Warehouse** opslaat in de volgende gegevens:</span><span class="sxs-lookup"><span data-stu-id="ef565-110">You can copy data **from Azure SQL Data Warehouse** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="ef565-111">U kunt gegevens kopiëren van de volgende gegevensarchieven **met Azure SQL Data Warehouse**:</span><span class="sxs-lookup"><span data-stu-id="ef565-111">You can copy data from the following data stores **to Azure SQL Data Warehouse**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!TIP]
> <span data-ttu-id="ef565-112">Wanneer gegevens uit SQL Server of Azure SQL Database kopiëren naar Azure SQL Data Warehouse, als de tabel niet in het doelarchief bestaat, maken Data Factory automatisch in de tabel in SQL Data Warehouse met behulp van het schema van de tabel in het gegevensarchief van de bron.</span><span class="sxs-lookup"><span data-stu-id="ef565-112">When copying data from SQL Server or Azure SQL Database to Azure SQL Data Warehouse, if the table does not exist in the destination store, Data Factory can automatically create the table in SQL Data Warehouse by using the schema of the table in the source data store.</span></span> <span data-ttu-id="ef565-113">Zie [automatisch maken van de tabel](#auto-table-creation) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ef565-113">See [Auto table creation](#auto-table-creation) for details.</span></span>

## <a name="supported-authentication-type"></a><span data-ttu-id="ef565-114">Ondersteund verificatietype</span><span class="sxs-lookup"><span data-stu-id="ef565-114">Supported authentication type</span></span>
<span data-ttu-id="ef565-115">Azure SQL Data Warehouse connector ondersteuning voor basisverificatie.</span><span class="sxs-lookup"><span data-stu-id="ef565-115">Azure SQL Data Warehouse connector support basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="ef565-116">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="ef565-116">Getting started</span></span>
<span data-ttu-id="ef565-117">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens worden verplaatst van een Azure SQL Data Warehouse met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="ef565-117">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Data Warehouse by using different tools/APIs.</span></span>

<span data-ttu-id="ef565-118">De eenvoudigste manier om een pijplijn waarmee gegevens van Azure SQL Data Warehouse worden gekopieerd maken is met de wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="ef565-118">The easiest way to create a pipeline that copies data to/from Azure SQL Data Warehouse is to use the Copy data wizard.</span></span> <span data-ttu-id="ef565-119">Zie [zelfstudie: gegevens laden in SQL Data Warehouse met Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) voor een snel overzicht over het maken van een pijplijn met de wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="ef565-119">See [Tutorial: Load data into SQL Data Warehouse with Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="ef565-120">U kunt ook de volgende hulpprogramma's gebruiken voor het maken van een pijplijn: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon**, **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="ef565-120">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="ef565-121">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies voor een pijplijn maken met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="ef565-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="ef565-122">Of u de hulpprogramma's of API's gebruiken, moet u de volgende stappen voor het maken van een pijplijn die de gegevens vanuit een brongegevensarchief naar een gegevensarchief sink verplaatst uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ef565-122">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="ef565-123">Maak een **gegevensfactory**.</span><span class="sxs-lookup"><span data-stu-id="ef565-123">Create a **data factory**.</span></span> <span data-ttu-id="ef565-124">Een gegevensfactory kan één of meer pijplijnen bevatten.</span><span class="sxs-lookup"><span data-stu-id="ef565-124">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="ef565-125">Maak **gekoppelde services** slaat om invoer- en gegevens te koppelen aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="ef565-125">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="ef565-126">Bijvoorbeeld, als u gegevens uit een Azure blob-opslag met een Azure SQL datawarehouse kopieert, maakt u twee gekoppelde services om te koppelen van uw Azure storage-account en de Azure SQL datawarehouse aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="ef565-126">For example, if you are copying data from an Azure blob storage to an Azure SQL data warehouse, you create two linked services to link your Azure storage account and Azure SQL data warehouse to your data factory.</span></span> <span data-ttu-id="ef565-127">Zie voor de gekoppelde service-eigenschappen die specifiek voor Azure SQL Data Warehouse zijn, [gekoppelde service-eigenschappen](#linked-service-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="ef565-127">For linked service properties that are specific to Azure SQL Data Warehouse, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="ef565-128">Maak **gegevenssets** vertegenwoordigt de invoer- en -gegevens voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="ef565-128">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="ef565-129">In het voorbeeld in de laatste stap wordt vermeld, maakt u een gegevensset om op te geven van de blob-container en de map waarin de invoergegevens.</span><span class="sxs-lookup"><span data-stu-id="ef565-129">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="ef565-130">En maken van een andere dataset om op te geven van de tabel in het Azure SQL datawarehouse waarin de gegevens die zijn gekopieerd uit de blobopslag.</span><span class="sxs-lookup"><span data-stu-id="ef565-130">And, you create another dataset to specify the table in the Azure SQL data warehouse that holds the data copied from the blob storage.</span></span> <span data-ttu-id="ef565-131">Zie voor eigenschappen van gegevensset die specifiek voor Azure SQL Data Warehouse zijn, [eigenschappen van gegevensset](#dataset-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="ef565-131">For dataset properties that are specific to Azure SQL Data Warehouse, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="ef565-132">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="ef565-132">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="ef565-133">In het voorbeeld eerder vermeld, gebruikt u BlobSource als een bron- en SqlDWSink als een sink voor de kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="ef565-133">In the example mentioned earlier, you use BlobSource as a source and SqlDWSink as a sink for the copy activity.</span></span> <span data-ttu-id="ef565-134">Op dezelfde manier als u van Azure SQL Data Warehouse naar Azure Blob Storage kopiëren wilt, gebruikt u SqlDWSource en BlobSink in de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="ef565-134">Similarly, if you are copying from Azure SQL Data Warehouse to Azure Blob Storage, you use SqlDWSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="ef565-135">Zie voor activiteitseigenschappen kopiëren die specifiek voor Azure SQL Data Warehouse zijn, [activiteitseigenschappen kopiëren](#copy-activity-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="ef565-135">For copy activity properties that are specific to Azure SQL Data Warehouse, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="ef565-136">Klik op de koppeling in de vorige sectie voor de gegevensopslag voor meer informatie over het gebruik van een gegevensarchief als een bron of een sink.</span><span class="sxs-lookup"><span data-stu-id="ef565-136">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>

<span data-ttu-id="ef565-137">Wanneer u de wizard gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ef565-137">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="ef565-138">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van de JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="ef565-138">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="ef565-139">Zie voor voorbeelden met JSON-definities voor Data Factory-entiteiten die worden gebruikt om gegevens te kopiëren naar/van een Azure SQL Data Warehouse, [JSON voorbeelden](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="ef565-139">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure SQL Data Warehouse, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) section of this article.</span></span>

<span data-ttu-id="ef565-140">De volgende secties bevatten informatie over de JSON-eigenschappen die worden gebruikt voor het definiëren van Data Factory-entiteiten die specifiek voor Azure SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="ef565-140">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure SQL Data Warehouse:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="ef565-141">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="ef565-141">Linked service properties</span></span>
<span data-ttu-id="ef565-142">De volgende tabel bevat een beschrijving voor JSON-elementen die specifiek zijn voor Azure SQL Data Warehouse gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="ef565-142">The following table provides description for JSON elements specific to Azure SQL Data Warehouse linked service.</span></span>

| <span data-ttu-id="ef565-143">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="ef565-143">Property</span></span> | <span data-ttu-id="ef565-144">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ef565-144">Description</span></span> | <span data-ttu-id="ef565-145">Vereist</span><span class="sxs-lookup"><span data-stu-id="ef565-145">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ef565-146">type</span><span class="sxs-lookup"><span data-stu-id="ef565-146">type</span></span> |<span data-ttu-id="ef565-147">De eigenschap type moet worden ingesteld op: **AzureSqlDW**</span><span class="sxs-lookup"><span data-stu-id="ef565-147">The type property must be set to: **AzureSqlDW**</span></span> |<span data-ttu-id="ef565-148">Ja</span><span class="sxs-lookup"><span data-stu-id="ef565-148">Yes</span></span> |
| <span data-ttu-id="ef565-149">connectionString</span><span class="sxs-lookup"><span data-stu-id="ef565-149">connectionString</span></span> |<span data-ttu-id="ef565-150">Geef informatie op die nodig zijn voor het verbinding maken met de Azure SQL Data Warehouse-exemplaar voor de eigenschap connectionString.</span><span class="sxs-lookup"><span data-stu-id="ef565-150">Specify information needed to connect to the Azure SQL Data Warehouse instance for the connectionString property.</span></span> <span data-ttu-id="ef565-151">Alleen basisverificatie wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="ef565-151">Only basic authentication is supported.</span></span> |<span data-ttu-id="ef565-152">Ja</span><span class="sxs-lookup"><span data-stu-id="ef565-152">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="ef565-153">Configureer [Azure SQL Database-Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) en de databaseserver worden [toestaan van Azure Services voor toegang tot de server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span><span class="sxs-lookup"><span data-stu-id="ef565-153">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) and the database server to [allow Azure Services to access the server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="ef565-154">Bovendien configureren als u gegevens naar Azure SQL Data Warehouse kopiëren wilt van buiten Azure met inbegrip van on-premises gegevensbronnen met data factory-gateway, de juiste IP-adresbereik voor de machine die gegevens te naar Azure SQL Data Warehouse verzenden is.</span><span class="sxs-lookup"><span data-stu-id="ef565-154">Additionally, if you are copying data to Azure SQL Data Warehouse from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for the machine that is sending data to Azure SQL Data Warehouse.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="ef565-155">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="ef565-155">Dataset properties</span></span>
<span data-ttu-id="ef565-156">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van de [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="ef565-156">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="ef565-157">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).</span><span class="sxs-lookup"><span data-stu-id="ef565-157">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="ef565-158">De sectie typeProperties verschilt voor elk type gegevensset en bevat informatie over de locatie van de gegevens in het gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="ef565-158">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="ef565-159">De **typeProperties** sectie voor de gegevensset van het type **AzureSqlDWTable** heeft de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="ef565-159">The **typeProperties** section for the dataset of type **AzureSqlDWTable** has the following properties:</span></span>

| <span data-ttu-id="ef565-160">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="ef565-160">Property</span></span> | <span data-ttu-id="ef565-161">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ef565-161">Description</span></span> | <span data-ttu-id="ef565-162">Vereist</span><span class="sxs-lookup"><span data-stu-id="ef565-162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ef565-163">tableName</span><span class="sxs-lookup"><span data-stu-id="ef565-163">tableName</span></span> |<span data-ttu-id="ef565-164">Naam van de tabel of weergave in de Azure SQL Data Warehouse-database waarnaar de gekoppelde service verwijst.</span><span class="sxs-lookup"><span data-stu-id="ef565-164">Name of the table or view in the Azure SQL Data Warehouse database that the linked service refers to.</span></span> |<span data-ttu-id="ef565-165">Ja</span><span class="sxs-lookup"><span data-stu-id="ef565-165">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="ef565-166">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="ef565-166">Copy activity properties</span></span>
<span data-ttu-id="ef565-167">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van activiteiten van de [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="ef565-167">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="ef565-168">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en -beleid zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="ef565-168">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="ef565-169">De Kopieeractiviteit slechts één invoer en slechts één uitvoer produceert.</span><span class="sxs-lookup"><span data-stu-id="ef565-169">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="ef565-170">Terwijl de eigenschappen die beschikbaar zijn in de sectie typeProperties van de activiteit variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="ef565-170">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="ef565-171">Voor de kopieeractiviteit variëren ze, afhankelijk van de typen van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="ef565-171">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

### <a name="sqldwsource"></a><span data-ttu-id="ef565-172">SqlDWSource</span><span class="sxs-lookup"><span data-stu-id="ef565-172">SqlDWSource</span></span>
<span data-ttu-id="ef565-173">Wanneer de bron is van het type **SqlDWSource**, de volgende eigenschappen beschikbaar zijn in **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="ef565-173">When source is of type **SqlDWSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="ef565-174">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="ef565-174">Property</span></span> | <span data-ttu-id="ef565-175">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ef565-175">Description</span></span> | <span data-ttu-id="ef565-176">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="ef565-176">Allowed values</span></span> | <span data-ttu-id="ef565-177">Vereist</span><span class="sxs-lookup"><span data-stu-id="ef565-177">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ef565-178">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="ef565-178">sqlReaderQuery</span></span> |<span data-ttu-id="ef565-179">Gebruik de aangepaste query om gegevens te lezen.</span><span class="sxs-lookup"><span data-stu-id="ef565-179">Use the custom query to read data.</span></span> |<span data-ttu-id="ef565-180">SQL-query-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="ef565-180">SQL query string.</span></span> <span data-ttu-id="ef565-181">Bijvoorbeeld: Selecteer * from MijnTabel.</span><span class="sxs-lookup"><span data-stu-id="ef565-181">For example: select * from MyTable.</span></span> |<span data-ttu-id="ef565-182">Nee</span><span class="sxs-lookup"><span data-stu-id="ef565-182">No</span></span> |
| <span data-ttu-id="ef565-183">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="ef565-183">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="ef565-184">Naam van de opgeslagen procedure die gegevens uit de brontabel leest.</span><span class="sxs-lookup"><span data-stu-id="ef565-184">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="ef565-185">Naam van de opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="ef565-185">Name of the stored procedure.</span></span> <span data-ttu-id="ef565-186">De laatste SQL-instructie moet een SELECT-instructie in de opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="ef565-186">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="ef565-187">Nee</span><span class="sxs-lookup"><span data-stu-id="ef565-187">No</span></span> |
| <span data-ttu-id="ef565-188">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="ef565-188">storedProcedureParameters</span></span> |<span data-ttu-id="ef565-189">Parameters voor de opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="ef565-189">Parameters for the stored procedure.</span></span> |<span data-ttu-id="ef565-190">Naam/waarde-paren.</span><span class="sxs-lookup"><span data-stu-id="ef565-190">Name/value pairs.</span></span> <span data-ttu-id="ef565-191">Namen en hoofdlettergebruik van parameters moeten overeenkomen met de naam en het hoofdlettergebruik van de parameters van opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="ef565-191">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="ef565-192">Nee</span><span class="sxs-lookup"><span data-stu-id="ef565-192">No</span></span> |

<span data-ttu-id="ef565-193">Als de **sqlReaderQuery** is opgegeven voor de SqlDWSource met de kopieerbewerking wordt deze query uitgevoerd op basis van de Azure SQL Data Warehouse-bron om de gegevens te verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="ef565-193">If the **sqlReaderQuery** is specified for the SqlDWSource, the Copy Activity runs this query against the Azure SQL Data Warehouse source to get the data.</span></span>

<span data-ttu-id="ef565-194">U kunt ook een opgeslagen procedure opgeven door te geven de **sqlReaderStoredProcedureName** en **storedProcedureParameters** (als de opgeslagen procedure parameters nodig heeft).</span><span class="sxs-lookup"><span data-stu-id="ef565-194">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="ef565-195">Als u geen sqlReaderQuery of sqlReaderStoredProcedureName opgeeft, worden de kolommen die zijn gedefinieerd in de sectie van de structuur van de gegevensset JSON worden gebruikt voor het bouwen van een query uitvoeren op basis van de Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ef565-195">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query to run against the Azure SQL Data Warehouse.</span></span> <span data-ttu-id="ef565-196">Voorbeeld: `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="ef565-196">Example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="ef565-197">Als de definitie van de gegevensset heeft niet de structuur, worden alle kolommen uit de tabel geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="ef565-197">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

#### <a name="sqldwsource-example"></a><span data-ttu-id="ef565-198">Voorbeeld van SqlDWSource</span><span class="sxs-lookup"><span data-stu-id="ef565-198">SqlDWSource example</span></span>

```JSON
"source": {
    "type": "SqlDWSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```
<span data-ttu-id="ef565-199">**De definitie van de opgeslagen procedure:**</span><span class="sxs-lookup"><span data-stu-id="ef565-199">**The stored procedure definition:**</span></span>

```SQL
CREATE PROCEDURE CopyTestSrcStoredProcedureWithParameters
(
    @stringData varchar(20),
    @identifier int
)
AS
SET NOCOUNT ON;
BEGIN
     select *
     from dbo.UnitTestSrcTable
     where dbo.UnitTestSrcTable.stringData != stringData
    and dbo.UnitTestSrcTable.identifier != identifier
END
GO
```

### <a name="sqldwsink"></a><span data-ttu-id="ef565-200">SqlDWSink</span><span class="sxs-lookup"><span data-stu-id="ef565-200">SqlDWSink</span></span>
<span data-ttu-id="ef565-201">**SqlDWSink** ondersteunt de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="ef565-201">**SqlDWSink** supports the following properties:</span></span>

| <span data-ttu-id="ef565-202">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="ef565-202">Property</span></span> | <span data-ttu-id="ef565-203">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ef565-203">Description</span></span> | <span data-ttu-id="ef565-204">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="ef565-204">Allowed values</span></span> | <span data-ttu-id="ef565-205">Vereist</span><span class="sxs-lookup"><span data-stu-id="ef565-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ef565-206">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="ef565-206">sqlWriterCleanupScript</span></span> |<span data-ttu-id="ef565-207">Geef een query voor de Kopieeractiviteit uitvoeren zodat de gegevens van een bepaald segment wordt opgeschoond.</span><span class="sxs-lookup"><span data-stu-id="ef565-207">Specify a query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="ef565-208">Zie voor meer informatie [herhaalbaarheid sectie](#repeatability-during-copy).</span><span class="sxs-lookup"><span data-stu-id="ef565-208">For details, see [repeatability section](#repeatability-during-copy).</span></span> |<span data-ttu-id="ef565-209">Een query-instructie.</span><span class="sxs-lookup"><span data-stu-id="ef565-209">A query statement.</span></span> |<span data-ttu-id="ef565-210">Nee</span><span class="sxs-lookup"><span data-stu-id="ef565-210">No</span></span> |
| <span data-ttu-id="ef565-211">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="ef565-211">allowPolyBase</span></span> |<span data-ttu-id="ef565-212">Geeft aan of PolyBase (indien van toepassing) gebruiken in plaats van BULKINSERT mechanisme.</span><span class="sxs-lookup"><span data-stu-id="ef565-212">Indicates whether to use PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="ef565-213">**Met PolyBase is de aanbevolen manier om gegevens te laden in SQL Data Warehouse.**</span><span class="sxs-lookup"><span data-stu-id="ef565-213">**Using PolyBase is the recommended way to load data into SQL Data Warehouse.**</span></span> <span data-ttu-id="ef565-214">Zie [gebruik PolyBase gegevens laadt in Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) sectie voor beperkingen en meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ef565-214">See [Use PolyBase to load data into Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) section for constraints and details.</span></span> |<span data-ttu-id="ef565-215">True</span><span class="sxs-lookup"><span data-stu-id="ef565-215">True</span></span> <br/><span data-ttu-id="ef565-216">False (standaard)</span><span class="sxs-lookup"><span data-stu-id="ef565-216">False (default)</span></span> |<span data-ttu-id="ef565-217">Nee</span><span class="sxs-lookup"><span data-stu-id="ef565-217">No</span></span> |
| <span data-ttu-id="ef565-218">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="ef565-218">polyBaseSettings</span></span> |<span data-ttu-id="ef565-219">Een groep met eigenschappen die kunnen worden opgegeven wanneer de **allowPolybase** eigenschap is ingesteld op **true**.</span><span class="sxs-lookup"><span data-stu-id="ef565-219">A group of properties that can be specified when the **allowPolybase** property is set to **true**.</span></span> |&nbsp; |<span data-ttu-id="ef565-220">Nee</span><span class="sxs-lookup"><span data-stu-id="ef565-220">No</span></span> |
| <span data-ttu-id="ef565-221">rejectValue</span><span class="sxs-lookup"><span data-stu-id="ef565-221">rejectValue</span></span> |<span data-ttu-id="ef565-222">Hiermee geeft u het nummer of het percentage van de rijen die kunnen worden afgewezen voordat de query is mislukt.</span><span class="sxs-lookup"><span data-stu-id="ef565-222">Specifies the number or percentage of rows that can be rejected before the query fails.</span></span> <br/><br/><span data-ttu-id="ef565-223">Meer informatie over opties voor het weigeren van de PolyBase in de **argumenten** sectie van [maken EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="ef565-223">Learn more about the PolyBase’s reject options in the **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="ef565-224">0 (standaard), 1, 2...</span><span class="sxs-lookup"><span data-stu-id="ef565-224">0 (default), 1, 2, …</span></span> |<span data-ttu-id="ef565-225">Nee</span><span class="sxs-lookup"><span data-stu-id="ef565-225">No</span></span> |
| <span data-ttu-id="ef565-226">rejectType</span><span class="sxs-lookup"><span data-stu-id="ef565-226">rejectType</span></span> |<span data-ttu-id="ef565-227">Hiermee geeft u op of de optie rejectValue is opgegeven als een letterlijke waarde of een percentage.</span><span class="sxs-lookup"><span data-stu-id="ef565-227">Specifies whether the rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="ef565-228">In waarde (standaard), Percentage</span><span class="sxs-lookup"><span data-stu-id="ef565-228">Value (default), Percentage</span></span> |<span data-ttu-id="ef565-229">Nee</span><span class="sxs-lookup"><span data-stu-id="ef565-229">No</span></span> |
| <span data-ttu-id="ef565-230">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="ef565-230">rejectSampleValue</span></span> |<span data-ttu-id="ef565-231">Bepaalt het aantal rijen om op te halen voordat de PolyBase berekent het percentage van de geweigerde rijen opnieuw.</span><span class="sxs-lookup"><span data-stu-id="ef565-231">Determines the number of rows to retrieve before the PolyBase recalculates the percentage of rejected rows.</span></span> |<span data-ttu-id="ef565-232">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="ef565-232">1, 2, …</span></span> |<span data-ttu-id="ef565-233">Ja, als **rejectType** is **percentage**</span><span class="sxs-lookup"><span data-stu-id="ef565-233">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="ef565-234">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="ef565-234">useTypeDefault</span></span> |<span data-ttu-id="ef565-235">Geeft aan hoe de ontbrekende waarden in tekstbestanden met scheidingstekens verwerken wanneer PolyBase gegevens uit het tekstbestand ophaalt.</span><span class="sxs-lookup"><span data-stu-id="ef565-235">Specifies how to handle missing values in delimited text files when PolyBase retrieves data from the text file.</span></span><br/><br/><span data-ttu-id="ef565-236">Meer informatie over deze eigenschap in de sectie argumenten [maken EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="ef565-236">Learn more about this property from the Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="ef565-237">True, False (standaard)</span><span class="sxs-lookup"><span data-stu-id="ef565-237">True, False (default)</span></span> |<span data-ttu-id="ef565-238">Nee</span><span class="sxs-lookup"><span data-stu-id="ef565-238">No</span></span> |
| <span data-ttu-id="ef565-239">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="ef565-239">writeBatchSize</span></span> |<span data-ttu-id="ef565-240">Gegevens invoegen in de SQL-tabel wanneer de buffergrootte writeBatchSize bereikt</span><span class="sxs-lookup"><span data-stu-id="ef565-240">Inserts data into the SQL table when the buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="ef565-241">Geheel getal (aantal rijen)</span><span class="sxs-lookup"><span data-stu-id="ef565-241">Integer (number of rows)</span></span> |<span data-ttu-id="ef565-242">Nee (standaard: 10000)</span><span class="sxs-lookup"><span data-stu-id="ef565-242">No (default: 10000)</span></span> |
| <span data-ttu-id="ef565-243">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="ef565-243">writeBatchTimeout</span></span> |<span data-ttu-id="ef565-244">Wachttijd voor de batch-insert-bewerking te voltooien voordat er een optreedt time-out.</span><span class="sxs-lookup"><span data-stu-id="ef565-244">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="ef565-245">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="ef565-245">timespan</span></span><br/><br/> <span data-ttu-id="ef565-246">Voorbeeld: "00: 30:00 ' (30 minuten).</span><span class="sxs-lookup"><span data-stu-id="ef565-246">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="ef565-247">Nee</span><span class="sxs-lookup"><span data-stu-id="ef565-247">No</span></span> |

#### <a name="sqldwsink-example"></a><span data-ttu-id="ef565-248">Voorbeeld van SqlDWSink</span><span class="sxs-lookup"><span data-stu-id="ef565-248">SqlDWSink example</span></span>

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true
}
```

## <a name="use-polybase-to-load-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="ef565-249">Gebruik PolyBase gegevens laadt in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ef565-249">Use PolyBase to load data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="ef565-250">Met behulp van  **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)**  is een efficiënte manier van het laden van grote hoeveelheid gegevens in Azure SQL Data Warehouse met hoge doorvoer.</span><span class="sxs-lookup"><span data-stu-id="ef565-250">Using **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** is an efficient way of loading large amount of data into Azure SQL Data Warehouse with high throughput.</span></span> <span data-ttu-id="ef565-251">Met behulp van PolyBase in plaats van het standaardmechanisme voor BULKINSERT ziet u een groot voordeel in de doorvoer.</span><span class="sxs-lookup"><span data-stu-id="ef565-251">You can see a large gain in the throughput by using PolyBase instead of the default BULKINSERT mechanism.</span></span> <span data-ttu-id="ef565-252">Zie [prestaties referentienummer kopiëren](data-factory-copy-activity-performance.md#performance-reference) met gedetailleerde vergelijking.</span><span class="sxs-lookup"><span data-stu-id="ef565-252">See [copy performance reference number](data-factory-copy-activity-performance.md#performance-reference) with detailed comparison.</span></span> <span data-ttu-id="ef565-253">Zie voor een overzicht met een gebruiksvoorbeeld [1 TB laden in Azure SQL Data Warehouse onder 15 minuten met Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span><span class="sxs-lookup"><span data-stu-id="ef565-253">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

* <span data-ttu-id="ef565-254">Als de brongegevens **Azure Blob- of Azure Data Lake Store**, en de indeling is compatibel met PolyBase, kunt u rechtstreeks kopiëren naar Azure SQL Data Warehouse met PolyBase.</span><span class="sxs-lookup"><span data-stu-id="ef565-254">If your source data is in **Azure Blob or Azure Data Lake Store**, and the format is compatible with PolyBase, you can directly copy to Azure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="ef565-255">Zie  **[Direct kopiëren met PolyBase](#direct-copy-using-polybase)**  met details.</span><span class="sxs-lookup"><span data-stu-id="ef565-255">See **[Direct copy using PolyBase](#direct-copy-using-polybase)** with details.</span></span>
* <span data-ttu-id="ef565-256">Als uw brongegevensarchief en de indeling wordt oorspronkelijk niet ondersteund door PolyBase, kunt u de  **[gefaseerde kopiëren met PolyBase](#staged-copy-using-polybase)**  in plaats daarvan functie.</span><span class="sxs-lookup"><span data-stu-id="ef565-256">If your source data store and format is not originally supported by PolyBase, you can use the **[Staged Copy using PolyBase](#staged-copy-using-polybase)** feature instead.</span></span> <span data-ttu-id="ef565-257">Dit biedt u ook betere doorvoer door automatisch converteren van de gegevens naar de PolyBase-compatibele indeling en opslaan van gegevens in Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="ef565-257">It also provides you better throughput by automatically converting the data into PolyBase-compatible format and storing the data in Azure Blob storage.</span></span> <span data-ttu-id="ef565-258">Vervolgens worden gegevens geladen in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ef565-258">It then loads data into SQL Data Warehouse.</span></span>

<span data-ttu-id="ef565-259">Stel de `allowPolyBase` eigenschap **true** zoals weergegeven in het volgende voorbeeld voor Azure Data Factory PolyBase gebruiken om gegevens te kopiëren naar Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ef565-259">Set the `allowPolyBase` property to **true** as shown in the following example for Azure Data Factory to use PolyBase to copy data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="ef565-260">Wanneer u allowPolyBase ingesteld op true, kunt u PolyBase specifieke eigenschappen met behulp van de `polyBaseSettings` eigenschappengroep.</span><span class="sxs-lookup"><span data-stu-id="ef565-260">When you set allowPolyBase to true, you can specify PolyBase specific properties using the `polyBaseSettings` property group.</span></span> <span data-ttu-id="ef565-261">Zie de [SqlDWSink](#SqlDWSink) sectie voor meer informatie over de eigenschappen die u met polyBaseSettings gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="ef565-261">see the [SqlDWSink](#SqlDWSink) section for details about properties that you can use with polyBaseSettings.</span></span>

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true,
    "polyBaseSettings":
    {
        "rejectType": "percentage",
        "rejectValue": 10.0,
        "rejectSampleValue": 100,
        "useTypeDefault": true
    }
}
```

### <a name="direct-copy-using-polybase"></a><span data-ttu-id="ef565-262">Directe kopiëren met PolyBase</span><span class="sxs-lookup"><span data-stu-id="ef565-262">Direct copy using PolyBase</span></span>
<span data-ttu-id="ef565-263">SQL Data Warehouse PolyBase ondersteuning rechtstreeks voor Azure-Blob en Azure Data Lake Store (met behulp van de service-principal) als bron en met vereisten voor een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="ef565-263">SQL Data Warehouse PolyBase directly support Azure Blob and Azure Data Lake Store (using service principal) as source and with specific file format requirements.</span></span> <span data-ttu-id="ef565-264">Als de brongegevens voldoet aan de criteria die in deze sectie beschreven, kunt u rechtstreeks van brongegevensarchief kopiëren naar Azure SQL Data Warehouse met PolyBase.</span><span class="sxs-lookup"><span data-stu-id="ef565-264">If your source data meets the criteria described in this section, you can directly copy from source data store to Azure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="ef565-265">Anders kunt u [gefaseerde kopiëren met PolyBase](#staged-copy-using-polybase).</span><span class="sxs-lookup"><span data-stu-id="ef565-265">Otherwise, you can use [Staged Copy using PolyBase](#staged-copy-using-polybase).</span></span>

> [!TIP]
> <span data-ttu-id="ef565-266">Om gegevens te kopiëren van Data Lake Store met SQL Data Warehouse efficiënt, meer wilt weten van [Azure Data Factory kunt u zelfs gemakkelijker en handige om inzichten bloot te van gegevens bij het gebruik van Data Lake Store met SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="ef565-266">To copy data from Data Lake Store to SQL Data Warehouse efficiently, learn more from [Azure Data Factory makes it even easier and convenient to uncover insights from data when using Data Lake Store with SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).</span></span>

<span data-ttu-id="ef565-267">Als niet aan de vereisten wordt voldaan, wordt Azure Data Factory controleert de instellingen en automatisch terugvalt op het BULKINSERT mechanisme voor de verplaatsing van gegevens.</span><span class="sxs-lookup"><span data-stu-id="ef565-267">If the requirements are not met, Azure Data Factory checks the settings and automatically falls back to the BULKINSERT mechanism for the data movement.</span></span>

1. <span data-ttu-id="ef565-268">**Bron gekoppelde service** is van het type: **AzureStorage** of **AzureDataLakeStore met verificatie van de service-principal**.</span><span class="sxs-lookup"><span data-stu-id="ef565-268">**Source linked service** is of type: **AzureStorage** or **AzureDataLakeStore with service principal authentication**.</span></span>  
2. <span data-ttu-id="ef565-269">De **invoergegevensset** is van het type: **AzureBlob** of **AzureDataLakeStore**, en de indeling Typ onder `type` eigenschappen is **OrcFormat**, of **TextFormat** met de volgende configuraties:</span><span class="sxs-lookup"><span data-stu-id="ef565-269">The **input dataset** is of type: **AzureBlob** or **AzureDataLakeStore**, and the format type under `type` properties is **OrcFormat**, or **TextFormat** with the following configurations:</span></span>

   1. <span data-ttu-id="ef565-270">`rowDelimiter`moet  **\n** .</span><span class="sxs-lookup"><span data-stu-id="ef565-270">`rowDelimiter` must be **\n**.</span></span>
   2. <span data-ttu-id="ef565-271">`nullValue`is ingesteld op **lege tekenreeks** (""), of `treatEmptyAsNull` is ingesteld op **true**.</span><span class="sxs-lookup"><span data-stu-id="ef565-271">`nullValue` is set to **empty string** (""), or `treatEmptyAsNull` is set to **true**.</span></span>
   3. <span data-ttu-id="ef565-272">`encodingName`is ingesteld op **utf-8**, namelijk **standaard** waarde.</span><span class="sxs-lookup"><span data-stu-id="ef565-272">`encodingName` is set to **utf-8**, which is **default** value.</span></span>
   4. <span data-ttu-id="ef565-273">`escapeChar`, `quoteChar`, `firstRowAsHeader`, en `skipLineCount` zijn niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="ef565-273">`escapeChar`, `quoteChar`, `firstRowAsHeader`, and `skipLineCount` are not specified.</span></span>
   5. <span data-ttu-id="ef565-274">`compression`kan **geen compressie**, **GZip**, of **Deflate**.</span><span class="sxs-lookup"><span data-stu-id="ef565-274">`compression` can be **no compression**, **GZip**, or **Deflate**.</span></span>

    ```JSON
    "typeProperties": {
       "folderPath": "<blobpath>",
       "format": {
           "type": "TextFormat",     
           "columnDelimiter": "<any delimiter>",
           "rowDelimiter": "\n",       
           "nullValue": "",           
           "encodingName": "utf-8"    
       },
       "compression": {  
           "type": "GZip",  
           "level": "Optimal"  
       }  
    },
    ```

3. <span data-ttu-id="ef565-275">Er is geen `skipHeaderLineCount` onder **BlobSource** of **AzureDataLakeStore** voor de kopieeractiviteit in de pijplijn.</span><span class="sxs-lookup"><span data-stu-id="ef565-275">There is no `skipHeaderLineCount` setting under **BlobSource** or **AzureDataLakeStore** for the Copy activity in the pipeline.</span></span>
4. <span data-ttu-id="ef565-276">Er is geen `sliceIdentifierColumnName` onder **SqlDWSink** voor de kopieeractiviteit in de pijplijn.</span><span class="sxs-lookup"><span data-stu-id="ef565-276">There is no `sliceIdentifierColumnName` setting under **SqlDWSink** for the Copy activity in the pipeline.</span></span> <span data-ttu-id="ef565-277">(PolyBase zorgt ervoor dat alle gegevens worden bijgewerkt of niet in een enkel uitvoering bijgewerkt wordt.</span><span class="sxs-lookup"><span data-stu-id="ef565-277">(PolyBase guarantees that all data is updated or nothing is updated in a single run.</span></span> <span data-ttu-id="ef565-278">Als u de **herhaalbaarheid**, kunt u `sqlWriterCleanupScript`).</span><span class="sxs-lookup"><span data-stu-id="ef565-278">To achieve **repeatability**, you could use `sqlWriterCleanupScript`).</span></span>
5. <span data-ttu-id="ef565-279">Er is geen `columnMapping` wordt gebruikt in de bijbehorende in kopie activiteit.</span><span class="sxs-lookup"><span data-stu-id="ef565-279">There is no `columnMapping` being used in the associated in Copy activity.</span></span>

### <a name="staged-copy-using-polybase"></a><span data-ttu-id="ef565-280">Gefaseerde kopiëren met PolyBase</span><span class="sxs-lookup"><span data-stu-id="ef565-280">Staged Copy using PolyBase</span></span>
<span data-ttu-id="ef565-281">Als de brongegevens niet voldoet aan de criteria die zijn geïntroduceerd in de vorige sectie, kunt u kopiëren van gegevens via een tussentijdse staging Azure Blob Storage (kan niet voor Premium-opslag) inschakelen.</span><span class="sxs-lookup"><span data-stu-id="ef565-281">When your source data doesn’t meet the criteria introduced in the previous section, you can enable copying data via an interim staging Azure Blob Storage (cannot be Premium Storage).</span></span> <span data-ttu-id="ef565-282">In dit geval voert Azure Data Factory automatisch transformaties op de gegevens die moeten voldoen aan de vereisten van de indeling van PolyBase gegevens en gebruik vervolgens PolyBase om gegevens te laden in SQL Data Warehouse en op de laatste opschoning uw tijdelijke gegevens van de Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="ef565-282">In this case, Azure Data Factory automatically performs transformations on the data to meet data format requirements of PolyBase, then use PolyBase to load data into SQL Data Warehouse, and at last clean-up your temp data from the Blob storage.</span></span> <span data-ttu-id="ef565-283">Zie [kopie gefaseerde](data-factory-copy-activity-performance.md#staged-copy) voor meer informatie over de werking kopiëren van gegevens via een gefaseerde installatie Azure-Blob in het algemeen.</span><span class="sxs-lookup"><span data-stu-id="ef565-283">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details on how copying data via a staging Azure Blob works in general.</span></span>

> [!NOTE]
> <span data-ttu-id="ef565-284">Wanneer het kopiëren van gegevens uit een on-premises gegevens opslaan in Azure SQL Data Warehouse met PolyBase en fasering, als uw Data Management Gateway-versie lager dan 2.4 is Java Runtime Environment (Java Runtime Environment) is vereist op uw computer met de gateway die wordt gebruikt voor het omzetten van de brongegevens naar de juiste indeling.</span><span class="sxs-lookup"><span data-stu-id="ef565-284">When copying data from an on-prem data store into Azure SQL Data Warehouse using PolyBase and staging, if your Data Management Gateway version is below 2.4, JRE (Java Runtime Environment) is required on your gateway machine that is used to transform your source data into proper format.</span></span> <span data-ttu-id="ef565-285">Stelt dat u een upgrade van uw gateway uit naar de meest recente uitvoeren om te voorkomen dat deze afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="ef565-285">Suggest you upgrade your gateway to the latest to avoid such dependency.</span></span>
>

<span data-ttu-id="ef565-286">Deze functie wilt gebruiken, maakt u een [gekoppelde Azure Storage-service](data-factory-azure-blob-connector.md#azure-storage-linked-service) die verwijst naar de Azure Storage-Account met de tussentijdse blobopslag, geeft u de `enableStaging` en `stagingSettings` eigenschappen voor de Kopieeractiviteit, zoals wordt weergegeven in de volgende code:</span><span class="sxs-lookup"><span data-stu-id="ef565-286">To use this feature, create an [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) that refers to the Azure Storage Account that has the interim blob storage, then specify the `enableStaging` and `stagingSettings` properties for the Copy Activity as shown in the following code:</span></span>

```json
"activities":[  
{
    "name": "Sample copy activity from SQL Server to SQL Data Warehouse via PolyBase",
    "type": "Copy",
    "inputs": [{ "name": "OnpremisesSQLServerInput" }],
    "outputs": [{ "name": "AzureSQLDWOutput" }],
    "typeProperties": {
        "source": {
            "type": "SqlSource",
        },
        "sink": {
            "type": "SqlDwSink",
            "allowPolyBase": true
        },
        "enableStaging": true,
        "stagingSettings": {
            "linkedServiceName": "MyStagingBlob"
        }
    }
}
]
```

## <a name="best-practices-when-using-polybase"></a><span data-ttu-id="ef565-287">Aanbevolen procedures voor met PolyBase</span><span class="sxs-lookup"><span data-stu-id="ef565-287">Best practices when using PolyBase</span></span>
<span data-ttu-id="ef565-288">De volgende secties bevatten aanvullende aanbevolen procedures voor de waarden die worden vermeld in [aanbevolen procedures voor Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="ef565-288">The following sections provide additional best practices to the ones that are mentioned in [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span></span>

### <a name="required-database-permission"></a><span data-ttu-id="ef565-289">Vereiste databasemachtiging</span><span class="sxs-lookup"><span data-stu-id="ef565-289">Required database permission</span></span>
<span data-ttu-id="ef565-290">Voor het gebruik van PolyBase, moet de gebruiker wordt gebruikt om gegevens te laden in SQL Data Warehouse heeft de [machtiging "Beheer"](https://msdn.microsoft.com/library/ms191291.aspx) op de doeldatabase.</span><span class="sxs-lookup"><span data-stu-id="ef565-290">To use PolyBase, it requires the user being used to load data into SQL Data Warehouse has the ["CONTROL" permission](https://msdn.microsoft.com/library/ms191291.aspx) on the target database.</span></span> <span data-ttu-id="ef565-291">Een manier om dat te bereiken is het toevoegen van die gebruiker als lid van de rol 'db_owner'.</span><span class="sxs-lookup"><span data-stu-id="ef565-291">One way to achieve that is to add that user as a member of "db_owner" role.</span></span> <span data-ttu-id="ef565-292">Meer informatie over hoe dat door de volgende [in deze sectie](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span><span class="sxs-lookup"><span data-stu-id="ef565-292">Learn how to do that by following [this section](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span></span>

### <a name="row-size-and-data-type-limitation"></a><span data-ttu-id="ef565-293">Typ de beperking rijgrootte en gegevens</span><span class="sxs-lookup"><span data-stu-id="ef565-293">Row size and data type limitation</span></span>
<span data-ttu-id="ef565-294">Polybase-belastingen zijn beperkt tot laden rijen beide kleiner is dan **1 MB** en kan niet worden geladen VARCHR(MAX), NVARCHAR(MAX) of VARBINARY(MAX).</span><span class="sxs-lookup"><span data-stu-id="ef565-294">Polybase loads are limited to loading rows both smaller than **1 MB** and cannot load to VARCHR(MAX), NVARCHAR(MAX) or VARBINARY(MAX).</span></span> <span data-ttu-id="ef565-295">Raadpleeg [hier](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span><span class="sxs-lookup"><span data-stu-id="ef565-295">Refer to [here](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span></span>

<span data-ttu-id="ef565-296">Als u hebt de brongegevens met rijen van de omvang is groter dan 1 MB, wilt u mogelijk de brontabellen verticaal gesplitst in verschillende kleine netwerken waarbij de grootste rijgrootte van elk van de limiet niet overschrijdt.</span><span class="sxs-lookup"><span data-stu-id="ef565-296">If you have source data with rows of size greater than 1 MB, you may want to split the source tables vertically into several small ones where the largest row size of each of them does not exceed the limit.</span></span> <span data-ttu-id="ef565-297">De tabellen voor kleinere kunnen vervolgens worden geladen met PolyBase en samengevoegd in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ef565-297">The smaller tables can then be loaded using PolyBase and merged together in Azure SQL Data Warehouse.</span></span>

### <a name="sql-data-warehouse-resource-class"></a><span data-ttu-id="ef565-298">De bronklasse SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ef565-298">SQL Data Warehouse resource class</span></span>
<span data-ttu-id="ef565-299">Overweeg om de best mogelijke doorvoer behalen, grotere bronklasse toewijzen aan de gebruiker wordt gebruikt om gegevens te laden in SQL Data Warehouse met PolyBase.</span><span class="sxs-lookup"><span data-stu-id="ef565-299">To achieve best possible throughput, consider to assign larger resource class to the user being used to load data into SQL Data Warehouse via PolyBase.</span></span> <span data-ttu-id="ef565-300">Meer informatie over hoe dat door de volgende [wijzigen van een voorbeeld van een gebruiker resource klasse](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="ef565-300">Learn how to do that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

### <a name="tablename-in-azure-sql-data-warehouse"></a><span data-ttu-id="ef565-301">tableName in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ef565-301">tableName in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="ef565-302">De volgende tabel bevat voorbeelden op het opgeven van de **tableName** eigenschap in de gegevensset JSON voor verschillende combinaties van schema en de tabelnaam.</span><span class="sxs-lookup"><span data-stu-id="ef565-302">The following table provides examples on how to specify the **tableName** property in dataset JSON for various combinations of schema and table name.</span></span>

| <span data-ttu-id="ef565-303">DB Schema</span><span class="sxs-lookup"><span data-stu-id="ef565-303">DB Schema</span></span> | <span data-ttu-id="ef565-304">De tabelnaam van de</span><span class="sxs-lookup"><span data-stu-id="ef565-304">Table name</span></span> | <span data-ttu-id="ef565-305">JSON-eigenschap tableName</span><span class="sxs-lookup"><span data-stu-id="ef565-305">tableName JSON property</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ef565-306">dbo</span><span class="sxs-lookup"><span data-stu-id="ef565-306">dbo</span></span> |<span data-ttu-id="ef565-307">MyTable</span><span class="sxs-lookup"><span data-stu-id="ef565-307">MyTable</span></span> |<span data-ttu-id="ef565-308">MyTable of dbo. MyTable of [dbo]. [MijnTabel]</span><span class="sxs-lookup"><span data-stu-id="ef565-308">MyTable or dbo.MyTable or [dbo].[MyTable]</span></span> |
| <span data-ttu-id="ef565-309">dbo1</span><span class="sxs-lookup"><span data-stu-id="ef565-309">dbo1</span></span> |<span data-ttu-id="ef565-310">MyTable</span><span class="sxs-lookup"><span data-stu-id="ef565-310">MyTable</span></span> |<span data-ttu-id="ef565-311">dbo1. MyTable of [dbo1]. [MijnTabel]</span><span class="sxs-lookup"><span data-stu-id="ef565-311">dbo1.MyTable or [dbo1].[MyTable]</span></span> |
| <span data-ttu-id="ef565-312">dbo</span><span class="sxs-lookup"><span data-stu-id="ef565-312">dbo</span></span> |<span data-ttu-id="ef565-313">My.Table</span><span class="sxs-lookup"><span data-stu-id="ef565-313">My.Table</span></span> |<span data-ttu-id="ef565-314">[My.Table] of [dbo]. [My.Table]</span><span class="sxs-lookup"><span data-stu-id="ef565-314">[My.Table] or [dbo].[My.Table]</span></span> |
| <span data-ttu-id="ef565-315">dbo1</span><span class="sxs-lookup"><span data-stu-id="ef565-315">dbo1</span></span> |<span data-ttu-id="ef565-316">My.Table</span><span class="sxs-lookup"><span data-stu-id="ef565-316">My.Table</span></span> |<span data-ttu-id="ef565-317">[dbo1]. [My.Table]</span><span class="sxs-lookup"><span data-stu-id="ef565-317">[dbo1].[My.Table]</span></span> |

<span data-ttu-id="ef565-318">Als u de volgende fout ziet, is het mogelijk een probleem met de waarde die u hebt opgegeven voor de eigenschap tableName.</span><span class="sxs-lookup"><span data-stu-id="ef565-318">If you see the following error, it could be an issue with the value you specified for the tableName property.</span></span> <span data-ttu-id="ef565-319">Zie de tabel voor de juiste manier waarden opgeven voor de eigenschap tableName JSON.</span><span class="sxs-lookup"><span data-stu-id="ef565-319">See the table for the correct way to specify values for the tableName JSON property.</span></span>  

```
Type=System.Data.SqlClient.SqlException,Message=Invalid object name 'stg.Account_test'.,Source=.Net SqlClient Data Provider
```

### <a name="columns-with-default-values"></a><span data-ttu-id="ef565-320">Kolommen met standaardwaarden</span><span class="sxs-lookup"><span data-stu-id="ef565-320">Columns with default values</span></span>
<span data-ttu-id="ef565-321">PolyBase-functie in de Data Factory accepteert alleen op dit moment is hetzelfde aantal kolommen in de doeltabel.</span><span class="sxs-lookup"><span data-stu-id="ef565-321">Currently, PolyBase feature in Data Factory only accepts the same number of columns as in the target table.</span></span> <span data-ttu-id="ef565-322">Stel, u hebt een tabel met vier kolommen en een ervan is gedefinieerd met een standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="ef565-322">Say, you have a table with four columns and one of them is defined with a default value.</span></span> <span data-ttu-id="ef565-323">De invoergegevens moet nog steeds vier kolommen bevatten.</span><span class="sxs-lookup"><span data-stu-id="ef565-323">The input data should still contain four columns.</span></span> <span data-ttu-id="ef565-324">Een invoergegevensset 3 kolommen bieden zou resulteert in een fout die vergelijkbaar is met het volgende bericht:</span><span class="sxs-lookup"><span data-stu-id="ef565-324">Providing a 3-column input dataset would yield an error similar to the following message:</span></span>

```
All columns of the table must be specified in the INSERT BULK statement.
```
<span data-ttu-id="ef565-325">NULL-waarde is een speciale vorm van de standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="ef565-325">NULL value is a special form of default value.</span></span> <span data-ttu-id="ef565-326">Als de kolom waarvoor null is toegestaan, kan de invoergegevens (in blob) voor de kolom leeg zijn (kan niet worden ontbreekt uit de invoer gegevensset).</span><span class="sxs-lookup"><span data-stu-id="ef565-326">If the column is nullable, the input data (in blob) for that column could be empty (cannot be missing from the input dataset).</span></span> <span data-ttu-id="ef565-327">PolyBase voegt NULL zijn voor deze in de Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ef565-327">PolyBase inserts NULL for them in the Azure SQL Data Warehouse.</span></span>  

## <a name="auto-table-creation"></a><span data-ttu-id="ef565-328">Maken van de tabel automatisch</span><span class="sxs-lookup"><span data-stu-id="ef565-328">Auto table creation</span></span>
<span data-ttu-id="ef565-329">Als u Wizard kopiëren gebruikt voor gegevens van SQL Server of Azure SQL Database kopiëren naar Azure SQL Data Warehouse en de tabel die overeenkomt met de brontabel niet in het doelarchief bestaat, maken Data Factory automatisch in de tabel in het datawarehouse met behulp van de bron-tabelschema.</span><span class="sxs-lookup"><span data-stu-id="ef565-329">If you are using Copy Wizard to copy data from SQL Server or Azure SQL Database to Azure SQL Data Warehouse and the table that corresponds to the source table does not exist in the destination store, Data Factory can automatically create the table in the data warehouse by using the source table schema.</span></span>

<span data-ttu-id="ef565-330">Data Factory maakt in de tabel in het doelarchief met dezelfde tabelnaam in het gegevensarchief van de bron.</span><span class="sxs-lookup"><span data-stu-id="ef565-330">Data Factory creates the table in the destination store with the same table name in the source data store.</span></span> <span data-ttu-id="ef565-331">De gegevenstypen voor kolommen worden gekozen op basis van de toewijzing van het volgende type zijn.</span><span class="sxs-lookup"><span data-stu-id="ef565-331">The data types for columns are chosen based on the following type mapping.</span></span> <span data-ttu-id="ef565-332">Indien nodig, voert deze typeconversies om op te lossen eventuele incompatibiliteiten tussen bron- en doelserver stores.</span><span class="sxs-lookup"><span data-stu-id="ef565-332">If needed, it performs type conversions to fix any incompatibilities between source and destination stores.</span></span> <span data-ttu-id="ef565-333">Round Robin tabeldistributie worden ook gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ef565-333">It also uses Round Robin table distribution.</span></span>

| <span data-ttu-id="ef565-334">Type gegevensbron SQL Database-kolom</span><span class="sxs-lookup"><span data-stu-id="ef565-334">Source SQL Database column type</span></span> | <span data-ttu-id="ef565-335">Doel-SQL DW-kolomtype (de maximale grootte)</span><span class="sxs-lookup"><span data-stu-id="ef565-335">Destination SQL DW column type (size limitation)</span></span> |
| --- | --- |
| <span data-ttu-id="ef565-336">int</span><span class="sxs-lookup"><span data-stu-id="ef565-336">Int</span></span> | <span data-ttu-id="ef565-337">int</span><span class="sxs-lookup"><span data-stu-id="ef565-337">Int</span></span> |
| <span data-ttu-id="ef565-338">BigInt</span><span class="sxs-lookup"><span data-stu-id="ef565-338">BigInt</span></span> | <span data-ttu-id="ef565-339">BigInt</span><span class="sxs-lookup"><span data-stu-id="ef565-339">BigInt</span></span> |
| <span data-ttu-id="ef565-340">SmallInt</span><span class="sxs-lookup"><span data-stu-id="ef565-340">SmallInt</span></span> | <span data-ttu-id="ef565-341">SmallInt</span><span class="sxs-lookup"><span data-stu-id="ef565-341">SmallInt</span></span> |
| <span data-ttu-id="ef565-342">TinyInt</span><span class="sxs-lookup"><span data-stu-id="ef565-342">TinyInt</span></span> | <span data-ttu-id="ef565-343">TinyInt</span><span class="sxs-lookup"><span data-stu-id="ef565-343">TinyInt</span></span> |
| <span data-ttu-id="ef565-344">bits</span><span class="sxs-lookup"><span data-stu-id="ef565-344">Bit</span></span> | <span data-ttu-id="ef565-345">bits</span><span class="sxs-lookup"><span data-stu-id="ef565-345">Bit</span></span> |
| <span data-ttu-id="ef565-346">Decimale</span><span class="sxs-lookup"><span data-stu-id="ef565-346">Decimal</span></span> | <span data-ttu-id="ef565-347">Decimale</span><span class="sxs-lookup"><span data-stu-id="ef565-347">Decimal</span></span> |
| <span data-ttu-id="ef565-348">numerieke</span><span class="sxs-lookup"><span data-stu-id="ef565-348">Numeric</span></span> | <span data-ttu-id="ef565-349">Decimale</span><span class="sxs-lookup"><span data-stu-id="ef565-349">Decimal</span></span> |
| <span data-ttu-id="ef565-350">Float</span><span class="sxs-lookup"><span data-stu-id="ef565-350">Float</span></span> | <span data-ttu-id="ef565-351">Float</span><span class="sxs-lookup"><span data-stu-id="ef565-351">Float</span></span> |
| <span data-ttu-id="ef565-352">Money</span><span class="sxs-lookup"><span data-stu-id="ef565-352">Money</span></span> | <span data-ttu-id="ef565-353">Money</span><span class="sxs-lookup"><span data-stu-id="ef565-353">Money</span></span> |
| <span data-ttu-id="ef565-354">Real</span><span class="sxs-lookup"><span data-stu-id="ef565-354">Real</span></span> | <span data-ttu-id="ef565-355">Real</span><span class="sxs-lookup"><span data-stu-id="ef565-355">Real</span></span> |
| <span data-ttu-id="ef565-356">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="ef565-356">SmallMoney</span></span> | <span data-ttu-id="ef565-357">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="ef565-357">SmallMoney</span></span> |
| <span data-ttu-id="ef565-358">Binaire</span><span class="sxs-lookup"><span data-stu-id="ef565-358">Binary</span></span> | <span data-ttu-id="ef565-359">Binaire</span><span class="sxs-lookup"><span data-stu-id="ef565-359">Binary</span></span> |
| <span data-ttu-id="ef565-360">varbinary</span><span class="sxs-lookup"><span data-stu-id="ef565-360">Varbinary</span></span> | <span data-ttu-id="ef565-361">Varbinary (maximaal 8000)</span><span class="sxs-lookup"><span data-stu-id="ef565-361">Varbinary (up to 8000)</span></span> |
| <span data-ttu-id="ef565-362">Date</span><span class="sxs-lookup"><span data-stu-id="ef565-362">Date</span></span> | <span data-ttu-id="ef565-363">Date</span><span class="sxs-lookup"><span data-stu-id="ef565-363">Date</span></span> |
| <span data-ttu-id="ef565-364">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="ef565-364">DateTime</span></span> | <span data-ttu-id="ef565-365">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="ef565-365">DateTime</span></span> |
| <span data-ttu-id="ef565-366">DateTime2</span><span class="sxs-lookup"><span data-stu-id="ef565-366">DateTime2</span></span> | <span data-ttu-id="ef565-367">DateTime2</span><span class="sxs-lookup"><span data-stu-id="ef565-367">DateTime2</span></span> |
| <span data-ttu-id="ef565-368">Time</span><span class="sxs-lookup"><span data-stu-id="ef565-368">Time</span></span> | <span data-ttu-id="ef565-369">Time</span><span class="sxs-lookup"><span data-stu-id="ef565-369">Time</span></span> |
| <span data-ttu-id="ef565-370">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="ef565-370">DateTimeOffset</span></span> | <span data-ttu-id="ef565-371">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="ef565-371">DateTimeOffset</span></span> |
| <span data-ttu-id="ef565-372">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="ef565-372">SmallDateTime</span></span> | <span data-ttu-id="ef565-373">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="ef565-373">SmallDateTime</span></span> |
| <span data-ttu-id="ef565-374">Tekst</span><span class="sxs-lookup"><span data-stu-id="ef565-374">Text</span></span> | <span data-ttu-id="ef565-375">Varchar (maximaal 8000)</span><span class="sxs-lookup"><span data-stu-id="ef565-375">Varchar (up to 8000)</span></span> |
| <span data-ttu-id="ef565-376">NText</span><span class="sxs-lookup"><span data-stu-id="ef565-376">NText</span></span> | <span data-ttu-id="ef565-377">NVarChar (maximaal 4000)</span><span class="sxs-lookup"><span data-stu-id="ef565-377">NVarChar (up to 4000)</span></span> |
| <span data-ttu-id="ef565-378">Installatiekopie</span><span class="sxs-lookup"><span data-stu-id="ef565-378">Image</span></span> | <span data-ttu-id="ef565-379">VarBinary (maximaal 8000)</span><span class="sxs-lookup"><span data-stu-id="ef565-379">VarBinary (up to 8000)</span></span> |
| <span data-ttu-id="ef565-380">UniqueIdentifier</span><span class="sxs-lookup"><span data-stu-id="ef565-380">UniqueIdentifier</span></span> | <span data-ttu-id="ef565-381">UniqueIdentifier</span><span class="sxs-lookup"><span data-stu-id="ef565-381">UniqueIdentifier</span></span> |
| <span data-ttu-id="ef565-382">CHAR</span><span class="sxs-lookup"><span data-stu-id="ef565-382">Char</span></span> | <span data-ttu-id="ef565-383">CHAR</span><span class="sxs-lookup"><span data-stu-id="ef565-383">Char</span></span> |
| <span data-ttu-id="ef565-384">NChar</span><span class="sxs-lookup"><span data-stu-id="ef565-384">NChar</span></span> | <span data-ttu-id="ef565-385">NChar</span><span class="sxs-lookup"><span data-stu-id="ef565-385">NChar</span></span> |
| <span data-ttu-id="ef565-386">VarChar</span><span class="sxs-lookup"><span data-stu-id="ef565-386">VarChar</span></span> | <span data-ttu-id="ef565-387">VarChar (maximaal 8000)</span><span class="sxs-lookup"><span data-stu-id="ef565-387">VarChar (up to 8000)</span></span> |
| <span data-ttu-id="ef565-388">NVarChar</span><span class="sxs-lookup"><span data-stu-id="ef565-388">NVarChar</span></span> | <span data-ttu-id="ef565-389">NVarChar (maximaal 4000)</span><span class="sxs-lookup"><span data-stu-id="ef565-389">NVarChar (up to 4000)</span></span> |
| <span data-ttu-id="ef565-390">XML</span><span class="sxs-lookup"><span data-stu-id="ef565-390">Xml</span></span> | <span data-ttu-id="ef565-391">Varchar (maximaal 8000)</span><span class="sxs-lookup"><span data-stu-id="ef565-391">Varchar (up to 8000)</span></span> |

[!INCLUDE [data-factory-type-repeatability-for-sql-sources](../../includes/data-factory-type-repeatability-for-sql-sources.md)]

## <a name="type-mapping-for-azure-sql-data-warehouse"></a><span data-ttu-id="ef565-392">Toewijzing van het type voor Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ef565-392">Type mapping for Azure SQL Data Warehouse</span></span>
<span data-ttu-id="ef565-393">Zoals vermeld in de [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel kopieerbewerking wordt automatische typeconversies van brontypen opvangen typen met de volgende stappen 2-benadering uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="ef565-393">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="ef565-394">Systeemeigen brontypen converteren naar .NET-type</span><span class="sxs-lookup"><span data-stu-id="ef565-394">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="ef565-395">Converteren van .NET-type naar systeemeigen sink-type</span><span class="sxs-lookup"><span data-stu-id="ef565-395">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="ef565-396">Bij het verplaatsen van gegevens naar & van Azure SQL Data Warehouse, worden de volgende toewijzingen gebruikt vanuit de SQL-type aan .NET-type en vice versa.</span><span class="sxs-lookup"><span data-stu-id="ef565-396">When moving data to & from Azure SQL Data Warehouse, the following mappings are used from SQL type to .NET type and vice versa.</span></span>

<span data-ttu-id="ef565-397">De toewijzing is hetzelfde als de [SQL Server gegevenstypetoewijzing voor ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span><span class="sxs-lookup"><span data-stu-id="ef565-397">The mapping is same as the [SQL Server Data Type Mapping for ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span></span>

| <span data-ttu-id="ef565-398">SQL Server Database Engine-type</span><span class="sxs-lookup"><span data-stu-id="ef565-398">SQL Server Database Engine type</span></span> | <span data-ttu-id="ef565-399">.NET framework-type</span><span class="sxs-lookup"><span data-stu-id="ef565-399">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="ef565-400">bigint</span><span class="sxs-lookup"><span data-stu-id="ef565-400">bigint</span></span> |<span data-ttu-id="ef565-401">Int64</span><span class="sxs-lookup"><span data-stu-id="ef565-401">Int64</span></span> |
| <span data-ttu-id="ef565-402">Binaire</span><span class="sxs-lookup"><span data-stu-id="ef565-402">binary</span></span> |<span data-ttu-id="ef565-403">Byte]</span><span class="sxs-lookup"><span data-stu-id="ef565-403">Byte[]</span></span> |
| <span data-ttu-id="ef565-404">bits</span><span class="sxs-lookup"><span data-stu-id="ef565-404">bit</span></span> |<span data-ttu-id="ef565-405">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="ef565-405">Boolean</span></span> |
| <span data-ttu-id="ef565-406">CHAR</span><span class="sxs-lookup"><span data-stu-id="ef565-406">char</span></span> |<span data-ttu-id="ef565-407">Tekenreeks, Char]</span><span class="sxs-lookup"><span data-stu-id="ef565-407">String, Char[]</span></span> |
| <span data-ttu-id="ef565-408">Datum</span><span class="sxs-lookup"><span data-stu-id="ef565-408">date</span></span> |<span data-ttu-id="ef565-409">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="ef565-409">DateTime</span></span> |
| <span data-ttu-id="ef565-410">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="ef565-410">Datetime</span></span> |<span data-ttu-id="ef565-411">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="ef565-411">DateTime</span></span> |
| <span data-ttu-id="ef565-412">datetime2</span><span class="sxs-lookup"><span data-stu-id="ef565-412">datetime2</span></span> |<span data-ttu-id="ef565-413">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="ef565-413">DateTime</span></span> |
| <span data-ttu-id="ef565-414">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="ef565-414">Datetimeoffset</span></span> |<span data-ttu-id="ef565-415">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="ef565-415">DateTimeOffset</span></span> |
| <span data-ttu-id="ef565-416">Decimale</span><span class="sxs-lookup"><span data-stu-id="ef565-416">Decimal</span></span> |<span data-ttu-id="ef565-417">Decimale</span><span class="sxs-lookup"><span data-stu-id="ef565-417">Decimal</span></span> |
| <span data-ttu-id="ef565-418">FILESTREAM-kenmerk (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="ef565-418">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="ef565-419">Byte]</span><span class="sxs-lookup"><span data-stu-id="ef565-419">Byte[]</span></span> |
| <span data-ttu-id="ef565-420">Float</span><span class="sxs-lookup"><span data-stu-id="ef565-420">Float</span></span> |<span data-ttu-id="ef565-421">dubbele</span><span class="sxs-lookup"><span data-stu-id="ef565-421">Double</span></span> |
| <span data-ttu-id="ef565-422">Afbeelding</span><span class="sxs-lookup"><span data-stu-id="ef565-422">image</span></span> |<span data-ttu-id="ef565-423">Byte]</span><span class="sxs-lookup"><span data-stu-id="ef565-423">Byte[]</span></span> |
| <span data-ttu-id="ef565-424">int</span><span class="sxs-lookup"><span data-stu-id="ef565-424">int</span></span> |<span data-ttu-id="ef565-425">Int32</span><span class="sxs-lookup"><span data-stu-id="ef565-425">Int32</span></span> |
| <span data-ttu-id="ef565-426">Money</span><span class="sxs-lookup"><span data-stu-id="ef565-426">money</span></span> |<span data-ttu-id="ef565-427">Decimale</span><span class="sxs-lookup"><span data-stu-id="ef565-427">Decimal</span></span> |
| <span data-ttu-id="ef565-428">nchar</span><span class="sxs-lookup"><span data-stu-id="ef565-428">nchar</span></span> |<span data-ttu-id="ef565-429">Tekenreeks, Char]</span><span class="sxs-lookup"><span data-stu-id="ef565-429">String, Char[]</span></span> |
| <span data-ttu-id="ef565-430">ntext</span><span class="sxs-lookup"><span data-stu-id="ef565-430">ntext</span></span> |<span data-ttu-id="ef565-431">Tekenreeks, Char]</span><span class="sxs-lookup"><span data-stu-id="ef565-431">String, Char[]</span></span> |
| <span data-ttu-id="ef565-432">numerieke</span><span class="sxs-lookup"><span data-stu-id="ef565-432">numeric</span></span> |<span data-ttu-id="ef565-433">Decimale</span><span class="sxs-lookup"><span data-stu-id="ef565-433">Decimal</span></span> |
| <span data-ttu-id="ef565-434">nvarchar</span><span class="sxs-lookup"><span data-stu-id="ef565-434">nvarchar</span></span> |<span data-ttu-id="ef565-435">Tekenreeks, Char]</span><span class="sxs-lookup"><span data-stu-id="ef565-435">String, Char[]</span></span> |
| <span data-ttu-id="ef565-436">echte</span><span class="sxs-lookup"><span data-stu-id="ef565-436">real</span></span> |<span data-ttu-id="ef565-437">Één</span><span class="sxs-lookup"><span data-stu-id="ef565-437">Single</span></span> |
| <span data-ttu-id="ef565-438">ROWVERSION</span><span class="sxs-lookup"><span data-stu-id="ef565-438">rowversion</span></span> |<span data-ttu-id="ef565-439">Byte]</span><span class="sxs-lookup"><span data-stu-id="ef565-439">Byte[]</span></span> |
| <span data-ttu-id="ef565-440">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="ef565-440">smalldatetime</span></span> |<span data-ttu-id="ef565-441">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="ef565-441">DateTime</span></span> |
| <span data-ttu-id="ef565-442">smallint</span><span class="sxs-lookup"><span data-stu-id="ef565-442">smallint</span></span> |<span data-ttu-id="ef565-443">Int16</span><span class="sxs-lookup"><span data-stu-id="ef565-443">Int16</span></span> |
| <span data-ttu-id="ef565-444">smallmoney</span><span class="sxs-lookup"><span data-stu-id="ef565-444">smallmoney</span></span> |<span data-ttu-id="ef565-445">Decimale</span><span class="sxs-lookup"><span data-stu-id="ef565-445">Decimal</span></span> |
| <span data-ttu-id="ef565-446">sql_variant</span><span class="sxs-lookup"><span data-stu-id="ef565-446">sql_variant</span></span> |<span data-ttu-id="ef565-447">Object *</span><span class="sxs-lookup"><span data-stu-id="ef565-447">Object *</span></span> |
| <span data-ttu-id="ef565-448">Tekst</span><span class="sxs-lookup"><span data-stu-id="ef565-448">text</span></span> |<span data-ttu-id="ef565-449">Tekenreeks, Char]</span><span class="sxs-lookup"><span data-stu-id="ef565-449">String, Char[]</span></span> |
| <span data-ttu-id="ef565-450">tijd</span><span class="sxs-lookup"><span data-stu-id="ef565-450">time</span></span> |<span data-ttu-id="ef565-451">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="ef565-451">TimeSpan</span></span> |
| <span data-ttu-id="ef565-452">tijdstempel</span><span class="sxs-lookup"><span data-stu-id="ef565-452">timestamp</span></span> |<span data-ttu-id="ef565-453">Byte]</span><span class="sxs-lookup"><span data-stu-id="ef565-453">Byte[]</span></span> |
| <span data-ttu-id="ef565-454">tinyint</span><span class="sxs-lookup"><span data-stu-id="ef565-454">tinyint</span></span> |<span data-ttu-id="ef565-455">Byte</span><span class="sxs-lookup"><span data-stu-id="ef565-455">Byte</span></span> |
| <span data-ttu-id="ef565-456">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="ef565-456">uniqueidentifier</span></span> |<span data-ttu-id="ef565-457">GUID</span><span class="sxs-lookup"><span data-stu-id="ef565-457">Guid</span></span> |
| <span data-ttu-id="ef565-458">varbinary</span><span class="sxs-lookup"><span data-stu-id="ef565-458">varbinary</span></span> |<span data-ttu-id="ef565-459">Byte]</span><span class="sxs-lookup"><span data-stu-id="ef565-459">Byte[]</span></span> |
| <span data-ttu-id="ef565-460">varchar</span><span class="sxs-lookup"><span data-stu-id="ef565-460">varchar</span></span> |<span data-ttu-id="ef565-461">Tekenreeks, Char]</span><span class="sxs-lookup"><span data-stu-id="ef565-461">String, Char[]</span></span> |
| <span data-ttu-id="ef565-462">xml</span><span class="sxs-lookup"><span data-stu-id="ef565-462">xml</span></span> |<span data-ttu-id="ef565-463">XML</span><span class="sxs-lookup"><span data-stu-id="ef565-463">Xml</span></span> |

<span data-ttu-id="ef565-464">U kunt ook kolommen uit de bron-gegevensset naar kolommen uit sink gegevensset in de definitie van de activiteit kopiëren toewijzen.</span><span class="sxs-lookup"><span data-stu-id="ef565-464">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span></span> <span data-ttu-id="ef565-465">Zie voor meer informatie [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="ef565-465">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="json-examples-for-copying-data-to-and-from-sql-data-warehouse"></a><span data-ttu-id="ef565-466">JSON-voorbeelden voor het kopiëren van gegevens naar en van SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ef565-466">JSON examples for copying data to and from SQL Data Warehouse</span></span>
<span data-ttu-id="ef565-467">De volgende voorbeelden geven voorbeeld JSON definities die u een pijplijn maken kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="ef565-467">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="ef565-468">Ze laten zien hoe om gegevens te kopiëren naar en van Azure SQL Data Warehouse en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="ef565-468">They show how to copy data to and from Azure SQL Data Warehouse and Azure Blob Storage.</span></span> <span data-ttu-id="ef565-469">Echter, de gegevens kunnen worden gekopieerd **rechtstreeks** uit een van de bronnen aan een van de PUT vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van de Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ef565-469">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-data-warehouse-to-azure-blob"></a><span data-ttu-id="ef565-470">Voorbeeld: Gegevens kopiëren van Azure SQL Data Warehouse naar Azure Blob</span><span class="sxs-lookup"><span data-stu-id="ef565-470">Example: Copy data from Azure SQL Data Warehouse to Azure Blob</span></span>
<span data-ttu-id="ef565-471">Het voorbeeld worden de volgende Data Factory-entiteiten gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="ef565-471">The sample defines the following Data Factory entities:</span></span>

1. <span data-ttu-id="ef565-472">Een gekoppelde service van het type [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ef565-472">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="ef565-473">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ef565-473">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="ef565-474">Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureSqlDWTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ef565-474">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
4. <span data-ttu-id="ef565-475">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ef565-475">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="ef565-476">Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [SqlDWSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ef565-476">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [SqlDWSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="ef565-477">De voorbeeld-tijdreeks (elk uur, dagelijks, enz.) worden gegevens gekopieerd van een tabel in Azure SQL Data Warehouse-database naar een blob elk uur.</span><span class="sxs-lookup"><span data-stu-id="ef565-477">The sample copies time-series (hourly, daily, etc.) data from a table in Azure SQL Data Warehouse database to a blob every hour.</span></span> <span data-ttu-id="ef565-478">De JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na de voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="ef565-478">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="ef565-479">**Azure SQL Data Warehouse gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="ef565-479">**Azure SQL Data Warehouse linked service:**</span></span>

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="ef565-480">**Azure Blob-opslag gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="ef565-480">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="ef565-481">**Azure SQL Data Warehouse invoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="ef565-481">**Azure SQL Data Warehouse input dataset:**</span></span>

<span data-ttu-id="ef565-482">Het voorbeeld wordt ervan uitgegaan dat u hebt een tabel 'MijnTabel' gemaakt in Azure SQL Data Warehouse en bevat een kolom met de naam 'timestampcolumn' voor de reeksgegevens.</span><span class="sxs-lookup"><span data-stu-id="ef565-482">The sample assumes you have created a table “MyTable” in Azure SQL Data Warehouse and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="ef565-483">Instelling 'extern': 'true' informeert de Data Factory-service dat de dataset extern is aan de gegevensfactory en niet wordt geproduceerd door een activiteit in de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="ef565-483">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```JSON
{
  "name": "AzureSqlDWInput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
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
<span data-ttu-id="ef565-484">**Azure Blob-uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="ef565-484">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="ef565-485">Gegevens worden geschreven naar een nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="ef565-485">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="ef565-486">Het pad naar de blob wordt dynamisch geëvalueerd op basis van de begintijd van het segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="ef565-486">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="ef565-487">Het mappad maakt gebruik van jaar, maand, dag en uur delen van de begintijd.</span><span class="sxs-lookup"><span data-stu-id="ef565-487">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="ef565-488">**De kopieeractiviteit in een pijplijn met SqlDWSource en BlobSink:**</span><span class="sxs-lookup"><span data-stu-id="ef565-488">**Copy activity in a pipeline with SqlDWSource and BlobSink:**</span></span>

<span data-ttu-id="ef565-489">De pijplijn bevat een Kopieeractiviteit die is geconfigureerd voor gebruik van de invoer- en uitvoergegevenssets en elk uur is gepland.</span><span class="sxs-lookup"><span data-stu-id="ef565-489">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="ef565-490">In de pijplijn-JSON-definitie de **bron** type is ingesteld op **SqlDWSource** en **sink** type is ingesteld op **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="ef565-490">In the pipeline JSON definition, the **source** type is set to **SqlDWSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="ef565-491">De SQL-query die is opgegeven voor de **SqlReaderQuery** eigenschap selecteert u de gegevens in het afgelopen uur te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="ef565-491">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLDWtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSqlDWInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlDWSource",
            "sqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
> [!NOTE]
> <span data-ttu-id="ef565-492">In het voorbeeld **sqlReaderQuery** is opgegeven voor de SqlDWSource.</span><span class="sxs-lookup"><span data-stu-id="ef565-492">In the example, **sqlReaderQuery** is specified for the SqlDWSource.</span></span> <span data-ttu-id="ef565-493">De Kopieeractiviteit wordt deze query uitgevoerd op basis van de Azure SQL Data Warehouse-bron om de gegevens te verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="ef565-493">The Copy Activity runs this query against the Azure SQL Data Warehouse source to get the data.</span></span>
>
> <span data-ttu-id="ef565-494">U kunt ook een opgeslagen procedure opgeven door te geven de **sqlReaderStoredProcedureName** en **storedProcedureParameters** (als de opgeslagen procedure parameters nodig heeft).</span><span class="sxs-lookup"><span data-stu-id="ef565-494">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>
>
> <span data-ttu-id="ef565-495">Als u geen sqlReaderQuery of sqlReaderStoredProcedureName opgeeft, worden de kolommen die zijn gedefinieerd in de sectie van de structuur van de gegevensset JSON worden gebruikt voor het bouwen van een query (Selecteer column1, column2 from MijnTabel) als u wilt uitvoeren op Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ef565-495">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section of the dataset JSON are used to build a query (select column1, column2 from mytable) to run against the Azure SQL Data Warehouse.</span></span> <span data-ttu-id="ef565-496">Als de definitie van de gegevensset heeft niet de structuur, worden alle kolommen uit de tabel geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="ef565-496">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>
>
>

### <a name="example-copy-data-from-azure-blob-to-azure-sql-data-warehouse"></a><span data-ttu-id="ef565-497">Voorbeeld: Gegevens kopiëren van Azure-Blob naar Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ef565-497">Example: Copy data from Azure Blob to Azure SQL Data Warehouse</span></span>
<span data-ttu-id="ef565-498">Het voorbeeld worden de volgende Data Factory-entiteiten gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="ef565-498">The sample defines the following Data Factory entities:</span></span>

1. <span data-ttu-id="ef565-499">Een gekoppelde service van het type [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ef565-499">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="ef565-500">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ef565-500">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="ef565-501">Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ef565-501">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="ef565-502">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureSqlDWTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ef565-502">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
5. <span data-ttu-id="ef565-503">Een [pijplijn](data-factory-create-pipelines.md) met de kopieeractiviteit die gebruikmaakt van [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) en [SqlDWSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ef565-503">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlDWSink](#copy-activity-properties).</span></span>

<span data-ttu-id="ef565-504">De voorbeeld-kopieën timeseries gegevens (elk uur, dagelijks, etc.) van Azure-blob naar een tabel in Azure SQL Data Warehouse-database om het uur.</span><span class="sxs-lookup"><span data-stu-id="ef565-504">The sample copies time-series data (hourly, daily, etc.) from Azure blob to a table in Azure SQL Data Warehouse database every hour.</span></span> <span data-ttu-id="ef565-505">De JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na de voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="ef565-505">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="ef565-506">**Azure SQL Data Warehouse gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="ef565-506">**Azure SQL Data Warehouse linked service:**</span></span>

```JSON
{
  "name": "AzureSqlDWLinkedService",
  "properties": {
    "type": "AzureSqlDW",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="ef565-507">**Azure Blob-opslag gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="ef565-507">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="ef565-508">**Azure Blob invoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="ef565-508">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="ef565-509">Gegevens wordt opgehaald uit een nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="ef565-509">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="ef565-510">Pad en naam van de map voor de blob worden dynamisch geëvalueerd op basis van de begintijd van het segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="ef565-510">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="ef565-511">Het mappad gebruikt jaar, maand en dag deel uit van de begintijd en de bestandsnaam wordt gebruikt voor het uur deel van de begintijd.</span><span class="sxs-lookup"><span data-stu-id="ef565-511">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="ef565-512">"extern": "true" instelling informeert de Data Factory-service dat deze tabel extern is aan de gegevensfactory en niet wordt geproduceerd door een activiteit in de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="ef565-512">“external”: “true” setting informs the Data Factory service that this table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="ef565-513">**Azure SQL Data Warehouse uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="ef565-513">**Azure SQL Data Warehouse output dataset:**</span></span>

<span data-ttu-id="ef565-514">Het voorbeeld worden gegevens gekopieerd naar een tabel met de naam "MijnTabel" in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ef565-514">The sample copies data to a table named “MyTable” in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="ef565-515">De tabel maken in Azure SQL Data Warehouse met hetzelfde aantal kolommen, zoals u verwacht dat de Blob-CSV-bestand bevatten.</span><span class="sxs-lookup"><span data-stu-id="ef565-515">Create the table in Azure SQL Data Warehouse with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="ef565-516">Nieuwe rijen worden toegevoegd aan de tabel om het uur.</span><span class="sxs-lookup"><span data-stu-id="ef565-516">New rows are added to the table every hour.</span></span>

```JSON
{
  "name": "AzureSqlDWOutput",
  "properties": {
    "type": "AzureSqlDWTable",
    "linkedServiceName": "AzureSqlDWLinkedService",
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
<span data-ttu-id="ef565-517">**De kopieeractiviteit in een pijplijn met BlobSource en SqlDWSink:**</span><span class="sxs-lookup"><span data-stu-id="ef565-517">**Copy activity in a pipeline with BlobSource and SqlDWSink:**</span></span>

<span data-ttu-id="ef565-518">De pijplijn bevat een Kopieeractiviteit die is geconfigureerd voor gebruik van de invoer- en uitvoergegevenssets en elk uur is gepland.</span><span class="sxs-lookup"><span data-stu-id="ef565-518">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="ef565-519">In de pijplijn-JSON-definitie de **bron** type is ingesteld op **BlobSource** en **sink** type is ingesteld op **SqlDWSink**.</span><span class="sxs-lookup"><span data-stu-id="ef565-519">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlDWSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQLDW",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlDWOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlDWSink",
            "allowPolyBase": true
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
<span data-ttu-id="ef565-520">Voor een overzicht, Zie de [1 TB laden in Azure SQL Data Warehouse onder 15 minuten met Azure Data Factory](data-factory-load-sql-data-warehouse.md) en [gegevens laden met Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) artikel in de documentatie van Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ef565-520">For a walkthrough, see the see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) and [Load data with Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) article in the Azure SQL Data Warehouse documentation.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="ef565-521">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="ef565-521">Performance and Tuning</span></span>
<span data-ttu-id="ef565-522">Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) voor meer informatie over de belangrijkste factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren om te optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="ef565-522">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
