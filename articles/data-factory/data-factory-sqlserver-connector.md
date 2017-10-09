---
title: aaaMove gegevens tooand van SQL Server | Microsoft Docs
description: Meer informatie over hoe toomove gegevens van/naar SQL Server-database die lokaal of in een virtuele machine in Azure met Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 864ece28-93b5-4309-9873-b095bbe6fedd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jingwang
ms.openlocfilehash: f0cccf56a670e62ec893d75052a81eb26d562050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-sql-server-on-premises-or-on-iaas-azure-vm-using-azure-data-factory"></a><span data-ttu-id="f3cbe-103">Verplaatsen van gegevens tooand van SQL Server on-premises of op IaaS (Azure VM) met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="f3cbe-103">Move data tooand from SQL Server on-premises or on IaaS (Azure VM) using Azure Data Factory</span></span>
<span data-ttu-id="f3cbe-104">Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit Hallo in Azure Data Factory toomove gegevens uit een on-premises SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data to/from an on-premises SQL Server database.</span></span> <span data-ttu-id="f3cbe-105">Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="f3cbe-106">Ondersteunde scenario 's</span><span class="sxs-lookup"><span data-stu-id="f3cbe-106">Supported scenarios</span></span>
<span data-ttu-id="f3cbe-107">U kunt gegevens kopiëren **uit een SQL Server-database** toohello gegevensarchieven te volgen:</span><span class="sxs-lookup"><span data-stu-id="f3cbe-107">You can copy data **from a SQL Server database** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="f3cbe-108">Gegevens kunnen worden gekopieerd van de volgende gegevensarchieven Hallo **tooa SQL Server-database**:</span><span class="sxs-lookup"><span data-stu-id="f3cbe-108">You can copy data from hello following data stores **tooa SQL Server database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-sql-server-versions"></a><span data-ttu-id="f3cbe-109">Ondersteunde versies van SQL Server</span><span class="sxs-lookup"><span data-stu-id="f3cbe-109">Supported SQL Server versions</span></span>
<span data-ttu-id="f3cbe-110">Deze ondersteuning van SQL Server-connector kopiëren van gegevens uit / toohello volgende versies van gehost exemplaar lokaal of in Azure IaaS met behulp van zowel de SQL-verificatie en de Windows-verificatie: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span><span class="sxs-lookup"><span data-stu-id="f3cbe-110">This SQL Server connector support copying data from/toohello following versions of instance hosted on-premises or in Azure IaaS using both SQL authentication and Windows authentication: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="f3cbe-111">Connectiviteit inschakelen</span><span class="sxs-lookup"><span data-stu-id="f3cbe-111">Enabling connectivity</span></span>
<span data-ttu-id="f3cbe-112">Hallo-concepten en de stappen die nodig zijn om verbinding te maken met SQL Server die wordt gehost on-premises of in Azure IaaS (Infrastructure-as-a-Service) virtuele machines zijn Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-112">hello concepts and steps needed for connecting with SQL Server hosted on-premises or in Azure IaaS (Infrastructure-as-a-Service) VMs are hello same.</span></span> <span data-ttu-id="f3cbe-113">In beide gevallen moet u toouse Data Management Gateway voor connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-113">In both cases, you need toouse Data Management Gateway for connectivity.</span></span>

<span data-ttu-id="f3cbe-114">Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn artikel over Data Management Gateway en stapsgewijze instructies over het instellen van Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-114">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span> <span data-ttu-id="f3cbe-115">Instellen van een gatewayexemplaar is een vereiste voor het verbinden met SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-115">Setting up a gateway instance is a pre-requisite for connecting with SQL Server.</span></span>

<span data-ttu-id="f3cbe-116">Tijdens de installatie van gateway op Hallo dezelfde lokale machine of de cloud VM-instantie als Hallo van SQL Server voor betere prestaties, raden we u deze installeren op afzonderlijke computers.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-116">While you can install gateway on hello same on-premises machine or cloud VM instance as hello SQL Server for better performance, we recommended that you install them on separate machines.</span></span> <span data-ttu-id="f3cbe-117">Hallo-gateway en SQL Server met op afzonderlijke computers, worden bronconflicten beperkt.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-117">Having hello gateway and SQL Server on separate machines reduces resource contention.</span></span>

## <a name="getting-started"></a><span data-ttu-id="f3cbe-118">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="f3cbe-118">Getting started</span></span>
<span data-ttu-id="f3cbe-119">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens uit een on-premises SQL Server database verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-119">You can create a pipeline with a copy activity that moves data to/from an on-premises SQL Server database by using different tools/APIs.</span></span>

