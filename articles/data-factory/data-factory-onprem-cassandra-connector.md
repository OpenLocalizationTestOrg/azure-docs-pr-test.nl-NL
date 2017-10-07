---
title: aaaMove gegevens van Cassandra gebruik Data Factory | Microsoft Docs
description: Meer informatie over hoe toomove gegevens uit een Cassandra lokale database met behulp van Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 085cc312-42ca-4f43-aa35-535b35a102d5
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 0e265d3a8439d0a2cb2a5c32e5ea8348a1617621
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-an-on-premises-cassandra-database-using-azure-data-factory"></a><span data-ttu-id="9dcb8-103">Verplaatsen van gegevens uit een on-premises Cassandra-database met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9dcb8-103">Move data from an on-premises Cassandra database using Azure Data Factory</span></span>
<span data-ttu-id="9dcb8-104">Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit Hallo in Azure Data Factory toomove gegevens uit een on-premises Cassandra-database.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises Cassandra database.</span></span> <span data-ttu-id="9dcb8-105">Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="9dcb8-106">U kunt gegevens uit een on-premises Cassandra gegevens store tooany ondersteund sink gegevensopslag kopiëren.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-106">You can copy data from an on-premises Cassandra data store tooany supported sink data store.</span></span> <span data-ttu-id="9dcb8-107">Zie voor een lijst van gegevens winkels ondersteund zoals sinks door kopieeractiviteit hello, Hallo [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="9dcb8-108">Data factory ondersteunt momenteel alleen verplaatsen van gegevens uit een data Cassandra tooother gegevensarchieven opslaan, maar niet voor het verplaatsen van gegevens uit andere winkels tooa Cassandra gegevens gegevensopslag.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-108">Data factory currently supports only moving data from a Cassandra data store tooother data stores, but not for moving data from other data stores tooa Cassandra data store.</span></span> 

