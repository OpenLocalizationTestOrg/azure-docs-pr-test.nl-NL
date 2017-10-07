---
title: aaaMove gegevens van Web-tabel met behulp van Azure Data Factory | Microsoft Docs
description: Meer informatie over hoe toomove gegevens uit een tabel in een Web-pagina met behulp van Azure Data Factory.
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
ms.openlocfilehash: e52216305583ebbe71ed896522f361bb22f01278
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-web-table-source-using-azure-data-factory"></a><span data-ttu-id="32ac9-103">Verplaatsen van gegevens uit een tabel Webbron met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="32ac9-103">Move data from a Web table source using Azure Data Factory</span></span>
<span data-ttu-id="32ac9-104">In dit artikel bevat een overzicht van hoe toouse hello Kopieeractiviteit in Azure Data Factory toomove gegevens uit een tabel in een webpagina tooa gegevensarchief sink ondersteund.</span><span class="sxs-lookup"><span data-stu-id="32ac9-104">This article outlines how toouse hello Copy Activity in Azure Data Factory toomove data from a table in a Web page tooa supported sink data store.</span></span> <span data-ttu-id="32ac9-105">In dit artikel is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel met daarin een algemeen overzicht van de verplaatsing van gegevens kopiëren-activiteit en Hallo lijst met gegevensarchieven ondersteund als bronnen/Put.</span><span class="sxs-lookup"><span data-stu-id="32ac9-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article that presents a general overview of data movement with copy activity and hello list of data stores supported as sources/sinks.</span></span>

<span data-ttu-id="32ac9-106">Data factory ondersteunt momenteel alleen zwevend gegevens van een Web-tabelgegevens tooother wordt opgeslagen, maar niet verplaatsen van gegevens van andere gegevens worden opgeslagen tooa Web tabel bestemming.</span><span class="sxs-lookup"><span data-stu-id="32ac9-106">Data factory currently supports only moving data from a Web table tooother data stores, but not moving data from other data stores tooa Web table destination.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="32ac9-107">Deze Web-connector ondersteunt momenteel alleen uitpakken tabelinhoud uit een HTML-pagina.</span><span class="sxs-lookup"><span data-stu-id="32ac9-107">This Web connector currently supports only extracting table content from an HTML page.</span></span> <span data-ttu-id="32ac9-108">tooretrieve gegevens van een HTTP/s-eindpunt gebruik [HTTP connector](data-factory-http-connector.md) in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="32ac9-108">tooretrieve data from a HTTP/s endpoint, use [HTTP connector](data-factory-http-connector.md) instead.</span></span>