<span data-ttu-id="f3cbe-120">Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="f3cbe-121">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="f3cbe-122">U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="f3cbe-123">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="f3cbe-124">Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="f3cbe-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="f3cbe-125">Maak een **gegevensfactory**.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-125">Create a **data factory**.</span></span> <span data-ttu-id="f3cbe-126">Een gegevensfactory kan één of meer pijplijnen bevatten.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="f3cbe-127">Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="f3cbe-128">Bijvoorbeeld, als u gegevens uit een SQL Server-database tooan Azure blob-opslag kopiëren wilt, u twee gekoppelde services toolink uw SQL Server-database en de Azure storage-account tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-128">For example, if you are copying data from a SQL Server database tooan Azure blob storage, you create two linked services toolink your SQL Server database and Azure storage account tooyour data factory.</span></span> <span data-ttu-id="f3cbe-129">Zie voor de gekoppelde service-eigenschappen die specifiek tooSQL Server-database, [gekoppelde service-eigenschappen](#linked-service-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-129">For linked service properties that are specific tooSQL Server database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="f3cbe-130">Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-130">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="f3cbe-131">In voorbeeld Hallo vermeld in de laatste stap Hallo kunt u een gegevensset toospecify Hallo SQL-tabel maken in uw SQL Server-database waarin de invoergegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-131">In hello example mentioned in hello last step, you create a dataset toospecify hello SQL table in your SQL Server database that contains hello input data.</span></span> <span data-ttu-id="f3cbe-132">Maken van een andere dataset toospecify Hallo blob-container en Hallo map Hallo gegevens gekopieerd van Hallo SQL Server-database.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-132">And, you create another dataset toospecify hello blob container and hello folder that holds hello data copied from hello SQL Server database.</span></span> <span data-ttu-id="f3cbe-133">Zie voor eigenschappen van gegevensset die specifieke tooSQL Server-database, [eigenschappen van gegevensset](#dataset-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-133">For dataset properties that are specific tooSQL Server database, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="f3cbe-134">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="f3cbe-135">In Hallo voorbeeld eerder vermeld, gebruikt u SqlSource als een bron- en BlobSink als een sink voor de kopieeractiviteit Hallo.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-135">In hello example mentioned earlier, you use SqlSource as a source and BlobSink as a sink for hello copy activity.</span></span> <span data-ttu-id="f3cbe-136">Op dezelfde manier als u uit Azure Blob Storage tooSQL Server-Database kopiëren wilt, gebruikt u BlobSource en SqlSink in Hallo kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-136">Similarly, if you are copying from Azure Blob Storage tooSQL Server Database, you use BlobSource and SqlSink in hello copy activity.</span></span> <span data-ttu-id="f3cbe-137">Zie voor activiteitseigenschappen kopiëren die specifieke tooSQL Server-Database, [activiteitseigenschappen kopiëren](#copy-activity-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-137">For copy activity properties that are specific tooSQL Server Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="f3cbe-138">Voor informatie over hoe toouse een gegevensarchief als een bron of een sink, klikt u op Hallo-koppeling in de vorige sectie Hallo voor de gegevensopslag.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-138">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span> 

<span data-ttu-id="f3cbe-139">Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-139">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="f3cbe-140">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="f3cbe-141">Zie voor voorbeelden met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens van/naar een lokale SQL Server-database zijn, [JSON voorbeelden](#json-examples-for-copying-data-from-and-to-sql-server) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-141">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an on-premises SQL Server database, see [JSON examples](#json-examples-for-copying-data-from-and-to-sql-server) section of this article.</span></span> 

<span data-ttu-id="f3cbe-142">Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooSQL Server zijn:</span><span class="sxs-lookup"><span data-stu-id="f3cbe-142">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooSQL Server:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="f3cbe-143">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="f3cbe-143">Linked service properties</span></span>
<span data-ttu-id="f3cbe-144">Maken van een gekoppelde service van het type **OnPremisesSqlServer** toolink een lokale SQL Server-database tooa data factory.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-144">You create a linked service of type **OnPremisesSqlServer** toolink an on-premises SQL Server database tooa data factory.</span></span> <span data-ttu-id="f3cbe-145">Hallo volgende tabel biedt een beschrijving voor de service voor JSON-elementen specifieke tooon-premises SQL Server gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-145">hello following table provides description for JSON elements specific tooon-premises SQL Server linked service.</span></span>

<span data-ttu-id="f3cbe-146">Hallo volgende tabel bevat een beschrijving voor JSON-elementen specifieke tooSQL gekoppelde Server-service.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-146">hello following table provides description for JSON elements specific tooSQL Server linked service.</span></span>

| <span data-ttu-id="f3cbe-147">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="f3cbe-147">Property</span></span> | <span data-ttu-id="f3cbe-148">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f3cbe-148">Description</span></span> | <span data-ttu-id="f3cbe-149">Vereist</span><span class="sxs-lookup"><span data-stu-id="f3cbe-149">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f3cbe-150">type</span><span class="sxs-lookup"><span data-stu-id="f3cbe-150">type</span></span> |<span data-ttu-id="f3cbe-151">Hallo type eigenschap moet worden ingesteld op: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-151">hello type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="f3cbe-152">Ja</span><span class="sxs-lookup"><span data-stu-id="f3cbe-152">Yes</span></span> |
| <span data-ttu-id="f3cbe-153">connectionString</span><span class="sxs-lookup"><span data-stu-id="f3cbe-153">connectionString</span></span> |<span data-ttu-id="f3cbe-154">Geef connectionString informatie nodig tooconnect toohello lokale SQL Server-database met behulp van de SQL-verificatie of de Windows-verificatie.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-154">Specify connectionString information needed tooconnect toohello on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="f3cbe-155">Ja</span><span class="sxs-lookup"><span data-stu-id="f3cbe-155">Yes</span></span> |
| <span data-ttu-id="f3cbe-156">gatewayName</span><span class="sxs-lookup"><span data-stu-id="f3cbe-156">gatewayName</span></span> |<span data-ttu-id="f3cbe-157">Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello lokale SQL Server-database gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-157">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises SQL Server database.</span></span> |<span data-ttu-id="f3cbe-158">Ja</span><span class="sxs-lookup"><span data-stu-id="f3cbe-158">Yes</span></span> |
| <span data-ttu-id="f3cbe-159">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="f3cbe-159">username</span></span> |<span data-ttu-id="f3cbe-160">Geef de gebruikersnaam als u Windows-verificatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-160">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="f3cbe-161">Voorbeeld: **domainname\\gebruikersnaam**.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-161">Example: **domainname\\username**.</span></span> |<span data-ttu-id="f3cbe-162">Nee</span><span class="sxs-lookup"><span data-stu-id="f3cbe-162">No</span></span> |
| <span data-ttu-id="f3cbe-163">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="f3cbe-163">password</span></span> |<span data-ttu-id="f3cbe-164">Wachtwoord voor gebruikersaccount Hallo die u hebt opgegeven voor Hallo gebruikersnaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-164">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="f3cbe-165">Nee</span><span class="sxs-lookup"><span data-stu-id="f3cbe-165">No</span></span> |

<span data-ttu-id="f3cbe-166">U kunt referenties met een Hallo versleutelen **nieuw AzureRmDataFactoryEncryptValue** cmdlet en in de verbindingsreeks hello gebruiken, zoals wordt weergegeven in het volgende voorbeeld Hallo (**EncryptedCredential** eigenschap):</span><span class="sxs-lookup"><span data-stu-id="f3cbe-166">You can encrypt credentials using hello **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in hello connection string as shown in hello following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

### <a name="samples"></a><span data-ttu-id="f3cbe-167">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="f3cbe-167">Samples</span></span>
<span data-ttu-id="f3cbe-168">**JSON voor het gebruik van SQL-verificatie**</span><span class="sxs-lookup"><span data-stu-id="f3cbe-168">**JSON for using SQL Authentication**</span></span>

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties":
    {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
<span data-ttu-id="f3cbe-169">**JSON voor het gebruik van Windows-verificatie**</span><span class="sxs-lookup"><span data-stu-id="f3cbe-169">**JSON for using Windows Authentication**</span></span>

<span data-ttu-id="f3cbe-170">Data Management Gateway imiteert Hallo opgegeven gebruiker account tooconnect toohello lokale SQL Server-database.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-170">Data Management Gateway will impersonate hello specified user account tooconnect toohello on-premises SQL Server database.</span></span> 

```json
{
     "Name": " MyOnPremisesSQLDB",
     "Properties":
     {
         "type": "OnPremisesSqlServer",
         "typeProperties": {
             "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
             "username": "<domain\\username>",
             "password": "<password>",
             "gatewayName": "<gateway name>"
        }
     }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="f3cbe-171">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="f3cbe-171">Dataset properties</span></span>
<span data-ttu-id="f3cbe-172">In Hallo voorbeelden, hebt u een gegevensset van het type gebruikt **SqlServerTable** toorepresent een tabel in een SQL Server-database.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-172">In hello samples, you have used a dataset of type **SqlServerTable** toorepresent a table in a SQL Server database.</span></span>  

<span data-ttu-id="f3cbe-173">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-173">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="f3cbe-174">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (SQL Server, Azure blob-, Azure-tabel, enz.).</span><span class="sxs-lookup"><span data-stu-id="f3cbe-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (SQL Server, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="f3cbe-175">Hallo typeProperties sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-175">hello typeProperties section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="f3cbe-176">Hallo **typeProperties** sectie voor Hallo gegevensset van het type **SqlServerTable** heeft Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="f3cbe-176">hello **typeProperties** section for hello dataset of type **SqlServerTable** has hello following properties:</span></span>

| <span data-ttu-id="f3cbe-177">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="f3cbe-177">Property</span></span> | <span data-ttu-id="f3cbe-178">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f3cbe-178">Description</span></span> | <span data-ttu-id="f3cbe-179">Vereist</span><span class="sxs-lookup"><span data-stu-id="f3cbe-179">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f3cbe-180">tableName</span><span class="sxs-lookup"><span data-stu-id="f3cbe-180">tableName</span></span> |<span data-ttu-id="f3cbe-181">De naam van het Hallo-tabel of weergave in Hallo SQL Server Database-instantie waarnaar de gekoppelde service verwijst.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-181">Name of hello table or view in hello SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="f3cbe-182">Ja</span><span class="sxs-lookup"><span data-stu-id="f3cbe-182">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="f3cbe-183">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="f3cbe-183">Copy activity properties</span></span>
<span data-ttu-id="f3cbe-184">Als u gegevens uit een SQL Server-database verplaatst, u Hallo brontype instellen in de kopieerbewerking Hallo te**SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-184">If you are moving data from a SQL Server database, you set hello source type in hello copy activity too**SqlSource**.</span></span> <span data-ttu-id="f3cbe-185">Als u gegevens tooa SQL Server-database verplaatst, u stelt Hallo sink-type in de kopieerbewerking Hallo te**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-185">Similarly, if you are moving data tooa SQL Server database, you set hello sink type in hello copy activity too**SqlSink**.</span></span> <span data-ttu-id="f3cbe-186">Deze sectie bevat een lijst met eigenschappen die worden ondersteund door SqlSource en SqlSink.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-186">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

<span data-ttu-id="f3cbe-187">Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-187">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="f3cbe-188">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en beleidsregels zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-188">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="f3cbe-189">Hallo Kopieeractiviteit slechts één invoer en slechts één uitvoer produceert.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-189">hello Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="f3cbe-190">Terwijl de eigenschappen die beschikbaar zijn in Hallo typeProperties gedeelte van de activiteit Hallo variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-190">Whereas, properties available in hello typeProperties section of hello activity vary with each activity type.</span></span> <span data-ttu-id="f3cbe-191">Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-191">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="f3cbe-192">SqlSource</span><span class="sxs-lookup"><span data-stu-id="f3cbe-192">SqlSource</span></span>
<span data-ttu-id="f3cbe-193">Wanneer u de gegevensbron in een kopieeractiviteit is van het type **SqlSource**, Hallo volgende eigenschappen beschikbaar zijn in **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="f3cbe-193">When source in a copy activity is of type **SqlSource**, hello following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="f3cbe-194">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="f3cbe-194">Property</span></span> | <span data-ttu-id="f3cbe-195">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f3cbe-195">Description</span></span> | <span data-ttu-id="f3cbe-196">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="f3cbe-196">Allowed values</span></span> | <span data-ttu-id="f3cbe-197">Vereist</span><span class="sxs-lookup"><span data-stu-id="f3cbe-197">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f3cbe-198">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="f3cbe-198">sqlReaderQuery</span></span> |<span data-ttu-id="f3cbe-199">Hallo aangepaste query tooread gegevens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-199">Use hello custom query tooread data.</span></span> |<span data-ttu-id="f3cbe-200">SQL-query-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-200">SQL query string.</span></span> <span data-ttu-id="f3cbe-201">Bijvoorbeeld: Selecteer * from MijnTabel.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-201">For example: select * from MyTable.</span></span> <span data-ttu-id="f3cbe-202">Kan naar meerdere tabellen uit Hallo database waarnaar wordt verwezen door de invoergegevensset Hallo verwijzen.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-202">May reference multiple tables from hello database referenced by hello input dataset.</span></span> <span data-ttu-id="f3cbe-203">Als niet wordt opgegeven, Hallo SQL-instructie die is uitgevoerd: Selecteer een van de MyTable.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-203">If not specified, hello SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="f3cbe-204">Nee</span><span class="sxs-lookup"><span data-stu-id="f3cbe-204">No</span></span> |
| <span data-ttu-id="f3cbe-205">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="f3cbe-205">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="f3cbe-206">Naam van Hallo opgeslagen procedure die gegevens uit Hallo brontabel leest.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-206">Name of hello stored procedure that reads data from hello source table.</span></span> |<span data-ttu-id="f3cbe-207">Naam van Hallo opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-207">Name of hello stored procedure.</span></span> <span data-ttu-id="f3cbe-208">Hallo laatste SQL-instructie moet een SELECT-instructie in Hallo opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-208">hello last SQL statement must be a SELECT statement in hello stored procedure.</span></span> |<span data-ttu-id="f3cbe-209">Nee</span><span class="sxs-lookup"><span data-stu-id="f3cbe-209">No</span></span> |
| <span data-ttu-id="f3cbe-210">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="f3cbe-210">storedProcedureParameters</span></span> |<span data-ttu-id="f3cbe-211">Parameters voor Hallo opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-211">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="f3cbe-212">Naam/waarde-paren.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-212">Name/value pairs.</span></span> <span data-ttu-id="f3cbe-213">Namen en hoofdlettergebruik van parameters moeten overeenkomen met Hallo namen en hoofdlettergebruik van Hallo opgeslagen procedureparameters.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-213">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="f3cbe-214">Nee</span><span class="sxs-lookup"><span data-stu-id="f3cbe-214">No</span></span> |

<span data-ttu-id="f3cbe-215">Als hello **sqlReaderQuery** is opgegeven voor Hallo SqlSource, hello Kopieeractiviteit deze query wordt uitgevoerd tegen Hallo SQL Server-Database tooget Hallo brongegevens.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-215">If hello **sqlReaderQuery** is specified for hello SqlSource, hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span>

<span data-ttu-id="f3cbe-216">U kunt ook een opgeslagen procedure opgeven door te geven Hallo **sqlReaderStoredProcedureName** en **storedProcedureParameters** (als hello opgeslagen procedure parameters zijn vereist).</span><span class="sxs-lookup"><span data-stu-id="f3cbe-216">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span>

<span data-ttu-id="f3cbe-217">Als u geen sqlReaderQuery of sqlReaderStoredProcedureName opgeeft, zijn gedefinieerd in de sectie structuur Hallo Hallo-kolommen gebruikte toobuild een toorun selectiequery tegen Hallo SQL Server-Database.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-217">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="f3cbe-218">Als de definitie van de gegevensset Hallo geen Hallo structuur, worden alle kolommen uit Hallo tabel geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-218">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

> [!NOTE]
> <span data-ttu-id="f3cbe-219">Als u werkt met **sqlReaderStoredProcedureName**, moet u nog steeds toospecify een waarde voor Hallo **tableName** eigenschap in de gegevensset Hallo JSON.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-219">When you use **sqlReaderStoredProcedureName**, you still need toospecify a value for hello **tableName** property in hello dataset JSON.</span></span> <span data-ttu-id="f3cbe-220">Er zijn geen controles uitgevoerd voor deze tabel al.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-220">There are no validations performed against this table though.</span></span>

### <a name="sqlsink"></a><span data-ttu-id="f3cbe-221">SqlSink</span><span class="sxs-lookup"><span data-stu-id="f3cbe-221">SqlSink</span></span>
<span data-ttu-id="f3cbe-222">**SqlSink** ondersteunt Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="f3cbe-222">**SqlSink** supports hello following properties:</span></span>

| <span data-ttu-id="f3cbe-223">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="f3cbe-223">Property</span></span> | <span data-ttu-id="f3cbe-224">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f3cbe-224">Description</span></span> | <span data-ttu-id="f3cbe-225">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="f3cbe-225">Allowed values</span></span> | <span data-ttu-id="f3cbe-226">Vereist</span><span class="sxs-lookup"><span data-stu-id="f3cbe-226">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="f3cbe-227">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="f3cbe-227">writeBatchTimeout</span></span> |<span data-ttu-id="f3cbe-228">Wachttijd voor Hallo batch insert-bewerking toocomplete voordat een time-out optreedt.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-228">Wait time for hello batch insert operation toocomplete before it times out.</span></span> |<span data-ttu-id="f3cbe-229">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="f3cbe-229">timespan</span></span><br/><br/> <span data-ttu-id="f3cbe-230">Voorbeeld: "00: 30:00 ' (30 minuten).</span><span class="sxs-lookup"><span data-stu-id="f3cbe-230">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="f3cbe-231">Nee</span><span class="sxs-lookup"><span data-stu-id="f3cbe-231">No</span></span> |
| <span data-ttu-id="f3cbe-232">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="f3cbe-232">writeBatchSize</span></span> |<span data-ttu-id="f3cbe-233">Voegt de gegevens in SQL-tabel Hallo wanneer Hallo buffergrootte writeBatchSize bereikt.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-233">Inserts data into hello SQL table when hello buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="f3cbe-234">Geheel getal (aantal rijen)</span><span class="sxs-lookup"><span data-stu-id="f3cbe-234">Integer (number of rows)</span></span> |<span data-ttu-id="f3cbe-235">Nee (standaard: 10000)</span><span class="sxs-lookup"><span data-stu-id="f3cbe-235">No (default: 10000)</span></span> |
| <span data-ttu-id="f3cbe-236">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="f3cbe-236">sqlWriterCleanupScript</span></span> |<span data-ttu-id="f3cbe-237">Query voor de Kopieeractiviteit tooexecute opgeven zodat de gegevens van een bepaald segment wordt opgeschoond.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-237">Specify query for Copy Activity tooexecute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="f3cbe-238">Zie voor meer informatie [herhaalbare kopiëren](#repeatable-copy) sectie.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-238">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="f3cbe-239">Een query-instructie.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-239">A query statement.</span></span> |<span data-ttu-id="f3cbe-240">Nee</span><span class="sxs-lookup"><span data-stu-id="f3cbe-240">No</span></span> |
| <span data-ttu-id="f3cbe-241">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="f3cbe-241">sliceIdentifierColumnName</span></span> |<span data-ttu-id="f3cbe-242">Geef kolomnaam voor Kopieeractiviteit toofill met segment-ID automatisch gegenereerd en die is gebruikt tooclean van gegevens van een bepaald segment wanneer opnieuw uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-242">Specify column name for Copy Activity toofill with auto generated slice identifier, which is used tooclean up data of a specific slice when rerun.</span></span> <span data-ttu-id="f3cbe-243">Zie voor meer informatie [herhaalbare kopiëren](#repeatable-copy) sectie.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-243">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="f3cbe-244">De naam van de kolom van een kolom met gegevenstype binary(32).</span><span class="sxs-lookup"><span data-stu-id="f3cbe-244">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="f3cbe-245">Nee</span><span class="sxs-lookup"><span data-stu-id="f3cbe-245">No</span></span> |
| <span data-ttu-id="f3cbe-246">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="f3cbe-246">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="f3cbe-247">Naam van Hallo opgeslagen procedure die upserts (updates/INSERT) gegevens in de doeltabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-247">Name of hello stored procedure that upserts (updates/inserts) data into hello target table.</span></span> |<span data-ttu-id="f3cbe-248">Naam van Hallo opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-248">Name of hello stored procedure.</span></span> |<span data-ttu-id="f3cbe-249">Nee</span><span class="sxs-lookup"><span data-stu-id="f3cbe-249">No</span></span> |
| <span data-ttu-id="f3cbe-250">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="f3cbe-250">storedProcedureParameters</span></span> |<span data-ttu-id="f3cbe-251">Parameters voor Hallo opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-251">Parameters for hello stored procedure.</span></span> |<span data-ttu-id="f3cbe-252">Naam/waarde-paren.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-252">Name/value pairs.</span></span> <span data-ttu-id="f3cbe-253">Namen en hoofdlettergebruik van parameters moeten overeenkomen met Hallo namen en hoofdlettergebruik van Hallo opgeslagen procedureparameters.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-253">Names and casing of parameters must match hello names and casing of hello stored procedure parameters.</span></span> |<span data-ttu-id="f3cbe-254">Nee</span><span class="sxs-lookup"><span data-stu-id="f3cbe-254">No</span></span> |
| <span data-ttu-id="f3cbe-255">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="f3cbe-255">sqlWriterTableType</span></span> |<span data-ttu-id="f3cbe-256">Geef tabel type naam toobe in Hallo opgeslagen procedure gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-256">Specify table type name toobe used in hello stored procedure.</span></span> <span data-ttu-id="f3cbe-257">Kopieeractiviteit beschikbaar Hallo-gegevens worden verplaatst in een tijdelijke tabel met dit tabeltype.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-257">Copy activity makes hello data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="f3cbe-258">Opgeslagen procedurecode kunt Hallo gegevens wordt gekopieerd met de bestaande gegevens vervolgens samenvoegen.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-258">Stored procedure code can then merge hello data being copied with existing data.</span></span> |<span data-ttu-id="f3cbe-259">Een typenaam van de tabel.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-259">A table type name.</span></span> |<span data-ttu-id="f3cbe-260">Nee</span><span class="sxs-lookup"><span data-stu-id="f3cbe-260">No</span></span> |


## <a name="json-examples-for-copying-data-from-and-toosql-server"></a><span data-ttu-id="f3cbe-261">JSON-voorbeelden voor het kopiëren van gegevens van en tooSQL Server</span><span class="sxs-lookup"><span data-stu-id="f3cbe-261">JSON examples for copying data from and tooSQL Server</span></span>
<span data-ttu-id="f3cbe-262">Hallo volgende voorbeelden geven voorbeeld JSON definities waarmee u een pijplijn toocreate kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="f3cbe-262">hello following examples provide sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="f3cbe-263">Hallo van de volgende voorbeelden tonen hoe toocopy gegevens tooand van SQL Server en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-263">hello following samples show how toocopy data tooand from SQL Server and Azure Blob Storage.</span></span> <span data-ttu-id="f3cbe-264">Echter gegevens kunnen worden gekopieerd **rechtstreeks** uit een van de bronnen tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-264">However, data can be copied **directly** from any of sources tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>     

## <a name="example-copy-data-from-sql-server-tooazure-blob"></a><span data-ttu-id="f3cbe-265">Voorbeeld: Gegevens uit SQL Server-tooAzure Blob kopiëren</span><span class="sxs-lookup"><span data-stu-id="f3cbe-265">Example: Copy data from SQL Server tooAzure Blob</span></span>
<span data-ttu-id="f3cbe-266">Hallo volgende ziet:</span><span class="sxs-lookup"><span data-stu-id="f3cbe-266">hello following sample shows:</span></span>

1. <span data-ttu-id="f3cbe-267">Een gekoppelde service van het type [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f3cbe-267">A linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="f3cbe-268">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f3cbe-268">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="f3cbe-269">Invoer [gegevensset](data-factory-create-datasets.md) van het type [SqlServerTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f3cbe-269">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](#dataset-properties).</span></span>
4. <span data-ttu-id="f3cbe-270">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f3cbe-270">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="f3cbe-271">Hallo [pijplijn](data-factory-create-pipelines.md) met de kopieeractiviteit die gebruikmaakt van [SqlSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="f3cbe-271">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="f3cbe-272">Hallo voorbeeld opgehaald-timeseries-gegevens uit een SQL Server-tabel tooan Azure blob elk uur.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-272">hello sample copies time-series data from a SQL Server table tooan Azure blob every hour.</span></span> <span data-ttu-id="f3cbe-273">Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-273">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="f3cbe-274">Instellen als eerste stap Hallo data management gateway.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-274">As a first step, setup hello data management gateway.</span></span> <span data-ttu-id="f3cbe-275">Hallo-instructies vindt u in Hallo [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-275">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="f3cbe-276">**SQL Server gekoppeld-service**</span><span class="sxs-lookup"><span data-stu-id="f3cbe-276">**SQL Server linked service**</span></span>
```json
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```
<span data-ttu-id="f3cbe-277">**Azure Blob-opslag gekoppelde service**</span><span class="sxs-lookup"><span data-stu-id="f3cbe-277">**Azure Blob storage linked service**</span></span>

```json
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="f3cbe-278">**SQL Server-invoergegevensset**</span><span class="sxs-lookup"><span data-stu-id="f3cbe-278">**SQL Server input dataset**</span></span>

<span data-ttu-id="f3cbe-279">Hallo-voorbeeld wordt ervan uitgegaan dat u hebt een tabel 'MijnTabel' gemaakt in SQL Server en deze bevat een kolom met de naam 'timestampcolumn' voor de reeksgegevens.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-279">hello sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="f3cbe-280">U kunt een query over meerdere tabellen in dezelfde database met behulp van een één gegevensset, maar één tabel moet worden gebruikt voor een van deze dataset Hallo tableName typeProperty Hallo.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-280">You can query over multiple tables within hello same database using a single dataset, but a single table must be used for hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="f3cbe-281">Instelling 'extern': 'true' informeert Data Factory-service die gegevensset Hallo externe toohello data factory is en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-281">Setting “external”: ”true” informs Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
  "name": "SqlServerInput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
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
<span data-ttu-id="f3cbe-282">**Azure Blob-uitvoergegevensset**</span><span class="sxs-lookup"><span data-stu-id="f3cbe-282">**Azure Blob output dataset**</span></span>

<span data-ttu-id="f3cbe-283">Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="f3cbe-283">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="f3cbe-284">pad naar map voor blob Hallo Hallo wordt dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-284">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="f3cbe-285">Hallo mappad jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-285">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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
<span data-ttu-id="f3cbe-286">**Pijplijn met de kopieeractiviteit**</span><span class="sxs-lookup"><span data-stu-id="f3cbe-286">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="f3cbe-287">Hallo pijplijn bevat een Kopieeractiviteit die is geconfigureerd toouse deze invoer- en uitvoergegevenssets en geplande toorun is om het uur.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-287">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="f3cbe-288">Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**SqlSource** en **sink** type is ingesteld, te**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-288">In hello pipeline JSON definition, hello **source** type is set too**SqlSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="f3cbe-289">Hallo SQL-query is opgegeven voor Hallo **SqlReaderQuery** eigenschap Hallo gegevens selecteert in Hallo voorbij toocopy uur.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-289">hello SQL query specified for hello **SqlReaderQuery** property selects hello data in hello past hour toocopy.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2016-06-01T18:00:00",
    "end":"2016-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
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
<span data-ttu-id="f3cbe-290">In dit voorbeeld **sqlReaderQuery** voor Hallo SqlSource is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-290">In this example, **sqlReaderQuery** is specified for hello SqlSource.</span></span> <span data-ttu-id="f3cbe-291">Deze query Hallo Kopieeractiviteit uitgevoerd tegen Hallo tooget SQL Server-Database-Hallo brongegevens.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-291">hello Copy Activity runs this query against hello SQL Server Database source tooget hello data.</span></span> <span data-ttu-id="f3cbe-292">U kunt ook een opgeslagen procedure opgeven door te geven Hallo **sqlReaderStoredProcedureName** en **storedProcedureParameters** (als hello opgeslagen procedure parameters zijn vereist).</span><span class="sxs-lookup"><span data-stu-id="f3cbe-292">Alternatively, you can specify a stored procedure by specifying hello **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if hello stored procedure takes parameters).</span></span> <span data-ttu-id="f3cbe-293">Hallo sqlReaderQuery kunt verwijzen naar meerdere tabellen in Hallo database waarnaar wordt verwezen door Hallo invoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-293">hello sqlReaderQuery can reference multiple tables within hello database referenced by hello input dataset.</span></span> <span data-ttu-id="f3cbe-294">Het is niet beperkt tooonly Hallo tabel van deze dataset tableName typeProperty Hallo ingesteld.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-294">It is not limited tooonly hello table set as hello dataset's tableName typeProperty.</span></span>

<span data-ttu-id="f3cbe-295">Als u geen sqlReaderQuery of sqlReaderStoredProcedureName opgeeft, zijn gedefinieerd in de sectie structuur Hallo Hallo-kolommen gebruikte toobuild een toorun selectiequery tegen Hallo SQL Server-Database.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-295">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, hello columns defined in hello structure section are used toobuild a select query toorun against hello SQL Server Database.</span></span> <span data-ttu-id="f3cbe-296">Als de definitie van de gegevensset Hallo geen Hallo structuur, worden alle kolommen uit Hallo tabel geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-296">If hello dataset definition does not have hello structure, all columns are selected from hello table.</span></span>

<span data-ttu-id="f3cbe-297">Zie Hallo [Sql-bron](#sqlsource) sectie en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) voor Hallo lijst met eigenschappen die ondersteund worden door SqlSource en BlobSink.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-297">See hello [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for hello list of properties supported by SqlSource and BlobSink.</span></span>

## <a name="example-copy-data-from-azure-blob-toosql-server"></a><span data-ttu-id="f3cbe-298">Voorbeeld: Gegevens kopiëren van Azure Blob-tooSQL Server</span><span class="sxs-lookup"><span data-stu-id="f3cbe-298">Example: Copy data from Azure Blob tooSQL Server</span></span>
<span data-ttu-id="f3cbe-299">Hallo volgende ziet:</span><span class="sxs-lookup"><span data-stu-id="f3cbe-299">hello following sample shows:</span></span>

1. <span data-ttu-id="f3cbe-300">Hallo gekoppelde service van het type [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f3cbe-300">hello linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="f3cbe-301">Hallo gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="f3cbe-301">hello linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="f3cbe-302">Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f3cbe-302">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="f3cbe-303">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="f3cbe-303">An output [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="f3cbe-304">Hallo [pijplijn](data-factory-create-pipelines.md) met de kopieeractiviteit die gebruikmaakt van [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) en [SqlSink](#sql-server-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="f3cbe-304">hello [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#sql-server-copy-activity-type-properties).</span></span>

<span data-ttu-id="f3cbe-305">Hallo voorbeeld opgehaald-timeseries-gegevens uit een Azure-blobopslag tooa SQL Server-tabel om het uur.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-305">hello sample copies time-series data from an Azure blob tooa SQL Server table every hour.</span></span> <span data-ttu-id="f3cbe-306">Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-306">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="f3cbe-307">**SQL Server gekoppeld-service**</span><span class="sxs-lookup"><span data-stu-id="f3cbe-307">**SQL Server linked service**</span></span>

```json
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```
<span data-ttu-id="f3cbe-308">**Azure Blob-opslag gekoppelde service**</span><span class="sxs-lookup"><span data-stu-id="f3cbe-308">**Azure Blob storage linked service**</span></span>

```json
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
<span data-ttu-id="f3cbe-309">**Azure Blob-invoergegevensset**</span><span class="sxs-lookup"><span data-stu-id="f3cbe-309">**Azure Blob input dataset**</span></span>

<span data-ttu-id="f3cbe-310">Gegevens wordt opgehaald uit een nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="f3cbe-310">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="f3cbe-311">Hallo map pad en de naam voor de blob Hallo worden dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-311">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="f3cbe-312">Hallo mappad jaar, maand en dag deel uit van de begintijd Hallo en bestandsnaam gebruikt Hallo uur deel uit van de begintijd Hallo.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-312">hello folder path uses year, month, and day part of hello start time and file name uses hello hour part of hello start time.</span></span> <span data-ttu-id="f3cbe-313">"extern": "true" instelling informeert Hallo Data Factory-service die gegevensset Hallo externe toohello data factory is en niet wordt geproduceerd door een activiteit in de gegevensfactory Hallo.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-313">“external”: “true” setting informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
      "fileName": "{Hour}.csv",
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
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
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
<span data-ttu-id="f3cbe-314">**Gegevensset voor SQL Server-uitvoer**</span><span class="sxs-lookup"><span data-stu-id="f3cbe-314">**SQL Server output dataset**</span></span>

<span data-ttu-id="f3cbe-315">Hallo voorbeeld kopieert gegevens tooa tabel "MijnTabel" in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-315">hello sample copies data tooa table named “MyTable” in SQL Server.</span></span> <span data-ttu-id="f3cbe-316">Hallo-tabel maken in SQL-Server met hetzelfde aantal kolommen Hallo zoals Hallo Blob CSV-bestand toocontain verwacht.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-316">Create hello table in SQL Server with hello same number of columns as you expect hello Blob CSV file toocontain.</span></span> <span data-ttu-id="f3cbe-317">Nieuwe rijen worden toohello tabel toegevoegd om het uur.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-317">New rows are added toohello table every hour.</span></span>

```json
{
  "name": "SqlServerOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
<span data-ttu-id="f3cbe-318">**Pijplijn met de kopieeractiviteit**</span><span class="sxs-lookup"><span data-stu-id="f3cbe-318">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="f3cbe-319">Hallo pijplijn bevat een Kopieeractiviteit die is geconfigureerd toouse deze invoer- en uitvoergegevenssets en geplande toorun is om het uur.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-319">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="f3cbe-320">Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**BlobSource** en **sink** type is ingesteld, te**SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-320">In hello pipeline JSON definition, hello **source** type is set too**BlobSource** and **sink** type is set too**SqlSink**.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": " SqlServerOutput "
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlSink"
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

## <a name="troubleshooting-connection-issues"></a><span data-ttu-id="f3cbe-321">Verbindingsproblemen oplossen</span><span class="sxs-lookup"><span data-stu-id="f3cbe-321">Troubleshooting connection issues</span></span>
1. <span data-ttu-id="f3cbe-322">Configureer uw SQL Server tooaccept externe verbindingen.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-322">Configure your SQL Server tooaccept remote connections.</span></span> <span data-ttu-id="f3cbe-323">Start **SQL Server Management Studio**, met de rechtermuisknop op **server**, en klik op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-323">Launch **SQL Server Management Studio**, right-click **server**, and click **Properties**.</span></span> <span data-ttu-id="f3cbe-324">Selecteer **verbindingen** van Hallo lijst en controle **toestaan externe verbindingen toohello server**.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-324">Select **Connections** from hello list and check **Allow remote connections toohello server**.</span></span>

    ![Externe verbindingen inschakelen](./media/data-factory-sqlserver-connector/AllowRemoteConnections.png)

    <span data-ttu-id="f3cbe-326">Zie [Hallo remote access Server Configuration Option configureert](https://msdn.microsoft.com/library/ms191464.aspx) voor gedetailleerde stappen.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-326">See [Configure hello remote access Server Configuration Option](https://msdn.microsoft.com/library/ms191464.aspx) for detailed steps.</span></span>
2. <span data-ttu-id="f3cbe-327">Start **SQL Server Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-327">Launch **SQL Server Configuration Manager**.</span></span> <span data-ttu-id="f3cbe-328">Vouw **SQL Server-netwerkconfiguratie** voor Hallo exemplaar u wilt en selecteer **protocollen voor MSSQLSERVER**.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-328">Expand **SQL Server Network Configuration** for hello instance you want, and select **Protocols for MSSQLSERVER**.</span></span> <span data-ttu-id="f3cbe-329">U ziet protocollen in Hallo rechterdeelvenster.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-329">You should see protocols in hello right-pane.</span></span> <span data-ttu-id="f3cbe-330">TCP/IP inschakelen met de rechtermuisknop op **TCP/IP** en te klikken op **inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-330">Enable TCP/IP by right-clicking **TCP/IP** and clicking **Enable**.</span></span>

    ![TCP/IP inschakelen](./media/data-factory-sqlserver-connector/EnableTCPProptocol.png)

    <span data-ttu-id="f3cbe-332">Zie [in- of uitschakelen van een Server netwerkprotocol](https://msdn.microsoft.com/library/ms191294.aspx) voor meer informatie en alternatieve manieren TCP/IP-protocol in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-332">See [Enable or Disable a Server Network Protocol](https://msdn.microsoft.com/library/ms191294.aspx) for details and alternate ways of enabling TCP/IP protocol.</span></span>
3. <span data-ttu-id="f3cbe-333">In hetzelfde venster Hallo, dubbelklikt u op **TCP/IP** toolaunch **TCP/IP-eigenschappen** venster.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-333">In hello same window, double-click **TCP/IP** toolaunch **TCP/IP Properties** window.</span></span>
4. <span data-ttu-id="f3cbe-334">Overschakelen van toohello **IP-adressen** tabblad. Schuif omlaag toosee **IPAll** sectie.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-334">Switch toohello **IP Addresses** tab. Scroll down toosee **IPAll** section.</span></span> <span data-ttu-id="f3cbe-335">Noteer Hallo ** TCP-poort ** (standaardwaarde is **1433**).</span><span class="sxs-lookup"><span data-stu-id="f3cbe-335">Note down hello **TCP Port **(default is **1433**).</span></span>
5. <span data-ttu-id="f3cbe-336">Maak een **regel voor Windows Firewall Hallo** op Hallo machine tooallow binnenkomend verkeer via deze poort.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-336">Create a **rule for hello Windows Firewall** on hello machine tooallow incoming traffic through this port.</span></span>  
6. <span data-ttu-id="f3cbe-337">**Verbinding controleren**: tooconnect toohello SQL Server met behulp van volledig gekwalificeerde naam SQL Server Management Studio gebruiken vanaf een andere computer.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-337">**Verify connection**: tooconnect toohello SQL Server using fully qualified name, use SQL Server Management Studio from a different machine.</span></span> <span data-ttu-id="f3cbe-338">Bijvoorbeeld: '<machine>.<domain>. Corp.<company>.com, 1433. "</span><span class="sxs-lookup"><span data-stu-id="f3cbe-338">For example: "<machine>.<domain>.corp.<company>.com,1433."</span></span>

   > [!IMPORTANT]

   > <span data-ttu-id="f3cbe-339">Zie [gegevens verplaatsen tussen lokale bronnen en Hallo cloud met Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) voor gedetailleerde informatie.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-339">See [Move data between on-premises sources and hello cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for detailed information.</span></span>
   >
   > <span data-ttu-id="f3cbe-340">Zie [gateway problemen](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) voor tips over het oplossen van verbinding of gateway gerelateerde problemen.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-340">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>
   >
   >


## <a name="identity-columns-in-hello-target-database"></a><span data-ttu-id="f3cbe-341">Id-kolommen in de doeldatabase Hallo</span><span class="sxs-lookup"><span data-stu-id="f3cbe-341">Identity columns in hello target database</span></span>
<span data-ttu-id="f3cbe-342">Deze sectie bevat een voorbeeld waarin gegevens worden gekopieerd van een brontabel met geen doeltabel identiteit kolom tooa met een identiteitskolom.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-342">This section provides an example that copies data from a source table with no identity column tooa destination table with an identity column.</span></span>

<span data-ttu-id="f3cbe-343">**Brontabel:**</span><span class="sxs-lookup"><span data-stu-id="f3cbe-343">**Source table:**</span></span>

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="f3cbe-344">**Doeltabel:**</span><span class="sxs-lookup"><span data-stu-id="f3cbe-344">**Destination table:**</span></span>

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

<span data-ttu-id="f3cbe-345">U ziet dat doeltabel Hallo heeft een identiteitskolom.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-345">Notice that hello target table has an identity column.</span></span>

<span data-ttu-id="f3cbe-346">**Bron gegevensset JSON-definitie**</span><span class="sxs-lookup"><span data-stu-id="f3cbe-346">**Source dataset JSON definition**</span></span>

```json
{
    "name": "SampleSource",
    "properties": {
        "published": false,
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
<span data-ttu-id="f3cbe-347">**Doel-dataset JSON-definitie**</span><span class="sxs-lookup"><span data-stu-id="f3cbe-347">**Destination dataset JSON definition**</span></span>

```json
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "published": false,
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }
}
```

<span data-ttu-id="f3cbe-348">Merk op dat als de bron en doel-tabel verschillende schema's zijn (doel heeft een extra kolom met de identiteit).</span><span class="sxs-lookup"><span data-stu-id="f3cbe-348">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="f3cbe-349">In dit scenario moet u toospecify **structuur** eigenschap in Hallo doel gegevenssetdefinitie, waaronder Hallo identiteitskolom niet.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-349">In this scenario, you need toospecify **structure** property in hello target dataset definition, which doesn’t include hello identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="f3cbe-350">Aanroepen van opgeslagen procedure uit SQL-sink</span><span class="sxs-lookup"><span data-stu-id="f3cbe-350">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="f3cbe-351">Zie [opgeslagen procedure voor SQL-sink aanroepen in de kopieerbewerking](data-factory-invoke-stored-procedure-from-copy-activity.md) artikel voor een voorbeeld van een opgeslagen procedure van SQL-sink in een kopieeractiviteit van een pijplijn wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-351">See [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article for an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline.</span></span>

## <a name="type-mapping-for-sql-server"></a><span data-ttu-id="f3cbe-352">Toewijzing van het type voor SQL server</span><span class="sxs-lookup"><span data-stu-id="f3cbe-352">Type mapping for SQL server</span></span>
<span data-ttu-id="f3cbe-353">Zoals vermeld in Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel Hallo kopieeractiviteit voert automatische typeconversies van brontypen typen toosink Hello 2 stap benadering te volgen:</span><span class="sxs-lookup"><span data-stu-id="f3cbe-353">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, hello Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="f3cbe-354">Systeemeigen bron typen too.NET type converteren</span><span class="sxs-lookup"><span data-stu-id="f3cbe-354">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="f3cbe-355">Converteren van .NET-type toonative sink-type</span><span class="sxs-lookup"><span data-stu-id="f3cbe-355">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="f3cbe-356">Als zwevend gegevens te & van SQL server, Hallo gebruikt volgende toewijzingen van de SQL-type too.NET type en vice versa.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-356">When moving data too& from SQL server, hello following mappings are used from SQL type too.NET type and vice versa.</span></span>

<span data-ttu-id="f3cbe-357">Hallo-toewijzing is hetzelfde als SQL Server gegevenstypetoewijzing voor ADO.NET Hallo.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-357">hello mapping is same as hello SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="f3cbe-358">SQL Server Database Engine-type</span><span class="sxs-lookup"><span data-stu-id="f3cbe-358">SQL Server Database Engine type</span></span> | <span data-ttu-id="f3cbe-359">.NET framework-type</span><span class="sxs-lookup"><span data-stu-id="f3cbe-359">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="f3cbe-360">bigint</span><span class="sxs-lookup"><span data-stu-id="f3cbe-360">bigint</span></span> |<span data-ttu-id="f3cbe-361">Int64</span><span class="sxs-lookup"><span data-stu-id="f3cbe-361">Int64</span></span> |
| <span data-ttu-id="f3cbe-362">Binaire</span><span class="sxs-lookup"><span data-stu-id="f3cbe-362">binary</span></span> |<span data-ttu-id="f3cbe-363">Byte]</span><span class="sxs-lookup"><span data-stu-id="f3cbe-363">Byte[]</span></span> |
| <span data-ttu-id="f3cbe-364">bits</span><span class="sxs-lookup"><span data-stu-id="f3cbe-364">bit</span></span> |<span data-ttu-id="f3cbe-365">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="f3cbe-365">Boolean</span></span> |
| <span data-ttu-id="f3cbe-366">CHAR</span><span class="sxs-lookup"><span data-stu-id="f3cbe-366">char</span></span> |<span data-ttu-id="f3cbe-367">Tekenreeks, Char]</span><span class="sxs-lookup"><span data-stu-id="f3cbe-367">String, Char[]</span></span> |
| <span data-ttu-id="f3cbe-368">Datum</span><span class="sxs-lookup"><span data-stu-id="f3cbe-368">date</span></span> |<span data-ttu-id="f3cbe-369">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="f3cbe-369">DateTime</span></span> |
| <span data-ttu-id="f3cbe-370">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="f3cbe-370">Datetime</span></span> |<span data-ttu-id="f3cbe-371">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="f3cbe-371">DateTime</span></span> |
| <span data-ttu-id="f3cbe-372">datetime2</span><span class="sxs-lookup"><span data-stu-id="f3cbe-372">datetime2</span></span> |<span data-ttu-id="f3cbe-373">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="f3cbe-373">DateTime</span></span> |
| <span data-ttu-id="f3cbe-374">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="f3cbe-374">Datetimeoffset</span></span> |<span data-ttu-id="f3cbe-375">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="f3cbe-375">DateTimeOffset</span></span> |
| <span data-ttu-id="f3cbe-376">Decimale</span><span class="sxs-lookup"><span data-stu-id="f3cbe-376">Decimal</span></span> |<span data-ttu-id="f3cbe-377">Decimale</span><span class="sxs-lookup"><span data-stu-id="f3cbe-377">Decimal</span></span> |
| <span data-ttu-id="f3cbe-378">FILESTREAM-kenmerk (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="f3cbe-378">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="f3cbe-379">Byte]</span><span class="sxs-lookup"><span data-stu-id="f3cbe-379">Byte[]</span></span> |
| <span data-ttu-id="f3cbe-380">Float</span><span class="sxs-lookup"><span data-stu-id="f3cbe-380">Float</span></span> |<span data-ttu-id="f3cbe-381">dubbele</span><span class="sxs-lookup"><span data-stu-id="f3cbe-381">Double</span></span> |
| <span data-ttu-id="f3cbe-382">Afbeelding</span><span class="sxs-lookup"><span data-stu-id="f3cbe-382">image</span></span> |<span data-ttu-id="f3cbe-383">Byte]</span><span class="sxs-lookup"><span data-stu-id="f3cbe-383">Byte[]</span></span> |
| <span data-ttu-id="f3cbe-384">int</span><span class="sxs-lookup"><span data-stu-id="f3cbe-384">int</span></span> |<span data-ttu-id="f3cbe-385">Int32</span><span class="sxs-lookup"><span data-stu-id="f3cbe-385">Int32</span></span> |
| <span data-ttu-id="f3cbe-386">Money</span><span class="sxs-lookup"><span data-stu-id="f3cbe-386">money</span></span> |<span data-ttu-id="f3cbe-387">Decimale</span><span class="sxs-lookup"><span data-stu-id="f3cbe-387">Decimal</span></span> |
| <span data-ttu-id="f3cbe-388">nchar</span><span class="sxs-lookup"><span data-stu-id="f3cbe-388">nchar</span></span> |<span data-ttu-id="f3cbe-389">Tekenreeks, Char]</span><span class="sxs-lookup"><span data-stu-id="f3cbe-389">String, Char[]</span></span> |
| <span data-ttu-id="f3cbe-390">ntext</span><span class="sxs-lookup"><span data-stu-id="f3cbe-390">ntext</span></span> |<span data-ttu-id="f3cbe-391">Tekenreeks, Char]</span><span class="sxs-lookup"><span data-stu-id="f3cbe-391">String, Char[]</span></span> |
| <span data-ttu-id="f3cbe-392">numerieke</span><span class="sxs-lookup"><span data-stu-id="f3cbe-392">numeric</span></span> |<span data-ttu-id="f3cbe-393">Decimale</span><span class="sxs-lookup"><span data-stu-id="f3cbe-393">Decimal</span></span> |
| <span data-ttu-id="f3cbe-394">nvarchar</span><span class="sxs-lookup"><span data-stu-id="f3cbe-394">nvarchar</span></span> |<span data-ttu-id="f3cbe-395">Tekenreeks, Char]</span><span class="sxs-lookup"><span data-stu-id="f3cbe-395">String, Char[]</span></span> |
| <span data-ttu-id="f3cbe-396">echte</span><span class="sxs-lookup"><span data-stu-id="f3cbe-396">real</span></span> |<span data-ttu-id="f3cbe-397">Één</span><span class="sxs-lookup"><span data-stu-id="f3cbe-397">Single</span></span> |
| <span data-ttu-id="f3cbe-398">ROWVERSION</span><span class="sxs-lookup"><span data-stu-id="f3cbe-398">rowversion</span></span> |<span data-ttu-id="f3cbe-399">Byte]</span><span class="sxs-lookup"><span data-stu-id="f3cbe-399">Byte[]</span></span> |
| <span data-ttu-id="f3cbe-400">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="f3cbe-400">smalldatetime</span></span> |<span data-ttu-id="f3cbe-401">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="f3cbe-401">DateTime</span></span> |
| <span data-ttu-id="f3cbe-402">smallint</span><span class="sxs-lookup"><span data-stu-id="f3cbe-402">smallint</span></span> |<span data-ttu-id="f3cbe-403">Int16</span><span class="sxs-lookup"><span data-stu-id="f3cbe-403">Int16</span></span> |
| <span data-ttu-id="f3cbe-404">smallmoney</span><span class="sxs-lookup"><span data-stu-id="f3cbe-404">smallmoney</span></span> |<span data-ttu-id="f3cbe-405">Decimale</span><span class="sxs-lookup"><span data-stu-id="f3cbe-405">Decimal</span></span> |
| <span data-ttu-id="f3cbe-406">sql_variant</span><span class="sxs-lookup"><span data-stu-id="f3cbe-406">sql_variant</span></span> |<span data-ttu-id="f3cbe-407">Object *</span><span class="sxs-lookup"><span data-stu-id="f3cbe-407">Object *</span></span> |
| <span data-ttu-id="f3cbe-408">Tekst</span><span class="sxs-lookup"><span data-stu-id="f3cbe-408">text</span></span> |<span data-ttu-id="f3cbe-409">Tekenreeks, Char]</span><span class="sxs-lookup"><span data-stu-id="f3cbe-409">String, Char[]</span></span> |
| <span data-ttu-id="f3cbe-410">tijd</span><span class="sxs-lookup"><span data-stu-id="f3cbe-410">time</span></span> |<span data-ttu-id="f3cbe-411">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="f3cbe-411">TimeSpan</span></span> |
| <span data-ttu-id="f3cbe-412">tijdstempel</span><span class="sxs-lookup"><span data-stu-id="f3cbe-412">timestamp</span></span> |<span data-ttu-id="f3cbe-413">Byte]</span><span class="sxs-lookup"><span data-stu-id="f3cbe-413">Byte[]</span></span> |
| <span data-ttu-id="f3cbe-414">tinyint</span><span class="sxs-lookup"><span data-stu-id="f3cbe-414">tinyint</span></span> |<span data-ttu-id="f3cbe-415">Byte</span><span class="sxs-lookup"><span data-stu-id="f3cbe-415">Byte</span></span> |
| <span data-ttu-id="f3cbe-416">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="f3cbe-416">uniqueidentifier</span></span> |<span data-ttu-id="f3cbe-417">GUID</span><span class="sxs-lookup"><span data-stu-id="f3cbe-417">Guid</span></span> |
| <span data-ttu-id="f3cbe-418">varbinary</span><span class="sxs-lookup"><span data-stu-id="f3cbe-418">varbinary</span></span> |<span data-ttu-id="f3cbe-419">Byte]</span><span class="sxs-lookup"><span data-stu-id="f3cbe-419">Byte[]</span></span> |
| <span data-ttu-id="f3cbe-420">varchar</span><span class="sxs-lookup"><span data-stu-id="f3cbe-420">varchar</span></span> |<span data-ttu-id="f3cbe-421">Tekenreeks, Char]</span><span class="sxs-lookup"><span data-stu-id="f3cbe-421">String, Char[]</span></span> |
| <span data-ttu-id="f3cbe-422">xml</span><span class="sxs-lookup"><span data-stu-id="f3cbe-422">xml</span></span> |<span data-ttu-id="f3cbe-423">XML</span><span class="sxs-lookup"><span data-stu-id="f3cbe-423">Xml</span></span> |

## <a name="mapping-source-toosink-columns"></a><span data-ttu-id="f3cbe-424">Toewijzing toosink bronkolommen</span><span class="sxs-lookup"><span data-stu-id="f3cbe-424">Mapping source toosink columns</span></span>
<span data-ttu-id="f3cbe-425">toomap kolommen uit de bron gegevensset toocolumns uit sink gegevensset, Zie [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="f3cbe-425">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="f3cbe-426">Herhaalbare kopiëren</span><span class="sxs-lookup"><span data-stu-id="f3cbe-426">Repeatable copy</span></span>
<span data-ttu-id="f3cbe-427">Bij het kopiëren van gegevens tooSQL Server-Database, voegt Hallo kopieeractiviteit gegevenstabel toohello sink standaard.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-427">When copying data tooSQL Server Database, hello copy activity appends data toohello sink table by default.</span></span> <span data-ttu-id="f3cbe-428">een UPSERT tooperform in plaats daarvan Zie [herhaalbare schrijven tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) artikel.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-428">tooperform an UPSERT instead,  See [Repeatable write tooSqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="f3cbe-429">Houd bij het kopiëren van gegevens uit een relationele gegevensopslag, herhaalbaarheid rekening tooavoid ongewenste resultaten.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-429">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="f3cbe-430">In Azure Data Factory, kunt u een segment handmatig opnieuw.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-430">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="f3cbe-431">U kunt ook een beleid voor opnieuw proberen voor een gegevensset configureren zodat een segment wordt opnieuw uitgevoerd wanneer een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-431">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="f3cbe-432">Wanneer een segment opnieuw in beide gevallen wordt uitgevoerd, moet u ervoor dat dezelfde gegevens Hallo toomake wordt gelezen ongeacht hoe vaak een segment wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-432">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="f3cbe-433">Zie [Repeatable van relationele bronnen lezen](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="f3cbe-433">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="f3cbe-434">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="f3cbe-434">Performance and Tuning</span></span>
<span data-ttu-id="f3cbe-435">Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.</span><span class="sxs-lookup"><span data-stu-id="f3cbe-435">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
