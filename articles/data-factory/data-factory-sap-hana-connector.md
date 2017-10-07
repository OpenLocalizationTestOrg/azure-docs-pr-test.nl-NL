---
title: aaaMove gegevens uit de SAP HANA met behulp van Azure Data Factory | Microsoft Docs
description: Meer informatie over het toomove gegevens uit de SAP HANA met behulp van Azure Data Factory.
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
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 5cefe4c8ed01ea4e86e02496b2f8a9083d0b949c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-sap-hana-using-azure-data-factory"></a><span data-ttu-id="65731-103">Verplaatsen van gegevens uit SAP HANA, met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="65731-103">Move data From SAP HANA using Azure Data Factory</span></span>
<span data-ttu-id="65731-104">Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit in Azure Data Factory toomove gegevens uit een lokale SAP HANA Hallo.</span><span class="sxs-lookup"><span data-stu-id="65731-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises SAP HANA.</span></span> <span data-ttu-id="65731-105">Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.</span><span class="sxs-lookup"><span data-stu-id="65731-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="65731-106">U kunt gegevens uit een on-premises SAP HANA store tooany ondersteund sink gegevens gegevensopslag kopiëren.</span><span class="sxs-lookup"><span data-stu-id="65731-106">You can copy data from an on-premises SAP HANA data store tooany supported sink data store.</span></span> <span data-ttu-id="65731-107">Zie voor een lijst van gegevens winkels ondersteund zoals sinks door kopieeractiviteit hello, Hallo [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel.</span><span class="sxs-lookup"><span data-stu-id="65731-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="65731-108">Data factory ondersteunt momenteel alleen verplaatsen van gegevens uit een SAP HANA tooother gegevens worden opgeslagen, maar niet voor SAP HANA tooan verplaatsen van gegevens van andere gegevens worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="65731-108">Data factory currently supports only moving data from an SAP HANA tooother data stores, but not for moving data from other data stores tooan SAP HANA.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="65731-109">Ondersteunde versies en installatie</span><span class="sxs-lookup"><span data-stu-id="65731-109">Supported versions and installation</span></span>
<span data-ttu-id="65731-110">Deze connector ondersteunt een willekeurige versie van de SAP HANA-database.</span><span class="sxs-lookup"><span data-stu-id="65731-110">This connector supports any version of SAP HANA database.</span></span> <span data-ttu-id="65731-111">Het ondersteunt kopiëren van gegevens van HANA informatiemodellen (zoals weergaven, analyse en berekening) en rij/kolom tabellen met behulp van SQL-query's.</span><span class="sxs-lookup"><span data-stu-id="65731-111">It supports copying data from HANA information models (such as Analytic and Calculation views) and Row/Column tables using SQL queries.</span></span>

<span data-ttu-id="65731-112">tooenable hello connectiviteit toohello SAP HANA-exemplaar installeren Hallo volgende onderdelen:</span><span class="sxs-lookup"><span data-stu-id="65731-112">tooenable hello connectivity toohello SAP HANA instance, install hello following components:</span></span>
- <span data-ttu-id="65731-113">**Data Management Gateway**: Data Factory-service ondersteunt verbindingen van tooon-premises gegevens winkels (inclusief SAP HANA) met een onderdeel genaamd Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="65731-113">**Data Management Gateway**: Data Factory service supports connecting tooon-premises data stores (including SAP HANA) using a component called Data Management Gateway.</span></span> <span data-ttu-id="65731-114">toolearn over Data Management Gateway en stapsgewijze instructies voor het instellen van Hallo-gateway, Zie [verplaatsen tussen on-premises gegevens gegevensarchief gegevensarchief toocloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="65731-114">toolearn about Data Management Gateway and step-by-step instructions for setting up hello gateway, see [Moving data between on-premises data store toocloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="65731-115">Gateway is vereist, zelfs als Hallo SAP HANA wordt gehost in een Azure IaaS virtuele machine (VM).</span><span class="sxs-lookup"><span data-stu-id="65731-115">Gateway is required even if hello SAP HANA is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="65731-116">U kunt Hallo gateway installeren op Hallo dezelfde virtuele machine als Hallo gegevens opslaan of op een andere virtuele machine zo lang Hallo gateway kunt verbinding maken met toohello-database.</span><span class="sxs-lookup"><span data-stu-id="65731-116">You can install hello gateway on hello same VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>
- <span data-ttu-id="65731-117">**SAP HANA ODBC-stuurprogramma** op Hallo gateway-apparaat.</span><span class="sxs-lookup"><span data-stu-id="65731-117">**SAP HANA ODBC driver** on hello gateway machine.</span></span> <span data-ttu-id="65731-118">U kunt Hallo SAP HANA ODBC-stuurprogramma downloaden van Hallo [SAP Software Download Center](https://support.sap.com/swdc).</span><span class="sxs-lookup"><span data-stu-id="65731-118">You can download hello SAP HANA ODBC driver from hello [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="65731-119">Zoeken met trefwoorden Hallo **SAP HANA-CLIENT voor Windows**.</span><span class="sxs-lookup"><span data-stu-id="65731-119">Search with hello keyword **SAP HANA CLIENT for Windows**.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="65731-120">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="65731-120">Getting started</span></span>
<span data-ttu-id="65731-121">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens vanuit een on-premises Cassandra-gegevensopslag verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="65731-121">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="65731-122">Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="65731-122">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="65731-123">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="65731-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="65731-124">U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="65731-124">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="65731-125">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="65731-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="65731-126">Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="65731-126">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="65731-127">Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="65731-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="65731-128">Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="65731-128">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="65731-129">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="65731-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="65731-130">Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="65731-130">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="65731-131">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="65731-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="65731-132">Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens uit een lokale SAP HANA zijn [JSON-voorbeeld: gegevens kopiëren van SAP HANA tooAzure Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="65731-132">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises SAP HANA, see [JSON example: Copy data from SAP HANA tooAzure Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="65731-133">Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooan SAP HANA-gegevensarchief zijn:</span><span class="sxs-lookup"><span data-stu-id="65731-133">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooan SAP HANA data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="65731-134">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="65731-134">Linked service properties</span></span>
<span data-ttu-id="65731-135">Hallo volgende tabel bevat de beschrijving voor JSON-elementen specifieke tooSAP HANA gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="65731-135">hello following table provides description for JSON elements specific tooSAP HANA linked service.</span></span>

<span data-ttu-id="65731-136">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="65731-136">Property</span></span> | <span data-ttu-id="65731-137">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="65731-137">Description</span></span> | <span data-ttu-id="65731-138">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="65731-138">Allowed values</span></span> | <span data-ttu-id="65731-139">Vereist</span><span class="sxs-lookup"><span data-stu-id="65731-139">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="65731-140">server</span><span class="sxs-lookup"><span data-stu-id="65731-140">server</span></span> | <span data-ttu-id="65731-141">Naam van het Hallo-server op welke Hallo SAP HANA exemplaar zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="65731-141">Name of hello server on which hello SAP HANA instance resides.</span></span> <span data-ttu-id="65731-142">Als de server een aangepaste poort gebruikt is, geeft u `server:port`.</span><span class="sxs-lookup"><span data-stu-id="65731-142">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="65731-143">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="65731-143">string</span></span> | <span data-ttu-id="65731-144">Ja</span><span class="sxs-lookup"><span data-stu-id="65731-144">Yes</span></span>
<span data-ttu-id="65731-145">authenticationType</span><span class="sxs-lookup"><span data-stu-id="65731-145">authenticationType</span></span> | <span data-ttu-id="65731-146">Het type verificatie.</span><span class="sxs-lookup"><span data-stu-id="65731-146">Type of authentication.</span></span> | <span data-ttu-id="65731-147">De tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="65731-147">string.</span></span> <span data-ttu-id="65731-148">'Basic' of 'Windows'</span><span class="sxs-lookup"><span data-stu-id="65731-148">"Basic" or "Windows"</span></span> | <span data-ttu-id="65731-149">Ja</span><span class="sxs-lookup"><span data-stu-id="65731-149">Yes</span></span> 
<span data-ttu-id="65731-150">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="65731-150">username</span></span> | <span data-ttu-id="65731-151">Naam van het Hallo-gebruiker met toegang toohello SAP-server</span><span class="sxs-lookup"><span data-stu-id="65731-151">Name of hello user who has access toohello SAP server</span></span> | <span data-ttu-id="65731-152">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="65731-152">string</span></span> | <span data-ttu-id="65731-153">Ja</span><span class="sxs-lookup"><span data-stu-id="65731-153">Yes</span></span>
<span data-ttu-id="65731-154">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="65731-154">password</span></span> | <span data-ttu-id="65731-155">Wachtwoord voor gebruiker Hallo.</span><span class="sxs-lookup"><span data-stu-id="65731-155">Password for hello user.</span></span> | <span data-ttu-id="65731-156">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="65731-156">string</span></span> | <span data-ttu-id="65731-157">Ja</span><span class="sxs-lookup"><span data-stu-id="65731-157">Yes</span></span>
<span data-ttu-id="65731-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="65731-158">gatewayName</span></span> | <span data-ttu-id="65731-159">Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello lokale SAP HANA-exemplaar gebruiken.</span><span class="sxs-lookup"><span data-stu-id="65731-159">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SAP HANA instance.</span></span> | <span data-ttu-id="65731-160">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="65731-160">string</span></span> | <span data-ttu-id="65731-161">Ja</span><span class="sxs-lookup"><span data-stu-id="65731-161">Yes</span></span>
<span data-ttu-id="65731-162">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="65731-162">encryptedCredential</span></span> | <span data-ttu-id="65731-163">Hallo versleutelde referentie-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="65731-163">hello encrypted credential string.</span></span> | <span data-ttu-id="65731-164">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="65731-164">string</span></span> | <span data-ttu-id="65731-165">Nee</span><span class="sxs-lookup"><span data-stu-id="65731-165">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="65731-166">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="65731-166">Dataset properties</span></span>
<span data-ttu-id="65731-167">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="65731-167">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="65731-168">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).</span><span class="sxs-lookup"><span data-stu-id="65731-168">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="65731-169">Hallo **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="65731-169">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="65731-170">Er zijn geen type-specifieke eigenschappen ondersteund voor SAP HANA-gegevensset Hallo van het type **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="65731-170">There are no type-specific properties supported for hello SAP HANA dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="65731-171">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="65731-171">Copy activity properties</span></span>
<span data-ttu-id="65731-172">Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="65731-172">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="65731-173">Eigenschappen zoals naam, beschrijving, invoer en uitvoer tabellen, zijn de beleidsregels zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="65731-173">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="65731-174">Dat eigenschappen beschikbaar zijn in Hallo **typeProperties** sectie van de activiteit Hallo variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="65731-174">Whereas, properties available in hello **typeProperties** section of hello activity vary with each activity type.</span></span> <span data-ttu-id="65731-175">Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="65731-175">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="65731-176">Wanneer u de gegevensbron in de kopieerbewerking is van het type **RelationalSource** (waaronder SAP HANA), Hallo volgende eigenschappen beschikbaar zijn in de sectie typeProperties:</span><span class="sxs-lookup"><span data-stu-id="65731-176">When source in copy activity is of type **RelationalSource** (which includes SAP HANA), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="65731-177">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="65731-177">Property</span></span> | <span data-ttu-id="65731-178">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="65731-178">Description</span></span> | <span data-ttu-id="65731-179">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="65731-179">Allowed values</span></span> | <span data-ttu-id="65731-180">Vereist</span><span class="sxs-lookup"><span data-stu-id="65731-180">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="65731-181">query</span><span class="sxs-lookup"><span data-stu-id="65731-181">query</span></span> | <span data-ttu-id="65731-182">Hiermee geeft u Hallo SQL query tooread gegevens van Hallo SAP HANA-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="65731-182">Specifies hello SQL query tooread data from hello SAP HANA instance.</span></span> | <span data-ttu-id="65731-183">SQL-query.</span><span class="sxs-lookup"><span data-stu-id="65731-183">SQL query.</span></span> | <span data-ttu-id="65731-184">Ja</span><span class="sxs-lookup"><span data-stu-id="65731-184">Yes</span></span> |

## <a name="json-example-copy-data-from-sap-hana-tooazure-blob"></a><span data-ttu-id="65731-185">JSON-voorbeeld: gegevens uit een SAP HANA tooAzure Blob kopiëren</span><span class="sxs-lookup"><span data-stu-id="65731-185">JSON example: Copy data from SAP HANA tooAzure Blob</span></span>
<span data-ttu-id="65731-186">Hallo volgende voorbeeld vindt u voorbeeld JSON definities waarmee u een pijplijn toocreate kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="65731-186">hello following sample provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="65731-187">In dit voorbeeld laat zien hoe toocopy gegevens uit een lokale SAP HANA tooan Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="65731-187">This sample shows how toocopy data from an on-premises SAP HANA tooan Azure Blob Storage.</span></span> <span data-ttu-id="65731-188">Echter, de gegevens kunnen worden gekopieerd **rechtstreeks** tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="65731-188">However, data can be copied **directly** tooany of hello sinks listed [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="65731-189">Dit voorbeeld bevat JSON-fragmenten.</span><span class="sxs-lookup"><span data-stu-id="65731-189">This sample provides JSON snippets.</span></span> <span data-ttu-id="65731-190">Dit omvat geen stapsgewijze instructies voor het maken van de gegevensfactory Hallo.</span><span class="sxs-lookup"><span data-stu-id="65731-190">It does not include step-by-step instructions for creating hello data factory.</span></span> <span data-ttu-id="65731-191">Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor stapsgewijze instructies.</span><span class="sxs-lookup"><span data-stu-id="65731-191">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="65731-192">Hallo voorbeeld heeft Hallo data factory-entiteiten te volgen:</span><span class="sxs-lookup"><span data-stu-id="65731-192">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="65731-193">Een gekoppelde service van het type [SapHana](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="65731-193">A linked service of type [SapHana](#linked-service-properties).</span></span>
2. <span data-ttu-id="65731-194">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="65731-194">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="65731-195">Invoer [gegevensset](data-factory-create-datasets.md) van het type [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="65731-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="65731-196">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="65731-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="65731-197">Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [RelationalSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="65731-197">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="65731-198">Hallo voorbeeld gegevens worden gekopieerd van een SAP HANA-exemplaar tooan Azure blob per uur.</span><span class="sxs-lookup"><span data-stu-id="65731-198">hello sample copies data from an SAP HANA instance tooan Azure blob hourly.</span></span> <span data-ttu-id="65731-199">Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="65731-199">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="65731-200">Instellen als eerste stap Hallo data management gateway.</span><span class="sxs-lookup"><span data-stu-id="65731-200">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="65731-201">Hallo-instructies vindt u in Hallo [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="65731-201">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-hana-linked-service"></a><span data-ttu-id="65731-202">SAP HANA gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="65731-202">SAP HANA linked service</span></span>
<span data-ttu-id="65731-203">Deze gekoppelde service wordt uw exemplaar voor SAP HANA toohello gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="65731-203">This linked service links your SAP HANA instance toohello data factory.</span></span> <span data-ttu-id="65731-204">Hallo type wordt ingesteld te**SapHana**.</span><span class="sxs-lookup"><span data-stu-id="65731-204">hello type property is set too**SapHana**.</span></span> <span data-ttu-id="65731-205">Hallo typeProperties sectie bevat verbindingsinformatie voor Hallo SAP HANA-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="65731-205">hello typeProperties section provides connection information for hello SAP HANA instance.</span></span>

```json
{
    "name": "SapHanaLinkedService",
    "properties":
    {
        "type": "SapHana",
        "typeProperties":
        {
            "server": "<server name>",
            "authenticationType": "<Basic, or Windows>",
            "username": "<SAP user>",
            "password": "<Password for SAP user>",
            "gatewayName": "<gateway name>"
        }
    }
}

```

### <a name="azure-storage-linked-service"></a><span data-ttu-id="65731-206">Een gekoppelde Azure Storage-service</span><span class="sxs-lookup"><span data-stu-id="65731-206">Azure Storage linked service</span></span>
<span data-ttu-id="65731-207">Deze gekoppelde service uw Azure Storage-account toohello data factory.</span><span class="sxs-lookup"><span data-stu-id="65731-207">This linked service links your Azure Storage account toohello data factory.</span></span> <span data-ttu-id="65731-208">Hallo type wordt ingesteld te**AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="65731-208">hello type property is set too**AzureStorage**.</span></span> <span data-ttu-id="65731-209">Hallo typeProperties sectie bevat de verbindingsgegevens voor hello Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="65731-209">hello typeProperties section provides connection information for hello Azure Storage account.</span></span>

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

### <a name="sap-hana-input-dataset"></a><span data-ttu-id="65731-210">SAP HANA-invoergegevensset</span><span class="sxs-lookup"><span data-stu-id="65731-210">SAP HANA input dataset</span></span>

<span data-ttu-id="65731-211">Deze gegevensset definieert Hallo SAP HANA-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="65731-211">This dataset defines hello SAP HANA dataset.</span></span> <span data-ttu-id="65731-212">U stelt Hallo Hallo Data Factory-gegevensset te**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="65731-212">You set hello type of hello Data Factory dataset too**RelationalTable**.</span></span> <span data-ttu-id="65731-213">Op dit moment kunt opgeeft u geen type-specifieke eigenschappen voor een SAP HANA-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="65731-213">Currently, you do not specify any type-specific properties for an SAP HANA dataset.</span></span> <span data-ttu-id="65731-214">Hallo-query in Hallo Kopieeractiviteit definitie geeft aan welke gegevens tooread van Hallo SAP HANA-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="65731-214">hello query in hello Copy Activity definition specifies what data tooread from hello SAP HANA instance.</span></span> 

<span data-ttu-id="65731-215">Instellen van de eigenschap external tootrue informeert het Hallo Data Factory-service die tabel Hallo externe toohello data factory is en niet wordt geproduceerd door een activiteit in de gegevensfactory Hallo.</span><span class="sxs-lookup"><span data-stu-id="65731-215">Setting external property tootrue informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

<span data-ttu-id="65731-216">Frequentie en het interval eigenschappen definieert Hallo planning.</span><span class="sxs-lookup"><span data-stu-id="65731-216">Frequency and interval properties defines hello schedule.</span></span> <span data-ttu-id="65731-217">In dit geval Hallo gegevens gelezen uit Hallo SAP HANA exemplaar per uur.</span><span class="sxs-lookup"><span data-stu-id="65731-217">In this case, hello data is read from hello SAP HANA instance hourly.</span></span> 

```json
{
    "name": "SapHanaDataset",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "SapHanaLinkedService",
        "typeProperties": {},
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="65731-218">Azure Blob-uitvoergegevensset</span><span class="sxs-lookup"><span data-stu-id="65731-218">Azure Blob output dataset</span></span>
<span data-ttu-id="65731-219">Deze gegevensset definieert Hallo uitvoer Azure Blob-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="65731-219">This dataset defines hello output Azure Blob dataset.</span></span> <span data-ttu-id="65731-220">de eigenschap type Hallo is tooAzureBlob ingesteld.</span><span class="sxs-lookup"><span data-stu-id="65731-220">hello type property is set tooAzureBlob.</span></span> <span data-ttu-id="65731-221">Hallo bevat typeProperties waar Hallo gegevens gekopieerd vanaf Hallo SAP HANA-exemplaar worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="65731-221">hello typeProperties section provides where hello data copied from hello SAP HANA instance is stored.</span></span> <span data-ttu-id="65731-222">Hallo-gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="65731-222">hello data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="65731-223">pad naar map voor blob Hallo Hallo wordt dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="65731-223">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="65731-224">Hallo mappad jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="65731-224">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/saphana/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="65731-225">Pijplijn met de kopieeractiviteit</span><span class="sxs-lookup"><span data-stu-id="65731-225">Pipeline with Copy activity</span></span>

<span data-ttu-id="65731-226">Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur.</span><span class="sxs-lookup"><span data-stu-id="65731-226">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="65731-227">Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**RelationalSource** (voor SAP HANA-bron) en **sink** type is ingesteld, te**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="65731-227">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** (for SAP HANA source) and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="65731-228">Hallo SQL-query is opgegeven voor Hallo **query** eigenschap Hallo gegevens selecteert in Hallo voorbij toocopy uur.</span><span class="sxs-lookup"><span data-stu-id="65731-228">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopySapHanaToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "<SQL Query for HANA>"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "SapHanaDataset"
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
                "name": "SapHanaToBlob"
            }
        ],
        "start": "2017-03-01T18:00:00Z",
        "end": "2017-03-01T19:00:00Z"
    }
}
```


### <a name="type-mapping-for-sap-hana"></a><span data-ttu-id="65731-229">Toewijzing van het type voor SAP HANA</span><span class="sxs-lookup"><span data-stu-id="65731-229">Type mapping for SAP HANA</span></span>
<span data-ttu-id="65731-230">Zoals vermeld in Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel kopieeractiviteit voert automatische typeconversies van brontypen typen toosink Hello benadering in twee stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="65731-230">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="65731-231">Systeemeigen bron typen too.NET type converteren</span><span class="sxs-lookup"><span data-stu-id="65731-231">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="65731-232">Converteren van .NET-type toonative sink-type</span><span class="sxs-lookup"><span data-stu-id="65731-232">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="65731-233">Bij het verplaatsen van gegevens uit een SAP HANA, worden uit SAP HANA typen too.NET typen Hallo volgende toewijzingen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="65731-233">When moving data from SAP HANA, hello following mappings are used from SAP HANA types too.NET types.</span></span>

<span data-ttu-id="65731-234">SAP HANA-Type</span><span class="sxs-lookup"><span data-stu-id="65731-234">SAP HANA Type</span></span> | <span data-ttu-id="65731-235">.NET op basis van Type</span><span class="sxs-lookup"><span data-stu-id="65731-235">.NET Based Type</span></span>
------------- | ---------------
<span data-ttu-id="65731-236">TINYINT</span><span class="sxs-lookup"><span data-stu-id="65731-236">TINYINT</span></span> | <span data-ttu-id="65731-237">Byte</span><span class="sxs-lookup"><span data-stu-id="65731-237">Byte</span></span>
<span data-ttu-id="65731-238">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="65731-238">SMALLINT</span></span> | <span data-ttu-id="65731-239">Int16</span><span class="sxs-lookup"><span data-stu-id="65731-239">Int16</span></span>
<span data-ttu-id="65731-240">INT</span><span class="sxs-lookup"><span data-stu-id="65731-240">INT</span></span> | <span data-ttu-id="65731-241">Int32</span><span class="sxs-lookup"><span data-stu-id="65731-241">Int32</span></span>
<span data-ttu-id="65731-242">BIGINT</span><span class="sxs-lookup"><span data-stu-id="65731-242">BIGINT</span></span> | <span data-ttu-id="65731-243">Int64</span><span class="sxs-lookup"><span data-stu-id="65731-243">Int64</span></span>
<span data-ttu-id="65731-244">ECHTE</span><span class="sxs-lookup"><span data-stu-id="65731-244">REAL</span></span> | <span data-ttu-id="65731-245">Één</span><span class="sxs-lookup"><span data-stu-id="65731-245">Single</span></span>
<span data-ttu-id="65731-246">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="65731-246">DOUBLE</span></span> | <span data-ttu-id="65731-247">Één</span><span class="sxs-lookup"><span data-stu-id="65731-247">Single</span></span>
<span data-ttu-id="65731-248">DECIMALE</span><span class="sxs-lookup"><span data-stu-id="65731-248">DECIMAL</span></span> | <span data-ttu-id="65731-249">Decimale</span><span class="sxs-lookup"><span data-stu-id="65731-249">Decimal</span></span>
<span data-ttu-id="65731-250">BOOLEAANSE WAARDE</span><span class="sxs-lookup"><span data-stu-id="65731-250">BOOLEAN</span></span> | <span data-ttu-id="65731-251">Byte</span><span class="sxs-lookup"><span data-stu-id="65731-251">Byte</span></span>
<span data-ttu-id="65731-252">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="65731-252">VARCHAR</span></span> | <span data-ttu-id="65731-253">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="65731-253">String</span></span>
<span data-ttu-id="65731-254">NVARCHAR</span><span class="sxs-lookup"><span data-stu-id="65731-254">NVARCHAR</span></span> | <span data-ttu-id="65731-255">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="65731-255">String</span></span>
<span data-ttu-id="65731-256">CLOB</span><span class="sxs-lookup"><span data-stu-id="65731-256">CLOB</span></span> | <span data-ttu-id="65731-257">Byte]</span><span class="sxs-lookup"><span data-stu-id="65731-257">Byte[]</span></span>
<span data-ttu-id="65731-258">ALPHANUM</span><span class="sxs-lookup"><span data-stu-id="65731-258">ALPHANUM</span></span> | <span data-ttu-id="65731-259">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="65731-259">String</span></span>
<span data-ttu-id="65731-260">BLOB</span><span class="sxs-lookup"><span data-stu-id="65731-260">BLOB</span></span> | <span data-ttu-id="65731-261">Byte]</span><span class="sxs-lookup"><span data-stu-id="65731-261">Byte[]</span></span>
<span data-ttu-id="65731-262">DATUM</span><span class="sxs-lookup"><span data-stu-id="65731-262">DATE</span></span> | <span data-ttu-id="65731-263">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="65731-263">DateTime</span></span>
<span data-ttu-id="65731-264">TIJD</span><span class="sxs-lookup"><span data-stu-id="65731-264">TIME</span></span> | <span data-ttu-id="65731-265">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="65731-265">TimeSpan</span></span>
<span data-ttu-id="65731-266">TIJDSTEMPEL</span><span class="sxs-lookup"><span data-stu-id="65731-266">TIMESTAMP</span></span> | <span data-ttu-id="65731-267">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="65731-267">DateTime</span></span>
<span data-ttu-id="65731-268">SECONDDATE</span><span class="sxs-lookup"><span data-stu-id="65731-268">SECONDDATE</span></span> | <span data-ttu-id="65731-269">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="65731-269">DateTime</span></span>

## <a name="known-limitations"></a><span data-ttu-id="65731-270">Bekende beperkingen</span><span class="sxs-lookup"><span data-stu-id="65731-270">Known limitations</span></span>
<span data-ttu-id="65731-271">Er zijn enkele bekende beperkingen bij het kopiëren van gegevens uit een SAP HANA:</span><span class="sxs-lookup"><span data-stu-id="65731-271">There are a few known limitations when copying data from SAP HANA:</span></span>

- <span data-ttu-id="65731-272">NVARCHAR tekenreeksen zijn afgekapt toomaximum lengte van 4000 Unicode-tekens</span><span class="sxs-lookup"><span data-stu-id="65731-272">NVARCHAR strings are truncated toomaximum length of 4000 Unicode characters</span></span>
- <span data-ttu-id="65731-273">SMALLDECIMAL wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="65731-273">SMALLDECIMAL is not supported</span></span>
- <span data-ttu-id="65731-274">VARBINARY wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="65731-274">VARBINARY is not supported</span></span>
- <span data-ttu-id="65731-275">Geldige datums tussen 12-1899/30 zijn en 12-9999/31</span><span class="sxs-lookup"><span data-stu-id="65731-275">Valid Dates are between 1899/12/30 and 9999/12/31</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="65731-276">Bronkolommen toosink toewijzen</span><span class="sxs-lookup"><span data-stu-id="65731-276">Map source toosink columns</span></span>
<span data-ttu-id="65731-277">Zie toolearn over het toewijzen van kolommen in bron gegevensset toocolumns in sink-gegevensset [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="65731-277">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="65731-278">Herhaalbare leesbewerking van relationele bronnen</span><span class="sxs-lookup"><span data-stu-id="65731-278">Repeatable read from relational sources</span></span>
<span data-ttu-id="65731-279">Houd bij het kopiëren van gegevens uit een relationele gegevensopslag, herhaalbaarheid rekening tooavoid ongewenste resultaten.</span><span class="sxs-lookup"><span data-stu-id="65731-279">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="65731-280">In Azure Data Factory, kunt u een segment handmatig opnieuw.</span><span class="sxs-lookup"><span data-stu-id="65731-280">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="65731-281">U kunt ook een beleid voor opnieuw proberen voor een gegevensset configureren zodat een segment wordt opnieuw uitgevoerd wanneer een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="65731-281">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="65731-282">Wanneer een segment opnieuw in beide gevallen wordt uitgevoerd, moet u ervoor dat dezelfde gegevens Hallo toomake wordt gelezen ongeacht hoe vaak een segment wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="65731-282">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="65731-283">Zie [Repeatable van relationele bronnen lezen](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="65731-283">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="65731-284">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="65731-284">Performance and Tuning</span></span>
<span data-ttu-id="65731-285">Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.</span><span class="sxs-lookup"><span data-stu-id="65731-285">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
