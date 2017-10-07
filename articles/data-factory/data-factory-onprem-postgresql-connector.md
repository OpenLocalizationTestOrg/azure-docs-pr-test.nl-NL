---
title: aaaMove gegevens van PostgreSQL met behulp van Azure Data Factory | Microsoft Docs
description: Meer informatie over het toomove gegevens uit een PostgreSQL-Database met behulp van Azure Data Factory.
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
ms.openlocfilehash: ea384f4e06f7d7bedae2949e4ea727c8f8806614
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-postgresql-using-azure-data-factory"></a><span data-ttu-id="39e7d-103">Verplaatsen van gegevens uit een PostgreSQL met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="39e7d-103">Move data from PostgreSQL using Azure Data Factory</span></span>
<span data-ttu-id="39e7d-104">Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit Hallo in Azure Data Factory toomove gegevens uit een on-premises PostgreSQL-database.</span><span class="sxs-lookup"><span data-stu-id="39e7d-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises PostgreSQL database.</span></span> <span data-ttu-id="39e7d-105">Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.</span><span class="sxs-lookup"><span data-stu-id="39e7d-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="39e7d-106">U kunt gegevens uit een on-premises PostgreSQL gegevens store tooany ondersteund sink gegevensopslag kopiëren.</span><span class="sxs-lookup"><span data-stu-id="39e7d-106">You can copy data from an on-premises PostgreSQL data store tooany supported sink data store.</span></span> <span data-ttu-id="39e7d-107">Zie voor een lijst van gegevensarchieven als PUT wordt ondersteund door Hallo kopieeractiviteit [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="39e7d-107">For a list of data stores supported as sinks by hello copy activity, see [supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="39e7d-108">Data factory momenteel ondersteunt het verplaatsen van gegevens uit een PostgreSQL-database tooother gegevensarchieven, maar niet voor tooan PostgreSQL-database verplaatsen van gegevens van andere gegevens worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="39e7d-108">Data factory currently supports moving data from a PostgreSQL database tooother data stores, but not for moving data from other data stores tooan PostgreSQL database.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="39e7d-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="39e7d-109">prerequisites</span></span>

<span data-ttu-id="39e7d-110">Data Factory-service ondersteunt verbindende tooon lokale PostgreSQL gegevensbronnen waarvoor gebruik Hallo Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="39e7d-110">Data Factory service supports connecting tooon-premises PostgreSQL sources using hello Data Management Gateway.</span></span> <span data-ttu-id="39e7d-111">Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn artikel over Data Management Gateway en stapsgewijze instructies over het instellen van Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="39e7d-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="39e7d-112">Gateway is vereist, zelfs als Hallo PostgreSQL-database wordt gehost in een Azure IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="39e7d-112">Gateway is required even if hello PostgreSQL database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="39e7d-113">U kunt de gateway installeren op Hallo dezelfde IaaS VM als Hallo gegevens opslaan of op een andere virtuele machine zo lang Hallo gateway kunt verbinding maken met toohello-database.</span><span class="sxs-lookup"><span data-stu-id="39e7d-113">You can install gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="39e7d-114">Zie [gateway problemen](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) voor tips over het oplossen van verbinding of gateway gerelateerde problemen.</span><span class="sxs-lookup"><span data-stu-id="39e7d-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="39e7d-115">Ondersteunde versies en installatie</span><span class="sxs-lookup"><span data-stu-id="39e7d-115">Supported versions and installation</span></span>
<span data-ttu-id="39e7d-116">Voor Data Management Gateway tooconnect toohello PostgreSQL-Database, installeert u Hallo [Ngpsql-gegevensprovider voor PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 of boven op Hallo hetzelfde systeem als Data Management Gateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="39e7d-116">For Data Management Gateway tooconnect toohello PostgreSQL Database, install hello [Ngpsql data provider for PostgreSQL](http://go.microsoft.com/fwlink/?linkid=282716) 2.0.12 or above on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="39e7d-117">PostgreSQL versie 7.4 en hoger wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="39e7d-117">PostgreSQL version 7.4 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="39e7d-118">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="39e7d-118">Getting started</span></span>
<span data-ttu-id="39e7d-119">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens vanuit een on-premises PostgreSQL-gegevensopslag verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="39e7d-119">You can create a pipeline with a copy activity that moves data from an on-premises PostgreSQL data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="39e7d-120">Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="39e7d-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="39e7d-121">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="39e7d-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="39e7d-122">U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen:</span><span class="sxs-lookup"><span data-stu-id="39e7d-122">You can also use hello following tools toocreate a pipeline:</span></span> 
    - <span data-ttu-id="39e7d-123">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="39e7d-123">Azure portal</span></span>
    - <span data-ttu-id="39e7d-124">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="39e7d-124">Visual Studio</span></span>
    - <span data-ttu-id="39e7d-125">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="39e7d-125">Azure PowerShell</span></span>
    - <span data-ttu-id="39e7d-126">Azure Resource Manager-sjabloon</span><span class="sxs-lookup"><span data-stu-id="39e7d-126">Azure Resource Manager template</span></span>
    - <span data-ttu-id="39e7d-127">.NET API</span><span class="sxs-lookup"><span data-stu-id="39e7d-127">.NET API</span></span>
    - <span data-ttu-id="39e7d-128">REST API</span><span class="sxs-lookup"><span data-stu-id="39e7d-128">REST API</span></span>

     <span data-ttu-id="39e7d-129">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="39e7d-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="39e7d-130">Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="39e7d-130">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="39e7d-131">Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="39e7d-131">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="39e7d-132">Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="39e7d-132">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="39e7d-133">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="39e7d-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="39e7d-134">Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="39e7d-134">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="39e7d-135">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="39e7d-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="39e7d-136">Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens uit een on-premises PostgreSQL-gegevensopslag zijn [JSON-voorbeeld: gegevens kopiëren van PostgreSQL tooAzure Blob](#json-example-copy-data-from-postgresql-to-azure-blob) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="39e7d-136">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises PostgreSQL data store, see [JSON example: Copy data from PostgreSQL tooAzure Blob](#json-example-copy-data-from-postgresql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="39e7d-137">Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooa PostgreSQL-gegevensarchief zijn:</span><span class="sxs-lookup"><span data-stu-id="39e7d-137">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa PostgreSQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="39e7d-138">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="39e7d-138">Linked service properties</span></span>
<span data-ttu-id="39e7d-139">Hallo volgende tabel biedt een beschrijving voor de JSON-elementen specifieke tooPostgreSQL gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="39e7d-139">hello following table provides description for JSON elements specific tooPostgreSQL linked service.</span></span>

| <span data-ttu-id="39e7d-140">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="39e7d-140">Property</span></span> | <span data-ttu-id="39e7d-141">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="39e7d-141">Description</span></span> | <span data-ttu-id="39e7d-142">Vereist</span><span class="sxs-lookup"><span data-stu-id="39e7d-142">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="39e7d-143">type</span><span class="sxs-lookup"><span data-stu-id="39e7d-143">type</span></span> |<span data-ttu-id="39e7d-144">Hallo type eigenschap moet worden ingesteld op: **OnPremisesPostgreSql**</span><span class="sxs-lookup"><span data-stu-id="39e7d-144">hello type property must be set to: **OnPremisesPostgreSql**</span></span> |<span data-ttu-id="39e7d-145">Ja</span><span class="sxs-lookup"><span data-stu-id="39e7d-145">Yes</span></span> |
| <span data-ttu-id="39e7d-146">server</span><span class="sxs-lookup"><span data-stu-id="39e7d-146">server</span></span> |<span data-ttu-id="39e7d-147">Naam van Hallo PostgreSQL-server.</span><span class="sxs-lookup"><span data-stu-id="39e7d-147">Name of hello PostgreSQL server.</span></span> |<span data-ttu-id="39e7d-148">Ja</span><span class="sxs-lookup"><span data-stu-id="39e7d-148">Yes</span></span> |
| <span data-ttu-id="39e7d-149">database</span><span class="sxs-lookup"><span data-stu-id="39e7d-149">database</span></span> |<span data-ttu-id="39e7d-150">Naam van Hallo PostgreSQL-database.</span><span class="sxs-lookup"><span data-stu-id="39e7d-150">Name of hello PostgreSQL database.</span></span> |<span data-ttu-id="39e7d-151">Ja</span><span class="sxs-lookup"><span data-stu-id="39e7d-151">Yes</span></span> |
| <span data-ttu-id="39e7d-152">Schema</span><span class="sxs-lookup"><span data-stu-id="39e7d-152">schema</span></span> |<span data-ttu-id="39e7d-153">Naam van Hallo schema in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="39e7d-153">Name of hello schema in hello database.</span></span> <span data-ttu-id="39e7d-154">Hallo-schemanaam is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="39e7d-154">hello schema name is case-sensitive.</span></span> |<span data-ttu-id="39e7d-155">Nee</span><span class="sxs-lookup"><span data-stu-id="39e7d-155">No</span></span> |
| <span data-ttu-id="39e7d-156">authenticationType</span><span class="sxs-lookup"><span data-stu-id="39e7d-156">authenticationType</span></span> |<span data-ttu-id="39e7d-157">Type verificatie gebruikt tooconnect toohello PostgreSQL-database.</span><span class="sxs-lookup"><span data-stu-id="39e7d-157">Type of authentication used tooconnect toohello PostgreSQL database.</span></span> <span data-ttu-id="39e7d-158">Mogelijke waarden zijn: anoniem, basis en Windows.</span><span class="sxs-lookup"><span data-stu-id="39e7d-158">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="39e7d-159">Ja</span><span class="sxs-lookup"><span data-stu-id="39e7d-159">Yes</span></span> |
| <span data-ttu-id="39e7d-160">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="39e7d-160">username</span></span> |<span data-ttu-id="39e7d-161">Geef de gebruikersnaam als u basisverificatie of Windows-verificatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="39e7d-161">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="39e7d-162">Nee</span><span class="sxs-lookup"><span data-stu-id="39e7d-162">No</span></span> |
| <span data-ttu-id="39e7d-163">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="39e7d-163">password</span></span> |<span data-ttu-id="39e7d-164">Wachtwoord voor gebruikersaccount Hallo die u hebt opgegeven voor Hallo gebruikersnaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="39e7d-164">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="39e7d-165">Nee</span><span class="sxs-lookup"><span data-stu-id="39e7d-165">No</span></span> |
| <span data-ttu-id="39e7d-166">gatewayName</span><span class="sxs-lookup"><span data-stu-id="39e7d-166">gatewayName</span></span> |<span data-ttu-id="39e7d-167">Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello lokale PostgreSQL-database gebruiken.</span><span class="sxs-lookup"><span data-stu-id="39e7d-167">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises PostgreSQL database.</span></span> |<span data-ttu-id="39e7d-168">Ja</span><span class="sxs-lookup"><span data-stu-id="39e7d-168">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="39e7d-169">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="39e7d-169">Dataset properties</span></span>
<span data-ttu-id="39e7d-170">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="39e7d-170">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="39e7d-171">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle typen van de gegevensset.</span><span class="sxs-lookup"><span data-stu-id="39e7d-171">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types.</span></span>

<span data-ttu-id="39e7d-172">Hallo typeProperties sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="39e7d-172">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="39e7d-173">Hallo typeProperties sectie voor de gegevensset van het type **RelationalTable** (inclusief PostgreSQL gegevensset) heeft Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="39e7d-173">hello typeProperties section for dataset of type **RelationalTable** (which includes PostgreSQL dataset) has hello following properties:</span></span>

| <span data-ttu-id="39e7d-174">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="39e7d-174">Property</span></span> | <span data-ttu-id="39e7d-175">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="39e7d-175">Description</span></span> | <span data-ttu-id="39e7d-176">Vereist</span><span class="sxs-lookup"><span data-stu-id="39e7d-176">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="39e7d-177">tableName</span><span class="sxs-lookup"><span data-stu-id="39e7d-177">tableName</span></span> |<span data-ttu-id="39e7d-178">De naam van de tabel Hallo in Hallo PostgreSQL-Database-instantie waarnaar de gekoppelde service verwijst.</span><span class="sxs-lookup"><span data-stu-id="39e7d-178">Name of hello table in hello PostgreSQL Database instance that linked service refers to.</span></span> <span data-ttu-id="39e7d-179">Hallo tableName is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="39e7d-179">hello tableName is case-sensitive.</span></span> |<span data-ttu-id="39e7d-180">Nee (als **query** van **RelationalSource** is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="39e7d-180">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="39e7d-181">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="39e7d-181">Copy activity properties</span></span>
<span data-ttu-id="39e7d-182">Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="39e7d-182">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="39e7d-183">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en -beleid zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="39e7d-183">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="39e7d-184">Terwijl de eigenschappen die beschikbaar zijn in Hallo typeProperties gedeelte van de activiteit Hallo variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="39e7d-184">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="39e7d-185">Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="39e7d-185">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="39e7d-186">Wanneer de bron is van het type **RelationalSource** (waaronder PostgreSQL), Hallo volgende eigenschappen beschikbaar zijn in de sectie typeProperties:</span><span class="sxs-lookup"><span data-stu-id="39e7d-186">When source is of type **RelationalSource** (which includes PostgreSQL), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="39e7d-187">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="39e7d-187">Property</span></span> | <span data-ttu-id="39e7d-188">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="39e7d-188">Description</span></span> | <span data-ttu-id="39e7d-189">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="39e7d-189">Allowed values</span></span> | <span data-ttu-id="39e7d-190">Vereist</span><span class="sxs-lookup"><span data-stu-id="39e7d-190">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="39e7d-191">query</span><span class="sxs-lookup"><span data-stu-id="39e7d-191">query</span></span> |<span data-ttu-id="39e7d-192">Hallo aangepaste query tooread gegevens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="39e7d-192">Use hello custom query tooread data.</span></span> |<span data-ttu-id="39e7d-193">SQL-query-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="39e7d-193">SQL query string.</span></span> <span data-ttu-id="39e7d-194">Bijvoorbeeld: "query": "Selecteer * uit \"MySchema\".\" MyTable\"'.</span><span class="sxs-lookup"><span data-stu-id="39e7d-194">For example: "query": "select * from \"MySchema\".\"MyTable\"".</span></span> |<span data-ttu-id="39e7d-195">Nee (als **tableName** van **gegevensset** is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="39e7d-195">No (if **tableName** of **dataset** is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="39e7d-196">Schema- en tabelnamen zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="39e7d-196">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="39e7d-197">Omsluiten in `""` (dubbele aanhalingstekens) in Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="39e7d-197">Enclose them in `""` (double quotes) in hello query.</span></span>  

<span data-ttu-id="39e7d-198">**Voorbeeld:**</span><span class="sxs-lookup"><span data-stu-id="39e7d-198">**Example:**</span></span>

 `"query": "select * from \"MySchema\".\"MyTable\""`

## <a name="json-example-copy-data-from-postgresql-tooazure-blob"></a><span data-ttu-id="39e7d-199">JSON-voorbeeld: gegevens kopiëren van PostgreSQL tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="39e7d-199">JSON example: Copy data from PostgreSQL tooAzure Blob</span></span>
<span data-ttu-id="39e7d-200">In dit voorbeeld voorbeeld JSON definities bevat dat u een pijplijn toocreate gebruiken met behulp van kunt [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="39e7d-200">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="39e7d-201">Ze geven weer hoe toocopy gegevens uit een PostgreSQL-database tooAzure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="39e7d-201">They show how toocopy data from PostgreSQL database tooAzure Blob Storage.</span></span> <span data-ttu-id="39e7d-202">Gegevens kunnen echter wel gekopieerde tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="39e7d-202">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

> [!IMPORTANT]
> <span data-ttu-id="39e7d-203">Dit voorbeeld bevat JSON-fragmenten.</span><span class="sxs-lookup"><span data-stu-id="39e7d-203">This sample provides JSON snippets.</span></span> <span data-ttu-id="39e7d-204">Dit omvat geen stapsgewijze instructies voor het maken van de gegevensfactory Hallo.</span><span class="sxs-lookup"><span data-stu-id="39e7d-204">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="39e7d-205">Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor stapsgewijze instructies.</span><span class="sxs-lookup"><span data-stu-id="39e7d-205">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="39e7d-206">Hallo voorbeeld heeft Hallo data factory-entiteiten te volgen:</span><span class="sxs-lookup"><span data-stu-id="39e7d-206">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="39e7d-207">Een gekoppelde service van het type [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="39e7d-207">A linked service of type [OnPremisesPostgreSql](data-factory-onprem-postgresql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="39e7d-208">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="39e7d-208">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="39e7d-209">Invoer [gegevensset](data-factory-create-datasets.md) van het type [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="39e7d-209">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-postgresql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="39e7d-210">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="39e7d-210">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="39e7d-211">Hallo [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="39e7d-211">hello [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-postgresql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="39e7d-212">Hallo voorbeeld kopieert gegevens van de resultaten van een query in een PostgreSQL-database tooa blob elk uur.</span><span class="sxs-lookup"><span data-stu-id="39e7d-212">hello sample copies data from a query result in PostgreSQL database tooa blob every hour.</span></span> <span data-ttu-id="39e7d-213">Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="39e7d-213">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="39e7d-214">Instellen als eerste stap Hallo data management gateway.</span><span class="sxs-lookup"><span data-stu-id="39e7d-214">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="39e7d-215">Hallo-instructies vindt u in Hallo [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="39e7d-215">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="39e7d-216">**PostgreSQL gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="39e7d-216">**PostgreSQL linked service:**</span></span>

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
<span data-ttu-id="39e7d-217">**Azure Blob-opslag gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="39e7d-217">**Azure Blob storage linked service:**</span></span>

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
<span data-ttu-id="39e7d-218">**PostgreSQL invoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="39e7d-218">**PostgreSQL input dataset:**</span></span>

<span data-ttu-id="39e7d-219">Hallo-voorbeeld wordt ervan uitgegaan dat u hebt een tabel 'MijnTabel' gemaakt in PostgreSQL en bevat een kolom met de naam 'tijdstempel' voor de reeksgegevens.</span><span class="sxs-lookup"><span data-stu-id="39e7d-219">hello sample assumes you have created a table “MyTable” in PostgreSQL and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="39e7d-220">Instelling `"external": true` informeert Hallo Data Factory-service die gegevensset Hallo externe toohello data factory is en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="39e7d-220">Setting `"external": true` informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="39e7d-221">**Azure Blob-uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="39e7d-221">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="39e7d-222">Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="39e7d-222">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="39e7d-223">Hallo map pad en de naam voor de blob Hallo worden dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="39e7d-223">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="39e7d-224">Hallo mappad jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="39e7d-224">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="39e7d-225">**Pijplijn met de kopieeractiviteit:**</span><span class="sxs-lookup"><span data-stu-id="39e7d-225">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="39e7d-226">Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun per uur is.</span><span class="sxs-lookup"><span data-stu-id="39e7d-226">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="39e7d-227">Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**RelationalSource** en **sink** type is ingesteld, te**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="39e7d-227">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="39e7d-228">Hallo SQL-query is opgegeven voor Hallo **query** eigenschap selecteert Hallo gegevens uit Hallo public.usstates tabel in Hallo PostgreSQL-database.</span><span class="sxs-lookup"><span data-stu-id="39e7d-228">hello SQL query specified for hello **query** property selects hello data from hello public.usstates table in hello PostgreSQL database.</span></span>

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
## <a name="type-mapping-for-postgresql"></a><span data-ttu-id="39e7d-229">Toewijzing van het type voor PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="39e7d-229">Type mapping for PostgreSQL</span></span>
<span data-ttu-id="39e7d-230">Zoals vermeld in Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel kopieeractiviteit voert automatische typeconversies van brontypen typen toosink Hello 2 stap benadering te volgen:</span><span class="sxs-lookup"><span data-stu-id="39e7d-230">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="39e7d-231">Systeemeigen bron typen too.NET type converteren</span><span class="sxs-lookup"><span data-stu-id="39e7d-231">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="39e7d-232">Converteren van .NET-type toonative sink-type</span><span class="sxs-lookup"><span data-stu-id="39e7d-232">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="39e7d-233">Bij het verplaatsen van gegevens tooPostgreSQL worden hello volgende toewijzingen gebruikt vanuit PostgreSQL type too.NET type.</span><span class="sxs-lookup"><span data-stu-id="39e7d-233">When moving data tooPostgreSQL, hello following mappings are used from PostgreSQL type too.NET type.</span></span>

| <span data-ttu-id="39e7d-234">Type PostgreSQL-Database</span><span class="sxs-lookup"><span data-stu-id="39e7d-234">PostgreSQL Database type</span></span> | <span data-ttu-id="39e7d-235">PostgresSQL aliassen</span><span class="sxs-lookup"><span data-stu-id="39e7d-235">PostgresSQL aliases</span></span> | <span data-ttu-id="39e7d-236">.NET framework-type</span><span class="sxs-lookup"><span data-stu-id="39e7d-236">.NET Framework type</span></span> |
| --- | --- | --- |
| <span data-ttu-id="39e7d-237">abstime</span><span class="sxs-lookup"><span data-stu-id="39e7d-237">abstime</span></span> | |<span data-ttu-id="39e7d-238">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="39e7d-238">Datetime</span></span> | &nbsp;
| <span data-ttu-id="39e7d-239">bigint</span><span class="sxs-lookup"><span data-stu-id="39e7d-239">bigint</span></span> |<span data-ttu-id="39e7d-240">int8</span><span class="sxs-lookup"><span data-stu-id="39e7d-240">int8</span></span> |<span data-ttu-id="39e7d-241">Int64</span><span class="sxs-lookup"><span data-stu-id="39e7d-241">Int64</span></span> |
| <span data-ttu-id="39e7d-242">bigserial</span><span class="sxs-lookup"><span data-stu-id="39e7d-242">bigserial</span></span> |<span data-ttu-id="39e7d-243">serial8</span><span class="sxs-lookup"><span data-stu-id="39e7d-243">serial8</span></span> |<span data-ttu-id="39e7d-244">Int64</span><span class="sxs-lookup"><span data-stu-id="39e7d-244">Int64</span></span> |
| <span data-ttu-id="39e7d-245">bits [(n)]</span><span class="sxs-lookup"><span data-stu-id="39e7d-245">bit [ (n) ]</span></span> | |<span data-ttu-id="39e7d-246">Byte [], String</span><span class="sxs-lookup"><span data-stu-id="39e7d-246">Byte[], String</span></span> | &nbsp;
| <span data-ttu-id="39e7d-247">bit uiteenlopende [(n)]</span><span class="sxs-lookup"><span data-stu-id="39e7d-247">bit varying [ (n) ]</span></span> |<span data-ttu-id="39e7d-248">varbit</span><span class="sxs-lookup"><span data-stu-id="39e7d-248">varbit</span></span> |<span data-ttu-id="39e7d-249">Byte [], String</span><span class="sxs-lookup"><span data-stu-id="39e7d-249">Byte[], String</span></span> |
| <span data-ttu-id="39e7d-250">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="39e7d-250">boolean</span></span> |<span data-ttu-id="39e7d-251">BOOL</span><span class="sxs-lookup"><span data-stu-id="39e7d-251">bool</span></span> |<span data-ttu-id="39e7d-252">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="39e7d-252">Boolean</span></span> |
| <span data-ttu-id="39e7d-253">Vak</span><span class="sxs-lookup"><span data-stu-id="39e7d-253">box</span></span> | |<span data-ttu-id="39e7d-254">Byte [], String</span><span class="sxs-lookup"><span data-stu-id="39e7d-254">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="39e7d-255">bytea</span><span class="sxs-lookup"><span data-stu-id="39e7d-255">bytea</span></span> | |<span data-ttu-id="39e7d-256">Byte [], String</span><span class="sxs-lookup"><span data-stu-id="39e7d-256">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="39e7d-257">teken [(n)]</span><span class="sxs-lookup"><span data-stu-id="39e7d-257">character [ (n) ]</span></span> |<span data-ttu-id="39e7d-258">char [(n)]</span><span class="sxs-lookup"><span data-stu-id="39e7d-258">char [ (n) ]</span></span> |<span data-ttu-id="39e7d-259">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="39e7d-259">String</span></span> |
| <span data-ttu-id="39e7d-260">teken wisselende [(n)]</span><span class="sxs-lookup"><span data-stu-id="39e7d-260">character varying [ (n) ]</span></span> |<span data-ttu-id="39e7d-261">varchar [(n)]</span><span class="sxs-lookup"><span data-stu-id="39e7d-261">varchar [ (n) ]</span></span> |<span data-ttu-id="39e7d-262">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="39e7d-262">String</span></span> |
| <span data-ttu-id="39e7d-263">CID</span><span class="sxs-lookup"><span data-stu-id="39e7d-263">cid</span></span> | |<span data-ttu-id="39e7d-264">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="39e7d-264">String</span></span> |&nbsp;
| <span data-ttu-id="39e7d-265">CIDR</span><span class="sxs-lookup"><span data-stu-id="39e7d-265">cidr</span></span> | |<span data-ttu-id="39e7d-266">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="39e7d-266">String</span></span> |&nbsp;
| <span data-ttu-id="39e7d-267">cirkel</span><span class="sxs-lookup"><span data-stu-id="39e7d-267">circle</span></span> | |<span data-ttu-id="39e7d-268">Byte [], String</span><span class="sxs-lookup"><span data-stu-id="39e7d-268">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="39e7d-269">Datum</span><span class="sxs-lookup"><span data-stu-id="39e7d-269">date</span></span> | |<span data-ttu-id="39e7d-270">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="39e7d-270">Datetime</span></span> |&nbsp;
| <span data-ttu-id="39e7d-271">DateRange</span><span class="sxs-lookup"><span data-stu-id="39e7d-271">daterange</span></span> | |<span data-ttu-id="39e7d-272">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="39e7d-272">String</span></span> |&nbsp;
| <span data-ttu-id="39e7d-273">dubbele precisie</span><span class="sxs-lookup"><span data-stu-id="39e7d-273">double precision</span></span> |<span data-ttu-id="39e7d-274">FLOAT8</span><span class="sxs-lookup"><span data-stu-id="39e7d-274">float8</span></span> |<span data-ttu-id="39e7d-275">dubbele</span><span class="sxs-lookup"><span data-stu-id="39e7d-275">Double</span></span> |
| <span data-ttu-id="39e7d-276">INet</span><span class="sxs-lookup"><span data-stu-id="39e7d-276">inet</span></span> | |<span data-ttu-id="39e7d-277">Byte [], String</span><span class="sxs-lookup"><span data-stu-id="39e7d-277">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="39e7d-278">intarry</span><span class="sxs-lookup"><span data-stu-id="39e7d-278">intarry</span></span> | |<span data-ttu-id="39e7d-279">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="39e7d-279">String</span></span> |&nbsp;
| <span data-ttu-id="39e7d-280">int4range</span><span class="sxs-lookup"><span data-stu-id="39e7d-280">int4range</span></span> | |<span data-ttu-id="39e7d-281">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="39e7d-281">String</span></span> |&nbsp;
| <span data-ttu-id="39e7d-282">int8range</span><span class="sxs-lookup"><span data-stu-id="39e7d-282">int8range</span></span> | |<span data-ttu-id="39e7d-283">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="39e7d-283">String</span></span> |&nbsp;
| <span data-ttu-id="39e7d-284">geheel getal</span><span class="sxs-lookup"><span data-stu-id="39e7d-284">integer</span></span> |<span data-ttu-id="39e7d-285">int, int4</span><span class="sxs-lookup"><span data-stu-id="39e7d-285">int, int4</span></span> |<span data-ttu-id="39e7d-286">Int32</span><span class="sxs-lookup"><span data-stu-id="39e7d-286">Int32</span></span> |
| <span data-ttu-id="39e7d-287">interval [velden] [(p)]</span><span class="sxs-lookup"><span data-stu-id="39e7d-287">interval [ fields ] [ (p) ]</span></span> | |<span data-ttu-id="39e7d-288">Periode</span><span class="sxs-lookup"><span data-stu-id="39e7d-288">Timespan</span></span> |&nbsp;
| <span data-ttu-id="39e7d-289">JSON</span><span class="sxs-lookup"><span data-stu-id="39e7d-289">json</span></span> | |<span data-ttu-id="39e7d-290">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="39e7d-290">String</span></span> |&nbsp;
| <span data-ttu-id="39e7d-291">jsonb</span><span class="sxs-lookup"><span data-stu-id="39e7d-291">jsonb</span></span> | |<span data-ttu-id="39e7d-292">Byte]</span><span class="sxs-lookup"><span data-stu-id="39e7d-292">Byte[]</span></span> |&nbsp;
| <span data-ttu-id="39e7d-293">regel</span><span class="sxs-lookup"><span data-stu-id="39e7d-293">line</span></span> | |<span data-ttu-id="39e7d-294">Byte [], String</span><span class="sxs-lookup"><span data-stu-id="39e7d-294">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="39e7d-295">lseg</span><span class="sxs-lookup"><span data-stu-id="39e7d-295">lseg</span></span> | |<span data-ttu-id="39e7d-296">Byte [], String</span><span class="sxs-lookup"><span data-stu-id="39e7d-296">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="39e7d-297">macaddr</span><span class="sxs-lookup"><span data-stu-id="39e7d-297">macaddr</span></span> | |<span data-ttu-id="39e7d-298">Byte [], String</span><span class="sxs-lookup"><span data-stu-id="39e7d-298">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="39e7d-299">Money</span><span class="sxs-lookup"><span data-stu-id="39e7d-299">money</span></span> | |<span data-ttu-id="39e7d-300">Decimale</span><span class="sxs-lookup"><span data-stu-id="39e7d-300">Decimal</span></span> |&nbsp;
| <span data-ttu-id="39e7d-301">numerieke [(p, s)]</span><span class="sxs-lookup"><span data-stu-id="39e7d-301">numeric [ (p, s) ]</span></span> |<span data-ttu-id="39e7d-302">Decimal [(p, s)]</span><span class="sxs-lookup"><span data-stu-id="39e7d-302">decimal [ (p, s) ]</span></span> |<span data-ttu-id="39e7d-303">Decimale</span><span class="sxs-lookup"><span data-stu-id="39e7d-303">Decimal</span></span> |
| <span data-ttu-id="39e7d-304">numrange</span><span class="sxs-lookup"><span data-stu-id="39e7d-304">numrange</span></span> | |<span data-ttu-id="39e7d-305">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="39e7d-305">String</span></span> |&nbsp;
| <span data-ttu-id="39e7d-306">OID</span><span class="sxs-lookup"><span data-stu-id="39e7d-306">oid</span></span> | |<span data-ttu-id="39e7d-307">Int32</span><span class="sxs-lookup"><span data-stu-id="39e7d-307">Int32</span></span> |&nbsp;
| <span data-ttu-id="39e7d-308">Pad</span><span class="sxs-lookup"><span data-stu-id="39e7d-308">path</span></span> | |<span data-ttu-id="39e7d-309">Byte [], String</span><span class="sxs-lookup"><span data-stu-id="39e7d-309">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="39e7d-310">pg_lsn</span><span class="sxs-lookup"><span data-stu-id="39e7d-310">pg_lsn</span></span> | |<span data-ttu-id="39e7d-311">Int64</span><span class="sxs-lookup"><span data-stu-id="39e7d-311">Int64</span></span> |&nbsp;
| <span data-ttu-id="39e7d-312">beheerpunt</span><span class="sxs-lookup"><span data-stu-id="39e7d-312">point</span></span> | |<span data-ttu-id="39e7d-313">Byte [], String</span><span class="sxs-lookup"><span data-stu-id="39e7d-313">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="39e7d-314">veelhoek</span><span class="sxs-lookup"><span data-stu-id="39e7d-314">polygon</span></span> | |<span data-ttu-id="39e7d-315">Byte [], String</span><span class="sxs-lookup"><span data-stu-id="39e7d-315">Byte[], String</span></span> |&nbsp;
| <span data-ttu-id="39e7d-316">echte</span><span class="sxs-lookup"><span data-stu-id="39e7d-316">real</span></span> |<span data-ttu-id="39e7d-317">FLOAT4</span><span class="sxs-lookup"><span data-stu-id="39e7d-317">float4</span></span> |<span data-ttu-id="39e7d-318">Één</span><span class="sxs-lookup"><span data-stu-id="39e7d-318">Single</span></span> |
| <span data-ttu-id="39e7d-319">smallint</span><span class="sxs-lookup"><span data-stu-id="39e7d-319">smallint</span></span> |<span data-ttu-id="39e7d-320">int2</span><span class="sxs-lookup"><span data-stu-id="39e7d-320">int2</span></span> |<span data-ttu-id="39e7d-321">Int16</span><span class="sxs-lookup"><span data-stu-id="39e7d-321">Int16</span></span> |
| <span data-ttu-id="39e7d-322">smallserial</span><span class="sxs-lookup"><span data-stu-id="39e7d-322">smallserial</span></span> |<span data-ttu-id="39e7d-323">serial2</span><span class="sxs-lookup"><span data-stu-id="39e7d-323">serial2</span></span> |<span data-ttu-id="39e7d-324">Int16</span><span class="sxs-lookup"><span data-stu-id="39e7d-324">Int16</span></span> |
| <span data-ttu-id="39e7d-325">Seriële</span><span class="sxs-lookup"><span data-stu-id="39e7d-325">serial</span></span> |<span data-ttu-id="39e7d-326">serial4</span><span class="sxs-lookup"><span data-stu-id="39e7d-326">serial4</span></span> |<span data-ttu-id="39e7d-327">Int32</span><span class="sxs-lookup"><span data-stu-id="39e7d-327">Int32</span></span> |
| <span data-ttu-id="39e7d-328">Tekst</span><span class="sxs-lookup"><span data-stu-id="39e7d-328">text</span></span> | |<span data-ttu-id="39e7d-329">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="39e7d-329">String</span></span> |&nbsp;

## <a name="map-source-toosink-columns"></a><span data-ttu-id="39e7d-330">Bronkolommen toosink toewijzen</span><span class="sxs-lookup"><span data-stu-id="39e7d-330">Map source toosink columns</span></span>
<span data-ttu-id="39e7d-331">Zie toolearn over het toewijzen van kolommen in bron gegevensset toocolumns in sink-gegevensset [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="39e7d-331">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="39e7d-332">Herhaalbare leesbewerking van relationele bronnen</span><span class="sxs-lookup"><span data-stu-id="39e7d-332">Repeatable read from relational sources</span></span>
<span data-ttu-id="39e7d-333">Houd bij het kopiëren van gegevens uit een relationele gegevensopslag, herhaalbaarheid rekening tooavoid ongewenste resultaten.</span><span class="sxs-lookup"><span data-stu-id="39e7d-333">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="39e7d-334">In Azure Data Factory, kunt u een segment handmatig opnieuw.</span><span class="sxs-lookup"><span data-stu-id="39e7d-334">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="39e7d-335">U kunt ook een beleid voor opnieuw proberen voor een gegevensset configureren zodat een segment wordt opnieuw uitgevoerd wanneer een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="39e7d-335">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="39e7d-336">Wanneer een segment opnieuw in beide gevallen wordt uitgevoerd, moet u ervoor dat dezelfde gegevens Hallo toomake wordt gelezen ongeacht hoe vaak een segment wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="39e7d-336">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="39e7d-337">Zie [Repeatable van relationele bronnen lezen](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="39e7d-337">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="39e7d-338">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="39e7d-338">Performance and Tuning</span></span>
<span data-ttu-id="39e7d-339">Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.</span><span class="sxs-lookup"><span data-stu-id="39e7d-339">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
