---
title: gegevens uit een SAP Business Warehouse met behulp van Azure Data Factory aaaMove | Microsoft Docs
description: Meer informatie over het toomove gegevens uit een SAP Business Warehouse met behulp van Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: 85df16f4759a846f578cad301e3cf918179143d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sap-business-warehouse-using-azure-data-factory"></a><span data-ttu-id="1f62d-103">Verplaatsen van gegevens uit SAP Business Warehouse met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="1f62d-103">Move data From SAP Business Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="1f62d-104">Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit in Azure Data Factory toomove gegevens uit een SAP Business Warehouse (BW) voor lokale Hallo.</span><span class="sxs-lookup"><span data-stu-id="1f62d-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises SAP Business Warehouse (BW).</span></span> <span data-ttu-id="1f62d-105">Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.</span><span class="sxs-lookup"><span data-stu-id="1f62d-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="1f62d-106">U kunt gegevens uit een on-premises SAP Business Warehouse store tooany ondersteund sink gegevens gegevensopslag kopiëren.</span><span class="sxs-lookup"><span data-stu-id="1f62d-106">You can copy data from an on-premises SAP Business Warehouse data store tooany supported sink data store.</span></span> <span data-ttu-id="1f62d-107">Zie voor een lijst van gegevens winkels ondersteund zoals sinks door kopieeractiviteit hello, Hallo [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel.</span><span class="sxs-lookup"><span data-stu-id="1f62d-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="1f62d-108">Data factory ondersteunt momenteel alleen verplaatsen van gegevens uit een SAP Business Warehouse tooother gegevens worden opgeslagen, maar niet voor tooan SAP Business Warehouse verplaatsen van gegevens van andere gegevens worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="1f62d-108">Data factory currently supports only moving data from an SAP Business Warehouse tooother data stores, but not for moving data from other data stores tooan SAP Business Warehouse.</span></span> 

