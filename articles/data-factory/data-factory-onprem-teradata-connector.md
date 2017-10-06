---
title: aaaMove gegevens van Teradata met behulp van Azure Data Factory | Microsoft Docs
description: Meer informatie over Teradata-Connector voor Hallo Data Factory-service waarmee u gegevens van de Teradata-Database verplaatsen
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 98eb76d8-5f3d-4667-b76e-e59ed3eea3ae
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: jingwang
ms.openlocfilehash: 79153476157666463b499edaa7585adaf8ad3bee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-teradata-using-azure-data-factory"></a><span data-ttu-id="78e70-103">Verplaatsen van gegevens uit een Teradata met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="78e70-103">Move data from Teradata using Azure Data Factory</span></span>
<span data-ttu-id="78e70-104">Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit Hallo in Azure Data Factory toomove gegevens uit een on-premises Teradata-database.</span><span class="sxs-lookup"><span data-stu-id="78e70-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises Teradata database.</span></span> <span data-ttu-id="78e70-105">Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.</span><span class="sxs-lookup"><span data-stu-id="78e70-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="78e70-106">U kunt gegevens uit een on-premises Teradata gegevens store tooany ondersteund sink gegevensopslag kopiëren.</span><span class="sxs-lookup"><span data-stu-id="78e70-106">You can copy data from an on-premises Teradata data store tooany supported sink data store.</span></span> <span data-ttu-id="78e70-107">Zie voor een lijst van gegevens winkels ondersteund zoals sinks door kopieeractiviteit hello, Hallo [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel.</span><span class="sxs-lookup"><span data-stu-id="78e70-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="78e70-108">Data factory ondersteunt momenteel alleen gegevens uit een Teradata-gegevens opslaan tooother gegevensarchieven verplaatsen, maar niet voor het verplaatsen van gegevens uit andere gegevens winkels tooa Teradata-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="78e70-108">Data factory currently supports only moving data from a Teradata data store tooother data stores, but not for moving data from other data stores tooa Teradata data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="78e70-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="78e70-109">Prerequisites</span></span>
<span data-ttu-id="78e70-110">Data factory ondersteunt verbindende tooon lokale Teradata bronnen via Hallo Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="78e70-110">Data factory supports connecting tooon-premises Teradata sources via hello Data Management Gateway.</span></span> <span data-ttu-id="78e70-111">Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn artikel over Data Management Gateway en stapsgewijze instructies over het instellen van Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="78e70-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span>

<span data-ttu-id="78e70-112">Gateway is vereist, zelfs als hello Teradata wordt gehost door een virtuele machine van Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="78e70-112">Gateway is required even if hello Teradata is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="78e70-113">U kunt Hallo gateway installeren op Hallo dezelfde IaaS VM als Hallo gegevens opslaan of op een andere virtuele machine zo lang Hallo gateway kunt verbinding maken met toohello-database.</span><span class="sxs-lookup"><span data-stu-id="78e70-113">You can install hello gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="78e70-114">Zie [gateway problemen](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) voor tips over het oplossen van verbinding of gateway gerelateerde problemen.</span><span class="sxs-lookup"><span data-stu-id="78e70-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="78e70-115">Ondersteunde versies en installatie</span><span class="sxs-lookup"><span data-stu-id="78e70-115">Supported versions and installation</span></span>
<span data-ttu-id="78e70-116">Data Management Gateway tooconnect toohello Teradata-Database, moet u tooinstall hello [.NET-gegevensprovider voor Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) versie 14 of boven op Hallo hetzelfde systeem als Data Management Gateway Hallo.</span><span class="sxs-lookup"><span data-stu-id="78e70-116">For Data Management Gateway tooconnect toohello Teradata Database, you need tooinstall hello [.NET Data Provider for Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) version 14 or above on hello same system as hello Data Management Gateway.</span></span> <span data-ttu-id="78e70-117">Teradata versie 12 en hoger wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="78e70-117">Teradata version 12 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="78e70-118">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="78e70-118">Getting started</span></span>
<span data-ttu-id="78e70-119">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens vanuit een on-premises Cassandra-gegevensopslag verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="78e70-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="78e70-120">Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="78e70-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="78e70-121">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="78e70-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span> 
- <span data-ttu-id="78e70-122">U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="78e70-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="78e70-123">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="78e70-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="78e70-124">Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="78e70-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="78e70-125">Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="78e70-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="78e70-126">Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="78e70-126">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="78e70-127">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="78e70-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="78e70-128">Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="78e70-128">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="78e70-129">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="78e70-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="78e70-130">Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens uit een on-premises Teradata-gegevensopslag zijn [JSON-voorbeeld: gegevens kopiëren van Teradata tooAzure Blob](#json-example-copy-data-from-teradata-to-azure-blob) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="78e70-130">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an on-premises Teradata data store, see [JSON example: Copy data from Teradata tooAzure Blob](#json-example-copy-data-from-teradata-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="78e70-131">Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooa Teradata-gegevensarchief zijn:</span><span class="sxs-lookup"><span data-stu-id="78e70-131">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooa Teradata data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="78e70-132">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="78e70-132">Linked service properties</span></span>
<span data-ttu-id="78e70-133">Hallo volgende tabel biedt een beschrijving voor de JSON-elementen specifieke tooTeradata gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="78e70-133">hello following table provides description for JSON elements specific tooTeradata linked service.</span></span>

| <span data-ttu-id="78e70-134">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="78e70-134">Property</span></span> | <span data-ttu-id="78e70-135">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="78e70-135">Description</span></span> | <span data-ttu-id="78e70-136">Vereist</span><span class="sxs-lookup"><span data-stu-id="78e70-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="78e70-137">type</span><span class="sxs-lookup"><span data-stu-id="78e70-137">type</span></span> |<span data-ttu-id="78e70-138">Hallo type eigenschap moet worden ingesteld op: **OnPremisesTeradata**</span><span class="sxs-lookup"><span data-stu-id="78e70-138">hello type property must be set to: **OnPremisesTeradata**</span></span> |<span data-ttu-id="78e70-139">Ja</span><span class="sxs-lookup"><span data-stu-id="78e70-139">Yes</span></span> |
| <span data-ttu-id="78e70-140">server</span><span class="sxs-lookup"><span data-stu-id="78e70-140">server</span></span> |<span data-ttu-id="78e70-141">Naam van Hallo Teradata-server.</span><span class="sxs-lookup"><span data-stu-id="78e70-141">Name of hello Teradata server.</span></span> |<span data-ttu-id="78e70-142">Ja</span><span class="sxs-lookup"><span data-stu-id="78e70-142">Yes</span></span> |
| <span data-ttu-id="78e70-143">authenticationType</span><span class="sxs-lookup"><span data-stu-id="78e70-143">authenticationType</span></span> |<span data-ttu-id="78e70-144">Type verificatie gebruikt tooconnect toohello Teradata-database.</span><span class="sxs-lookup"><span data-stu-id="78e70-144">Type of authentication used tooconnect toohello Teradata database.</span></span> <span data-ttu-id="78e70-145">Mogelijke waarden zijn: anoniem, basis en Windows.</span><span class="sxs-lookup"><span data-stu-id="78e70-145">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="78e70-146">Ja</span><span class="sxs-lookup"><span data-stu-id="78e70-146">Yes</span></span> |
| <span data-ttu-id="78e70-147">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="78e70-147">username</span></span> |<span data-ttu-id="78e70-148">Geef de gebruikersnaam als u basisverificatie of Windows-verificatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="78e70-148">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="78e70-149">Nee</span><span class="sxs-lookup"><span data-stu-id="78e70-149">No</span></span> |
| <span data-ttu-id="78e70-150">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="78e70-150">password</span></span> |<span data-ttu-id="78e70-151">Wachtwoord voor gebruikersaccount Hallo die u hebt opgegeven voor Hallo gebruikersnaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="78e70-151">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="78e70-152">Nee</span><span class="sxs-lookup"><span data-stu-id="78e70-152">No</span></span> |
| <span data-ttu-id="78e70-153">gatewayName</span><span class="sxs-lookup"><span data-stu-id="78e70-153">gatewayName</span></span> |<span data-ttu-id="78e70-154">Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello lokale Teradata-database gebruiken.</span><span class="sxs-lookup"><span data-stu-id="78e70-154">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises Teradata database.</span></span> |<span data-ttu-id="78e70-155">Ja</span><span class="sxs-lookup"><span data-stu-id="78e70-155">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="78e70-156">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="78e70-156">Dataset properties</span></span>
<span data-ttu-id="78e70-157">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="78e70-157">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="78e70-158">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).</span><span class="sxs-lookup"><span data-stu-id="78e70-158">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="78e70-159">Hallo **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="78e70-159">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="78e70-160">Er zijn momenteel geen type-eigenschappen voor Hallo Teradata gegevensset ondersteund.</span><span class="sxs-lookup"><span data-stu-id="78e70-160">Currently, there are no type properties supported for hello Teradata dataset.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="78e70-161">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="78e70-161">Copy activity properties</span></span>
<span data-ttu-id="78e70-162">Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="78e70-162">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="78e70-163">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en beleidsregels zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="78e70-163">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="78e70-164">Terwijl de eigenschappen die beschikbaar zijn in Hallo typeProperties gedeelte van de activiteit Hallo variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="78e70-164">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="78e70-165">Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="78e70-165">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="78e70-166">Wanneer Hallo-bron is van het type **RelationalSource** (waaronder Teradata), Hallo volgende eigenschappen beschikbaar zijn in **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="78e70-166">When hello source is of type **RelationalSource** (which includes Teradata), hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="78e70-167">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="78e70-167">Property</span></span> | <span data-ttu-id="78e70-168">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="78e70-168">Description</span></span> | <span data-ttu-id="78e70-169">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="78e70-169">Allowed values</span></span> | <span data-ttu-id="78e70-170">Vereist</span><span class="sxs-lookup"><span data-stu-id="78e70-170">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="78e70-171">query</span><span class="sxs-lookup"><span data-stu-id="78e70-171">query</span></span> |<span data-ttu-id="78e70-172">Hallo aangepaste query tooread gegevens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="78e70-172">Use hello custom query tooread data.</span></span> |<span data-ttu-id="78e70-173">SQL-query-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="78e70-173">SQL query string.</span></span> <span data-ttu-id="78e70-174">Bijvoorbeeld: Selecteer * from MijnTabel.</span><span class="sxs-lookup"><span data-stu-id="78e70-174">For example: select * from MyTable.</span></span> |<span data-ttu-id="78e70-175">Ja</span><span class="sxs-lookup"><span data-stu-id="78e70-175">Yes</span></span> |

### <a name="json-example-copy-data-from-teradata-tooazure-blob"></a><span data-ttu-id="78e70-176">JSON-voorbeeld: gegevens kopiëren van Teradata tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="78e70-176">JSON example: Copy data from Teradata tooAzure Blob</span></span>
<span data-ttu-id="78e70-177">Hallo volgende voorbeeld wordt een voorbeeld JSON definities waarmee u een pijplijn toocreate kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="78e70-177">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="78e70-178">Ze geven weer hoe toocopy gegevens van Teradata tooAzure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="78e70-178">They show how toocopy data from Teradata tooAzure Blob Storage.</span></span> <span data-ttu-id="78e70-179">Gegevens kunnen echter wel gekopieerde tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="78e70-179">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="78e70-180">Hallo voorbeeld heeft Hallo data factory-entiteiten te volgen:</span><span class="sxs-lookup"><span data-stu-id="78e70-180">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="78e70-181">Een gekoppelde service van het type [OnPremisesTeradata](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="78e70-181">A linked service of type [OnPremisesTeradata](#linked-service-properties).</span></span>
2. <span data-ttu-id="78e70-182">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="78e70-182">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="78e70-183">Invoer [gegevensset](data-factory-create-datasets.md) van het type [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="78e70-183">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="78e70-184">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="78e70-184">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="78e70-185">Hallo [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [RelationalSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="78e70-185">hello [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="78e70-186">Hallo voorbeeld kopieert gegevens van de resultaten van een query in Teradata-database tooa blob elk uur.</span><span class="sxs-lookup"><span data-stu-id="78e70-186">hello sample copies data from a query result in Teradata database tooa blob every hour.</span></span> <span data-ttu-id="78e70-187">Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="78e70-187">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="78e70-188">Instellen als eerste stap Hallo data management gateway.</span><span class="sxs-lookup"><span data-stu-id="78e70-188">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="78e70-189">Hallo-instructies vindt u in Hallo [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="78e70-189">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="78e70-190">**Teradata gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="78e70-190">**Teradata linked service:**</span></span>

```json
{
    "name": "OnPremTeradataLinkedService",
    "properties": {
        "type": "OnPremisesTeradata",
        "typeProperties": {
            "server": "<server>",
            "authenticationType": "<authentication type>",
            "username": "<username>",
            "password": "<password>",
            "gatewayName": "<gatewayName>"
        }
    }
}
```

<span data-ttu-id="78e70-191">**Azure Blob-opslag gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="78e70-191">**Azure Blob storage linked service:**</span></span>

```json
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

<span data-ttu-id="78e70-192">**Teradata invoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="78e70-192">**Teradata input dataset:**</span></span>

<span data-ttu-id="78e70-193">Hallo-voorbeeld wordt ervan uitgegaan dat u hebt een tabel 'MijnTabel' gemaakt in Teradata en bevat een kolom met de naam 'tijdstempel' voor de reeksgegevens.</span><span class="sxs-lookup"><span data-stu-id="78e70-193">hello sample assumes you have created a table “MyTable” in Teradata and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="78e70-194">Instelling 'extern': true informeert Hallo Data Factory-service die tabel Hallo externe toohello data factory is en niet wordt geproduceerd door een activiteit in de gegevensfactory Hallo.</span><span class="sxs-lookup"><span data-stu-id="78e70-194">Setting “external”: true informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "TeradataDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremTeradataLinkedService",
        "typeProperties": {
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

<span data-ttu-id="78e70-195">**Azure Blob-uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="78e70-195">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="78e70-196">Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="78e70-196">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="78e70-197">pad naar map voor blob Hallo Hallo wordt dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="78e70-197">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="78e70-198">Hallo mappad jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="78e70-198">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobTeradataDataSet",
    "properties": {
        "published": false,
        "location": {
            "type": "AzureBlobLocation",
            "folderPath": "mycontainer/teradata/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
            ],
            "linkedServiceName": "AzureStorageLinkedService"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```
<span data-ttu-id="78e70-199">**Pijplijn met de kopieeractiviteit:**</span><span class="sxs-lookup"><span data-stu-id="78e70-199">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="78e70-200">Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun per uur is.</span><span class="sxs-lookup"><span data-stu-id="78e70-200">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="78e70-201">Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**RelationalSource** en **sink** type is ingesteld, te**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="78e70-201">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="78e70-202">Hallo SQL-query is opgegeven voor Hallo **query** eigenschap Hallo gegevens selecteert in Hallo voorbij toocopy uur.</span><span class="sxs-lookup"><span data-stu-id="78e70-202">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopyTeradataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', SliceStart, SliceEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "TeradataDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobTeradataDataSet"
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
                "name": "TeradataToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z",
        "isPaused": false
    }
}
```
## <a name="type-mapping-for-teradata"></a><span data-ttu-id="78e70-203">Toewijzing van het type voor Teradata</span><span class="sxs-lookup"><span data-stu-id="78e70-203">Type mapping for Teradata</span></span>
<span data-ttu-id="78e70-204">Zoals vermeld in Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel Hallo kopieeractiviteit voert automatische typeconversies van brontypen typen toosink Hello 2 stap benadering te volgen:</span><span class="sxs-lookup"><span data-stu-id="78e70-204">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, hello Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="78e70-205">Systeemeigen bron typen too.NET type converteren</span><span class="sxs-lookup"><span data-stu-id="78e70-205">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="78e70-206">Converteren van .NET-type toonative sink-type</span><span class="sxs-lookup"><span data-stu-id="78e70-206">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="78e70-207">Bij het verplaatsen van gegevens tooTeradata worden hello volgende toewijzingen gebruikt vanuit Teradata type too.NET type.</span><span class="sxs-lookup"><span data-stu-id="78e70-207">When moving data tooTeradata, hello following mappings are used from Teradata type too.NET type.</span></span>

| <span data-ttu-id="78e70-208">Type Teradata-Database</span><span class="sxs-lookup"><span data-stu-id="78e70-208">Teradata Database type</span></span> | <span data-ttu-id="78e70-209">.NET framework-type</span><span class="sxs-lookup"><span data-stu-id="78e70-209">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="78e70-210">CHAR</span><span class="sxs-lookup"><span data-stu-id="78e70-210">Char</span></span> |<span data-ttu-id="78e70-211">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="78e70-211">String</span></span> |
| <span data-ttu-id="78e70-212">CLOB</span><span class="sxs-lookup"><span data-stu-id="78e70-212">Clob</span></span> |<span data-ttu-id="78e70-213">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="78e70-213">String</span></span> |
| <span data-ttu-id="78e70-214">Afbeelding</span><span class="sxs-lookup"><span data-stu-id="78e70-214">Graphic</span></span> |<span data-ttu-id="78e70-215">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="78e70-215">String</span></span> |
| <span data-ttu-id="78e70-216">VarChar</span><span class="sxs-lookup"><span data-stu-id="78e70-216">VarChar</span></span> |<span data-ttu-id="78e70-217">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="78e70-217">String</span></span> |
| <span data-ttu-id="78e70-218">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="78e70-218">VarGraphic</span></span> |<span data-ttu-id="78e70-219">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="78e70-219">String</span></span> |
| <span data-ttu-id="78e70-220">Blob</span><span class="sxs-lookup"><span data-stu-id="78e70-220">Blob</span></span> |<span data-ttu-id="78e70-221">Byte]</span><span class="sxs-lookup"><span data-stu-id="78e70-221">Byte[]</span></span> |
| <span data-ttu-id="78e70-222">Byte</span><span class="sxs-lookup"><span data-stu-id="78e70-222">Byte</span></span> |<span data-ttu-id="78e70-223">Byte]</span><span class="sxs-lookup"><span data-stu-id="78e70-223">Byte[]</span></span> |
| <span data-ttu-id="78e70-224">VarByte</span><span class="sxs-lookup"><span data-stu-id="78e70-224">VarByte</span></span> |<span data-ttu-id="78e70-225">Byte]</span><span class="sxs-lookup"><span data-stu-id="78e70-225">Byte[]</span></span> |
| <span data-ttu-id="78e70-226">BigInt</span><span class="sxs-lookup"><span data-stu-id="78e70-226">BigInt</span></span> |<span data-ttu-id="78e70-227">Int64</span><span class="sxs-lookup"><span data-stu-id="78e70-227">Int64</span></span> |
| <span data-ttu-id="78e70-228">ByteInt</span><span class="sxs-lookup"><span data-stu-id="78e70-228">ByteInt</span></span> |<span data-ttu-id="78e70-229">Int16</span><span class="sxs-lookup"><span data-stu-id="78e70-229">Int16</span></span> |
| <span data-ttu-id="78e70-230">Decimale</span><span class="sxs-lookup"><span data-stu-id="78e70-230">Decimal</span></span> |<span data-ttu-id="78e70-231">Decimale</span><span class="sxs-lookup"><span data-stu-id="78e70-231">Decimal</span></span> |
| <span data-ttu-id="78e70-232">dubbele</span><span class="sxs-lookup"><span data-stu-id="78e70-232">Double</span></span> |<span data-ttu-id="78e70-233">dubbele</span><span class="sxs-lookup"><span data-stu-id="78e70-233">Double</span></span> |
| <span data-ttu-id="78e70-234">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="78e70-234">Integer</span></span> |<span data-ttu-id="78e70-235">Int32</span><span class="sxs-lookup"><span data-stu-id="78e70-235">Int32</span></span> |
| <span data-ttu-id="78e70-236">Aantal</span><span class="sxs-lookup"><span data-stu-id="78e70-236">Number</span></span> |<span data-ttu-id="78e70-237">dubbele</span><span class="sxs-lookup"><span data-stu-id="78e70-237">Double</span></span> |
| <span data-ttu-id="78e70-238">SmallInt</span><span class="sxs-lookup"><span data-stu-id="78e70-238">SmallInt</span></span> |<span data-ttu-id="78e70-239">Int16</span><span class="sxs-lookup"><span data-stu-id="78e70-239">Int16</span></span> |
| <span data-ttu-id="78e70-240">Date</span><span class="sxs-lookup"><span data-stu-id="78e70-240">Date</span></span> |<span data-ttu-id="78e70-241">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="78e70-241">DateTime</span></span> |
| <span data-ttu-id="78e70-242">Time</span><span class="sxs-lookup"><span data-stu-id="78e70-242">Time</span></span> |<span data-ttu-id="78e70-243">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="78e70-243">TimeSpan</span></span> |
| <span data-ttu-id="78e70-244">Tijd met de tijdzone</span><span class="sxs-lookup"><span data-stu-id="78e70-244">Time With Time Zone</span></span> |<span data-ttu-id="78e70-245">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="78e70-245">String</span></span> |
| <span data-ttu-id="78e70-246">tijdstempel</span><span class="sxs-lookup"><span data-stu-id="78e70-246">Timestamp</span></span> |<span data-ttu-id="78e70-247">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="78e70-247">DateTime</span></span> |
| <span data-ttu-id="78e70-248">Tijdstempel met tijdzone</span><span class="sxs-lookup"><span data-stu-id="78e70-248">Timestamp With Time Zone</span></span> |<span data-ttu-id="78e70-249">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="78e70-249">DateTimeOffset</span></span> |
| <span data-ttu-id="78e70-250">Interval dag</span><span class="sxs-lookup"><span data-stu-id="78e70-250">Interval Day</span></span> |<span data-ttu-id="78e70-251">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="78e70-251">TimeSpan</span></span> |
| <span data-ttu-id="78e70-252">Interval dag tooHour</span><span class="sxs-lookup"><span data-stu-id="78e70-252">Interval Day tooHour</span></span> |<span data-ttu-id="78e70-253">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="78e70-253">TimeSpan</span></span> |
| <span data-ttu-id="78e70-254">Interval dag tooMinute</span><span class="sxs-lookup"><span data-stu-id="78e70-254">Interval Day tooMinute</span></span> |<span data-ttu-id="78e70-255">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="78e70-255">TimeSpan</span></span> |
| <span data-ttu-id="78e70-256">Interval dag tooSecond</span><span class="sxs-lookup"><span data-stu-id="78e70-256">Interval Day tooSecond</span></span> |<span data-ttu-id="78e70-257">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="78e70-257">TimeSpan</span></span> |
| <span data-ttu-id="78e70-258">Interval uur</span><span class="sxs-lookup"><span data-stu-id="78e70-258">Interval Hour</span></span> |<span data-ttu-id="78e70-259">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="78e70-259">TimeSpan</span></span> |
| <span data-ttu-id="78e70-260">Interval uur tooMinute</span><span class="sxs-lookup"><span data-stu-id="78e70-260">Interval Hour tooMinute</span></span> |<span data-ttu-id="78e70-261">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="78e70-261">TimeSpan</span></span> |
| <span data-ttu-id="78e70-262">Interval uur tooSecond</span><span class="sxs-lookup"><span data-stu-id="78e70-262">Interval Hour tooSecond</span></span> |<span data-ttu-id="78e70-263">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="78e70-263">TimeSpan</span></span> |
| <span data-ttu-id="78e70-264">Interval minuut</span><span class="sxs-lookup"><span data-stu-id="78e70-264">Interval Minute</span></span> |<span data-ttu-id="78e70-265">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="78e70-265">TimeSpan</span></span> |
| <span data-ttu-id="78e70-266">De minuut tooSecond interval</span><span class="sxs-lookup"><span data-stu-id="78e70-266">Interval Minute tooSecond</span></span> |<span data-ttu-id="78e70-267">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="78e70-267">TimeSpan</span></span> |
| <span data-ttu-id="78e70-268">Interval tweede</span><span class="sxs-lookup"><span data-stu-id="78e70-268">Interval Second</span></span> |<span data-ttu-id="78e70-269">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="78e70-269">TimeSpan</span></span> |
| <span data-ttu-id="78e70-270">Interval jaar</span><span class="sxs-lookup"><span data-stu-id="78e70-270">Interval Year</span></span> |<span data-ttu-id="78e70-271">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="78e70-271">String</span></span> |
| <span data-ttu-id="78e70-272">Interval jaar tooMonth</span><span class="sxs-lookup"><span data-stu-id="78e70-272">Interval Year tooMonth</span></span> |<span data-ttu-id="78e70-273">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="78e70-273">String</span></span> |
| <span data-ttu-id="78e70-274">Interval maand</span><span class="sxs-lookup"><span data-stu-id="78e70-274">Interval Month</span></span> |<span data-ttu-id="78e70-275">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="78e70-275">String</span></span> |
| <span data-ttu-id="78e70-276">Period(date)</span><span class="sxs-lookup"><span data-stu-id="78e70-276">Period(Date)</span></span> |<span data-ttu-id="78e70-277">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="78e70-277">String</span></span> |
| <span data-ttu-id="78e70-278">Period(Time)</span><span class="sxs-lookup"><span data-stu-id="78e70-278">Period(Time)</span></span> |<span data-ttu-id="78e70-279">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="78e70-279">String</span></span> |
| <span data-ttu-id="78e70-280">Periode (tijd met tijdzone)</span><span class="sxs-lookup"><span data-stu-id="78e70-280">Period(Time With Time Zone)</span></span> |<span data-ttu-id="78e70-281">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="78e70-281">String</span></span> |
| <span data-ttu-id="78e70-282">Period(timestamp)</span><span class="sxs-lookup"><span data-stu-id="78e70-282">Period(Timestamp)</span></span> |<span data-ttu-id="78e70-283">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="78e70-283">String</span></span> |
| <span data-ttu-id="78e70-284">Periode (tijdstempel met tijdzone)</span><span class="sxs-lookup"><span data-stu-id="78e70-284">Period(Timestamp With Time Zone)</span></span> |<span data-ttu-id="78e70-285">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="78e70-285">String</span></span> |
| <span data-ttu-id="78e70-286">XML</span><span class="sxs-lookup"><span data-stu-id="78e70-286">Xml</span></span> |<span data-ttu-id="78e70-287">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="78e70-287">String</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="78e70-288">Bronkolommen toosink toewijzen</span><span class="sxs-lookup"><span data-stu-id="78e70-288">Map source toosink columns</span></span>
<span data-ttu-id="78e70-289">Zie toolearn over het toewijzen van kolommen in bron gegevensset toocolumns in sink-gegevensset [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="78e70-289">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="78e70-290">Herhaalbare leesbewerking van relationele bronnen</span><span class="sxs-lookup"><span data-stu-id="78e70-290">Repeatable read from relational sources</span></span>
<span data-ttu-id="78e70-291">Houd bij het kopiëren van gegevens uit een relationele gegevensopslag, herhaalbaarheid rekening tooavoid ongewenste resultaten.</span><span class="sxs-lookup"><span data-stu-id="78e70-291">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="78e70-292">In Azure Data Factory, kunt u een segment handmatig opnieuw.</span><span class="sxs-lookup"><span data-stu-id="78e70-292">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="78e70-293">U kunt ook een beleid voor opnieuw proberen voor een gegevensset configureren zodat een segment wordt opnieuw uitgevoerd wanneer een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="78e70-293">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="78e70-294">Wanneer een segment opnieuw in beide gevallen wordt uitgevoerd, moet u ervoor dat dezelfde gegevens Hallo toomake wordt gelezen ongeacht hoe vaak een segment wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="78e70-294">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="78e70-295">Zie [Repeatable van relationele bronnen lezen](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="78e70-295">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="78e70-296">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="78e70-296">Performance and Tuning</span></span>
<span data-ttu-id="78e70-297">Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.</span><span class="sxs-lookup"><span data-stu-id="78e70-297">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
