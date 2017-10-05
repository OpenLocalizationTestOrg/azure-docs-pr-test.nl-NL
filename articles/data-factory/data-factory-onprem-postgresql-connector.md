---
title: Verplaatsen van gegevens van PostgreSQL met behulp van Azure Data Factory | Microsoft Docs
description: Meer informatie over het verplaatsen van gegevens uit een PostgreSQL-Database met behulp van Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 888d9ebc-2500-4071-b6d1-0f6bd1b5997c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: fd26f0d03f8b0b352a6544a81ad952d2e2a1b7a0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-postgresql-using-azure-data-factory"></a><span data-ttu-id="4aad3-103">Verplaatsen van gegevens uit een PostgreSQL met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="4aad3-103">Move data from PostgreSQL using Azure Data Factory</span></span>
<span data-ttu-id="4aad3-104">In dit artikel wordt uitgelegd hoe de Kopieeractiviteit in Azure Data Factory om gegevens te verplaatsen van een on-premises PostgreSQL-database gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4aad3-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises PostgreSQL database.</span></span> <span data-ttu-id="4aad3-105">Dit is gebaseerd op de [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, hetgeen een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit toont.</span><span class="sxs-lookup"><span data-stu-id="4aad3-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="4aad3-106">U kunt gegevens uit een on-premises PostgreSQL-gegevensopslag kopiëren naar een ondersteunde sink data store.</span><span class="sxs-lookup"><span data-stu-id="4aad3-106">You can copy data from an on-premises PostgreSQL data store to any supported sink data store.</span></span> <span data-ttu-id="4aad3-107">Zie voor een lijst met gegevensarchieven als PUT wordt ondersteund door de kopieeractiviteit, [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="4aad3-107">For a list of data stores supported as sinks by the copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="4aad3-108">Data factory ondersteunt momenteel zwevend gegevens uit een PostgreSQL-database op andere gegevensarchieven, maar niet voor het verplaatsen van gegevens uit andere gegevensarchieven naar een PostgreSQL-database.</span><span class="sxs-lookup"><span data-stu-id="4aad3-108">Data factory currently supports moving data from a PostgreSQL database to other data stores, but not for moving data from other data stores to an PostgreSQL database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4aad3-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4aad3-109">prerequisites</span></span>

<span data-ttu-id="4aad3-110">Verbinding maken met lokale PostgreSQL bronnen met behulp van Data Management Gateway biedt ondersteuning voor Data Factory-service.</span><span class="sxs-lookup"><span data-stu-id="4aad3-110">Data Factory service supports connecting to on-premises PostgreSQL sources using the Data Management Gateway.</span></span> <span data-ttu-id="4aad3-111">Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor meer informatie over Data Management Gateway en stapsgewijze instructies over het instellen van de gateway.</span><span class="sxs-lookup"><span data-stu-id="4aad3-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="4aad3-112">Gateway is vereist, zelfs als de PostgreSQL-database wordt gehost in een Azure IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="4aad3-112">Gateway is required even if the PostgreSQL database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="4aad3-113">U kunt gateway installeren op de dezelfde IaaS VM als gegevensopslag of op een andere virtuele machine, zolang de gateway verbinding met de database maken kan.</span><span class="sxs-lookup"><span data-stu-id="4aad3-113">You can install gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="4aad3-114">Zie [gateway problemen](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) voor tips over het oplossen van verbinding of gateway gerelateerde problemen.</span><span class="sxs-lookup"><span data-stu-id="4aad3-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="4aad3-115">Ondersteunde versies en installatie</span><span class="sxs-lookup"><span data-stu-id="4aad3-115">Supported versions and installation</span></span>
<span data-ttu-id="4aad3-116">Voor de Data Management Gateway verbinding maken met de PostgreSQL-Database, installeert u de [Ngpsql-gegevensprovider voor PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 of hoger op hetzelfde systeem als Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="4aad3-116">For Data Management Gateway to connect to the PostgreSQL Database, install the [Ngpsql data provider for PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 or above on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="4aad3-117">PostgreSQL versie 7.4 en hoger wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="4aad3-117">PostgreSQL version 7.4 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="4aad3-118">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="4aad3-118">Getting started</span></span>
<span data-ttu-id="4aad3-119">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens vanuit een on-premises PostgreSQL-gegevensopslag verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="4aad3-119">You can create a pipeline with a copy activity that moves data from an on-premises PostgreSQL data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="4aad3-120">De eenvoudigste manier om een pijplijn maken is met de **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="4aad3-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="4aad3-121">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met de wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="4aad3-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="4aad3-122">U kunt ook de volgende hulpprogramma's gebruiken voor het maken van een pijplijn:</span><span class="sxs-lookup"><span data-stu-id="4aad3-122">You can also use the following tools to create a pipeline:</span></span> 
    - <span data-ttu-id="4aad3-123">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="4aad3-123">Azure portal</span></span>
    - <span data-ttu-id="4aad3-124">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4aad3-124">Visual Studio</span></span>
    - <span data-ttu-id="4aad3-125">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4aad3-125">Azure PowerShell</span></span>
    - <span data-ttu-id="4aad3-126">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="4aad3-126">Azure Resource Manager template</span></span>
    - <span data-ttu-id="4aad3-127">.NET API</span><span class="sxs-lookup"><span data-stu-id="4aad3-127">.NET API</span></span>
    - <span data-ttu-id="4aad3-128">REST API</span><span class="sxs-lookup"><span data-stu-id="4aad3-128">REST API</span></span>

     <span data-ttu-id="4aad3-129">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies voor een pijplijn maken met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="4aad3-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="4aad3-130">Of u de hulpprogramma's of API's gebruiken, moet u de volgende stappen voor het maken van een pijplijn die de gegevens vanuit een brongegevensarchief naar een gegevensarchief sink verplaatst uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="4aad3-130">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="4aad3-131">Maak **gekoppelde services** slaat om invoer- en gegevens te koppelen aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="4aad3-131">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="4aad3-132">Maak **gegevenssets** vertegenwoordigt de invoer- en -gegevens voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="4aad3-132">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="4aad3-133">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="4aad3-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="4aad3-134">Wanneer u de wizard gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4aad3-134">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="4aad3-135">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van de JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="4aad3-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="4aad3-136">Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die worden gebruikt om gegevens te kopiëren uit een on-premises PostgreSQL-gegevensopslag [JSON-voorbeeld: gegevens kopiëren van PostgreSQL naar Azure Blob](#json-example-copy-data-from-postgresql-to-azure-blob) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="4aad3-136">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises PostgreSQL data store, see [JSON example: Copy data from PostgreSQL to Azure Blob](#json-example-copy-data-from-postgresql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="4aad3-137">De volgende secties bevatten informatie over de JSON-eigenschappen die worden gebruikt voor het definiëren van Data Factory-entiteiten specifieke naar een PostgreSQL-gegevensopslag:</span><span class="sxs-lookup"><span data-stu-id="4aad3-137">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a PostgreSQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="4aad3-138">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="4aad3-138">Linked service properties</span></span>
<span data-ttu-id="4aad3-139">De volgende tabel bevat een beschrijving voor JSON-elementen die specifiek zijn voor PostgreSQL gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="4aad3-139">The following table provides description for JSON elements specific to PostgreSQL linked service.</span></span>

| <span data-ttu-id="4aad3-140">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="4aad3-140">Property</span></span> | <span data-ttu-id="4aad3-141">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4aad3-141">Description</span></span> | <span data-ttu-id="4aad3-142">Vereist</span><span class="sxs-lookup"><span data-stu-id="4aad3-142">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4aad3-143">type</span><span class="sxs-lookup"><span data-stu-id="4aad3-143">type</span></span> |<span data-ttu-id="4aad3-144">De eigenschap type moet worden ingesteld op: **OnPremisesPostgreSql**</span><span class="sxs-lookup"><span data-stu-id="4aad3-144">The type property must be set to: **OnPremisesPostgreSql**</span></span> |<span data-ttu-id="4aad3-145">Ja</span><span class="sxs-lookup"><span data-stu-id="4aad3-145">Yes</span></span> |
| <span data-ttu-id="4aad3-146">server</span><span class="sxs-lookup"><span data-stu-id="4aad3-146">server</span></span> |<span data-ttu-id="4aad3-147">De naam van de PostgreSQL-server.</span><span class="sxs-lookup"><span data-stu-id="4aad3-147">Name of the PostgreSQL server.</span></span> |<span data-ttu-id="4aad3-148">Ja</span><span class="sxs-lookup"><span data-stu-id="4aad3-148">Yes</span></span> |
| <span data-ttu-id="4aad3-149">database</span><span class="sxs-lookup"><span data-stu-id="4aad3-149">database</span></span> |<span data-ttu-id="4aad3-150">De naam van de PostgreSQL-database.</span><span class="sxs-lookup"><span data-stu-id="4aad3-150">Name of the PostgreSQL database.</span></span> |<span data-ttu-id="4aad3-151">Ja</span><span class="sxs-lookup"><span data-stu-id="4aad3-151">Yes</span></span> |
| <span data-ttu-id="4aad3-152">Schema</span><span class="sxs-lookup"><span data-stu-id="4aad3-152">schema</span></span> |<span data-ttu-id="4aad3-153">De naam van het schema in de database.</span><span class="sxs-lookup"><span data-stu-id="4aad3-153">Name of the schema in the database.</span></span> <span data-ttu-id="4aad3-154">Naam van het schema is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="4aad3-154">The schema name is case-sensitive.</span></span> |<span data-ttu-id="4aad3-155">Nee</span><span class="sxs-lookup"><span data-stu-id="4aad3-155">No</span></span> |
| <span data-ttu-id="4aad3-156">authenticationType</span><span class="sxs-lookup"><span data-stu-id="4aad3-156">authenticationType</span></span> |<span data-ttu-id="4aad3-157">Het soort verificatie die wordt gebruikt voor verbinding met de PostgreSQL-database.</span><span class="sxs-lookup"><span data-stu-id="4aad3-157">Type of authentication used to connect to the PostgreSQL database.</span></span> <span data-ttu-id="4aad3-158">Mogelijke waarden zijn: anoniem, basis en Windows.</span><span class="sxs-lookup"><span data-stu-id="4aad3-158">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="4aad3-159">Ja</span><span class="sxs-lookup"><span data-stu-id="4aad3-159">Yes</span></span> |
| <span data-ttu-id="4aad3-160">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="4aad3-160">username</span></span> |<span data-ttu-id="4aad3-161">Geef de gebruikersnaam als u basisverificatie of Windows-verificatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4aad3-161">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="4aad3-162">Nee</span><span class="sxs-lookup"><span data-stu-id="4aad3-162">No</span></span> |
| <span data-ttu-id="4aad3-163">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="4aad3-163">password</span></span> |<span data-ttu-id="4aad3-164">Wachtwoord voor het gebruikersaccount dat u hebt opgegeven voor de gebruikersnaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="4aad3-164">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="4aad3-165">Nee</span><span class="sxs-lookup"><span data-stu-id="4aad3-165">No</span></span> |
| <span data-ttu-id="4aad3-166">gatewayName</span><span class="sxs-lookup"><span data-stu-id="4aad3-166">gatewayName</span></span> |<span data-ttu-id="4aad3-167">Naam van de gateway die voor de Data Factory-service gebruiken moet voor verbinding met de lokale PostgreSQL-database.</span><span class="sxs-lookup"><span data-stu-id="4aad3-167">Name of the gateway that the Data Factory service should use to connect to the on-premises PostgreSQL database.</span></span> |<span data-ttu-id="4aad3-168">Ja</span><span class="sxs-lookup"><span data-stu-id="4aad3-168">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="4aad3-169">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="4aad3-169">Dataset properties</span></span>
<span data-ttu-id="4aad3-170">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van de [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="4aad3-170">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="4aad3-171">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle typen van de gegevensset.</span><span class="sxs-lookup"><span data-stu-id="4aad3-171">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="4aad3-172">De sectie typeProperties verschilt voor elk type gegevensset en bevat informatie over de locatie van de gegevens in het gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="4aad3-172">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="4aad3-173">De typeProperties sectie voor de gegevensset van het type **RelationalTable** (inclusief PostgreSQL gegevensset) heeft de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="4aad3-173">The typeProperties section for dataset of type **RelationalTable** (which includes PostgreSQL dataset) has the following properties:</span></span>

| <span data-ttu-id="4aad3-174">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="4aad3-174">Property</span></span> | <span data-ttu-id="4aad3-175">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4aad3-175">Description</span></span> | <span data-ttu-id="4aad3-176">Vereist</span><span class="sxs-lookup"><span data-stu-id="4aad3-176">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4aad3-177">tableName</span><span class="sxs-lookup"><span data-stu-id="4aad3-177">tableName</span></span> |<span data-ttu-id="4aad3-178">De naam van de tabel in de PostgreSQL-Database-instantie waarnaar de gekoppelde service verwijst.</span><span class="sxs-lookup"><span data-stu-id="4aad3-178">Name of the table in the PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="4aad3-179">De tabelnaam is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="4aad3-179">The tableName is case-sensitive.</span></span> |<span data-ttu-id="4aad3-180">Nee (als **query** van **RelationalSource** is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="4aad3-180">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="4aad3-181">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="4aad3-181">Copy activity properties</span></span>
<span data-ttu-id="4aad3-182">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van activiteiten van de [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="4aad3-182">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="4aad3-183">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en -beleid zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="4aad3-183">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="4aad3-184">Terwijl de eigenschappen die beschikbaar zijn in de sectie typeProperties van de activiteit variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="4aad3-184">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="4aad3-185">Voor de kopieeractiviteit variëren ze, afhankelijk van de typen van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="4aad3-185">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="4aad3-186">Wanneer de bron is van het type **RelationalSource** (waaronder PostgreSQL), de volgende eigenschappen beschikbaar zijn in de sectie typeProperties:</span><span class="sxs-lookup"><span data-stu-id="4aad3-186">When source is of type **RelationalSource** (which includes PostgreSQL), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="4aad3-187">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="4aad3-187">Property</span></span> | <span data-ttu-id="4aad3-188">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4aad3-188">Description</span></span> | <span data-ttu-id="4aad3-189">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="4aad3-189">Allowed values</span></span> | <span data-ttu-id="4aad3-190">Vereist</span><span class="sxs-lookup"><span data-stu-id="4aad3-190">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4aad3-191">query</span><span class="sxs-lookup"><span data-stu-id="4aad3-191">query</span></span> |<span data-ttu-id="4aad3-192">Gebruik de aangepaste query om gegevens te lezen.</span><span class="sxs-lookup"><span data-stu-id="4aad3-192">Use the custom query to read data.</span></span> |<span data-ttu-id="4aad3-193">SQL-query-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="4aad3-193">SQL query string.</span></span> <span data-ttu-id="4aad3-194">Bijvoorbeeld: "query": "Selecteer * uit \"MySchema\".\" MyTable\"'.</span><span class="sxs-lookup"><span data-stu-id="4aad3-194">For example: "query": "select * from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="4aad3-195">Nee (als **tableName** van **gegevensset** is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="4aad3-195">No (if **tableName** of **dataset** is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="4aad3-196">Schema- en tabelnamen zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="4aad3-196">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="4aad3-197">Omsluiten in `""` (dubbele aanhalingstekens) in de query.</span><span class="sxs-lookup"><span data-stu-id="4aad3-197">Enclose them in `""` (double quotes) in the query.</span></span>  

<span data-ttu-id="4aad3-198">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="4aad3-198">**Example:**</span></span>

 `"query": "select * from \"MySchema\".\"MyTable\""`

## <a name="json-example-copy-data-from-postgresql-to-azure-blob"></a><span data-ttu-id="4aad3-199">JSON-voorbeeld: gegevens kopiëren van PostgreSQL naar Azure Blob</span><span class="sxs-lookup"><span data-stu-id="4aad3-199">JSON example: Copy data from PostgreSQL to Azure Blob</span></span>
<span data-ttu-id="4aad3-200">In dit voorbeeld bevat definities van de voorbeeld-JSON die u een pijplijn maken kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="4aad3-200">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="4aad3-201">Ze laten zien hoe gegevens uit een PostgreSQL-database kopiëren naar Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="4aad3-201">They show how to copy data from PostgreSQL database to Azure Blob Storage.</span></span> <span data-ttu-id="4aad3-202">Gegevens kunnen echter worden gekopieerd naar een van de PUT vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van de Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="4aad3-202">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="4aad3-203">Dit voorbeeld bevat JSON-fragmenten.</span><span class="sxs-lookup"><span data-stu-id="4aad3-203">This sample provides JSON snippets.</span></span> <span data-ttu-id="4aad3-204">Dit omvat geen stapsgewijze instructies voor het maken van de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="4aad3-204">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="4aad3-205">Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor stapsgewijze instructies.</span><span class="sxs-lookup"><span data-stu-id="4aad3-205">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="4aad3-206">Het voorbeeld heeft de volgende data factory-entiteiten:</span><span class="sxs-lookup"><span data-stu-id="4aad3-206">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="4aad3-207">Een gekoppelde service van het type [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4aad3-207">A linked service of type [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="4aad3-208">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4aad3-208">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="4aad3-209">Invoer [gegevensset](data-factory-create-datasets.md) van het type [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4aad3-209">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="4aad3-210">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4aad3-210">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="4aad3-211">De [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="4aad3-211">The [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="4aad3-212">Het voorbeeld kopieert gegevens van de resultaten van een query in een PostgreSQL-database naar een blob elk uur.</span><span class="sxs-lookup"><span data-stu-id="4aad3-212">The sample copies data from a query result in PostgreSQL database to a blob every hour.</span></span> <span data-ttu-id="4aad3-213">De JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na de voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="4aad3-213">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="4aad3-214">Het instellen van de data management gateway als eerste stap.</span><span class="sxs-lookup"><span data-stu-id="4aad3-214">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="4aad3-215">De instructies vindt u in de [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="4aad3-215">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="4aad3-216">**PostgreSQL gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="4aad3-216">**PostgreSQL linked service:**</span></span>

```json
{
    "name": "OnPremPostgreSqlLinkedService",
    "properties": {
        "type": "OnPremisesPostgreSql",
        "typeProperties": {
            "server": "<server>",
            "database": "<database>",
            "schema": "<schema>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```
<span data-ttu-id="4aad3-217">**Azure Blob-opslag gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="4aad3-217">**Azure Blob storage linked service:**</span></span>

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
    "type": "AzureStorage",
    "typeProperties": {
        "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
    }
    }
}
```
<span data-ttu-id="4aad3-218">**PostgreSQL invoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="4aad3-218">**PostgreSQL input dataset:**</span></span>

<span data-ttu-id="4aad3-219">Het voorbeeld wordt ervan uitgegaan dat u hebt een tabel 'MijnTabel' gemaakt in PostgreSQL en bevat een kolom met de naam 'tijdstempel' voor de reeksgegevens.</span><span class="sxs-lookup"><span data-stu-id="4aad3-219">The sample assumes you have created a table “MyTable” in PostgreSQL and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="4aad3-220">Instelling `"external": true` informeert de Data Factory-service dat de dataset extern is aan de gegevensfactory en niet wordt geproduceerd door een activiteit in de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="4aad3-220">Setting `"external": true` informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "PostgreSqlDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremPostgreSqlLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

<span data-ttu-id="4aad3-221">**Azure Blob-uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="4aad3-221">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="4aad3-222">Gegevens worden geschreven naar een nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="4aad3-222">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="4aad3-223">Pad en naam van de map voor de blob worden dynamisch geëvalueerd op basis van de begintijd van het segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="4aad3-223">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="4aad3-224">Het mappad maakt gebruik van jaar, maand, dag en uur delen van de begintijd.</span><span class="sxs-lookup"><span data-stu-id="4aad3-224">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobPostgreSqlDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/postgresql/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="4aad3-225">**Pijplijn met de kopieeractiviteit:**</span><span class="sxs-lookup"><span data-stu-id="4aad3-225">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="4aad3-226">De pijplijn bevat een Kopieeractiviteit die is geconfigureerd voor gebruik van de invoer- en uitvoergegevenssets en is gepland voor uitvoering per uur.</span><span class="sxs-lookup"><span data-stu-id="4aad3-226">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="4aad3-227">In de pijplijn-JSON-definitie de **bron** type is ingesteld op **RelationalSource** en **sink** type is ingesteld op **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="4aad3-227">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="4aad3-228">De SQL-query die is opgegeven voor de **query** eigenschap selecteert u de gegevens uit de tabel public.usstates in de PostgreSQL-database.</span><span class="sxs-lookup"><span data-stu-id="4aad3-228">The SQL query specified for the **query** property selects the data from the public.usstates table in the PostgreSQL database.</span></span>

```json
{
    "name": "CopyPostgreSqlToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"public\".\"usstates\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "PostgreSqlDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobPostgreSqlDataSet"
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
                "name": "PostgreSqlToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```
## <a name="type-mapping-for-postgresql"></a><span data-ttu-id="4aad3-229">Toewijzing van het type voor PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="4aad3-229">Type mapping for PostgreSQL</span></span>
<span data-ttu-id="4aad3-230">Zoals vermeld in de [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel kopieeractiviteit voert automatische typeconversies van brontypen opvangen typen met de volgende stappen 2-benadering:</span><span class="sxs-lookup"><span data-stu-id="4aad3-230">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="4aad3-231">Systeemeigen brontypen converteren naar .NET-type</span><span class="sxs-lookup"><span data-stu-id="4aad3-231">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="4aad3-232">Converteren van .NET-type naar systeemeigen sink-type</span><span class="sxs-lookup"><span data-stu-id="4aad3-232">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="4aad3-233">Wanneer u gegevens naar PostgreSQL verplaatst, worden de volgende toewijzingen van PostgreSQL type gebruikt voor .NET-type.</span><span class="sxs-lookup"><span data-stu-id="4aad3-233">When moving data to PostgreSQL, the following mappings are used from PostgreSQL type to .NET type.</span></span>

| <span data-ttu-id="4aad3-234">Type PostgreSQL-Database</span><span class="sxs-lookup"><span data-stu-id="4aad3-234">PostgreSQL Database type</span></span> | <span data-ttu-id="4aad3-235">PostgresSQL aliassen</span><span class="sxs-lookup"><span data-stu-id="4aad3-235">PostgresSQL aliases</span></span> | <span data-ttu-id="4aad3-236">.NET framework-type</span><span class="sxs-lookup"><span data-stu-id="4aad3-236">.NET Framework type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4aad3-237">abstime</span><span class="sxs-lookup"><span data-stu-id="4aad3-237">abstime</span></span> | |<span data-ttu-id="4aad3-238">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="4aad3-238">Datetime</span></span> | &nbsp;
| <span data-ttu-id="4aad3-239">bigint</span><span class="sxs-lookup"><span data-stu-id="4aad3-239">bigint</span></span> |<span data-ttu-id="4aad3-240">int8</span><span class="sxs-lookup"><span data-stu-id="4aad3-240">int8</span></span> |<span data-ttu-id="4aad3-241">Int64</span><span class="sxs-lookup"><span data-stu-id="4aad3-241">Int64</span></span> |
| <span data-ttu-id="4aad3-242">bigserial</span><span class="sxs-lookup"><span data-stu-id="4aad3-242">bigserial</span></span> |<span data-ttu-id="4aad3-243">serial8</span><span class="sxs-lookup"><span data-stu-id="4aad3-243">serial8</span></span> |<span data-ttu-id="4aad3-244">Int64</span><span class="sxs-lookup"><span data-stu-id="4aad3-244">Int64</span></span> |
| <span data-ttu-id="4aad3-245">bits [(n)]</span><span class="sxs-lookup"><span data-stu-id="4aad3-245">bit [ (n) ]</span></span> | |<span data-ttu-id="4aad3-246">Byte [], String</span><span class="sxs-lookup"><span data-stu-id="4aad3-246">Byte[], String</span></span> | &nbsp;
| <span data-ttu-id="4aad3-247">bit uiteenlopende [(n)]</span><span class="sxs-lookup"><span data-stu-id="4aad3-247">bit varying [ (n) ]</span></span> |<span data-ttu-id="4aad3-248">varbit</span><span class="sxs-lookup"><span data-stu-id="4aad3-248">varbit</span></span> |<span data-ttu-id="4aad3-249">Byte [], String</span><span class="sxs-lookup"><span data-stu-id="4aad3-249">Byte[], String</span></span> |
| <span data-ttu-id="4aad3-250">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="4aad3-250">boolean</span></span> |<span data-ttu-id="4aad3-251">BOOL</span><span class="sxs-lookup"><span data-stu-id="4aad3-251">bool</span></span> |<span data-ttu-id="4aad3-252">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="4aad3-252">Boolean</span></span> |
| <span data-ttu-id="4aad3-253">Vak</span><span class="sxs-lookup"><span data-stu-id="4aad3-253">box</span></span> | |<span data-ttu-id="4aad3-254">Byte [], String</span><span class="sxs-lookup"><span data-stu-id="4aad3-254">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="4aad3-255">bytea</span><span class="sxs-lookup"><span data-stu-id="4aad3-255">bytea</span></span> | |<span data-ttu-id="4aad3-256">Byte [], String</span><span class="sxs-lookup"><span data-stu-id="4aad3-256">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="4aad3-257">teken [(n)]</span><span class="sxs-lookup"><span data-stu-id="4aad3-257">character [ (n) ]</span></span> |<span data-ttu-id="4aad3-258">char [(n)]</span><span class="sxs-lookup"><span data-stu-id="4aad3-258">char [ (n) ]</span></span> |<span data-ttu-id="4aad3-259">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4aad3-259">String</span></span> |
| <span data-ttu-id="4aad3-260">teken wisselende [(n)]</span><span class="sxs-lookup"><span data-stu-id="4aad3-260">character varying [ (n) ]</span></span> |<span data-ttu-id="4aad3-261">varchar [(n)]</span><span class="sxs-lookup"><span data-stu-id="4aad3-261">varchar [ (n) ]</span></span> |<span data-ttu-id="4aad3-262">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4aad3-262">String</span></span> |
| <span data-ttu-id="4aad3-263">CID</span><span class="sxs-lookup"><span data-stu-id="4aad3-263">cid</span></span> | |<span data-ttu-id="4aad3-264">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4aad3-264">String</span></span> |&nbsp;
| <span data-ttu-id="4aad3-265">CIDR</span><span class="sxs-lookup"><span data-stu-id="4aad3-265">cidr</span></span> | |<span data-ttu-id="4aad3-266">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4aad3-266">String</span></span> |&nbsp;
| <span data-ttu-id="4aad3-267">cirkel</span><span class="sxs-lookup"><span data-stu-id="4aad3-267">circle</span></span> | |<span data-ttu-id="4aad3-268">Byte [], String</span><span class="sxs-lookup"><span data-stu-id="4aad3-268">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="4aad3-269">Datum</span><span class="sxs-lookup"><span data-stu-id="4aad3-269">date</span></span> | |<span data-ttu-id="4aad3-270">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="4aad3-270">Datetime</span></span> |&nbsp;
| <span data-ttu-id="4aad3-271">DateRange</span><span class="sxs-lookup"><span data-stu-id="4aad3-271">daterange</span></span> | |<span data-ttu-id="4aad3-272">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4aad3-272">String</span></span> |&nbsp;
| <span data-ttu-id="4aad3-273">dubbele precisie</span><span class="sxs-lookup"><span data-stu-id="4aad3-273">double precision</span></span> |<span data-ttu-id="4aad3-274">FLOAT8</span><span class="sxs-lookup"><span data-stu-id="4aad3-274">float8</span></span> |<span data-ttu-id="4aad3-275">dubbele</span><span class="sxs-lookup"><span data-stu-id="4aad3-275">Double</span></span> |
| <span data-ttu-id="4aad3-276">INet</span><span class="sxs-lookup"><span data-stu-id="4aad3-276">inet</span></span> | |<span data-ttu-id="4aad3-277">Byte [], String</span><span class="sxs-lookup"><span data-stu-id="4aad3-277">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="4aad3-278">intarry</span><span class="sxs-lookup"><span data-stu-id="4aad3-278">intarry</span></span> | |<span data-ttu-id="4aad3-279">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4aad3-279">String</span></span> |&nbsp;
| <span data-ttu-id="4aad3-280">int4range</span><span class="sxs-lookup"><span data-stu-id="4aad3-280">int4range</span></span> | |<span data-ttu-id="4aad3-281">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4aad3-281">String</span></span> |&nbsp;
| <span data-ttu-id="4aad3-282">int8range</span><span class="sxs-lookup"><span data-stu-id="4aad3-282">int8range</span></span> | |<span data-ttu-id="4aad3-283">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4aad3-283">String</span></span> |&nbsp;
| <span data-ttu-id="4aad3-284">geheel getal</span><span class="sxs-lookup"><span data-stu-id="4aad3-284">integer</span></span> |<span data-ttu-id="4aad3-285">int, int4</span><span class="sxs-lookup"><span data-stu-id="4aad3-285">int, int4</span></span> |<span data-ttu-id="4aad3-286">Int32</span><span class="sxs-lookup"><span data-stu-id="4aad3-286">Int32</span></span> |
| <span data-ttu-id="4aad3-287">interval [velden] [(p)]</span><span class="sxs-lookup"><span data-stu-id="4aad3-287">interval [ fields ] [ (p) ]</span></span> | |<span data-ttu-id="4aad3-288">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="4aad3-288">Timespan</span></span> |&nbsp;
| <span data-ttu-id="4aad3-289">JSON</span><span class="sxs-lookup"><span data-stu-id="4aad3-289">json</span></span> | |<span data-ttu-id="4aad3-290">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4aad3-290">String</span></span> |&nbsp;
| <span data-ttu-id="4aad3-291">jsonb</span><span class="sxs-lookup"><span data-stu-id="4aad3-291">jsonb</span></span> | |<span data-ttu-id="4aad3-292">Byte]</span><span class="sxs-lookup"><span data-stu-id="4aad3-292">Byte[]</span></span> |&nbsp;
| <span data-ttu-id="4aad3-293">regel</span><span class="sxs-lookup"><span data-stu-id="4aad3-293">line</span></span> | |<span data-ttu-id="4aad3-294">Byte [], String</span><span class="sxs-lookup"><span data-stu-id="4aad3-294">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="4aad3-295">lseg</span><span class="sxs-lookup"><span data-stu-id="4aad3-295">lseg</span></span> | |<span data-ttu-id="4aad3-296">Byte [], String</span><span class="sxs-lookup"><span data-stu-id="4aad3-296">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="4aad3-297">macaddr</span><span class="sxs-lookup"><span data-stu-id="4aad3-297">macaddr</span></span> | |<span data-ttu-id="4aad3-298">Byte [], String</span><span class="sxs-lookup"><span data-stu-id="4aad3-298">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="4aad3-299">Money</span><span class="sxs-lookup"><span data-stu-id="4aad3-299">money</span></span> | |<span data-ttu-id="4aad3-300">Decimale</span><span class="sxs-lookup"><span data-stu-id="4aad3-300">Decimal</span></span> |&nbsp;
| <span data-ttu-id="4aad3-301">numerieke [(p, s)]</span><span class="sxs-lookup"><span data-stu-id="4aad3-301">numeric [ (p, s) ]</span></span> |<span data-ttu-id="4aad3-302">Decimal [(p, s)]</span><span class="sxs-lookup"><span data-stu-id="4aad3-302">decimal [ (p, s) ]</span></span> |<span data-ttu-id="4aad3-303">Decimale</span><span class="sxs-lookup"><span data-stu-id="4aad3-303">Decimal</span></span> |
| <span data-ttu-id="4aad3-304">numrange</span><span class="sxs-lookup"><span data-stu-id="4aad3-304">numrange</span></span> | |<span data-ttu-id="4aad3-305">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4aad3-305">String</span></span> |&nbsp;
| <span data-ttu-id="4aad3-306">OID</span><span class="sxs-lookup"><span data-stu-id="4aad3-306">oid</span></span> | |<span data-ttu-id="4aad3-307">Int32</span><span class="sxs-lookup"><span data-stu-id="4aad3-307">Int32</span></span> |&nbsp;
| <span data-ttu-id="4aad3-308">Pad</span><span class="sxs-lookup"><span data-stu-id="4aad3-308">path</span></span> | |<span data-ttu-id="4aad3-309">Byte [], String</span><span class="sxs-lookup"><span data-stu-id="4aad3-309">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="4aad3-310">pg_lsn</span><span class="sxs-lookup"><span data-stu-id="4aad3-310">pg_lsn</span></span> | |<span data-ttu-id="4aad3-311">Int64</span><span class="sxs-lookup"><span data-stu-id="4aad3-311">Int64</span></span> |&nbsp;
| <span data-ttu-id="4aad3-312">beheerpunt</span><span class="sxs-lookup"><span data-stu-id="4aad3-312">point</span></span> | |<span data-ttu-id="4aad3-313">Byte [], String</span><span class="sxs-lookup"><span data-stu-id="4aad3-313">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="4aad3-314">veelhoek</span><span class="sxs-lookup"><span data-stu-id="4aad3-314">polygon</span></span> | |<span data-ttu-id="4aad3-315">Byte [], String</span><span class="sxs-lookup"><span data-stu-id="4aad3-315">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="4aad3-316">echte</span><span class="sxs-lookup"><span data-stu-id="4aad3-316">real</span></span> |<span data-ttu-id="4aad3-317">FLOAT4</span><span class="sxs-lookup"><span data-stu-id="4aad3-317">float4</span></span> |<span data-ttu-id="4aad3-318">Één</span><span class="sxs-lookup"><span data-stu-id="4aad3-318">Single</span></span> |
| <span data-ttu-id="4aad3-319">smallint</span><span class="sxs-lookup"><span data-stu-id="4aad3-319">smallint</span></span> |<span data-ttu-id="4aad3-320">int2</span><span class="sxs-lookup"><span data-stu-id="4aad3-320">int2</span></span> |<span data-ttu-id="4aad3-321">Int16</span><span class="sxs-lookup"><span data-stu-id="4aad3-321">Int16</span></span> |
| <span data-ttu-id="4aad3-322">smallserial</span><span class="sxs-lookup"><span data-stu-id="4aad3-322">smallserial</span></span> |<span data-ttu-id="4aad3-323">serial2</span><span class="sxs-lookup"><span data-stu-id="4aad3-323">serial2</span></span> |<span data-ttu-id="4aad3-324">Int16</span><span class="sxs-lookup"><span data-stu-id="4aad3-324">Int16</span></span> |
| <span data-ttu-id="4aad3-325">Seriële</span><span class="sxs-lookup"><span data-stu-id="4aad3-325">serial</span></span> |<span data-ttu-id="4aad3-326">serial4</span><span class="sxs-lookup"><span data-stu-id="4aad3-326">serial4</span></span> |<span data-ttu-id="4aad3-327">Int32</span><span class="sxs-lookup"><span data-stu-id="4aad3-327">Int32</span></span> |
| <span data-ttu-id="4aad3-328">Tekst</span><span class="sxs-lookup"><span data-stu-id="4aad3-328">text</span></span> | |<span data-ttu-id="4aad3-329">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="4aad3-329">String</span></span> |&nbsp;

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="4aad3-330">Bron van de kaart opvangen kolommen</span><span class="sxs-lookup"><span data-stu-id="4aad3-330">Map source to sink columns</span></span>
<span data-ttu-id="4aad3-331">Zie voor meer informatie over het toewijzen van kolommen in gegevensset naar kolommen in gegevensset sink bron, [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="4aad3-331">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="4aad3-332">Herhaalbare leesbewerking van relationele bronnen</span><span class="sxs-lookup"><span data-stu-id="4aad3-332">Repeatable read from relational sources</span></span>
<span data-ttu-id="4aad3-333">Bij het kopiëren van gegevens van relationele gegevens worden opgeslagen, moet u herhaalbaarheid Houd in gedachten om te voorkomen dat ongewenste resultaten.</span><span class="sxs-lookup"><span data-stu-id="4aad3-333">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="4aad3-334">In Azure Data Factory, kunt u een segment handmatig opnieuw.</span><span class="sxs-lookup"><span data-stu-id="4aad3-334">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="4aad3-335">U kunt ook een beleid voor opnieuw proberen voor een gegevensset configureren zodat een segment wordt opnieuw uitgevoerd wanneer een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="4aad3-335">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="4aad3-336">Wanneer een segment opnieuw in beide gevallen wordt uitgevoerd, moet u ervoor zorgen dat dezelfde gegevens is gelezen ongeacht hoe vaak een segment wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4aad3-336">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="4aad3-337">Zie [Repeatable van relationele bronnen lezen](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="4aad3-337">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="4aad3-338">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="4aad3-338">Performance and Tuning</span></span>
<span data-ttu-id="4aad3-339">Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) voor meer informatie over de belangrijkste factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren om te optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="4aad3-339">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
