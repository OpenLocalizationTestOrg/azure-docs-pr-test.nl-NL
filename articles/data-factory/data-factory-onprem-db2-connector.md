---
title: gegevens van de aaaMove van DB2 met behulp van Azure Data Factory | Microsoft Docs
description: Meer informatie over hoe toomove gegevens uit een lokale DB2-database met behulp van Azure Data Factory-Kopieeractiviteit
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
ms.openlocfilehash: 696ac059be644cb3901c37d2fc746e0682c65a1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-db2-by-using-azure-data-factory-copy-activity"></a><span data-ttu-id="b7db5-103">Gegevens verplaatsen van DB2 met behulp van Azure Data Factory-Kopieeractiviteit</span><span class="sxs-lookup"><span data-stu-id="b7db5-103">Move data from DB2 by using Azure Data Factory Copy Activity</span></span>
<span data-ttu-id="b7db5-104">Dit artikel wordt beschreven hoe u de Kopieeractiviteit in Azure Data Factory toocopy gegevens van een gegevensarchief voor lokale DB2-database tooa kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b7db5-104">This article describes how you can use Copy Activity in Azure Data Factory toocopy data from an on-premises DB2 database tooa data store.</span></span> <span data-ttu-id="b7db5-105">U kunt kopiëren tooany gegevensopslag die wordt vermeld als een ondersteunde sink in Hallo [activiteiten voor gegevensverplaatsing Data Factory](data-factory-data-movement-activities.md#supported-data-stores-and-formats) artikel.</span><span class="sxs-lookup"><span data-stu-id="b7db5-105">You can copy data tooany store that is listed as a supported sink in hello [Data Factory data movement activities](data-factory-data-movement-activities.md#supported-data-stores-and-formats) article.</span></span> <span data-ttu-id="b7db5-106">In dit onderwerp is gebaseerd op Hallo Data Factory-artikel, dat geeft een overzicht van de verplaatsing van gegevens met behulp van de Kopieeractiviteit en lijsten Hallo ondersteund data store combinaties.</span><span class="sxs-lookup"><span data-stu-id="b7db5-106">This topic builds on hello Data Factory article, which presents an overview of data movement by using Copy Activity and lists hello supported data store combinations.</span></span> 

