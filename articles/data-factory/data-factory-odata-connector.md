---
title: Gegevens uit OData-bronnen verplaatsen | Microsoft Docs
description: Meer informatie over het verplaatsen van gegevens uit OData-bronnen met behulp van Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: de28fa56-3204-4546-a4df-21a21de43ed7
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: 624b6c8f317477d83539392c6c2f15c2dc69d401
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="move-data-from-a-odata-source-using-azure-data-factory"></a><span data-ttu-id="60d77-103">Verplaatsen van gegevens uit een OData-bron met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="60d77-103">Move data From a OData source using Azure Data Factory</span></span>
<span data-ttu-id="60d77-104">Dit artikel wordt uitgelegd hoe u de Kopieeractiviteit in Azure Data Factory om gegevens te verplaatsen van een OData-bron.</span><span class="sxs-lookup"><span data-stu-id="60d77-104">This article explains how to use the Copy Activity in Azure Data Factory to move data from an OData source.</span></span> <span data-ttu-id="60d77-105">Dit is gebaseerd op de [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, hetgeen een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit toont.</span><span class="sxs-lookup"><span data-stu-id="60d77-105">It builds on the [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with the copy activity.</span></span>

<span data-ttu-id="60d77-106">U kunt gegevens uit een OData-bron kopiëren naar een ondersteunde sink-gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="60d77-106">You can copy data from an OData source to any supported sink data store.</span></span> <span data-ttu-id="60d77-107">Zie voor een lijst met gegevensarchieven als PUT wordt ondersteund door de kopieeractiviteit, de [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel.</span><span class="sxs-lookup"><span data-stu-id="60d77-107">For a list of data stores supported as sinks by the copy activity, see the [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="60d77-108">Data factory ondersteunt momenteel alleen zwevend gegevens uit een OData-bron naar andere gegevensarchieven, maar niet voor het verplaatsen van gegevens uit andere gegevensarchieven naar een OData-bron.</span><span class="sxs-lookup"><span data-stu-id="60d77-108">Data factory currently supports only moving data from an OData source to other data stores, but not for moving data from other data stores to an OData source.</span></span> 

## <a name="supported-versions-and-authentication-types"></a><span data-ttu-id="60d77-109">Ondersteunde versies en verificatietypen</span><span class="sxs-lookup"><span data-stu-id="60d77-109">Supported versions and authentication types</span></span>
<span data-ttu-id="60d77-110">Deze OData-connector ondersteuning voor OData-versie 3.0 en 4.0 en u kunt kopiëren van gegevens uit zowel cloud OData en lokale OData-bronnen.</span><span class="sxs-lookup"><span data-stu-id="60d77-110">This OData connector support OData version 3.0 and 4.0, and you can copy data from both cloud OData and on-premises OData sources.</span></span> <span data-ttu-id="60d77-111">Voor de laatste moet u de Data Management Gateway installeren.</span><span class="sxs-lookup"><span data-stu-id="60d77-111">For the latter, you need to install the Data Management Gateway.</span></span> <span data-ttu-id="60d77-112">Zie [gegevens verplaatsen tussen on-premises en cloud](data-factory-move-data-between-onprem-and-cloud.md) voor meer informatie over Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="60d77-112">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

<span data-ttu-id="60d77-113">Hieronder verificatie worden typen ondersteund:</span><span class="sxs-lookup"><span data-stu-id="60d77-113">Below authentication types are supported:</span></span>

* <span data-ttu-id="60d77-114">Voor toegang tot **cloud** OData-feed, kunt u anoniem, basis (gebruikersnaam en wachtwoord) of Azure Active Directory op basis van OAuth-verificatie.</span><span class="sxs-lookup"><span data-stu-id="60d77-114">To access **cloud** OData feed, you can use anonymous, basic (user name and password), or Azure Active Directory based OAuth authentication.</span></span>
* <span data-ttu-id="60d77-115">Voor toegang tot **lokale** OData-feed, kunt u anoniem, basis (gebruikersnaam en wachtwoord) of Windows-verificatie.</span><span class="sxs-lookup"><span data-stu-id="60d77-115">To access **on-premises** OData feed, you can use anonymous, basic (user name and password), or Windows authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="60d77-116">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="60d77-116">Getting started</span></span>
<span data-ttu-id="60d77-117">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens uit een OData-bron verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="60d77-117">You can create a pipeline with a copy activity that moves data from an OData source by using different tools/APIs.</span></span>

<span data-ttu-id="60d77-118">De eenvoudigste manier om een pijplijn maken is met de **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="60d77-118">The easiest way to create a pipeline is to use the **Copy Wizard**.</span></span> <span data-ttu-id="60d77-119">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met de wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="60d77-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using the Copy data wizard.</span></span>

<span data-ttu-id="60d77-120">U kunt ook de volgende hulpprogramma's gebruiken voor het maken van een pijplijn: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon**, **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="60d77-120">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="60d77-121">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies voor een pijplijn maken met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="60d77-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span> 

<span data-ttu-id="60d77-122">Of u de hulpprogramma's of API's gebruiken, moet u de volgende stappen voor het maken van een pijplijn die de gegevens vanuit een brongegevensarchief naar een gegevensarchief sink verplaatst uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="60d77-122">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span> 

1. <span data-ttu-id="60d77-123">Maak **gekoppelde services** slaat om invoer- en gegevens te koppelen aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="60d77-123">Create **linked services** to link input and output data stores to your data factory.</span></span>
2. <span data-ttu-id="60d77-124">Maak **gegevenssets** vertegenwoordigt de invoer- en -gegevens voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="60d77-124">Create **datasets** to represent input and output data for the copy operation.</span></span> 
3. <span data-ttu-id="60d77-125">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="60d77-125">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="60d77-126">Wanneer u de wizard gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="60d77-126">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="60d77-127">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van de JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="60d77-127">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="60d77-128">Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die worden gebruikt om gegevens te kopiëren van een OData-bron [JSON-voorbeeld: gegevens kopiëren van de OData-bron naar Azure Blob](#json-example-copy-data-from-odata-source-to-azure-blob) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="60d77-128">For a sample with JSON definitions for Data Factory entities that are used to copy data from an OData source, see [JSON example: Copy data from OData source to Azure Blob](#json-example-copy-data-from-odata-source-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="60d77-129">De volgende secties bevatten informatie over de JSON-eigenschappen die worden gebruikt voor het definiëren van Data Factory-entiteiten specifieke OData-bron:</span><span class="sxs-lookup"><span data-stu-id="60d77-129">The following sections provide details about JSON properties that are used to define Data Factory entities specific to OData source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="60d77-130">Eigenschappen van de gekoppelde Service</span><span class="sxs-lookup"><span data-stu-id="60d77-130">Linked Service properties</span></span>
<span data-ttu-id="60d77-131">De volgende tabel bevat een beschrijving voor JSON-elementen die specifiek zijn voor de gekoppelde OData-service.</span><span class="sxs-lookup"><span data-stu-id="60d77-131">The following table provides description for JSON elements specific to OData linked service.</span></span>

| <span data-ttu-id="60d77-132">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="60d77-132">Property</span></span> | <span data-ttu-id="60d77-133">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="60d77-133">Description</span></span> | <span data-ttu-id="60d77-134">Vereist</span><span class="sxs-lookup"><span data-stu-id="60d77-134">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="60d77-135">type</span><span class="sxs-lookup"><span data-stu-id="60d77-135">type</span></span> |<span data-ttu-id="60d77-136">De eigenschap type moet worden ingesteld op: **OData**</span><span class="sxs-lookup"><span data-stu-id="60d77-136">The type property must be set to: **OData**</span></span> |<span data-ttu-id="60d77-137">Ja</span><span class="sxs-lookup"><span data-stu-id="60d77-137">Yes</span></span> |
| <span data-ttu-id="60d77-138">URL</span><span class="sxs-lookup"><span data-stu-id="60d77-138">url</span></span> |<span data-ttu-id="60d77-139">URL van de OData-service.</span><span class="sxs-lookup"><span data-stu-id="60d77-139">Url of the OData service.</span></span> |<span data-ttu-id="60d77-140">Ja</span><span class="sxs-lookup"><span data-stu-id="60d77-140">Yes</span></span> |
| <span data-ttu-id="60d77-141">authenticationType</span><span class="sxs-lookup"><span data-stu-id="60d77-141">authenticationType</span></span> |<span data-ttu-id="60d77-142">Het soort verificatie gebruikt voor verbinding met de OData-bron.</span><span class="sxs-lookup"><span data-stu-id="60d77-142">Type of authentication used to connect to the OData source.</span></span> <br/><br/> <span data-ttu-id="60d77-143">Mogelijke waarden zijn voor OData-cloud, anoniem, basis en OAuth (Opmerking momenteel alleen ondersteuning voor Azure Data Factory Azure Active Directory op basis van OAuth).</span><span class="sxs-lookup"><span data-stu-id="60d77-143">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="60d77-144">Mogelijke waarden zijn voor lokale OData, anoniem, basis en Windows.</span><span class="sxs-lookup"><span data-stu-id="60d77-144">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="60d77-145">Ja</span><span class="sxs-lookup"><span data-stu-id="60d77-145">Yes</span></span> |
| <span data-ttu-id="60d77-146">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="60d77-146">username</span></span> |<span data-ttu-id="60d77-147">Geef de gebruikersnaam als u basisverificatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="60d77-147">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="60d77-148">Ja (alleen als u basisverificatie gebruikt)</span><span class="sxs-lookup"><span data-stu-id="60d77-148">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="60d77-149">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="60d77-149">password</span></span> |<span data-ttu-id="60d77-150">Wachtwoord voor het gebruikersaccount dat u hebt opgegeven voor de gebruikersnaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="60d77-150">Specify password for the user account you specified for the username.</span></span> |<span data-ttu-id="60d77-151">Ja (alleen als u basisverificatie gebruikt)</span><span class="sxs-lookup"><span data-stu-id="60d77-151">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="60d77-152">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="60d77-152">authorizedCredential</span></span> |<span data-ttu-id="60d77-153">Als u van OAuth gebruikmaakt, klikt u op **autoriseren** in de Data Factory-Wizard kopiëren of Editor en voer uw referenties en vervolgens de waarde van deze eigenschap wordt niet automatisch wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="60d77-153">If you are using OAuth, click **Authorize** button in the Data Factory Copy Wizard or Editor and enter your credential, then the value of this property will be auto-generated.</span></span> |<span data-ttu-id="60d77-154">Ja (alleen als u OAuth-verificatie gebruikt)</span><span class="sxs-lookup"><span data-stu-id="60d77-154">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="60d77-155">gatewayName</span><span class="sxs-lookup"><span data-stu-id="60d77-155">gatewayName</span></span> |<span data-ttu-id="60d77-156">Naam van de gateway die voor de Data Factory-service verbinding maken met het lokale OData-service wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="60d77-156">Name of the gateway that the Data Factory service should use to connect to the on-premises OData service.</span></span> <span data-ttu-id="60d77-157">Geef alleen als u gegevens uit een on-premises OData-bron kopiëren wilt.</span><span class="sxs-lookup"><span data-stu-id="60d77-157">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="60d77-158">Nee</span><span class="sxs-lookup"><span data-stu-id="60d77-158">No</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="60d77-159">Met behulp van basisverificatie</span><span class="sxs-lookup"><span data-stu-id="60d77-159">Using Basic authentication</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Basic",
            "username": "username",
            "password": "password"
        }
    }
}
```

### <a name="using-anonymous-authentication"></a><span data-ttu-id="60d77-160">Anonieme verificatie</span><span class="sxs-lookup"><span data-stu-id="60d77-160">Using Anonymous authentication</span></span>
```json
{
    "name": "ODataLinkedService",
        "properties":
    {
        "type": "OData",
        "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
        }
    }
}
```

### <a name="using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="60d77-161">Met behulp van Windows-verificatie toegang tot lokale OData-bron</span><span class="sxs-lookup"><span data-stu-id="60d77-161">Using Windows authentication accessing on-premises OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of on-premises OData source e.g. Dynamics CRM>",
            "authenticationType": "Windows",
            "username": "domain\\user",
            "password": "password",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="60d77-162">Met behulp van OAuth-verificatie bij toegang tot cloud OData-bron</span><span class="sxs-lookup"><span data-stu-id="60d77-162">Using OAuth authentication accessing cloud OData source</span></span>
```json
{
    "name": "inputLinkedService",
    "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "<endpoint of cloud OData source e.g. https://<tenant>.crm.dynamics.com/XRMServices/2011/OrganizationData.svc>",
            "authenticationType": "OAuth",
            "authorizedCredential": "<auto generated by clicking the Authorize button on UI>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="60d77-163">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="60d77-163">Dataset properties</span></span>
<span data-ttu-id="60d77-164">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van de [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="60d77-164">For a full list of sections & properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="60d77-165">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).</span><span class="sxs-lookup"><span data-stu-id="60d77-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="60d77-166">De **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over de locatie van de gegevens in het gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="60d77-166">The **typeProperties** section is different for each type of dataset and provides information about the location of the data in the data store.</span></span> <span data-ttu-id="60d77-167">De typeProperties sectie voor de gegevensset van het type **ODataResource** (inclusief OData-gegevensset) heeft de volgende eigenschappen</span><span class="sxs-lookup"><span data-stu-id="60d77-167">The typeProperties section for dataset of type **ODataResource** (which includes OData dataset) has the following properties</span></span>

| <span data-ttu-id="60d77-168">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="60d77-168">Property</span></span> | <span data-ttu-id="60d77-169">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="60d77-169">Description</span></span> | <span data-ttu-id="60d77-170">Vereist</span><span class="sxs-lookup"><span data-stu-id="60d77-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="60d77-171">Pad</span><span class="sxs-lookup"><span data-stu-id="60d77-171">path</span></span> |<span data-ttu-id="60d77-172">Pad naar de OData-bron</span><span class="sxs-lookup"><span data-stu-id="60d77-172">Path to the OData resource</span></span> |<span data-ttu-id="60d77-173">Nee</span><span class="sxs-lookup"><span data-stu-id="60d77-173">No</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="60d77-174">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="60d77-174">Copy activity properties</span></span>
<span data-ttu-id="60d77-175">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van activiteiten van de [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="60d77-175">For a full list of sections & properties available for defining activities, see the [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="60d77-176">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en -beleid zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="60d77-176">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="60d77-177">Eigenschappen die beschikbaar zijn in de sectie typeProperties van de activiteit wordt aan de andere kant variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="60d77-177">Properties available in the typeProperties section of the activity on the other hand vary with each activity type.</span></span> <span data-ttu-id="60d77-178">Voor de kopieeractiviteit variëren ze, afhankelijk van de typen van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="60d77-178">For Copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="60d77-179">Wanneer de bron is van het type **RelationalSource** (inclusief OData) de volgende eigenschappen beschikbaar zijn in de sectie typeProperties:</span><span class="sxs-lookup"><span data-stu-id="60d77-179">When source is of type **RelationalSource** (which includes OData) the following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="60d77-180">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="60d77-180">Property</span></span> | <span data-ttu-id="60d77-181">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="60d77-181">Description</span></span> | <span data-ttu-id="60d77-182">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="60d77-182">Example</span></span> | <span data-ttu-id="60d77-183">Vereist</span><span class="sxs-lookup"><span data-stu-id="60d77-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="60d77-184">query</span><span class="sxs-lookup"><span data-stu-id="60d77-184">query</span></span> |<span data-ttu-id="60d77-185">Gebruik de aangepaste query om gegevens te lezen.</span><span class="sxs-lookup"><span data-stu-id="60d77-185">Use the custom query to read data.</span></span> |<span data-ttu-id="60d77-186">'? $select = naam, beschrijving & $top = 5 '</span><span class="sxs-lookup"><span data-stu-id="60d77-186">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="60d77-187">Nee</span><span class="sxs-lookup"><span data-stu-id="60d77-187">No</span></span> |

## <a name="type-mapping-for-odata"></a><span data-ttu-id="60d77-188">Toewijzing van het type voor OData</span><span class="sxs-lookup"><span data-stu-id="60d77-188">Type Mapping for OData</span></span>
<span data-ttu-id="60d77-189">Zoals vermeld in de [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel kopieerbewerking wordt automatische typeconversies van brontypen opvangen typen met de volgende benadering voor in twee stappen uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="60d77-189">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following two-step approach.</span></span>

1. <span data-ttu-id="60d77-190">Systeemeigen brontypen converteren naar .NET-type</span><span class="sxs-lookup"><span data-stu-id="60d77-190">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="60d77-191">Converteren van .NET-type naar systeemeigen sink-type</span><span class="sxs-lookup"><span data-stu-id="60d77-191">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="60d77-192">Bij het verplaatsen van gegevens uit OData, worden de volgende toewijzingen van OData-types gebruikt voor .NET-type.</span><span class="sxs-lookup"><span data-stu-id="60d77-192">When moving data from OData, the following mappings are used from OData types to .NET type.</span></span>

| <span data-ttu-id="60d77-193">OData-gegevenstype</span><span class="sxs-lookup"><span data-stu-id="60d77-193">OData Data Type</span></span> | <span data-ttu-id="60d77-194">.NET-type</span><span class="sxs-lookup"><span data-stu-id="60d77-194">.NET Type</span></span> |
| --- | --- |
| <span data-ttu-id="60d77-195">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="60d77-195">Edm.Binary</span></span> |<span data-ttu-id="60d77-196">Byte]</span><span class="sxs-lookup"><span data-stu-id="60d77-196">Byte[]</span></span> |
| <span data-ttu-id="60d77-197">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="60d77-197">Edm.Boolean</span></span> |<span data-ttu-id="60d77-198">BOOL</span><span class="sxs-lookup"><span data-stu-id="60d77-198">Bool</span></span> |
| <span data-ttu-id="60d77-199">Edm.Byte</span><span class="sxs-lookup"><span data-stu-id="60d77-199">Edm.Byte</span></span> |<span data-ttu-id="60d77-200">Byte]</span><span class="sxs-lookup"><span data-stu-id="60d77-200">Byte[]</span></span> |
| <span data-ttu-id="60d77-201">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="60d77-201">Edm.DateTime</span></span> |<span data-ttu-id="60d77-202">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="60d77-202">DateTime</span></span> |
| <span data-ttu-id="60d77-203">Edm.Decimal</span><span class="sxs-lookup"><span data-stu-id="60d77-203">Edm.Decimal</span></span> |<span data-ttu-id="60d77-204">Decimale</span><span class="sxs-lookup"><span data-stu-id="60d77-204">Decimal</span></span> |
| <span data-ttu-id="60d77-205">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="60d77-205">Edm.Double</span></span> |<span data-ttu-id="60d77-206">dubbele</span><span class="sxs-lookup"><span data-stu-id="60d77-206">Double</span></span> |
| <span data-ttu-id="60d77-207">Edm.Single</span><span class="sxs-lookup"><span data-stu-id="60d77-207">Edm.Single</span></span> |<span data-ttu-id="60d77-208">Één</span><span class="sxs-lookup"><span data-stu-id="60d77-208">Single</span></span> |
| <span data-ttu-id="60d77-209">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="60d77-209">Edm.Guid</span></span> |<span data-ttu-id="60d77-210">GUID</span><span class="sxs-lookup"><span data-stu-id="60d77-210">Guid</span></span> |
| <span data-ttu-id="60d77-211">Edm.Int16</span><span class="sxs-lookup"><span data-stu-id="60d77-211">Edm.Int16</span></span> |<span data-ttu-id="60d77-212">Int16</span><span class="sxs-lookup"><span data-stu-id="60d77-212">Int16</span></span> |
| <span data-ttu-id="60d77-213">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="60d77-213">Edm.Int32</span></span> |<span data-ttu-id="60d77-214">Int32</span><span class="sxs-lookup"><span data-stu-id="60d77-214">Int32</span></span> |
| <span data-ttu-id="60d77-215">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="60d77-215">Edm.Int64</span></span> |<span data-ttu-id="60d77-216">Int64</span><span class="sxs-lookup"><span data-stu-id="60d77-216">Int64</span></span> |
| <span data-ttu-id="60d77-217">Edm.SByte</span><span class="sxs-lookup"><span data-stu-id="60d77-217">Edm.SByte</span></span> |<span data-ttu-id="60d77-218">Int16</span><span class="sxs-lookup"><span data-stu-id="60d77-218">Int16</span></span> |
| <span data-ttu-id="60d77-219">Edm.String</span><span class="sxs-lookup"><span data-stu-id="60d77-219">Edm.String</span></span> |<span data-ttu-id="60d77-220">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="60d77-220">String</span></span> |
| <span data-ttu-id="60d77-221">Edm.Time</span><span class="sxs-lookup"><span data-stu-id="60d77-221">Edm.Time</span></span> |<span data-ttu-id="60d77-222">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="60d77-222">TimeSpan</span></span> |
| <span data-ttu-id="60d77-223">Edm.DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="60d77-223">Edm.DateTimeOffset</span></span> |<span data-ttu-id="60d77-224">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="60d77-224">DateTimeOffset</span></span> |

> [!Note]
> <span data-ttu-id="60d77-225">OData complexe gegevenstypen zoals Object worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="60d77-225">OData complex data types e.g. Object are not supported.</span></span>

## <a name="json-example-copy-data-from-odata-source-to-azure-blob"></a><span data-ttu-id="60d77-226">JSON-voorbeeld: gegevens kopiëren van de OData-bron naar Azure Blob</span><span class="sxs-lookup"><span data-stu-id="60d77-226">JSON example: Copy data from OData source to Azure Blob</span></span>
<span data-ttu-id="60d77-227">In dit voorbeeld bevat definities van de voorbeeld-JSON die u een pijplijn maken kunt met behulp van [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="60d77-227">This example provides sample JSON definitions that you can use to create a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="60d77-228">Ze laten zien hoe gegevens kopiëren van een OData-bron naar een Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="60d77-228">They show how to copy data from an OData source to an Azure Blob Storage.</span></span> <span data-ttu-id="60d77-229">Gegevens kunnen echter worden gekopieerd naar een van de PUT vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van de Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="60d77-229">However, data can be copied to any of the sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using the Copy Activity in Azure Data Factory.</span></span> <span data-ttu-id="60d77-230">Het voorbeeld heeft de volgende Data Factory-entiteiten:</span><span class="sxs-lookup"><span data-stu-id="60d77-230">The sample has the following Data Factory entities:</span></span>

1. <span data-ttu-id="60d77-231">Een gekoppelde service van het type [OData](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="60d77-231">A linked service of type [OData](#linked-service-properties).</span></span>
2. <span data-ttu-id="60d77-232">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="60d77-232">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="60d77-233">Invoer [gegevensset](data-factory-create-datasets.md) van het type [ODataResource](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="60d77-233">An input [dataset](data-factory-create-datasets.md) of type [ODataResource](#dataset-properties).</span></span>
4. <span data-ttu-id="60d77-234">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="60d77-234">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="60d77-235">Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [RelationalSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="60d77-235">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="60d77-236">Het voorbeeld worden gegevens gekopieerd van een query op een OData-bron met een Azure-blob elk uur.</span><span class="sxs-lookup"><span data-stu-id="60d77-236">The sample copies data from querying against an OData source to an Azure blob every hour.</span></span> <span data-ttu-id="60d77-237">De JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na de voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="60d77-237">The JSON properties used in these samples are described in sections following the samples.</span></span>

<span data-ttu-id="60d77-238">**OData gekoppelde service:** in dit voorbeeld wordt de anonieme verificatie.</span><span class="sxs-lookup"><span data-stu-id="60d77-238">**OData linked service:** This example uses the Anonymous authentication.</span></span> <span data-ttu-id="60d77-239">Zie [OData gekoppelde service](#linked-service-properties) sectie voor verschillende soorten verificatie die u kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="60d77-239">See [OData linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

```json
{
    "name": "ODataLinkedService",
        "properties":
    {
        "type": "OData",
            "typeProperties":
        {
            "url": "http://services.odata.org/OData/OData.svc",
            "authenticationType": "Anonymous"
            }
        }
}
```

<span data-ttu-id="60d77-240">**Gekoppelde Azure Storage-service:**</span><span class="sxs-lookup"><span data-stu-id="60d77-240">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="60d77-241">**OData-invoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="60d77-241">**OData input dataset:**</span></span>

<span data-ttu-id="60d77-242">Instelling 'extern': 'true' informeert de Data Factory-service dat de dataset extern is aan de gegevensfactory en niet wordt geproduceerd door een activiteit in de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="60d77-242">Setting “external”: ”true” informs the Data Factory service that the dataset is external to the data factory and is not produced by an activity in the data factory.</span></span>

```json
{
    "name": "ODataDataset",
    "properties":
    {
        "type": "ODataResource",
        "typeProperties":
        {
                "path": "Products"
        },
        "linkedServiceName": "ODataLinkedService",
        "structure": [],
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {
            "retryInterval": "00:01:00",
            "retryTimeout": "00:10:00",
            "maximumRetry": 3                
        }
    }
}
```

<span data-ttu-id="60d77-243">Geven **pad** in de gegevensset definitie is optioneel.</span><span class="sxs-lookup"><span data-stu-id="60d77-243">Specifying **path** in the dataset definition is optional.</span></span>

<span data-ttu-id="60d77-244">**Azure Blob-uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="60d77-244">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="60d77-245">Gegevens worden geschreven naar een nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="60d77-245">Data is written to a new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="60d77-246">Het pad naar de blob wordt dynamisch geëvalueerd op basis van de begintijd van het segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="60d77-246">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="60d77-247">Het mappad maakt gebruik van jaar, maand, dag en uur delen van de begintijd.</span><span class="sxs-lookup"><span data-stu-id="60d77-247">The folder path uses year, month, day, and hours parts of the start time.</span></span>

```json
{
    "name": "AzureBlobODataDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/odata/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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


<span data-ttu-id="60d77-248">**De kopieeractiviteit in een pijplijn met OData-bron en sink van Blob:**</span><span class="sxs-lookup"><span data-stu-id="60d77-248">**Copy activity in a pipeline with OData source and Blob sink:**</span></span>

<span data-ttu-id="60d77-249">De pijplijn bevat een Kopieeractiviteit die is geconfigureerd voor gebruik van de invoer- en uitvoergegevenssets en elk uur is gepland.</span><span class="sxs-lookup"><span data-stu-id="60d77-249">The pipeline contains a Copy Activity that is configured to use the input and output datasets and is scheduled to run every hour.</span></span> <span data-ttu-id="60d77-250">In de pijplijn-JSON-definitie de **bron** type is ingesteld op **RelationalSource** en **sink** type is ingesteld op **BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="60d77-250">In the pipeline JSON definition, the **source** type is set to **RelationalSource** and **sink** type is set to **BlobSink**.</span></span> <span data-ttu-id="60d77-251">De SQL-query die is opgegeven voor de **query** eigenschap selecteert u de meest recente gegevens (nieuwste) van de OData-bron.</span><span class="sxs-lookup"><span data-stu-id="60d77-251">The SQL query specified for the **query** property selects the latest (newest) data from the OData source.</span></span>

```json
{
    "name": "CopyODataToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "RelationalSource",
                        "query": "?$select=Name, Description&$top=5",
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "ODataDataSet"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobODataDataSet"
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
                "name": "ODataToBlob"
            }
        ],
        "start": "2017-02-01T18:00:00Z",
        "end": "2017-02-03T19:00:00Z"
    }
}
```

<span data-ttu-id="60d77-252">Geven **query** in de pijplijn definitie is optioneel.</span><span class="sxs-lookup"><span data-stu-id="60d77-252">Specifying **query** in the pipeline definition is optional.</span></span> <span data-ttu-id="60d77-253">De **URL** is dat de Data Factory-service gebruikt om gegevens te halen: URL die is opgegeven in de gekoppelde service (vereist) + pad dat is opgegeven in de gegevensset (optioneel) + query in de pijplijn (optioneel).</span><span class="sxs-lookup"><span data-stu-id="60d77-253">The **URL** that the Data Factory service uses to retrieve data is: URL specified in the linked service (required) + path specified in the dataset (optional) + query in the pipeline (optional).</span></span>


### <a name="type-mapping-for-odata"></a><span data-ttu-id="60d77-254">Toewijzing van het type voor OData</span><span class="sxs-lookup"><span data-stu-id="60d77-254">Type mapping for OData</span></span>
<span data-ttu-id="60d77-255">Zoals vermeld in de [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel kopieerbewerking wordt automatische typeconversies van brontypen opvangen typen met de volgende stappen 2-benadering uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="60d77-255">As mentioned in the [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types to sink types with the following 2-step approach:</span></span>

1. <span data-ttu-id="60d77-256">Systeemeigen brontypen converteren naar .NET-type</span><span class="sxs-lookup"><span data-stu-id="60d77-256">Convert from native source types to .NET type</span></span>
2. <span data-ttu-id="60d77-257">Converteren van .NET-type naar systeemeigen sink-type</span><span class="sxs-lookup"><span data-stu-id="60d77-257">Convert from .NET type to native sink type</span></span>

<span data-ttu-id="60d77-258">Wanneer zwevend gegevens uit OData-gegevens opslaat, worden de OData-gegevenstypen toegewezen aan .NET-typen.</span><span class="sxs-lookup"><span data-stu-id="60d77-258">When moving data from OData data stores, OData data types are mapped to .NET types.</span></span>

## <a name="map-source-to-sink-columns"></a><span data-ttu-id="60d77-259">Bron van de kaart opvangen kolommen</span><span class="sxs-lookup"><span data-stu-id="60d77-259">Map source to sink columns</span></span>
<span data-ttu-id="60d77-260">Zie voor meer informatie over het toewijzen van kolommen in gegevensset naar kolommen in gegevensset sink bron, [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="60d77-260">To learn about mapping columns in source dataset to columns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="60d77-261">Herhaalbare leesbewerking van relationele bronnen</span><span class="sxs-lookup"><span data-stu-id="60d77-261">Repeatable read from relational sources</span></span>
<span data-ttu-id="60d77-262">Bij het kopiëren van gegevens van relationele gegevens worden opgeslagen, moet u herhaalbaarheid Houd in gedachten om te voorkomen dat ongewenste resultaten.</span><span class="sxs-lookup"><span data-stu-id="60d77-262">When copying data from relational data stores, keep repeatability in mind to avoid unintended outcomes.</span></span> <span data-ttu-id="60d77-263">In Azure Data Factory, kunt u een segment handmatig opnieuw.</span><span class="sxs-lookup"><span data-stu-id="60d77-263">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="60d77-264">U kunt ook een beleid voor opnieuw proberen voor een gegevensset configureren zodat een segment wordt opnieuw uitgevoerd wanneer een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="60d77-264">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="60d77-265">Wanneer een segment opnieuw in beide gevallen wordt uitgevoerd, moet u ervoor zorgen dat dezelfde gegevens is gelezen ongeacht hoe vaak een segment wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="60d77-265">When a slice is rerun in either way, you need to make sure that the same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="60d77-266">Zie [Repeatable van relationele bronnen lezen](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="60d77-266">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="60d77-267">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="60d77-267">Performance and Tuning</span></span>
<span data-ttu-id="60d77-268">Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) voor meer informatie over de belangrijkste factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren om te optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="60d77-268">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) to learn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways to optimize it.</span></span>
