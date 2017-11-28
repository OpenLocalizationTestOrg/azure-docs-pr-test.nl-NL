---
title: Gegevens verplaatsen naar en van SQL Server | Microsoft Docs
description: Meer informatie over het verplaatsen van gegevens uit SQL Server-database on-premises of in een virtuele machine in Azure met Azure Data Factory.
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
ms.openlocfilehash: 9cd2077d897631457925cda5ef5e6df3c0c33177
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-to-and-from-sql-server-on-premises-or-on-iaas-azure-vm-using-azure-data-factory"></a><span data-ttu-id="a997a-103">Verplaatsen van gegevens naar en van SQL Server on-premises of op IaaS (Azure VM) met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="a997a-103">Move data to and from SQL Server on-premises or on IaaS (Azure VM) using Azure Data Factory</span></span>
<span data-ttu-id="a997a-104">Dit artikel wordt uitgelegd dat het gebruik van de Kopieeractiviteit in Azure Data Factory om gegevens uit een on-premises SQL Server database te verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="a997a-104">This article explains how to use the Copy Activity in Azure Data Factory to move data to/from an on-premises SQL Server database.</span></span> <span data-ttu-id="a997a-105">Dit is gebaseerd op de [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, hetgeen een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit toont.</span><span class="sxs-lookup"><span data-stu-id="a997a-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span> 

## <a name="supported-scenarios"></a><span data-ttu-id="a997a-106">Ondersteunde scenario 's</span><span class="sxs-lookup"><span data-stu-id="a997a-106">Supported scenarios</span></span>
<span data-ttu-id="a997a-107">U kunt gegevens kopiëren **uit een SQL Server-database** opslaat in de volgende gegevens:</span><span class="sxs-lookup"><span data-stu-id="a997a-107">You can copy data **from a SQL Server database** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="a997a-108">U kunt gegevens kopiëren van de volgende gegevensarchieven **met een SQL Server-database**:</span><span class="sxs-lookup"><span data-stu-id="a997a-108">You can copy data from the following data stores **to a SQL Server database**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-sql-server-versions"></a><span data-ttu-id="a997a-109">Ondersteunde versies van SQL Server</span><span class="sxs-lookup"><span data-stu-id="a997a-109">Supported SQL Server versions</span></span>
<span data-ttu-id="a997a-110">Deze ondersteuning van SQL Server-connector kopiëren van gegevens van/naar de volgende versies van gehost exemplaar lokaal of in Azure IaaS met behulp van zowel de SQL-verificatie en de Windows-verificatie: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span><span class="sxs-lookup"><span data-stu-id="a997a-110">This SQL Server connector support copying data from/to the following versions of instance hosted on-premises or in Azure IaaS using both SQL authentication and Windows authentication: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005</span></span>

## <a name="enabling-connectivity"></a><span data-ttu-id="a997a-111">Connectiviteit inschakelen</span><span class="sxs-lookup"><span data-stu-id="a997a-111">Enabling connectivity</span></span>
<span data-ttu-id="a997a-112">De concepten en de stappen die nodig zijn om verbinding te maken met SQL Server die wordt gehost on-premises of in virtuele machines van Azure IaaS (Infrastructure-as-a-Service) zijn hetzelfde.</span><span class="sxs-lookup"><span data-stu-id="a997a-112">The concepts and steps needed for connecting with SQL Server hosted on-premises or in Azure IaaS (Infrastructure-as-a-Service) VMs are the same.</span></span> <span data-ttu-id="a997a-113">In beide gevallen moet u Data Management Gateway gebruiken voor verbinding.</span><span class="sxs-lookup"><span data-stu-id="a997a-113">In both cases, you need to use Data Management Gateway for connectivity.</span></span>

<span data-ttu-id="a997a-114">Zie [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel voor meer informatie over Data Management Gateway en stapsgewijze instructies over het instellen van de gateway.</span><span class="sxs-lookup"><span data-stu-id="a997a-114">See [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article to learn about Data Management Gateway and step-by-step instructions on setting up the gateway.</span></span> <span data-ttu-id="a997a-115">Instellen van een gatewayexemplaar is een vereiste voor het verbinden met SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a997a-115">Setting up a gateway instance is a pre-requisite for connecting with SQL Server.</span></span>

<span data-ttu-id="a997a-116">Terwijl de SQL-Server voor betere prestaties u gateway op de lokale machine, dezelfde of de cloud VM-instantie installeren kunt, raden wij u deze installeren op afzonderlijke computers.</span><span class="sxs-lookup"><span data-stu-id="a997a-116">While you can install gateway on the same on-premises machine or cloud VM instance as the SQL Server for better performance, we recommended that you install them on separate machines.</span></span> <span data-ttu-id="a997a-117">Met de gateway en de SQL Server op afzonderlijke computers, worden bronconflicten beperkt.</span><span class="sxs-lookup"><span data-stu-id="a997a-117">Having the gateway and SQL Server on separate machines reduces resource contention.</span></span>

## <a name="getting-started"></a><span data-ttu-id="a997a-118">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="a997a-118">Getting started</span></span>
<span data-ttu-id="a997a-119">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens uit een on-premises SQL Server database verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="a997a-119">You can create a pipeline with a copy activity that moves data to/from an on-premises SQL Server database by using different tools/APIs.</span></span>

<span data-ttu-id="a997a-120">De eenvoudigste manier om een pijplijn maken is met de **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="a997a-120">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="a997a-121">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met de wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="a997a-121">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="a997a-122">U kunt ook de volgende hulpprogramma's gebruiken voor het maken van een pijplijn: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon**, **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="a997a-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="a997a-123">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies voor een pijplijn maken met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="a997a-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="a997a-124">Of u de hulpprogramma's of API's gebruiken, moet u de volgende stappen voor het maken van een pijplijn die de gegevens vanuit een brongegevensarchief naar een gegevensarchief sink verplaatst uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="a997a-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="a997a-125">Maak een **gegevensfactory**.</span><span class="sxs-lookup"><span data-stu-id="a997a-125">Create a **data factory**.</span></span> <span data-ttu-id="a997a-126">Een gegevensfactory kan één of meer pijplijnen bevatten.</span><span class="sxs-lookup"><span data-stu-id="a997a-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="a997a-127">Maak **gekoppelde services** slaat om invoer- en gegevens te koppelen aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="a997a-127">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="a997a-128">Bijvoorbeeld, als u gegevens uit een SQL Server-database naar een Azure blob storage kopiëren wilt, maakt u twee gekoppelde services als u wilt uw SQL Server-database en de Azure storage-account koppelen aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="a997a-128">For example, if you are copying data from a SQL Server database to an Azure blob storage, you create two linked services to link your SQL Server database and Azure storage account to your data factory.</span></span> <span data-ttu-id="a997a-129">Zie voor de gekoppelde service-eigenschappen die specifiek voor SQL Server-database zijn, [gekoppelde service-eigenschappen](#linked-service-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="a997a-129">For linked service properties that are specific to SQL Server database, see [linked service properties](#linked-service-properties) section.</span></span> 
3. <span data-ttu-id="a997a-130">Maak **gegevenssets** vertegenwoordigt de invoer- en -gegevens voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="a997a-130">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="a997a-131">In het voorbeeld in de laatste stap wordt vermeld, maakt u een gegevensset om op te geven van de SQL-tabel in uw SQL Server-database waarin de invoergegevens.</span><span class="sxs-lookup"><span data-stu-id="a997a-131">In the example mentioned in the last step, you create a dataset to specify the SQL table in your SQL Server database that contains the input data.</span></span> <span data-ttu-id="a997a-132">En u een andere gegevensset opgeven van de blob-container en de map waarin de gegevens die zijn gekopieerd uit de SQL Server-database maken.</span><span class="sxs-lookup"><span data-stu-id="a997a-132">And, you create another dataset to specify the blob container and the folder that holds the data copied from the SQL Server database.</span></span> <span data-ttu-id="a997a-133">Zie voor eigenschappen van gegevensset die specifiek voor SQL Server-database zijn, [eigenschappen van gegevensset](#dataset-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="a997a-133">For dataset properties that are specific to SQL Server database, see [dataset properties](#dataset-properties) section.</span></span>
4. <span data-ttu-id="a997a-134">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="a997a-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="a997a-135">In het voorbeeld eerder vermeld, gebruikt u SqlSource als een bron- en BlobSink als een sink voor de kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="a997a-135">In the example mentioned earlier, you use SqlSource as a source and BlobSink as a sink for the copy activity.</span></span> <span data-ttu-id="a997a-136">Op dezelfde manier als u uit Azure Blob Storage met SQL Server-Database kopiëren wilt, gebruikt u BlobSource en SqlSink in de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="a997a-136">Similarly, if you are copying from Azure Blob Storage to SQL Server Database, you use BlobSource and SqlSink in the copy activity.</span></span> <span data-ttu-id="a997a-137">Zie voor activiteitseigenschappen kopiëren die specifiek voor SQL Server-Database zijn, [activiteitseigenschappen kopiëren](#copy-activity-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="a997a-137">For copy activity properties that are specific to SQL Server Database, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="a997a-138">Klik op de koppeling in de vorige sectie voor de gegevensopslag voor meer informatie over het gebruik van een gegevensarchief als een bron of een sink.</span><span class="sxs-lookup"><span data-stu-id="a997a-138">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span> 

<span data-ttu-id="a997a-139">Wanneer u de wizard gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a997a-139">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="a997a-140">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van de JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="a997a-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="a997a-141">Zie voor voorbeelden met JSON-definities voor Data Factory-entiteiten die worden gebruikt om gegevens te kopiëren naar/van een on-premises SQL Server database [JSON voorbeelden](#json-examples-for-copying-data-from-and-to-sql-server) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="a997a-141">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an on-premises SQL Server database, see [JSON examples](#json-examples-for-copying-data-from-and-to-sql-server) section of this article.</span></span> 

<span data-ttu-id="a997a-142">De volgende secties bevatten informatie over de JSON-eigenschappen die worden gebruikt voor het definiëren van Data Factory-entiteiten specifieke met SQL Server:</span><span class="sxs-lookup"><span data-stu-id="a997a-142">The following sections provide details about JSON properties that are used to define Data Factory entities specific to SQL Server:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="a997a-143">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="a997a-143">Linked service properties</span></span>
<span data-ttu-id="a997a-144">Maken van een gekoppelde service van het type **OnPremisesSqlServer** een on-premises SQL Server database koppelen aan een gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="a997a-144">You create a linked service of type **OnPremisesSqlServer** to link an on-premises SQL Server database to a data factory.</span></span> <span data-ttu-id="a997a-145">De volgende tabel bevat een beschrijving voor JSON-elementen die specifiek zijn voor lokale SQL Server gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="a997a-145">The following table provides description for JSON elements specific to on-premises SQL Server linked service.</span></span>

<span data-ttu-id="a997a-146">De volgende tabel bevat een beschrijving voor JSON-elementen die specifiek zijn voor de service SQL Server gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="a997a-146">The following table provides description for JSON elements specific to SQL Server linked service.</span></span>

| <span data-ttu-id="a997a-147">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="a997a-147">Property</span></span> | <span data-ttu-id="a997a-148">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a997a-148">Description</span></span> | <span data-ttu-id="a997a-149">Vereist</span><span class="sxs-lookup"><span data-stu-id="a997a-149">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a997a-150">type</span><span class="sxs-lookup"><span data-stu-id="a997a-150">type</span></span> |<span data-ttu-id="a997a-151">De eigenschap type moet worden ingesteld op: **OnPremisesSqlServer**.</span><span class="sxs-lookup"><span data-stu-id="a997a-151">The type property should be set to: **OnPremisesSqlServer**.</span></span> |<span data-ttu-id="a997a-152">Ja</span><span class="sxs-lookup"><span data-stu-id="a997a-152">Yes</span></span> |
| <span data-ttu-id="a997a-153">connectionString</span><span class="sxs-lookup"><span data-stu-id="a997a-153">connectionString</span></span> |<span data-ttu-id="a997a-154">ConnectionString informatie die nodig zijn voor de verbinding met de lokale SQL Server-database met behulp van de SQL-verificatie of de Windows-verificatie opgeven.</span><span class="sxs-lookup"><span data-stu-id="a997a-154">Specify connectionString information needed to connect to the on-premises SQL Server database using either SQL authentication or Windows authentication.</span></span> |<span data-ttu-id="a997a-155">Ja</span><span class="sxs-lookup"><span data-stu-id="a997a-155">Yes</span></span> |
| <span data-ttu-id="a997a-156">gatewayName</span><span class="sxs-lookup"><span data-stu-id="a997a-156">gatewayName</span></span> |<span data-ttu-id="a997a-157">Naam van de gateway die voor de Data Factory-service gebruiken moet voor verbinding met het lokale SQL Server-database.</span><span class="sxs-lookup"><span data-stu-id="a997a-157">Name of the gateway that the Data Factory service should use to connect to the on-premises SQL Server database.</span></span> |<span data-ttu-id="a997a-158">Ja</span><span class="sxs-lookup"><span data-stu-id="a997a-158">Yes</span></span> |
| <span data-ttu-id="a997a-159">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="a997a-159">username</span></span> |<span data-ttu-id="a997a-160">Geef de gebruikersnaam als u Windows-verificatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="a997a-160">Specify user name if you are using Windows Authentication.</span></span> <span data-ttu-id="a997a-161">Voorbeeld: **domainname\\gebruikersnaam**.</span><span class="sxs-lookup"><span data-stu-id="a997a-161">Example: **domainname\\username**.</span></span> |<span data-ttu-id="a997a-162">Nee</span><span class="sxs-lookup"><span data-stu-id="a997a-162">No</span></span> |
| <span data-ttu-id="a997a-163">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="a997a-163">password</span></span> |<span data-ttu-id="a997a-164">Wachtwoord voor het gebruikersaccount dat u hebt opgegeven voor de gebruikersnaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="a997a-164">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="a997a-165">Nee</span><span class="sxs-lookup"><span data-stu-id="a997a-165">No</span></span> |

<span data-ttu-id="a997a-166">U kunt versleutelen referenties met behulp van de **nieuw AzureRmDataFactoryEncryptValue** cmdlet en in de verbindingsreeks gebruiken, zoals wordt weergegeven in het volgende voorbeeld (**EncryptedCredential** eigenschap):</span><span class="sxs-lookup"><span data-stu-id="a997a-166">You can encrypt credentials using the **New-AzureRmDataFactoryEncryptValue** cmdlet and use them in the connection string as shown in the following example (**EncryptedCredential** property):</span></span>  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

### <a name="samples"></a><span data-ttu-id="a997a-167">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="a997a-167">Samples</span></span>
<span data-ttu-id="a997a-168">**JSON voor het gebruik van SQL-verificatie**</span><span class="sxs-lookup"><span data-stu-id="a997a-168">**JSON for using SQL Authentication**</span></span>

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
<span data-ttu-id="a997a-169">**JSON voor het gebruik van Windows-verificatie**</span><span class="sxs-lookup"><span data-stu-id="a997a-169">**JSON for using Windows Authentication**</span></span>

<span data-ttu-id="a997a-170">Data Management Gateway wordt het opgegeven gebruikersaccount verbinding maken met de lokale SQL Server-database te imiteren.</span><span class="sxs-lookup"><span data-stu-id="a997a-170">Data Management Gateway will impersonate the specified user account to connect to the on-premises SQL Server database.</span></span> 

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

## <a name="dataset-properties"></a><span data-ttu-id="a997a-171">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="a997a-171">Dataset properties</span></span>
<span data-ttu-id="a997a-172">In de voorbeelden hebt u een gegevensset van het type gebruikt **SqlServerTable** vertegenwoordigt een tabel in een SQL Server-database.</span><span class="sxs-lookup"><span data-stu-id="a997a-172">In the samples, you have used a dataset of type **SqlServerTable** to represent a table in a SQL Server database.</span></span>  

<span data-ttu-id="a997a-173">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van de [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="a997a-173">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="a997a-174">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (SQL Server, Azure blob-, Azure-tabel, enz.).</span><span class="sxs-lookup"><span data-stu-id="a997a-174">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (SQL Server, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="a997a-175">De sectie typeProperties verschilt voor elk type gegevensset en bevat informatie over de locatie van de gegevens in het gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="a997a-175">The typeProperties section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="a997a-176">De **typeProperties** sectie voor de gegevensset van het type **SqlServerTable** heeft de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="a997a-176">The **typeProperties** section for the dataset of type **SqlServerTable** has the following properties:</span></span>

| <span data-ttu-id="a997a-177">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="a997a-177">Property</span></span> | <span data-ttu-id="a997a-178">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a997a-178">Description</span></span> | <span data-ttu-id="a997a-179">Vereist</span><span class="sxs-lookup"><span data-stu-id="a997a-179">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a997a-180">tableName</span><span class="sxs-lookup"><span data-stu-id="a997a-180">tableName</span></span> |<span data-ttu-id="a997a-181">De naam van de tabel of weergave in de SQL Server-Database-instantie waarnaar de gekoppelde service verwijst.</span><span class="sxs-lookup"><span data-stu-id="a997a-181">Name of the table or view in the SQL Server Database instance that linked service refers to.</span></span> |<span data-ttu-id="a997a-182">Ja</span><span class="sxs-lookup"><span data-stu-id="a997a-182">Yes</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="a997a-183">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="a997a-183">Copy activity properties</span></span>
<span data-ttu-id="a997a-184">Als u gegevens uit een SQL Server-database verplaatst, u het brontype instellen in de kopieerbewerking naar **SqlSource**.</span><span class="sxs-lookup"><span data-stu-id="a997a-184">If you are moving data from a SQL Server database, you set the source type in the copy activity to **SqlSource**.</span></span> <span data-ttu-id="a997a-185">Als u gegevens naar een SQL Server-database verplaatst, u stelt het sink-type in de kopieerbewerking naar **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="a997a-185">Similarly, if you are moving data to a SQL Server database, you set the sink type in the copy activity to **SqlSink**.</span></span> <span data-ttu-id="a997a-186">Deze sectie bevat een lijst met eigenschappen die worden ondersteund door SqlSource en SqlSink.</span><span class="sxs-lookup"><span data-stu-id="a997a-186">This section provides a list of properties supported by SqlSource and SqlSink.</span></span>

<span data-ttu-id="a997a-187">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van activiteiten van de [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="a997a-187">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="a997a-188">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en beleidsregels zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="a997a-188">Properties such as name, description, input and output tables, and policies are available for all types of activities.</span></span>

> [!NOTE]
> <span data-ttu-id="a997a-189">De Kopieeractiviteit slechts één invoer en slechts één uitvoer produceert.</span><span class="sxs-lookup"><span data-stu-id="a997a-189">The Copy Activity takes only one input and produces only one output.</span></span>

<span data-ttu-id="a997a-190">Terwijl de eigenschappen die beschikbaar zijn in de sectie typeProperties van de activiteit variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="a997a-190">Whereas, properties available in the typeProperties section of the activity vary with each activity type.</span></span> <span data-ttu-id="a997a-191">Voor de kopieeractiviteit variëren ze, afhankelijk van de typen van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="a997a-191">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

### <a name="sqlsource"></a><span data-ttu-id="a997a-192">SqlSource</span><span class="sxs-lookup"><span data-stu-id="a997a-192">SqlSource</span></span>
<span data-ttu-id="a997a-193">Wanneer u de gegevensbron in een kopieeractiviteit is van het type **SqlSource**, de volgende eigenschappen beschikbaar zijn in **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="a997a-193">When source in a copy activity is of type **SqlSource**, the following properties are available in **typeProperties** section:</span></span>

| <span data-ttu-id="a997a-194">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="a997a-194">Property</span></span> | <span data-ttu-id="a997a-195">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a997a-195">Description</span></span> | <span data-ttu-id="a997a-196">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="a997a-196">Allowed values</span></span> | <span data-ttu-id="a997a-197">Vereist</span><span class="sxs-lookup"><span data-stu-id="a997a-197">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a997a-198">sqlReaderQuery</span><span class="sxs-lookup"><span data-stu-id="a997a-198">sqlReaderQuery</span></span> |<span data-ttu-id="a997a-199">Gebruik de aangepaste query om gegevens te lezen.</span><span class="sxs-lookup"><span data-stu-id="a997a-199">Use the custom query to read data.</span></span> |<span data-ttu-id="a997a-200">SQL-query-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="a997a-200">SQL query string.</span></span> <span data-ttu-id="a997a-201">Bijvoorbeeld: Selecteer * from MijnTabel.</span><span class="sxs-lookup"><span data-stu-id="a997a-201">For example: select * from MyTable.</span></span> <span data-ttu-id="a997a-202">Kan naar meerdere tabellen uit de database waarnaar wordt verwezen door de invoergegevensset verwijzen.</span><span class="sxs-lookup"><span data-stu-id="a997a-202">May reference multiple tables from the database referenced by the input dataset.</span></span> <span data-ttu-id="a997a-203">Als niet wordt opgegeven, de SQL-instructie die is uitgevoerd: Selecteer een van de MyTable.</span><span class="sxs-lookup"><span data-stu-id="a997a-203">If not specified, the SQL statement that is executed: select from MyTable.</span></span> |<span data-ttu-id="a997a-204">Nee</span><span class="sxs-lookup"><span data-stu-id="a997a-204">No</span></span> |
| <span data-ttu-id="a997a-205">sqlReaderStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="a997a-205">sqlReaderStoredProcedureName</span></span> |<span data-ttu-id="a997a-206">Naam van de opgeslagen procedure die gegevens uit de brontabel leest.</span><span class="sxs-lookup"><span data-stu-id="a997a-206">Name of the stored procedure that reads data from the source table.</span></span> |<span data-ttu-id="a997a-207">Naam van de opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="a997a-207">Name of the stored procedure.</span></span> <span data-ttu-id="a997a-208">De laatste SQL-instructie moet een SELECT-instructie in de opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="a997a-208">The last SQL statement must be a SELECT statement in the stored procedure.</span></span> |<span data-ttu-id="a997a-209">Nee</span><span class="sxs-lookup"><span data-stu-id="a997a-209">No</span></span> |
| <span data-ttu-id="a997a-210">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="a997a-210">storedProcedureParameters</span></span> |<span data-ttu-id="a997a-211">Parameters voor de opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="a997a-211">Parameters for the stored procedure.</span></span> |<span data-ttu-id="a997a-212">Naam/waarde-paren.</span><span class="sxs-lookup"><span data-stu-id="a997a-212">Name/value pairs.</span></span> <span data-ttu-id="a997a-213">Namen en hoofdlettergebruik van parameters moeten overeenkomen met de naam en het hoofdlettergebruik van de parameters van opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="a997a-213">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="a997a-214">Nee</span><span class="sxs-lookup"><span data-stu-id="a997a-214">No</span></span> |

<span data-ttu-id="a997a-215">Als de **sqlReaderQuery** is opgegeven voor de SqlSource met de kopieerbewerking wordt deze query uitgevoerd op basis van de bron van de SQL Server-Database om de gegevens te verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="a997a-215">If the **sqlReaderQuery** is specified for the SqlSource, the Copy Activity runs this query against the SQL Server Database source to get the data.</span></span>

<span data-ttu-id="a997a-216">U kunt ook een opgeslagen procedure opgeven door te geven de **sqlReaderStoredProcedureName** en **storedProcedureParameters** (als de opgeslagen procedure parameters nodig heeft).</span><span class="sxs-lookup"><span data-stu-id="a997a-216">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span>

<span data-ttu-id="a997a-217">Als u sqlReaderQuery of sqlReaderStoredProcedureName niet opgeeft, worden de kolommen die zijn gedefinieerd in de sectie structuur gebruikt voor het bouwen van een select-query uitvoeren op de SQL Server-Database.</span><span class="sxs-lookup"><span data-stu-id="a997a-217">If you do not specify either sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="a997a-218">Als de definitie van de gegevensset heeft niet de structuur, worden alle kolommen uit de tabel geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="a997a-218">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

> [!NOTE]
> <span data-ttu-id="a997a-219">Als u werkt met **sqlReaderStoredProcedureName**, moet u toch een waarde opgeven voor de **tableName** eigenschap in de JSON van de gegevensset.</span><span class="sxs-lookup"><span data-stu-id="a997a-219">When you use **sqlReaderStoredProcedureName**, you still need to specify a value for the **tableName** property in the dataset JSON.</span></span> <span data-ttu-id="a997a-220">Er zijn geen controles uitgevoerd voor deze tabel al.</span><span class="sxs-lookup"><span data-stu-id="a997a-220">There are no validations performed against this table though.</span></span>

### <a name="sqlsink"></a><span data-ttu-id="a997a-221">SqlSink</span><span class="sxs-lookup"><span data-stu-id="a997a-221">SqlSink</span></span>
<span data-ttu-id="a997a-222">**SqlSink** ondersteunt de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="a997a-222">**SqlSink** supports the following properties:</span></span>

| <span data-ttu-id="a997a-223">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="a997a-223">Property</span></span> | <span data-ttu-id="a997a-224">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="a997a-224">Description</span></span> | <span data-ttu-id="a997a-225">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="a997a-225">Allowed values</span></span> | <span data-ttu-id="a997a-226">Vereist</span><span class="sxs-lookup"><span data-stu-id="a997a-226">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="a997a-227">writeBatchTimeout</span><span class="sxs-lookup"><span data-stu-id="a997a-227">writeBatchTimeout</span></span> |<span data-ttu-id="a997a-228">Wachttijd voor de batch-insert-bewerking te voltooien voordat er een optreedt time-out.</span><span class="sxs-lookup"><span data-stu-id="a997a-228">Wait time for the batch insert operation to complete before it times out.</span></span> |<span data-ttu-id="a997a-229">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="a997a-229">timespan</span></span><br/><br/> <span data-ttu-id="a997a-230">Voorbeeld: "00: 30:00 ' (30 minuten).</span><span class="sxs-lookup"><span data-stu-id="a997a-230">Example: “00:30:00” (30 minutes).</span></span> |<span data-ttu-id="a997a-231">Nee</span><span class="sxs-lookup"><span data-stu-id="a997a-231">No</span></span> |
| <span data-ttu-id="a997a-232">writeBatchSize</span><span class="sxs-lookup"><span data-stu-id="a997a-232">writeBatchSize</span></span> |<span data-ttu-id="a997a-233">Voegt de gegevens in de SQL-tabel wanneer de buffergrootte writeBatchSize bereikt.</span><span class="sxs-lookup"><span data-stu-id="a997a-233">Inserts data into the SQL table when the buffer size reaches writeBatchSize.</span></span> |<span data-ttu-id="a997a-234">Geheel getal (aantal rijen)</span><span class="sxs-lookup"><span data-stu-id="a997a-234">Integer (number of rows)</span></span> |<span data-ttu-id="a997a-235">Nee (standaard: 10000)</span><span class="sxs-lookup"><span data-stu-id="a997a-235">No (default: 10000)</span></span> |
| <span data-ttu-id="a997a-236">sqlWriterCleanupScript</span><span class="sxs-lookup"><span data-stu-id="a997a-236">sqlWriterCleanupScript</span></span> |<span data-ttu-id="a997a-237">Query voor de Kopieeractiviteit uitvoeren zodat de gegevens van een bepaald segment wordt opgeschoond opgeven.</span><span class="sxs-lookup"><span data-stu-id="a997a-237">Specify query for Copy Activity to execute such that data of a specific slice is cleaned up.</span></span> <span data-ttu-id="a997a-238">Zie voor meer informatie [herhaalbare kopiëren](#repeatable-copy) sectie.</span><span class="sxs-lookup"><span data-stu-id="a997a-238">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="a997a-239">Een query-instructie.</span><span class="sxs-lookup"><span data-stu-id="a997a-239">A query statement.</span></span> |<span data-ttu-id="a997a-240">Nee</span><span class="sxs-lookup"><span data-stu-id="a997a-240">No</span></span> |
| <span data-ttu-id="a997a-241">sliceIdentifierColumnName</span><span class="sxs-lookup"><span data-stu-id="a997a-241">sliceIdentifierColumnName</span></span> |<span data-ttu-id="a997a-242">Geef de naam van de kolom voor de Kopieeractiviteit te vullen met de segment-ID automatisch gegenereerd en die wordt gebruikt voor het opschonen van de gegevens van een bepaald segment wanneer opnieuw uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a997a-242">Specify column name for Copy Activity to fill with auto generated slice identifier, which is used to clean up data of a specific slice when rerun.</span></span> <span data-ttu-id="a997a-243">Zie voor meer informatie [herhaalbare kopiëren](#repeatable-copy) sectie.</span><span class="sxs-lookup"><span data-stu-id="a997a-243">For more information, see [repeatable copy](#repeatable-copy) section.</span></span> |<span data-ttu-id="a997a-244">De naam van de kolom van een kolom met gegevenstype binary(32).</span><span class="sxs-lookup"><span data-stu-id="a997a-244">Column name of a column with data type of binary(32).</span></span> |<span data-ttu-id="a997a-245">Nee</span><span class="sxs-lookup"><span data-stu-id="a997a-245">No</span></span> |
| <span data-ttu-id="a997a-246">sqlWriterStoredProcedureName</span><span class="sxs-lookup"><span data-stu-id="a997a-246">sqlWriterStoredProcedureName</span></span> |<span data-ttu-id="a997a-247">Naam van de opgeslagen procedure die upserts (updates/INSERT) gegevens in de doeltabel.</span><span class="sxs-lookup"><span data-stu-id="a997a-247">Name of the stored procedure that upserts (updates/inserts) data into the target table.</span></span> |<span data-ttu-id="a997a-248">Naam van de opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="a997a-248">Name of the stored procedure.</span></span> |<span data-ttu-id="a997a-249">Nee</span><span class="sxs-lookup"><span data-stu-id="a997a-249">No</span></span> |
| <span data-ttu-id="a997a-250">storedProcedureParameters</span><span class="sxs-lookup"><span data-stu-id="a997a-250">storedProcedureParameters</span></span> |<span data-ttu-id="a997a-251">Parameters voor de opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="a997a-251">Parameters for the stored procedure.</span></span> |<span data-ttu-id="a997a-252">Naam/waarde-paren.</span><span class="sxs-lookup"><span data-stu-id="a997a-252">Name/value pairs.</span></span> <span data-ttu-id="a997a-253">Namen en hoofdlettergebruik van parameters moeten overeenkomen met de naam en het hoofdlettergebruik van de parameters van opgeslagen procedure.</span><span class="sxs-lookup"><span data-stu-id="a997a-253">Names and casing of parameters must match the names and casing of the stored procedure parameters.</span></span> |<span data-ttu-id="a997a-254">Nee</span><span class="sxs-lookup"><span data-stu-id="a997a-254">No</span></span> |
| <span data-ttu-id="a997a-255">sqlWriterTableType</span><span class="sxs-lookup"><span data-stu-id="a997a-255">sqlWriterTableType</span></span> |<span data-ttu-id="a997a-256">Type tabelnaam moet worden gebruikt in de opgeslagen procedure opgeven.</span><span class="sxs-lookup"><span data-stu-id="a997a-256">Specify table type name to be used in the stored procedure.</span></span> <span data-ttu-id="a997a-257">Kopieeractiviteit maakt u de gegevens worden verplaatst beschikbaar zijn in een tijdelijke tabel met dit tabeltype.</span><span class="sxs-lookup"><span data-stu-id="a997a-257">Copy activity makes the data being moved available in a temp table with this table type.</span></span> <span data-ttu-id="a997a-258">Code van de opgeslagen procedure kan de gegevens wordt gekopieerd met de bestaande gegevens vervolgens samenvoegen.</span><span class="sxs-lookup"><span data-stu-id="a997a-258">Stored procedure code can then merge the data being copied with existing data.</span></span> |<span data-ttu-id="a997a-259">Een typenaam van de tabel.</span><span class="sxs-lookup"><span data-stu-id="a997a-259">A table type name.</span></span> |<span data-ttu-id="a997a-260">Nee</span><span class="sxs-lookup"><span data-stu-id="a997a-260">No</span></span> |


## <a name="json-examples-for-copying-data-from-and-to-sql-server"></a><span data-ttu-id="a997a-261">JSON-voorbeelden voor het kopiëren van gegevens van en naar SQL Server</span><span class="sxs-lookup"><span data-stu-id="a997a-261">JSON examples for copying data from and to SQL Server</span></span>
<span data-ttu-id="a997a-262">De volgende voorbeelden geven voorbeeld JSON definities die u een pijplijn maken kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a997a-262">The following examples provide sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="a997a-263">De volgende voorbeelden laten zien hoe om gegevens te kopiëren naar en van SQL Server en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="a997a-263">The following samples show how to copy data to and from SQL Server and Azure Blob Storage.</span></span> <span data-ttu-id="a997a-264">Echter, de gegevens kunnen worden gekopieerd **rechtstreeks** uit een van de bronnen aan een van de PUT vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van de Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="a997a-264">However, data can be copied **directly** from any of sources to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span>     

## <a name="example-copy-data-from-sql-server-to-azure-blob"></a><span data-ttu-id="a997a-265">Voorbeeld: Gegevens kopiëren van SQL Server naar Azure Blob</span><span class="sxs-lookup"><span data-stu-id="a997a-265">Example: Copy data from SQL Server to Azure Blob</span></span>
<span data-ttu-id="a997a-266">Het volgende voorbeeld toont:</span><span class="sxs-lookup"><span data-stu-id="a997a-266">The following sample shows:</span></span>

1. <span data-ttu-id="a997a-267">Een gekoppelde service van het type [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a997a-267">A linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="a997a-268">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a997a-268">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="a997a-269">Invoer [gegevensset](data-factory-create-datasets.md) van het type [SqlServerTable](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a997a-269">An input [dataset](data-factory-create-datasets.md) of type [SqlServerTable](#dataset-properties).</span></span>
4. <span data-ttu-id="a997a-270">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a997a-270">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="a997a-271">De [pijplijn](data-factory-create-pipelines.md) met de kopieeractiviteit die gebruikmaakt van [SqlSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="a997a-271">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [SqlSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="a997a-272">Het voorbeeld kopieert timeseries gegevens uit een tabel met SQL Server naar een Azure-blob elk uur.</span><span class="sxs-lookup"><span data-stu-id="a997a-272">The sample copies time-series data from a SQL Server table to an Azure blob every hour.</span></span> <span data-ttu-id="a997a-273">De JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na de voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="a997a-273">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="a997a-274">Het instellen van de data management gateway als eerste stap.</span><span class="sxs-lookup"><span data-stu-id="a997a-274">As a first step, setup the data management gateway.</span></span> <span data-ttu-id="a997a-275">De instructies vindt u in de [verplaatsen van gegevens tussen lokale locaties en cloud](data-factory-move-data-between-onprem-and-cloud.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="a997a-275">The instructions are in the [moving data between on-premises locations and cloud](data-factory-move-data-between-onprem-and-cloud.md) article.</span></span>

<span data-ttu-id="a997a-276">**SQL Server gekoppeld-service**</span><span class="sxs-lookup"><span data-stu-id="a997a-276">**SQL Server linked service**</span></span>
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
<span data-ttu-id="a997a-277">**Azure Blob-opslag gekoppelde service**</span><span class="sxs-lookup"><span data-stu-id="a997a-277">**Azure Blob storage linked service**</span></span>

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
<span data-ttu-id="a997a-278">**SQL Server-invoergegevensset**</span><span class="sxs-lookup"><span data-stu-id="a997a-278">**SQL Server input dataset**</span></span>

<span data-ttu-id="a997a-279">Het voorbeeld wordt ervan uitgegaan dat u hebt een tabel 'MijnTabel' gemaakt in SQL Server en deze bevat een kolom met de naam 'timestampcolumn' voor de reeksgegevens.</span><span class="sxs-lookup"><span data-stu-id="a997a-279">The sample assumes you have created a table “MyTable” in SQL Server and it contains a column called “timestampcolumn” for time series data.</span></span> <span data-ttu-id="a997a-280">U kunt een query over meerdere tabellen binnen dezelfde database met behulp van een één gegevensset, maar één tabel moet worden gebruikt voor de gegevensset tableName typeProperty.</span><span class="sxs-lookup"><span data-stu-id="a997a-280">You can query over multiple tables within the same database using a single dataset, but a single table must be used for the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="a997a-281">Instelling 'extern': 'true' informeert Data Factory-service dat de dataset extern is aan de gegevensfactory en niet wordt geproduceerd door een activiteit in de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="a997a-281">Setting “external”: ”true” informs Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="a997a-282">**Azure Blob-uitvoergegevensset**</span><span class="sxs-lookup"><span data-stu-id="a997a-282">**Azure Blob output dataset**</span></span>

<span data-ttu-id="a997a-283">Gegevens worden geschreven naar een nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="a997a-283">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="a997a-284">Het pad naar de blob wordt dynamisch geëvalueerd op basis van de begintijd van het segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="a997a-284">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="a997a-285">Het mappad maakt gebruik van jaar, maand, dag en uur delen van de begintijd.</span><span class="sxs-lookup"><span data-stu-id="a997a-285">The folder path uses year, month, day, and hours parts of the start time.</span></span>

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
<span data-ttu-id="a997a-286">**Pijplijn met de kopieeractiviteit**</span><span class="sxs-lookup"><span data-stu-id="a997a-286">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="a997a-287">De pijplijn bevat een Kopieeractiviteit die is geconfigureerd voor gebruik van deze invoer- en uitvoergegevenssets en elk uur is gepland.</span><span class="sxs-lookup"><span data-stu-id="a997a-287">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="a997a-288">In de pijplijn-JSON-definitie de **bron** type is ingesteld op **SqlSource** en **sink** type is ingesteld op **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="a997a-288">In the pipeline JSON definition, the **source** type is set to **SqlSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="a997a-289">De SQL-query die is opgegeven voor de **SqlReaderQuery** eigenschap selecteert u de gegevens in het afgelopen uur te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="a997a-289">The SQL query specified for the **SqlReaderQuery** property selects the data in the past hour to copy.</span></span>

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
<span data-ttu-id="a997a-290">In dit voorbeeld **sqlReaderQuery** is opgegeven voor de SqlSource.</span><span class="sxs-lookup"><span data-stu-id="a997a-290">In this example, **sqlReaderQuery** is specified for the SqlSource.</span></span> <span data-ttu-id="a997a-291">De Kopieeractiviteit wordt deze query uitgevoerd op basis van de bron van de SQL Server-Database om de gegevens te verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="a997a-291">The Copy Activity runs this query against the SQL Server Database source to get the data.</span></span> <span data-ttu-id="a997a-292">U kunt ook een opgeslagen procedure opgeven door te geven de **sqlReaderStoredProcedureName** en **storedProcedureParameters** (als de opgeslagen procedure parameters nodig heeft).</span><span class="sxs-lookup"><span data-stu-id="a997a-292">Alternatively, you can specify a stored procedure by specifying the **sqlReaderStoredProcedureName** and **storedProcedureParameters** (if the stored procedure takes parameters).</span></span> <span data-ttu-id="a997a-293">De sqlReaderQuery kunt verwijzen naar meerdere tabellen in de database waarnaar wordt verwezen door de invoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="a997a-293">The sqlReaderQuery can reference multiple tables within the database referenced by the input dataset.</span></span> <span data-ttu-id="a997a-294">Het is niet beperkt tot alleen de tabel als de dataset tableName typeProperty instellen.</span><span class="sxs-lookup"><span data-stu-id="a997a-294">It is not limited to only the table set as the dataset's tableName typeProperty.</span></span>

<span data-ttu-id="a997a-295">Als u geen sqlReaderQuery of sqlReaderStoredProcedureName opgeeft, worden de kolommen die zijn gedefinieerd in de sectie structuur gebruikt voor het bouwen van een select-query uitvoeren op de SQL Server-Database.</span><span class="sxs-lookup"><span data-stu-id="a997a-295">If you do not specify sqlReaderQuery or sqlReaderStoredProcedureName, the columns defined in the structure section are used to build a select query to run against the SQL Server Database.</span></span> <span data-ttu-id="a997a-296">Als de definitie van de gegevensset heeft niet de structuur, worden alle kolommen uit de tabel geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="a997a-296">If the dataset definition does not have the structure, all columns are selected from the table.</span></span>

<span data-ttu-id="a997a-297">Zie de [Sql-bron](#sqlsource) sectie en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) voor de lijst met eigenschappen die ondersteund worden door SqlSource en BlobSink.</span><span class="sxs-lookup"><span data-stu-id="a997a-297">See the [Sql Source](#sqlsource) section and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) for the list of properties supported by SqlSource and BlobSink.</span></span>

## <a name="example-copy-data-from-azure-blob-to-sql-server"></a><span data-ttu-id="a997a-298">Voorbeeld: Gegevens kopiëren van Azure-Blob naar SQL Server</span><span class="sxs-lookup"><span data-stu-id="a997a-298">Example: Copy data from Azure Blob to SQL Server</span></span>
<span data-ttu-id="a997a-299">Het volgende voorbeeld toont:</span><span class="sxs-lookup"><span data-stu-id="a997a-299">The following sample shows:</span></span>

1. <span data-ttu-id="a997a-300">De gekoppelde service van het type [OnPremisesSqlServer](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a997a-300">The linked service of type [OnPremisesSqlServer](#linked-service-properties).</span></span>
2. <span data-ttu-id="a997a-301">De gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="a997a-301">The linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="a997a-302">Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a997a-302">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
4. <span data-ttu-id="a997a-303">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="a997a-303">An output [dataset](data-factory-create-datasets.md) of type [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="a997a-304">De [pijplijn](data-factory-create-pipelines.md) met de kopieeractiviteit die gebruikmaakt van [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) en [SqlSink](#sql-server-copy-activity-type-properties).</span><span class="sxs-lookup"><span data-stu-id="a997a-304">The [pipeline](data-factory-create-pipelines.md) with Copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [SqlSink](#sql-server-copy-activity-type-properties).</span></span>

<span data-ttu-id="a997a-305">De voorbeeld-kopieën timeseries gegevens van een Azure-blob naar een SQL Server tabel om het uur.</span><span class="sxs-lookup"><span data-stu-id="a997a-305">The sample copies time-series data from an Azure blob to a SQL Server table every hour.</span></span> <span data-ttu-id="a997a-306">De JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na de voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="a997a-306">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="a997a-307">**SQL Server gekoppeld-service**</span><span class="sxs-lookup"><span data-stu-id="a997a-307">**SQL Server linked service**</span></span>

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
<span data-ttu-id="a997a-308">**Azure Blob-opslag gekoppelde service**</span><span class="sxs-lookup"><span data-stu-id="a997a-308">**Azure Blob storage linked service**</span></span>

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
<span data-ttu-id="a997a-309">**Azure Blob-invoergegevensset**</span><span class="sxs-lookup"><span data-stu-id="a997a-309">**Azure Blob input dataset**</span></span>

<span data-ttu-id="a997a-310">Gegevens wordt opgehaald uit een nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="a997a-310">Data is picked up from a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="a997a-311">Pad en naam van de map voor de blob worden dynamisch geëvalueerd op basis van de begintijd van het segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="a997a-311">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="a997a-312">Het mappad gebruikt jaar, maand en dag deel uit van de begintijd en de bestandsnaam wordt gebruikt voor het uur deel van de begintijd.</span><span class="sxs-lookup"><span data-stu-id="a997a-312">The folder path uses year, month, and day part of the start time and file name uses the hour part of the start time.</span></span> <span data-ttu-id="a997a-313">"extern": "true" instelling informeert de Data Factory-service dat de dataset extern is aan de gegevensfactory en niet wordt geproduceerd door een activiteit in de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="a997a-313">“external”: “true” setting informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="a997a-314">**Gegevensset voor SQL Server-uitvoer**</span><span class="sxs-lookup"><span data-stu-id="a997a-314">**SQL Server output dataset**</span></span>

<span data-ttu-id="a997a-315">Het voorbeeld worden gegevens gekopieerd naar een tabel met de naam "MijnTabel" in SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a997a-315">The sample copies data to a table named “MyTable” in SQL Server.</span></span> <span data-ttu-id="a997a-316">De tabel in SQL-Server met hetzelfde aantal kolommen maken zoals u verwacht dat de Blob-CSV-bestand bevatten.</span><span class="sxs-lookup"><span data-stu-id="a997a-316">Create the table in SQL Server with the same number of columns as you expect the Blob CSV file to contain.</span></span> <span data-ttu-id="a997a-317">Nieuwe rijen worden toegevoegd aan de tabel om het uur.</span><span class="sxs-lookup"><span data-stu-id="a997a-317">New rows are added to the table every hour.</span></span>

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
<span data-ttu-id="a997a-318">**Pijplijn met de kopieeractiviteit**</span><span class="sxs-lookup"><span data-stu-id="a997a-318">**Pipeline with Copy activity**</span></span>

<span data-ttu-id="a997a-319">De pijplijn bevat een Kopieeractiviteit die is geconfigureerd voor gebruik van deze invoer- en uitvoergegevenssets en elk uur is gepland.</span><span class="sxs-lookup"><span data-stu-id="a997a-319">The pipeline contains a Copy Activity that is configured to use these input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="a997a-320">In de pijplijn-JSON-definitie de **bron** type is ingesteld op **BlobSource** en **sink** type is ingesteld op **SqlSink**.</span><span class="sxs-lookup"><span data-stu-id="a997a-320">In the pipeline JSON definition, the **source** type is set to **BlobSource** and **sink** type is set to **SqlSink**.</span></span>

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

## <a name="troubleshooting-connection-issues"></a><span data-ttu-id="a997a-321">Verbindingsproblemen oplossen</span><span class="sxs-lookup"><span data-stu-id="a997a-321">Troubleshooting connection issues</span></span>
1. <span data-ttu-id="a997a-322">Configureer uw SQL Server om externe verbindingen te accepteren.</span><span class="sxs-lookup"><span data-stu-id="a997a-322">Configure your SQL Server to accept remote connections.</span></span> <span data-ttu-id="a997a-323">Start **SQL Server Management Studio**, met de rechtermuisknop op **server**, en klik op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="a997a-323">Launch **SQL Server Management Studio**, right-click **server**, and click **Properties**.</span></span> <span data-ttu-id="a997a-324">Selecteer **verbindingen** uit de lijst en het selectievakje **toestaan van externe verbindingen met de server**.</span><span class="sxs-lookup"><span data-stu-id="a997a-324">Select **Connections** from the list and check **Allow remote connections to the server**.</span></span>

    ![Externe verbindingen inschakelen](./media/data-factory-sqlserver-connector/AllowRemoteConnections.png)

    <span data-ttu-id="a997a-326">Zie [de serverconfiguratieoptie voor externe toegang configureren](https://msdn.microsoft.com/library/ms191464.aspx) voor gedetailleerde stappen.</span><span class="sxs-lookup"><span data-stu-id="a997a-326">See [Configure the remote access Server Configuration Option](https://msdn.microsoft.com/library/ms191464.aspx) for detailed steps.</span></span>
2. <span data-ttu-id="a997a-327">Start **SQL Server Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="a997a-327">Launch **SQL Server Configuration Manager**.</span></span> <span data-ttu-id="a997a-328">Vouw **SQL Server-netwerkconfiguratie** voor het exemplaar dat u wilt gebruiken en selecteer **protocollen voor MSSQLSERVER**.</span><span class="sxs-lookup"><span data-stu-id="a997a-328">Expand **SQL Server Network Configuration** for the instance you want, and select **Protocols for MSSQLSERVER**.</span></span> <span data-ttu-id="a997a-329">U ziet protocollen in het rechterdeelvenster.</span><span class="sxs-lookup"><span data-stu-id="a997a-329">You should see protocols in the right-pane.</span></span> <span data-ttu-id="a997a-330">TCP/IP inschakelen met de rechtermuisknop op **TCP/IP** en te klikken op **inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="a997a-330">Enable TCP/IP by right-clicking **TCP/IP** and clicking **Enable**.</span></span>

    ![TCP/IP inschakelen](./media/data-factory-sqlserver-connector/EnableTCPProptocol.png)

    <span data-ttu-id="a997a-332">Zie [in- of uitschakelen van een Server netwerkprotocol](https://msdn.microsoft.com/library/ms191294.aspx) voor meer informatie en alternatieve manieren TCP/IP-protocol in te schakelen.</span><span class="sxs-lookup"><span data-stu-id="a997a-332">See [Enable or Disable a Server Network Protocol](https://msdn.microsoft.com/library/ms191294.aspx) for details and alternate ways of enabling TCP/IP protocol.</span></span>
3. <span data-ttu-id="a997a-333">Dubbelklik in het venster dezelfde **TCP/IP** starten **TCP/IP-eigenschappen** venster.</span><span class="sxs-lookup"><span data-stu-id="a997a-333">In the same window, double-click **TCP/IP** to launch **TCP/IP Properties** window.</span></span>
4. <span data-ttu-id="a997a-334">Overschakelen naar de **IP-adressen** tabblad.</span><span class="sxs-lookup"><span data-stu-id="a997a-334">Switch to the **IP Addresses** tab.</span></span> <span data-ttu-id="a997a-335">Schuif helemaal naar Zie **IPAll** sectie.</span><span class="sxs-lookup"><span data-stu-id="a997a-335">Scroll down to see **IPAll** section.</span></span> <span data-ttu-id="a997a-336">Noteer de ** TCP-poort ** (standaardwaarde is **1433**).</span><span class="sxs-lookup"><span data-stu-id="a997a-336">Note down the **TCP Port **(default is **1433**).</span></span>
5. <span data-ttu-id="a997a-337">Maak een **regel voor de Windows Firewall** op de computer waarmee binnenkomend verkeer via deze poort.</span><span class="sxs-lookup"><span data-stu-id="a997a-337">Create a **rule for the Windows Firewall** on the machine to allow incoming traffic through this port.</span></span>  
6. <span data-ttu-id="a997a-338">**Verbinding controleren**: voor verbinding met de volledig gekwalificeerde naam SQL-Server, SQL Server Management Studio uit een andere computer te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a997a-338">**Verify connection**: To connect to the SQL Server using fully qualified name, use SQL Server Management Studio from a different machine.</span></span> <span data-ttu-id="a997a-339">Bijvoorbeeld: '<machine>.<domain>. Corp.<company>.com, 1433. "</span><span class="sxs-lookup"><span data-stu-id="a997a-339">For example: "<machine>.<domain>.corp.<company>.com,1433."</span></span>

   > [!IMPORTANT]

   > <span data-ttu-id="a997a-340">Zie [gegevens verplaatsen tussen lokale bronnen en de cloud met Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) voor gedetailleerde informatie.</span><span class="sxs-lookup"><span data-stu-id="a997a-340">See [Move data between on-premises sources and the cloud with Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) for detailed information.</span></span>
   >
   > <span data-ttu-id="a997a-341">Zie [gateway problemen](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) voor tips over het oplossen van verbinding of gateway gerelateerde problemen.</span><span class="sxs-lookup"><span data-stu-id="a997a-341">See [Troubleshoot gateway issues](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) for tips on troubleshooting connection/gateway related issues.</span></span>
   >
   >


## <a name="identity-columns-in-the-target-database"></a><span data-ttu-id="a997a-342">Id-kolommen in de doeldatabase</span><span class="sxs-lookup"><span data-stu-id="a997a-342">Identity columns in the target database</span></span>
<span data-ttu-id="a997a-343">Deze sectie bevat een voorbeeld waarin gegevens uit een brontabel met geen identiteitskolom naar een doeltabel met een identiteitskolom kopieert.</span><span class="sxs-lookup"><span data-stu-id="a997a-343">This section provides an example that copies data from a source table with no identity column to a destination table with an identity column.</span></span>

<span data-ttu-id="a997a-344">**Brontabel:**</span><span class="sxs-lookup"><span data-stu-id="a997a-344">**Source table:**</span></span>

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
<span data-ttu-id="a997a-345">**Doeltabel:**</span><span class="sxs-lookup"><span data-stu-id="a997a-345">**Destination table:**</span></span>

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

<span data-ttu-id="a997a-346">U ziet dat de doeltabel een identiteitskolom.</span><span class="sxs-lookup"><span data-stu-id="a997a-346">Notice that the target table has an identity column.</span></span>

<span data-ttu-id="a997a-347">**Bron gegevensset JSON-definitie**</span><span class="sxs-lookup"><span data-stu-id="a997a-347">**Source dataset JSON definition**</span></span>

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
<span data-ttu-id="a997a-348">**Doel-dataset JSON-definitie**</span><span class="sxs-lookup"><span data-stu-id="a997a-348">**Destination dataset JSON definition**</span></span>

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

<span data-ttu-id="a997a-349">Merk op dat als de bron en doel-tabel verschillende schema's zijn (doel heeft een extra kolom met de identiteit).</span><span class="sxs-lookup"><span data-stu-id="a997a-349">Notice that as your source and target table have different schema (target has an additional column with identity).</span></span> <span data-ttu-id="a997a-350">In dit scenario moet u opgeven **structuur** eigenschap in de definitie van de gegevensset doel, waaronder de identiteitskolom niet.</span><span class="sxs-lookup"><span data-stu-id="a997a-350">In this scenario, you need to specify **structure** property in the target dataset definition, which doesn’t include the identity column.</span></span>

## <a name="invoke-stored-procedure-from-sql-sink"></a><span data-ttu-id="a997a-351">Aanroepen van opgeslagen procedure uit SQL-sink</span><span class="sxs-lookup"><span data-stu-id="a997a-351">Invoke stored procedure from SQL sink</span></span>
<span data-ttu-id="a997a-352">Zie [opgeslagen procedure voor SQL-sink aanroepen in de kopieerbewerking](data-factory-invoke-stored-procedure-from-copy-activity.md) artikel voor een voorbeeld van een opgeslagen procedure van SQL-sink in een kopieeractiviteit van een pijplijn wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="a997a-352">See [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) article for an example of invoking a stored procedure from SQL sink in a copy activity of a pipeline.</span></span>

## <a name="type-mapping-for-sql-server"></a><span data-ttu-id="a997a-353">Toewijzing van het type voor SQL server</span><span class="sxs-lookup"><span data-stu-id="a997a-353">Type mapping for SQL server</span></span>
<span data-ttu-id="a997a-354">Zoals vermeld in de [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel de kopieerbewerking wordt automatische typeconversies van brontypen opvangen typen met de volgende stappen 2-benadering uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="a997a-354">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, the Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="a997a-355">Systeemeigen brontypen converteren naar .NET-type</span><span class="sxs-lookup"><span data-stu-id="a997a-355">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="a997a-356">Converteren van .NET-type naar systeemeigen sink-type</span><span class="sxs-lookup"><span data-stu-id="a997a-356">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="a997a-357">Bij het verplaatsen van gegevens naar & uit SQL server, worden de volgende toewijzingen gebruikt vanuit de SQL-type aan .NET-type en vice versa.</span><span class="sxs-lookup"><span data-stu-id="a997a-357">When moving data to & from SQL server, the following mappings are used from SQL type to .NET type and vice versa.</span></span>

<span data-ttu-id="a997a-358">De toewijzing is hetzelfde als de SQL Server gegevenstypetoewijzing voor ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="a997a-358">The mapping is same as the SQL Server Data Type Mapping for ADO.NET.</span></span>

| <span data-ttu-id="a997a-359">SQL Server Database Engine-type</span><span class="sxs-lookup"><span data-stu-id="a997a-359">SQL Server Database Engine type</span></span> | <span data-ttu-id="a997a-360">.NET framework-type</span><span class="sxs-lookup"><span data-stu-id="a997a-360">.NET Framework type</span></span> |
| --- | --- |
| <span data-ttu-id="a997a-361">bigint</span><span class="sxs-lookup"><span data-stu-id="a997a-361">bigint</span></span> |<span data-ttu-id="a997a-362">Int64</span><span class="sxs-lookup"><span data-stu-id="a997a-362">Int64</span></span> |
| <span data-ttu-id="a997a-363">Binaire</span><span class="sxs-lookup"><span data-stu-id="a997a-363">binary</span></span> |<span data-ttu-id="a997a-364">Byte]</span><span class="sxs-lookup"><span data-stu-id="a997a-364">Byte[]</span></span> |
| <span data-ttu-id="a997a-365">bits</span><span class="sxs-lookup"><span data-stu-id="a997a-365">bit</span></span> |<span data-ttu-id="a997a-366">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="a997a-366">Boolean</span></span> |
| <span data-ttu-id="a997a-367">CHAR</span><span class="sxs-lookup"><span data-stu-id="a997a-367">char</span></span> |<span data-ttu-id="a997a-368">Tekenreeks, Char]</span><span class="sxs-lookup"><span data-stu-id="a997a-368">String, Char[]</span></span> |
| <span data-ttu-id="a997a-369">Datum</span><span class="sxs-lookup"><span data-stu-id="a997a-369">date</span></span> |<span data-ttu-id="a997a-370">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="a997a-370">DateTime</span></span> |
| <span data-ttu-id="a997a-371">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="a997a-371">Datetime</span></span> |<span data-ttu-id="a997a-372">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="a997a-372">DateTime</span></span> |
| <span data-ttu-id="a997a-373">datetime2</span><span class="sxs-lookup"><span data-stu-id="a997a-373">datetime2</span></span> |<span data-ttu-id="a997a-374">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="a997a-374">DateTime</span></span> |
| <span data-ttu-id="a997a-375">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="a997a-375">Datetimeoffset</span></span> |<span data-ttu-id="a997a-376">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="a997a-376">DateTimeOffset</span></span> |
| <span data-ttu-id="a997a-377">Decimale</span><span class="sxs-lookup"><span data-stu-id="a997a-377">Decimal</span></span> |<span data-ttu-id="a997a-378">Decimale</span><span class="sxs-lookup"><span data-stu-id="a997a-378">Decimal</span></span> |
| <span data-ttu-id="a997a-379">FILESTREAM-kenmerk (varbinary(max))</span><span class="sxs-lookup"><span data-stu-id="a997a-379">FILESTREAM attribute (varbinary(max))</span></span> |<span data-ttu-id="a997a-380">Byte]</span><span class="sxs-lookup"><span data-stu-id="a997a-380">Byte[]</span></span> |
| <span data-ttu-id="a997a-381">Float</span><span class="sxs-lookup"><span data-stu-id="a997a-381">Float</span></span> |<span data-ttu-id="a997a-382">dubbele</span><span class="sxs-lookup"><span data-stu-id="a997a-382">Double</span></span> |
| <span data-ttu-id="a997a-383">Afbeelding</span><span class="sxs-lookup"><span data-stu-id="a997a-383">image</span></span> |<span data-ttu-id="a997a-384">Byte]</span><span class="sxs-lookup"><span data-stu-id="a997a-384">Byte[]</span></span> |
| <span data-ttu-id="a997a-385">int</span><span class="sxs-lookup"><span data-stu-id="a997a-385">int</span></span> |<span data-ttu-id="a997a-386">Int32</span><span class="sxs-lookup"><span data-stu-id="a997a-386">Int32</span></span> |
| <span data-ttu-id="a997a-387">Money</span><span class="sxs-lookup"><span data-stu-id="a997a-387">money</span></span> |<span data-ttu-id="a997a-388">Decimale</span><span class="sxs-lookup"><span data-stu-id="a997a-388">Decimal</span></span> |
| <span data-ttu-id="a997a-389">nchar</span><span class="sxs-lookup"><span data-stu-id="a997a-389">nchar</span></span> |<span data-ttu-id="a997a-390">Tekenreeks, Char]</span><span class="sxs-lookup"><span data-stu-id="a997a-390">String, Char[]</span></span> |
| <span data-ttu-id="a997a-391">ntext</span><span class="sxs-lookup"><span data-stu-id="a997a-391">ntext</span></span> |<span data-ttu-id="a997a-392">Tekenreeks, Char]</span><span class="sxs-lookup"><span data-stu-id="a997a-392">String, Char[]</span></span> |
| <span data-ttu-id="a997a-393">numerieke</span><span class="sxs-lookup"><span data-stu-id="a997a-393">numeric</span></span> |<span data-ttu-id="a997a-394">Decimale</span><span class="sxs-lookup"><span data-stu-id="a997a-394">Decimal</span></span> |
| <span data-ttu-id="a997a-395">nvarchar</span><span class="sxs-lookup"><span data-stu-id="a997a-395">nvarchar</span></span> |<span data-ttu-id="a997a-396">Tekenreeks, Char]</span><span class="sxs-lookup"><span data-stu-id="a997a-396">String, Char[]</span></span> |
| <span data-ttu-id="a997a-397">echte</span><span class="sxs-lookup"><span data-stu-id="a997a-397">real</span></span> |<span data-ttu-id="a997a-398">Één</span><span class="sxs-lookup"><span data-stu-id="a997a-398">Single</span></span> |
| <span data-ttu-id="a997a-399">ROWVERSION</span><span class="sxs-lookup"><span data-stu-id="a997a-399">rowversion</span></span> |<span data-ttu-id="a997a-400">Byte]</span><span class="sxs-lookup"><span data-stu-id="a997a-400">Byte[]</span></span> |
| <span data-ttu-id="a997a-401">smalldatetime</span><span class="sxs-lookup"><span data-stu-id="a997a-401">smalldatetime</span></span> |<span data-ttu-id="a997a-402">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="a997a-402">DateTime</span></span> |
| <span data-ttu-id="a997a-403">smallint</span><span class="sxs-lookup"><span data-stu-id="a997a-403">smallint</span></span> |<span data-ttu-id="a997a-404">Int16</span><span class="sxs-lookup"><span data-stu-id="a997a-404">Int16</span></span> |
| <span data-ttu-id="a997a-405">smallmoney</span><span class="sxs-lookup"><span data-stu-id="a997a-405">smallmoney</span></span> |<span data-ttu-id="a997a-406">Decimale</span><span class="sxs-lookup"><span data-stu-id="a997a-406">Decimal</span></span> |
| <span data-ttu-id="a997a-407">sql_variant</span><span class="sxs-lookup"><span data-stu-id="a997a-407">sql_variant</span></span> |<span data-ttu-id="a997a-408">Object *</span><span class="sxs-lookup"><span data-stu-id="a997a-408">Object *</span></span> |
| <span data-ttu-id="a997a-409">Tekst</span><span class="sxs-lookup"><span data-stu-id="a997a-409">text</span></span> |<span data-ttu-id="a997a-410">Tekenreeks, Char]</span><span class="sxs-lookup"><span data-stu-id="a997a-410">String, Char[]</span></span> |
| <span data-ttu-id="a997a-411">tijd</span><span class="sxs-lookup"><span data-stu-id="a997a-411">time</span></span> |<span data-ttu-id="a997a-412">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="a997a-412">TimeSpan</span></span> |
| <span data-ttu-id="a997a-413">tijdstempel</span><span class="sxs-lookup"><span data-stu-id="a997a-413">timestamp</span></span> |<span data-ttu-id="a997a-414">Byte]</span><span class="sxs-lookup"><span data-stu-id="a997a-414">Byte[]</span></span> |
| <span data-ttu-id="a997a-415">tinyint</span><span class="sxs-lookup"><span data-stu-id="a997a-415">tinyint</span></span> |<span data-ttu-id="a997a-416">Byte</span><span class="sxs-lookup"><span data-stu-id="a997a-416">Byte</span></span> |
| <span data-ttu-id="a997a-417">uniqueidentifier</span><span class="sxs-lookup"><span data-stu-id="a997a-417">uniqueidentifier</span></span> |<span data-ttu-id="a997a-418">GUID</span><span class="sxs-lookup"><span data-stu-id="a997a-418">Guid</span></span> |
| <span data-ttu-id="a997a-419">varbinary</span><span class="sxs-lookup"><span data-stu-id="a997a-419">varbinary</span></span> |<span data-ttu-id="a997a-420">Byte]</span><span class="sxs-lookup"><span data-stu-id="a997a-420">Byte[]</span></span> |
| <span data-ttu-id="a997a-421">varchar</span><span class="sxs-lookup"><span data-stu-id="a997a-421">varchar</span></span> |<span data-ttu-id="a997a-422">Tekenreeks, Char]</span><span class="sxs-lookup"><span data-stu-id="a997a-422">String, Char[]</span></span> |
| <span data-ttu-id="a997a-423">xml</span><span class="sxs-lookup"><span data-stu-id="a997a-423">xml</span></span> |<span data-ttu-id="a997a-424">XML</span><span class="sxs-lookup"><span data-stu-id="a997a-424">Xml</span></span> |

## <a name="mapping-source-to-sink-columns"></a><span data-ttu-id="a997a-425">Toewijzingsbron opvangen kolommen</span><span class="sxs-lookup"><span data-stu-id="a997a-425">Mapping source to sink columns</span></span>
<span data-ttu-id="a997a-426">Zie het toewijzen van kolommen uit de bron-gegevensset naar kolommen uit de dataset sink [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="a997a-426">To map columns from source dataset to columns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-copy"></a><span data-ttu-id="a997a-427">Herhaalbare kopiëren</span><span class="sxs-lookup"><span data-stu-id="a997a-427">Repeatable copy</span></span>
<span data-ttu-id="a997a-428">Bij het kopiëren van gegevens naar SQL Server-Database, de kopieeractiviteit worden gegevens toegevoegd aan de tabel sink standaard.</span><span class="sxs-lookup"><span data-stu-id="a997a-428">When copying data to SQL Server Database, the copy activity appends data to the sink table by default.</span></span> <span data-ttu-id="a997a-429">Om uit te voeren in plaats daarvan een UPSERT, Zie [Repeatable schrijven naar SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) artikel.</span><span class="sxs-lookup"><span data-stu-id="a997a-429">To perform an UPSERT instead,  See [Repeatable write to SqlSink](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) article.</span></span> 

<span data-ttu-id="a997a-430">Bij het kopiëren van gegevens van relationele gegevens worden opgeslagen, moet u herhaalbaarheid Houd in gedachten om te voorkomen dat ongewenste resultaten.</span><span class="sxs-lookup"><span data-stu-id="a997a-430">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="a997a-431">In Azure Data Factory, kunt u een segment handmatig opnieuw.</span><span class="sxs-lookup"><span data-stu-id="a997a-431">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="a997a-432">U kunt ook een beleid voor opnieuw proberen voor een gegevensset configureren zodat een segment wordt opnieuw uitgevoerd wanneer een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="a997a-432">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="a997a-433">Wanneer een segment opnieuw in beide gevallen wordt uitgevoerd, moet u ervoor zorgen dat dezelfde gegevens is gelezen ongeacht hoe vaak een segment wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a997a-433">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="a997a-434">Zie [Repeatable van relationele bronnen lezen](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="a997a-434">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="a997a-435">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="a997a-435">Performance and Tuning</span></span>
<span data-ttu-id="a997a-436">Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) voor meer informatie over de belangrijkste factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren om te optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="a997a-436">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
