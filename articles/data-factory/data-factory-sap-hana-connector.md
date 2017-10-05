---
title: Verplaatsen van gegevens uit een SAP HANA met behulp van Azure Data Factory | Microsoft Docs
description: Meer informatie over het verplaatsen van gegevens uit een SAP HANA met behulp van Azure Data Factory.
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
ms.openlocfilehash: 2ab488d82d24999a6231e40cb719715463c51d64
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-sap-hana-using-azure-data-factory"></a><span data-ttu-id="16354-103">Verplaatsen van gegevens uit SAP HANA, met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="16354-103">Move data From SAP HANA using Azure Data Factory</span></span>
<span data-ttu-id="16354-104">Dit artikel wordt uitgelegd hoe u de Kopieeractiviteit in Azure Data Factory om gegevens te verplaatsen van een lokale SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="16354-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises SAP HANA.</span></span> <span data-ttu-id="16354-105">Dit is gebaseerd op de [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, hetgeen een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit toont.</span><span class="sxs-lookup"><span data-stu-id="16354-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="16354-106">U kunt gegevens uit een on-premises SAP HANA-gegevensopslag kopiëren naar een ondersteunde sink-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="16354-106">You can copy data from an on-premises SAP HANA data store to any supported sink data store.</span></span> <span data-ttu-id="16354-107">Zie voor een lijst met gegevensarchieven als PUT wordt ondersteund door de kopieeractiviteit, de [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel.</span><span class="sxs-lookup"><span data-stu-id="16354-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="16354-108">Data factory ondersteunt momenteel alleen zwevend gegevens uit een SAP HANA tot andere gegevensarchieven, maar niet voor het verplaatsen van gegevens uit andere gegevensarchieven naar een SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="16354-108">Data factory currently supports only moving data from an SAP HANA to other data stores, but not for moving data from other data stores to an SAP HANA.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="16354-109">Ondersteunde versies en installatie</span><span class="sxs-lookup"><span data-stu-id="16354-109">Supported versions and installation</span></span>
<span data-ttu-id="16354-110">Deze connector ondersteunt een willekeurige versie van de SAP HANA-database.</span><span class="sxs-lookup"><span data-stu-id="16354-110">This connector supports any version of SAP HANA database.</span></span> <span data-ttu-id="16354-111">Het ondersteunt kopiëren van gegevens van HANA informatiemodellen (zoals weergaven, analyse en berekening) en rij/kolom tabellen met behulp van SQL-query's.</span><span class="sxs-lookup"><span data-stu-id="16354-111">It supports copying data from HANA information models (such as Analytic and Calculation views) and Row/Column tables using SQL queries.</span></span>

<span data-ttu-id="16354-112">Installeer de volgende onderdelen te maken van de verbinding met de SAP HANA-exemplaar:</span><span class="sxs-lookup"><span data-stu-id="16354-112">To enable the connectivity to the SAP HANA instance, install the following components:</span></span>
- <span data-ttu-id="16354-113">**Data Management Gateway**: Data Factory-service ondersteunt het verbinden met on-premises gegevens winkels (inclusief SAP HANA) met een onderdeel genaamd Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="16354-113">**Data Management Gateway**: Data Factory service supports connecting to on-premises data stores (including SAP HANA) using a component called Data Management Gateway.</span></span> <span data-ttu-id="16354-114">Zie voor meer informatie over Data Management Gateway en stapsgewijze instructies voor het instellen van de gateway, [Moving gegevens tussen on-premises gegevens opslaan in de cloud gegevensarchief](data-factory-move-data-between-onprem-and-cloud.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="16354-114">To learn about Data Management Gateway and step-by-step instructions for setting up the gateway, see [Moving data between on-premises data store to cloud data store](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span> <span data-ttu-id="16354-115">Gateway is vereist, zelfs als de SAP HANA wordt gehost in een Azure IaaS virtuele machine (VM).</span><span class="sxs-lookup"><span data-stu-id="16354-115">Gateway is required even if the SAP HANA is hosted in an Azure IaaS virtual machine (VM).</span></span> <span data-ttu-id="16354-116">U kunt de gateway installeren op dezelfde virtuele machine als gegevensopslag of op een andere virtuele machine, zolang de gateway verbinding met de database maken kan.</span><span class="sxs-lookup"><span data-stu-id="16354-116">You can install the gateway on the same VM as the data store or on a different VM as long as the gateway can connect to the database.</span></span>
- <span data-ttu-id="16354-117">**SAP HANA ODBC-stuurprogramma** op de gateway-apparaat.</span><span class="sxs-lookup"><span data-stu-id="16354-117">**SAP HANA ODBC driver** on the gateway machine.</span></span> <span data-ttu-id="16354-118">U kunt downloaden de SAP HANA ODBC-stuurprogramma van de [SAP Software Download Center](https://support.sap.com/swdc).</span><span class="sxs-lookup"><span data-stu-id="16354-118">You can download the SAP HANA ODBC driver from the [SAP Software Download Center](https://support.sap.com/swdc).</span></span> <span data-ttu-id="16354-119">Zoeken met het trefwoord **SAP HANA-CLIENT voor Windows**.</span><span class="sxs-lookup"><span data-stu-id="16354-119">Search with the keyword **SAP HANA CLIENT for Windows**.</span></span> 

## <a name="getting-started"></a><span data-ttu-id="16354-120">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="16354-120">Getting started</span></span>
<span data-ttu-id="16354-121">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens vanuit een on-premises Cassandra-gegevensopslag verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="16354-121">You can create a pipeline with a copy activity that moves data from an on-premises Cassandra data store by using different tools/APIs.</span></span> 

- <span data-ttu-id="16354-122">De eenvoudigste manier om een pijplijn maken is met de **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="16354-122">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="16354-123">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met de wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="16354-123">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span> 
- <span data-ttu-id="16354-124">U kunt ook de volgende hulpprogramma's gebruiken voor het maken van een pijplijn: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon**, **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="16354-124">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="16354-125">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies voor een pijplijn maken met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="16354-125">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="16354-126">Of u de hulpprogramma's of API's gebruiken, moet u de volgende stappen voor het maken van een pijplijn die de gegevens vanuit een brongegevensarchief naar een gegevensarchief sink verplaatst uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="16354-126">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="16354-127">Maak **gekoppelde services** slaat om invoer- en gegevens te koppelen aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="16354-127">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="16354-128">Maak **gegevenssets** vertegenwoordigt de invoer- en -gegevens voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="16354-128">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="16354-129">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="16354-129">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="16354-130">Wanneer u de wizard gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="16354-130">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="16354-131">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van de JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="16354-131">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="16354-132">Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die worden gebruikt om gegevens te kopiëren van een lokale SAP HANA [JSON-voorbeeld: gegevens kopiëren van SAP HANA naar Azure Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="16354-132">For a sample with JSON definitions for Data Factory entities that are used to copy data from an on-premises SAP HANA, see [JSON example: Copy data from SAP HANA to Azure Blob](#json-example-copy-data-from-sap-hana-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="16354-133">De volgende secties bevatten informatie over de JSON-eigenschappen die worden gebruikt voor het definiëren van specifieke Data Factory-entiteiten met een SAP HANA-gegevensopslag:</span><span class="sxs-lookup"><span data-stu-id="16354-133">The following sections provide details about JSON properties that are used to define Data Factory entities specific to an SAP HANA data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="16354-134">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="16354-134">Linked service properties</span></span>
<span data-ttu-id="16354-135">De volgende tabel bevat een beschrijving voor JSON-elementen die specifiek zijn voor SAP HANA gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="16354-135">The following table provides description for JSON elements specific to SAP HANA linked service.</span></span>

<span data-ttu-id="16354-136">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="16354-136">Property</span></span> | <span data-ttu-id="16354-137">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="16354-137">Description</span></span> | <span data-ttu-id="16354-138">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="16354-138">Allowed values</span></span> | <span data-ttu-id="16354-139">Vereist</span><span class="sxs-lookup"><span data-stu-id="16354-139">Required</span></span>
-------- | ----------- | -------------- | --------
<span data-ttu-id="16354-140">server</span><span class="sxs-lookup"><span data-stu-id="16354-140">server</span></span> | <span data-ttu-id="16354-141">Naam van de server waarop het exemplaar SAP HANA zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="16354-141">Name of the server on which the SAP HANA instance resides.</span></span> <span data-ttu-id="16354-142">Als de server een aangepaste poort gebruikt is, geeft u `server:port`.</span><span class="sxs-lookup"><span data-stu-id="16354-142">If your server is using a customized port, specify `server:port`.</span></span> | <span data-ttu-id="16354-143">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="16354-143">string</span></span> | <span data-ttu-id="16354-144">Ja</span><span class="sxs-lookup"><span data-stu-id="16354-144">Yes</span></span>
<span data-ttu-id="16354-145">authenticationType</span><span class="sxs-lookup"><span data-stu-id="16354-145">authenticationType</span></span> | <span data-ttu-id="16354-146">Het type verificatie.</span><span class="sxs-lookup"><span data-stu-id="16354-146">Type of authentication.</span></span> | <span data-ttu-id="16354-147">De tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="16354-147">string.</span></span> <span data-ttu-id="16354-148">'Basic' of 'Windows'</span><span class="sxs-lookup"><span data-stu-id="16354-148">"Basic" or "Windows"</span></span> | <span data-ttu-id="16354-149">Ja</span><span class="sxs-lookup"><span data-stu-id="16354-149">Yes</span></span> 
<span data-ttu-id="16354-150">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="16354-150">username</span></span> | <span data-ttu-id="16354-151">Naam van de gebruiker die toegang tot de SAP-server heeft</span><span class="sxs-lookup"><span data-stu-id="16354-151">Name of the user who has access to the SAP server</span></span> | <span data-ttu-id="16354-152">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="16354-152">string</span></span> | <span data-ttu-id="16354-153">Ja</span><span class="sxs-lookup"><span data-stu-id="16354-153">Yes</span></span>
<span data-ttu-id="16354-154">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="16354-154">password</span></span> | <span data-ttu-id="16354-155">Wachtwoord voor de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="16354-155">Password for the user.</span></span> | <span data-ttu-id="16354-156">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="16354-156">string</span></span> | <span data-ttu-id="16354-157">Ja</span><span class="sxs-lookup"><span data-stu-id="16354-157">Yes</span></span>
<span data-ttu-id="16354-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="16354-158">gatewayName</span></span> | <span data-ttu-id="16354-159">Naam van de gateway die voor de Data Factory-service gebruiken moet voor verbinding met de lokale SAP HANA-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="16354-159">Name of the gateway that the Data Factory service should use to connect to the on-premises SAP HANA instance.</span></span> | <span data-ttu-id="16354-160">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="16354-160">string</span></span> | <span data-ttu-id="16354-161">Ja</span><span class="sxs-lookup"><span data-stu-id="16354-161">Yes</span></span>
<span data-ttu-id="16354-162">encryptedCredential</span><span class="sxs-lookup"><span data-stu-id="16354-162">encryptedCredential</span></span> | <span data-ttu-id="16354-163">De versleutelde referentie-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="16354-163">The encrypted credential string.</span></span> | <span data-ttu-id="16354-164">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="16354-164">string</span></span> | <span data-ttu-id="16354-165">Nee</span><span class="sxs-lookup"><span data-stu-id="16354-165">No</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="16354-166">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="16354-166">Dataset properties</span></span>
<span data-ttu-id="16354-167">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van de [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="16354-167">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="16354-168">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).</span><span class="sxs-lookup"><span data-stu-id="16354-168">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="16354-169">De **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over de locatie van de gegevens in het gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="16354-169">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="16354-170">Er zijn geen type-specifieke eigenschappen voor de gegevensset SAP HANA van het type ondersteund **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="16354-170">There are no type-specific properties supported for the SAP HANA dataset of type **RelationalTable**.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="16354-171">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="16354-171">Copy activity properties</span></span>
<span data-ttu-id="16354-172">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van activiteiten van de [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="16354-172">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="16354-173">Eigenschappen zoals naam, beschrijving, invoer en uitvoer tabellen, zijn de beleidsregels zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="16354-173">Properties such as name, description, input and output tables, are policies are available for all types of activities.</span></span>

<span data-ttu-id="16354-174">Dat eigenschappen beschikbaar zijn in de **typeProperties** sectie van de activiteit variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="16354-174">Whereas, properties available in the **typeProperties** section of the activity vary with each activity type.</span></span> <span data-ttu-id="16354-175">Voor de kopieeractiviteit variëren ze, afhankelijk van de typen van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="16354-175">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="16354-176">Wanneer u de gegevensbron in de kopieerbewerking is van het type **RelationalSource** (waaronder SAP HANA), de volgende eigenschappen beschikbaar zijn in de sectie typeProperties:</span><span class="sxs-lookup"><span data-stu-id="16354-176">When source in copy activity is of type **RelationalSource** (which includes SAP HANA), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="16354-177">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="16354-177">Property</span></span> | <span data-ttu-id="16354-178">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="16354-178">Description</span></span> | <span data-ttu-id="16354-179">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="16354-179">Allowed values</span></span> | <span data-ttu-id="16354-180">Vereist</span><span class="sxs-lookup"><span data-stu-id="16354-180">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="16354-181">query</span><span class="sxs-lookup"><span data-stu-id="16354-181">query</span></span> | <span data-ttu-id="16354-182">Hiermee geeft u de SQL-query voor het lezen van gegevens uit de SAP HANA-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="16354-182">Specifies the SQL query to read data from the SAP HANA instance.</span></span> | <span data-ttu-id="16354-183">SQL-query.</span><span class="sxs-lookup"><span data-stu-id="16354-183">SQL query.</span></span> | <span data-ttu-id="16354-184">Ja</span><span class="sxs-lookup"><span data-stu-id="16354-184">Yes</span></span> |

## <a name="json-example-copy-data-from-sap-hana-to-azure-blob"></a><span data-ttu-id="16354-185">JSON-voorbeeld: gegevens kopiëren van SAP HANA naar Azure Blob</span><span class="sxs-lookup"><span data-stu-id="16354-185">JSON example: Copy data from SAP HANA to Azure Blob</span></span>
<span data-ttu-id="16354-186">Het volgende voorbeeld bevat definities van de voorbeeld-JSON die u een pijplijn maken kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="16354-186">The following sample provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="16354-187">Dit voorbeeld laat zien hoe gegevens kopiëren van een lokale SAP HANA naar een Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="16354-187">This sample shows how to copy data from an on-premises SAP HANA to an Azure Blob Storage.</span></span> <span data-ttu-id="16354-188">Echter, de gegevens kunnen worden gekopieerd **rechtstreeks** vermeld met een van de PUT [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van de Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="16354-188">However, data can be copied **directly** to any of the sinks listed [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="16354-189">Dit voorbeeld bevat JSON-fragmenten.</span><span class="sxs-lookup"><span data-stu-id="16354-189">This sample provides JSON snippets.</span></span> <span data-ttu-id="16354-190">Dit omvat geen stapsgewijze instructies voor het maken van de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="16354-190">It does not include step-by-step instructions for creating the data factory.</span></span> <span data-ttu-id="16354-191">Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor stapsgewijze instructies.</span><span class="sxs-lookup"><span data-stu-id="16354-191">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions.</span></span>

<span data-ttu-id="16354-192">Het voorbeeld heeft de volgende data factory-entiteiten:</span><span class="sxs-lookup"><span data-stu-id="16354-192">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="16354-193">Een gekoppelde service van het type [SapHana](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="16354-193">A linked service of type [SapHana](#linked-service-properties).</span></span>
2. <span data-ttu-id="16354-194">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="16354-194">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="16354-195">Invoer [gegevensset](data-factory-create-datasets.md) van het type [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="16354-195">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="16354-196">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="16354-196">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="16354-197">Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [RelationalSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="16354-197">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="16354-198">Het voorbeeld worden gegevens gekopieerd van een SAP HANA-exemplaar met een Azure-blob per uur.</span><span class="sxs-lookup"><span data-stu-id="16354-198">The sample copies data from an SAP HANA instance to an Azure blob hourly.</span></span> <span data-ttu-id="16354-199">De JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na de voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="16354-199">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="16354-200">Het instellen van de data management gateway als eerste stap.</span><span class="sxs-lookup"><span data-stu-id="16354-200">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="16354-201">De instructies vindt u in de [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="16354-201">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

### <a name="sap-hana-linked-service"></a><span data-ttu-id="16354-202">SAP HANA gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="16354-202">SAP HANA linked service</span></span>
<span data-ttu-id="16354-203">Deze service koppelingen uw SAP HANA-exemplaar gekoppeld aan de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="16354-203">This linked service links your SAP HANA instance to the data factory.</span></span> <span data-ttu-id="16354-204">De eigenschap type is ingesteld op **SapHana**.</span><span class="sxs-lookup"><span data-stu-id="16354-204">The type property is set to **SapHana**.</span></span> <span data-ttu-id="16354-205">De sectie typeProperties biedt verbindingsgegevens voor het SAP HANA-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="16354-205">The typeProperties section provides connection information for the SAP HANA instance.</span></span>

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

### <a name="azure-storage-linked-service"></a><span data-ttu-id="16354-206">Een gekoppelde Azure Storage-service</span><span class="sxs-lookup"><span data-stu-id="16354-206">Azure Storage linked service</span></span>
<span data-ttu-id="16354-207">Deze service koppelingen uw Azure Storage-account gekoppeld aan de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="16354-207">This linked service links your Azure Storage account to the data factory.</span></span> <span data-ttu-id="16354-208">De eigenschap type is ingesteld op **AzureStorage**.</span><span class="sxs-lookup"><span data-stu-id="16354-208">The type property is set to **AzureStorage**.</span></span> <span data-ttu-id="16354-209">De sectie typeProperties biedt verbindingsgegevens voor de Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="16354-209">The typeProperties section provides connection information for the Azure Storage account.</span></span>

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

### <a name="sap-hana-input-dataset"></a><span data-ttu-id="16354-210">SAP HANA-invoergegevensset</span><span class="sxs-lookup"><span data-stu-id="16354-210">SAP HANA input dataset</span></span>

<span data-ttu-id="16354-211">Deze gegevensset definieert de SAP HANA-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="16354-211">This dataset defines the SAP HANA dataset.</span></span> <span data-ttu-id="16354-212">Instellen van het type van de Data Factory-gegevensset **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="16354-212">You set the type of the Data Factory dataset to **RelationalTable**.</span></span> <span data-ttu-id="16354-213">Op dit moment kunt opgeeft u geen type-specifieke eigenschappen voor een SAP HANA-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="16354-213">Currently, you do not specify any type-specific properties for an SAP HANA dataset.</span></span> <span data-ttu-id="16354-214">De query in de definitie van de Kopieeractiviteit geeft aan welke gegevens moeten worden gelezen uit de SAP HANA-exemplaar.</span><span class="sxs-lookup"><span data-stu-id="16354-214">The query in the Copy Activity definition specifies what data to read from the SAP HANA instance.</span></span> 

<span data-ttu-id="16354-215">De Data Factory-service als externe eigenschap instelt op true worden informeert dat de tabel aan de gegevensfactory extern en niet wordt geproduceerd door een activiteit in de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="16354-215">Setting external property to true informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

<span data-ttu-id="16354-216">Frequentie en het interval eigenschappen definieert de planning.</span><span class="sxs-lookup"><span data-stu-id="16354-216">Frequency and interval properties defines the schedule.</span></span> <span data-ttu-id="16354-217">In dit geval worden de gegevens gelezen uit de SAP HANA-exemplaar per uur.</span><span class="sxs-lookup"><span data-stu-id="16354-217">In this case, the data is read from the SAP HANA instance hourly.</span></span> 

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

### <a name="azure-blob-output-dataset"></a><span data-ttu-id="16354-218">Azure Blob-uitvoergegevensset</span><span class="sxs-lookup"><span data-stu-id="16354-218">Azure Blob output dataset</span></span>
<span data-ttu-id="16354-219">Deze gegevensset definieert de uitvoer-Azure Blob-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="16354-219">This dataset defines the output Azure Blob dataset.</span></span> <span data-ttu-id="16354-220">De eigenschap type is ingesteld op AzureBlob.</span><span class="sxs-lookup"><span data-stu-id="16354-220">The type property is set to AzureBlob.</span></span> <span data-ttu-id="16354-221">De sectie typeProperties biedt waar de gegevens die zijn gekopieerd uit de SAP HANA-exemplaar wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="16354-221">The typeProperties section provides where the data copied from the SAP HANA instance is stored.</span></span> <span data-ttu-id="16354-222">De gegevens worden geschreven naar een nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="16354-222">The data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="16354-223">Het pad naar de blob wordt dynamisch geëvalueerd op basis van de begintijd van het segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="16354-223">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="16354-224">Het mappad maakt gebruik van jaar, maand, dag en uur delen van de begintijd.</span><span class="sxs-lookup"><span data-stu-id="16354-224">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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


### <a name="pipeline-with-copy-activity"></a><span data-ttu-id="16354-225">Pijplijn met de kopieeractiviteit</span><span class="sxs-lookup"><span data-stu-id="16354-225">Pipeline with Copy activity</span></span>

<span data-ttu-id="16354-226">De pijplijn bevat een Kopieeractiviteit die is geconfigureerd voor gebruik van de invoer- en uitvoergegevenssets en elk uur is gepland.</span><span class="sxs-lookup"><span data-stu-id="16354-226">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="16354-227">In de pijplijn-JSON-definitie de **bron** type is ingesteld op **RelationalSource** (voor SAP HANA-bron) en **sink** type is ingesteld op **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="16354-227">In the pipeline JSON definition, the **source** type is set to **RelationalSource** (for SAP HANA source) and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="16354-228">De SQL-query die is opgegeven voor de **query** eigenschap selecteert u de gegevens in het afgelopen uur te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="16354-228">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

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


### <a name="type-mapping-for-sap-hana"></a><span data-ttu-id="16354-229">Toewijzing van het type voor SAP HANA</span><span class="sxs-lookup"><span data-stu-id="16354-229">Type mapping for SAP HANA</span></span>
<span data-ttu-id="16354-230">Zoals vermeld in de [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel kopieerbewerking wordt automatische typeconversies van brontypen opvangen typen met de volgende benadering voor in twee stappen uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="16354-230">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="16354-231">Systeemeigen brontypen converteren naar .NET-type</span><span class="sxs-lookup"><span data-stu-id="16354-231">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="16354-232">Converteren van .NET-type naar systeemeigen sink-type</span><span class="sxs-lookup"><span data-stu-id="16354-232">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="16354-233">Bij het verplaatsen van gegevens uit een SAP HANA, worden de volgende toewijzingen uit SAP HANA-typen gebruikt voor .NET-typen.</span><span class="sxs-lookup"><span data-stu-id="16354-233">When moving data from SAP HANA, the following mappings are used from SAP HANA types to .NET types.</span></span>

<span data-ttu-id="16354-234">SAP HANA-Type</span><span class="sxs-lookup"><span data-stu-id="16354-234">SAP HANA Type</span></span> | <span data-ttu-id="16354-235">.NET op basis van Type</span><span class="sxs-lookup"><span data-stu-id="16354-235">.NET Based Type</span></span>
------------- | ---------------
<span data-ttu-id="16354-236">TINYINT</span><span class="sxs-lookup"><span data-stu-id="16354-236">TINYINT</span></span> | <span data-ttu-id="16354-237">Byte</span><span class="sxs-lookup"><span data-stu-id="16354-237">Byte</span></span>
<span data-ttu-id="16354-238">SMALLINT</span><span class="sxs-lookup"><span data-stu-id="16354-238">SMALLINT</span></span> | <span data-ttu-id="16354-239">Int16</span><span class="sxs-lookup"><span data-stu-id="16354-239">Int16</span></span>
<span data-ttu-id="16354-240">INT</span><span class="sxs-lookup"><span data-stu-id="16354-240">INT</span></span> | <span data-ttu-id="16354-241">Int32</span><span class="sxs-lookup"><span data-stu-id="16354-241">Int32</span></span>
<span data-ttu-id="16354-242">BIGINT</span><span class="sxs-lookup"><span data-stu-id="16354-242">BIGINT</span></span> | <span data-ttu-id="16354-243">Int64</span><span class="sxs-lookup"><span data-stu-id="16354-243">Int64</span></span>
<span data-ttu-id="16354-244">ECHTE</span><span class="sxs-lookup"><span data-stu-id="16354-244">REAL</span></span> | <span data-ttu-id="16354-245">Één</span><span class="sxs-lookup"><span data-stu-id="16354-245">Single</span></span>
<span data-ttu-id="16354-246">DOUBLE</span><span class="sxs-lookup"><span data-stu-id="16354-246">DOUBLE</span></span> | <span data-ttu-id="16354-247">Één</span><span class="sxs-lookup"><span data-stu-id="16354-247">Single</span></span>
<span data-ttu-id="16354-248">DECIMALE</span><span class="sxs-lookup"><span data-stu-id="16354-248">DECIMAL</span></span> | <span data-ttu-id="16354-249">Decimale</span><span class="sxs-lookup"><span data-stu-id="16354-249">Decimal</span></span>
<span data-ttu-id="16354-250">BOOLEAANSE WAARDE</span><span class="sxs-lookup"><span data-stu-id="16354-250">BOOLEAN</span></span> | <span data-ttu-id="16354-251">Byte</span><span class="sxs-lookup"><span data-stu-id="16354-251">Byte</span></span>
<span data-ttu-id="16354-252">VARCHAR</span><span class="sxs-lookup"><span data-stu-id="16354-252">VARCHAR</span></span> | <span data-ttu-id="16354-253">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="16354-253">String</span></span>
<span data-ttu-id="16354-254">NVARCHAR</span><span class="sxs-lookup"><span data-stu-id="16354-254">NVARCHAR</span></span> | <span data-ttu-id="16354-255">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="16354-255">String</span></span>
<span data-ttu-id="16354-256">CLOB</span><span class="sxs-lookup"><span data-stu-id="16354-256">CLOB</span></span> | <span data-ttu-id="16354-257">Byte]</span><span class="sxs-lookup"><span data-stu-id="16354-257">Byte[]</span></span>
<span data-ttu-id="16354-258">ALPHANUM</span><span class="sxs-lookup"><span data-stu-id="16354-258">ALPHANUM</span></span> | <span data-ttu-id="16354-259">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="16354-259">String</span></span>
<span data-ttu-id="16354-260">BLOB</span><span class="sxs-lookup"><span data-stu-id="16354-260">BLOB</span></span> | <span data-ttu-id="16354-261">Byte]</span><span class="sxs-lookup"><span data-stu-id="16354-261">Byte[]</span></span>
<span data-ttu-id="16354-262">DATUM</span><span class="sxs-lookup"><span data-stu-id="16354-262">DATE</span></span> | <span data-ttu-id="16354-263">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="16354-263">DateTime</span></span>
<span data-ttu-id="16354-264">TIJD</span><span class="sxs-lookup"><span data-stu-id="16354-264">TIME</span></span> | <span data-ttu-id="16354-265">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="16354-265">TimeSpan</span></span>
<span data-ttu-id="16354-266">TIJDSTEMPEL</span><span class="sxs-lookup"><span data-stu-id="16354-266">TIMESTAMP</span></span> | <span data-ttu-id="16354-267">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="16354-267">DateTime</span></span>
<span data-ttu-id="16354-268">SECONDDATE</span><span class="sxs-lookup"><span data-stu-id="16354-268">SECONDDATE</span></span> | <span data-ttu-id="16354-269">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="16354-269">DateTime</span></span>

## <a name="known-limitations"></a><span data-ttu-id="16354-270">Bekende beperkingen</span><span class="sxs-lookup"><span data-stu-id="16354-270">Known limitations</span></span>
<span data-ttu-id="16354-271">Er zijn enkele bekende beperkingen bij het kopiëren van gegevens uit een SAP HANA:</span><span class="sxs-lookup"><span data-stu-id="16354-271">There are a few known limitations when copying data from SAP HANA:</span></span>

- <span data-ttu-id="16354-272">NVARCHAR tekenreeksen worden afgekapt tot de maximale lengte van 4000 Unicode-tekens</span><span class="sxs-lookup"><span data-stu-id="16354-272">NVARCHAR strings are truncated to maximum length of 4000 Unicode characters</span></span>
- <span data-ttu-id="16354-273">SMALLDECIMAL wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="16354-273">SMALLDECIMAL is not supported</span></span>
- <span data-ttu-id="16354-274">VARBINARY wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="16354-274">VARBINARY is not supported</span></span>
- <span data-ttu-id="16354-275">Geldige datums tussen 12-1899/30 zijn en 12-9999/31</span><span class="sxs-lookup"><span data-stu-id="16354-275">Valid Dates are between 1899/12/30 and 9999/12/31</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="16354-276">Bron van de kaart opvangen kolommen</span><span class="sxs-lookup"><span data-stu-id="16354-276">Map source to sink columns</span></span>
<span data-ttu-id="16354-277">Zie voor meer informatie over het toewijzen van kolommen in gegevensset naar kolommen in gegevensset sink bron, [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="16354-277">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="16354-278">Herhaalbare leesbewerking van relationele bronnen</span><span class="sxs-lookup"><span data-stu-id="16354-278">Repeatable read from relational sources</span></span>
<span data-ttu-id="16354-279">Bij het kopiëren van gegevens van relationele gegevens worden opgeslagen, moet u herhaalbaarheid Houd in gedachten om te voorkomen dat ongewenste resultaten.</span><span class="sxs-lookup"><span data-stu-id="16354-279">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="16354-280">In Azure Data Factory, kunt u een segment handmatig opnieuw.</span><span class="sxs-lookup"><span data-stu-id="16354-280">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="16354-281">U kunt ook een beleid voor opnieuw proberen voor een gegevensset configureren zodat een segment wordt opnieuw uitgevoerd wanneer een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="16354-281">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="16354-282">Wanneer een segment opnieuw in beide gevallen wordt uitgevoerd, moet u ervoor zorgen dat dezelfde gegevens is gelezen ongeacht hoe vaak een segment wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="16354-282">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="16354-283">Zie [Repeatable van relationele bronnen lezen](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span><span class="sxs-lookup"><span data-stu-id="16354-283">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources)</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="16354-284">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="16354-284">Performance and Tuning</span></span>
<span data-ttu-id="16354-285">Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) voor meer informatie over de belangrijkste factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren om te optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="16354-285">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
