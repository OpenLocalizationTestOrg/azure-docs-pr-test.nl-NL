---
title: aaaMove gegevens vanaf Amazon Redshift gebruik Data Factory | Microsoft Docs
description: Meer informatie over het toomove gegevens vanaf Amazon Redshift met behulp van Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 01d15078-58dc-455c-9d9d-98fbdf4ea51e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 2a097320734ebdd57282d250f7fdba35741777f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-redshift-using-azure-data-factory"></a><span data-ttu-id="9adf6-103">Verplaatsen van gegevens vanaf Amazon Redshift, met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9adf6-103">Move data From Amazon Redshift using Azure Data Factory</span></span>
<span data-ttu-id="9adf6-104">Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit in Azure Data Factory toomove gegevens vanaf Amazon Redshift Hallo.</span><span class="sxs-lookup"><span data-stu-id="9adf6-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from Amazon Redshift.</span></span> <span data-ttu-id="9adf6-105">Hallo artikel bouwt voort op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.</span><span class="sxs-lookup"><span data-stu-id="9adf6-105">hello article builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

<span data-ttu-id="9adf6-106">U kunt gegevens kopiëren van Amazon Redshift tooany ondersteund sink-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="9adf6-106">You can copy data from Amazon Redshift tooany supported sink data store.</span></span> <span data-ttu-id="9adf6-107">Zie voor een lijst van gegevensarchieven als PUT wordt ondersteund door Hallo kopieeractiviteit [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="9adf6-107">For a list of data stores supported as sinks by hello copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="9adf6-108">Data factory ondersteunt momenteel verplaatsen van gegevens vanaf Amazon Redshift tooother gegevensarchieven, maar niet voor het verplaatsen van gegevens van andere gegevens winkels tooAmazon Redshift.</span><span class="sxs-lookup"><span data-stu-id="9adf6-108">Data factory currently supports moving data from Amazon Redshift tooother data stores, but not for moving data from other data stores tooAmazon Redshift.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9adf6-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9adf6-109">Prerequisites</span></span>
* <span data-ttu-id="9adf6-110">Als u gegevens tooan on-premises-gegevensopslag verplaatst, installeert u [Data Management Gateway](data-factory-data-management-gateway.md) op een on-premises machine.</span><span class="sxs-lookup"><span data-stu-id="9adf6-110">If you are moving data tooan on-premises data store, install [Data Management Gateway](data-factory-data-management-gateway.md) on an on-premises machine.</span></span> <span data-ttu-id="9adf6-111">Vervolgens Grant Data Management Gateway (Gebruik IP-adres van de machine Hallo) Hallo RAS tooAmazon Redshift-cluster.</span><span class="sxs-lookup"><span data-stu-id="9adf6-111">Then, Grant Data Management Gateway (use IP address of hello machine) hello access tooAmazon Redshift cluster.</span></span> <span data-ttu-id="9adf6-112">Zie [autoriseren toegang toohello cluster](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) voor instructies.</span><span class="sxs-lookup"><span data-stu-id="9adf6-112">See [Authorize access toohello cluster](http://docs.aws.amazon.com/redshift/latest/gsg/rs-gsg-authorize-cluster-access.html) for instructions.</span></span>
* <span data-ttu-id="9adf6-113">Als u gegevensarchief tooan Azure gegevens overstapt, Zie [Azure Data Center-IP-adresbereiken](https://www.microsoft.com/download/details.aspx?id=41653) voor Hallo Compute IP-adres en SQL-adresbereiken die worden gebruikt door hello Azure-datacenters.</span><span class="sxs-lookup"><span data-stu-id="9adf6-113">If you are moving data tooan Azure data store, see [Azure Data Center IP Ranges](https://www.microsoft.com/download/details.aspx?id=41653) for hello Compute IP address and SQL ranges used by hello Azure data centers.</span></span>

## <a name="getting-started"></a><span data-ttu-id="9adf6-114">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="9adf6-114">Getting started</span></span>
<span data-ttu-id="9adf6-115">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens uit een bron Amazon Redshift verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="9adf6-115">You can create a pipeline with a copy activity that moves data from an Amazon Redshift source by using different tools/APIs.</span></span>

<span data-ttu-id="9adf6-116">Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="9adf6-116">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="9adf6-117">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="9adf6-117">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="9adf6-118">U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="9adf6-118">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="9adf6-119">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="9adf6-119">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="9adf6-120">Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9adf6-120">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="9adf6-121">Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="9adf6-121">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="9adf6-122">Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="9adf6-122">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="9adf6-123">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="9adf6-123">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="9adf6-124">Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9adf6-124">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="9adf6-125">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="9adf6-125">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="9adf6-126">Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens van een gegevensarchief Amazon Redshift zijn [JSON-voorbeeld: gegevens kopiëren van Amazon Redshift tooAzure Blob](#json-example-copy-data-from-amazon-redshift-to-azure-blob) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="9adf6-126">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an Amazon Redshift data store, see [JSON example: Copy data from Amazon Redshift tooAzure Blob](#json-example-copy-data-from-amazon-redshift-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="9adf6-127">Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooAmazon Redshift zijn:</span><span class="sxs-lookup"><span data-stu-id="9adf6-127">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAmazon Redshift:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="9adf6-128">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="9adf6-128">Linked service properties</span></span>
<span data-ttu-id="9adf6-129">Hallo volgende tabel bevat een beschrijving voor JSON-elementen specifieke tooAmazon Redshift gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="9adf6-129">hello following table provides description for JSON elements specific tooAmazon Redshift linked service.</span></span>

| <span data-ttu-id="9adf6-130">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="9adf6-130">Property</span></span> | <span data-ttu-id="9adf6-131">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9adf6-131">Description</span></span> | <span data-ttu-id="9adf6-132">Vereist</span><span class="sxs-lookup"><span data-stu-id="9adf6-132">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9adf6-133">type</span><span class="sxs-lookup"><span data-stu-id="9adf6-133">type</span></span> |<span data-ttu-id="9adf6-134">Hallo type eigenschap moet worden ingesteld op: **AmazonRedshift**.</span><span class="sxs-lookup"><span data-stu-id="9adf6-134">hello type property must be set to: **AmazonRedshift**.</span></span> |<span data-ttu-id="9adf6-135">Ja</span><span class="sxs-lookup"><span data-stu-id="9adf6-135">Yes</span></span> |
| <span data-ttu-id="9adf6-136">server</span><span class="sxs-lookup"><span data-stu-id="9adf6-136">server</span></span> |<span data-ttu-id="9adf6-137">IP-naam adres of de hostnaam van Hallo Amazon Redshift server.</span><span class="sxs-lookup"><span data-stu-id="9adf6-137">IP address or host name of hello Amazon Redshift server.</span></span> |<span data-ttu-id="9adf6-138">Ja</span><span class="sxs-lookup"><span data-stu-id="9adf6-138">Yes</span></span> |
| <span data-ttu-id="9adf6-139">poort</span><span class="sxs-lookup"><span data-stu-id="9adf6-139">port</span></span> |<span data-ttu-id="9adf6-140">toolisten Hello aantal Hallo TCP-poort die Hallo Amazon Redshift server gebruikt voor clientverbindingen.</span><span class="sxs-lookup"><span data-stu-id="9adf6-140">hello number of hello TCP port that hello Amazon Redshift server uses toolisten for client connections.</span></span> |<span data-ttu-id="9adf6-141">Nee, de standaardwaarde: 5439</span><span class="sxs-lookup"><span data-stu-id="9adf6-141">No, default value: 5439</span></span> |
| <span data-ttu-id="9adf6-142">database</span><span class="sxs-lookup"><span data-stu-id="9adf6-142">database</span></span> |<span data-ttu-id="9adf6-143">Naam van Hallo Amazon Redshift database.</span><span class="sxs-lookup"><span data-stu-id="9adf6-143">Name of hello Amazon Redshift database.</span></span> |<span data-ttu-id="9adf6-144">Ja</span><span class="sxs-lookup"><span data-stu-id="9adf6-144">Yes</span></span> |
| <span data-ttu-id="9adf6-145">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="9adf6-145">username</span></span> |<span data-ttu-id="9adf6-146">Naam van de gebruiker die toegang toohello database heeft.</span><span class="sxs-lookup"><span data-stu-id="9adf6-146">Name of user who has access toohello database.</span></span> |<span data-ttu-id="9adf6-147">Ja</span><span class="sxs-lookup"><span data-stu-id="9adf6-147">Yes</span></span> |
| <span data-ttu-id="9adf6-148">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="9adf6-148">password</span></span> |<span data-ttu-id="9adf6-149">Wachtwoord voor gebruikersaccount Hallo.</span><span class="sxs-lookup"><span data-stu-id="9adf6-149">Password for hello user account.</span></span> |<span data-ttu-id="9adf6-150">Ja</span><span class="sxs-lookup"><span data-stu-id="9adf6-150">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="9adf6-151">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="9adf6-151">Dataset properties</span></span>
<span data-ttu-id="9adf6-152">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="9adf6-152">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="9adf6-153">Secties zoals structuur, beschikbaarheid en beleid zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).</span><span class="sxs-lookup"><span data-stu-id="9adf6-153">Sections such as structure, availability, and policy are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="9adf6-154">Hallo **typeProperties** sectie verschilt voor elk type dataset.</span><span class="sxs-lookup"><span data-stu-id="9adf6-154">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="9adf6-155">Het levert informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="9adf6-155">It provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="9adf6-156">Hallo typeProperties sectie voor de gegevensset van het type **RelationalTable** (inclusief Amazon Redshift gegevensset) heeft Hallo volgende eigenschappen</span><span class="sxs-lookup"><span data-stu-id="9adf6-156">hello typeProperties section for dataset of type **RelationalTable** (which includes Amazon Redshift dataset) has hello following properties</span></span>

| <span data-ttu-id="9adf6-157">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="9adf6-157">Property</span></span> | <span data-ttu-id="9adf6-158">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9adf6-158">Description</span></span> | <span data-ttu-id="9adf6-159">Vereist</span><span class="sxs-lookup"><span data-stu-id="9adf6-159">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9adf6-160">tableName</span><span class="sxs-lookup"><span data-stu-id="9adf6-160">tableName</span></span> |<span data-ttu-id="9adf6-161">De naam van de tabel Hallo in Hallo Amazon Redshift database waarnaar de gekoppelde service verwijst.</span><span class="sxs-lookup"><span data-stu-id="9adf6-161">Name of hello table in hello Amazon Redshift database that linked service refers to.</span></span> |<span data-ttu-id="9adf6-162">Nee (als **query** van **RelationalSource** is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="9adf6-162">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="9adf6-163">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="9adf6-163">Copy activity properties</span></span>
<span data-ttu-id="9adf6-164">Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="9adf6-164">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="9adf6-165">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en beleidsregels zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="9adf6-165">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="9adf6-166">Dat eigenschappen beschikbaar zijn in Hallo **typeProperties** sectie van de activiteit Hallo variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="9adf6-166">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="9adf6-167">Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="9adf6-167">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="9adf6-168">Wanneer de bron van de kopieerbewerking is van het type **RelationalSource** (waaronder Amazon Redshift), Hallo volgende eigenschappen beschikbaar zijn in de sectie typeProperties:</span><span class="sxs-lookup"><span data-stu-id="9adf6-168">When source of copy activity is of type **RelationalSource** (which includes Amazon Redshift), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="9adf6-169">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="9adf6-169">Property</span></span> | <span data-ttu-id="9adf6-170">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9adf6-170">Description</span></span> | <span data-ttu-id="9adf6-171">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="9adf6-171">Allowed values</span></span> | <span data-ttu-id="9adf6-172">Vereist</span><span class="sxs-lookup"><span data-stu-id="9adf6-172">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9adf6-173">query</span><span class="sxs-lookup"><span data-stu-id="9adf6-173">query</span></span> |<span data-ttu-id="9adf6-174">Hallo aangepaste query tooread gegevens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9adf6-174">Use hello custom query tooread data.</span></span> |<span data-ttu-id="9adf6-175">SQL-query-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="9adf6-175">SQL query string.</span></span> <span data-ttu-id="9adf6-176">Bijvoorbeeld: Selecteer * from MijnTabel.</span><span class="sxs-lookup"><span data-stu-id="9adf6-176">For example: select * from MyTable.</span></span> |<span data-ttu-id="9adf6-177">Nee (als **tableName** van **gegevensset** is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="9adf6-177">No (if **tableName** of **dataset** is specified)</span></span> |

## <a name="json-example-copy-data-from-amazon-redshift-tooazure-blob"></a><span data-ttu-id="9adf6-178">JSON-voorbeeld: gegevens kopiëren van Amazon Redshift tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="9adf6-178">JSON example: Copy data from Amazon Redshift tooAzure Blob</span></span>
<span data-ttu-id="9adf6-179">Dit voorbeeld ziet u hoe toocopy gegevens uit een Redshift Amazon tooan Azure Blob Storage-database.</span><span class="sxs-lookup"><span data-stu-id="9adf6-179">This sample shows how toocopy data from an Amazon Redshift database tooan Azure Blob Storage.</span></span> <span data-ttu-id="9adf6-180">Echter, de gegevens kunnen worden gekopieerd **rechtstreeks** tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="9adf6-180">However, data can be copied **directly** tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="9adf6-181">Hallo voorbeeld heeft Hallo data factory-entiteiten te volgen:</span><span class="sxs-lookup"><span data-stu-id="9adf6-181">hello sample has hello following data factory entities:</span></span>

* <span data-ttu-id="9adf6-182">Een gekoppelde service van het type [AmazonRedshift](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="9adf6-182">A linked service of type [AmazonRedshift](#linked-service-properties).</span></span>
* <span data-ttu-id="9adf6-183">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="9adf6-183">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="9adf6-184">Invoer [gegevensset](data-factory-create-datasets.md) van het type [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="9adf6-184">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
* <span data-ttu-id="9adf6-185">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="9adf6-185">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="9adf6-186">Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [RelationalSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="9adf6-186">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md##copy-activity-properties).</span></span>

<span data-ttu-id="9adf6-187">Hallo voorbeeld kopieert gegevens van de resultaten van een query in Amazon Redshift tooa blob elk uur.</span><span class="sxs-lookup"><span data-stu-id="9adf6-187">hello sample copies data from a query result in Amazon Redshift tooa blob every hour.</span></span> <span data-ttu-id="9adf6-188">Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="9adf6-188">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="9adf6-189">**Amazon Redshift gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="9adf6-189">**Amazon Redshift linked service:**</span></span>

```json
{
    "name": "AmazonRedshiftLinkedService",
    "properties":
    {
        "type": "AmazonRedshift",
        "typeProperties":
        {
            "server": "< hello IP address or host name of hello Amazon Redshift server >",
            "port": <hello number of hello TCP port that hello Amazon Redshift server uses toolisten for client connections.>,
            "database": "<hello database name of hello Amazon Redshift database>",
            "username": "<username>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="9adf6-190">**Gekoppelde Azure Storage-service:**</span><span class="sxs-lookup"><span data-stu-id="9adf6-190">**Azure Storage linked service:**</span></span>

```json
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="9adf6-191">**Amazon Redshift invoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="9adf6-191">**Amazon Redshift input dataset:**</span></span>

<span data-ttu-id="9adf6-192">Instelling `"external": true` informeert Hallo Data Factory-service die gegevensset Hallo externe toohello data factory is en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="9adf6-192">Setting `"external": true` informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span> <span data-ttu-id="9adf6-193">Deze eigenschap tootrue niet instellen op een invoergegevensset dat niet door een activiteit in de pijplijn hello wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="9adf6-193">Set this property tootrue on an input dataset that is not produced by an activity in hello pipeline.</span></span>

```json
{
    "name": "AmazonRedshiftInputDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "AmazonRedshiftLinkedService",
        "typeProperties": {
            "tableName": "<Table name>"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="9adf6-194">**Azure Blob-uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="9adf6-194">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="9adf6-195">Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="9adf6-195">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="9adf6-196">pad naar map voor blob Hallo Hallo wordt dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="9adf6-196">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="9adf6-197">Hallo mappad jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9adf6-197">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazonredshift/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
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
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="9adf6-198">**De kopieeractiviteit in een pijplijn met Azure Redshift bron (RelationalSource) en Blob sink:**</span><span class="sxs-lookup"><span data-stu-id="9adf6-198">**Copy activity in a pipeline with Azure Redshift source (RelationalSource) and Blob sink:**</span></span>

<span data-ttu-id="9adf6-199">Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur.</span><span class="sxs-lookup"><span data-stu-id="9adf6-199">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="9adf6-200">Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**RelationalSource** en **sink** type is ingesteld, te**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="9adf6-200">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="9adf6-201">Hallo SQL-query is opgegeven voor Hallo **query** eigenschap Hallo gegevens selecteert in Hallo voorbij toocopy uur.</span><span class="sxs-lookup"><span data-stu-id="9adf6-201">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopyAmazonRedshiftToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonRedshiftInputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "AmazonRedshiftToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-amazon-redshift"></a><span data-ttu-id="9adf6-202">Toewijzing van het type voor Amazon Redshift</span><span class="sxs-lookup"><span data-stu-id="9adf6-202">Type mapping for Amazon Redshift</span></span>
<span data-ttu-id="9adf6-203">Zoals vermeld in Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel kopieeractiviteit voert automatische typeconversies van brontypen typen toosink Hello benadering in twee stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="9adf6-203">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="9adf6-204">Systeemeigen bron typen too.NET type converteren</span><span class="sxs-lookup"><span data-stu-id="9adf6-204">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="9adf6-205">Converteren van .NET-type toonative sink-type</span><span class="sxs-lookup"><span data-stu-id="9adf6-205">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="9adf6-206">Bij het verplaatsen van gegevens tooAmazon Redshift worden Hallo volgende toewijzingen van Amazon Redshift typen too.NET typen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9adf6-206">When moving data tooAmazon Redshift, hello following mappings are used from Amazon Redshift types too.NET types.</span></span>

| <span data-ttu-id="9adf6-207">Amazon Redshift Type</span><span class="sxs-lookup"><span data-stu-id="9adf6-207">Amazon Redshift Type</span></span> | <span data-ttu-id="9adf6-208">.NET op basis van Type</span><span class="sxs-lookup"><span data-stu-id="9adf6-208">.NET Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="9adf6-209">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="9adf6-209">SMALLINT</span></span> |<span data-ttu-id="9adf6-210">Int16</span><span class="sxs-lookup"><span data-stu-id="9adf6-210">Int16</span></span> |
| <span data-ttu-id="9adf6-211">GEHEEL GETAL</span><span class="sxs-lookup"><span data-stu-id="9adf6-211">INTEGER</span></span> |<span data-ttu-id="9adf6-212">Int32</span><span class="sxs-lookup"><span data-stu-id="9adf6-212">Int32</span></span> |
| <span data-ttu-id="9adf6-213">BIGINT</span><span class="sxs-lookup"><span data-stu-id="9adf6-213">BIGINT</span></span> |<span data-ttu-id="9adf6-214">Int64</span><span class="sxs-lookup"><span data-stu-id="9adf6-214">Int64</span></span> |
| <span data-ttu-id="9adf6-215">DECIMALE</span><span class="sxs-lookup"><span data-stu-id="9adf6-215">DECIMAL</span></span> |<span data-ttu-id="9adf6-216">Decimale</span><span class="sxs-lookup"><span data-stu-id="9adf6-216">Decimal</span></span> |
| <span data-ttu-id="9adf6-217">ECHTE</span><span class="sxs-lookup"><span data-stu-id="9adf6-217">REAL</span></span> |<span data-ttu-id="9adf6-218">Één</span><span class="sxs-lookup"><span data-stu-id="9adf6-218">Single</span></span> |
| <span data-ttu-id="9adf6-219">DUBBELE PRECISIE</span><span class="sxs-lookup"><span data-stu-id="9adf6-219">DOUBLE PRECISION</span></span> |<span data-ttu-id="9adf6-220">dubbele</span><span class="sxs-lookup"><span data-stu-id="9adf6-220">Double</span></span> |
| <span data-ttu-id="9adf6-221">BOOLEAANSE WAARDE</span><span class="sxs-lookup"><span data-stu-id="9adf6-221">BOOLEAN</span></span> |<span data-ttu-id="9adf6-222">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9adf6-222">String</span></span> |
| <span data-ttu-id="9adf6-223">CHAR</span><span class="sxs-lookup"><span data-stu-id="9adf6-223">CHAR</span></span> |<span data-ttu-id="9adf6-224">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9adf6-224">String</span></span> |
| <span data-ttu-id="9adf6-225">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="9adf6-225">VARCHAR</span></span> |<span data-ttu-id="9adf6-226">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9adf6-226">String</span></span> |
| <span data-ttu-id="9adf6-227">DATUM</span><span class="sxs-lookup"><span data-stu-id="9adf6-227">DATE</span></span> |<span data-ttu-id="9adf6-228">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="9adf6-228">DateTime</span></span> |
| <span data-ttu-id="9adf6-229">TIJDSTEMPEL</span><span class="sxs-lookup"><span data-stu-id="9adf6-229">TIMESTAMP</span></span> |<span data-ttu-id="9adf6-230">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="9adf6-230">DateTime</span></span> |
| <span data-ttu-id="9adf6-231">TEKST</span><span class="sxs-lookup"><span data-stu-id="9adf6-231">TEXT</span></span> |<span data-ttu-id="9adf6-232">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9adf6-232">String</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="9adf6-233">Bronkolommen toosink toewijzen</span><span class="sxs-lookup"><span data-stu-id="9adf6-233">Map source toosink columns</span></span>
<span data-ttu-id="9adf6-234">Zie toolearn over het toewijzen van kolommen in bron gegevensset toocolumns in sink-gegevensset [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="9adf6-234">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="9adf6-235">Herhaalbare leesbewerking van relationele bronnen</span><span class="sxs-lookup"><span data-stu-id="9adf6-235">Repeatable read from relational sources</span></span>
<span data-ttu-id="9adf6-236">Houd bij het kopiëren van gegevens uit een relationele gegevensopslag, herhaalbaarheid rekening tooavoid ongewenste resultaten.</span><span class="sxs-lookup"><span data-stu-id="9adf6-236">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="9adf6-237">In Azure Data Factory, kunt u een segment handmatig opnieuw.</span><span class="sxs-lookup"><span data-stu-id="9adf6-237">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="9adf6-238">U kunt ook een beleid voor opnieuw proberen voor een gegevensset configureren zodat een segment wordt opnieuw uitgevoerd wanneer een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="9adf6-238">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="9adf6-239">Wanneer een segment opnieuw in beide gevallen wordt uitgevoerd, moet u ervoor dat dezelfde gegevens Hallo toomake wordt gelezen ongeacht hoe vaak een segment wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9adf6-239">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="9adf6-240">Zie [Repeatable van relationele bronnen lezen](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="9adf6-240">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="9adf6-241">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="9adf6-241">Performance and Tuning</span></span>
<span data-ttu-id="9adf6-242">Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.</span><span class="sxs-lookup"><span data-stu-id="9adf6-242">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9adf6-243">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9adf6-243">Next Steps</span></span>
<span data-ttu-id="9adf6-244">Zie Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="9adf6-244">See hello following articles:</span></span>

* <span data-ttu-id="9adf6-245">[Zelfstudie voor kopiëren-activiteit](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies voor het maken van een pijplijn met een Kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="9adf6-245">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
