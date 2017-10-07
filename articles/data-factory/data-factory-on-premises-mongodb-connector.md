---
title: aaaMove gegevens van MongoDB gebruik Data Factory | Microsoft Docs
description: Meer informatie over hoe de gegevens toomove van MongoDB-database met behulp van Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 10ca7d9a-7715-4446-bf59-2d2876584550
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: jingwang
ms.openlocfilehash: 154e85712f27b978976c7499c43dde9429f124c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-mongodb-using-azure-data-factory"></a><span data-ttu-id="13b13-103">Verplaatsen van gegevens van MongoDB met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="13b13-103">Move data From MongoDB using Azure Data Factory</span></span>
<span data-ttu-id="13b13-104">Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit Hallo in Azure Data Factory toomove gegevens uit een on-premises MongoDB-database.</span><span class="sxs-lookup"><span data-stu-id="13b13-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises MongoDB database.</span></span> <span data-ttu-id="13b13-105">Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.</span><span class="sxs-lookup"><span data-stu-id="13b13-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="13b13-106">U kunt gegevens uit een on-premises MongoDB gegevens store tooany ondersteund sink gegevensopslag kopiëren.</span><span class="sxs-lookup"><span data-stu-id="13b13-106">You can copy data from an on-premises MongoDB data store tooany supported sink data store.</span></span> <span data-ttu-id="13b13-107">Zie voor een lijst van gegevens winkels ondersteund zoals sinks door kopieeractiviteit hello, Hallo [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel.</span><span class="sxs-lookup"><span data-stu-id="13b13-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="13b13-108">Data factory ondersteunt momenteel alleen verplaatsen van gegevens uit een data MongoDB tooother gegevensarchieven opslaan, maar niet voor het verplaatsen van gegevens uit andere gegevens winkels tooan MongoDB-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="13b13-108">Data factory currently supports only moving data from a MongoDB data store tooother data stores, but not for moving data from other data stores tooan MongoDB datastore.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="13b13-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="13b13-109">Prerequisites</span></span>
<span data-ttu-id="13b13-110">Voor hello Azure Data Factory-service toobe kunnen tooconnect tooyour lokale MongoDB-database, moet u de volgende onderdelen Hallo installeren:</span><span class="sxs-lookup"><span data-stu-id="13b13-110">For hello Azure Data Factory service toobe able tooconnect tooyour on-premises MongoDB database, you must install hello following components:</span></span>

- <span data-ttu-id="13b13-111">Ondersteunde MongoDB-versies zijn: 2.4, 2.6, 3.0 en 3.2.</span><span class="sxs-lookup"><span data-stu-id="13b13-111">Supported MongoDB versions are:  2.4, 2.6, 3.0, and 3.2.</span></span>
- <span data-ttu-id="13b13-112">Data Management Gateway op dezelfde machine Hallo die hosts Hallo-database of op een afzonderlijke computer tooavoid concurrentie voor resources met Hallo-database.</span><span class="sxs-lookup"><span data-stu-id="13b13-112">Data Management Gateway on hello same machine that hosts hello database or on a separate machine tooavoid competing for resources with hello database.</span></span> <span data-ttu-id="13b13-113">Data Management Gateway is een software die is verbonden lokale gegevensbronnen toocloud services op een manier veilig en beheerd.</span><span class="sxs-lookup"><span data-stu-id="13b13-113">Data Management Gateway is a software that connects on-premises data sources toocloud services in a secure and managed way.</span></span> <span data-ttu-id="13b13-114">Zie [Data Management Gateway](data-factory-data-management-gateway.md) voor meer informatie over Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="13b13-114">See [Data Management Gateway](data-factory-data-management-gateway.md) article for details about Data Management Gateway.</span></span> <span data-ttu-id="13b13-115">Zie [verplaatsen van gegevens uit de lokale toocloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor stapsgewijze instructies over het instellen van Hallo gateway een data pipeline toomove gegevens.</span><span class="sxs-lookup"><span data-stu-id="13b13-115">See [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway a data pipeline toomove data.</span></span>

    <span data-ttu-id="13b13-116">Wanneer u Hallo-gateway installeert, installeert deze automatisch een tooMongoDB tooconnect van Microsoft MongoDB ODBC-stuurprogramma die wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="13b13-116">When you install hello gateway, it automatically installs a Microsoft MongoDB ODBC driver used tooconnect tooMongoDB.</span></span>

    > [!NOTE]
    > <span data-ttu-id="13b13-117">U moet toouse Hallo gateway tooconnect tooMongoDB, zelfs als deze wordt gehost in Azure IaaS VM's.</span><span class="sxs-lookup"><span data-stu-id="13b13-117">You need toouse hello gateway tooconnect tooMongoDB even if it is hosted in Azure IaaS VMs.</span></span> <span data-ttu-id="13b13-118">Als u tooconnect tooan exemplaar van MongoDB gehost in de cloud probeert, kunt u ook Hallo gatewayexemplaar installeren in Hallo IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="13b13-118">If you are trying tooconnect tooan instance of MongoDB hosted in cloud, you can also install hello gateway instance in hello IaaS VM.</span></span>

## <a name="getting-started"></a><span data-ttu-id="13b13-119">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="13b13-119">Getting started</span></span>
<span data-ttu-id="13b13-120">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens vanuit een on-premises MongoDB-gegevensopslag verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="13b13-120">You can create a pipeline with a copy activity that moves data from an on-premises MongoDB data store by using different tools/APIs.</span></span>

<span data-ttu-id="13b13-121">Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="13b13-121">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="13b13-122">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="13b13-122">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="13b13-123">U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="13b13-123">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="13b13-124">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="13b13-124">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="13b13-125">Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="13b13-125">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="13b13-126">Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="13b13-126">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="13b13-127">Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="13b13-127">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="13b13-128">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="13b13-128">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="13b13-129">Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="13b13-129">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="13b13-130">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="13b13-130">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="13b13-131">Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens uit een on-premises MongoDB-gegevensopslag zijn [JSON-voorbeeld: gegevens kopiëren van MongoDB tooAzure Blob](#json-example-copy-data-from-mongodb-to-azure-blob) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="13b13-131">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises MongoDB data store, see [JSON example: Copy data from MongoDB tooAzure Blob](#json-example-copy-data-from-mongodb-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="13b13-132">Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikte toodefine Data Factory-entiteiten specifieke tooMongoDB bron:</span><span class="sxs-lookup"><span data-stu-id="13b13-132">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooMongoDB source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="13b13-133">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="13b13-133">Linked service properties</span></span>
<span data-ttu-id="13b13-134">Hallo volgende tabel bevat de beschrijving voor JSON-elementen die specifiek te**OnPremisesMongoDB** gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="13b13-134">hello following table provides description for JSON elements specific too**OnPremisesMongoDB** linked service.</span></span>

| <span data-ttu-id="13b13-135">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="13b13-135">Property</span></span> | <span data-ttu-id="13b13-136">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="13b13-136">Description</span></span> | <span data-ttu-id="13b13-137">Vereist</span><span class="sxs-lookup"><span data-stu-id="13b13-137">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="13b13-138">type</span><span class="sxs-lookup"><span data-stu-id="13b13-138">type</span></span> |<span data-ttu-id="13b13-139">Hallo type eigenschap moet worden ingesteld op: **OnPremisesMongoDb**</span><span class="sxs-lookup"><span data-stu-id="13b13-139">hello type property must be set to: **OnPremisesMongoDb**</span></span> |<span data-ttu-id="13b13-140">Ja</span><span class="sxs-lookup"><span data-stu-id="13b13-140">Yes</span></span> |
| <span data-ttu-id="13b13-141">server</span><span class="sxs-lookup"><span data-stu-id="13b13-141">server</span></span> |<span data-ttu-id="13b13-142">IP-adres of de hostnaam de naam van Hallo MongoDB-server.</span><span class="sxs-lookup"><span data-stu-id="13b13-142">IP address or host name of hello MongoDB server.</span></span> |<span data-ttu-id="13b13-143">Ja</span><span class="sxs-lookup"><span data-stu-id="13b13-143">Yes</span></span> |
| <span data-ttu-id="13b13-144">poort</span><span class="sxs-lookup"><span data-stu-id="13b13-144">port</span></span> |<span data-ttu-id="13b13-145">Toolisten TCP-poort die Hallo MongoDB-server gebruikt voor clientverbindingen.</span><span class="sxs-lookup"><span data-stu-id="13b13-145">TCP port that hello MongoDB server uses toolisten for client connections.</span></span> |<span data-ttu-id="13b13-146">Optionele standaardwaarde: 27017</span><span class="sxs-lookup"><span data-stu-id="13b13-146">Optional, default value: 27017</span></span> |
| <span data-ttu-id="13b13-147">authenticationType</span><span class="sxs-lookup"><span data-stu-id="13b13-147">authenticationType</span></span> |<span data-ttu-id="13b13-148">Basic of anonieme.</span><span class="sxs-lookup"><span data-stu-id="13b13-148">Basic, or Anonymous.</span></span> |<span data-ttu-id="13b13-149">Ja</span><span class="sxs-lookup"><span data-stu-id="13b13-149">Yes</span></span> |
| <span data-ttu-id="13b13-150">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="13b13-150">username</span></span> |<span data-ttu-id="13b13-151">Gebruiker account tooaccess MongoDB.</span><span class="sxs-lookup"><span data-stu-id="13b13-151">User account tooaccess MongoDB.</span></span> |<span data-ttu-id="13b13-152">Ja (als u basisverificatie wordt gebruikt).</span><span class="sxs-lookup"><span data-stu-id="13b13-152">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="13b13-153">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="13b13-153">password</span></span> |<span data-ttu-id="13b13-154">Wachtwoord voor gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="13b13-154">Password for hello user.</span></span> |<span data-ttu-id="13b13-155">Ja (als u basisverificatie wordt gebruikt).</span><span class="sxs-lookup"><span data-stu-id="13b13-155">Yes (if basic authentication is used).</span></span> |
| <span data-ttu-id="13b13-156">authSource</span><span class="sxs-lookup"><span data-stu-id="13b13-156">authSource</span></span> |<span data-ttu-id="13b13-157">Naam van Hallo MongoDB-database dat u wilt dat toouse toocheck uw referenties voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="13b13-157">Name of hello MongoDB database that you want toouse toocheck your credentials for authentication.</span></span> |<span data-ttu-id="13b13-158">Optioneel (als basisverificatie wordt gebruikt).</span><span class="sxs-lookup"><span data-stu-id="13b13-158">Optional (if basic authentication is used).</span></span> <span data-ttu-id="13b13-159">Standaard: maakt gebruik van Hallo-beheerdersaccount en Hallo database die is opgegeven met de eigenschap databaseName.</span><span class="sxs-lookup"><span data-stu-id="13b13-159">default: uses hello admin account and hello database specified using databaseName property.</span></span> |
| <span data-ttu-id="13b13-160">DatabaseName</span><span class="sxs-lookup"><span data-stu-id="13b13-160">databaseName</span></span> |<span data-ttu-id="13b13-161">Naam van Hallo MongoDB-database die u tooaccess wilt.</span><span class="sxs-lookup"><span data-stu-id="13b13-161">Name of hello MongoDB database that you want tooaccess.</span></span> |<span data-ttu-id="13b13-162">Ja</span><span class="sxs-lookup"><span data-stu-id="13b13-162">Yes</span></span> |
| <span data-ttu-id="13b13-163">gatewayName</span><span class="sxs-lookup"><span data-stu-id="13b13-163">gatewayName</span></span> |<span data-ttu-id="13b13-164">Naam van het Hallo-gateway die toegang heeft tot Hallo-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="13b13-164">Name of hello gateway that accesses hello data store.</span></span> |<span data-ttu-id="13b13-165">Ja</span><span class="sxs-lookup"><span data-stu-id="13b13-165">Yes</span></span> |
| <span data-ttu-id="13b13-166">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="13b13-166">encryptedCredential</span></span> |<span data-ttu-id="13b13-167">Referentie versleuteld door de gateway.</span><span class="sxs-lookup"><span data-stu-id="13b13-167">Credential encrypted by gateway.</span></span> |<span data-ttu-id="13b13-168">Optioneel</span><span class="sxs-lookup"><span data-stu-id="13b13-168">Optional</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="13b13-169">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="13b13-169">Dataset properties</span></span>
<span data-ttu-id="13b13-170">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="13b13-170">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="13b13-171">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).</span><span class="sxs-lookup"><span data-stu-id="13b13-171">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="13b13-172">Hallo **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="13b13-172">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="13b13-173">Hallo typeProperties sectie voor de gegevensset van het type **MongoDbCollection** heeft Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="13b13-173">hello typeProperties section for dataset of type **MongoDbCollection** has hello following properties:</span></span>

| <span data-ttu-id="13b13-174">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="13b13-174">Property</span></span> | <span data-ttu-id="13b13-175">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="13b13-175">Description</span></span> | <span data-ttu-id="13b13-176">Vereist</span><span class="sxs-lookup"><span data-stu-id="13b13-176">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="13b13-177">CollectionName</span><span class="sxs-lookup"><span data-stu-id="13b13-177">collectionName</span></span> |<span data-ttu-id="13b13-178">Naam van de verzameling Hallo in MongoDB-database.</span><span class="sxs-lookup"><span data-stu-id="13b13-178">Name of hello collection in MongoDB database.</span></span> |<span data-ttu-id="13b13-179">Ja</span><span class="sxs-lookup"><span data-stu-id="13b13-179">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="13b13-180">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="13b13-180">Copy activity properties</span></span>
<span data-ttu-id="13b13-181">Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="13b13-181">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="13b13-182">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en -beleid zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="13b13-182">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="13b13-183">Eigenschappen die beschikbaar zijn in Hallo **typeProperties** sectie Hallo-activiteit op Hallo daarentegen variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="13b13-183">Properties available in hello **typeProperties** section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="13b13-184">Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="13b13-184">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="13b13-185">Wanneer Hallo-bron is van het type **MongoDbSource** Hallo volgende eigenschappen beschikbaar zijn in de sectie typeProperties:</span><span class="sxs-lookup"><span data-stu-id="13b13-185">When hello source is of type **MongoDbSource** hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="13b13-186">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="13b13-186">Property</span></span> | <span data-ttu-id="13b13-187">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="13b13-187">Description</span></span> | <span data-ttu-id="13b13-188">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="13b13-188">Allowed values</span></span> | <span data-ttu-id="13b13-189">Vereist</span><span class="sxs-lookup"><span data-stu-id="13b13-189">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="13b13-190">query</span><span class="sxs-lookup"><span data-stu-id="13b13-190">query</span></span> |<span data-ttu-id="13b13-191">Hallo aangepaste query tooread gegevens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="13b13-191">Use hello custom query tooread data.</span></span> |<span data-ttu-id="13b13-192">SQL-92 queryreeks.</span><span class="sxs-lookup"><span data-stu-id="13b13-192">SQL-92 query string.</span></span> <span data-ttu-id="13b13-193">Bijvoorbeeld: Selecteer * from MijnTabel.</span><span class="sxs-lookup"><span data-stu-id="13b13-193">For example: select * from MyTable.</span></span> |<span data-ttu-id="13b13-194">Nee (als **collectionName** van **gegevensset** is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="13b13-194">No (if **collectionName** of **dataset** is specified)</span></span> |



## <a name="json-example-copy-data-from-mongodb-tooazure-blob"></a><span data-ttu-id="13b13-195">JSON-voorbeeld: gegevens kopiëren van MongoDB tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="13b13-195">JSON example: Copy data from MongoDB tooAzure Blob</span></span>
<span data-ttu-id="13b13-196">In dit voorbeeld voorbeeld JSON definities bevat dat u een pijplijn toocreate gebruiken met behulp van kunt [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="13b13-196">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="13b13-197">Er wordt weergegeven hoe toocopy gegevens uit een lokale MongoDB tooan Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="13b13-197">It shows how toocopy data from an on-premises MongoDB tooan Azure Blob Storage.</span></span> <span data-ttu-id="13b13-198">Gegevens kunnen echter wel gekopieerde tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="13b13-198">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="13b13-199">Hallo voorbeeld heeft Hallo data factory-entiteiten te volgen:</span><span class="sxs-lookup"><span data-stu-id="13b13-199">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="13b13-200">Een gekoppelde service van het type [OnPremisesMongoDb](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="13b13-200">A linked service of type [OnPremisesMongoDb](#linked-service-properties).</span></span>
2. <span data-ttu-id="13b13-201">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="13b13-201">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="13b13-202">Invoer [gegevensset](data-factory-create-datasets.md) van het type [MongoDbCollection](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="13b13-202">An input [dataset](data-factory-create-datasets.md) of type [MongoDbCollection](#dataset-properties).</span></span>
4. <span data-ttu-id="13b13-203">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="13b13-203">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="13b13-204">Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [MongoDbSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="13b13-204">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [MongoDbSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="13b13-205">Hallo voorbeeld kopieert gegevens van de resultaten van een query in de MongoDB-database tooa blob elk uur.</span><span class="sxs-lookup"><span data-stu-id="13b13-205">hello sample copies data from a query result in MongoDB database tooa blob every hour.</span></span> <span data-ttu-id="13b13-206">Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="13b13-206">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="13b13-207">Instellen als eerste stap Hallo data management gateway volgens de instructies in Hallo Hallo [Data Management Gateway](data-factory-data-management-gateway.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="13b13-207">As a first step, setup hello data management gateway as per hello instructions in hello [Data Management Gateway](data-factory-data-management-gateway.md) article.</span></span>

<span data-ttu-id="13b13-208">**MongoDB gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="13b13-208">**MongoDB linked service:**</span></span>

```json
{
    "name": "OnPremisesMongoDbLinkedService",
    "properties":
    {
        "type": "OnPremisesMongoDb",
        "typeProperties":
        {
            "authenticationType": "<Basic or Anonymous>",
            "server": "< hello IP address or host name of hello MongoDB server >",  
            "port": "<hello number of hello TCP port that hello MongoDB server uses toolisten for client connections.>",
            "username": "<username>",
            "password": "<password>",
           "authSource": "< hello database that you want toouse toocheck your credentials for authentication. >",
            "databaseName": "<database name>",
            "gatewayName": "<mygateway>"
        }
    }
}
```

<span data-ttu-id="13b13-209">**Gekoppelde Azure Storage-service:**</span><span class="sxs-lookup"><span data-stu-id="13b13-209">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="13b13-210">**MongoDB-invoergegevensset:** instellen 'extern': 'true' informeert Hallo Data Factory-service die tabel Hallo externe toohello data factory is en niet wordt geproduceerd door een activiteit in de gegevensfactory Hallo.</span><span class="sxs-lookup"><span data-stu-id="13b13-210">**MongoDB input dataset:** Setting “external”: ”true” informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
     "name":  "MongoDbInputDataset",
    "properties": {
        "type": "MongoDbCollection",
        "linkedServiceName": "OnPremisesMongoDbLinkedService",
        "typeProperties": {
            "collectionName": "<Collection name>"    
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

<span data-ttu-id="13b13-211">**Azure Blob-uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="13b13-211">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="13b13-212">Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="13b13-212">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="13b13-213">pad naar map voor blob Hallo Hallo wordt dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="13b13-213">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="13b13-214">Hallo mappad jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="13b13-214">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/frommongodb/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="13b13-215">**De kopieeractiviteit in een pijplijn met MongoDB-bron en sink van Blob:**</span><span class="sxs-lookup"><span data-stu-id="13b13-215">**Copy activity in a pipeline with MongoDB source and Blob sink:**</span></span>

<span data-ttu-id="13b13-216">Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo hierboven invoer- en uitvoergegevenssets en geplande toorun elk uur.</span><span class="sxs-lookup"><span data-stu-id="13b13-216">hello pipeline contains a Copy Activity that is configured toouse hello above input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="13b13-217">Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**MongoDbSource** en **sink** type is ingesteld, te**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="13b13-217">In hello pipeline JSON definition, hello **source** type is set too**MongoDbSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="13b13-218">Hallo SQL-query is opgegeven voor Hallo **query** eigenschap Hallo gegevens selecteert in Hallo voorbij toocopy uur.</span><span class="sxs-lookup"><span data-stu-id="13b13-218">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopyMongoDBToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "MongoDbSource",
                        "query": "$$Text.Format('select * from  MyTable where LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "MongoDbInputDataset"
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
                "name": "MongoDBToAzureBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```


## <a name="schema-by-data-factory"></a><span data-ttu-id="13b13-219">Schema door Data Factory</span><span class="sxs-lookup"><span data-stu-id="13b13-219">Schema by Data Factory</span></span>
<span data-ttu-id="13b13-220">Azure Data Factory-service afleidt schema uit een verzameling MongoDB met behulp van Hallo nieuwste 100 documenten in Hallo-verzameling.</span><span class="sxs-lookup"><span data-stu-id="13b13-220">Azure Data Factory service infers schema from a MongoDB collection by using hello latest 100 documents in hello collection.</span></span> <span data-ttu-id="13b13-221">Als deze 100 documenten niet volledig schema bevatten, kunnen sommige kolommen tijdens de kopieerbewerking Hallo worden genegeerd.</span><span class="sxs-lookup"><span data-stu-id="13b13-221">If these 100 documents do not contain full schema, some columns may be ignored during hello copy operation.</span></span>

## <a name="type-mapping-for-mongodb"></a><span data-ttu-id="13b13-222">Toewijzing van het type voor MongoDB</span><span class="sxs-lookup"><span data-stu-id="13b13-222">Type mapping for MongoDB</span></span>
<span data-ttu-id="13b13-223">Zoals vermeld in Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel kopieeractiviteit voert automatische typeconversies van brontypen typen toosink Hello 2 stap benadering te volgen:</span><span class="sxs-lookup"><span data-stu-id="13b13-223">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="13b13-224">Systeemeigen bron typen too.NET type converteren</span><span class="sxs-lookup"><span data-stu-id="13b13-224">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="13b13-225">Converteren van .NET-type toonative sink-type</span><span class="sxs-lookup"><span data-stu-id="13b13-225">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="13b13-226">Bij het verplaatsen van gegevens tooMongoDB Hallo na worden toewijzingen van MongoDB typen too.NET typen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="13b13-226">When moving data tooMongoDB hello following mappings are used from MongoDB types too.NET types.</span></span>

| <span data-ttu-id="13b13-227">MongoDB-type</span><span class="sxs-lookup"><span data-stu-id="13b13-227">MongoDB type</span></span> | <span data-ttu-id="13b13-228">.NET framework-type</span><span class="sxs-lookup"><span data-stu-id="13b13-228">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="13b13-229">Binaire</span><span class="sxs-lookup"><span data-stu-id="13b13-229">Binary</span></span> |<span data-ttu-id="13b13-230">Byte]</span><span class="sxs-lookup"><span data-stu-id="13b13-230">Byte[]</span></span> |
| <span data-ttu-id="13b13-231">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="13b13-231">Boolean</span></span> |<span data-ttu-id="13b13-232">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="13b13-232">Boolean</span></span> |
| <span data-ttu-id="13b13-233">Date</span><span class="sxs-lookup"><span data-stu-id="13b13-233">Date</span></span> |<span data-ttu-id="13b13-234">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="13b13-234">DateTime</span></span> |
| <span data-ttu-id="13b13-235">NumberDouble</span><span class="sxs-lookup"><span data-stu-id="13b13-235">NumberDouble</span></span> |<span data-ttu-id="13b13-236">dubbele</span><span class="sxs-lookup"><span data-stu-id="13b13-236">Double</span></span> |
| <span data-ttu-id="13b13-237">NumberInt</span><span class="sxs-lookup"><span data-stu-id="13b13-237">NumberInt</span></span> |<span data-ttu-id="13b13-238">Int32</span><span class="sxs-lookup"><span data-stu-id="13b13-238">Int32</span></span> |
| <span data-ttu-id="13b13-239">NumberLong</span><span class="sxs-lookup"><span data-stu-id="13b13-239">NumberLong</span></span> |<span data-ttu-id="13b13-240">Int64</span><span class="sxs-lookup"><span data-stu-id="13b13-240">Int64</span></span> |
| <span data-ttu-id="13b13-241">Object-id</span><span class="sxs-lookup"><span data-stu-id="13b13-241">ObjectID</span></span> |<span data-ttu-id="13b13-242">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="13b13-242">String</span></span> |
| <span data-ttu-id="13b13-243">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="13b13-243">String</span></span> |<span data-ttu-id="13b13-244">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="13b13-244">String</span></span> |
| <span data-ttu-id="13b13-245">UUID</span><span class="sxs-lookup"><span data-stu-id="13b13-245">UUID</span></span> |<span data-ttu-id="13b13-246">GUID</span><span class="sxs-lookup"><span data-stu-id="13b13-246">Guid</span></span> |
| <span data-ttu-id="13b13-247">Object</span><span class="sxs-lookup"><span data-stu-id="13b13-247">Object</span></span> |<span data-ttu-id="13b13-248">Renormalized plat in kolommen met '_' als geneste scheidingsteken</span><span class="sxs-lookup"><span data-stu-id="13b13-248">Renormalized into flatten columns with “_” as nested separator</span></span> |

> [!NOTE]
> <span data-ttu-id="13b13-249">toolearn over ondersteuning voor arrays met virtuele tabellen te verwijzen[ondersteuning voor complexe typen virtuele tabellen met](#support-for-complex-types-using-virtual-tables) hieronder.</span><span class="sxs-lookup"><span data-stu-id="13b13-249">toolearn about support for arrays using virtual tables, refer too[Support for complex types using virtual tables](#support-for-complex-types-using-virtual-tables) section below.</span></span>

<span data-ttu-id="13b13-250">Op dit moment Hallo na MongoDB-gegevenstypen worden niet ondersteund: DBPointer, JavaScript, Max per minuut sleutel, reguliere expressie, symbool, Timestamp, Undefined</span><span class="sxs-lookup"><span data-stu-id="13b13-250">Currently, hello following MongoDB data types are not supported: DBPointer, JavaScript, Max/Min key, Regular Expression, Symbol, Timestamp, Undefined</span></span>

## <a name="support-for-complex-types-using-virtual-tables"></a><span data-ttu-id="13b13-251">Ondersteuning voor complexe typen met behulp van de virtuele tabellen</span><span class="sxs-lookup"><span data-stu-id="13b13-251">Support for complex types using virtual tables</span></span>
<span data-ttu-id="13b13-252">Azure Data Factory maakt gebruik van een ingebouwde ODBC-stuurprogramma tooconnect tooand gegevens kopiëren van de MongoDB-database.</span><span class="sxs-lookup"><span data-stu-id="13b13-252">Azure Data Factory uses a built-in ODBC driver tooconnect tooand copy data from your MongoDB database.</span></span> <span data-ttu-id="13b13-253">Voor complexe gegevenstypen zoals matrices of objecten met verschillende typen op Hallo documenten normaliseert Hallo stuurprogramma gegevens opnieuw in de bijbehorende virtuele tabellen.</span><span class="sxs-lookup"><span data-stu-id="13b13-253">For complex types such as arrays or objects with different types across hello documents, hello driver re-normalizes data into corresponding virtual tables.</span></span> <span data-ttu-id="13b13-254">In het bijzonder als een tabel bevat een dergelijke kolommen, genereert Hallo stuurprogramma Hallo virtuele tabellen te volgen:</span><span class="sxs-lookup"><span data-stu-id="13b13-254">Specifically, if a table contains such columns, hello driver generates hello following virtual tables:</span></span>

* <span data-ttu-id="13b13-255">Een **basistabel**, die bevat dezelfde gegevens als de echte tabel, met uitzondering van kolommen van het complexe type Hallo HALLO hallo.</span><span class="sxs-lookup"><span data-stu-id="13b13-255">A **base table**, which contains hello same data as hello real table except for hello complex type columns.</span></span> <span data-ttu-id="13b13-256">de basistabel Hallo gebruikt Hallo dezelfde naam als Hallo echte tabel die wordt vertegenwoordigd.</span><span class="sxs-lookup"><span data-stu-id="13b13-256">hello base table uses hello same name as hello real table that it represents.</span></span>
* <span data-ttu-id="13b13-257">Een **virtuele tabel** voor elke kolom complex type zijn dat wordt uitgebreid Hallo geneste gegevens.</span><span class="sxs-lookup"><span data-stu-id="13b13-257">A **virtual table** for each complex type column, which expands hello nested data.</span></span> <span data-ttu-id="13b13-258">Hallo virtuele tabellen zijn benoemde met Hallo-naam van de echte tabel hello, een scheidingsteken '_' en het Hallo-naam van het Hallo-matrix of object.</span><span class="sxs-lookup"><span data-stu-id="13b13-258">hello virtual tables are named using hello name of hello real table, a separator “_” and hello name of hello array or object.</span></span>

<span data-ttu-id="13b13-259">Virtuele tabellen verwijzen toohello-gegevens in de echte tabel hello, waardoor Hallo stuurprogramma tooaccess Hallo gedenormaliseerd gegevens.</span><span class="sxs-lookup"><span data-stu-id="13b13-259">Virtual tables refer toohello data in hello real table, enabling hello driver tooaccess hello denormalized data.</span></span> <span data-ttu-id="13b13-260">Zie de sectie Voorbeeld onder meer informatie.</span><span class="sxs-lookup"><span data-stu-id="13b13-260">See Example section below details.</span></span> <span data-ttu-id="13b13-261">Hallo-inhoud van het MongoDB-matrices kunt u door het uitvoeren van query's en het toevoegen aan virtuele tabellen Hallo openen.</span><span class="sxs-lookup"><span data-stu-id="13b13-261">You can access hello content of MongoDB arrays by querying and joining hello virtual tables.</span></span>

<span data-ttu-id="13b13-262">U kunt Hallo [Wizard kopiëren](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively weergeven lijst met tabellen in de MongoDB-database met inbegrip van de virtuele tabellen Hallo Hallo en een voorbeeld van gegevens binnen Hallo.</span><span class="sxs-lookup"><span data-stu-id="13b13-262">You can use hello [Copy Wizard](data-factory-data-movement-activities.md#create-a-pipeline-with-copy-activity) toointuitively view hello list of tables in MongoDB database including hello virtual tables, and preview hello data inside.</span></span> <span data-ttu-id="13b13-263">U kunt ook maakt u een query in de Wizard kopiëren Hallo en toosee Hallo resultaat valideren.</span><span class="sxs-lookup"><span data-stu-id="13b13-263">You can also construct a query in hello Copy Wizard and validate toosee hello result.</span></span>

### <a name="example"></a><span data-ttu-id="13b13-264">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="13b13-264">Example</span></span>
<span data-ttu-id="13b13-265">'ExampleTable' hieronder is bijvoorbeeld een MongoDB-tabel met één kolom met een matrix van objecten in elke cel – facturen en één kolom met een matrix van scalaire typen – classificaties.</span><span class="sxs-lookup"><span data-stu-id="13b13-265">For example, “ExampleTable” below is a MongoDB table that has one column with an array of Objects in each cell – Invoices, and one column with an array of Scalar types – Ratings.</span></span>

| <span data-ttu-id="13b13-266">_id</span><span class="sxs-lookup"><span data-stu-id="13b13-266">_id</span></span> | <span data-ttu-id="13b13-267">Naam van de klant</span><span class="sxs-lookup"><span data-stu-id="13b13-267">Customer Name</span></span> | <span data-ttu-id="13b13-268">Facturen</span><span class="sxs-lookup"><span data-stu-id="13b13-268">Invoices</span></span> | <span data-ttu-id="13b13-269">Serviceniveau</span><span class="sxs-lookup"><span data-stu-id="13b13-269">Service Level</span></span> | <span data-ttu-id="13b13-270">De classificaties</span><span class="sxs-lookup"><span data-stu-id="13b13-270">Ratings</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="13b13-271">1111</span><span class="sxs-lookup"><span data-stu-id="13b13-271">1111</span></span> |<span data-ttu-id="13b13-272">ABC</span><span class="sxs-lookup"><span data-stu-id="13b13-272">ABC</span></span> |<span data-ttu-id="13b13-273">[{invoice_id: '123' item: 'toaster', de prijs: '456' korting: "0,2"}, {invoice_id: '124' item: 'ingesteld', prijs: '1235' korting: "0,2"}]</span><span class="sxs-lookup"><span data-stu-id="13b13-273">[{invoice_id:”123”, item:”toaster”, price:”456”, discount:”0.2”}, {invoice_id:”124”, item:”oven”, price: ”1235”, discount: ”0.2”}]</span></span> |<span data-ttu-id="13b13-274">Zilver</span><span class="sxs-lookup"><span data-stu-id="13b13-274">Silver</span></span> |<span data-ttu-id="13b13-275">[5,6]</span><span class="sxs-lookup"><span data-stu-id="13b13-275">[5,6]</span></span> |
| <span data-ttu-id="13b13-276">2222</span><span class="sxs-lookup"><span data-stu-id="13b13-276">2222</span></span> |<span data-ttu-id="13b13-277">XYZ</span><span class="sxs-lookup"><span data-stu-id="13b13-277">XYZ</span></span> |<span data-ttu-id="13b13-278">[{invoice_id: item '135': 'koelkast', prijs: '12543' korting: "0,0"}]</span><span class="sxs-lookup"><span data-stu-id="13b13-278">[{invoice_id:”135”, item:”fridge”, price: ”12543”, discount: ”0.0”}]</span></span> |<span data-ttu-id="13b13-279">Goud</span><span class="sxs-lookup"><span data-stu-id="13b13-279">Gold</span></span> |<span data-ttu-id="13b13-280">[1,2]</span><span class="sxs-lookup"><span data-stu-id="13b13-280">[1,2]</span></span> |

<span data-ttu-id="13b13-281">Hallo stuurprogramma genereert meerdere virtuele tabellen toorepresent deze één tabel.</span><span class="sxs-lookup"><span data-stu-id="13b13-281">hello driver would generate multiple virtual tables toorepresent this single table.</span></span> <span data-ttu-id="13b13-282">de eerste virtuele tabel Hallo is Hallo basistabel met de naam 'ExampleTable', hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="13b13-282">hello first virtual table is hello base table named “ExampleTable”, shown below.</span></span> <span data-ttu-id="13b13-283">Hallo basistabel bevat alle Hallo gegevens van de oorspronkelijke tabel hello, maar Hallo gegevens van Hallo matrices is weggelaten en in virtuele tabellen Hallo is uitgevouwen.</span><span class="sxs-lookup"><span data-stu-id="13b13-283">hello base table contains all hello data of hello original table, but hello data from hello arrays has been omitted and is expanded in hello virtual tables.</span></span>

| <span data-ttu-id="13b13-284">_id</span><span class="sxs-lookup"><span data-stu-id="13b13-284">_id</span></span> | <span data-ttu-id="13b13-285">Naam van de klant</span><span class="sxs-lookup"><span data-stu-id="13b13-285">Customer Name</span></span> | <span data-ttu-id="13b13-286">Serviceniveau</span><span class="sxs-lookup"><span data-stu-id="13b13-286">Service Level</span></span> |
| --- | --- | --- |
| <span data-ttu-id="13b13-287">1111</span><span class="sxs-lookup"><span data-stu-id="13b13-287">1111</span></span> |<span data-ttu-id="13b13-288">ABC</span><span class="sxs-lookup"><span data-stu-id="13b13-288">ABC</span></span> |<span data-ttu-id="13b13-289">Zilver</span><span class="sxs-lookup"><span data-stu-id="13b13-289">Silver</span></span> |
| <span data-ttu-id="13b13-290">2222</span><span class="sxs-lookup"><span data-stu-id="13b13-290">2222</span></span> |<span data-ttu-id="13b13-291">XYZ</span><span class="sxs-lookup"><span data-stu-id="13b13-291">XYZ</span></span> |<span data-ttu-id="13b13-292">Goud</span><span class="sxs-lookup"><span data-stu-id="13b13-292">Gold</span></span> |

<span data-ttu-id="13b13-293">Hallo volgende tabellen bevatten Hallo virtuele tabellen die oorspronkelijke matrices in voorbeeld Hallo Hallo vertegenwoordigen.</span><span class="sxs-lookup"><span data-stu-id="13b13-293">hello following tables show hello virtual tables that represent hello original arrays in hello example.</span></span> <span data-ttu-id="13b13-294">Deze tabellen bevatten de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="13b13-294">These tables contain hello following:</span></span>

* <span data-ttu-id="13b13-295">Verwijzing naar een back-toohello originele primaire-sleutelkolom bijbehorende toohello rij van de oorspronkelijke matrix hello (via Hallo _id kolom)</span><span class="sxs-lookup"><span data-stu-id="13b13-295">A reference back toohello original primary key column corresponding toohello row of hello original array (via hello _id column)</span></span>
* <span data-ttu-id="13b13-296">Een indicatie van de positie van gegevens binnen de oorspronkelijke matrix Hallo HALLO hallo</span><span class="sxs-lookup"><span data-stu-id="13b13-296">An indication of hello position of hello data within hello original array</span></span>
* <span data-ttu-id="13b13-297">Hallo-gegevens voor elk element in een matrix van Hallo uitgevouwen</span><span class="sxs-lookup"><span data-stu-id="13b13-297">hello expanded data for each element within hello array</span></span>

<span data-ttu-id="13b13-298">Tabel 'ExampleTable_Invoices':</span><span class="sxs-lookup"><span data-stu-id="13b13-298">Table “ExampleTable_Invoices”:</span></span>

| <span data-ttu-id="13b13-299">_id</span><span class="sxs-lookup"><span data-stu-id="13b13-299">_id</span></span> | <span data-ttu-id="13b13-300">ExampleTable_Invoices_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="13b13-300">ExampleTable_Invoices_dim1_idx</span></span> | <span data-ttu-id="13b13-301">invoice_id</span><span class="sxs-lookup"><span data-stu-id="13b13-301">invoice_id</span></span> | <span data-ttu-id="13b13-302">item</span><span class="sxs-lookup"><span data-stu-id="13b13-302">item</span></span> | <span data-ttu-id="13b13-303">price</span><span class="sxs-lookup"><span data-stu-id="13b13-303">price</span></span> | <span data-ttu-id="13b13-304">Korting</span><span class="sxs-lookup"><span data-stu-id="13b13-304">Discount</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="13b13-305">1111</span><span class="sxs-lookup"><span data-stu-id="13b13-305">1111</span></span> |<span data-ttu-id="13b13-306">0</span><span class="sxs-lookup"><span data-stu-id="13b13-306">0</span></span> |<span data-ttu-id="13b13-307">123</span><span class="sxs-lookup"><span data-stu-id="13b13-307">123</span></span> |<span data-ttu-id="13b13-308">toaster</span><span class="sxs-lookup"><span data-stu-id="13b13-308">toaster</span></span> |<span data-ttu-id="13b13-309">456</span><span class="sxs-lookup"><span data-stu-id="13b13-309">456</span></span> |<span data-ttu-id="13b13-310">0.2</span><span class="sxs-lookup"><span data-stu-id="13b13-310">0.2</span></span> |
| <span data-ttu-id="13b13-311">1111</span><span class="sxs-lookup"><span data-stu-id="13b13-311">1111</span></span> |<span data-ttu-id="13b13-312">1</span><span class="sxs-lookup"><span data-stu-id="13b13-312">1</span></span> |<span data-ttu-id="13b13-313">124</span><span class="sxs-lookup"><span data-stu-id="13b13-313">124</span></span> |<span data-ttu-id="13b13-314">ingesteld</span><span class="sxs-lookup"><span data-stu-id="13b13-314">oven</span></span> |<span data-ttu-id="13b13-315">1235</span><span class="sxs-lookup"><span data-stu-id="13b13-315">1235</span></span> |<span data-ttu-id="13b13-316">0.2</span><span class="sxs-lookup"><span data-stu-id="13b13-316">0.2</span></span> |
| <span data-ttu-id="13b13-317">2222</span><span class="sxs-lookup"><span data-stu-id="13b13-317">2222</span></span> |<span data-ttu-id="13b13-318">0</span><span class="sxs-lookup"><span data-stu-id="13b13-318">0</span></span> |<span data-ttu-id="13b13-319">135</span><span class="sxs-lookup"><span data-stu-id="13b13-319">135</span></span> |<span data-ttu-id="13b13-320">koelkast</span><span class="sxs-lookup"><span data-stu-id="13b13-320">fridge</span></span> |<span data-ttu-id="13b13-321">12543</span><span class="sxs-lookup"><span data-stu-id="13b13-321">12543</span></span> |<span data-ttu-id="13b13-322">0.0</span><span class="sxs-lookup"><span data-stu-id="13b13-322">0.0</span></span> |

<span data-ttu-id="13b13-323">Tabel 'ExampleTable_Ratings':</span><span class="sxs-lookup"><span data-stu-id="13b13-323">Table “ExampleTable_Ratings”:</span></span>

| <span data-ttu-id="13b13-324">_id</span><span class="sxs-lookup"><span data-stu-id="13b13-324">_id</span></span> | <span data-ttu-id="13b13-325">ExampleTable_Ratings_dim1_idx</span><span class="sxs-lookup"><span data-stu-id="13b13-325">ExampleTable_Ratings_dim1_idx</span></span> | <span data-ttu-id="13b13-326">ExampleTable_Ratings</span><span class="sxs-lookup"><span data-stu-id="13b13-326">ExampleTable_Ratings</span></span> |
| --- | --- | --- |
| <span data-ttu-id="13b13-327">1111</span><span class="sxs-lookup"><span data-stu-id="13b13-327">1111</span></span> |<span data-ttu-id="13b13-328">0</span><span class="sxs-lookup"><span data-stu-id="13b13-328">0</span></span> |<span data-ttu-id="13b13-329">5</span><span class="sxs-lookup"><span data-stu-id="13b13-329">5</span></span> |
| <span data-ttu-id="13b13-330">1111</span><span class="sxs-lookup"><span data-stu-id="13b13-330">1111</span></span> |<span data-ttu-id="13b13-331">1</span><span class="sxs-lookup"><span data-stu-id="13b13-331">1</span></span> |<span data-ttu-id="13b13-332">6</span><span class="sxs-lookup"><span data-stu-id="13b13-332">6</span></span> |
| <span data-ttu-id="13b13-333">2222</span><span class="sxs-lookup"><span data-stu-id="13b13-333">2222</span></span> |<span data-ttu-id="13b13-334">0</span><span class="sxs-lookup"><span data-stu-id="13b13-334">0</span></span> |<span data-ttu-id="13b13-335">1</span><span class="sxs-lookup"><span data-stu-id="13b13-335">1</span></span> |
| <span data-ttu-id="13b13-336">2222</span><span class="sxs-lookup"><span data-stu-id="13b13-336">2222</span></span> |<span data-ttu-id="13b13-337">1</span><span class="sxs-lookup"><span data-stu-id="13b13-337">1</span></span> |<span data-ttu-id="13b13-338">2</span><span class="sxs-lookup"><span data-stu-id="13b13-338">2</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="13b13-339">Bronkolommen toosink toewijzen</span><span class="sxs-lookup"><span data-stu-id="13b13-339">Map source toosink columns</span></span>
<span data-ttu-id="13b13-340">Zie toolearn over het toewijzen van kolommen in bron gegevensset toocolumns in sink-gegevensset [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="13b13-340">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="13b13-341">Herhaalbare leesbewerking van relationele bronnen</span><span class="sxs-lookup"><span data-stu-id="13b13-341">Repeatable read from relational sources</span></span>
<span data-ttu-id="13b13-342">Houd bij het kopiëren van gegevens uit een relationele gegevensopslag, herhaalbaarheid rekening tooavoid ongewenste resultaten.</span><span class="sxs-lookup"><span data-stu-id="13b13-342">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="13b13-343">In Azure Data Factory, kunt u een segment handmatig opnieuw.</span><span class="sxs-lookup"><span data-stu-id="13b13-343">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="13b13-344">U kunt ook een beleid voor opnieuw proberen voor een gegevensset configureren zodat een segment wordt opnieuw uitgevoerd wanneer een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="13b13-344">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="13b13-345">Wanneer een segment opnieuw in beide gevallen wordt uitgevoerd, moet u ervoor dat dezelfde gegevens Hallo toomake wordt gelezen ongeacht hoe vaak een segment wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="13b13-345">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="13b13-346">Zie [Repeatable van relationele bronnen lezen](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="13b13-346">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="13b13-347">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="13b13-347">Performance and Tuning</span></span>
<span data-ttu-id="13b13-348">Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.</span><span class="sxs-lookup"><span data-stu-id="13b13-348">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="13b13-349">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="13b13-349">Next Steps</span></span>
<span data-ttu-id="13b13-350">Zie [gegevens verplaatsen tussen on-premises en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor stapsgewijze instructies voor het maken van een pijplijn gegevens die worden verplaatst gegevens uit een on-premises gegevens tooan Azure data store opslaan.</span><span class="sxs-lookup"><span data-stu-id="13b13-350">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions for creating a data pipeline that moves data from an on-premises data store tooan Azure data store.</span></span>
