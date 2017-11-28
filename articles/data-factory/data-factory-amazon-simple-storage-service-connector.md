---
title: aaaMove gegevens vanaf Amazon eenvoudige Storage-Service met behulp van de Data Factory | Microsoft Docs
description: Meer informatie over het toomove gegevens vanaf Amazon eenvoudige Storage-Service (S3) met behulp van Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 636d3179-eba8-4841-bcb4-3563f6822a26
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 8a8cd2845fd1de74413bd0372f3aabfb4817549b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-simple-storage-service-by-using-azure-data-factory"></a><span data-ttu-id="a7de4-103">Gegevens verplaatsen van Amazon eenvoudige Storage-Service met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a7de4-103">Move data from Amazon Simple Storage Service by using Azure Data Factory</span></span>
<span data-ttu-id="a7de4-104">Dit artikel wordt uitgelegd hoe toouse hello kopieeractiviteit in Azure Data Factory toomove gegevens vanaf Amazon eenvoudige Storage-Service (S3).</span><span class="sxs-lookup"><span data-stu-id="a7de4-104">This article explains how toouse hello copy activity in Azure Data Factory toomove data from Amazon Simple Storage Service (S3).</span></span> <span data-ttu-id="a7de4-105">Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.</span><span class="sxs-lookup"><span data-stu-id="a7de4-105">It builds on hello [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="a7de4-106">U kunt gegevens kopiëren van Amazon S3 tooany ondersteund sink-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="a7de4-106">You can copy data from Amazon S3 tooany supported sink data store.</span></span> <span data-ttu-id="a7de4-107">Zie voor een lijst van gegevens winkels ondersteund zoals sinks door kopieeractiviteit hello, Hallo [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel.</span><span class="sxs-lookup"><span data-stu-id="a7de4-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="a7de4-108">Data Factory ondersteunt momenteel alleen zwevend gegevens vanaf Amazon S3 tooother gegevensarchieven, maar tooAmazon S3 niet verplaatsen van gegevens van andere gegevens worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="a7de4-108">Data Factory currently supports only moving data from Amazon S3 tooother data stores, but not moving data from other data stores tooAmazon S3.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="a7de4-109">Vereiste machtigingen</span><span class="sxs-lookup"><span data-stu-id="a7de4-109">Required permissions</span></span>
<span data-ttu-id="a7de4-110">toocopy gegevens vanaf Amazon S3, zorg ervoor dat u de volgende machtigingen Hallo hebt gekregen:</span><span class="sxs-lookup"><span data-stu-id="a7de4-110">toocopy data from Amazon S3, make sure you have been granted hello following permissions:</span></span>

* <span data-ttu-id="a7de4-111">`s3:GetObject`en `s3:GetObjectVersion` voor Amazon S3 Object bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="a7de4-111">`s3:GetObject` and `s3:GetObjectVersion` for Amazon S3 Object Operations.</span></span>
* <span data-ttu-id="a7de4-112">`s3:ListBucket`voor Amazon S3-Bucket bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="a7de4-112">`s3:ListBucket` for Amazon S3 Bucket Operations.</span></span> <span data-ttu-id="a7de4-113">Als u Data Factory-Wizard kopiëren, Hallo `s3:ListAllMyBuckets` is ook vereist.</span><span class="sxs-lookup"><span data-stu-id="a7de4-113">If you are using hello Data Factory Copy Wizard, `s3:ListAllMyBuckets` is also required.</span></span>

<span data-ttu-id="a7de4-114">Zie voor meer informatie over de volledige lijst van Amazon S3 machtigingen Hallo [machtigingen geven in een beleid](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span><span class="sxs-lookup"><span data-stu-id="a7de4-114">For details about hello full list of Amazon S3 permissions, see [Specifying Permissions in a Policy](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span></span>

## <a name="getting-started"></a><span data-ttu-id="a7de4-115">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="a7de4-115">Getting started</span></span>
<span data-ttu-id="a7de4-116">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens worden verplaatst van een bron Amazon S3 met behulp van verschillende hulpprogramma's of API's.</span><span class="sxs-lookup"><span data-stu-id="a7de4-116">You can create a pipeline with a copy activity that moves data from an Amazon S3 source by using different tools or APIs.</span></span>

<span data-ttu-id="a7de4-117">Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="a7de4-117">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="a7de4-118">Zie voor een snel overzicht [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="a7de4-118">For a quick walkthrough, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="a7de4-119">U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="a7de4-119">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="a7de4-120">Zie voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit, Hallo [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="a7de4-120">For step-by-step instructions toocreate a pipeline with a copy activity, see hello [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="a7de4-121">Of u hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="a7de4-121">Whether you use tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="a7de4-122">Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="a7de4-122">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="a7de4-123">Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="a7de4-123">Create **datasets** toorepresent input and output data for hello copy operation.</span></span>
3. <span data-ttu-id="a7de4-124">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="a7de4-124">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="a7de4-125">Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a7de4-125">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="a7de4-126">Wanneer u hulpprogramma's of API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="a7de4-126">When you use tools or APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span> <span data-ttu-id="a7de4-127">Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens van een gegevensarchief Amazon S3 zijn Hallo [JSON-voorbeeld: gegevens kopiëren van Amazon S3 tooAzure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="a7de4-127">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an Amazon S3 data store, see hello [JSON example: Copy data from Amazon S3 tooAzure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="a7de4-128">Zie voor meer informatie over ondersteunde indelingen voor de bestands- en compressie voor een kopieeractiviteit [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="a7de4-128">For details about supported file and compression formats for a copy activity, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="a7de4-129">Hallo volgende secties bevatten informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooAmazon S3 zijn.</span><span class="sxs-lookup"><span data-stu-id="a7de4-129">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAmazon S3.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="a7de4-130">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="a7de4-130">Linked service properties</span></span>
<span data-ttu-id="a7de4-131">Een gekoppelde service een gegevensfactory store tooa gegevens gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="a7de4-131">A linked service links a data store tooa data factory.</span></span> <span data-ttu-id="a7de4-132">Maken van een gekoppelde service van het type **AwsAccessKey** toolink uw gegevensfactory tooyour Amazon S3 gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="a7de4-132">You create a linked service of type **AwsAccessKey** toolink your Amazon S3 data store tooyour data factory.</span></span> <span data-ttu-id="a7de4-133">Hallo volgende tabel biedt een beschrijving op voor JSON-elementen specifieke tooAmazon S3 (AwsAccessKey) gekoppeld-service.</span><span class="sxs-lookup"><span data-stu-id="a7de4-133">hello following table provides description for JSON elements specific tooAmazon S3 (AwsAccessKey) linked service.</span></span>

| <span data-ttu-id="a7de4-134">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="a7de4-134">Property</span></span> | <span data-ttu-id="a7de4-135">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a7de4-135">Description</span></span> | <span data-ttu-id="a7de4-136">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="a7de4-136">Allowed values</span></span> | <span data-ttu-id="a7de4-137">Vereist</span><span class="sxs-lookup"><span data-stu-id="a7de4-137">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a7de4-138">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="a7de4-138">accessKeyID</span></span> |<span data-ttu-id="a7de4-139">ID van de geheime toegangssleutel Hallo.</span><span class="sxs-lookup"><span data-stu-id="a7de4-139">ID of hello secret access key.</span></span> |<span data-ttu-id="a7de4-140">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="a7de4-140">string</span></span> |<span data-ttu-id="a7de4-141">Ja</span><span class="sxs-lookup"><span data-stu-id="a7de4-141">Yes</span></span> |
| <span data-ttu-id="a7de4-142">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="a7de4-142">secretAccessKey</span></span> |<span data-ttu-id="a7de4-143">Hallo geheime toegangssleutel zelf.</span><span class="sxs-lookup"><span data-stu-id="a7de4-143">hello secret access key itself.</span></span> |<span data-ttu-id="a7de4-144">Versleutelde geheime tekenreeks</span><span class="sxs-lookup"><span data-stu-id="a7de4-144">Encrypted secret string</span></span> |<span data-ttu-id="a7de4-145">Ja</span><span class="sxs-lookup"><span data-stu-id="a7de4-145">Yes</span></span> |

<span data-ttu-id="a7de4-146">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a7de4-146">Here is an example:</span></span>

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="a7de4-147">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="a7de4-147">Dataset properties</span></span>
<span data-ttu-id="a7de4-148">een gegevensset toorepresent toospecify invoergegevens in Azure Blob storage, stel de eigenschap Hallo type van de gegevensset Hallo te**AmazonS3**.</span><span class="sxs-lookup"><span data-stu-id="a7de4-148">toospecify a dataset toorepresent input data in Azure Blob storage, set hello type property of hello dataset too**AmazonS3**.</span></span> <span data-ttu-id="a7de4-149">Set Hallo **linkedServiceName** eigenschap van de naam van dataset toohello Hallo Hallo Amazon S3 gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="a7de4-149">Set hello **linkedServiceName** property of hello dataset toohello name of hello Amazon S3 linked service.</span></span> <span data-ttu-id="a7de4-150">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets [gegevenssets maken](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="a7de4-150">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> 

<span data-ttu-id="a7de4-151">Secties zoals structuur, beschikbaarheid en beleid zijn identiek voor alle typen van de gegevensset (zoals SQL-database, blob van Azure en Azure-tabel).</span><span class="sxs-lookup"><span data-stu-id="a7de4-151">Sections such as structure, availability, and policy are similar for all dataset types (such as SQL database, Azure blob, and Azure table).</span></span> <span data-ttu-id="a7de4-152">Hallo **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="a7de4-152">hello **typeProperties** section is different for each type of dataset, and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="a7de4-153">Hallo **typeProperties** sectie voor een gegevensset van het type **AmazonS3** (inclusief Hallo Amazon S3 gegevensset) heeft Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="a7de4-153">hello **typeProperties** section for a dataset of type **AmazonS3** (which includes hello Amazon S3 dataset) has hello following properties:</span></span>

| <span data-ttu-id="a7de4-154">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="a7de4-154">Property</span></span> | <span data-ttu-id="a7de4-155">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a7de4-155">Description</span></span> | <span data-ttu-id="a7de4-156">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="a7de4-156">Allowed values</span></span> | <span data-ttu-id="a7de4-157">Vereist</span><span class="sxs-lookup"><span data-stu-id="a7de4-157">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a7de4-158">bucketName</span><span class="sxs-lookup"><span data-stu-id="a7de4-158">bucketName</span></span> |<span data-ttu-id="a7de4-159">Hallo S3-Bucketnaam.</span><span class="sxs-lookup"><span data-stu-id="a7de4-159">hello S3 bucket name.</span></span> |<span data-ttu-id="a7de4-160">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="a7de4-160">String</span></span> |<span data-ttu-id="a7de4-161">Ja</span><span class="sxs-lookup"><span data-stu-id="a7de4-161">Yes</span></span> |
| <span data-ttu-id="a7de4-162">sleutel</span><span class="sxs-lookup"><span data-stu-id="a7de4-162">key</span></span> |<span data-ttu-id="a7de4-163">Hallo S3 objectsleutel.</span><span class="sxs-lookup"><span data-stu-id="a7de4-163">hello S3 object key.</span></span> |<span data-ttu-id="a7de4-164">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="a7de4-164">String</span></span> |<span data-ttu-id="a7de4-165">Nee</span><span class="sxs-lookup"><span data-stu-id="a7de4-165">No</span></span> |
| <span data-ttu-id="a7de4-166">voorvoegsel</span><span class="sxs-lookup"><span data-stu-id="a7de4-166">prefix</span></span> |<span data-ttu-id="a7de4-167">Voorvoegsel voor Hallo S3 objectsleutel.</span><span class="sxs-lookup"><span data-stu-id="a7de4-167">Prefix for hello S3 object key.</span></span> <span data-ttu-id="a7de4-168">Objecten waarvan sleutels met dit voorvoegsel beginnen worden geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="a7de4-168">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="a7de4-169">Geldt alleen als sleutel is leeg.</span><span class="sxs-lookup"><span data-stu-id="a7de4-169">Applies only when key is empty.</span></span> |<span data-ttu-id="a7de4-170">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="a7de4-170">String</span></span> |<span data-ttu-id="a7de4-171">Nee</span><span class="sxs-lookup"><span data-stu-id="a7de4-171">No</span></span> |
| <span data-ttu-id="a7de4-172">Versie</span><span class="sxs-lookup"><span data-stu-id="a7de4-172">version</span></span> |<span data-ttu-id="a7de4-173">Hallo-versie van Hallo S3-object als S3 versiebeheer is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="a7de4-173">hello version of hello S3 object, if S3 versioning is enabled.</span></span> |<span data-ttu-id="a7de4-174">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="a7de4-174">String</span></span> |<span data-ttu-id="a7de4-175">Nee</span><span class="sxs-lookup"><span data-stu-id="a7de4-175">No</span></span> |
| <span data-ttu-id="a7de4-176">Indeling</span><span class="sxs-lookup"><span data-stu-id="a7de4-176">format</span></span> | <span data-ttu-id="a7de4-177">Hallo na indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="a7de4-177">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="a7de4-178">Set Hallo **type** eigenschap onder indeling tooone van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="a7de4-178">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="a7de4-179">Zie voor meer informatie, Hallo [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [JSON-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren-indeling ](data-factory-supported-file-and-compression-formats.md#parquet-format) secties.</span><span class="sxs-lookup"><span data-stu-id="a7de4-179">For more information, see hello [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="a7de4-180">Als u bestanden als toocopy wilt-tussen bestandsgebaseerde winkels (binaire kopiëren) overslaan Hallo indeling sectie in beide definities invoer en uitvoer gegevensset.</span><span class="sxs-lookup"><span data-stu-id="a7de4-180">If you want toocopy files as-is between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="a7de4-181">Nee</span><span class="sxs-lookup"><span data-stu-id="a7de4-181">No</span></span> | |
| <span data-ttu-id="a7de4-182">Compressie</span><span class="sxs-lookup"><span data-stu-id="a7de4-182">compression</span></span> | <span data-ttu-id="a7de4-183">Hallo-type en compressieniveau voor Hallo gegevens opgeven.</span><span class="sxs-lookup"><span data-stu-id="a7de4-183">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="a7de4-184">Hallo ondersteunde typen zijn: **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="a7de4-184">hello supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="a7de4-185">Hallo ondersteund niveaus zijn: **optimale** en **snelst**.</span><span class="sxs-lookup"><span data-stu-id="a7de4-185">hello supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="a7de4-186">Zie voor meer informatie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="a7de4-186">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="a7de4-187">Nee</span><span class="sxs-lookup"><span data-stu-id="a7de4-187">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="a7de4-188">**bucketName + toets** Hallo-locatie van Hallo S3 object, waarbij bucket Hallo hoofdcontainer voor S3-objecten en sleutel Hallo volledig pad toohello S3-object.</span><span class="sxs-lookup"><span data-stu-id="a7de4-188">**bucketName + key** specifies hello location of hello S3 object, where bucket is hello root container for S3 objects, and key is hello full path toohello S3 object.</span></span>

### <a name="sample-dataset-with-prefix"></a><span data-ttu-id="a7de4-189">Voorbeeldgegevensset met voorvoegsel</span><span class="sxs-lookup"><span data-stu-id="a7de4-189">Sample dataset with prefix</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "testbucket",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
### <a name="sample-dataset-with-version"></a><span data-ttu-id="a7de4-190">Voorbeeldgegevensset (met versie)</span><span class="sxs-lookup"><span data-stu-id="a7de4-190">Sample dataset (with version)</span></span>

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "testbucket",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="dynamic-paths-for-s3"></a><span data-ttu-id="a7de4-191">Dynamische paden voor S3</span><span class="sxs-lookup"><span data-stu-id="a7de4-191">Dynamic paths for S3</span></span>
<span data-ttu-id="a7de4-192">Hallo voorgaande voorbeeld gebruikt vaste waarden voor Hallo **sleutel** en **bucketName** eigenschappen in Hallo Amazon S3-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="a7de4-192">hello preceding sample uses fixed values for hello **key** and **bucketName** properties in hello Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "testbucket",
```

<span data-ttu-id="a7de4-193">U kunt deze eigenschappen tijdens runtime dynamisch berekenen met behulp van systeemvariabelen zoals SliceStart Gegevensfactory hebben.</span><span class="sxs-lookup"><span data-stu-id="a7de4-193">You can have Data Factory calculate these properties dynamically at runtime, by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="a7de4-194">U kunt doen hello dezelfde voor Hallo **voorvoegsel** eigenschap van een gegevensset Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="a7de4-194">You can do hello same for hello **prefix** property of an Amazon S3 dataset.</span></span> <span data-ttu-id="a7de4-195">Zie voor een lijst van ondersteunde functies en variabelen [Data Factory-functies en systeemvariabelen](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="a7de4-195">For a list of supported functions and variables, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="a7de4-196">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="a7de4-196">Copy activity properties</span></span>
<span data-ttu-id="a7de4-197">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van activiteiten [pijplijnen maken](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="a7de4-197">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="a7de4-198">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en beleidsregels zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="a7de4-198">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span> <span data-ttu-id="a7de4-199">Eigenschappen die beschikbaar zijn in Hallo **typeProperties** sectie van de activiteit Hallo variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="a7de4-199">Properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="a7de4-200">Voor de kopieeractiviteit hello afhankelijk eigenschappen van Hallo soorten gegevensbronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="a7de4-200">For hello copy activity, properties vary depending on hello types of sources and sinks.</span></span> <span data-ttu-id="a7de4-201">Wanneer een bron in de kopieerbewerking Hallo is van het type **FileSystemSource** (waaronder Amazon S3), Hallo eigenschap na is beschikbaar in **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="a7de4-201">When a source in hello copy activity is of type **FileSystemSource** (which includes Amazon S3), hello following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="a7de4-202">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="a7de4-202">Property</span></span> | <span data-ttu-id="a7de4-203">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a7de4-203">Description</span></span> | <span data-ttu-id="a7de4-204">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="a7de4-204">Allowed values</span></span> | <span data-ttu-id="a7de4-205">Vereist</span><span class="sxs-lookup"><span data-stu-id="a7de4-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a7de4-206">Recursieve</span><span class="sxs-lookup"><span data-stu-id="a7de4-206">recursive</span></span> |<span data-ttu-id="a7de4-207">Hiermee geeft u op of toorecursively lijst S3 onder Hallo directory-objecten.</span><span class="sxs-lookup"><span data-stu-id="a7de4-207">Specifies whether toorecursively list S3 objects under hello directory.</span></span> |<span data-ttu-id="a7de4-208">waar/onwaar</span><span class="sxs-lookup"><span data-stu-id="a7de4-208">true/false</span></span> |<span data-ttu-id="a7de4-209">Nee</span><span class="sxs-lookup"><span data-stu-id="a7de4-209">No</span></span> |

## <a name="json-example-copy-data-from-amazon-s3-tooazure-blob-storage"></a><span data-ttu-id="a7de4-210">JSON-voorbeeld: gegevens kopiëren van Amazon S3 tooAzure Blob-opslag</span><span class="sxs-lookup"><span data-stu-id="a7de4-210">JSON example: Copy data from Amazon S3 tooAzure Blob storage</span></span>
<span data-ttu-id="a7de4-211">In dit voorbeeld laat zien hoe toocopy gegevens vanaf Amazon S3 tooan Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="a7de4-211">This sample shows how toocopy data from Amazon S3 tooan Azure Blob storage.</span></span> <span data-ttu-id="a7de4-212">Echter gegevens kunnen worden gekopieerd rechtstreeks te[van Hallo put die worden ondersteund](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van de kopieeractiviteit Hallo in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="a7de4-212">However, data can be copied directly too[any of hello sinks that are supported](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using hello copy activity in Data Factory.</span></span>

<span data-ttu-id="a7de4-213">Hallo-voorbeeld bevat JSON-definities voor Hallo Data Factory-entiteiten te volgen.</span><span class="sxs-lookup"><span data-stu-id="a7de4-213">hello sample provides JSON definitions for hello following Data Factory entities.</span></span> <span data-ttu-id="a7de4-214">U kunt deze definities toocreate een pijplijn toocopy gegevens vanaf Amazon S3 tooBlob opslag, met behulp van Hallo [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), of [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a7de4-214">You can use these definitions toocreate a pipeline toocopy data from Amazon S3 tooBlob storage, by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>   

* <span data-ttu-id="a7de4-215">Een gekoppelde service van het type [AwsAccessKey](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a7de4-215">A linked service of type [AwsAccessKey](#linked-service-properties).</span></span>
* <span data-ttu-id="a7de4-216">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a7de4-216">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="a7de4-217">Invoer [gegevensset](data-factory-create-datasets.md) van het type [AmazonS3](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a7de4-217">An input [dataset](data-factory-create-datasets.md) of type [AmazonS3](#dataset-properties).</span></span>
* <span data-ttu-id="a7de4-218">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a7de4-218">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="a7de4-219">Een [pijplijn](data-factory-create-pipelines.md) met de kopieeractiviteit die gebruikmaakt van [FileSystemSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="a7de4-219">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="a7de4-220">Hallo voorbeeld kopieert gegevens van Amazon S3 tooan Azure blob elk uur.</span><span class="sxs-lookup"><span data-stu-id="a7de4-220">hello sample copies data from Amazon S3 tooan Azure blob every hour.</span></span> <span data-ttu-id="a7de4-221">Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="a7de4-221">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

### <a name="amazon-s3-linked-service"></a><span data-ttu-id="a7de4-222">Amazon S3 gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="a7de4-222">Amazon S3 linked service</span></span>

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="a7de4-223">Een gekoppelde Azure Storage-service</span><span class="sxs-lookup"><span data-stu-id="a7de4-223">Azure Storage linked service</span></span>

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

### <a name="amazon-s3-input-dataset"></a><span data-ttu-id="a7de4-224">Invoergegevensset Amazon S3</span><span class="sxs-lookup"><span data-stu-id="a7de4-224">Amazon S3 input dataset</span></span>

<span data-ttu-id="a7de4-225">Instelling **'extern': true** informeert Hallo Data Factory-service die gegevensset Hallo externe toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="a7de4-225">Setting **"external": true** informs hello Data Factory service that hello dataset is external toohello data factory.</span></span> <span data-ttu-id="a7de4-226">Deze eigenschap tootrue niet instellen op een invoergegevensset dat niet door een activiteit in de pijplijn hello wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="a7de4-226">Set this property tootrue on an input dataset that is not produced by an activity in hello pipeline.</span></span>

```json
    {
        "name": "AmazonS3InputDataset",
        "properties": {
            "type": "AmazonS3",
            "linkedServiceName": "AmazonS3LinkedService",
            "typeProperties": {
                "key": "testFolder/test.orc",
                "bucketName": "testbucket",
                "format": {
                    "type": "OrcFormat"
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "external": true
        }
    }
```


### <a name="azure-blob-output-dataset"></a><span data-ttu-id="a7de4-227">Azure Blob-uitvoergegevensset</span><span class="sxs-lookup"><span data-stu-id="a7de4-227">Azure Blob output dataset</span></span>

<span data-ttu-id="a7de4-228">Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="a7de4-228">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="a7de4-229">pad naar map voor blob Hallo Hallo wordt dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="a7de4-229">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="a7de4-230">mappad Hallo Hallo jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a7de4-230">hello folder path uses hello year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazons3/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="copy-activity-in-a-pipeline-with-an-amazon-s3-source-and-a-blob-sink"></a><span data-ttu-id="a7de4-231">De kopieeractiviteit in een pijplijn met een bron Amazon S3 en een blob-sink</span><span class="sxs-lookup"><span data-stu-id="a7de4-231">Copy activity in a pipeline with an Amazon S3 source and a blob sink</span></span>

<span data-ttu-id="a7de4-232">Hallo pijplijn bevat een kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur.</span><span class="sxs-lookup"><span data-stu-id="a7de4-232">hello pipeline contains a copy activity that is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="a7de4-233">Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**FileSystemSource**, en **sink** type is ingesteld, te**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="a7de4-233">In hello pipeline JSON definition, hello **source** type is set too**FileSystemSource**, and **sink** type is set too**BlobSink**.</span></span>

```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "FileSystemSource",
                        "recursive": true
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonS3InputDataset"
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
                "name": "AmazonS3ToBlob"
            }
        ],
        "start": "2014-08-08T18:00:00Z",
        "end": "2014-08-08T19:00:00Z"
    }
}
```
> [!NOTE]
> <span data-ttu-id="a7de4-234">Zie toomap kolommen uit een toocolumns bron gegevensset uit een gegevensset sink [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="a7de4-234">toomap columns from a source dataset toocolumns from a sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="a7de4-235">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a7de4-235">Next steps</span></span>
<span data-ttu-id="a7de4-236">Zie Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="a7de4-236">See hello following articles:</span></span>

* <span data-ttu-id="a7de4-237">toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (kopieeractiviteit) in Gegevensfactory en verschillende manieren toooptimize, Zie Hallo [activiteit prestaties en prestatieafstemming handleiding kopiëren](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="a7de4-237">toolearn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways toooptimize it, see hello [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="a7de4-238">Zie voor stapsgewijze instructies voor het maken van een pijplijn met een kopieeractiviteit hello [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="a7de4-238">For step-by-step instructions for creating a pipeline with a copy activity, see hello [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