## <a name="getting-started"></a><span data-ttu-id="32ac9-109">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="32ac9-109">Getting started</span></span>
<span data-ttu-id="32ac9-110">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens vanuit een on-premises Cassandra-gegevensopslag verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="32ac9-110">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="32ac9-111">Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="32ac9-111">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="32ac9-112">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="32ac9-112">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="32ac9-113">U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="32ac9-113">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="32ac9-114">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="32ac9-114">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="32ac9-115">Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="32ac9-115">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="32ac9-116">Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="32ac9-116">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="32ac9-117">Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="32ac9-117">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="32ac9-118">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="32ac9-118">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="32ac9-119">Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="32ac9-119">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="32ac9-120">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="32ac9-120">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="32ac9-121">Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens uit een tabel web zijn [JSON-voorbeeld: gegevens kopiëren van Web tabel tooAzure Blob](#json-example-copy-data-from-web-table-to-azure-blob) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="32ac9-121">For a sample with JSON definitions for Data Factory entities that are used toocopy data from a web table, see [JSON example: Copy data from Web table tooAzure Blob](#json-example-copy-data-from-web-table-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="32ac9-122">Hallo volgende secties vindt u informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooa Web tabel zijn:</span><span class="sxs-lookup"><span data-stu-id="32ac9-122">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Web table:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="32ac9-123">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="32ac9-123">Linked service properties</span></span>
<span data-ttu-id="32ac9-124">Hallo volgende tabel biedt een beschrijving voor de JSON-elementen specifieke tooWeb gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="32ac9-124">hello following table provides description for JSON elements specific tooWeb linked service.</span></span>

| <span data-ttu-id="32ac9-125">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="32ac9-125">Property</span></span> | <span data-ttu-id="32ac9-126">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="32ac9-126">Description</span></span> | <span data-ttu-id="32ac9-127">Vereist</span><span class="sxs-lookup"><span data-stu-id="32ac9-127">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="32ac9-128">type</span><span class="sxs-lookup"><span data-stu-id="32ac9-128">type</span></span> |<span data-ttu-id="32ac9-129">Hallo type eigenschap moet worden ingesteld op: **Web**</span><span class="sxs-lookup"><span data-stu-id="32ac9-129">hello type property must be set to: **Web**</span></span> |<span data-ttu-id="32ac9-130">Ja</span><span class="sxs-lookup"><span data-stu-id="32ac9-130">Yes</span></span> |
| <span data-ttu-id="32ac9-131">URL</span><span class="sxs-lookup"><span data-stu-id="32ac9-131">Url</span></span> |<span data-ttu-id="32ac9-132">URL toohello webbron</span><span class="sxs-lookup"><span data-stu-id="32ac9-132">URL toohello Web source</span></span> |<span data-ttu-id="32ac9-133">Ja</span><span class="sxs-lookup"><span data-stu-id="32ac9-133">Yes</span></span> |
| <span data-ttu-id="32ac9-134">authenticationType</span><span class="sxs-lookup"><span data-stu-id="32ac9-134">authenticationType</span></span> |<span data-ttu-id="32ac9-135">Anonieme.</span><span class="sxs-lookup"><span data-stu-id="32ac9-135">Anonymous.</span></span> |<span data-ttu-id="32ac9-136">Ja</span><span class="sxs-lookup"><span data-stu-id="32ac9-136">Yes</span></span> |

### <a name="using-anonymous-authentication"></a><span data-ttu-id="32ac9-137">Anonieme verificatie</span><span class="sxs-lookup"><span data-stu-id="32ac9-137">Using Anonymous authentication</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="32ac9-138">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="32ac9-138">Dataset properties</span></span>
<span data-ttu-id="32ac9-139">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="32ac9-139">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="32ac9-140">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).</span><span class="sxs-lookup"><span data-stu-id="32ac9-140">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="32ac9-141">Hallo **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="32ac9-141">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="32ac9-142">Hallo typeProperties sectie voor de gegevensset van het type **WebTable** heeft de volgende eigenschappen Hallo</span><span class="sxs-lookup"><span data-stu-id="32ac9-142">hello typeProperties section for dataset of type **WebTable** has hello following properties</span></span>