## <a name="supported-versions"></a><span data-ttu-id="9dcb8-109">Ondersteunde versies</span><span class="sxs-lookup"><span data-stu-id="9dcb8-109">Supported versions</span></span>
<span data-ttu-id="9dcb8-110">Hallo Cassandra connector ondersteunt Hallo volgende versies van Cassandra: 2.X.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-110">hello Cassandra connector supports hello following versions of Cassandra: 2.X.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9dcb8-111">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9dcb8-111">Prerequisites</span></span>
<span data-ttu-id="9dcb8-112">Voor hello Azure Data Factory-service toobe kunnen tooconnect tooyour lokale Cassandra-database, moet u een Data Management Gateway installeren op Hallo dezelfde die hosts Hallo-database van de computer of op een afzonderlijke computer tooavoid concurreren voor bronnen met Hallo de database.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-112">For hello Azure Data Factory service toobe able tooconnect tooyour on-premises Cassandra database, you must install a Data Management Gateway on hello same machine that hosts hello database or on a separate machine tooavoid competing for resources with hello database.</span></span> <span data-ttu-id="9dcb8-113">Data Management Gateway is een onderdeel dat lokale gegevensbronnen toocloud services in een veilige en beheerde manier verbindt.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-113">Data Management Gateway is a component that connects on-premises data sources toocloud services in a secure and managed way.</span></span> <span data-ttu-id="9dcb8-114">Zie [Data Management Gateway](data-factory-data-management-gateway.md) voor meer informatie over Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="9dcb8-115">Zie [verplaatsen van gegevens uit de lokale toocloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor stapsgewijze instructies over het instellen van Hallo gateway een data pipeline toomove gegevens.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-115">See [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway a data pipeline toomove data.</span></span>

<span data-ttu-id="9dcb8-116">Zelfs als het Hallo-database wordt gehost in Hallo cloud, bijvoorbeeld op een virtuele machine van Azure IaaS, moet u Hallo gateway tooconnect tooa Cassandra database gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-116">You must use hello gateway tooconnect tooa Cassandra database even if hello database is hosted in hello cloud, for example, on an Azure IaaS VM.</span></span> <span data-ttu-id="9dcb8-117">Y u Hallo-gateway kan hebben op dezelfde virtuele machine die hosts Hallo database Hallo of op een afzonderlijke virtuele machine zo lang Hallo gateway kunt verbinding maken met toohello database.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-117">Y You can have hello gateway on hello same VM that hosts hello database or on a separate VM as long as hello gateway can connect toohello database.</span></span>  

<span data-ttu-id="9dcb8-118">Wanneer u Hallo-gateway installeert, installeert deze automatisch een Microsoft Cassandra ODBC-stuurprogramma gebruikt tooconnect tooCassandra database.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-118">When you install hello gateway, it automatically installs a Microsoft Cassandra ODBC driver used tooconnect tooCassandra database.</span></span> <span data-ttu-id="9dcb8-119">Dus u hoeft niet toomanually stuurprogramma installeren op de gatewaycomputer Hallo bij het kopiëren van gegevens uit Hallo Cassandra database.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-119">Therefore, you don't need toomanually install any driver on hello gateway machine when copying data from hello Cassandra database.</span></span> 

> [!NOTE]
> <span data-ttu-id="9dcb8-120">Zie [gateway problemen](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) voor tips over het oplossen van verbinding of gateway gerelateerde problemen.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-120">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="9dcb8-121">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="9dcb8-121">Getting started</span></span>
<span data-ttu-id="9dcb8-122">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens vanuit een on-premises Cassandra-gegevensopslag verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-122">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="9dcb8-123">Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-123">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="9dcb8-124">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="9dcb8-125">U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-125">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="9dcb8-126">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="9dcb8-127">Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="9dcb8-127">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="9dcb8-128">Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-128">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="9dcb8-129">Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-129">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="9dcb8-130">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="9dcb8-131">Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-131">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="9dcb8-132">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="9dcb8-133">Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens uit een on-premises Cassandra-gegevensopslag zijn [JSON-voorbeeld: gegevens kopiëren van Cassandra tooAzure Blob](#json-example-copy-data-from-cassandra-to-azure-blob) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-133">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises Cassandra data store, see [JSON example: Copy data from Cassandra tooAzure Blob](#json-example-copy-data-from-cassandra-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="9dcb8-134">Hallo volgende secties vindt u informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooa Cassandra gegevensarchief zijn:</span><span class="sxs-lookup"><span data-stu-id="9dcb8-134">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Cassandra data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="9dcb8-135">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="9dcb8-135">Linked service properties</span></span>
<span data-ttu-id="9dcb8-136">Hallo volgende tabel biedt een beschrijving voor de JSON-elementen specifieke tooCassandra gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-136">hello following table provides description for JSON elements specific tooCassandra linked service.</span></span>

| <span data-ttu-id="9dcb8-137">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="9dcb8-137">Property</span></span> | <span data-ttu-id="9dcb8-138">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9dcb8-138">Description</span></span> | <span data-ttu-id="9dcb8-139">Vereist</span><span class="sxs-lookup"><span data-stu-id="9dcb8-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9dcb8-140">type</span><span class="sxs-lookup"><span data-stu-id="9dcb8-140">type</span></span> |<span data-ttu-id="9dcb8-141">Hallo type eigenschap moet worden ingesteld op: **OnPremisesCassandra**</span><span class="sxs-lookup"><span data-stu-id="9dcb8-141">hello type property must be set to: **OnPremisesCassandra**</span></span> |<span data-ttu-id="9dcb8-142">Ja</span><span class="sxs-lookup"><span data-stu-id="9dcb8-142">Yes</span></span> |
| <span data-ttu-id="9dcb8-143">host</span><span class="sxs-lookup"><span data-stu-id="9dcb8-143">host</span></span> |<span data-ttu-id="9dcb8-144">Een of meer IP-adressen of hostnamen van Cassandra servers.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-144">One or more IP addresses or host names of Cassandra servers.</span></span><br/><br/><span data-ttu-id="9dcb8-145">Geef een door komma's gescheiden lijst met IP-adressen of namen tooconnect tooall hostservers gelijktijdig.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-145">Specify a comma-separated list of IP addresses or host names tooconnect tooall servers concurrently.</span></span> |<span data-ttu-id="9dcb8-146">Ja</span><span class="sxs-lookup"><span data-stu-id="9dcb8-146">Yes</span></span> |
| <span data-ttu-id="9dcb8-147">poort</span><span class="sxs-lookup"><span data-stu-id="9dcb8-147">port</span></span> |<span data-ttu-id="9dcb8-148">toolisten Hello TCP-poort die Hallo Cassandra server gebruikt voor clientverbindingen.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-148">hello TCP port that hello Cassandra server uses toolisten for client connections.</span></span> |<span data-ttu-id="9dcb8-149">Nee, de standaardwaarde: 9042</span><span class="sxs-lookup"><span data-stu-id="9dcb8-149">No, default value: 9042</span></span> |
| <span data-ttu-id="9dcb8-150">authenticationType</span><span class="sxs-lookup"><span data-stu-id="9dcb8-150">authenticationType</span></span> |<span data-ttu-id="9dcb8-151">Basic- of anonieme</span><span class="sxs-lookup"><span data-stu-id="9dcb8-151">Basic, or Anonymous</span></span> |<span data-ttu-id="9dcb8-152">Ja</span><span class="sxs-lookup"><span data-stu-id="9dcb8-152">Yes</span></span> |
| <span data-ttu-id="9dcb8-153">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="9dcb8-153">username</span></span> |<span data-ttu-id="9dcb8-154">Geef de gebruikersnaam voor Hallo-gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-154">Specify user name for hello user account.</span></span> |<span data-ttu-id="9dcb8-155">Ja, als authenticationType tooBasic is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-155">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="9dcb8-156">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="9dcb8-156">password</span></span> |<span data-ttu-id="9dcb8-157">Wachtwoord voor gebruikersaccount Hallo opgeven.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-157">Specify password for hello user account.</span></span> |<span data-ttu-id="9dcb8-158">Ja, als authenticationType tooBasic is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-158">Yes, if authenticationType is set tooBasic.</span></span> |
| <span data-ttu-id="9dcb8-159">gatewayName</span><span class="sxs-lookup"><span data-stu-id="9dcb8-159">gatewayName</span></span> |<span data-ttu-id="9dcb8-160">Hallo-naam van Hallo-gateway die is gebruikt tooconnect toohello lokale Cassandra-database.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-160">hello name of hello gateway that is used tooconnect toohello on-premises Cassandra database.</span></span> |<span data-ttu-id="9dcb8-161">Ja</span><span class="sxs-lookup"><span data-stu-id="9dcb8-161">Yes</span></span> |
| <span data-ttu-id="9dcb8-162">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="9dcb8-162">encryptedCredential</span></span> |<span data-ttu-id="9dcb8-163">Referentie versleuteld door Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-163">Credential encrypted by hello gateway.</span></span> |<span data-ttu-id="9dcb8-164">Nee</span><span class="sxs-lookup"><span data-stu-id="9dcb8-164">No</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="9dcb8-165">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="9dcb8-165">Dataset properties</span></span>
<span data-ttu-id="9dcb8-166">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-166">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="9dcb8-167">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).</span><span class="sxs-lookup"><span data-stu-id="9dcb8-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="9dcb8-168">Hallo **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-168">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="9dcb8-169">Hallo typeProperties sectie voor de gegevensset van het type **CassandraTable** heeft de volgende eigenschappen Hallo</span><span class="sxs-lookup"><span data-stu-id="9dcb8-169">hello typeProperties section for dataset of type **CassandraTable** has hello following properties</span></span>

| <span data-ttu-id="9dcb8-170">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="9dcb8-170">Property</span></span> | <span data-ttu-id="9dcb8-171">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9dcb8-171">Description</span></span> | <span data-ttu-id="9dcb8-172">Vereist</span><span class="sxs-lookup"><span data-stu-id="9dcb8-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9dcb8-173">met keyspace</span><span class="sxs-lookup"><span data-stu-id="9dcb8-173">keyspace</span></span> |<span data-ttu-id="9dcb8-174">Naam van Hallo keyspace of het schema in Cassandra-database.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-174">Name of hello keyspace or schema in Cassandra database.</span></span> |<span data-ttu-id="9dcb8-175">Ja (als **query** voor **CassandraSource** is niet gedefinieerd).</span><span class="sxs-lookup"><span data-stu-id="9dcb8-175">Yes (If **query** for **CassandraSource** is not defined).</span></span> |
| <span data-ttu-id="9dcb8-176">tableName</span><span class="sxs-lookup"><span data-stu-id="9dcb8-176">tableName</span></span> |<span data-ttu-id="9dcb8-177">Naam van de tabel Hallo in Cassandra-database.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-177">Name of hello table in Cassandra database.</span></span> |<span data-ttu-id="9dcb8-178">Ja (als **query** voor **CassandraSource** is niet gedefinieerd).</span><span class="sxs-lookup"><span data-stu-id="9dcb8-178">Yes (If **query** for **CassandraSource** is not defined).</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="9dcb8-179">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="9dcb8-179">Copy activity properties</span></span>
<span data-ttu-id="9dcb8-180">Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-180">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="9dcb8-181">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en -beleid zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-181">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="9dcb8-182">Terwijl de eigenschappen die beschikbaar zijn in Hallo typeProperties gedeelte van de activiteit Hallo variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-182">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="9dcb8-183">Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-183">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="9dcb8-184">Wanneer de bron is van het type **CassandraSource**, Hallo volgende eigenschappen beschikbaar zijn in de sectie typeProperties:</span><span class="sxs-lookup"><span data-stu-id="9dcb8-184">When source is of type **CassandraSource**, hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="9dcb8-185">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="9dcb8-185">Property</span></span> | <span data-ttu-id="9dcb8-186">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="9dcb8-186">Description</span></span> | <span data-ttu-id="9dcb8-187">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="9dcb8-187">Allowed values</span></span> | <span data-ttu-id="9dcb8-188">Vereist</span><span class="sxs-lookup"><span data-stu-id="9dcb8-188">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9dcb8-189">query</span><span class="sxs-lookup"><span data-stu-id="9dcb8-189">query</span></span> |<span data-ttu-id="9dcb8-190">Hallo aangepaste query tooread gegevens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-190">Use hello custom query tooread data.</span></span> |<span data-ttu-id="9dcb8-191">SQL-92 query of CQL query.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-191">SQL-92 query or CQL query.</span></span> <span data-ttu-id="9dcb8-192">Zie [CQL verwijzing](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span><span class="sxs-lookup"><span data-stu-id="9dcb8-192">See [CQL reference](https://docs.datastax.com/en/cql/3.1/cql/cql_reference/cqlReferenceTOC.html).</span></span> <br/><br/><span data-ttu-id="9dcb8-193">Wanneer u SQL-query gebruikt, geef **keyspace name.table naam** toorepresent Hallo tabel gewenste tooquery.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-193">When using SQL query, specify **keyspace name.table name** toorepresent hello table you want tooquery.</span></span> |<span data-ttu-id="9dcb8-194">Nee (als tableName en keyspace op gegevensset zijn gedefinieerd).</span><span class="sxs-lookup"><span data-stu-id="9dcb8-194">No (if tableName and keyspace on dataset are defined).</span></span> |
| <span data-ttu-id="9dcb8-195">consistencyLevel</span><span class="sxs-lookup"><span data-stu-id="9dcb8-195">consistencyLevel</span></span> |<span data-ttu-id="9dcb8-196">Hallo consistentieniveau geeft het aantal replica's tooa leesaanvraag moet reageren voordat gegevens toohello clienttoepassing wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-196">hello consistency level specifies how many replicas must respond tooa read request before returning data toohello client application.</span></span> <span data-ttu-id="9dcb8-197">Cassandra controles Hallo opgegeven aantal replica's voor gegevens toosatisfy Hallo leesaanvraag.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-197">Cassandra checks hello specified number of replicas for data toosatisfy hello read request.</span></span> |<span data-ttu-id="9dcb8-198">EEN, TWEE, DRIE, QUORUM, ALL, LOCAL_QUORUM EACH_QUORUM, LOCAL_ONE.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-198">ONE, TWO, THREE, QUORUM, ALL, LOCAL_QUORUM, EACH_QUORUM, LOCAL_ONE.</span></span> <span data-ttu-id="9dcb8-199">Zie [gegevensconsistentie configureren](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-199">See [Configuring data consistency](http://docs.datastax.com/en//cassandra/2.0/cassandra/dml/dml_config_consistency_c.html) for details.</span></span> |<span data-ttu-id="9dcb8-200">Nee.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-200">No.</span></span> <span data-ttu-id="9dcb8-201">Standaardwaarde is een.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-201">Default value is ONE.</span></span> |

## <a name="json-example-copy-data-from-cassandra-tooazure-blob"></a><span data-ttu-id="9dcb8-202">JSON-voorbeeld: gegevens kopiëren van Cassandra tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="9dcb8-202">JSON example: Copy data from Cassandra tooAzure Blob</span></span>
<span data-ttu-id="9dcb8-203">In dit voorbeeld voorbeeld JSON definities bevat dat u een pijplijn toocreate gebruiken met behulp van kunt [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="9dcb8-203">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="9dcb8-204">Er wordt weergegeven hoe toocopy gegevens uit een lokale Cassandra tooan Azure Blob Storage-database.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-204">It shows how toocopy data from an on-premises Cassandra database tooan Azure Blob Storage.</span></span> <span data-ttu-id="9dcb8-205">Gegevens kunnen echter wel gekopieerde tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-205">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9dcb8-206">Dit voorbeeld bevat JSON-fragmenten.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-206">This sample provides JSON snippets.</span></span> <span data-ttu-id="9dcb8-207">Dit omvat geen stapsgewijze instructies voor het maken van de gegevensfactory Hallo.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-207">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="9dcb8-208">Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor stapsgewijze instructies.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-208">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="9dcb8-209">Hallo voorbeeld heeft Hallo data factory-entiteiten te volgen:</span><span class="sxs-lookup"><span data-stu-id="9dcb8-209">hello sample has hello following data factory entities:</span></span>

* <span data-ttu-id="9dcb8-210">Een gekoppelde service van het type [OnPremisesCassandra](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="9dcb8-210">A linked service of type [OnPremisesCassandra](#linked-service-properties).</span></span>
* <span data-ttu-id="9dcb8-211">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="9dcb8-211">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="9dcb8-212">Invoer [gegevensset](data-factory-create-datasets.md) van het type [CassandraTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="9dcb8-212">An input [dataset](data-factory-create-datasets.md) of type [CassandraTable](#dataset-properties).</span></span>
* <span data-ttu-id="9dcb8-213">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="9dcb8-213">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="9dcb8-214">Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [CassandraSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="9dcb8-214">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [CassandraSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="9dcb8-215">**Cassandra gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="9dcb8-215">**Cassandra linked service:**</span></span>

<span data-ttu-id="9dcb8-216">In dit voorbeeld wordt Hallo **Cassandra** gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-216">This example uses hello **Cassandra** linked service.</span></span> <span data-ttu-id="9dcb8-217">Zie [Cassandra gekoppelde service](#linked-service-properties) gedeelte voor het Hallo-eigenschappen die ondersteund worden door deze gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-217">See [Cassandra linked service](#linked-service-properties) section for hello properties supported by this linked service.</span></span>  

```json
{
    "name": "CassandraLinkedService",
    "properties":
    {
        "type": "OnPremisesCassandra",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "host": "mycassandraserver",
            "port": 9042,
            "username": "user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="9dcb8-218">**Gekoppelde Azure Storage-service:**</span><span class="sxs-lookup"><span data-stu-id="9dcb8-218">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="9dcb8-219">**Cassandra invoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="9dcb8-219">**Cassandra input dataset:**</span></span>

```json
{
    "name": "CassandraInput",
    "properties": {
        "linkedServiceName": "CassandraLinkedService",
        "type": "CassandraTable",
        "typeProperties": {
            "tableName": "mytable",
            "keySpace": "mykeyspace"
        },
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

<span data-ttu-id="9dcb8-220">Instelling **externe** te**true** informeert Hallo Data Factory-service die gegevensset Hallo externe toohello data factory is en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-220">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

<span data-ttu-id="9dcb8-221">**Azure Blob-uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="9dcb8-221">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="9dcb8-222">Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="9dcb8-222">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/fromcassandra"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="9dcb8-223">**De kopieeractiviteit in een pijplijn met Cassandra bron en sink van Blob:**</span><span class="sxs-lookup"><span data-stu-id="9dcb8-223">**Copy activity in a pipeline with Cassandra source and Blob sink:**</span></span>

<span data-ttu-id="9dcb8-224">Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-224">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="9dcb8-225">Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**CassandraSource** en **sink** type is ingesteld, te**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-225">In hello pipeline JSON definition, hello **source** type is set too**CassandraSource** and **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="9dcb8-226">Zie [RelationalSource type-eigenschappen](#copy-activity-properties) voor Hallo lijst met eigenschappen die ondersteund worden door Hallo RelationalSource.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-226">See [RelationalSource type properties](#copy-activity-properties) for hello list of properties supported by hello RelationalSource.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "CassandraToAzureBlob",
            "description": "Copy from Cassandra tooan Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "CassandraInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "CassandraSource",
                    "query": "select id, firstname, lastname from mykeyspace.mytable"

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

### <a name="type-mapping-for-cassandra"></a><span data-ttu-id="9dcb8-227">Toewijzing van het type voor Cassandra</span><span class="sxs-lookup"><span data-stu-id="9dcb8-227">Type mapping for Cassandra</span></span>
| <span data-ttu-id="9dcb8-228">Type Cassandra</span><span class="sxs-lookup"><span data-stu-id="9dcb8-228">Cassandra Type</span></span> | <span data-ttu-id="9dcb8-229">.NET op basis van Type</span><span class="sxs-lookup"><span data-stu-id="9dcb8-229">.Net Based Type</span></span> |
| --- | --- |
| <span data-ttu-id="9dcb8-230">ASCII</span><span class="sxs-lookup"><span data-stu-id="9dcb8-230">ASCII</span></span> |<span data-ttu-id="9dcb8-231">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9dcb8-231">String</span></span> |
| <span data-ttu-id="9dcb8-232">BIGINT</span><span class="sxs-lookup"><span data-stu-id="9dcb8-232">BIGINT</span></span> |<span data-ttu-id="9dcb8-233">Int64</span><span class="sxs-lookup"><span data-stu-id="9dcb8-233">Int64</span></span> |
| <span data-ttu-id="9dcb8-234">BLOB</span><span class="sxs-lookup"><span data-stu-id="9dcb8-234">BLOB</span></span> |<span data-ttu-id="9dcb8-235">Byte]</span><span class="sxs-lookup"><span data-stu-id="9dcb8-235">Byte[]</span></span> |
| <span data-ttu-id="9dcb8-236">BOOLEAANSE WAARDE</span><span class="sxs-lookup"><span data-stu-id="9dcb8-236">BOOLEAN</span></span> |<span data-ttu-id="9dcb8-237">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="9dcb8-237">Boolean</span></span> |
| <span data-ttu-id="9dcb8-238">DECIMALE</span><span class="sxs-lookup"><span data-stu-id="9dcb8-238">DECIMAL</span></span> |<span data-ttu-id="9dcb8-239">Decimale</span><span class="sxs-lookup"><span data-stu-id="9dcb8-239">Decimal</span></span> |
| <span data-ttu-id="9dcb8-240">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="9dcb8-240">DOUBLE</span></span> |<span data-ttu-id="9dcb8-241">dubbele</span><span class="sxs-lookup"><span data-stu-id="9dcb8-241">Double</span></span> |
| <span data-ttu-id="9dcb8-242">FLOAT</span><span class="sxs-lookup"><span data-stu-id="9dcb8-242">FLOAT</span></span> |<span data-ttu-id="9dcb8-243">Één</span><span class="sxs-lookup"><span data-stu-id="9dcb8-243">Single</span></span> |
| <span data-ttu-id="9dcb8-244">INET</span><span class="sxs-lookup"><span data-stu-id="9dcb8-244">INET</span></span> |<span data-ttu-id="9dcb8-245">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9dcb8-245">String</span></span> |
| <span data-ttu-id="9dcb8-246">INT</span><span class="sxs-lookup"><span data-stu-id="9dcb8-246">INT</span></span> |<span data-ttu-id="9dcb8-247">Int32</span><span class="sxs-lookup"><span data-stu-id="9dcb8-247">Int32</span></span> |
| <span data-ttu-id="9dcb8-248">TEKST</span><span class="sxs-lookup"><span data-stu-id="9dcb8-248">TEXT</span></span> |<span data-ttu-id="9dcb8-249">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9dcb8-249">String</span></span> |
| <span data-ttu-id="9dcb8-250">TIJDSTEMPEL</span><span class="sxs-lookup"><span data-stu-id="9dcb8-250">TIMESTAMP</span></span> |<span data-ttu-id="9dcb8-251">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="9dcb8-251">DateTime</span></span> |
| <span data-ttu-id="9dcb8-252">TIMEUUID</span><span class="sxs-lookup"><span data-stu-id="9dcb8-252">TIMEUUID</span></span> |<span data-ttu-id="9dcb8-253">GUID</span><span class="sxs-lookup"><span data-stu-id="9dcb8-253">Guid</span></span> |
| <span data-ttu-id="9dcb8-254">UUID</span><span class="sxs-lookup"><span data-stu-id="9dcb8-254">UUID</span></span> |<span data-ttu-id="9dcb8-255">GUID</span><span class="sxs-lookup"><span data-stu-id="9dcb8-255">Guid</span></span> |
| <span data-ttu-id="9dcb8-256">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="9dcb8-256">VARCHAR</span></span> |<span data-ttu-id="9dcb8-257">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="9dcb8-257">String</span></span> |
| <span data-ttu-id="9dcb8-258">VARINT</span><span class="sxs-lookup"><span data-stu-id="9dcb8-258">VARINT</span></span> |<span data-ttu-id="9dcb8-259">Decimale</span><span class="sxs-lookup"><span data-stu-id="9dcb8-259">Decimal</span></span> |

> [!NOTE]
> <span data-ttu-id="9dcb8-260">Voor de verzameling van typen (kaart, set, lijst, enzovoort) te verwijzen[werken met Cassandra verzamelingtypen met behulp van de virtuele tabel](#work-with-collections-using-virtual-table) sectie.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-260">For collection types (map, set, list, etc.), refer too[Work with Cassandra collection types using virtual table](#work-with-collections-using-virtual-table) section.</span></span>
>
> <span data-ttu-id="9dcb8-261">Gebruiker gedefinieerde typen worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-261">User-defined types are not supported.</span></span>
>
> <span data-ttu-id="9dcb8-262">Hallo-lengte van binaire kolom en String-lengte kan niet groter zijn dan 4000.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-262">hello length of Binary Column and String Column lengths cannot be greater than 4000.</span></span>
>
>

## <a name="work-with-collections-using-virtual-table"></a><span data-ttu-id="9dcb8-263">Werken met behulp van de virtuele tabel verzamelingen</span><span class="sxs-lookup"><span data-stu-id="9dcb8-263">Work with collections using virtual table</span></span>
<span data-ttu-id="9dcb8-264">Azure Data Factory maakt gebruik van een ingebouwde ODBC-stuurprogramma tooconnect tooand gegevens kopiëren van de database Cassandra.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-264">Azure Data Factory uses a built-in ODBC driver tooconnect tooand copy data from your Cassandra database.</span></span> <span data-ttu-id="9dcb8-265">Voor verzamelingtypen met inbegrip van de kaart, de verzameling en de lijst, renormalizes Hallo stuurprogramma Hallo gegevens in de bijbehorende virtuele tabellen.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-265">For collection types including map, set and list, hello driver renormalizes hello data into corresponding virtual tables.</span></span> <span data-ttu-id="9dcb8-266">In het bijzonder als een tabel bevat de verzameling kolommen, genereert Hallo stuurprogramma Hallo virtuele tabellen te volgen:</span><span class="sxs-lookup"><span data-stu-id="9dcb8-266">Specifically, if a table contains any collection columns, hello driver generates hello following virtual tables:</span></span>

* <span data-ttu-id="9dcb8-267">Een **basistabel**, die bevat Hallo dezelfde gegevens als Hallo echte tabel, met uitzondering Hallo verzameling kolommen.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-267">A **base table**, which contains hello same data as hello real table except for hello collection columns.</span></span> <span data-ttu-id="9dcb8-268">de basistabel Hallo gebruikt Hallo dezelfde naam als Hallo echte tabel die wordt vertegenwoordigd.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-268">hello base table uses hello same name as hello real table that it represents.</span></span>
* <span data-ttu-id="9dcb8-269">Een **virtuele tabel** voor elke kolom collectie die geneste Hallo gegevens wordt uitgebreid.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-269">A **virtual table** for each collection column, which expands hello nested data.</span></span> <span data-ttu-id="9dcb8-270">Hallo virtuele tabellen waarbij de verzamelingen zijn benoemde Hallo-naam van Hallo echte tabel, een scheidingsteken '*vt*' en naam van de Hallo van Hallo-kolom.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-270">hello virtual tables that represent collections are named using hello name of hello real table, a separator “*vt*” and hello name of hello column.</span></span>

<span data-ttu-id="9dcb8-271">Virtuele tabellen verwijzen toohello-gegevens in de echte tabel hello, waardoor Hallo stuurprogramma tooaccess Hallo gedenormaliseerd gegevens.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-271">Virtual tables refer toohello data in hello real table, enabling hello driver tooaccess hello denormalized data.</span></span> <span data-ttu-id="9dcb8-272">Zie het voorbeeld gedeelte voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-272">See Example section for details.</span></span> <span data-ttu-id="9dcb8-273">Hallo-inhoud van Cassandra verzamelingen kunt u door het uitvoeren van query's en het toevoegen aan virtuele tabellen Hallo openen.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-273">You can access hello content of Cassandra collections by querying and joining hello virtual tables.</span></span>

<span data-ttu-id="9dcb8-274">U kunt Hallo [Wizard kopiëren](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively weergeven Hallo lijst met tabellen in Cassandra database, inclusief Hallo virtuele tabellen en een voorbeeld van gegevens binnen Hallo.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-274">You can use hello [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively view hello list of tables in Cassandra database including hello virtual tables, and preview hello data inside.</span></span> <span data-ttu-id="9dcb8-275">U kunt ook maakt u een query in de Wizard kopiëren Hallo en toosee Hallo resultaat valideren.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-275">You can also construct a query in hello Copy Wizard and validate toosee hello result.</span></span>

### <a name="example"></a><span data-ttu-id="9dcb8-276">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="9dcb8-276">Example</span></span>
<span data-ttu-id="9dcb8-277">Hallo is volgende 'ExampleTable' bijvoorbeeld een databasetabel Cassandra die een geheel getal primaire-sleutelkolom met de naam 'pk_int', een tekstkolom benoemde waarde, een lijstkolom, een kaart kolom en een set-kolom (met de naam 'StringSet') bevat.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-277">For example, hello following “ExampleTable” is a Cassandra database table that contains an integer primary key column named “pk_int”, a text column named value, a list column, a map column, and a set column (named “StringSet”).</span></span>

| <span data-ttu-id="9dcb8-278">pk_int</span><span class="sxs-lookup"><span data-stu-id="9dcb8-278">pk_int</span></span> | <span data-ttu-id="9dcb8-279">Waarde</span><span class="sxs-lookup"><span data-stu-id="9dcb8-279">Value</span></span> | <span data-ttu-id="9dcb8-280">Lijst</span><span class="sxs-lookup"><span data-stu-id="9dcb8-280">List</span></span> | <span data-ttu-id="9dcb8-281">Kaart</span><span class="sxs-lookup"><span data-stu-id="9dcb8-281">Map</span></span> | <span data-ttu-id="9dcb8-282">StringSet</span><span class="sxs-lookup"><span data-stu-id="9dcb8-282">StringSet</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="9dcb8-283">1</span><span class="sxs-lookup"><span data-stu-id="9dcb8-283">1</span></span> |<span data-ttu-id="9dcb8-284">'Voorbeeldwaarde 1'</span><span class="sxs-lookup"><span data-stu-id="9dcb8-284">"sample value 1"</span></span> |<span data-ttu-id="9dcb8-285">["1", "2", "3"]</span><span class="sxs-lookup"><span data-stu-id="9dcb8-285">["1", "2", "3"]</span></span> |<span data-ttu-id="9dcb8-286">{"S1": "a", "S2": "b"}</span><span class="sxs-lookup"><span data-stu-id="9dcb8-286">{"S1": "a", "S2": "b"}</span></span> |<span data-ttu-id="9dcb8-287">{"A", "B", "C"}</span><span class="sxs-lookup"><span data-stu-id="9dcb8-287">{"A", "B", "C"}</span></span> |
| <span data-ttu-id="9dcb8-288">3</span><span class="sxs-lookup"><span data-stu-id="9dcb8-288">3</span></span> |<span data-ttu-id="9dcb8-289">"Voorbeeldwaarde 3"</span><span class="sxs-lookup"><span data-stu-id="9dcb8-289">"sample value 3"</span></span> |<span data-ttu-id="9dcb8-290">["100", "101", "102", "105"]</span><span class="sxs-lookup"><span data-stu-id="9dcb8-290">["100", "101", "102", "105"]</span></span> |<span data-ttu-id="9dcb8-291">{"S1": "t"}</span><span class="sxs-lookup"><span data-stu-id="9dcb8-291">{"S1": "t"}</span></span> |<span data-ttu-id="9dcb8-292">{"A", "E"}</span><span class="sxs-lookup"><span data-stu-id="9dcb8-292">{"A", "E"}</span></span> |

<span data-ttu-id="9dcb8-293">Hallo stuurprogramma genereert meerdere virtuele tabellen toorepresent deze één tabel.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-293">hello driver would generate multiple virtual tables toorepresent this single table.</span></span> <span data-ttu-id="9dcb8-294">Hallo refererende-sleutelkolommen in virtuele tabellen Hallo Hallo primaire-sleutelkolommen in Hallo echte tabel verwijzen naar en geven aan welke real tabelrij rij Hallo virtuele tabel komt overeen met.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-294">hello foreign key columns in hello virtual tables reference hello primary key columns in hello real table, and indicate which real table row hello virtual table row corresponds to.</span></span>

<span data-ttu-id="9dcb8-295">de eerste virtuele tabel Hallo is Hallo basistabel met de naam 'ExampleTable' wordt weergegeven in de volgende tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-295">hello first virtual table is hello base table named “ExampleTable” is shown in hello following table.</span></span> <span data-ttu-id="9dcb8-296">de basistabel Hallo Hallo bevat dezelfde gegevens als de oorspronkelijke databasetabel hello, met uitzondering van Hallo verzamelingen, die worden weggelaten uit deze tabel en uitgevouwen in andere virtuele tabellen.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-296">hello base table contains hello same data as hello original database table except for hello collections, which are omitted from this table and expanded in other virtual tables.</span></span>

| <span data-ttu-id="9dcb8-297">pk_int</span><span class="sxs-lookup"><span data-stu-id="9dcb8-297">pk_int</span></span> | <span data-ttu-id="9dcb8-298">Waarde</span><span class="sxs-lookup"><span data-stu-id="9dcb8-298">Value</span></span> |
| --- | --- |
| <span data-ttu-id="9dcb8-299">1</span><span class="sxs-lookup"><span data-stu-id="9dcb8-299">1</span></span> |<span data-ttu-id="9dcb8-300">'Voorbeeldwaarde 1'</span><span class="sxs-lookup"><span data-stu-id="9dcb8-300">"sample value 1"</span></span> |
| <span data-ttu-id="9dcb8-301">3</span><span class="sxs-lookup"><span data-stu-id="9dcb8-301">3</span></span> |<span data-ttu-id="9dcb8-302">"Voorbeeldwaarde 3"</span><span class="sxs-lookup"><span data-stu-id="9dcb8-302">"sample value 3"</span></span> |

<span data-ttu-id="9dcb8-303">Hallo bevatten volgende tabellen Hallo virtuele tabellen die gegevens uit de lijst, toewijzing en StringSet kolommen Hallo Hallo renormalize.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-303">hello following tables show hello virtual tables that renormalize hello data from hello List, Map, and StringSet columns.</span></span> <span data-ttu-id="9dcb8-304">Hallo kolommen met namen die met '_index' of '_key eindigen' hello positie van gegevens binnen de oorspronkelijke lijst Hallo of kaart Hallo aangeven.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-304">hello columns with names that end with “_index” or “_key” indicate hello position of hello data within hello original list or map.</span></span> <span data-ttu-id="9dcb8-305">Hallo kolommen met namen die met '_Waarde eindigen' bevatten Hallo uitgevouwen gegevens uit de verzameling Hallo.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-305">hello columns with names that end with “_value” contain hello expanded data from hello collection.</span></span>

#### <a name="table-exampletablevtlist"></a><span data-ttu-id="9dcb8-306">Tabel 'ExampleTable_vt_List':</span><span class="sxs-lookup"><span data-stu-id="9dcb8-306">Table “ExampleTable_vt_List”:</span></span>
| <span data-ttu-id="9dcb8-307">pk_int</span><span class="sxs-lookup"><span data-stu-id="9dcb8-307">pk_int</span></span> | <span data-ttu-id="9dcb8-308">List_index</span><span class="sxs-lookup"><span data-stu-id="9dcb8-308">List_index</span></span> | <span data-ttu-id="9dcb8-309">List_value</span><span class="sxs-lookup"><span data-stu-id="9dcb8-309">List_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9dcb8-310">1</span><span class="sxs-lookup"><span data-stu-id="9dcb8-310">1</span></span> |<span data-ttu-id="9dcb8-311">0</span><span class="sxs-lookup"><span data-stu-id="9dcb8-311">0</span></span> |<span data-ttu-id="9dcb8-312">1</span><span class="sxs-lookup"><span data-stu-id="9dcb8-312">1</span></span> |
| <span data-ttu-id="9dcb8-313">1</span><span class="sxs-lookup"><span data-stu-id="9dcb8-313">1</span></span> |<span data-ttu-id="9dcb8-314">1</span><span class="sxs-lookup"><span data-stu-id="9dcb8-314">1</span></span> |<span data-ttu-id="9dcb8-315">2</span><span class="sxs-lookup"><span data-stu-id="9dcb8-315">2</span></span> |
| <span data-ttu-id="9dcb8-316">1</span><span class="sxs-lookup"><span data-stu-id="9dcb8-316">1</span></span> |<span data-ttu-id="9dcb8-317">2</span><span class="sxs-lookup"><span data-stu-id="9dcb8-317">2</span></span> |<span data-ttu-id="9dcb8-318">3</span><span class="sxs-lookup"><span data-stu-id="9dcb8-318">3</span></span> |
| <span data-ttu-id="9dcb8-319">3</span><span class="sxs-lookup"><span data-stu-id="9dcb8-319">3</span></span> |<span data-ttu-id="9dcb8-320">0</span><span class="sxs-lookup"><span data-stu-id="9dcb8-320">0</span></span> |<span data-ttu-id="9dcb8-321">100</span><span class="sxs-lookup"><span data-stu-id="9dcb8-321">100</span></span> |
| <span data-ttu-id="9dcb8-322">3</span><span class="sxs-lookup"><span data-stu-id="9dcb8-322">3</span></span> |<span data-ttu-id="9dcb8-323">1</span><span class="sxs-lookup"><span data-stu-id="9dcb8-323">1</span></span> |<span data-ttu-id="9dcb8-324">101</span><span class="sxs-lookup"><span data-stu-id="9dcb8-324">101</span></span> |
| <span data-ttu-id="9dcb8-325">3</span><span class="sxs-lookup"><span data-stu-id="9dcb8-325">3</span></span> |<span data-ttu-id="9dcb8-326">2</span><span class="sxs-lookup"><span data-stu-id="9dcb8-326">2</span></span> |<span data-ttu-id="9dcb8-327">102</span><span class="sxs-lookup"><span data-stu-id="9dcb8-327">102</span></span> |
| <span data-ttu-id="9dcb8-328">3</span><span class="sxs-lookup"><span data-stu-id="9dcb8-328">3</span></span> |<span data-ttu-id="9dcb8-329">3</span><span class="sxs-lookup"><span data-stu-id="9dcb8-329">3</span></span> |<span data-ttu-id="9dcb8-330">103</span><span class="sxs-lookup"><span data-stu-id="9dcb8-330">103</span></span> |

#### <a name="table-exampletablevtmap"></a><span data-ttu-id="9dcb8-331">Tabel 'ExampleTable_vt_Map':</span><span class="sxs-lookup"><span data-stu-id="9dcb8-331">Table “ExampleTable_vt_Map”:</span></span>
| <span data-ttu-id="9dcb8-332">pk_int</span><span class="sxs-lookup"><span data-stu-id="9dcb8-332">pk_int</span></span> | <span data-ttu-id="9dcb8-333">Map_key</span><span class="sxs-lookup"><span data-stu-id="9dcb8-333">Map_key</span></span> | <span data-ttu-id="9dcb8-334">Map_value</span><span class="sxs-lookup"><span data-stu-id="9dcb8-334">Map_value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9dcb8-335">1</span><span class="sxs-lookup"><span data-stu-id="9dcb8-335">1</span></span> |<span data-ttu-id="9dcb8-336">S1</span><span class="sxs-lookup"><span data-stu-id="9dcb8-336">S1</span></span> |<span data-ttu-id="9dcb8-337">A</span><span class="sxs-lookup"><span data-stu-id="9dcb8-337">A</span></span> |
| <span data-ttu-id="9dcb8-338">1</span><span class="sxs-lookup"><span data-stu-id="9dcb8-338">1</span></span> |<span data-ttu-id="9dcb8-339">S2</span><span class="sxs-lookup"><span data-stu-id="9dcb8-339">S2</span></span> |<span data-ttu-id="9dcb8-340">B</span><span class="sxs-lookup"><span data-stu-id="9dcb8-340">b</span></span> |
| <span data-ttu-id="9dcb8-341">3</span><span class="sxs-lookup"><span data-stu-id="9dcb8-341">3</span></span> |<span data-ttu-id="9dcb8-342">S1</span><span class="sxs-lookup"><span data-stu-id="9dcb8-342">S1</span></span> |<span data-ttu-id="9dcb8-343">T</span><span class="sxs-lookup"><span data-stu-id="9dcb8-343">t</span></span> |

#### <a name="table-exampletablevtstringset"></a><span data-ttu-id="9dcb8-344">Tabel 'ExampleTable_vt_StringSet':</span><span class="sxs-lookup"><span data-stu-id="9dcb8-344">Table “ExampleTable_vt_StringSet”:</span></span>
| <span data-ttu-id="9dcb8-345">pk_int</span><span class="sxs-lookup"><span data-stu-id="9dcb8-345">pk_int</span></span> | <span data-ttu-id="9dcb8-346">StringSet_value</span><span class="sxs-lookup"><span data-stu-id="9dcb8-346">StringSet_value</span></span> |
| --- | --- |
| <span data-ttu-id="9dcb8-347">1</span><span class="sxs-lookup"><span data-stu-id="9dcb8-347">1</span></span> |<span data-ttu-id="9dcb8-348">A</span><span class="sxs-lookup"><span data-stu-id="9dcb8-348">A</span></span> |
| <span data-ttu-id="9dcb8-349">1</span><span class="sxs-lookup"><span data-stu-id="9dcb8-349">1</span></span> |<span data-ttu-id="9dcb8-350">B</span><span class="sxs-lookup"><span data-stu-id="9dcb8-350">B</span></span> |
| <span data-ttu-id="9dcb8-351">1</span><span class="sxs-lookup"><span data-stu-id="9dcb8-351">1</span></span> |<span data-ttu-id="9dcb8-352">C</span><span class="sxs-lookup"><span data-stu-id="9dcb8-352">C</span></span> |
| <span data-ttu-id="9dcb8-353">3</span><span class="sxs-lookup"><span data-stu-id="9dcb8-353">3</span></span> |<span data-ttu-id="9dcb8-354">A</span><span class="sxs-lookup"><span data-stu-id="9dcb8-354">A</span></span> |
| <span data-ttu-id="9dcb8-355">3</span><span class="sxs-lookup"><span data-stu-id="9dcb8-355">3</span></span> |<span data-ttu-id="9dcb8-356">E</span><span class="sxs-lookup"><span data-stu-id="9dcb8-356">E</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="9dcb8-357">Bronkolommen toosink toewijzen</span><span class="sxs-lookup"><span data-stu-id="9dcb8-357">Map source toosink columns</span></span>
<span data-ttu-id="9dcb8-358">Zie toolearn over het toewijzen van kolommen in bron gegevensset toocolumns in sink-gegevensset [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="9dcb8-358">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="9dcb8-359">Herhaalbare leesbewerking van relationele bronnen</span><span class="sxs-lookup"><span data-stu-id="9dcb8-359">Repeatable read from relational sources</span></span>
<span data-ttu-id="9dcb8-360">Houd bij het kopiëren van gegevens uit een relationele gegevensopslag, herhaalbaarheid rekening tooavoid ongewenste resultaten.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-360">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="9dcb8-361">In Azure Data Factory, kunt u een segment handmatig opnieuw.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-361">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="9dcb8-362">U kunt ook een beleid voor opnieuw proberen voor een gegevensset configureren zodat een segment wordt opnieuw uitgevoerd wanneer een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-362">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="9dcb8-363">Wanneer een segment opnieuw in beide gevallen wordt uitgevoerd, moet u ervoor dat dezelfde gegevens Hallo toomake wordt gelezen ongeacht hoe vaak een segment wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-363">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="9dcb8-364">Zie [Repeatable van relationele bronnen lezen](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="9dcb8-364">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="9dcb8-365">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="9dcb8-365">Performance and Tuning</span></span>
<span data-ttu-id="9dcb8-366">Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.</span><span class="sxs-lookup"><span data-stu-id="9dcb8-366">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
