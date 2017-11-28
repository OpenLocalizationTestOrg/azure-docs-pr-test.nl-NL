---
title: aaaCopy gegevens van/naar Oracle gebruik Data Factory | Microsoft Docs
description: Meer informatie over hoe toocopy gegevens van Oracle-database die on-premises met Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3c20aa95-a8a1-4aae-9180-a6a16d64a109
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: adb6d5fbe38e18791616ac77e8179970bbea37fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tofrom-on-premises-oracle-using-azure-data-factory"></a><span data-ttu-id="76b5a-103">Gegevens kopiëren van lokale Oracle met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="76b5a-103">Copy data to/from on-premises Oracle using Azure Data Factory</span></span>
<span data-ttu-id="76b5a-104">Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit Hallo in Azure Data Factory toomove gegevens uit een lokale Oracle-database.</span><span class="sxs-lookup"><span data-stu-id="76b5a-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from an on-premises Oracle database.</span></span> <span data-ttu-id="76b5a-105">Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.</span><span class="sxs-lookup"><span data-stu-id="76b5a-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="76b5a-106">Ondersteunde scenario 's</span><span class="sxs-lookup"><span data-stu-id="76b5a-106">Supported scenarios</span></span>
<span data-ttu-id="76b5a-107">U kunt gegevens kopiëren **uit een Oracle-database** toohello gegevensarchieven te volgen:</span><span class="sxs-lookup"><span data-stu-id="76b5a-107">You can copy data **from an Oracle database** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="76b5a-108">Gegevens kunnen worden gekopieerd van de volgende gegevensarchieven Hallo **tooan Oracle-database**:</span><span class="sxs-lookup"><span data-stu-id="76b5a-108">You can copy data from hello following data stores **tooan Oracle database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="prerequisites"></a><span data-ttu-id="76b5a-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="76b5a-109">Prerequisites</span></span>
<span data-ttu-id="76b5a-110">Data Factory ondersteunt verbindende tooon-premises Oracle-gegevensbronnen waarvoor gebruik wordt Hallo Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="76b5a-110">Data Factory supports connecting tooon-premises Oracle sources using hello Data Management Gateway.</span></span> <span data-ttu-id="76b5a-111">Zie [Data Management Gateway](data-factory-data-management-gateway.md) toolearn artikel over Data Management Gateway en [verplaatsen van gegevens uit de lokale toocloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor stapsgewijze instructies over het instellen van Hallo gateway een pijplijn gegevens toomove gegevens.</span><span class="sxs-lookup"><span data-stu-id="76b5a-111">See [Data Management Gateway](data-factory-data-management-gateway.md) article toolearn about Data Management Gateway and [Move data from on-premises toocloud](data-factory-move-data-between-onprem-and-cloud.md) article for step-by-step instructions on setting up hello gateway a data pipeline toomove data.</span></span>

<span data-ttu-id="76b5a-112">Gateway is vereist, zelfs als hello Oracle wordt gehost door een virtuele machine van Azure IaaS.</span><span class="sxs-lookup"><span data-stu-id="76b5a-112">Gateway is required even if hello Oracle is hosted in an Azure IaaS VM.</span></span> <span data-ttu-id="76b5a-113">U kunt Hallo gateway installeren op Hallo dezelfde IaaS VM als Hallo gegevens opslaan of op een andere virtuele machine zo lang Hallo gateway kunt verbinding maken met toohello-database.</span><span class="sxs-lookup"><span data-stu-id="76b5a-113">You can install hello gateway on hello same IaaS VM as hello data store or on a different VM as long as hello gateway can connect toohello database.</span></span>

> [!NOTE]
> <span data-ttu-id="76b5a-114">Zie [gateway problemen](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) voor tips over het oplossen van verbinding of gateway gerelateerde problemen.</span><span class="sxs-lookup"><span data-stu-id="76b5a-114">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="supported-versions-and-installation"></a><span data-ttu-id="76b5a-115">Ondersteunde versies en installatie</span><span class="sxs-lookup"><span data-stu-id="76b5a-115">Supported versions and installation</span></span>
<span data-ttu-id="76b5a-116">Twee versies van stuurprogramma's bieden ondersteuning voor deze connector Oracle:</span><span class="sxs-lookup"><span data-stu-id="76b5a-116">This Oracle connector support two versions of drivers:</span></span>

- <span data-ttu-id="76b5a-117">**Microsoft-stuurprogramma voor Oracle (aanbevolen)**: vanaf Data Management Gateway versie 2.7, een Microsoft-stuurprogramma voor Oracle wordt automatisch geïnstalleerd samen met de gateway hello, dus u hoeft niet tooadditionally ingang Hallo stuurprogramma tooestablish connectiviteit tooOracle, en u kunt ook de prestaties beter kopie dit stuurprogramma gebruikt.</span><span class="sxs-lookup"><span data-stu-id="76b5a-117">**Microsoft driver for Oracle (recommended)**: starting from Data Management Gateway version 2.7, a Microsoft driver for Oracle is automatically installed along with hello gateway, so you don't need tooadditionally handle hello driver in order tooestablish connectivity tooOracle, and you can also experience better copy performance using this driver.</span></span> <span data-ttu-id="76b5a-118">Hieronder versies van Oracle worden databases ondersteund:</span><span class="sxs-lookup"><span data-stu-id="76b5a-118">Below versions of Oracle databases are supported:</span></span>
    - <span data-ttu-id="76b5a-119">Oracle 12c R1 (12.1)</span><span class="sxs-lookup"><span data-stu-id="76b5a-119">Oracle 12c R1 (12.1)</span></span>
    - <span data-ttu-id="76b5a-120">Oracle 11g R1, R2 (11.1, 11.2)</span><span class="sxs-lookup"><span data-stu-id="76b5a-120">Oracle 11g R1, R2 (11.1, 11.2)</span></span>
    - <span data-ttu-id="76b5a-121">Oracle 10g R1, R2 (10.1, 10.2)</span><span class="sxs-lookup"><span data-stu-id="76b5a-121">Oracle 10g R1, R2 (10.1, 10.2)</span></span>
    - <span data-ttu-id="76b5a-122">Oracle 9i R1, R2 (9.0.1, 9.2)</span><span class="sxs-lookup"><span data-stu-id="76b5a-122">Oracle 9i R1, R2 (9.0.1, 9.2)</span></span>
    - <span data-ttu-id="76b5a-123">Oracle 8i R3 (8.1.7)</span><span class="sxs-lookup"><span data-stu-id="76b5a-123">Oracle 8i R3 (8.1.7)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="76b5a-124">Microsoft-stuurprogramma voor Oracle ondersteunt momenteel alleen kopiëren van gegevens uit Oracle, maar niet schrijven tooOracle.</span><span class="sxs-lookup"><span data-stu-id="76b5a-124">Currently Microsoft driver for Oracle only supports copying data from Oracle but not writing tooOracle.</span></span> <span data-ttu-id="76b5a-125">En dit stuurprogramma biedt geen ondersteuning voor opmerking Hallo test verbinding mogelijkheid in het tabblad Data Management Gateway diagnostische gegevens.</span><span class="sxs-lookup"><span data-stu-id="76b5a-125">And note hello test connection capability in Data Management Gateway Diagnostics tab does not support this driver.</span></span> <span data-ttu-id="76b5a-126">U kunt ook Hallo kopie wizard toovalidate Hallo connectiviteit gebruiken.</span><span class="sxs-lookup"><span data-stu-id="76b5a-126">Alternatively, you can use hello copy wizard toovalidate hello connectivity.</span></span>
>

- <span data-ttu-id="76b5a-127">**Oracle-gegevensprovider voor .NET:** u kunt ook toouse Oracle-gegevensprovider toocopy gegevens uit / tooOracle.</span><span class="sxs-lookup"><span data-stu-id="76b5a-127">**Oracle Data Provider for .NET:** you can also choose toouse Oracle Data Provider toocopy data from/tooOracle.</span></span> <span data-ttu-id="76b5a-128">Dit onderdeel is opgenomen in [Oracle Data Access-onderdelen voor Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span><span class="sxs-lookup"><span data-stu-id="76b5a-128">This component is included in [Oracle Data Access Components for Windows](http://www.oracle.com/technetwork/topics/dotnet/downloads/).</span></span> <span data-ttu-id="76b5a-129">Hallo juiste versie (32/64 bits) installeren op Hallo-machine waarop Hallo gateway is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="76b5a-129">Install hello appropriate version (32/64 bit) on hello machine where hello gateway is installed.</span></span> <span data-ttu-id="76b5a-130">[Oracle-gegevensprovider .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) toegang tot tooOracle Database 10 g versie 2 of hoger.</span><span class="sxs-lookup"><span data-stu-id="76b5a-130">[Oracle Data Provider .NET 12.1](http://docs.oracle.com/database/121/ODPNT/InstallSystemRequirements.htm#ODPNT149) can access tooOracle Database 10g Release 2 or later.</span></span>

    <span data-ttu-id="76b5a-131">Als u 'XCopy installatie' kiest, stappen in Hallo Leesmij.htm.</span><span class="sxs-lookup"><span data-stu-id="76b5a-131">If you choose “XCopy Installation”, follow steps in hello readme.htm.</span></span> <span data-ttu-id="76b5a-132">U wordt aangeraden u Hallo installatieprogramma met een gebruikersinterface (niet-XCopy een).</span><span class="sxs-lookup"><span data-stu-id="76b5a-132">We recommend you choose hello installer with UI (non-XCopy one).</span></span>

    <span data-ttu-id="76b5a-133">Na de installatie van de provider hello, **opnieuw** Hallo Data Management Gateway hostservice op uw machine met behulp van de Services-applet (of) Data Management Gateway Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="76b5a-133">After installing hello provider, **restart** hello Data Management Gateway host service on your machine using Services applet (or) Data Management Gateway Configuration Manager.</span></span>  

<span data-ttu-id="76b5a-134">Als u de wizard tooauthor Hallo kopiëren kopieerpijplijn gebruikt, worden Hallo stuurprogrammatype automatisch bepaald.</span><span class="sxs-lookup"><span data-stu-id="76b5a-134">If you use copy wizard tooauthor hello copy pipeline, hello driver type will be auto-determined.</span></span> <span data-ttu-id="76b5a-135">Microsoft-stuurprogramma wordt standaard gebruikt tenzij uw versie van de gegevensgateway lager dan 2.7 is of kies van Oracle als sink.</span><span class="sxs-lookup"><span data-stu-id="76b5a-135">Microsoft driver will be used by default, unless your gateway version is lower than 2.7 or you choose Oracle as sink.</span></span>

## <a name="getting-started"></a><span data-ttu-id="76b5a-136">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="76b5a-136">Getting started</span></span>
<span data-ttu-id="76b5a-137">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens uit een lokale Oracle-database verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="76b5a-137">You can create a pipeline with a copy activity that moves data to/from an on-premises Oracle database by using different tools/APIs.</span></span>

<span data-ttu-id="76b5a-138">Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="76b5a-138">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="76b5a-139">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="76b5a-139">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="76b5a-140">U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="76b5a-140">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="76b5a-141">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="76b5a-141">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="76b5a-142">Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="76b5a-142">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="76b5a-143">Maak een **gegevensfactory**.</span><span class="sxs-lookup"><span data-stu-id="76b5a-143">Create a **data factory**.</span></span> <span data-ttu-id="76b5a-144">Een gegevensfactory kan één of meer pijplijnen bevatten.</span><span class="sxs-lookup"><span data-stu-id="76b5a-144">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="76b5a-145">Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="76b5a-145">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="76b5a-146">Bijvoorbeeld, als u gegevens uit een Oralce database tooan Azure blob-opslag kopiëren wilt, u twee gekoppelde services toolink uw Oracle-database en de Azure storage-account tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="76b5a-146">For example, if you are copying data from an Oralce database tooan Azure blob storage, you create two linked services toolink your Oracle database and Azure storage account tooyour data factory.</span></span> <span data-ttu-id="76b5a-147">Zie voor de gekoppelde service-eigenschappen die specifiek tooOracle, [gekoppelde service-eigenschappen](#linked-service-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="76b5a-147">For linked service properties that are specific tooOracle, see [linked service properties](#linked-service-properties) section.</span></span>
3. <span data-ttu-id="76b5a-148">Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="76b5a-148">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="76b5a-149">In vermeld in de laatste stap Hallo Hallo voorbeeld maakt u een gegevensset toospecify Hallo tabel in de Oracle-database waarin de invoergegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="76b5a-149">In hello example mentioned in hello last step, you create a dataset toospecify hello table in your Oracle database that contains hello input data.</span></span> <span data-ttu-id="76b5a-150">Maken van een andere dataset toospecify Hallo blob-container en Hallo map Hallo gegevens gekopieerd van Hallo Oracle-database.</span><span class="sxs-lookup"><span data-stu-id="76b5a-150">And, you create another dataset toospecify hello blob container and hello folder that holds hello data copied from hello Oracle database.</span></span> <span data-ttu-id="76b5a-151">Zie voor eigenschappen van gegevensset die specifieke tooOracle, [eigenschappen van gegevensset](#dataset-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="76b5a-151">For dataset properties that are specific tooOracle, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="76b5a-152">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="76b5a-152">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="76b5a-153">In Hallo voorbeeld eerder vermeld, gebruikt u OracleSource als een bron- en BlobSink als een sink voor de kopieeractiviteit Hallo.</span><span class="sxs-lookup"><span data-stu-id="76b5a-153">In hello example mentioned earlier, you use OracleSource as a source and BlobSink as a sink for hello copy activity.</span></span> <span data-ttu-id="76b5a-154">Op dezelfde manier als u uit Azure Blob Storage tooOracle Database kopiëren wilt, gebruikt u BlobSource en OracleSink in Hallo kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="76b5a-154">Similarly, if you are copying from Azure Blob Storage tooOracle Database, you use BlobSource and OracleSink in hello copy activity.</span></span> <span data-ttu-id="76b5a-155">Zie voor activiteitseigenschappen kopiëren die specifieke tooOracle database, [activiteitseigenschappen kopiëren](#copy-activity-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="76b5a-155">For copy activity properties that are specific tooOracle database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="76b5a-156">Voor informatie over hoe toouse een gegevensarchief als een bron of een sink, klikt u op Hallo-koppeling in de vorige sectie Hallo voor de gegevensopslag.</span><span class="sxs-lookup"><span data-stu-id="76b5a-156">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span> 

<span data-ttu-id="76b5a-157">Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="76b5a-157">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="76b5a-158">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="76b5a-158">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="76b5a-159">Zie voor voorbeelden met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens van/naar een lokale Oracle-database zijn, [JSON voorbeelden](#json-examples-for-copying-data-to-and-from-oracle-database) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="76b5a-159">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an on-premises Oracle database, see [JSON examples](#json-examples-for-copying-data-to-and-from-oracle-database) section of this article.</span></span>

<span data-ttu-id="76b5a-160">Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten zijn:</span><span class="sxs-lookup"><span data-stu-id="76b5a-160">hello following sections provide details about JSON properties that are used toodefine Data Factory entities:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="76b5a-161">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="76b5a-161">Linked service properties</span></span>
<span data-ttu-id="76b5a-162">Hallo volgende tabel biedt een beschrijving voor de JSON-elementen specifieke tooOracle gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="76b5a-162">hello following table provides description for JSON elements specific tooOracle linked service.</span></span>

| <span data-ttu-id="76b5a-163">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="76b5a-163">Property</span></span> | <span data-ttu-id="76b5a-164">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="76b5a-164">Description</span></span> | <span data-ttu-id="76b5a-165">Vereist</span><span class="sxs-lookup"><span data-stu-id="76b5a-165">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="76b5a-166">type</span><span class="sxs-lookup"><span data-stu-id="76b5a-166">type</span></span> |<span data-ttu-id="76b5a-167">Hallo type eigenschap moet worden ingesteld op: **OnPremisesOracle**</span><span class="sxs-lookup"><span data-stu-id="76b5a-167">hello type property must be set to: **OnPremisesOracle**</span></span> |<span data-ttu-id="76b5a-168">Ja</span><span class="sxs-lookup"><span data-stu-id="76b5a-168">Yes</span></span> |
| <span data-ttu-id="76b5a-169">driverType</span><span class="sxs-lookup"><span data-stu-id="76b5a-169">driverType</span></span> | <span data-ttu-id="76b5a-170">Geef op welke stuurprogramma toouse toocopy gegevens uit / tooOracle Database.</span><span class="sxs-lookup"><span data-stu-id="76b5a-170">Specify which driver toouse toocopy data from/tooOracle Database.</span></span> <span data-ttu-id="76b5a-171">Toegestane waarden zijn **Microsoft** of **ODP** (standaard).</span><span class="sxs-lookup"><span data-stu-id="76b5a-171">Allowed values are **Microsoft** or **ODP** (default).</span></span> <span data-ttu-id="76b5a-172">Zie [ondersteunde versie en installatieopties](#supported-versions-and-installation) gedeelte stuurprogrammagegevens.</span><span class="sxs-lookup"><span data-stu-id="76b5a-172">See [Supported version and installation](#supported-versions-and-installation) section on driver details.</span></span> | <span data-ttu-id="76b5a-173">Nee</span><span class="sxs-lookup"><span data-stu-id="76b5a-173">No</span></span> |
| <span data-ttu-id="76b5a-174">connectionString</span><span class="sxs-lookup"><span data-stu-id="76b5a-174">connectionString</span></span> | <span data-ttu-id="76b5a-175">Geef informatie tooconnect toohello Oracle-Database-exemplaar voor de eigenschap connectionString Hallo nodig.</span><span class="sxs-lookup"><span data-stu-id="76b5a-175">Specify information needed tooconnect toohello Oracle Database instance for hello connectionString property.</span></span> | <span data-ttu-id="76b5a-176">Ja</span><span class="sxs-lookup"><span data-stu-id="76b5a-176">Yes</span></span> |
| <span data-ttu-id="76b5a-177">gatewayName</span><span class="sxs-lookup"><span data-stu-id="76b5a-177">gatewayName</span></span> | <span data-ttu-id="76b5a-178">Naam van Hallo gateway die die gebruikte tooconnect toohello lokale Oracle-server</span><span class="sxs-lookup"><span data-stu-id="76b5a-178">Name of hello gateway that that is used tooconnect toohello on-premises Oracle server</span></span> |<span data-ttu-id="76b5a-179">Ja</span><span class="sxs-lookup"><span data-stu-id="76b5a-179">Yes</span></span> |

<span data-ttu-id="76b5a-180">**Voorbeeld: met behulp van het stuurprogramma Microsoft:**</span><span class="sxs-lookup"><span data-stu-id="76b5a-180">**Example: using Microsoft driver:**</span></span>
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="76b5a-181">**Voorbeeld: met behulp van ODP stuurprogramma**</span><span class="sxs-lookup"><span data-stu-id="76b5a-181">**Example: using ODP driver**</span></span>

<span data-ttu-id="76b5a-182">Raadpleeg te[deze site](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) voor Hallo indelingen toegestaan.</span><span class="sxs-lookup"><span data-stu-id="76b5a-182">Refer too[this site](https://www.connectionstrings.com/oracle-data-provider-for-net-odp-net/) for hello allowed formats.</span></span>

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="76b5a-183">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="76b5a-183">Dataset properties</span></span>
<span data-ttu-id="76b5a-184">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="76b5a-184">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="76b5a-185">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Oracle, Azure blob-, Azure-tabel, enz.).</span><span class="sxs-lookup"><span data-stu-id="76b5a-185">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Oracle, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="76b5a-186">Hallo typeProperties sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="76b5a-186">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="76b5a-187">Hallo typeProperties sectie voor Hallo gegevensset van het type OracleTable heeft Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="76b5a-187">hello typeProperties section for hello dataset of type OracleTable has hello following properties:</span></span>

| <span data-ttu-id="76b5a-188">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="76b5a-188">Property</span></span> | <span data-ttu-id="76b5a-189">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="76b5a-189">Description</span></span> | <span data-ttu-id="76b5a-190">Vereist</span><span class="sxs-lookup"><span data-stu-id="76b5a-190">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="76b5a-191">tableName</span><span class="sxs-lookup"><span data-stu-id="76b5a-191">tableName</span></span> |<span data-ttu-id="76b5a-192">De naam van de tabel Hallo in Hallo Oracle-Database die Hallo gekoppelde service verwijst.</span><span class="sxs-lookup"><span data-stu-id="76b5a-192">Name of hello table in hello Oracle Database that hello linked service refers to.</span></span> |<span data-ttu-id="76b5a-193">Nee (als **oracleReaderQuery** van **OracleSource** is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="76b5a-193">No (if **oracleReaderQuery** of **OracleSource** is specified)</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="76b5a-194">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="76b5a-194">Copy activity properties</span></span>
<span data-ttu-id="76b5a-195">Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="76b5a-195">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="76b5a-196">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en -beleid zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="76b5a-196">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="76b5a-197">Hallo Kopieeractiviteit slechts één invoer en slechts één uitvoer produceert.</span><span class="sxs-lookup"><span data-stu-id="76b5a-197">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="76b5a-198">Terwijl de eigenschappen die beschikbaar zijn in Hallo typeProperties gedeelte van de activiteit Hallo variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="76b5a-198">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="76b5a-199">Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="76b5a-199">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

### <a name="oraclesource"></a><span data-ttu-id="76b5a-200">OracleSource</span><span class="sxs-lookup"><span data-stu-id="76b5a-200">OracleSource</span></span>
<span data-ttu-id="76b5a-201">In de kopieerbewerking wanneer Hallo bron van het type **OracleSource** Hallo volgende eigenschappen beschikbaar zijn in **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="76b5a-201">In Copy activity, when hello source is of type **OracleSource** hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="76b5a-202">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="76b5a-202">Property</span></span> | <span data-ttu-id="76b5a-203">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="76b5a-203">Description</span></span> | <span data-ttu-id="76b5a-204">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="76b5a-204">Allowed values</span></span> | <span data-ttu-id="76b5a-205">Vereist</span><span class="sxs-lookup"><span data-stu-id="76b5a-205">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="76b5a-206">oracleReaderQuery</span><span class="sxs-lookup"><span data-stu-id="76b5a-206">oracleReaderQuery</span></span> |<span data-ttu-id="76b5a-207">Hallo aangepaste query tooread gegevens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="76b5a-207">Use hello custom query tooread data.</span></span> |<span data-ttu-id="76b5a-208">SQL-query-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="76b5a-208">SQL query string.</span></span> <span data-ttu-id="76b5a-209">Bijvoorbeeld: Selecteer * from MijnTabel</span><span class="sxs-lookup"><span data-stu-id="76b5a-209">For example: select * from MyTable</span></span> <br/><br/><span data-ttu-id="76b5a-210">Als niet wordt opgegeven, Hallo SQL-instructie die is uitgevoerd: Selecteer * from MijnTabel</span><span class="sxs-lookup"><span data-stu-id="76b5a-210">If not specified, hello SQL statement that is executed: select * from MyTable</span></span> |<span data-ttu-id="76b5a-211">Nee (als **tableName** van **gegevensset** is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="76b5a-211">No (if **tableName** of **dataset** is specified)</span></span> |

### <a name="oraclesink"></a><span data-ttu-id="76b5a-212">OracleSink</span><span class="sxs-lookup"><span data-stu-id="76b5a-212">OracleSink</span></span>
<span data-ttu-id="76b5a-213">**OracleSink** ondersteunt Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="76b5a-213">**OracleSink** supports hello following properties:</span></span>

| <span data-ttu-id="76b5a-214">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="76b5a-214">Property</span></span> | <span data-ttu-id="76b5a-215">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="76b5a-215">Description</span></span> | <span data-ttu-id="76b5a-216">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="76b5a-216">Allowed values</span></span> | <span data-ttu-id="76b5a-217">Vereist</span><span class="sxs-lookup"><span data-stu-id="76b5a-217">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="76b5a-218">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="76b5a-218">writeBatchTimeout</span></span> |<span data-ttu-id="76b5a-219">Wachttijd voor Hallo batch insert-bewerking toocomplete voordat een time-out optreedt.</span><span class="sxs-lookup"><span data-stu-id="76b5a-219">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="76b5a-220">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="76b5a-220">timespan</span></span><br/><br/> <span data-ttu-id="76b5a-221">Voorbeeld: 00:30:00 (30 minuten).</span><span class="sxs-lookup"><span data-stu-id="76b5a-221">Example: 00:30:00 (30 minutes).</span></span> |<span data-ttu-id="76b5a-222">Nee</span><span class="sxs-lookup"><span data-stu-id="76b5a-222">No</span></span> |
| <span data-ttu-id="76b5a-223">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="76b5a-223">writeBatchSize</span></span> |<span data-ttu-id="76b5a-224">Voegt de gegevens in SQL-tabel Hallo wanneer Hallo buffergrootte writeBatchSize bereikt.</span><span class="sxs-lookup"><span data-stu-id="76b5a-224">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="76b5a-225">Geheel getal (aantal rijen)</span><span class="sxs-lookup"><span data-stu-id="76b5a-225">Integer (number of rows)</span></span> |<span data-ttu-id="76b5a-226">Nee (standaard: 100)</span><span class="sxs-lookup"><span data-stu-id="76b5a-226">No (default: 100)</span></span> |
| <span data-ttu-id="76b5a-227">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="76b5a-227">sqlWriterCleanupScript</span></span> |<span data-ttu-id="76b5a-228">Geef een query voor de Kopieeractiviteit tooexecute zodat de gegevens van een bepaald segment wordt opgeschoond.</span><span class="sxs-lookup"><span data-stu-id="76b5a-228">Specify a query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> |<span data-ttu-id="76b5a-229">Een query-instructie.</span><span class="sxs-lookup"><span data-stu-id="76b5a-229">A query statement.</span></span> |<span data-ttu-id="76b5a-230">Nee</span><span class="sxs-lookup"><span data-stu-id="76b5a-230">No</span></span> |
| <span data-ttu-id="76b5a-231">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="76b5a-231">sliceIdentifierColumnName</span></span> |<span data-ttu-id="76b5a-232">Geef kolomnaam voor Kopieeractiviteit toofill met segment-ID automatisch gegenereerd en die is gebruikt tooclean van gegevens van een bepaald segment wanneer opnieuw uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="76b5a-232">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> |<span data-ttu-id="76b5a-233">De naam van de kolom van een kolom met gegevenstype binary(32).</span><span class="sxs-lookup"><span data-stu-id="76b5a-233">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="76b5a-234">Nee</span><span class="sxs-lookup"><span data-stu-id="76b5a-234">No</span></span> |

## <a name="json-examples-for-copying-data-tooand-from-oracle-database"></a><span data-ttu-id="76b5a-235">JSON-voorbeelden voor het kopiëren van gegevens tooand van Oracle-database</span><span class="sxs-lookup"><span data-stu-id="76b5a-235">JSON examples for copying data tooand from Oracle database</span></span>
<span data-ttu-id="76b5a-236">Hallo volgende voorbeeld wordt een voorbeeld JSON definities waarmee u een pijplijn toocreate kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="76b5a-236">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="76b5a-237">Ze geven weer hoe toocopy gegevens van / naar/van Azure Blob Storage tooan Oracle-database.</span><span class="sxs-lookup"><span data-stu-id="76b5a-237">They show how toocopy data from/tooan Oracle database to/from Azure Blob Storage.</span></span> <span data-ttu-id="76b5a-238">Gegevens kunnen echter wel gekopieerde tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="76b5a-238">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

## <a name="example-copy-data-from-oracle-tooazure-blob"></a><span data-ttu-id="76b5a-239">Voorbeeld: Gegevens kopiëren van Oracle tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="76b5a-239">Example: Copy data from Oracle tooAzure Blob</span></span>

<span data-ttu-id="76b5a-240">Hallo voorbeeld heeft Hallo data factory-entiteiten te volgen:</span><span class="sxs-lookup"><span data-stu-id="76b5a-240">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="76b5a-241">Een gekoppelde service van het type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="76b5a-241">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="76b5a-242">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="76b5a-242">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="76b5a-243">Invoer [gegevensset](data-factory-create-datasets.md) van het type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="76b5a-243">An input [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="76b5a-244">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="76b5a-244">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="76b5a-245">Een [pijplijn](data-factory-create-pipelines.md) met de kopieeractiviteit die gebruikmaakt van [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) als bron en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) als sink.</span><span class="sxs-lookup"><span data-stu-id="76b5a-245">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [OracleSource](data-factory-onprem-oracle-connector.md#copy-activity-properties) as source and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="76b5a-246">Hallo voorbeeld kopieert gegevens uit een tabel in een lokale Oracle-database tooa blob per uur.</span><span class="sxs-lookup"><span data-stu-id="76b5a-246">hello sample copies data from a table in an on-premises Oracle database tooa blob hourly.</span></span> <span data-ttu-id="76b5a-247">Zie voor meer informatie over diverse eigenschappen die worden gebruikt in de steekproef Hallo documentatie in de secties na Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="76b5a-247">For more information on various properties used in hello sample, see documentation in sections following hello samples.</span></span>

<span data-ttu-id="76b5a-248">**Oracle gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="76b5a-248">**Oracle linked service:**</span></span>

```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "driverType": "Microsoft",
            "connectionString":"Host=<host>;Port=<port>;Sid=<sid>;User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="76b5a-249">**Azure Blob-opslag gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="76b5a-249">**Azure Blob storage linked service:**</span></span>

```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

<span data-ttu-id="76b5a-250">**Oracle-invoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="76b5a-250">**Oracle input dataset:**</span></span>

<span data-ttu-id="76b5a-251">Hallo-voorbeeld wordt ervan uitgegaan dat u hebt een tabel 'MijnTabel' gemaakt in Oracle en bevat een kolom met de naam 'timestampcolumn' voor de reeksgegevens.</span><span class="sxs-lookup"><span data-stu-id="76b5a-251">hello sample assumes you have created a table “MyTable” in Oracle and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="76b5a-252">Instelling 'extern': 'true' informeert Hallo Data Factory-service die gegevensset Hallo externe toohello data factory is en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="76b5a-252">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "OracleInput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "external": true,
        "availability": {
            "offset": "01:00:00",
            "interval": "1",
            "anchorDateTime": "2014-02-27T12:00:00",
            "frequency": "Hour"
        },
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

<span data-ttu-id="76b5a-253">**Azure Blob-uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="76b5a-253">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="76b5a-254">Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="76b5a-254">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="76b5a-255">Hallo map pad en de naam voor de blob Hallo worden dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="76b5a-255">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="76b5a-256">Hallo mappad jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="76b5a-256">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
            "format": {
                "type": "TextFormat",
                "columnDelimiter": "\t",
                "rowDelimiter": "\n"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="76b5a-257">**Pijplijn met de kopieeractiviteit:**</span><span class="sxs-lookup"><span data-stu-id="76b5a-257">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="76b5a-258">Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun per uur is.</span><span class="sxs-lookup"><span data-stu-id="76b5a-258">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun hourly.</span></span> <span data-ttu-id="76b5a-259">Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**OracleSource** en **sink** type is ingesteld, te**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="76b5a-259">In hello pipeline JSON definition, hello **source** type is set too**OracleSource** and **sink** type is set too**BlobSink**.</span></span>  <span data-ttu-id="76b5a-260">Hallo SQL-query is opgegeven met **oracleReaderQuery** eigenschap Hallo gegevens selecteert in Hallo voorbij toocopy uur.</span><span class="sxs-lookup"><span data-stu-id="76b5a-260">hello SQL query specified with **oracleReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "OracletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": " OracleInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "OracleSource",
                        "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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

## <a name="example-copy-data-from-azure-blob-toooracle"></a><span data-ttu-id="76b5a-261">Voorbeeld: Gegevens kopiëren van Azure Blob-tooOracle</span><span class="sxs-lookup"><span data-stu-id="76b5a-261">Example: Copy data from Azure Blob tooOracle</span></span>
<span data-ttu-id="76b5a-262">Dit voorbeeld toont hoe toocopy gegevens uit een Azure Blob Storage tooan lokale Oracle-database.</span><span class="sxs-lookup"><span data-stu-id="76b5a-262">This sample shows how toocopy data from an Azure Blob Storage tooan on-premises Oracle database.</span></span> <span data-ttu-id="76b5a-263">Echter, de gegevens kunnen worden gekopieerd **rechtstreeks** vanaf elke Hallo bronnen vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="76b5a-263">However, data can be copied **directly** from any of hello sources stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>  

<span data-ttu-id="76b5a-264">Hallo voorbeeld heeft Hallo data factory-entiteiten te volgen:</span><span class="sxs-lookup"><span data-stu-id="76b5a-264">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="76b5a-265">Een gekoppelde service van het type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="76b5a-265">A linked service of type [OnPremisesOracle](data-factory-onprem-oracle-connector.md#linked-service-properties).</span></span>
2. <span data-ttu-id="76b5a-266">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="76b5a-266">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="76b5a-267">Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="76b5a-267">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="76b5a-268">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="76b5a-268">An output [dataset](data-factory-create-datasets.md) of type [OracleTable](data-factory-onprem-oracle-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="76b5a-269">Een [pijplijn](data-factory-create-pipelines.md) met de kopieeractiviteit die gebruikmaakt van [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) als bron [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) als sink.</span><span class="sxs-lookup"><span data-stu-id="76b5a-269">A [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) as source [OracleSink](data-factory-onprem-oracle-connector.md#copy-activity-properties) as sink.</span></span>

<span data-ttu-id="76b5a-270">Hallo-voorbeeld worden gegevens gekopieerd van een blob tooa-tabel in een lokale Oracle-database om het uur.</span><span class="sxs-lookup"><span data-stu-id="76b5a-270">hello sample copies data from a blob tooa table in an on-premises Oracle database every hour.</span></span> <span data-ttu-id="76b5a-271">Zie voor meer informatie over diverse eigenschappen die worden gebruikt in de steekproef Hallo documentatie in de secties na Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="76b5a-271">For more information on various properties used in hello sample, see documentation in sections following hello samples.</span></span>

<span data-ttu-id="76b5a-272">**Oracle gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="76b5a-272">**Oracle linked service:**</span></span>
```json
{
    "name": "OnPremisesOracleLinkedService",
    "properties": {
        "type": "OnPremisesOracle",
        "typeProperties": {
            "connectionString": "Data Source=(DESCRIPTION=(ADDRESS=(PROTOCOL=TCP)(HOST=<hostname>)(PORT=<port number>))(CONNECT_DATA=(SERVICE_NAME=<SID>)));
            User Id=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```

<span data-ttu-id="76b5a-273">**Azure Blob-opslag gekoppelde service:**</span><span class="sxs-lookup"><span data-stu-id="76b5a-273">**Azure Blob storage linked service:**</span></span>
```json
{
    "name": "StorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<Account key>"
        }
    }
}
```

<span data-ttu-id="76b5a-274">**Azure Blob-invoergegevensset**</span><span class="sxs-lookup"><span data-stu-id="76b5a-274">**Azure Blob input dataset**</span></span>

<span data-ttu-id="76b5a-275">Gegevens wordt opgehaald uit een nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="76b5a-275">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="76b5a-276">Hallo map pad en de naam voor de blob Hallo worden dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="76b5a-276">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="76b5a-277">Hallo mappad jaar, maand en dag deel uit van de begintijd Hallo en bestandsnaam gebruikt Hallo uur deel uit van de begintijd Hallo.</span><span class="sxs-lookup"><span data-stu-id="76b5a-277">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="76b5a-278">"extern": "true" instelling informeert Hallo Data Factory-service dat deze tabel externe toohello gegevensfactory en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="76b5a-278">“external”: “true” setting informs hello Data Factory service that this table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
                }
            ],
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ",",
                "rowDelimiter": "\n"
            }
        },
        "external": true,
        "availability": {
            "frequency": "Day",
            "interval": 1
        },
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

<span data-ttu-id="76b5a-279">**Oracle-uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="76b5a-279">**Oracle output dataset:**</span></span>

<span data-ttu-id="76b5a-280">Hallo-voorbeeld wordt ervan uitgegaan dat u een tabel "MijnTabel" in Oracle hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="76b5a-280">hello sample assumes you have created a table “MyTable” in Oracle.</span></span> <span data-ttu-id="76b5a-281">Hallo-tabel maken in Oracle met hetzelfde aantal kolommen Hallo zoals Hallo Blob CSV-bestand toocontain verwacht.</span><span class="sxs-lookup"><span data-stu-id="76b5a-281">Create hello table in Oracle with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="76b5a-282">Nieuwe rijen worden toohello tabel toegevoegd om het uur.</span><span class="sxs-lookup"><span data-stu-id="76b5a-282">New rows are added toohello table every hour.</span></span>

```json
{
    "name": "OracleOutput",
    "properties": {
        "type": "OracleTable",
        "linkedServiceName": "OnPremisesOracleLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Day",
            "interval": "1"
        }
    }
}
```

<span data-ttu-id="76b5a-283">**Pijplijn met de kopieeractiviteit:**</span><span class="sxs-lookup"><span data-stu-id="76b5a-283">**Pipeline with Copy activity:**</span></span>

<span data-ttu-id="76b5a-284">Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur.</span><span class="sxs-lookup"><span data-stu-id="76b5a-284">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="76b5a-285">Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**BlobSource** en Hallo **sink** type is ingesteld, te**OracleSink**.</span><span class="sxs-lookup"><span data-stu-id="76b5a-285">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and hello **sink** type is set too**OracleSink**.</span></span>  

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-05T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
            {
                "name": "AzureBlobtoOracle",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                    {
                        "name": "AzureBlobInput"
                    }
                ],
                "outputs": [
                    {
                        "name": "OracleOutput"
                    }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "OracleSink"
                    }
                },
                "scheduler": {
                    "frequency": "Day",
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


## <a name="troubleshooting-tips"></a><span data-ttu-id="76b5a-286">Tips voor probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="76b5a-286">Troubleshooting tips</span></span>
### <a name="problem-1-net-framework-data-provider"></a><span data-ttu-id="76b5a-287">Probleem 1: .NET Framework-gegevensprovider</span><span class="sxs-lookup"><span data-stu-id="76b5a-287">Problem 1: .NET Framework Data Provider</span></span>

<span data-ttu-id="76b5a-288">U ziet de volgende Hallo **foutbericht**:</span><span class="sxs-lookup"><span data-stu-id="76b5a-288">You see hello following **error message**:</span></span>

    Copy activity met invalid parameters: 'UnknownParameterName', Detailed message: Unable toofind hello requested .Net Framework Data Provider. It may not be installed”.  

<span data-ttu-id="76b5a-289">**Mogelijke oorzaken:**</span><span class="sxs-lookup"><span data-stu-id="76b5a-289">**Possible causes:**</span></span>

1. <span data-ttu-id="76b5a-290">Hallo .NET Framework Data Provider voor Oracle is niet geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="76b5a-290">hello .NET Framework Data Provider for Oracle was not installed.</span></span>
2. <span data-ttu-id="76b5a-291">Hallo .NET Framework Data Provider voor Oracle geïnstalleerde too.NET Framework 2.0 en is niet gevonden in mappen Hallo .NET Framework 4.0.</span><span class="sxs-lookup"><span data-stu-id="76b5a-291">hello .NET Framework Data Provider for Oracle was installed too.NET Framework 2.0 and is not found in hello .NET Framework 4.0 folders.</span></span>

<span data-ttu-id="76b5a-292">**Resolutie/tijdelijke oplossing:**</span><span class="sxs-lookup"><span data-stu-id="76b5a-292">**Resolution/Workaround:**</span></span>

1. <span data-ttu-id="76b5a-293">Als u dit nog niet hebt geïnstalleerd Hallo .NET-Provider voor Oracle, [installeren](http://www.oracle.com/technetwork/topics/dotnet/downloads/) en probeer het opnieuw Hallo scenario.</span><span class="sxs-lookup"><span data-stu-id="76b5a-293">If you haven't installed hello .NET Provider for Oracle, [install it](http://www.oracle.com/technetwork/topics/dotnet/downloads/) and retry hello scenario.</span></span>
2. <span data-ttu-id="76b5a-294">Als u Hallo foutbericht krijgt zelfs na het installeren van de provider hello, Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="76b5a-294">If you get hello error message even after installing hello provider, do hello following steps:</span></span>
   1. <span data-ttu-id="76b5a-295">Machine config van .NET 2.0 openen vanuit de map Hallo: <system disk>: \Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span><span class="sxs-lookup"><span data-stu-id="76b5a-295">Open machine config of .NET 2.0 from hello folder: <system disk>:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG\machine.config.</span></span>
   2. <span data-ttu-id="76b5a-296">Zoeken naar **Oracle-gegevensprovider voor .NET**, en u moet kunnen toofind een vermelding zoals weergegeven in het voorbeeld onder na Hallo **systeem.gegevens** -> **DbProviderFactories**: '<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Oracle-gegevensprovider voor .NET</span><span class="sxs-lookup"><span data-stu-id="76b5a-296">Search for **Oracle Data Provider for .NET**, and you should be able toofind an entry as shown in hello following sample under **system.data** -> **DbProviderFactories**: “<add name="Oracle Data Provider for .NET" invariant="Oracle.DataAccess.Client" description="Oracle Data Provider for .NET</span></span>" type="Oracle.DataAccess.Client.OracleClientFactory, Oracle.DataAccess, Version=2.112.3.0, Culture=neutral, PublicKeyToken=89b483f429c47342" /><span data-ttu-id="76b5a-297">”</span><span class="sxs-lookup"><span data-stu-id="76b5a-297">”</span></span>
3. <span data-ttu-id="76b5a-298">Deze vermelding toohello machine.config-bestand in Hallo na v4.0 map kopiëren: <system disk>: \Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config en wijziging Hallo versie too4.xxx.x.x.</span><span class="sxs-lookup"><span data-stu-id="76b5a-298">Copy this entry toohello machine.config file in hello following v4.0 folder: <system disk>:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config, and change hello version too4.xxx.x.x.</span></span>
4. <span data-ttu-id="76b5a-299">'< Pad ODP.NET geïnstalleerde > \11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll' in hello globale assembly-cache (GAC) installeren door te voeren `gacutil /i [provider path]`. ## tips voor probleemoplossing</span><span class="sxs-lookup"><span data-stu-id="76b5a-299">Install “<ODP.NET Installed Path>\11.2.0\client_1\odp.net\bin\4\Oracle.DataAccess.dll” into hello global assembly cache (GAC) by running `gacutil /i [provider path]`.## Troubleshooting tips</span></span>

### <a name="problem-2-datetime-formatting"></a><span data-ttu-id="76b5a-300">Probleem 2: opmaak voor datum/tijd</span><span class="sxs-lookup"><span data-stu-id="76b5a-300">Problem 2: datetime formatting</span></span>

<span data-ttu-id="76b5a-301">U ziet de volgende Hallo **foutbericht**:</span><span class="sxs-lookup"><span data-stu-id="76b5a-301">You see hello following **error message**:</span></span>

    Message=Operation failed in Oracle Database with hello following error: 'ORA-01861: literal does not match format string'.,Source=,''Type=Oracle.DataAccess.Client.OracleException,Message=ORA-01861: literal does not match format string,Source=Oracle Data Provider for .NET,'.

<span data-ttu-id="76b5a-302">**Resolutie/tijdelijke oplossing:**</span><span class="sxs-lookup"><span data-stu-id="76b5a-302">**Resolution/Workaround:**</span></span>

<span data-ttu-id="76b5a-303">Mogelijk moet u tooadjust Hallo queryreeks in de kopieerbewerking op basis van hoe datums zijn geconfigureerd in de Oracle-database, zoals weergegeven in de volgende hello (met Hallo to_date functie) voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="76b5a-303">You may need tooadjust hello query string in your copy activity based on how dates are configured in your Oracle database, as shown in hello following sample (using hello to_date function):</span></span>

    "oracleReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= to_date(\\'{0:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\')  AND timestampcolumn < to_date(\\'{1:MM-dd-yyyy HH:mm}\\',\\'MM/DD/YYYY HH24:MI\\') ', WindowStart, WindowEnd)"


## <a name="type-mapping-for-oracle"></a><span data-ttu-id="76b5a-304">Toewijzing van het type voor Oracle</span><span class="sxs-lookup"><span data-stu-id="76b5a-304">Type mapping for Oracle</span></span>
<span data-ttu-id="76b5a-305">Zoals vermeld in Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel kopieeractiviteit voert automatische typeconversies van brontypen typen toosink Hello 2 stap benadering te volgen:</span><span class="sxs-lookup"><span data-stu-id="76b5a-305">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="76b5a-306">Systeemeigen bron typen too.NET type converteren</span><span class="sxs-lookup"><span data-stu-id="76b5a-306">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="76b5a-307">Converteren van .NET-type toonative sink-type</span><span class="sxs-lookup"><span data-stu-id="76b5a-307">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="76b5a-308">Bij het verplaatsen van gegevens uit Oracle, worden volgende toewijzingen Hallo gebruikt van het type Oracle-too.NET gegevenstype en vice versa.</span><span class="sxs-lookup"><span data-stu-id="76b5a-308">When moving data from Oracle, hello following mappings are used from Oracle data type too.NET type and vice versa.</span></span>

| <span data-ttu-id="76b5a-309">Oracle-gegevenstype</span><span class="sxs-lookup"><span data-stu-id="76b5a-309">Oracle data type</span></span> | <span data-ttu-id="76b5a-310">.NET framework-gegevenstype</span><span class="sxs-lookup"><span data-stu-id="76b5a-310">.NET Framework data type</span></span> |
| --- | --- |
| <span data-ttu-id="76b5a-311">BBESTAND</span><span class="sxs-lookup"><span data-stu-id="76b5a-311">BFILE</span></span> |<span data-ttu-id="76b5a-312">Byte]</span><span class="sxs-lookup"><span data-stu-id="76b5a-312">Byte[]</span></span> |
| <span data-ttu-id="76b5a-313">BLOB</span><span class="sxs-lookup"><span data-stu-id="76b5a-313">BLOB</span></span> |<span data-ttu-id="76b5a-314">Byte]</span><span class="sxs-lookup"><span data-stu-id="76b5a-314">Byte[]</span></span> |
| <span data-ttu-id="76b5a-315">CHAR</span><span class="sxs-lookup"><span data-stu-id="76b5a-315">CHAR</span></span> |<span data-ttu-id="76b5a-316">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="76b5a-316">String</span></span> |
| <span data-ttu-id="76b5a-317">CLOB</span><span class="sxs-lookup"><span data-stu-id="76b5a-317">CLOB</span></span> |<span data-ttu-id="76b5a-318">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="76b5a-318">String</span></span> |
| <span data-ttu-id="76b5a-319">DATUM</span><span class="sxs-lookup"><span data-stu-id="76b5a-319">DATE</span></span> |<span data-ttu-id="76b5a-320">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="76b5a-320">DateTime</span></span> |
| <span data-ttu-id="76b5a-321">FLOAT</span><span class="sxs-lookup"><span data-stu-id="76b5a-321">FLOAT</span></span> |<span data-ttu-id="76b5a-322">Decimaal, tekenreeks (als precision > 28)</span><span class="sxs-lookup"><span data-stu-id="76b5a-322">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="76b5a-323">GEHEEL GETAL</span><span class="sxs-lookup"><span data-stu-id="76b5a-323">INTEGER</span></span> |<span data-ttu-id="76b5a-324">Decimaal, tekenreeks (als precision > 28)</span><span class="sxs-lookup"><span data-stu-id="76b5a-324">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="76b5a-325">INTERVAL jaar tooMONTH</span><span class="sxs-lookup"><span data-stu-id="76b5a-325">INTERVAL YEAR tooMONTH</span></span> |<span data-ttu-id="76b5a-326">Int32</span><span class="sxs-lookup"><span data-stu-id="76b5a-326">Int32</span></span> |
| <span data-ttu-id="76b5a-327">INTERVAL dag tooSECOND</span><span class="sxs-lookup"><span data-stu-id="76b5a-327">INTERVAL DAY tooSECOND</span></span> |<span data-ttu-id="76b5a-328">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="76b5a-328">TimeSpan</span></span> |
| <span data-ttu-id="76b5a-329">LANG</span><span class="sxs-lookup"><span data-stu-id="76b5a-329">LONG</span></span> |<span data-ttu-id="76b5a-330">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="76b5a-330">String</span></span> |
| <span data-ttu-id="76b5a-331">LANGE ONBEWERKTE</span><span class="sxs-lookup"><span data-stu-id="76b5a-331">LONG RAW</span></span> |<span data-ttu-id="76b5a-332">Byte]</span><span class="sxs-lookup"><span data-stu-id="76b5a-332">Byte[]</span></span> |
| <span data-ttu-id="76b5a-333">NCHAR</span><span class="sxs-lookup"><span data-stu-id="76b5a-333">NCHAR</span></span> |<span data-ttu-id="76b5a-334">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="76b5a-334">String</span></span> |
| <span data-ttu-id="76b5a-335">NCLOB</span><span class="sxs-lookup"><span data-stu-id="76b5a-335">NCLOB</span></span> |<span data-ttu-id="76b5a-336">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="76b5a-336">String</span></span> |
| <span data-ttu-id="76b5a-337">AANTAL</span><span class="sxs-lookup"><span data-stu-id="76b5a-337">NUMBER</span></span> |<span data-ttu-id="76b5a-338">Decimaal, tekenreeks (als precision > 28)</span><span class="sxs-lookup"><span data-stu-id="76b5a-338">Decimal, String (if precision > 28)</span></span> |
| <span data-ttu-id="76b5a-339">NVARCHAR2</span><span class="sxs-lookup"><span data-stu-id="76b5a-339">NVARCHAR2</span></span> |<span data-ttu-id="76b5a-340">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="76b5a-340">String</span></span> |
| <span data-ttu-id="76b5a-341">ONBEWERKTE</span><span class="sxs-lookup"><span data-stu-id="76b5a-341">RAW</span></span> |<span data-ttu-id="76b5a-342">Byte]</span><span class="sxs-lookup"><span data-stu-id="76b5a-342">Byte[]</span></span> |
| <span data-ttu-id="76b5a-343">ROWID</span><span class="sxs-lookup"><span data-stu-id="76b5a-343">ROWID</span></span> |<span data-ttu-id="76b5a-344">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="76b5a-344">String</span></span> |
| <span data-ttu-id="76b5a-345">TIJDSTEMPEL</span><span class="sxs-lookup"><span data-stu-id="76b5a-345">TIMESTAMP</span></span> |<span data-ttu-id="76b5a-346">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="76b5a-346">DateTime</span></span> |
| <span data-ttu-id="76b5a-347">TIJDSTEMPEL MET DE LOKALE TIJDZONE</span><span class="sxs-lookup"><span data-stu-id="76b5a-347">TIMESTAMP WITH LOCAL TIME ZONE</span></span> |<span data-ttu-id="76b5a-348">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="76b5a-348">DateTime</span></span> |
| <span data-ttu-id="76b5a-349">TIJDSTEMPEL MET TIJDZONE</span><span class="sxs-lookup"><span data-stu-id="76b5a-349">TIMESTAMP WITH TIME ZONE</span></span> |<span data-ttu-id="76b5a-350">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="76b5a-350">DateTime</span></span> |
| <span data-ttu-id="76b5a-351">NIET-ONDERTEKEND GEHEEL GETAL</span><span class="sxs-lookup"><span data-stu-id="76b5a-351">UNSIGNED INTEGER</span></span> |<span data-ttu-id="76b5a-352">Aantal</span><span class="sxs-lookup"><span data-stu-id="76b5a-352">Number</span></span> |
| <span data-ttu-id="76b5a-353">VARCHAR2</span><span class="sxs-lookup"><span data-stu-id="76b5a-353">VARCHAR2</span></span> |<span data-ttu-id="76b5a-354">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="76b5a-354">String</span></span> |
| <span data-ttu-id="76b5a-355">XML</span><span class="sxs-lookup"><span data-stu-id="76b5a-355">XML</span></span> |<span data-ttu-id="76b5a-356">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="76b5a-356">String</span></span> |

> [!NOTE]
> <span data-ttu-id="76b5a-357">Gegevenstype **INTERVAL jaar tooMONTH** en **INTERVAL dag tooSECOND** worden niet ondersteund bij gebruik van Microsoft-stuurprogramma.</span><span class="sxs-lookup"><span data-stu-id="76b5a-357">Data type **INTERVAL YEAR tooMONTH** and **INTERVAL DAY tooSECOND** are not supported when using Microsoft driver.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="76b5a-358">Bronkolommen toosink toewijzen</span><span class="sxs-lookup"><span data-stu-id="76b5a-358">Map source toosink columns</span></span>
<span data-ttu-id="76b5a-359">Zie toolearn over het toewijzen van kolommen in bron gegevensset toocolumns in sink-gegevensset [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="76b5a-359">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="76b5a-360">Herhaalbare leesbewerking van relationele bronnen</span><span class="sxs-lookup"><span data-stu-id="76b5a-360">Repeatable read from relational sources</span></span>
<span data-ttu-id="76b5a-361">Houd bij het kopiëren van gegevens uit een relationele gegevensopslag, herhaalbaarheid rekening tooavoid ongewenste resultaten.</span><span class="sxs-lookup"><span data-stu-id="76b5a-361">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="76b5a-362">In Azure Data Factory, kunt u een segment handmatig opnieuw.</span><span class="sxs-lookup"><span data-stu-id="76b5a-362">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="76b5a-363">U kunt ook een beleid voor opnieuw proberen voor een gegevensset configureren zodat een segment wordt opnieuw uitgevoerd wanneer een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="76b5a-363">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="76b5a-364">Wanneer een segment opnieuw in beide gevallen wordt uitgevoerd, moet u ervoor dat dezelfde gegevens Hallo toomake wordt gelezen ongeacht hoe vaak een segment wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="76b5a-364">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="76b5a-365">Zie [Repeatable van relationele bronnen lezen](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="76b5a-365">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="76b5a-366">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="76b5a-366">Performance and Tuning</span></span>
<span data-ttu-id="76b5a-367">Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.</span><span class="sxs-lookup"><span data-stu-id="76b5a-367">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
