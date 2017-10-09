---
title: aaaPush gegevens tooSearch index met behulp van de Data Factory | Microsoft Docs
description: Meer informatie over het toopush gegevens tooAzure Search-Index met behulp van Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f8d46e1e-5c37-4408-80fb-c54be532a4ab
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: f2d973d0a2c24d6448e2d59e37e24503aa433018
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="push-data-tooan-azure-search-index-by-using-azure-data-factory"></a><span data-ttu-id="c8e95-103">Push-gegevens tooan Azure Search-index met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="c8e95-103">Push data tooan Azure Search index by using Azure Data Factory</span></span>
<span data-ttu-id="c8e95-104">Dit artikel wordt beschreven hoe toouse hello Kopieeractiviteit toopush van een ondersteunde brongegevens gegevensarchief tooAzure Search-index.</span><span class="sxs-lookup"><span data-stu-id="c8e95-104">This article describes how toouse hello Copy Activity toopush data from a supported source data store tooAzure Search index.</span></span> <span data-ttu-id="c8e95-105">Ondersteunde bron gegevensarchieven worden vermeld in de bronkolom Hallo Hallo [ondersteunde gegevensbronnen en put](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel.</span><span class="sxs-lookup"><span data-stu-id="c8e95-105">Supported source data stores are listed in hello Source column of hello [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="c8e95-106">In dit artikel is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin Kopieeractiviteit en combinaties van ondersteunde gegevens store een algemeen overzicht van de verplaatsing van gegevens biedt.</span><span class="sxs-lookup"><span data-stu-id="c8e95-106">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="c8e95-107">Connectiviteit inschakelen</span><span class="sxs-lookup"><span data-stu-id="c8e95-107">Enabling connectivity</span></span>
<span data-ttu-id="c8e95-108">tooallow Data Factory-service verbinding tooan on-premises gegevensopslag, u Data Management Gateway installeren in uw on-premises omgeving.</span><span class="sxs-lookup"><span data-stu-id="c8e95-108">tooallow Data Factory service connect tooan on-premises data store, you install Data Management Gateway in your on-premises environment.</span></span> <span data-ttu-id="c8e95-109">U kunt de gateway installeren op Hallo dezelfde machine die als host fungeert voor de brongegevens Hallo opslaan of op een afzonderlijke computer tooavoid concurrentie voor resources met Hallo gegevens opslaan.</span><span class="sxs-lookup"><span data-stu-id="c8e95-109">You can install gateway on hello same machine that hosts hello source data store or on a separate machine tooavoid competing for resources with hello data store.</span></span>

<span data-ttu-id="c8e95-110">Data Management Gateway maakt verbinding lokale gegevensbronnen toocloud services op een manier veilig en beheerd.</span><span class="sxs-lookup"><span data-stu-id="c8e95-110">Data Management Gateway connects on-premises data sources toocloud services in a secure and managed way.</span></span> <span data-ttu-id="c8e95-111">Zie [gegevens verplaatsen tussen on-premises en cloud](data-factory-move-data-between-onprem-and-cloud.md) voor meer informatie over Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="c8e95-111">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="c8e95-112">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="c8e95-112">Getting started</span></span>
<span data-ttu-id="c8e95-113">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens uit een bron data store tooAzure Search-index worden met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="c8e95-113">You can create a pipeline with a copy activity that pushes data from a source data store tooAzure Search index by using different tools/APIs.</span></span>

<span data-ttu-id="c8e95-114">Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="c8e95-114">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="c8e95-115">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="c8e95-115">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="c8e95-116">U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="c8e95-116">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="c8e95-117">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="c8e95-117">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="c8e95-118">Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="c8e95-118">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="c8e95-119">Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="c8e95-119">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="c8e95-120">Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="c8e95-120">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="c8e95-121">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="c8e95-121">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="c8e95-122">Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c8e95-122">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="c8e95-123">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="c8e95-123">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="c8e95-124">Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens tooAzure Search-index zijn [JSON-voorbeeld: gegevens kopiëren van lokale SQL Server tooAzure Search-index](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="c8e95-124">For a sample with JSON definitions for Data Factory entities that are used toocopy data tooAzure Search index, see [JSON example: Copy data from on-premises SQL Server tooAzure Search index](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) section of this article.</span></span> 

<span data-ttu-id="c8e95-125">Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooAzure Search-Index zijn:</span><span class="sxs-lookup"><span data-stu-id="c8e95-125">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure Search Index:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="c8e95-126">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="c8e95-126">Linked service properties</span></span>

<span data-ttu-id="c8e95-127">Hallo volgende tabel bevat beschrijvingen van JSON-elementen die specifiek toohello Azure Search gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="c8e95-127">hello following table provides descriptions for JSON elements that are specific toohello Azure Search linked service.</span></span>

| <span data-ttu-id="c8e95-128">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="c8e95-128">Property</span></span> | <span data-ttu-id="c8e95-129">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c8e95-129">Description</span></span> | <span data-ttu-id="c8e95-130">Vereist</span><span class="sxs-lookup"><span data-stu-id="c8e95-130">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="c8e95-131">type</span><span class="sxs-lookup"><span data-stu-id="c8e95-131">type</span></span> | <span data-ttu-id="c8e95-132">Hallo type eigenschap moet worden ingesteld op: **AzureSearch**.</span><span class="sxs-lookup"><span data-stu-id="c8e95-132">hello type property must be set to: **AzureSearch**.</span></span> | <span data-ttu-id="c8e95-133">Ja</span><span class="sxs-lookup"><span data-stu-id="c8e95-133">Yes</span></span> |
| <span data-ttu-id="c8e95-134">URL</span><span class="sxs-lookup"><span data-stu-id="c8e95-134">url</span></span> | <span data-ttu-id="c8e95-135">De URL voor hello Azure Search-service.</span><span class="sxs-lookup"><span data-stu-id="c8e95-135">URL for hello Azure Search service.</span></span> | <span data-ttu-id="c8e95-136">Ja</span><span class="sxs-lookup"><span data-stu-id="c8e95-136">Yes</span></span> |
| <span data-ttu-id="c8e95-137">sleutel</span><span class="sxs-lookup"><span data-stu-id="c8e95-137">key</span></span> | <span data-ttu-id="c8e95-138">Administratorsleutel voor hello Azure Search-service.</span><span class="sxs-lookup"><span data-stu-id="c8e95-138">Admin key for hello Azure Search service.</span></span> | <span data-ttu-id="c8e95-139">Ja</span><span class="sxs-lookup"><span data-stu-id="c8e95-139">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="c8e95-140">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="c8e95-140">Dataset properties</span></span>

<span data-ttu-id="c8e95-141">Zie voor een volledige lijst van de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets en secties Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="c8e95-141">For a full list of sections and properties that are available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="c8e95-142">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle typen van de gegevensset.</span><span class="sxs-lookup"><span data-stu-id="c8e95-142">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span> <span data-ttu-id="c8e95-143">Hallo **typeProperties** sectie verschilt voor elk type dataset.</span><span class="sxs-lookup"><span data-stu-id="c8e95-143">hello **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="c8e95-144">Hallo typeProperties sectie voor een gegevensset van het type Hallo **AzureSearchIndex** heeft Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="c8e95-144">hello typeProperties section for a dataset of hello type **AzureSearchIndex** has hello following properties:</span></span>

| <span data-ttu-id="c8e95-145">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="c8e95-145">Property</span></span> | <span data-ttu-id="c8e95-146">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c8e95-146">Description</span></span> | <span data-ttu-id="c8e95-147">Vereist</span><span class="sxs-lookup"><span data-stu-id="c8e95-147">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="c8e95-148">type</span><span class="sxs-lookup"><span data-stu-id="c8e95-148">type</span></span> | <span data-ttu-id="c8e95-149">de eigenschap type Hello te moet worden ingesteld**AzureSearchIndex**.</span><span class="sxs-lookup"><span data-stu-id="c8e95-149">hello type property must be set too**AzureSearchIndex**.</span></span>| <span data-ttu-id="c8e95-150">Ja</span><span class="sxs-lookup"><span data-stu-id="c8e95-150">Yes</span></span> |
| <span data-ttu-id="c8e95-151">NaamCommunity</span><span class="sxs-lookup"><span data-stu-id="c8e95-151">indexName</span></span> | <span data-ttu-id="c8e95-152">Naam van hello Azure Search-index.</span><span class="sxs-lookup"><span data-stu-id="c8e95-152">Name of hello Azure Search index.</span></span> <span data-ttu-id="c8e95-153">Data Factory maakt geen Hallo index.</span><span class="sxs-lookup"><span data-stu-id="c8e95-153">Data Factory does not create hello index.</span></span> <span data-ttu-id="c8e95-154">Hallo-index moet bestaan in Azure Search.</span><span class="sxs-lookup"><span data-stu-id="c8e95-154">hello index must exist in Azure Search.</span></span> | <span data-ttu-id="c8e95-155">Ja</span><span class="sxs-lookup"><span data-stu-id="c8e95-155">Yes</span></span> |


## <a name="copy-activity-properties"></a><span data-ttu-id="c8e95-156">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="c8e95-156">Copy activity properties</span></span>
<span data-ttu-id="c8e95-157">Zie voor een volledige lijst van de eigenschappen die beschikbaar zijn voor het definiëren van activiteiten en secties Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="c8e95-157">For a full list of sections and properties that are available for defining activities, see hello [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="c8e95-158">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoertabellen en verschillende beleidsregels zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="c8e95-158">Properties such as name, description, input and output tables, and various policies are available for all types of activities.</span></span> <span data-ttu-id="c8e95-159">Terwijl de eigenschappen die beschikbaar zijn in Hallo typeProperties sectie variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="c8e95-159">Whereas, properties available in hello typeProperties section vary with each activity type.</span></span> <span data-ttu-id="c8e95-160">Voor de Kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="c8e95-160">For Copy Activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="c8e95-161">Voor de Kopieeractiviteit wanneer Hallo sink Hallo type **AzureSearchIndexSink**, Hallo volgende eigenschappen beschikbaar zijn in de sectie typeProperties:</span><span class="sxs-lookup"><span data-stu-id="c8e95-161">For Copy Activity, when hello sink is of hello type **AzureSearchIndexSink**, hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="c8e95-162">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="c8e95-162">Property</span></span> | <span data-ttu-id="c8e95-163">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c8e95-163">Description</span></span> | <span data-ttu-id="c8e95-164">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="c8e95-164">Allowed values</span></span> | <span data-ttu-id="c8e95-165">Vereist</span><span class="sxs-lookup"><span data-stu-id="c8e95-165">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="c8e95-166">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="c8e95-166">WriteBehavior</span></span> | <span data-ttu-id="c8e95-167">Hiermee geeft u op of toomerge of vervangen, wanneer een document al in Hallo index bestaat.</span><span class="sxs-lookup"><span data-stu-id="c8e95-167">Specifies whether toomerge or replace when a document already exists in hello index.</span></span> <span data-ttu-id="c8e95-168">Zie Hallo [WriteBehavior eigenschap](#writebehavior-property).</span><span class="sxs-lookup"><span data-stu-id="c8e95-168">See hello [WriteBehavior property](#writebehavior-property).</span></span>| <span data-ttu-id="c8e95-169">samenvoegen (standaard)</span><span class="sxs-lookup"><span data-stu-id="c8e95-169">Merge (default)</span></span><br/><span data-ttu-id="c8e95-170">Uploaden</span><span class="sxs-lookup"><span data-stu-id="c8e95-170">Upload</span></span>| <span data-ttu-id="c8e95-171">Nee</span><span class="sxs-lookup"><span data-stu-id="c8e95-171">No</span></span> |
| <span data-ttu-id="c8e95-172">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="c8e95-172">WriteBatchSize</span></span> | <span data-ttu-id="c8e95-173">Gegevens geüpload in hello Azure Search-index wanneer Hallo buffergrootte writeBatchSize bereikt.</span><span class="sxs-lookup"><span data-stu-id="c8e95-173">Uploads data into hello Azure Search index when hello buffer size reaches writeBatchSize.</span></span> <span data-ttu-id="c8e95-174">Zie Hallo [WriteBatchSize eigenschap](#writebatchsize-property) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c8e95-174">See hello [WriteBatchSize property](#writebatchsize-property) for details.</span></span> | <span data-ttu-id="c8e95-175">1 too1 000.</span><span class="sxs-lookup"><span data-stu-id="c8e95-175">1 too1,000.</span></span> <span data-ttu-id="c8e95-176">Standaardwaarde is 1000.</span><span class="sxs-lookup"><span data-stu-id="c8e95-176">Default value is 1000.</span></span> | <span data-ttu-id="c8e95-177">Nee</span><span class="sxs-lookup"><span data-stu-id="c8e95-177">No</span></span> |

### <a name="writebehavior-property"></a><span data-ttu-id="c8e95-178">De eigenschap WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="c8e95-178">WriteBehavior property</span></span>
<span data-ttu-id="c8e95-179">AzureSearchSink upserts bij het schrijven van gegevens.</span><span class="sxs-lookup"><span data-stu-id="c8e95-179">AzureSearchSink upserts when writing data.</span></span> <span data-ttu-id="c8e95-180">Met andere woorden, bij het schrijven van een document als Hallo documentsleutel al in de Azure Search-index hello bestaat Azure Search-updates Hallo bestaand document in plaats van er een conflict uitzondering is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="c8e95-180">In other words, when writing a document, if hello document key already exists in hello Azure Search index, Azure Search updates hello existing document rather than throwing a conflict exception.</span></span>

<span data-ttu-id="c8e95-181">Hallo AzureSearchSink biedt Hallo na twee upsert gedrag (via AzureSearch SDK):</span><span class="sxs-lookup"><span data-stu-id="c8e95-181">hello AzureSearchSink provides hello following two upsert behaviors (by using AzureSearch SDK):</span></span>

- <span data-ttu-id="c8e95-182">**Samenvoegen**: alle Hallo-kolommen in een nieuw document Hallo worden gecombineerd met een bestaande Hallo.</span><span class="sxs-lookup"><span data-stu-id="c8e95-182">**Merge**: combine all hello columns in hello new document with hello existing one.</span></span> <span data-ttu-id="c8e95-183">Voor kolommen met null-waarde in een nieuw document Hallo blijft Hallo-waarde in een bestaande Hallo behouden.</span><span class="sxs-lookup"><span data-stu-id="c8e95-183">For columns with null value in hello new document, hello value in hello existing one is preserved.</span></span>
- <span data-ttu-id="c8e95-184">**Uploaden**: Hallo nieuw document vervangt bestaande Hallo.</span><span class="sxs-lookup"><span data-stu-id="c8e95-184">**Upload**: hello new document replaces hello existing one.</span></span> <span data-ttu-id="c8e95-185">Voor de kolommen is niet opgegeven in een nieuw document hello, toonull op Hallo waarde is ingesteld of er een niet-null-waarde in een bestaand document Hallo of niet is.</span><span class="sxs-lookup"><span data-stu-id="c8e95-185">For columns not specified in hello new document, hello value is set toonull whether there is a non-null value in hello existing document or not.</span></span>

<span data-ttu-id="c8e95-186">Hallo standaardgedrag is **samenvoegen**.</span><span class="sxs-lookup"><span data-stu-id="c8e95-186">hello default behavior is **Merge**.</span></span>

### <a name="writebatchsize-property"></a><span data-ttu-id="c8e95-187">De eigenschap WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="c8e95-187">WriteBatchSize Property</span></span>
<span data-ttu-id="c8e95-188">Azure Search-service ondersteunt documenten schrijven als een batch.</span><span class="sxs-lookup"><span data-stu-id="c8e95-188">Azure Search service supports writing documents as a batch.</span></span> <span data-ttu-id="c8e95-189">Een batch kan 1 too1, 000 acties bevatten.</span><span class="sxs-lookup"><span data-stu-id="c8e95-189">A batch can contain 1 too1,000 Actions.</span></span> <span data-ttu-id="c8e95-190">Een actie verwerkt één document tooperform Hallo uploaden/merge-bewerking.</span><span class="sxs-lookup"><span data-stu-id="c8e95-190">An action handles one document tooperform hello upload/merge operation.</span></span>

### <a name="data-type-support"></a><span data-ttu-id="c8e95-191">Ondersteuning voor gegevenstype</span><span class="sxs-lookup"><span data-stu-id="c8e95-191">Data type support</span></span>
<span data-ttu-id="c8e95-192">Hallo volgende tabel geeft aan of een Azure Search-gegevenstype of niet wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="c8e95-192">hello following table specifies whether an Azure Search data type is supported or not.</span></span>

| <span data-ttu-id="c8e95-193">Azure Search-gegevenstype</span><span class="sxs-lookup"><span data-stu-id="c8e95-193">Azure Search data type</span></span> | <span data-ttu-id="c8e95-194">Ondersteund in Azure Search Sink</span><span class="sxs-lookup"><span data-stu-id="c8e95-194">Supported in Azure Search Sink</span></span> |
| ---------------------- | ------------------------------ |
| <span data-ttu-id="c8e95-195">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c8e95-195">String</span></span> | <span data-ttu-id="c8e95-196">J</span><span class="sxs-lookup"><span data-stu-id="c8e95-196">Y</span></span> |
| <span data-ttu-id="c8e95-197">Int32</span><span class="sxs-lookup"><span data-stu-id="c8e95-197">Int32</span></span> | <span data-ttu-id="c8e95-198">J</span><span class="sxs-lookup"><span data-stu-id="c8e95-198">Y</span></span> |
| <span data-ttu-id="c8e95-199">Int64</span><span class="sxs-lookup"><span data-stu-id="c8e95-199">Int64</span></span> | <span data-ttu-id="c8e95-200">J</span><span class="sxs-lookup"><span data-stu-id="c8e95-200">Y</span></span> |
| <span data-ttu-id="c8e95-201">dubbele</span><span class="sxs-lookup"><span data-stu-id="c8e95-201">Double</span></span> | <span data-ttu-id="c8e95-202">J</span><span class="sxs-lookup"><span data-stu-id="c8e95-202">Y</span></span> |
| <span data-ttu-id="c8e95-203">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="c8e95-203">Boolean</span></span> | <span data-ttu-id="c8e95-204">J</span><span class="sxs-lookup"><span data-stu-id="c8e95-204">Y</span></span> |
| <span data-ttu-id="c8e95-205">DataTimeOffset</span><span class="sxs-lookup"><span data-stu-id="c8e95-205">DataTimeOffset</span></span> | <span data-ttu-id="c8e95-206">J</span><span class="sxs-lookup"><span data-stu-id="c8e95-206">Y</span></span> |
| <span data-ttu-id="c8e95-207">Tekenreeksmatrix</span><span class="sxs-lookup"><span data-stu-id="c8e95-207">String Array</span></span> | <span data-ttu-id="c8e95-208">N</span><span class="sxs-lookup"><span data-stu-id="c8e95-208">N</span></span> |
| <span data-ttu-id="c8e95-209">GeographyPoint</span><span class="sxs-lookup"><span data-stu-id="c8e95-209">GeographyPoint</span></span> | <span data-ttu-id="c8e95-210">N</span><span class="sxs-lookup"><span data-stu-id="c8e95-210">N</span></span> |

## <a name="json-example-copy-data-from-on-premises-sql-server-tooazure-search-index"></a><span data-ttu-id="c8e95-211">JSON-voorbeeld: gegevens kopiëren van lokale SQL Server tooAzure Search-index</span><span class="sxs-lookup"><span data-stu-id="c8e95-211">JSON example: Copy data from on-premises SQL Server tooAzure Search index</span></span>

<span data-ttu-id="c8e95-212">Hallo volgende ziet:</span><span class="sxs-lookup"><span data-stu-id="c8e95-212">hello following sample shows:</span></span>

1.  <span data-ttu-id="c8e95-213">Een gekoppelde service van het type [AzureSearch](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c8e95-213">A linked service of type [AzureSearch](#linked-service-properties).</span></span>
2.  <span data-ttu-id="c8e95-214">Een gekoppelde service van het type [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c8e95-214">A linked service of type [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span></span>
3.  <span data-ttu-id="c8e95-215">Invoer [gegevensset](data-factory-create-datasets.md) van het type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c8e95-215">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
4.  <span data-ttu-id="c8e95-216">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureSearchIndex](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c8e95-216">An output [dataset](data-factory-create-datasets.md) of type [AzureSearchIndex](#dataset-properties).</span></span>
4.  <span data-ttu-id="c8e95-217">Een [pijplijn](data-factory-create-pipelines.md) met een kopieeractiviteit die gebruikmaakt van [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) en [AzureSearchIndexSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="c8e95-217">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) and [AzureSearchIndexSink](#copy-activity-properties).</span></span>

<span data-ttu-id="c8e95-218">Hallo voorbeeld kopieert per uur timeseries gegevens uit een lokale SQL Server-database tooan Azure Search-index.</span><span class="sxs-lookup"><span data-stu-id="c8e95-218">hello sample copies time-series data from an on-premises SQL Server database tooan Azure Search index hourly.</span></span> <span data-ttu-id="c8e95-219">Hallo JSON-eigenschappen die in dit voorbeeld worden beschreven in de secties na Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="c8e95-219">hello JSON properties used in this sample are described in sections following hello samples.</span></span>

<span data-ttu-id="c8e95-220">Instellen als eerste stap Hallo data management gateway op uw on-premises machine.</span><span class="sxs-lookup"><span data-stu-id="c8e95-220">As a first step, setup hello data management gateway on your on-premises machine.</span></span> <span data-ttu-id="c8e95-221">Hallo-instructies vindt u in Hallo [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="c8e95-221">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="c8e95-222">**Azure Search gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="c8e95-222">**Azure Search linked service:**</span></span>

```JSON
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

<span data-ttu-id="c8e95-223">**SQL Server gekoppeld-service**</span><span class="sxs-lookup"><span data-stu-id="c8e95-223">**SQL Server linked service**</span></span>

```JSON
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```

<span data-ttu-id="c8e95-224">**SQL Server-invoergegevensset**</span><span class="sxs-lookup"><span data-stu-id="c8e95-224">**SQL Server input dataset**</span></span>

<span data-ttu-id="c8e95-225">Hallo-voorbeeld wordt ervan uitgegaan dat u hebt een tabel 'MijnTabel' gemaakt in SQL Server en deze bevat een kolom met de naam 'timestampcolumn' voor de reeksgegevens.</span><span class="sxs-lookup"><span data-stu-id="c8e95-225">hello sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="c8e95-226">U kunt een query over meerdere tabellen in dezelfde database met behulp van een één gegevensset, maar één tabel moet worden gebruikt voor een van deze dataset Hallo tableName typeProperty Hallo.</span><span class="sxs-lookup"><span data-stu-id="c8e95-226">You can query over multiple tables within hello same database using a single dataset, but a single table must be used for hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="c8e95-227">Instelling 'extern': 'true' informeert Data Factory-service die gegevensset Hallo externe toohello data factory is en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="c8e95-227">Setting “external”: ”true” informs Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
{
  "name": "SqlServerDataset",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
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

<span data-ttu-id="c8e95-228">**Azure Search uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="c8e95-228">**Azure Search output dataset:**</span></span>

<span data-ttu-id="c8e95-229">Hallo voorbeeld kopieën gegevens tooan Azure Search-index met de naam **producten**.</span><span class="sxs-lookup"><span data-stu-id="c8e95-229">hello sample copies data tooan Azure Search index named **products**.</span></span> <span data-ttu-id="c8e95-230">Data Factory maakt geen Hallo index.</span><span class="sxs-lookup"><span data-stu-id="c8e95-230">Data Factory does not create hello index.</span></span> <span data-ttu-id="c8e95-231">tootest hello steekproef, maakt u een index met deze naam.</span><span class="sxs-lookup"><span data-stu-id="c8e95-231">tootest hello sample, create an index with this name.</span></span> <span data-ttu-id="c8e95-232">Hello Azure Search-index maken met Hallo hetzelfde aantal kolommen in Hallo invoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="c8e95-232">Create hello Azure Search index with hello same number of columns as in hello input dataset.</span></span> <span data-ttu-id="c8e95-233">Nieuwe vermeldingen worden toohello Azure Search-index toegevoegd om het uur.</span><span class="sxs-lookup"><span data-stu-id="c8e95-233">New entries are added toohello Azure Search index every hour.</span></span>

```JSON
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties" : {
            "indexName": "products",
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
   }
}
```

<span data-ttu-id="c8e95-234">**De kopieeractiviteit in een pijplijn met de SQL-bron en sink van Azure Search-Index:**</span><span class="sxs-lookup"><span data-stu-id="c8e95-234">**Copy activity in a pipeline with SQL source and Azure Search Index sink:**</span></span>

<span data-ttu-id="c8e95-235">Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur.</span><span class="sxs-lookup"><span data-stu-id="c8e95-235">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="c8e95-236">Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**SqlSource** en **sink** type is ingesteld, te**AzureSearchIndexSink**.</span><span class="sxs-lookup"><span data-stu-id="c8e95-236">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**AzureSearchIndexSink**.</span></span> <span data-ttu-id="c8e95-237">Hallo SQL-query is opgegeven voor Hallo **SqlReaderQuery** eigenschap Hallo gegevens selecteert in Hallo voorbij toocopy uur.</span><span class="sxs-lookup"><span data-stu-id="c8e95-237">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoAzureSearchIndex",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSearchIndexDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "AzureSearchIndexSink"
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

<span data-ttu-id="c8e95-238">Als u gegevens uit een cloud-gegevensarchief in Azure Search kopiëren wilt `executionLocation` eigenschap is vereist.</span><span class="sxs-lookup"><span data-stu-id="c8e95-238">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="c8e95-239">Hallo volgende JSON-fragment toont Hallo-wijziging nodig onder Kopieeractiviteit `typeProperties` als voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="c8e95-239">hello following JSON snippet shows hello change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="c8e95-240">Controleer [kopiëren van gegevens tussen gegevensarchieven cloud](data-factory-data-movement-activities.md#global) sectie voor meer details en de ondersteunde waarden.</span><span class="sxs-lookup"><span data-stu-id="c8e95-240">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```


## <a name="copy-from-a-cloud-source"></a><span data-ttu-id="c8e95-241">Kopiëren van een cloud-bron</span><span class="sxs-lookup"><span data-stu-id="c8e95-241">Copy from a cloud source</span></span>
<span data-ttu-id="c8e95-242">Als u gegevens uit een cloud-gegevensarchief in Azure Search kopiëren wilt `executionLocation` eigenschap is vereist.</span><span class="sxs-lookup"><span data-stu-id="c8e95-242">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="c8e95-243">Hallo volgende JSON-fragment toont Hallo-wijziging nodig onder Kopieeractiviteit `typeProperties` als voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="c8e95-243">hello following JSON snippet shows hello change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="c8e95-244">Controleer [kopiëren van gegevens tussen gegevensarchieven cloud](data-factory-data-movement-activities.md#global) sectie voor meer details en de ondersteunde waarden.</span><span class="sxs-lookup"><span data-stu-id="c8e95-244">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```

<span data-ttu-id="c8e95-245">U kunt ook kolommen uit de bron gegevensset toocolumns uit sink gegevensset in de definitie van de activiteit kopiëren Hallo toewijzen.</span><span class="sxs-lookup"><span data-stu-id="c8e95-245">You can also map columns from source dataset toocolumns from sink dataset in hello copy activity definition.</span></span> <span data-ttu-id="c8e95-246">Zie voor meer informatie [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="c8e95-246">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="c8e95-247">Prestaties en afstemmen</span><span class="sxs-lookup"><span data-stu-id="c8e95-247">Performance and tuning</span></span>  
<span data-ttu-id="c8e95-248">Zie Hallo [Kopieeractiviteit prestaties en prestatieafstemming handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) en verschillende manieren toooptimize deze.</span><span class="sxs-lookup"><span data-stu-id="c8e95-248">See hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c8e95-249">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c8e95-249">Next steps</span></span>
<span data-ttu-id="c8e95-250">Zie Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="c8e95-250">See hello following articles:</span></span>

* <span data-ttu-id="c8e95-251">[Zelfstudie voor kopiëren-activiteit](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies voor het maken van een pijplijn met een Kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="c8e95-251">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
