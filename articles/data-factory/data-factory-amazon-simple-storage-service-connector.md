---
title: Gegevens verplaatsen van Amazon eenvoudige Storage-Service met behulp van de Data Factory | Microsoft Docs
description: Meer informatie over het verplaatsen van gegevens vanaf Amazon eenvoudige Storage-Service (S3) met behulp van Azure Data Factory.
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
ms.openlocfilehash: 3e21f7dfccc3b235071344a28c7d94f65e6bf9ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-amazon-simple-storage-service-by-using-azure-data-factory"></a><span data-ttu-id="de4ae-103">Gegevens verplaatsen van Amazon eenvoudige Storage-Service met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="de4ae-103">Move data from Amazon Simple Storage Service by using Azure Data Factory</span></span>
<span data-ttu-id="de4ae-104">In dit artikel wordt uitgelegd hoe de kopieeractiviteit in Azure Data Factory om gegevens te verplaatsen van Amazon eenvoudige Storage-Service (S3) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="de4ae-104">This article explains how to use the copy activity in Azure Data Factory to move data from Amazon Simple Storage Service (S3).</span></span> <span data-ttu-id="de4ae-105">Dit is gebaseerd op de [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, hetgeen een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit toont.</span><span class="sxs-lookup"><span data-stu-id="de4ae-105">It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="de4ae-106">U kunt gegevens vanaf Amazon S3 kopiëren naar een ondersteunde sink-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="de4ae-106">You can copy data from Amazon S3 to any supported sink data store.</span></span> <span data-ttu-id="de4ae-107">Zie voor een lijst met gegevensarchieven als PUT wordt ondersteund door de kopieeractiviteit, de [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel.</span><span class="sxs-lookup"><span data-stu-id="de4ae-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="de4ae-108">Data Factory ondersteunt momenteel alleen zwevend gegevens vanaf Amazon S3 naar andere gegevensarchieven, maar niet verplaatsen van gegevens van andere gegevens worden opgeslagen op de Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="de4ae-108">Data Factory currently supports only moving data from Amazon S3 to other data stores, but not moving data from other data stores to Amazon S3.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="de4ae-109">Vereiste machtigingen</span><span class="sxs-lookup"><span data-stu-id="de4ae-109">Required permissions</span></span>
<span data-ttu-id="de4ae-110">Als u wilt kopiëren van gegevens vanaf Amazon S3, moet dat u de volgende machtigingen hebben gekregen:</span><span class="sxs-lookup"><span data-stu-id="de4ae-110">To copy data from Amazon S3, make sure you have been granted the following permissions:</span></span>

* <span data-ttu-id="de4ae-111">`s3:GetObject`en `s3:GetObjectVersion` voor Amazon S3 Object bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="de4ae-111">`s3:GetObject` and `s3:GetObjectVersion` for Amazon S3 Object Operations.</span></span>
* <span data-ttu-id="de4ae-112">`s3:ListBucket`voor Amazon S3-Bucket bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="de4ae-112">`s3:ListBucket` for Amazon S3 Bucket Operations.</span></span> <span data-ttu-id="de4ae-113">Als u de Data Factory-Wizard kopiëren, `s3:ListAllMyBuckets` is ook vereist.</span><span class="sxs-lookup"><span data-stu-id="de4ae-113">If you are using the Data Factory Copy Wizard, `s3:ListAllMyBuckets` is also required.</span></span>

<span data-ttu-id="de4ae-114">Zie voor meer informatie over de volledige lijst met machtigingen voor Amazon S3 [machtigingen geven in een beleid](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span><span class="sxs-lookup"><span data-stu-id="de4ae-114">For details about the full list of Amazon S3 permissions, see [Specifying Permissions in a Policy](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).</span></span>

## <a name="getting-started"></a><span data-ttu-id="de4ae-115">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="de4ae-115">Getting started</span></span>
<span data-ttu-id="de4ae-116">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens worden verplaatst van een bron Amazon S3 met behulp van verschillende hulpprogramma's of API's.</span><span class="sxs-lookup"><span data-stu-id="de4ae-116">You can create a pipeline with a copy activity that moves data from an Amazon S3 source by using different tools or APIs.</span></span>

<span data-ttu-id="de4ae-117">De eenvoudigste manier om een pijplijn maken is met de **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="de4ae-117">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="de4ae-118">Zie voor een snel overzicht [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="de4ae-118">For a quick walkthrough, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="de4ae-119">U kunt ook de volgende hulpprogramma's gebruiken voor het maken van een pijplijn: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon**, **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="de4ae-119">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="de4ae-120">Zie voor stapsgewijze instructies voor het maken van een pijplijn met een kopieeractiviteit de [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="de4ae-120">For step-by-step instructions to create a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>

<span data-ttu-id="de4ae-121">Of u hulpprogramma's of API's gebruiken, moet u de volgende stappen voor het maken van een pijplijn die de gegevens vanuit een brongegevensarchief naar een gegevensarchief sink verplaatst uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="de4ae-121">Whether you use tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="de4ae-122">Maak **gekoppelde services** slaat om invoer- en gegevens te koppelen aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="de4ae-122">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="de4ae-123">Maak **gegevenssets** vertegenwoordigt de invoer- en -gegevens voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="de4ae-123">Create **datasets** to represent input and output data for the copy operation.</span></span>
3. <span data-ttu-id="de4ae-124">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="de4ae-124">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span>

<span data-ttu-id="de4ae-125">Wanneer u de wizard gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="de4ae-125">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="de4ae-126">Wanneer u hulpprogramma's of API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van de JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="de4ae-126">When you use tools or APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span> <span data-ttu-id="de4ae-127">Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die worden gebruikt om gegevens te kopiëren uit een gegevensopslag Amazon S3, de [JSON-voorbeeld: gegevens kopiëren van Amazon S3 naar Azure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="de4ae-127">For a sample with JSON definitions for Data Factory entities that are used to copy data from an Amazon S3 data store, see the [JSON example: Copy data from Amazon S3 to Azure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) section of this article.</span></span>

> [!NOTE]
> <span data-ttu-id="de4ae-128">Zie voor meer informatie over ondersteunde indelingen voor de bestands- en compressie voor een kopieeractiviteit [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span><span class="sxs-lookup"><span data-stu-id="de4ae-128">For details about supported file and compression formats for a copy activity, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md).</span></span>

<span data-ttu-id="de4ae-129">De volgende secties bevatten informatie over de JSON-eigenschappen die worden gebruikt voor het definiëren van Data Factory-entiteiten specifieke naar Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="de4ae-129">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Amazon S3.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="de4ae-130">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="de4ae-130">Linked service properties</span></span>
<span data-ttu-id="de4ae-131">Een gekoppelde service gegevensopslag is gekoppeld aan een gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="de4ae-131">A linked service links a data store to a data factory.</span></span> <span data-ttu-id="de4ae-132">Maken van een gekoppelde service van het type **AwsAccessKey** uw Amazon S3 data store koppelen aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="de4ae-132">You create a linked service of type **AwsAccessKey** to link your Amazon S3 data store to your data factory.</span></span> <span data-ttu-id="de4ae-133">De volgende tabel bevat een beschrijving voor JSON-elementen die specifiek zijn voor Amazon S3 (AwsAccessKey) gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="de4ae-133">The following table provides description for JSON elements specific to Amazon S3 (AwsAccessKey) linked service.</span></span>

| <span data-ttu-id="de4ae-134">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="de4ae-134">Property</span></span> | <span data-ttu-id="de4ae-135">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="de4ae-135">Description</span></span> | <span data-ttu-id="de4ae-136">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="de4ae-136">Allowed values</span></span> | <span data-ttu-id="de4ae-137">Vereist</span><span class="sxs-lookup"><span data-stu-id="de4ae-137">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="de4ae-138">accessKeyID</span><span class="sxs-lookup"><span data-stu-id="de4ae-138">accessKeyID</span></span> |<span data-ttu-id="de4ae-139">ID van de geheime toegangssleutel.</span><span class="sxs-lookup"><span data-stu-id="de4ae-139">ID of the secret access key.</span></span> |<span data-ttu-id="de4ae-140">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="de4ae-140">string</span></span> |<span data-ttu-id="de4ae-141">Ja</span><span class="sxs-lookup"><span data-stu-id="de4ae-141">Yes</span></span> |
| <span data-ttu-id="de4ae-142">secretAccessKey</span><span class="sxs-lookup"><span data-stu-id="de4ae-142">secretAccessKey</span></span> |<span data-ttu-id="de4ae-143">De geheime toegangssleutel zelf.</span><span class="sxs-lookup"><span data-stu-id="de4ae-143">The secret access key itself.</span></span> |<span data-ttu-id="de4ae-144">Versleutelde geheime tekenreeks</span><span class="sxs-lookup"><span data-stu-id="de4ae-144">Encrypted secret string</span></span> |<span data-ttu-id="de4ae-145">Ja</span><span class="sxs-lookup"><span data-stu-id="de4ae-145">Yes</span></span> |

<span data-ttu-id="de4ae-146">Hier volgt een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="de4ae-146">Here is an example:</span></span>

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

## <a name="dataset-properties"></a><span data-ttu-id="de4ae-147">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="de4ae-147">Dataset properties</span></span>
<span data-ttu-id="de4ae-148">Als een dataset staat voor invoergegevens in Azure Blob-opslag opgeven, stelt u de eigenschap type van de gegevensset **AmazonS3**.</span><span class="sxs-lookup"><span data-stu-id="de4ae-148">To specify a dataset to represent input data in Azure Blob storage, set the type property of the dataset to **AmazonS3**.</span></span> <span data-ttu-id="de4ae-149">Stel de **linkedServiceName** eigenschap van de gegevensset op de naam van de Amazon S3 gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="de4ae-149">Set the **linkedServiceName** property of the dataset to the name of the Amazon S3 linked service.</span></span> <span data-ttu-id="de4ae-150">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets [gegevenssets maken](data-factory-create-datasets.md).</span><span class="sxs-lookup"><span data-stu-id="de4ae-150">For a full list of sections and properties available for defining datasets, see [Creating datasets](data-factory-create-datasets.md).</span></span> 

<span data-ttu-id="de4ae-151">Secties zoals structuur, beschikbaarheid en beleid zijn identiek voor alle typen van de gegevensset (zoals SQL-database, blob van Azure en Azure-tabel).</span><span class="sxs-lookup"><span data-stu-id="de4ae-151">Sections such as structure, availability, and policy are similar for all dataset types (such as SQL database, Azure blob, and Azure table).</span></span> <span data-ttu-id="de4ae-152">De **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over de locatie van de gegevens in het gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="de4ae-152">The **typeProperties** section is different for each type of dataset, and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="de4ae-153">De **typeProperties** sectie voor een gegevensset van het type **AmazonS3** (waaronder de gegevensset Amazon S3) heeft de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="de4ae-153">The **typeProperties** section for a dataset of type **AmazonS3** (which includes the Amazon S3 dataset) has the following properties:</span></span>

| <span data-ttu-id="de4ae-154">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="de4ae-154">Property</span></span> | <span data-ttu-id="de4ae-155">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="de4ae-155">Description</span></span> | <span data-ttu-id="de4ae-156">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="de4ae-156">Allowed values</span></span> | <span data-ttu-id="de4ae-157">Vereist</span><span class="sxs-lookup"><span data-stu-id="de4ae-157">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="de4ae-158">bucketName</span><span class="sxs-lookup"><span data-stu-id="de4ae-158">bucketName</span></span> |<span data-ttu-id="de4ae-159">De naam van de S3-bucket.</span><span class="sxs-lookup"><span data-stu-id="de4ae-159">The S3 bucket name.</span></span> |<span data-ttu-id="de4ae-160">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="de4ae-160">String</span></span> |<span data-ttu-id="de4ae-161">Ja</span><span class="sxs-lookup"><span data-stu-id="de4ae-161">Yes</span></span> |
| <span data-ttu-id="de4ae-162">sleutel</span><span class="sxs-lookup"><span data-stu-id="de4ae-162">key</span></span> |<span data-ttu-id="de4ae-163">De sleutel van het object S3.</span><span class="sxs-lookup"><span data-stu-id="de4ae-163">The S3 object key.</span></span> |<span data-ttu-id="de4ae-164">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="de4ae-164">String</span></span> |<span data-ttu-id="de4ae-165">Nee</span><span class="sxs-lookup"><span data-stu-id="de4ae-165">No</span></span> |
| <span data-ttu-id="de4ae-166">voorvoegsel</span><span class="sxs-lookup"><span data-stu-id="de4ae-166">prefix</span></span> |<span data-ttu-id="de4ae-167">Voorvoegsel voor de sleutel S3-object.</span><span class="sxs-lookup"><span data-stu-id="de4ae-167">Prefix for the S3 object key.</span></span> <span data-ttu-id="de4ae-168">Objecten waarvan sleutels met dit voorvoegsel beginnen worden geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="de4ae-168">Objects whose keys start with this prefix are selected.</span></span> <span data-ttu-id="de4ae-169">Geldt alleen als sleutel is leeg.</span><span class="sxs-lookup"><span data-stu-id="de4ae-169">Applies only when key is empty.</span></span> |<span data-ttu-id="de4ae-170">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="de4ae-170">String</span></span> |<span data-ttu-id="de4ae-171">Nee</span><span class="sxs-lookup"><span data-stu-id="de4ae-171">No</span></span> |
| <span data-ttu-id="de4ae-172">Versie</span><span class="sxs-lookup"><span data-stu-id="de4ae-172">version</span></span> |<span data-ttu-id="de4ae-173">De versie van het object S3, als S3 versiebeheer is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="de4ae-173">The version of the S3 object, if S3 versioning is enabled.</span></span> |<span data-ttu-id="de4ae-174">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="de4ae-174">String</span></span> |<span data-ttu-id="de4ae-175">Nee</span><span class="sxs-lookup"><span data-stu-id="de4ae-175">No</span></span> |
| <span data-ttu-id="de4ae-176">Indeling</span><span class="sxs-lookup"><span data-stu-id="de4ae-176">format</span></span> | <span data-ttu-id="de4ae-177">De volgende indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="de4ae-177">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="de4ae-178">Stel de **type** eigenschap onder indeling op een van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="de4ae-178">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="de4ae-179">Zie voor meer informatie de [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [JSON-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren indeling](data-factory-supported-file-and-compression-formats.md#parquet-format) secties.</span><span class="sxs-lookup"><span data-stu-id="de4ae-179">For more information, see the [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="de4ae-180">Als u wilt kopiëren van bestanden als-is tussen bestandsgebaseerde winkels (binaire kopiëren), de indeling-sectie in beide definities invoer en uitvoer gegevensset overslaan.</span><span class="sxs-lookup"><span data-stu-id="de4ae-180">If you want to copy files as-is between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="de4ae-181">Nee</span><span class="sxs-lookup"><span data-stu-id="de4ae-181">No</span></span> | |
| <span data-ttu-id="de4ae-182">Compressie</span><span class="sxs-lookup"><span data-stu-id="de4ae-182">compression</span></span> | <span data-ttu-id="de4ae-183">Geef het type en de compressie van de gegevens.</span><span class="sxs-lookup"><span data-stu-id="de4ae-183">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="de4ae-184">De ondersteunde typen zijn: **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="de4ae-184">The supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="de4ae-185">De ondersteunde niveaus: **optimale** en **snelst**.</span><span class="sxs-lookup"><span data-stu-id="de4ae-185">The supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="de4ae-186">Zie voor meer informatie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="de4ae-186">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="de4ae-187">Nee</span><span class="sxs-lookup"><span data-stu-id="de4ae-187">No</span></span> | |


> [!NOTE]
> <span data-ttu-id="de4ae-188">**bucketName + toets** geeft de locatie van het object S3, waarbij bucket de hoofdcontainer voor S3-objecten en -sleutel is het volledige pad naar het S3-object.</span><span class="sxs-lookup"><span data-stu-id="de4ae-188">**bucketName + key** specifies the location of the S3 object, where bucket is the root container for S3 objects, and key is the full path to the S3 object.</span></span>

### <a name="sample-dataset-with-prefix"></a><span data-ttu-id="de4ae-189">Voorbeeldgegevensset met voorvoegsel</span><span class="sxs-lookup"><span data-stu-id="de4ae-189">Sample dataset with prefix</span></span>

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
### <a name="sample-dataset-with-version"></a><span data-ttu-id="de4ae-190">Voorbeeldgegevensset (met versie)</span><span class="sxs-lookup"><span data-stu-id="de4ae-190">Sample dataset (with version)</span></span>

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

### <a name="dynamic-paths-for-s3"></a><span data-ttu-id="de4ae-191">Dynamische paden voor S3</span><span class="sxs-lookup"><span data-stu-id="de4ae-191">Dynamic paths for S3</span></span>
<span data-ttu-id="de4ae-192">Het vorige voorbeeld gebruikmaakt van vaste waarden voor de **sleutel** en **bucketName** eigenschappen in de Amazon S3-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="de4ae-192">The preceding sample uses fixed values for the **key** and **bucketName** properties in the Amazon S3 dataset.</span></span>

```json
"key": "testFolder/test.orc",
"bucketName": "testbucket",
```

<span data-ttu-id="de4ae-193">U kunt deze eigenschappen tijdens runtime dynamisch berekenen met behulp van systeemvariabelen zoals SliceStart Gegevensfactory hebben.</span><span class="sxs-lookup"><span data-stu-id="de4ae-193">You can have Data Factory calculate these properties dynamically at runtime, by using system variables such as SliceStart.</span></span>

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

<span data-ttu-id="de4ae-194">U kunt hetzelfde doen voor de **voorvoegsel** eigenschap van een gegevensset Amazon S3.</span><span class="sxs-lookup"><span data-stu-id="de4ae-194">You can do the same for the **prefix** property of an Amazon S3 dataset.</span></span> <span data-ttu-id="de4ae-195">Zie voor een lijst van ondersteunde functies en variabelen [Data Factory-functies en systeemvariabelen](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="de4ae-195">For a list of supported functions and variables, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="de4ae-196">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="de4ae-196">Copy activity properties</span></span>
<span data-ttu-id="de4ae-197">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van activiteiten [pijplijnen maken](data-factory-create-pipelines.md).</span><span class="sxs-lookup"><span data-stu-id="de4ae-197">For a full list of sections and properties available for defining activities, see [Creating pipelines](data-factory-create-pipelines.md).</span></span> <span data-ttu-id="de4ae-198">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en beleidsregels zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="de4ae-198">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span> <span data-ttu-id="de4ae-199">Eigenschappen die beschikbaar zijn in de **typeProperties** sectie van de activiteit variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="de4ae-199">Properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="de4ae-200">Voor de kopieeractiviteit variëren eigenschappen, afhankelijk van de typen van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="de4ae-200">For the copy activity, properties vary depending on the types of sources and sinks.</span></span> <span data-ttu-id="de4ae-201">Wanneer een bron in de kopieerbewerking is van het type **FileSystemSource** (waaronder Amazon S3), de volgende eigenschap is beschikbaar in **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="de4ae-201">When a source in the copy activity is of type **FileSystemSource** (which includes Amazon S3), the following property is available in **typeProperties** section:</span></span>

| <span data-ttu-id="de4ae-202">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="de4ae-202">Property</span></span> | <span data-ttu-id="de4ae-203">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="de4ae-203">Description</span></span> | <span data-ttu-id="de4ae-204">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="de4ae-204">Allowed values</span></span> | <span data-ttu-id="de4ae-205">Vereist</span><span class="sxs-lookup"><span data-stu-id="de4ae-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="de4ae-206">Recursieve</span><span class="sxs-lookup"><span data-stu-id="de4ae-206">recursive</span></span> |<span data-ttu-id="de4ae-207">Hiermee geeft u op of voor recursief S3 lijst objecten in de map.</span><span class="sxs-lookup"><span data-stu-id="de4ae-207">Specifies whether to recursively list S3 objects under the directory.</span></span> |<span data-ttu-id="de4ae-208">waar/onwaar</span><span class="sxs-lookup"><span data-stu-id="de4ae-208">true/false</span></span> |<span data-ttu-id="de4ae-209">Nee</span><span class="sxs-lookup"><span data-stu-id="de4ae-209">No</span></span> |

## <a name="json-example-copy-data-from-amazon-s3-to-azure-blob-storage"></a><span data-ttu-id="de4ae-210">JSON-voorbeeld: gegevens kopiëren van Amazon S3 naar Azure Blob-opslag</span><span class="sxs-lookup"><span data-stu-id="de4ae-210">JSON example: Copy data from Amazon S3 to Azure Blob storage</span></span>
<span data-ttu-id="de4ae-211">Dit voorbeeld laat zien hoe gegevens vanaf Amazon S3 kopiëren naar een Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="de4ae-211">This sample shows how to copy data from Amazon S3 to an Azure Blob storage.</span></span> <span data-ttu-id="de4ae-212">Echter, gegevens rechtstreeks naar kunnen worden gekopieerd [een van de put die worden ondersteund](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van de kopieeractiviteit in Data Factory.</span><span class="sxs-lookup"><span data-stu-id="de4ae-212">However, data can be copied directly to [any of the sinks that are supported](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using the copy activity in Data Factory.</span></span>

<span data-ttu-id="de4ae-213">Het voorbeeld bevat JSON-definities voor de volgende Data Factory-entiteiten.</span><span class="sxs-lookup"><span data-stu-id="de4ae-213">The sample provides JSON definitions for the following Data Factory entities.</span></span> <span data-ttu-id="de4ae-214">U kunt deze definities gebruiken voor het maken van een pijplijn om gegevens te kopiëren vanaf Amazon S3 naar Blob storage met behulp van de [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), of [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="de4ae-214">You can use these definitions to create a pipeline to copy data from Amazon S3 to Blob storage, by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span>   

* <span data-ttu-id="de4ae-215">Een gekoppelde service van het type [AwsAccessKey](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="de4ae-215">A linked service of type [AwsAccessKey](#linked-service-properties).</span></span>
* <span data-ttu-id="de4ae-216">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="de4ae-216">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="de4ae-217">Invoer [gegevensset](data-factory-create-datasets.md) van het type [AmazonS3](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="de4ae-217">An input [dataset](data-factory-create-datasets.md) of type [AmazonS3](#dataset-properties).</span></span>
* <span data-ttu-id="de4ae-218">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="de4ae-218">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="de4ae-219">Een [pijplijn](data-factory-create-pipelines.md) met de kopieeractiviteit die gebruikmaakt van [FileSystemSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="de4ae-219">A [pipeline](data-factory-create-pipelines.md) with copy activity that uses [FileSystemSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="de4ae-220">Het voorbeeld worden gegevens gekopieerd vanaf Amazon S3 met een Azure-blob elk uur.</span><span class="sxs-lookup"><span data-stu-id="de4ae-220">The sample copies data from Amazon S3 to an Azure blob every hour.</span></span> <span data-ttu-id="de4ae-221">De JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na de voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="de4ae-221">The JSON properties used in these samples are described in sections following the samples.</span></span>

### <a name="amazon-s3-linked-service"></a><span data-ttu-id="de4ae-222">Amazon S3 gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="de4ae-222">Amazon S3 linked service</span></span>

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

### <a name="azure-storage-linked-service"></a><span data-ttu-id="de4ae-223">Een gekoppelde Azure Storage-service</span><span class="sxs-lookup"><span data-stu-id="de4ae-223">Azure Storage linked service</span></span>

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

### <a name="amazon-s3-input-dataset"></a><span data-ttu-id="de4ae-224">Invoergegevensset Amazon S3</span><span class="sxs-lookup"><span data-stu-id="de4ae-224">Amazon S3 input dataset</span></span>

<span data-ttu-id="de4ae-225">Instelling **'extern': true** informeert de Data Factory-service dat de dataset externe aan de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="de4ae-225">Setting **"external": true** informs the Data Factory service that the dataset is external to the data factory.</span></span> <span data-ttu-id="de4ae-226">Deze eigenschap instelt op true in een invoergegevensset die niet wordt geproduceerd door een activiteit in de pijplijn.</span><span class="sxs-lookup"><span data-stu-id="de4ae-226">Set this property to true on an input dataset that is not produced by an activity in the pipeline.</span></span>

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


### <a name="azure-blob-output-dataset"></a><span data-ttu-id="de4ae-227">Azure Blob-uitvoergegevensset</span><span class="sxs-lookup"><span data-stu-id="de4ae-227">Azure Blob output dataset</span></span>

<span data-ttu-id="de4ae-228">Gegevens worden geschreven naar een nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="de4ae-228">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="de4ae-229">Het pad naar de blob wordt dynamisch geëvalueerd op basis van de begintijd van het segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="de4ae-229">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="de4ae-230">Het mappad maakt gebruik van het jaar, maand, dag en uur delen van de begintijd.</span><span class="sxs-lookup"><span data-stu-id="de4ae-230">The folder path uses the year, month, day, and hours parts of the start time.</span></span>

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


### <a name="copy-activity-in-a-pipeline-with-an-amazon-s3-source-and-a-blob-sink"></a><span data-ttu-id="de4ae-231">De kopieeractiviteit in een pijplijn met een bron Amazon S3 en een blob-sink</span><span class="sxs-lookup"><span data-stu-id="de4ae-231">Copy activity in a pipeline with an Amazon S3 source and a blob sink</span></span>

<span data-ttu-id="de4ae-232">De pijplijn bevat een kopieeractiviteit die is geconfigureerd voor gebruik van de invoer- en uitvoergegevenssets en elk uur is gepland.</span><span class="sxs-lookup"><span data-stu-id="de4ae-232">The pipeline contains a copy activity that is configured to use the input and output datasets, and is scheduled to run every hour.</span></span> <span data-ttu-id="de4ae-233">In de pijplijn-JSON-definitie de **bron** type is ingesteld op **FileSystemSource**, en **sink** type is ingesteld op **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="de4ae-233">In the pipeline JSON definition, the **source** type is set to **FileSystemSource**, and **sink** type is set to **BlobSink**.</span></span>

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
> <span data-ttu-id="de4ae-234">Zie het toewijzen van kolommen uit een gegevensset bron naar kolommen uit een gegevensset sink [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="de4ae-234">To map columns from a source dataset to columns from a sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="next-steps"></a><span data-ttu-id="de4ae-235">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="de4ae-235">Next steps</span></span>
<span data-ttu-id="de4ae-236">Zie de volgende artikelen:</span><span class="sxs-lookup"><span data-stu-id="de4ae-236">See the following articles:</span></span>

* <span data-ttu-id="de4ae-237">Zie voor meer informatie over de belangrijkste factoren die prestaties impact van gegevensverplaatsing (kopieeractiviteit) in de Data Factory en verschillende manieren om te optimaliseren, de [activiteit prestaties en prestatieafstemming handleiding kopiëren](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="de4ae-237">To learn about key factors that impact performance of data movement (copy activity) in Data Factory, and various ways to optimize it, see the [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md).</span></span>

* <span data-ttu-id="de4ae-238">Zie voor stapsgewijze instructies voor het maken van een pijplijn met een kopieeractiviteit de [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="de4ae-238">For step-by-step instructions for creating a pipeline with a copy activity, see the [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span>
