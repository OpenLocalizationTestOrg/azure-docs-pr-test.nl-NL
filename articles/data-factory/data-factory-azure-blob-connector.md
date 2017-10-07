---
title: aaaCopy gegevens van/naar Azure Blob Storage | Microsoft Docs
description: 'Meer informatie over hoe toocopy blob-gegevens in Azure Data Factory. Gebruik onze voorbeeld: hoe toocopy gegevens tooand uit Azure Blob Storage en Azure SQL Database.'
keywords: "BLOB-gegevens, azure-blob kopiëren"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: bec8160f-5e07-47e4-8ee1-ebb14cfb805d
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 8428c64e8e8b1084b3f2f680c4e1819559e4ffa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooor-from-azure-blob-storage-using-azure-data-factory"></a><span data-ttu-id="658ed-105">Kopiëren van gegevens tooor uit Azure Blob Storage met Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="658ed-105">Copy data tooor from Azure Blob Storage using Azure Data Factory</span></span>
<span data-ttu-id="658ed-106">Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit Hallo in Azure Data Factory toocopy gegevens tooand uit Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="658ed-106">This article explains how toouse hello Copy Activity in Azure Data Factory toocopy data tooand from Azure Blob Storage.</span></span> <span data-ttu-id="658ed-107">Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.</span><span class="sxs-lookup"><span data-stu-id="658ed-107">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

## <a name="overview"></a><span data-ttu-id="658ed-108">Overzicht</span><span class="sxs-lookup"><span data-stu-id="658ed-108">Overview</span></span>
<span data-ttu-id="658ed-109">U kunt gegevens kopiëren van een ondersteunde bron gegevens opslaan tooAzure Blob Storage of Azure Blob-opslag ondersteund tooany sink gegevens opslaan.</span><span class="sxs-lookup"><span data-stu-id="658ed-109">You can copy data from any supported source data store tooAzure Blob Storage or from Azure Blob Storage tooany supported sink data store.</span></span> <span data-ttu-id="658ed-110">Hello volgende tabel geeft een lijst van gegevensarchieven ondersteund als bronnen of sinks door Hallo kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="658ed-110">hello following table provides a list of data stores supported as sources or sinks by hello copy activity.</span></span> <span data-ttu-id="658ed-111">U kunt bijvoorbeeld gegevens verplaatsen **van** een SQL Server-database of een Azure SQL database **naar** Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="658ed-111">For example, you can move data **from** a SQL Server database or an Azure SQL database **to** an Azure blob storage.</span></span> <span data-ttu-id="658ed-112">En u kunt gegevens kopiëren **van** Azure blob-opslag **naar** een Azure SQL Data Warehouse of een verzameling Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="658ed-112">And, you can copy data **from** Azure blob storage **to** an Azure SQL Data Warehouse or an Azure Cosmos DB collection.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="658ed-113">Ondersteunde scenario 's</span><span class="sxs-lookup"><span data-stu-id="658ed-113">Supported scenarios</span></span>
<span data-ttu-id="658ed-114">U kunt gegevens kopiëren **uit Azure Blob Storage** toohello gegevensarchieven te volgen:</span><span class="sxs-lookup"><span data-stu-id="658ed-114">You can copy data **from Azure Blob Storage** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="658ed-115">Gegevens kunnen worden gekopieerd van de volgende gegevensarchieven Hallo **tooAzure Blob Storage**:</span><span class="sxs-lookup"><span data-stu-id="658ed-115">You can copy data from hello following data stores **tooAzure Blob Storage**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]
 
> [!IMPORTANT]
> <span data-ttu-id="658ed-116">Kopieeractiviteit ondersteunt kopiëren van gegevens van / tooboth voor algemene doeleinden Azure Storage-accounts en Hot/Cool storage-Blob.</span><span class="sxs-lookup"><span data-stu-id="658ed-116">Copy Activity supports copying data from/tooboth general-purpose Azure Storage accounts and Hot/Cool Blob storage.</span></span> <span data-ttu-id="658ed-117">Hallo-activiteit ondersteunt **lezen van het blok, toevoegen of pagina-blobs**, maar ondersteunt **tooonly blok-blobs schrijven**.</span><span class="sxs-lookup"><span data-stu-id="658ed-117">hello activity supports **reading from block, append, or page blobs**, but supports **writing tooonly block blobs**.</span></span> <span data-ttu-id="658ed-118">Azure Premium-opslag wordt niet ondersteund als een sink omdat het wordt ondersteund door de pagina-blobs.</span><span class="sxs-lookup"><span data-stu-id="658ed-118">Azure Premium Storage is not supported as a sink because it is backed by page blobs.</span></span>
> 
> <span data-ttu-id="658ed-119">Kopieeractiviteit verwijdert geen gegevens van de bron Hallo nadat Hallo gegevens correct zijn gekopieerd toohello bestemming.</span><span class="sxs-lookup"><span data-stu-id="658ed-119">Copy Activity does not delete data from hello source after hello data is successfully copied toohello destination.</span></span> <span data-ttu-id="658ed-120">Als u brongegevens toodelete na een geslaagde kopie moet, maakt u een [aangepaste activiteit](data-factory-use-custom-activities.md) toodelete Hallo van gegevens en Hallo activiteit in de pijplijn hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="658ed-120">If you need toodelete source data after a successful copy, create a [custom activity](data-factory-use-custom-activities.md) toodelete hello data and use hello activity in hello pipeline.</span></span> <span data-ttu-id="658ed-121">Zie voor een voorbeeld Hallo [verwijderen blob of de map voorbeeld op GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity).</span><span class="sxs-lookup"><span data-stu-id="658ed-121">For an example, see hello [Delete blob or folder sample on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity).</span></span> 

## <a name="get-started"></a><span data-ttu-id="658ed-122">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="658ed-122">Get started</span></span>
<span data-ttu-id="658ed-123">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens uit een Azure Blob-opslag verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="658ed-123">You can create a pipeline with a copy activity that moves data to/from an Azure Blob Storage by using different tools/APIs.</span></span>

