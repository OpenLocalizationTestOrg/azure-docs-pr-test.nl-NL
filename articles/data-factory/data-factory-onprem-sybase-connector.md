---
title: aaaMove gegevens van Sybase met behulp van Azure Data Factory | Microsoft Docs
description: Meer informatie over het toomove gegevens van Sybase-Database met behulp van Azure Data Factory.
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
ms.openlocfilehash: ad003ec502028d56db9570fe08af329eb5b71817
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sybase-using-azure-data-factory"></a><span data-ttu-id="0ff6d-103">Gegevens verplaatsen van Sybase met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="0ff6d-103">Move data from Sybase using Azure Data Factory</span></span>
<span data-ttu-id="0ff6d-104">Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit Hallo in Azure Data Factory toomove gegevens uit een on-premises Sybase-database.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises Sybase database.</span></span> <span data-ttu-id="0ff6d-105">Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="0ff6d-106">U kunt gegevens uit een on-premises Sybase gegevens store tooany ondersteund sink gegevensopslag kopiëren.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-106">You can copy data from an on-premises Sybase data store tooany supported sink data store.</span></span> <span data-ttu-id="0ff6d-107">Zie voor een lijst van gegevens winkels ondersteund zoals sinks door kopieeractiviteit hello, Hallo [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="0ff6d-108">Data factory ondersteunt momenteel alleen gegevens uit een Sybase-gegevens opslaan tooother gegevensarchieven verplaatsen, maar niet voor het verplaatsen van gegevens uit andere gegevens winkels tooa Sybase-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-108">Data factory currently supports only moving data from a Sybase data store tooother data stores, but not for moving data from other data stores tooa Sybase data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0ff6d-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0ff6d-109">Prerequisites</span></span>
<span data-ttu-id="0ff6d-110">Data Factory-service ondersteunt verbindende tooon lokale Sybase gegevensbronnen waarvoor gebruik Hallo Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-110">Data Factory service supports connecting tooon-premises Sybase sources using hello Data Management Gateway.</span></span> <span data-ttu-id="0ff6d-111">Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn artikel over Data Management Gateway en stapsgewijze instructies over het instellen van Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="0ff6d-112">Gateway is vereist, zelfs als Hallo Sybase-database wordt gehost in een Azure IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-112">Gateway is required even if hello Sybase database is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="0ff6d-113">U kunt Hallo gateway installeren op Hallo dezelfde IaaS VM als Hallo gegevens opslaan of op een andere virtuele machine zo lang Hallo gateway kunt verbinding maken met toohello-database.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-113">You can install hello gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="0ff6d-114">Zie [gateway problemen](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) voor tips over het oplossen van verbinding of gateway gerelateerde problemen.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="0ff6d-115">Ondersteunde versies en installatie</span><span class="sxs-lookup"><span data-stu-id="0ff6d-115">Supported versions and installation</span></span>
<span data-ttu-id="0ff6d-116">Data Management Gateway tooconnect toohello Sybase-Database, moet u tooinstall hello [data provider voor Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 of boven op Hallo hetzelfde systeem als Data Management Gateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-116">For Data Management Gateway tooconnect toohello Sybase Database, you need tooinstall hello [data provider for Sybase iAnywhere.Data.SQLAnywhere](http://go.microsoft.com/fwlink/?linkid=324846) 16 or above on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="0ff6d-117">Sybase versie 16 en hoger wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-117">Sybase version 16 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="0ff6d-118">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="0ff6d-118">Getting started</span></span>
<span data-ttu-id="0ff6d-119">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens vanuit een on-premises Cassandra-gegevensopslag verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="0ff6d-120">Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="0ff6d-121">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="0ff6d-122">U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="0ff6d-123">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="0ff6d-124">Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="0ff6d-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="0ff6d-125">Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="0ff6d-126">Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-126">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="0ff6d-127">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="0ff6d-128">Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-128">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="0ff6d-129">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="0ff6d-130">Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens uit een on-premises Sybase-gegevensopslag zijn [JSON-voorbeeld: gegevens kopiëren van Sybase tooAzure Blob](#json-example-copy-data-from-sybase-to-azure-blob) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-130">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises Sybase data store, see [JSON example: Copy data from Sybase tooAzure Blob](#json-example-copy-data-from-sybase-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="0ff6d-131">Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooa Sybase-gegevensarchief zijn:</span><span class="sxs-lookup"><span data-stu-id="0ff6d-131">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Sybase data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="0ff6d-132">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="0ff6d-132">Linked service properties</span></span>
<span data-ttu-id="0ff6d-133">Hallo volgende tabel biedt een beschrijving voor de JSON-elementen specifieke tooSybase gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-133">hello following table provides description for JSON elements specific tooSybase linked service.</span></span>

| <span data-ttu-id="0ff6d-134">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="0ff6d-134">Property</span></span> | <span data-ttu-id="0ff6d-135">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0ff6d-135">Description</span></span> | <span data-ttu-id="0ff6d-136">Vereist</span><span class="sxs-lookup"><span data-stu-id="0ff6d-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ff6d-137">type</span><span class="sxs-lookup"><span data-stu-id="0ff6d-137">type</span></span> |<span data-ttu-id="0ff6d-138">Hallo type eigenschap moet worden ingesteld op: **OnPremisesSybase**</span><span class="sxs-lookup"><span data-stu-id="0ff6d-138">hello type property must be set to: **OnPremisesSybase**</span></span> |<span data-ttu-id="0ff6d-139">Ja</span><span class="sxs-lookup"><span data-stu-id="0ff6d-139">Yes</span></span> |
| <span data-ttu-id="0ff6d-140">server</span><span class="sxs-lookup"><span data-stu-id="0ff6d-140">server</span></span> |<span data-ttu-id="0ff6d-141">Naam van Hallo Sybase-server.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-141">Name of hello Sybase server.</span></span> |<span data-ttu-id="0ff6d-142">Ja</span><span class="sxs-lookup"><span data-stu-id="0ff6d-142">Yes</span></span> |
| <span data-ttu-id="0ff6d-143">database</span><span class="sxs-lookup"><span data-stu-id="0ff6d-143">database</span></span> |<span data-ttu-id="0ff6d-144">Naam van Hallo Sybase-database.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-144">Name of hello Sybase database.</span></span> |<span data-ttu-id="0ff6d-145">Ja</span><span class="sxs-lookup"><span data-stu-id="0ff6d-145">Yes</span></span> |
| <span data-ttu-id="0ff6d-146">Schema</span><span class="sxs-lookup"><span data-stu-id="0ff6d-146">schema</span></span> |<span data-ttu-id="0ff6d-147">Naam van Hallo schema in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-147">Name of hello schema in hello database.</span></span> |<span data-ttu-id="0ff6d-148">Nee</span><span class="sxs-lookup"><span data-stu-id="0ff6d-148">No</span></span> |
| <span data-ttu-id="0ff6d-149">authenticationType</span><span class="sxs-lookup"><span data-stu-id="0ff6d-149">authenticationType</span></span> |<span data-ttu-id="0ff6d-150">Type verificatie gebruikt tooconnect toohello Sybase-database.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-150">Type of authentication used tooconnect toohello Sybase database.</span></span> <span data-ttu-id="0ff6d-151">Mogelijke waarden zijn: anoniem, basis en Windows.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-151">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="0ff6d-152">Ja</span><span class="sxs-lookup"><span data-stu-id="0ff6d-152">Yes</span></span> |
| <span data-ttu-id="0ff6d-153">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="0ff6d-153">username</span></span> |<span data-ttu-id="0ff6d-154">Geef de gebruikersnaam als u basisverificatie of Windows-verificatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-154">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="0ff6d-155">Nee</span><span class="sxs-lookup"><span data-stu-id="0ff6d-155">No</span></span> |
| <span data-ttu-id="0ff6d-156">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="0ff6d-156">password</span></span> |<span data-ttu-id="0ff6d-157">Wachtwoord voor gebruikersaccount Hallo die u hebt opgegeven voor Hallo gebruikersnaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-157">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="0ff6d-158">Nee</span><span class="sxs-lookup"><span data-stu-id="0ff6d-158">No</span></span> |
| <span data-ttu-id="0ff6d-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="0ff6d-159">gatewayName</span></span> |<span data-ttu-id="0ff6d-160">Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello lokale Sybase-database gebruiken.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-160">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Sybase database.</span></span> |<span data-ttu-id="0ff6d-161">Ja</span><span class="sxs-lookup"><span data-stu-id="0ff6d-161">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="0ff6d-162">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="0ff6d-162">Dataset properties</span></span>
<span data-ttu-id="0ff6d-163">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-163">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="0ff6d-164">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).</span><span class="sxs-lookup"><span data-stu-id="0ff6d-164">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="0ff6d-165">Hallo typeProperties sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-165">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="0ff6d-166">Hallo **typeProperties** sectie voor de gegevensset van het type **RelationalTable** (inclusief Sybase gegevensset) heeft Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="0ff6d-166">hello **typeProperties** section for dataset of type **RelationalTable** (which includes Sybase dataset) has hello following properties:</span></span>

| <span data-ttu-id="0ff6d-167">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="0ff6d-167">Property</span></span> | <span data-ttu-id="0ff6d-168">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0ff6d-168">Description</span></span> | <span data-ttu-id="0ff6d-169">Vereist</span><span class="sxs-lookup"><span data-stu-id="0ff6d-169">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0ff6d-170">tableName</span><span class="sxs-lookup"><span data-stu-id="0ff6d-170">tableName</span></span> |<span data-ttu-id="0ff6d-171">De naam van de tabel Hallo in Hallo Sybase-Database-instantie waarnaar de gekoppelde service verwijst.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-171">Name of hello table in hello Sybase Database instance that linked service refers to.</span></span> |<span data-ttu-id="0ff6d-172">Nee (als **query** van **RelationalSource** is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="0ff6d-172">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="0ff6d-173">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="0ff6d-173">Copy activity properties</span></span>
<span data-ttu-id="0ff6d-174">Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-174">For a full list of sections & properties available for defining activities, see [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="0ff6d-175">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en -beleid zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-175">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="0ff6d-176">Terwijl de eigenschappen die beschikbaar zijn in Hallo typeProperties gedeelte van de activiteit Hallo variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-176">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="0ff6d-177">Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-177">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="0ff6d-178">Wanneer Hallo-bron is van het type **RelationalSource** (waaronder Sybase), Hallo volgende eigenschappen beschikbaar zijn in **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="0ff6d-178">When hello source is of type **RelationalSource** (which includes Sybase), hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="0ff6d-179">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="0ff6d-179">Property</span></span> | <span data-ttu-id="0ff6d-180">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0ff6d-180">Description</span></span> | <span data-ttu-id="0ff6d-181">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="0ff6d-181">Allowed values</span></span> | <span data-ttu-id="0ff6d-182">Vereist</span><span class="sxs-lookup"><span data-stu-id="0ff6d-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ff6d-183">query</span><span class="sxs-lookup"><span data-stu-id="0ff6d-183">query</span></span> |<span data-ttu-id="0ff6d-184">Hallo aangepaste query tooread gegevens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-184">Use hello custom query tooread data.</span></span> |<span data-ttu-id="0ff6d-185">SQL-query-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-185">SQL query string.</span></span> <span data-ttu-id="0ff6d-186">Bijvoorbeeld: Selecteer * from MijnTabel.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-186">For example: select * from MyTable.</span></span> |<span data-ttu-id="0ff6d-187">Nee (als **tableName** van **gegevensset** is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="0ff6d-187">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-sybase-tooazure-blob"></a><span data-ttu-id="0ff6d-188">JSON-voorbeeld: gegevens kopiëren van Sybase tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="0ff6d-188">JSON example: Copy data from Sybase tooAzure Blob</span></span>
<span data-ttu-id="0ff6d-189">Hallo volgende voorbeeld wordt een voorbeeld JSON definities waarmee u een pijplijn toocreate kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="0ff6d-189">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="0ff6d-190">Ze geven weer hoe toocopy gegevens van Sybase-database tooAzure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-190">They show how toocopy data from Sybase database tooAzure Blob Storage.</span></span> <span data-ttu-id="0ff6d-191">Gegevens kunnen echter wel gekopieerde tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-191">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="0ff6d-192">Hallo voorbeeld heeft Hallo data factory-entiteiten te volgen:</span><span class="sxs-lookup"><span data-stu-id="0ff6d-192">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="0ff6d-193">Een gekoppelde service van het type [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ff6d-193">A linked service of type [OnPremisesSybase](data-factory-onprem-sybase-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="0ff6d-194">Een liked service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="0ff6d-194">A liked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="0ff6d-195">Invoer [gegevensset](data-factory-create-datasets.md) van het type [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0ff6d-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-sybase-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="0ff6d-196">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="0ff6d-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="0ff6d-197">Hallo [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="0ff6d-197">hello [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-sybase-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="0ff6d-198">Hallo voorbeeld kopieert gegevens van de resultaten van een query in een Sybase-database tooa blob elk uur.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-198">hello sample copies data from a query result in Sybase database tooa blob every hour.</span></span> <span data-ttu-id="0ff6d-199">Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-199">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="0ff6d-200">Instellen als eerste stap Hallo data management gateway.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-200">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="0ff6d-201">Hallo-instructies vindt u in Hallo [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-201">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="0ff6d-202">**Sybase gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="0ff6d-202">**Sybase linked service:**</span></span>

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

<span data-ttu-id="0ff6d-203">**Azure Blob-opslag gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="0ff6d-203">**Azure Blob storage linked service:**</span></span>

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

<span data-ttu-id="0ff6d-204">**Sybase invoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="0ff6d-204">**Sybase input dataset:**</span></span>

<span data-ttu-id="0ff6d-205">Hallo-voorbeeld wordt ervan uitgegaan dat u hebt een tabel 'MijnTabel' gemaakt in Sybase en bevat een kolom met de naam 'tijdstempel' voor de reeksgegevens.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-205">hello sample assumes you have created a table “MyTable” in Sybase and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="0ff6d-206">Instelling 'extern': true Hallo Data Factory-service informeert dat deze gegevensset externe toohello gegevensfactory en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-206">Setting “external”: true informs hello Data Factory service that this dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span> <span data-ttu-id="0ff6d-207">U ziet dat Hallo **type** Hallo gekoppelde service is ingesteld op: **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-207">Notice that hello **type** of hello linked service is set to: **RelationalTable**.</span></span>

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

<span data-ttu-id="0ff6d-208">**Azure Blob-uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="0ff6d-208">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="0ff6d-209">Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="0ff6d-209">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="0ff6d-210">pad naar map voor blob Hallo Hallo wordt dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-210">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="0ff6d-211">Hallo mappad jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-211">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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

<span data-ttu-id="0ff6d-212">**Pijplijn met de kopieeractiviteit:**</span><span class="sxs-lookup"><span data-stu-id="0ff6d-212">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="0ff6d-213">Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun per uur is.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-213">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="0ff6d-214">Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**RelationalSource** en **sink** type is ingesteld, te**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-214">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="0ff6d-215">Hallo SQL-query is opgegeven voor Hallo **query** eigenschap Hallo gegevens uit Hallo DBA geselecteerd. Ordertabel in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-215">hello SQL query specified for hello **query** property selects hello data from hello DBA.Orders table in hello database.</span></span>

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

## <a name="type-mapping-for-sybase"></a><span data-ttu-id="0ff6d-216">Toewijzing van het type voor Sybase</span><span class="sxs-lookup"><span data-stu-id="0ff6d-216">Type mapping for Sybase</span></span>
<span data-ttu-id="0ff6d-217">Zoals vermeld in Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel Hallo kopieeractiviteit voert automatische typeconversies van brontypen typen toosink Hello 2 stap benadering te volgen:</span><span class="sxs-lookup"><span data-stu-id="0ff6d-217">As mentioned in hello [Data Movement Activities](data-factory-data-movement-activities.md) article, hello Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="0ff6d-218">Systeemeigen bron typen too.NET type converteren</span><span class="sxs-lookup"><span data-stu-id="0ff6d-218">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="0ff6d-219">Converteren van .NET-type toonative sink-type</span><span class="sxs-lookup"><span data-stu-id="0ff6d-219">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="0ff6d-220">Sybase ondersteunt T-SQL en T-SQL-typen.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-220">Sybase supports T-SQL and T-SQL types.</span></span> <span data-ttu-id="0ff6d-221">Zie voor een toewijzingstabel van sql typen too.NET type [Azure SQL-Connector](data-factory-azure-sql-connector.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-221">For a mapping table from sql types too.NET type, see [Azure SQL Connector](data-factory-azure-sql-connector.md) article.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="0ff6d-222">Bronkolommen toosink toewijzen</span><span class="sxs-lookup"><span data-stu-id="0ff6d-222">Map source toosink columns</span></span>
<span data-ttu-id="0ff6d-223">Zie toolearn over het toewijzen van kolommen in bron gegevensset toocolumns in sink-gegevensset [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="0ff6d-223">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="0ff6d-224">Herhaalbare leesbewerking van relationele bronnen</span><span class="sxs-lookup"><span data-stu-id="0ff6d-224">Repeatable read from relational sources</span></span>
<span data-ttu-id="0ff6d-225">Houd bij het kopiëren van gegevens uit een relationele gegevensopslag, herhaalbaarheid rekening tooavoid ongewenste resultaten.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-225">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="0ff6d-226">In Azure Data Factory, kunt u een segment handmatig opnieuw.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-226">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="0ff6d-227">U kunt ook een beleid voor opnieuw proberen voor een gegevensset configureren zodat een segment wordt opnieuw uitgevoerd wanneer een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-227">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="0ff6d-228">Wanneer een segment opnieuw in beide gevallen wordt uitgevoerd, moet u ervoor dat dezelfde gegevens Hallo toomake wordt gelezen ongeacht hoe vaak een segment wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-228">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="0ff6d-229">Zie [Repeatable van relationele bronnen lezen](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="0ff6d-229">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="0ff6d-230">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="0ff6d-230">Performance and Tuning</span></span>
<span data-ttu-id="0ff6d-231">Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.</span><span class="sxs-lookup"><span data-stu-id="0ff6d-231">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
