---
title: gegevens uit gegevensarchieven ODBC aaaMove | Microsoft Docs
description: Meer informatie over hoe toomove gegevens van ODBC-gegevens worden opgeslagen met behulp van Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: ad70a598-c031-4339-a883-c6125403cb76
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: jingwang
ms.openlocfilehash: bf96e71da449313b6144bb194205c572d2ca2030
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-odbc-data-stores-using-azure-data-factory"></a><span data-ttu-id="ed72d-103">Verplaatsen van gegevens van ODBC-gegevensarchieven met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="ed72d-103">Move data From ODBC data stores using Azure Data Factory</span></span>
<span data-ttu-id="ed72d-104">Dit artikel wordt uitgelegd hoe toouse hello Kopieeractiviteit in Azure Data Factory toomove gegevens uit een on-premises ODBC gegevens opslaan.</span><span class="sxs-lookup"><span data-stu-id="ed72d-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an on-premises ODBC data store.</span></span> <span data-ttu-id="ed72d-105">Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.</span><span class="sxs-lookup"><span data-stu-id="ed72d-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="ed72d-106">U kunt gegevens kopiëren van een ODBC data store tooany ondersteund sink-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="ed72d-106">You can copy data from an ODBC data store tooany supported sink data store.</span></span> <span data-ttu-id="ed72d-107">Zie voor een lijst van gegevens winkels ondersteund zoals sinks door kopieeractiviteit hello, Hallo [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel.</span><span class="sxs-lookup"><span data-stu-id="ed72d-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="ed72d-108">Data factory ondersteunt momenteel alleen verplaatsen van gegevens van een ODBC-gegevensbron tooother gegevensarchieven opslaan, maar niet voor het verplaatsen van gegevens uit andere gegevens winkels tooan ODBC data store.</span><span class="sxs-lookup"><span data-stu-id="ed72d-108">Data factory currently supports only moving data from an ODBC data store tooother data stores, but not for moving data from other data stores tooan ODBC data store.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="ed72d-109">Connectiviteit inschakelen</span><span class="sxs-lookup"><span data-stu-id="ed72d-109">Enabling connectivity</span></span>
<span data-ttu-id="ed72d-110">Data Factory-service ondersteunt verbindende tooon lokale ODBC-bronnen met behulp van Hallo Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="ed72d-110">Data Factory service supports connecting tooon-premises ODBC sources using hello Data Management Gateway.</span></span> <span data-ttu-id="ed72d-111">Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn artikel over Data Management Gateway en stapsgewijze instructies over het instellen van Hallo-gateway.</span><span class="sxs-lookup"><span data-stu-id="ed72d-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article toolearn about Data Management Gateway and step-by-step instructions on setting up hello gateway.</span></span> <span data-ttu-id="ed72d-112">Hallo gateway tooconnect tooan-ODBC-gegevensarchief gebruiken, zelfs als deze is opgenomen in een Azure IaaS VM.</span><span class="sxs-lookup"><span data-stu-id="ed72d-112">Use hello gateway tooconnect tooan ODBC data store even if it is hosted in an Azure IaaS VM.</span></span>

<span data-ttu-id="ed72d-113">U kunt Hallo gateway installeren op Hallo dezelfde on-premises machine of virtuele machine van Azure als gegevensopslag voor ODBC-Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="ed72d-113">You can install hello gateway on hello same on-premises machine or hello Azure VM as hello ODBC data store.</span></span> <span data-ttu-id="ed72d-114">We raden u echter aan dat u Hallo-gateway op een afzonderlijke computer/Azure IaaS VM installeert tooavoid bronconflicten en voor betere prestaties.</span><span class="sxs-lookup"><span data-stu-id="ed72d-114">However, we recommend that you install hello gateway on a separate machine/Azure IaaS VM tooavoid resource contention and for better performance.</span></span> <span data-ttu-id="ed72d-115">Wanneer u Hallo-gateway op een afzonderlijke computer installeert, is het Hallo-machine moeten kunnen tooaccess Hallo machine met Hallo ODBC data store.</span><span class="sxs-lookup"><span data-stu-id="ed72d-115">When you install hello gateway on a separate machine, hello machine should be able tooaccess hello machine with hello ODBC data store.</span></span>

<span data-ttu-id="ed72d-116">Naast Hallo Data Management Gateway moet u ook tooinstall Hallo ODBC-stuurprogramma voor de gegevensopslag Hallo op Hallo gateway-apparaat.</span><span class="sxs-lookup"><span data-stu-id="ed72d-116">Apart from hello Data Management Gateway, you also need tooinstall hello ODBC driver for hello data store on hello gateway machine.</span></span>

> [!NOTE]
> <span data-ttu-id="ed72d-117">Zie [gateway problemen](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) voor tips over het oplossen van verbinding of gateway gerelateerde problemen.</span><span class="sxs-lookup"><span data-stu-id="ed72d-117">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="ed72d-118">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="ed72d-118">Getting started</span></span>
<span data-ttu-id="ed72d-119">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens uit een ODBC data store verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="ed72d-119">You can create a pipeline with a copy activity that moves data from an ODBC data store by using different tools/APIs.</span></span>

<span data-ttu-id="ed72d-120">Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="ed72d-120">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="ed72d-121">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="ed72d-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="ed72d-122">U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="ed72d-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="ed72d-123">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="ed72d-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="ed72d-124">Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="ed72d-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="ed72d-125">Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="ed72d-125">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="ed72d-126">Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="ed72d-126">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="ed72d-127">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="ed72d-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="ed72d-128">Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ed72d-128">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="ed72d-129">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="ed72d-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="ed72d-130">Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens uit een ODBC data store zijn [JSON-voorbeeld: gegevens kopiëren van ODBC-gegevens opslaan tooAzure Blob](#json-example-copy-data-from-odbc-data-store-to-azure-blob) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="ed72d-130">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an ODBC data store, see [JSON example: Copy data from ODBC data store tooAzure Blob](#json-example-copy-data-from-odbc-data-store-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="ed72d-131">Hallo volgende secties bieden informatie over de JSON-eigenschappen die specifiek tooODBC gegevensopslag voor gebruikte toodefine Data Factory-entiteiten zijn:</span><span class="sxs-lookup"><span data-stu-id="ed72d-131">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooODBC data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="ed72d-132">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="ed72d-132">Linked service properties</span></span>
<span data-ttu-id="ed72d-133">Hallo volgende tabel biedt een beschrijving voor de JSON-elementen specifieke tooODBC gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="ed72d-133">hello following table provides description for JSON elements specific tooODBC linked service.</span></span>

| <span data-ttu-id="ed72d-134">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="ed72d-134">Property</span></span> | <span data-ttu-id="ed72d-135">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ed72d-135">Description</span></span> | <span data-ttu-id="ed72d-136">Vereist</span><span class="sxs-lookup"><span data-stu-id="ed72d-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed72d-137">type</span><span class="sxs-lookup"><span data-stu-id="ed72d-137">type</span></span> |<span data-ttu-id="ed72d-138">Hallo type eigenschap moet worden ingesteld op: **OnPremisesOdbc**</span><span class="sxs-lookup"><span data-stu-id="ed72d-138">hello type property must be set to: **OnPremisesOdbc**</span></span> |<span data-ttu-id="ed72d-139">Ja</span><span class="sxs-lookup"><span data-stu-id="ed72d-139">Yes</span></span> |
| <span data-ttu-id="ed72d-140">connectionString</span><span class="sxs-lookup"><span data-stu-id="ed72d-140">connectionString</span></span> |<span data-ttu-id="ed72d-141">Hallo niet access credential gedeelte van het Hallo-verbindingsreeks en een optionele versleuteld referentie.</span><span class="sxs-lookup"><span data-stu-id="ed72d-141">hello non-access credential portion of hello connection string and an optional encrypted credential.</span></span> <span data-ttu-id="ed72d-142">Zie de voorbeelden in Hallo uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="ed72d-142">See examples in hello following sections.</span></span> |<span data-ttu-id="ed72d-143">Ja</span><span class="sxs-lookup"><span data-stu-id="ed72d-143">Yes</span></span> |
| <span data-ttu-id="ed72d-144">referentie</span><span class="sxs-lookup"><span data-stu-id="ed72d-144">credential</span></span> |<span data-ttu-id="ed72d-145">Hallo toegang referentie gedeelte van het Hallo-verbindingsreeks die is opgegeven in de indeling van de eigenschapswaarde specifieke stuurprogramma's.</span><span class="sxs-lookup"><span data-stu-id="ed72d-145">hello access credential portion of hello connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="ed72d-146">Voorbeeld: "Uid =<user ID>; Pwd =<password>; RefreshToken =<secret refresh token>; '.</span><span class="sxs-lookup"><span data-stu-id="ed72d-146">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="ed72d-147">Nee</span><span class="sxs-lookup"><span data-stu-id="ed72d-147">No</span></span> |
| <span data-ttu-id="ed72d-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="ed72d-148">authenticationType</span></span> |<span data-ttu-id="ed72d-149">Type verificatie gebruikt tooconnect toohello ODBC-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="ed72d-149">Type of authentication used tooconnect toohello ODBC data store.</span></span> <span data-ttu-id="ed72d-150">Mogelijke waarden zijn: anonieme en Basic.</span><span class="sxs-lookup"><span data-stu-id="ed72d-150">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="ed72d-151">Ja</span><span class="sxs-lookup"><span data-stu-id="ed72d-151">Yes</span></span> |
| <span data-ttu-id="ed72d-152">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="ed72d-152">username</span></span> |<span data-ttu-id="ed72d-153">Geef de gebruikersnaam als u basisverificatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ed72d-153">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="ed72d-154">Nee</span><span class="sxs-lookup"><span data-stu-id="ed72d-154">No</span></span> |
| <span data-ttu-id="ed72d-155">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="ed72d-155">password</span></span> |<span data-ttu-id="ed72d-156">Wachtwoord voor gebruikersaccount Hallo die u hebt opgegeven voor Hallo gebruikersnaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="ed72d-156">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="ed72d-157">Nee</span><span class="sxs-lookup"><span data-stu-id="ed72d-157">No</span></span> |
| <span data-ttu-id="ed72d-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="ed72d-158">gatewayName</span></span> |<span data-ttu-id="ed72d-159">Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello ODBC-gegevensarchief gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ed72d-159">Name of hello gateway that hello Data Factory service should use tooconnect toohello ODBC data store.</span></span> |<span data-ttu-id="ed72d-160">Ja</span><span class="sxs-lookup"><span data-stu-id="ed72d-160">Yes</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="ed72d-161">Met behulp van basisverificatie</span><span class="sxs-lookup"><span data-stu-id="ed72d-161">Using Basic authentication</span></span>

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```
### <a name="using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="ed72d-162">Met behulp van basisverificatie met versleutelde referenties</span><span class="sxs-lookup"><span data-stu-id="ed72d-162">Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="ed72d-163">U kunt versleutelen Hallo-referenties met een Hallo [nieuw AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) cmdlet (versie 1.0 van Azure PowerShell) of [nieuw AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0,9 of een eerdere versie van Hallo Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="ed72d-163">You can encrypt hello credentials using hello [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of hello Azure PowerShell).</span></span>  

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=myserver.database.windows.net; Database=TestDatabase;;EncryptedCredential=eyJDb25uZWN0...........................",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a><span data-ttu-id="ed72d-164">Anonieme verificatie</span><span class="sxs-lookup"><span data-stu-id="ed72d-164">Using Anonymous authentication</span></span>

```json
{
    "name": "odbc",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "connectionString": "Driver={SQL Server};Server={servername}.database.windows.net; Database=TestDatabase;",
            "credential": "UID={uid};PWD={pwd}",
            "gatewayName": "mygateway"
        }
    }
}
```


## <a name="dataset-properties"></a><span data-ttu-id="ed72d-165">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="ed72d-165">Dataset properties</span></span>
<span data-ttu-id="ed72d-166">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="ed72d-166">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="ed72d-167">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).</span><span class="sxs-lookup"><span data-stu-id="ed72d-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="ed72d-168">Hallo **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="ed72d-168">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="ed72d-169">Hallo typeProperties sectie voor de gegevensset van het type **RelationalTable** (waaronder ODBC gegevensset) heeft Hallo volgende eigenschappen</span><span class="sxs-lookup"><span data-stu-id="ed72d-169">hello typeProperties section for dataset of type **RelationalTable** (which includes ODBC dataset) has hello following properties</span></span>

| <span data-ttu-id="ed72d-170">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="ed72d-170">Property</span></span> | <span data-ttu-id="ed72d-171">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ed72d-171">Description</span></span> | <span data-ttu-id="ed72d-172">Vereist</span><span class="sxs-lookup"><span data-stu-id="ed72d-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ed72d-173">tableName</span><span class="sxs-lookup"><span data-stu-id="ed72d-173">tableName</span></span> |<span data-ttu-id="ed72d-174">Naam van de tabel Hallo in Hallo ODBC-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="ed72d-174">Name of hello table in hello ODBC data store.</span></span> |<span data-ttu-id="ed72d-175">Ja</span><span class="sxs-lookup"><span data-stu-id="ed72d-175">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="ed72d-176">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="ed72d-176">Copy activity properties</span></span>
<span data-ttu-id="ed72d-177">Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="ed72d-177">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="ed72d-178">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en beleidsregels zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="ed72d-178">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="ed72d-179">Eigenschappen die beschikbaar zijn in Hallo **typeProperties** sectie Hallo-activiteit op Hallo daarentegen variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="ed72d-179">Properties available in hello **typeProperties** section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="ed72d-180">Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="ed72d-180">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="ed72d-181">In de kopieeractiviteit, wanneer de bron van het type **RelationalSource** (waaronder ODBC), Hallo volgende eigenschappen beschikbaar zijn in de sectie typeProperties:</span><span class="sxs-lookup"><span data-stu-id="ed72d-181">In copy activity, when source is of type **RelationalSource** (which includes ODBC), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="ed72d-182">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="ed72d-182">Property</span></span> | <span data-ttu-id="ed72d-183">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ed72d-183">Description</span></span> | <span data-ttu-id="ed72d-184">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="ed72d-184">Allowed values</span></span> | <span data-ttu-id="ed72d-185">Vereist</span><span class="sxs-lookup"><span data-stu-id="ed72d-185">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="ed72d-186">query</span><span class="sxs-lookup"><span data-stu-id="ed72d-186">query</span></span> |<span data-ttu-id="ed72d-187">Hallo aangepaste query tooread gegevens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ed72d-187">Use hello custom query tooread data.</span></span> |<span data-ttu-id="ed72d-188">SQL-query-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="ed72d-188">SQL query string.</span></span> <span data-ttu-id="ed72d-189">Bijvoorbeeld: Selecteer * from MijnTabel.</span><span class="sxs-lookup"><span data-stu-id="ed72d-189">For example: select * from MyTable.</span></span> |<span data-ttu-id="ed72d-190">Ja</span><span class="sxs-lookup"><span data-stu-id="ed72d-190">Yes</span></span> |


## <a name="json-example-copy-data-from-odbc-data-store-tooazure-blob"></a><span data-ttu-id="ed72d-191">JSON-voorbeeld: gegevens kopiëren van gegevens van ODBC-tooAzure Blob opslaan</span><span class="sxs-lookup"><span data-stu-id="ed72d-191">JSON example: Copy data from ODBC data store tooAzure Blob</span></span>
<span data-ttu-id="ed72d-192">In dit voorbeeld bevat definities van de JSON die u een pijplijn toocreate gebruiken met behulp van kunt [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="ed72d-192">This example provides JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="ed72d-193">Er wordt weergegeven hoe toocopy van een ODBC-gegevensbron tooan Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="ed72d-193">It shows how toocopy data from an ODBC source tooan Azure Blob Storage.</span></span> <span data-ttu-id="ed72d-194">Gegevens kunnen echter wel gekopieerde tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="ed72d-194">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="ed72d-195">Hallo voorbeeld heeft Hallo data factory-entiteiten te volgen:</span><span class="sxs-lookup"><span data-stu-id="ed72d-195">hello sample has hello following data factory entities:</span></span>

1. <span data-ttu-id="ed72d-196">Een gekoppelde service van het type [OnPremisesOdbc](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ed72d-196">A linked service of type [OnPremisesOdbc](#linked-service-properties).</span></span>
2. <span data-ttu-id="ed72d-197">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="ed72d-197">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="ed72d-198">Invoer [gegevensset](data-factory-create-datasets.md) van het type [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ed72d-198">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="ed72d-199">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="ed72d-199">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="ed72d-200">Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [RelationalSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="ed72d-200">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="ed72d-201">Hallo voorbeeld kopieert gegevens van de resultaten van een query in een ODBC data store tooa blob elk uur.</span><span class="sxs-lookup"><span data-stu-id="ed72d-201">hello sample copies data from a query result in an ODBC data store tooa blob every hour.</span></span> <span data-ttu-id="ed72d-202">Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="ed72d-202">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="ed72d-203">Instellen als eerste stap Hallo data management gateway.</span><span class="sxs-lookup"><span data-stu-id="ed72d-203">As a first step, set up hello data management gateway.</span></span> <span data-ttu-id="ed72d-204">Hallo-instructies vindt u in Hallo [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="ed72d-204">hello instructions are in hello [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="ed72d-205">**ODBC gekoppelde service** in dit voorbeeld gebruikt Hallo basisverificatie.</span><span class="sxs-lookup"><span data-stu-id="ed72d-205">**ODBC linked service** This example uses hello Basic authentication.</span></span> <span data-ttu-id="ed72d-206">Zie [ODBC gekoppelde service](#linked-service-properties) sectie voor verschillende soorten verificatie die u kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ed72d-206">See [ODBC linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "OnPremOdbcLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "authenticationType": "Basic",
            "connectionString": "Driver={SQL Server};Server=Server.database.windows.net; Database=TestDatabase;",
            "userName": "username",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

<span data-ttu-id="ed72d-207">**Een gekoppelde Azure Storage-service**</span><span class="sxs-lookup"><span data-stu-id="ed72d-207">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="ed72d-208">**ODBC-invoergegevensset**</span><span class="sxs-lookup"><span data-stu-id="ed72d-208">**ODBC input dataset**</span></span>

<span data-ttu-id="ed72d-209">Hallo-voorbeeld wordt ervan uitgegaan dat u een tabel "MijnTabel" hebt gemaakt in een ODBC-database en deze bevat een kolom met de naam 'timestampcolumn' voor de reeksgegevens.</span><span class="sxs-lookup"><span data-stu-id="ed72d-209">hello sample assumes you have created a table “MyTable” in an ODBC database and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="ed72d-210">Instelling 'extern': 'true' informeert Hallo Data Factory-service die gegevensset Hallo externe toohello data factory is en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="ed72d-210">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "ODBCDataSet",
    "properties": {
        "published": false,
        "type": "RelationalTable",
        "linkedServiceName": "OnPremOdbcLinkedService",
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

<span data-ttu-id="ed72d-211">**Azure Blob-uitvoergegevensset**</span><span class="sxs-lookup"><span data-stu-id="ed72d-211">**Azure Blob output dataset**</span></span>

<span data-ttu-id="ed72d-212">Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="ed72d-212">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="ed72d-213">pad naar map voor blob Hallo Hallo wordt dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="ed72d-213">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="ed72d-214">Hallo mappad jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ed72d-214">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

```json
{
    "name": "AzureBlobOdbcDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odbc/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


<span data-ttu-id="ed72d-215">**Kopieeractiviteit in een pijplijn met ODBC-gegevensbron (RelationalSource) en Blob sink (BlobSink)**</span><span class="sxs-lookup"><span data-stu-id="ed72d-215">**Copy activity in a pipeline with ODBC source (RelationalSource) and Blob sink (BlobSink)**</span></span>

<span data-ttu-id="ed72d-216">Hallo pijplijn bevat een Kopieeractiviteit die is geconfigureerd toouse deze invoer- en uitvoergegevenssets en geplande toorun is om het uur.</span><span class="sxs-lookup"><span data-stu-id="ed72d-216">hello pipeline contains a Copy Activity that is configured toouse these input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="ed72d-217">Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**RelationalSource** en **sink** type is ingesteld, te**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="ed72d-217">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="ed72d-218">Hallo SQL-query is opgegeven voor Hallo **query** eigenschap Hallo gegevens selecteert in Hallo voorbij toocopy uur.</span><span class="sxs-lookup"><span data-stu-id="ed72d-218">hello SQL query specified for hello **query** property selects hello data in hello past hour toocopy.</span></span>

```json
{
    "name": "CopyODBCToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "$$Text.Format('select * from MyTable where timestamp >= \\'{0:yyyy-MM-ddTHH:mm:ss}\\' AND timestamp < \\'{1:yyyy-MM-ddTHH:mm:ss}\\'', WindowStart, WindowEnd)"
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "OdbcDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOdbcDataSet"
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
                "name": "OdbcToBlob"
            }
        ],
        "start": "2016-06-01T18:00:00Z",
        "end": "2016-06-01T19:00:00Z"
    }
}
```
### <a name="type-mapping-for-odbc"></a><span data-ttu-id="ed72d-219">Toewijzing van het type voor ODBC</span><span class="sxs-lookup"><span data-stu-id="ed72d-219">Type mapping for ODBC</span></span>
<span data-ttu-id="ed72d-220">Zoals vermeld in Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel kopieeractiviteit voert automatische typeconversies van brontypen typen toosink Hello benadering in twee stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="ed72d-220">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach:</span></span>

1. <span data-ttu-id="ed72d-221">Systeemeigen bron typen too.NET type converteren</span><span class="sxs-lookup"><span data-stu-id="ed72d-221">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="ed72d-222">Converteren van .NET-type toonative sink-type</span><span class="sxs-lookup"><span data-stu-id="ed72d-222">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="ed72d-223">Bij het verplaatsen van gegevens uit gegevensarchieven ODBC, ODBC-gegevenstypen zijn toegewezen too.NET typen zoals vermeld in Hallo [Gegevenstypetoewijzingen ODBC](https://msdn.microsoft.com/library/cc668763.aspx) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="ed72d-223">When moving data from ODBC data stores, ODBC data types are mapped too.NET types as mentioned in hello [ODBC Data Type Mappings](https://msdn.microsoft.com/library/cc668763.aspx) topic.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="ed72d-224">Bronkolommen toosink toewijzen</span><span class="sxs-lookup"><span data-stu-id="ed72d-224">Map source toosink columns</span></span>
<span data-ttu-id="ed72d-225">Zie toolearn over het toewijzen van kolommen in bron gegevensset toocolumns in sink-gegevensset [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="ed72d-225">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="ed72d-226">Herhaalbare leesbewerking van relationele bronnen</span><span class="sxs-lookup"><span data-stu-id="ed72d-226">Repeatable read from relational sources</span></span>
<span data-ttu-id="ed72d-227">Houd bij het kopiëren van gegevens uit een relationele gegevensopslag, herhaalbaarheid rekening tooavoid ongewenste resultaten.</span><span class="sxs-lookup"><span data-stu-id="ed72d-227">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="ed72d-228">In Azure Data Factory, kunt u een segment handmatig opnieuw.</span><span class="sxs-lookup"><span data-stu-id="ed72d-228">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="ed72d-229">U kunt ook een beleid voor opnieuw proberen voor een gegevensset configureren zodat een segment wordt opnieuw uitgevoerd wanneer een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="ed72d-229">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="ed72d-230">Wanneer een segment opnieuw in beide gevallen wordt uitgevoerd, moet u ervoor dat dezelfde gegevens Hallo toomake wordt gelezen ongeacht hoe vaak een segment wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ed72d-230">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="ed72d-231">Zie [Repeatable van relationele bronnen lezen](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="ed72d-231">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="ge-historian-store"></a><span data-ttu-id="ed72d-232">GE Historian store</span><span class="sxs-lookup"><span data-stu-id="ed72d-232">GE Historian store</span></span>
<span data-ttu-id="ed72d-233">Maken van een ODBC-gekoppelde service toolink een [GE Proficy Historian (nu GE Historian)](http://www.geautomation.com/products/proficy-historian) gegevensarchief tooan Azure-gegevensfactory zoals weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="ed72d-233">You create an ODBC linked service toolink a [GE Proficy Historian (now GE Historian)](http://www.geautomation.com/products/proficy-historian) data store tooan Azure data factory as shown in hello following example:</span></span>

```json
{
    "name": "HistorianLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "connectionString": "DSN=<name of hello GE Historian store>",
            "gatewayName": "<gateway name>",
            "authenticationType": "Basic",
            "userName": "<user name>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="ed72d-234">Data Management Gateway op een on-premises machine gateway installeren en registreren Hallo met Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="ed72d-234">Install Data Management Gateway on an on-premises machine and register hello gateway with hello portal.</span></span> <span data-ttu-id="ed72d-235">Hallo-gateway is geïnstalleerd op uw lokale computer gebruikt Hallo ODBC-stuurprogramma voor GE Historian tooconnect toohello GE Historian gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="ed72d-235">hello gateway installed on your on-premises computer uses hello ODBC driver for GE Historian tooconnect toohello GE Historian data store.</span></span> <span data-ttu-id="ed72d-236">Daarom Hallo stuurprogramma installeren als deze nog niet is geïnstalleerd op de gatewaycomputer Hallo.</span><span class="sxs-lookup"><span data-stu-id="ed72d-236">Therefore, install hello driver if it is not already installed on hello gateway machine.</span></span> <span data-ttu-id="ed72d-237">Zie [connectiviteit inschakelen](#enabling-connectivity) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ed72d-237">See [Enabling connectivity](#enabling-connectivity) section for details.</span></span>

<span data-ttu-id="ed72d-238">Voordat u Hallo GE Historian opslaan in een Data Factory-oplossing gebruikt, moet u controleren of Hallo gateway toohello gegevensarchief volgens de instructies in de volgende sectie Hallo verbinding kan maken.</span><span class="sxs-lookup"><span data-stu-id="ed72d-238">Before you use hello GE Historian store in a Data Factory solution, verify whether hello gateway can connect toohello data store using instructions in hello next section.</span></span>

<span data-ttu-id="ed72d-239">Lees Hallo artikel vanaf Hallo voor een gedetailleerd overzicht van het gebruik van ODBC-gegevens worden opgeslagen als bron gegevensarchieven een kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="ed72d-239">Read hello article from hello beginning for a detailed overview of using ODBC data stores as source data stores in a copy operation.</span></span>  

## <a name="troubleshoot-connectivity-issues"></a><span data-ttu-id="ed72d-240">Verbindingsproblemen oplossen</span><span class="sxs-lookup"><span data-stu-id="ed72d-240">Troubleshoot connectivity issues</span></span>
<span data-ttu-id="ed72d-241">verbindingsproblemen tootroubleshoot, gebruik Hallo **Diagnostics** tabblad van **Data Management Gateway Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="ed72d-241">tootroubleshoot connection issues, use hello **Diagnostics** tab of **Data Management Gateway Configuration Manager**.</span></span>

1. <span data-ttu-id="ed72d-242">Start **Data Management Gateway Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="ed72d-242">Launch **Data Management Gateway Configuration Manager**.</span></span> <span data-ttu-id="ed72d-243">U kunt ofwel "C:\Program Files\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe' rechtstreeks (of) zoekopdracht uitvoeren voor **Gateway** toofind een koppeling te**Microsoft Data Management Gateway** de toepassing zoals weergegeven in Hallo installatiekopie te volgen.</span><span class="sxs-lookup"><span data-stu-id="ed72d-243">You can either run "C:\Program Files\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe" directly (or) search for **Gateway** toofind a link too**Microsoft Data Management Gateway** application as shown in hello following image.</span></span>

    ![Gateway zoeken](./media/data-factory-odbc-connector/search-gateway.png)
2. <span data-ttu-id="ed72d-245">Overschakelen van toohello **Diagnostics** tabblad.</span><span class="sxs-lookup"><span data-stu-id="ed72d-245">Switch toohello **Diagnostics** tab.</span></span>

    ![Gateway diagnostische gegevens](./media/data-factory-odbc-connector/data-factory-gateway-diagnostics.png)
3. <span data-ttu-id="ed72d-247">Selecteer Hallo **type** gegevens opslaan (gekoppelde service).</span><span class="sxs-lookup"><span data-stu-id="ed72d-247">Select hello **type** of data store (linked service).</span></span>
4. <span data-ttu-id="ed72d-248">Geef **verificatie** en voer **referenties** (of) Voer **verbindingsreeks** die is gebruikt tooconnect toohello-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="ed72d-248">Specify **authentication** and enter **credentials** (or) enter **connection string** that is used tooconnect toohello data store.</span></span>
5. <span data-ttu-id="ed72d-249">Klik op **verbinding testen** tootest Hallo verbinding toohello-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="ed72d-249">Click **Test connection** tootest hello connection toohello data store.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="ed72d-250">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="ed72d-250">Performance and Tuning</span></span>
<span data-ttu-id="ed72d-251">Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.</span><span class="sxs-lookup"><span data-stu-id="ed72d-251">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
