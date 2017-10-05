---
title: Verplaatsen van gegevens uit een Teradata met behulp van Azure Data Factory | Microsoft Docs
description: Meer informatie over Teradata-Connector voor de Data Factory-service waarmee u gegevens van de Teradata-Database verplaatsen
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
ms.openlocfilehash: 01edb32cd9e20d4199feac5b98a73aa06b74fec2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="move-data-from-teradata-using-azure-data-factory"></a><span data-ttu-id="c5e45-103">Verplaatsen van gegevens uit een Teradata met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="c5e45-103">Move data from Teradata using Azure Data Factory</span></span>
<span data-ttu-id="c5e45-104">In dit artikel wordt uitgelegd hoe de Kopieeractiviteit in Azure Data Factory om gegevens te verplaatsen van een on-premises Teradata-database gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c5e45-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises Teradata database.</span></span> <span data-ttu-id="c5e45-105">Dit is gebaseerd op de [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, hetgeen een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit toont.</span><span class="sxs-lookup"><span data-stu-id="c5e45-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="c5e45-106">U kunt gegevens uit een on-premises Teradata-gegevensopslag kopiëren naar een ondersteunde sink-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="c5e45-106">You can copy data from an on-premises Teradata data store to any supported sink data store.</span></span> <span data-ttu-id="c5e45-107">Zie voor een lijst met gegevensarchieven als PUT wordt ondersteund door de kopieeractiviteit, de [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel.</span><span class="sxs-lookup"><span data-stu-id="c5e45-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="c5e45-108">Data factory ondersteunt momenteel alleen zwevend gegevens uit een Teradata-gegevensarchief tot andere gegevensarchieven, maar niet voor het verplaatsen van gegevens uit andere gegevensarchieven met een Teradata-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="c5e45-108">Data factory currently supports only moving data from a Teradata data store to other data stores, but not for moving data from other data stores to a Teradata data store.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="c5e45-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c5e45-109">Prerequisites</span></span>
<span data-ttu-id="c5e45-110">Data factory ondersteunt verbindingen met de lokale Teradata bronnen via Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="c5e45-110">Data factory supports connecting to on-premises Teradata sources via the Data Management Gateway.</span></span> <span data-ttu-id="c5e45-111">Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor meer informatie over Data Management Gateway en stapsgewijze instructies over het instellen van de gateway.</span><span class="sxs-lookup"><span data-stu-id="c5e45-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span>

<span data-ttu-id="c5e45-112">Gateway is vereist, zelfs als de Teradata wordt gehost in een Azure IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="c5e45-112">Gateway is required even if the Teradata is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="c5e45-113">U kunt de gateway installeren op de dezelfde IaaS VM als gegevensopslag of op een andere virtuele machine, zolang de gateway verbinding met de database maken kan.</span><span class="sxs-lookup"><span data-stu-id="c5e45-113">You can install the gateway on the same IaaS VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>

> [!NOTE]
> <span data-ttu-id="c5e45-114">Zie [gateway problemen](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) voor tips over het oplossen van verbinding of gateway gerelateerde problemen.</span><span class="sxs-lookup"><span data-stu-id="c5e45-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="c5e45-115">Ondersteunde versies en installatie</span><span class="sxs-lookup"><span data-stu-id="c5e45-115">Supported versions and installation</span></span>
<span data-ttu-id="c5e45-116">Voor de Data Management Gateway verbinding maken met de Teradata-Database, moet u voor het installeren van de [.NET-gegevensprovider voor Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) versie 14 of hoger op hetzelfde systeem als Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="c5e45-116">For Data Management Gateway to connect to the Teradata Database, you need to install the [.NET Data Provider for Teradata](http://go.microsoft.com/fwlink/?LinkId=278886) version 14 or above on the same system as the Data Management Gateway.</span></span> <span data-ttu-id="c5e45-117">Teradata versie 12 en hoger wordt ondersteund.</span><span class="sxs-lookup"><span data-stu-id="c5e45-117">Teradata version 12 and above is supported.</span></span>

## <a name="getting-started"></a><span data-ttu-id="c5e45-118">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="c5e45-118">Getting started</span></span>
<span data-ttu-id="c5e45-119">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens vanuit een on-premises Cassandra-gegevensopslag verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="c5e45-119">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="c5e45-120">De eenvoudigste manier om een pijplijn maken is met de **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="c5e45-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="c5e45-121">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met de wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="c5e45-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="c5e45-122">U kunt ook de volgende hulpprogramma's gebruiken voor het maken van een pijplijn: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon**, **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="c5e45-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="c5e45-123">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies voor een pijplijn maken met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="c5e45-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="c5e45-124">Of u de hulpprogramma's of API's gebruiken, moet u de volgende stappen voor het maken van een pijplijn die de gegevens vanuit een brongegevensarchief naar een gegevensarchief sink verplaatst uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="c5e45-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="c5e45-125">Maak **gekoppelde services** slaat om invoer- en gegevens te koppelen aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="c5e45-125">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="c5e45-126">Maak **gegevenssets** vertegenwoordigt de invoer- en -gegevens voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="c5e45-126">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="c5e45-127">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="c5e45-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="c5e45-128">Wanneer u de wizard gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c5e45-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="c5e45-129">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van de JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="c5e45-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="c5e45-130">Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die worden gebruikt om gegevens te kopiëren uit een on-premises Teradata-gegevensopslag [JSON-voorbeeld: gegevens kopiëren van Teradata naar Azure Blob](#json-example-copy-data-from-teradata-to-azure-blob) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="c5e45-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises Teradata data store, see [JSON example: Copy data from Teradata to Azure Blob](#json-example-copy-data-from-teradata-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="c5e45-131">De volgende secties bevatten informatie over de JSON-eigenschappen die worden gebruikt voor het definiëren van specifieke Data Factory-entiteiten met een Teradata-gegevensarchief:</span><span class="sxs-lookup"><span data-stu-id="c5e45-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to a Teradata data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="c5e45-132">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="c5e45-132">Linked service properties</span></span>
<span data-ttu-id="c5e45-133">De volgende tabel bevat een beschrijving voor JSON-elementen die specifiek zijn voor Teradata gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="c5e45-133">The following table provides description for JSON elements specific to Teradata linked service.</span></span>

| <span data-ttu-id="c5e45-134">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="c5e45-134">Property</span></span> | <span data-ttu-id="c5e45-135">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c5e45-135">Description</span></span> | <span data-ttu-id="c5e45-136">Vereist</span><span class="sxs-lookup"><span data-stu-id="c5e45-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c5e45-137">type</span><span class="sxs-lookup"><span data-stu-id="c5e45-137">type</span></span> |<span data-ttu-id="c5e45-138">De eigenschap type moet worden ingesteld op: **OnPremisesTeradata**</span><span class="sxs-lookup"><span data-stu-id="c5e45-138">The type property must be set to: **OnPremisesTeradata**</span></span> |<span data-ttu-id="c5e45-139">Ja</span><span class="sxs-lookup"><span data-stu-id="c5e45-139">Yes</span></span> |
| <span data-ttu-id="c5e45-140">server</span><span class="sxs-lookup"><span data-stu-id="c5e45-140">server</span></span> |<span data-ttu-id="c5e45-141">De naam van de Teradata-server.</span><span class="sxs-lookup"><span data-stu-id="c5e45-141">Name of the Teradata server.</span></span> |<span data-ttu-id="c5e45-142">Ja</span><span class="sxs-lookup"><span data-stu-id="c5e45-142">Yes</span></span> |
| <span data-ttu-id="c5e45-143">authenticationType</span><span class="sxs-lookup"><span data-stu-id="c5e45-143">authenticationType</span></span> |<span data-ttu-id="c5e45-144">Het soort verificatie die verbinding maken met de Teradata-database wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c5e45-144">Type of authentication used to connect to the Teradata database.</span></span> <span data-ttu-id="c5e45-145">Mogelijke waarden zijn: anoniem, basis en Windows.</span><span class="sxs-lookup"><span data-stu-id="c5e45-145">Possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="c5e45-146">Ja</span><span class="sxs-lookup"><span data-stu-id="c5e45-146">Yes</span></span> |
| <span data-ttu-id="c5e45-147">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="c5e45-147">username</span></span> |<span data-ttu-id="c5e45-148">Geef de gebruikersnaam als u basisverificatie of Windows-verificatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c5e45-148">Specify user name if you are using Basic or Windows authentication.</span></span> |<span data-ttu-id="c5e45-149">Nee</span><span class="sxs-lookup"><span data-stu-id="c5e45-149">No</span></span> |
| <span data-ttu-id="c5e45-150">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="c5e45-150">password</span></span> |<span data-ttu-id="c5e45-151">Wachtwoord voor het gebruikersaccount dat u hebt opgegeven voor de gebruikersnaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="c5e45-151">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="c5e45-152">Nee</span><span class="sxs-lookup"><span data-stu-id="c5e45-152">No</span></span> |
| <span data-ttu-id="c5e45-153">gatewayName</span><span class="sxs-lookup"><span data-stu-id="c5e45-153">gatewayName</span></span> |<span data-ttu-id="c5e45-154">Naam van de gateway die voor de Data Factory-service gebruiken moet voor verbinding met de lokale Teradata-database.</span><span class="sxs-lookup"><span data-stu-id="c5e45-154">Name of the gateway that the Data Factory service should use to connect to the on-premises Teradata database.</span></span> |<span data-ttu-id="c5e45-155">Ja</span><span class="sxs-lookup"><span data-stu-id="c5e45-155">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="c5e45-156">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="c5e45-156">Dataset properties</span></span>
<span data-ttu-id="c5e45-157">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van de [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="c5e45-157">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="c5e45-158">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).</span><span class="sxs-lookup"><span data-stu-id="c5e45-158">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="c5e45-159">De **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over de locatie van de gegevens in het gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="c5e45-159">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="c5e45-160">Er zijn momenteel geen type-eigenschappen voor de gegevensset Teradata ondersteund.</span><span class="sxs-lookup"><span data-stu-id="c5e45-160">Currently, there are no type properties supported for the Teradata dataset.</span></span>

## <a name="copy-activity-properties"></a><span data-ttu-id="c5e45-161">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="c5e45-161">Copy activity properties</span></span>
<span data-ttu-id="c5e45-162">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van activiteiten van de [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="c5e45-162">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="c5e45-163">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en beleidsregels zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="c5e45-163">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="c5e45-164">Terwijl de eigenschappen die beschikbaar zijn in de sectie typeProperties van de activiteit variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="c5e45-164">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="c5e45-165">Voor de kopieeractiviteit variëren ze, afhankelijk van de typen van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="c5e45-165">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="c5e45-166">Wanneer de bron is van het type **RelationalSource** (waaronder Teradata), de volgende eigenschappen beschikbaar zijn in **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="c5e45-166">When the source is of type **RelationalSource** (which includes Teradata), the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="c5e45-167">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="c5e45-167">Property</span></span> | <span data-ttu-id="c5e45-168">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c5e45-168">Description</span></span> | <span data-ttu-id="c5e45-169">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="c5e45-169">Allowed values</span></span> | <span data-ttu-id="c5e45-170">Vereist</span><span class="sxs-lookup"><span data-stu-id="c5e45-170">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c5e45-171">query</span><span class="sxs-lookup"><span data-stu-id="c5e45-171">query</span></span> |<span data-ttu-id="c5e45-172">Gebruik de aangepaste query om gegevens te lezen.</span><span class="sxs-lookup"><span data-stu-id="c5e45-172">Use the custom query to read data.</span></span> |<span data-ttu-id="c5e45-173">SQL-query-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="c5e45-173">SQL query string.</span></span> <span data-ttu-id="c5e45-174">Bijvoorbeeld: Selecteer * from MijnTabel.</span><span class="sxs-lookup"><span data-stu-id="c5e45-174">For example: select * from MyTable.</span></span> |<span data-ttu-id="c5e45-175">Ja</span><span class="sxs-lookup"><span data-stu-id="c5e45-175">Yes</span></span> |

### <a name="json-example-copy-data-from-teradata-to-azure-blob"></a><span data-ttu-id="c5e45-176">JSON-voorbeeld: gegevens kopiëren van Teradata naar Azure Blob</span><span class="sxs-lookup"><span data-stu-id="c5e45-176">JSON example: Copy data from Teradata to Azure Blob</span></span>
<span data-ttu-id="c5e45-177">Het volgende voorbeeld bevat definities van de voorbeeld-JSON die u een pijplijn maken kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c5e45-177">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="c5e45-178">Ze laten zien hoe gegevens kopiëren van Teradata naar Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="c5e45-178">They show how to copy data from Teradata to Azure Blob Storage.</span></span> <span data-ttu-id="c5e45-179">Gegevens kunnen echter worden gekopieerd naar een van de PUT vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van de Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c5e45-179">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="c5e45-180">Het voorbeeld heeft de volgende data factory-entiteiten:</span><span class="sxs-lookup"><span data-stu-id="c5e45-180">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="c5e45-181">Een gekoppelde service van het type [OnPremisesTeradata](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c5e45-181">A linked service of type [OnPremisesTeradata](#linked-service-properties).</span></span>
2. <span data-ttu-id="c5e45-182">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c5e45-182">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="c5e45-183">Invoer [gegevensset](data-factory-create-datasets.md) van het type [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c5e45-183">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="c5e45-184">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c5e45-184">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="c5e45-185">De [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [RelationalSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="c5e45-185">The [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="c5e45-186">Het voorbeeld kopieert gegevens van de resultaten van een query in Teradata-database naar een blob elk uur.</span><span class="sxs-lookup"><span data-stu-id="c5e45-186">The sample copies data from a query result in Teradata database to a blob every hour.</span></span> <span data-ttu-id="c5e45-187">De JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na de voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="c5e45-187">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="c5e45-188">Het instellen van de data management gateway als eerste stap.</span><span class="sxs-lookup"><span data-stu-id="c5e45-188">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="c5e45-189">De instructies vindt u in de [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="c5e45-189">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="c5e45-190">**Teradata gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="c5e45-190">**Teradata linked service:**</span></span>

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

<span data-ttu-id="c5e45-191">**Azure Blob-opslag gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="c5e45-191">**Azure Blob storage linked service:**</span></span>

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

<span data-ttu-id="c5e45-192">**Teradata invoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="c5e45-192">**Teradata input dataset:**</span></span>

<span data-ttu-id="c5e45-193">Het voorbeeld wordt ervan uitgegaan dat u hebt een tabel 'MijnTabel' gemaakt in Teradata en bevat een kolom met de naam 'tijdstempel' voor de reeksgegevens.</span><span class="sxs-lookup"><span data-stu-id="c5e45-193">The sample assumes you have created a table “MyTable” in Teradata and it contains a column called “timestamp” for time series data.</span></span>

<span data-ttu-id="c5e45-194">Instelling 'extern': true informeert de Data Factory-service dat de tabel aan de gegevensfactory extern en niet wordt geproduceerd door een activiteit in de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="c5e45-194">Setting “external”: true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="c5e45-195">**Azure Blob-uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="c5e45-195">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="c5e45-196">Gegevens worden geschreven naar een nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="c5e45-196">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="c5e45-197">Het pad naar de blob wordt dynamisch geëvalueerd op basis van de begintijd van het segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="c5e45-197">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="c5e45-198">Het mappad maakt gebruik van jaar, maand, dag en uur delen van de begintijd.</span><span class="sxs-lookup"><span data-stu-id="c5e45-198">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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
<span data-ttu-id="c5e45-199">**Pijplijn met de kopieeractiviteit:**</span><span class="sxs-lookup"><span data-stu-id="c5e45-199">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="c5e45-200">De pijplijn bevat een Kopieeractiviteit die is geconfigureerd voor gebruik van de invoer- en uitvoergegevenssets en is gepland voor uitvoering per uur.</span><span class="sxs-lookup"><span data-stu-id="c5e45-200">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run hourly.</span></span> <span data-ttu-id="c5e45-201">In de pijplijn-JSON-definitie de **bron** type is ingesteld op **RelationalSource** en **sink** type is ingesteld op **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="c5e45-201">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="c5e45-202">De SQL-query die is opgegeven voor de **query** eigenschap selecteert u de gegevens in het afgelopen uur te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="c5e45-202">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

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
## <a name="type-mapping-for-teradata"></a><span data-ttu-id="c5e45-203">Toewijzing van het type voor Teradata</span><span class="sxs-lookup"><span data-stu-id="c5e45-203">Type mapping for Teradata</span></span>
<span data-ttu-id="c5e45-204">Zoals vermeld in de [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel de kopieerbewerking wordt automatische typeconversies van brontypen opvangen typen met de volgende stappen 2-benadering uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="c5e45-204">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="c5e45-205">Systeemeigen brontypen converteren naar .NET-type</span><span class="sxs-lookup"><span data-stu-id="c5e45-205">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="c5e45-206">Converteren van .NET-type naar systeemeigen sink-type</span><span class="sxs-lookup"><span data-stu-id="c5e45-206">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="c5e45-207">Wanneer u gegevens naar Teradata verplaatst, worden de volgende toewijzingen van Teradata type gebruikt voor .NET-type.</span><span class="sxs-lookup"><span data-stu-id="c5e45-207">When moving data to Teradata, the following mappings are used from Teradata type to .NET type.</span></span>

| <span data-ttu-id="c5e45-208">Type Teradata-Database</span><span class="sxs-lookup"><span data-stu-id="c5e45-208">Teradata Database type</span></span> | <span data-ttu-id="c5e45-209">.NET framework-type</span><span class="sxs-lookup"><span data-stu-id="c5e45-209">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="c5e45-210">CHAR</span><span class="sxs-lookup"><span data-stu-id="c5e45-210">Char</span></span> |<span data-ttu-id="c5e45-211">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c5e45-211">String</span></span> |
| <span data-ttu-id="c5e45-212">CLOB</span><span class="sxs-lookup"><span data-stu-id="c5e45-212">Clob</span></span> |<span data-ttu-id="c5e45-213">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c5e45-213">String</span></span> |
| <span data-ttu-id="c5e45-214">Afbeelding</span><span class="sxs-lookup"><span data-stu-id="c5e45-214">Graphic</span></span> |<span data-ttu-id="c5e45-215">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c5e45-215">String</span></span> |
| <span data-ttu-id="c5e45-216">VarChar</span><span class="sxs-lookup"><span data-stu-id="c5e45-216">VarChar</span></span> |<span data-ttu-id="c5e45-217">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c5e45-217">String</span></span> |
| <span data-ttu-id="c5e45-218">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="c5e45-218">VarGraphic</span></span> |<span data-ttu-id="c5e45-219">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c5e45-219">String</span></span> |
| <span data-ttu-id="c5e45-220">Blob</span><span class="sxs-lookup"><span data-stu-id="c5e45-220">Blob</span></span> |<span data-ttu-id="c5e45-221">Byte]</span><span class="sxs-lookup"><span data-stu-id="c5e45-221">Byte[]</span></span> |
| <span data-ttu-id="c5e45-222">Byte</span><span class="sxs-lookup"><span data-stu-id="c5e45-222">Byte</span></span> |<span data-ttu-id="c5e45-223">Byte]</span><span class="sxs-lookup"><span data-stu-id="c5e45-223">Byte[]</span></span> |
| <span data-ttu-id="c5e45-224">VarByte</span><span class="sxs-lookup"><span data-stu-id="c5e45-224">VarByte</span></span> |<span data-ttu-id="c5e45-225">Byte]</span><span class="sxs-lookup"><span data-stu-id="c5e45-225">Byte[]</span></span> |
| <span data-ttu-id="c5e45-226">BigInt</span><span class="sxs-lookup"><span data-stu-id="c5e45-226">BigInt</span></span> |<span data-ttu-id="c5e45-227">Int64</span><span class="sxs-lookup"><span data-stu-id="c5e45-227">Int64</span></span> |
| <span data-ttu-id="c5e45-228">ByteInt</span><span class="sxs-lookup"><span data-stu-id="c5e45-228">ByteInt</span></span> |<span data-ttu-id="c5e45-229">Int16</span><span class="sxs-lookup"><span data-stu-id="c5e45-229">Int16</span></span> |
| <span data-ttu-id="c5e45-230">Decimale</span><span class="sxs-lookup"><span data-stu-id="c5e45-230">Decimal</span></span> |<span data-ttu-id="c5e45-231">Decimale</span><span class="sxs-lookup"><span data-stu-id="c5e45-231">Decimal</span></span> |
| <span data-ttu-id="c5e45-232">dubbele</span><span class="sxs-lookup"><span data-stu-id="c5e45-232">Double</span></span> |<span data-ttu-id="c5e45-233">dubbele</span><span class="sxs-lookup"><span data-stu-id="c5e45-233">Double</span></span> |
| <span data-ttu-id="c5e45-234">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="c5e45-234">Integer</span></span> |<span data-ttu-id="c5e45-235">Int32</span><span class="sxs-lookup"><span data-stu-id="c5e45-235">Int32</span></span> |
| <span data-ttu-id="c5e45-236">Aantal</span><span class="sxs-lookup"><span data-stu-id="c5e45-236">Number</span></span> |<span data-ttu-id="c5e45-237">dubbele</span><span class="sxs-lookup"><span data-stu-id="c5e45-237">Double</span></span> |
| <span data-ttu-id="c5e45-238">SmallInt</span><span class="sxs-lookup"><span data-stu-id="c5e45-238">SmallInt</span></span> |<span data-ttu-id="c5e45-239">Int16</span><span class="sxs-lookup"><span data-stu-id="c5e45-239">Int16</span></span> |
| <span data-ttu-id="c5e45-240">Date</span><span class="sxs-lookup"><span data-stu-id="c5e45-240">Date</span></span> |<span data-ttu-id="c5e45-241">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="c5e45-241">DateTime</span></span> |
| <span data-ttu-id="c5e45-242">Time</span><span class="sxs-lookup"><span data-stu-id="c5e45-242">Time</span></span> |<span data-ttu-id="c5e45-243">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="c5e45-243">TimeSpan</span></span> |
| <span data-ttu-id="c5e45-244">Tijd met de tijdzone</span><span class="sxs-lookup"><span data-stu-id="c5e45-244">Time With Time Zone</span></span> |<span data-ttu-id="c5e45-245">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c5e45-245">String</span></span> |
| <span data-ttu-id="c5e45-246">tijdstempel</span><span class="sxs-lookup"><span data-stu-id="c5e45-246">Timestamp</span></span> |<span data-ttu-id="c5e45-247">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="c5e45-247">DateTime</span></span> |
| <span data-ttu-id="c5e45-248">Tijdstempel met tijdzone</span><span class="sxs-lookup"><span data-stu-id="c5e45-248">Timestamp With Time Zone</span></span> |<span data-ttu-id="c5e45-249">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="c5e45-249">DateTimeOffset</span></span> |
| <span data-ttu-id="c5e45-250">Interval dag</span><span class="sxs-lookup"><span data-stu-id="c5e45-250">Interval Day</span></span> |<span data-ttu-id="c5e45-251">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="c5e45-251">TimeSpan</span></span> |
| <span data-ttu-id="c5e45-252">Interval dag uur</span><span class="sxs-lookup"><span data-stu-id="c5e45-252">Interval Day To Hour</span></span> |<span data-ttu-id="c5e45-253">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="c5e45-253">TimeSpan</span></span> |
| <span data-ttu-id="c5e45-254">Interval dag minuut</span><span class="sxs-lookup"><span data-stu-id="c5e45-254">Interval Day To Minute</span></span> |<span data-ttu-id="c5e45-255">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="c5e45-255">TimeSpan</span></span> |
| <span data-ttu-id="c5e45-256">Tweede interval dag</span><span class="sxs-lookup"><span data-stu-id="c5e45-256">Interval Day To Second</span></span> |<span data-ttu-id="c5e45-257">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="c5e45-257">TimeSpan</span></span> |
| <span data-ttu-id="c5e45-258">Interval uur</span><span class="sxs-lookup"><span data-stu-id="c5e45-258">Interval Hour</span></span> |<span data-ttu-id="c5e45-259">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="c5e45-259">TimeSpan</span></span> |
| <span data-ttu-id="c5e45-260">Interval uur, minuut</span><span class="sxs-lookup"><span data-stu-id="c5e45-260">Interval Hour To Minute</span></span> |<span data-ttu-id="c5e45-261">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="c5e45-261">TimeSpan</span></span> |
| <span data-ttu-id="c5e45-262">Tweede interval uur</span><span class="sxs-lookup"><span data-stu-id="c5e45-262">Interval Hour To Second</span></span> |<span data-ttu-id="c5e45-263">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="c5e45-263">TimeSpan</span></span> |
| <span data-ttu-id="c5e45-264">Interval minuut</span><span class="sxs-lookup"><span data-stu-id="c5e45-264">Interval Minute</span></span> |<span data-ttu-id="c5e45-265">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="c5e45-265">TimeSpan</span></span> |
| <span data-ttu-id="c5e45-266">Minuut tweede interval</span><span class="sxs-lookup"><span data-stu-id="c5e45-266">Interval Minute To Second</span></span> |<span data-ttu-id="c5e45-267">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="c5e45-267">TimeSpan</span></span> |
| <span data-ttu-id="c5e45-268">Interval tweede</span><span class="sxs-lookup"><span data-stu-id="c5e45-268">Interval Second</span></span> |<span data-ttu-id="c5e45-269">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="c5e45-269">TimeSpan</span></span> |
| <span data-ttu-id="c5e45-270">Interval jaar</span><span class="sxs-lookup"><span data-stu-id="c5e45-270">Interval Year</span></span> |<span data-ttu-id="c5e45-271">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c5e45-271">String</span></span> |
| <span data-ttu-id="c5e45-272">Interval jaar, maand</span><span class="sxs-lookup"><span data-stu-id="c5e45-272">Interval Year To Month</span></span> |<span data-ttu-id="c5e45-273">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c5e45-273">String</span></span> |
| <span data-ttu-id="c5e45-274">Interval maand</span><span class="sxs-lookup"><span data-stu-id="c5e45-274">Interval Month</span></span> |<span data-ttu-id="c5e45-275">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c5e45-275">String</span></span> |
| <span data-ttu-id="c5e45-276">Period(date)</span><span class="sxs-lookup"><span data-stu-id="c5e45-276">Period(Date)</span></span> |<span data-ttu-id="c5e45-277">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c5e45-277">String</span></span> |
| <span data-ttu-id="c5e45-278">Period(Time)</span><span class="sxs-lookup"><span data-stu-id="c5e45-278">Period(Time)</span></span> |<span data-ttu-id="c5e45-279">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c5e45-279">String</span></span> |
| <span data-ttu-id="c5e45-280">Periode (tijd met tijdzone)</span><span class="sxs-lookup"><span data-stu-id="c5e45-280">Period(Time With Time Zone)</span></span> |<span data-ttu-id="c5e45-281">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c5e45-281">String</span></span> |
| <span data-ttu-id="c5e45-282">Period(timestamp)</span><span class="sxs-lookup"><span data-stu-id="c5e45-282">Period(Timestamp)</span></span> |<span data-ttu-id="c5e45-283">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c5e45-283">String</span></span> |
| <span data-ttu-id="c5e45-284">Periode (tijdstempel met tijdzone)</span><span class="sxs-lookup"><span data-stu-id="c5e45-284">Period(Timestamp With Time Zone)</span></span> |<span data-ttu-id="c5e45-285">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c5e45-285">String</span></span> |
| <span data-ttu-id="c5e45-286">XML</span><span class="sxs-lookup"><span data-stu-id="c5e45-286">Xml</span></span> |<span data-ttu-id="c5e45-287">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c5e45-287">String</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="c5e45-288">Bron van de kaart opvangen kolommen</span><span class="sxs-lookup"><span data-stu-id="c5e45-288">Map source to sink columns</span></span>
<span data-ttu-id="c5e45-289">Zie voor meer informatie over het toewijzen van kolommen in gegevensset naar kolommen in gegevensset sink bron, [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="c5e45-289">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="c5e45-290">Herhaalbare leesbewerking van relationele bronnen</span><span class="sxs-lookup"><span data-stu-id="c5e45-290">Repeatable read from relational sources</span></span>
<span data-ttu-id="c5e45-291">Bij het kopiëren van gegevens van relationele gegevens worden opgeslagen, moet u herhaalbaarheid Houd in gedachten om te voorkomen dat ongewenste resultaten.</span><span class="sxs-lookup"><span data-stu-id="c5e45-291">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="c5e45-292">In Azure Data Factory, kunt u een segment handmatig opnieuw.</span><span class="sxs-lookup"><span data-stu-id="c5e45-292">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="c5e45-293">U kunt ook een beleid voor opnieuw proberen voor een gegevensset configureren zodat een segment wordt opnieuw uitgevoerd wanneer een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="c5e45-293">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="c5e45-294">Wanneer een segment opnieuw in beide gevallen wordt uitgevoerd, moet u ervoor zorgen dat dezelfde gegevens is gelezen ongeacht hoe vaak een segment wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c5e45-294">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="c5e45-295">Zie [Repeatable van relationele bronnen lezen](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="c5e45-295">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="c5e45-296">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="c5e45-296">Performance and Tuning</span></span>
<span data-ttu-id="c5e45-297">Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) voor meer informatie over de belangrijkste factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren om te optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="c5e45-297">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
