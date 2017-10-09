---
title: aaaCopy gegevens van/naar Azure SQL Database | Microsoft Docs
description: Meer informatie over hoe toocopy gegevens van/naar Azure SQL Database met Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 484f735b-8464-40ba-a9fc-820e6553159e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: d2ff16191afb028da75699c5e4d0bb310538db0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-database-using-azure-data-factory"></a><span data-ttu-id="d77e0-103">Tooand gegevens kopiëren van Azure SQL Database met Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d77e0-103">Copy data tooand from Azure SQL Database using Azure Data Factory</span></span>
<span data-ttu-id="d77e0-104">Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit Hallo in Azure Data Factory toomove gegevens tooand van Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="d77e0-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data tooand from Azure SQL Database.</span></span> <span data-ttu-id="d77e0-105">Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.</span><span class="sxs-lookup"><span data-stu-id="d77e0-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>  

## <a name="supported-scenarios"></a><span data-ttu-id="d77e0-106">Ondersteunde scenario 's</span><span class="sxs-lookup"><span data-stu-id="d77e0-106">Supported scenarios</span></span>
<span data-ttu-id="d77e0-107">U kunt gegevens kopiëren **van Azure SQL Database** toohello gegevensarchieven te volgen:</span><span class="sxs-lookup"><span data-stu-id="d77e0-107">You can copy data **from Azure SQL Database** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="d77e0-108">Gegevens kunnen worden gekopieerd van de volgende gegevensarchieven Hallo **tooAzure SQL-Database**:</span><span class="sxs-lookup"><span data-stu-id="d77e0-108">You can copy data from hello following data stores **tooAzure SQL Database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-authentication-type"></a><span data-ttu-id="d77e0-109">Ondersteund verificatietype</span><span class="sxs-lookup"><span data-stu-id="d77e0-109">Supported authentication type</span></span>
<span data-ttu-id="d77e0-110">Azure SQL Database-connector biedt ondersteuning voor basisverificatie.</span><span class="sxs-lookup"><span data-stu-id="d77e0-110">Azure SQL Database connector supports basic authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="d77e0-111">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="d77e0-111">Getting started</span></span>
<span data-ttu-id="d77e0-112">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens uit een Azure SQL Database verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="d77e0-112">You can create a pipeline with a copy activity that moves data to/from an Azure SQL Database by using different tools/APIs.</span></span>

