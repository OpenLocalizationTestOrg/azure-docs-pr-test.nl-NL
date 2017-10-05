---
title: "Gegevens kopiëren naar/van Azure Blob Storage | Microsoft Docs"
description: "Informatie over het kopiëren van blob-gegevens in Azure Data Factory. Gebruik onze voorbeeld: gegevens kopiëren naar en van Azure Blob Storage en Azure SQL Database."
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
ms.openlocfilehash: 2cf955b52010869a4e753c441e17bdd32fd2e63d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="copy-data-to-or-from-azure-blob-storage-using-azure-data-factory"></a><span data-ttu-id="c4fd0-105">Kopiëren van gegevens of naar Azure Blob Storage met Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="c4fd0-105">Copy data to or from Azure Blob Storage using Azure Data Factory</span></span>
<span data-ttu-id="c4fd0-106">In dit artikel wordt uitgelegd hoe de Kopieeractiviteit in Azure Data Factory om gegevens te kopiëren naar en van Azure Blob Storage gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-106">This article explains how to use the Copy Activity in Azure Data Factory to copy data to and from Azure Blob Storage.</span></span> <span data-ttu-id="c4fd0-107">Dit is gebaseerd op de [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, hetgeen een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit toont.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-107">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

## <a name="overview"></a><span data-ttu-id="c4fd0-108">Overzicht</span><span class="sxs-lookup"><span data-stu-id="c4fd0-108">Overview</span></span>
<span data-ttu-id="c4fd0-109">U kunt gegevens kopiëren van alle ondersteunde brongegevensarchief naar Azure Blob Storage of Azure Blob Storage met alle ondersteunde sink-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-109">You can copy data from any supported source data store to Azure Blob Storage or from Azure Blob Storage to any supported sink data store.</span></span> <span data-ttu-id="c4fd0-110">De volgende tabel geeft een lijst van gegevensarchieven ondersteund als bronnen of sinks door met de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-110">The following table provides a list of data stores supported as sources or sinks by the copy activity.</span></span> <span data-ttu-id="c4fd0-111">U kunt bijvoorbeeld gegevens verplaatsen **van** een SQL Server-database of een Azure SQL database **naar** Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-111">For example, you can move data **from** a SQL Server database or an Azure SQL database **to** an Azure blob storage.</span></span> <span data-ttu-id="c4fd0-112">En u kunt gegevens kopiëren **van** Azure blob-opslag **naar** een Azure SQL Data Warehouse of een verzameling Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-112">And, you can copy data **from** Azure blob storage **to** an Azure SQL Data Warehouse or an Azure Cosmos DB collection.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="c4fd0-113">Ondersteunde scenario 's</span><span class="sxs-lookup"><span data-stu-id="c4fd0-113">Supported scenarios</span></span>
<span data-ttu-id="c4fd0-114">U kunt gegevens kopiëren **uit Azure Blob Storage** opslaat in de volgende gegevens:</span><span class="sxs-lookup"><span data-stu-id="c4fd0-114">You can copy data **from Azure Blob Storage** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="c4fd0-115">U kunt gegevens kopiëren van de volgende gegevensarchieven **naar Azure Blob Storage**:</span><span class="sxs-lookup"><span data-stu-id="c4fd0-115">You can copy data from the following data stores **to Azure Blob Storage**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]
 
