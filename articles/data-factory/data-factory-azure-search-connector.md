---
title: Push-gegevens naar de Search-index met behulp van de Data Factory | Microsoft Docs
description: Meer informatie over de push-gegevens naar Azure Search-Index met behulp van Azure Data Factory.
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
ms.openlocfilehash: 5c617c7a2f2eb4da2164ce5f802354a64dfd1fa1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="push-data-to-an-azure-search-index-by-using-azure-data-factory"></a><span data-ttu-id="8fec7-103">Push-gegevens naar een Azure Search-index met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="8fec7-103">Push data to an Azure Search index by using Azure Data Factory</span></span>
<span data-ttu-id="8fec7-104">In dit artikel wordt beschreven hoe de Kopieeractiviteit gebruiken om gegevens te pushen van een gegevensarchief ondersteunde bron voor Azure Search-index.</span><span class="sxs-lookup"><span data-stu-id="8fec7-104">This article describes how to use the Copy Activity to push data from a supported source data store to Azure Search index.</span></span> <span data-ttu-id="8fec7-105">Ondersteunde bron gegevensarchieven worden vermeld in de kolom bron van de [ondersteunde gegevensbronnen en put](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel.</span><span class="sxs-lookup"><span data-stu-id="8fec7-105">Supported source data stores are listed in the Source column of the [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="8fec7-106">In dit artikel is gebaseerd op de [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin Kopieeractiviteit en combinaties van ondersteunde gegevens store een algemeen overzicht van de verplaatsing van gegevens biedt.</span><span class="sxs-lookup"><span data-stu-id="8fec7-106">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="8fec7-107">Connectiviteit inschakelen</span><span class="sxs-lookup"><span data-stu-id="8fec7-107">Enabling connectivity</span></span>
<span data-ttu-id="8fec7-108">Als u Data Factory-service verbinding maken met een on-premises gegevensopslag, moet u Data Management Gateway installeren in uw on-premises omgeving.</span><span class="sxs-lookup"><span data-stu-id="8fec7-108">To allow Data Factory service connect to an on-premises data store, you install Data Management Gateway in your on-premises environment.</span></span> <span data-ttu-id="8fec7-109">U kunt de gateway installeren op dezelfde computer als hosts de brongegevens opslaan of op een afzonderlijke computer om te voorkomen dat concurrentie voor resources met de gegevensopslag.</span><span class="sxs-lookup"><span data-stu-id="8fec7-109">You can install gateway on the same machine that hosts the source data store or on a separate machine to avoid competing for resources with the data store.</span></span>

<span data-ttu-id="8fec7-110">Data Management Gateway verbindt on-premises gegevensbronnen met cloud-services in een veilige en beheerde manier.</span><span class="sxs-lookup"><span data-stu-id="8fec7-110">Data Management Gateway connects on-premises data sources to cloud services in a secure and managed way.</span></span> <span data-ttu-id="8fec7-111">Zie [gegevens verplaatsen tussen on-premises en cloud](data-factory-move-data-between-onprem-and-cloud.md) voor meer informatie over Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="8fec7-111">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

## <a name="getting-started"></a><span data-ttu-id="8fec7-112">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="8fec7-112">Getting started</span></span>
<span data-ttu-id="8fec7-113">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens uit een gegevensopslag bron verstuurd naar Azure Search-index met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="8fec7-113">You can create a pipeline with a copy activity that pushes data from a source data store to Azure Search index by using different tools/APIs.</span></span>

<span data-ttu-id="8fec7-114">De eenvoudigste manier om een pijplijn maken is met de **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="8fec7-114">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="8fec7-115">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met de wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="8fec7-115">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="8fec7-116">U kunt ook de volgende hulpprogramma's gebruiken voor het maken van een pijplijn: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon**, **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="8fec7-116">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="8fec7-117">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies voor een pijplijn maken met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="8fec7-117">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="8fec7-118">Of u de hulpprogramma's of API's gebruiken, moet u de volgende stappen voor het maken van een pijplijn die de gegevens vanuit een brongegevensarchief naar een gegevensarchief sink verplaatst uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="8fec7-118">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="8fec7-119">Maak **gekoppelde services** slaat om invoer- en gegevens te koppelen aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="8fec7-119">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="8fec7-120">Maak **gegevenssets** vertegenwoordigt de invoer- en -gegevens voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="8fec7-120">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="8fec7-121">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="8fec7-121">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="8fec7-122">Wanneer u de wizard gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8fec7-122">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="8fec7-123">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van de JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="8fec7-123">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="8fec7-124">Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die worden gebruikt om gegevens te kopiëren naar Azure Search-index [JSON-voorbeeld: gegevens kopiëren van on-premises SQL-Server naar Azure Search-index](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="8fec7-124">For a sample with JSON definitions for Data Factory entities that are used to copy data to Azure Search index, see [JSON example: Copy data from on-premises SQL Server to Azure Search index](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) section of this article.</span></span> 

<span data-ttu-id="8fec7-125">De volgende secties bevatten informatie over de JSON-eigenschappen die worden gebruikt voor het definiëren van Data Factory-entiteiten die specifiek voor Azure Search-Index:</span><span class="sxs-lookup"><span data-stu-id="8fec7-125">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Search Index:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="8fec7-126">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="8fec7-126">Linked service properties</span></span>

<span data-ttu-id="8fec7-127">De volgende tabel bevat beschrijvingen van JSON-elementen die specifiek voor de service Azure Search is gekoppeld zijn.</span><span class="sxs-lookup"><span data-stu-id="8fec7-127">The following table provides descriptions for JSON elements that are specific to the Azure Search linked service.</span></span>

| <span data-ttu-id="8fec7-128">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="8fec7-128">Property</span></span> | <span data-ttu-id="8fec7-129">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8fec7-129">Description</span></span> | <span data-ttu-id="8fec7-130">Vereist</span><span class="sxs-lookup"><span data-stu-id="8fec7-130">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="8fec7-131">type</span><span class="sxs-lookup"><span data-stu-id="8fec7-131">type</span></span> | <span data-ttu-id="8fec7-132">De eigenschap type moet worden ingesteld op: **AzureSearch**.</span><span class="sxs-lookup"><span data-stu-id="8fec7-132">The type property must be set to: **AzureSearch**.</span></span> | <span data-ttu-id="8fec7-133">Ja</span><span class="sxs-lookup"><span data-stu-id="8fec7-133">Yes</span></span> |
| <span data-ttu-id="8fec7-134">URL</span><span class="sxs-lookup"><span data-stu-id="8fec7-134">url</span></span> | <span data-ttu-id="8fec7-135">De URL voor de Azure Search-service.</span><span class="sxs-lookup"><span data-stu-id="8fec7-135">URL for the Azure Search service.</span></span> | <span data-ttu-id="8fec7-136">Ja</span><span class="sxs-lookup"><span data-stu-id="8fec7-136">Yes</span></span> |
| <span data-ttu-id="8fec7-137">sleutel</span><span class="sxs-lookup"><span data-stu-id="8fec7-137">key</span></span> | <span data-ttu-id="8fec7-138">Administrator-code voor de Azure Search-service.</span><span class="sxs-lookup"><span data-stu-id="8fec7-138">Admin key for the Azure Search service.</span></span> | <span data-ttu-id="8fec7-139">Ja</span><span class="sxs-lookup"><span data-stu-id="8fec7-139">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="8fec7-140">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="8fec7-140">Dataset properties</span></span>

<span data-ttu-id="8fec7-141">Zie voor een volledige lijst met eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets en secties, de [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="8fec7-141">For a full list of sections and properties that are available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="8fec7-142">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle typen van de gegevensset.</span><span class="sxs-lookup"><span data-stu-id="8fec7-142">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span> <span data-ttu-id="8fec7-143">De **typeProperties** sectie verschilt voor elk type dataset.</span><span class="sxs-lookup"><span data-stu-id="8fec7-143">The **typeProperties** section is different for each type of dataset.</span></span> <span data-ttu-id="8fec7-144">De typeProperties sectie voor een gegevensset van het type **AzureSearchIndex** heeft de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="8fec7-144">The typeProperties section for a dataset of the type **AzureSearchIndex** has the following properties:</span></span>

| <span data-ttu-id="8fec7-145">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="8fec7-145">Property</span></span> | <span data-ttu-id="8fec7-146">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8fec7-146">Description</span></span> | <span data-ttu-id="8fec7-147">Vereist</span><span class="sxs-lookup"><span data-stu-id="8fec7-147">Required</span></span> |
| -------- | ----------- | -------- |
| <span data-ttu-id="8fec7-148">type</span><span class="sxs-lookup"><span data-stu-id="8fec7-148">type</span></span> | <span data-ttu-id="8fec7-149">De eigenschap type moet worden ingesteld op **AzureSearchIndex**.</span><span class="sxs-lookup"><span data-stu-id="8fec7-149">The type property must be set to **AzureSearchIndex**.</span></span>| <span data-ttu-id="8fec7-150">Ja</span><span class="sxs-lookup"><span data-stu-id="8fec7-150">Yes</span></span> |
| <span data-ttu-id="8fec7-151">NaamCommunity</span><span class="sxs-lookup"><span data-stu-id="8fec7-151">indexName</span></span> | <span data-ttu-id="8fec7-152">De naam van de Azure Search-index.</span><span class="sxs-lookup"><span data-stu-id="8fec7-152">Name of the Azure Search index.</span></span> <span data-ttu-id="8fec7-153">Data Factory maakt niet de index.</span><span class="sxs-lookup"><span data-stu-id="8fec7-153">Data Factory does not create the index.</span></span> <span data-ttu-id="8fec7-154">De index moet bestaan in Azure Search.</span><span class="sxs-lookup"><span data-stu-id="8fec7-154">The index must exist in Azure Search.</span></span> | <span data-ttu-id="8fec7-155">Ja</span><span class="sxs-lookup"><span data-stu-id="8fec7-155">Yes</span></span> |


## <a name="copy-activity-properties"></a><span data-ttu-id="8fec7-156">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="8fec7-156">Copy activity properties</span></span>
<span data-ttu-id="8fec7-157">Zie voor een volledige lijst met eigenschappen die beschikbaar zijn voor het definiëren van activiteiten en secties, de [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="8fec7-157">For a full list of sections and properties that are available for defining activities, see the [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="8fec7-158">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoertabellen en verschillende beleidsregels zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="8fec7-158">Properties such as name, description, input and output tables, and various policies are available for all types of activities.</span></span> <span data-ttu-id="8fec7-159">Terwijl de eigenschappen die beschikbaar zijn in de sectie typeProperties variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="8fec7-159">Whereas, properties available in the typeProperties section vary with each activity type.</span></span> <span data-ttu-id="8fec7-160">Voor de Kopieeractiviteit variëren ze, afhankelijk van de typen van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="8fec7-160">For Copy Activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="8fec7-161">Voor de Kopieeractiviteit, wanneer de sink van het type is **AzureSearchIndexSink**, de volgende eigenschappen beschikbaar zijn in de sectie typeProperties:</span><span class="sxs-lookup"><span data-stu-id="8fec7-161">For Copy Activity, when the sink is of the type **AzureSearchIndexSink**, the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="8fec7-162">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="8fec7-162">Property</span></span> | <span data-ttu-id="8fec7-163">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="8fec7-163">Description</span></span> | <span data-ttu-id="8fec7-164">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="8fec7-164">Allowed values</span></span> | <span data-ttu-id="8fec7-165">Vereist</span><span class="sxs-lookup"><span data-stu-id="8fec7-165">Required</span></span> |
| -------- | ----------- | -------------- | -------- |
| <span data-ttu-id="8fec7-166">WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="8fec7-166">WriteBehavior</span></span> | <span data-ttu-id="8fec7-167">Geeft aan of samenvoegen of wanneer een document al in de index bestaat te vervangen.</span><span class="sxs-lookup"><span data-stu-id="8fec7-167">Specifies whether to merge or replace when a document already exists in the index.</span></span> <span data-ttu-id="8fec7-168">Zie de [WriteBehavior eigenschap](#writebehavior-property).</span><span class="sxs-lookup"><span data-stu-id="8fec7-168">See the [WriteBehavior property](#writebehavior-property).</span></span>| <span data-ttu-id="8fec7-169">samenvoegen (standaard)</span><span class="sxs-lookup"><span data-stu-id="8fec7-169">Merge (default)</span></span><br/><span data-ttu-id="8fec7-170">Uploaden</span><span class="sxs-lookup"><span data-stu-id="8fec7-170">Upload</span></span>| <span data-ttu-id="8fec7-171">Nee</span><span class="sxs-lookup"><span data-stu-id="8fec7-171">No</span></span> |
| <span data-ttu-id="8fec7-172">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="8fec7-172">WriteBatchSize</span></span> | <span data-ttu-id="8fec7-173">Gegevens geüpload naar de Azure Search-index wanneer de buffergrootte writeBatchSize bereikt.</span><span class="sxs-lookup"><span data-stu-id="8fec7-173">Uploads data into the Azure Search index when the buffer size reaches writeBatchSize.</span></span> <span data-ttu-id="8fec7-174">Zie de [WriteBatchSize eigenschap](#writebatchsize-property) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8fec7-174">See the [WriteBatchSize property](#writebatchsize-property) for details.</span></span> | <span data-ttu-id="8fec7-175">1-1000.</span><span class="sxs-lookup"><span data-stu-id="8fec7-175">1 to 1,000.</span></span> <span data-ttu-id="8fec7-176">Standaardwaarde is 1000.</span><span class="sxs-lookup"><span data-stu-id="8fec7-176">Default value is 1000.</span></span> | <span data-ttu-id="8fec7-177">Nee</span><span class="sxs-lookup"><span data-stu-id="8fec7-177">No</span></span> |

### <a name="writebehavior-property"></a><span data-ttu-id="8fec7-178">De eigenschap WriteBehavior</span><span class="sxs-lookup"><span data-stu-id="8fec7-178">WriteBehavior property</span></span>
<span data-ttu-id="8fec7-179">AzureSearchSink upserts bij het schrijven van gegevens.</span><span class="sxs-lookup"><span data-stu-id="8fec7-179">AzureSearchSink upserts when writing data.</span></span> <span data-ttu-id="8fec7-180">Bij het schrijven van een document, als de documentsleutel al in de Azure Search-index bestaat, updates Azure Search met andere woorden, het bestaande document in plaats van er een conflict uitzondering is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="8fec7-180">In other words, when writing a document, if the document key already exists in the Azure Search index, Azure Search updates the existing document rather than throwing a conflict exception.</span></span>

<span data-ttu-id="8fec7-181">De AzureSearchSink biedt de volgende twee upsert problemen (met behulp van AzureSearch SDK):</span><span class="sxs-lookup"><span data-stu-id="8fec7-181">The AzureSearchSink provides the following two upsert behaviors (by using AzureSearch SDK):</span></span>

- <span data-ttu-id="8fec7-182">**Samenvoegen**: alle kolommen in het nieuwe document met de huidige combineren.</span><span class="sxs-lookup"><span data-stu-id="8fec7-182">**Merge**: combine all the columns in the new document with the existing one.</span></span> <span data-ttu-id="8fec7-183">Voor kolommen met null-waarde in het nieuwe document, wordt de waarde in de bestaande waarde bewaard.</span><span class="sxs-lookup"><span data-stu-id="8fec7-183">For columns with null value in the new document, the value in the existing one is preserved.</span></span>
- <span data-ttu-id="8fec7-184">**Uploaden**: nieuw document vervangt de bestaande waarde.</span><span class="sxs-lookup"><span data-stu-id="8fec7-184">**Upload**: The new document replaces the existing one.</span></span> <span data-ttu-id="8fec7-185">Voor de kolommen is niet opgegeven in het nieuwe document, wordt de waarde ingesteld op null of er een niet-null-waarde in een bestaand document of niet is.</span><span class="sxs-lookup"><span data-stu-id="8fec7-185">For columns not specified in the new document, the value is set to null whether there is a non-null value in the existing document or not.</span></span>

<span data-ttu-id="8fec7-186">Het standaardgedrag **samenvoegen**.</span><span class="sxs-lookup"><span data-stu-id="8fec7-186">The default behavior is **Merge**.</span></span>

### <a name="writebatchsize-property"></a><span data-ttu-id="8fec7-187">De eigenschap WriteBatchSize</span><span class="sxs-lookup"><span data-stu-id="8fec7-187">WriteBatchSize Property</span></span>
<span data-ttu-id="8fec7-188">Azure Search-service ondersteunt documenten schrijven als een batch.</span><span class="sxs-lookup"><span data-stu-id="8fec7-188">Azure Search service supports writing documents as a batch.</span></span> <span data-ttu-id="8fec7-189">Een batch kunt 1-1000 acties bevatten.</span><span class="sxs-lookup"><span data-stu-id="8fec7-189">A batch can contain 1 to 1,000 Actions.</span></span> <span data-ttu-id="8fec7-190">Een actie verwerkt één document als de upload/merge-bewerking wilt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="8fec7-190">An action handles one document to perform the upload/merge operation.</span></span>

### <a name="data-type-support"></a><span data-ttu-id="8fec7-191">Ondersteuning voor gegevenstype</span><span class="sxs-lookup"><span data-stu-id="8fec7-191">Data type support</span></span>
<span data-ttu-id="8fec7-192">De volgende tabel geeft aan of een Azure Search-gegevenstype of niet wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="8fec7-192">The following table specifies whether an Azure Search data type is supported or not.</span></span>

| <span data-ttu-id="8fec7-193">Azure Search-gegevenstype</span><span class="sxs-lookup"><span data-stu-id="8fec7-193">Azure Search data type</span></span> | <span data-ttu-id="8fec7-194">Ondersteund in Azure Search Sink</span><span class="sxs-lookup"><span data-stu-id="8fec7-194">Supported in Azure Search Sink</span></span> |
| ---------------------- | ------------------------------ |
| <span data-ttu-id="8fec7-195">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="8fec7-195">String</span></span> | <span data-ttu-id="8fec7-196">J</span><span class="sxs-lookup"><span data-stu-id="8fec7-196">Y</span></span> |
| <span data-ttu-id="8fec7-197">Int32</span><span class="sxs-lookup"><span data-stu-id="8fec7-197">Int32</span></span> | <span data-ttu-id="8fec7-198">J</span><span class="sxs-lookup"><span data-stu-id="8fec7-198">Y</span></span> |
| <span data-ttu-id="8fec7-199">Int64</span><span class="sxs-lookup"><span data-stu-id="8fec7-199">Int64</span></span> | <span data-ttu-id="8fec7-200">J</span><span class="sxs-lookup"><span data-stu-id="8fec7-200">Y</span></span> |
| <span data-ttu-id="8fec7-201">dubbele</span><span class="sxs-lookup"><span data-stu-id="8fec7-201">Double</span></span> | <span data-ttu-id="8fec7-202">J</span><span class="sxs-lookup"><span data-stu-id="8fec7-202">Y</span></span> |
| <span data-ttu-id="8fec7-203">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="8fec7-203">Boolean</span></span> | <span data-ttu-id="8fec7-204">J</span><span class="sxs-lookup"><span data-stu-id="8fec7-204">Y</span></span> |
| <span data-ttu-id="8fec7-205">DataTimeOffset</span><span class="sxs-lookup"><span data-stu-id="8fec7-205">DataTimeOffset</span></span> | <span data-ttu-id="8fec7-206">J</span><span class="sxs-lookup"><span data-stu-id="8fec7-206">Y</span></span> |
| <span data-ttu-id="8fec7-207">Tekenreeksmatrix</span><span class="sxs-lookup"><span data-stu-id="8fec7-207">String Array</span></span> | <span data-ttu-id="8fec7-208">N</span><span class="sxs-lookup"><span data-stu-id="8fec7-208">N</span></span> |
| <span data-ttu-id="8fec7-209">GeographyPoint</span><span class="sxs-lookup"><span data-stu-id="8fec7-209">GeographyPoint</span></span> | <span data-ttu-id="8fec7-210">N</span><span class="sxs-lookup"><span data-stu-id="8fec7-210">N</span></span> |

## <a name="json-example-copy-data-from-on-premises-sql-server-to-azure-search-index"></a><span data-ttu-id="8fec7-211">JSON-voorbeeld: gegevens kopiëren van on-premises SQL-Server naar Azure Search-index</span><span class="sxs-lookup"><span data-stu-id="8fec7-211">JSON example: Copy data from on-premises SQL Server to Azure Search index</span></span>

<span data-ttu-id="8fec7-212">Het volgende voorbeeld toont:</span><span class="sxs-lookup"><span data-stu-id="8fec7-212">The following sample shows:</span></span>

1.  <span data-ttu-id="8fec7-213">Een gekoppelde service van het type [AzureSearch](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8fec7-213">A linked service of type [AzureSearch](#linked-service-properties).</span></span>
2.  <span data-ttu-id="8fec7-214">Een gekoppelde service van het type [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="8fec7-214">A linked service of type [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).</span></span>
3.  <span data-ttu-id="8fec7-215">Invoer [gegevensset](data-factory-create-datasets.md) van het type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8fec7-215">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
4.  <span data-ttu-id="8fec7-216">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureSearchIndex](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="8fec7-216">An output [dataset](data-factory-create-datasets.md) of type [AzureSearchIndex](#dataset-properties).</span></span>
4.  <span data-ttu-id="8fec7-217">Een [pijplijn](data-factory-create-pipelines.md) met een kopieeractiviteit die gebruikmaakt van [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) en [AzureSearchIndexSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="8fec7-217">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) and [AzureSearchIndexSink](#copy-activity-properties).</span></span>

<span data-ttu-id="8fec7-218">Het voorbeeld kopieert tijdreeks gegevens van een on-premises SQL Server database naar een Azure Search-index per uur.</span><span class="sxs-lookup"><span data-stu-id="8fec7-218">The sample copies time-series data from an on-premises SQL Server database to an Azure Search index hourly.</span></span> <span data-ttu-id="8fec7-219">De JSON-eigenschappen die in dit voorbeeld worden in voorbeelden van de volgende secties beschreven.</span><span class="sxs-lookup"><span data-stu-id="8fec7-219">The JSON properties used in this sample are described in sections following the samples.</span></span>

<span data-ttu-id="8fec7-220">Als een eerste stap het instellen van de data management gateway op uw on-premises machine.</span><span class="sxs-lookup"><span data-stu-id="8fec7-220">As a first step, setup the data management gateway on your on-premises machine.</span></span> <span data-ttu-id="8fec7-221">De instructies vindt u in de [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="8fec7-221">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="8fec7-222">**Azure Search gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="8fec7-222">**Azure Search linked service:**</span></span>

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

<span data-ttu-id="8fec7-223">**SQL Server gekoppeld-service**</span><span class="sxs-lookup"><span data-stu-id="8fec7-223">**SQL Server linked service**</span></span>

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

<span data-ttu-id="8fec7-224">**SQL Server-invoergegevensset**</span><span class="sxs-lookup"><span data-stu-id="8fec7-224">**SQL Server input dataset**</span></span>

<span data-ttu-id="8fec7-225">Het voorbeeld wordt ervan uitgegaan dat u hebt een tabel 'MijnTabel' gemaakt in SQL Server en deze bevat een kolom met de naam 'timestampcolumn' voor de reeksgegevens.</span><span class="sxs-lookup"><span data-stu-id="8fec7-225">The sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="8fec7-226">U kunt een query over meerdere tabellen binnen dezelfde database met behulp van een één gegevensset, maar één tabel moet worden gebruikt voor de gegevensset tableName typeProperty.</span><span class="sxs-lookup"><span data-stu-id="8fec7-226">You can query over multiple tables within the same database using a single dataset, but a single table must be used for the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="8fec7-227">Instelling 'extern': 'true' informeert Data Factory-service dat de dataset extern is aan de gegevensfactory en niet wordt geproduceerd door een activiteit in de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="8fec7-227">Setting “external”: ”true” informs Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="8fec7-228">**Azure Search uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="8fec7-228">**Azure Search output dataset:**</span></span>

<span data-ttu-id="8fec7-229">Het voorbeeld worden gegevens gekopieerd naar een Azure Search-index met de naam **producten**.</span><span class="sxs-lookup"><span data-stu-id="8fec7-229">The sample copies data to an Azure Search index named **products**.</span></span> <span data-ttu-id="8fec7-230">Data Factory maakt niet de index.</span><span class="sxs-lookup"><span data-stu-id="8fec7-230">Data Factory does not create the index.</span></span> <span data-ttu-id="8fec7-231">Als u wilt testen van de steekproef, moet u een index maken met deze naam.</span><span class="sxs-lookup"><span data-stu-id="8fec7-231">To test the sample, create an index with this name.</span></span> <span data-ttu-id="8fec7-232">De Azure Search-index maken met hetzelfde aantal kolommen in de invoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="8fec7-232">Create the Azure Search index with the same number of columns as in the input dataset.</span></span> <span data-ttu-id="8fec7-233">Nieuwe items worden toegevoegd aan de Azure Search-index om het uur.</span><span class="sxs-lookup"><span data-stu-id="8fec7-233">New entries are added to the Azure Search index every hour.</span></span>

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

<span data-ttu-id="8fec7-234">**De kopieeractiviteit in een pijplijn met de SQL-bron en sink van Azure Search-Index:**</span><span class="sxs-lookup"><span data-stu-id="8fec7-234">**Copy activity in a pipeline with SQL source and Azure Search Index sink:**</span></span>

<span data-ttu-id="8fec7-235">De pijplijn bevat een Kopieeractiviteit die is geconfigureerd voor gebruik van de invoer- en uitvoergegevenssets en elk uur is gepland.</span><span class="sxs-lookup"><span data-stu-id="8fec7-235">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="8fec7-236">In de pijplijn-JSON-definitie de **bron** type is ingesteld op **SqlSource** en **sink** type is ingesteld op **AzureSearchIndexSink**.</span><span class="sxs-lookup"><span data-stu-id="8fec7-236">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **AzureSearchIndexSink**.</span></span> <span data-ttu-id="8fec7-237">De SQL-query die is opgegeven voor de **SqlReaderQuery** eigenschap selecteert u de gegevens in het afgelopen uur te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="8fec7-237">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

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

<span data-ttu-id="8fec7-238">Als u gegevens uit een cloud-gegevensarchief in Azure Search kopiëren wilt `executionLocation` eigenschap is vereist.</span><span class="sxs-lookup"><span data-stu-id="8fec7-238">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="8fec7-239">De volgende JSON-fragment toont de wijziging nodig onder Kopieeractiviteit `typeProperties` als voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="8fec7-239">The following JSON snippet shows the change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="8fec7-240">Controleer [kopiëren van gegevens tussen gegevensarchieven cloud](data-factory-data-movement-activities.md#global) sectie voor meer details en de ondersteunde waarden.</span><span class="sxs-lookup"><span data-stu-id="8fec7-240">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

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


## <a name="copy-from-a-cloud-source"></a><span data-ttu-id="8fec7-241">Kopiëren van een cloud-bron</span><span class="sxs-lookup"><span data-stu-id="8fec7-241">Copy from a cloud source</span></span>
<span data-ttu-id="8fec7-242">Als u gegevens uit een cloud-gegevensarchief in Azure Search kopiëren wilt `executionLocation` eigenschap is vereist.</span><span class="sxs-lookup"><span data-stu-id="8fec7-242">If you are copying data from a cloud data store into Azure Search, `executionLocation` property is required.</span></span> <span data-ttu-id="8fec7-243">De volgende JSON-fragment toont de wijziging nodig onder Kopieeractiviteit `typeProperties` als voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="8fec7-243">The following JSON snippet shows the change needed under Copy Activity `typeProperties` as an example.</span></span> <span data-ttu-id="8fec7-244">Controleer [kopiëren van gegevens tussen gegevensarchieven cloud](data-factory-data-movement-activities.md#global) sectie voor meer details en de ondersteunde waarden.</span><span class="sxs-lookup"><span data-stu-id="8fec7-244">Check [Copy data between cloud data stores](data-factory-data-movement-activities.md#global) section for supported values and more details.</span></span>

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

<span data-ttu-id="8fec7-245">U kunt ook kolommen uit de bron-gegevensset naar kolommen uit sink gegevensset in de definitie van de activiteit kopiëren toewijzen.</span><span class="sxs-lookup"><span data-stu-id="8fec7-245">You can also map columns from source dataset to columns from sink dataset in the copy activity definition.</span></span> <span data-ttu-id="8fec7-246">Zie voor meer informatie [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="8fec7-246">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="8fec7-247">Prestaties en afstemmen</span><span class="sxs-lookup"><span data-stu-id="8fec7-247">Performance and tuning</span></span>  
<span data-ttu-id="8fec7-248">Zie de [Kopieeractiviteit prestaties en prestatieafstemming handleiding](data-factory-copy-activity-performance.md) voor meer informatie over de belangrijkste factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) en verschillende manieren om te optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="8fec7-248">See the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) and various ways to optimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8fec7-249">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8fec7-249">Next steps</span></span>
<span data-ttu-id="8fec7-250">Zie de volgende artikelen:</span><span class="sxs-lookup"><span data-stu-id="8fec7-250">See the following articles:</span></span>

* <span data-ttu-id="8fec7-251">[Zelfstudie voor kopiëren-activiteit](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies voor het maken van een pijplijn met een Kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="8fec7-251">[Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions for creating a pipeline with a Copy Activity.</span></span>
