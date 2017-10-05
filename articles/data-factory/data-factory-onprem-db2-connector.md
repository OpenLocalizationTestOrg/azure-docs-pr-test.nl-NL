---
title: Gegevens verplaatsen van DB2 met behulp van Azure Data Factory | Microsoft Docs
description: Meer informatie over het verplaatsen van gegevens uit een lokale DB2-database met behulp van Azure Data Factory-Kopieeractiviteit
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c1644e17-4560-46bb-bf3c-b923126671f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: 6a89cc44724dbb5b46a9e89d6da24d9b35ddbbef
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-from-db2-by-using-azure-data-factory-copy-activity"></a><span data-ttu-id="a03e2-103">Gegevens verplaatsen van DB2 met behulp van Azure Data Factory-Kopieeractiviteit</span><span class="sxs-lookup"><span data-stu-id="a03e2-103">Move data from DB2 by using Azure Data Factory Copy Activity</span></span>
<span data-ttu-id="a03e2-104">Dit artikel wordt beschreven hoe u kunt Kopieeractiviteit in Azure Data Factory om gegevens van een lokale DB2-database kopiëren naar een gegevensopslag.</span><span class="sxs-lookup"><span data-stu-id="a03e2-104">This article describes how you can use Copy Activity in Azure Data Factory to copy data from an on-premises DB2 database to a data store.</span></span> <span data-ttu-id="a03e2-105">U kunt gegevens kopiëren naar een archief dat wordt vermeld als een ondersteunde sink in de [activiteiten voor gegevensverplaatsing Data Factory](data-factory-data-movement-activities.md#supported-data-stores-and-formats) artikel.</span><span class="sxs-lookup"><span data-stu-id="a03e2-105">You can copy data to any store that is listed as a supported sink in the [Data Factory data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> <span data-ttu-id="a03e2-106">In dit onderwerp is gebaseerd op het Data Factory-artikel dat geeft een overzicht van de verplaatsing van gegevens met behulp van de Kopieeractiviteit en geeft een lijst van de store-combinaties van ondersteunde gegevens.</span><span class="sxs-lookup"><span data-stu-id="a03e2-106">This topic builds on the Data Factory article, which presents an overview of data movement by using Copy Activity and lists the supported data store combinations.</span></span> 

<span data-ttu-id="a03e2-107">Data Factory ondersteunt momenteel alleen zwevend gegevens uit een DB2-database naar een [ondersteunde sink gegevensarchief](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="a03e2-107">Data Factory currently supports only moving data from a DB2 database to a [supported sink data store](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="a03e2-108">Verplaatsen van gegevens van andere gegevens worden opgeslagen op een DB2 database wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="a03e2-108">Moving data from other data stores to a DB2 database is not supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a03e2-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="a03e2-109">Prerequisites</span></span>
<span data-ttu-id="a03e2-110">Data Factory ondersteunt verbindingen met een lokale DB2-database met behulp van de [data management gateway](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="a03e2-110">Data Factory supports connecting to an on-premises DB2 database by using the [data management gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="a03e2-111">Zie voor stapsgewijze instructies voor het instellen van de data gateway pijplijn om uw gegevens te verplaatsen, de [gegevens verplaatsen van on-premises naar cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="a03e2-111">For step-by-step instructions to set up the gateway data pipeline to move your data, see the [Move data from on-premises to cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="a03e2-112">Een gateway is vereist, zelfs als de DB2 wordt gehost op Azure IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="a03e2-112">A gateway is required even if the DB2 is hosted on Azure IaaS VM.</span></span> <span data-ttu-id="a03e2-113">U kunt de gateway installeren op de dezelfde IaaS VM als gegevensopslag.</span><span class="sxs-lookup"><span data-stu-id="a03e2-113">You can install the gateway on the same IaaS VM as the data store.</span></span> <span data-ttu-id="a03e2-114">Als de gateway verbinding met de database maken kan, kunt u de gateway installeren op een andere virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="a03e2-114">If the gateway can connect to the database, you can install the gateway on a different VM.</span></span>

<span data-ttu-id="a03e2-115">Data management gateway biedt een ingebouwde DB2-stuurprogramma, dus u een stuurprogramma hoeft voor het kopiëren van gegevens van DB2 handmatig installeren.</span><span class="sxs-lookup"><span data-stu-id="a03e2-115">The data management gateway provides a built-in DB2 driver, so you don't need to manually install a driver to copy data from DB2.</span></span>

> [!NOTE]
> <span data-ttu-id="a03e2-116">Zie voor tips over het oplossen van de verbinding en gateway problemen met de [gateway problemen](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) artikel.</span><span class="sxs-lookup"><span data-stu-id="a03e2-116">For tips on troubleshooting connection and gateway issues, see the [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) article.</span></span>


## <a name="supported-versions"></a><span data-ttu-id="a03e2-117">Ondersteunde versies</span><span class="sxs-lookup"><span data-stu-id="a03e2-117">Supported versions</span></span>
<span data-ttu-id="a03e2-118">De Data Factory DB2-connector ondersteunt de volgende IBM DB2-platforms en versies met gedistribueerd relationele Database architectuur (DRDA) SQL toegang Manager versie 9, 10 en 11:</span><span class="sxs-lookup"><span data-stu-id="a03e2-118">The Data Factory DB2 connector supports the following IBM DB2 platforms and versions with Distributed Relational Database Architecture (DRDA) SQL Access Manager versions 9, 10, and 11:</span></span>

* <span data-ttu-id="a03e2-119">IBM DB2 voor z-/ OS-versie 11.1</span><span class="sxs-lookup"><span data-stu-id="a03e2-119">IBM DB2 for z/OS version 11.1</span></span>
* <span data-ttu-id="a03e2-120">IBM DB2 voor z-/ OS-versie 10.1</span><span class="sxs-lookup"><span data-stu-id="a03e2-120">IBM DB2 for z/OS version 10.1</span></span>
* <span data-ttu-id="a03e2-121">IBM DB2 voor i (AS400) versie 7.2</span><span class="sxs-lookup"><span data-stu-id="a03e2-121">IBM DB2 for i (AS400) version 7.2</span></span>
* <span data-ttu-id="a03e2-122">IBM DB2 voor i (AS400) versie 7.1</span><span class="sxs-lookup"><span data-stu-id="a03e2-122">IBM DB2 for i (AS400) version 7.1</span></span>
* <span data-ttu-id="a03e2-123">IBM DB2 voor Linux, UNIX- en Windows (LUW) versie 11</span><span class="sxs-lookup"><span data-stu-id="a03e2-123">IBM DB2 for Linux, UNIX, and Windows (LUW) version 11</span></span>
* <span data-ttu-id="a03e2-124">IBM DB2 voor LUW versie 10.5</span><span class="sxs-lookup"><span data-stu-id="a03e2-124">IBM DB2 for LUW version 10.5</span></span>
* <span data-ttu-id="a03e2-125">IBM DB2 voor LUW versie 10.1</span><span class="sxs-lookup"><span data-stu-id="a03e2-125">IBM DB2 for LUW version 10.1</span></span>

> [!TIP]
> <span data-ttu-id="a03e2-126">Als u het foutbericht 'het pakket overeenkomt met de aanvraag voor een SQL-instructie uitvoeren is niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="a03e2-126">If you receive the error message "The package corresponding to an SQL statement execution request was not found.</span></span> <span data-ttu-id="a03e2-127">SQLSTATE = 51002 SQLCODE =-805, ' de reden hiervoor is een benodigde pakket is niet gemaakt voor de normale gebruiker van het besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="a03e2-127">SQLSTATE=51002 SQLCODE=-805," the reason is a necessary package is not created for the normal user on the OS.</span></span> <span data-ttu-id="a03e2-128">Volg deze instructies voor het type DB2-dit probleem op te lossen:</span><span class="sxs-lookup"><span data-stu-id="a03e2-128">To resolve this issue, follow these instructions for your DB2 server type:</span></span>
> - <span data-ttu-id="a03e2-129">DB2 voor i (AS400): een hoofdgebruiker maken van de verzameling voor de normale gebruiker voordat de kopieerbewerking wordt uitgevoerd, kunnen.</span><span class="sxs-lookup"><span data-stu-id="a03e2-129">DB2 for i (AS400): Let a power user create the collection for the normal user before running Copy Activity.</span></span> <span data-ttu-id="a03e2-130">Gebruik de opdracht voor het maken van de verzameling:`create collection <username>`</span><span class="sxs-lookup"><span data-stu-id="a03e2-130">To create the collection, use the command: `create collection <username>`</span></span>
> - <span data-ttu-id="a03e2-131">DB2 voor z-/ OS of LUW: gebruik een account met hoge bevoegdheden--hoofdgebruiker of beheerder met pakket-instanties en BIND, BINDADD, EXECUTE verlenen aan openbare machtigingen--de kopie eenmaal wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a03e2-131">DB2 for z/OS or LUW: Use a high privilege account--a power user or admin that has package authorities and BIND, BINDADD, GRANT EXECUTE TO PUBLIC permissions--to run the copy once.</span></span> <span data-ttu-id="a03e2-132">Het benodigde pakket wordt automatisch gemaakt tijdens het kopiëren.</span><span class="sxs-lookup"><span data-stu-id="a03e2-132">The necessary package is automatically created during the copy.</span></span> <span data-ttu-id="a03e2-133">U kunt daarna terug naar de normale gebruiker schakelen voor uw volgende kopie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a03e2-133">Afterward, you can switch back to the normal user for your subsequent copy runs.</span></span>

## <a name="getting-started"></a><span data-ttu-id="a03e2-134">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="a03e2-134">Getting started</span></span>
<span data-ttu-id="a03e2-135">U kunt een pijplijn maken met een kopieeractiviteit om gegevens te verplaatsen van een on-premises DB2-gegevensopslag met behulp van verschillende hulpprogramma's en API's:</span><span class="sxs-lookup"><span data-stu-id="a03e2-135">You can create a pipeline with a copy activity to move data from an on-premises DB2 data store by using different tools and APIs:</span></span> 

- <span data-ttu-id="a03e2-136">Er is de eenvoudigste manier om een pijplijn maken met de Wizard kopiëren van Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="a03e2-136">The easiest way to create a pipeline is to use the Azure Data Factory Copy Wizard.</span></span> <span data-ttu-id="a03e2-137">Zie voor een snel overzicht over het maken van een pijplijn met behulp van de Wizard kopiëren, de [zelfstudie: een pijplijn maken met behulp van de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="a03e2-137">For a quick walkthrough on creating a pipeline by using the Copy Wizard, see the [Tutorial: Create a pipeline by using the Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span> 
- <span data-ttu-id="a03e2-138">U kunt ook hulpprogramma's gebruiken voor het maken van een pijplijn, met inbegrip van de Azure-portal, Visual Studio, Azure PowerShell, een Azure Resource Manager-sjabloon, de .NET API en de REST-API.</span><span class="sxs-lookup"><span data-stu-id="a03e2-138">You can also use tools to create a pipeline, including the Azure portal, Visual Studio, Azure PowerShell, an Azure Resource Manager template, the .NET API, and the REST API.</span></span> <span data-ttu-id="a03e2-139">Zie voor stapsgewijze instructies voor het maken van een pijplijn met een kopieeractiviteit de [Kopieeractiviteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="a03e2-139">For step-by-step instructions to create a pipeline with a copy activity, see the [Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

<span data-ttu-id="a03e2-140">Of u de hulpprogramma's of API's gebruiken, moet u de volgende stappen voor het maken van een pijplijn die de gegevens vanuit een brongegevensarchief naar een gegevensarchief sink verplaatst uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="a03e2-140">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="a03e2-141">Gekoppelde services om te koppelen van de invoer en uitvoer van de opgeslagen gegevens aan uw gegevensfactory maken.</span><span class="sxs-lookup"><span data-stu-id="a03e2-141">Create linked services to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="a03e2-142">Maak gegevenssets vertegenwoordigen de invoer- en -gegevens voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="a03e2-142">Create datasets to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="a03e2-143">Een pijplijn maken met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="a03e2-143">Create a pipeline with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="a03e2-144">Wanneer u de Wizard kopiëren, de JSON-definities voor de Data Factory gekoppelde worden services, gegevenssets en pijplijn entiteiten automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a03e2-144">When you use the Copy Wizard, JSON definitions for the Data Factory linked services, datasets, and pipeline entities are automatically created for you.</span></span> <span data-ttu-id="a03e2-145">Wanneer u hulpprogramma's of API's (met uitzondering van de .NET API) gebruikt, kunt u de Data Factory-entiteiten definiëren met behulp van de JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="a03e2-145">When you use tools or APIs (except the .NET API), you define the Data Factory entities by using the JSON format.</span></span> <span data-ttu-id="a03e2-146">De [JSON-voorbeeld: gegevens kopiëren van DB2 naar Azure Blob storage](#json-example-copy-data-from-db2-to-azure-blob) ziet u de JSON-definities voor de Data Factory-entiteiten die worden gebruikt om gegevens te kopiëren uit een on-premises DB2-gegevensopslag.</span><span class="sxs-lookup"><span data-stu-id="a03e2-146">The [JSON example: Copy data from DB2 to Azure Blob storage](#json-example-copy-data-from-db2-to-azure-blob) shows the JSON definitions for the Data Factory entities that are used to copy data from an on-premises DB2 data store.</span></span>

<span data-ttu-id="a03e2-147">De volgende secties bieden details over de JSON-eigenschappen die worden gebruikt voor het definiëren van de Data Factory-entiteiten die specifiek voor een DB2-gegevensarchief zijn.</span><span class="sxs-lookup"><span data-stu-id="a03e2-147">The following sections provide details about the JSON properties that are used to define the Data Factory entities that are specific to a DB2 data store.</span></span>

## <a name="db2-linked-service-properties"></a><span data-ttu-id="a03e2-148">DB2 gekoppelde service-eigenschappen</span><span class="sxs-lookup"><span data-stu-id="a03e2-148">DB2 linked service properties</span></span>
<span data-ttu-id="a03e2-149">De volgende tabel bevat de JSON-eigenschappen die specifiek voor een service DB2 gekoppeld zijn.</span><span class="sxs-lookup"><span data-stu-id="a03e2-149">The following table lists the JSON properties that are specific to a DB2 linked service.</span></span>

| <span data-ttu-id="a03e2-150">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="a03e2-150">Property</span></span> | <span data-ttu-id="a03e2-151">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a03e2-151">Description</span></span> | <span data-ttu-id="a03e2-152">Vereist</span><span class="sxs-lookup"><span data-stu-id="a03e2-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a03e2-153">**type**</span><span class="sxs-lookup"><span data-stu-id="a03e2-153">**type**</span></span> |<span data-ttu-id="a03e2-154">Deze eigenschap moet worden ingesteld op **OnPremisesDB2**.</span><span class="sxs-lookup"><span data-stu-id="a03e2-154">This property must be set to **OnPremisesDB2**.</span></span> |<span data-ttu-id="a03e2-155">Ja</span><span class="sxs-lookup"><span data-stu-id="a03e2-155">Yes</span></span> |
| <span data-ttu-id="a03e2-156">**Server**</span><span class="sxs-lookup"><span data-stu-id="a03e2-156">**server**</span></span> |<span data-ttu-id="a03e2-157">De naam van de DB2-server.</span><span class="sxs-lookup"><span data-stu-id="a03e2-157">The name of the DB2 server.</span></span> |<span data-ttu-id="a03e2-158">Ja</span><span class="sxs-lookup"><span data-stu-id="a03e2-158">Yes</span></span> |
| <span data-ttu-id="a03e2-159">**database**</span><span class="sxs-lookup"><span data-stu-id="a03e2-159">**database**</span></span> |<span data-ttu-id="a03e2-160">De naam van de DB2-database.</span><span class="sxs-lookup"><span data-stu-id="a03e2-160">The name of the DB2 database.</span></span> |<span data-ttu-id="a03e2-161">Ja</span><span class="sxs-lookup"><span data-stu-id="a03e2-161">Yes</span></span> |
| <span data-ttu-id="a03e2-162">**schema**</span><span class="sxs-lookup"><span data-stu-id="a03e2-162">**schema**</span></span> |<span data-ttu-id="a03e2-163">De naam van het schema in de DB2-database.</span><span class="sxs-lookup"><span data-stu-id="a03e2-163">The name of the schema in the DB2 database.</span></span> <span data-ttu-id="a03e2-164">Deze eigenschap is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="a03e2-164">This property is case-sensitive.</span></span> |<span data-ttu-id="a03e2-165">Nee</span><span class="sxs-lookup"><span data-stu-id="a03e2-165">No</span></span> |
| <span data-ttu-id="a03e2-166">**authenticationType**</span><span class="sxs-lookup"><span data-stu-id="a03e2-166">**authenticationType**</span></span> |<span data-ttu-id="a03e2-167">Het type verificatie dat wordt gebruikt voor het verbinding maken met de DB2-database.</span><span class="sxs-lookup"><span data-stu-id="a03e2-167">The type of authentication that is used to connect to the DB2 database.</span></span> <span data-ttu-id="a03e2-168">De mogelijke waarden zijn: anoniem, basis en Windows.</span><span class="sxs-lookup"><span data-stu-id="a03e2-168">The possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="a03e2-169">Ja</span><span class="sxs-lookup"><span data-stu-id="a03e2-169">Yes</span></span> |
| <span data-ttu-id="a03e2-170">**gebruikersnaam**</span><span class="sxs-lookup"><span data-stu-id="a03e2-170">**username**</span></span> |<span data-ttu-id="a03e2-171">De naam voor het gebruikersaccount als u basisverificatie of Windows-verificatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a03e2-171">The name for the user account if you use Basic or Windows authentication.</span></span> |<span data-ttu-id="a03e2-172">Nee</span><span class="sxs-lookup"><span data-stu-id="a03e2-172">No</span></span> |
| <span data-ttu-id="a03e2-173">**wachtwoord**</span><span class="sxs-lookup"><span data-stu-id="a03e2-173">**password**</span></span> |<span data-ttu-id="a03e2-174">Het wachtwoord voor het gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="a03e2-174">The password for the user account.</span></span> |<span data-ttu-id="a03e2-175">Nee</span><span class="sxs-lookup"><span data-stu-id="a03e2-175">No</span></span> |
| <span data-ttu-id="a03e2-176">**gatewayName**</span><span class="sxs-lookup"><span data-stu-id="a03e2-176">**gatewayName**</span></span> |<span data-ttu-id="a03e2-177">De naam van de gateway die voor de Data Factory-service gebruiken moet voor verbinding met de lokale DB2-database.</span><span class="sxs-lookup"><span data-stu-id="a03e2-177">The name of the gateway that the Data Factory service should use to connect to the on-premises DB2 database.</span></span> |<span data-ttu-id="a03e2-178">Ja</span><span class="sxs-lookup"><span data-stu-id="a03e2-178">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="a03e2-179">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="a03e2-179">Dataset properties</span></span>
<span data-ttu-id="a03e2-180">Zie voor een lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets, de [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="a03e2-180">For a list of the sections and properties that are available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="a03e2-181">Secties, zoals **structuur**, **beschikbaarheid**, en de **beleid** voor een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure Blob storage, Azure Table storage enzovoort).</span><span class="sxs-lookup"><span data-stu-id="a03e2-181">Sections, such as **structure**, **availability**, and the **policy** for a dataset JSON, are similar for all dataset types (Azure SQL, Azure Blob storage, Azure Table storage, and so on).</span></span>

<span data-ttu-id="a03e2-182">De **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over de locatie van de gegevens in het gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="a03e2-182">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="a03e2-183">De **typeProperties** sectie voor een gegevensset van het type **RelationalTable**, waaronder de gegevensset DB2 heeft de volgende eigenschap:</span><span class="sxs-lookup"><span data-stu-id="a03e2-183">The **typeProperties** section for a dataset of type **RelationalTable**, which includes the DB2 dataset, has the following property:</span></span>

| <span data-ttu-id="a03e2-184">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="a03e2-184">Property</span></span> | <span data-ttu-id="a03e2-185">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a03e2-185">Description</span></span> | <span data-ttu-id="a03e2-186">Vereist</span><span class="sxs-lookup"><span data-stu-id="a03e2-186">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a03e2-187">**tableName**</span><span class="sxs-lookup"><span data-stu-id="a03e2-187">**tableName**</span></span> |<span data-ttu-id="a03e2-188">De naam van de tabel in de DB2-database-instantie waarnaar de gekoppelde service verwijst.</span><span class="sxs-lookup"><span data-stu-id="a03e2-188">The name of the table in the DB2 database instance that the linked service refers to.</span></span> <span data-ttu-id="a03e2-189">Deze eigenschap is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="a03e2-189">This property is case-sensitive.</span></span> |<span data-ttu-id="a03e2-190">Nee (als de **query** eigenschap van de kopieeractiviteit van een van het type **RelationalSource** is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="a03e2-190">No (if the **query** property of a copy activity of type **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="a03e2-191">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="a03e2-191">Copy Activity properties</span></span>
<span data-ttu-id="a03e2-192">Zie voor een lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van de activiteiten kopiëren zijn de [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="a03e2-192">For a list of the sections and properties that are available for defining copy activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="a03e2-193">Eigenschappen van de activiteit, zoals kopiëren **naam**, **beschrijving**, **invoer** tabel **levert** tabel en **beleid**, zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="a03e2-193">Copy Activity properties, such as **name**, **description**, **inputs** table, **outputs** table, and **policy**, are available for all types of activities.</span></span> <span data-ttu-id="a03e2-194">De eigenschappen die beschikbaar zijn in de **typeProperties** sectie van de activiteit voor elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="a03e2-194">The properties that are available in the **typeProperties** section of the activity for each activity type.</span></span> <span data-ttu-id="a03e2-195">Voor de Kopieeractiviteit, wordt de eigenschappen variëren afhankelijk van de soorten gegevensbronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="a03e2-195">For Copy Activity, the properties vary depending on the types of data sources and sinks.</span></span>

<span data-ttu-id="a03e2-196">Voor de Kopieeractiviteit, wanneer de bron van het type **RelationalSource** (waaronder DB2), de volgende eigenschappen beschikbaar zijn in de **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="a03e2-196">For Copy Activity, when the source is of type **RelationalSource** (which includes DB2), the following properties are available in the **typeProperties** section:</span></span>

| <span data-ttu-id="a03e2-197">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="a03e2-197">Property</span></span> | <span data-ttu-id="a03e2-198">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a03e2-198">Description</span></span> | <span data-ttu-id="a03e2-199">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="a03e2-199">Allowed values</span></span> | <span data-ttu-id="a03e2-200">Vereist</span><span class="sxs-lookup"><span data-stu-id="a03e2-200">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a03e2-201">**query**</span><span class="sxs-lookup"><span data-stu-id="a03e2-201">**query**</span></span> |<span data-ttu-id="a03e2-202">Gebruik de aangepaste query om de gegevens te lezen.</span><span class="sxs-lookup"><span data-stu-id="a03e2-202">Use the custom query to read the data.</span></span> |<span data-ttu-id="a03e2-203">SQL-query-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="a03e2-203">SQL query string.</span></span> <span data-ttu-id="a03e2-204">Bijvoorbeeld: `"query": "select * from "MySchema"."MyTable""`</span><span class="sxs-lookup"><span data-stu-id="a03e2-204">For example: `"query": "select * from "MySchema"."MyTable""`</span></span> |<span data-ttu-id="a03e2-205">Nee (als de **tableName** eigenschap van een dataset is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="a03e2-205">No (if the **tableName** property of a dataset is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="a03e2-206">Schema- en tabelnamen zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="a03e2-206">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="a03e2-207">In de query-instructie, moet u de namen van eigenschappen met behulp van "" (dubbele aanhalingstekens).</span><span class="sxs-lookup"><span data-stu-id="a03e2-207">In the query statement, enclose property names by using "" (double quotes).</span></span> <span data-ttu-id="a03e2-208">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="a03e2-208">For example:</span></span>
>
> ```sql
> "query": "select * from "DB2ADMIN"."Customers""
> ```

## <a name="json-example-copy-data-from-db2-to-azure-blob-storage"></a><span data-ttu-id="a03e2-209">JSON-voorbeeld: gegevens kopiëren van DB2 naar Azure Blob-opslag</span><span class="sxs-lookup"><span data-stu-id="a03e2-209">JSON example: Copy data from DB2 to Azure Blob storage</span></span>
<span data-ttu-id="a03e2-210">In dit voorbeeld bevat definities van de voorbeeld-JSON die u een pijplijn maken kunt met behulp van de [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a03e2-210">This example provides sample JSON definitions that you can use to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="a03e2-211">In het voorbeeld ziet u hoe gegevens uit een DB2-database kopiëren naar de Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="a03e2-211">The example shows you how to copy data from a DB2 database to Blob storage.</span></span> <span data-ttu-id="a03e2-212">Gegevens kunnen echter worden gekopieerd naar [alle ondersteunde gegevens opslaan sink-type](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Azure Data Factory-Kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="a03e2-212">However, data can be copied to [any supported data store sink type](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Azure Data Factory Copy Activity.</span></span>

<span data-ttu-id="a03e2-213">Het voorbeeld heeft de volgende Data Factory-entiteiten:</span><span class="sxs-lookup"><span data-stu-id="a03e2-213">The sample has the following Data Factory entities:</span></span>

- <span data-ttu-id="a03e2-214">Een DB2 gekoppelde service van het type [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="a03e2-214">A DB2 linked service of type [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="a03e2-215">Een Azure Blob-opslag gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="a03e2-215">An Azure Blob storage linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="a03e2-216">Invoer [gegevensset](data-factory-create-datasets.md) van het type [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="a03e2-216">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="a03e2-217">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="a03e2-217">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="a03e2-218">Een [pijplijn](data-factory-create-pipelines.md) met een kopieeractiviteit die gebruikmaakt van de [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) eigenschappen</span><span class="sxs-lookup"><span data-stu-id="a03e2-218">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses the [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) properties</span></span>

<span data-ttu-id="a03e2-219">Het voorbeeld kopieert gegevens van de resultaten van een query in een DB2-database naar een Azure-blob per uur.</span><span class="sxs-lookup"><span data-stu-id="a03e2-219">The sample copies data from a query result in a DB2 database to an Azure blob hourly.</span></span> <span data-ttu-id="a03e2-220">De JSON-eigenschappen die worden gebruikt in de steekproef die worden beschreven in de secties die, de definities van de entiteit volgen.</span><span class="sxs-lookup"><span data-stu-id="a03e2-220">The JSON properties that are used in the sample are described in the sections that follow the entity definitions.</span></span>

<span data-ttu-id="a03e2-221">Als eerste stap, installeren en configureren van een data gateway.</span><span class="sxs-lookup"><span data-stu-id="a03e2-221">As a first step, install and configure a data gateway.</span></span> <span data-ttu-id="a03e2-222">Instructies vindt u in de [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="a03e2-222">Instructions are in the [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="a03e2-223">**DB2 gekoppelde service**</span><span class="sxs-lookup"><span data-stu-id="a03e2-223">**DB2 linked service**</span></span>

```json
{
    "name": "OnPremDb2LinkedService",
    "properties": {
        "type": "OnPremisesDb2",
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

<span data-ttu-id="a03e2-224">**Azure Blob-opslag gekoppelde service**</span><span class="sxs-lookup"><span data-stu-id="a03e2-224">**Azure Blob storage linked service**</span></span>

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

<span data-ttu-id="a03e2-225">**Invoergegevensset DB2**</span><span class="sxs-lookup"><span data-stu-id="a03e2-225">**DB2 input dataset**</span></span>

<span data-ttu-id="a03e2-226">Het voorbeeld wordt ervan uitgegaan dat u een tabel in DB2 MijnTabel "" met een kolom met het label 'tijdstempel' voor het gegevenstype van de reeks tijd hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a03e2-226">The sample assumes that you have created a table in DB2 named "MyTable" that has a column labeled "timestamp" for the time series data.</span></span>

<span data-ttu-id="a03e2-227">De **externe** eigenschap is ingesteld op 'true'.</span><span class="sxs-lookup"><span data-stu-id="a03e2-227">The **external** property is set to "true."</span></span> <span data-ttu-id="a03e2-228">Deze instelling informeert de Data Factory-service dat deze gegevensset extern is aan de gegevensfactory en niet wordt geproduceerd door een activiteit in de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="a03e2-228">This setting informs the Data Factory service that this dataset is external to the data factory and is not produced by an activity in the data factory.</span></span> <span data-ttu-id="a03e2-229">U ziet dat de **type** eigenschap is ingesteld op **RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="a03e2-229">Notice that the **type** property is set to **RelationalTable**.</span></span>


```json
{
    "name": "Db2DataSet",
    "properties": {
        "type": "RelationalTable",
        "linkedServiceName": "OnPremDb2LinkedService",
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

<span data-ttu-id="a03e2-230">**Azure Blob-uitvoergegevensset**</span><span class="sxs-lookup"><span data-stu-id="a03e2-230">**Azure Blob output dataset**</span></span>

<span data-ttu-id="a03e2-231">Gegevens worden geschreven naar een nieuwe blob elk uur door in te stellen de **frequentie** eigenschap in op "Uur" en de **interval** eigenschap in op 1.</span><span class="sxs-lookup"><span data-stu-id="a03e2-231">Data is written to a new blob every hour by setting the **frequency** property to "Hour" and the **interval** property to 1.</span></span> <span data-ttu-id="a03e2-232">De **folderPath** eigenschap voor de blob dynamisch wordt geëvalueerd op basis van de begintijd van het segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="a03e2-232">The **folderPath** property for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="a03e2-233">Het mappad maakt gebruik van het jaar, maand, dag en uur delen van de begintijd.</span><span class="sxs-lookup"><span data-stu-id="a03e2-233">The folder path uses the year, month, day, and hour parts of the start time.</span></span>

```json
{
    "name": "AzureBlobDb2DataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/db2/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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

<span data-ttu-id="a03e2-234">**Pijplijn voor de kopieeractiviteit**</span><span class="sxs-lookup"><span data-stu-id="a03e2-234">**Pipeline for the copy activity**</span></span>

<span data-ttu-id="a03e2-235">De pijplijn bevat een kopieeractiviteit dat is geconfigureerd voor gebruik van de opgegeven invoer- en uitvoergegevenssets en die is gepland voor elk uur uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a03e2-235">The pipeline contains a copy activity that is configured to use specified input and output datasets and which is scheduled to run every hour.</span></span> <span data-ttu-id="a03e2-236">In de JSON-definitie voor de pijplijn de **bron** type is ingesteld op **RelationalSource** en de **sink** type is ingesteld op **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="a03e2-236">In the JSON definition for the pipeline, the **source** type is set to **RelationalSource** and the **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="a03e2-237">De SQL-query die is opgegeven voor de **query** eigenschap selecteert u de gegevens uit de tabel 'Orders'.</span><span class="sxs-lookup"><span data-stu-id="a03e2-237">The SQL query specified for the **query** property selects the data from the "Orders" table.</span></span>

```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for the copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "select * from \"Orders\""
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                },
                "inputs": [
                    {
                        "name": "Db2DataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobDb2DataSet"
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
                "name": "Db2ToBlob"
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="type-mapping-for-db2"></a><span data-ttu-id="a03e2-238">Toewijzing van het type voor DB2</span><span class="sxs-lookup"><span data-stu-id="a03e2-238">Type mapping for DB2</span></span>
<span data-ttu-id="a03e2-239">Zoals vermeld in de [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel Kopieeractiviteit voert automatische typeconversies van brontype naar het opvangen van type met behulp van de volgende benadering voor in twee stappen:</span><span class="sxs-lookup"><span data-stu-id="a03e2-239">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy Activity performs automatic type conversions from source type to sink type by using the following two-step approach:</span></span>

1. <span data-ttu-id="a03e2-240">Converteren van een systeemeigen brontype naar een .NET-type</span><span class="sxs-lookup"><span data-stu-id="a03e2-240">Convert from a native source type to a .NET type</span></span>
2. <span data-ttu-id="a03e2-241">Converteren van een .NET-type naar een systeemeigen sink-type</span><span class="sxs-lookup"><span data-stu-id="a03e2-241">Convert from a .NET type to a native sink type</span></span>

<span data-ttu-id="a03e2-242">De volgende toewijzingen worden gebruikt wanneer de Kopieeractiviteit converteert de gegevens uit een DB2-type naar een .NET-type:</span><span class="sxs-lookup"><span data-stu-id="a03e2-242">The following mappings are used when Copy Activity converts the data from a DB2 type to a .NET type:</span></span>

| <span data-ttu-id="a03e2-243">Type DB2-database</span><span class="sxs-lookup"><span data-stu-id="a03e2-243">DB2 database type</span></span> | <span data-ttu-id="a03e2-244">.NET framework-type</span><span class="sxs-lookup"><span data-stu-id="a03e2-244">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="a03e2-245">SmallInt</span><span class="sxs-lookup"><span data-stu-id="a03e2-245">SmallInt</span></span> |<span data-ttu-id="a03e2-246">Int16</span><span class="sxs-lookup"><span data-stu-id="a03e2-246">Int16</span></span> |
| <span data-ttu-id="a03e2-247">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="a03e2-247">Integer</span></span> |<span data-ttu-id="a03e2-248">Int32</span><span class="sxs-lookup"><span data-stu-id="a03e2-248">Int32</span></span> |
| <span data-ttu-id="a03e2-249">BigInt</span><span class="sxs-lookup"><span data-stu-id="a03e2-249">BigInt</span></span> |<span data-ttu-id="a03e2-250">Int64</span><span class="sxs-lookup"><span data-stu-id="a03e2-250">Int64</span></span> |
| <span data-ttu-id="a03e2-251">Real</span><span class="sxs-lookup"><span data-stu-id="a03e2-251">Real</span></span> |<span data-ttu-id="a03e2-252">Één</span><span class="sxs-lookup"><span data-stu-id="a03e2-252">Single</span></span> |
| <span data-ttu-id="a03e2-253">dubbele</span><span class="sxs-lookup"><span data-stu-id="a03e2-253">Double</span></span> |<span data-ttu-id="a03e2-254">dubbele</span><span class="sxs-lookup"><span data-stu-id="a03e2-254">Double</span></span> |
| <span data-ttu-id="a03e2-255">Float</span><span class="sxs-lookup"><span data-stu-id="a03e2-255">Float</span></span> |<span data-ttu-id="a03e2-256">dubbele</span><span class="sxs-lookup"><span data-stu-id="a03e2-256">Double</span></span> |
| <span data-ttu-id="a03e2-257">Decimale</span><span class="sxs-lookup"><span data-stu-id="a03e2-257">Decimal</span></span> |<span data-ttu-id="a03e2-258">Decimale</span><span class="sxs-lookup"><span data-stu-id="a03e2-258">Decimal</span></span> |
| <span data-ttu-id="a03e2-259">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="a03e2-259">DecimalFloat</span></span> |<span data-ttu-id="a03e2-260">Decimale</span><span class="sxs-lookup"><span data-stu-id="a03e2-260">Decimal</span></span> |
| <span data-ttu-id="a03e2-261">numerieke</span><span class="sxs-lookup"><span data-stu-id="a03e2-261">Numeric</span></span> |<span data-ttu-id="a03e2-262">Decimale</span><span class="sxs-lookup"><span data-stu-id="a03e2-262">Decimal</span></span> |
| <span data-ttu-id="a03e2-263">Date</span><span class="sxs-lookup"><span data-stu-id="a03e2-263">Date</span></span> |<span data-ttu-id="a03e2-264">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="a03e2-264">DateTime</span></span> |
| <span data-ttu-id="a03e2-265">Time</span><span class="sxs-lookup"><span data-stu-id="a03e2-265">Time</span></span> |<span data-ttu-id="a03e2-266">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="a03e2-266">TimeSpan</span></span> |
| <span data-ttu-id="a03e2-267">tijdstempel</span><span class="sxs-lookup"><span data-stu-id="a03e2-267">Timestamp</span></span> |<span data-ttu-id="a03e2-268">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="a03e2-268">DateTime</span></span> |
| <span data-ttu-id="a03e2-269">XML</span><span class="sxs-lookup"><span data-stu-id="a03e2-269">Xml</span></span> |<span data-ttu-id="a03e2-270">Byte]</span><span class="sxs-lookup"><span data-stu-id="a03e2-270">Byte[]</span></span> |
| <span data-ttu-id="a03e2-271">CHAR</span><span class="sxs-lookup"><span data-stu-id="a03e2-271">Char</span></span> |<span data-ttu-id="a03e2-272">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="a03e2-272">String</span></span> |
| <span data-ttu-id="a03e2-273">VarChar</span><span class="sxs-lookup"><span data-stu-id="a03e2-273">VarChar</span></span> |<span data-ttu-id="a03e2-274">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="a03e2-274">String</span></span> |
| <span data-ttu-id="a03e2-275">LongVarChar</span><span class="sxs-lookup"><span data-stu-id="a03e2-275">LongVarChar</span></span> |<span data-ttu-id="a03e2-276">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="a03e2-276">String</span></span> |
| <span data-ttu-id="a03e2-277">DB2DynArray</span><span class="sxs-lookup"><span data-stu-id="a03e2-277">DB2DynArray</span></span> |<span data-ttu-id="a03e2-278">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="a03e2-278">String</span></span> |
| <span data-ttu-id="a03e2-279">Binaire</span><span class="sxs-lookup"><span data-stu-id="a03e2-279">Binary</span></span> |<span data-ttu-id="a03e2-280">Byte]</span><span class="sxs-lookup"><span data-stu-id="a03e2-280">Byte[]</span></span> |
| <span data-ttu-id="a03e2-281">VarBinary</span><span class="sxs-lookup"><span data-stu-id="a03e2-281">VarBinary</span></span> |<span data-ttu-id="a03e2-282">Byte]</span><span class="sxs-lookup"><span data-stu-id="a03e2-282">Byte[]</span></span> |
| <span data-ttu-id="a03e2-283">LongVarBinary</span><span class="sxs-lookup"><span data-stu-id="a03e2-283">LongVarBinary</span></span> |<span data-ttu-id="a03e2-284">Byte]</span><span class="sxs-lookup"><span data-stu-id="a03e2-284">Byte[]</span></span> |
| <span data-ttu-id="a03e2-285">Afbeelding</span><span class="sxs-lookup"><span data-stu-id="a03e2-285">Graphic</span></span> |<span data-ttu-id="a03e2-286">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="a03e2-286">String</span></span> |
| <span data-ttu-id="a03e2-287">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="a03e2-287">VarGraphic</span></span> |<span data-ttu-id="a03e2-288">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="a03e2-288">String</span></span> |
| <span data-ttu-id="a03e2-289">LongVarGraphic</span><span class="sxs-lookup"><span data-stu-id="a03e2-289">LongVarGraphic</span></span> |<span data-ttu-id="a03e2-290">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="a03e2-290">String</span></span> |
| <span data-ttu-id="a03e2-291">CLOB</span><span class="sxs-lookup"><span data-stu-id="a03e2-291">Clob</span></span> |<span data-ttu-id="a03e2-292">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="a03e2-292">String</span></span> |
| <span data-ttu-id="a03e2-293">Blob</span><span class="sxs-lookup"><span data-stu-id="a03e2-293">Blob</span></span> |<span data-ttu-id="a03e2-294">Byte]</span><span class="sxs-lookup"><span data-stu-id="a03e2-294">Byte[]</span></span> |
| <span data-ttu-id="a03e2-295">DbClob</span><span class="sxs-lookup"><span data-stu-id="a03e2-295">DbClob</span></span> |<span data-ttu-id="a03e2-296">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="a03e2-296">String</span></span> |
| <span data-ttu-id="a03e2-297">SmallInt</span><span class="sxs-lookup"><span data-stu-id="a03e2-297">SmallInt</span></span> |<span data-ttu-id="a03e2-298">Int16</span><span class="sxs-lookup"><span data-stu-id="a03e2-298">Int16</span></span> |
| <span data-ttu-id="a03e2-299">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="a03e2-299">Integer</span></span> |<span data-ttu-id="a03e2-300">Int32</span><span class="sxs-lookup"><span data-stu-id="a03e2-300">Int32</span></span> |
| <span data-ttu-id="a03e2-301">BigInt</span><span class="sxs-lookup"><span data-stu-id="a03e2-301">BigInt</span></span> |<span data-ttu-id="a03e2-302">Int64</span><span class="sxs-lookup"><span data-stu-id="a03e2-302">Int64</span></span> |
| <span data-ttu-id="a03e2-303">Real</span><span class="sxs-lookup"><span data-stu-id="a03e2-303">Real</span></span> |<span data-ttu-id="a03e2-304">Één</span><span class="sxs-lookup"><span data-stu-id="a03e2-304">Single</span></span> |
| <span data-ttu-id="a03e2-305">dubbele</span><span class="sxs-lookup"><span data-stu-id="a03e2-305">Double</span></span> |<span data-ttu-id="a03e2-306">dubbele</span><span class="sxs-lookup"><span data-stu-id="a03e2-306">Double</span></span> |
| <span data-ttu-id="a03e2-307">Float</span><span class="sxs-lookup"><span data-stu-id="a03e2-307">Float</span></span> |<span data-ttu-id="a03e2-308">dubbele</span><span class="sxs-lookup"><span data-stu-id="a03e2-308">Double</span></span> |
| <span data-ttu-id="a03e2-309">Decimale</span><span class="sxs-lookup"><span data-stu-id="a03e2-309">Decimal</span></span> |<span data-ttu-id="a03e2-310">Decimale</span><span class="sxs-lookup"><span data-stu-id="a03e2-310">Decimal</span></span> |
| <span data-ttu-id="a03e2-311">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="a03e2-311">DecimalFloat</span></span> |<span data-ttu-id="a03e2-312">Decimale</span><span class="sxs-lookup"><span data-stu-id="a03e2-312">Decimal</span></span> |
| <span data-ttu-id="a03e2-313">numerieke</span><span class="sxs-lookup"><span data-stu-id="a03e2-313">Numeric</span></span> |<span data-ttu-id="a03e2-314">Decimale</span><span class="sxs-lookup"><span data-stu-id="a03e2-314">Decimal</span></span> |
| <span data-ttu-id="a03e2-315">Date</span><span class="sxs-lookup"><span data-stu-id="a03e2-315">Date</span></span> |<span data-ttu-id="a03e2-316">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="a03e2-316">DateTime</span></span> |
| <span data-ttu-id="a03e2-317">Time</span><span class="sxs-lookup"><span data-stu-id="a03e2-317">Time</span></span> |<span data-ttu-id="a03e2-318">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="a03e2-318">TimeSpan</span></span> |
| <span data-ttu-id="a03e2-319">tijdstempel</span><span class="sxs-lookup"><span data-stu-id="a03e2-319">Timestamp</span></span> |<span data-ttu-id="a03e2-320">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="a03e2-320">DateTime</span></span> |
| <span data-ttu-id="a03e2-321">XML</span><span class="sxs-lookup"><span data-stu-id="a03e2-321">Xml</span></span> |<span data-ttu-id="a03e2-322">Byte]</span><span class="sxs-lookup"><span data-stu-id="a03e2-322">Byte[]</span></span> |
| <span data-ttu-id="a03e2-323">CHAR</span><span class="sxs-lookup"><span data-stu-id="a03e2-323">Char</span></span> |<span data-ttu-id="a03e2-324">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="a03e2-324">String</span></span> |

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="a03e2-325">Bron van de kaart opvangen kolommen</span><span class="sxs-lookup"><span data-stu-id="a03e2-325">Map source to sink columns</span></span>
<span data-ttu-id="a03e2-326">Zie voor informatie over het toewijzen van kolommen in de bron-gegevensset aan kolommen in de gegevensset sink, [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="a03e2-326">To learn how to map columns in the source dataset to columns in the sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-reads-from-relational-sources"></a><span data-ttu-id="a03e2-327">Herhaalbare leesbewerkingen van relationele bronnen</span><span class="sxs-lookup"><span data-stu-id="a03e2-327">Repeatable reads from relational sources</span></span>
<span data-ttu-id="a03e2-328">Wanneer u gegevens uit een relationele gegevensopslag kopiëren, moet rekening houden om te voorkomen dat ongewenste resultaten herhaalbaarheid.</span><span class="sxs-lookup"><span data-stu-id="a03e2-328">When you copy data from a relational data store, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="a03e2-329">In Azure Data Factory, kunt u een segment handmatig opnieuw.</span><span class="sxs-lookup"><span data-stu-id="a03e2-329">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="a03e2-330">U kunt ook configureren met de nieuwe poging **beleid** eigenschap voor een gegevensset naar een segment opnieuw uitvoeren wanneer een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="a03e2-330">You can also configure the retry **policy** property for a dataset to rerun a slice when a failure occurs.</span></span> <span data-ttu-id="a03e2-331">Zorg ervoor dat dezelfde gegevens is gelezen, ongeacht hoe vaak het segment opnieuw wordt uitgevoerd en ongeacht hoe u het segment opnieuw uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a03e2-331">Make sure that the same data is read no matter how many times the slice is rerun, and regardless of how you rerun the slice.</span></span> <span data-ttu-id="a03e2-332">Zie voor meer informatie [Repeatable leest uit relationele bronnen](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="a03e2-332">For more information, see [Repeatable reads from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="a03e2-333">Prestaties en afstemmen</span><span class="sxs-lookup"><span data-stu-id="a03e2-333">Performance and tuning</span></span>
<span data-ttu-id="a03e2-334">Meer informatie over de belangrijkste factoren die invloed hebben op de prestaties van de Kopieeractiviteit en manieren om te optimaliseren in de [handleiding afstemmen en uitvoering van de activiteit](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="a03e2-334">Learn about key factors that affect the performance of Copy Activity and ways to optimize performance in the [Copy Activity Performance and Tuning Guide](data-factory-copy-activity-performance.md).</span></span>