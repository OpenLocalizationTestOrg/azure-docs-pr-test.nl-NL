---
title: aaaCopy gegevens van/naar Azure SQL Data Warehouse | Microsoft Docs
description: Meer informatie over hoe toocopy gegevens van/naar Azure SQL Data Warehouse met behulp van Azure Data Factory
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
ms.openlocfilehash: 75bfcf3c99844fc1297ca500107da23cf875e41f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-data-warehouse-using-azure-data-factory"></a><span data-ttu-id="44256-103">Tooand gegevens kopiëren van Azure SQL Data Warehouse met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="44256-103">Copy data tooand from Azure SQL Data Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="44256-104">Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit Hallo in Azure Data Factory toomove gegevens van Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="44256-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from Azure SQL Data Warehouse.</span></span> <span data-ttu-id="44256-105">Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.</span><span class="sxs-lookup"><span data-stu-id="44256-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>  

> [!TIP]
> <span data-ttu-id="44256-106">tooachieve optimaal, gebruikt u PolyBase tooload gegevens in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="44256-106">tooachieve best performance, use PolyBase tooload data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="44256-107">Hallo [gebruik PolyBase tooload gegevens in Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) sectie bevat informatie.</span><span class="sxs-lookup"><span data-stu-id="44256-107">hello [Use PolyBase tooload data into Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) section has details.</span></span> <span data-ttu-id="44256-108">Zie voor een overzicht met een gebruiksvoorbeeld [1 TB laden in Azure SQL Data Warehouse onder 15 minuten met Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span><span class="sxs-lookup"><span data-stu-id="44256-108">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="44256-109">Ondersteunde scenario 's</span><span class="sxs-lookup"><span data-stu-id="44256-109">Supported scenarios</span></span>
<span data-ttu-id="44256-110">U kunt gegevens kopiëren **van Azure SQL Data Warehouse** toohello gegevensarchieven te volgen:</span><span class="sxs-lookup"><span data-stu-id="44256-110">You can copy data **from Azure SQL Data Warehouse** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="44256-111">Gegevens kunnen worden gekopieerd van de volgende gegevensarchieven Hallo **tooAzure SQL Data Warehouse**:</span><span class="sxs-lookup"><span data-stu-id="44256-111">You can copy data from hello following data stores **tooAzure SQL Data Warehouse**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!TIP]
> <span data-ttu-id="44256-112">Bij het kopiëren van gegevens uit SQL Server of Azure SQL Database tooAzure kunt SQL Data Warehouse, als Hallo tabel niet in het doelarchief hello, Data Factory bestaat automatisch Hallo tabel maken in SQL Data Warehouse met behulp van schema van tabel Hallo Hallo in Hallo bron gegevensopslag.</span><span class="sxs-lookup"><span data-stu-id="44256-112">When copying data from SQL Server or Azure SQL Database tooAzure SQL Data Warehouse, if hello table does not exist in hello destination store, Data Factory can automatically create hello table in SQL Data Warehouse by using hello schema of hello table in hello source data store.</span></span> <span data-ttu-id="44256-113">Zie [automatisch maken van de tabel](#auto-table-creation) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="44256-113">See [Auto table creation](#auto-table-creation) for details.</span></span>

## <a name="supported-authentication-type"></a><span data-ttu-id="44256-114">Ondersteund verificatietype</span><span class="sxs-lookup"><span data-stu-id="44256-114">Supported authentication type</span></span>
<span data-ttu-id="44256-115">Azure SQL Data Warehouse connector ondersteuning voor basisverificatie.</span><span class="sxs-lookup"><span data-stu-id="44256-115">Azure SQL Data Warehouse connector support basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="44256-116">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="44256-116">Getting started</span></span>
<span data-ttu-id="44256-117">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens worden verplaatst van een Azure SQL Data Warehouse met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="44256-117">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Data Warehouse by using different tools/APIs.</span></span>

<span data-ttu-id="44256-118">Hallo gemakkelijkste manier toocreate een pijplijn waarmee gegevens van Azure SQL Data Warehouse worden gekopieerd is wizard toouse Hallo kopiëren-gegevens.</span><span class="sxs-lookup"><span data-stu-id="44256-118">hello easiest way toocreate a pipeline that copies data to/from Azure SQL Data Warehouse is toouse hello Copy data wizard.</span></span> <span data-ttu-id="44256-119">Zie [zelfstudie: gegevens laden in SQL Data Warehouse met Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="44256-119">See [Tutorial: Load data into SQL Data Warehouse with Data Factory](../sql-data-warehouse/sql-data-warehouse-load-with-data-factory.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="44256-120">U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="44256-120">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="44256-121">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="44256-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="44256-122">Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="44256-122">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="44256-123">Maak een **gegevensfactory**.</span><span class="sxs-lookup"><span data-stu-id="44256-123">Create a **data factory**.</span></span> <span data-ttu-id="44256-124">Een gegevensfactory kan één of meer pijplijnen bevatten.</span><span class="sxs-lookup"><span data-stu-id="44256-124">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="44256-125">Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="44256-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="44256-126">Bijvoorbeeld, als u gegevens uit een Azure blob storage tooan Azure SQL datawarehouse kopiëren wilt, u twee gekoppelde services toolink uw Azure storage-account en Azure SQL datawarehouse tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="44256-126">For example, if you are copying data from an Azure blob storage tooan Azure SQL data warehouse, you create two linked services toolink your Azure storage account and Azure SQL data warehouse tooyour data factory.</span></span> <span data-ttu-id="44256-127">Zie voor de gekoppelde service-eigenschappen die specifiek tooAzure SQL Data Warehouse, [gekoppelde service-eigenschappen](#linked-service-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="44256-127">For linked service properties that are specific tooAzure SQL Data Warehouse, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="44256-128">Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="44256-128">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="44256-129">In vermeld in de laatste stap Hallo Hallo voorbeeld maakt u een gegevensset toospecify Hallo blob-container en map met invoergegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="44256-129">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="44256-130">En u een andere dataset toospecify Hallo tabel maken in hello Azure SQL datawarehouse die Hallo gegevens gekopieerd van de blob-opslag Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="44256-130">And, you create another dataset toospecify hello table in hello Azure SQL data warehouse that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="44256-131">Zie voor eigenschappen van gegevensset die specifieke tooAzure SQL Data Warehouse, [eigenschappen van gegevensset](#dataset-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="44256-131">For dataset properties that are specific tooAzure SQL Data Warehouse, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="44256-132">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="44256-132">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="44256-133">In Hallo voorbeeld eerder vermeld, gebruikt u BlobSource als een bron- en SqlDWSink als een sink voor de kopieeractiviteit Hallo.</span><span class="sxs-lookup"><span data-stu-id="44256-133">In hello example mentioned earlier, you use BlobSource as a source and SqlDWSink as a sink for hello copy activity.</span></span> <span data-ttu-id="44256-134">Op dezelfde manier als u van Azure SQL Data Warehouse tooAzure Blob Storage kopiëren wilt, gebruikt u SqlDWSource en BlobSink in Hallo kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="44256-134">Similarly, if you are copying from Azure SQL Data Warehouse tooAzure Blob Storage, you use SqlDWSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="44256-135">Zie voor activiteitseigenschappen kopiëren die specifieke tooAzure SQL Data Warehouse, [activiteitseigenschappen kopiëren](#copy-activity-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="44256-135">For copy activity properties that are specific tooAzure SQL Data Warehouse, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="44256-136">Voor informatie over hoe toouse een gegevensarchief als een bron of een sink, klikt u op Hallo-koppeling in de vorige sectie Hallo voor de gegevensopslag.</span><span class="sxs-lookup"><span data-stu-id="44256-136">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>

<span data-ttu-id="44256-137">Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="44256-137">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="44256-138">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="44256-138">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="44256-139">Zie voor voorbeelden met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens van/naar een Azure SQL Data Warehouse zijn, [JSON voorbeelden](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="44256-139">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure SQL Data Warehouse, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-data-warehouse) section of this article.</span></span>

<span data-ttu-id="44256-140">Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooAzure SQL Data Warehouse zijn:</span><span class="sxs-lookup"><span data-stu-id="44256-140">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure SQL Data Warehouse:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="44256-141">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="44256-141">Linked service properties</span></span>
<span data-ttu-id="44256-142">Hallo volgende tabel bevat een beschrijving voor JSON-elementen specifieke tooAzure SQL Data Warehouse gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="44256-142">hello following table provides description for JSON elements specific tooAzure SQL Data Warehouse linked service.</span></span>

| <span data-ttu-id="44256-143">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="44256-143">Property</span></span> | <span data-ttu-id="44256-144">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="44256-144">Description</span></span> | <span data-ttu-id="44256-145">Vereist</span><span class="sxs-lookup"><span data-stu-id="44256-145">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44256-146">type</span><span class="sxs-lookup"><span data-stu-id="44256-146">type</span></span> |<span data-ttu-id="44256-147">Hallo type eigenschap moet worden ingesteld op: **AzureSqlDW**</span><span class="sxs-lookup"><span data-stu-id="44256-147">hello type property must be set to: **AzureSqlDW**</span></span> |<span data-ttu-id="44256-148">Ja</span><span class="sxs-lookup"><span data-stu-id="44256-148">Yes</span></span> |
| <span data-ttu-id="44256-149">connectionString</span><span class="sxs-lookup"><span data-stu-id="44256-149">connectionString</span></span> |<span data-ttu-id="44256-150">Geef informatie tooconnect toohello Azure SQL Data Warehouse-exemplaar voor de eigenschap connectionString Hallo nodig.</span><span class="sxs-lookup"><span data-stu-id="44256-150">Specify information needed tooconnect toohello Azure SQL Data Warehouse instance for hello connectionString property.</span></span> <span data-ttu-id="44256-151">Alleen basisverificatie wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="44256-151">Only basic authentication is supported.</span></span> |<span data-ttu-id="44256-152">Ja</span><span class="sxs-lookup"><span data-stu-id="44256-152">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="44256-153">Configureer [Azure SQL Database-Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) en database-server te Hallo[Azure Services tooaccess Hallo server toestaan](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span><span class="sxs-lookup"><span data-stu-id="44256-153">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) and hello database server too[allow Azure Services tooaccess hello server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="44256-154">Bovendien configureren als u gegevens tooAzure SQL Data Warehouse kopiëren wilt uit buiten Azure met inbegrip van on-premises gegevensbronnen met data factory-gateway, de juiste IP-adresbereik voor Hallo-machine dat gegevens tooAzure SQL Data Warehouse verzendt.</span><span class="sxs-lookup"><span data-stu-id="44256-154">Additionally, if you are copying data tooAzure SQL Data Warehouse from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for hello machine that is sending data tooAzure SQL Data Warehouse.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="44256-155">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="44256-155">Dataset properties</span></span>
<span data-ttu-id="44256-156">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="44256-156">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="44256-157">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).</span><span class="sxs-lookup"><span data-stu-id="44256-157">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="44256-158">Hallo typeProperties sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="44256-158">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="44256-159">Hallo **typeProperties** sectie voor Hallo gegevensset van het type **AzureSqlDWTable** heeft Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="44256-159">hello **typeProperties** section for hello dataset of type **AzureSqlDWTable** has hello following properties:</span></span>

| <span data-ttu-id="44256-160">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="44256-160">Property</span></span> | <span data-ttu-id="44256-161">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="44256-161">Description</span></span> | <span data-ttu-id="44256-162">Vereist</span><span class="sxs-lookup"><span data-stu-id="44256-162">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44256-163">tableName</span><span class="sxs-lookup"><span data-stu-id="44256-163">tableName</span></span> |<span data-ttu-id="44256-164">De naam van het Hallo-tabel of weergave in hello Azure SQL Data Warehouse-database die Hallo gekoppelde service verwijst.</span><span class="sxs-lookup"><span data-stu-id="44256-164">Name of hello table or view in hello Azure SQL Data Warehouse database that hello linked service refers to.</span></span> |<span data-ttu-id="44256-165">Ja</span><span class="sxs-lookup"><span data-stu-id="44256-165">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="44256-166">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="44256-166">Copy activity properties</span></span>
<span data-ttu-id="44256-167">Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="44256-167">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="44256-168">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en -beleid zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="44256-168">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="44256-169">Hallo Kopieeractiviteit slechts één invoer en slechts één uitvoer produceert.</span><span class="sxs-lookup"><span data-stu-id="44256-169">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="44256-170">Terwijl de eigenschappen die beschikbaar zijn in Hallo typeProperties gedeelte van de activiteit Hallo variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="44256-170">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="44256-171">Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="44256-171">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

### <a name="sqldwsource"></a><span data-ttu-id="44256-172">SqlDWSource</span><span class="sxs-lookup"><span data-stu-id="44256-172">SqlDWSource</span></span>
<span data-ttu-id="44256-173">Wanneer de bron is van het type **SqlDWSource**, Hallo volgende eigenschappen beschikbaar zijn in **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="44256-173">When source is of type **SqlDWSource**, hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="44256-174">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="44256-174">Property</span></span> | <span data-ttu-id="44256-175">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="44256-175">Description</span></span> | <span data-ttu-id="44256-176">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="44256-176">Allowed values</span></span> | <span data-ttu-id="44256-177">Vereist</span><span class="sxs-lookup"><span data-stu-id="44256-177">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="44256-178">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="44256-178">sqlReaderQuery</span></span> |<span data-ttu-id="44256-179">Hallo aangepaste query tooread gegevens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="44256-179">Use hello custom query tooread data.</span></span> |<span data-ttu-id="44256-180">SQL-query-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="44256-180">SQL query string.</span></span> <span data-ttu-id="44256-181">Bijvoorbeeld: Selecteer * from MijnTabel.</span><span class="sxs-lookup"><span data-stu-id="44256-181">For example: select * from MyTable.</span></span> |<span data-ttu-id="44256-182">Nee</span><span class="sxs-lookup"><span data-stu-id="44256-182">No</span></span> |
| <span data-ttu-id="44256-183">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="44256-183">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="44256-184">Naam van Hallo opgeslagen procedure die gegevens uit Hallo brontabel leest.</span><span class="sxs-lookup"><span data-stu-id="44256-184">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="44256-185">Naam van Hallo opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="44256-185">Name of hello stored procedure.</span></span> <span data-ttu-id="44256-186">Hallo laatste SQL-instructie moet een SELECT-instructie in Hallo opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="44256-186">hello last SQL statement must be a SELECT statement in hello stored procedure.</span></span> |<span data-ttu-id="44256-187">Nee</span><span class="sxs-lookup"><span data-stu-id="44256-187">No</span></span> |
| <span data-ttu-id="44256-188">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="44256-188">storedProcedureParameters</span></span> |<span data-ttu-id="44256-189">Parameters voor Hallo opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="44256-189">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="44256-190">Naam/waarde-paren.</span><span class="sxs-lookup"><span data-stu-id="44256-190">Name/value pairs.</span></span> <span data-ttu-id="44256-191">Namen en hoofdlettergebruik van parameters moeten overeenkomen met Hallo namen en hoofdlettergebruik van Hallo opgeslagen procedureparameters.</span><span class="sxs-lookup"><span data-stu-id="44256-191">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="44256-192">Nee</span><span class="sxs-lookup"><span data-stu-id="44256-192">No</span></span> |

<span data-ttu-id="44256-193">Als hello **sqlReaderQuery** is opgegeven voor Hallo SqlDWSource, hello Kopieeractiviteit deze query wordt uitgevoerd tegen Hallo tooget Azure SQL Data Warehouse-Hallo brongegevens.</span><span class="sxs-lookup"><span data-stu-id="44256-193">If hello **sqlReaderQuery** is specified for hello SqlDWSource, hello Copy Activity runs this query against hello Azure SQL Data Warehouse source tooget hello data.</span></span>

<span data-ttu-id="44256-194">U kunt ook een opgeslagen procedure opgeven door te geven Hallo **sqlReaderStoredProcedureName** en **storedProcedureParameters** (als hello opgeslagen procedure parameters zijn vereist).</span><span class="sxs-lookup"><span data-stu-id="44256-194">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="44256-195">Als u geen sqlReaderQuery of sqlReaderStoredProcedureName opgeeft, zijn Hallo kolommen gedefinieerd in de sectie Hallo structuur van Hallo gegevensset JSON gebruikte toobuild een query toorun tegen hello Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="44256-195">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query toorun against hello Azure SQL Data Warehouse.</span></span> <span data-ttu-id="44256-196">Voorbeeld: `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="44256-196">Example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="44256-197">Als de definitie van de gegevensset Hallo geen Hallo structuur, worden alle kolommen uit Hallo tabel geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="44256-197">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

#### <a name="sqldwsource-example"></a><span data-ttu-id="44256-198">Voorbeeld van SqlDWSource</span><span class="sxs-lookup"><span data-stu-id="44256-198">SqlDWSource example</span></span>

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
<span data-ttu-id="44256-199">**Hallo opgeslagen proceduredefinitie:**</span><span class="sxs-lookup"><span data-stu-id="44256-199">**hello stored procedure definition:**</span></span>

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

### <a name="sqldwsink"></a><span data-ttu-id="44256-200">SqlDWSink</span><span class="sxs-lookup"><span data-stu-id="44256-200">SqlDWSink</span></span>
<span data-ttu-id="44256-201">**SqlDWSink** ondersteunt Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="44256-201">**SqlDWSink** supports hello following properties:</span></span>

| <span data-ttu-id="44256-202">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="44256-202">Property</span></span> | <span data-ttu-id="44256-203">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="44256-203">Description</span></span> | <span data-ttu-id="44256-204">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="44256-204">Allowed values</span></span> | <span data-ttu-id="44256-205">Vereist</span><span class="sxs-lookup"><span data-stu-id="44256-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="44256-206">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="44256-206">sqlWriterCleanupScript</span></span> |<span data-ttu-id="44256-207">Geef een query voor de Kopieeractiviteit tooexecute zodat de gegevens van een bepaald segment wordt opgeschoond.</span><span class="sxs-lookup"><span data-stu-id="44256-207">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="44256-208">Zie voor meer informatie [herhaalbaarheid sectie](#repeatability-during-copy).</span><span class="sxs-lookup"><span data-stu-id="44256-208">For details, see [repeatability section](#repeatability-during-copy).</span></span> |<span data-ttu-id="44256-209">Een query-instructie.</span><span class="sxs-lookup"><span data-stu-id="44256-209">A query statement.</span></span> |<span data-ttu-id="44256-210">Nee</span><span class="sxs-lookup"><span data-stu-id="44256-210">No</span></span> |
| <span data-ttu-id="44256-211">allowPolyBase</span><span class="sxs-lookup"><span data-stu-id="44256-211">allowPolyBase</span></span> |<span data-ttu-id="44256-212">Hiermee wordt aangegeven of toouse PolyBase (indien van toepassing) in plaats van BULKINSERT mechanisme.</span><span class="sxs-lookup"><span data-stu-id="44256-212">Indicates whether toouse PolyBase (when applicable) instead of BULKINSERT mechanism.</span></span> <br/><br/> <span data-ttu-id="44256-213">**Met PolyBase is Hallo aanbevolen manier tooload gegevens in SQL Data Warehouse.**</span><span class="sxs-lookup"><span data-stu-id="44256-213">**Using PolyBase is hello recommended way tooload data into SQL Data Warehouse.**</span></span> <span data-ttu-id="44256-214">Zie [gebruik PolyBase tooload gegevens in Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) sectie voor beperkingen en meer informatie.</span><span class="sxs-lookup"><span data-stu-id="44256-214">See [Use PolyBase tooload data into Azure SQL Data Warehouse](#use-polybase-to-load-data-into-azure-sql-data-warehouse) section for constraints and details.</span></span> |<span data-ttu-id="44256-215">True</span><span class="sxs-lookup"><span data-stu-id="44256-215">True</span></span> <br/><span data-ttu-id="44256-216">False (standaard)</span><span class="sxs-lookup"><span data-stu-id="44256-216">False (default)</span></span> |<span data-ttu-id="44256-217">Nee</span><span class="sxs-lookup"><span data-stu-id="44256-217">No</span></span> |
| <span data-ttu-id="44256-218">polyBaseSettings</span><span class="sxs-lookup"><span data-stu-id="44256-218">polyBaseSettings</span></span> |<span data-ttu-id="44256-219">Een groep met eigenschappen die kunnen worden opgegeven wanneer hello **allowPolybase** eigenschap is ingesteld, te**true**.</span><span class="sxs-lookup"><span data-stu-id="44256-219">A group of properties that can be specified when hello **allowPolybase** property is set too**true**.</span></span> |&nbsp; |<span data-ttu-id="44256-220">Nee</span><span class="sxs-lookup"><span data-stu-id="44256-220">No</span></span> |
| <span data-ttu-id="44256-221">rejectValue</span><span class="sxs-lookup"><span data-stu-id="44256-221">rejectValue</span></span> |<span data-ttu-id="44256-222">Hiermee geeft u op Hallo getal of het percentage van de rijen die kunnen worden afgewezen voordat het Hallo-query is mislukt.</span><span class="sxs-lookup"><span data-stu-id="44256-222">Specifies hello number or percentage of rows that can be rejected before hello query fails.</span></span> <br/><br/><span data-ttu-id="44256-223">Meer informatie over Hallo PolyBase van opties in Hallo afwijzen **argumenten** sectie van [maken EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="44256-223">Learn more about hello PolyBase’s reject options in hello **Arguments** section of [CREATE EXTERNAL TABLE (Transact-SQL)](https://msdn.microsoft.com/library/dn935021.aspx) topic.</span></span> |<span data-ttu-id="44256-224">0 (standaard), 1, 2...</span><span class="sxs-lookup"><span data-stu-id="44256-224">0 (default), 1, 2, …</span></span> |<span data-ttu-id="44256-225">Nee</span><span class="sxs-lookup"><span data-stu-id="44256-225">No</span></span> |
| <span data-ttu-id="44256-226">rejectType</span><span class="sxs-lookup"><span data-stu-id="44256-226">rejectType</span></span> |<span data-ttu-id="44256-227">Hiermee geeft u op of Hallo rejectValue optie is opgegeven als een letterlijke waarde of een percentage.</span><span class="sxs-lookup"><span data-stu-id="44256-227">Specifies whether hello rejectValue option is specified as a literal value or a percentage.</span></span> |<span data-ttu-id="44256-228">In waarde (standaard), Percentage</span><span class="sxs-lookup"><span data-stu-id="44256-228">Value (default), Percentage</span></span> |<span data-ttu-id="44256-229">Nee</span><span class="sxs-lookup"><span data-stu-id="44256-229">No</span></span> |
| <span data-ttu-id="44256-230">rejectSampleValue</span><span class="sxs-lookup"><span data-stu-id="44256-230">rejectSampleValue</span></span> |<span data-ttu-id="44256-231">Bepaalt het aantal rijen tooretrieve Hallo voordat Hallo PolyBase Hallo percentage geweigerde rijen opnieuw berekend.</span><span class="sxs-lookup"><span data-stu-id="44256-231">Determines hello number of rows tooretrieve before hello PolyBase recalculates hello percentage of rejected rows.</span></span> |<span data-ttu-id="44256-232">1, 2, …</span><span class="sxs-lookup"><span data-stu-id="44256-232">1, 2, …</span></span> |<span data-ttu-id="44256-233">Ja, als **rejectType** is **percentage**</span><span class="sxs-lookup"><span data-stu-id="44256-233">Yes, if **rejectType** is **percentage**</span></span> |
| <span data-ttu-id="44256-234">useTypeDefault</span><span class="sxs-lookup"><span data-stu-id="44256-234">useTypeDefault</span></span> |<span data-ttu-id="44256-235">Hiermee geeft u op hoe toohandle ontbreken waarden in tekstbestanden gescheiden wanneer PolyBase gegevens uit Hallo tekstbestand ophaalt.</span><span class="sxs-lookup"><span data-stu-id="44256-235">Specifies how toohandle missing values in delimited text files when PolyBase retrieves data from hello text file.</span></span><br/><br/><span data-ttu-id="44256-236">Meer informatie over deze eigenschap in Hallo argumenten sectie [maken EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span><span class="sxs-lookup"><span data-stu-id="44256-236">Learn more about this property from hello Arguments section in [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](https://msdn.microsoft.com/library/dn935026.aspx).</span></span> |<span data-ttu-id="44256-237">True, False (standaard)</span><span class="sxs-lookup"><span data-stu-id="44256-237">True, False (default)</span></span> |<span data-ttu-id="44256-238">Nee</span><span class="sxs-lookup"><span data-stu-id="44256-238">No</span></span> |
| <span data-ttu-id="44256-239">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="44256-239">writeBatchSize</span></span> |<span data-ttu-id="44256-240">Voegt de gegevens in SQL-tabel Hallo wanneer Hallo buffergrootte writeBatchSize bereikt</span><span class="sxs-lookup"><span data-stu-id="44256-240">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize</span></span> |<span data-ttu-id="44256-241">Geheel getal (aantal rijen)</span><span class="sxs-lookup"><span data-stu-id="44256-241">Integer (number of rows)</span></span> |<span data-ttu-id="44256-242">Nee (standaard: 10000)</span><span class="sxs-lookup"><span data-stu-id="44256-242">No (default: 10000)</span></span> |
| <span data-ttu-id="44256-243">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="44256-243">writeBatchTimeout</span></span> |<span data-ttu-id="44256-244">Wachttijd voor Hallo batch insert-bewerking toocomplete voordat een time-out optreedt.</span><span class="sxs-lookup"><span data-stu-id="44256-244">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="44256-245">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="44256-245">timespan</span></span><br/><br/> <span data-ttu-id="44256-246">Voorbeeld: "00: 30:00 ' (30 minuten).</span><span class="sxs-lookup"><span data-stu-id="44256-246">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="44256-247">Nee</span><span class="sxs-lookup"><span data-stu-id="44256-247">No</span></span> |

#### <a name="sqldwsink-example"></a><span data-ttu-id="44256-248">Voorbeeld van SqlDWSink</span><span class="sxs-lookup"><span data-stu-id="44256-248">SqlDWSink example</span></span>

```JSON
"sink": {
    "type": "SqlDWSink",
    "allowPolyBase": true
}
```

## <a name="use-polybase-tooload-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="44256-249">PolyBase tooload gegevens in Azure SQL Data Warehouse gebruiken</span><span class="sxs-lookup"><span data-stu-id="44256-249">Use PolyBase tooload data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="44256-250">Met behulp van  **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)**  is een efficiënte manier van het laden van grote hoeveelheid gegevens in Azure SQL Data Warehouse met hoge doorvoer.</span><span class="sxs-lookup"><span data-stu-id="44256-250">Using **[PolyBase](https://docs.microsoft.com/sql/relational-databases/polybase/polybase-guide)** is an efficient way of loading large amount of data into Azure SQL Data Warehouse with high throughput.</span></span> <span data-ttu-id="44256-251">U kunt een grote toename in doorvoer Hallo zien door met PolyBase in plaats van Hallo BULKINSERT standaardmechanisme.</span><span class="sxs-lookup"><span data-stu-id="44256-251">You can see a large gain in hello throughput by using PolyBase instead of hello default BULKINSERT mechanism.</span></span> <span data-ttu-id="44256-252">Zie [prestaties referentienummer kopiëren](data-factory-copy-activity-performance.md#performance-reference) met gedetailleerde vergelijking.</span><span class="sxs-lookup"><span data-stu-id="44256-252">See [copy performance reference number](data-factory-copy-activity-performance.md#performance-reference) with detailed comparison.</span></span> <span data-ttu-id="44256-253">Zie voor een overzicht met een gebruiksvoorbeeld [1 TB laden in Azure SQL Data Warehouse onder 15 minuten met Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span><span class="sxs-lookup"><span data-stu-id="44256-253">For a walkthrough with a use case, see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md).</span></span>

* <span data-ttu-id="44256-254">Als de brongegevens **Azure Blob- of Azure Data Lake Store**, en Hallo-indeling is compatibel met PolyBase, kunt u rechtstreeks tooAzure SQL Data Warehouse met PolyBase kopiëren.</span><span class="sxs-lookup"><span data-stu-id="44256-254">If your source data is in **Azure Blob or Azure Data Lake Store**, and hello format is compatible with PolyBase, you can directly copy tooAzure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="44256-255">Zie  **[Direct kopiëren met PolyBase](#direct-copy-using-polybase)**  met details.</span><span class="sxs-lookup"><span data-stu-id="44256-255">See **[Direct copy using PolyBase](#direct-copy-using-polybase)** with details.</span></span>
* <span data-ttu-id="44256-256">Als uw brongegevensarchief en de indeling wordt oorspronkelijk niet ondersteund door PolyBase, kunt u Hallo  **[gefaseerde kopiëren met PolyBase](#staged-copy-using-polybase)**  in plaats daarvan functie.</span><span class="sxs-lookup"><span data-stu-id="44256-256">If your source data store and format is not originally supported by PolyBase, you can use hello **[Staged Copy using PolyBase](#staged-copy-using-polybase)** feature instead.</span></span> <span data-ttu-id="44256-257">Dit biedt u ook betere doorvoer door automatisch converteren van Hallo gegevens naar de PolyBase-compatibele indeling en Hallo gegevens opslaan in Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="44256-257">It also provides you better throughput by automatically converting hello data into PolyBase-compatible format and storing hello data in Azure Blob storage.</span></span> <span data-ttu-id="44256-258">Vervolgens worden gegevens geladen in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="44256-258">It then loads data into SQL Data Warehouse.</span></span>

<span data-ttu-id="44256-259">Set Hallo `allowPolyBase` eigenschap te**true** zoals weergegeven in het volgende voorbeeld voor Azure Data Factory toouse PolyBase toocopy gegevens in Azure SQL Data Warehouse Hallo.</span><span class="sxs-lookup"><span data-stu-id="44256-259">Set hello `allowPolyBase` property too**true** as shown in hello following example for Azure Data Factory toouse PolyBase toocopy data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="44256-260">Als u allowPolyBase tootrue instelt, kunt u PolyBase specifieke eigenschappen met Hallo `polyBaseSettings` eigenschappengroep.</span><span class="sxs-lookup"><span data-stu-id="44256-260">When you set allowPolyBase tootrue, you can specify PolyBase specific properties using hello `polyBaseSettings` property group.</span></span> <span data-ttu-id="44256-261">Zie Hallo [SqlDWSink](#SqlDWSink) sectie voor meer informatie over de eigenschappen die u met polyBaseSettings gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="44256-261">see hello [SqlDWSink](#SqlDWSink) section for details about properties that you can use with polyBaseSettings.</span></span>

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

### <a name="direct-copy-using-polybase"></a><span data-ttu-id="44256-262">Directe kopiëren met PolyBase</span><span class="sxs-lookup"><span data-stu-id="44256-262">Direct copy using PolyBase</span></span>
<span data-ttu-id="44256-263">SQL Data Warehouse PolyBase ondersteuning rechtstreeks voor Azure-Blob en Azure Data Lake Store (met behulp van de service-principal) als bron en met vereisten voor een specifieke indeling.</span><span class="sxs-lookup"><span data-stu-id="44256-263">SQL Data Warehouse PolyBase directly support Azure Blob and Azure Data Lake Store (using service principal) as source and with specific file format requirements.</span></span> <span data-ttu-id="44256-264">Als de brongegevens voldoet aan Hallo criteria in deze sectie beschreven, kunt u rechtstreeks kopiëren van bron data store tooAzure die SQL Data Warehouse met PolyBase.</span><span class="sxs-lookup"><span data-stu-id="44256-264">If your source data meets hello criteria described in this section, you can directly copy from source data store tooAzure SQL Data Warehouse using PolyBase.</span></span> <span data-ttu-id="44256-265">Anders kunt u [gefaseerde kopiëren met PolyBase](#staged-copy-using-polybase).</span><span class="sxs-lookup"><span data-stu-id="44256-265">Otherwise, you can use [Staged Copy using PolyBase](#staged-copy-using-polybase).</span></span>

> [!TIP]
> <span data-ttu-id="44256-266">toocopy gegevens van Data Lake Store tooSQL Data Warehouse efficiënt, meer wilt weten van [Azure Data Factory maakt het eenvoudiger en handige toouncover inzicht in gegevens, zelfs als u Data Lake Store met SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="44256-266">toocopy data from Data Lake Store tooSQL Data Warehouse efficiently, learn more from [Azure Data Factory makes it even easier and convenient toouncover insights from data when using Data Lake Store with SQL Data Warehouse](https://blogs.msdn.microsoft.com/azuredatalake/2017/04/08/azure-data-factory-makes-it-even-easier-and-convenient-to-uncover-insights-from-data-when-using-data-lake-store-with-sql-data-warehouse/).</span></span>

<span data-ttu-id="44256-267">Als Hallo vereisten niet wordt voldaan, wordt Azure Data Factory Hallo instellingen controleert en automatisch terugvalt toohello BULKINSERT mechanisme voor gegevensverplaatsing Hallo.</span><span class="sxs-lookup"><span data-stu-id="44256-267">If hello requirements are not met, Azure Data Factory checks hello settings and automatically falls back toohello BULKINSERT mechanism for hello data movement.</span></span>

1. <span data-ttu-id="44256-268">**Bron gekoppelde service** is van het type: **AzureStorage** of **AzureDataLakeStore met verificatie van de service-principal**.</span><span class="sxs-lookup"><span data-stu-id="44256-268">**Source linked service** is of type: **AzureStorage** or **AzureDataLakeStore with service principal authentication**.</span></span>  
2. <span data-ttu-id="44256-269">Hallo **invoergegevensset** is van het type: **AzureBlob** of **AzureDataLakeStore**, en hello, indelingstype onder `type` eigenschappen is **OrcFormat** , of **TextFormat** Hello volgende configuraties:</span><span class="sxs-lookup"><span data-stu-id="44256-269">hello **input dataset** is of type: **AzureBlob** or **AzureDataLakeStore**, and hello format type under `type` properties is **OrcFormat**, or **TextFormat** with hello following configurations:</span></span>

   1. <span data-ttu-id="44256-270">`rowDelimiter`moet  **\n** .</span><span class="sxs-lookup"><span data-stu-id="44256-270">`rowDelimiter` must be **\n**.</span></span>
   2. <span data-ttu-id="44256-271">`nullValue`te is ingesteld,**lege tekenreeks** (""), of `treatEmptyAsNull` te is ingesteld,**true**.</span><span class="sxs-lookup"><span data-stu-id="44256-271">`nullValue` is set too**empty string** (""), or `treatEmptyAsNull` is set too**true**.</span></span>
   3. <span data-ttu-id="44256-272">`encodingName`te is ingesteld,**utf-8**, namelijk **standaard** waarde.</span><span class="sxs-lookup"><span data-stu-id="44256-272">`encodingName` is set too**utf-8**, which is **default** value.</span></span>
   4. <span data-ttu-id="44256-273">`escapeChar`, `quoteChar`, `firstRowAsHeader`, en `skipLineCount` zijn niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="44256-273">`escapeChar`, `quoteChar`, `firstRowAsHeader`, and `skipLineCount` are not specified.</span></span>
   5. <span data-ttu-id="44256-274">`compression`kan **geen compressie**, **GZip**, of **Deflate**.</span><span class="sxs-lookup"><span data-stu-id="44256-274">`compression` can be **no compression**, **GZip**, or **Deflate**.</span></span>

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

3. <span data-ttu-id="44256-275">Er is geen `skipHeaderLineCount` onder **BlobSource** of **AzureDataLakeStore** voor Hallo kopieeractiviteit in Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="44256-275">There is no `skipHeaderLineCount` setting under **BlobSource** or **AzureDataLakeStore** for hello Copy activity in hello pipeline.</span></span>
4. <span data-ttu-id="44256-276">Er is geen `sliceIdentifierColumnName` onder **SqlDWSink** voor Hallo kopieeractiviteit in Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="44256-276">There is no `sliceIdentifierColumnName` setting under **SqlDWSink** for hello Copy activity in hello pipeline.</span></span> <span data-ttu-id="44256-277">(PolyBase zorgt ervoor dat alle gegevens worden bijgewerkt of niet in een enkel uitvoering bijgewerkt wordt.</span><span class="sxs-lookup"><span data-stu-id="44256-277">(PolyBase guarantees that all data is updated or nothing is updated in a single run.</span></span> <span data-ttu-id="44256-278">tooachieve **herhaalbaarheid**, kunt u `sqlWriterCleanupScript`).</span><span class="sxs-lookup"><span data-stu-id="44256-278">tooachieve **repeatability**, you could use `sqlWriterCleanupScript`).</span></span>
5. <span data-ttu-id="44256-279">Er is geen `columnMapping` in Hallo gekoppeld in de kopieerbewerking wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="44256-279">There is no `columnMapping` being used in hello associated in Copy activity.</span></span>

### <a name="staged-copy-using-polybase"></a><span data-ttu-id="44256-280">Gefaseerde kopiëren met PolyBase</span><span class="sxs-lookup"><span data-stu-id="44256-280">Staged Copy using PolyBase</span></span>
<span data-ttu-id="44256-281">Als de brongegevens niet voldoet aan de Hallo criteria die zijn geïntroduceerd in de vorige sectie hello, kunt u kopiëren van gegevens via een tussentijdse staging Azure Blob Storage (kan niet voor Premium-opslag) inschakelen.</span><span class="sxs-lookup"><span data-stu-id="44256-281">When your source data doesn’t meet hello criteria introduced in hello previous section, you can enable copying data via an interim staging Azure Blob Storage (cannot be Premium Storage).</span></span> <span data-ttu-id="44256-282">In dit geval Azure Data Factory automatisch voert transformaties op Hallo toomeet gegevens indeling vereisten van gegevens en gebruik PolyBase tooload gegevens vervolgens PolyBase in SQL Data Warehouse en ten minste opschonen uw tijdelijke gegevens uit Hallo Blob storage.</span><span class="sxs-lookup"><span data-stu-id="44256-282">In this case, Azure Data Factory automatically performs transformations on hello data toomeet data format requirements of PolyBase, then use PolyBase tooload data into SQL Data Warehouse, and at last clean-up your temp data from hello Blob storage.</span></span> <span data-ttu-id="44256-283">Zie [kopie gefaseerde](data-factory-copy-activity-performance.md#staged-copy) voor meer informatie over de werking kopiëren van gegevens via een gefaseerde installatie Azure-Blob in het algemeen.</span><span class="sxs-lookup"><span data-stu-id="44256-283">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details on how copying data via a staging Azure Blob works in general.</span></span>

> [!NOTE]
> <span data-ttu-id="44256-284">Bij het kopiëren van gegevens uit een on-premises gegevens opslaan in Azure SQL Data Warehouse met PolyBase en fasering, als uw Data Management Gateway-versie lager dan 2.4 is Java Runtime Environment (Java Runtime Environment) is vereist op de gateway van de computer die is gebruikt tootransform de brongegevens in de juiste notatie.</span><span class="sxs-lookup"><span data-stu-id="44256-284">When copying data from an on-prem data store into Azure SQL Data Warehouse using PolyBase and staging, if your Data Management Gateway version is below 2.4, JRE (Java Runtime Environment) is required on your gateway machine that is used tootransform your source data into proper format.</span></span> <span data-ttu-id="44256-285">Stelt dat u uw gateway toohello nieuwste tooavoid deze afhankelijkheid upgraden.</span><span class="sxs-lookup"><span data-stu-id="44256-285">Suggest you upgrade your gateway toohello latest tooavoid such dependency.</span></span>
>

<span data-ttu-id="44256-286">toouse die deze functie, maakt een [gekoppelde Azure Storage-service](data-factory-azure-blob-connector.md#azure-storage-linked-service) die toohello Azure Storage-Account met Hallo tussentijdse blob storage verwijst, geeft u Hallo `enableStaging` en `stagingSettings` eigenschappen voor Hallo kopieerbewerking zoals u in de volgende code Hallo:</span><span class="sxs-lookup"><span data-stu-id="44256-286">toouse this feature, create an [Azure Storage linked service](data-factory-azure-blob-connector.md#azure-storage-linked-service) that refers toohello Azure Storage Account that has hello interim blob storage, then specify hello `enableStaging` and `stagingSettings` properties for hello Copy Activity as shown in hello following code:</span></span>

```json
"activities":[  
{
    "name": "Sample copy activity from SQL Server tooSQL Data Warehouse via PolyBase",
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

## <a name="best-practices-when-using-polybase"></a><span data-ttu-id="44256-287">Aanbevolen procedures voor met PolyBase</span><span class="sxs-lookup"><span data-stu-id="44256-287">Best practices when using PolyBase</span></span>
<span data-ttu-id="44256-288">Hallo volgende secties bevatten aanvullende best practices toohello die worden vermeld in [aanbevolen procedures voor Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="44256-288">hello following sections provide additional best practices toohello ones that are mentioned in [Best practices for Azure SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-best-practices.md).</span></span>

### <a name="required-database-permission"></a><span data-ttu-id="44256-289">Vereiste databasemachtiging</span><span class="sxs-lookup"><span data-stu-id="44256-289">Required database permission</span></span>
<span data-ttu-id="44256-290">toouse PolyBase, hiervoor Hallo gebruiker worden gegevens in SQL Data Warehouse gebruikte tooload heeft Hallo [machtiging "Beheer"](https://msdn.microsoft.com/library/ms191291.aspx) op Hallo doeldatabase.</span><span class="sxs-lookup"><span data-stu-id="44256-290">toouse PolyBase, it requires hello user being used tooload data into SQL Data Warehouse has hello ["CONTROL" permission](https://msdn.microsoft.com/library/ms191291.aspx) on hello target database.</span></span> <span data-ttu-id="44256-291">Eenzijdige tooachieve die tooadd die gebruiker als lid van de rol 'db_owner'.</span><span class="sxs-lookup"><span data-stu-id="44256-291">One way tooachieve that is tooadd that user as a member of "db_owner" role.</span></span> <span data-ttu-id="44256-292">Meer informatie over hoe toodo die door de volgende [in deze sectie](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span><span class="sxs-lookup"><span data-stu-id="44256-292">Learn how toodo that by following [this section](../sql-data-warehouse/sql-data-warehouse-overview-manage-security.md#authorization).</span></span>

### <a name="row-size-and-data-type-limitation"></a><span data-ttu-id="44256-293">Typ de beperking rijgrootte en gegevens</span><span class="sxs-lookup"><span data-stu-id="44256-293">Row size and data type limitation</span></span>
<span data-ttu-id="44256-294">Polybase-belastingen zijn beperkt tooloading rijen beide kleiner is dan **1 MB** en kan niet worden geladen tooVARCHR(MAX), NVARCHAR(MAX) of VARBINARY(MAX).</span><span class="sxs-lookup"><span data-stu-id="44256-294">Polybase loads are limited tooloading rows both smaller than **1 MB** and cannot load tooVARCHR(MAX), NVARCHAR(MAX) or VARBINARY(MAX).</span></span> <span data-ttu-id="44256-295">Raadpleeg te[hier](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span><span class="sxs-lookup"><span data-stu-id="44256-295">Refer too[here](../sql-data-warehouse/sql-data-warehouse-service-capacity-limits.md#loads).</span></span>

<span data-ttu-id="44256-296">Als u de brongegevens met rijen van de omvang is groter dan 1 MB hebt, kunt u toosplit Hallo brontabellen verticaal in verschillende kleine netwerken waar Hallo grootste rijgrootte van elk van deze Hallo limiet niet overschrijdt.</span><span class="sxs-lookup"><span data-stu-id="44256-296">If you have source data with rows of size greater than 1 MB, you may want toosplit hello source tables vertically into several small ones where hello largest row size of each of them does not exceed hello limit.</span></span> <span data-ttu-id="44256-297">Hallo kleinere tabellen kunnen vervolgens worden geladen met PolyBase en samengevoegd in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="44256-297">hello smaller tables can then be loaded using PolyBase and merged together in Azure SQL Data Warehouse.</span></span>

### <a name="sql-data-warehouse-resource-class"></a><span data-ttu-id="44256-298">De bronklasse SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="44256-298">SQL Data Warehouse resource class</span></span>
<span data-ttu-id="44256-299">tooachieve best mogelijke doorvoer, overweeg tooassign groter resource klasse toohello gebruiker wordt tooload gegevens in SQL Data Warehouse met PolyBase gebruikt.</span><span class="sxs-lookup"><span data-stu-id="44256-299">tooachieve best possible throughput, consider tooassign larger resource class toohello user being used tooload data into SQL Data Warehouse via PolyBase.</span></span> <span data-ttu-id="44256-300">Meer informatie over hoe toodo die door de volgende [wijzigen van een voorbeeld van een gebruiker resource klasse](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="44256-300">Learn how toodo that by following [Change a user resource class example](../sql-data-warehouse/sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

### <a name="tablename-in-azure-sql-data-warehouse"></a><span data-ttu-id="44256-301">tableName in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="44256-301">tableName in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="44256-302">Hallo volgende tabel bevat voorbeelden van hoe toospecify hello **tableName** eigenschap in de gegevensset JSON voor verschillende combinaties van schema en de tabelnaam.</span><span class="sxs-lookup"><span data-stu-id="44256-302">hello following table provides examples on how toospecify hello **tableName** property in dataset JSON for various combinations of schema and table name.</span></span>

| <span data-ttu-id="44256-303">DB Schema</span><span class="sxs-lookup"><span data-stu-id="44256-303">DB Schema</span></span> | <span data-ttu-id="44256-304">De tabelnaam van de</span><span class="sxs-lookup"><span data-stu-id="44256-304">Table name</span></span> | <span data-ttu-id="44256-305">JSON-eigenschap tableName</span><span class="sxs-lookup"><span data-stu-id="44256-305">tableName JSON property</span></span> |
| --- | --- | --- |
| <span data-ttu-id="44256-306">dbo</span><span class="sxs-lookup"><span data-stu-id="44256-306">dbo</span></span> |<span data-ttu-id="44256-307">MyTable</span><span class="sxs-lookup"><span data-stu-id="44256-307">MyTable</span></span> |<span data-ttu-id="44256-308">MyTable of dbo. MyTable of [dbo]. [MijnTabel]</span><span class="sxs-lookup"><span data-stu-id="44256-308">MyTable or dbo.MyTable or [dbo].[MyTable]</span></span> |
| <span data-ttu-id="44256-309">dbo1</span><span class="sxs-lookup"><span data-stu-id="44256-309">dbo1</span></span> |<span data-ttu-id="44256-310">MyTable</span><span class="sxs-lookup"><span data-stu-id="44256-310">MyTable</span></span> |<span data-ttu-id="44256-311">dbo1. MyTable of [dbo1]. [MijnTabel]</span><span class="sxs-lookup"><span data-stu-id="44256-311">dbo1.MyTable or [dbo1].[MyTable]</span></span> |
| <span data-ttu-id="44256-312">dbo</span><span class="sxs-lookup"><span data-stu-id="44256-312">dbo</span></span> |<span data-ttu-id="44256-313">My.Table</span><span class="sxs-lookup"><span data-stu-id="44256-313">My.Table</span></span> |<span data-ttu-id="44256-314">[My.Table] of [dbo]. [My.Table]</span><span class="sxs-lookup"><span data-stu-id="44256-314">[My.Table] or [dbo].[My.Table]</span></span> |
| <span data-ttu-id="44256-315">dbo1</span><span class="sxs-lookup"><span data-stu-id="44256-315">dbo1</span></span> |<span data-ttu-id="44256-316">My.Table</span><span class="sxs-lookup"><span data-stu-id="44256-316">My.Table</span></span> |<span data-ttu-id="44256-317">[dbo1]. [My.Table]</span><span class="sxs-lookup"><span data-stu-id="44256-317">[dbo1].[My.Table]</span></span> |

<span data-ttu-id="44256-318">Als u de volgende fout Hallo ziet, is het mogelijk een probleem met het Hallo-waarde die u hebt opgegeven voor de eigenschap tableName Hallo.</span><span class="sxs-lookup"><span data-stu-id="44256-318">If you see hello following error, it could be an issue with hello value you specified for hello tableName property.</span></span> <span data-ttu-id="44256-319">Zie de tabel Hallo voor Hallo juiste manier toospecify waarden voor de bijbehorende eigenschap tableName JSON Hallo.</span><span class="sxs-lookup"><span data-stu-id="44256-319">See hello table for hello correct way toospecify values for hello tableName JSON property.</span></span>  

```
Type=System.Data.SqlClient.SqlException,Message=Invalid object name 'stg.Account_test'.,Source=.Net SqlClient Data Provider
```

### <a name="columns-with-default-values"></a><span data-ttu-id="44256-320">Kolommen met standaardwaarden</span><span class="sxs-lookup"><span data-stu-id="44256-320">Columns with default values</span></span>
<span data-ttu-id="44256-321">Op dit moment PolyBase-functie in de Data Factory accepteert alleen hetzelfde aantal kolommen in de doeltabel Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="44256-321">Currently, PolyBase feature in Data Factory only accepts hello same number of columns as in hello target table.</span></span> <span data-ttu-id="44256-322">Stel, u hebt een tabel met vier kolommen en een ervan is gedefinieerd met een standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="44256-322">Say, you have a table with four columns and one of them is defined with a default value.</span></span> <span data-ttu-id="44256-323">Hallo invoergegevens moet nog steeds vier kolommen bevatten.</span><span class="sxs-lookup"><span data-stu-id="44256-323">hello input data should still contain four columns.</span></span> <span data-ttu-id="44256-324">Een invoergegevensset 3 kolommen bieden zou resulteert in een fout vergelijkbare toohello volgende bericht:</span><span class="sxs-lookup"><span data-stu-id="44256-324">Providing a 3-column input dataset would yield an error similar toohello following message:</span></span>

```
All columns of hello table must be specified in hello INSERT BULK statement.
```
<span data-ttu-id="44256-325">NULL-waarde is een speciale vorm van de standaardwaarde.</span><span class="sxs-lookup"><span data-stu-id="44256-325">NULL value is a special form of default value.</span></span> <span data-ttu-id="44256-326">Als Hallo kolom waarvoor null is toegestaan, kan het invoergegevens hello (in blob) voor de kolom leeg zijn (kan niet aanwezig zijn op Hallo invoergegevensset).</span><span class="sxs-lookup"><span data-stu-id="44256-326">If hello column is nullable, hello input data (in blob) for that column could be empty (cannot be missing from hello input dataset).</span></span> <span data-ttu-id="44256-327">PolyBase voegt NULL zijn voor deze in hello Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="44256-327">PolyBase inserts NULL for them in hello Azure SQL Data Warehouse.</span></span>  

## <a name="auto-table-creation"></a><span data-ttu-id="44256-328">Maken van de tabel automatisch</span><span class="sxs-lookup"><span data-stu-id="44256-328">Auto table creation</span></span>
<span data-ttu-id="44256-329">Als u gegevens van de Wizard kopiëren toocopy van SQL Server gebruikt of Azure SQL Database tooAzure SQL Data Warehouse en Hallo tabel die overeenkomt met de brontabel toohello niet in het doelarchief hello bestaat, maken Data Factory automatisch Hallo-tabel in Hallo het datawarehouse met behulp van de bron-tabelschema Hallo.</span><span class="sxs-lookup"><span data-stu-id="44256-329">If you are using Copy Wizard toocopy data from SQL Server or Azure SQL Database tooAzure SQL Data Warehouse and hello table that corresponds toohello source table does not exist in hello destination store, Data Factory can automatically create hello table in hello data warehouse by using hello source table schema.</span></span>

<span data-ttu-id="44256-330">Data Factory maakt Hallo tabel in het doelarchief Hallo Hello dezelfde naam in Hallo brongegevensarchief tabel.</span><span class="sxs-lookup"><span data-stu-id="44256-330">Data Factory creates hello table in hello destination store with hello same table name in hello source data store.</span></span> <span data-ttu-id="44256-331">Hallo-gegevenstypen voor kolommen worden gekozen op basis van Hallo toewijzing van het type te volgen.</span><span class="sxs-lookup"><span data-stu-id="44256-331">hello data types for columns are chosen based on hello following type mapping.</span></span> <span data-ttu-id="44256-332">Indien nodig, voert het type conversies toofix incompatibiliteitsproblemen tussen bron- en doelserver stores.</span><span class="sxs-lookup"><span data-stu-id="44256-332">If needed, it performs type conversions toofix any incompatibilities between source and destination stores.</span></span> <span data-ttu-id="44256-333">Round Robin tabeldistributie worden ook gebruikt.</span><span class="sxs-lookup"><span data-stu-id="44256-333">It also uses Round Robin table distribution.</span></span>

| <span data-ttu-id="44256-334">Type gegevensbron SQL Database-kolom</span><span class="sxs-lookup"><span data-stu-id="44256-334">Source SQL Database column type</span></span> | <span data-ttu-id="44256-335">Doel-SQL DW-kolomtype (de maximale grootte)</span><span class="sxs-lookup"><span data-stu-id="44256-335">Destination SQL DW column type (size limitation)</span></span> |
| --- | --- |
| <span data-ttu-id="44256-336">int</span><span class="sxs-lookup"><span data-stu-id="44256-336">Int</span></span> | <span data-ttu-id="44256-337">int</span><span class="sxs-lookup"><span data-stu-id="44256-337">Int</span></span> |
| <span data-ttu-id="44256-338">BigInt</span><span class="sxs-lookup"><span data-stu-id="44256-338">BigInt</span></span> | <span data-ttu-id="44256-339">BigInt</span><span class="sxs-lookup"><span data-stu-id="44256-339">BigInt</span></span> |
| <span data-ttu-id="44256-340">SmallInt</span><span class="sxs-lookup"><span data-stu-id="44256-340">SmallInt</span></span> | <span data-ttu-id="44256-341">SmallInt</span><span class="sxs-lookup"><span data-stu-id="44256-341">SmallInt</span></span> |
| <span data-ttu-id="44256-342">TinyInt</span><span class="sxs-lookup"><span data-stu-id="44256-342">TinyInt</span></span> | <span data-ttu-id="44256-343">TinyInt</span><span class="sxs-lookup"><span data-stu-id="44256-343">TinyInt</span></span> |
| <span data-ttu-id="44256-344">bits</span><span class="sxs-lookup"><span data-stu-id="44256-344">Bit</span></span> | <span data-ttu-id="44256-345">bits</span><span class="sxs-lookup"><span data-stu-id="44256-345">Bit</span></span> |
| <span data-ttu-id="44256-346">Decimale</span><span class="sxs-lookup"><span data-stu-id="44256-346">Decimal</span></span> | <span data-ttu-id="44256-347">Decimale</span><span class="sxs-lookup"><span data-stu-id="44256-347">Decimal</span></span> |
| <span data-ttu-id="44256-348">numerieke</span><span class="sxs-lookup"><span data-stu-id="44256-348">Numeric</span></span> | <span data-ttu-id="44256-349">Decimale</span><span class="sxs-lookup"><span data-stu-id="44256-349">Decimal</span></span> |
| <span data-ttu-id="44256-350">Float</span><span class="sxs-lookup"><span data-stu-id="44256-350">Float</span></span> | <span data-ttu-id="44256-351">Float</span><span class="sxs-lookup"><span data-stu-id="44256-351">Float</span></span> |
| <span data-ttu-id="44256-352">Money</span><span class="sxs-lookup"><span data-stu-id="44256-352">Money</span></span> | <span data-ttu-id="44256-353">Money</span><span class="sxs-lookup"><span data-stu-id="44256-353">Money</span></span> |
| <span data-ttu-id="44256-354">Real</span><span class="sxs-lookup"><span data-stu-id="44256-354">Real</span></span> | <span data-ttu-id="44256-355">Real</span><span class="sxs-lookup"><span data-stu-id="44256-355">Real</span></span> |
| <span data-ttu-id="44256-356">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="44256-356">SmallMoney</span></span> | <span data-ttu-id="44256-357">SmallMoney</span><span class="sxs-lookup"><span data-stu-id="44256-357">SmallMoney</span></span> |
| <span data-ttu-id="44256-358">Binaire</span><span class="sxs-lookup"><span data-stu-id="44256-358">Binary</span></span> | <span data-ttu-id="44256-359">Binaire</span><span class="sxs-lookup"><span data-stu-id="44256-359">Binary</span></span> |
| <span data-ttu-id="44256-360">varbinary</span><span class="sxs-lookup"><span data-stu-id="44256-360">Varbinary</span></span> | <span data-ttu-id="44256-361">Varbinary (omhoog too8000)</span><span class="sxs-lookup"><span data-stu-id="44256-361">Varbinary (up too8000)</span></span> |
| <span data-ttu-id="44256-362">Date</span><span class="sxs-lookup"><span data-stu-id="44256-362">Date</span></span> | <span data-ttu-id="44256-363">Date</span><span class="sxs-lookup"><span data-stu-id="44256-363">Date</span></span> |
| <span data-ttu-id="44256-364">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="44256-364">DateTime</span></span> | <span data-ttu-id="44256-365">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="44256-365">DateTime</span></span> |
| <span data-ttu-id="44256-366">DateTime2</span><span class="sxs-lookup"><span data-stu-id="44256-366">DateTime2</span></span> | <span data-ttu-id="44256-367">DateTime2</span><span class="sxs-lookup"><span data-stu-id="44256-367">DateTime2</span></span> |
| <span data-ttu-id="44256-368">Time</span><span class="sxs-lookup"><span data-stu-id="44256-368">Time</span></span> | <span data-ttu-id="44256-369">Time</span><span class="sxs-lookup"><span data-stu-id="44256-369">Time</span></span> |
| <span data-ttu-id="44256-370">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="44256-370">DateTimeOffset</span></span> | <span data-ttu-id="44256-371">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="44256-371">DateTimeOffset</span></span> |
| <span data-ttu-id="44256-372">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="44256-372">SmallDateTime</span></span> | <span data-ttu-id="44256-373">SmallDateTime</span><span class="sxs-lookup"><span data-stu-id="44256-373">SmallDateTime</span></span> |
| <span data-ttu-id="44256-374">Tekst</span><span class="sxs-lookup"><span data-stu-id="44256-374">Text</span></span> | <span data-ttu-id="44256-375">Varchar (omhoog too8000)</span><span class="sxs-lookup"><span data-stu-id="44256-375">Varchar (up too8000)</span></span> |
| <span data-ttu-id="44256-376">NText</span><span class="sxs-lookup"><span data-stu-id="44256-376">NText</span></span> | <span data-ttu-id="44256-377">NVarChar (omhoog too4000)</span><span class="sxs-lookup"><span data-stu-id="44256-377">NVarChar (up too4000)</span></span> |
| <span data-ttu-id="44256-378">Installatiekopie</span><span class="sxs-lookup"><span data-stu-id="44256-378">Image</span></span> | <span data-ttu-id="44256-379">VarBinary (omhoog too8000)</span><span class="sxs-lookup"><span data-stu-id="44256-379">VarBinary (up too8000)</span></span> |
| <span data-ttu-id="44256-380">UniqueIdentifier</span><span class="sxs-lookup"><span data-stu-id="44256-380">UniqueIdentifier</span></span> | <span data-ttu-id="44256-381">UniqueIdentifier</span><span class="sxs-lookup"><span data-stu-id="44256-381">UniqueIdentifier</span></span> |
| <span data-ttu-id="44256-382">CHAR</span><span class="sxs-lookup"><span data-stu-id="44256-382">Char</span></span> | <span data-ttu-id="44256-383">CHAR</span><span class="sxs-lookup"><span data-stu-id="44256-383">Char</span></span> |
| <span data-ttu-id="44256-384">NChar</span><span class="sxs-lookup"><span data-stu-id="44256-384">NChar</span></span> | <span data-ttu-id="44256-385">NChar</span><span class="sxs-lookup"><span data-stu-id="44256-385">NChar</span></span> |
| <span data-ttu-id="44256-386">VarChar</span><span class="sxs-lookup"><span data-stu-id="44256-386">VarChar</span></span> | <span data-ttu-id="44256-387">VarChar (omhoog too8000)</span><span class="sxs-lookup"><span data-stu-id="44256-387">VarChar (up too8000)</span></span> |
| <span data-ttu-id="44256-388">NVarChar</span><span class="sxs-lookup"><span data-stu-id="44256-388">NVarChar</span></span> | <span data-ttu-id="44256-389">NVarChar (omhoog too4000)</span><span class="sxs-lookup"><span data-stu-id="44256-389">NVarChar (up too4000)</span></span> |
| <span data-ttu-id="44256-390">XML</span><span class="sxs-lookup"><span data-stu-id="44256-390">Xml</span></span> | <span data-ttu-id="44256-391">Varchar (omhoog too8000)</span><span class="sxs-lookup"><span data-stu-id="44256-391">Varchar (up too8000)</span></span> |

[!INCLUDE [data-factory-type-repeatability-for-sql-sources](../../includes/data-factory-type-repeatability-for-sql-sources.md)]

## <a name="type-mapping-for-azure-sql-data-warehouse"></a><span data-ttu-id="44256-392">Toewijzing van het type voor Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="44256-392">Type mapping for Azure SQL Data Warehouse</span></span>
<span data-ttu-id="44256-393">Zoals vermeld in Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel kopieeractiviteit voert automatische typeconversies van brontypen typen toosink Hello 2 stap benadering te volgen:</span><span class="sxs-lookup"><span data-stu-id="44256-393">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="44256-394">Systeemeigen bron typen too.NET type converteren</span><span class="sxs-lookup"><span data-stu-id="44256-394">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="44256-395">Converteren van .NET-type toonative sink-type</span><span class="sxs-lookup"><span data-stu-id="44256-395">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="44256-396">Bij het verplaatsen van gegevens te & van Azure SQL Data Warehouse worden hello volgende toewijzingen gebruikt vanuit SQL type too.NET type en vice versa.</span><span class="sxs-lookup"><span data-stu-id="44256-396">When moving data too& from Azure SQL Data Warehouse, hello following mappings are used from SQL type too.NET type and vice versa.</span></span>

<span data-ttu-id="44256-397">Hallo-toewijzing is hetzelfde als Hallo [SQL Server gegevenstypetoewijzing voor ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span><span class="sxs-lookup"><span data-stu-id="44256-397">hello mapping is same as hello [SQL Server Data Type Mapping for ADO.NET](https://msdn.microsoft.com/library/cc716729.aspx).</span></span>

| <span data-ttu-id="44256-398">SQL Server Database Engine-type</span><span class="sxs-lookup"><span data-stu-id="44256-398">SQL Server Database Engine type</span></span> | <span data-ttu-id="44256-399">.NET framework-type</span><span class="sxs-lookup"><span data-stu-id="44256-399">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="44256-400">bigint</span><span class="sxs-lookup"><span data-stu-id="44256-400">bigint</span></span> |<span data-ttu-id="44256-401">Int64</span><span class="sxs-lookup"><span data-stu-id="44256-401">Int64</span></span> |
| <span data-ttu-id="44256-402">Binaire</span><span class="sxs-lookup"><span data-stu-id="44256-402">binary</span></span> |<span data-ttu-id="44256-403">Byte]</span><span class="sxs-lookup"><span data-stu-id="44256-403">Byte[]</span></span> |
| <span data-ttu-id="44256-404">bits</span><span class="sxs-lookup"><span data-stu-id="44256-404">bit</span></span> |<span data-ttu-id="44256-405">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="44256-405">Boolean</span></span> |
| <span data-ttu-id="44256-406">CHAR</span><span class="sxs-lookup"><span data-stu-id="44256-406">char</span></span> |<span data-ttu-id="44256-407">Tekenreeks, Char]</span><span class="sxs-lookup"><span data-stu-id="44256-407">String, Char[]</span></span> |
| <span data-ttu-id="44256-408">Datum</span><span class="sxs-lookup"><span data-stu-id="44256-408">date</span></span> |<span data-ttu-id="44256-409">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="44256-409">DateTime</span></span> |
| <span data-ttu-id="44256-410">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="44256-410">Datetime</span></span> |<span data-ttu-id="44256-411">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="44256-411">DateTime</span></span> |
| <span data-ttu-id="44256-412">datetime2</span><span class="sxs-lookup"><span data-stu-id="44256-412">datetime2</span></span> |<span data-ttu-id="44256-413">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="44256-413">DateTime</span></span> |
| <span data-ttu-id="44256-414">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="44256-414">Datetimeoffset</span></span> |<span data-ttu-id="44256-415">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="44256-415">DateTimeOffset</span></span> |
| <span data-ttu-id="44256-416">Decimale</span><span class="sxs-lookup"><span data-stu-id="44256-416">Decimal</span></span> |<span data-ttu-id="44256-417">Decimale</span><span class="sxs-lookup"><span data-stu-id="44256-417">Decimal</span></span> |
| <span data-ttu-id="44256-418">FILESTREAM-kenmerk (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="44256-418">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="44256-419">Byte]</span><span class="sxs-lookup"><span data-stu-id="44256-419">Byte[]</span></span> |
| <span data-ttu-id="44256-420">Float</span><span class="sxs-lookup"><span data-stu-id="44256-420">Float</span></span> |<span data-ttu-id="44256-421">dubbele</span><span class="sxs-lookup"><span data-stu-id="44256-421">Double</span></span> |
| <span data-ttu-id="44256-422">Afbeelding</span><span class="sxs-lookup"><span data-stu-id="44256-422">image</span></span> |<span data-ttu-id="44256-423">Byte]</span><span class="sxs-lookup"><span data-stu-id="44256-423">Byte[]</span></span> |
| <span data-ttu-id="44256-424">int</span><span class="sxs-lookup"><span data-stu-id="44256-424">int</span></span> |<span data-ttu-id="44256-425">Int32</span><span class="sxs-lookup"><span data-stu-id="44256-425">Int32</span></span> |
| <span data-ttu-id="44256-426">Money</span><span class="sxs-lookup"><span data-stu-id="44256-426">money</span></span> |<span data-ttu-id="44256-427">Decimale</span><span class="sxs-lookup"><span data-stu-id="44256-427">Decimal</span></span> |
| <span data-ttu-id="44256-428">nchar</span><span class="sxs-lookup"><span data-stu-id="44256-428">nchar</span></span> |<span data-ttu-id="44256-429">Tekenreeks, Char]</span><span class="sxs-lookup"><span data-stu-id="44256-429">String, Char[]</span></span> |
| <span data-ttu-id="44256-430">ntext</span><span class="sxs-lookup"><span data-stu-id="44256-430">ntext</span></span> |<span data-ttu-id="44256-431">Tekenreeks, Char]</span><span class="sxs-lookup"><span data-stu-id="44256-431">String, Char[]</span></span> |
| <span data-ttu-id="44256-432">numerieke</span><span class="sxs-lookup"><span data-stu-id="44256-432">numeric</span></span> |<span data-ttu-id="44256-433">Decimale</span><span class="sxs-lookup"><span data-stu-id="44256-433">Decimal</span></span> |
| <span data-ttu-id="44256-434">nvarchar</span><span class="sxs-lookup"><span data-stu-id="44256-434">nvarchar</span></span> |<span data-ttu-id="44256-435">Tekenreeks, Char]</span><span class="sxs-lookup"><span data-stu-id="44256-435">String, Char[]</span></span> |
| <span data-ttu-id="44256-436">echte</span><span class="sxs-lookup"><span data-stu-id="44256-436">real</span></span> |<span data-ttu-id="44256-437">Één</span><span class="sxs-lookup"><span data-stu-id="44256-437">Single</span></span> |
| <span data-ttu-id="44256-438">ROWVERSION</span><span class="sxs-lookup"><span data-stu-id="44256-438">rowversion</span></span> |<span data-ttu-id="44256-439">Byte]</span><span class="sxs-lookup"><span data-stu-id="44256-439">Byte[]</span></span> |
| <span data-ttu-id="44256-440">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="44256-440">smalldatetime</span></span> |<span data-ttu-id="44256-441">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="44256-441">DateTime</span></span> |
| <span data-ttu-id="44256-442">smallint</span><span class="sxs-lookup"><span data-stu-id="44256-442">smallint</span></span> |<span data-ttu-id="44256-443">Int16</span><span class="sxs-lookup"><span data-stu-id="44256-443">Int16</span></span> |
| <span data-ttu-id="44256-444">smallmoney</span><span class="sxs-lookup"><span data-stu-id="44256-444">smallmoney</span></span> |<span data-ttu-id="44256-445">Decimale</span><span class="sxs-lookup"><span data-stu-id="44256-445">Decimal</span></span> |
| <span data-ttu-id="44256-446">sql_variant</span><span class="sxs-lookup"><span data-stu-id="44256-446">sql_variant</span></span> |<span data-ttu-id="44256-447">Object *</span><span class="sxs-lookup"><span data-stu-id="44256-447">Object *</span></span> |
| <span data-ttu-id="44256-448">Tekst</span><span class="sxs-lookup"><span data-stu-id="44256-448">text</span></span> |<span data-ttu-id="44256-449">Tekenreeks, Char]</span><span class="sxs-lookup"><span data-stu-id="44256-449">String, Char[]</span></span> |
| <span data-ttu-id="44256-450">tijd</span><span class="sxs-lookup"><span data-stu-id="44256-450">time</span></span> |<span data-ttu-id="44256-451">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="44256-451">TimeSpan</span></span> |
| <span data-ttu-id="44256-452">tijdstempel</span><span class="sxs-lookup"><span data-stu-id="44256-452">timestamp</span></span> |<span data-ttu-id="44256-453">Byte]</span><span class="sxs-lookup"><span data-stu-id="44256-453">Byte[]</span></span> |
| <span data-ttu-id="44256-454">tinyint</span><span class="sxs-lookup"><span data-stu-id="44256-454">tinyint</span></span> |<span data-ttu-id="44256-455">Byte</span><span class="sxs-lookup"><span data-stu-id="44256-455">Byte</span></span> |
| <span data-ttu-id="44256-456">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="44256-456">uniqueidentifier</span></span> |<span data-ttu-id="44256-457">GUID</span><span class="sxs-lookup"><span data-stu-id="44256-457">Guid</span></span> |
| <span data-ttu-id="44256-458">varbinary</span><span class="sxs-lookup"><span data-stu-id="44256-458">varbinary</span></span> |<span data-ttu-id="44256-459">Byte]</span><span class="sxs-lookup"><span data-stu-id="44256-459">Byte[]</span></span> |
| <span data-ttu-id="44256-460">varchar</span><span class="sxs-lookup"><span data-stu-id="44256-460">varchar</span></span> |<span data-ttu-id="44256-461">Tekenreeks, Char]</span><span class="sxs-lookup"><span data-stu-id="44256-461">String, Char[]</span></span> |
| <span data-ttu-id="44256-462">xml</span><span class="sxs-lookup"><span data-stu-id="44256-462">xml</span></span> |<span data-ttu-id="44256-463">XML</span><span class="sxs-lookup"><span data-stu-id="44256-463">Xml</span></span> |

<span data-ttu-id="44256-464">U kunt ook kolommen uit de bron gegevensset toocolumns uit sink gegevensset in de definitie van de activiteit kopiëren Hallo toewijzen.</span><span class="sxs-lookup"><span data-stu-id="44256-464">You can also map columns from source dataset toocolumns from sink dataset in hello copy activity definition.</span></span> <span data-ttu-id="44256-465">Zie voor meer informatie [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="44256-465">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="json-examples-for-copying-data-tooand-from-sql-data-warehouse"></a><span data-ttu-id="44256-466">JSON-voorbeelden voor het kopiëren van gegevens tooand van SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="44256-466">JSON examples for copying data tooand from SQL Data Warehouse</span></span>
<span data-ttu-id="44256-467">Hallo volgende voorbeelden geven voorbeeld JSON definities waarmee u een pijplijn toocreate kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="44256-467">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="44256-468">Ze geven weer hoe toocopy gegevens tooand van Azure SQL Data Warehouse en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="44256-468">They show how toocopy data tooand from Azure SQL Data Warehouse and Azure Blob Storage.</span></span> <span data-ttu-id="44256-469">Echter gegevens kunnen worden gekopieerd **rechtstreeks** uit een van de bronnen tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="44256-469">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-data-warehouse-tooazure-blob"></a><span data-ttu-id="44256-470">Voorbeeld: Gegevens kopiëren van Azure SQL Data Warehouse tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="44256-470">Example: Copy data from Azure SQL Data Warehouse tooAzure Blob</span></span>
<span data-ttu-id="44256-471">Hallo voorbeeld definieert Hallo Data Factory-entiteiten te volgen:</span><span class="sxs-lookup"><span data-stu-id="44256-471">hello sample defines hello following Data Factory entities:</span></span>

1. <span data-ttu-id="44256-472">Een gekoppelde service van het type [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="44256-472">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="44256-473">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="44256-473">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="44256-474">Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureSqlDWTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="44256-474">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
4. <span data-ttu-id="44256-475">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="44256-475">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="44256-476">Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [SqlDWSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="44256-476">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [SqlDWSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="44256-477">Hallo voorbeeld kopieert tijdreeks (elk uur, dagelijks, enz.) gegevens uit een tabel in Azure SQL Data Warehouse-database tooa blob elk uur.</span><span class="sxs-lookup"><span data-stu-id="44256-477">hello sample copies time-series (hourly, daily, etc.) data from a table in Azure SQL Data Warehouse database tooa blob every hour.</span></span> <span data-ttu-id="44256-478">Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="44256-478">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="44256-479">**Azure SQL Data Warehouse gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="44256-479">**Azure SQL Data Warehouse linked service:**</span></span>

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
<span data-ttu-id="44256-480">**Azure Blob-opslag gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="44256-480">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="44256-481">**Azure SQL Data Warehouse invoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="44256-481">**Azure SQL Data Warehouse input dataset:**</span></span>

<span data-ttu-id="44256-482">Hallo-voorbeeld wordt ervan uitgegaan dat u hebt een tabel 'MijnTabel' gemaakt in Azure SQL Data Warehouse en bevat een kolom met de naam 'timestampcolumn' voor de reeksgegevens.</span><span class="sxs-lookup"><span data-stu-id="44256-482">hello sample assumes you have created a table “MyTable” in Azure SQL Data Warehouse and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="44256-483">Instelling 'extern': 'true' informeert Hallo Data Factory-service die gegevensset Hallo externe toohello data factory is en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="44256-483">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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
<span data-ttu-id="44256-484">**Azure Blob-uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="44256-484">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="44256-485">Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="44256-485">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="44256-486">pad naar map voor blob Hallo Hallo wordt dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="44256-486">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="44256-487">Hallo mappad jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="44256-487">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="44256-488">**De kopieeractiviteit in een pijplijn met SqlDWSource en BlobSink:**</span><span class="sxs-lookup"><span data-stu-id="44256-488">**Copy activity in a pipeline with SqlDWSource and BlobSink:**</span></span>

<span data-ttu-id="44256-489">Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur.</span><span class="sxs-lookup"><span data-stu-id="44256-489">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="44256-490">Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**SqlDWSource** en **sink** type is ingesteld, te**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="44256-490">In hello pipeline JSON definition, hello **source** type is set too**SqlDWSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="44256-491">Hallo SQL-query is opgegeven voor Hallo **SqlReaderQuery** eigenschap Hallo gegevens selecteert in Hallo voorbij toocopy uur.</span><span class="sxs-lookup"><span data-stu-id="44256-491">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

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
> <span data-ttu-id="44256-492">In voorbeeld Hallo **sqlReaderQuery** voor Hallo SqlDWSource is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="44256-492">In hello example, **sqlReaderQuery** is specified for hello SqlDWSource.</span></span> <span data-ttu-id="44256-493">Deze query Hallo Kopieeractiviteit uitgevoerd tegen Hallo tooget Azure SQL Data Warehouse-Hallo brongegevens.</span><span class="sxs-lookup"><span data-stu-id="44256-493">hello Copy Activity runs this query against hello Azure SQL Data Warehouse source tooget hello data.</span></span>
>
> <span data-ttu-id="44256-494">U kunt ook een opgeslagen procedure opgeven door te geven Hallo **sqlReaderStoredProcedureName** en **storedProcedureParameters** (als hello opgeslagen procedure parameters zijn vereist).</span><span class="sxs-lookup"><span data-stu-id="44256-494">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>
>
> <span data-ttu-id="44256-495">Als u geen sqlReaderQuery of sqlReaderStoredProcedureName opgeeft, Hallo kolommen die zijn gedefinieerd in de sectie Hallo structuur van Hallo gegevensset JSON gebruikte toobuild (Selecteer column1, column2 from MijnTabel) van een query zijn toorun tegen hello Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="44256-495">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query (select column1, column2 from mytable) toorun against hello Azure SQL Data Warehouse.</span></span> <span data-ttu-id="44256-496">Als de definitie van de gegevensset Hallo geen Hallo structuur, worden alle kolommen uit Hallo tabel geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="44256-496">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>
>
>

### <a name="example-copy-data-from-azure-blob-tooazure-sql-data-warehouse"></a><span data-ttu-id="44256-497">Voorbeeld: Gegevens kopiëren van Azure Blob-tooAzure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="44256-497">Example: Copy data from Azure Blob tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="44256-498">Hallo voorbeeld definieert Hallo Data Factory-entiteiten te volgen:</span><span class="sxs-lookup"><span data-stu-id="44256-498">hello sample defines hello following Data Factory entities:</span></span>

1. <span data-ttu-id="44256-499">Een gekoppelde service van het type [AzureSqlDW](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="44256-499">A linked service of type [AzureSqlDW](#linked-service-properties).</span></span>
2. <span data-ttu-id="44256-500">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="44256-500">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="44256-501">Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="44256-501">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="44256-502">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureSqlDWTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="44256-502">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlDWTable](#dataset-properties).</span></span>
5. <span data-ttu-id="44256-503">Een [pijplijn](data-factory-create-pipelines.md) met de kopieeractiviteit die gebruikmaakt van [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) en [SqlDWSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="44256-503">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlDWSink](#copy-activity-properties).</span></span>

<span data-ttu-id="44256-504">Hallo voorbeeld kopieert timeseries gegevens (elk uur, dagelijks, enzovoort) uit Azure blob tooa tabel in Azure SQL Data Warehouse-database om het uur.</span><span class="sxs-lookup"><span data-stu-id="44256-504">hello sample copies time-series data (hourly, daily, etc.) from Azure blob tooa table in Azure SQL Data Warehouse database every hour.</span></span> <span data-ttu-id="44256-505">Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="44256-505">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="44256-506">**Azure SQL Data Warehouse gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="44256-506">**Azure SQL Data Warehouse linked service:**</span></span>

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
<span data-ttu-id="44256-507">**Azure Blob-opslag gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="44256-507">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="44256-508">**Azure Blob invoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="44256-508">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="44256-509">Gegevens wordt opgehaald uit een nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="44256-509">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="44256-510">Hallo map pad en de naam voor de blob Hallo worden dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="44256-510">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="44256-511">Hallo mappad jaar, maand en dag deel uit van de begintijd Hallo en bestandsnaam gebruikt Hallo uur deel uit van de begintijd Hallo.</span><span class="sxs-lookup"><span data-stu-id="44256-511">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="44256-512">"extern": "true" instelling informeert Hallo Data Factory-service dat deze tabel externe toohello gegevensfactory en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="44256-512">“external”: “true” setting informs hello Data Factory service that this table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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
<span data-ttu-id="44256-513">**Azure SQL Data Warehouse uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="44256-513">**Azure SQL Data Warehouse output dataset:**</span></span>

<span data-ttu-id="44256-514">Hallo voorbeeld kopieert gegevens tooa tabel "MijnTabel" in Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="44256-514">hello sample copies data tooa table named “MyTable” in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="44256-515">Hallo-tabel maken in Azure SQL Data Warehouse met hetzelfde aantal kolommen Hallo zoals Hallo Blob CSV-bestand toocontain verwacht.</span><span class="sxs-lookup"><span data-stu-id="44256-515">Create hello table in Azure SQL Data Warehouse with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="44256-516">Nieuwe rijen worden toohello tabel toegevoegd om het uur.</span><span class="sxs-lookup"><span data-stu-id="44256-516">New rows are added toohello table every hour.</span></span>

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
<span data-ttu-id="44256-517">**De kopieeractiviteit in een pijplijn met BlobSource en SqlDWSink:**</span><span class="sxs-lookup"><span data-stu-id="44256-517">**Copy activity in a pipeline with BlobSource and SqlDWSink:**</span></span>

<span data-ttu-id="44256-518">Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur.</span><span class="sxs-lookup"><span data-stu-id="44256-518">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="44256-519">Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**BlobSource** en **sink** type is ingesteld, te**SqlDWSink**.</span><span class="sxs-lookup"><span data-stu-id="44256-519">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlDWSink**.</span></span>

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
<span data-ttu-id="44256-520">Zie voor een overzicht, Zie Hallo [1 TB laden in Azure SQL Data Warehouse onder 15 minuten met Azure Data Factory](data-factory-load-sql-data-warehouse.md) en [gegevens laden met Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) artikel in hello Azure SQL Data Warehouse documentatie.</span><span class="sxs-lookup"><span data-stu-id="44256-520">For a walkthrough, see hello see [Load 1 TB into Azure SQL Data Warehouse under 15 minutes with Azure Data Factory](data-factory-load-sql-data-warehouse.md) and [Load data with Azure Data Factory](../sql-data-warehouse/sql-data-warehouse-get-started-load-with-azure-data-factory.md) article in hello Azure SQL Data Warehouse documentation.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="44256-521">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="44256-521">Performance and Tuning</span></span>
<span data-ttu-id="44256-522">Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.</span><span class="sxs-lookup"><span data-stu-id="44256-522">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
