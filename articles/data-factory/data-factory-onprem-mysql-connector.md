---
title: aaaMove gegevens van MySQL met behulp van Azure Data Factory | Microsoft Docs
description: Meer informatie over hoe de gegevens toomove van MySQL-database met behulp van Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 452f4fce-9eb5-40a0-92f8-1e98691bea4c
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: jingwang
ms.openlocfilehash: 3ffe969e42ce1a54b265c4739df43fdc594ea891
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mysql-using-azure-data-factory"></a><span data-ttu-id="97925-103">Verplaatsen van gegevens van MySQL met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="97925-103">Move data From MySQL using Azure Data Factory</span></span>
<span data-ttu-id="97925-104">Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit Hallo in Azure Data Factory toomove gegevens uit een lokale MySQL-database.</span><span class="sxs-lookup"><span data-stu-id="97925-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises MySQL database.</span></span> <span data-ttu-id="97925-105">Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.</span><span class="sxs-lookup"><span data-stu-id="97925-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="97925-106">U kunt gegevens uit een on-premises MySQL store tooany ondersteund sink gegevens gegevensopslag kopiëren.</span><span class="sxs-lookup"><span data-stu-id="97925-106">You can copy data from an on-premises MySQL data store tooany supported sink data store.</span></span> <span data-ttu-id="97925-107">Zie voor een lijst van gegevens winkels ondersteund zoals sinks door kopieeractiviteit hello, Hallo [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel.</span><span class="sxs-lookup"><span data-stu-id="97925-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="97925-108">Data factory ondersteunt momenteel alleen gegevens uit een MySQL-gegevens opslaan tooother gegevensarchieven verplaatsen, maar niet voor het verplaatsen van gegevens uit andere gegevens winkels tooan MySQL-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="97925-108">Data factory currently supports only moving data from a MySQL data store tooother data stores, but not for moving data from other data stores tooan MySQL data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="97925-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="97925-109">Prerequisites</span></span>
<span data-ttu-id="97925-110">Data Factory-service ondersteunt verbindende tooon lokale MySQL gegevensbronnen waarvoor gebruik Hallo Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="97925-110">Data Factory service supports connecting tooon-premises MySQL sources using hello Data Management Gateway.</span></span> <span data-ttu-id="97925-111">Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn artikel over Data Management Gateway en stapsgewijze instructies over het instellen van Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="97925-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="97925-112">Gateway is vereist, zelfs als Hallo MySQL-database wordt gehost in een Azure IaaS virtuele machine (VM).</span><span class="sxs-lookup"><span data-stu-id="97925-112">Gateway is required even if hello MySQL database is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="97925-113">U kunt Hallo gateway installeren op Hallo dezelfde virtuele machine als Hallo gegevens opslaan of op een andere virtuele machine zo lang Hallo gateway kunt verbinding maken met toohello-database.</span><span class="sxs-lookup"><span data-stu-id="97925-113">You can install hello gateway on hello same VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="97925-114">Zie [gateway problemen](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) voor tips over het oplossen van verbinding of gateway gerelateerde problemen.</span><span class="sxs-lookup"><span data-stu-id="97925-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="97925-115">Ondersteunde versies en installatie</span><span class="sxs-lookup"><span data-stu-id="97925-115">Supported versions and installation</span></span>
<span data-ttu-id="97925-116">Data Management Gateway tooconnect toohello MySQL-Database, moet u tooinstall hello [MySQL Connector/Net voor Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (versie 6.6.5 of hoger) Hallo op hetzelfde systeem als Data Management Gateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="97925-116">For Data Management Gateway tooconnect toohello MySQL Database, you need tooinstall hello [MySQL Connector/Net for Microsoft Windows](https://dev.mysql.com/downloads/connector/net/) (version 6.6.5 or above) on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="97925-117">MySQL versie 5.1 en hoger wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="97925-117">MySQL version 5.1 and above is supported.</span></span>

> [!TIP]
> <span data-ttu-id="97925-118">Als u fout raakt op 'Verificatie is mislukt omdat de externe partij Hallo heeft gesloten hello transport stroom.', overweeg tooupgrade Hallo MySQL Connector/Net toohigher versie.</span><span class="sxs-lookup"><span data-stu-id="97925-118">If you hit error on "Authentication failed because hello remote party has closed hello transport stream.", consider tooupgrade hello MySQL Connector/Net toohigher version.</span></span>

## <a name="getting-started"></a><span data-ttu-id="97925-119">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="97925-119">Getting started</span></span>
<span data-ttu-id="97925-120">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens vanuit een on-premises Cassandra-gegevensopslag verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="97925-120">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="97925-121">Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="97925-121">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="97925-122">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="97925-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="97925-123">U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="97925-123">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="97925-124">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="97925-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="97925-125">Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="97925-125">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="97925-126">Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="97925-126">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="97925-127">Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="97925-127">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="97925-128">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="97925-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="97925-129">Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="97925-129">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="97925-130">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="97925-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="97925-131">Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens uit een on-premises MySQL-gegevensopslag zijn [JSON-voorbeeld: gegevens kopiëren van MySQL tooAzure Blob](#json-example-copy-data-from-mysql-to-azure-blob) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="97925-131">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises MySQL data store, see [JSON example: Copy data from MySQL tooAzure Blob](#json-example-copy-data-from-mysql-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="97925-132">Hallo volgende secties vindt u informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooa MySQL-gegevensarchief zijn:</span><span class="sxs-lookup"><span data-stu-id="97925-132">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa MySQL data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="97925-133">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="97925-133">Linked service properties</span></span>
<span data-ttu-id="97925-134">Hallo volgende tabel biedt een beschrijving voor de JSON-elementen specifieke tooMySQL gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="97925-134">hello following table provides description for JSON elements specific tooMySQL linked service.</span></span>

| <span data-ttu-id="97925-135">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="97925-135">Property</span></span> | <span data-ttu-id="97925-136">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="97925-136">Description</span></span> | <span data-ttu-id="97925-137">Vereist</span><span class="sxs-lookup"><span data-stu-id="97925-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="97925-138">type</span><span class="sxs-lookup"><span data-stu-id="97925-138">type</span></span> |<span data-ttu-id="97925-139">Hallo type eigenschap moet worden ingesteld op: **OnPremisesMySql**</span><span class="sxs-lookup"><span data-stu-id="97925-139">hello type property must be set to: **OnPremisesMySql**</span></span> |<span data-ttu-id="97925-140">Ja</span><span class="sxs-lookup"><span data-stu-id="97925-140">Yes</span></span> |
| <span data-ttu-id="97925-141">server</span><span class="sxs-lookup"><span data-stu-id="97925-141">server</span></span> |<span data-ttu-id="97925-142">Naam van Hallo MySQL-server.</span><span class="sxs-lookup"><span data-stu-id="97925-142">Name of hello MySQL server.</span></span> |<span data-ttu-id="97925-143">Ja</span><span class="sxs-lookup"><span data-stu-id="97925-143">Yes</span></span> |
| <span data-ttu-id="97925-144">database</span><span class="sxs-lookup"><span data-stu-id="97925-144">database</span></span> |<span data-ttu-id="97925-145">Naam van Hallo MySQL-database.</span><span class="sxs-lookup"><span data-stu-id="97925-145">Name of hello MySQL database.</span></span> |<span data-ttu-id="97925-146">Ja</span><span class="sxs-lookup"><span data-stu-id="97925-146">Yes</span></span> |
| <span data-ttu-id="97925-147">Schema</span><span class="sxs-lookup"><span data-stu-id="97925-147">schema</span></span> |<span data-ttu-id="97925-148">Naam van Hallo schema in Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="97925-148">Name of hello schema in hello database.</span></span> |<span data-ttu-id="97925-149">Nee</span><span class="sxs-lookup"><span data-stu-id="97925-149">No</span></span> |
| <span data-ttu-id="97925-150">authenticationType</span><span class="sxs-lookup"><span data-stu-id="97925-150">authenticationType</span></span> |<span data-ttu-id="97925-151">Type verificatie gebruikt tooconnect toohello MySQL-database.</span><span class="sxs-lookup"><span data-stu-id="97925-151">Type of authentication used tooconnect toohello MySQL database.</span></span> <span data-ttu-id="97925-152">Mogelijke waarden zijn: `Basic`.</span><span class="sxs-lookup"><span data-stu-id="97925-152">Possible values are: `Basic`.</span></span> |<span data-ttu-id="97925-153">Ja</span><span class="sxs-lookup"><span data-stu-id="97925-153">Yes</span></span> |
| <span data-ttu-id="97925-154">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="97925-154">username</span></span> |<span data-ttu-id="97925-155">Geef de gebruiker de naam van tooconnect toohello MySQL-database.</span><span class="sxs-lookup"><span data-stu-id="97925-155">Specify user name tooconnect toohello MySQL database.</span></span> |<span data-ttu-id="97925-156">Ja</span><span class="sxs-lookup"><span data-stu-id="97925-156">Yes</span></span> |
| <span data-ttu-id="97925-157">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="97925-157">password</span></span> |<span data-ttu-id="97925-158">Geef het wachtwoord voor Hallo-gebruikersaccount die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="97925-158">Specify password for hello user account you specified.</span></span> |<span data-ttu-id="97925-159">Ja</span><span class="sxs-lookup"><span data-stu-id="97925-159">Yes</span></span> |
| <span data-ttu-id="97925-160">gatewayName</span><span class="sxs-lookup"><span data-stu-id="97925-160">gatewayName</span></span> |<span data-ttu-id="97925-161">Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello lokale MySQL-database gebruiken.</span><span class="sxs-lookup"><span data-stu-id="97925-161">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises MySQL database.</span></span> |<span data-ttu-id="97925-162">Ja</span><span class="sxs-lookup"><span data-stu-id="97925-162">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="97925-163">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="97925-163">Dataset properties</span></span>
<span data-ttu-id="97925-164">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="97925-164">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="97925-165">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).</span><span class="sxs-lookup"><span data-stu-id="97925-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="97925-166">Hallo **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="97925-166">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="97925-167">Hallo typeProperties sectie voor de gegevensset van het type **RelationalTable** (inclusief MySQL gegevensset) heeft Hallo volgende eigenschappen</span><span class="sxs-lookup"><span data-stu-id="97925-167">hello typeProperties section for dataset of type **RelationalTable** (which includes MySQL dataset) has hello following properties</span></span>

| <span data-ttu-id="97925-168">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="97925-168">Property</span></span> | <span data-ttu-id="97925-169">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="97925-169">Description</span></span> | <span data-ttu-id="97925-170">Vereist</span><span class="sxs-lookup"><span data-stu-id="97925-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="97925-171">tableName</span><span class="sxs-lookup"><span data-stu-id="97925-171">tableName</span></span> |<span data-ttu-id="97925-172">De naam van de tabel Hallo in Hallo MySQL-Database-instantie waarnaar de gekoppelde service verwijst.</span><span class="sxs-lookup"><span data-stu-id="97925-172">Name of hello table in hello MySQL Database instance that linked service refers to.</span></span> |<span data-ttu-id="97925-173">Nee (als **query** van **RelationalSource** is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="97925-173">No (if **query** of **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="97925-174">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="97925-174">Copy activity properties</span></span>
<span data-ttu-id="97925-175">Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="97925-175">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="97925-176">Eigenschappen zoals naam, beschrijving, invoer en uitvoer tabellen, zijn de beleidsregels zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="97925-176">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="97925-177">Dat eigenschappen beschikbaar zijn in Hallo **typeProperties** sectie van de activiteit Hallo variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="97925-177">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="97925-178">Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="97925-178">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="97925-179">Wanneer u de gegevensbron in de kopieerbewerking is van het type **RelationalSource** (waaronder MySQL), Hallo volgende eigenschappen beschikbaar zijn in de sectie typeProperties:</span><span class="sxs-lookup"><span data-stu-id="97925-179">When source in copy activity is of type **RelationalSource** (which includes MySQL), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="97925-180">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="97925-180">Property</span></span> | <span data-ttu-id="97925-181">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="97925-181">Description</span></span> | <span data-ttu-id="97925-182">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="97925-182">Allowed values</span></span> | <span data-ttu-id="97925-183">Vereist</span><span class="sxs-lookup"><span data-stu-id="97925-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="97925-184">query</span><span class="sxs-lookup"><span data-stu-id="97925-184">query</span></span> |<span data-ttu-id="97925-185">Hallo aangepaste query tooread gegevens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="97925-185">Use hello custom query tooread data.</span></span> |<span data-ttu-id="97925-186">SQL-query-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="97925-186">SQL query string.</span></span> <span data-ttu-id="97925-187">Bijvoorbeeld: Selecteer * from MijnTabel.</span><span class="sxs-lookup"><span data-stu-id="97925-187">For example: select * from MyTable.</span></span> |<span data-ttu-id="97925-188">Nee (als **tableName** van **gegevensset** is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="97925-188">No (if **tableName** of **dataset** is specified)</span></span> |


## <a name="json-example-copy-data-from-mysql-tooazure-blob"></a><span data-ttu-id="97925-189">JSON-voorbeeld: gegevens kopiëren van MySQL tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="97925-189">JSON example: Copy data from MySQL tooAzure Blob</span></span>
<span data-ttu-id="97925-190">In dit voorbeeld voorbeeld JSON definities bevat dat u een pijplijn toocreate gebruiken met behulp van kunt [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="97925-190">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="97925-191">Er wordt weergegeven hoe toocopy gegevens uit een lokale MySQL-database tooan Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="97925-191">It shows how toocopy data from an on-premises MySQL database tooan Azure Blob Storage.</span></span> <span data-ttu-id="97925-192">Gegevens kunnen echter wel gekopieerde tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="97925-192">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="97925-193">Dit voorbeeld bevat JSON-fragmenten.</span><span class="sxs-lookup"><span data-stu-id="97925-193">This sample provides JSON snippets.</span></span> <span data-ttu-id="97925-194">Dit omvat geen stapsgewijze instructies voor het maken van de gegevensfactory Hallo.</span><span class="sxs-lookup"><span data-stu-id="97925-194">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="97925-195">Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor stapsgewijze instructies.</span><span class="sxs-lookup"><span data-stu-id="97925-195">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="97925-196">Hallo voorbeeld heeft Hallo data factory-entiteiten te volgen:</span><span class="sxs-lookup"><span data-stu-id="97925-196">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="97925-197">Een gekoppelde service van het type [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="97925-197">A linked service of type [OnPremisesMySql](data-factory-onprem-mysql-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="97925-198">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="97925-198">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="97925-199">Invoer [gegevensset](data-factory-create-datasets.md) van het type [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="97925-199">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-mysql-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="97925-200">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="97925-200">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="97925-201">Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="97925-201">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](data-factory-onprem-mysql-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="97925-202">Hallo voorbeeld gegevens worden gekopieerd van de resultaten van een query in een MySQL-database tooa blob per uur.</span><span class="sxs-lookup"><span data-stu-id="97925-202">hello sample copies data from a query result in MySQL database tooa blob hourly.</span></span> <span data-ttu-id="97925-203">Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="97925-203">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="97925-204">Instellen als eerste stap Hallo data management gateway.</span><span class="sxs-lookup"><span data-stu-id="97925-204">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="97925-205">Hallo-instructies vindt u in Hallo [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="97925-205">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="97925-206">**MySQL gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="97925-206">**MySQL linked service:**</span></span>

```JSON
    {
      "name": "OnPremMySqlLinkedService",
      "properties": {
        "type": "OnPremisesMySql",
        "typeProperties": {
          "server": "<server name>",
          "database": "<database name>",
          "schema": "<schema name>",
          "authenticationType": "<authentication type>",
          "userName": "<user name>",
          "password": "<password>",
          "gatewayName": "<gateway>"
        }
      }
    }
```

<span data-ttu-id="97925-207">**Gekoppelde Azure Storage-service:**</span><span class="sxs-lookup"><span data-stu-id="97925-207">**Azure Storage linked service:**</span></span>

```JSON
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

<span data-ttu-id="97925-208">**MySQL-invoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="97925-208">**MySQL input dataset:**</span></span>

<span data-ttu-id="97925-209">Hallo-voorbeeld wordt ervan uitgegaan dat u hebt een tabel 'MijnTabel' gemaakt in MySQL en bevat een kolom met de naam 'timestampcolumn' voor de reeksgegevens.</span><span class="sxs-lookup"><span data-stu-id="97925-209">hello sample assumes you have created a table “MyTable” in MySQL and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="97925-210">Instelling 'extern': 'true' informeert Hallo Data Factory-service die tabel Hallo externe toohello data factory is en niet wordt geproduceerd door een activiteit in de gegevensfactory Hallo.</span><span class="sxs-lookup"><span data-stu-id="97925-210">Setting “external”: ”true” informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
    {
        "name": "MySqlDataSet",
        "properties": {
            "published": false,
            "type": "RelationalTable",
            "linkedServiceName": "OnPremMySqlLinkedService",
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

<span data-ttu-id="97925-211">**Azure Blob-uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="97925-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="97925-212">Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="97925-212">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="97925-213">pad naar map voor blob Hallo Hallo wordt dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="97925-213">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="97925-214">Hallo mappad jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="97925-214">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```JSON
    {
        "name": "AzureBlobMySqlDataSet",
        "properties": {
            "type": "AzureBlob",
            "linkedServiceName": "AzureStorageLinkedService",
            "typeProperties": {
                "folderPath": "mycontainer/mysql/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="97925-215">**Pijplijn met de kopieeractiviteit:**</span><span class="sxs-lookup"><span data-stu-id="97925-215">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="97925-216">Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur.</span><span class="sxs-lookup"><span data-stu-id="97925-216">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="97925-217">Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**RelationalSource** en **sink** type is ingesteld, te**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="97925-217">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="97925-218">Hallo SQL-query is opgegeven voor Hallo **query** eigenschap Hallo gegevens selecteert in Hallo voorbij toocopy uur.</span><span class="sxs-lookup"><span data-stu-id="97925-218">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```JSON
    {
        "name": "CopyMySqlToBlob",
        "properties": {
            "description": "pipeline for copy activity",
            "activities": [
                {
                    "type": "Copy",
                    "typeProperties": {
                        "source": {
                            "type": "RelationalSource",
                            "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                        },
                        "sink": {
                            "type": "BlobSink",
                            "writeBatchSize": 0,
                            "writeBatchTimeout": "00:00:00"
                        }
                    },
                    "inputs": [
                        {
                            "name": "MySqlDataSet"
                        }
                    ],
                    "outputs": [
                        {
                            "name": "AzureBlobMySqlDataSet"
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
                    "name": "MySqlToBlob"
                }
            ],
            "start": "2014-06-01T18:00:00Z",
            "end": "2014-06-01T19:00:00Z"
        }
    }
```


### <a name="type-mapping-for-mysql"></a><span data-ttu-id="97925-219">Toewijzing van het type voor MySQL</span><span class="sxs-lookup"><span data-stu-id="97925-219">Type mapping for MySQL</span></span>
<span data-ttu-id="97925-220">Zoals vermeld in Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel kopieeractiviteit voert automatische typeconversies van brontypen typen toosink Hello benadering in twee stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="97925-220">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="97925-221">Systeemeigen bron typen too.NET type converteren</span><span class="sxs-lookup"><span data-stu-id="97925-221">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="97925-222">Converteren van .NET-type toonative sink-type</span><span class="sxs-lookup"><span data-stu-id="97925-222">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="97925-223">Bij het verplaatsen van gegevens tooMySQL worden hello volgende toewijzingen gebruikt vanaf MySQL typen too.NET typen.</span><span class="sxs-lookup"><span data-stu-id="97925-223">When moving data tooMySQL, hello following mappings are used from MySQL types too.NET types.</span></span>

| <span data-ttu-id="97925-224">Type MySQL-Database</span><span class="sxs-lookup"><span data-stu-id="97925-224">MySQL Database type</span></span> | <span data-ttu-id="97925-225">.NET framework-type</span><span class="sxs-lookup"><span data-stu-id="97925-225">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="97925-226">niet-ondertekende bigint</span><span class="sxs-lookup"><span data-stu-id="97925-226">bigint unsigned</span></span> |<span data-ttu-id="97925-227">Decimale</span><span class="sxs-lookup"><span data-stu-id="97925-227">Decimal</span></span> |
| <span data-ttu-id="97925-228">bigint</span><span class="sxs-lookup"><span data-stu-id="97925-228">bigint</span></span> |<span data-ttu-id="97925-229">Int64</span><span class="sxs-lookup"><span data-stu-id="97925-229">Int64</span></span> |
| <span data-ttu-id="97925-230">bits</span><span class="sxs-lookup"><span data-stu-id="97925-230">bit</span></span> |<span data-ttu-id="97925-231">Decimale</span><span class="sxs-lookup"><span data-stu-id="97925-231">Decimal</span></span> |
| <span data-ttu-id="97925-232">BLOB</span><span class="sxs-lookup"><span data-stu-id="97925-232">blob</span></span> |<span data-ttu-id="97925-233">Byte]</span><span class="sxs-lookup"><span data-stu-id="97925-233">Byte[]</span></span> |
| <span data-ttu-id="97925-234">BOOL</span><span class="sxs-lookup"><span data-stu-id="97925-234">bool</span></span> |<span data-ttu-id="97925-235">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="97925-235">Boolean</span></span> |
| <span data-ttu-id="97925-236">CHAR</span><span class="sxs-lookup"><span data-stu-id="97925-236">char</span></span> |<span data-ttu-id="97925-237">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="97925-237">String</span></span> |
| <span data-ttu-id="97925-238">Datum</span><span class="sxs-lookup"><span data-stu-id="97925-238">date</span></span> |<span data-ttu-id="97925-239">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="97925-239">Datetime</span></span> |
| <span data-ttu-id="97925-240">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="97925-240">datetime</span></span> |<span data-ttu-id="97925-241">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="97925-241">Datetime</span></span> |
| <span data-ttu-id="97925-242">Decimale</span><span class="sxs-lookup"><span data-stu-id="97925-242">decimal</span></span> |<span data-ttu-id="97925-243">Decimale</span><span class="sxs-lookup"><span data-stu-id="97925-243">Decimal</span></span> |
| <span data-ttu-id="97925-244">dubbele precisie</span><span class="sxs-lookup"><span data-stu-id="97925-244">double precision</span></span> |<span data-ttu-id="97925-245">dubbele</span><span class="sxs-lookup"><span data-stu-id="97925-245">Double</span></span> |
| <span data-ttu-id="97925-246">dubbele</span><span class="sxs-lookup"><span data-stu-id="97925-246">double</span></span> |<span data-ttu-id="97925-247">dubbele</span><span class="sxs-lookup"><span data-stu-id="97925-247">Double</span></span> |
| <span data-ttu-id="97925-248">Enum</span><span class="sxs-lookup"><span data-stu-id="97925-248">enum</span></span> |<span data-ttu-id="97925-249">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="97925-249">String</span></span> |
| <span data-ttu-id="97925-250">Float</span><span class="sxs-lookup"><span data-stu-id="97925-250">float</span></span> |<span data-ttu-id="97925-251">Één</span><span class="sxs-lookup"><span data-stu-id="97925-251">Single</span></span> |
| <span data-ttu-id="97925-252">niet-ondertekende int</span><span class="sxs-lookup"><span data-stu-id="97925-252">int unsigned</span></span> |<span data-ttu-id="97925-253">Int64</span><span class="sxs-lookup"><span data-stu-id="97925-253">Int64</span></span> |
| <span data-ttu-id="97925-254">int</span><span class="sxs-lookup"><span data-stu-id="97925-254">int</span></span> |<span data-ttu-id="97925-255">Int32</span><span class="sxs-lookup"><span data-stu-id="97925-255">Int32</span></span> |
| <span data-ttu-id="97925-256">niet-ondertekend geheel getal</span><span class="sxs-lookup"><span data-stu-id="97925-256">integer unsigned</span></span> |<span data-ttu-id="97925-257">Int64</span><span class="sxs-lookup"><span data-stu-id="97925-257">Int64</span></span> |
| <span data-ttu-id="97925-258">geheel getal</span><span class="sxs-lookup"><span data-stu-id="97925-258">integer</span></span> |<span data-ttu-id="97925-259">Int32</span><span class="sxs-lookup"><span data-stu-id="97925-259">Int32</span></span> |
| <span data-ttu-id="97925-260">lange varbinary</span><span class="sxs-lookup"><span data-stu-id="97925-260">long varbinary</span></span> |<span data-ttu-id="97925-261">Byte]</span><span class="sxs-lookup"><span data-stu-id="97925-261">Byte[]</span></span> |
| <span data-ttu-id="97925-262">lange varchar</span><span class="sxs-lookup"><span data-stu-id="97925-262">long varchar</span></span> |<span data-ttu-id="97925-263">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="97925-263">String</span></span> |
| <span data-ttu-id="97925-264">longblob</span><span class="sxs-lookup"><span data-stu-id="97925-264">longblob</span></span> |<span data-ttu-id="97925-265">Byte]</span><span class="sxs-lookup"><span data-stu-id="97925-265">Byte[]</span></span> |
| <span data-ttu-id="97925-266">LONGTEXT</span><span class="sxs-lookup"><span data-stu-id="97925-266">longtext</span></span> |<span data-ttu-id="97925-267">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="97925-267">String</span></span> |
| <span data-ttu-id="97925-268">mediumblob</span><span class="sxs-lookup"><span data-stu-id="97925-268">mediumblob</span></span> |<span data-ttu-id="97925-269">Byte]</span><span class="sxs-lookup"><span data-stu-id="97925-269">Byte[]</span></span> |
| <span data-ttu-id="97925-270">niet-ondertekende mediumint</span><span class="sxs-lookup"><span data-stu-id="97925-270">mediumint unsigned</span></span> |<span data-ttu-id="97925-271">Int64</span><span class="sxs-lookup"><span data-stu-id="97925-271">Int64</span></span> |
| <span data-ttu-id="97925-272">mediumint</span><span class="sxs-lookup"><span data-stu-id="97925-272">mediumint</span></span> |<span data-ttu-id="97925-273">Int32</span><span class="sxs-lookup"><span data-stu-id="97925-273">Int32</span></span> |
| <span data-ttu-id="97925-274">mediumtext</span><span class="sxs-lookup"><span data-stu-id="97925-274">mediumtext</span></span> |<span data-ttu-id="97925-275">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="97925-275">String</span></span> |
| <span data-ttu-id="97925-276">numerieke</span><span class="sxs-lookup"><span data-stu-id="97925-276">numeric</span></span> |<span data-ttu-id="97925-277">Decimale</span><span class="sxs-lookup"><span data-stu-id="97925-277">Decimal</span></span> |
| <span data-ttu-id="97925-278">echte</span><span class="sxs-lookup"><span data-stu-id="97925-278">real</span></span> |<span data-ttu-id="97925-279">dubbele</span><span class="sxs-lookup"><span data-stu-id="97925-279">Double</span></span> |
| <span data-ttu-id="97925-280">instellen</span><span class="sxs-lookup"><span data-stu-id="97925-280">set</span></span> |<span data-ttu-id="97925-281">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="97925-281">String</span></span> |
| <span data-ttu-id="97925-282">niet-ondertekende smallint</span><span class="sxs-lookup"><span data-stu-id="97925-282">smallint unsigned</span></span> |<span data-ttu-id="97925-283">Int32</span><span class="sxs-lookup"><span data-stu-id="97925-283">Int32</span></span> |
| <span data-ttu-id="97925-284">smallint</span><span class="sxs-lookup"><span data-stu-id="97925-284">smallint</span></span> |<span data-ttu-id="97925-285">Int16</span><span class="sxs-lookup"><span data-stu-id="97925-285">Int16</span></span> |
| <span data-ttu-id="97925-286">Tekst</span><span class="sxs-lookup"><span data-stu-id="97925-286">text</span></span> |<span data-ttu-id="97925-287">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="97925-287">String</span></span> |
| <span data-ttu-id="97925-288">tijd</span><span class="sxs-lookup"><span data-stu-id="97925-288">time</span></span> |<span data-ttu-id="97925-289">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="97925-289">TimeSpan</span></span> |
| <span data-ttu-id="97925-290">tijdstempel</span><span class="sxs-lookup"><span data-stu-id="97925-290">timestamp</span></span> |<span data-ttu-id="97925-291">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="97925-291">Datetime</span></span> |
| <span data-ttu-id="97925-292">tinyblob</span><span class="sxs-lookup"><span data-stu-id="97925-292">tinyblob</span></span> |<span data-ttu-id="97925-293">Byte]</span><span class="sxs-lookup"><span data-stu-id="97925-293">Byte[]</span></span> |
| <span data-ttu-id="97925-294">niet-ondertekende tinyint</span><span class="sxs-lookup"><span data-stu-id="97925-294">tinyint unsigned</span></span> |<span data-ttu-id="97925-295">Int16</span><span class="sxs-lookup"><span data-stu-id="97925-295">Int16</span></span> |
| <span data-ttu-id="97925-296">tinyint</span><span class="sxs-lookup"><span data-stu-id="97925-296">tinyint</span></span> |<span data-ttu-id="97925-297">Int16</span><span class="sxs-lookup"><span data-stu-id="97925-297">Int16</span></span> |
| <span data-ttu-id="97925-298">tinytext</span><span class="sxs-lookup"><span data-stu-id="97925-298">tinytext</span></span> |<span data-ttu-id="97925-299">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="97925-299">String</span></span> |
| <span data-ttu-id="97925-300">varchar</span><span class="sxs-lookup"><span data-stu-id="97925-300">varchar</span></span> |<span data-ttu-id="97925-301">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="97925-301">String</span></span> |
| <span data-ttu-id="97925-302">jaar</span><span class="sxs-lookup"><span data-stu-id="97925-302">year</span></span> |<span data-ttu-id="97925-303">int</span><span class="sxs-lookup"><span data-stu-id="97925-303">Int</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="97925-304">Bronkolommen toosink toewijzen</span><span class="sxs-lookup"><span data-stu-id="97925-304">Map source toosink columns</span></span>
<span data-ttu-id="97925-305">Zie toolearn over het toewijzen van kolommen in bron gegevensset toocolumns in sink-gegevensset [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="97925-305">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="97925-306">Herhaalbare leesbewerking van relationele bronnen</span><span class="sxs-lookup"><span data-stu-id="97925-306">Repeatable read from relational sources</span></span>
<span data-ttu-id="97925-307">Houd bij het kopiëren van gegevens uit een relationele gegevensopslag, herhaalbaarheid rekening tooavoid ongewenste resultaten.</span><span class="sxs-lookup"><span data-stu-id="97925-307">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="97925-308">In Azure Data Factory, kunt u een segment handmatig opnieuw.</span><span class="sxs-lookup"><span data-stu-id="97925-308">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="97925-309">U kunt ook een beleid voor opnieuw proberen voor een gegevensset configureren zodat een segment wordt opnieuw uitgevoerd wanneer een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="97925-309">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="97925-310">Wanneer een segment opnieuw in beide gevallen wordt uitgevoerd, moet u ervoor dat dezelfde gegevens Hallo toomake wordt gelezen ongeacht hoe vaak een segment wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="97925-310">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="97925-311">Zie [Repeatable van relationele bronnen lezen](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="97925-311">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="97925-312">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="97925-312">Performance and Tuning</span></span>
<span data-ttu-id="97925-313">Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.</span><span class="sxs-lookup"><span data-stu-id="97925-313">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