## <a name="supported-versions-and-installation"></a><span data-ttu-id="1f62d-109">Ondersteunde versies en installatie</span><span class="sxs-lookup"><span data-stu-id="1f62d-109">Supported versions and installation</span></span>
<span data-ttu-id="1f62d-110">Deze connector ondersteunt SAP Business Warehouse versie 7.x.</span><span class="sxs-lookup"><span data-stu-id="1f62d-110">This connector supports SAP Business Warehouse version 7.x.</span></span> <span data-ttu-id="1f62d-111">Het ondersteunt kopiëren van gegevens van InfoCubes en QueryCubes (inclusief BEx query's) met behulp van de MDX-query's.</span><span class="sxs-lookup"><span data-stu-id="1f62d-111">It supports copying data from InfoCubes and QueryCubes (including BEx queries) using MDX queries.</span></span>

<span data-ttu-id="1f62d-112">tooenable hello connectiviteit toohello SAP BW-exemplaar installeren Hallo volgende onderdelen:</span><span class="sxs-lookup"><span data-stu-id="1f62d-112">tooenable hello connectivity toohello SAP BW instance, install hello following components:</span></span>
- <span data-ttu-id="1f62d-113">**Data Management Gateway**: Data Factory-service ondersteunt verbindingen van tooon-premises gegevens winkels (inclusief SAP Business Warehouse) met een onderdeel genaamd Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="1f62d-113">**Data Management Gateway**: Data Factory service supports connecting tooon-premises data stores (including SAP Business Warehouse) using a component called Data Management Gateway.</span></span> <span data-ttu-id="1f62d-114">toolearn over Data Management Gateway en stapsgewijze instructies voor het instellen van Hallo-gateway, Zie [verplaatsen tussen on-premises gegevens gegevensarchief gegevensarchief toocloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="1f62d-114">toolearn about Data Management Gateway and step-by-step instructions for setting up hello gateway, see [Moving data between on-premises data store toocloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="1f62d-115">Gateway is vereist, zelfs als Hallo SAP Business Warehouse wordt gehost in een Azure IaaS virtuele machine (VM).</span><span class="sxs-lookup"><span data-stu-id="1f62d-115">Gateway is required even if hello SAP Business Warehouse is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="1f62d-116">U kunt Hallo gateway installeren op Hallo dezelfde virtuele machine als Hallo gegevens opslaan of op een andere virtuele machine zo lang Hallo gateway kunt verbinding maken met toohello-database.</span><span class="sxs-lookup"><span data-stu-id="1f62d-116">You can install hello gateway on hello same VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>
- <span data-ttu-id="1f62d-117">**SAP NetWeaver bibliotheek** op Hallo gateway-apparaat.</span><span class="sxs-lookup"><span data-stu-id="1f62d-117">**SAP NetWeaver library** on hello gateway machine.</span></span> <span data-ttu-id="1f62d-118">U krijgt Hallo SAP Netweaver bibliotheek uit de SAP-beheerder of rechtstreeks uit Hallo [SAP Software Download Center](https://support.sap.com/swdc).</span><span class="sxs-lookup"><span data-stu-id="1f62d-118">You can get hello SAP Netweaver library from your SAP administrator, or directly from hello [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="1f62d-119">Zoeken naar Hallo **SAP-notitie #1025361** tooget Hallo downloadlocatie voor de meest recente versie Hallo.</span><span class="sxs-lookup"><span data-stu-id="1f62d-119">Search for hello **SAP Note #1025361** tooget hello download location for hello most recent version.</span></span> <span data-ttu-id="1f62d-120">Zorg ervoor dat het Hallo-architectuur voor SAP NetWeaver Hallo-bibliotheek (32-bits of 64-bits) overeenkomt met uw gateway-installatie.</span><span class="sxs-lookup"><span data-stu-id="1f62d-120">Make sure that hello architecture for hello SAP NetWeaver library (32-bit or 64-bit) matches your gateway installation.</span></span> <span data-ttu-id="1f62d-121">Installeer vervolgens alle bestanden in Hallo SAP NetWeaver RFC SDK volgens toohello SAP-notitie.</span><span class="sxs-lookup"><span data-stu-id="1f62d-121">Then install all files included in hello SAP NetWeaver RFC SDK according toohello SAP Note.</span></span> <span data-ttu-id="1f62d-122">Hallo SAP NetWeaver bibliotheek is ook opgenomen in Hallo SAP-hulpprogramma's voor Client-installatie.</span><span class="sxs-lookup"><span data-stu-id="1f62d-122">hello SAP NetWeaver library is also included in hello SAP Client Tools installation.</span></span>

> [!TIP]
> <span data-ttu-id="1f62d-123">Hallo-dll's opgehaald uit Hallo NetWeaver RFC SDK in de map system32 plaatsen.</span><span class="sxs-lookup"><span data-stu-id="1f62d-123">Put hello dlls extracted from hello NetWeaver RFC SDK into system32 folder.</span></span>

## <a name="getting-started"></a><span data-ttu-id="1f62d-124">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="1f62d-124">Getting started</span></span>
<span data-ttu-id="1f62d-125">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens vanuit een on-premises Cassandra-gegevensopslag verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="1f62d-125">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="1f62d-126">Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="1f62d-126">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="1f62d-127">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="1f62d-127">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="1f62d-128">U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="1f62d-128">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="1f62d-129">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="1f62d-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="1f62d-130">Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="1f62d-130">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="1f62d-131">Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="1f62d-131">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="1f62d-132">Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="1f62d-132">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="1f62d-133">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="1f62d-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="1f62d-134">Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1f62d-134">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="1f62d-135">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="1f62d-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="1f62d-136">Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens uit een lokale SAP Business Warehouse zijn [JSON-voorbeeld: gegevens kopiëren van een SAP Business Warehouse tooAzure Blob](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="1f62d-136">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises SAP Business Warehouse, see [JSON example: Copy data from SAP Business Warehouse tooAzure Blob](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="1f62d-137">Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooan SAP BW-gegevensarchief zijn:</span><span class="sxs-lookup"><span data-stu-id="1f62d-137">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooan SAP BW data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="1f62d-138">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="1f62d-138">Linked service properties</span></span>
<span data-ttu-id="1f62d-139">Hallo volgende tabel bevat een beschrijving voor JSON-elementen specifieke tooSAP Business Warehouse (BW) gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="1f62d-139">hello following table provides description for JSON elements specific tooSAP Business Warehouse (BW) linked service.</span></span>

<span data-ttu-id="1f62d-140">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="1f62d-140">Property</span></span> | <span data-ttu-id="1f62d-141">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="1f62d-141">Description</span></span> | <span data-ttu-id="1f62d-142">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="1f62d-142">Allowed values</span></span> | <span data-ttu-id="1f62d-143">Vereist</span><span class="sxs-lookup"><span data-stu-id="1f62d-143">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="1f62d-144">server</span><span class="sxs-lookup"><span data-stu-id="1f62d-144">server</span></span> | <span data-ttu-id="1f62d-145">Naam van het Hallo-server op welke Hallo SAP BW exemplaar zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="1f62d-145">Name of hello server on which hello SAP BW instance resides.</span></span> | <span data-ttu-id="1f62d-146">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="1f62d-146">string</span></span> | <span data-ttu-id="1f62d-147">Ja</span><span class="sxs-lookup"><span data-stu-id="1f62d-147">Yes</span></span>
<span data-ttu-id="1f62d-148">systemNumber</span><span class="sxs-lookup"><span data-stu-id="1f62d-148">systemNumber</span></span> | <span data-ttu-id="1f62d-149">Systeem aantal Hallo SAP BW-systeem.</span><span class="sxs-lookup"><span data-stu-id="1f62d-149">System number of hello SAP BW system.</span></span> | <span data-ttu-id="1f62d-150">Twee cijfers decimaal getal weergegeven als een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="1f62d-150">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="1f62d-151">Ja</span><span class="sxs-lookup"><span data-stu-id="1f62d-151">Yes</span></span>
<span data-ttu-id="1f62d-152">clientId</span><span class="sxs-lookup"><span data-stu-id="1f62d-152">clientId</span></span> | <span data-ttu-id="1f62d-153">Client-ID van de client Hallo in Hallo SAP W system.</span><span class="sxs-lookup"><span data-stu-id="1f62d-153">Client ID of hello client in hello SAP W system.</span></span> | <span data-ttu-id="1f62d-154">Drie cijfers decimaal getal weergegeven als een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="1f62d-154">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="1f62d-155">Ja</span><span class="sxs-lookup"><span data-stu-id="1f62d-155">Yes</span></span>
<span data-ttu-id="1f62d-156">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="1f62d-156">username</span></span> | <span data-ttu-id="1f62d-157">Naam van het Hallo-gebruiker met toegang toohello SAP-server</span><span class="sxs-lookup"><span data-stu-id="1f62d-157">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="1f62d-158">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="1f62d-158">string</span></span> | <span data-ttu-id="1f62d-159">Ja</span><span class="sxs-lookup"><span data-stu-id="1f62d-159">Yes</span></span>
<span data-ttu-id="1f62d-160">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="1f62d-160">password</span></span> | <span data-ttu-id="1f62d-161">Wachtwoord voor gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="1f62d-161">Password for hello user.</span></span> | <span data-ttu-id="1f62d-162">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="1f62d-162">string</span></span> | <span data-ttu-id="1f62d-163">Ja</span><span class="sxs-lookup"><span data-stu-id="1f62d-163">Yes</span></span>
<span data-ttu-id="1f62d-164">gatewayName</span><span class="sxs-lookup"><span data-stu-id="1f62d-164">gatewayName</span></span> | <span data-ttu-id="1f62d-165">Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello lokale SAP BW exemplaar gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1f62d-165">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP BW instance.</span></span> | <span data-ttu-id="1f62d-166">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="1f62d-166">string</span></span> | <span data-ttu-id="1f62d-167">Ja</span><span class="sxs-lookup"><span data-stu-id="1f62d-167">Yes</span></span>
<span data-ttu-id="1f62d-168">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="1f62d-168">encryptedCredential</span></span> | <span data-ttu-id="1f62d-169">Hallo versleutelde referentie-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="1f62d-169">hello encrypted credential string.</span></span> | <span data-ttu-id="1f62d-170">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="1f62d-170">string</span></span> | <span data-ttu-id="1f62d-171">Nee</span><span class="sxs-lookup"><span data-stu-id="1f62d-171">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="1f62d-172">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="1f62d-172">Dataset properties</span></span>
<span data-ttu-id="1f62d-173">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="1f62d-173">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="1f62d-174">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).</span><span class="sxs-lookup"><span data-stu-id="1f62d-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="1f62d-175">Hallo **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="1f62d-175">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="1f62d-176">Er zijn geen type-specifieke eigenschappen ondersteund voor SAP BW-gegevensset Hallo van het type **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="1f62d-176">There are no type-specific properties supported for hello SAP BW dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="1f62d-177">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="1f62d-177">Copy activity properties</span></span>
<span data-ttu-id="1f62d-178">Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="1f62d-178">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="1f62d-179">Eigenschappen zoals naam, beschrijving, invoer en uitvoer tabellen, zijn de beleidsregels zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="1f62d-179">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="1f62d-180">Dat eigenschappen beschikbaar zijn in Hallo **typeProperties** sectie van de activiteit Hallo variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="1f62d-180">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="1f62d-181">Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="1f62d-181">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="1f62d-182">Wanneer u de gegevensbron in de kopieerbewerking is van het type **RelationalSource** (waaronder SAP BW), Hallo volgende eigenschappen beschikbaar zijn in de sectie typeProperties:</span><span class="sxs-lookup"><span data-stu-id="1f62d-182">When source in copy activity is of type **RelationalSource** (which includes SAP BW), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="1f62d-183">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="1f62d-183">Property</span></span> | <span data-ttu-id="1f62d-184">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="1f62d-184">Description</span></span> | <span data-ttu-id="1f62d-185">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="1f62d-185">Allowed values</span></span> | <span data-ttu-id="1f62d-186">Vereist</span><span class="sxs-lookup"><span data-stu-id="1f62d-186">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="1f62d-187">query</span><span class="sxs-lookup"><span data-stu-id="1f62d-187">query</span></span> | <span data-ttu-id="1f62d-188">Hiermee geeft u Hallo MDX-query tooread gegevens van Hallo SAP BW-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="1f62d-188">Specifies hello MDX query tooread data from hello SAP BW instance.</span></span> | <span data-ttu-id="1f62d-189">MDX-query.</span><span class="sxs-lookup"><span data-stu-id="1f62d-189">MDX query.</span></span> | <span data-ttu-id="1f62d-190">Ja</span><span class="sxs-lookup"><span data-stu-id="1f62d-190">Yes</span></span> |


## <a name="json-example-copy-data-from-sap-business-warehouse-tooazure-blob"></a><span data-ttu-id="1f62d-191">JSON-voorbeeld: gegevens uit een SAP Business Warehouse tooAzure Blob kopiëren</span><span class="sxs-lookup"><span data-stu-id="1f62d-191">JSON example: Copy data from SAP Business Warehouse tooAzure Blob</span></span>
<span data-ttu-id="1f62d-192">Hallo volgende voorbeeld wordt een voorbeeld JSON definities waarmee u een pijplijn toocreate kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="1f62d-192">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="1f62d-193">In dit voorbeeld laat zien hoe toocopy gegevens uit een SAP Business Warehouse tooan voor lokale Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="1f62d-193">This sample shows how toocopy data from an on-premises SAP Business Warehouse tooan Azure Blob Storage.</span></span> <span data-ttu-id="1f62d-194">Echter, de gegevens kunnen worden gekopieerd **rechtstreeks** tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1f62d-194">However, data can be copied **directly** tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="1f62d-195">Dit voorbeeld bevat JSON-fragmenten.</span><span class="sxs-lookup"><span data-stu-id="1f62d-195">This sample provides JSON snippets.</span></span> <span data-ttu-id="1f62d-196">Dit omvat geen stapsgewijze instructies voor het maken van de gegevensfactory Hallo.</span><span class="sxs-lookup"><span data-stu-id="1f62d-196">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="1f62d-197">Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor stapsgewijze instructies.</span><span class="sxs-lookup"><span data-stu-id="1f62d-197">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="1f62d-198">Hallo voorbeeld heeft Hallo data factory-entiteiten te volgen:</span><span class="sxs-lookup"><span data-stu-id="1f62d-198">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="1f62d-199">Een gekoppelde service van het type [SapBw](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1f62d-199">A linked service of type [SapBw](#linked-service-properties).</span></span>
2. <span data-ttu-id="1f62d-200">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="1f62d-200">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="1f62d-201">Invoer [gegevensset](data-factory-create-datasets.md) van het type [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1f62d-201">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="1f62d-202">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="1f62d-202">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="1f62d-203">Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [RelationalSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="1f62d-203">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="1f62d-204">Hallo voorbeeld gegevens worden gekopieerd van een SAP Business Warehouse-exemplaar tooan Azure blob per uur.</span><span class="sxs-lookup"><span data-stu-id="1f62d-204">hello sample copies data from an SAP Business Warehouse instance tooan Azure blob hourly.</span></span> <span data-ttu-id="1f62d-205">Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="1f62d-205">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="1f62d-206">Instellen als eerste stap Hallo data management gateway.</span><span class="sxs-lookup"><span data-stu-id="1f62d-206">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="1f62d-207">Hallo-instructies vindt u in Hallo [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="1f62d-207">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-business-warehouse-linked-service"></a><span data-ttu-id="1f62d-208">SAP Business Warehouse gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="1f62d-208">SAP Business Warehouse linked service</span></span>
<span data-ttu-id="1f62d-209">Deze gekoppelde service wordt uw exemplaar voor SAP BW toohello gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="1f62d-209">This linked service links your SAP BW instance toohello data factory.</span></span> <span data-ttu-id="1f62d-210">Hallo type wordt ingesteld te**SapBw**.</span><span class="sxs-lookup"><span data-stu-id="1f62d-210">hello type property is set too**SapBw**.</span></span> <span data-ttu-id="1f62d-211">Hallo typeProperties sectie bevat verbindingsinformatie voor Hallo SAP BW-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="1f62d-211">hello typeProperties section provides connection information for hello SAP BW instance.</span></span> 

```json
{
    "name": "SapBwLinkedService",
    "properties":
    {
        "type": "SapBw",
        "typeProperties":
        {
            "server": "<server name>",
            "systemNumber": "<system number>",
            "clientId": "<client id>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="1f62d-212">Een gekoppelde Azure Storage-service</span><span class="sxs-lookup"><span data-stu-id="1f62d-212">Azure Storage linked service</span></span>
<span data-ttu-id="1f62d-213">Deze gekoppelde service uw Azure Storage-account toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="1f62d-213">This linked service links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="1f62d-214">Hallo type wordt ingesteld te**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="1f62d-214">hello type property is set too**AzureStorage**.</span></span> <span data-ttu-id="1f62d-215">Hallo typeProperties sectie bevat de verbindingsgegevens voor hello Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="1f62d-215">hello typeProperties section provides connection information for hello Azure Storage account.</span></span>

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

### <a name="sap-bw-input-dataset"></a><span data-ttu-id="1f62d-216">Invoergegevensset voor SAP BW</span><span class="sxs-lookup"><span data-stu-id="1f62d-216">SAP BW input dataset</span></span>
<span data-ttu-id="1f62d-217">Deze gegevensset definieert Hallo SAP Business Warehouse-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="1f62d-217">This dataset defines hello SAP Business Warehouse dataset.</span></span> <span data-ttu-id="1f62d-218">U stelt Hallo Hallo Data Factory-gegevensset te**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="1f62d-218">You set hello type of hello Data Factory dataset too**RelationalTable**.</span></span> <span data-ttu-id="1f62d-219">Op dit moment kunt opgeeft u geen type-specifieke eigenschappen voor een gegevensset SAP BW.</span><span class="sxs-lookup"><span data-stu-id="1f62d-219">Currently, you do not specify any type-specific properties for an SAP BW dataset.</span></span> <span data-ttu-id="1f62d-220">Hallo-query in Hallo Kopieeractiviteit definitie geeft aan welke gegevens tooread van Hallo SAP BW-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="1f62d-220">hello query in hello Copy Activity definition specifies what data tooread from hello SAP BW instance.</span></span> 

<span data-ttu-id="1f62d-221">Instellen van de eigenschap external tootrue informeert het Hallo Data Factory-service die tabel Hallo externe toohello data factory is en niet wordt geproduceerd door een activiteit in de gegevensfactory Hallo.</span><span class="sxs-lookup"><span data-stu-id="1f62d-221">Setting external property tootrue informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

<span data-ttu-id="1f62d-222">Frequentie en het interval eigenschappen definieert Hallo planning.</span><span class="sxs-lookup"><span data-stu-id="1f62d-222">Frequency and interval properties defines hello schedule.</span></span> <span data-ttu-id="1f62d-223">In dit geval Hallo gegevens gelezen uit Hallo SAP BW exemplaar per uur.</span><span class="sxs-lookup"><span data-stu-id="1f62d-223">In this case, hello data is read from hello SAP BW instance hourly.</span></span> 

```json
{
    "name": "SapBwDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapBwLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```



### <a name="azure-blob-output-dataset"></a><span data-ttu-id="1f62d-224">Azure Blob-uitvoergegevensset</span><span class="sxs-lookup"><span data-stu-id="1f62d-224">Azure Blob output dataset</span></span>
<span data-ttu-id="1f62d-225">Deze gegevensset definieert Hallo uitvoer Azure Blob-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="1f62d-225">This dataset defines hello output Azure Blob dataset.</span></span> <span data-ttu-id="1f62d-226">de eigenschap type Hallo is tooAzureBlob ingesteld.</span><span class="sxs-lookup"><span data-stu-id="1f62d-226">hello type property is set tooAzureBlob.</span></span> <span data-ttu-id="1f62d-227">Hallo bevat typeProperties waar Hallo gegevens gekopieerd vanaf Hallo SAP BW-exemplaar worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="1f62d-227">hello typeProperties section provides where hello data copied from hello SAP BW instance is stored.</span></span> <span data-ttu-id="1f62d-228">Hallo-gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="1f62d-228">hello data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="1f62d-229">pad naar map voor blob Hallo Hallo wordt dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="1f62d-229">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="1f62d-230">Hallo mappad jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1f62d-230">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/sapbw/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="1f62d-231">Pijplijn met de kopieeractiviteit</span><span class="sxs-lookup"><span data-stu-id="1f62d-231">Pipeline with Copy activity</span></span>
<span data-ttu-id="1f62d-232">Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur.</span><span class="sxs-lookup"><span data-stu-id="1f62d-232">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="1f62d-233">Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**RelationalSource** (voor SAP BW-bron) en **sink** type is ingesteld, te**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="1f62d-233">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** (for SAP BW source) and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="1f62d-234">Hallo-query is opgegeven voor Hallo **query** eigenschap Hallo gegevens selecteert in Hallo voorbij toocopy uur.</span><span class="sxs-lookup"><span data-stu-id="1f62d-234">hello query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopySapBwToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<MDX query for SAP BW>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapBwDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDataSet"
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
                "name": "SapBwToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```



### <a name="type-mapping-for-sap-bw"></a><span data-ttu-id="1f62d-235">Toewijzing van het type voor SAP BW</span><span class="sxs-lookup"><span data-stu-id="1f62d-235">Type mapping for SAP BW</span></span>
<span data-ttu-id="1f62d-236">Zoals vermeld in Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel kopieeractiviteit voert automatische typeconversies van brontypen typen toosink Hello benadering in twee stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="1f62d-236">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="1f62d-237">Systeemeigen bron typen too.NET type converteren</span><span class="sxs-lookup"><span data-stu-id="1f62d-237">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="1f62d-238">Converteren van .NET-type toonative sink-type</span><span class="sxs-lookup"><span data-stu-id="1f62d-238">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="1f62d-239">Bij het verplaatsen van gegevens uit SAP BW, worden volgende toewijzingen Hallo uit SAP BW typen too.NET typen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="1f62d-239">When moving data from SAP BW, hello following mappings are used from SAP BW types too.NET types.</span></span>

<span data-ttu-id="1f62d-240">Het gegevenstype in Hallo ABAP woordenlijst</span><span class="sxs-lookup"><span data-stu-id="1f62d-240">Data type in hello ABAP Dictionary</span></span> | <span data-ttu-id="1f62d-241">.NET-gegevenstype</span><span class="sxs-lookup"><span data-stu-id="1f62d-241">.Net Data Type</span></span>
-------------------------------- | --------------
<span data-ttu-id="1f62d-242">ACCP</span><span class="sxs-lookup"><span data-stu-id="1f62d-242">ACCP</span></span> |  <span data-ttu-id="1f62d-243">int</span><span class="sxs-lookup"><span data-stu-id="1f62d-243">Int</span></span>
<span data-ttu-id="1f62d-244">CHAR</span><span class="sxs-lookup"><span data-stu-id="1f62d-244">CHAR</span></span> | <span data-ttu-id="1f62d-245">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="1f62d-245">String</span></span>
<span data-ttu-id="1f62d-246">CLNT</span><span class="sxs-lookup"><span data-stu-id="1f62d-246">CLNT</span></span> | <span data-ttu-id="1f62d-247">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="1f62d-247">String</span></span>
<span data-ttu-id="1f62d-248">VAL</span><span class="sxs-lookup"><span data-stu-id="1f62d-248">CURR</span></span> | <span data-ttu-id="1f62d-249">Decimale</span><span class="sxs-lookup"><span data-stu-id="1f62d-249">Decimal</span></span>
<span data-ttu-id="1f62d-250">CUKY</span><span class="sxs-lookup"><span data-stu-id="1f62d-250">CUKY</span></span> | <span data-ttu-id="1f62d-251">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="1f62d-251">String</span></span>
<span data-ttu-id="1f62d-252">DECEMBER</span><span class="sxs-lookup"><span data-stu-id="1f62d-252">DEC</span></span> | <span data-ttu-id="1f62d-253">Decimale</span><span class="sxs-lookup"><span data-stu-id="1f62d-253">Decimal</span></span>
<span data-ttu-id="1f62d-254">FLTP</span><span class="sxs-lookup"><span data-stu-id="1f62d-254">FLTP</span></span> | <span data-ttu-id="1f62d-255">dubbele</span><span class="sxs-lookup"><span data-stu-id="1f62d-255">Double</span></span>
<span data-ttu-id="1f62d-256">INT1</span><span class="sxs-lookup"><span data-stu-id="1f62d-256">INT1</span></span> | <span data-ttu-id="1f62d-257">Byte</span><span class="sxs-lookup"><span data-stu-id="1f62d-257">Byte</span></span>
<span data-ttu-id="1f62d-258">INT2</span><span class="sxs-lookup"><span data-stu-id="1f62d-258">INT2</span></span> | <span data-ttu-id="1f62d-259">Int16</span><span class="sxs-lookup"><span data-stu-id="1f62d-259">Int16</span></span>
<span data-ttu-id="1f62d-260">INT4</span><span class="sxs-lookup"><span data-stu-id="1f62d-260">INT4</span></span> | <span data-ttu-id="1f62d-261">int</span><span class="sxs-lookup"><span data-stu-id="1f62d-261">Int</span></span>
<span data-ttu-id="1f62d-262">LANG</span><span class="sxs-lookup"><span data-stu-id="1f62d-262">LANG</span></span> | <span data-ttu-id="1f62d-263">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="1f62d-263">String</span></span>
<span data-ttu-id="1f62d-264">LCHR</span><span class="sxs-lookup"><span data-stu-id="1f62d-264">LCHR</span></span> | <span data-ttu-id="1f62d-265">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="1f62d-265">String</span></span>
<span data-ttu-id="1f62d-266">LRAW</span><span class="sxs-lookup"><span data-stu-id="1f62d-266">LRAW</span></span> | <span data-ttu-id="1f62d-267">Byte]</span><span class="sxs-lookup"><span data-stu-id="1f62d-267">Byte[]</span></span>
<span data-ttu-id="1f62d-268">PREC</span><span class="sxs-lookup"><span data-stu-id="1f62d-268">PREC</span></span> | <span data-ttu-id="1f62d-269">Int16</span><span class="sxs-lookup"><span data-stu-id="1f62d-269">Int16</span></span>
<span data-ttu-id="1f62d-270">QUAN</span><span class="sxs-lookup"><span data-stu-id="1f62d-270">QUAN</span></span> | <span data-ttu-id="1f62d-271">Decimale</span><span class="sxs-lookup"><span data-stu-id="1f62d-271">Decimal</span></span>
<span data-ttu-id="1f62d-272">ONBEWERKTE</span><span class="sxs-lookup"><span data-stu-id="1f62d-272">RAW</span></span> | <span data-ttu-id="1f62d-273">Byte]</span><span class="sxs-lookup"><span data-stu-id="1f62d-273">Byte[]</span></span>
<span data-ttu-id="1f62d-274">RAWSTRING</span><span class="sxs-lookup"><span data-stu-id="1f62d-274">RAWSTRING</span></span> | <span data-ttu-id="1f62d-275">Byte]</span><span class="sxs-lookup"><span data-stu-id="1f62d-275">Byte[]</span></span>
<span data-ttu-id="1f62d-276">TEKENREEKS</span><span class="sxs-lookup"><span data-stu-id="1f62d-276">STRING</span></span> | <span data-ttu-id="1f62d-277">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="1f62d-277">String</span></span>
<span data-ttu-id="1f62d-278">EENHEID</span><span class="sxs-lookup"><span data-stu-id="1f62d-278">UNIT</span></span> | <span data-ttu-id="1f62d-279">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="1f62d-279">String</span></span>
<span data-ttu-id="1f62d-280">DATS</span><span class="sxs-lookup"><span data-stu-id="1f62d-280">DATS</span></span> | <span data-ttu-id="1f62d-281">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="1f62d-281">String</span></span>
<span data-ttu-id="1f62d-282">NUMC</span><span class="sxs-lookup"><span data-stu-id="1f62d-282">NUMC</span></span> | <span data-ttu-id="1f62d-283">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="1f62d-283">String</span></span>
<span data-ttu-id="1f62d-284">TIM 'S</span><span class="sxs-lookup"><span data-stu-id="1f62d-284">TIMS</span></span> | <span data-ttu-id="1f62d-285">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="1f62d-285">String</span></span>

> [!NOTE]
> <span data-ttu-id="1f62d-286">toomap kolommen uit de bron gegevensset toocolumns uit sink gegevensset, Zie [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="1f62d-286">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="map-source-toosink-columns"></a><span data-ttu-id="1f62d-287">Bronkolommen toosink toewijzen</span><span class="sxs-lookup"><span data-stu-id="1f62d-287">Map source toosink columns</span></span>
<span data-ttu-id="1f62d-288">Zie toolearn over het toewijzen van kolommen in bron gegevensset toocolumns in sink-gegevensset [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="1f62d-288">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="1f62d-289">Herhaalbare leesbewerking van relationele bronnen</span><span class="sxs-lookup"><span data-stu-id="1f62d-289">Repeatable read from relational sources</span></span>
<span data-ttu-id="1f62d-290">Houd bij het kopiëren van gegevens uit een relationele gegevensopslag, herhaalbaarheid rekening tooavoid ongewenste resultaten.</span><span class="sxs-lookup"><span data-stu-id="1f62d-290">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="1f62d-291">In Azure Data Factory, kunt u een segment handmatig opnieuw.</span><span class="sxs-lookup"><span data-stu-id="1f62d-291">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="1f62d-292">U kunt ook een beleid voor opnieuw proberen voor een gegevensset configureren zodat een segment wordt opnieuw uitgevoerd wanneer een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="1f62d-292">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="1f62d-293">Wanneer een segment opnieuw in beide gevallen wordt uitgevoerd, moet u ervoor dat dezelfde gegevens Hallo toomake wordt gelezen ongeacht hoe vaak een segment wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1f62d-293">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="1f62d-294">Zie [Repeatable van relationele bronnen lezen](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="1f62d-294">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="1f62d-295">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="1f62d-295">Performance and Tuning</span></span>
<span data-ttu-id="1f62d-296">Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.</span><span class="sxs-lookup"><span data-stu-id="1f62d-296">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