<span data-ttu-id="d77e0-113">Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="d77e0-113">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="d77e0-114">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="d77e0-114">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="d77e0-115">U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="d77e0-115">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="d77e0-116">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="d77e0-116">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="d77e0-117">Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="d77e0-117">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="d77e0-118">Maak een **gegevensfactory**.</span><span class="sxs-lookup"><span data-stu-id="d77e0-118">Create a **data factory**.</span></span> <span data-ttu-id="d77e0-119">Een gegevensfactory kan één of meer pijplijnen bevatten.</span><span class="sxs-lookup"><span data-stu-id="d77e0-119">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="d77e0-120">Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="d77e0-120">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="d77e0-121">Bijvoorbeeld, als u gegevens uit een Azure blob storage tooan Azure SQL database kopiëren wilt, u twee gekoppelde services toolink uw Azure storage-account en de Azure SQL database tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="d77e0-121">For example, if you are copying data from an Azure blob storage tooan Azure SQL database, you create two linked services toolink your Azure storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="d77e0-122">Zie voor de gekoppelde service-eigenschappen die specifiek tooAzure SQL-Database, [gekoppelde service-eigenschappen](#linked-service-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="d77e0-122">For linked service properties that are specific tooAzure SQL Database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="d77e0-123">Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="d77e0-123">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="d77e0-124">In vermeld in de laatste stap Hallo Hallo voorbeeld maakt u een gegevensset toospecify Hallo blob-container en map met invoergegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="d77e0-124">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="d77e0-125">En u een andere dataset toospecify Hallo SQL-tabel maken in hello Azure SQL-database waarin Hallo-gegevens die zijn gekopieerd uit Hallo blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="d77e0-125">And, you create another dataset toospecify hello SQL table in hello Azure SQL database  that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="d77e0-126">Zie voor eigenschappen van gegevensset die specifieke tooAzure Data Lake Store, [eigenschappen van gegevensset](#dataset-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="d77e0-126">For dataset properties that are specific tooAzure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="d77e0-127">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="d77e0-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="d77e0-128">In Hallo voorbeeld eerder vermeld, gebruikt u BlobSource als een bron- en SqlSink als een sink voor de kopieeractiviteit Hallo.</span><span class="sxs-lookup"><span data-stu-id="d77e0-128">In hello example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for hello copy activity.</span></span> <span data-ttu-id="d77e0-129">Op dezelfde manier als u van Azure SQL Database tooAzure Blob Storage kopiëren wilt, gebruikt u SqlSource en BlobSink in Hallo kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="d77e0-129">Similarly, if you are copying from Azure SQL Database tooAzure Blob Storage, you use SqlSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="d77e0-130">Zie voor activiteitseigenschappen kopiëren die specifieke tooAzure SQL-Database, [activiteitseigenschappen kopiëren](#copy-activity-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="d77e0-130">For copy activity properties that are specific tooAzure SQL Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="d77e0-131">Voor informatie over hoe toouse een gegevensarchief als een bron of een sink, klikt u op Hallo-koppeling in de vorige sectie Hallo voor de gegevensopslag.</span><span class="sxs-lookup"><span data-stu-id="d77e0-131">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>

<span data-ttu-id="d77e0-132">Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="d77e0-132">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="d77e0-133">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="d77e0-133">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="d77e0-134">Zie voor voorbeelden met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens van/naar een Azure SQL Database zijn, [JSON voorbeelden](#json-examples-for-copying-data-to-and-from-sql-database) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="d77e0-134">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure SQL Database, see [JSON examples](#json-examples-for-copying-data-to-and-from-sql-database) section of this article.</span></span> 

<span data-ttu-id="d77e0-135">Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooAzure SQL-Database zijn:</span><span class="sxs-lookup"><span data-stu-id="d77e0-135">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure SQL Database:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="d77e0-136">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="d77e0-136">Linked service properties</span></span>
<span data-ttu-id="d77e0-137">Een Azure SQL gekoppelde service wordt een Azure SQL database tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="d77e0-137">An Azure SQL linked service links an Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="d77e0-138">Hallo volgende tabel bevat de beschrijving voor JSON-elementen specifieke tooAzure SQL gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="d77e0-138">hello following table provides description for JSON elements specific tooAzure SQL linked service.</span></span>

| <span data-ttu-id="d77e0-139">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="d77e0-139">Property</span></span> | <span data-ttu-id="d77e0-140">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d77e0-140">Description</span></span> | <span data-ttu-id="d77e0-141">Vereist</span><span class="sxs-lookup"><span data-stu-id="d77e0-141">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d77e0-142">type</span><span class="sxs-lookup"><span data-stu-id="d77e0-142">type</span></span> |<span data-ttu-id="d77e0-143">Hallo type eigenschap moet worden ingesteld op: **AzureSqlDatabase**</span><span class="sxs-lookup"><span data-stu-id="d77e0-143">hello type property must be set to: **AzureSqlDatabase**</span></span> |<span data-ttu-id="d77e0-144">Ja</span><span class="sxs-lookup"><span data-stu-id="d77e0-144">Yes</span></span> |
| <span data-ttu-id="d77e0-145">connectionString</span><span class="sxs-lookup"><span data-stu-id="d77e0-145">connectionString</span></span> |<span data-ttu-id="d77e0-146">Geef informatie tooconnect toohello Azure SQL Database-exemplaar voor de eigenschap connectionString Hallo nodig.</span><span class="sxs-lookup"><span data-stu-id="d77e0-146">Specify information needed tooconnect toohello Azure SQL Database instance for hello connectionString property.</span></span> <span data-ttu-id="d77e0-147">Alleen basisverificatie wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="d77e0-147">Only basic authentication is supported.</span></span> |<span data-ttu-id="d77e0-148">Ja</span><span class="sxs-lookup"><span data-stu-id="d77e0-148">Yes</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="d77e0-149">Configureer [Azure SQL Database-Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) Hallo databaseserver te[Azure Services tooaccess Hallo server toestaan](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span><span class="sxs-lookup"><span data-stu-id="d77e0-149">Configure [Azure SQL Database Firewall](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) hello database server too[allow Azure Services tooaccess hello server](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure).</span></span> <span data-ttu-id="d77e0-150">Bovendien configureren als u gegevens tooAzure SQL-Database kopieert van de externe Azure met inbegrip van on-premises gegevensbronnen met data factory-gateway, de juiste IP-adresbereik voor Hallo-machine dat gegevens tooAzure SQL-Database verzendt.</span><span class="sxs-lookup"><span data-stu-id="d77e0-150">Additionally, if you are copying data tooAzure SQL Database from outside Azure including from on-premises data sources with data factory gateway, configure appropriate IP address range for hello machine that is sending data tooAzure SQL Database.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="d77e0-151">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="d77e0-151">Dataset properties</span></span>
<span data-ttu-id="d77e0-152">een gegevensset toorepresent toospecify invoer- of -gegevens in een Azure SQL database, stelt u Hallo type-eigenschap van Hallo gegevensset: **AzureSqlTable**.</span><span class="sxs-lookup"><span data-stu-id="d77e0-152">toospecify a dataset toorepresent input or output data in an Azure SQL database, you set hello type property of hello dataset to: **AzureSqlTable**.</span></span> <span data-ttu-id="d77e0-153">Set Hallo **linkedServiceName** eigenschap van de naam van dataset toohello Hallo Hallo Azure SQL gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="d77e0-153">Set hello **linkedServiceName** property of hello dataset toohello name of hello Azure SQL linked service.</span></span>  

<span data-ttu-id="d77e0-154">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="d77e0-154">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="d77e0-155">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).</span><span class="sxs-lookup"><span data-stu-id="d77e0-155">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="d77e0-156">Hallo typeProperties sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="d77e0-156">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="d77e0-157">Hallo **typeProperties** sectie voor Hallo gegevensset van het type **AzureSqlTable** heeft Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="d77e0-157">hello **typeProperties** section for hello dataset of type **AzureSqlTable** has hello following properties:</span></span>

| <span data-ttu-id="d77e0-158">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="d77e0-158">Property</span></span> | <span data-ttu-id="d77e0-159">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d77e0-159">Description</span></span> | <span data-ttu-id="d77e0-160">Vereist</span><span class="sxs-lookup"><span data-stu-id="d77e0-160">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d77e0-161">tableName</span><span class="sxs-lookup"><span data-stu-id="d77e0-161">tableName</span></span> |<span data-ttu-id="d77e0-162">De naam van het Hallo-tabel of weergave in hello Azure SQL Database-exemplaar waarnaar de gekoppelde service verwijst.</span><span class="sxs-lookup"><span data-stu-id="d77e0-162">Name of hello table or view in hello Azure SQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="d77e0-163">Ja</span><span class="sxs-lookup"><span data-stu-id="d77e0-163">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="d77e0-164">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="d77e0-164">Copy activity properties</span></span>
<span data-ttu-id="d77e0-165">Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="d77e0-165">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="d77e0-166">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en -beleid zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="d77e0-166">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="d77e0-167">Hallo Kopieeractiviteit slechts één invoer en slechts één uitvoer produceert.</span><span class="sxs-lookup"><span data-stu-id="d77e0-167">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="d77e0-168">Dat eigenschappen beschikbaar zijn in Hallo **typeProperties** sectie van de activiteit Hallo variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="d77e0-168">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="d77e0-169">Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="d77e0-169">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="d77e0-170">Als u gegevens uit een Azure SQL-database verplaatst, u Hallo brontype instellen in de kopieerbewerking Hallo te**SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="d77e0-170">If you are moving data from an Azure SQL database, you set hello source type in hello copy activity too**SqlSource**.</span></span> <span data-ttu-id="d77e0-171">Als u gegevens tooan Azure SQL-database verplaatst, u stelt Hallo sink-type in de kopieerbewerking Hallo te**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="d77e0-171">Similarly, if you are moving data tooan Azure SQL database, you set hello sink type in hello copy activity too**SqlSink**.</span></span> <span data-ttu-id="d77e0-172">Deze sectie bevat een lijst met eigenschappen die worden ondersteund door SqlSource en SqlSink.</span><span class="sxs-lookup"><span data-stu-id="d77e0-172">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="d77e0-173">SqlSource</span><span class="sxs-lookup"><span data-stu-id="d77e0-173">SqlSource</span></span>
<span data-ttu-id="d77e0-174">In de kopieerbewerking wanneer Hallo bron van het type **SqlSource**, Hallo volgende eigenschappen beschikbaar zijn in **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="d77e0-174">In copy activity, when hello source is of type **SqlSource**, hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="d77e0-175">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="d77e0-175">Property</span></span> | <span data-ttu-id="d77e0-176">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d77e0-176">Description</span></span> | <span data-ttu-id="d77e0-177">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="d77e0-177">Allowed values</span></span> | <span data-ttu-id="d77e0-178">Vereist</span><span class="sxs-lookup"><span data-stu-id="d77e0-178">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d77e0-179">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="d77e0-179">sqlReaderQuery</span></span> |<span data-ttu-id="d77e0-180">Hallo aangepaste query tooread gegevens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d77e0-180">Use hello custom query tooread data.</span></span> |<span data-ttu-id="d77e0-181">SQL-query-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="d77e0-181">SQL query string.</span></span> <span data-ttu-id="d77e0-182">Voorbeeld: `select * from MyTable`.</span><span class="sxs-lookup"><span data-stu-id="d77e0-182">Example: `select * from MyTable`.</span></span> |<span data-ttu-id="d77e0-183">Nee</span><span class="sxs-lookup"><span data-stu-id="d77e0-183">No</span></span> |
| <span data-ttu-id="d77e0-184">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="d77e0-184">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="d77e0-185">Naam van Hallo opgeslagen procedure die gegevens uit Hallo brontabel leest.</span><span class="sxs-lookup"><span data-stu-id="d77e0-185">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="d77e0-186">Naam van Hallo opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="d77e0-186">Name of hello stored procedure.</span></span> <span data-ttu-id="d77e0-187">Hallo laatste SQL-instructie moet een SELECT-instructie in Hallo opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="d77e0-187">hello last SQL statement must be a SELECT statement in hello stored procedure.</span></span> |<span data-ttu-id="d77e0-188">Nee</span><span class="sxs-lookup"><span data-stu-id="d77e0-188">No</span></span> |
| <span data-ttu-id="d77e0-189">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="d77e0-189">storedProcedureParameters</span></span> |<span data-ttu-id="d77e0-190">Parameters voor Hallo opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="d77e0-190">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="d77e0-191">Naam/waarde-paren.</span><span class="sxs-lookup"><span data-stu-id="d77e0-191">Name/value pairs.</span></span> <span data-ttu-id="d77e0-192">Namen en hoofdlettergebruik van parameters moeten overeenkomen met Hallo namen en hoofdlettergebruik van Hallo opgeslagen procedureparameters.</span><span class="sxs-lookup"><span data-stu-id="d77e0-192">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="d77e0-193">Nee</span><span class="sxs-lookup"><span data-stu-id="d77e0-193">No</span></span> |

<span data-ttu-id="d77e0-194">Als hello **sqlReaderQuery** is opgegeven voor Hallo SqlSource, hello Kopieeractiviteit deze query wordt uitgevoerd tegen hello Azure SQL Database tooget Hallo brongegevens.</span><span class="sxs-lookup"><span data-stu-id="d77e0-194">If hello **sqlReaderQuery** is specified for hello SqlSource, hello Copy Activity runs this query against hello Azure SQL Database source tooget hello data.</span></span> <span data-ttu-id="d77e0-195">U kunt ook een opgeslagen procedure opgeven door te geven Hallo **sqlReaderStoredProcedureName** en **storedProcedureParameters** (als hello opgeslagen procedure parameters zijn vereist).</span><span class="sxs-lookup"><span data-stu-id="d77e0-195">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="d77e0-196">Als u geen sqlReaderQuery of sqlReaderStoredProcedureName opgeeft, Hallo kolommen die zijn gedefinieerd in de sectie Hallo structuur van Hallo gegevensset JSON gebruikte toobuild een query zijn (`select column1, column2 from mytable`) toorun tegen hello Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="d77e0-196">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query (`select column1, column2 from mytable`) toorun against hello Azure SQL Database.</span></span> <span data-ttu-id="d77e0-197">Als de definitie van de gegevensset Hallo geen Hallo structuur, worden alle kolommen uit Hallo tabel geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="d77e0-197">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="d77e0-198">Als u werkt met **sqlReaderStoredProcedureName**, moet u nog steeds toospecify een waarde voor Hallo **tableName** eigenschap in de gegevensset Hallo JSON.</span><span class="sxs-lookup"><span data-stu-id="d77e0-198">When you use **sqlReaderStoredProcedureName**, you still need toospecify a value for hello **tableName** property in hello dataset JSON.</span></span> <span data-ttu-id="d77e0-199">Er zijn geen controles uitgevoerd voor deze tabel al.</span><span class="sxs-lookup"><span data-stu-id="d77e0-199">There are no validations performed against this table though.</span></span>
>
>

### <a name="sqlsource-example"></a><span data-ttu-id="d77e0-200">Voorbeeld van SqlSource</span><span class="sxs-lookup"><span data-stu-id="d77e0-200">SqlSource example</span></span>

```JSON
"source": {
    "type": "SqlSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```

<span data-ttu-id="d77e0-201">**Hallo opgeslagen proceduredefinitie:**</span><span class="sxs-lookup"><span data-stu-id="d77e0-201">**hello stored procedure definition:**</span></span>

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

### <a name="sqlsink"></a><span data-ttu-id="d77e0-202">SqlSink</span><span class="sxs-lookup"><span data-stu-id="d77e0-202">SqlSink</span></span>
<span data-ttu-id="d77e0-203">**SqlSink** ondersteunt Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="d77e0-203">**SqlSink** supports hello following properties:</span></span>

| <span data-ttu-id="d77e0-204">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="d77e0-204">Property</span></span> | <span data-ttu-id="d77e0-205">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d77e0-205">Description</span></span> | <span data-ttu-id="d77e0-206">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="d77e0-206">Allowed values</span></span> | <span data-ttu-id="d77e0-207">Vereist</span><span class="sxs-lookup"><span data-stu-id="d77e0-207">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d77e0-208">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="d77e0-208">writeBatchTimeout</span></span> |<span data-ttu-id="d77e0-209">Wachttijd voor Hallo batch insert-bewerking toocomplete voordat een time-out optreedt.</span><span class="sxs-lookup"><span data-stu-id="d77e0-209">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="d77e0-210">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="d77e0-210">timespan</span></span><br/><br/> <span data-ttu-id="d77e0-211">Voorbeeld: "00: 30:00 ' (30 minuten).</span><span class="sxs-lookup"><span data-stu-id="d77e0-211">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="d77e0-212">Nee</span><span class="sxs-lookup"><span data-stu-id="d77e0-212">No</span></span> |
| <span data-ttu-id="d77e0-213">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="d77e0-213">writeBatchSize</span></span> |<span data-ttu-id="d77e0-214">Voegt de gegevens in SQL-tabel Hallo wanneer Hallo buffergrootte writeBatchSize bereikt.</span><span class="sxs-lookup"><span data-stu-id="d77e0-214">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="d77e0-215">Geheel getal (aantal rijen)</span><span class="sxs-lookup"><span data-stu-id="d77e0-215">Integer (number of rows)</span></span> |<span data-ttu-id="d77e0-216">Nee (standaard: 10000)</span><span class="sxs-lookup"><span data-stu-id="d77e0-216">No (default: 10000)</span></span> |
| <span data-ttu-id="d77e0-217">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="d77e0-217">sqlWriterCleanupScript</span></span> |<span data-ttu-id="d77e0-218">Geef een query voor de Kopieeractiviteit tooexecute zodat de gegevens van een bepaald segment wordt opgeschoond.</span><span class="sxs-lookup"><span data-stu-id="d77e0-218">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="d77e0-219">Zie voor meer informatie [herhaalbare kopiëren](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="d77e0-219">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="d77e0-220">Een query-instructie.</span><span class="sxs-lookup"><span data-stu-id="d77e0-220">A query statement.</span></span> |<span data-ttu-id="d77e0-221">Nee</span><span class="sxs-lookup"><span data-stu-id="d77e0-221">No</span></span> |
| <span data-ttu-id="d77e0-222">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="d77e0-222">sliceIdentifierColumnName</span></span> |<span data-ttu-id="d77e0-223">Geef de naam van een kolom voor de Kopieeractiviteit toofill met segment-ID automatisch gegenereerd en die is gebruikt tooclean van gegevens van een bepaald segment wanneer opnieuw uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d77e0-223">Specify a column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> <span data-ttu-id="d77e0-224">Zie voor meer informatie [herhaalbare kopiëren](#repeatable-copy).</span><span class="sxs-lookup"><span data-stu-id="d77e0-224">For more information, see [repeatable copy](#repeatable-copy).</span></span> |<span data-ttu-id="d77e0-225">De naam van de kolom van een kolom met gegevenstype binary(32).</span><span class="sxs-lookup"><span data-stu-id="d77e0-225">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="d77e0-226">Nee</span><span class="sxs-lookup"><span data-stu-id="d77e0-226">No</span></span> |
| <span data-ttu-id="d77e0-227">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="d77e0-227">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="d77e0-228">Naam van Hallo opgeslagen procedure die upserts (updates/INSERT) gegevens in de doeltabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="d77e0-228">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="d77e0-229">Naam van Hallo opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="d77e0-229">Name of hello stored procedure.</span></span> |<span data-ttu-id="d77e0-230">Nee</span><span class="sxs-lookup"><span data-stu-id="d77e0-230">No</span></span> |
| <span data-ttu-id="d77e0-231">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="d77e0-231">storedProcedureParameters</span></span> |<span data-ttu-id="d77e0-232">Parameters voor Hallo opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="d77e0-232">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="d77e0-233">Naam/waarde-paren.</span><span class="sxs-lookup"><span data-stu-id="d77e0-233">Name/value pairs.</span></span> <span data-ttu-id="d77e0-234">Namen en hoofdlettergebruik van parameters moeten overeenkomen met Hallo namen en hoofdlettergebruik van Hallo opgeslagen procedureparameters.</span><span class="sxs-lookup"><span data-stu-id="d77e0-234">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="d77e0-235">Nee</span><span class="sxs-lookup"><span data-stu-id="d77e0-235">No</span></span> |
| <span data-ttu-id="d77e0-236">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="d77e0-236">sqlWriterTableType</span></span> |<span data-ttu-id="d77e0-237">Geef een tabel type naam toobe in Hallo opgeslagen procedure gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d77e0-237">Specify a table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="d77e0-238">Kopieeractiviteit beschikbaar Hallo-gegevens worden verplaatst in een tijdelijke tabel met dit tabeltype.</span><span class="sxs-lookup"><span data-stu-id="d77e0-238">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="d77e0-239">Opgeslagen procedurecode kunt Hallo gegevens wordt gekopieerd met de bestaande gegevens vervolgens samenvoegen.</span><span class="sxs-lookup"><span data-stu-id="d77e0-239">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="d77e0-240">Een typenaam van de tabel.</span><span class="sxs-lookup"><span data-stu-id="d77e0-240">A table type name.</span></span> |<span data-ttu-id="d77e0-241">Nee</span><span class="sxs-lookup"><span data-stu-id="d77e0-241">No</span></span> |

#### <a name="sqlsink-example"></a><span data-ttu-id="d77e0-242">Voorbeeld van SqlSink</span><span class="sxs-lookup"><span data-stu-id="d77e0-242">SqlSink example</span></span>

```JSON
"sink": {
    "type": "SqlSink",
    "writeBatchSize": 1000000,
    "writeBatchTimeout": "00:05:00",
    "sqlWriterStoredProcedureName": "CopyTestStoredProcedureWithParameters",
    "sqlWriterTableType": "CopyTestTableType",
    "storedProcedureParameters": {
        "identifier": { "value": "1", "type": "Int" },
        "stringData": { "value": "str1" },
        "decimalData": { "value": "1", "type": "Decimal" }
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-sql-database"></a><span data-ttu-id="d77e0-243">JSON-voorbeelden voor het kopiëren van gegevens tooand uit SQL-Database</span><span class="sxs-lookup"><span data-stu-id="d77e0-243">JSON examples for copying data tooand from SQL Database</span></span>
<span data-ttu-id="d77e0-244">Hallo volgende voorbeelden geven voorbeeld JSON definities waarmee u een pijplijn toocreate kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d77e0-244">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="d77e0-245">Ze geven weer hoe toocopy gegevens tooand van Azure SQL Database en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="d77e0-245">They show how toocopy data tooand from Azure SQL Database and Azure Blob Storage.</span></span> <span data-ttu-id="d77e0-246">Echter gegevens kunnen worden gekopieerd **rechtstreeks** uit een van de bronnen tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d77e0-246">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="example-copy-data-from-azure-sql-database-tooazure-blob"></a><span data-ttu-id="d77e0-247">Voorbeeld: Gegevens kopiëren van Azure SQL Database tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="d77e0-247">Example: Copy data from Azure SQL Database tooAzure Blob</span></span>
<span data-ttu-id="d77e0-248">Hallo definieert dezelfde Hallo Data Factory-entiteiten te volgen:</span><span class="sxs-lookup"><span data-stu-id="d77e0-248">hello same defines hello following Data Factory entities:</span></span>

1. <span data-ttu-id="d77e0-249">Een gekoppelde service van het type [AzureSqlDatabase](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d77e0-249">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="d77e0-250">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d77e0-250">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="d77e0-251">Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureSqlTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d77e0-251">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
4. <span data-ttu-id="d77e0-252">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d77e0-252">An output [dataset](data-factory-create-datasets.md) of type [Azure Blob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="d77e0-253">Een [pijplijn](data-factory-create-pipelines.md) met een kopieeractiviteit die gebruikmaakt van [SqlSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="d77e0-253">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="d77e0-254">Hallo voorbeeld kopieert timeseries gegevens (elk uur, dagelijks, enzovoort) uit een tabel in Azure SQL database tooa blob elk uur.</span><span class="sxs-lookup"><span data-stu-id="d77e0-254">hello sample copies time-series data (hourly, daily, etc.) from a table in Azure SQL database tooa blob every hour.</span></span> <span data-ttu-id="d77e0-255">Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="d77e0-255">hello JSON properties used in these samples are described in sections following hello samples.</span></span>  

<span data-ttu-id="d77e0-256">**Azure SQL Database, gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="d77e0-256">**Azure SQL Database linked service:**</span></span>

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="d77e0-257">Zie Hallo [Azure SQL gekoppelde Service](#linked-service) sectie voor Hallo lijst van eigenschappen die worden ondersteund door deze gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="d77e0-257">See hello [Azure SQL Linked Service](#linked-service) section for hello list of properties supported by this linked service.</span></span>

<span data-ttu-id="d77e0-258">**Azure Blob-opslag gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="d77e0-258">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="d77e0-259">Zie Hallo [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) artikel voor Hallo lijst met eigenschappen die ondersteund worden door deze gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="d77e0-259">See hello [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for hello list of properties supported by this linked service.</span></span>


<span data-ttu-id="d77e0-260">**Azure SQL invoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="d77e0-260">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="d77e0-261">Hallo-voorbeeld wordt ervan uitgegaan dat u hebt een tabel 'MijnTabel' gemaakt in Azure SQL en bevat een kolom met de naam 'timestampcolumn' voor de reeksgegevens.</span><span class="sxs-lookup"><span data-stu-id="d77e0-261">hello sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="d77e0-262">Instelling 'extern': 'true' informeert hello Azure Data Factory-service die gegevensset Hallo externe toohello data factory is en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="d77e0-262">Setting “external”: ”true” informs hello Azure Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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

<span data-ttu-id="d77e0-263">Zie Hallo [type-eigenschappen van Azure SQL gegevensset](#dataset) sectie voor Hallo lijst van eigenschappen die worden ondersteund door dit type dataset.</span><span class="sxs-lookup"><span data-stu-id="d77e0-263">See hello [Azure SQL dataset type properties](#dataset) section for hello list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="d77e0-264">**Azure Blob-uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="d77e0-264">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="d77e0-265">Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="d77e0-265">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="d77e0-266">pad naar map voor blob Hallo Hallo wordt dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="d77e0-266">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="d77e0-267">Hallo mappad jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d77e0-267">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}/",
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
<span data-ttu-id="d77e0-268">Zie Hallo [type-eigenschappen van Azure Blob-gegevensset](data-factory-azure-blob-connector.md#dataset-properties) sectie voor Hallo lijst van eigenschappen die worden ondersteund door dit type dataset.</span><span class="sxs-lookup"><span data-stu-id="d77e0-268">See hello [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for hello list of properties supported by this dataset type.</span></span>  

<span data-ttu-id="d77e0-269">**Een kopieeractiviteit in een pijplijn met de SQL-bron en sink van Blob:**</span><span class="sxs-lookup"><span data-stu-id="d77e0-269">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="d77e0-270">Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur.</span><span class="sxs-lookup"><span data-stu-id="d77e0-270">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="d77e0-271">Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**SqlSource** en **sink** type is ingesteld, te**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="d77e0-271">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="d77e0-272">Hallo SQL-query is opgegeven voor Hallo **SqlReaderQuery** eigenschap Hallo gegevens selecteert in Hallo voorbij toocopy uur.</span><span class="sxs-lookup"><span data-stu-id="d77e0-272">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoBlob",
        "description": "copy activity",
        "type": "Copy",
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
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
<span data-ttu-id="d77e0-273">In voorbeeld Hallo **sqlReaderQuery** voor Hallo SqlSource is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="d77e0-273">In hello example, **sqlReaderQuery** is specified for hello SqlSource.</span></span> <span data-ttu-id="d77e0-274">Deze query Hallo Kopieeractiviteit uitgevoerd tegen Hallo tooget Azure SQL Database-Hallo brongegevens.</span><span class="sxs-lookup"><span data-stu-id="d77e0-274">hello Copy Activity runs this query against hello Azure SQL Database source tooget hello data.</span></span> <span data-ttu-id="d77e0-275">U kunt ook een opgeslagen procedure opgeven door te geven Hallo **sqlReaderStoredProcedureName** en **storedProcedureParameters** (als hello opgeslagen procedure parameters zijn vereist).</span><span class="sxs-lookup"><span data-stu-id="d77e0-275">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="d77e0-276">Als u geen sqlReaderQuery of sqlReaderStoredProcedureName opgeeft, zijn Hallo kolommen gedefinieerd in de sectie Hallo structuur van Hallo gegevensset JSON gebruikte toobuild een query toorun tegen hello Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="d77e0-276">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section of hello dataset JSON are used toobuild a query toorun against hello Azure SQL Database.</span></span> <span data-ttu-id="d77e0-277">Bijvoorbeeld: `select column1, column2 from mytable`.</span><span class="sxs-lookup"><span data-stu-id="d77e0-277">For example: `select column1, column2 from mytable`.</span></span> <span data-ttu-id="d77e0-278">Als de definitie van de gegevensset Hallo geen Hallo structuur, worden alle kolommen uit Hallo tabel geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="d77e0-278">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

<span data-ttu-id="d77e0-279">Zie Hallo [Sql-bron](#sqlsource) sectie en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) voor Hallo lijst met eigenschappen die ondersteund worden door SqlSource en BlobSink.</span><span class="sxs-lookup"><span data-stu-id="d77e0-279">See hello [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for hello list of properties supported by SqlSource and BlobSink.</span></span>

### <a name="example-copy-data-from-azure-blob-tooazure-sql-database"></a><span data-ttu-id="d77e0-280">Voorbeeld: Gegevens kopiëren van Azure Blob-tooAzure SQL-Database</span><span class="sxs-lookup"><span data-stu-id="d77e0-280">Example: Copy data from Azure Blob tooAzure SQL Database</span></span>
<span data-ttu-id="d77e0-281">Hallo voorbeeld definieert Hallo Data Factory-entiteiten te volgen:</span><span class="sxs-lookup"><span data-stu-id="d77e0-281">hello sample defines hello following Data Factory entities:</span></span>  

1. <span data-ttu-id="d77e0-282">Een gekoppelde service van het type [AzureSqlDatabase](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d77e0-282">A linked service of type [AzureSqlDatabase](#linked-service-properties).</span></span>
2. <span data-ttu-id="d77e0-283">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="d77e0-283">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="d77e0-284">Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d77e0-284">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="d77e0-285">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureSqlTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="d77e0-285">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](#dataset-properties).</span></span>
5. <span data-ttu-id="d77e0-286">Een [pijplijn](data-factory-create-pipelines.md) met de kopieeractiviteit die gebruikmaakt van [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) en [SqlSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="d77e0-286">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#copy-activity-properties).</span></span>

<span data-ttu-id="d77e0-287">Hallo voorbeeld kopieert timeseries gegevens (elk uur, dagelijks, enzovoort) uit Azure blob tooa tabel in Azure SQL database om het uur.</span><span class="sxs-lookup"><span data-stu-id="d77e0-287">hello sample copies time-series data (hourly, daily, etc.) from Azure blob tooa table in Azure SQL database every hour.</span></span> <span data-ttu-id="d77e0-288">Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="d77e0-288">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="d77e0-289">**Azure SQL gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="d77e0-289">**Azure SQL linked service:**</span></span>

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
<span data-ttu-id="d77e0-290">Zie Hallo [Azure SQL gekoppelde Service](#linked-service) sectie voor Hallo lijst van eigenschappen die worden ondersteund door deze gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="d77e0-290">See hello [Azure SQL Linked Service](#linked-service) section for hello list of properties supported by this linked service.</span></span>

<span data-ttu-id="d77e0-291">**Azure Blob-opslag gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="d77e0-291">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="d77e0-292">Zie Hallo [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) artikel voor Hallo lijst met eigenschappen die ondersteund worden door deze gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="d77e0-292">See hello [Azure Blob](data-factory-azure-blob-connector.md#azure-storage-linked-service) article for hello list of properties supported by this linked service.</span></span>


<span data-ttu-id="d77e0-293">**Azure Blob invoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="d77e0-293">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="d77e0-294">Gegevens wordt opgehaald uit een nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="d77e0-294">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="d77e0-295">Hallo map pad en de naam voor de blob Hallo worden dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="d77e0-295">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="d77e0-296">Hallo mappad jaar, maand en dag deel uit van de begintijd Hallo en bestandsnaam gebruikt Hallo uur deel uit van de begintijd Hallo.</span><span class="sxs-lookup"><span data-stu-id="d77e0-296">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="d77e0-297">"extern": "true" instelling informeert Hallo Data Factory-service dat deze tabel externe toohello gegevensfactory en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="d77e0-297">“external”: “true” setting informs hello Data Factory service that this table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
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
<span data-ttu-id="d77e0-298">Zie Hallo [type-eigenschappen van Azure Blob-gegevensset](data-factory-azure-blob-connector.md#dataset-properties) sectie voor Hallo lijst van eigenschappen die worden ondersteund door dit type dataset.</span><span class="sxs-lookup"><span data-stu-id="d77e0-298">See hello [Azure Blob dataset type properties](data-factory-azure-blob-connector.md#dataset-properties) section for hello list of properties supported by this dataset type.</span></span>

<span data-ttu-id="d77e0-299">**Azure SQL Database uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="d77e0-299">**Azure SQL Database output dataset:**</span></span>

<span data-ttu-id="d77e0-300">Hallo voorbeeld kopieert gegevens tooa tabel "MijnTabel" in Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="d77e0-300">hello sample copies data tooa table named “MyTable” in Azure SQL.</span></span> <span data-ttu-id="d77e0-301">Hallo-tabel maken in Azure SQL met hetzelfde aantal kolommen Hallo zoals Hallo Blob CSV-bestand toocontain verwacht.</span><span class="sxs-lookup"><span data-stu-id="d77e0-301">Create hello table in Azure SQL with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="d77e0-302">Nieuwe rijen worden toohello tabel toegevoegd om het uur.</span><span class="sxs-lookup"><span data-stu-id="d77e0-302">New rows are added toohello table every hour.</span></span>

```JSON
{
  "name": "AzureSqlOutput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
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
<span data-ttu-id="d77e0-303">Zie Hallo [type-eigenschappen van Azure SQL gegevensset](#dataset) sectie voor Hallo lijst van eigenschappen die worden ondersteund door dit type dataset.</span><span class="sxs-lookup"><span data-stu-id="d77e0-303">See hello [Azure SQL dataset type properties](#dataset) section for hello list of properties supported by this dataset type.</span></span>

<span data-ttu-id="d77e0-304">**Een kopieeractiviteit in een pijplijn met Blob-bron en sink SQL:**</span><span class="sxs-lookup"><span data-stu-id="d77e0-304">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="d77e0-305">Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur.</span><span class="sxs-lookup"><span data-stu-id="d77e0-305">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="d77e0-306">Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**BlobSource** en **sink** type is ingesteld, te**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="d77e0-306">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlSink"
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
<span data-ttu-id="d77e0-307">Zie Hallo [Sql Sink](#sqlsink) sectie en [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) voor Hallo lijst met eigenschappen die ondersteund worden door SqlSink en BlobSource.</span><span class="sxs-lookup"><span data-stu-id="d77e0-307">See hello [Sql Sink](#sqlsink) section and [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) for hello list of properties supported by SqlSink and BlobSource.</span></span>

## <a name="identity-columns-in-hello-target-database"></a><span data-ttu-id="d77e0-308">Id-kolommen in de doeldatabase Hallo</span><span class="sxs-lookup"><span data-stu-id="d77e0-308">Identity columns in hello target database</span></span>
<span data-ttu-id="d77e0-309">Deze sectie toont een voorbeeld van het kopiëren van gegevens uit een brontabel zonder een doeltabel identiteit kolom tooa met een identiteitskolom.</span><span class="sxs-lookup"><span data-stu-id="d77e0-309">This section provides an example for copying data from a source table without an identity column tooa destination table with an identity column.</span></span>

<span data-ttu-id="d77e0-310">**Brontabel:**</span><span class="sxs-lookup"><span data-stu-id="d77e0-310">**Source table:**</span></span>

```SQL
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="d77e0-311">**Doeltabel:**</span><span class="sxs-lookup"><span data-stu-id="d77e0-311">**Destination table:**</span></span>

```SQL
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```
<span data-ttu-id="d77e0-312">U ziet dat doeltabel Hallo heeft een identiteitskolom.</span><span class="sxs-lookup"><span data-stu-id="d77e0-312">Notice that hello target table has an identity column.</span></span>

<span data-ttu-id="d77e0-313">**Bron gegevensset JSON-definitie**</span><span class="sxs-lookup"><span data-stu-id="d77e0-313">**Source dataset JSON definition**</span></span>

```JSON
{
    "name": "SampleSource",
    "properties": {
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
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
<span data-ttu-id="d77e0-314">**Doel-dataset JSON-definitie**</span><span class="sxs-lookup"><span data-stu-id="d77e0-314">**Destination dataset JSON definition**</span></span>

```JSON
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }    
}
```

<span data-ttu-id="d77e0-315">Merk op dat als de bron en doel-tabel verschillende schema's zijn (doel heeft een extra kolom met de identiteit).</span><span class="sxs-lookup"><span data-stu-id="d77e0-315">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="d77e0-316">In dit scenario moet u toospecify **structuur** eigenschap in Hallo doel gegevenssetdefinitie, waaronder Hallo identiteitskolom niet.</span><span class="sxs-lookup"><span data-stu-id="d77e0-316">In this scenario, you need toospecify **structure** property in hello target dataset definition, which doesn’t include hello identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="d77e0-317">Aanroepen van opgeslagen procedure uit SQL-sink</span><span class="sxs-lookup"><span data-stu-id="d77e0-317">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="d77e0-318">Zie voor een voorbeeld van een opgeslagen procedure van SQL-sink in een kopieeractiviteit van een pijplijn wordt aangeroepen, [opgeslagen procedure voor SQL-sink aanroepen in de kopieerbewerking](data-factory-invoke-stored-procedure-from-copy-activity.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="d77e0-318">For an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline, see [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article.</span></span> 

## <a name="type-mapping-for-azure-sql-database"></a><span data-ttu-id="d77e0-319">Toewijzing van het type voor Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="d77e0-319">Type mapping for Azure SQL Database</span></span>
<span data-ttu-id="d77e0-320">Zoals vermeld in Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel kopieeractiviteit voert automatische typeconversies van brontypen typen toosink Hello 2 stap benadering te volgen:</span><span class="sxs-lookup"><span data-stu-id="d77e0-320">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="d77e0-321">Systeemeigen bron typen too.NET type converteren</span><span class="sxs-lookup"><span data-stu-id="d77e0-321">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="d77e0-322">Converteren van .NET-type toonative sink-type</span><span class="sxs-lookup"><span data-stu-id="d77e0-322">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="d77e0-323">Bij het verplaatsen van gegevens tooand van Azure SQL Database, worden hello volgende toewijzingen gebruikt vanuit SQL type too.NET type en vice versa.</span><span class="sxs-lookup"><span data-stu-id="d77e0-323">When moving data tooand from Azure SQL Database, hello following mappings are used from SQL type too.NET type and vice versa.</span></span> <span data-ttu-id="d77e0-324">Hallo-toewijzing is hetzelfde als SQL Server gegevenstypetoewijzing voor ADO.NET Hallo.</span><span class="sxs-lookup"><span data-stu-id="d77e0-324">hello mapping is same as hello SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="d77e0-325">SQL Server Database Engine-type</span><span class="sxs-lookup"><span data-stu-id="d77e0-325">SQL Server Database Engine type</span></span> | <span data-ttu-id="d77e0-326">.NET framework-type</span><span class="sxs-lookup"><span data-stu-id="d77e0-326">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="d77e0-327">bigint</span><span class="sxs-lookup"><span data-stu-id="d77e0-327">bigint</span></span> |<span data-ttu-id="d77e0-328">Int64</span><span class="sxs-lookup"><span data-stu-id="d77e0-328">Int64</span></span> |
| <span data-ttu-id="d77e0-329">Binaire</span><span class="sxs-lookup"><span data-stu-id="d77e0-329">binary</span></span> |<span data-ttu-id="d77e0-330">Byte]</span><span class="sxs-lookup"><span data-stu-id="d77e0-330">Byte[]</span></span> |
| <span data-ttu-id="d77e0-331">bits</span><span class="sxs-lookup"><span data-stu-id="d77e0-331">bit</span></span> |<span data-ttu-id="d77e0-332">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="d77e0-332">Boolean</span></span> |
| <span data-ttu-id="d77e0-333">CHAR</span><span class="sxs-lookup"><span data-stu-id="d77e0-333">char</span></span> |<span data-ttu-id="d77e0-334">Tekenreeks, Char]</span><span class="sxs-lookup"><span data-stu-id="d77e0-334">String, Char[]</span></span> |
| <span data-ttu-id="d77e0-335">Datum</span><span class="sxs-lookup"><span data-stu-id="d77e0-335">date</span></span> |<span data-ttu-id="d77e0-336">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="d77e0-336">DateTime</span></span> |
| <span data-ttu-id="d77e0-337">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="d77e0-337">Datetime</span></span> |<span data-ttu-id="d77e0-338">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="d77e0-338">DateTime</span></span> |
| <span data-ttu-id="d77e0-339">datetime2</span><span class="sxs-lookup"><span data-stu-id="d77e0-339">datetime2</span></span> |<span data-ttu-id="d77e0-340">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="d77e0-340">DateTime</span></span> |
| <span data-ttu-id="d77e0-341">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="d77e0-341">Datetimeoffset</span></span> |<span data-ttu-id="d77e0-342">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="d77e0-342">DateTimeOffset</span></span> |
| <span data-ttu-id="d77e0-343">Decimale</span><span class="sxs-lookup"><span data-stu-id="d77e0-343">Decimal</span></span> |<span data-ttu-id="d77e0-344">Decimale</span><span class="sxs-lookup"><span data-stu-id="d77e0-344">Decimal</span></span> |
| <span data-ttu-id="d77e0-345">FILESTREAM-kenmerk (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="d77e0-345">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="d77e0-346">Byte]</span><span class="sxs-lookup"><span data-stu-id="d77e0-346">Byte[]</span></span> |
| <span data-ttu-id="d77e0-347">Float</span><span class="sxs-lookup"><span data-stu-id="d77e0-347">Float</span></span> |<span data-ttu-id="d77e0-348">dubbele</span><span class="sxs-lookup"><span data-stu-id="d77e0-348">Double</span></span> |
| <span data-ttu-id="d77e0-349">Afbeelding</span><span class="sxs-lookup"><span data-stu-id="d77e0-349">image</span></span> |<span data-ttu-id="d77e0-350">Byte]</span><span class="sxs-lookup"><span data-stu-id="d77e0-350">Byte[]</span></span> |
| <span data-ttu-id="d77e0-351">int</span><span class="sxs-lookup"><span data-stu-id="d77e0-351">int</span></span> |<span data-ttu-id="d77e0-352">Int32</span><span class="sxs-lookup"><span data-stu-id="d77e0-352">Int32</span></span> |
| <span data-ttu-id="d77e0-353">Money</span><span class="sxs-lookup"><span data-stu-id="d77e0-353">money</span></span> |<span data-ttu-id="d77e0-354">Decimale</span><span class="sxs-lookup"><span data-stu-id="d77e0-354">Decimal</span></span> |
| <span data-ttu-id="d77e0-355">nchar</span><span class="sxs-lookup"><span data-stu-id="d77e0-355">nchar</span></span> |<span data-ttu-id="d77e0-356">Tekenreeks, Char]</span><span class="sxs-lookup"><span data-stu-id="d77e0-356">String, Char[]</span></span> |
| <span data-ttu-id="d77e0-357">ntext</span><span class="sxs-lookup"><span data-stu-id="d77e0-357">ntext</span></span> |<span data-ttu-id="d77e0-358">Tekenreeks, Char]</span><span class="sxs-lookup"><span data-stu-id="d77e0-358">String, Char[]</span></span> |
| <span data-ttu-id="d77e0-359">numerieke</span><span class="sxs-lookup"><span data-stu-id="d77e0-359">numeric</span></span> |<span data-ttu-id="d77e0-360">Decimale</span><span class="sxs-lookup"><span data-stu-id="d77e0-360">Decimal</span></span> |
| <span data-ttu-id="d77e0-361">nvarchar</span><span class="sxs-lookup"><span data-stu-id="d77e0-361">nvarchar</span></span> |<span data-ttu-id="d77e0-362">Tekenreeks, Char]</span><span class="sxs-lookup"><span data-stu-id="d77e0-362">String, Char[]</span></span> |
| <span data-ttu-id="d77e0-363">echte</span><span class="sxs-lookup"><span data-stu-id="d77e0-363">real</span></span> |<span data-ttu-id="d77e0-364">Één</span><span class="sxs-lookup"><span data-stu-id="d77e0-364">Single</span></span> |
| <span data-ttu-id="d77e0-365">ROWVERSION</span><span class="sxs-lookup"><span data-stu-id="d77e0-365">rowversion</span></span> |<span data-ttu-id="d77e0-366">Byte]</span><span class="sxs-lookup"><span data-stu-id="d77e0-366">Byte[]</span></span> |
| <span data-ttu-id="d77e0-367">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="d77e0-367">smalldatetime</span></span> |<span data-ttu-id="d77e0-368">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="d77e0-368">DateTime</span></span> |
| <span data-ttu-id="d77e0-369">smallint</span><span class="sxs-lookup"><span data-stu-id="d77e0-369">smallint</span></span> |<span data-ttu-id="d77e0-370">Int16</span><span class="sxs-lookup"><span data-stu-id="d77e0-370">Int16</span></span> |
| <span data-ttu-id="d77e0-371">smallmoney</span><span class="sxs-lookup"><span data-stu-id="d77e0-371">smallmoney</span></span> |<span data-ttu-id="d77e0-372">Decimale</span><span class="sxs-lookup"><span data-stu-id="d77e0-372">Decimal</span></span> |
| <span data-ttu-id="d77e0-373">sql_variant</span><span class="sxs-lookup"><span data-stu-id="d77e0-373">sql_variant</span></span> |<span data-ttu-id="d77e0-374">Object *</span><span class="sxs-lookup"><span data-stu-id="d77e0-374">Object *</span></span> |
| <span data-ttu-id="d77e0-375">Tekst</span><span class="sxs-lookup"><span data-stu-id="d77e0-375">text</span></span> |<span data-ttu-id="d77e0-376">Tekenreeks, Char]</span><span class="sxs-lookup"><span data-stu-id="d77e0-376">String, Char[]</span></span> |
| <span data-ttu-id="d77e0-377">tijd</span><span class="sxs-lookup"><span data-stu-id="d77e0-377">time</span></span> |<span data-ttu-id="d77e0-378">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="d77e0-378">TimeSpan</span></span> |
| <span data-ttu-id="d77e0-379">tijdstempel</span><span class="sxs-lookup"><span data-stu-id="d77e0-379">timestamp</span></span> |<span data-ttu-id="d77e0-380">Byte]</span><span class="sxs-lookup"><span data-stu-id="d77e0-380">Byte[]</span></span> |
| <span data-ttu-id="d77e0-381">tinyint</span><span class="sxs-lookup"><span data-stu-id="d77e0-381">tinyint</span></span> |<span data-ttu-id="d77e0-382">Byte</span><span class="sxs-lookup"><span data-stu-id="d77e0-382">Byte</span></span> |
| <span data-ttu-id="d77e0-383">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="d77e0-383">uniqueidentifier</span></span> |<span data-ttu-id="d77e0-384">GUID</span><span class="sxs-lookup"><span data-stu-id="d77e0-384">Guid</span></span> |
| <span data-ttu-id="d77e0-385">varbinary</span><span class="sxs-lookup"><span data-stu-id="d77e0-385">varbinary</span></span> |<span data-ttu-id="d77e0-386">Byte]</span><span class="sxs-lookup"><span data-stu-id="d77e0-386">Byte[]</span></span> |
| <span data-ttu-id="d77e0-387">varchar</span><span class="sxs-lookup"><span data-stu-id="d77e0-387">varchar</span></span> |<span data-ttu-id="d77e0-388">Tekenreeks, Char]</span><span class="sxs-lookup"><span data-stu-id="d77e0-388">String, Char[]</span></span> |
| <span data-ttu-id="d77e0-389">xml</span><span class="sxs-lookup"><span data-stu-id="d77e0-389">xml</span></span> |<span data-ttu-id="d77e0-390">XML</span><span class="sxs-lookup"><span data-stu-id="d77e0-390">Xml</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="d77e0-391">Bronkolommen toosink toewijzen</span><span class="sxs-lookup"><span data-stu-id="d77e0-391">Map source toosink columns</span></span>
<span data-ttu-id="d77e0-392">Zie toolearn over het toewijzen van kolommen in bron gegevensset toocolumns in sink-gegevensset [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="d77e0-392">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="d77e0-393">Herhaalbare kopiëren</span><span class="sxs-lookup"><span data-stu-id="d77e0-393">Repeatable copy</span></span>
<span data-ttu-id="d77e0-394">Bij het kopiëren van gegevens tooSQL Server-Database, voegt Hallo kopieeractiviteit gegevenstabel toohello sink standaard.</span><span class="sxs-lookup"><span data-stu-id="d77e0-394">When copying data tooSQL Server Database, hello copy activity appends data toohello sink table by default.</span></span> <span data-ttu-id="d77e0-395">een UPSERT tooperform in plaats daarvan Zie [herhaalbare schrijven tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) artikel.</span><span class="sxs-lookup"><span data-stu-id="d77e0-395">tooperform an UPSERT instead,  See [Repeatable write tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="d77e0-396">Houd bij het kopiëren van gegevens uit een relationele gegevensopslag, herhaalbaarheid rekening tooavoid ongewenste resultaten.</span><span class="sxs-lookup"><span data-stu-id="d77e0-396">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="d77e0-397">In Azure Data Factory, kunt u een segment handmatig opnieuw.</span><span class="sxs-lookup"><span data-stu-id="d77e0-397">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="d77e0-398">U kunt ook een beleid voor opnieuw proberen voor een gegevensset configureren zodat een segment wordt opnieuw uitgevoerd wanneer een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="d77e0-398">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="d77e0-399">Wanneer een segment opnieuw in beide gevallen wordt uitgevoerd, moet u ervoor dat dezelfde gegevens Hallo toomake wordt gelezen ongeacht hoe vaak een segment wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d77e0-399">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="d77e0-400">Zie [Repeatable van relationele bronnen lezen](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="d77e0-400">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="d77e0-401">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="d77e0-401">Performance and Tuning</span></span>
<span data-ttu-id="d77e0-402">Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.</span><span class="sxs-lookup"><span data-stu-id="d77e0-402">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
