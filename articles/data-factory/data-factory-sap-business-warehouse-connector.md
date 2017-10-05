---
title: Verplaatsen van gegevens uit een SAP Business Warehouse met behulp van Azure Data Factory | Microsoft Docs
description: Meer informatie over het verplaatsen van gegevens uit een SAP Business Warehouse met behulp van Azure Data Factory.
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
ms.openlocfilehash: 220ccc8b94797880d335385046001c5f3b17c862
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-sap-business-warehouse-using-azure-data-factory"></a><span data-ttu-id="c9a56-103">Verplaatsen van gegevens uit SAP Business Warehouse met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="c9a56-103">Move data From SAP Business Warehouse using Azure Data Factory</span></span>
<span data-ttu-id="c9a56-104">In dit artikel wordt uitgelegd hoe de Kopieeractiviteit in Azure Data Factory om gegevens te verplaatsen van een lokale SAP Business Warehouse (BW) gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c9a56-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises SAP Business Warehouse (BW).</span></span> <span data-ttu-id="c9a56-105">Dit is gebaseerd op de [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, hetgeen een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit toont.</span><span class="sxs-lookup"><span data-stu-id="c9a56-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="c9a56-106">U kunt gegevens uit een on-premises SAP Business Warehouse-gegevensopslag kopiëren naar een ondersteunde sink-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="c9a56-106">You can copy data from an on-premises SAP Business Warehouse data store to any supported sink data store.</span></span> <span data-ttu-id="c9a56-107">Zie voor een lijst met gegevensarchieven als PUT wordt ondersteund door de kopieeractiviteit, de [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel.</span><span class="sxs-lookup"><span data-stu-id="c9a56-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="c9a56-108">Data factory ondersteunt momenteel alleen zwevend gegevens uit een SAP Business Warehouse tot andere gegevensarchieven, maar niet voor het verplaatsen van gegevens uit andere gegevensarchieven naar een SAP Business Warehouse.</span><span class="sxs-lookup"><span data-stu-id="c9a56-108">Data factory currently supports only moving data from an SAP Business Warehouse to other data stores, but not for moving data from other data stores to an SAP Business Warehouse.</span></span> 

## <a name="supported-versions-and-installation"></a><span data-ttu-id="c9a56-109">Ondersteunde versies en installatie</span><span class="sxs-lookup"><span data-stu-id="c9a56-109">Supported versions and installation</span></span>
<span data-ttu-id="c9a56-110">Deze connector ondersteunt SAP Business Warehouse versie 7.x.</span><span class="sxs-lookup"><span data-stu-id="c9a56-110">This connector supports SAP Business Warehouse version 7.x.</span></span> <span data-ttu-id="c9a56-111">Het ondersteunt kopiëren van gegevens van InfoCubes en QueryCubes (inclusief BEx query's) met behulp van de MDX-query's.</span><span class="sxs-lookup"><span data-stu-id="c9a56-111">It supports copying data from InfoCubes and QueryCubes (including BEx queries) using MDX queries.</span></span>

<span data-ttu-id="c9a56-112">Als u de verbinding met het exemplaar SAP BW installeert de volgende onderdelen:</span><span class="sxs-lookup"><span data-stu-id="c9a56-112">To enable the connectivity to the SAP BW instance, install the following components:</span></span>
- <span data-ttu-id="c9a56-113">**Data Management Gateway**: Data Factory-service ondersteunt het verbinden met on-premises gegevens winkels (inclusief SAP Business Warehouse) met een onderdeel genaamd Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="c9a56-113">**Data Management Gateway**: Data Factory service supports connecting to on-premises data stores (including SAP Business Warehouse) using a component called Data Management Gateway.</span></span> <span data-ttu-id="c9a56-114">Zie voor meer informatie over Data Management Gateway en stapsgewijze instructies voor het instellen van de gateway, [Moving gegevens tussen on-premises gegevens opslaan in de cloud gegevensarchief](data-factory-move-data-between-onprem-and-cloud.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="c9a56-114">To learn about Data Management Gateway and step-by-step instructions for setting up the gateway, see [Moving data between on-premises data store to cloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="c9a56-115">Gateway is vereist, zelfs als de SAP Business Warehouse wordt gehost in een Azure IaaS virtuele machine (VM).</span><span class="sxs-lookup"><span data-stu-id="c9a56-115">Gateway is required even if the SAP Business Warehouse is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="c9a56-116">U kunt de gateway installeren op dezelfde virtuele machine als gegevensopslag of op een andere virtuele machine, zolang de gateway verbinding met de database maken kan.</span><span class="sxs-lookup"><span data-stu-id="c9a56-116">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>
- <span data-ttu-id="c9a56-117">**SAP NetWeaver bibliotheek** op de gateway-apparaat.</span><span class="sxs-lookup"><span data-stu-id="c9a56-117">**SAP NetWeaver library** on the gateway machine.</span></span> <span data-ttu-id="c9a56-118">U kunt de bibliotheek SAP Netweaver ophalen uit de SAP-beheerder of rechtstreeks uit de [SAP Software Download Center](https://support.sap.com/swdc).</span><span class="sxs-lookup"><span data-stu-id="c9a56-118">You can get the SAP Netweaver library from your SAP administrator, or directly from the [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="c9a56-119">Zoeken naar de **SAP-notitie #1025361** ophalen van de downloadlocatie voor de meest recente versie.</span><span class="sxs-lookup"><span data-stu-id="c9a56-119">Search for the **SAP Note #1025361** to get the download location for the most recent version.</span></span> <span data-ttu-id="c9a56-120">Zorg ervoor dat de architectuur voor de bibliotheek SAP NetWeaver (32-bits of 64-bits) overeenkomt met de gateway-installatie.</span><span class="sxs-lookup"><span data-stu-id="c9a56-120">Make sure that the architecture for the SAP NetWeaver library (32-bit or 64-bit) matches your gateway installation.</span></span> <span data-ttu-id="c9a56-121">Installeer vervolgens alle bestanden die zijn opgenomen in de SDK SAP NetWeaver RFC volgens de SAP-notitie.</span><span class="sxs-lookup"><span data-stu-id="c9a56-121">Then install all files included in the SAP NetWeaver RFC SDK according to the SAP Note.</span></span> <span data-ttu-id="c9a56-122">De bibliotheek SAP NetWeaver is ook opgenomen in de clienthulpprogramma's voor SAP-installatie.</span><span class="sxs-lookup"><span data-stu-id="c9a56-122">The SAP NetWeaver library is also included in the SAP Client Tools installation.</span></span>

> [!TIP]
> <span data-ttu-id="c9a56-123">De DLL's van de NetWeaver RFC-SDK hebt uitgepakt in de map system32 plaatsen.</span><span class="sxs-lookup"><span data-stu-id="c9a56-123">Put the dlls extracted from the NetWeaver RFC SDK into system32 folder.</span></span>

## <a name="getting-started"></a><span data-ttu-id="c9a56-124">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="c9a56-124">Getting started</span></span>
<span data-ttu-id="c9a56-125">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens vanuit een on-premises Cassandra-gegevensopslag verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="c9a56-125">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="c9a56-126">De eenvoudigste manier om een pijplijn maken is met de **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="c9a56-126">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="c9a56-127">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met de wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="c9a56-127">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="c9a56-128">U kunt ook de volgende hulpprogramma's gebruiken voor het maken van een pijplijn: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon**, **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="c9a56-128">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="c9a56-129">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies voor een pijplijn maken met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="c9a56-129">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="c9a56-130">Of u de hulpprogramma's of API's gebruiken, moet u de volgende stappen voor het maken van een pijplijn die de gegevens vanuit een brongegevensarchief naar een gegevensarchief sink verplaatst uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="c9a56-130">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="c9a56-131">Maak **gekoppelde services** slaat om invoer- en gegevens te koppelen aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="c9a56-131">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="c9a56-132">Maak **gegevenssets** vertegenwoordigt de invoer- en -gegevens voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="c9a56-132">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="c9a56-133">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="c9a56-133">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="c9a56-134">Wanneer u de wizard gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c9a56-134">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="c9a56-135">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van de JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="c9a56-135">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="c9a56-136">Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die worden gebruikt om gegevens te kopiëren van een lokale SAP Business Warehouse [JSON-voorbeeld: gegevens kopiëren van een SAP Business Warehouse naar Azure Blob](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="c9a56-136">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises SAP Business Warehouse, see [JSON example: Copy data from SAP Business Warehouse to Azure Blob](#json-example-copy-data-from-sap-business-warehouse-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="c9a56-137">De volgende secties bevatten informatie over de JSON-eigenschappen die worden gebruikt voor het definiëren van specifieke Data Factory-entiteiten met een SAP BW-gegevensopslag:</span><span class="sxs-lookup"><span data-stu-id="c9a56-137">The following sections provide details about JSON properties that are used to define Data Factory entities specific to an SAP BW data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="c9a56-138">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="c9a56-138">Linked service properties</span></span>
<span data-ttu-id="c9a56-139">De volgende tabel bevat een beschrijving voor JSON-elementen die specifiek zijn voor SAP Business Warehouse (BW) gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="c9a56-139">The following table provides description for JSON elements specific to SAP Business Warehouse (BW) linked service.</span></span>

<span data-ttu-id="c9a56-140">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="c9a56-140">Property</span></span> | <span data-ttu-id="c9a56-141">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c9a56-141">Description</span></span> | <span data-ttu-id="c9a56-142">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="c9a56-142">Allowed values</span></span> | <span data-ttu-id="c9a56-143">Vereist</span><span class="sxs-lookup"><span data-stu-id="c9a56-143">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="c9a56-144">server</span><span class="sxs-lookup"><span data-stu-id="c9a56-144">server</span></span> | <span data-ttu-id="c9a56-145">Naam van de server waarop het exemplaar SAP BW zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="c9a56-145">Name of the server on which the SAP BW instance resides.</span></span> | <span data-ttu-id="c9a56-146">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c9a56-146">string</span></span> | <span data-ttu-id="c9a56-147">Ja</span><span class="sxs-lookup"><span data-stu-id="c9a56-147">Yes</span></span>
<span data-ttu-id="c9a56-148">systemNumber</span><span class="sxs-lookup"><span data-stu-id="c9a56-148">systemNumber</span></span> | <span data-ttu-id="c9a56-149">Systeemnummer van het SAP BW-systeem.</span><span class="sxs-lookup"><span data-stu-id="c9a56-149">System number of the SAP BW system.</span></span> | <span data-ttu-id="c9a56-150">Twee cijfers decimaal getal weergegeven als een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="c9a56-150">Two-digit decimal number represented as a string.</span></span> | <span data-ttu-id="c9a56-151">Ja</span><span class="sxs-lookup"><span data-stu-id="c9a56-151">Yes</span></span>
<span data-ttu-id="c9a56-152">clientId</span><span class="sxs-lookup"><span data-stu-id="c9a56-152">clientId</span></span> | <span data-ttu-id="c9a56-153">Client-ID van de client in het systeem SAP-W.</span><span class="sxs-lookup"><span data-stu-id="c9a56-153">Client ID of the client in the SAP W system.</span></span> | <span data-ttu-id="c9a56-154">Drie cijfers decimaal getal weergegeven als een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="c9a56-154">Three-digit decimal number represented as a string.</span></span> | <span data-ttu-id="c9a56-155">Ja</span><span class="sxs-lookup"><span data-stu-id="c9a56-155">Yes</span></span>
<span data-ttu-id="c9a56-156">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="c9a56-156">username</span></span> | <span data-ttu-id="c9a56-157">Naam van de gebruiker die toegang tot de SAP-server heeft</span><span class="sxs-lookup"><span data-stu-id="c9a56-157">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="c9a56-158">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c9a56-158">string</span></span> | <span data-ttu-id="c9a56-159">Ja</span><span class="sxs-lookup"><span data-stu-id="c9a56-159">Yes</span></span>
<span data-ttu-id="c9a56-160">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="c9a56-160">password</span></span> | <span data-ttu-id="c9a56-161">Wachtwoord voor de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="c9a56-161">Password for the user.</span></span> | <span data-ttu-id="c9a56-162">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c9a56-162">string</span></span> | <span data-ttu-id="c9a56-163">Ja</span><span class="sxs-lookup"><span data-stu-id="c9a56-163">Yes</span></span>
<span data-ttu-id="c9a56-164">gatewayName</span><span class="sxs-lookup"><span data-stu-id="c9a56-164">gatewayName</span></span> | <span data-ttu-id="c9a56-165">Naam van de gateway die voor de Data Factory-service gebruiken moet voor verbinding met de lokale SAP BW-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="c9a56-165">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP BW instance.</span></span> | <span data-ttu-id="c9a56-166">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c9a56-166">string</span></span> | <span data-ttu-id="c9a56-167">Ja</span><span class="sxs-lookup"><span data-stu-id="c9a56-167">Yes</span></span>
<span data-ttu-id="c9a56-168">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="c9a56-168">encryptedCredential</span></span> | <span data-ttu-id="c9a56-169">De versleutelde referentie-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="c9a56-169">The encrypted credential string.</span></span> | <span data-ttu-id="c9a56-170">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c9a56-170">string</span></span> | <span data-ttu-id="c9a56-171">Nee</span><span class="sxs-lookup"><span data-stu-id="c9a56-171">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="c9a56-172">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="c9a56-172">Dataset properties</span></span>
<span data-ttu-id="c9a56-173">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van de [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="c9a56-173">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="c9a56-174">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).</span><span class="sxs-lookup"><span data-stu-id="c9a56-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="c9a56-175">De **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over de locatie van de gegevens in het gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="c9a56-175">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="c9a56-176">Er zijn geen type-specifieke eigenschappen voor de gegevensset SAP BW van het type ondersteund **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="c9a56-176">There are no type-specific properties supported for the SAP BW dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="c9a56-177">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="c9a56-177">Copy activity properties</span></span>
<span data-ttu-id="c9a56-178">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van activiteiten van de [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="c9a56-178">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="c9a56-179">Eigenschappen zoals naam, beschrijving, invoer en uitvoer tabellen, zijn de beleidsregels zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="c9a56-179">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="c9a56-180">Dat eigenschappen beschikbaar zijn in de **typeProperties** sectie van de activiteit variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="c9a56-180">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="c9a56-181">Voor de kopieeractiviteit variëren ze, afhankelijk van de typen van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="c9a56-181">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="c9a56-182">Wanneer u de gegevensbron in de kopieerbewerking is van het type **RelationalSource** (waaronder SAP BW), de volgende eigenschappen beschikbaar zijn in de sectie typeProperties:</span><span class="sxs-lookup"><span data-stu-id="c9a56-182">When source in copy activity is of type **RelationalSource** (which includes SAP BW), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="c9a56-183">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="c9a56-183">Property</span></span> | <span data-ttu-id="c9a56-184">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c9a56-184">Description</span></span> | <span data-ttu-id="c9a56-185">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="c9a56-185">Allowed values</span></span> | <span data-ttu-id="c9a56-186">Vereist</span><span class="sxs-lookup"><span data-stu-id="c9a56-186">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c9a56-187">query</span><span class="sxs-lookup"><span data-stu-id="c9a56-187">query</span></span> | <span data-ttu-id="c9a56-188">Hiermee geeft u de MDX-query om te lezen van gegevens uit de SAP BW-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="c9a56-188">Specifies the MDX query to read data from the SAP BW instance.</span></span> | <span data-ttu-id="c9a56-189">MDX-query.</span><span class="sxs-lookup"><span data-stu-id="c9a56-189">MDX query.</span></span> | <span data-ttu-id="c9a56-190">Ja</span><span class="sxs-lookup"><span data-stu-id="c9a56-190">Yes</span></span> |


## <a name="json-example-copy-data-from-sap-business-warehouse-to-azure-blob"></a><span data-ttu-id="c9a56-191">JSON-voorbeeld: gegevens kopiëren van een SAP Business Warehouse naar Azure Blob</span><span class="sxs-lookup"><span data-stu-id="c9a56-191">JSON example: Copy data from SAP Business Warehouse to Azure Blob</span></span>
<span data-ttu-id="c9a56-192">Het volgende voorbeeld bevat definities van de voorbeeld-JSON die u een pijplijn maken kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c9a56-192">The following example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="c9a56-193">Dit voorbeeld laat zien hoe gegevens kopiëren van een lokale SAP Business Warehouse naar een Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="c9a56-193">This sample shows how to copy data from an on-premises SAP Business Warehouse to an Azure Blob Storage.</span></span> <span data-ttu-id="c9a56-194">Echter, de gegevens kunnen worden gekopieerd **rechtstreeks** aan een van de PUT vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van de Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c9a56-194">However, data can be copied **directly** to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="c9a56-195">Dit voorbeeld bevat JSON-fragmenten.</span><span class="sxs-lookup"><span data-stu-id="c9a56-195">This sample provides JSON snippets.</span></span> <span data-ttu-id="c9a56-196">Dit omvat geen stapsgewijze instructies voor het maken van de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="c9a56-196">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="c9a56-197">Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor stapsgewijze instructies.</span><span class="sxs-lookup"><span data-stu-id="c9a56-197">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="c9a56-198">Het voorbeeld heeft de volgende data factory-entiteiten:</span><span class="sxs-lookup"><span data-stu-id="c9a56-198">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="c9a56-199">Een gekoppelde service van het type [SapBw](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c9a56-199">A linked service of type [SapBw](#linked-service-properties).</span></span>
2. <span data-ttu-id="c9a56-200">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c9a56-200">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="c9a56-201">Invoer [gegevensset](data-factory-create-datasets.md) van het type [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c9a56-201">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="c9a56-202">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c9a56-202">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="c9a56-203">Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [RelationalSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="c9a56-203">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="c9a56-204">Het voorbeeld worden gegevens gekopieerd van een SAP Business Warehouse-exemplaar met een Azure-blob per uur.</span><span class="sxs-lookup"><span data-stu-id="c9a56-204">The sample copies data from an SAP Business Warehouse instance to an Azure blob hourly.</span></span> <span data-ttu-id="c9a56-205">De JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na de voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="c9a56-205">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="c9a56-206">Het instellen van de data management gateway als eerste stap.</span><span class="sxs-lookup"><span data-stu-id="c9a56-206">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="c9a56-207">De instructies vindt u in de [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="c9a56-207">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-business-warehouse-linked-service"></a><span data-ttu-id="c9a56-208">SAP Business Warehouse gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="c9a56-208">SAP Business Warehouse linked service</span></span>
<span data-ttu-id="c9a56-209">Deze service koppelingen uw SAP BW-exemplaar gekoppeld aan de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="c9a56-209">This linked service links your SAP BW instance to the data factory.</span></span> <span data-ttu-id="c9a56-210">De eigenschap type is ingesteld op **SapBw**.</span><span class="sxs-lookup"><span data-stu-id="c9a56-210">The type property is set to **SapBw**.</span></span> <span data-ttu-id="c9a56-211">De sectie typeProperties biedt verbindingsgegevens voor het SAP BW-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="c9a56-211">The typeProperties section provides connection information for the SAP BW instance.</span></span> 

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

### <a name="azure-storage-linked-service"></a><span data-ttu-id="c9a56-212">Een gekoppelde Azure Storage-service</span><span class="sxs-lookup"><span data-stu-id="c9a56-212">Azure Storage linked service</span></span>
<span data-ttu-id="c9a56-213">Deze service koppelingen uw Azure Storage-account gekoppeld aan de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="c9a56-213">This linked service links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="c9a56-214">De eigenschap type is ingesteld op **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="c9a56-214">The type property is set to **AzureStorage**.</span></span> <span data-ttu-id="c9a56-215">De sectie typeProperties biedt verbindingsgegevens voor de Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="c9a56-215">The typeProperties section provides connection information for the Azure Storage account.</span></span>

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

### <a name="sap-bw-input-dataset"></a><span data-ttu-id="c9a56-216">Invoergegevensset voor SAP BW</span><span class="sxs-lookup"><span data-stu-id="c9a56-216">SAP BW input dataset</span></span>
<span data-ttu-id="c9a56-217">Deze gegevensset definieert de SAP Business Warehouse-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="c9a56-217">This dataset defines the SAP Business Warehouse dataset.</span></span> <span data-ttu-id="c9a56-218">Instellen van het type van de Data Factory-gegevensset **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="c9a56-218">You set the type of the Data Factory dataset to **RelationalTable**.</span></span> <span data-ttu-id="c9a56-219">Op dit moment kunt opgeeft u geen type-specifieke eigenschappen voor een gegevensset SAP BW.</span><span class="sxs-lookup"><span data-stu-id="c9a56-219">Currently, you do not specify any type-specific properties for an SAP BW dataset.</span></span> <span data-ttu-id="c9a56-220">De query in de definitie van de Kopieeractiviteit geeft aan welke gegevens moeten worden gelezen uit de SAP BW-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="c9a56-220">The query in the Copy Activity definition specifies what data to read from the SAP BW instance.</span></span> 

<span data-ttu-id="c9a56-221">De Data Factory-service als externe eigenschap instelt op true worden informeert dat de tabel aan de gegevensfactory extern en niet wordt geproduceerd door een activiteit in de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="c9a56-221">Setting external property to true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

<span data-ttu-id="c9a56-222">Frequentie en het interval eigenschappen definieert de planning.</span><span class="sxs-lookup"><span data-stu-id="c9a56-222">Frequency and interval properties defines the schedule.</span></span> <span data-ttu-id="c9a56-223">In dit geval worden de gegevens gelezen uit de SAP BW-exemplaar per uur.</span><span class="sxs-lookup"><span data-stu-id="c9a56-223">In this case, the data is read from the SAP BW instance hourly.</span></span> 

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



### <a name="azure-blob-output-dataset"></a><span data-ttu-id="c9a56-224">Azure Blob-uitvoergegevensset</span><span class="sxs-lookup"><span data-stu-id="c9a56-224">Azure Blob output dataset</span></span>
<span data-ttu-id="c9a56-225">Deze gegevensset definieert de uitvoer-Azure Blob-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="c9a56-225">This dataset defines the output Azure Blob dataset.</span></span> <span data-ttu-id="c9a56-226">De eigenschap type is ingesteld op AzureBlob.</span><span class="sxs-lookup"><span data-stu-id="c9a56-226">The type property is set to AzureBlob.</span></span> <span data-ttu-id="c9a56-227">De sectie typeProperties biedt waar de gegevens die zijn gekopieerd uit de SAP BW-exemplaar wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="c9a56-227">The typeProperties section provides where the data copied from the SAP BW instance is stored.</span></span> <span data-ttu-id="c9a56-228">De gegevens worden geschreven naar een nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="c9a56-228">The data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="c9a56-229">Het pad naar de blob wordt dynamisch geëvalueerd op basis van de begintijd van het segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="c9a56-229">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="c9a56-230">Het mappad maakt gebruik van jaar, maand, dag en uur delen van de begintijd.</span><span class="sxs-lookup"><span data-stu-id="c9a56-230">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="c9a56-231">Pijplijn met de kopieeractiviteit</span><span class="sxs-lookup"><span data-stu-id="c9a56-231">Pipeline with Copy activity</span></span>
<span data-ttu-id="c9a56-232">De pijplijn bevat een Kopieeractiviteit die is geconfigureerd voor gebruik van de invoer- en uitvoergegevenssets en elk uur is gepland.</span><span class="sxs-lookup"><span data-stu-id="c9a56-232">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="c9a56-233">In de pijplijn-JSON-definitie de **bron** type is ingesteld op **RelationalSource** (voor SAP BW-bron) en **sink** type is ingesteld op **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="c9a56-233">In the pipeline JSON definition, the **source** type is set to **RelationalSource** (for SAP BW source) and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="c9a56-234">De query is opgegeven voor de **query** eigenschap selecteert u de gegevens in het afgelopen uur te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="c9a56-234">The query specified for the **query** property selects the data in the past hour to copy.</span></span>

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



### <a name="type-mapping-for-sap-bw"></a><span data-ttu-id="c9a56-235">Toewijzing van het type voor SAP BW</span><span class="sxs-lookup"><span data-stu-id="c9a56-235">Type mapping for SAP BW</span></span>
<span data-ttu-id="c9a56-236">Zoals vermeld in de [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel kopieerbewerking wordt automatische typeconversies van brontypen opvangen typen met de volgende benadering voor in twee stappen uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="c9a56-236">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="c9a56-237">Systeemeigen brontypen converteren naar .NET-type</span><span class="sxs-lookup"><span data-stu-id="c9a56-237">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="c9a56-238">Converteren van .NET-type naar systeemeigen sink-type</span><span class="sxs-lookup"><span data-stu-id="c9a56-238">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="c9a56-239">Bij het verplaatsen van gegevens uit SAP BW, worden de volgende toewijzingen uit SAP BW typen gebruikt voor .NET-typen.</span><span class="sxs-lookup"><span data-stu-id="c9a56-239">When moving data from SAP BW, the following mappings are used from SAP BW types to .NET types.</span></span>

<span data-ttu-id="c9a56-240">Gegevenstype in de woordenlijst ABAP</span><span class="sxs-lookup"><span data-stu-id="c9a56-240">Data type in the ABAP Dictionary</span></span> | <span data-ttu-id="c9a56-241">.NET-gegevenstype</span><span class="sxs-lookup"><span data-stu-id="c9a56-241">.Net Data Type</span></span>
-------------------------------- | --------------
<span data-ttu-id="c9a56-242">ACCP</span><span class="sxs-lookup"><span data-stu-id="c9a56-242">ACCP</span></span> |  <span data-ttu-id="c9a56-243">int</span><span class="sxs-lookup"><span data-stu-id="c9a56-243">Int</span></span>
<span data-ttu-id="c9a56-244">CHAR</span><span class="sxs-lookup"><span data-stu-id="c9a56-244">CHAR</span></span> | <span data-ttu-id="c9a56-245">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c9a56-245">String</span></span>
<span data-ttu-id="c9a56-246">CLNT</span><span class="sxs-lookup"><span data-stu-id="c9a56-246">CLNT</span></span> | <span data-ttu-id="c9a56-247">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c9a56-247">String</span></span>
<span data-ttu-id="c9a56-248">VAL</span><span class="sxs-lookup"><span data-stu-id="c9a56-248">CURR</span></span> | <span data-ttu-id="c9a56-249">Decimale</span><span class="sxs-lookup"><span data-stu-id="c9a56-249">Decimal</span></span>
<span data-ttu-id="c9a56-250">CUKY</span><span class="sxs-lookup"><span data-stu-id="c9a56-250">CUKY</span></span> | <span data-ttu-id="c9a56-251">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c9a56-251">String</span></span>
<span data-ttu-id="c9a56-252">DECEMBER</span><span class="sxs-lookup"><span data-stu-id="c9a56-252">DEC</span></span> | <span data-ttu-id="c9a56-253">Decimale</span><span class="sxs-lookup"><span data-stu-id="c9a56-253">Decimal</span></span>
<span data-ttu-id="c9a56-254">FLTP</span><span class="sxs-lookup"><span data-stu-id="c9a56-254">FLTP</span></span> | <span data-ttu-id="c9a56-255">dubbele</span><span class="sxs-lookup"><span data-stu-id="c9a56-255">Double</span></span>
<span data-ttu-id="c9a56-256">INT1</span><span class="sxs-lookup"><span data-stu-id="c9a56-256">INT1</span></span> | <span data-ttu-id="c9a56-257">Byte</span><span class="sxs-lookup"><span data-stu-id="c9a56-257">Byte</span></span>
<span data-ttu-id="c9a56-258">INT2</span><span class="sxs-lookup"><span data-stu-id="c9a56-258">INT2</span></span> | <span data-ttu-id="c9a56-259">Int16</span><span class="sxs-lookup"><span data-stu-id="c9a56-259">Int16</span></span>
<span data-ttu-id="c9a56-260">INT4</span><span class="sxs-lookup"><span data-stu-id="c9a56-260">INT4</span></span> | <span data-ttu-id="c9a56-261">int</span><span class="sxs-lookup"><span data-stu-id="c9a56-261">Int</span></span>
<span data-ttu-id="c9a56-262">LANG</span><span class="sxs-lookup"><span data-stu-id="c9a56-262">LANG</span></span> | <span data-ttu-id="c9a56-263">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c9a56-263">String</span></span>
<span data-ttu-id="c9a56-264">LCHR</span><span class="sxs-lookup"><span data-stu-id="c9a56-264">LCHR</span></span> | <span data-ttu-id="c9a56-265">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c9a56-265">String</span></span>
<span data-ttu-id="c9a56-266">LRAW</span><span class="sxs-lookup"><span data-stu-id="c9a56-266">LRAW</span></span> | <span data-ttu-id="c9a56-267">Byte]</span><span class="sxs-lookup"><span data-stu-id="c9a56-267">Byte[]</span></span>
<span data-ttu-id="c9a56-268">PREC</span><span class="sxs-lookup"><span data-stu-id="c9a56-268">PREC</span></span> | <span data-ttu-id="c9a56-269">Int16</span><span class="sxs-lookup"><span data-stu-id="c9a56-269">Int16</span></span>
<span data-ttu-id="c9a56-270">QUAN</span><span class="sxs-lookup"><span data-stu-id="c9a56-270">QUAN</span></span> | <span data-ttu-id="c9a56-271">Decimale</span><span class="sxs-lookup"><span data-stu-id="c9a56-271">Decimal</span></span>
<span data-ttu-id="c9a56-272">ONBEWERKTE</span><span class="sxs-lookup"><span data-stu-id="c9a56-272">RAW</span></span> | <span data-ttu-id="c9a56-273">Byte]</span><span class="sxs-lookup"><span data-stu-id="c9a56-273">Byte[]</span></span>
<span data-ttu-id="c9a56-274">RAWSTRING</span><span class="sxs-lookup"><span data-stu-id="c9a56-274">RAWSTRING</span></span> | <span data-ttu-id="c9a56-275">Byte]</span><span class="sxs-lookup"><span data-stu-id="c9a56-275">Byte[]</span></span>
<span data-ttu-id="c9a56-276">TEKENREEKS</span><span class="sxs-lookup"><span data-stu-id="c9a56-276">STRING</span></span> | <span data-ttu-id="c9a56-277">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c9a56-277">String</span></span>
<span data-ttu-id="c9a56-278">EENHEID</span><span class="sxs-lookup"><span data-stu-id="c9a56-278">UNIT</span></span> | <span data-ttu-id="c9a56-279">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c9a56-279">String</span></span>
<span data-ttu-id="c9a56-280">DATS</span><span class="sxs-lookup"><span data-stu-id="c9a56-280">DATS</span></span> | <span data-ttu-id="c9a56-281">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c9a56-281">String</span></span>
<span data-ttu-id="c9a56-282">NUMC</span><span class="sxs-lookup"><span data-stu-id="c9a56-282">NUMC</span></span> | <span data-ttu-id="c9a56-283">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c9a56-283">String</span></span>
<span data-ttu-id="c9a56-284">TIM 'S</span><span class="sxs-lookup"><span data-stu-id="c9a56-284">TIMS</span></span> | <span data-ttu-id="c9a56-285">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="c9a56-285">String</span></span>

> [!NOTE]
> <span data-ttu-id="c9a56-286">Zie het toewijzen van kolommen uit de bron-gegevensset naar kolommen uit de dataset sink [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="c9a56-286">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>


## <a name="map-source-to-sink-columns"></a><span data-ttu-id="c9a56-287">Bron van de kaart opvangen kolommen</span><span class="sxs-lookup"><span data-stu-id="c9a56-287">Map source to sink columns</span></span>
<span data-ttu-id="c9a56-288">Zie voor meer informatie over het toewijzen van kolommen in gegevensset naar kolommen in gegevensset sink bron, [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="c9a56-288">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="c9a56-289">Herhaalbare leesbewerking van relationele bronnen</span><span class="sxs-lookup"><span data-stu-id="c9a56-289">Repeatable read from relational sources</span></span>
<span data-ttu-id="c9a56-290">Bij het kopiëren van gegevens van relationele gegevens worden opgeslagen, moet u herhaalbaarheid Houd in gedachten om te voorkomen dat ongewenste resultaten.</span><span class="sxs-lookup"><span data-stu-id="c9a56-290">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="c9a56-291">In Azure Data Factory, kunt u een segment handmatig opnieuw.</span><span class="sxs-lookup"><span data-stu-id="c9a56-291">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="c9a56-292">U kunt ook een beleid voor opnieuw proberen voor een gegevensset configureren zodat een segment wordt opnieuw uitgevoerd wanneer een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="c9a56-292">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="c9a56-293">Wanneer een segment opnieuw in beide gevallen wordt uitgevoerd, moet u ervoor zorgen dat dezelfde gegevens is gelezen ongeacht hoe vaak een segment wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c9a56-293">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="c9a56-294">Zie [Repeatable van relationele bronnen lezen](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="c9a56-294">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="c9a56-295">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="c9a56-295">Performance and Tuning</span></span>
<span data-ttu-id="c9a56-296">Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) voor meer informatie over de belangrijkste factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren om te optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="c9a56-296">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