> [!IMPORTANT]
> <span data-ttu-id="c4fd0-116">Kopieeractiviteit ondersteunt kopiëren van gegevens van/naar zowel algemeen Azure Storage-accounts als Hot/Cool Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-116">Copy Activity supports copying data from/to both general-purpose Azure Storage accounts and Hot/Cool Blob storage.</span></span> <span data-ttu-id="c4fd0-117">De activiteit ondersteunt **lezen van het blok, toevoegen of pagina-blobs**, maar ondersteunt **schrijven naar alleen blok-blobs**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-117">The activity supports **reading from block, append, or page blobs**, but supports **writing to only block blobs**.</span></span> <span data-ttu-id="c4fd0-118">Azure Premium-opslag wordt niet ondersteund als een sink omdat het wordt ondersteund door de pagina-blobs.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-118">Azure Premium Storage is not supported as a sink because it is backed by page blobs.</span></span>
> 
> <span data-ttu-id="c4fd0-119">Kopieeractiviteit verwijdert geen gegevens van de bron nadat de gegevens is gekopieerd naar de bestemming.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-119">Copy Activity does not delete data from the source after the data is successfully copied to the destination.</span></span> <span data-ttu-id="c4fd0-120">Als u brongegevens verwijderen na een geslaagde kopie moet, maakt u een [aangepaste activiteit](data-factory-use-custom-activities.md) verwijderen van de gegevens en de activiteit in de pijplijn gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-120">If you need to delete source data after a successful copy, create a [custom activity](data-factory-use-custom-activities.md) to delete the data and use the activity in the pipeline.</span></span> <span data-ttu-id="c4fd0-121">Zie voor een voorbeeld de [verwijderen blob of de map voorbeeld op GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity).</span><span class="sxs-lookup"><span data-stu-id="c4fd0-121">For an example, see the [Delete blob or folder sample on GitHub](https://github.com/Azure/Azure-DataFactory/tree/master/Samples/DeleteBlobFileFolderCustomActivity).</span></span> 

## <a name="get-started"></a><span data-ttu-id="c4fd0-122">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="c4fd0-122">Get started</span></span>
<span data-ttu-id="c4fd0-123">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens uit een Azure Blob-opslag verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-123">You can create a pipeline with a copy activity that moves data to/from an Azure Blob Storage by using different tools/APIs.</span></span>

<span data-ttu-id="c4fd0-124">De eenvoudigste manier om een pijplijn maken is met de **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-124">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="c4fd0-125">Dit artikel bevat een [scenario](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) voor het maken van een pijplijn om gegevens te kopiëren van een Azure Blob Storage-locatie naar een andere locatie van de Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-125">This article has a [walkthrough](#walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage) for creating a pipeline to copy data from an Azure Blob Storage location  to another Azure Blob Storage location.</span></span> <span data-ttu-id="c4fd0-126">Zie voor een zelfstudie over het maken van een pijplijn om gegevens te kopiëren uit een Azure Blob Storage met Azure SQL Database [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="c4fd0-126">For a tutorial on creating a pipeline to copy data from an Azure Blob Storage to Azure SQL Database, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="c4fd0-127">U kunt ook de volgende hulpprogramma's gebruiken voor het maken van een pijplijn: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon**, **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-127">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="c4fd0-128">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies voor een pijplijn maken met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-128">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="c4fd0-129">Of u de hulpprogramma's of API's gebruiken, moet u de volgende stappen voor het maken van een pijplijn die de gegevens vanuit een brongegevensarchief naar een gegevensarchief sink verplaatst uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="c4fd0-129">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="c4fd0-130">Maak een **gegevensfactory**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-130">Create a **data factory**.</span></span> <span data-ttu-id="c4fd0-131">Een gegevensfactory kan één of meer pijplijnen bevatten.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-131">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="c4fd0-132">Maak **gekoppelde services** slaat om invoer- en gegevens te koppelen aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-132">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="c4fd0-133">Bijvoorbeeld, als u gegevens uit een Azure blob-opslag naar een Azure SQL database kopiëren wilt, maakt u twee gekoppelde services als u wilt uw Azure storage-account en de Azure SQL database koppelen aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-133">For example, if you are copying data from an Azure blob storage to an Azure SQL database, you create two linked services to link your Azure storage account and Azure SQL database to your data factory.</span></span> <span data-ttu-id="c4fd0-134">Zie voor de gekoppelde service-eigenschappen die specifiek voor Azure Blob Storage zijn, [gekoppelde service-eigenschappen](#linked-service-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-134">For linked service properties that are specific to Azure Blob Storage, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="c4fd0-135">Maak **gegevenssets** vertegenwoordigt de invoer- en -gegevens voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-135">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="c4fd0-136">In het voorbeeld in de laatste stap wordt vermeld, maakt u een gegevensset om op te geven van de blob-container en de map waarin de invoergegevens.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-136">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="c4fd0-137">En maken van een andere gegevensset opgeven van de SQL-tabel in de Azure SQL-database waarin de gegevens die zijn gekopieerd uit de blobopslag.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-137">And, you create another dataset to specify the SQL table in the Azure SQL database that holds the data copied from the blob storage.</span></span> <span data-ttu-id="c4fd0-138">Zie voor eigenschappen van gegevensset die specifiek voor Azure Blob Storage zijn, [eigenschappen van gegevensset](#dataset-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-138">For dataset properties that are specific to Azure Blob Storage, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="c4fd0-139">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-139">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="c4fd0-140">In het voorbeeld eerder vermeld, gebruikt u BlobSource als een bron- en SqlSink als een sink voor de kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-140">In the example mentioned earlier, you use BlobSource as a source and SqlSink as a sink for the copy activity.</span></span> <span data-ttu-id="c4fd0-141">Op dezelfde manier als u van Azure SQL Database in Azure Blob-opslag kopiëren wilt, gebruikt u SqlSource en BlobSink in de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-141">Similarly, if you are copying from Azure SQL Database to Azure Blob Storage, you use SqlSource and BlobSink in the copy activity.</span></span> <span data-ttu-id="c4fd0-142">Zie voor activiteitseigenschappen kopiëren die specifiek voor Azure Blob Storage zijn, [activiteitseigenschappen kopiëren](#copy-activity-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-142">For copy activity properties that are specific to Azure Blob Storage, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="c4fd0-143">Klik op de koppeling in de vorige sectie voor de gegevensopslag voor meer informatie over het gebruik van een gegevensarchief als een bron of een sink.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-143">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>  

<span data-ttu-id="c4fd0-144">Wanneer u de wizard gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-144">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="c4fd0-145">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van de JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-145">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="c4fd0-146">Zie voor voorbeelden met JSON-definities voor Data Factory-entiteiten die worden gebruikt om gegevens te kopiëren naar/van een Azure Blob Storage, [JSON voorbeelden](#json-examples-for-copying-data-to-and-from-blob-storage  ) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-146">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Blob Storage, see [JSON examples](#json-examples-for-copying-data-to-and-from-blob-storage  ) section of this article.</span></span>

<span data-ttu-id="c4fd0-147">De volgende secties bevatten informatie over de JSON-eigenschappen die worden gebruikt voor het definiëren van Data Factory-entiteiten specifieke naar Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-147">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Azure Blob Storage.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="c4fd0-148">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="c4fd0-148">Linked service properties</span></span>
<span data-ttu-id="c4fd0-149">Er zijn twee soorten gekoppelde services die kunt u een Azure Storage koppelen aan een Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-149">There are two types of linked services you can use to link an Azure Storage to an Azure data factory.</span></span> <span data-ttu-id="c4fd0-150">Ze zijn: **AzureStorage** gekoppelde service en **AzureStorageSas** gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-150">They are: **AzureStorage** linked service and **AzureStorageSas** linked service.</span></span> <span data-ttu-id="c4fd0-151">De gekoppelde Azure Storage-service biedt de gegevensfactory met globale toegang tot Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-151">The Azure Storage linked service provides the data factory with global access to the Azure Storage.</span></span> <span data-ttu-id="c4fd0-152">Terwijl de Azure Storage SAS (Shared Access Signature) gekoppelde biedt service de gegevensfactory met de toegang beperkt/tijdsgebonden naar Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-152">Whereas, The Azure Storage SAS (Shared Access Signature) linked service provides the data factory with restricted/time-bound access to the Azure Storage.</span></span> <span data-ttu-id="c4fd0-153">Er zijn geen andere verschillen tussen deze twee gekoppelde services.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-153">There are no other differences between these two linked services.</span></span> <span data-ttu-id="c4fd0-154">Kies de gekoppelde service die bij uw behoeften past.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-154">Choose the linked service that suits your needs.</span></span> <span data-ttu-id="c4fd0-155">De volgende secties bevatten meer details over deze twee gekoppelde services.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-155">The following sections provide more details on these two linked services.</span></span>

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a><span data-ttu-id="c4fd0-156">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="c4fd0-156">Dataset properties</span></span>
<span data-ttu-id="c4fd0-157">Als u een gegevensset te vertegenwoordigen de invoer- of -gegevens in een Azure Blob Storage, die u stelt de eigenschap type van de gegevensset: **AzureBlob**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-157">To specify a dataset to represent input or output data in an Azure Blob Storage, you set the type property of the dataset to: **AzureBlob**.</span></span> <span data-ttu-id="c4fd0-158">Stel de **linkedServiceName** eigenschap van de gegevensset op de naam van de Azure Storage of Azure Storage SAS gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-158">Set the **linkedServiceName** property of the dataset to the name of the Azure Storage or Azure Storage SAS linked service.</span></span>  <span data-ttu-id="c4fd0-159">Geef de eigenschappen van het type van de gegevensset de **blob-container** en de **map** in blob storage.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-159">The type properties of the dataset specify the **blob container** and the **folder** in the blob storage.</span></span>

<span data-ttu-id="c4fd0-160">Zie voor een volledige lijst van de JSON-secties en eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van de [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-160">For a full list of JSON sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="c4fd0-161">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).</span><span class="sxs-lookup"><span data-stu-id="c4fd0-161">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="c4fd0-162">Data factory ondersteunt de volgende compatibel met CLS .NET op basis van type-waarden voor het ontwikkelen van type-informatie in 'structuur' voor het schema op lezen gegevensbronnen zoals Azure blob: Int16, Int32, Int64, één, Double, Decimal, Byte [], Bool, String, Guid, Datetime, DateTimeOffset, Timespan.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-162">Data factory supports the following CLS-compliant .NET based type values for providing type information in “structure” for schema-on-read data sources like Azure blob: Int16, Int32, Int64, Single, Double, Decimal, Byte[], Bool, String, Guid, Datetime, Datetimeoffset, Timespan.</span></span> <span data-ttu-id="c4fd0-163">Data Factory voert automatisch typeconversies bij het verplaatsen van gegevens uit een gegevensopslag bron naar een gegevensarchief sink.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-163">Data Factory automatically performs type conversions when moving data from a source data store to a sink data store.</span></span>

<span data-ttu-id="c4fd0-164">De **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over de locatie opmaken enz., van de gegevens in het gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-164">The **typeProperties** section is different for each type of dataset and provides information about the location, format etc., of the data in the data store.</span></span> <span data-ttu-id="c4fd0-165">De typeProperties sectie voor de gegevensset van het type **AzureBlob** gegevensset heeft de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="c4fd0-165">The typeProperties section for dataset of type **AzureBlob** dataset has the following properties:</span></span>

| <span data-ttu-id="c4fd0-166">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="c4fd0-166">Property</span></span> | <span data-ttu-id="c4fd0-167">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c4fd0-167">Description</span></span> | <span data-ttu-id="c4fd0-168">Vereist</span><span class="sxs-lookup"><span data-stu-id="c4fd0-168">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c4fd0-169">folderPath</span><span class="sxs-lookup"><span data-stu-id="c4fd0-169">folderPath</span></span> |<span data-ttu-id="c4fd0-170">Pad naar de container en map in blob storage.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-170">Path to the container and folder in the blob storage.</span></span> <span data-ttu-id="c4fd0-171">Voorbeeld: myblobcontainer\myblobfolder\\</span><span class="sxs-lookup"><span data-stu-id="c4fd0-171">Example: myblobcontainer\myblobfolder\\</span></span> |<span data-ttu-id="c4fd0-172">Ja</span><span class="sxs-lookup"><span data-stu-id="c4fd0-172">Yes</span></span> |
| <span data-ttu-id="c4fd0-173">fileName</span><span class="sxs-lookup"><span data-stu-id="c4fd0-173">fileName</span></span> |<span data-ttu-id="c4fd0-174">De naam van de blob.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-174">Name of the blob.</span></span> <span data-ttu-id="c4fd0-175">Bestandsnaam is optioneel en is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-175">fileName is optional and case-sensitive.</span></span><br/><br/><span data-ttu-id="c4fd0-176">Als u een filename opgeeft, wordt de activiteit (inclusief kopiëren) werkt op de specifieke Blob.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-176">If you specify a filename, the activity (including Copy) works on the specific Blob.</span></span><br/><br/><span data-ttu-id="c4fd0-177">FileName is opgegeven, bevat kopiëren alle Blobs in de folderPath voor invoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-177">When fileName is not specified, Copy includes all Blobs in the folderPath for input dataset.</span></span><br/><br/><span data-ttu-id="c4fd0-178">Wanneer **fileName** is niet opgegeven voor een uitvoergegevensset en **preserveHierarchy** niet is opgegeven in activiteit sink, de naam van het gegenereerde bestand zou worden in de volgende indeling: Data.<Guid>. txt (bijvoorbeeld:: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span><span class="sxs-lookup"><span data-stu-id="c4fd0-178">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, the name of the generated file would be in the following this format: Data.<Guid>.txt (for example: : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt</span></span> |<span data-ttu-id="c4fd0-179">Nee</span><span class="sxs-lookup"><span data-stu-id="c4fd0-179">No</span></span> |
| <span data-ttu-id="c4fd0-180">partitionedBy</span><span class="sxs-lookup"><span data-stu-id="c4fd0-180">partitionedBy</span></span> |<span data-ttu-id="c4fd0-181">partitionedBy is een optionele eigenschap.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-181">partitionedBy is an optional property.</span></span> <span data-ttu-id="c4fd0-182">U kunt deze gebruiken om op te geven van een dynamische folderPath en de bestandsnaam voor de reeksgegevens.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-182">You can use it to specify a dynamic folderPath and filename for time series data.</span></span> <span data-ttu-id="c4fd0-183">FolderPath kan bijvoorbeeld parameters worden gebruikt voor elk uur van gegevens.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-183">For example, folderPath can be parameterized for every hour of data.</span></span> <span data-ttu-id="c4fd0-184">Zie de [partitionedBy eigenschap sectie](#using-partitionedBy-property) voor meer informatie en voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-184">See the [Using partitionedBy property section](#using-partitionedBy-property) for details and examples.</span></span> |<span data-ttu-id="c4fd0-185">Nee</span><span class="sxs-lookup"><span data-stu-id="c4fd0-185">No</span></span> |
| <span data-ttu-id="c4fd0-186">Indeling</span><span class="sxs-lookup"><span data-stu-id="c4fd0-186">format</span></span> | <span data-ttu-id="c4fd0-187">De volgende indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-187">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, **ParquetFormat**.</span></span> <span data-ttu-id="c4fd0-188">Stel de **type** eigenschap onder indeling op een van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-188">Set the **type** property under format to one of these values.</span></span> <span data-ttu-id="c4fd0-189">Zie voor meer informatie [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [Json-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren indeling](data-factory-supported-file-and-compression-formats.md#parquet-format) secties.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-189">For more information, see [Text Format](data-factory-supported-file-and-compression-formats.md#text-format), [Json Format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro Format](data-factory-supported-file-and-compression-formats.md#avro-format), [Orc Format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections.</span></span> <br><br> <span data-ttu-id="c4fd0-190">Als u wilt **kopiëren van bestanden als-is** overslaan tussen bestandsgebaseerde winkels (binaire kopiëren), de sectie indeling in de definities van beide invoer en uitvoer gegevensset.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-190">If you want to **copy files as-is** between file-based stores (binary copy), skip the format section in both input and output dataset definitions.</span></span> |<span data-ttu-id="c4fd0-191">Nee</span><span class="sxs-lookup"><span data-stu-id="c4fd0-191">No</span></span> |
| <span data-ttu-id="c4fd0-192">Compressie</span><span class="sxs-lookup"><span data-stu-id="c4fd0-192">compression</span></span> | <span data-ttu-id="c4fd0-193">Geef het type en de compressie van de gegevens.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-193">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="c4fd0-194">Ondersteunde typen zijn: **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-194">Supported types are: **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="c4fd0-195">Ondersteunde niveaus: **optimale** en **snelst**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-195">Supported levels are: **Optimal** and **Fastest**.</span></span> <span data-ttu-id="c4fd0-196">Zie voor meer informatie [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="c4fd0-196">For more information, see [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="c4fd0-197">Nee</span><span class="sxs-lookup"><span data-stu-id="c4fd0-197">No</span></span> |

### <a name="using-partitionedby-property"></a><span data-ttu-id="c4fd0-198">Gebruik de eigenschap partitionedBy</span><span class="sxs-lookup"><span data-stu-id="c4fd0-198">Using partitionedBy property</span></span>
<span data-ttu-id="c4fd0-199">Zoals vermeld in de vorige sectie, kunt u een dynamische folderPath en de bestandsnaam voor de time series-gegevens met de **partitionedBy** -eigenschap [Data Factory-functies en de systeemvariabelen](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="c4fd0-199">As mentioned in the previous section, you can specify a dynamic folderPath and filename for time series data with the **partitionedBy** property, [Data Factory functions, and the system variables](data-factory-functions-variables.md).</span></span>

<span data-ttu-id="c4fd0-200">Zie voor meer informatie over tijd reeks gegevenssets, planning en segmenten [gegevenssets maken](data-factory-create-datasets.md) en [planning en uitvoering](data-factory-scheduling-and-execution.md) artikelen.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-200">For more information on time series datasets, scheduling, and slices, see [Creating Datasets](data-factory-create-datasets.md) and [Scheduling & Execution](data-factory-scheduling-and-execution.md) articles.</span></span>

#### <a name="sample-1"></a><span data-ttu-id="c4fd0-201">Voorbeeld 1</span><span class="sxs-lookup"><span data-stu-id="c4fd0-201">Sample 1</span></span>

```json
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="c4fd0-202">In dit voorbeeld {segment} is vervangen door de opgegeven waarde van de Data Factory systeemvariabele SliceStart in de notatie (YYYYMMDDHH).</span><span class="sxs-lookup"><span data-stu-id="c4fd0-202">In this example, {Slice} is replaced with the value of Data Factory system variable SliceStart in the format (YYYYMMDDHH) specified.</span></span> <span data-ttu-id="c4fd0-203">De SliceStart verwijst voor het starten van de tijd van het segment.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-203">The SliceStart refers to start time of the slice.</span></span> <span data-ttu-id="c4fd0-204">FolderPath verschilt voor elk segment.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-204">The folderPath is different for each slice.</span></span> <span data-ttu-id="c4fd0-205">Bijvoorbeeld: wikidatagateway/wikisampledataout/2014100103 of wikidatagateway/wikisampledataout/2014100104</span><span class="sxs-lookup"><span data-stu-id="c4fd0-205">For example: wikidatagateway/wikisampledataout/2014100103 or wikidatagateway/wikisampledataout/2014100104</span></span>

#### <a name="sample-2"></a><span data-ttu-id="c4fd0-206">Voorbeeld 2</span><span class="sxs-lookup"><span data-stu-id="c4fd0-206">Sample 2</span></span>

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

<span data-ttu-id="c4fd0-207">In dit voorbeeld worden jaar, maand, dag en tijd van de SliceStart uitgepakt in verschillende variabelen die worden gebruikt door de eigenschappen voor folderPath en de bestandsnaam.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-207">In this example, year, month, day, and time of SliceStart are extracted into separate variables that are used by folderPath and fileName properties.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="c4fd0-208">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="c4fd0-208">Copy activity properties</span></span>
<span data-ttu-id="c4fd0-209">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van activiteiten van de [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-209">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="c4fd0-210">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer gegevenssets en beleidsregels zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-210">Properties such as name, description, input and output datasets, and policies are available for all types of activities.</span></span> <span data-ttu-id="c4fd0-211">Dat eigenschappen beschikbaar zijn in de **typeProperties** sectie van de activiteit variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-211">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="c4fd0-212">Voor de kopieeractiviteit variëren ze, afhankelijk van de typen van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-212">For Copy activity, they vary depending on the types of sources and sinks.</span></span> <span data-ttu-id="c4fd0-213">Als u gegevens uit een Azure Blob-opslag verplaatst, u het brontype instellen in de kopieerbewerking naar **BlobSource**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-213">If you are moving data from an Azure Blob Storage, you set the source type in the copy activity to **BlobSource**.</span></span> <span data-ttu-id="c4fd0-214">Als u gegevens naar een Azure Blob Storage verplaatst, u stelt het sink-type in de kopieerbewerking naar **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-214">Similarly, if you are moving data to an Azure Blob Storage, you set the sink type in the copy activity to **BlobSink**.</span></span> <span data-ttu-id="c4fd0-215">Deze sectie bevat een lijst met eigenschappen die worden ondersteund door BlobSource en BlobSink.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-215">This section provides a list of properties supported by BlobSource and BlobSink.</span></span>

<span data-ttu-id="c4fd0-216">**BlobSource** ondersteunt de volgende eigenschappen in de **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="c4fd0-216">**BlobSource** supports the following properties in the **typeProperties** section:</span></span>

| <span data-ttu-id="c4fd0-217">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="c4fd0-217">Property</span></span> | <span data-ttu-id="c4fd0-218">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c4fd0-218">Description</span></span> | <span data-ttu-id="c4fd0-219">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="c4fd0-219">Allowed values</span></span> | <span data-ttu-id="c4fd0-220">Vereist</span><span class="sxs-lookup"><span data-stu-id="c4fd0-220">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c4fd0-221">Recursieve</span><span class="sxs-lookup"><span data-stu-id="c4fd0-221">recursive</span></span> |<span data-ttu-id="c4fd0-222">Hiermee wordt aangegeven of de gegevens recursief is gelezen uit de submappen of alleen uit de opgegeven map.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-222">Indicates whether the data is read recursively from the sub folders or only from the specified folder.</span></span> |<span data-ttu-id="c4fd0-223">True (standaardwaarde), False</span><span class="sxs-lookup"><span data-stu-id="c4fd0-223">True (default value), False</span></span> |<span data-ttu-id="c4fd0-224">Nee</span><span class="sxs-lookup"><span data-stu-id="c4fd0-224">No</span></span> |

<span data-ttu-id="c4fd0-225">**BlobSink** ondersteunt de volgende eigenschappen **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="c4fd0-225">**BlobSink** supports the following properties **typeProperties** section:</span></span>

| <span data-ttu-id="c4fd0-226">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="c4fd0-226">Property</span></span> | <span data-ttu-id="c4fd0-227">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c4fd0-227">Description</span></span> | <span data-ttu-id="c4fd0-228">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="c4fd0-228">Allowed values</span></span> | <span data-ttu-id="c4fd0-229">Vereist</span><span class="sxs-lookup"><span data-stu-id="c4fd0-229">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c4fd0-230">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="c4fd0-230">copyBehavior</span></span> |<span data-ttu-id="c4fd0-231">Definieert het gedrag kopiëren wanneer de bron BlobSource of het bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-231">Defines the copy behavior when the source is BlobSource or FileSystem.</span></span> |<span data-ttu-id="c4fd0-232"><b>PreserveHierarchy</b>: behoudt de bestandshiërarchie in de doelmap.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-232"><b>PreserveHierarchy</b>: preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="c4fd0-233">Het relatieve pad van het bronbestand naar de bronmap is identiek aan het relatieve pad van doelbestand naar doelmap.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-233">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="c4fd0-234"><b>FlattenHierarchy</b>: alle bestanden uit de bronmap zijn in het eerste niveau van de doelmap.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-234"><b>FlattenHierarchy</b>: all files from the source folder are in the first level of target folder.</span></span> <span data-ttu-id="c4fd0-235">De doelbestanden hebben automatisch gegenereerde naam.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-235">The target files have auto generated name.</span></span> <br/><br/><span data-ttu-id="c4fd0-236"><b>MergeFiles</b>: alle bestanden uit de bronmap op één bestand worden samengevoegd.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-236"><b>MergeFiles</b>: merges all files from the source folder to one file.</span></span> <span data-ttu-id="c4fd0-237">Als de naam van het bestand/de opgegeven Blob is opgegeven, zijn de samengevoegde bestandsnaam de opgegeven naam; anders zou worden automatisch gegenereerde naam.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-237">If the File/Blob Name is specified, the merged file name would be the specified name; otherwise, would be auto-generated file name.</span></span> |<span data-ttu-id="c4fd0-238">Nee</span><span class="sxs-lookup"><span data-stu-id="c4fd0-238">No</span></span> |

<span data-ttu-id="c4fd0-239">**BlobSource** biedt ook ondersteuning voor deze twee eigenschappen voor achterwaartse compatibiliteit.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-239">**BlobSource** also supports these two properties for backward compatibility.</span></span>

* <span data-ttu-id="c4fd0-240">**treatEmptyAsNull**: Hiermee wordt aangegeven of null of lege tekenreeks behandelen als null-waarde.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-240">**treatEmptyAsNull**: Specifies whether to treat null or empty string as null value.</span></span>
* <span data-ttu-id="c4fd0-241">**skipHeaderLineCount** -geeft aan hoeveel lijnen moeten worden overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-241">**skipHeaderLineCount** - Specifies how many lines need be skipped.</span></span> <span data-ttu-id="c4fd0-242">Dit geldt alleen wanneer invoergegevensset gebruikmaakt TextFormat.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-242">It is applicable only when input dataset is using TextFormat.</span></span>

<span data-ttu-id="c4fd0-243">Op deze manier **BlobSink** ondersteunt de volgende eigenschap voor achterwaartse compatibiliteit.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-243">Similarly, **BlobSink** supports the following property for backward compatibility.</span></span>

* <span data-ttu-id="c4fd0-244">**blobWriterAddHeader**: Hiermee bepaalt u of een koptekst van de kolomdefinities toevoegen tijdens het schrijven naar een uitvoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-244">**blobWriterAddHeader**: Specifies whether to add a header of column definitions while writing to an output dataset.</span></span>

<span data-ttu-id="c4fd0-245">Gegevenssets ondersteunen nu de volgende eigenschappen die dezelfde functionaliteit implementeren: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-245">Datasets now support the following properties that implement the same functionality: **treatEmptyAsNull**, **skipLineCount**, **firstRowAsHeader**.</span></span>

<span data-ttu-id="c4fd0-246">De volgende tabel bevat richtlijnen over het gebruik van de eigenschappen van nieuwe gegevensset in plaats van deze eigenschappen van de bron/sink blob.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-246">The following table provides guidance on using the new dataset properties in place of these blob source/sink properties.</span></span>

| <span data-ttu-id="c4fd0-247">Activiteitseigenschap kopiëren</span><span class="sxs-lookup"><span data-stu-id="c4fd0-247">Copy Activity property</span></span> | <span data-ttu-id="c4fd0-248">Eigenschap DataSet</span><span class="sxs-lookup"><span data-stu-id="c4fd0-248">Dataset property</span></span> |
|:--- |:--- |
| <span data-ttu-id="c4fd0-249">skipHeaderLineCount op BlobSource</span><span class="sxs-lookup"><span data-stu-id="c4fd0-249">skipHeaderLineCount on BlobSource</span></span> |<span data-ttu-id="c4fd0-250">skipLineCount en firstRowAsHeader.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-250">skipLineCount and firstRowAsHeader.</span></span> <span data-ttu-id="c4fd0-251">Regels eerst worden overgeslagen en wordt de eerste rij als een koptekst gelezen.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-251">Lines are skipped first and then the first row is read as a header.</span></span> |
| <span data-ttu-id="c4fd0-252">treatEmptyAsNull op BlobSource</span><span class="sxs-lookup"><span data-stu-id="c4fd0-252">treatEmptyAsNull on BlobSource</span></span> |<span data-ttu-id="c4fd0-253">treatEmptyAsNull op invoergegevensset</span><span class="sxs-lookup"><span data-stu-id="c4fd0-253">treatEmptyAsNull on input dataset</span></span> |
| <span data-ttu-id="c4fd0-254">blobWriterAddHeader op BlobSink</span><span class="sxs-lookup"><span data-stu-id="c4fd0-254">blobWriterAddHeader on BlobSink</span></span> |<span data-ttu-id="c4fd0-255">firstRowAsHeader op uitvoergegevensset</span><span class="sxs-lookup"><span data-stu-id="c4fd0-255">firstRowAsHeader on output dataset</span></span> |

<span data-ttu-id="c4fd0-256">Zie [geven TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) sectie voor meer informatie over deze eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-256">See [Specifying TextFormat](data-factory-supported-file-and-compression-formats.md#text-format) section for detailed information on these properties.</span></span>    

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="c4fd0-257">Voorbeelden van recursieve en copyBehavior</span><span class="sxs-lookup"><span data-stu-id="c4fd0-257">recursive and copyBehavior examples</span></span>
<span data-ttu-id="c4fd0-258">Deze sectie beschrijft het resulterende gedrag van de kopieerbewerking voor verschillende combinaties van recursieve en copyBehavior waarden.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-258">This section describes the resulting behavior of the Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="c4fd0-259">Recursieve</span><span class="sxs-lookup"><span data-stu-id="c4fd0-259">recursive</span></span> | <span data-ttu-id="c4fd0-260">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="c4fd0-260">copyBehavior</span></span> | <span data-ttu-id="c4fd0-261">Resulterende gedrag</span><span class="sxs-lookup"><span data-stu-id="c4fd0-261">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c4fd0-262">De waarde True</span><span class="sxs-lookup"><span data-stu-id="c4fd0-262">true</span></span> |<span data-ttu-id="c4fd0-263">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="c4fd0-263">preserveHierarchy</span></span> |<span data-ttu-id="c4fd0-264">Voor een bronmap Map1 met de volgende structuur:</span><span class="sxs-lookup"><span data-stu-id="c4fd0-264">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="c4fd0-265">Map1</span><span class="sxs-lookup"><span data-stu-id="c4fd0-265">Folder1</span></span><br/><span data-ttu-id="c4fd0-266">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="c4fd0-266">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="c4fd0-267">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="c4fd0-267">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="c4fd0-268">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="c4fd0-268">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="c4fd0-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="c4fd0-269">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="c4fd0-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="c4fd0-270">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="c4fd0-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="c4fd0-271">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="c4fd0-272">de doelmap Map1 wordt gemaakt met dezelfde structuur als de bron</span><span class="sxs-lookup"><span data-stu-id="c4fd0-272">the target folder Folder1 is created with the same structure as the source</span></span><br/><br/><span data-ttu-id="c4fd0-273">Map1</span><span class="sxs-lookup"><span data-stu-id="c4fd0-273">Folder1</span></span><br/><span data-ttu-id="c4fd0-274">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="c4fd0-274">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="c4fd0-275">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="c4fd0-275">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="c4fd0-276">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="c4fd0-276">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="c4fd0-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="c4fd0-277">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="c4fd0-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="c4fd0-278">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="c4fd0-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-279">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="c4fd0-280">De waarde True</span><span class="sxs-lookup"><span data-stu-id="c4fd0-280">true</span></span> |<span data-ttu-id="c4fd0-281">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="c4fd0-281">flattenHierarchy</span></span> |<span data-ttu-id="c4fd0-282">Voor een bronmap Map1 met de volgende structuur:</span><span class="sxs-lookup"><span data-stu-id="c4fd0-282">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="c4fd0-283">Map1</span><span class="sxs-lookup"><span data-stu-id="c4fd0-283">Folder1</span></span><br/><span data-ttu-id="c4fd0-284">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="c4fd0-284">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="c4fd0-285">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="c4fd0-285">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="c4fd0-286">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="c4fd0-286">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="c4fd0-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="c4fd0-287">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="c4fd0-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="c4fd0-288">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="c4fd0-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="c4fd0-289">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="c4fd0-290">het doel Map1 wordt gemaakt met de volgende structuur:</span><span class="sxs-lookup"><span data-stu-id="c4fd0-290">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="c4fd0-291">Map1</span><span class="sxs-lookup"><span data-stu-id="c4fd0-291">Folder1</span></span><br/><span data-ttu-id="c4fd0-292">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor File1</span><span class="sxs-lookup"><span data-stu-id="c4fd0-292">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="c4fd0-293">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor bestand2</span><span class="sxs-lookup"><span data-stu-id="c4fd0-293">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="c4fd0-294">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor bestand3</span><span class="sxs-lookup"><span data-stu-id="c4fd0-294">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="c4fd0-295">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor File4</span><span class="sxs-lookup"><span data-stu-id="c4fd0-295">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="c4fd0-296">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor File5</span><span class="sxs-lookup"><span data-stu-id="c4fd0-296">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="c4fd0-297">De waarde True</span><span class="sxs-lookup"><span data-stu-id="c4fd0-297">true</span></span> |<span data-ttu-id="c4fd0-298">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="c4fd0-298">mergeFiles</span></span> |<span data-ttu-id="c4fd0-299">Voor een bronmap Map1 met de volgende structuur:</span><span class="sxs-lookup"><span data-stu-id="c4fd0-299">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="c4fd0-300">Map1</span><span class="sxs-lookup"><span data-stu-id="c4fd0-300">Folder1</span></span><br/><span data-ttu-id="c4fd0-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="c4fd0-301">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="c4fd0-302">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="c4fd0-302">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="c4fd0-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="c4fd0-303">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="c4fd0-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="c4fd0-304">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="c4fd0-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="c4fd0-305">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="c4fd0-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="c4fd0-306">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="c4fd0-307">het doel Map1 wordt gemaakt met de volgende structuur:</span><span class="sxs-lookup"><span data-stu-id="c4fd0-307">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="c4fd0-308">Map1</span><span class="sxs-lookup"><span data-stu-id="c4fd0-308">Folder1</span></span><br/><span data-ttu-id="c4fd0-309">&nbsp;&nbsp;&nbsp;&nbsp;File1 bestand2 + bestand3 + File4 + bestand 5 inhoud worden samengevoegd in één bestand met automatisch gegenereerde naam</span><span class="sxs-lookup"><span data-stu-id="c4fd0-309">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="c4fd0-310">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="c4fd0-310">false</span></span> |<span data-ttu-id="c4fd0-311">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="c4fd0-311">preserveHierarchy</span></span> |<span data-ttu-id="c4fd0-312">Voor een bronmap Map1 met de volgende structuur:</span><span class="sxs-lookup"><span data-stu-id="c4fd0-312">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="c4fd0-313">Map1</span><span class="sxs-lookup"><span data-stu-id="c4fd0-313">Folder1</span></span><br/><span data-ttu-id="c4fd0-314">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="c4fd0-314">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="c4fd0-315">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="c4fd0-315">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="c4fd0-316">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="c4fd0-316">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="c4fd0-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="c4fd0-317">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="c4fd0-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="c4fd0-318">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="c4fd0-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="c4fd0-319">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="c4fd0-320">de doelmap Map1 wordt gemaakt met de volgende structuur</span><span class="sxs-lookup"><span data-stu-id="c4fd0-320">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="c4fd0-321">Map1</span><span class="sxs-lookup"><span data-stu-id="c4fd0-321">Folder1</span></span><br/><span data-ttu-id="c4fd0-322">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="c4fd0-322">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="c4fd0-323">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="c4fd0-323">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="c4fd0-324">Subfolder1 bestand3 File4 en File5 zijn niet opgenomen.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-324">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="c4fd0-325">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="c4fd0-325">false</span></span> |<span data-ttu-id="c4fd0-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="c4fd0-326">flattenHierarchy</span></span> |<span data-ttu-id="c4fd0-327">Voor een bronmap Map1 met de volgende structuur:</span><span class="sxs-lookup"><span data-stu-id="c4fd0-327">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="c4fd0-328">Map1</span><span class="sxs-lookup"><span data-stu-id="c4fd0-328">Folder1</span></span><br/><span data-ttu-id="c4fd0-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="c4fd0-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="c4fd0-330">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="c4fd0-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="c4fd0-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="c4fd0-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="c4fd0-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="c4fd0-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="c4fd0-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="c4fd0-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="c4fd0-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="c4fd0-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="c4fd0-335">de doelmap Map1 wordt gemaakt met de volgende structuur</span><span class="sxs-lookup"><span data-stu-id="c4fd0-335">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="c4fd0-336">Map1</span><span class="sxs-lookup"><span data-stu-id="c4fd0-336">Folder1</span></span><br/><span data-ttu-id="c4fd0-337">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor File1</span><span class="sxs-lookup"><span data-stu-id="c4fd0-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="c4fd0-338">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor bestand2</span><span class="sxs-lookup"><span data-stu-id="c4fd0-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="c4fd0-339">Subfolder1 bestand3 File4 en File5 zijn niet opgenomen.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-339">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="c4fd0-340">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="c4fd0-340">false</span></span> |<span data-ttu-id="c4fd0-341">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="c4fd0-341">mergeFiles</span></span> |<span data-ttu-id="c4fd0-342">Voor een bronmap Map1 met de volgende structuur:</span><span class="sxs-lookup"><span data-stu-id="c4fd0-342">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="c4fd0-343">Map1</span><span class="sxs-lookup"><span data-stu-id="c4fd0-343">Folder1</span></span><br/><span data-ttu-id="c4fd0-344">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="c4fd0-344">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="c4fd0-345">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="c4fd0-345">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="c4fd0-346">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="c4fd0-346">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="c4fd0-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="c4fd0-347">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="c4fd0-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="c4fd0-348">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="c4fd0-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="c4fd0-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="c4fd0-350">de doelmap Map1 wordt gemaakt met de volgende structuur</span><span class="sxs-lookup"><span data-stu-id="c4fd0-350">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="c4fd0-351">Map1</span><span class="sxs-lookup"><span data-stu-id="c4fd0-351">Folder1</span></span><br/><span data-ttu-id="c4fd0-352">&nbsp;&nbsp;&nbsp;&nbsp;File1 + bestand2 inhoud worden samengevoegd in één bestand met automatisch gegenereerde naam.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-352">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="c4fd0-353">automatisch gegenereerde naam voor File1</span><span class="sxs-lookup"><span data-stu-id="c4fd0-353">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="c4fd0-354">Subfolder1 bestand3 File4 en File5 zijn niet opgenomen.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-354">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="walkthrough-use-copy-wizard-to-copy-data-tofrom-blob-storage"></a><span data-ttu-id="c4fd0-355">Walkthrough: Wizard voor de kopie gebruiken om gegevens te kopiëren naar/van de Blob-opslag</span><span class="sxs-lookup"><span data-stu-id="c4fd0-355">Walkthrough: Use Copy Wizard to copy data to/from Blob Storage</span></span>
<span data-ttu-id="c4fd0-356">Bekijk het snel kopiëren van gegevens uit een Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-356">Let's look at how to quickly copy data to/from an Azure blob storage.</span></span> <span data-ttu-id="c4fd0-357">In dit overzicht bron- en doelserver gegevensopslag van het type: Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-357">In this walkthrough, both source and destination data stores of type: Azure Blob Storage.</span></span> <span data-ttu-id="c4fd0-358">De pijplijn in dit scenario kopieert gegevens vanuit een map naar een andere map in de blobcontainer met dezelfde.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-358">The pipeline in this walkthrough copies data from a folder to another folder in the same blob container.</span></span> <span data-ttu-id="c4fd0-359">In dit scenario is opzettelijk eenvoudig om weer te geven u eigenschappen of instellingen bij gebruik van Blob Storage als een bron- of sink.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-359">This walkthrough is intentionally simple to show you settings or properties when using Blob Storage as a source or sink.</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="c4fd0-360">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c4fd0-360">Prerequisites</span></span>
1. <span data-ttu-id="c4fd0-361">Maak een algemeen **Azure Storage-Account** als u nog niet hebt.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-361">Create a general-purpose **Azure Storage Account** if you don't have one already.</span></span> <span data-ttu-id="c4fd0-362">U de blobopslag gebruiken als beide **bron** en **bestemming** gegevens opslaan in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-362">You use the blob storage as both **source** and **destination** data store in this walkthrough.</span></span> <span data-ttu-id="c4fd0-363">Als u geen Azure storage-account hebt, raadpleegt u de [een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) voor stappen voor het maken van een artikel.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-363">if you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article for steps to create one.</span></span>
2. <span data-ttu-id="c4fd0-364">Maak een blobcontainer met de naam **adfblobconnector** in het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-364">Create a blob container named **adfblobconnector** in the storage account.</span></span> 
4. <span data-ttu-id="c4fd0-365">Maak een map met de naam **invoer** in de **adfblobconnector** container.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-365">Create a folder named **input** in the **adfblobconnector** container.</span></span>
5. <span data-ttu-id="c4fd0-366">Maak een bestand met de naam **emp.txt** met de volgende inhoud en upload het naar de **invoer** map met hulpprogramma's zoals [Azure Opslagverkenner](https://azurestorageexplorer.codeplex.com/)</span><span class="sxs-lookup"><span data-stu-id="c4fd0-366">Create a file named **emp.txt** with the following content and upload it to the **input** folder by using tools such as [Azure Storage Explorer](https://azurestorageexplorer.codeplex.com/)</span></span>
    ```json
    John, Doe
    Jane, Doe
    ```
### <a name="create-the-data-factory"></a><span data-ttu-id="c4fd0-367">De gegevensfactory maken</span><span class="sxs-lookup"><span data-stu-id="c4fd0-367">Create the data factory</span></span>
1. <span data-ttu-id="c4fd0-368">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c4fd0-368">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="c4fd0-369">Klik op **+ nieuw** vanuit de linkerbovenhoek op **Intelligence en analyse**, en klik op **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-369">Click **+ NEW** from the top-left corner, click **Intelligence + analytics**, and click **Data Factory**.</span></span>
3. <span data-ttu-id="c4fd0-370">In de blade **Nieuwe gegevensfactory**:</span><span class="sxs-lookup"><span data-stu-id="c4fd0-370">In the **New data factory** blade:</span></span>   
    1. <span data-ttu-id="c4fd0-371">Voer **ADFBlobConnectorDF** voor de **naam**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-371">Enter **ADFBlobConnectorDF** for the **name**.</span></span> <span data-ttu-id="c4fd0-372">De naam van de Azure-gegevensfactory moet wereldwijd uniek zijn.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-372">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="c4fd0-373">Als u de foutmelding: `*Data factory name “ADFBlobConnectorDF” is not available`, wijzig de naam van de gegevensfactory (bijvoorbeeld yournameADFBlobConnectorDF) en probeert u het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-373">If you receive the error: `*Data factory name “ADFBlobConnectorDF” is not available`, change the name of the data factory (for example, yournameADFBlobConnectorDF) and try creating again.</span></span> <span data-ttu-id="c4fd0-374">Raadpleeg het onderwerp [Data Factory - Naamgevingsregels](data-factory-naming-rules.md) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-374">See [Data Factory - Naming Rules](data-factory-naming-rules.md) topic for naming rules for Data Factory artifacts.</span></span>
    2. <span data-ttu-id="c4fd0-375">Selecteer uw Azure-**abonnement**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-375">Select your Azure **subscription**.</span></span>
    3. <span data-ttu-id="c4fd0-376">Selecteer voor de resourcegroep **gebruik bestaande** op een bestaande resourcegroep selecteren (of) selecteren **nieuw** een naam voor een resourcegroep in te voeren.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-376">For Resource Group, select **Use existing** to select an existing resource group (or) select **Create new** to enter a name for a resource group.</span></span>
    4. <span data-ttu-id="c4fd0-377">Selecteer een **locatie** voor de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-377">Select a **location** for the data factory.</span></span>
    5. <span data-ttu-id="c4fd0-378">Selecteer het selectievakje **Vastmaken aan dashboard** onderaan de blade.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-378">Select **Pin to dashboard** check box at the bottom of the blade.</span></span>
    6. <span data-ttu-id="c4fd0-379">Klik op **Create**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-379">Click **Create**.</span></span>
3. <span data-ttu-id="c4fd0-380">Nadat het maken voltooid is, ziet u de **Data Factory** blade zoals weergegeven in de volgende afbeelding: ![Data factory-startpagina](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span><span class="sxs-lookup"><span data-stu-id="c4fd0-380">After the creation is complete, you see the **Data Factory** blade as shown in the following image: ![Data factory home page](./media/data-factory-azure-blob-connector/data-factory-home-page.png)</span></span>

### <a name="copy-wizard"></a><span data-ttu-id="c4fd0-381">De wizard Kopiëren</span><span class="sxs-lookup"><span data-stu-id="c4fd0-381">Copy Wizard</span></span>
1. <span data-ttu-id="c4fd0-382">Klik op de startpagina van de Data Factory de **kopiëren van gegevens [PREVIEW]** tegel starten **Data-Wizard kopiëren** op een afzonderlijke tabblad.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-382">On the Data Factory home page, click the **Copy data [PREVIEW]** tile to launch **Copy Data Wizard** in a separate tab.</span></span>    
    
    > [!NOTE]
    >    <span data-ttu-id="c4fd0-383">Als u ziet dat de webbrowser is vastgelopen bij 'Autoriseren...', schakelt **blokkeren van cookies van derden en sitegegevens** instellen (of) laat dit ingeschakeld en maakt een uitzondering voor **login.microsoftonline.com**en probeer het opnieuw starten van de wizard.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-383">If you see that the web browser is stuck at "Authorizing...", disable/uncheck **Block third-party cookies and site data** setting (or) keep it enabled and create an exception for **login.microsoftonline.com** and then try launching the wizard again.</span></span>
2. <span data-ttu-id="c4fd0-384">Op de pagina **Eigenschappen**:</span><span class="sxs-lookup"><span data-stu-id="c4fd0-384">In the **Properties** page:</span></span>
    1. <span data-ttu-id="c4fd0-385">Voer **CopyPipeline** voor **taaknaam**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-385">Enter **CopyPipeline** for **Task name**.</span></span> <span data-ttu-id="c4fd0-386">Naam van de taak is de naam van de pijplijn in uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-386">The task name is the name of the pipeline in your data factory.</span></span>
    2. <span data-ttu-id="c4fd0-387">Voer een **beschrijving** voor de taak (optioneel).</span><span class="sxs-lookup"><span data-stu-id="c4fd0-387">Enter a **description** for the task (optional).</span></span>
    3. <span data-ttu-id="c4fd0-388">Voor **taak uitgebracht of taakschema**, blijven de **regelmatig wordt uitgevoerd volgens schema** optie.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-388">For **Task cadence or Task schedule**, keep the **Run regularly on schedule** option.</span></span> <span data-ttu-id="c4fd0-389">Als u deze taak slechts één keer in plaats van uitvoeren volgens een schema herhaaldelijk uitvoeren wilt, selecteert u **eenmaal nu uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-389">If you want to run this task only once instead of run repeatedly on a schedule, select **Run once now**.</span></span> <span data-ttu-id="c4fd0-390">Als u selecteert, **eenmaal nu uitvoeren** optie, een [eenmalige pijplijn](data-factory-create-pipelines.md#onetime-pipeline) wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-390">If you select, **Run once now** option, a [one-time pipeline](data-factory-create-pipelines.md#onetime-pipeline) is created.</span></span> 
    4. <span data-ttu-id="c4fd0-391">De instellingen voor bewaren **terugkerend patroon**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-391">Keep the settings for **Recurring pattern**.</span></span> <span data-ttu-id="c4fd0-392">Deze taak wordt uitgevoerd dagelijks tussen de begin- en eindtijden die u in de volgende stap opgeeft.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-392">This task runs daily between the start and end times you specify in the next step.</span></span>
    5. <span data-ttu-id="c4fd0-393">Wijzig de **begindatum tijd** naar **21/04/2017**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-393">Change the **Start date time** to **04/21/2017**.</span></span> 
    6. <span data-ttu-id="c4fd0-394">Wijzig de **einddatum en-tijd** naar **25/04/2017**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-394">Change the **End date time** to **04/25/2017**.</span></span> <span data-ttu-id="c4fd0-395">U kunt naar het type van de datum in plaats van het bladeren door de kalender.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-395">You may want to type the date instead of browsing through the calendar.</span></span>     
    8. <span data-ttu-id="c4fd0-396">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-396">Click **Next**.</span></span>
      <span data-ttu-id="c4fd0-397">![Hulpprogramma voor kopiëren - pagina eigenschappen](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span><span class="sxs-lookup"><span data-stu-id="c4fd0-397">![Copy Tool - Properties page](./media/data-factory-azure-blob-connector/copy-tool-properties-page.png)</span></span> 
3. <span data-ttu-id="c4fd0-398">Op de pagina **Brongegevensarchief** klikt u op de tegel **Azure Blob Storage**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-398">On the **Source data store** page, click **Azure Blob Storage** tile.</span></span> <span data-ttu-id="c4fd0-399">U gebruikt deze pagina om het brongegevensarchief op te geven voor de kopieertaak.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-399">You use this page to specify the source data store for the copy task.</span></span> <span data-ttu-id="c4fd0-400">U kunt een bestaande gekoppelde service van een gegevensarchief gebruiken of een nieuw gegevensarchief opgeven.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-400">You can use an existing data store linked service (or) specify a new data store.</span></span> <span data-ttu-id="c4fd0-401">Voor het gebruik van een bestaande gekoppelde service, selecteert u **van bestaande gekoppelde SERVICES** en selecteer de juiste gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-401">To use an existing linked service, you would select **FROM EXISTING LINKED SERVICES** and select the right linked service.</span></span> 
    <span data-ttu-id="c4fd0-402">![Hulpprogramma voor kopiëren - brongegevensarchief](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span><span class="sxs-lookup"><span data-stu-id="c4fd0-402">![Copy Tool - Source data store page](./media/data-factory-azure-blob-connector/copy-tool-source-data-store-page.png)</span></span>
4. <span data-ttu-id="c4fd0-403">Op de pagina **Het Azure Blob Storage-account opgeven**:</span><span class="sxs-lookup"><span data-stu-id="c4fd0-403">On the **Specify the Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="c4fd0-404">Houd de automatisch gegenereerde naam voor **verbindingsnaam**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-404">Keep the auto-generated name for **Connection name**.</span></span> <span data-ttu-id="c4fd0-405">Naam van de verbinding is de naam van de gekoppelde service van het type: Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-405">The connection name is the name of the linked service of type: Azure Storage.</span></span> 
   2. <span data-ttu-id="c4fd0-406">Controleer of de optie **Van Azure-abonnementen** is geselecteerd als **accountselectiemethode**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-406">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="c4fd0-407">Selecteer uw Azure-abonnement of houden **Alles selecteren** voor **Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-407">Select your Azure subscription or keep **Select all** for **Azure subscription**.</span></span>   
   4. <span data-ttu-id="c4fd0-408">Selecteer een **Azure-opslagaccount** uit de lijst met Azure-opslagaccounts die beschikbaar is voor het abonnement dat u hebt geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-408">Select an **Azure storage account** from the list of Azure storage accounts available in the selected subscription.</span></span> <span data-ttu-id="c4fd0-409">U kunt ook opslagaccountinstellingen handmatig door het selecteren van **handmatig invoeren** optie voor de **Accountselectiemethode**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-409">You can also choose to enter storage account settings manually by selecting **Enter manually** option for the **Account selection method**.</span></span>
   5. <span data-ttu-id="c4fd0-410">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-410">Click **Next**.</span></span> 
      <span data-ttu-id="c4fd0-411">![Hulpprogramma voor kopiëren - het Azure Blob storage-account opgeven](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span><span class="sxs-lookup"><span data-stu-id="c4fd0-411">![Copy Tool - Specify the Azure Blob storage account](./media/data-factory-azure-blob-connector/copy-tool-specify-azure-blob-storage-account.png)</span></span>
5. <span data-ttu-id="c4fd0-412">Op de pagina **Het invoerbestand of de invoermap kiezen**:</span><span class="sxs-lookup"><span data-stu-id="c4fd0-412">On **Choose the input file or folder** page:</span></span>
   1. <span data-ttu-id="c4fd0-413">Dubbelklik op **adfblobcontainer**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-413">Double-click **adfblobcontainer**.</span></span>
   2. <span data-ttu-id="c4fd0-414">Selecteer **invoer**, en klik op **Kies**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-414">Select **input**, and click **Choose**.</span></span> <span data-ttu-id="c4fd0-415">In dit scenario maakt selecteren u de invoermap.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-415">In this walkthrough, you select the input folder.</span></span> <span data-ttu-id="c4fd0-416">U kunt ook selecteren de emp.txt-bestand in de map in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-416">You could also select the emp.txt file in the folder instead.</span></span> 
      <span data-ttu-id="c4fd0-417">![Hulpprogramma voor kopiëren - het invoerbestand of de invoermap kiezen](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="c4fd0-417">![Copy Tool - Choose the input file or folder](./media/data-factory-azure-blob-connector/copy-tool-choose-input-file-or-folder.png)</span></span>
6. <span data-ttu-id="c4fd0-418">Op de **het invoerbestand of de invoermap kiezen** pagina:</span><span class="sxs-lookup"><span data-stu-id="c4fd0-418">On the **Choose the input file or folder** page:</span></span>
    1. <span data-ttu-id="c4fd0-419">Controleer of de **bestand of map** is ingesteld op **adfblobconnector/invoer**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-419">Confirm that the **file or folder** is set to **adfblobconnector/input**.</span></span> <span data-ttu-id="c4fd0-420">Als de bestanden in submappen, bijvoorbeeld 04-01-2017, 2017/04/02 en enzovoort, en geef adfblobconnector/invoer / {year} / {month} / {day} voor bestand of map.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-420">If the files are in sub folders, for example, 2017/04/01, 2017/04/02, and so on, enter adfblobconnector/input/{year}/{month}/{day} for file or folder.</span></span> <span data-ttu-id="c4fd0-421">Als u op TAB buiten het tekstvak drukt, ziet u drie vervolgkeuzelijsten indelingen selecteren voor jaar (jjjj), de maand (MM) en de dag (dd).</span><span class="sxs-lookup"><span data-stu-id="c4fd0-421">When you press TAB out of the text box, you see three drop-down lists to select formats for year (yyyy), month (MM), and day (dd).</span></span> 
    2. <span data-ttu-id="c4fd0-422">Stel geen **kopiëren van bestand recursief**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-422">Do not set **Copy file recursively**.</span></span> <span data-ttu-id="c4fd0-423">Selecteer deze optie om recursief bladeren door mappen voor bestanden worden gekopieerd naar de bestemming.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-423">Select this option to recursively traverse through folders for files to be copied to the destination.</span></span> 
    3. <span data-ttu-id="c4fd0-424">Niet de **binaire kopiëren** optie.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-424">Do not the **binary copy** option.</span></span> <span data-ttu-id="c4fd0-425">Selecteer deze optie voor het uitvoeren van een binaire kopie van het bronbestand naar de bestemming.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-425">Select this option to perform a binary copy of source file to the destination.</span></span> <span data-ttu-id="c4fd0-426">Selecteer niet voor dit scenario zodat u meer opties in de volgende pagina's kunt zien.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-426">Do not select for this walkthrough so that you can see more options in the next pages.</span></span> 
    4. <span data-ttu-id="c4fd0-427">Controleer of de **compressietype** is ingesteld op **geen**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-427">Confirm that the **Compression type** is set to **None**.</span></span> <span data-ttu-id="c4fd0-428">Selecteer een waarde voor deze optie als de bronbestanden in een van de ondersteunde indelingen zijn gecomprimeerd.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-428">Select a value for this option if your source files are compressed in one of the supported formats.</span></span> 
    5. <span data-ttu-id="c4fd0-429">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-429">Click **Next**.</span></span>
    <span data-ttu-id="c4fd0-430">![Hulpprogramma voor kopiëren - het invoerbestand of de invoermap kiezen](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span><span class="sxs-lookup"><span data-stu-id="c4fd0-430">![Copy Tool - Choose the input file or folder](./media/data-factory-azure-blob-connector/chose-input-file-folder.png)</span></span> 
7. <span data-ttu-id="c4fd0-431">Op de pagina **Bestandsinstellingen** ziet u de scheidingstekens en het schema dat automatisch is gedetecteerd door de wizard tijdens het parseren van het bestand.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-431">On the **File format settings** page, you see the delimiters and the schema that is auto-detected by the wizard by parsing the file.</span></span> 
    1. <span data-ttu-id="c4fd0-432">Bevestig de volgende opties: een.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-432">Confirm the following options: a.</span></span> <span data-ttu-id="c4fd0-433">De **bestandsindeling** is ingesteld op **tekstindeling**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-433">The **file format** is set to **Text format**.</span></span> <span data-ttu-id="c4fd0-434">Hier ziet u de ondersteunde indelingen in de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-434">You can see all the supported formats in the drop-down list.</span></span> <span data-ttu-id="c4fd0-435">Bijvoorbeeld: JSON, Avro, ORC, parketvloeren.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-435">For example: JSON, Avro, ORC, Parquet.</span></span>
        <span data-ttu-id="c4fd0-436">b.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-436">b.</span></span> <span data-ttu-id="c4fd0-437">De **kolomscheidingsteken** is ingesteld op `Comma (,)`.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-437">The **column delimiter** is set to `Comma (,)`.</span></span> <span data-ttu-id="c4fd0-438">Hier ziet u de andere kolom scheidingstekens die door Data Factory worden ondersteund in de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-438">You can see the other column delimiters supported by Data Factory in the drop-down list.</span></span> <span data-ttu-id="c4fd0-439">U kunt ook een aangepaste scheidingsteken opgeven.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-439">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="c4fd0-440">c.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-440">c.</span></span> <span data-ttu-id="c4fd0-441">De **rijscheidingsteken** is ingesteld op `Carriage Return + Line feed (\r\n)`.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-441">The **row delimiter** is set to `Carriage Return + Line feed (\r\n)`.</span></span> <span data-ttu-id="c4fd0-442">Hier ziet u de andere rij scheidingstekens die door Data Factory worden ondersteund in de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-442">You can see the other row delimiters supported by Data Factory in the drop-down list.</span></span> <span data-ttu-id="c4fd0-443">U kunt ook een aangepaste scheidingsteken opgeven.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-443">You can also specify a custom delimiter.</span></span>
        <span data-ttu-id="c4fd0-444">d.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-444">d.</span></span> <span data-ttu-id="c4fd0-445">De **aantal regels overslaan** is ingesteld op **0**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-445">The **skip line count** is set to **0**.</span></span> <span data-ttu-id="c4fd0-446">Als u een paar regels moet worden overgeslagen aan de bovenkant van het bestand wilt, voert u hier het nummer.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-446">If you want a few lines to be skipped at the top of the file, enter the number here.</span></span>
        <span data-ttu-id="c4fd0-447">e.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-447">e.</span></span>  <span data-ttu-id="c4fd0-448">De **eerste gegevensrij kolomnamen bevat** is niet ingesteld.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-448">The **first data row contains column names** is not set.</span></span> <span data-ttu-id="c4fd0-449">Selecteer deze optie als de bronbestanden kolomnamen in de eerste rij bevatten.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-449">If the source files contain column names in the first row, select this option.</span></span>
        <span data-ttu-id="c4fd0-450">f.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-450">f.</span></span> <span data-ttu-id="c4fd0-451">De **leeg kolomwaarde behandelen als null** optie is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-451">The **treat empty column value as null** option is set.</span></span>
    2. <span data-ttu-id="c4fd0-452">Vouw **geavanceerde instellingen** om geavanceerde optie beschikbaar te zien.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-452">Expand **Advanced settings** to see advanced option available.</span></span>
    3. <span data-ttu-id="c4fd0-453">Aan de onderkant van de pagina, Zie de **preview** van gegevens van het bestand emp.txt.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-453">At the bottom of the page, see the **preview** of data from the emp.txt file.</span></span>
    4. <span data-ttu-id="c4fd0-454">Klik op **SCHEMA** tabblad onderaan om te zien van het schema dat u de wizard kopiëren die zijn afgeleid door te kijken naar de gegevens in het bronbestand.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-454">Click **SCHEMA** tab at the bottom to see the schema that the copy wizard inferred by looking at the data in the source file.</span></span>
    5. <span data-ttu-id="c4fd0-455">Klik op **Volgende** nadat u de scheidingstekens hebt gecontroleerd en een voorbeeld van de gegevens hebt bekeken.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-455">Click **Next** after you review the delimiters and preview data.</span></span>
    <span data-ttu-id="c4fd0-456">![Hulpprogramma voor kopiëren - bestandsindelingsinstellingen](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span><span class="sxs-lookup"><span data-stu-id="c4fd0-456">![Copy Tool - File format settings](./media/data-factory-azure-blob-connector/copy-tool-file-format-settings.png)</span></span>  
8. <span data-ttu-id="c4fd0-457">Op de **bestemming gegevensarchief pagina**, selecteer **Azure Blob Storage**, en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-457">On the **Destination data store page**, select **Azure Blob Storage**, and click **Next**.</span></span> <span data-ttu-id="c4fd0-458">Als zowel de bron- en doelserver gegevensarchieven in dit scenario gebruikt u de Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-458">You are using the Azure Blob Storage as both the source and destination data stores in this walkthrough.</span></span>    
    <span data-ttu-id="c4fd0-459">![Hulpprogramma voor kopiëren - gegevensarchief van de doelserver selecteren](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span><span class="sxs-lookup"><span data-stu-id="c4fd0-459">![Copy Tool - select destination data store](media/data-factory-azure-blob-connector/select-destination-data-store.png)</span></span>
9. <span data-ttu-id="c4fd0-460">Op **de Azure Blob storage-account opgeven** pagina:</span><span class="sxs-lookup"><span data-stu-id="c4fd0-460">On **Specify the Azure Blob storage account** page:</span></span>
   1. <span data-ttu-id="c4fd0-461">Voer **AzureStorageLinkedService** voor de **verbindingsnaam** veld.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-461">Enter **AzureStorageLinkedService** for the **Connection name** field.</span></span>
   2. <span data-ttu-id="c4fd0-462">Controleer of de optie **Van Azure-abonnementen** is geselecteerd als **accountselectiemethode**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-462">Confirm that **From Azure subscriptions** option is selected for **Account selection method**.</span></span>
   3. <span data-ttu-id="c4fd0-463">Selecteer uw Azure-**abonnement**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-463">Select your Azure **subscription**.</span></span>  
   4. <span data-ttu-id="c4fd0-464">Selecteer uw Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-464">Select your Azure storage account.</span></span> 
   5. <span data-ttu-id="c4fd0-465">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-465">Click **Next**.</span></span>     
10. <span data-ttu-id="c4fd0-466">Op de **het uitvoerbestand of de invoermap kiezen** pagina:</span><span class="sxs-lookup"><span data-stu-id="c4fd0-466">On the **Choose the output file or folder** page:</span></span> 
    6. <span data-ttu-id="c4fd0-467">Geef **mappad** als **adfblobconnector/uitvoer / {year} / {month} / {day}**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-467">specify **Folder path** as **adfblobconnector/output/{year}/{month}/{day}**.</span></span> <span data-ttu-id="c4fd0-468">Voer **tabblad**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-468">Enter **TAB**.</span></span>
    7. <span data-ttu-id="c4fd0-469">Voor de **jaar**, selecteer **jjjj**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-469">For the **year**, select **yyyy**.</span></span>
    8. <span data-ttu-id="c4fd0-470">Voor de **maand**, bevestig dat is ingesteld op **MM**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-470">For the **month**, confirm that it is set to **MM**.</span></span>
    9. <span data-ttu-id="c4fd0-471">Voor de **dag**, bevestig dat is ingesteld op **dd**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-471">For the **day**, confirm that it is set to **dd**.</span></span>
    10. <span data-ttu-id="c4fd0-472">Controleer of de **compressietype** is ingesteld op **geen**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-472">Confirm that the **compression type** is set to **None**.</span></span>
    11. <span data-ttu-id="c4fd0-473">Controleer of de **gedrag kopiëren** is ingesteld op **bestanden samenvoegen**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-473">Confirm that the **copy behavior** is set to **Merge files**.</span></span> <span data-ttu-id="c4fd0-474">Als het uitvoerbestand met dezelfde naam al bestaat, wordt de nieuwe inhoud toegevoegd aan hetzelfde bestand aan het einde.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-474">If the output file with the same name already exists, the new content is added to the same file at the end.</span></span>
    12. <span data-ttu-id="c4fd0-475">Klik op **Volgende**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-475">Click **Next**.</span></span>
    <span data-ttu-id="c4fd0-476">![Hulpprogramma voor kopiëren - bestand voor uitvoer of de invoermap kiezen](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span><span class="sxs-lookup"><span data-stu-id="c4fd0-476">![Copy Tool - Choose output file or folder](media/data-factory-azure-blob-connector/choose-the-output-file-or-folder.png)</span></span>
11. <span data-ttu-id="c4fd0-477">Op de **bestandsindelingsinstellingen** pagina, controleert u de instellingen en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-477">On the **File format settings** page, review the settings, and click **Next**.</span></span> <span data-ttu-id="c4fd0-478">Een van de aanvullende opties hier is een koptekst kunt toevoegen aan het uitvoerbestand.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-478">One of the additional options here is to add a header to the output file.</span></span> <span data-ttu-id="c4fd0-479">Als u deze optie selecteert, wordt een veldnamenrij toegevoegd met namen van de kolommen van het schema van de bron.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-479">If you select that option, a header row is added with names of the columns from the schema of the source.</span></span> <span data-ttu-id="c4fd0-480">Wanneer u het schema voor de bron weergeeft, kunt u de standaardkolomnamen wijzigen.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-480">You can rename the default column names when viewing the schema for the source.</span></span> <span data-ttu-id="c4fd0-481">U kan bijvoorbeeld de eerste kolom wijzigen voornaam en achternaam tweede kolom.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-481">For example, you could change the first column to First Name and second column to Last Name.</span></span> <span data-ttu-id="c4fd0-482">Vervolgens wordt het bestand voor uitvoer gegenereerd met een header met deze namen als kolomnamen.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-482">Then, the output file is generated with a header with these names as column names.</span></span> 
    <span data-ttu-id="c4fd0-483">![Hulpprogramma voor kopiëren - bestandsindelingsinstellingen voor bestemming](media/data-factory-azure-blob-connector/file-format-destination.png)</span><span class="sxs-lookup"><span data-stu-id="c4fd0-483">![Copy Tool - File format settings for destination](media/data-factory-azure-blob-connector/file-format-destination.png)</span></span>
12. <span data-ttu-id="c4fd0-484">Op de **prestatie-instellingen** pagina, controleert u of **eenheden cloud** en **kopieën parallelle** zijn ingesteld op **automatisch**, en klik op volgende.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-484">On the **Performance settings** page, confirm that **cloud units** and **parallel copies** are set to **Auto**, and click Next.</span></span> <span data-ttu-id="c4fd0-485">Zie voor meer informatie over deze instellingen [activiteit prestaties en prestatieafstemming handleiding kopiëren](data-factory-copy-activity-performance.md#parallel-copy).</span><span class="sxs-lookup"><span data-stu-id="c4fd0-485">For details about these settings, see [Copy activity performance and tuning guide](data-factory-copy-activity-performance.md#parallel-copy).</span></span>
    <span data-ttu-id="c4fd0-486">![Hulpprogramma voor kopiëren - prestatie-instellingen](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span><span class="sxs-lookup"><span data-stu-id="c4fd0-486">![Copy Tool - Performance settings](media/data-factory-azure-blob-connector/copy-performance-settings.png)</span></span> 
14. <span data-ttu-id="c4fd0-487">Op de **samenvatting** pagina, controleert u alle instellingen (taakeigenschappen, instellingen voor de bron- en doelserver en instellingen) en klik op **volgende**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-487">On the **Summary** page, review all settings (task properties, settings for source and destination, and copy settings), and click **Next**.</span></span>
    <span data-ttu-id="c4fd0-488">![Hulpprogramma voor kopiëren - pagina overzicht](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span><span class="sxs-lookup"><span data-stu-id="c4fd0-488">![Copy Tool - Summary page](media/data-factory-azure-blob-connector/copy-tool-summary-page.png)</span></span>
15. <span data-ttu-id="c4fd0-489">Lees de informatie op de pagina **Samenvatting** en klik op **Voltooien**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-489">Review information in the **Summary** page, and click **Finish**.</span></span> <span data-ttu-id="c4fd0-490">De wizard maakt twee gekoppelde services, twee gegevenssets (invoer en uitvoer) en één pijplijn in de gegevensfactory (van waaruit u de wizard Kopiëren hebt gestart).</span><span class="sxs-lookup"><span data-stu-id="c4fd0-490">The wizard creates two linked services, two datasets (input and output), and one pipeline in the data factory (from where you launched the Copy Wizard).</span></span>
    <span data-ttu-id="c4fd0-491">![Hulpprogramma voor kopiëren - pagina van de implementatie](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span><span class="sxs-lookup"><span data-stu-id="c4fd0-491">![Copy Tool - Deployment page](media/data-factory-azure-blob-connector/copy-tool-deployment-page.png)</span></span>

### <a name="monitor-the-pipeline-copy-task"></a><span data-ttu-id="c4fd0-492">Bewaken van de pijplijn (taak kopiëren)</span><span class="sxs-lookup"><span data-stu-id="c4fd0-492">Monitor the pipeline (copy task)</span></span>

1. <span data-ttu-id="c4fd0-493">Klik op de koppeling `Click here to monitor copy pipeline` op de **implementatie** pagina.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-493">Click the link `Click here to monitor copy pipeline` on the **Deployment** page.</span></span> 
2. <span data-ttu-id="c4fd0-494">U ziet de **bewaken en beheren van de toepassing** op een afzonderlijke tabblad.  ![Bewaken en beheren van App](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span><span class="sxs-lookup"><span data-stu-id="c4fd0-494">You should see the **Monitor and Manage application** in a separate tab.  ![Monitor and Manage App](media/data-factory-azure-blob-connector/monitor-manage-app.png)</span></span>
3. <span data-ttu-id="c4fd0-495">Wijzig de **start** tijd boven aan `04/19/2017` en **end** tijd `04/27/2017`, en klik vervolgens op **toepassen**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-495">Change the **start** time at the top to `04/19/2017` and **end** time to `04/27/2017`, and then click **Apply**.</span></span> 
4. <span data-ttu-id="c4fd0-496">Ziet u vijf activiteit windows in de **ACTIVITEITSVENSTERS** lijst.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-496">You should see five activity windows in the **ACTIVITY WINDOWS** list.</span></span> <span data-ttu-id="c4fd0-497">De **WindowStart** tijden moeten voldoende zijn voor alle dagen vanaf het begin van de pijplijn tot eindtijden pipeline.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-497">The **WindowStart** times should cover all days from pipeline start to pipeline end times.</span></span> 
5. <span data-ttu-id="c4fd0-498">Klik op **vernieuwen** knop voor de **ACTIVITEITSVENSTERS** lijst een paar keer tot u de status van alle activiteitsvensters is ingesteld op gereed.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-498">Click **Refresh** button for the **ACTIVITY WINDOWS** list a few times until you see the status of all the activity windows is set to Ready.</span></span> 
6. <span data-ttu-id="c4fd0-499">Controleer nu of dat de uitvoerbestanden worden gegenereerd in de map voor uitvoer van de container adfblobconnector.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-499">Now, verify that the output files are generated in the output folder of adfblobconnector container.</span></span> <span data-ttu-id="c4fd0-500">Hier ziet u de volgende mapstructuur in de uitvoermap:</span><span class="sxs-lookup"><span data-stu-id="c4fd0-500">You should see the following folder structure in the output folder:</span></span> 
    ```
    2017/04/21
    2017/04/22
    2017/04/23
    2017/04/24
    2017/04/25    
    ```
<span data-ttu-id="c4fd0-501">Zie voor gedetailleerde informatie over het controleren en beheren van gegevensfactory [bewaken en beheren van de Data Factory-pijplijn](data-factory-monitor-manage-app.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-501">For detailed information about monitoring and managing data factories, see [Monitor and manage Data Factory pipeline](data-factory-monitor-manage-app.md) article.</span></span> 
 
### <a name="data-factory-entities"></a><span data-ttu-id="c4fd0-502">Data Factory-entiteiten</span><span class="sxs-lookup"><span data-stu-id="c4fd0-502">Data Factory entities</span></span>
<span data-ttu-id="c4fd0-503">Nu Ga terug naar het tabblad met de Data Factory-startpagina.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-503">Now, switch back to the tab with the Data Factory home page.</span></span> <span data-ttu-id="c4fd0-504">U ziet dat er twee gekoppelde services, twee gegevenssets en een pijplijn in uw data factory nu zijn.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-504">Notice that there are two linked services, two datasets, and one pipeline in your data factory now.</span></span> 

![Data Factory-startpagina met entiteiten](media/data-factory-azure-blob-connector/data-factory-home-page-with-numbers.png)

<span data-ttu-id="c4fd0-506">Klik op **auteur en implementeren van** Data Factory-Editor te starten.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-506">Click **Author and deploy** to launch Data Factory Editor.</span></span> 

![Data Factory Editor](media/data-factory-azure-blob-connector/data-factory-editor.png)

<span data-ttu-id="c4fd0-508">U ziet de volgende Data Factory-entiteiten in uw data factory:</span><span class="sxs-lookup"><span data-stu-id="c4fd0-508">You should see the following Data Factory entities in your data factory:</span></span> 

 - <span data-ttu-id="c4fd0-509">Twee gekoppelde services.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-509">Two linked services.</span></span> <span data-ttu-id="c4fd0-510">Een voor de bron en de andere is voor de bestemming.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-510">One for the source and the other one for the destination.</span></span> <span data-ttu-id="c4fd0-511">De gekoppelde services verwijzen naar hetzelfde Azure-opslagaccount in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-511">Both the linked services refer to the same Azure Storage account in this walkthrough.</span></span> 
 - <span data-ttu-id="c4fd0-512">Twee gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-512">Two datasets.</span></span> <span data-ttu-id="c4fd0-513">Een invoergegevensset en een uitvoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-513">An input dataset and an output dataset.</span></span> <span data-ttu-id="c4fd0-514">In dit scenario maakt gebruik van de blobcontainer met dezelfde beide maar verwijzen naar andere mappen (invoer en uitvoer).</span><span class="sxs-lookup"><span data-stu-id="c4fd0-514">In this walkthrough, both use the same blob container but refer to different folders (input and output).</span></span>
 - <span data-ttu-id="c4fd0-515">Een pijplijn.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-515">A pipeline.</span></span> <span data-ttu-id="c4fd0-516">De pijplijn bevat een kopieeractiviteit die gebruikmaakt van een blob-bron- en een blob-sink gegevens vanaf de locatie van een Azure-blob kopiëren naar een andere locatie van de Azure-blob.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-516">The pipeline contains a copy activity that uses a blob source and a blob sink to copy data from an Azure blob location to another Azure blob location.</span></span> 

<span data-ttu-id="c4fd0-517">De volgende secties bevatten meer informatie over deze entiteiten.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-517">The following sections provide more information about these entities.</span></span> 

#### <a name="linked-services"></a><span data-ttu-id="c4fd0-518">Gekoppelde services</span><span class="sxs-lookup"><span data-stu-id="c4fd0-518">Linked services</span></span>
<span data-ttu-id="c4fd0-519">Hier ziet u twee gekoppelde services.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-519">You should see two linked services.</span></span> <span data-ttu-id="c4fd0-520">Een voor de bron en de andere is voor de bestemming.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-520">One for the source and the other one for the destination.</span></span> <span data-ttu-id="c4fd0-521">In dit overzicht beide definities er hetzelfde uitzien, met uitzondering van de namen.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-521">In this walkthrough, both definitions look the same except for the names.</span></span> <span data-ttu-id="c4fd0-522">De **type** van de gekoppelde service is ingesteld op **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-522">The **type** of the linked service is set to **AzureStorage**.</span></span> <span data-ttu-id="c4fd0-523">Belangrijkste eigenschap van de definitie van de gekoppelde service is de **connectionString**, die wordt gebruikt door de Data Factory verbinding maken met uw Azure Storage-account tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-523">Most important property of the linked service definition is the **connectionString**, which is used by Data Factory to connect to your Azure Storage account at runtime.</span></span> <span data-ttu-id="c4fd0-524">De eigenschap hubName in de definitie negeren.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-524">Ignore the hubName property in the definition.</span></span> 

##### <a name="source-blob-storage-linked-service"></a><span data-ttu-id="c4fd0-525">Bron blob-opslag gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="c4fd0-525">Source blob storage linked service</span></span>
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

##### <a name="destination-blob-storage-linked-service"></a><span data-ttu-id="c4fd0-526">Bestemming blob-opslag gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="c4fd0-526">Destination blob storage linked service</span></span>

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

<span data-ttu-id="c4fd0-527">Zie voor meer informatie over Azure Storage gekoppelde service [gekoppelde service-eigenschappen](#linked-service-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-527">For more information about Azure Storage linked service, see [Linked service properties](#linked-service-properties) section.</span></span> 

#### <a name="datasets"></a><span data-ttu-id="c4fd0-528">Gegevenssets</span><span class="sxs-lookup"><span data-stu-id="c4fd0-528">Datasets</span></span>
<span data-ttu-id="c4fd0-529">Er zijn twee gegevenssets: een invoergegevensset en een uitvoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-529">There are two datasets: an input dataset and an output dataset.</span></span> <span data-ttu-id="c4fd0-530">Het type van de gegevensset is ingesteld op **AzureBlob** voor beide.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-530">The type of the dataset is set to **AzureBlob** for both.</span></span> 

<span data-ttu-id="c4fd0-531">Invoergegevensset verwijst naar de **invoer** map van de **adfblobconnector** blob-container.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-531">The input dataset points to the **input** folder of the **adfblobconnector** blob container.</span></span> <span data-ttu-id="c4fd0-532">De **externe** eigenschap is ingesteld op **true** voor deze gegevensset omdat de gegevens niet wordt geproduceerd door de pijplijn met de kopieeractiviteit waarmee deze dataset als invoer.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-532">The **external** property is set to **true** for this dataset as the data is not produced by the pipeline with the copy activity that takes this dataset as an input.</span></span> 

<span data-ttu-id="c4fd0-533">De uitvoergegevensset die verwijst naar de **uitvoer** map van de dezelfde blobcontainer.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-533">The output dataset points to the **output** folder of the same blob container.</span></span> <span data-ttu-id="c4fd0-534">De uitvoergegevensset wordt ook gebruikgemaakt van het jaar, maand en dag van de **SliceStart** systeemvariabele dynamisch evalueren van het pad naar het uitvoerbestand.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-534">The output dataset also uses the year, month, and day of the **SliceStart** system variable to dynamically evaluate the path for the output file.</span></span> <span data-ttu-id="c4fd0-535">Zie voor een lijst met functies en ondersteund door Data Factory systeemvariabelen [Data Factory-functies en systeemvariabelen](data-factory-functions-variables.md).</span><span class="sxs-lookup"><span data-stu-id="c4fd0-535">For a list of functions and system variables supported by Data Factory, see [Data Factory functions and system variables](data-factory-functions-variables.md).</span></span> <span data-ttu-id="c4fd0-536">De **externe** eigenschap is ingesteld op **false** (standaardwaarde) omdat deze gegevensset wordt geproduceerd door de pijplijn.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-536">The **external** property is set to **false** (default value) because this dataset is produced by the pipeline.</span></span> 

<span data-ttu-id="c4fd0-537">Zie voor meer informatie over de eigenschappen die worden ondersteund door Azure Blob-gegevensset [eigenschappen van gegevensset](#dataset-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-537">For more information about properties supported by Azure Blob dataset, see [Dataset properties](#dataset-properties) section.</span></span>

##### <a name="input-dataset"></a><span data-ttu-id="c4fd0-538">Invoergegevensset</span><span class="sxs-lookup"><span data-stu-id="c4fd0-538">Input dataset</span></span>

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

##### <a name="output-dataset"></a><span data-ttu-id="c4fd0-539">Uitvoergegevensset</span><span class="sxs-lookup"><span data-stu-id="c4fd0-539">Output dataset</span></span>

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

#### <a name="pipeline"></a><span data-ttu-id="c4fd0-540">Pijplijn</span><span class="sxs-lookup"><span data-stu-id="c4fd0-540">Pipeline</span></span>
<span data-ttu-id="c4fd0-541">De pijplijn heeft slechts één activiteit.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-541">The pipeline has just one activity.</span></span> <span data-ttu-id="c4fd0-542">De **type** van de activiteit is ingesteld op **kopie**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-542">The **type** of the activity is set to **Copy**.</span></span>  <span data-ttu-id="c4fd0-543">In de type-eigenschappen voor de activiteit zijn er twee secties, één voor de gegevensbron en de andere één voor sink.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-543">In the type properties for the activity, there are two sections, one for source and the other one for sink.</span></span> <span data-ttu-id="c4fd0-544">Het brontype is ingesteld op **BlobSource** als de activiteit van gegevens van een blob-opslag kopiëren.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-544">The source type is set to **BlobSource** as the activity is copying data from a blob storage.</span></span> <span data-ttu-id="c4fd0-545">Het sink-type is ingesteld op **BlobSink** als de activiteit voor het kopiëren van gegevens naar een blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-545">The sink type is set to **BlobSink** as the activity copying data to a blob storage.</span></span> <span data-ttu-id="c4fd0-546">De kopieeractiviteit duurt InputDataset-z4y als invoer en OutputDataset-z4y als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-546">The copy activity takes InputDataset-z4y as the input and OutputDataset-z4y as the output.</span></span> 

<span data-ttu-id="c4fd0-547">Zie voor meer informatie over de eigenschappen die worden ondersteund door BlobSource en BlobSink [activiteitseigenschappen kopiëren](#copy-activity-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-547">For more information about properties supported by BlobSource and BlobSink, see [Copy activity properties](#copy-activity-properties) section.</span></span> 

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

## <a name="json-examples-for-copying-data-to-and-from-blob-storage"></a><span data-ttu-id="c4fd0-548">JSON-voorbeelden voor het kopiëren van gegevens naar en van Blob-opslag</span><span class="sxs-lookup"><span data-stu-id="c4fd0-548">JSON examples for copying data to and from Blob Storage</span></span>  
<span data-ttu-id="c4fd0-549">De volgende voorbeelden geven voorbeeld JSON definities die u een pijplijn maken kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c4fd0-549">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="c4fd0-550">Ze laten zien hoe gegevens van en naar Azure Blob Storage en Azure SQL Database kopiëren.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-550">They show how to copy data to and from Azure Blob Storage and Azure SQL Database.</span></span> <span data-ttu-id="c4fd0-551">Echter, de gegevens kunnen worden gekopieerd **rechtstreeks** uit een van de bronnen aan een van de PUT vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van de Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-551">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

### <a name="json-example-copy-data-from-blob-storage-to-sql-database"></a><span data-ttu-id="c4fd0-552">JSON-voorbeeld: Gegevens kopiëren van Blob-opslag naar SQL-Database</span><span class="sxs-lookup"><span data-stu-id="c4fd0-552">JSON Example: Copy data from Blob Storage to SQL Database</span></span>
<span data-ttu-id="c4fd0-553">Het volgende voorbeeld toont:</span><span class="sxs-lookup"><span data-stu-id="c4fd0-553">The following sample shows:</span></span>

1. <span data-ttu-id="c4fd0-554">Een gekoppelde service van het type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c4fd0-554">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="c4fd0-555">Een gekoppelde service van het type [AzureStorage](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c4fd0-555">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="c4fd0-556">Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c4fd0-556">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
4. <span data-ttu-id="c4fd0-557">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c4fd0-557">An output [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="c4fd0-558">Een [pijplijn](data-factory-create-pipelines.md) met een kopieeractiviteit die gebruikmaakt van [BlobSource](#copy-activity-properties) en [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="c4fd0-558">A [pipeline](data-factory-create-pipelines.md) with a Copy activity that uses [BlobSource](#copy-activity-properties) and [SqlSink](data-factory-azure-sql-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="c4fd0-559">De voorbeeld-kopieën timeseries gegevens van een Azure-blob naar een Azure SQL tabel per uur.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-559">The sample copies time-series data from an Azure blob to an Azure SQL table hourly.</span></span> <span data-ttu-id="c4fd0-560">De JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na de voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-560">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="c4fd0-561">**Azure SQL gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="c4fd0-561">**Azure SQL linked service:**</span></span>

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
<span data-ttu-id="c4fd0-562">**Gekoppelde Azure Storage-service:**</span><span class="sxs-lookup"><span data-stu-id="c4fd0-562">**Azure Storage linked service:**</span></span>

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
<span data-ttu-id="c4fd0-563">Azure Data Factory ondersteunt twee soorten gekoppelde Azure Storage-services: **AzureStorage** en **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-563">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="c4fd0-564">U de verbindingsreeks met de sleutel van de account opgeven voor de eerste en voor de latere, geeft u de Shared Access Signature (SAS)-Uri.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-564">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="c4fd0-565">Zie [gekoppelde Services](#linked-service-properties) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-565">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="c4fd0-566">**Azure Blob invoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="c4fd0-566">**Azure Blob input dataset:**</span></span>

<span data-ttu-id="c4fd0-567">Gegevens wordt opgehaald uit een nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="c4fd0-567">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="c4fd0-568">Pad en naam van de map voor de blob worden dynamisch geëvalueerd op basis van de begintijd van het segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-568">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="c4fd0-569">Het mappad gebruikt jaar, maand en dag deel uit van de begintijd en de bestandsnaam wordt gebruikt voor het uur deel van de begintijd.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-569">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="c4fd0-570">"extern": "true" instelling Data Factory informeert dat de tabel aan de gegevensfactory extern en niet wordt geproduceerd door een activiteit in de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-570">“external”: “true” setting informs Data Factory that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="c4fd0-571">**Azure SQL-uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="c4fd0-571">**Azure SQL output dataset:**</span></span>

<span data-ttu-id="c4fd0-572">De voorbeeldgegevens kopieert naar een tabel met de naam "MijnTabel" in een Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-572">The sample copies data to a table named “MyTable” in an Azure SQL database.</span></span> <span data-ttu-id="c4fd0-573">De tabel in uw Azure SQL database met hetzelfde aantal kolommen maken, zoals u verwacht dat de Blob-CSV-bestand bevatten.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-573">Create the table in your Azure SQL database with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="c4fd0-574">Nieuwe rijen worden toegevoegd aan de tabel om het uur.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-574">New rows are added to the table every hour.</span></span>

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
<span data-ttu-id="c4fd0-575">**Een kopieeractiviteit in een pijplijn met Blob-bron en sink SQL:**</span><span class="sxs-lookup"><span data-stu-id="c4fd0-575">**A copy activity in a pipeline with Blob source and SQL sink:**</span></span>

<span data-ttu-id="c4fd0-576">De pijplijn bevat een Kopieeractiviteit die is geconfigureerd voor gebruik van de invoer- en uitvoergegevenssets en elk uur is gepland.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-576">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="c4fd0-577">In de pijplijn-JSON-definitie de **bron** type is ingesteld op **BlobSource** en **sink** type is ingesteld op **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-577">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

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
### <a name="json-example-copy-data-from-azure-sql-to-azure-blob"></a><span data-ttu-id="c4fd0-578">JSON-voorbeeld: Gegevens kopiëren van Azure SQL naar Azure Blob</span><span class="sxs-lookup"><span data-stu-id="c4fd0-578">JSON Example: Copy data from Azure SQL to Azure Blob</span></span>
<span data-ttu-id="c4fd0-579">Het volgende voorbeeld toont:</span><span class="sxs-lookup"><span data-stu-id="c4fd0-579">The following sample shows:</span></span>

1. <span data-ttu-id="c4fd0-580">Een gekoppelde service van het type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c4fd0-580">A linked service of type [AzureSqlDatabase](data-factory-azure-sql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="c4fd0-581">Een gekoppelde service van het type [AzureStorage](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c4fd0-581">A linked service of type [AzureStorage](#linked-service-properties).</span></span>
3. <span data-ttu-id="c4fd0-582">Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c4fd0-582">An input [dataset](data-factory-create-datasets.md) of type [AzureSqlTable](data-factory-azure-sql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="c4fd0-583">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c4fd0-583">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](#dataset-properties).</span></span>
5. <span data-ttu-id="c4fd0-584">Een [pijplijn](data-factory-create-pipelines.md) met de kopieeractiviteit die gebruikmaakt van [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) en [BlobSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="c4fd0-584">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](data-factory-azure-sql-connector.md#copy-activity-properties) and [BlobSink](#copy-activity-properties).</span></span>

<span data-ttu-id="c4fd0-585">Het voorbeeld kopieert tijdreeks gegevens van een Azure SQL-tabel naar een Azure-blob per uur.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-585">The sample copies time-series data from an Azure SQL table to an Azure blob hourly.</span></span> <span data-ttu-id="c4fd0-586">De JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na de voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-586">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="c4fd0-587">**Azure SQL gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="c4fd0-587">**Azure SQL linked service:**</span></span>

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
<span data-ttu-id="c4fd0-588">**Gekoppelde Azure Storage-service:**</span><span class="sxs-lookup"><span data-stu-id="c4fd0-588">**Azure Storage linked service:**</span></span>

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
<span data-ttu-id="c4fd0-589">Azure Data Factory ondersteunt twee soorten gekoppelde Azure Storage-services: **AzureStorage** en **AzureStorageSas**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-589">Azure Data Factory supports two types of Azure Storage linked services: **AzureStorage** and **AzureStorageSas**.</span></span> <span data-ttu-id="c4fd0-590">U de verbindingsreeks met de sleutel van de account opgeven voor de eerste en voor de latere, geeft u de Shared Access Signature (SAS)-Uri.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-590">For the first one, you specify the connection string that includes the account key and for the later one, you specify the Shared Access Signature (SAS) Uri.</span></span> <span data-ttu-id="c4fd0-591">Zie [gekoppelde Services](#linked-service-properties) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-591">See [Linked Services](#linked-service-properties) section for details.</span></span>  

<span data-ttu-id="c4fd0-592">**Azure SQL invoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="c4fd0-592">**Azure SQL input dataset:**</span></span>

<span data-ttu-id="c4fd0-593">Het voorbeeld wordt ervan uitgegaan dat u hebt een tabel 'MijnTabel' gemaakt in Azure SQL en bevat een kolom met de naam 'timestampcolumn' voor de reeksgegevens.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-593">The sample assumes you have created a table “MyTable” in Azure SQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="c4fd0-594">Instelling 'extern': 'true' informeert Data Factory-service dat de tabel aan de gegevensfactory extern en niet wordt geproduceerd door een activiteit in de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-594">Setting “external”: ”true” informs Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="c4fd0-595">**Azure Blob-uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="c4fd0-595">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="c4fd0-596">Gegevens worden geschreven naar een nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="c4fd0-596">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="c4fd0-597">Het pad naar de blob wordt dynamisch geëvalueerd op basis van de begintijd van het segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-597">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="c4fd0-598">Het mappad maakt gebruik van jaar, maand, dag en uur delen van de begintijd.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-598">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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

<span data-ttu-id="c4fd0-599">**Een kopieeractiviteit in een pijplijn met de SQL-bron en sink van Blob:**</span><span class="sxs-lookup"><span data-stu-id="c4fd0-599">**A copy activity in a pipeline with SQL source and Blob sink:**</span></span>

<span data-ttu-id="c4fd0-600">De pijplijn bevat een Kopieeractiviteit die is geconfigureerd voor gebruik van de invoer- en uitvoergegevenssets en elk uur is gepland.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-600">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="c4fd0-601">In de pijplijn-JSON-definitie de **bron** type is ingesteld op **SqlSource** en **sink** type is ingesteld op **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-601">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="c4fd0-602">De SQL-query die is opgegeven voor de **SqlReaderQuery** eigenschap selecteert u de gegevens in het afgelopen uur te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-602">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

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
> <span data-ttu-id="c4fd0-603">Zie het toewijzen van kolommen uit de bron-gegevensset naar kolommen uit de dataset sink [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="c4fd0-603">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="c4fd0-604">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="c4fd0-604">Performance and Tuning</span></span>
<span data-ttu-id="c4fd0-605">Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) voor meer informatie over de belangrijkste factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren om te optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="c4fd0-605">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
