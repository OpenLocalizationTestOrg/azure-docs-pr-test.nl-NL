---
title: Verplaatsen van gegevens van Web-tabel met behulp van Azure Data Factory | Microsoft Docs
description: Meer informatie over het verplaatsen van gegevens uit een tabel in een webpagina met behulp van Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f54a26a4-baa4-4255-9791-5a8f935898e2
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: 9e006bc7289fa0239f1650ac6ad43dd159e3c7e0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-a-web-table-source-using-azure-data-factory"></a><span data-ttu-id="a8069-103">Verplaatsen van gegevens uit een tabel Webbron met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a8069-103">Move data from a Web table source using Azure Data Factory</span></span>
<span data-ttu-id="a8069-104">In dit artikel bevat een overzicht van het gebruik van de Kopieeractiviteit in Azure Data Factory om gegevens te verplaatsen van een tabel in een webpagina met een ondersteunde sink-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="a8069-104">This article outlines how to use the Copy Activity in Azure Data Factory to move data from a table in a Web page to a supported sink data store.</span></span> <span data-ttu-id="a8069-105">In dit artikel is gebaseerd op de [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel met daarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit en de lijst met gegevensarchieven ondersteund als bronnen/Put.</span><span class="sxs-lookup"><span data-stu-id="a8069-105">This article builds on the [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and the list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="a8069-106">Data factory ondersteunt momenteel alleen zwevend gegevens uit een tabel Web naar andere gegevensarchieven, maar niet verplaatsen van gegevens van andere gegevens worden opgeslagen op een doel van de tabel Web.</span><span class="sxs-lookup"><span data-stu-id="a8069-106">Data factory currently supports only moving data from a Web table to other data stores, but not moving data from other data stores to a Web table destination.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a8069-107">Deze Web-connector ondersteunt momenteel alleen uitpakken tabelinhoud uit een HTML-pagina.</span><span class="sxs-lookup"><span data-stu-id="a8069-107">This Web connector currently supports only extracting table content from an HTML page.</span></span> <span data-ttu-id="a8069-108">Voor informatie over het ophalen van gegevens van een HTTP/s-eindpunt gebruik [HTTP connector](data-factory-http-connector.md) in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="a8069-108">To retrieve data from a HTTP/s endpoint, use [HTTP connector](data-factory-http-connector.md) instead.</span></span>

## <a name="getting-started"></a><span data-ttu-id="a8069-109">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="a8069-109">Getting started</span></span>
<span data-ttu-id="a8069-110">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens vanuit een on-premises Cassandra-gegevensopslag verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="a8069-110">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="a8069-111">De eenvoudigste manier om een pijplijn maken is met de **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="a8069-111">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="a8069-112">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met de wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="a8069-112">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="a8069-113">U kunt ook de volgende hulpprogramma's gebruiken voor het maken van een pijplijn: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon**, **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="a8069-113">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="a8069-114">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies voor een pijplijn maken met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="a8069-114">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="a8069-115">Of u de hulpprogramma's of API's gebruiken, moet u de volgende stappen voor het maken van een pijplijn die de gegevens vanuit een brongegevensarchief naar een gegevensarchief sink verplaatst uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="a8069-115">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="a8069-116">Maak **gekoppelde services** slaat om invoer- en gegevens te koppelen aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="a8069-116">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="a8069-117">Maak **gegevenssets** vertegenwoordigt de invoer- en -gegevens voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="a8069-117">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="a8069-118">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="a8069-118">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="a8069-119">Wanneer u de wizard gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a8069-119">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="a8069-120">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van de JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="a8069-120">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="a8069-121">Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die worden gebruikt om gegevens te kopiëren uit een tabel web [JSON-voorbeeld: gegevens kopiëren van de tabel Web naar Azure Blob](#json-example-copy-data-from-web-table-to-azure-blob) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="a8069-121">For a sample with JSON definitions for Data Factory entities that are used to copy data from a web table, see [JSON example: Copy data from Web table to Azure Blob](#json-example-copy-data-from-web-table-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="a8069-122">De volgende secties bevatten informatie over de JSON-eigenschappen die worden gebruikt voor het definiëren van Data Factory-entiteiten specifieke naar een Web-tabel:</span><span class="sxs-lookup"><span data-stu-id="a8069-122">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Web table:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="a8069-123">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="a8069-123">Linked service properties</span></span>
<span data-ttu-id="a8069-124">De volgende tabel bevat een beschrijving voor JSON-elementen die specifiek zijn voor de gekoppelde webservice.</span><span class="sxs-lookup"><span data-stu-id="a8069-124">The following table provides description for JSON elements specific to Web linked service.</span></span>

| <span data-ttu-id="a8069-125">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="a8069-125">Property</span></span> | <span data-ttu-id="a8069-126">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a8069-126">Description</span></span> | <span data-ttu-id="a8069-127">Vereist</span><span class="sxs-lookup"><span data-stu-id="a8069-127">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a8069-128">type</span><span class="sxs-lookup"><span data-stu-id="a8069-128">type</span></span> |<span data-ttu-id="a8069-129">De eigenschap type moet worden ingesteld op: **Web**</span><span class="sxs-lookup"><span data-stu-id="a8069-129">The type property must be set to: **Web**</span></span> |<span data-ttu-id="a8069-130">Ja</span><span class="sxs-lookup"><span data-stu-id="a8069-130">Yes</span></span> |
| <span data-ttu-id="a8069-131">URL</span><span class="sxs-lookup"><span data-stu-id="a8069-131">Url</span></span> |<span data-ttu-id="a8069-132">URL van de webbron</span><span class="sxs-lookup"><span data-stu-id="a8069-132">URL to the Web source</span></span> |<span data-ttu-id="a8069-133">Ja</span><span class="sxs-lookup"><span data-stu-id="a8069-133">Yes</span></span> |
| <span data-ttu-id="a8069-134">authenticationType</span><span class="sxs-lookup"><span data-stu-id="a8069-134">authenticationType</span></span> |<span data-ttu-id="a8069-135">Anonieme.</span><span class="sxs-lookup"><span data-stu-id="a8069-135">Anonymous.</span></span> |<span data-ttu-id="a8069-136">Ja</span><span class="sxs-lookup"><span data-stu-id="a8069-136">Yes</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="a8069-137">Anonieme verificatie</span><span class="sxs-lookup"><span data-stu-id="a8069-137">Using Anonymous authentication</span></span>

```json
{
    "name": "web",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="a8069-138">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="a8069-138">Dataset properties</span></span>
<span data-ttu-id="a8069-139">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van de [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="a8069-139">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="a8069-140">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).</span><span class="sxs-lookup"><span data-stu-id="a8069-140">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="a8069-141">De **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over de locatie van de gegevens in het gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="a8069-141">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="a8069-142">De typeProperties sectie voor de gegevensset van het type **WebTable** heeft de volgende eigenschappen</span><span class="sxs-lookup"><span data-stu-id="a8069-142">The typeProperties section for dataset of type **WebTable** has the following properties</span></span>

| <span data-ttu-id="a8069-143">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="a8069-143">Property</span></span> | <span data-ttu-id="a8069-144">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a8069-144">Description</span></span> | <span data-ttu-id="a8069-145">Vereist</span><span class="sxs-lookup"><span data-stu-id="a8069-145">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="a8069-146">type</span><span class="sxs-lookup"><span data-stu-id="a8069-146">type</span></span> |<span data-ttu-id="a8069-147">Het type van de gegevensset.</span><span class="sxs-lookup"><span data-stu-id="a8069-147">type of the dataset.</span></span> <span data-ttu-id="a8069-148">moet worden ingesteld op **WebTable**</span><span class="sxs-lookup"><span data-stu-id="a8069-148">must be set to **WebTable**</span></span> |<span data-ttu-id="a8069-149">Ja</span><span class="sxs-lookup"><span data-stu-id="a8069-149">Yes</span></span> |
| <span data-ttu-id="a8069-150">Pad</span><span class="sxs-lookup"><span data-stu-id="a8069-150">path</span></span> |<span data-ttu-id="a8069-151">Een relatieve URL naar de resource die de tabel bevat.</span><span class="sxs-lookup"><span data-stu-id="a8069-151">A relative URL to the resource that contains the table.</span></span> |<span data-ttu-id="a8069-152">Nee.</span><span class="sxs-lookup"><span data-stu-id="a8069-152">No.</span></span> <span data-ttu-id="a8069-153">Als het pad niet wordt opgegeven, worden alleen de URL die is opgegeven in de definitie van de gekoppelde service wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a8069-153">When path is not specified, only the URL specified in the linked service definition is used.</span></span> |
| <span data-ttu-id="a8069-154">Index</span><span class="sxs-lookup"><span data-stu-id="a8069-154">index</span></span> |<span data-ttu-id="a8069-155">De index van de tabel in de resource.</span><span class="sxs-lookup"><span data-stu-id="a8069-155">The index of the table in the resource.</span></span> <span data-ttu-id="a8069-156">Zie [Get-index van een tabel in een HTML-pagina](#get-index-of-a-table-in-an-html-page) sectie voor stappen voor het ophalen van de index van een tabel in een HTML-pagina.</span><span class="sxs-lookup"><span data-stu-id="a8069-156">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span></span> |<span data-ttu-id="a8069-157">Ja</span><span class="sxs-lookup"><span data-stu-id="a8069-157">Yes</span></span> |

<span data-ttu-id="a8069-158">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="a8069-158">**Example:**</span></span>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

## <a name="copy-activity-properties"></a><span data-ttu-id="a8069-159">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="a8069-159">Copy activity properties</span></span>
<span data-ttu-id="a8069-160">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van activiteiten van de [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="a8069-160">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="a8069-161">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en -beleid zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="a8069-161">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="a8069-162">Terwijl de eigenschappen die beschikbaar zijn in de sectie typeProperties van de activiteit variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="a8069-162">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="a8069-163">Voor de kopieeractiviteit variëren ze, afhankelijk van de typen van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="a8069-163">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="a8069-164">Wanneer de bron is in de kopieerbewerking is momenteel van het type **WebSource**, zonder aanvullende eigenschappen worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="a8069-164">Currently, when the source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>


## <a name="json-example-copy-data-from-web-table-to-azure-blob"></a><span data-ttu-id="a8069-165">JSON-voorbeeld: gegevens kopiëren van de tabel Web naar Azure Blob</span><span class="sxs-lookup"><span data-stu-id="a8069-165">JSON example: Copy data from Web table to Azure Blob</span></span>
<span data-ttu-id="a8069-166">Het volgende voorbeeld toont:</span><span class="sxs-lookup"><span data-stu-id="a8069-166">The following sample shows:</span></span>

1. <span data-ttu-id="a8069-167">Een gekoppelde service van het type [Web](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a8069-167">A linked service of type [Web](#linked-service-properties).</span></span>
2. <span data-ttu-id="a8069-168">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a8069-168">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="a8069-169">Invoer [gegevensset](data-factory-create-datasets.md) van het type [WebTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a8069-169">An input [dataset](data-factory-create-datasets.md) of type [WebTable](#dataset-properties).</span></span>
4. <span data-ttu-id="a8069-170">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a8069-170">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="a8069-171">Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [WebSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="a8069-171">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [WebSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="a8069-172">Het voorbeeld worden gegevens gekopieerd van een Web-tabel met een Azure-blob elk uur.</span><span class="sxs-lookup"><span data-stu-id="a8069-172">The sample copies data from a Web table to an Azure blob every hour.</span></span> <span data-ttu-id="a8069-173">De JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na de voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="a8069-173">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="a8069-174">Het volgende voorbeeld laat zien hoe gegevens kopiëren van een Web-tabel naar een Azure-blob.</span><span class="sxs-lookup"><span data-stu-id="a8069-174">The following sample shows how to copy data from a Web table to an Azure blob.</span></span> <span data-ttu-id="a8069-175">Echter gegevens kunnen worden gekopieerd naar een van de PUT vermeld in de [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel met behulp van de Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="a8069-175">However, data can be copied directly to any of the sinks stated in the [Data Movement Activities](data-factory-data-movement-activities.md) article by using the Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="a8069-176">**Web service gekoppelde** in dit voorbeeld maakt gebruik van de webservice gekoppeld met anonieme verificatie.</span><span class="sxs-lookup"><span data-stu-id="a8069-176">**Web linked service** This example uses the Web linked service with anonymous authentication.</span></span> <span data-ttu-id="a8069-177">Zie [Web gekoppelde service](#linked-service-properties) sectie voor verschillende soorten verificatie die u kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a8069-177">See [Web linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "WebLinkedService",
    "properties":
    {
        "type": "Web",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "url" : "https://en.wikipedia.org/wiki/"
        }
    }
}
```

<span data-ttu-id="a8069-178">**Een gekoppelde Azure Storage-service**</span><span class="sxs-lookup"><span data-stu-id="a8069-178">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="a8069-179">**WebTable invoergegevensset** instelling **externe** naar **true** informeert de Data Factory-service dat de dataset extern is aan de gegevensfactory en niet wordt geproduceerd door een activiteit in de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="a8069-179">**WebTable input dataset** Setting **external** to **true** informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="a8069-180">Zie [Get-index van een tabel in een HTML-pagina](#get-index-of-a-table-in-an-html-page) sectie voor stappen voor het ophalen van de index van een tabel in een HTML-pagina.</span><span class="sxs-lookup"><span data-stu-id="a8069-180">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps to getting index of a table in an HTML page.</span></span>  
>
>

```json
{
    "name": "WebTableInput",
    "properties": {
        "type": "WebTable",
        "linkedServiceName": "WebLinkedService",
        "typeProperties": {
            "index": 1,
            "path": "AFI's_100_Years...100_Movies"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```


<span data-ttu-id="a8069-181">**Azure Blob-uitvoergegevensset**</span><span class="sxs-lookup"><span data-stu-id="a8069-181">**Azure Blob output dataset**</span></span>

<span data-ttu-id="a8069-182">Gegevens worden geschreven naar een nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="a8069-182">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/Movies"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```



<span data-ttu-id="a8069-183">**Pijplijn met de kopieeractiviteit**</span><span class="sxs-lookup"><span data-stu-id="a8069-183">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="a8069-184">De pijplijn bevat een Kopieeractiviteit die is geconfigureerd voor gebruik van de invoer- en uitvoergegevenssets en elk uur is gepland.</span><span class="sxs-lookup"><span data-stu-id="a8069-184">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="a8069-185">In de pijplijn-JSON-definitie de **bron** type is ingesteld op **WebSource** en **sink** type is ingesteld op **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="a8069-185">In the pipeline JSON definition, the **source** type is set to **WebSource** and **sink** type is set to **BlobSink**.</span></span>

<span data-ttu-id="a8069-186">Zie [WebSource type-eigenschappen](#copy-activity-type-properties) voor de lijst met eigenschappen die door de WebSource ondersteund.</span><span class="sxs-lookup"><span data-stu-id="a8069-186">See [WebSource type properties](#copy-activity-type-properties) for the list of properties supported by the WebSource.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "WebTableToAzureBlob",
        "description": "Copy from a Web table to an Azure blob",
        "type": "Copy",
        "inputs": [
          {
            "name": "WebTableInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "WebSource"
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

## <a name="get-index-of-a-table-in-an-html-page"></a><span data-ttu-id="a8069-187">Ophalen van de index van een tabel in een HTML-pagina</span><span class="sxs-lookup"><span data-stu-id="a8069-187">Get index of a table in an HTML page</span></span>
1. <span data-ttu-id="a8069-188">Start **Excel 2016** en schakel over naar de **gegevens** tabblad.</span><span class="sxs-lookup"><span data-stu-id="a8069-188">Launch **Excel 2016** and switch to the **Data** tab.</span></span>  
2. <span data-ttu-id="a8069-189">Klik op **nieuwe Query** Wijs op de werkbalk **van andere bronnen** en klik op **uit Web**.</span><span class="sxs-lookup"><span data-stu-id="a8069-189">Click **New Query** on the toolbar, point to **From Other Sources** and click **From Web**.</span></span>

    ![Power Query-menu](./media/data-factory-web-table-connector/PowerQuery-Menu.png)
3. <span data-ttu-id="a8069-191">In de **uit Web** dialoogvenster Voer **URL** die u wilt gebruiken in de gekoppelde service JSON (bijvoorbeeld: https://en.wikipedia.org/wiki/) samen met het pad dat u voor de gegevensset opgeven wilt (bijvoorbeeld: AFI % 27s_100_Years... 100_Movies), en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="a8069-191">In the **From Web** dialog box, enter **URL** that you would use in linked service JSON (for example: https://en.wikipedia.org/wiki/) along with path you would specify for the dataset (for example: AFI%27s_100_Years...100_Movies), and click **OK**.</span></span>

    ![Dialoogvenster Web](./media/data-factory-web-table-connector/FromWeb-DialogBox.png)

    <span data-ttu-id="a8069-193">URL die wordt gebruikt in dit voorbeeld: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span><span class="sxs-lookup"><span data-stu-id="a8069-193">URL used in this example: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span></span>
4. <span data-ttu-id="a8069-194">Als u ziet **toegang tot webinhoud** dialoogvenster Selecteer het recht **URL**, **verificatie**, en klik op **Connect**.</span><span class="sxs-lookup"><span data-stu-id="a8069-194">If you see **Access Web content** dialog box, select the right **URL**, **authentication**, and click **Connect**.</span></span>

   ![Dialoogvenster voor toegang tot Web-inhoud](./media/data-factory-web-table-connector/AccessWebContentDialog.png)
5. <span data-ttu-id="a8069-196">Klik op een **tabel** item in de structuurweergave van de inhoud uit de tabel en klik vervolgens op **bewerken** knop onderaan.</span><span class="sxs-lookup"><span data-stu-id="a8069-196">Click a **table** item in the tree view to see content from the table and then click **Edit** button at the bottom.</span></span>  

   ![Dialoogvenster Navigator](./media/data-factory-web-table-connector/Navigator-DialogBox.png)
6. <span data-ttu-id="a8069-198">In de **Query-Editor** venster, klikt u op **geavanceerde Editor** op de werkbalk.</span><span class="sxs-lookup"><span data-stu-id="a8069-198">In the **Query Editor** window, click **Advanced Editor** button on the toolbar.</span></span>

    ![De knop Geavanceerd Editor](./media/data-factory-web-table-connector/QueryEditor-AdvancedEditorButton.png)
7. <span data-ttu-id="a8069-200">Het getal naast 'Bron' is in het dialoogvenster Geavanceerde Editor voor de index.</span><span class="sxs-lookup"><span data-stu-id="a8069-200">In the Advanced Editor dialog box, the number next to "Source" is the index.</span></span>

    ![Geavanceerde Editor - Index](./media/data-factory-web-table-connector/AdvancedEditor-Index.png)

<span data-ttu-id="a8069-202">Als u Excel 2013 gebruikt, gebruikt u [Microsoft Power Query voor Excel](https://www.microsoft.com/download/details.aspx?id=39379) ophalen van de index.</span><span class="sxs-lookup"><span data-stu-id="a8069-202">If you are using Excel 2013, use [Microsoft Power Query for Excel](https://www.microsoft.com/download/details.aspx?id=39379) to get the index.</span></span> <span data-ttu-id="a8069-203">Zie [verbinding maken met een webpagina](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a8069-203">See [Connect to a web page](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) article for details.</span></span> <span data-ttu-id="a8069-204">De stappen zijn vergelijkbaar zijn als u [Microsoft Power BI voor bureaublad](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="a8069-204">The steps are similar if you are using [Microsoft Power BI for Desktop](https://powerbi.microsoft.com/desktop/).</span></span>

> [!NOTE]
> <span data-ttu-id="a8069-205">Zie het toewijzen van kolommen uit de bron-gegevensset naar kolommen uit de dataset sink [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="a8069-205">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="a8069-206">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="a8069-206">Performance and Tuning</span></span>
<span data-ttu-id="a8069-207">Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) voor meer informatie over de belangrijkste factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren om te optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="a8069-207">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
