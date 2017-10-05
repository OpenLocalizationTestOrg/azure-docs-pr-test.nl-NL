---
title: Verplaatsen van gegevens uit de ODBC-gegevensarchieven | Microsoft Docs
description: Meer informatie over het verplaatsen van gegevens van ODBC-gegevensarchieven met behulp van Azure Data Factory.
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
ms.openlocfilehash: 269d9802ca4a6a16dbf9021929fe21104cb431f7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-odbc-data-stores-using-azure-data-factory"></a><span data-ttu-id="94d95-103">Verplaatsen van gegevens van ODBC-gegevensarchieven met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="94d95-103">Move data From ODBC data stores using Azure Data Factory</span></span>
<span data-ttu-id="94d95-104">Dit artikel wordt uitgelegd dat het gebruik van de Kopieeractiviteit in Azure Data Factory om gegevens te verplaatsen van een lokale ODBC-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="94d95-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an on-premises ODBC data store.</span></span> <span data-ttu-id="94d95-105">Dit is gebaseerd op de [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, hetgeen een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit toont.</span><span class="sxs-lookup"><span data-stu-id="94d95-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="94d95-106">U kunt gegevens uit een ODBC data store kopiëren naar een ondersteunde sink-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="94d95-106">You can copy data from an ODBC data store to any supported sink data store.</span></span> <span data-ttu-id="94d95-107">Zie voor een lijst met gegevensarchieven als PUT wordt ondersteund door de kopieeractiviteit, de [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel.</span><span class="sxs-lookup"><span data-stu-id="94d95-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="94d95-108">Data factory ondersteunt momenteel alleen zwevend gegevens uit een ODBC data store tot andere gegevensarchieven, maar niet voor het verplaatsen van gegevens uit andere gegevensarchieven naar een ODBC data store.</span><span class="sxs-lookup"><span data-stu-id="94d95-108">Data factory currently supports only moving data from an ODBC data store to other data stores, but not for moving data from other data stores to an ODBC data store.</span></span> 

## <a name="enabling-connectivity"></a><span data-ttu-id="94d95-109">Connectiviteit inschakelen</span><span class="sxs-lookup"><span data-stu-id="94d95-109">Enabling connectivity</span></span>
<span data-ttu-id="94d95-110">Verbinding maken met lokale ODBC-bronnen met behulp van Data Management Gateway biedt ondersteuning voor Data Factory-service.</span><span class="sxs-lookup"><span data-stu-id="94d95-110">Data Factory service supports connecting to on-premises ODBC sources using the Data Management Gateway.</span></span> <span data-ttu-id="94d95-111">Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor meer informatie over Data Management Gateway en stapsgewijze instructies over het instellen van de gateway.</span><span class="sxs-lookup"><span data-stu-id="94d95-111">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span> <span data-ttu-id="94d95-112">Verbinding maken met een ODBC-gegevensarchief, zelfs als deze is opgenomen in een Azure IaaS-VM met gebruik van de gateway.</span><span class="sxs-lookup"><span data-stu-id="94d95-112">Use the gateway to connect to an ODBC data store even if it is hosted in an Azure IaaS VM.</span></span>

<span data-ttu-id="94d95-113">U kunt de gateway installeren op de lokale machine of de virtuele machine van Azure als het beheerprogramma voor ODBC-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="94d95-113">You can install the gateway on the same on-premises machine or the Azure VM as the ODBC data store.</span></span> <span data-ttu-id="94d95-114">We raden echter aan dat u de gateway installeren op een afzonderlijke computer/Azure IaaS VM om bronconflicten te voorkomen en voor betere prestaties.</span><span class="sxs-lookup"><span data-stu-id="94d95-114">However, we recommend that you install the gateway on a separate machine/Azure IaaS VM to avoid resource contention and for better performance.</span></span> <span data-ttu-id="94d95-115">Wanneer u de gateway op een afzonderlijke computer installeert, is de machine moet toegang kunnen krijgen tot de machine met het beheerprogramma voor ODBC-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="94d95-115">When you install the gateway on a separate machine, the machine should be able to access the machine with the ODBC data store.</span></span>

<span data-ttu-id="94d95-116">Naast de Data Management Gateway moet u ook het ODBC-stuurprogramma voor de gegevensopslag installeren op de gateway-apparaat.</span><span class="sxs-lookup"><span data-stu-id="94d95-116">Apart from the Data Management Gateway, you also need to install the ODBC driver for the data store on the gateway machine.</span></span>

> [!NOTE]
> <span data-ttu-id="94d95-117">Zie [gateway problemen](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) voor tips over het oplossen van verbinding of gateway gerelateerde problemen.</span><span class="sxs-lookup"><span data-stu-id="94d95-117">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>

## <a name="getting-started"></a><span data-ttu-id="94d95-118">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="94d95-118">Getting started</span></span>
<span data-ttu-id="94d95-119">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens uit een ODBC data store verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="94d95-119">You can create a pipeline with a copy activity that moves data from an ODBC data store by using different tools/APIs.</span></span>

<span data-ttu-id="94d95-120">De eenvoudigste manier om een pijplijn maken is met de **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="94d95-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="94d95-121">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met de wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="94d95-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="94d95-122">U kunt ook de volgende hulpprogramma's gebruiken voor het maken van een pijplijn: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon**, **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="94d95-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="94d95-123">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies voor een pijplijn maken met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="94d95-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="94d95-124">Of u de hulpprogramma's of API's gebruiken, moet u de volgende stappen voor het maken van een pijplijn die de gegevens vanuit een brongegevensarchief naar een gegevensarchief sink verplaatst uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="94d95-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="94d95-125">Maak **gekoppelde services** slaat om invoer- en gegevens te koppelen aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="94d95-125">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="94d95-126">Maak **gegevenssets** vertegenwoordigt de invoer- en -gegevens voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="94d95-126">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="94d95-127">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="94d95-127">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="94d95-128">Wanneer u de wizard gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="94d95-128">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="94d95-129">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van de JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="94d95-129">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="94d95-130">Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die worden gebruikt om gegevens te kopiëren uit een ODBC data store [JSON-voorbeeld: gegevens kopiëren van ODBC-gegevens opslaan naar Azure Blob](#json-example-copy-data-from-odbc-data-store-to-azure-blob) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="94d95-130">For a sample with JSON definitions for Data Factory entities that are used to copy data from an ODBC data store, see [JSON example: Copy data from ODBC data store to Azure Blob](#json-example-copy-data-from-odbc-data-store-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="94d95-131">De volgende secties bevatten informatie over de JSON-eigenschappen die worden gebruikt voor het definiëren van Data Factory-entiteiten specifieke naar ODBC data store:</span><span class="sxs-lookup"><span data-stu-id="94d95-131">The following sections provide details about JSON properties that are used to define Data Factory entities specific to ODBC data store:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="94d95-132">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="94d95-132">Linked service properties</span></span>
<span data-ttu-id="94d95-133">De volgende tabel bevat de beschrijving voor JSON-elementen die specifiek zijn voor ODBC gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="94d95-133">The following table provides description for JSON elements specific to ODBC linked service.</span></span>

| <span data-ttu-id="94d95-134">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="94d95-134">Property</span></span> | <span data-ttu-id="94d95-135">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="94d95-135">Description</span></span> | <span data-ttu-id="94d95-136">Vereist</span><span class="sxs-lookup"><span data-stu-id="94d95-136">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="94d95-137">type</span><span class="sxs-lookup"><span data-stu-id="94d95-137">type</span></span> |<span data-ttu-id="94d95-138">De eigenschap type moet worden ingesteld op: **OnPremisesOdbc**</span><span class="sxs-lookup"><span data-stu-id="94d95-138">The type property must be set to: **OnPremisesOdbc**</span></span> |<span data-ttu-id="94d95-139">Ja</span><span class="sxs-lookup"><span data-stu-id="94d95-139">Yes</span></span> |
| <span data-ttu-id="94d95-140">connectionString</span><span class="sxs-lookup"><span data-stu-id="94d95-140">connectionString</span></span> |<span data-ttu-id="94d95-141">Het gedeelte niet access referentie van de verbindingsreeks en een optionele referentie versleuteld.</span><span class="sxs-lookup"><span data-stu-id="94d95-141">The non-access credential portion of the connection string and an optional encrypted credential.</span></span> <span data-ttu-id="94d95-142">Zie de voorbeelden in de volgende secties.</span><span class="sxs-lookup"><span data-stu-id="94d95-142">See examples in the following sections.</span></span> |<span data-ttu-id="94d95-143">Ja</span><span class="sxs-lookup"><span data-stu-id="94d95-143">Yes</span></span> |
| <span data-ttu-id="94d95-144">referentie</span><span class="sxs-lookup"><span data-stu-id="94d95-144">credential</span></span> |<span data-ttu-id="94d95-145">Het gedeelte van de referentie toegang van de verbindingsreeks die is opgegeven in de indeling van de eigenschapswaarde specifieke stuurprogramma's.</span><span class="sxs-lookup"><span data-stu-id="94d95-145">The access credential portion of the connection string specified in driver-specific property-value format.</span></span> <span data-ttu-id="94d95-146">Voorbeeld: "Uid =<user ID>; Pwd =<password>; RefreshToken =<secret refresh token>; '.</span><span class="sxs-lookup"><span data-stu-id="94d95-146">Example: “Uid=<user ID>;Pwd=<password>;RefreshToken=<secret refresh token>;”.</span></span> |<span data-ttu-id="94d95-147">Nee</span><span class="sxs-lookup"><span data-stu-id="94d95-147">No</span></span> |
| <span data-ttu-id="94d95-148">authenticationType</span><span class="sxs-lookup"><span data-stu-id="94d95-148">authenticationType</span></span> |<span data-ttu-id="94d95-149">Het soort verificatie gebruikt voor verbinding met het beheerprogramma voor ODBC-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="94d95-149">Type of authentication used to connect to the ODBC data store.</span></span> <span data-ttu-id="94d95-150">Mogelijke waarden zijn: anonieme en Basic.</span><span class="sxs-lookup"><span data-stu-id="94d95-150">Possible values are: Anonymous and Basic.</span></span> |<span data-ttu-id="94d95-151">Ja</span><span class="sxs-lookup"><span data-stu-id="94d95-151">Yes</span></span> |
| <span data-ttu-id="94d95-152">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="94d95-152">username</span></span> |<span data-ttu-id="94d95-153">Geef de gebruikersnaam als u basisverificatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="94d95-153">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="94d95-154">Nee</span><span class="sxs-lookup"><span data-stu-id="94d95-154">No</span></span> |
| <span data-ttu-id="94d95-155">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="94d95-155">password</span></span> |<span data-ttu-id="94d95-156">Wachtwoord voor het gebruikersaccount dat u hebt opgegeven voor de gebruikersnaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="94d95-156">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="94d95-157">Nee</span><span class="sxs-lookup"><span data-stu-id="94d95-157">No</span></span> |
| <span data-ttu-id="94d95-158">gatewayName</span><span class="sxs-lookup"><span data-stu-id="94d95-158">gatewayName</span></span> |<span data-ttu-id="94d95-159">Naam van de gateway die voor de Data Factory-service gebruiken moet voor verbinding met het beheerprogramma voor ODBC-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="94d95-159">Name of the gateway that the Data Factory service should use to connect to the ODBC data store.</span></span> |<span data-ttu-id="94d95-160">Ja</span><span class="sxs-lookup"><span data-stu-id="94d95-160">Yes</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="94d95-161">Met behulp van basisverificatie</span><span class="sxs-lookup"><span data-stu-id="94d95-161">Using Basic authentication</span></span>

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
### <a name="using-basic-authentication-with-encrypted-credentials"></a><span data-ttu-id="94d95-162">Met behulp van basisverificatie met versleutelde referenties</span><span class="sxs-lookup"><span data-stu-id="94d95-162">Using Basic authentication with encrypted credentials</span></span>
<span data-ttu-id="94d95-163">U kunt de referenties met versleutelen de [nieuw AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) cmdlet (versie 1.0 van Azure PowerShell) of [nieuw AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0,9 of een eerdere versie van Azure PowerShell).</span><span class="sxs-lookup"><span data-stu-id="94d95-163">You can encrypt the credentials using the [New-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) (1.0 version of Azure PowerShell) cmdlet or [New-AzureDataFactoryEncryptValue](https://msdn.microsoft.com/library/dn834940.aspx) (0.9 or earlier version of the Azure PowerShell).</span></span>  

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

### <a name="using-anonymous-authentication"></a><span data-ttu-id="94d95-164">Anonieme verificatie</span><span class="sxs-lookup"><span data-stu-id="94d95-164">Using Anonymous authentication</span></span>

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


## <a name="dataset-properties"></a><span data-ttu-id="94d95-165">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="94d95-165">Dataset properties</span></span>
<span data-ttu-id="94d95-166">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van de [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="94d95-166">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="94d95-167">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).</span><span class="sxs-lookup"><span data-stu-id="94d95-167">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="94d95-168">De **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over de locatie van de gegevens in het gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="94d95-168">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="94d95-169">De typeProperties sectie voor de gegevensset van het type **RelationalTable** (waaronder ODBC gegevensset) heeft de volgende eigenschappen</span><span class="sxs-lookup"><span data-stu-id="94d95-169">The typeProperties section for dataset of type **RelationalTable** (which includes ODBC dataset) has the following properties</span></span>

| <span data-ttu-id="94d95-170">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="94d95-170">Property</span></span> | <span data-ttu-id="94d95-171">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="94d95-171">Description</span></span> | <span data-ttu-id="94d95-172">Vereist</span><span class="sxs-lookup"><span data-stu-id="94d95-172">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="94d95-173">tableName</span><span class="sxs-lookup"><span data-stu-id="94d95-173">tableName</span></span> |<span data-ttu-id="94d95-174">De naam van de tabel in het beheerprogramma voor ODBC-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="94d95-174">Name of the table in the ODBC data store.</span></span> |<span data-ttu-id="94d95-175">Ja</span><span class="sxs-lookup"><span data-stu-id="94d95-175">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="94d95-176">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="94d95-176">Copy activity properties</span></span>
<span data-ttu-id="94d95-177">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van activiteiten van de [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="94d95-177">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="94d95-178">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en beleidsregels zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="94d95-178">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

<span data-ttu-id="94d95-179">Eigenschappen die beschikbaar zijn in de **typeProperties** sectie van de activiteit aan de andere kant variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="94d95-179">Properties available in the **typeProperties** section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="94d95-180">Voor de kopieeractiviteit variëren ze, afhankelijk van de typen van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="94d95-180">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="94d95-181">In de kopieeractiviteit, wanneer de bron van het type **RelationalSource** (waaronder ODBC), de volgende eigenschappen beschikbaar zijn in de sectie typeProperties:</span><span class="sxs-lookup"><span data-stu-id="94d95-181">In copy activity, when source is of type **RelationalSource** (which includes ODBC), the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="94d95-182">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="94d95-182">Property</span></span> | <span data-ttu-id="94d95-183">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="94d95-183">Description</span></span> | <span data-ttu-id="94d95-184">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="94d95-184">Allowed values</span></span> | <span data-ttu-id="94d95-185">Vereist</span><span class="sxs-lookup"><span data-stu-id="94d95-185">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="94d95-186">query</span><span class="sxs-lookup"><span data-stu-id="94d95-186">query</span></span> |<span data-ttu-id="94d95-187">Gebruik de aangepaste query om gegevens te lezen.</span><span class="sxs-lookup"><span data-stu-id="94d95-187">Use the custom query to read data.</span></span> |<span data-ttu-id="94d95-188">SQL-query-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="94d95-188">SQL query string.</span></span> <span data-ttu-id="94d95-189">Bijvoorbeeld: Selecteer * from MijnTabel.</span><span class="sxs-lookup"><span data-stu-id="94d95-189">For example: select * from MyTable.</span></span> |<span data-ttu-id="94d95-190">Ja</span><span class="sxs-lookup"><span data-stu-id="94d95-190">Yes</span></span> |


## <a name="json-example-copy-data-from-odbc-data-store-to-azure-blob"></a><span data-ttu-id="94d95-191">JSON-voorbeeld: gegevens kopiëren van ODBC-gegevens naar Azure Blob opslaan</span><span class="sxs-lookup"><span data-stu-id="94d95-191">JSON example: Copy data from ODBC data store to Azure Blob</span></span>
<span data-ttu-id="94d95-192">In dit voorbeeld bevat definities van JSON die u een pijplijn maken kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="94d95-192">This example provides JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="94d95-193">Er wordt weergegeven hoe gegevens kopiëren van een ODBC-gegevensbron naar een Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="94d95-193">It shows how to copy data from an ODBC source to an Azure Blob Storage.</span></span> <span data-ttu-id="94d95-194">Gegevens kunnen echter worden gekopieerd naar een van de PUT vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van de Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="94d95-194">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>

<span data-ttu-id="94d95-195">Het voorbeeld heeft de volgende data factory-entiteiten:</span><span class="sxs-lookup"><span data-stu-id="94d95-195">The sample has the following data factory entities:</span></span>

1. <span data-ttu-id="94d95-196">Een gekoppelde service van het type [OnPremisesOdbc](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="94d95-196">A linked service of type [OnPremisesOdbc](#linked-service-properties).</span></span>
2. <span data-ttu-id="94d95-197">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="94d95-197">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="94d95-198">Invoer [gegevensset](data-factory-create-datasets.md) van het type [RelationalTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="94d95-198">An input [dataset](data-factory-create-datasets.md) of type [RelationalTable](#dataset-properties).</span></span>
4. <span data-ttu-id="94d95-199">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="94d95-199">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="94d95-200">Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [RelationalSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="94d95-200">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="94d95-201">Het voorbeeld kopieert gegevens van de resultaten van een query in een ODBC-gegevensarchief naar een blob elk uur.</span><span class="sxs-lookup"><span data-stu-id="94d95-201">The sample copies data from a query result in an ODBC data store to a blob every hour.</span></span> <span data-ttu-id="94d95-202">De JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na de voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="94d95-202">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="94d95-203">Instellen als eerste stap van de data management gateway.</span><span class="sxs-lookup"><span data-stu-id="94d95-203">As a first step, set up the data management gateway.</span></span> <span data-ttu-id="94d95-204">De instructies vindt u in de [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="94d95-204">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="94d95-205">**ODBC gekoppelde service** in dit voorbeeld wordt de basisverificatie.</span><span class="sxs-lookup"><span data-stu-id="94d95-205">**ODBC linked service** This example uses the Basic authentication.</span></span> <span data-ttu-id="94d95-206">Zie [ODBC gekoppelde service](#linked-service-properties) sectie voor verschillende soorten verificatie die u kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="94d95-206">See [ODBC linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

<span data-ttu-id="94d95-207">**Een gekoppelde Azure Storage-service**</span><span class="sxs-lookup"><span data-stu-id="94d95-207">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="94d95-208">**ODBC-invoergegevensset**</span><span class="sxs-lookup"><span data-stu-id="94d95-208">**ODBC input dataset**</span></span>

<span data-ttu-id="94d95-209">Het voorbeeld wordt ervan uitgegaan dat u een tabel "MijnTabel" hebt gemaakt in een ODBC-database en deze bevat een kolom met de naam 'timestampcolumn' voor de reeksgegevens.</span><span class="sxs-lookup"><span data-stu-id="94d95-209">The sample assumes you have created a table “MyTable” in an ODBC database and it contains a column called “timestampcolumn” for time series data.</span></span>

<span data-ttu-id="94d95-210">Instelling 'extern': 'true' informeert de Data Factory-service dat de dataset extern is aan de gegevensfactory en niet wordt geproduceerd door een activiteit in de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="94d95-210">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="94d95-211">**Azure Blob-uitvoergegevensset**</span><span class="sxs-lookup"><span data-stu-id="94d95-211">**Azure Blob output dataset**</span></span>

<span data-ttu-id="94d95-212">Gegevens worden geschreven naar een nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="94d95-212">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="94d95-213">Het pad naar de blob wordt dynamisch geëvalueerd op basis van de begintijd van het segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="94d95-213">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="94d95-214">Het mappad maakt gebruik van jaar, maand, dag en uur delen van de begintijd.</span><span class="sxs-lookup"><span data-stu-id="94d95-214">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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


<span data-ttu-id="94d95-215">**Kopieeractiviteit in een pijplijn met ODBC-gegevensbron (RelationalSource) en Blob sink (BlobSink)**</span><span class="sxs-lookup"><span data-stu-id="94d95-215">**Copy activity in a pipeline with ODBC source (RelationalSource) and Blob sink (BlobSink)**</span></span>

<span data-ttu-id="94d95-216">De pijplijn bevat een Kopieeractiviteit die is geconfigureerd voor gebruik van deze invoer- en uitvoergegevenssets en elk uur is gepland.</span><span class="sxs-lookup"><span data-stu-id="94d95-216">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="94d95-217">In de pijplijn-JSON-definitie de **bron** type is ingesteld op **RelationalSource** en **sink** type is ingesteld op **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="94d95-217">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="94d95-218">De SQL-query die is opgegeven voor de **query** eigenschap selecteert u de gegevens in het afgelopen uur te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="94d95-218">The SQL query specified for the **query** property selects the data in the past hour to copy.</span></span>

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
### <a name="type-mapping-for-odbc"></a><span data-ttu-id="94d95-219">Toewijzing van het type voor ODBC</span><span class="sxs-lookup"><span data-stu-id="94d95-219">Type mapping for ODBC</span></span>
<span data-ttu-id="94d95-220">Zoals vermeld in de [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel kopieerbewerking wordt automatische typeconversies van brontypen opvangen typen met de volgende benadering voor in twee stappen uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="94d95-220">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach:</span></span>

1. <span data-ttu-id="94d95-221">Systeemeigen brontypen converteren naar .NET-type</span><span class="sxs-lookup"><span data-stu-id="94d95-221">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="94d95-222">Converteren van .NET-type naar systeemeigen sink-type</span><span class="sxs-lookup"><span data-stu-id="94d95-222">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="94d95-223">Bij het verplaatsen van gegevens uit gegevensarchieven ODBC, ODBC-gegevenstypen zijn toegewezen aan .NET-typen, zoals vermeld in de [Gegevenstypetoewijzingen ODBC](https://msdn.microsoft.com/library/cc668763.aspx) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="94d95-223">When moving data from ODBC data stores, ODBC data types are mapped to .NET types as mentioned in the [ODBC Data Type Mappings](https://msdn.microsoft.com/library/cc668763.aspx) topic.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="94d95-224">Bron van de kaart opvangen kolommen</span><span class="sxs-lookup"><span data-stu-id="94d95-224">Map source to sink columns</span></span>
<span data-ttu-id="94d95-225">Zie voor meer informatie over het toewijzen van kolommen in gegevensset naar kolommen in gegevensset sink bron, [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="94d95-225">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="94d95-226">Herhaalbare leesbewerking van relationele bronnen</span><span class="sxs-lookup"><span data-stu-id="94d95-226">Repeatable read from relational sources</span></span>
<span data-ttu-id="94d95-227">Bij het kopiëren van gegevens van relationele gegevens worden opgeslagen, moet u herhaalbaarheid Houd in gedachten om te voorkomen dat ongewenste resultaten.</span><span class="sxs-lookup"><span data-stu-id="94d95-227">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="94d95-228">In Azure Data Factory, kunt u een segment handmatig opnieuw.</span><span class="sxs-lookup"><span data-stu-id="94d95-228">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="94d95-229">U kunt ook een beleid voor opnieuw proberen voor een gegevensset configureren zodat een segment wordt opnieuw uitgevoerd wanneer een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="94d95-229">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="94d95-230">Wanneer een segment opnieuw in beide gevallen wordt uitgevoerd, moet u ervoor zorgen dat dezelfde gegevens is gelezen ongeacht hoe vaak een segment wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="94d95-230">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="94d95-231">Zie [Repeatable van relationele bronnen lezen](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="94d95-231">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="ge-historian-store"></a><span data-ttu-id="94d95-232">GE Historian store</span><span class="sxs-lookup"><span data-stu-id="94d95-232">GE Historian store</span></span>
<span data-ttu-id="94d95-233">Maken van een service gekoppelde ODBC-om te koppelen een [GE Proficy Historian (nu GE Historian)](http://www.geautomation.com/products/proficy-historian) gegevensarchief aan een Azure data factory zoals weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="94d95-233">You create an ODBC linked service to link a [GE Proficy Historian (now GE Historian)](http://www.geautomation.com/products/proficy-historian) data store to an Azure data factory as shown in the following example:</span></span>

```json
{
    "name": "HistorianLinkedService",
    "properties":
    {
        "type": "OnPremisesOdbc",
        "typeProperties":
        {
            "connectionString": "DSN=<name of the GE Historian store>",
            "gatewayName": "<gateway name>",
            "authenticationType": "Basic",
            "userName": "<user name>",
            "password": "<password>"
        }
    }
}
```

<span data-ttu-id="94d95-234">Data Management Gateway installeren op een on-premises machine en de gateway registreren met de portal.</span><span class="sxs-lookup"><span data-stu-id="94d95-234">Install Data Management Gateway on an on-premises machine and register the gateway with the portal.</span></span> <span data-ttu-id="94d95-235">Het ODBC-stuurprogramma voor GE Historian de gateway is geïnstalleerd op uw lokale computer gebruikt om verbinding met de gegevensopslag GE Historian.</span><span class="sxs-lookup"><span data-stu-id="94d95-235">The gateway installed on your on-premises computer uses the ODBC driver for GE Historian to connect to the GE Historian data store.</span></span> <span data-ttu-id="94d95-236">Installeer het stuurprogramma daarom als deze nog niet is geïnstalleerd op de gateway-apparaat.</span><span class="sxs-lookup"><span data-stu-id="94d95-236">Therefore, install the driver if it is not already installed on the gateway machine.</span></span> <span data-ttu-id="94d95-237">Zie [connectiviteit inschakelen](#enabling-connectivity) sectie voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="94d95-237">See [Enabling connectivity](#enabling-connectivity) section for details.</span></span>

<span data-ttu-id="94d95-238">Voordat u de store GE Historian in een Data Factory-oplossing gebruikt, moet u controleren of de gateway verbinding kan maken met de gegevensopslag volgens de instructies in de volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="94d95-238">Before you use the GE Historian store in a Data Factory solution, verify whether the gateway can connect to the data store using instructions in the next section.</span></span>

<span data-ttu-id="94d95-239">Lees het artikel vanaf het begin voor een gedetailleerd overzicht van het gebruik van ODBC-gegevens worden opgeslagen als bron gegevensarchieven een kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="94d95-239">Read the article from the beginning for a detailed overview of using ODBC data stores as source data stores in a copy operation.</span></span>  

## <a name="troubleshoot-connectivity-issues"></a><span data-ttu-id="94d95-240">Verbindingsproblemen oplossen</span><span class="sxs-lookup"><span data-stu-id="94d95-240">Troubleshoot connectivity issues</span></span>
<span data-ttu-id="94d95-241">Gebruik voor het oplossen van problemen met de **Diagnostics** tabblad van **Data Management Gateway Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="94d95-241">To troubleshoot connection issues, use the **Diagnostics** tab of **Data Management Gateway Configuration Manager**.</span></span>

1. <span data-ttu-id="94d95-242">Start **Data Management Gateway Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="94d95-242">Launch **Data Management Gateway Configuration Manager**.</span></span> <span data-ttu-id="94d95-243">U kunt ofwel "C:\Program Files\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe' rechtstreeks (of) zoekopdracht uitvoeren voor **Gateway** vinden van een koppeling naar **Microsoft Data Management Gateway** de toepassing zoals weergegeven in de volgende afbeelding.</span><span class="sxs-lookup"><span data-stu-id="94d95-243">You can either run "C:\Program Files\Microsoft Data Management Gateway\1.0\Shared\ConfigManager.exe" directly (or) search for **Gateway** to find a link to **Microsoft Data Management Gateway** application as shown in the following image.</span></span>

    ![Gateway zoeken](./media/data-factory-odbc-connector/search-gateway.png)
2. <span data-ttu-id="94d95-245">Overschakelen naar de **Diagnostics** tabblad.</span><span class="sxs-lookup"><span data-stu-id="94d95-245">Switch to the **Diagnostics** tab.</span></span>

    ![Gateway diagnostische gegevens](./media/data-factory-odbc-connector/data-factory-gateway-diagnostics.png)
3. <span data-ttu-id="94d95-247">Selecteer de **type** gegevens opslaan (gekoppelde service).</span><span class="sxs-lookup"><span data-stu-id="94d95-247">Select the **type** of data store (linked service).</span></span>
4. <span data-ttu-id="94d95-248">Geef **verificatie** en voer **referenties** (of) Voer **verbindingsreeks** die wordt gebruikt voor het verbinding maken met het gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="94d95-248">Specify **authentication** and enter **credentials** (or) enter **connection string** that is used to connect to the data store.</span></span>
5. <span data-ttu-id="94d95-249">Klik op **verbinding testen** voor het testen van de verbinding met het gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="94d95-249">Click **Test connection** to test the connection to the data store.</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="94d95-250">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="94d95-250">Performance and Tuning</span></span>
<span data-ttu-id="94d95-251">Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) voor meer informatie over de belangrijkste factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren om te optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="94d95-251">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
