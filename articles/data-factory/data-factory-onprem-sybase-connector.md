---
title: Gegevens verplaatsen van Sybase met behulp van Azure Data Factory | Microsoft Docs
description: Meer informatie over het verplaatsen van gegevens uit een Sybase-Database met behulp van Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: b379ee10-0ff5-4974-8c87-c95f82f1c5c6
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: 617e604b220b8bc1c452e67da83f733448e16c0b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-sybase-using-azure-data-factory"></a><span data-ttu-id="ede76-103">Gegevens verplaatsen van Sybase met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="ede76-103">Move data from Sybase using Azure Data Factory</span></span>
<span data-ttu-id="ede76-104">In dit artikel wordt uitgelegd hoe de Kopieeractiviteit in Azure Data Factory om gegevens te verplaatsen van een on-premises Sybase-database gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ede76-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Sybase database.</span></span> <span data-ttu-id="ede76-105">Dit is gebaseerd op de [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, hetgeen een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit toont.</span><span class="sxs-lookup"><span data-stu-id="ede76-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="ede76-106">U kunt gegevens uit een on-premises Sybase-gegevensopslag kopiëren naar een ondersteunde sink-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="ede76-106">You can copy data from an on-premises Sybase data store to any supported sink data store.</span></span> <span data-ttu-id="ede76-107">Zie voor een lijst met gegevensarchieven als PUT wordt ondersteund door de kopieeractiviteit, de [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel.</span><span class="sxs-lookup"><span data-stu-id="ede76-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="ede76-108">Data factory ondersteunt momenteel alleen zwevend gegevens uit een Sybase-gegevensarchief tot andere gegevensarchieven, maar niet voor het verplaatsen van gegevens uit andere gegevensarchieven met een Sybase-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="ede76-108">Data factory currently supports only moving data from a Sybase data store to other data stores, but not for moving data from other data stores to a Sybase data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ede76-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ede76-109">Prerequisites</span></span>
<span data-ttu-id="ede76-110">Verbinding maken met lokale Sybase bronnen met behulp van Data Management Gateway biedt ondersteuning voor Data Factory-service.</span><span class="sxs-lookup"><span data-stu-id="ede76-110">Data Factory service supports connecting to on-premises Sybase sources using the Data Management Gateway.</span></span> <span data-ttu-id="ede76-111">Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor meer informatie over Data Management Gateway en stapsgewijze instructies over het instellen van de gateway.</span><span class="sxs-lookup"><span data-stu-id="ede76-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="ede76-112">Gateway is vereist, zelfs als de Sybase-database wordt gehost in een Azure IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="ede76-112">Gateway is required even if the Sybase database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="ede76-113">U kunt de gateway installeren op de dezelfde IaaS VM als gegevensopslag of op een andere virtuele machine, zolang de gateway verbinding met de database maken kan.</span><span class="sxs-lookup"><span data-stu-id="ede76-113">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="ede76-114">Zie [gateway problemen](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) voor tips over het oplossen van verbinding of gateway gerelateerde problemen.</span><span class="sxs-lookup"><span data-stu-id="ede76-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="ede76-115">Ondersteunde versies en installatie</span><span class="sxs-lookup"><span data-stu-id="ede76-115">Supported versions and installation</span></span>
<span data-ttu-id="ede76-116">Voor de Data Management Gateway verbinding maken met de Sybase-Database, moet u voor het installeren van de [data provider voor Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 of hoger op hetzelfde systeem als Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="ede76-116">For Data Management Gateway to connect to the Sybase Database, you need to install the [data provider for Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 or above on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="ede76-117">Sybase versie 16 en hoger wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="ede76-117">Sybase version 16 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="ede76-118">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="ede76-118">Getting started</span></span>
<span data-ttu-id="ede76-119">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens vanuit een on-premises Cassandra-gegevensopslag verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="ede76-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="ede76-120">De eenvoudigste manier om een pijplijn maken is met de **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="ede76-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="ede76-121">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met de wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="ede76-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="ede76-122">U kunt ook de volgende hulpprogramma's gebruiken voor het maken van een pijplijn: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon**, **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="ede76-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="ede76-123">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies voor een pijplijn maken met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="ede76-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="ede76-124">Of u de hulpprogramma's of API's gebruiken, moet u de volgende stappen voor het maken van een pijplijn die de gegevens vanuit een brongegevensarchief naar een gegevensarchief sink verplaatst uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ede76-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="ede76-125">Maak **gekoppelde services** slaat om invoer- en gegevens te koppelen aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="ede76-125">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="ede76-126">Maak **gegevenssets** vertegenwoordigt de invoer- en -gegevens voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="ede76-126">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="ede76-127">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="ede76-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="ede76-128">Wanneer u de wizard gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ede76-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="ede76-129">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van de JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="ede76-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="ede76-130">Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die worden gebruikt om gegevens te kopiëren uit een on-premises Sybase-gegevensopslag [JSON-voorbeeld: gegevens kopiëren van Sybase naar Azure Blob](#json-example-copy-data-from-sybase-to-azure-blob) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="ede76-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Sybase data store, see [JSON example: Copy data from Sybase to Azure Blob](#json-example-copy-data-from-sybase-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="ede76-131">De volgende secties bevatten informatie over de JSON-eigenschappen die worden gebruikt voor het definiëren van specifieke Data Factory-entiteiten met een Sybase-gegevensarchief:</span><span class="sxs-lookup"><span data-stu-id="ede76-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Sybase data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="ede76-132">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="ede76-132">Linked service properties</span></span>
<span data-ttu-id="ede76-133">De volgende tabel bevat een beschrijving voor JSON-elementen die specifiek zijn voor Sybase gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="ede76-133">The following table provides description for JSON elements specific to Sybase linked service.</span></span>

| <span data-ttu-id="ede76-134">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="ede76-134">Property</span></span> | <span data-ttu-id="ede76-135">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ede76-135">Description</span></span> | <span data-ttu-id="ede76-136">Vereist</span><span class="sxs-lookup"><span data-stu-id="ede76-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ede76-137">type</span><span class="sxs-lookup"><span data-stu-id="ede76-137">type</span></span> |<span data-ttu-id="ede76-138">De eigenschap type moet worden ingesteld op: **OnPremisesSybase**</span><span class="sxs-lookup"><span data-stu-id="ede76-138">The type property must be set to: **OnPremisesSybase**</span></span> |<span data-ttu-id="ede76-139">Ja</span><span class="sxs-lookup"><span data-stu-id="ede76-139">Yes</span></span> |
| <span data-ttu-id="ede76-140">server</span><span class="sxs-lookup"><span data-stu-id="ede76-140">server</span></span> |<span data-ttu-id="ede76-141">De naam van de Sybase-server.</span><span class="sxs-lookup"><span data-stu-id="ede76-141">Name of the Sybase server.</span></span> |<span data-ttu-id="ede76-142">Ja</span><span class="sxs-lookup"><span data-stu-id="ede76-142">Yes</span></span> |
| <span data-ttu-id="ede76-143">database</span><span class="sxs-lookup"><span data-stu-id="ede76-143">database</span></span> |<span data-ttu-id="ede76-144">Naam van de Sybase-database.</span><span class="sxs-lookup"><span data-stu-id="ede76-144">Name of the Sybase database.</span></span> |<span data-ttu-id="ede76-145">Ja</span><span class="sxs-lookup"><span data-stu-id="ede76-145">Yes</span></span> |
| <span data-ttu-id="ede76-146">Schema</span><span class="sxs-lookup"><span data-stu-id="ede76-146">schema</span></span> |<span data-ttu-id="ede76-147">De naam van het schema in de database.</span><span class="sxs-lookup"><span data-stu-id="ede76-147">Name of the schema in the database.</span></span> |<span data-ttu-id="ede76-148">Nee</span><span class="sxs-lookup"><span data-stu-id="ede76-148">No</span></span> |
| <span data-ttu-id="ede76-149">authenticationType</span><span class="sxs-lookup"><span data-stu-id="ede76-149">authenticationType</span></span> |<span data-ttu-id="ede76-150">Het soort verificatie die verbinding maken met de Sybase-database wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ede76-150">Type of authentication used to connect to the Sybase database.</span></span> <span data-ttu-id="ede76-151">Mogelijke waarden zijn: anoniem, basis en Windows.</span><span class="sxs-lookup"><span data-stu-id="ede76-151">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="ede76-152">Ja</span><span class="sxs-lookup"><span data-stu-id="ede76-152">Yes</span></span> |
| <span data-ttu-id="ede76-153">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="ede76-153">username</span></span> |<span data-ttu-id="ede76-154">Geef de gebruikersnaam als u basisverificatie of Windows-verificatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ede76-154">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="ede76-155">Nee</span><span class="sxs-lookup"><span data-stu-id="ede76-155">No</span></span> |
| <span data-ttu-id="ede76-156">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="ede76-156">password</span></span> |<span data-ttu-id="ede76-157">Wachtwoord voor het gebruikersaccount dat u hebt opgegeven voor de gebruikersnaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="ede76-157">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="ede76-158">Nee</span><span class="sxs-lookup"><span data-stu-id="ede76-158">No</span></span> |
| <span data-ttu-id="ede76-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="ede76-159">gatewayName</span></span> |<span data-ttu-id="ede76-160">Naam van de gateway die voor de Data Factory-service gebruiken moet voor verbinding met de lokale Sybase-database.</span><span class="sxs-lookup"><span data-stu-id="ede76-160">Name of the gateway that the Data Factory service should use to connect to the on-premises Sybase database.</span></span> |<span data-ttu-id="ede76-161">Ja</span><span class="sxs-lookup"><span data-stu-id="ede76-161">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="ede76-162">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="ede76-162">Dataset properties</span></span>
<span data-ttu-id="ede76-163">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van de [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="ede76-163">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="ede76-164">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).</span><span class="sxs-lookup"><span data-stu-id="ede76-164">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="ede76-165">De sectie typeProperties verschilt voor elk type gegevensset en bevat informatie over de locatie van de gegevens in het gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="ede76-165">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="ede76-166">De **typeProperties** sectie voor de gegevensset van het type **RelationalTable** (inclusief Sybase gegevensset) heeft de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="ede76-166">The **typeProperties** section for dataset of type **RelationalTable** (which includes Sybase dataset) has the following properties:</span></span>

| <span data-ttu-id="ede76-167">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="ede76-167">Property</span></span> | <span data-ttu-id="ede76-168">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ede76-168">Description</span></span> | <span data-ttu-id="ede76-169">Vereist</span><span class="sxs-lookup"><span data-stu-id="ede76-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ede76-170">tableName</span><span class="sxs-lookup"><span data-stu-id="ede76-170">tableName</span></span> |<span data-ttu-id="ede76-171">De naam van de tabel in de Sybase-Database-instantie waarnaar de gekoppelde service verwijst.</span><span class="sxs-lookup"><span data-stu-id="ede76-171">Name of the table in the Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="ede76-172">Nee (als **query** van **RelationalSource** is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="ede76-172">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="ede76-173">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="ede76-173">Copy activity properties</span></span>
<span data-ttu-id="ede76-174">Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="ede76-174">For a full list of sections & properties available for defining activities, see [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="ede76-175">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en -beleid zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="ede76-175">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="ede76-176">Terwijl de eigenschappen die beschikbaar zijn in de sectie typeProperties van de activiteit variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="ede76-176">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="ede76-177">Voor de kopieeractiviteit variëren ze, afhankelijk van de typen van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="ede76-177">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="ede76-178">Wanneer de bron is van het type **RelationalSource** (waaronder Sybase), de volgende eigenschappen beschikbaar zijn in **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="ede76-178">When the source is of type **RelationalSource** (which includes Sybase), the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="ede76-179">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="ede76-179">Property</span></span> | <span data-ttu-id="ede76-180">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ede76-180">Description</span></span> | <span data-ttu-id="ede76-181">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="ede76-181">Allowed values</span></span> | <span data-ttu-id="ede76-182">Vereist</span><span class="sxs-lookup"><span data-stu-id="ede76-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ede76-183">query</span><span class="sxs-lookup"><span data-stu-id="ede76-183">query</span></span> |<span data-ttu-id="ede76-184">Gebruik de aangepaste query om gegevens te lezen.</span><span class="sxs-lookup"><span data-stu-id="ede76-184">Use the custom query to read data.</span></span> |<span data-ttu-id="ede76-185">SQL-query-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="ede76-185">SQL query string.</span></span> <span data-ttu-id="ede76-186">Bijvoorbeeld: Selecteer * from MijnTabel.</span><span class="sxs-lookup"><span data-stu-id="ede76-186">For example: select * from MyTable.</span></span> |<span data-ttu-id="ede76-187">Nee (als **tableName** van **gegevensset** is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="ede76-187">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-sybase-to-azure-blob"></a><span data-ttu-id="ede76-188">JSON-voorbeeld: gegevens kopiëren van Sybase naar Azure Blob</span><span class="sxs-lookup"><span data-stu-id="ede76-188">JSON example: Copy data from Sybase to Azure Blob</span></span>
<span data-ttu-id="ede76-189">Het volgende voorbeeld bevat definities van de voorbeeld-JSON die u een pijplijn maken kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="ede76-189">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="ede76-190">Ze laten zien hoe gegevens uit een Sybase-database kopiëren naar Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="ede76-190">They show how to copy data from Sybase database to Azure Blob Storage.</span></span> <span data-ttu-id="ede76-191">Gegevens kunnen echter worden gekopieerd naar een van de PUT vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van de Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ede76-191">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="ede76-192">Het voorbeeld heeft de volgende data factory-entiteiten:</span><span class="sxs-lookup"><span data-stu-id="ede76-192">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="ede76-193">Een gekoppelde service van het type [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ede76-193">A linked service of type [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="ede76-194">Een liked service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ede76-194">A liked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="ede76-195">Invoer [gegevensset](data-factory-create-datasets.md) van het type [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ede76-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="ede76-196">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ede76-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="ede76-197">De [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ede76-197">The [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="ede76-198">Het voorbeeld kopieert gegevens van de resultaten van een query in een Sybase-database naar een blob elk uur.</span><span class="sxs-lookup"><span data-stu-id="ede76-198">The sample copies data from a query result in Sybase database to a blob every hour.</span></span> <span data-ttu-id="ede76-199">De JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na de voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="ede76-199">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="ede76-200">Het instellen van de data management gateway als eerste stap.</span><span class="sxs-lookup"><span data-stu-id="ede76-200">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="ede76-201">De instructies vindt u in de [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="ede76-201">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="ede76-202">**Sybase gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="ede76-202">**Sybase linked service:**</span></span>

```JSON
{
    "name": "OnPremSybaseLinkedService",
    "properties": {
        "type": "OnPremisesSybase",
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

<span data-ttu-id="ede76-203">**Azure Blob-opslag gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="ede76-203">**Azure Blob storage linked service:**</span></span>

```JSON
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorageLinkedService",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"
        }
    }
}
```

<span data-ttu-id="ede76-204">**Sybase invoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="ede76-204">**Sybase input dataset:**</span></span>

<span data-ttu-id="ede76-205">Het voorbeeld wordt ervan uitgegaan dat u hebt een tabel 'MijnTabel' gemaakt in Sybase en bevat een kolom met de naam 'tijdstempel' voor de reeksgegevens.</span><span class="sxs-lookup"><span data-stu-id="ede76-205">The sample assumes you have created a table “MyTable” in Sybase and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="ede76-206">Instelling 'extern': true informeert de Data Factory-service dat deze gegevensset extern is aan de gegevensfactory en niet wordt geproduceerd door een activiteit in de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="ede76-206">Setting “external”: true informs the Data Factory service that this dataset is external to the data factory and is not produced by an activity in the data factory.</span></span> <span data-ttu-id="ede76-207">U ziet dat de **type** van de gekoppelde service is ingesteld op: **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="ede76-207">Notice that the **type** of the linked service is set to: **RelationalTable**.</span></span>

```JSON
{
    "name": "SybaseDataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremSybaseLinkedService",
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

<span data-ttu-id="ede76-208">**Azure Blob-uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="ede76-208">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="ede76-209">Gegevens worden geschreven naar een nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="ede76-209">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="ede76-210">Het pad naar de blob wordt dynamisch geëvalueerd op basis van de begintijd van het segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="ede76-210">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="ede76-211">Het mappad maakt gebruik van jaar, maand, dag en uur delen van de begintijd.</span><span class="sxs-lookup"><span data-stu-id="ede76-211">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```JSON
{
    "name": "AzureBlobSybaseDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sybase/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="ede76-212">**Pijplijn met de kopieeractiviteit:**</span><span class="sxs-lookup"><span data-stu-id="ede76-212">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="ede76-213">De pijplijn bevat een Kopieeractiviteit die is geconfigureerd voor gebruik van de invoer- en uitvoergegevenssets en is gepland voor uitvoering per uur.</span><span class="sxs-lookup"><span data-stu-id="ede76-213">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="ede76-214">In de pijplijn-JSON-definitie de **bron** type is ingesteld op **RelationalSource** en **sink** type is ingesteld op **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="ede76-214">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="ede76-215">De SQL-query die is opgegeven voor de **query** eigenschap selecteert u de gegevens van de DBA. De ordertabel in de database.</span><span class="sxs-lookup"><span data-stu-id="ede76-215">The SQL query specified for the **query** property selects the data from the DBA.Orders table in the database.</span></span>

```JSON
{
    "name": "CopySybaseToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from DBA.Orders"
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "SybaseDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobSybaseDataSet"
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
                "name": "SybaseToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-sybase"></a><span data-ttu-id="ede76-216">Toewijzing van het type voor Sybase</span><span class="sxs-lookup"><span data-stu-id="ede76-216">Type mapping for Sybase</span></span>
<span data-ttu-id="ede76-217">Zoals vermeld in de [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel de kopieerbewerking wordt automatische typeconversies van brontypen opvangen typen met de volgende stappen 2-benadering uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="ede76-217">As mentioned in the [Data Movement Activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="ede76-218">Systeemeigen brontypen converteren naar .NET-type</span><span class="sxs-lookup"><span data-stu-id="ede76-218">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="ede76-219">Converteren van .NET-type naar systeemeigen sink-type</span><span class="sxs-lookup"><span data-stu-id="ede76-219">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="ede76-220">Sybase ondersteunt T-SQL en T-SQL-typen.</span><span class="sxs-lookup"><span data-stu-id="ede76-220">Sybase supports T-SQL and T-SQL types.</span></span> <span data-ttu-id="ede76-221">Zie voor een toewijzingstabel van de sql-typen voor .NET-type [Azure SQL-Connector](data-factory-azure-sql-connector.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="ede76-221">For a mapping table from sql types to .NET type, see [Azure SQL Connector](data-factory-azure-sql-connector.md) article.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="ede76-222">Bron van de kaart opvangen kolommen</span><span class="sxs-lookup"><span data-stu-id="ede76-222">Map source to sink columns</span></span>
<span data-ttu-id="ede76-223">Zie voor meer informatie over het toewijzen van kolommen in gegevensset naar kolommen in gegevensset sink bron, [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="ede76-223">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="ede76-224">Herhaalbare leesbewerking van relationele bronnen</span><span class="sxs-lookup"><span data-stu-id="ede76-224">Repeatable read from relational sources</span></span>
<span data-ttu-id="ede76-225">Bij het kopiëren van gegevens van relationele gegevens worden opgeslagen, moet u herhaalbaarheid Houd in gedachten om te voorkomen dat ongewenste resultaten.</span><span class="sxs-lookup"><span data-stu-id="ede76-225">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="ede76-226">In Azure Data Factory, kunt u een segment handmatig opnieuw.</span><span class="sxs-lookup"><span data-stu-id="ede76-226">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="ede76-227">U kunt ook een beleid voor opnieuw proberen voor een gegevensset configureren zodat een segment wordt opnieuw uitgevoerd wanneer een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="ede76-227">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="ede76-228">Wanneer een segment opnieuw in beide gevallen wordt uitgevoerd, moet u ervoor zorgen dat dezelfde gegevens is gelezen ongeacht hoe vaak een segment wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ede76-228">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="ede76-229">Zie [Repeatable van relationele bronnen lezen](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="ede76-229">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="ede76-230">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="ede76-230">Performance and Tuning</span></span>
<span data-ttu-id="ede76-231">Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) voor meer informatie over de belangrijkste factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren om te optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="ede76-231">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