<span data-ttu-id="658ed-124">Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="658ed-124">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="658ed-125">Dit artikel bevat een [scenario](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) voor het maken van een pijplijn toocopy gegevens van een Azure Blob Storage locatie tooanother Azure Blob Storage-locatie.</span><span class="sxs-lookup"><span data-stu-id="658ed-125">This article has a [walkthrough](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) for creating a pipeline toocopy data from an Azure Blob Storage location  tooanother Azure Blob Storage location.</span></span> <span data-ttu-id="658ed-126">Zie voor een zelfstudie over het maken van een pijplijn toocopy gegevens van een Azure Blob Storage tooAzure SQL-Database, [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="658ed-126">For a tutorial on creating a pipeline toocopy data from an Azure Blob Storage tooAzure SQL Database, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="658ed-127">U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="658ed-127">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="658ed-128">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="658ed-128">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="658ed-129">Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="658ed-129">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="658ed-130">Maak een **gegevensfactory**.</span><span class="sxs-lookup"><span data-stu-id="658ed-130">Create a **data factory**.</span></span> <span data-ttu-id="658ed-131">Een gegevensfactory kan één of meer pijplijnen bevatten.</span><span class="sxs-lookup"><span data-stu-id="658ed-131">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="658ed-132">Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="658ed-132">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="658ed-133">Bijvoorbeeld, als u gegevens uit een Azure blob storage tooan Azure SQL database kopiëren wilt, u twee gekoppelde services toolink uw Azure storage-account en de Azure SQL database tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="658ed-133">For example, if you are copying data from an Azure blob storage tooan Azure SQL database, you create two linked services toolink your Azure storage account and Azure SQL database tooyour data factory.</span></span> <span data-ttu-id="658ed-134">Zie voor de gekoppelde service-eigenschappen die specifiek tooAzure Blob Storage, [gekoppelde service-eigenschappen](#linked-service-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="658ed-134">For linked service properties that are specific tooAzure Blob Storage, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="658ed-135">Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="658ed-135">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="658ed-136">In vermeld in de laatste stap Hallo Hallo voorbeeld maakt u een gegevensset toospecify Hallo blob-container en map met invoergegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="658ed-136">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="658ed-137">En u een andere dataset toospecify Hallo SQL-tabel maken in hello Azure SQL-database waarin Hallo-gegevens die zijn gekopieerd uit Hallo blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="658ed-137">And, you create another dataset toospecify hello SQL table in hello Azure SQL database that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="658ed-138">Zie voor eigenschappen van gegevensset die specifieke tooAzure Blob Storage, [eigenschappen van gegevensset](#dataset-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="658ed-138">For dataset properties that are specific tooAzure Blob Storage, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="658ed-139">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="658ed-139">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="658ed-140">In Hallo voorbeeld eerder vermeld, gebruikt u BlobSource als een bron- en SqlSink als een sink voor de kopieeractiviteit Hallo.</span><span class="sxs-lookup"><span data-stu-id="658ed-140">In hello example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for hello copy activity.</span></span> <span data-ttu-id="658ed-141">Op dezelfde manier als u van Azure SQL Database tooAzure Blob Storage kopiëren wilt, gebruikt u SqlSource en BlobSink in Hallo kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="658ed-141">Similarly, if you are copying from Azure SQL Database tooAzure Blob Storage, you use SqlSource and BlobSink in hello copy activity.</span></span> <span data-ttu-id="658ed-142">Zie voor activiteitseigenschappen kopiëren die specifieke tooAzure Blob Storage, [activiteitseigenschappen kopiëren](#copy-activity-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="658ed-142">For copy activity properties that are specific tooAzure Blob Storage, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="658ed-143">Voor informatie over hoe toouse een gegevensarchief als een bron of een sink, klikt u op Hallo-koppeling in de vorige sectie Hallo voor de gegevensopslag.</span><span class="sxs-lookup"><span data-stu-id="658ed-143">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>  

<span data-ttu-id="658ed-144">Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="658ed-144">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="658ed-145">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="658ed-145">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="658ed-146">Zie voor voorbeelden met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens van/naar een Azure Blob Storage zijn, [JSON voorbeelden](#json-examples-for-copying-data-to-and-from-blob-storage  ) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="658ed-146">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure Blob Storage, see [JSON examples](#json-examples-for-copying-data-to-and-from-blob-storage  ) section of this article.</span></span>

<span data-ttu-id="658ed-147">Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooAzure Blob Storage zijn.</span><span class="sxs-lookup"><span data-stu-id="658ed-147">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooAzure Blob Storage.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="658ed-148">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="658ed-148">Linked service properties</span></span>
<span data-ttu-id="658ed-149">Er zijn twee typen van de gekoppelde services kunt u een Azure Storage tooan Azure data factory toolink.</span><span class="sxs-lookup"><span data-stu-id="658ed-149">There are two types of linked services you can use toolink an Azure Storage tooan Azure data factory.</span></span> <span data-ttu-id="658ed-150">Ze zijn: **AzureStorage** gekoppelde service en **AzureStorageSas** gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="658ed-150">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="658ed-151">Hallo gekoppelde Azure Storage-service biedt Hallo data factory met globale toegang toohello Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="658ed-151">hello Azure Storage linked service provides hello data factory with global access toohello Azure Storage.</span></span> <span data-ttu-id="658ed-152">Terwijl hello Azure Storage SAS (Shared Access Signature) gekoppelde biedt service Hallo gegevensfactory met de toegang beperkt/tijdsgebonden toohello Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="658ed-152">Whereas, hello Azure Storage SAS (Shared Access Signature) linked service provides hello data factory with restricted/time-bound access toohello Azure Storage.</span></span> <span data-ttu-id="658ed-153">Er zijn geen andere verschillen tussen deze twee gekoppelde services.</span><span class="sxs-lookup"><span data-stu-id="658ed-153">There are no other differences between these two linked services.</span></span> <span data-ttu-id="658ed-154">Kies Hallo gekoppelde service die bij uw behoeften past.</span><span class="sxs-lookup"><span data-stu-id="658ed-154">Choose hello linked service that suits your needs.</span></span> <span data-ttu-id="658ed-155">Hallo vindt volgende secties u meer informatie over deze twee gekoppelde services.</span><span class="sxs-lookup"><span data-stu-id="658ed-155">hello following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="658ed-156">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="658ed-156">Dataset properties</span></span>
<span data-ttu-id="658ed-157">een gegevensset toorepresent toospecify invoer- of -gegevens in een Azure Blob Storage, stelt u Hallo type-eigenschap van Hallo gegevensset: **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="658ed-157">toospecify a dataset toorepresent input or output data in an Azure Blob Storage, you set hello type property of hello dataset to: **AzureBlob**.</span></span> <span data-ttu-id="658ed-158">Set Hallo **linkedServiceName** eigenschap Hallo gegevensset toohello naam van hello Azure Storage of Azure Storage SAS gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="658ed-158">Set hello **linkedServiceName** property of hello dataset toohello name of hello Azure Storage or Azure Storage SAS linked service.</span></span>  <span data-ttu-id="658ed-159">Hallo-eigenschappen van gegevensset Hallo Hallo opgeven **blob-container** en Hallo **map** in Hallo blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="658ed-159">hello type properties of hello dataset specify hello **blob container** and hello **folder** in hello blob storage.</span></span>

<span data-ttu-id="658ed-160">Zie voor een volledige lijst van JSON-secties & eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="658ed-160">For a full list of JSON sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="658ed-161">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).</span><span class="sxs-lookup"><span data-stu-id="658ed-161">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="658ed-162">Data factory ondersteunt Hallo compatibel met CLS .NET op basis van waarden voor het ontwikkelen van type-informatie in 'structuur' voor het schema op lezen gegevensbronnen zoals Azure blob te volgen: Int16, Int32, Int64, één, Double, Decimal, Byte [], Bool, String, Guid, Datetime, DateTimeOffset, Timespan.</span><span class="sxs-lookup"><span data-stu-id="658ed-162">Data factory supports hello following CLS-compliant .NET based type values for providing type information in “structure” for schema-on-read data sources like Azure blob: Int16, Int32, Int64, Single, Double, Decimal, Byte[], Bool, String, Guid, Datetime, Datetimeoffset, Timespan.</span></span> <span data-ttu-id="658ed-163">Data Factory voert automatisch typeconversies bij het verplaatsen van gegevens uit een brongegevens tooa sink data store opslaan.</span><span class="sxs-lookup"><span data-stu-id="658ed-163">Data Factory automatically performs type conversions when moving data from a source data store tooa sink data store.</span></span>

<span data-ttu-id="658ed-164">Hallo **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over Hallo locatie, opmaken enz., van gegevens in het gegevensarchief Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="658ed-164">hello **typeProperties** section is different for each type of dataset and provides information about hello location, format etc., of hello data in hello data store.</span></span> <span data-ttu-id="658ed-165">Hallo typeProperties sectie voor de gegevensset van het type **AzureBlob** dataset bevat Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="658ed-165">hello typeProperties section for dataset of type **AzureBlob** dataset has hello following properties:</span></span>

| <span data-ttu-id="658ed-166">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="658ed-166">Property</span></span> | <span data-ttu-id="658ed-167">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="658ed-167">Description</span></span> | <span data-ttu-id="658ed-168">Vereist</span><span class="sxs-lookup"><span data-stu-id="658ed-168">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="658ed-169">folderPath</span><span class="sxs-lookup"><span data-stu-id="658ed-169">folderPath</span></span> |<span data-ttu-id="658ed-170">Pad toohello container en map in Hallo blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="658ed-170">Path toohello container and folder in hello blob storage.</span></span> <span data-ttu-id="658ed-171">Voorbeeld: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="658ed-171">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="658ed-172">Ja</span><span class="sxs-lookup"><span data-stu-id="658ed-172">Yes</span></span> |
| <span data-ttu-id="658ed-173">fileName</span><span class="sxs-lookup"><span data-stu-id="658ed-173">fileName</span></span> |<span data-ttu-id="658ed-174">De naam van Hallo blob.</span><span class="sxs-lookup"><span data-stu-id="658ed-174">Name of hello blob.</span></span> <span data-ttu-id="658ed-175">Bestandsnaam is optioneel en is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="658ed-175">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="658ed-176">Als u een bestandsnaam, Hallo activiteit (inclusief kopiëren) werkt opgeeft op Hallo specifieke Blob.</span><span class="sxs-lookup"><span data-stu-id="658ed-176">If you specify a filename, hello activity (including Copy) works on hello specific Blob.</span></span><br/><br/><span data-ttu-id="658ed-177">Bestandsnaam is opgegeven, bevat kopiëren alle Blobs Hallo folderPath voor invoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="658ed-177">When fileName is not specified, Copy includes all Blobs in hello folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="658ed-178">Wanneer **fileName** is niet opgegeven voor een uitvoergegevensset en **preserveHierarchy** niet is opgegeven in activiteit sink Hallo-naam van Hallo gegenereerd bestand zou zijn in Hallo volgt deze indeling: Data.<Guid>. txt (bijvoorbeeld:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="658ed-178">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, hello name of hello generated file would be in hello following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="658ed-179">Nee</span><span class="sxs-lookup"><span data-stu-id="658ed-179">No</span></span> |
| <span data-ttu-id="658ed-180">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="658ed-180">partitionedBy</span></span> |<span data-ttu-id="658ed-181">partitionedBy is een optionele eigenschap.</span><span class="sxs-lookup"><span data-stu-id="658ed-181">partitionedBy is an optional property.</span></span> <span data-ttu-id="658ed-182">Kunt u deze toospecify een dynamische folderPath en de bestandsnaam voor de reeksgegevens.</span><span class="sxs-lookup"><span data-stu-id="658ed-182">You can use it toospecify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="658ed-183">FolderPath kan bijvoorbeeld parameters worden gebruikt voor elk uur van gegevens.</span><span class="sxs-lookup"><span data-stu-id="658ed-183">For example, folderPath can be parameterized for every hour of data.</span></span> <span data-ttu-id="658ed-184">Zie Hallo [partitionedBy eigenschap sectie](#using-partitionedBy-property) voor meer informatie en voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="658ed-184">See hello [Using partitionedBy property section](#using-partitionedBy-property) for details and examples.</span></span> |<span data-ttu-id="658ed-185">Nee</span><span class="sxs-lookup"><span data-stu-id="658ed-185">No</span></span> |
| <span data-ttu-id="658ed-186">Indeling</span><span class="sxs-lookup"><span data-stu-id="658ed-186">format</span></span> | <span data-ttu-id="658ed-187">Hallo na indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="658ed-187">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="658ed-188">Set Hallo **type** eigenschap onder indeling tooone van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="658ed-188">Set hello **type** property under format tooone of these values.</span></span> <span data-ttu-id="658ed-189">Zie voor meer informatie [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [Json-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren indeling](data-factory-supported-file-and-compression-formats.md#parquet-format) secties.</span><span class="sxs-lookup"><span data-stu-id="658ed-189">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="658ed-190">Als u wilt dat te**kopiëren van bestanden als-is** tussen bestandsgebaseerde winkels (binaire kopiëren) Hallo indeling sectie in beide definities invoer en uitvoer gegevensset overslaan.</span><span class="sxs-lookup"><span data-stu-id="658ed-190">If you want too**copy files as-is** between file-based stores (binary copy), skip hello format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="658ed-191">Nee</span><span class="sxs-lookup"><span data-stu-id="658ed-191">No</span></span> |
| <span data-ttu-id="658ed-192">Compressie</span><span class="sxs-lookup"><span data-stu-id="658ed-192">compression</span></span> | <span data-ttu-id="658ed-193">Hallo-type en compressieniveau voor Hallo gegevens opgeven.</span><span class="sxs-lookup"><span data-stu-id="658ed-193">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="658ed-194">Ondersteunde typen zijn: **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="658ed-194">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="658ed-195">Ondersteunde niveaus: **optimale** en **snelst**.</span><span class="sxs-lookup"><span data-stu-id="658ed-195">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="658ed-196">Zie voor meer informatie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="658ed-196">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="658ed-197">Nee</span><span class="sxs-lookup"><span data-stu-id="658ed-197">No</span></span> |

### <a name="using-partitionedby-property"></a><span data-ttu-id="658ed-198">Gebruik de eigenschap partitionedBy</span><span class="sxs-lookup"><span data-stu-id="658ed-198">Using partitionedBy property</span></span>
<span data-ttu-id="658ed-199">Zoals vermeld in de vorige sectie hello, kunt u een dynamische folderPath en de bestandsnaam voor de reeks tijdgegevens Hello **partitionedBy** -eigenschap [Data Factory-functies en Hallo systeemvariabelen](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="658ed-199">As mentioned in hello previous section, you can specify a dynamic folderPath and filename for time series data with hello **partitionedBy** property, [Data Factory functions, and hello system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="658ed-200">Zie voor meer informatie over tijd reeks gegevenssets, planning en segmenten [gegevenssets maken](data-factory-create-datasets.md) en [planning en uitvoering](data-factory-scheduling-and-execution.md) artikelen.</span><span class="sxs-lookup"><span data-stu-id="658ed-200">For more information on time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md) and [Scheduling & Execution](data-factory-scheduling-and-execution.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="658ed-201">Voorbeeld 1</span><span class="sxs-lookup"><span data-stu-id="658ed-201">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="658ed-202">In dit voorbeeld {segment} is vervangen door de waarde van de Hallo van Data Factory systeemvariabele SliceStart Hallo-indeling (YYYYMMDDHH) opgegeven.</span><span class="sxs-lookup"><span data-stu-id="658ed-202">In this example, {Slice} is replaced with hello value of Data Factory system variable SliceStart in hello format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="658ed-203">Hallo SliceStart verwijst toostart tijd van Hallo segment.</span><span class="sxs-lookup"><span data-stu-id="658ed-203">hello SliceStart refers toostart time of hello slice.</span></span> <span data-ttu-id="658ed-204">Hallo folderPath verschilt voor elk segment.</span><span class="sxs-lookup"><span data-stu-id="658ed-204">hello folderPath is different for each slice.</span></span> <span data-ttu-id="658ed-205">Bijvoorbeeld: wikidatagateway/wikisampledataout/2014100103 of wikidatagateway/wikisampledataout/2014100104</span><span class="sxs-lookup"><span data-stu-id="658ed-205">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104</span></span>

#### <a name="sample-2"></a><span data-ttu-id="658ed-206">Voorbeeld 2</span><span class="sxs-lookup"><span data-stu-id="658ed-206">Sample 2</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```

<span data-ttu-id="658ed-207">In dit voorbeeld worden jaar, maand, dag en tijd van de SliceStart uitgepakt in verschillende variabelen die worden gebruikt door de eigenschappen voor folderPath en de bestandsnaam.</span><span class="sxs-lookup"><span data-stu-id="658ed-207">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="658ed-208">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="658ed-208">Copy activity properties</span></span>
<span data-ttu-id="658ed-209">Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="658ed-209">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="658ed-210">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer gegevenssets en beleidsregels zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="658ed-210">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="658ed-211">Dat eigenschappen beschikbaar zijn in Hallo **typeProperties** sectie van de activiteit Hallo variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="658ed-211">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="658ed-212">Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="658ed-212">For Copy activity, they vary depending on hello types of sources and sinks.</span></span> <span data-ttu-id="658ed-213">Als u gegevens uit een Azure Blob-opslag verplaatst, u Hallo brontype instellen in de kopieeractiviteit hello te**BlobSource**.</span><span class="sxs-lookup"><span data-stu-id="658ed-213">If you are moving data from an Azure Blob Storage, you set hello source type in hello copy activity too**BlobSource**.</span></span> <span data-ttu-id="658ed-214">Als u gegevens tooan Azure Blob-opslag verplaatst, u stelt Hallo sink-type in de kopieerbewerking Hallo te**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="658ed-214">Similarly, if you are moving data tooan Azure Blob Storage, you set hello sink type in hello copy activity too**BlobSink**.</span></span> <span data-ttu-id="658ed-215">Deze sectie bevat een lijst met eigenschappen die worden ondersteund door BlobSource en BlobSink.</span><span class="sxs-lookup"><span data-stu-id="658ed-215">This section provides a list of properties supported by BlobSource and BlobSink.</span></span>

<span data-ttu-id="658ed-216">**BlobSource** ondersteunt de volgende eigenschappen in Hallo Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="658ed-216">**BlobSource** supports hello following properties in hello **typeProperties** section:</span></span>

| <span data-ttu-id="658ed-217">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="658ed-217">Property</span></span> | <span data-ttu-id="658ed-218">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="658ed-218">Description</span></span> | <span data-ttu-id="658ed-219">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="658ed-219">Allowed values</span></span> | <span data-ttu-id="658ed-220">Vereist</span><span class="sxs-lookup"><span data-stu-id="658ed-220">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="658ed-221">Recursieve</span><span class="sxs-lookup"><span data-stu-id="658ed-221">recursive</span></span> |<span data-ttu-id="658ed-222">Hiermee wordt aangegeven of Hallo gegevens recursief is gelezen vanuit Hallo submappen of alleen vanuit de opgegeven map Hallo.</span><span class="sxs-lookup"><span data-stu-id="658ed-222">Indicates whether hello data is read recursively from hello sub folders or only from hello specified folder.</span></span> |<span data-ttu-id="658ed-223">True (standaardwaarde), False</span><span class="sxs-lookup"><span data-stu-id="658ed-223">True (default value), False</span></span> |<span data-ttu-id="658ed-224">Nee</span><span class="sxs-lookup"><span data-stu-id="658ed-224">No</span></span> |

<span data-ttu-id="658ed-225">**BlobSink** ondersteunt de volgende eigenschappen Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="658ed-225">**BlobSink** supports hello following properties **typeProperties** section:</span></span>

| <span data-ttu-id="658ed-226">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="658ed-226">Property</span></span> | <span data-ttu-id="658ed-227">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="658ed-227">Description</span></span> | <span data-ttu-id="658ed-228">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="658ed-228">Allowed values</span></span> | <span data-ttu-id="658ed-229">Vereist</span><span class="sxs-lookup"><span data-stu-id="658ed-229">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="658ed-230">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="658ed-230">copyBehavior</span></span> |<span data-ttu-id="658ed-231">Hallo kopie gedrag definieert wanneer Hallo bron BlobSource of bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="658ed-231">Defines hello copy behavior when hello source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="658ed-232"><b>PreserveHierarchy</b>: gehandhaafd Hallo bestandshiërarchie in de doelmap Hallo.</span><span class="sxs-lookup"><span data-stu-id="658ed-232"><b>PreserveHierarchy</b>: preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="658ed-233">Hallo relatieve pad van de bestandsmap toosource bron is identiek toohello relatieve pad van de bestandsmap tootarget doel.</span><span class="sxs-lookup"><span data-stu-id="658ed-233">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="658ed-234"><b>FlattenHierarchy</b>: alle bestanden uit de bronmap Hallo zijn in Hallo eerst niveau van de doelmap.</span><span class="sxs-lookup"><span data-stu-id="658ed-234"><b>FlattenHierarchy</b>: all files from hello source folder are in hello first level of target folder.</span></span> <span data-ttu-id="658ed-235">Hallo doelbestanden hebben automatisch gegenereerde naam.</span><span class="sxs-lookup"><span data-stu-id="658ed-235">hello target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="658ed-236"><b>MergeFiles</b>: alle bestanden uit map Hallo-tooone bronbestand worden samengevoegd.</span><span class="sxs-lookup"><span data-stu-id="658ed-236"><b>MergeFiles</b>: merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="658ed-237">Als Hallo bestand/Blob-naam wordt opgegeven, zou Hallo Samengevoegde bestandsnaam Hallo opgegeven name; zijn anders zou worden automatisch gegenereerde naam.</span><span class="sxs-lookup"><span data-stu-id="658ed-237">If hello File/Blob Name is specified, hello merged file name would be hello specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="658ed-238">Nee</span><span class="sxs-lookup"><span data-stu-id="658ed-238">No</span></span> |

<span data-ttu-id="658ed-239">**BlobSource** biedt ook ondersteuning voor deze twee eigenschappen voor achterwaartse compatibiliteit.</span><span class="sxs-lookup"><span data-stu-id="658ed-239">**BlobSource** also supports these two properties for backward compatibility.</span></span>

* <span data-ttu-id="658ed-240">**treatEmptyAsNull**: Hiermee geeft u op of tootreat null of lege tekenreeks als null-waarde.</span><span class="sxs-lookup"><span data-stu-id="658ed-240">**treatEmptyAsNull**: Specifies whether tootreat null or empty string as null value.</span></span>
* <span data-ttu-id="658ed-241">**skipHeaderLineCount** -geeft aan hoeveel lijnen moeten worden overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="658ed-241">**skipHeaderLineCount** - Specifies how many lines need be skipped.</span></span> <span data-ttu-id="658ed-242">Dit geldt alleen wanneer invoergegevensset gebruikmaakt TextFormat.</span><span class="sxs-lookup"><span data-stu-id="658ed-242">It is applicable only when input dataset is using TextFormat.</span></span>

<span data-ttu-id="658ed-243">Op deze manier **BlobSink** ondersteunt Hallo na eigenschap voor achterwaartse compatibiliteit.</span><span class="sxs-lookup"><span data-stu-id="658ed-243">Similarly, **BlobSink** supports hello following property for backward compatibility.</span></span>

* <span data-ttu-id="658ed-244">**blobWriterAddHeader**: Hiermee geeft u op of een koptekst van de kolomdefinities tijdens het schrijven van tooan tooadd uitvoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="658ed-244">**blobWriterAddHeader**: Specifies whether tooadd a header of column definitions while writing tooan output dataset.</span></span>

<span data-ttu-id="658ed-245">Gegevenssets nu ondersteuning Hallo volgende eigenschappen met dezelfde functionaliteit Hallo: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span><span class="sxs-lookup"><span data-stu-id="658ed-245">Datasets now support hello following properties that implement hello same functionality: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span></span>

<span data-ttu-id="658ed-246">Hallo volgende tabel bevat richtlijnen over het gebruik van Hallo nieuwe eigenschappen van gegevensset in plaats van deze eigenschappen van de bron/sink blob.</span><span class="sxs-lookup"><span data-stu-id="658ed-246">hello following table provides guidance on using hello new dataset properties in place of these blob source/sink properties.</span></span>

| <span data-ttu-id="658ed-247">Activiteitseigenschap kopiëren</span><span class="sxs-lookup"><span data-stu-id="658ed-247">Copy Activity property</span></span> | <span data-ttu-id="658ed-248">Eigenschap DataSet</span><span class="sxs-lookup"><span data-stu-id="658ed-248">Dataset property</span></span> |
|:--- |:--- |
| <span data-ttu-id="658ed-249">skipHeaderLineCount op BlobSource</span><span class="sxs-lookup"><span data-stu-id="658ed-249">skipHeaderLineCount on BlobSource</span></span> |<span data-ttu-id="658ed-250">skipLineCount en firstRowAsHeader.</span><span class="sxs-lookup"><span data-stu-id="658ed-250">skipLineCount and firstRowAsHeader.</span></span> <span data-ttu-id="658ed-251">Regels eerst worden overgeslagen en wordt de eerste rij Hallo gelezen als een koptekst.</span><span class="sxs-lookup"><span data-stu-id="658ed-251">Lines are skipped first and then hello first row is read as a header.</span></span> |
| <span data-ttu-id="658ed-252">treatEmptyAsNull op BlobSource</span><span class="sxs-lookup"><span data-stu-id="658ed-252">treatEmptyAsNull on BlobSource</span></span> |<span data-ttu-id="658ed-253">treatEmptyAsNull op invoergegevensset</span><span class="sxs-lookup"><span data-stu-id="658ed-253">treatEmptyAsNull on input dataset</span></span> |
| <span data-ttu-id="658ed-254">blobWriterAddHeader op BlobSink</span><span class="sxs-lookup"><span data-stu-id="658ed-254">blobWriterAddHeader on BlobSink</span></span> |<span data-ttu-id="658ed-255">firstRowAsHeader op uitvoergegevensset</span><span class="sxs-lookup"><span data-stu-id="658ed-255">firstRowAsHeader on output dataset</span></span> |

<span data-ttu-id="658ed-256">Zie [geven TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) sectie voor meer informatie over deze eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="658ed-256">See [Specifying TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) section for detailed information on these properties.</span></span>    

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="658ed-257">Voorbeelden van recursieve en copyBehavior</span><span class="sxs-lookup"><span data-stu-id="658ed-257">recursive and copyBehavior examples</span></span>
<span data-ttu-id="658ed-258">Deze sectie beschrijft Hallo resulterende gedrag van de kopieerbewerking Hallo voor verschillende combinaties van recursieve en copyBehavior waarden.</span><span class="sxs-lookup"><span data-stu-id="658ed-258">This section describes hello resulting behavior of hello Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="658ed-259">Recursieve</span><span class="sxs-lookup"><span data-stu-id="658ed-259">recursive</span></span> | <span data-ttu-id="658ed-260">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="658ed-260">copyBehavior</span></span> | <span data-ttu-id="658ed-261">Resulterende gedrag</span><span class="sxs-lookup"><span data-stu-id="658ed-261">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="658ed-262">De waarde True</span><span class="sxs-lookup"><span data-stu-id="658ed-262">true</span></span> |<span data-ttu-id="658ed-263">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="658ed-263">preserveHierarchy</span></span> |<span data-ttu-id="658ed-264">Voor een bronmap Map1 Hello structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="658ed-264">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="658ed-265">Map1</span><span class="sxs-lookup"><span data-stu-id="658ed-265">Folder1</span></span><br/><span data-ttu-id="658ed-266">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="658ed-266">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="658ed-267">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="658ed-267">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="658ed-268">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="658ed-268">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="658ed-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="658ed-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="658ed-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="658ed-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="658ed-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="658ed-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="658ed-272">Hallo doelmap Map1 wordt gemaakt met dezelfde structuur, als de bron Hallo Hallo</span><span class="sxs-lookup"><span data-stu-id="658ed-272">hello target folder Folder1 is created with hello same structure as hello source</span></span><br/><br/><span data-ttu-id="658ed-273">Map1</span><span class="sxs-lookup"><span data-stu-id="658ed-273">Folder1</span></span><br/><span data-ttu-id="658ed-274">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="658ed-274">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="658ed-275">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="658ed-275">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="658ed-276">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="658ed-276">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="658ed-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="658ed-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="658ed-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="658ed-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="658ed-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span><span class="sxs-lookup"><span data-stu-id="658ed-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="658ed-280">De waarde True</span><span class="sxs-lookup"><span data-stu-id="658ed-280">true</span></span> |<span data-ttu-id="658ed-281">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="658ed-281">flattenHierarchy</span></span> |<span data-ttu-id="658ed-282">Voor een bronmap Map1 Hello structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="658ed-282">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="658ed-283">Map1</span><span class="sxs-lookup"><span data-stu-id="658ed-283">Folder1</span></span><br/><span data-ttu-id="658ed-284">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="658ed-284">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="658ed-285">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="658ed-285">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="658ed-286">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="658ed-286">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="658ed-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="658ed-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="658ed-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="658ed-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="658ed-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="658ed-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="658ed-290">Hallo doel Map1 is gemaakt met de Hallo structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="658ed-290">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="658ed-291">Map1</span><span class="sxs-lookup"><span data-stu-id="658ed-291">Folder1</span></span><br/><span data-ttu-id="658ed-292">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor File1</span><span class="sxs-lookup"><span data-stu-id="658ed-292">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="658ed-293">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor bestand2</span><span class="sxs-lookup"><span data-stu-id="658ed-293">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="658ed-294">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor bestand3</span><span class="sxs-lookup"><span data-stu-id="658ed-294">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="658ed-295">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor File4</span><span class="sxs-lookup"><span data-stu-id="658ed-295">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="658ed-296">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor File5</span><span class="sxs-lookup"><span data-stu-id="658ed-296">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="658ed-297">De waarde True</span><span class="sxs-lookup"><span data-stu-id="658ed-297">true</span></span> |<span data-ttu-id="658ed-298">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="658ed-298">mergeFiles</span></span> |<span data-ttu-id="658ed-299">Voor een bronmap Map1 Hello structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="658ed-299">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="658ed-300">Map1</span><span class="sxs-lookup"><span data-stu-id="658ed-300">Folder1</span></span><br/><span data-ttu-id="658ed-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="658ed-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="658ed-302">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="658ed-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="658ed-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="658ed-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="658ed-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="658ed-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="658ed-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="658ed-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="658ed-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="658ed-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="658ed-307">Hallo doel Map1 is gemaakt met de Hallo structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="658ed-307">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="658ed-308">Map1</span><span class="sxs-lookup"><span data-stu-id="658ed-308">Folder1</span></span><br/><span data-ttu-id="658ed-309">&nbsp;&nbsp;&nbsp;&nbsp;File1 bestand2 + bestand3 + File4 + bestand 5 inhoud worden samengevoegd in één bestand met automatisch gegenereerde naam</span><span class="sxs-lookup"><span data-stu-id="658ed-309">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="658ed-310">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="658ed-310">false</span></span> |<span data-ttu-id="658ed-311">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="658ed-311">preserveHierarchy</span></span> |<span data-ttu-id="658ed-312">Voor een bronmap Map1 Hello structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="658ed-312">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="658ed-313">Map1</span><span class="sxs-lookup"><span data-stu-id="658ed-313">Folder1</span></span><br/><span data-ttu-id="658ed-314">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="658ed-314">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="658ed-315">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="658ed-315">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="658ed-316">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="658ed-316">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="658ed-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="658ed-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="658ed-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="658ed-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="658ed-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="658ed-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="658ed-320">Hallo doelmap Map1 wordt gemaakt met de Hallo structuur te volgen</span><span class="sxs-lookup"><span data-stu-id="658ed-320">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="658ed-321">Map1</span><span class="sxs-lookup"><span data-stu-id="658ed-321">Folder1</span></span><br/><span data-ttu-id="658ed-322">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="658ed-322">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="658ed-323">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="658ed-323">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="658ed-324">Subfolder1 bestand3 File4 en File5 zijn niet opgenomen.</span><span class="sxs-lookup"><span data-stu-id="658ed-324">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="658ed-325">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="658ed-325">false</span></span> |<span data-ttu-id="658ed-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="658ed-326">flattenHierarchy</span></span> |<span data-ttu-id="658ed-327">Voor een bronmap Map1 Hello structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="658ed-327">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="658ed-328">Map1</span><span class="sxs-lookup"><span data-stu-id="658ed-328">Folder1</span></span><br/><span data-ttu-id="658ed-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="658ed-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="658ed-330">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="658ed-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="658ed-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="658ed-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="658ed-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="658ed-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="658ed-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="658ed-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="658ed-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="658ed-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="658ed-335">Hallo doelmap Map1 wordt gemaakt met de Hallo structuur te volgen</span><span class="sxs-lookup"><span data-stu-id="658ed-335">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="658ed-336">Map1</span><span class="sxs-lookup"><span data-stu-id="658ed-336">Folder1</span></span><br/><span data-ttu-id="658ed-337">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor File1</span><span class="sxs-lookup"><span data-stu-id="658ed-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="658ed-338">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor bestand2</span><span class="sxs-lookup"><span data-stu-id="658ed-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="658ed-339">Subfolder1 bestand3 File4 en File5 zijn niet opgenomen.</span><span class="sxs-lookup"><span data-stu-id="658ed-339">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="658ed-340">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="658ed-340">false</span></span> |<span data-ttu-id="658ed-341">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="658ed-341">mergeFiles</span></span> |<span data-ttu-id="658ed-342">Voor een bronmap Map1 Hello structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="658ed-342">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="658ed-343">Map1</span><span class="sxs-lookup"><span data-stu-id="658ed-343">Folder1</span></span><br/><span data-ttu-id="658ed-344">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="658ed-344">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="658ed-345">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="658ed-345">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="658ed-346">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="658ed-346">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="658ed-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="658ed-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="658ed-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="658ed-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="658ed-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="658ed-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="658ed-350">Hallo doelmap Map1 wordt gemaakt met de Hallo structuur te volgen</span><span class="sxs-lookup"><span data-stu-id="658ed-350">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="658ed-351">Map1</span><span class="sxs-lookup"><span data-stu-id="658ed-351">Folder1</span></span><br/><span data-ttu-id="658ed-352">&nbsp;&nbsp;&nbsp;&nbsp;File1 + bestand2 inhoud worden samengevoegd in één bestand met automatisch gegenereerde naam.</span><span class="sxs-lookup"><span data-stu-id="658ed-352">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="658ed-353">automatisch gegenereerde naam voor File1</span><span class="sxs-lookup"><span data-stu-id="658ed-353">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="658ed-354">Subfolder1 bestand3 File4 en File5 zijn niet opgenomen.</span><span class="sxs-lookup"><span data-stu-id="658ed-354">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="walkthrough-use-copy-wizard-toocopy-data-tofrom-blob-storage"></a><span data-ttu-id="658ed-355">Overzicht: De Wizard kopiëren gebruiken toocopy gegevens van/naar Blob Storage</span><span class="sxs-lookup"><span data-stu-id="658ed-355">Walkthrough: Use Copy Wizard toocopy data to/from Blob Storage</span></span>
<span data-ttu-id="658ed-356">Bekijk hoe gegevens voor het kopiëren van tooquickly van een Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="658ed-356">Let's look at how tooquickly copy data to/from an Azure blob storage.</span></span> <span data-ttu-id="658ed-357">In dit overzicht bron- en doelserver gegevensopslag van het type: Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="658ed-357">In this walkthrough, both source and destination data stores of type: Azure Blob Storage.</span></span> <span data-ttu-id="658ed-358">Hallo pijplijn in dit scenario kopieert gegevens van een map tooanother in Hallo dezelfde blob-container.</span><span class="sxs-lookup"><span data-stu-id="658ed-358">hello pipeline in this walkthrough copies data from a folder tooanother folder in hello same blob container.</span></span> <span data-ttu-id="658ed-359">In dit scenario is opzettelijk eenvoudige tooshow u instellingen of eigenschappen bij gebruik van Blob Storage als een bron- of sink.</span><span class="sxs-lookup"><span data-stu-id="658ed-359">This walkthrough is intentionally simple tooshow you settings or properties when using Blob Storage as a source or sink.</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="658ed-360">Vereisten</span><span class="sxs-lookup"><span data-stu-id="658ed-360">Prerequisites</span></span>
1. <span data-ttu-id="658ed-361">Maak een algemeen **Azure Storage-Account** als u nog niet hebt.</span><span class="sxs-lookup"><span data-stu-id="658ed-361">Create a general-purpose **Azure Storage Account** if you don't have one already.</span></span> <span data-ttu-id="658ed-362">U Hallo blob storage gebruiken als beide **bron** en **bestemming** gegevens opslaan in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="658ed-362">You use hello blob storage as both **source** and **destination** data store in this walkthrough.</span></span> <span data-ttu-id="658ed-363">Als u geen Azure storage-account hebt, raadpleegt u Hallo [een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) artikel voor stappen toocreate een.</span><span class="sxs-lookup"><span data-stu-id="658ed-363">if you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps toocreate one.</span></span>
2. <span data-ttu-id="658ed-364">Maak een blobcontainer met de naam **adfblobconnector** in Hallo storage-account.</span><span class="sxs-lookup"><span data-stu-id="658ed-364">Create a blob container named **adfblobconnector** in hello storage account.</span></span> 
4. <span data-ttu-id="658ed-365">Maak een map met de naam **invoer** in Hallo **adfblobconnector** container.</span><span class="sxs-lookup"><span data-stu-id="658ed-365">Create a folder named **input** in hello **adfblobconnector** container.</span></span>
5. <span data-ttu-id="658ed-366">Maak een bestand met de naam **emp.txt** Hello na inhoud en upload het toohello **invoer** map met hulpprogramma's zoals [Azure Opslagverkenner](https://azurestorageexplorer.codeplex.com/)</span><span class="sxs-lookup"><span data-stu-id="658ed-366">Create a file named **emp.txt** with hello following content and upload it toohello **input** folder by using tools such as [Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/)</span></span>
    ```json
    John, Doe
    Jane, Doe
    ```
### <a name="create-hello-data-factory"></a><span data-ttu-id="658ed-367">Hallo een gegevensfactory maken</span><span class="sxs-lookup"><span data-stu-id="658ed-367">Create hello data factory</span></span>
1. <span data-ttu-id="658ed-368">Meld u aan toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="658ed-368">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="658ed-369">Klik op **+ nieuw** van de linkerbovenhoek hello, klikt u op **Intelligence en analyse**, en klik op **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="658ed-369">Click **+ NEW** from hello top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="658ed-370">In Hallo **nieuwe gegevensfactory** blade:</span><span class="sxs-lookup"><span data-stu-id="658ed-370">In hello **New data factory** blade:</span></span>   
    1. <span data-ttu-id="658ed-371">Voer **ADFBlobConnectorDF** voor Hallo **naam**.</span><span class="sxs-lookup"><span data-stu-id="658ed-371">Enter **ADFBlobConnectorDF** for hello **name**.</span></span> <span data-ttu-id="658ed-372">Hallo-naam van hello Azure-gegevensfactory moet wereldwijd uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="658ed-372">hello name of hello Azure data factory must be globally unique.</span></span> <span data-ttu-id="658ed-373">Als u de foutmelding Hallo: `*Data factory name “ADFBlobConnectorDF” is not available`, wijzigt Hallo-naam van gegevensfactory hello (bijvoorbeeld yournameADFBlobConnectorDF) en probeert u het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="658ed-373">If you receive hello error: `*Data factory name “ADFBlobConnectorDF” is not available`, change hello name of hello data factory (for example, yournameADFBlobConnectorDF) and try creating again.</span></span> <span data-ttu-id="658ed-374">Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.</span><span class="sxs-lookup"><span data-stu-id="658ed-374">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
    2. <span data-ttu-id="658ed-375">Selecteer uw Azure-**abonnement**.</span><span class="sxs-lookup"><span data-stu-id="658ed-375">Select your Azure **subscription**.</span></span>
    3. <span data-ttu-id="658ed-376">Selecteer voor de resourcegroep **gebruik bestaande** tooselect een bestaande resource group (of) Selecteer **nieuw** tooenter een naam voor een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="658ed-376">For Resource Group, select **Use existing** tooselect an existing resource group (or) select **Create new** tooenter a name for a resource group.</span></span>
    4. <span data-ttu-id="658ed-377">Selecteer een **locatie** voor Hallo data factory.</span><span class="sxs-lookup"><span data-stu-id="658ed-377">Select a **location** for hello data factory.</span></span>
    5. <span data-ttu-id="658ed-378">Selecteer **pincode toodashboard** selectievakje onderaan Hallo Hallo-blade.</span><span class="sxs-lookup"><span data-stu-id="658ed-378">Select **Pin toodashboard** check box at hello bottom of hello blade.</span></span>
    6. <span data-ttu-id="658ed-379">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="658ed-379">Click **Create**.</span></span>
3. <span data-ttu-id="658ed-380">Nadat het maken van Hallo voltooid is, ziet u Hallo **Data Factory** blade zoals weergegeven in Hallo volgende afbeelding: ![Data factory-startpagina](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span><span class="sxs-lookup"><span data-stu-id="658ed-380">After hello creation is complete, you see hello **Data Factory** blade as shown in hello following image: ![Data factory home page](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span></span>

### <a name="copy-wizard"></a><span data-ttu-id="658ed-381">De wizard Kopiëren</span><span class="sxs-lookup"><span data-stu-id="658ed-381">Copy Wizard</span></span>
1. <span data-ttu-id="658ed-382">Op Hallo Data Factory-startpagina, klikt u op Hallo **kopiëren van gegevens [PREVIEW]** tegel toolaunch **Data-Wizard kopiëren** op een afzonderlijke tabblad.</span><span class="sxs-lookup"><span data-stu-id="658ed-382">On hello Data Factory home page, click hello **Copy data [PREVIEW]** tile toolaunch **Copy Data Wizard** in a separate tab.</span></span>    
    
    > [!NOTE]
    >    <span data-ttu-id="658ed-383">Als u ziet dat Hallo webbrowser is vastgelopen bij 'Autoriseren...', schakelt **blokkeren van cookies van derden en sitegegevens** instellen (of) laat dit ingeschakeld en maakt een uitzondering voor **login.microsoftonline.com**en probeer het opnieuw starten van Hallo-wizard.</span><span class="sxs-lookup"><span data-stu-id="658ed-383">If you see that hello web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching hello wizard again.</span></span>
2. <span data-ttu-id="658ed-384">In Hallo **eigenschappen** pagina:</span><span class="sxs-lookup"><span data-stu-id="658ed-384">In hello **Properties** page:</span></span>
    1. <span data-ttu-id="658ed-385">Voer **CopyPipeline** voor **taaknaam**.</span><span class="sxs-lookup"><span data-stu-id="658ed-385">Enter **CopyPipeline** for **Task name**.</span></span> <span data-ttu-id="658ed-386">Hallo-taaknaam is Hallo-naam van Hallo pijplijn in uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="658ed-386">hello task name is hello name of hello pipeline in your data factory.</span></span>
    2. <span data-ttu-id="658ed-387">Voer een **beschrijving** voor Hallo taak (optioneel).</span><span class="sxs-lookup"><span data-stu-id="658ed-387">Enter a **description** for hello task (optional).</span></span>
    3. <span data-ttu-id="658ed-388">Voor **taak uitgebracht of taakschema**, Hallo houden **regelmatig wordt uitgevoerd volgens schema** optie.</span><span class="sxs-lookup"><span data-stu-id="658ed-388">For **Task cadence or Task schedule**, keep hello **Run regularly on schedule** option.</span></span> <span data-ttu-id="658ed-389">Als u wilt dat deze taak slechts eenmaal in plaats van meerdere keren uitgevoerd volgens een schema toorun, selecteert u **eenmaal nu uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="658ed-389">If you want toorun this task only once instead of run repeatedly on a schedule, select **Run once now**.</span></span> <span data-ttu-id="658ed-390">Als u selecteert, **eenmaal nu uitvoeren** optie, een [eenmalige pijplijn](data-factory-create-pipelines.md#onetime-pipeline) wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="658ed-390">If you select, **Run once now** option, a [one-time pipeline](data-factory-create-pipelines.md#onetime-pipeline) is created.</span></span> 
    4. <span data-ttu-id="658ed-391">Hallo-instellingen voor bewaren **terugkerend patroon**.</span><span class="sxs-lookup"><span data-stu-id="658ed-391">Keep hello settings for **Recurring pattern**.</span></span> <span data-ttu-id="658ed-392">Deze taak dagelijks wordt uitgevoerd tussen Hallo beginnen en eindigen tijd in die u in de volgende stap Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="658ed-392">This task runs daily between hello start and end times you specify in hello next step.</span></span>
    5. <span data-ttu-id="658ed-393">Wijziging Hallo **begindatum tijd** te**21/04/2017**.</span><span class="sxs-lookup"><span data-stu-id="658ed-393">Change hello **Start date time** too**04/21/2017**.</span></span> 
    6. <span data-ttu-id="658ed-394">Wijziging Hallo **einddatum en-tijd** te**25/04/2017**.</span><span class="sxs-lookup"><span data-stu-id="658ed-394">Change hello **End date time** too**04/25/2017**.</span></span> <span data-ttu-id="658ed-395">U kunt tootype Hallo datum in plaats van het bladeren door Hallo kalender.</span><span class="sxs-lookup"><span data-stu-id="658ed-395">You may want tootype hello date instead of browsing through hello calendar.</span></span>     
    8. <span data-ttu-id="658ed-396">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="658ed-396">Click **Next**.</span></span>
      <span data-ttu-id="658ed-397">![Hulpprogramma voor kopiëren - pagina eigenschappen](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span><span class="sxs-lookup"><span data-stu-id="658ed-397">![Copy Tool - Properties page](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span></span> 
3. <span data-ttu-id="658ed-398">Op Hallo **brongegevensarchief** pagina, klikt u op **Azure Blob Storage** tegel.</span><span class="sxs-lookup"><span data-stu-id="658ed-398">On hello **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="658ed-399">U gebruikt deze pagina toospecify Hallo-brongegevensarchief voor Hallo kopieertaak.</span><span class="sxs-lookup"><span data-stu-id="658ed-399">You use this page toospecify hello source data store for hello copy task.</span></span> <span data-ttu-id="658ed-400">U kunt een bestaande gekoppelde service van een gegevensarchief gebruiken of een nieuw gegevensarchief opgeven.</span><span class="sxs-lookup"><span data-stu-id="658ed-400">You can use an existing data store linked service (or) specify a new data store.</span></span> <span data-ttu-id="658ed-401">toouse een bestaande gekoppelde service, selecteert u **van bestaande gekoppelde SERVICES** en selecteer Hallo juiste gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="658ed-401">toouse an existing linked service, you would select **FROM EXISTING LINKED SERVICES** and select hello right linked service.</span></span> 
    <span data-ttu-id="658ed-402">![Hulpprogramma voor kopiëren - brongegevensarchief](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span><span class="sxs-lookup"><span data-stu-id="658ed-402">![Copy Tool - Source data store page](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span></span>
4. <span data-ttu-id="658ed-403">Op Hallo **hello Azure Blob storage-account opgeven** pagina:</span><span class="sxs-lookup"><span data-stu-id="658ed-403">On hello **Specify hello Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="658ed-404">Hallo automatisch gegenereerde naam voor **verbindingsnaam**.</span><span class="sxs-lookup"><span data-stu-id="658ed-404">Keep hello auto-generated name for **Connection name**.</span></span> <span data-ttu-id="658ed-405">Hallo verbindingsnaam heet Hallo Hallo gekoppelde service van het type: Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="658ed-405">hello connection name is hello name of hello linked service of type: Azure Storage.</span></span> 
   2. <span data-ttu-id="658ed-406">Controleer of de optie **Van Azure-abonnementen** is geselecteerd als **accountselectiemethode**.</span><span class="sxs-lookup"><span data-stu-id="658ed-406">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="658ed-407">Selecteer uw Azure-abonnement of houden **Alles selecteren** voor **Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="658ed-407">Select your Azure subscription or keep **Select all** for **Azure subscription**.</span></span>   
   4. <span data-ttu-id="658ed-408">Selecteer een **Azure storage-account** van Hallo lijst met Azure storage accounts beschikbaar in het abonnement Hallo geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="658ed-408">Select an **Azure storage account** from hello list of Azure storage accounts available in hello selected subscription.</span></span> <span data-ttu-id="658ed-409">U kunt ook tooenter Opslaginstellingen account handmatig door het selecteren van **handmatig invoeren** optie voor Hallo **Accountselectiemethode**.</span><span class="sxs-lookup"><span data-stu-id="658ed-409">You can also choose tooenter storage account settings manually by selecting **Enter manually** option for hello **Account selection method**.</span></span>
   5. <span data-ttu-id="658ed-410">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="658ed-410">Click **Next**.</span></span> 
      <span data-ttu-id="658ed-411">![Hulpprogramma voor kopiëren - hello Azure Blob storage-account opgeven](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span><span class="sxs-lookup"><span data-stu-id="658ed-411">![Copy Tool - Specify hello Azure Blob storage account](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span></span>
5. <span data-ttu-id="658ed-412">Op **Kies Hallo invoerbestand of de map** pagina:</span><span class="sxs-lookup"><span data-stu-id="658ed-412">On **Choose hello input file or folder** page:</span></span>
   1. <span data-ttu-id="658ed-413">Dubbelklik op **adfblobcontainer**.</span><span class="sxs-lookup"><span data-stu-id="658ed-413">Double-click **adfblobcontainer**.</span></span>
   2. <span data-ttu-id="658ed-414">Selecteer **invoer**, en klik op **Kies**.</span><span class="sxs-lookup"><span data-stu-id="658ed-414">Select **input**, and click **Choose**.</span></span> <span data-ttu-id="658ed-415">In dit scenario maakt selecteren u de invoermap Hallo.</span><span class="sxs-lookup"><span data-stu-id="658ed-415">In this walkthrough, you select hello input folder.</span></span> <span data-ttu-id="658ed-416">U kunt ook selecteren Hallo emp.txt bestand in map Hallo in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="658ed-416">You could also select hello emp.txt file in hello folder instead.</span></span> 
      <span data-ttu-id="658ed-417">![Hulpprogramma voor kopiëren - Hallo invoerbestand of de invoermap kiezen](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="658ed-417">![Copy Tool - Choose hello input file or folder](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span></span>
6. <span data-ttu-id="658ed-418">Op Hallo **Kies Hallo invoerbestand of de map** pagina:</span><span class="sxs-lookup"><span data-stu-id="658ed-418">On hello **Choose hello input file or folder** page:</span></span>
    1. <span data-ttu-id="658ed-419">Bevestig dat Hallo **bestand of map** te is ingesteld,**adfblobconnector/invoer**.</span><span class="sxs-lookup"><span data-stu-id="658ed-419">Confirm that hello **file or folder** is set too**adfblobconnector/input**.</span></span> <span data-ttu-id="658ed-420">Als Hallo-bestanden in submappen, bijvoorbeeld 04-01-2017, 2017/04/02 en enzovoort, en geef adfblobconnector/invoer / {year} / {month} / {day} voor bestand of map.</span><span class="sxs-lookup"><span data-stu-id="658ed-420">If hello files are in sub folders, for example, 2017/04/01, 2017/04/02, and so on, enter adfblobconnector/input/{year}/{month}/{day} for file or folder.</span></span> <span data-ttu-id="658ed-421">Wanneer u op tabblad buiten het tekstvak hello, ziet u drie vervolgkeuzelijsten tooselect indelingen voor het jaar (jjjj), de maand (MM) en de dag (dd).</span><span class="sxs-lookup"><span data-stu-id="658ed-421">When you press TAB out of hello text box, you see three drop-down lists tooselect formats for year (yyyy), month (MM), and day (dd).</span></span> 
    2. <span data-ttu-id="658ed-422">Stel geen **kopiëren van bestand recursief**.</span><span class="sxs-lookup"><span data-stu-id="658ed-422">Do not set **Copy file recursively**.</span></span> <span data-ttu-id="658ed-423">Selecteer deze optie toorecursively bladeren door mappen voor bestanden toobe gekopieerde toohello doel.</span><span class="sxs-lookup"><span data-stu-id="658ed-423">Select this option toorecursively traverse through folders for files toobe copied toohello destination.</span></span> 
    3. <span data-ttu-id="658ed-424">Niet Hallo **binaire kopiëren** optie.</span><span class="sxs-lookup"><span data-stu-id="658ed-424">Do not hello **binary copy** option.</span></span> <span data-ttu-id="658ed-425">Selecteer deze optie tooperform een binaire kopie van de bron-bestand toohello doel.</span><span class="sxs-lookup"><span data-stu-id="658ed-425">Select this option tooperform a binary copy of source file toohello destination.</span></span> <span data-ttu-id="658ed-426">Selecteer niet voor dit scenario zodat u meer opties in de volgende pagina's Hallo kunt zien.</span><span class="sxs-lookup"><span data-stu-id="658ed-426">Do not select for this walkthrough so that you can see more options in hello next pages.</span></span> 
    4. <span data-ttu-id="658ed-427">Bevestig dat Hallo **compressietype** te is ingesteld,**geen**.</span><span class="sxs-lookup"><span data-stu-id="658ed-427">Confirm that hello **Compression type** is set too**None**.</span></span> <span data-ttu-id="658ed-428">Selecteer een waarde voor deze optie als de bronbestanden in een van Hallo ondersteunde indelingen zijn gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="658ed-428">Select a value for this option if your source files are compressed in one of hello supported formats.</span></span> 
    5. <span data-ttu-id="658ed-429">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="658ed-429">Click **Next**.</span></span>
    <span data-ttu-id="658ed-430">![Hulpprogramma voor kopiëren - Hallo invoerbestand of de invoermap kiezen](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span><span class="sxs-lookup"><span data-stu-id="658ed-430">![Copy Tool - Choose hello input file or folder](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span></span> 
7. <span data-ttu-id="658ed-431">Op Hallo **bestandsindelingsinstellingen** pagina ziet u Hallo scheidingstekens en het Hallo-schema die automatisch worden gedetecteerd door de wizard Hallo door parseren Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="658ed-431">On hello **File format settings** page, you see hello delimiters and hello schema that is auto-detected by hello wizard by parsing hello file.</span></span> 
    1. <span data-ttu-id="658ed-432">Bevestig Hallo volgende opties: een.</span><span class="sxs-lookup"><span data-stu-id="658ed-432">Confirm hello following options: a.</span></span> <span data-ttu-id="658ed-433">Hallo **bestandsindeling** te is ingesteld,**tekstindeling**.</span><span class="sxs-lookup"><span data-stu-id="658ed-433">hello **file format** is set too**Text format**.</span></span> <span data-ttu-id="658ed-434">U kunt alle Hallo ondersteund notaties in de vervolgkeuzelijst Hallo zien.</span><span class="sxs-lookup"><span data-stu-id="658ed-434">You can see all hello supported formats in hello drop-down list.</span></span> <span data-ttu-id="658ed-435">Bijvoorbeeld: JSON, Avro, ORC, parketvloeren.</span><span class="sxs-lookup"><span data-stu-id="658ed-435">For example: JSON, Avro, ORC, Parquet.</span></span>
        <span data-ttu-id="658ed-436">b.</span><span class="sxs-lookup"><span data-stu-id="658ed-436">b.</span></span> <span data-ttu-id="658ed-437">Hallo **kolomscheidingsteken** te is ingesteld`Comma (,)`.</span><span class="sxs-lookup"><span data-stu-id="658ed-437">hello **column delimiter** is set too`Comma (,)`.</span></span> <span data-ttu-id="658ed-438">U kunt zien andere kolom scheidingstekens die door Data Factory worden ondersteund in de vervolgkeuzelijst Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="658ed-438">You can see hello other column delimiters supported by Data Factory in hello drop-down list.</span></span> <span data-ttu-id="658ed-439">U kunt ook een aangepaste scheidingsteken opgeven.</span><span class="sxs-lookup"><span data-stu-id="658ed-439">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="658ed-440">c.</span><span class="sxs-lookup"><span data-stu-id="658ed-440">c.</span></span> <span data-ttu-id="658ed-441">Hallo **rijscheidingsteken** te is ingesteld`Carriage Return + Line feed (\r\n)`.</span><span class="sxs-lookup"><span data-stu-id="658ed-441">hello **row delimiter** is set too`Carriage Return + Line feed (\r\n)`.</span></span> <span data-ttu-id="658ed-442">U kunt zien andere rij scheidingstekens die door Data Factory worden ondersteund in de vervolgkeuzelijst Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="658ed-442">You can see hello other row delimiters supported by Data Factory in hello drop-down list.</span></span> <span data-ttu-id="658ed-443">U kunt ook een aangepaste scheidingsteken opgeven.</span><span class="sxs-lookup"><span data-stu-id="658ed-443">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="658ed-444">d.</span><span class="sxs-lookup"><span data-stu-id="658ed-444">d.</span></span> <span data-ttu-id="658ed-445">Hallo **aantal regels overslaan** te is ingesteld,**0**.</span><span class="sxs-lookup"><span data-stu-id="658ed-445">hello **skip line count** is set too**0**.</span></span> <span data-ttu-id="658ed-446">Als u een paar regels toobe overgeslagen Hallo boven aan het Hallo-bestand wilt, voert u hier Hallo-nummer.</span><span class="sxs-lookup"><span data-stu-id="658ed-446">If you want a few lines toobe skipped at hello top of hello file, enter hello number here.</span></span>
        <span data-ttu-id="658ed-447">e.</span><span class="sxs-lookup"><span data-stu-id="658ed-447">e.</span></span>  <span data-ttu-id="658ed-448">Hallo **eerste gegevensrij kolomnamen bevat** is niet ingesteld.</span><span class="sxs-lookup"><span data-stu-id="658ed-448">hello **first data row contains column names** is not set.</span></span> <span data-ttu-id="658ed-449">Selecteer deze optie als Hallo-bronbestanden kolomnamen in de eerste rij hello bevat.</span><span class="sxs-lookup"><span data-stu-id="658ed-449">If hello source files contain column names in hello first row, select this option.</span></span>
        <span data-ttu-id="658ed-450">f.</span><span class="sxs-lookup"><span data-stu-id="658ed-450">f.</span></span> <span data-ttu-id="658ed-451">Hallo **leeg kolomwaarde behandelen als null** optie is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="658ed-451">hello **treat empty column value as null** option is set.</span></span>
    2. <span data-ttu-id="658ed-452">Vouw **geavanceerde instellingen** toosee geavanceerde optie beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="658ed-452">Expand **Advanced settings** toosee advanced option available.</span></span>
    3. <span data-ttu-id="658ed-453">Aan de onderkant van de Hallo van Hallo pagina, Zie Hallo **preview** van gegevens van Hallo emp.txt bestand.</span><span class="sxs-lookup"><span data-stu-id="658ed-453">At hello bottom of hello page, see hello **preview** of data from hello emp.txt file.</span></span>
    4. <span data-ttu-id="658ed-454">Klik op **SCHEMA** tabblad die wizard voor het kopiëren van Hallo afgeleid door te kijken Hallo-gegevens in het bronbestand Hallo Hallo onder toosee Hallo schema.</span><span class="sxs-lookup"><span data-stu-id="658ed-454">Click **SCHEMA** tab at hello bottom toosee hello schema that hello copy wizard inferred by looking at hello data in hello source file.</span></span>
    5. <span data-ttu-id="658ed-455">Klik op **volgende** nadat u hello scheidingstekens bekijkt en een voorbeeld van gegevens.</span><span class="sxs-lookup"><span data-stu-id="658ed-455">Click **Next** after you review hello delimiters and preview data.</span></span>
    <span data-ttu-id="658ed-456">![Hulpprogramma voor kopiëren - bestandsindelingsinstellingen](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span><span class="sxs-lookup"><span data-stu-id="658ed-456">![Copy Tool - File format settings](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span></span>  
8. <span data-ttu-id="658ed-457">Op Hallo **bestemming gegevensarchief pagina**, selecteer **Azure Blob Storage**, en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="658ed-457">On hello **Destination data store page**, select **Azure Blob Storage**, and click **Next**.</span></span> <span data-ttu-id="658ed-458">Als beide Hallo bron- en doelserver gegevensarchieven in dit scenario gebruikt u hello Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="658ed-458">You are using hello Azure Blob Storage as both hello source and destination data stores in this walkthrough.</span></span>    
    <span data-ttu-id="658ed-459">![Hulpprogramma voor kopiëren - gegevensarchief van de doelserver selecteren](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span><span class="sxs-lookup"><span data-stu-id="658ed-459">![Copy Tool - select destination data store](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span></span>
9. <span data-ttu-id="658ed-460">Op **hello Azure Blob storage-account opgeven** pagina:</span><span class="sxs-lookup"><span data-stu-id="658ed-460">On **Specify hello Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="658ed-461">Voer **AzureStorageLinkedService** voor Hallo **verbindingsnaam** veld.</span><span class="sxs-lookup"><span data-stu-id="658ed-461">Enter **AzureStorageLinkedService** for hello **Connection name** field.</span></span>
   2. <span data-ttu-id="658ed-462">Controleer of de optie **Van Azure-abonnementen** is geselecteerd als **accountselectiemethode**.</span><span class="sxs-lookup"><span data-stu-id="658ed-462">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="658ed-463">Selecteer uw Azure-**abonnement**.</span><span class="sxs-lookup"><span data-stu-id="658ed-463">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="658ed-464">Selecteer uw Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="658ed-464">Select your Azure storage account.</span></span> 
   5. <span data-ttu-id="658ed-465">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="658ed-465">Click **Next**.</span></span>     
10. <span data-ttu-id="658ed-466">Op Hallo **Kies Hallo bestand of map uitvoer** pagina:</span><span class="sxs-lookup"><span data-stu-id="658ed-466">On hello **Choose hello output file or folder** page:</span></span> 
    6. <span data-ttu-id="658ed-467">Geef **mappad** als **adfblobconnector/uitvoer / {year} / {month} / {day}**.</span><span class="sxs-lookup"><span data-stu-id="658ed-467">specify **Folder path** as **adfblobconnector/output/{year}/{month}/{day}**.</span></span> <span data-ttu-id="658ed-468">Voer **tabblad**.</span><span class="sxs-lookup"><span data-stu-id="658ed-468">Enter **TAB**.</span></span>
    7. <span data-ttu-id="658ed-469">Voor Hallo **jaar**, selecteer **jjjj**.</span><span class="sxs-lookup"><span data-stu-id="658ed-469">For hello **year**, select **yyyy**.</span></span>
    8. <span data-ttu-id="658ed-470">Voor Hallo **maand**, Controleer te ingesteld**MM**.</span><span class="sxs-lookup"><span data-stu-id="658ed-470">For hello **month**, confirm that it is set too**MM**.</span></span>
    9. <span data-ttu-id="658ed-471">Voor Hallo **dag**, Controleer te ingesteld**dd**.</span><span class="sxs-lookup"><span data-stu-id="658ed-471">For hello **day**, confirm that it is set too**dd**.</span></span>
    10. <span data-ttu-id="658ed-472">Bevestig dat Hallo **compressietype** te is ingesteld,**geen**.</span><span class="sxs-lookup"><span data-stu-id="658ed-472">Confirm that hello **compression type** is set too**None**.</span></span>
    11. <span data-ttu-id="658ed-473">Bevestig dat Hallo **gedrag kopiëren** te is ingesteld,**bestanden samenvoegen**.</span><span class="sxs-lookup"><span data-stu-id="658ed-473">Confirm that hello **copy behavior** is set too**Merge files**.</span></span> <span data-ttu-id="658ed-474">Als Hallo uitvoerbestand met dezelfde naam al bestaat hello, is hello nieuwe inhoud toegevoegd toohello hetzelfde bestand aan Hallo einde.</span><span class="sxs-lookup"><span data-stu-id="658ed-474">If hello output file with hello same name already exists, hello new content is added toohello same file at hello end.</span></span>
    12. <span data-ttu-id="658ed-475">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="658ed-475">Click **Next**.</span></span>
    <span data-ttu-id="658ed-476">![Hulpprogramma voor kopiëren - bestand voor uitvoer of de invoermap kiezen](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="658ed-476">![Copy Tool - Choose output file or folder](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span></span>
11. <span data-ttu-id="658ed-477">Op Hallo **bestandsindelingsinstellingen** pagina, Hallo instellingen bekijken en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="658ed-477">On hello **File format settings** page, review hello settings, and click **Next**.</span></span> <span data-ttu-id="658ed-478">Een van de Hallo hier extra opties is tooadd een header toohello-uitvoerbestand.</span><span class="sxs-lookup"><span data-stu-id="658ed-478">One of hello additional options here is tooadd a header toohello output file.</span></span> <span data-ttu-id="658ed-479">Als u deze optie selecteert, wordt een veldnamenrij toegevoegd met namen van kolommen Hallo van Hallo-schema van Hallo bron.</span><span class="sxs-lookup"><span data-stu-id="658ed-479">If you select that option, a header row is added with names of hello columns from hello schema of hello source.</span></span> <span data-ttu-id="658ed-480">Wanneer u bekijkt hello schema voor Hallo bron, kunt u Hallo standaardkolomnamen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="658ed-480">You can rename hello default column names when viewing hello schema for hello source.</span></span> <span data-ttu-id="658ed-481">U kan bijvoorbeeld Hallo eerste kolom tooFirst naam en de tweede kolom tooLast naam wijzigen.</span><span class="sxs-lookup"><span data-stu-id="658ed-481">For example, you could change hello first column tooFirst Name and second column tooLast Name.</span></span> <span data-ttu-id="658ed-482">Hallo-bestand voor uitvoer wordt vervolgens gegenereerd met een header met deze namen als kolomnamen.</span><span class="sxs-lookup"><span data-stu-id="658ed-482">Then, hello output file is generated with a header with these names as column names.</span></span> 
    <span data-ttu-id="658ed-483">![Hulpprogramma voor kopiëren - bestandsindelingsinstellingen voor bestemming](media/data-factory-azure-blob-connector/file-format-destination.png)</span><span class="sxs-lookup"><span data-stu-id="658ed-483">![Copy Tool - File format settings for destination](media/data-factory-azure-blob-connector/file-format-destination.png)</span></span>
12. <span data-ttu-id="658ed-484">Op Hallo **prestatie-instellingen** pagina, controleert u of **eenheden cloud** en **kopieën parallelle** te zijn ingesteld**automatisch**, en klik op volgende.</span><span class="sxs-lookup"><span data-stu-id="658ed-484">On hello **Performance settings** page, confirm that **cloud units** and **parallel copies** are set too**Auto**, and click Next.</span></span> <span data-ttu-id="658ed-485">Zie voor meer informatie over deze instellingen [activiteit prestaties en prestatieafstemming handleiding kopiëren](data-factory-copy-activity-performance.md#parallel-copy).</span><span class="sxs-lookup"><span data-stu-id="658ed-485">For details about these settings, see [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md#parallel-copy).</span></span>
    <span data-ttu-id="658ed-486">![Hulpprogramma voor kopiëren - prestatie-instellingen](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span><span class="sxs-lookup"><span data-stu-id="658ed-486">![Copy Tool - Performance settings](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span></span> 
14. <span data-ttu-id="658ed-487">Op Hallo **samenvatting** pagina, controleert u alle instellingen (taakeigenschappen, instellingen voor de bron- en doelserver en instellingen) en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="658ed-487">On hello **Summary** page, review all settings (task properties, settings for source and destination, and copy settings), and click **Next**.</span></span>
    <span data-ttu-id="658ed-488">![Hulpprogramma voor kopiëren - pagina overzicht](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span><span class="sxs-lookup"><span data-stu-id="658ed-488">![Copy Tool - Summary page](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span></span>
15. <span data-ttu-id="658ed-489">Bekijk de informatie in Hallo **samenvatting** pagina en klik op **voltooien**.</span><span class="sxs-lookup"><span data-stu-id="658ed-489">Review information in hello **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="658ed-490">Hallo-wizard maakt twee gekoppelde services, twee gegevenssets (invoer en uitvoer) en één pijplijn in de gegevensfactory hello (van waaruit u Hallo Wizard kopiëren hebt gestart).</span><span class="sxs-lookup"><span data-stu-id="658ed-490">hello wizard creates two linked services, two datasets (input and output), and one pipeline in hello data factory (from where you launched hello Copy Wizard).</span></span>
    <span data-ttu-id="658ed-491">![Hulpprogramma voor kopiëren - pagina van de implementatie](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span><span class="sxs-lookup"><span data-stu-id="658ed-491">![Copy Tool - Deployment page](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span></span>

### <a name="monitor-hello-pipeline-copy-task"></a><span data-ttu-id="658ed-492">De pijplijn bewaken hello (taak kopiëren)</span><span class="sxs-lookup"><span data-stu-id="658ed-492">Monitor hello pipeline (copy task)</span></span>

1. <span data-ttu-id="658ed-493">Klik op de koppeling Hallo `Click here toomonitor copy pipeline` op Hallo **implementatie** pagina.</span><span class="sxs-lookup"><span data-stu-id="658ed-493">Click hello link `Click here toomonitor copy pipeline` on hello **Deployment** page.</span></span> 
2. <span data-ttu-id="658ed-494">U ziet Hallo **bewaken en beheren van de toepassing** op een afzonderlijke tabblad.  ![Bewaken en beheren van App](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span><span class="sxs-lookup"><span data-stu-id="658ed-494">You should see hello **Monitor and Manage application** in a separate tab.  ![Monitor and Manage App](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span></span>
3. <span data-ttu-id="658ed-495">Wijziging Hallo **start** tijd Hallo boven te`04/19/2017` en **end** tijd te`04/27/2017`, en klik vervolgens op **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="658ed-495">Change hello **start** time at hello top too`04/19/2017` and **end** time too`04/27/2017`, and then click **Apply**.</span></span> 
4. <span data-ttu-id="658ed-496">Ziet u vijf activiteitsvensters in Hallo **ACTIVITEITSVENSTERS** lijst.</span><span class="sxs-lookup"><span data-stu-id="658ed-496">You should see five activity windows in hello **ACTIVITY WINDOWS** list.</span></span> <span data-ttu-id="658ed-497">Hallo **WindowStart** tijden moeten voldoende zijn voor alle dagen van de pijplijn start toopipeline eindtijden.</span><span class="sxs-lookup"><span data-stu-id="658ed-497">hello **WindowStart** times should cover all days from pipeline start toopipeline end times.</span></span> 
5. <span data-ttu-id="658ed-498">Klik op **vernieuwen** knop voor Hallo **ACTIVITEITSVENSTERS** lijst een paar keer totdat er status van alle Hallo activiteit windows hello tooReady is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="658ed-498">Click **Refresh** button for hello **ACTIVITY WINDOWS** list a few times until you see hello status of all hello activity windows is set tooReady.</span></span> 
6. <span data-ttu-id="658ed-499">Controleer nu of dat de uitvoerbestanden Hallo worden gegenereerd in de uitvoermap Hallo van adfblobconnector container.</span><span class="sxs-lookup"><span data-stu-id="658ed-499">Now, verify that hello output files are generated in hello output folder of adfblobconnector container.</span></span> <span data-ttu-id="658ed-500">U ziet de volgende mapstructuur in de uitvoermap Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="658ed-500">You should see hello following folder structure in hello output folder:</span></span> 
    ```
    2017/04/21
    2017/04/22
    2017/04/23
    2017/04/24
    2017/04/25    
    ```
<span data-ttu-id="658ed-501">Zie voor gedetailleerde informatie over het controleren en beheren van gegevensfactory [bewaken en beheren van de Data Factory-pijplijn](data-factory-monitor-manage-app.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="658ed-501">For detailed information about monitoring and managing data factories, see [Monitor and manage Data Factory pipeline](data-factory-monitor-manage-app.md) article.</span></span> 
 
### <a name="data-factory-entities"></a><span data-ttu-id="658ed-502">Data Factory-entiteiten</span><span class="sxs-lookup"><span data-stu-id="658ed-502">Data Factory entities</span></span>
<span data-ttu-id="658ed-503">Nu switch back toohello tabblad met Hallo Data Factory-startpagina.</span><span class="sxs-lookup"><span data-stu-id="658ed-503">Now, switch back toohello tab with hello Data Factory home page.</span></span> <span data-ttu-id="658ed-504">U ziet dat er twee gekoppelde services, twee gegevenssets en een pijplijn in uw data factory nu zijn.</span><span class="sxs-lookup"><span data-stu-id="658ed-504">Notice that there are two linked services, two datasets, and one pipeline in your data factory now.</span></span> 

![Data Factory-startpagina met entiteiten](media/data-factory-azure-blob-connector/data-factory-home-page-with-numbers.png)

<span data-ttu-id="658ed-506">Klik op **auteur en implementeren van** toolaunch Data Factory-Editor.</span><span class="sxs-lookup"><span data-stu-id="658ed-506">Click **Author and deploy** toolaunch Data Factory Editor.</span></span> 

![Data Factory Editor](media/data-factory-azure-blob-connector/data-factory-editor.png)

<span data-ttu-id="658ed-508">U ziet Hallo Data Factory-entiteiten in uw data factory te volgen:</span><span class="sxs-lookup"><span data-stu-id="658ed-508">You should see hello following Data Factory entities in your data factory:</span></span> 

 - <span data-ttu-id="658ed-509">Twee gekoppelde services.</span><span class="sxs-lookup"><span data-stu-id="658ed-509">Two linked services.</span></span> <span data-ttu-id="658ed-510">Een voor Hallo bron- en Hallo andere voor Hallo bestemming.</span><span class="sxs-lookup"><span data-stu-id="658ed-510">One for hello source and hello other one for hello destination.</span></span> <span data-ttu-id="658ed-511">Beide Hallo gekoppelde services verwijzen toohello dezelfde Azure-opslagaccount in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="658ed-511">Both hello linked services refer toohello same Azure Storage account in this walkthrough.</span></span> 
 - <span data-ttu-id="658ed-512">Twee gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="658ed-512">Two datasets.</span></span> <span data-ttu-id="658ed-513">Een invoergegevensset en een uitvoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="658ed-513">An input dataset and an output dataset.</span></span> <span data-ttu-id="658ed-514">In dit scenario maken beide gebruik Hallo dezelfde blob-container, maar verwijzen toodifferent mappen (invoer en uitvoer).</span><span class="sxs-lookup"><span data-stu-id="658ed-514">In this walkthrough, both use hello same blob container but refer toodifferent folders (input and output).</span></span>
 - <span data-ttu-id="658ed-515">Een pijplijn.</span><span class="sxs-lookup"><span data-stu-id="658ed-515">A pipeline.</span></span> <span data-ttu-id="658ed-516">Hallo pijplijn bevat een kopieeractiviteit die gebruikmaakt van een blob-bron- en een blob sink toocopy-gegevens van een Azure-blobopslag locatie tooanother Azure blob-locatie.</span><span class="sxs-lookup"><span data-stu-id="658ed-516">hello pipeline contains a copy activity that uses a blob source and a blob sink toocopy data from an Azure blob location tooanother Azure blob location.</span></span> 

<span data-ttu-id="658ed-517">Hallo bevatten volgende secties meer informatie over deze entiteiten.</span><span class="sxs-lookup"><span data-stu-id="658ed-517">hello following sections provide more information about these entities.</span></span> 

#### <a name="linked-services"></a><span data-ttu-id="658ed-518">Gekoppelde services</span><span class="sxs-lookup"><span data-stu-id="658ed-518">Linked services</span></span>
<span data-ttu-id="658ed-519">Hier ziet u twee gekoppelde services.</span><span class="sxs-lookup"><span data-stu-id="658ed-519">You should see two linked services.</span></span> <span data-ttu-id="658ed-520">Een voor Hallo bron- en Hallo andere voor Hallo bestemming.</span><span class="sxs-lookup"><span data-stu-id="658ed-520">One for hello source and hello other one for hello destination.</span></span> <span data-ttu-id="658ed-521">In dit overzicht Hallo beide uiterlijk definities dezelfde behalve Hallo namen.</span><span class="sxs-lookup"><span data-stu-id="658ed-521">In this walkthrough, both definitions look hello same except for hello names.</span></span> <span data-ttu-id="658ed-522">Hallo **type** Hallo gekoppelde service te ingesteld**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="658ed-522">hello **type** of hello linked service is set too**AzureStorage**.</span></span> <span data-ttu-id="658ed-523">Belangrijkste eigenschap van de servicedefinitie Hallo gekoppeld is Hallo **connectionString**, die wordt gebruikt door de Data Factory tooconnect tooyour Azure Storage-account tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="658ed-523">Most important property of hello linked service definition is hello **connectionString**, which is used by Data Factory tooconnect tooyour Azure Storage account at runtime.</span></span> <span data-ttu-id="658ed-524">Hallo hubName eigenschap in de definitie van de Hallo negeren.</span><span class="sxs-lookup"><span data-stu-id="658ed-524">Ignore hello hubName property in hello definition.</span></span> 

##### <a name="source-blob-storage-linked-service"></a><span data-ttu-id="658ed-525">Bron blob-opslag gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="658ed-525">Source blob storage linked service</span></span>
```json
{
    "name": "Source-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

##### <a name="destination-blob-storage-linked-service"></a><span data-ttu-id="658ed-526">Bestemming blob-opslag gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="658ed-526">Destination blob storage linked service</span></span>

```json
{
    "name": "Destination-BlobStorage-z4y",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=mystorageaccount;AccountKey=**********"
        }
    }
}
```

<span data-ttu-id="658ed-527">Zie voor meer informatie over Azure Storage gekoppelde service [gekoppelde service-eigenschappen](#linked-service-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="658ed-527">For more information about Azure Storage linked service, see [Linked service properties](#linked-service-properties) section.</span></span> 

#### <a name="datasets"></a><span data-ttu-id="658ed-528">Gegevenssets</span><span class="sxs-lookup"><span data-stu-id="658ed-528">Datasets</span></span>
<span data-ttu-id="658ed-529">Er zijn twee gegevenssets: een invoergegevensset en een uitvoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="658ed-529">There are two datasets: an input dataset and an output dataset.</span></span> <span data-ttu-id="658ed-530">Hallo type Hallo gegevensset te is ingesteld**AzureBlob** voor beide.</span><span class="sxs-lookup"><span data-stu-id="658ed-530">hello type of hello dataset is set too**AzureBlob** for both.</span></span> 

<span data-ttu-id="658ed-531">Hallo invoergegevensset verwijst toohello **invoer** map Hallo **adfblobconnector** blob-container.</span><span class="sxs-lookup"><span data-stu-id="658ed-531">hello input dataset points toohello **input** folder of hello **adfblobconnector** blob container.</span></span> <span data-ttu-id="658ed-532">Hallo **externe** eigenschap is ingesteld, te**true** voor deze gegevensset als Hallo gegevens wordt niet gemaakt door Hallo pijplijn met de Hallo kopieeractiviteit waarmee deze dataset als invoer.</span><span class="sxs-lookup"><span data-stu-id="658ed-532">hello **external** property is set too**true** for this dataset as hello data is not produced by hello pipeline with hello copy activity that takes this dataset as an input.</span></span> 

<span data-ttu-id="658ed-533">Hallo output dataset punten toohello **uitvoer** map Hallo dezelfde blob-container.</span><span class="sxs-lookup"><span data-stu-id="658ed-533">hello output dataset points toohello **output** folder of hello same blob container.</span></span> <span data-ttu-id="658ed-534">Hallo uitvoergegevensset gebruikt ook Hallo jaar, maand en dag Hallo **SliceStart** system variabele toodynamically Hallo pad voor het uitvoerbestand Hallo evalueren.</span><span class="sxs-lookup"><span data-stu-id="658ed-534">hello output dataset also uses hello year, month, and day of hello **SliceStart** system variable toodynamically evaluate hello path for hello output file.</span></span> <span data-ttu-id="658ed-535">Zie voor een lijst met functies en ondersteund door Data Factory systeemvariabelen [Data Factory-functies en systeemvariabelen](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="658ed-535">For a list of functions and system variables supported by Data Factory, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span> <span data-ttu-id="658ed-536">Hallo **externe** eigenschap is ingesteld, te**false** (standaardwaarde) omdat deze gegevensset wordt geproduceerd door Hallo pijplijn.</span><span class="sxs-lookup"><span data-stu-id="658ed-536">hello **external** property is set too**false** (default value) because this dataset is produced by hello pipeline.</span></span> 

<span data-ttu-id="658ed-537">Zie voor meer informatie over de eigenschappen die worden ondersteund door Azure Blob-gegevensset [eigenschappen van gegevensset](#dataset-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="658ed-537">For more information about properties supported by Azure Blob dataset, see [Dataset properties](#dataset-properties) section.</span></span>

##### <a name="input-dataset"></a><span data-ttu-id="658ed-538">Invoergegevensset</span><span class="sxs-lookup"><span data-stu-id="658ed-538">Input dataset</span></span>

```json
{
    "name": "InputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Source-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/input/",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```

##### <a name="output-dataset"></a><span data-ttu-id="658ed-539">Uitvoergegevensset</span><span class="sxs-lookup"><span data-stu-id="658ed-539">Output dataset</span></span>

```json
{
    "name": "OutputDataset-z4y",
    "properties": {
        "structure": [
            { "name": "Prop_0", "type": "String" },
            { "name": "Prop_1", "type": "String" }
        ],
        "type": "AzureBlob",
        "linkedServiceName": "Destination-BlobStorage-z4y",
        "typeProperties": {
            "folderPath": "adfblobconnector/output/{year}/{month}/{day}",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            },
            "partitionedBy": [
                { "name": "year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
                { "name": "month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
                { "name": "day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } }
            ]
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

#### <a name="pipeline"></a><span data-ttu-id="658ed-540">Pijplijn</span><span class="sxs-lookup"><span data-stu-id="658ed-540">Pipeline</span></span>
<span data-ttu-id="658ed-541">Hallo pipeline heeft slechts één activiteit.</span><span class="sxs-lookup"><span data-stu-id="658ed-541">hello pipeline has just one activity.</span></span> <span data-ttu-id="658ed-542">Hallo **type** Hallo activiteit te ingesteld**kopie**.</span><span class="sxs-lookup"><span data-stu-id="658ed-542">hello **type** of hello activity is set too**Copy**.</span></span>  <span data-ttu-id="658ed-543">In Hallo type-eigenschappen voor Hallo activiteit zijn er twee secties, één voor de bron- en Hallo andere voor sink.</span><span class="sxs-lookup"><span data-stu-id="658ed-543">In hello type properties for hello activity, there are two sections, one for source and hello other one for sink.</span></span> <span data-ttu-id="658ed-544">type Hello te is ingesteld**BlobSource** zoals Hallo activiteit van gegevens van een blob-opslag kopiëren.</span><span class="sxs-lookup"><span data-stu-id="658ed-544">hello source type is set too**BlobSource** as hello activity is copying data from a blob storage.</span></span> <span data-ttu-id="658ed-545">Hallo sink-type is ingesteld te**BlobSink** als Hallo activiteit kopiëren van gegevens tooa blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="658ed-545">hello sink type is set too**BlobSink** as hello activity copying data tooa blob storage.</span></span> <span data-ttu-id="658ed-546">Hallo kopieeractiviteit Neem InputDataset z4y als Hallo invoer- en OutputDataset-z4y als Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="658ed-546">hello copy activity takes InputDataset-z4y as hello input and OutputDataset-z4y as hello output.</span></span> 

<span data-ttu-id="658ed-547">Zie voor meer informatie over de eigenschappen die worden ondersteund door BlobSource en BlobSink [activiteitseigenschappen kopiëren](#copy-activity-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="658ed-547">For more information about properties supported by BlobSource and BlobSink, see [Copy activity properties](#copy-activity-properties) section.</span></span> 

```json
{
    "name": "CopyPipeline",
    "properties": {
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "BlobSource",
                        "recursive": false
                    },
                    "sink": {
                        "type": "BlobSink",
                        "copyBehavior": "MergeFiles",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "InputDataset-z4y"
                    }
                ],
                "outputs": [
                    {
                        "name": "OutputDataset-z4y"
                    }
                ],
                "policy": {
                    "timeout": "1.00:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "style": "StartOfInterval",
                    "retry": 3,
                    "longRetry": 0,
                    "longRetryInterval": "00:00:00"
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "Activity-0-Blob path_ adfblobconnector_input_->OutputDataset-z4y"
            }
        ],
        "start": "2017-04-21T22:34:00Z",
        "end": "2017-04-25T05:00:00Z",
        "isPaused": false,
        "pipelineMode": "Scheduled"
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-blob-storage"></a><span data-ttu-id="658ed-548">JSON-voorbeelden voor het kopiëren van gegevens tooand van Blob-opslag</span><span class="sxs-lookup"><span data-stu-id="658ed-548">JSON examples for copying data tooand from Blob Storage</span></span>  
<span data-ttu-id="658ed-549">Hallo volgende voorbeelden geven voorbeeld JSON definities waarmee u een pijplijn toocreate kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="658ed-549">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="658ed-550">Ze geven weer hoe toocopy gegevens tooand uit Azure Blob Storage en Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="658ed-550">They show how toocopy data tooand from Azure Blob Storage and Azure SQL Database.</span></span> <span data-ttu-id="658ed-551">Echter gegevens kunnen worden gekopieerd **rechtstreeks** uit een van de bronnen tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="658ed-551">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

### <a name="json-example-copy-data-from-blob-storage-toosql-database"></a><span data-ttu-id="658ed-552">JSON-voorbeeld: Gegevens kopiëren van Blob Storage tooSQL Database</span><span class="sxs-lookup"><span data-stu-id="658ed-552">JSON Example: Copy data from Blob Storage tooSQL Database</span></span>
<span data-ttu-id="658ed-553">Hallo volgende ziet:</span><span class="sxs-lookup"><span data-stu-id="658ed-553">hello following sample shows:</span></span>

1. <span data-ttu-id="658ed-554">Een gekoppelde service van het type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="658ed-554">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="658ed-555">Een gekoppelde service van het type [AzureStorage](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="658ed-555">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="658ed-556">Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="658ed-556">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
4. <span data-ttu-id="658ed-557">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="658ed-557">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="658ed-558">Een [pijplijn](data-factory-create-pipelines.md) met een kopieeractiviteit die gebruikmaakt van [BlobSource](#copy-activity-properties) en [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="658ed-558">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [BlobSource](#copy-activity-properties) and [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="658ed-559">Hallo voorbeeld kopieert timeseries gegevens uit een Azure-blobopslag tooan Azure SQL-tabel per uur.</span><span class="sxs-lookup"><span data-stu-id="658ed-559">hello sample copies time-series data from an Azure blob tooan Azure SQL table hourly.</span></span> <span data-ttu-id="658ed-560">Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="658ed-560">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="658ed-561">**Azure SQL gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="658ed-561">**Azure SQL linked service:**</span></span>

```json
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
<span data-ttu-id="658ed-562">**Gekoppelde Azure Storage-service:**</span><span class="sxs-lookup"><span data-stu-id="658ed-562">**Azure Storage linked service:**</span></span>

```json
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
<span data-ttu-id="658ed-563">Azure Data Factory ondersteunt twee soorten gekoppelde Azure Storage-services: **AzureStorage** en **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="658ed-563">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="658ed-564">Hallo voor eerste, u Hallo verbindingsreeks met Hallo accountsleutel opgeven en voor latere Hallo, u Hallo Shared Access Signature (SAS)-Uri opgeven.</span><span class="sxs-lookup"><span data-stu-id="658ed-564">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="658ed-565">Zie [gekoppelde Services](#linked-service-properties) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="658ed-565">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="658ed-566">**Azure Blob invoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="658ed-566">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="658ed-567">Gegevens wordt opgehaald uit een nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="658ed-567">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="658ed-568">Hallo map pad en de naam voor de blob Hallo worden dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="658ed-568">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="658ed-569">Hallo mappad jaar, maand en dag deel uit van de begintijd Hallo en bestandsnaam gebruikt Hallo uur deel uit van de begintijd Hallo.</span><span class="sxs-lookup"><span data-stu-id="658ed-569">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="658ed-570">"extern": "true" instelling informeert Data Factory die tabel Hallo externe toohello data factory is en niet wordt geproduceerd door een activiteit in de gegevensfactory Hallo.</span><span class="sxs-lookup"><span data-stu-id="658ed-570">“external”: “true” setting informs Data Factory that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
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
<span data-ttu-id="658ed-571">**Azure SQL-uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="658ed-571">**Azure SQL output dataset:**</span></span>

<span data-ttu-id="658ed-572">Hallo voorbeeld kopieert gegevens tooa tabel "MijnTabel" in een Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="658ed-572">hello sample copies data tooa table named “MyTable” in an Azure SQL database.</span></span> <span data-ttu-id="658ed-573">Hallo-tabel maken in uw Azure SQL database met hetzelfde aantal kolommen Hallo zoals Hallo Blob CSV-bestand toocontain verwacht.</span><span class="sxs-lookup"><span data-stu-id="658ed-573">Create hello table in your Azure SQL database with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="658ed-574">Nieuwe rijen worden toohello tabel toegevoegd om het uur.</span><span class="sxs-lookup"><span data-stu-id="658ed-574">New rows are added toohello table every hour.</span></span>

```json
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
<span data-ttu-id="658ed-575">**Een kopieeractiviteit in een pijplijn met Blob-bron en sink SQL:**</span><span class="sxs-lookup"><span data-stu-id="658ed-575">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="658ed-576">Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur.</span><span class="sxs-lookup"><span data-stu-id="658ed-576">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="658ed-577">Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**BlobSource** en **sink** type is ingesteld, te**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="658ed-577">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

```json
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
            "type": "BlobSource"
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
### <a name="json-example-copy-data-from-azure-sql-tooazure-blob"></a><span data-ttu-id="658ed-578">JSON-voorbeeld: Gegevens kopiëren van Azure SQL tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="658ed-578">JSON Example: Copy data from Azure SQL tooAzure Blob</span></span>
<span data-ttu-id="658ed-579">Hallo volgende ziet:</span><span class="sxs-lookup"><span data-stu-id="658ed-579">hello following sample shows:</span></span>

1. <span data-ttu-id="658ed-580">Een gekoppelde service van het type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="658ed-580">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="658ed-581">Een gekoppelde service van het type [AzureStorage](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="658ed-581">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="658ed-582">Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="658ed-582">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="658ed-583">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="658ed-583">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
5. <span data-ttu-id="658ed-584">Een [pijplijn](data-factory-create-pipelines.md) met de kopieeractiviteit die gebruikmaakt van [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) en [BlobSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="658ed-584">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) and [BlobSink](#copy-activity-properties).</span></span>

<span data-ttu-id="658ed-585">Hallo voorbeeld kopieert timeseries gegevens van een Azure SQL-tabel tooan Azure blob per uur.</span><span class="sxs-lookup"><span data-stu-id="658ed-585">hello sample copies time-series data from an Azure SQL table tooan Azure blob hourly.</span></span> <span data-ttu-id="658ed-586">Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="658ed-586">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="658ed-587">**Azure SQL gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="658ed-587">**Azure SQL linked service:**</span></span>

```json
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
<span data-ttu-id="658ed-588">**Gekoppelde Azure Storage-service:**</span><span class="sxs-lookup"><span data-stu-id="658ed-588">**Azure Storage linked service:**</span></span>

```json
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
<span data-ttu-id="658ed-589">Azure Data Factory ondersteunt twee soorten gekoppelde Azure Storage-services: **AzureStorage** en **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="658ed-589">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="658ed-590">Hallo voor eerste, u Hallo verbindingsreeks met Hallo accountsleutel opgeven en voor latere Hallo, u Hallo Shared Access Signature (SAS)-Uri opgeven.</span><span class="sxs-lookup"><span data-stu-id="658ed-590">For hello first one, you specify hello connection string that includes hello account key and for hello later one, you specify hello Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="658ed-591">Zie [gekoppelde Services](#linked-service-properties) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="658ed-591">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="658ed-592">**Azure SQL invoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="658ed-592">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="658ed-593">Hallo-voorbeeld wordt ervan uitgegaan dat u hebt een tabel 'MijnTabel' gemaakt in Azure SQL en bevat een kolom met de naam 'timestampcolumn' voor de reeksgegevens.</span><span class="sxs-lookup"><span data-stu-id="658ed-593">hello sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="658ed-594">Instelling 'extern': 'true' informeert Data Factory-service die tabel Hallo externe toohello data factory is en niet wordt geproduceerd door een activiteit in de gegevensfactory Hallo.</span><span class="sxs-lookup"><span data-stu-id="658ed-594">Setting “external”: ”true” informs Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
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

<span data-ttu-id="658ed-595">**Azure Blob-uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="658ed-595">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="658ed-596">Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="658ed-596">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="658ed-597">pad naar map voor blob Hallo Hallo wordt dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="658ed-597">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="658ed-598">Hallo mappad jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="658ed-598">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
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
          "value": { "type": "DateTime",  "date": "SliceStart", "format": "yyyy" } },
        { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
        { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
        { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "HH" } }
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

<span data-ttu-id="658ed-599">**Een kopieeractiviteit in een pijplijn met de SQL-bron en sink van Blob:**</span><span class="sxs-lookup"><span data-stu-id="658ed-599">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="658ed-600">Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur.</span><span class="sxs-lookup"><span data-stu-id="658ed-600">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="658ed-601">Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**SqlSource** en **sink** type is ingesteld, te**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="658ed-601">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="658ed-602">Hallo SQL-query is opgegeven voor Hallo **SqlReaderQuery** eigenschap Hallo gegevens selecteert in Hallo voorbij toocopy uur.</span><span class="sxs-lookup"><span data-stu-id="658ed-602">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```json
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

> [!NOTE]
> <span data-ttu-id="658ed-603">toomap kolommen uit de bron gegevensset toocolumns uit sink gegevensset, Zie [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="658ed-603">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="658ed-604">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="658ed-604">Performance and Tuning</span></span>
<span data-ttu-id="658ed-605">Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.</span><span class="sxs-lookup"><span data-stu-id="658ed-605">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