| <span data-ttu-id="32ac9-143">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="32ac9-143">Property</span></span> | <span data-ttu-id="32ac9-144">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="32ac9-144">Description</span></span> | <span data-ttu-id="32ac9-145">Vereist</span><span class="sxs-lookup"><span data-stu-id="32ac9-145">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="32ac9-146">type</span><span class="sxs-lookup"><span data-stu-id="32ac9-146">type</span></span> |<span data-ttu-id="32ac9-147">Type Hallo gegevensset.</span><span class="sxs-lookup"><span data-stu-id="32ac9-147">type of hello dataset.</span></span> <span data-ttu-id="32ac9-148">te moet worden ingesteld**WebTable**</span><span class="sxs-lookup"><span data-stu-id="32ac9-148">must be set too**WebTable**</span></span> |<span data-ttu-id="32ac9-149">Ja</span><span class="sxs-lookup"><span data-stu-id="32ac9-149">Yes</span></span> |
| <span data-ttu-id="32ac9-150">Pad</span><span class="sxs-lookup"><span data-stu-id="32ac9-150">path</span></span> |<span data-ttu-id="32ac9-151">Een relatieve URL toohello-bron die Hallo tabel bevat.</span><span class="sxs-lookup"><span data-stu-id="32ac9-151">A relative URL toohello resource that contains hello table.</span></span> |<span data-ttu-id="32ac9-152">Nee.</span><span class="sxs-lookup"><span data-stu-id="32ac9-152">No.</span></span> <span data-ttu-id="32ac9-153">Wanneer het pad niet wordt opgegeven, wordt alleen Hallo URL die is opgegeven in de servicedefinitie Hallo gekoppeld gebruikt.</span><span class="sxs-lookup"><span data-stu-id="32ac9-153">When path is not specified, only hello URL specified in hello linked service definition is used.</span></span> |
| <span data-ttu-id="32ac9-154">Index</span><span class="sxs-lookup"><span data-stu-id="32ac9-154">index</span></span> |<span data-ttu-id="32ac9-155">Hallo index van de tabel Hallo in Hallo resource.</span><span class="sxs-lookup"><span data-stu-id="32ac9-155">hello index of hello table in hello resource.</span></span> <span data-ttu-id="32ac9-156">Zie [Get-index van een tabel in een HTML-pagina](#get-index-of-a-table-in-an-html-page) sectie voor stappen toogetting index van een tabel in een HTML-pagina.</span><span class="sxs-lookup"><span data-stu-id="32ac9-156">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps toogetting index of a table in an HTML page.</span></span> |<span data-ttu-id="32ac9-157">Ja</span><span class="sxs-lookup"><span data-stu-id="32ac9-157">Yes</span></span> |

<span data-ttu-id="32ac9-158">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="32ac9-158">**Example:**</span></span>

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

## <a name="copy-activity-properties"></a><span data-ttu-id="32ac9-159">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="32ac9-159">Copy activity properties</span></span>
<span data-ttu-id="32ac9-160">Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="32ac9-160">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="32ac9-161">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en -beleid zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="32ac9-161">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="32ac9-162">Terwijl de eigenschappen die beschikbaar zijn in Hallo typeProperties gedeelte van de activiteit Hallo variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="32ac9-162">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="32ac9-163">Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="32ac9-163">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="32ac9-164">Op dit moment wanneer Hallo-bron in de kopieerbewerking is van het type **WebSource**, zonder aanvullende eigenschappen worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="32ac9-164">Currently, when hello source in copy activity is of type **WebSource**, no additional properties are supported.</span></span>


## <a name="json-example-copy-data-from-web-table-tooazure-blob"></a><span data-ttu-id="32ac9-165">JSON-voorbeeld: gegevens kopiëren van Web tabel tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="32ac9-165">JSON example: Copy data from Web table tooAzure Blob</span></span>
<span data-ttu-id="32ac9-166">Hallo volgende ziet:</span><span class="sxs-lookup"><span data-stu-id="32ac9-166">hello following sample shows:</span></span>

1. <span data-ttu-id="32ac9-167">Een gekoppelde service van het type [Web](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="32ac9-167">A linked service of type [Web](#linked-service-properties).</span></span>
2. <span data-ttu-id="32ac9-168">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="32ac9-168">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="32ac9-169">Invoer [gegevensset](data-factory-create-datasets.md) van het type [WebTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="32ac9-169">An input [dataset](data-factory-create-datasets.md) of type [WebTable](#dataset-properties).</span></span>
4. <span data-ttu-id="32ac9-170">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="32ac9-170">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="32ac9-171">Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [WebSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="32ac9-171">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [WebSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="32ac9-172">Hallo-voorbeeld worden gegevens gekopieerd van een Web tabel tooan Azure blob elk uur.</span><span class="sxs-lookup"><span data-stu-id="32ac9-172">hello sample copies data from a Web table tooan Azure blob every hour.</span></span> <span data-ttu-id="32ac9-173">Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="32ac9-173">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="32ac9-174">Hallo volgende voorbeeld ziet u hoe toocopy gegevens van een Web tabel tooan Azure-blob.</span><span class="sxs-lookup"><span data-stu-id="32ac9-174">hello following sample shows how toocopy data from a Web table tooan Azure blob.</span></span> <span data-ttu-id="32ac9-175">Echter gegevens kunnen worden gekopieerd direct tooany Hallo sinks vermelde in Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel met behulp van Hallo Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="32ac9-175">However, data can be copied directly tooany of hello sinks stated in hello [Data Movement Activities](data-factory-data-movement-activities.md) article by using hello Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="32ac9-176">**Web service gekoppelde** in dit voorbeeld gebruikt Hallo Web gekoppelde service met anonieme verificatie.</span><span class="sxs-lookup"><span data-stu-id="32ac9-176">**Web linked service** This example uses hello Web linked service with anonymous authentication.</span></span> <span data-ttu-id="32ac9-177">Zie [Web gekoppelde service](#linked-service-properties) sectie voor verschillende soorten verificatie die u kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="32ac9-177">See [Web linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

<span data-ttu-id="32ac9-178">**Een gekoppelde Azure Storage-service**</span><span class="sxs-lookup"><span data-stu-id="32ac9-178">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="32ac9-179">**WebTable invoergegevensset** instelling **externe** te**true** Hallo Data Factory-service te informeren dat gegevensset Hallo externe toohello data factory is en niet wordt geproduceerd door een activiteit in Hallo Data factory.</span><span class="sxs-lookup"><span data-stu-id="32ac9-179">**WebTable input dataset** Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

> [!NOTE]
> <span data-ttu-id="32ac9-180">Zie [Get-index van een tabel in een HTML-pagina](#get-index-of-a-table-in-an-html-page) sectie voor stappen toogetting index van een tabel in een HTML-pagina.</span><span class="sxs-lookup"><span data-stu-id="32ac9-180">See [Get index of a table in an HTML page](#get-index-of-a-table-in-an-html-page) section for steps toogetting index of a table in an HTML page.</span></span>  
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


<span data-ttu-id="32ac9-181">**Azure Blob-uitvoergegevensset**</span><span class="sxs-lookup"><span data-stu-id="32ac9-181">**Azure Blob output dataset**</span></span>

<span data-ttu-id="32ac9-182">Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="32ac9-182">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

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



<span data-ttu-id="32ac9-183">**Pijplijn met de kopieeractiviteit**</span><span class="sxs-lookup"><span data-stu-id="32ac9-183">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="32ac9-184">Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur.</span><span class="sxs-lookup"><span data-stu-id="32ac9-184">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="32ac9-185">Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**WebSource** en **sink** type is ingesteld, te**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="32ac9-185">In hello pipeline JSON definition, hello **source** type is set too**WebSource** and **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="32ac9-186">Zie [WebSource type-eigenschappen](#copy-activity-type-properties) voor Hallo lijst met eigenschappen die ondersteund worden door Hallo WebSource.</span><span class="sxs-lookup"><span data-stu-id="32ac9-186">See [WebSource type properties](#copy-activity-type-properties) for hello list of properties supported by hello WebSource.</span></span>

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
        "description": "Copy from a Web table tooan Azure blob",
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

## <a name="get-index-of-a-table-in-an-html-page"></a><span data-ttu-id="32ac9-187">Ophalen van de index van een tabel in een HTML-pagina</span><span class="sxs-lookup"><span data-stu-id="32ac9-187">Get index of a table in an HTML page</span></span>
1. <span data-ttu-id="32ac9-188">Start **Excel 2016** en switch toohello **gegevens** tabblad.</span><span class="sxs-lookup"><span data-stu-id="32ac9-188">Launch **Excel 2016** and switch toohello **Data** tab.</span></span>  
2. <span data-ttu-id="32ac9-189">Klik op **nieuwe Query** op Hallo werkbalk wijst te**van andere bronnen** en klik op **uit Web**.</span><span class="sxs-lookup"><span data-stu-id="32ac9-189">Click **New Query** on hello toolbar, point too**From Other Sources** and click **From Web**.</span></span>

    ![Power Query-menu](./media/data-factory-web-table-connector/PowerQuery-Menu.png)
3. <span data-ttu-id="32ac9-191">In Hallo **uit Web** dialoogvenster Voer **URL** die u wilt gebruiken in de gekoppelde service JSON (bijvoorbeeld: https://en.wikipedia.org/wiki/) samen met u voor de gegevensset Hallo geeft pad (bijvoorbeeld: AFI % 27s_100_Years... 100_Movies), en klik op **OK**.</span><span class="sxs-lookup"><span data-stu-id="32ac9-191">In hello **From Web** dialog box, enter **URL** that you would use in linked service JSON (for example: https://en.wikipedia.org/wiki/) along with path you would specify for hello dataset (for example: AFI%27s_100_Years...100_Movies), and click **OK**.</span></span>

    ![Dialoogvenster Web](./media/data-factory-web-table-connector/FromWeb-DialogBox.png)

    <span data-ttu-id="32ac9-193">URL die wordt gebruikt in dit voorbeeld: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span><span class="sxs-lookup"><span data-stu-id="32ac9-193">URL used in this example: https://en.wikipedia.org/wiki/AFI%27s_100_Years...100_Movies</span></span>
4. <span data-ttu-id="32ac9-194">Als u ziet **toegang tot webinhoud** in het dialoogvenster, selecteer Hallo rechts **URL**, **verificatie**, en klik op **Connect**.</span><span class="sxs-lookup"><span data-stu-id="32ac9-194">If you see **Access Web content** dialog box, select hello right **URL**, **authentication**, and click **Connect**.</span></span>

   ![Dialoogvenster voor toegang tot Web-inhoud](./media/data-factory-web-table-connector/AccessWebContentDialog.png)
5. <span data-ttu-id="32ac9-196">Klik op een **tabel** in Hallo structuur weergave toosee inhoud uit de tabel Hallo-item en klik vervolgens op **bewerken** knop Hallo onder aan.</span><span class="sxs-lookup"><span data-stu-id="32ac9-196">Click a **table** item in hello tree view toosee content from hello table and then click **Edit** button at hello bottom.</span></span>  

   ![Dialoogvenster Navigator](./media/data-factory-web-table-connector/Navigator-DialogBox.png)
6. <span data-ttu-id="32ac9-198">In Hallo **Query-Editor** venster, klikt u op **geavanceerde Editor** op de werkbalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="32ac9-198">In hello **Query Editor** window, click **Advanced Editor** button on hello toolbar.</span></span>

    ![De knop Geavanceerd Editor](./media/data-factory-web-table-connector/QueryEditor-AdvancedEditorButton.png)
7. <span data-ttu-id="32ac9-200">Hallo Hallo geavanceerde Editor in het dialoogvenster getal naast te 'Bron' hello index is.</span><span class="sxs-lookup"><span data-stu-id="32ac9-200">In hello Advanced Editor dialog box, hello number next too"Source" is hello index.</span></span>

    ![Geavanceerde Editor - Index](./media/data-factory-web-table-connector/AdvancedEditor-Index.png)

<span data-ttu-id="32ac9-202">Als u Excel 2013 gebruikt, gebruikt u [Microsoft Power Query voor Excel](https://www.microsoft.com/download/details.aspx?id=39379) tooget Hallo index.</span><span class="sxs-lookup"><span data-stu-id="32ac9-202">If you are using Excel 2013, use [Microsoft Power Query for Excel](https://www.microsoft.com/download/details.aspx?id=39379) tooget hello index.</span></span> <span data-ttu-id="32ac9-203">Zie [Connect tooa webpagina](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="32ac9-203">See [Connect tooa web page](https://support.office.com/article/Connect-to-a-web-page-Power-Query-b2725d67-c9e8-43e6-a590-c0a175bd64d8) article for details.</span></span> <span data-ttu-id="32ac9-204">Hallo stappen zijn vergelijkbaar zijn als u [Microsoft Power BI voor bureaublad](https://powerbi.microsoft.com/desktop/).</span><span class="sxs-lookup"><span data-stu-id="32ac9-204">hello steps are similar if you are using [Microsoft Power BI for Desktop](https://powerbi.microsoft.com/desktop/).</span></span>

> [!NOTE]
> <span data-ttu-id="32ac9-205">toomap kolommen uit de bron gegevensset toocolumns uit sink gegevensset, Zie [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="32ac9-205">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="32ac9-206">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="32ac9-206">Performance and Tuning</span></span>
<span data-ttu-id="32ac9-207">Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.</span><span class="sxs-lookup"><span data-stu-id="32ac9-207">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