<span data-ttu-id="b7db5-107">Data Factory ondersteunt momenteel alleen zwevend gegevens uit een DB2-database tooa [ondersteunde sink gegevensarchief](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span><span class="sxs-lookup"><span data-stu-id="b7db5-107">Data Factory currently supports only moving data from a DB2 database tooa [supported sink data store](data-factory-data-movement-activities.md#supported-data-stores-and-formats).</span></span> <span data-ttu-id="b7db5-108">Verplaatsen van gegevens van andere gegevens worden opgeslagen tooa DB2-database wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="b7db5-108">Moving data from other data stores tooa DB2 database is not supported.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7db5-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b7db5-109">Prerequisites</span></span>
<span data-ttu-id="b7db5-110">Data Factory ondersteunt verbindende tooan lokale DB2-database met behulp van Hallo [data management gateway](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="b7db5-110">Data Factory supports connecting tooan on-premises DB2 database by using hello [data management gateway](data-factory-data-management-gateway.md).</span></span> <span data-ttu-id="b7db5-111">Stapsgewijze instructies tooset Hallo gateway upgegevens toomove met uw gegevens pipeline, kunt u Hallo [verplaatsen van gegevens uit de lokale toocloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="b7db5-111">For step-by-step instructions tooset up hello gateway data pipeline toomove your data, see hello [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="b7db5-112">Een gateway is vereist, zelfs als hello DB2 op Azure IaaS VM gehost wordt.</span><span class="sxs-lookup"><span data-stu-id="b7db5-112">A gateway is required even if hello DB2 is hosted on Azure IaaS VM.</span></span> <span data-ttu-id="b7db5-113">U kunt Hallo gateway installeren op Hallo dezelfde IaaS VM als Hallo-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="b7db5-113">You can install hello gateway on hello same IaaS VM as hello data store.</span></span> <span data-ttu-id="b7db5-114">Als Hallo gateway verbinding toohello database maken kunt, kunt u Hallo gateway installeren op een andere virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="b7db5-114">If hello gateway can connect toohello database, you can install hello gateway on a different VM.</span></span>

<span data-ttu-id="b7db5-115">Hallo data management gateway biedt een ingebouwd DB2-stuurprogramma, zodat u niet moet toomanually installeert een stuurprogramma toocopy gegevens uit een DB2.</span><span class="sxs-lookup"><span data-stu-id="b7db5-115">hello data management gateway provides a built-in DB2 driver, so you don't need toomanually install a driver toocopy data from DB2.</span></span>

> [!NOTE]
> <span data-ttu-id="b7db5-116">Zie voor tips over het oplossen van de verbinding en gateway problemen Hallo [gateway problemen](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) artikel.</span><span class="sxs-lookup"><span data-stu-id="b7db5-116">For tips on troubleshooting connection and gateway issues, see hello [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) article.</span></span>


## <a name="supported-versions"></a><span data-ttu-id="b7db5-117">Ondersteunde versies</span><span class="sxs-lookup"><span data-stu-id="b7db5-117">Supported versions</span></span>
<span data-ttu-id="b7db5-118">Hallo Data Factory DB2-connector ondersteunt Hallo IBM DB2-platformen en versies met gedistribueerd relationele Database architectuur (DRDA) SQL toegang Manager versie 9, 10 en 11 te volgen:</span><span class="sxs-lookup"><span data-stu-id="b7db5-118">hello Data Factory DB2 connector supports hello following IBM DB2 platforms and versions with Distributed Relational Database Architecture (DRDA) SQL Access Manager versions 9, 10, and 11:</span></span>

* <span data-ttu-id="b7db5-119">IBM DB2 voor z-/ OS-versie 11.1</span><span class="sxs-lookup"><span data-stu-id="b7db5-119">IBM DB2 for z/OS version 11.1</span></span>
* <span data-ttu-id="b7db5-120">IBM DB2 voor z-/ OS-versie 10.1</span><span class="sxs-lookup"><span data-stu-id="b7db5-120">IBM DB2 for z/OS version 10.1</span></span>
* <span data-ttu-id="b7db5-121">IBM DB2 voor i (AS400) versie 7.2</span><span class="sxs-lookup"><span data-stu-id="b7db5-121">IBM DB2 for i (AS400) version 7.2</span></span>
* <span data-ttu-id="b7db5-122">IBM DB2 voor i (AS400) versie 7.1</span><span class="sxs-lookup"><span data-stu-id="b7db5-122">IBM DB2 for i (AS400) version 7.1</span></span>
* <span data-ttu-id="b7db5-123">IBM DB2 voor Linux, UNIX- en Windows (LUW) versie 11</span><span class="sxs-lookup"><span data-stu-id="b7db5-123">IBM DB2 for Linux, UNIX, and Windows (LUW) version 11</span></span>
* <span data-ttu-id="b7db5-124">IBM DB2 voor LUW versie 10.5</span><span class="sxs-lookup"><span data-stu-id="b7db5-124">IBM DB2 for LUW version 10.5</span></span>
* <span data-ttu-id="b7db5-125">IBM DB2 voor LUW versie 10.1</span><span class="sxs-lookup"><span data-stu-id="b7db5-125">IBM DB2 for LUW version 10.1</span></span>

> [!TIP]
> <span data-ttu-id="b7db5-126">Als u Hallo 'hello pakket bijbehorende tooan SQL-instructie aanvraag voor het uitvoeren is niet gevonden foutbericht.</span><span class="sxs-lookup"><span data-stu-id="b7db5-126">If you receive hello error message "hello package corresponding tooan SQL statement execution request was not found.</span></span> <span data-ttu-id="b7db5-127">SQLSTATE 805-51002 SQLCODE =, = "hello reden hiervoor is een benodigde pakket is niet gemaakt voor normale gebruiker Hallo op Hallo OS.</span><span class="sxs-lookup"><span data-stu-id="b7db5-127">SQLSTATE=51002 SQLCODE=-805," hello reason is a necessary package is not created for hello normal user on hello OS.</span></span> <span data-ttu-id="b7db5-128">tooresolve dit probleem, volgt u deze instructies voor het type DB2:</span><span class="sxs-lookup"><span data-stu-id="b7db5-128">tooresolve this issue, follow these instructions for your DB2 server type:</span></span>
> - <span data-ttu-id="b7db5-129">DB2 voor i (AS400): laat een hoofdgebruiker Hallo verzameling voor normale gebruiker Hallo voordat u Kopieeractiviteit maken.</span><span class="sxs-lookup"><span data-stu-id="b7db5-129">DB2 for i (AS400): Let a power user create hello collection for hello normal user before running Copy Activity.</span></span> <span data-ttu-id="b7db5-130">toocreate hello verzameling Hallo-opdracht gebruiken:`create collection <username>`</span><span class="sxs-lookup"><span data-stu-id="b7db5-130">toocreate hello collection, use hello command: `create collection <username>`</span></span>
> - <span data-ttu-id="b7db5-131">DB2 voor z-/ OS of LUW: gebruik een account met hoge bevoegdheden--hoofdgebruiker of beheerder met pakket-instanties en BIND, BINDADD, moeten de MACHTIGINGEN EXECUTE tooPUBLIC--toorun Hallo eenmaal kopiëren.</span><span class="sxs-lookup"><span data-stu-id="b7db5-131">DB2 for z/OS or LUW: Use a high privilege account--a power user or admin that has package authorities and BIND, BINDADD, GRANT EXECUTE tooPUBLIC permissions--toorun hello copy once.</span></span> <span data-ttu-id="b7db5-132">Hallo benodigde pakket wordt automatisch gemaakt tijdens het Hallo kopiëren.</span><span class="sxs-lookup"><span data-stu-id="b7db5-132">hello necessary package is automatically created during hello copy.</span></span> <span data-ttu-id="b7db5-133">Daarna kunt u back-toohello normale gebruiker schakelen voor uw volgende kopie wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b7db5-133">Afterward, you can switch back toohello normal user for your subsequent copy runs.</span></span>

## <a name="getting-started"></a><span data-ttu-id="b7db5-134">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="b7db5-134">Getting started</span></span>
<span data-ttu-id="b7db5-135">U kunt een pijplijn maken met een kopie activiteit toomove gegevens uit een on-premises DB2-gegevensopslag met behulp van verschillende hulpprogramma's en API's:</span><span class="sxs-lookup"><span data-stu-id="b7db5-135">You can create a pipeline with a copy activity toomove data from an on-premises DB2 data store by using different tools and APIs:</span></span> 

- <span data-ttu-id="b7db5-136">Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello Azure Data Factory-Wizard voor kopiëren.</span><span class="sxs-lookup"><span data-stu-id="b7db5-136">hello easiest way toocreate a pipeline is toouse hello Azure Data Factory Copy Wizard.</span></span> <span data-ttu-id="b7db5-137">Zie voor een snel overzicht over het maken van een pijplijn met behulp van de Wizard kopiëren Hallo Hallo [zelfstudie: een pijplijn maken met behulp van de Wizard kopiëren Hallo](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="b7db5-137">For a quick walkthrough on creating a pipeline by using hello Copy Wizard, see hello [Tutorial: Create a pipeline by using hello Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span> 
- <span data-ttu-id="b7db5-138">U kunt ook extra toocreate een pijplijn, met inbegrip van hello Azure-portal, Visual Studio, Azure PowerShell, een Azure Resource Manager-sjabloon, Hallo .NET API en Hallo REST-API.</span><span class="sxs-lookup"><span data-stu-id="b7db5-138">You can also use tools toocreate a pipeline, including hello Azure portal, Visual Studio, Azure PowerShell, an Azure Resource Manager template, hello .NET API, and hello REST API.</span></span> <span data-ttu-id="b7db5-139">Zie voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit, Hallo [Kopieeractiviteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="b7db5-139">For step-by-step instructions toocreate a pipeline with a copy activity, see hello [Copy Activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).</span></span> 

<span data-ttu-id="b7db5-140">Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="b7db5-140">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="b7db5-141">Gekoppelde services toolink en uitvoergegevens winkels tooyour een gegevensfactory maken.</span><span class="sxs-lookup"><span data-stu-id="b7db5-141">Create linked services toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="b7db5-142">Maakt u gegevenssets toorepresent invoer en uitvoergegevens voor Hallo kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="b7db5-142">Create datasets toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="b7db5-143">Een pijplijn maken met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="b7db5-143">Create a pipeline with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="b7db5-144">Wanneer u Hallo Wizard kopiëren JSON-definities voor Hallo Data Factory gekoppelde services, worden gegevenssets en pijplijn entiteiten automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b7db5-144">When you use hello Copy Wizard, JSON definitions for hello Data Factory linked services, datasets, and pipeline entities are automatically created for you.</span></span> <span data-ttu-id="b7db5-145">Wanneer u hulpprogramma's of API's (met uitzondering van Hallo .NET API) gebruikt, kunt u Data Factory-entiteiten Hallo definiëren met behulp van Hallo JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="b7db5-145">When you use tools or APIs (except hello .NET API), you define hello Data Factory entities by using hello JSON format.</span></span> <span data-ttu-id="b7db5-146">Hallo [JSON-voorbeeld: gegevens kopiëren van DB2 tooAzure blobopslag](#json-example-copy-data-from-db2-to-azure-blob) toont Hallo JSON definities voor Hallo Data Factory-entiteiten die gebruikt toocopy gegevens uit een on-premises DB2-gegevensopslag zijn.</span><span class="sxs-lookup"><span data-stu-id="b7db5-146">hello [JSON example: Copy data from DB2 tooAzure Blob storage](#json-example-copy-data-from-db2-to-azure-blob) shows hello JSON definitions for hello Data Factory entities that are used toocopy data from an on-premises DB2 data store.</span></span>

<span data-ttu-id="b7db5-147">Hallo volgende secties bevatten informatie over Hallo JSON-eigenschappen die zijn gebruikt toodefine Hallo Data Factory-entiteiten die specifieke tooa DB2-gegevensarchief zijn.</span><span class="sxs-lookup"><span data-stu-id="b7db5-147">hello following sections provide details about hello JSON properties that are used toodefine hello Data Factory entities that are specific tooa DB2 data store.</span></span>

## <a name="db2-linked-service-properties"></a><span data-ttu-id="b7db5-148">DB2 gekoppelde service-eigenschappen</span><span class="sxs-lookup"><span data-stu-id="b7db5-148">DB2 linked service properties</span></span>
<span data-ttu-id="b7db5-149">Hallo volgende tabel geeft een lijst Hallo JSON-eigenschappen die specifiek tooa DB2 gekoppelde service zijn.</span><span class="sxs-lookup"><span data-stu-id="b7db5-149">hello following table lists hello JSON properties that are specific tooa DB2 linked service.</span></span>

| <span data-ttu-id="b7db5-150">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="b7db5-150">Property</span></span> | <span data-ttu-id="b7db5-151">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b7db5-151">Description</span></span> | <span data-ttu-id="b7db5-152">Vereist</span><span class="sxs-lookup"><span data-stu-id="b7db5-152">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b7db5-153">**type**</span><span class="sxs-lookup"><span data-stu-id="b7db5-153">**type**</span></span> |<span data-ttu-id="b7db5-154">Deze eigenschap te moet worden ingesteld**OnPremisesDB2**.</span><span class="sxs-lookup"><span data-stu-id="b7db5-154">This property must be set too**OnPremisesDB2**.</span></span> |<span data-ttu-id="b7db5-155">Ja</span><span class="sxs-lookup"><span data-stu-id="b7db5-155">Yes</span></span> |
| <span data-ttu-id="b7db5-156">**Server**</span><span class="sxs-lookup"><span data-stu-id="b7db5-156">**server**</span></span> |<span data-ttu-id="b7db5-157">Hallo-naam van Hallo DB2-server.</span><span class="sxs-lookup"><span data-stu-id="b7db5-157">hello name of hello DB2 server.</span></span> |<span data-ttu-id="b7db5-158">Ja</span><span class="sxs-lookup"><span data-stu-id="b7db5-158">Yes</span></span> |
| <span data-ttu-id="b7db5-159">**database**</span><span class="sxs-lookup"><span data-stu-id="b7db5-159">**database**</span></span> |<span data-ttu-id="b7db5-160">Hallo-naam van Hallo DB2-database.</span><span class="sxs-lookup"><span data-stu-id="b7db5-160">hello name of hello DB2 database.</span></span> |<span data-ttu-id="b7db5-161">Ja</span><span class="sxs-lookup"><span data-stu-id="b7db5-161">Yes</span></span> |
| <span data-ttu-id="b7db5-162">**schema**</span><span class="sxs-lookup"><span data-stu-id="b7db5-162">**schema**</span></span> |<span data-ttu-id="b7db5-163">Hallo-naam van het Hallo-schema in Hallo DB2-database.</span><span class="sxs-lookup"><span data-stu-id="b7db5-163">hello name of hello schema in hello DB2 database.</span></span> <span data-ttu-id="b7db5-164">Deze eigenschap is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="b7db5-164">This property is case-sensitive.</span></span> |<span data-ttu-id="b7db5-165">Nee</span><span class="sxs-lookup"><span data-stu-id="b7db5-165">No</span></span> |
| <span data-ttu-id="b7db5-166">**authenticationType**</span><span class="sxs-lookup"><span data-stu-id="b7db5-166">**authenticationType**</span></span> |<span data-ttu-id="b7db5-167">Hallo type verificatie dat is gebruikt tooconnect toohello DB2-database.</span><span class="sxs-lookup"><span data-stu-id="b7db5-167">hello type of authentication that is used tooconnect toohello DB2 database.</span></span> <span data-ttu-id="b7db5-168">Hallo mogelijke waarden zijn: anoniem, basis en Windows.</span><span class="sxs-lookup"><span data-stu-id="b7db5-168">hello possible values are: Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="b7db5-169">Ja</span><span class="sxs-lookup"><span data-stu-id="b7db5-169">Yes</span></span> |
| <span data-ttu-id="b7db5-170">**gebruikersnaam**</span><span class="sxs-lookup"><span data-stu-id="b7db5-170">**username**</span></span> |<span data-ttu-id="b7db5-171">Hallo-naam voor de gebruikersaccount Hallo als u basisverificatie of Windows-verificatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b7db5-171">hello name for hello user account if you use Basic or Windows authentication.</span></span> |<span data-ttu-id="b7db5-172">Nee</span><span class="sxs-lookup"><span data-stu-id="b7db5-172">No</span></span> |
| <span data-ttu-id="b7db5-173">**wachtwoord**</span><span class="sxs-lookup"><span data-stu-id="b7db5-173">**password**</span></span> |<span data-ttu-id="b7db5-174">Hallo-wachtwoord voor gebruikersaccount Hallo.</span><span class="sxs-lookup"><span data-stu-id="b7db5-174">hello password for hello user account.</span></span> |<span data-ttu-id="b7db5-175">Nee</span><span class="sxs-lookup"><span data-stu-id="b7db5-175">No</span></span> |
| <span data-ttu-id="b7db5-176">**gatewayName**</span><span class="sxs-lookup"><span data-stu-id="b7db5-176">**gatewayName**</span></span> |<span data-ttu-id="b7db5-177">Hallo-naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello lokale DB2-database gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b7db5-177">hello name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises DB2 database.</span></span> |<span data-ttu-id="b7db5-178">Ja</span><span class="sxs-lookup"><span data-stu-id="b7db5-178">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="b7db5-179">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="b7db5-179">Dataset properties</span></span>
<span data-ttu-id="b7db5-180">Zie voor een lijst met eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets en Hallo secties, Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="b7db5-180">For a list of hello sections and properties that are available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="b7db5-181">Secties, zoals **structuur**, **beschikbaarheid**, en Hallo **beleid** voor een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure Blob storage, Azure Table opslag, enzovoort).</span><span class="sxs-lookup"><span data-stu-id="b7db5-181">Sections, such as **structure**, **availability**, and hello **policy** for a dataset JSON, are similar for all dataset types (Azure SQL, Azure Blob storage, Azure Table storage, and so on).</span></span>

<span data-ttu-id="b7db5-182">Hallo **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="b7db5-182">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="b7db5-183">Hallo **typeProperties** sectie voor een gegevensset van het type **RelationalTable**, waarop Hallo DB2 gegevensset bevat, heeft de volgende eigenschap Hallo:</span><span class="sxs-lookup"><span data-stu-id="b7db5-183">hello **typeProperties** section for a dataset of type **RelationalTable**, which includes hello DB2 dataset, has hello following property:</span></span>

| <span data-ttu-id="b7db5-184">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="b7db5-184">Property</span></span> | <span data-ttu-id="b7db5-185">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b7db5-185">Description</span></span> | <span data-ttu-id="b7db5-186">Vereist</span><span class="sxs-lookup"><span data-stu-id="b7db5-186">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b7db5-187">**tableName**</span><span class="sxs-lookup"><span data-stu-id="b7db5-187">**tableName**</span></span> |<span data-ttu-id="b7db5-188">Hallo-naam van de tabel Hallo in Hallo DB2-database-instantie die Hallo gekoppelde service verwijst.</span><span class="sxs-lookup"><span data-stu-id="b7db5-188">hello name of hello table in hello DB2 database instance that hello linked service refers to.</span></span> <span data-ttu-id="b7db5-189">Deze eigenschap is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="b7db5-189">This property is case-sensitive.</span></span> |<span data-ttu-id="b7db5-190">Nee (als hello **query** eigenschap van de kopieeractiviteit van een van het type **RelationalSource** is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="b7db5-190">No (if hello **query** property of a copy activity of type **RelationalSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="b7db5-191">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="b7db5-191">Copy Activity properties</span></span>
<span data-ttu-id="b7db5-192">Zie voor een lijst met eigenschappen die beschikbaar zijn voor het definiëren van de activiteiten kopiëren en Hallo secties, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="b7db5-192">For a list of hello sections and properties that are available for defining copy activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="b7db5-193">Eigenschappen van de activiteit, zoals kopiëren **naam**, **beschrijving**, **invoer** tabel **levert** tabel en **beleid**, zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="b7db5-193">Copy Activity properties, such as **name**, **description**, **inputs** table, **outputs** table, and **policy**, are available for all types of activities.</span></span> <span data-ttu-id="b7db5-194">eigenschappen die beschikbaar in Hallo zijn Hallo **typeProperties** sectie van de activiteit Hallo voor elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="b7db5-194">hello properties that are available in hello **typeProperties** section of hello activity for each activity type.</span></span> <span data-ttu-id="b7db5-195">Voor de Kopieeractiviteit, wordt Hallo eigenschappen variëren afhankelijk van Hallo soorten gegevensbronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="b7db5-195">For Copy Activity, hello properties vary depending on hello types of data sources and sinks.</span></span>

<span data-ttu-id="b7db5-196">Voor de Kopieeractiviteit wanneer Hallo bron van het type **RelationalSource** (waaronder DB2), Hallo volgende eigenschappen beschikbaar zijn in Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="b7db5-196">For Copy Activity, when hello source is of type **RelationalSource** (which includes DB2), hello following properties are available in hello **typeProperties** section:</span></span>

| <span data-ttu-id="b7db5-197">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="b7db5-197">Property</span></span> | <span data-ttu-id="b7db5-198">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b7db5-198">Description</span></span> | <span data-ttu-id="b7db5-199">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="b7db5-199">Allowed values</span></span> | <span data-ttu-id="b7db5-200">Vereist</span><span class="sxs-lookup"><span data-stu-id="b7db5-200">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b7db5-201">**query**</span><span class="sxs-lookup"><span data-stu-id="b7db5-201">**query**</span></span> |<span data-ttu-id="b7db5-202">Hallo aangepaste query tooread Hallo gegevens gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b7db5-202">Use hello custom query tooread hello data.</span></span> |<span data-ttu-id="b7db5-203">SQL-query-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="b7db5-203">SQL query string.</span></span> <span data-ttu-id="b7db5-204">Bijvoorbeeld: `"query": "select * from "MySchema"."MyTable""`</span><span class="sxs-lookup"><span data-stu-id="b7db5-204">For example: `"query": "select * from "MySchema"."MyTable""`</span></span> |<span data-ttu-id="b7db5-205">Nee (als hello **tableName** eigenschap van een dataset is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="b7db5-205">No (if hello **tableName** property of a dataset is specified)</span></span> |

> [!NOTE]
> <span data-ttu-id="b7db5-206">Schema- en tabelnamen zijn hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="b7db5-206">Schema and table names are case-sensitive.</span></span> <span data-ttu-id="b7db5-207">In de query-instructie hello, moet u de namen van eigenschappen met behulp van "" (dubbele aanhalingstekens).</span><span class="sxs-lookup"><span data-stu-id="b7db5-207">In hello query statement, enclose property names by using "" (double quotes).</span></span> <span data-ttu-id="b7db5-208">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b7db5-208">For example:</span></span>
>
> ```sql
> "query": "select * from "DB2ADMIN"."Customers""
> ```

## <a name="json-example-copy-data-from-db2-tooazure-blob-storage"></a><span data-ttu-id="b7db5-209">JSON-voorbeeld: gegevens kopiëren van DB2 tooAzure Blob-opslag</span><span class="sxs-lookup"><span data-stu-id="b7db5-209">JSON example: Copy data from DB2 tooAzure Blob storage</span></span>
<span data-ttu-id="b7db5-210">In dit voorbeeld bevat definities van de JSON voorbeeld kunt u een pijplijn toocreate door Hallo gebruiken [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="b7db5-210">This example provides sample JSON definitions that you can use toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="b7db5-211">Hallo-voorbeeld ziet u hoe toocopy gegevens uit een DB2-database tooBlob opslag.</span><span class="sxs-lookup"><span data-stu-id="b7db5-211">hello example shows you how toocopy data from a DB2 database tooBlob storage.</span></span> <span data-ttu-id="b7db5-212">Echter gegevens te kunnen worden gekopieerd[alle ondersteunde gegevens opslaan sink-type](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Azure Data Factory-Kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="b7db5-212">However, data can be copied too[any supported data store sink type](data-factory-data-movement-activities.md#supported-data-stores-and-formats) by using Azure Data Factory Copy Activity.</span></span>

<span data-ttu-id="b7db5-213">Hallo voorbeeld heeft Hallo Data Factory-entiteiten te volgen:</span><span class="sxs-lookup"><span data-stu-id="b7db5-213">hello sample has hello following Data Factory entities:</span></span>

- <span data-ttu-id="b7db5-214">Een DB2 gekoppelde service van het type [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="b7db5-214">A DB2 linked service of type [OnPremisesDb2](data-factory-onprem-db2-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="b7db5-215">Een Azure Blob-opslag gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="b7db5-215">An Azure Blob storage linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
- <span data-ttu-id="b7db5-216">Invoer [gegevensset](data-factory-create-datasets.md) van het type [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="b7db5-216">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](data-factory-onprem-db2-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="b7db5-217">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="b7db5-217">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
- <span data-ttu-id="b7db5-218">Een [pijplijn](data-factory-create-pipelines.md) met een kopieeractiviteit die gebruikmaakt van Hallo [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) eigenschappen</span><span class="sxs-lookup"><span data-stu-id="b7db5-218">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses hello [RelationalSource](data-factory-onprem-db2-connector.md#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) properties</span></span>

<span data-ttu-id="b7db5-219">Hallo voorbeeld gegevens worden gekopieerd van de resultaten van een query in een DB2-database tooan Azure blob per uur.</span><span class="sxs-lookup"><span data-stu-id="b7db5-219">hello sample copies data from a query result in a DB2 database tooan Azure blob hourly.</span></span> <span data-ttu-id="b7db5-220">Hallo JSON-eigenschappen die worden gebruikt in de steekproef Hallo worden Hallo die in secties Hallo entiteit definities beschreven.</span><span class="sxs-lookup"><span data-stu-id="b7db5-220">hello JSON properties that are used in hello sample are described in hello sections that follow hello entity definitions.</span></span>

<span data-ttu-id="b7db5-221">Als eerste stap, installeren en configureren van een data gateway.</span><span class="sxs-lookup"><span data-stu-id="b7db5-221">As a first step, install and configure a data gateway.</span></span> <span data-ttu-id="b7db5-222">Instructies vindt u in Hallo [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="b7db5-222">Instructions are in hello [Moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="b7db5-223">**DB2 gekoppelde service**</span><span class="sxs-lookup"><span data-stu-id="b7db5-223">**DB2 linked service**</span></span>

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

<span data-ttu-id="b7db5-224">**Azure Blob-opslag gekoppelde service**</span><span class="sxs-lookup"><span data-stu-id="b7db5-224">**Azure Blob storage linked service**</span></span>

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

<span data-ttu-id="b7db5-225">**Invoergegevensset DB2**</span><span class="sxs-lookup"><span data-stu-id="b7db5-225">**DB2 input dataset**</span></span>

<span data-ttu-id="b7db5-226">Hallo-voorbeeld wordt ervan uitgegaan dat u een tabel in DB2 MijnTabel "" met een kolom met het label 'tijdstempel' hello tijd reeks gegevens hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b7db5-226">hello sample assumes that you have created a table in DB2 named "MyTable" that has a column labeled "timestamp" for hello time series data.</span></span>

<span data-ttu-id="b7db5-227">Hallo **externe** eigenschap is ingesteld te 'true'.</span><span class="sxs-lookup"><span data-stu-id="b7db5-227">hello **external** property is set too"true."</span></span> <span data-ttu-id="b7db5-228">Deze instelling informeert Hallo Data Factory-service dat deze gegevensset externe toohello gegevensfactory en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="b7db5-228">This setting informs hello Data Factory service that this dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span> <span data-ttu-id="b7db5-229">U ziet dat Hallo **type** eigenschap is ingesteld, te**RelationalTable**.</span><span class="sxs-lookup"><span data-stu-id="b7db5-229">Notice that hello **type** property is set too**RelationalTable**.</span></span>


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

<span data-ttu-id="b7db5-230">**Azure Blob-uitvoergegevensset**</span><span class="sxs-lookup"><span data-stu-id="b7db5-230">**Azure Blob output dataset**</span></span>

<span data-ttu-id="b7db5-231">Gegevens worden geschreven tooa nieuwe blob elk uur door Hallo instelling **frequentie** eigenschap te "Uur" en Hallo **interval** eigenschap too1.</span><span class="sxs-lookup"><span data-stu-id="b7db5-231">Data is written tooa new blob every hour by setting hello **frequency** property too"Hour" and hello **interval** property too1.</span></span> <span data-ttu-id="b7db5-232">Hallo **folderPath** eigenschap voor Hallo blob dynamisch wordt geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="b7db5-232">hello **folderPath** property for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="b7db5-233">mappad Hallo Hallo jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b7db5-233">hello folder path uses hello year, month, day, and hour parts of hello start time.</span></span>

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

<span data-ttu-id="b7db5-234">**Pijplijn voor de kopieeractiviteit Hallo**</span><span class="sxs-lookup"><span data-stu-id="b7db5-234">**Pipeline for hello copy activity**</span></span>

<span data-ttu-id="b7db5-235">Hallo pijplijn bevat een kopieeractiviteit die is geconfigureerd toouse opgegeven invoer- en uitvoergegevenssets en geplande toorun elk uur is.</span><span class="sxs-lookup"><span data-stu-id="b7db5-235">hello pipeline contains a copy activity that is configured toouse specified input and output datasets and which is scheduled toorun every hour.</span></span> <span data-ttu-id="b7db5-236">Hallo in JSON-definitie voor de pijplijn Hallo Hallo, **bron** type is ingesteld, te**RelationalSource** en Hallo **sink** type is ingesteld, te**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="b7db5-236">In hello JSON definition for hello pipeline, hello **source** type is set too**RelationalSource** and hello **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="b7db5-237">Hallo SQL-query is opgegeven voor Hallo **query** eigenschap Hallo gegevens uit de tabel 'Orders' hello selecteert.</span><span class="sxs-lookup"><span data-stu-id="b7db5-237">hello SQL query specified for hello **query** property selects hello data from hello "Orders" table.</span></span>

```json
{
    "name": "CopyDb2ToBlob",
    "properties": {
        "description": "pipeline for hello copy activity",
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

## <a name="type-mapping-for-db2"></a><span data-ttu-id="b7db5-238">Toewijzing van het type voor DB2</span><span class="sxs-lookup"><span data-stu-id="b7db5-238">Type mapping for DB2</span></span>
<span data-ttu-id="b7db5-239">Zoals vermeld in Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel Kopieeractiviteit automatische typeconversies van brontype type toosink uitvoert met behulp van Hallo benadering in twee stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b7db5-239">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy Activity performs automatic type conversions from source type toosink type by using hello following two-step approach:</span></span>

1. <span data-ttu-id="b7db5-240">Converteren van een systeemeigen bron type tooa .NET-type</span><span class="sxs-lookup"><span data-stu-id="b7db5-240">Convert from a native source type tooa .NET type</span></span>
2. <span data-ttu-id="b7db5-241">Converteren van een .NET type tooa systeemeigen sink-type</span><span class="sxs-lookup"><span data-stu-id="b7db5-241">Convert from a .NET type tooa native sink type</span></span>

<span data-ttu-id="b7db5-242">Hallo worden volgende toewijzingen gebruikt wanneer de Kopieeractiviteit converteert Hallo gegevens uit een DB2 type tooa .NET-type:</span><span class="sxs-lookup"><span data-stu-id="b7db5-242">hello following mappings are used when Copy Activity converts hello data from a DB2 type tooa .NET type:</span></span>

| <span data-ttu-id="b7db5-243">Type DB2-database</span><span class="sxs-lookup"><span data-stu-id="b7db5-243">DB2 database type</span></span> | <span data-ttu-id="b7db5-244">.NET framework-type</span><span class="sxs-lookup"><span data-stu-id="b7db5-244">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="b7db5-245">SmallInt</span><span class="sxs-lookup"><span data-stu-id="b7db5-245">SmallInt</span></span> |<span data-ttu-id="b7db5-246">Int16</span><span class="sxs-lookup"><span data-stu-id="b7db5-246">Int16</span></span> |
| <span data-ttu-id="b7db5-247">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="b7db5-247">Integer</span></span> |<span data-ttu-id="b7db5-248">Int32</span><span class="sxs-lookup"><span data-stu-id="b7db5-248">Int32</span></span> |
| <span data-ttu-id="b7db5-249">BigInt</span><span class="sxs-lookup"><span data-stu-id="b7db5-249">BigInt</span></span> |<span data-ttu-id="b7db5-250">Int64</span><span class="sxs-lookup"><span data-stu-id="b7db5-250">Int64</span></span> |
| <span data-ttu-id="b7db5-251">Real</span><span class="sxs-lookup"><span data-stu-id="b7db5-251">Real</span></span> |<span data-ttu-id="b7db5-252">Één</span><span class="sxs-lookup"><span data-stu-id="b7db5-252">Single</span></span> |
| <span data-ttu-id="b7db5-253">dubbele</span><span class="sxs-lookup"><span data-stu-id="b7db5-253">Double</span></span> |<span data-ttu-id="b7db5-254">dubbele</span><span class="sxs-lookup"><span data-stu-id="b7db5-254">Double</span></span> |
| <span data-ttu-id="b7db5-255">Float</span><span class="sxs-lookup"><span data-stu-id="b7db5-255">Float</span></span> |<span data-ttu-id="b7db5-256">dubbele</span><span class="sxs-lookup"><span data-stu-id="b7db5-256">Double</span></span> |
| <span data-ttu-id="b7db5-257">Decimale</span><span class="sxs-lookup"><span data-stu-id="b7db5-257">Decimal</span></span> |<span data-ttu-id="b7db5-258">Decimale</span><span class="sxs-lookup"><span data-stu-id="b7db5-258">Decimal</span></span> |
| <span data-ttu-id="b7db5-259">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="b7db5-259">DecimalFloat</span></span> |<span data-ttu-id="b7db5-260">Decimale</span><span class="sxs-lookup"><span data-stu-id="b7db5-260">Decimal</span></span> |
| <span data-ttu-id="b7db5-261">numerieke</span><span class="sxs-lookup"><span data-stu-id="b7db5-261">Numeric</span></span> |<span data-ttu-id="b7db5-262">Decimale</span><span class="sxs-lookup"><span data-stu-id="b7db5-262">Decimal</span></span> |
| <span data-ttu-id="b7db5-263">Date</span><span class="sxs-lookup"><span data-stu-id="b7db5-263">Date</span></span> |<span data-ttu-id="b7db5-264">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="b7db5-264">DateTime</span></span> |
| <span data-ttu-id="b7db5-265">Time</span><span class="sxs-lookup"><span data-stu-id="b7db5-265">Time</span></span> |<span data-ttu-id="b7db5-266">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="b7db5-266">TimeSpan</span></span> |
| <span data-ttu-id="b7db5-267">tijdstempel</span><span class="sxs-lookup"><span data-stu-id="b7db5-267">Timestamp</span></span> |<span data-ttu-id="b7db5-268">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="b7db5-268">DateTime</span></span> |
| <span data-ttu-id="b7db5-269">XML</span><span class="sxs-lookup"><span data-stu-id="b7db5-269">Xml</span></span> |<span data-ttu-id="b7db5-270">Byte]</span><span class="sxs-lookup"><span data-stu-id="b7db5-270">Byte[]</span></span> |
| <span data-ttu-id="b7db5-271">CHAR</span><span class="sxs-lookup"><span data-stu-id="b7db5-271">Char</span></span> |<span data-ttu-id="b7db5-272">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b7db5-272">String</span></span> |
| <span data-ttu-id="b7db5-273">VarChar</span><span class="sxs-lookup"><span data-stu-id="b7db5-273">VarChar</span></span> |<span data-ttu-id="b7db5-274">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b7db5-274">String</span></span> |
| <span data-ttu-id="b7db5-275">LongVarChar</span><span class="sxs-lookup"><span data-stu-id="b7db5-275">LongVarChar</span></span> |<span data-ttu-id="b7db5-276">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b7db5-276">String</span></span> |
| <span data-ttu-id="b7db5-277">DB2DynArray</span><span class="sxs-lookup"><span data-stu-id="b7db5-277">DB2DynArray</span></span> |<span data-ttu-id="b7db5-278">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b7db5-278">String</span></span> |
| <span data-ttu-id="b7db5-279">Binaire</span><span class="sxs-lookup"><span data-stu-id="b7db5-279">Binary</span></span> |<span data-ttu-id="b7db5-280">Byte]</span><span class="sxs-lookup"><span data-stu-id="b7db5-280">Byte[]</span></span> |
| <span data-ttu-id="b7db5-281">VarBinary</span><span class="sxs-lookup"><span data-stu-id="b7db5-281">VarBinary</span></span> |<span data-ttu-id="b7db5-282">Byte]</span><span class="sxs-lookup"><span data-stu-id="b7db5-282">Byte[]</span></span> |
| <span data-ttu-id="b7db5-283">LongVarBinary</span><span class="sxs-lookup"><span data-stu-id="b7db5-283">LongVarBinary</span></span> |<span data-ttu-id="b7db5-284">Byte]</span><span class="sxs-lookup"><span data-stu-id="b7db5-284">Byte[]</span></span> |
| <span data-ttu-id="b7db5-285">Afbeelding</span><span class="sxs-lookup"><span data-stu-id="b7db5-285">Graphic</span></span> |<span data-ttu-id="b7db5-286">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b7db5-286">String</span></span> |
| <span data-ttu-id="b7db5-287">VarGraphic</span><span class="sxs-lookup"><span data-stu-id="b7db5-287">VarGraphic</span></span> |<span data-ttu-id="b7db5-288">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b7db5-288">String</span></span> |
| <span data-ttu-id="b7db5-289">LongVarGraphic</span><span class="sxs-lookup"><span data-stu-id="b7db5-289">LongVarGraphic</span></span> |<span data-ttu-id="b7db5-290">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b7db5-290">String</span></span> |
| <span data-ttu-id="b7db5-291">CLOB</span><span class="sxs-lookup"><span data-stu-id="b7db5-291">Clob</span></span> |<span data-ttu-id="b7db5-292">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b7db5-292">String</span></span> |
| <span data-ttu-id="b7db5-293">Blob</span><span class="sxs-lookup"><span data-stu-id="b7db5-293">Blob</span></span> |<span data-ttu-id="b7db5-294">Byte]</span><span class="sxs-lookup"><span data-stu-id="b7db5-294">Byte[]</span></span> |
| <span data-ttu-id="b7db5-295">DbClob</span><span class="sxs-lookup"><span data-stu-id="b7db5-295">DbClob</span></span> |<span data-ttu-id="b7db5-296">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b7db5-296">String</span></span> |
| <span data-ttu-id="b7db5-297">SmallInt</span><span class="sxs-lookup"><span data-stu-id="b7db5-297">SmallInt</span></span> |<span data-ttu-id="b7db5-298">Int16</span><span class="sxs-lookup"><span data-stu-id="b7db5-298">Int16</span></span> |
| <span data-ttu-id="b7db5-299">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="b7db5-299">Integer</span></span> |<span data-ttu-id="b7db5-300">Int32</span><span class="sxs-lookup"><span data-stu-id="b7db5-300">Int32</span></span> |
| <span data-ttu-id="b7db5-301">BigInt</span><span class="sxs-lookup"><span data-stu-id="b7db5-301">BigInt</span></span> |<span data-ttu-id="b7db5-302">Int64</span><span class="sxs-lookup"><span data-stu-id="b7db5-302">Int64</span></span> |
| <span data-ttu-id="b7db5-303">Real</span><span class="sxs-lookup"><span data-stu-id="b7db5-303">Real</span></span> |<span data-ttu-id="b7db5-304">Één</span><span class="sxs-lookup"><span data-stu-id="b7db5-304">Single</span></span> |
| <span data-ttu-id="b7db5-305">dubbele</span><span class="sxs-lookup"><span data-stu-id="b7db5-305">Double</span></span> |<span data-ttu-id="b7db5-306">dubbele</span><span class="sxs-lookup"><span data-stu-id="b7db5-306">Double</span></span> |
| <span data-ttu-id="b7db5-307">Float</span><span class="sxs-lookup"><span data-stu-id="b7db5-307">Float</span></span> |<span data-ttu-id="b7db5-308">dubbele</span><span class="sxs-lookup"><span data-stu-id="b7db5-308">Double</span></span> |
| <span data-ttu-id="b7db5-309">Decimale</span><span class="sxs-lookup"><span data-stu-id="b7db5-309">Decimal</span></span> |<span data-ttu-id="b7db5-310">Decimale</span><span class="sxs-lookup"><span data-stu-id="b7db5-310">Decimal</span></span> |
| <span data-ttu-id="b7db5-311">DecimalFloat</span><span class="sxs-lookup"><span data-stu-id="b7db5-311">DecimalFloat</span></span> |<span data-ttu-id="b7db5-312">Decimale</span><span class="sxs-lookup"><span data-stu-id="b7db5-312">Decimal</span></span> |
| <span data-ttu-id="b7db5-313">numerieke</span><span class="sxs-lookup"><span data-stu-id="b7db5-313">Numeric</span></span> |<span data-ttu-id="b7db5-314">Decimale</span><span class="sxs-lookup"><span data-stu-id="b7db5-314">Decimal</span></span> |
| <span data-ttu-id="b7db5-315">Date</span><span class="sxs-lookup"><span data-stu-id="b7db5-315">Date</span></span> |<span data-ttu-id="b7db5-316">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="b7db5-316">DateTime</span></span> |
| <span data-ttu-id="b7db5-317">Time</span><span class="sxs-lookup"><span data-stu-id="b7db5-317">Time</span></span> |<span data-ttu-id="b7db5-318">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="b7db5-318">TimeSpan</span></span> |
| <span data-ttu-id="b7db5-319">tijdstempel</span><span class="sxs-lookup"><span data-stu-id="b7db5-319">Timestamp</span></span> |<span data-ttu-id="b7db5-320">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="b7db5-320">DateTime</span></span> |
| <span data-ttu-id="b7db5-321">XML</span><span class="sxs-lookup"><span data-stu-id="b7db5-321">Xml</span></span> |<span data-ttu-id="b7db5-322">Byte]</span><span class="sxs-lookup"><span data-stu-id="b7db5-322">Byte[]</span></span> |
| <span data-ttu-id="b7db5-323">CHAR</span><span class="sxs-lookup"><span data-stu-id="b7db5-323">Char</span></span> |<span data-ttu-id="b7db5-324">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b7db5-324">String</span></span> |

## <a name="map-source-toosink-columns"></a><span data-ttu-id="b7db5-325">Bronkolommen toosink toewijzen</span><span class="sxs-lookup"><span data-stu-id="b7db5-325">Map source toosink columns</span></span>
<span data-ttu-id="b7db5-326">hoe toomap kolommen in Hallo bron gegevensset toocolumns in Hallo sink gegevensset, Zie toolearn [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="b7db5-326">toolearn how toomap columns in hello source dataset toocolumns in hello sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-reads-from-relational-sources"></a><span data-ttu-id="b7db5-327">Herhaalbare leesbewerkingen van relationele bronnen</span><span class="sxs-lookup"><span data-stu-id="b7db5-327">Repeatable reads from relational sources</span></span>
<span data-ttu-id="b7db5-328">Wanneer u gegevens uit een relationele gegevensopslag kopiëren, moet u herhaalbaarheid rekening tooavoid ongewenste resultaten.</span><span class="sxs-lookup"><span data-stu-id="b7db5-328">When you copy data from a relational data store, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="b7db5-329">In Azure Data Factory, kunt u een segment handmatig opnieuw.</span><span class="sxs-lookup"><span data-stu-id="b7db5-329">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="b7db5-330">U kunt ook Hallo opnieuw configureren **beleid** eigenschap voor een gegevensset toorerun een segment wanneer er een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="b7db5-330">You can also configure hello retry **policy** property for a dataset toorerun a slice when a failure occurs.</span></span> <span data-ttu-id="b7db5-331">Zorg ervoor dat Hallo dezelfde gegevens gelezen ongeacht hoe vaak Hallo segment is opnieuw uitvoeren en ongeacht hoe u Hallo segment opnieuw uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b7db5-331">Make sure that hello same data is read no matter how many times hello slice is rerun, and regardless of how you rerun hello slice.</span></span> <span data-ttu-id="b7db5-332">Zie voor meer informatie [Repeatable leest uit relationele bronnen](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="b7db5-332">For more information, see [Repeatable reads from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="b7db5-333">Prestaties en afstemmen</span><span class="sxs-lookup"><span data-stu-id="b7db5-333">Performance and tuning</span></span>
<span data-ttu-id="b7db5-334">Meer informatie over de belangrijkste factoren die invloed hebben op prestaties van de Kopieeractiviteit en manieren toooptimize prestaties in Hallo Hallo [handleiding afstemmen en uitvoering van de activiteit](data-factory-copy-activity-performance.md).</span><span class="sxs-lookup"><span data-stu-id="b7db5-334">Learn about key factors that affect hello performance of Copy Activity and ways toooptimize performance in hello [Copy Activity Performance and Tuning Guide](data-factory-copy-activity-performance.md).</span></span>
