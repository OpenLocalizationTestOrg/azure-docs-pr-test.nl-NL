---
title: aaaMove gegevens uit OData-bronnen | Microsoft Docs
description: Meer informatie over hoe toomove gegevens uit OData gegevensbronnen met behulp van Azure Data Factory.
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
ms.openlocfilehash: 328efe4fd274fb3e54c1d2f209e4614c77c1ff37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-a-odata-source-using-azure-data-factory"></a><span data-ttu-id="58a46-103">Verplaatsen van gegevens uit een OData-bron met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="58a46-103">Move data From a OData source using Azure Data Factory</span></span>
<span data-ttu-id="58a46-104">Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit Hallo in Azure Data Factory toomove gegevens uit een OData-bron.</span><span class="sxs-lookup"><span data-stu-id="58a46-104">This article explains how toouse hello Copy Activity in Azure Data Factory toomove data from an OData source.</span></span> <span data-ttu-id="58a46-105">Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin een algemeen overzicht van de verplaatsing van gegevens met de kopieeractiviteit Hallo geeft.</span><span class="sxs-lookup"><span data-stu-id="58a46-105">It builds on hello [Data Movement Activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with hello copy activity.</span></span>

<span data-ttu-id="58a46-106">U kunt gegevens kopiëren van een gegevensarchief voor OData-bron tooany ondersteund sink.</span><span class="sxs-lookup"><span data-stu-id="58a46-106">You can copy data from an OData source tooany supported sink data store.</span></span> <span data-ttu-id="58a46-107">Zie voor een lijst van gegevens winkels ondersteund zoals sinks door kopieeractiviteit hello, Hallo [ondersteunde gegevensarchieven](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel.</span><span class="sxs-lookup"><span data-stu-id="58a46-107">For a list of data stores supported as sinks by hello copy activity, see hello [Supported data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="58a46-108">Data factory ondersteunt momenteel alleen verplaatsen van gegevens uit een OData-brongegevens tooother is opgeslagen, maar niet voor het verplaatsen van gegevens van andere gegevens worden opgeslagen tooan OData-bron.</span><span class="sxs-lookup"><span data-stu-id="58a46-108">Data factory currently supports only moving data from an OData source tooother data stores, but not for moving data from other data stores tooan OData source.</span></span> 

## <a name="supported-versions-and-authentication-types"></a><span data-ttu-id="58a46-109">Ondersteunde versies en verificatietypen</span><span class="sxs-lookup"><span data-stu-id="58a46-109">Supported versions and authentication types</span></span>
<span data-ttu-id="58a46-110">Deze OData-connector ondersteuning voor OData-versie 3.0 en 4.0 en u kunt kopiëren van gegevens uit zowel cloud OData en lokale OData-bronnen.</span><span class="sxs-lookup"><span data-stu-id="58a46-110">This OData connector support OData version 3.0 and 4.0, and you can copy data from both cloud OData and on-premises OData sources.</span></span> <span data-ttu-id="58a46-111">Hallo laatstgenoemde moet u tooinstall Hallo Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="58a46-111">For hello latter, you need tooinstall hello Data Management Gateway.</span></span> <span data-ttu-id="58a46-112">Zie [gegevens verplaatsen tussen on-premises en cloud](data-factory-move-data-between-onprem-and-cloud.md) voor meer informatie over Data Management Gateway.</span><span class="sxs-lookup"><span data-stu-id="58a46-112">See [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for details about Data Management Gateway.</span></span>

<span data-ttu-id="58a46-113">Hieronder verificatie worden typen ondersteund:</span><span class="sxs-lookup"><span data-stu-id="58a46-113">Below authentication types are supported:</span></span>

* <span data-ttu-id="58a46-114">tooaccess **cloud** OData-feed, kunt u anoniem, basis (gebruikersnaam en wachtwoord) of Azure Active Directory op basis van OAuth-verificatie.</span><span class="sxs-lookup"><span data-stu-id="58a46-114">tooaccess **cloud** OData feed, you can use anonymous, basic (user name and password), or Azure Active Directory based OAuth authentication.</span></span>
* <span data-ttu-id="58a46-115">tooaccess **lokale** OData-feed, kunt u anoniem, basis (gebruikersnaam en wachtwoord) of Windows-verificatie.</span><span class="sxs-lookup"><span data-stu-id="58a46-115">tooaccess **on-premises** OData feed, you can use anonymous, basic (user name and password), or Windows authentication.</span></span>

## <a name="getting-started"></a><span data-ttu-id="58a46-116">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="58a46-116">Getting started</span></span>
<span data-ttu-id="58a46-117">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens uit een OData-bron verplaatst met behulp van verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="58a46-117">You can create a pipeline with a copy activity that moves data from an OData source by using different tools/APIs.</span></span>

<span data-ttu-id="58a46-118">Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="58a46-118">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="58a46-119">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="58a46-119">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="58a46-120">U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="58a46-120">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="58a46-121">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="58a46-121">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="58a46-122">Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="58a46-122">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="58a46-123">Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="58a46-123">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="58a46-124">Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="58a46-124">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="58a46-125">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="58a46-125">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="58a46-126">Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="58a46-126">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="58a46-127">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="58a46-127">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="58a46-128">Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens uit een OData-bron zijn [JSON-voorbeeld: gegevens kopiëren van de OData-bron tooAzure Blob](#json-example-copy-data-from-odata-source-to-azure-blob) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="58a46-128">For a sample with JSON definitions for Data Factory entities that are used toocopy data from an OData source, see [JSON example: Copy data from OData source tooAzure Blob](#json-example-copy-data-from-odata-source-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="58a46-129">Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikte toodefine Data Factory-entiteiten specifieke tooOData bron:</span><span class="sxs-lookup"><span data-stu-id="58a46-129">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooOData source:</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="58a46-130">Eigenschappen van de gekoppelde Service</span><span class="sxs-lookup"><span data-stu-id="58a46-130">Linked Service properties</span></span>
<span data-ttu-id="58a46-131">Hallo volgende tabel biedt een beschrijving voor de JSON-elementen specifieke tooOData gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="58a46-131">hello following table provides description for JSON elements specific tooOData linked service.</span></span>

| <span data-ttu-id="58a46-132">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="58a46-132">Property</span></span> | <span data-ttu-id="58a46-133">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="58a46-133">Description</span></span> | <span data-ttu-id="58a46-134">Vereist</span><span class="sxs-lookup"><span data-stu-id="58a46-134">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="58a46-135">type</span><span class="sxs-lookup"><span data-stu-id="58a46-135">type</span></span> |<span data-ttu-id="58a46-136">Hallo type eigenschap moet worden ingesteld op: **OData**</span><span class="sxs-lookup"><span data-stu-id="58a46-136">hello type property must be set to: **OData**</span></span> |<span data-ttu-id="58a46-137">Ja</span><span class="sxs-lookup"><span data-stu-id="58a46-137">Yes</span></span> |
| <span data-ttu-id="58a46-138">URL</span><span class="sxs-lookup"><span data-stu-id="58a46-138">url</span></span> |<span data-ttu-id="58a46-139">URL van Hallo OData-service.</span><span class="sxs-lookup"><span data-stu-id="58a46-139">Url of hello OData service.</span></span> |<span data-ttu-id="58a46-140">Ja</span><span class="sxs-lookup"><span data-stu-id="58a46-140">Yes</span></span> |
| <span data-ttu-id="58a46-141">authenticationType</span><span class="sxs-lookup"><span data-stu-id="58a46-141">authenticationType</span></span> |<span data-ttu-id="58a46-142">Type verificatie gebruikt tooconnect toohello OData-bron.</span><span class="sxs-lookup"><span data-stu-id="58a46-142">Type of authentication used tooconnect toohello OData source.</span></span> <br/><br/> <span data-ttu-id="58a46-143">Mogelijke waarden zijn voor OData-cloud, anoniem, basis en OAuth (Opmerking momenteel alleen ondersteuning voor Azure Data Factory Azure Active Directory op basis van OAuth).</span><span class="sxs-lookup"><span data-stu-id="58a46-143">For cloud OData, possible values are Anonymous, Basic, and OAuth (note Azure Data Factory currently only support Azure Active Directory based OAuth).</span></span> <br/><br/> <span data-ttu-id="58a46-144">Mogelijke waarden zijn voor lokale OData, anoniem, basis en Windows.</span><span class="sxs-lookup"><span data-stu-id="58a46-144">For on-premises OData, possible values are Anonymous, Basic, and Windows.</span></span> |<span data-ttu-id="58a46-145">Ja</span><span class="sxs-lookup"><span data-stu-id="58a46-145">Yes</span></span> |
| <span data-ttu-id="58a46-146">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="58a46-146">username</span></span> |<span data-ttu-id="58a46-147">Geef de gebruikersnaam als u basisverificatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="58a46-147">Specify user name if you are using Basic authentication.</span></span> |<span data-ttu-id="58a46-148">Ja (alleen als u basisverificatie gebruikt)</span><span class="sxs-lookup"><span data-stu-id="58a46-148">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="58a46-149">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="58a46-149">password</span></span> |<span data-ttu-id="58a46-150">Wachtwoord voor gebruikersaccount Hallo die u hebt opgegeven voor Hallo gebruikersnaam opgeven.</span><span class="sxs-lookup"><span data-stu-id="58a46-150">Specify password for hello user account you specified for hello username.</span></span> |<span data-ttu-id="58a46-151">Ja (alleen als u basisverificatie gebruikt)</span><span class="sxs-lookup"><span data-stu-id="58a46-151">Yes (only if you are using Basic authentication)</span></span> |
| <span data-ttu-id="58a46-152">authorizedCredential</span><span class="sxs-lookup"><span data-stu-id="58a46-152">authorizedCredential</span></span> |<span data-ttu-id="58a46-153">Als u van OAuth gebruikmaakt, klikt u op **autoriseren** knop op Hallo Data Factory-Wizard kopiëren of Editor en voer uw referenties wordt Hallo-waarde van deze eigenschap automatisch wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="58a46-153">If you are using OAuth, click **Authorize** button in hello Data Factory Copy Wizard or Editor and enter your credential, then hello value of this property will be auto-generated.</span></span> |<span data-ttu-id="58a46-154">Ja (alleen als u OAuth-verificatie gebruikt)</span><span class="sxs-lookup"><span data-stu-id="58a46-154">Yes (only if you are using OAuth authentication)</span></span> |
| <span data-ttu-id="58a46-155">gatewayName</span><span class="sxs-lookup"><span data-stu-id="58a46-155">gatewayName</span></span> |<span data-ttu-id="58a46-156">Naam van Hallo-gateway die Hallo Data Factory-service moet tooconnect toohello on-premises OData-service gebruiken.</span><span class="sxs-lookup"><span data-stu-id="58a46-156">Name of hello gateway that hello Data Factory service should use tooconnect toohello on-premises OData service.</span></span> <span data-ttu-id="58a46-157">Geef alleen als u gegevens uit een on-premises OData-bron kopiëren wilt.</span><span class="sxs-lookup"><span data-stu-id="58a46-157">Specify only if you are copying data from on-prem OData source.</span></span> |<span data-ttu-id="58a46-158">Nee</span><span class="sxs-lookup"><span data-stu-id="58a46-158">No</span></span> |

### <a name="using-basic-authentication"></a><span data-ttu-id="58a46-159">Met behulp van basisverificatie</span><span class="sxs-lookup"><span data-stu-id="58a46-159">Using Basic authentication</span></span>
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

### <a name="using-anonymous-authentication"></a><span data-ttu-id="58a46-160">Anonieme verificatie</span><span class="sxs-lookup"><span data-stu-id="58a46-160">Using Anonymous authentication</span></span>
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

### <a name="using-windows-authentication-accessing-on-premises-odata-source"></a><span data-ttu-id="58a46-161">Met behulp van Windows-verificatie toegang tot lokale OData-bron</span><span class="sxs-lookup"><span data-stu-id="58a46-161">Using Windows authentication accessing on-premises OData source</span></span>
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

### <a name="using-oauth-authentication-accessing-cloud-odata-source"></a><span data-ttu-id="58a46-162">Met behulp van OAuth-verificatie bij toegang tot cloud OData-bron</span><span class="sxs-lookup"><span data-stu-id="58a46-162">Using OAuth authentication accessing cloud OData source</span></span>
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
            "authorizedCredential": "<auto generated by clicking hello Authorize button on UI>"
        }
    }
}
```

## <a name="dataset-properties"></a><span data-ttu-id="58a46-163">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="58a46-163">Dataset properties</span></span>
<span data-ttu-id="58a46-164">Zie voor een volledige lijst van de secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets van Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="58a46-164">For a full list of sections & properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="58a46-165">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle gegevensset typen (Azure SQL, Azure blob-, Azure-tabel, enz.).</span><span class="sxs-lookup"><span data-stu-id="58a46-165">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, etc.).</span></span>

<span data-ttu-id="58a46-166">Hallo **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="58a46-166">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="58a46-167">Hallo typeProperties sectie voor de gegevensset van het type **ODataResource** (inclusief OData-gegevensset) heeft Hallo volgende eigenschappen</span><span class="sxs-lookup"><span data-stu-id="58a46-167">hello typeProperties section for dataset of type **ODataResource** (which includes OData dataset) has hello following properties</span></span>

| <span data-ttu-id="58a46-168">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="58a46-168">Property</span></span> | <span data-ttu-id="58a46-169">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="58a46-169">Description</span></span> | <span data-ttu-id="58a46-170">Vereist</span><span class="sxs-lookup"><span data-stu-id="58a46-170">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="58a46-171">Pad</span><span class="sxs-lookup"><span data-stu-id="58a46-171">path</span></span> |<span data-ttu-id="58a46-172">Pad toohello OData-bron</span><span class="sxs-lookup"><span data-stu-id="58a46-172">Path toohello OData resource</span></span> |<span data-ttu-id="58a46-173">Nee</span><span class="sxs-lookup"><span data-stu-id="58a46-173">No</span></span> |

## <a name="copy-activity-properties"></a><span data-ttu-id="58a46-174">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="58a46-174">Copy activity properties</span></span>
<span data-ttu-id="58a46-175">Zie voor een volledige lijst met secties & eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="58a46-175">For a full list of sections & properties available for defining activities, see hello [Creating Pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="58a46-176">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en -beleid zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="58a46-176">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="58a46-177">Eigenschappen beschikbaar zijn in Hallo typeProperties sectie Hallo-activiteit op Hallo daarentegen variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="58a46-177">Properties available in hello typeProperties section of hello activity on hello other hand vary with each activity type.</span></span> <span data-ttu-id="58a46-178">Voor de kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="58a46-178">For Copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="58a46-179">Wanneer de bron is van het type **RelationalSource** (inclusief OData) Hallo volgende eigenschappen beschikbaar zijn in de sectie typeProperties:</span><span class="sxs-lookup"><span data-stu-id="58a46-179">When source is of type **RelationalSource** (which includes OData) hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="58a46-180">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="58a46-180">Property</span></span> | <span data-ttu-id="58a46-181">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="58a46-181">Description</span></span> | <span data-ttu-id="58a46-182">Voorbeeld</span><span class="sxs-lookup"><span data-stu-id="58a46-182">Example</span></span> | <span data-ttu-id="58a46-183">Vereist</span><span class="sxs-lookup"><span data-stu-id="58a46-183">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="58a46-184">query</span><span class="sxs-lookup"><span data-stu-id="58a46-184">query</span></span> |<span data-ttu-id="58a46-185">Hallo aangepaste query tooread gegevens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="58a46-185">Use hello custom query tooread data.</span></span> |<span data-ttu-id="58a46-186">'? $select = naam, beschrijving & $top = 5 '</span><span class="sxs-lookup"><span data-stu-id="58a46-186">"?$select=Name, Description&$top=5"</span></span> |<span data-ttu-id="58a46-187">Nee</span><span class="sxs-lookup"><span data-stu-id="58a46-187">No</span></span> |

## <a name="type-mapping-for-odata"></a><span data-ttu-id="58a46-188">Toewijzing van het type voor OData</span><span class="sxs-lookup"><span data-stu-id="58a46-188">Type Mapping for OData</span></span>
<span data-ttu-id="58a46-189">Zoals vermeld in Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel kopieeractiviteit voert automatische typeconversies van brontypen typen toosink Hello benadering in twee stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="58a46-189">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following two-step approach.</span></span>

1. <span data-ttu-id="58a46-190">Systeemeigen bron typen too.NET type converteren</span><span class="sxs-lookup"><span data-stu-id="58a46-190">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="58a46-191">Converteren van .NET-type toonative sink-type</span><span class="sxs-lookup"><span data-stu-id="58a46-191">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="58a46-192">Bij het verplaatsen van gegevens uit OData hello volgende toewijzingen gebruikt van OData-typen too.NET type.</span><span class="sxs-lookup"><span data-stu-id="58a46-192">When moving data from OData, hello following mappings are used from OData types too.NET type.</span></span>

| <span data-ttu-id="58a46-193">OData-gegevenstype</span><span class="sxs-lookup"><span data-stu-id="58a46-193">OData Data Type</span></span> | <span data-ttu-id="58a46-194">.NET-type</span><span class="sxs-lookup"><span data-stu-id="58a46-194">.NET Type</span></span> |
| --- | --- |
| <span data-ttu-id="58a46-195">Edm.Binary</span><span class="sxs-lookup"><span data-stu-id="58a46-195">Edm.Binary</span></span> |<span data-ttu-id="58a46-196">Byte]</span><span class="sxs-lookup"><span data-stu-id="58a46-196">Byte[]</span></span> |
| <span data-ttu-id="58a46-197">Edm.Boolean</span><span class="sxs-lookup"><span data-stu-id="58a46-197">Edm.Boolean</span></span> |<span data-ttu-id="58a46-198">BOOL</span><span class="sxs-lookup"><span data-stu-id="58a46-198">Bool</span></span> |
| <span data-ttu-id="58a46-199">Edm.Byte</span><span class="sxs-lookup"><span data-stu-id="58a46-199">Edm.Byte</span></span> |<span data-ttu-id="58a46-200">Byte]</span><span class="sxs-lookup"><span data-stu-id="58a46-200">Byte[]</span></span> |
| <span data-ttu-id="58a46-201">Edm.DateTime</span><span class="sxs-lookup"><span data-stu-id="58a46-201">Edm.DateTime</span></span> |<span data-ttu-id="58a46-202">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="58a46-202">DateTime</span></span> |
| <span data-ttu-id="58a46-203">Edm.Decimal</span><span class="sxs-lookup"><span data-stu-id="58a46-203">Edm.Decimal</span></span> |<span data-ttu-id="58a46-204">Decimale</span><span class="sxs-lookup"><span data-stu-id="58a46-204">Decimal</span></span> |
| <span data-ttu-id="58a46-205">Edm.Double</span><span class="sxs-lookup"><span data-stu-id="58a46-205">Edm.Double</span></span> |<span data-ttu-id="58a46-206">dubbele</span><span class="sxs-lookup"><span data-stu-id="58a46-206">Double</span></span> |
| <span data-ttu-id="58a46-207">Edm.Single</span><span class="sxs-lookup"><span data-stu-id="58a46-207">Edm.Single</span></span> |<span data-ttu-id="58a46-208">Één</span><span class="sxs-lookup"><span data-stu-id="58a46-208">Single</span></span> |
| <span data-ttu-id="58a46-209">Edm.Guid</span><span class="sxs-lookup"><span data-stu-id="58a46-209">Edm.Guid</span></span> |<span data-ttu-id="58a46-210">GUID</span><span class="sxs-lookup"><span data-stu-id="58a46-210">Guid</span></span> |
| <span data-ttu-id="58a46-211">Edm.Int16</span><span class="sxs-lookup"><span data-stu-id="58a46-211">Edm.Int16</span></span> |<span data-ttu-id="58a46-212">Int16</span><span class="sxs-lookup"><span data-stu-id="58a46-212">Int16</span></span> |
| <span data-ttu-id="58a46-213">Edm.Int32</span><span class="sxs-lookup"><span data-stu-id="58a46-213">Edm.Int32</span></span> |<span data-ttu-id="58a46-214">Int32</span><span class="sxs-lookup"><span data-stu-id="58a46-214">Int32</span></span> |
| <span data-ttu-id="58a46-215">Edm.Int64</span><span class="sxs-lookup"><span data-stu-id="58a46-215">Edm.Int64</span></span> |<span data-ttu-id="58a46-216">Int64</span><span class="sxs-lookup"><span data-stu-id="58a46-216">Int64</span></span> |
| <span data-ttu-id="58a46-217">Edm.SByte</span><span class="sxs-lookup"><span data-stu-id="58a46-217">Edm.SByte</span></span> |<span data-ttu-id="58a46-218">Int16</span><span class="sxs-lookup"><span data-stu-id="58a46-218">Int16</span></span> |
| <span data-ttu-id="58a46-219">Edm.String</span><span class="sxs-lookup"><span data-stu-id="58a46-219">Edm.String</span></span> |<span data-ttu-id="58a46-220">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="58a46-220">String</span></span> |
| <span data-ttu-id="58a46-221">Edm.Time</span><span class="sxs-lookup"><span data-stu-id="58a46-221">Edm.Time</span></span> |<span data-ttu-id="58a46-222">TimeSpan</span><span class="sxs-lookup"><span data-stu-id="58a46-222">TimeSpan</span></span> |
| <span data-ttu-id="58a46-223">Edm.DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="58a46-223">Edm.DateTimeOffset</span></span> |<span data-ttu-id="58a46-224">DateTimeOffset</span><span class="sxs-lookup"><span data-stu-id="58a46-224">DateTimeOffset</span></span> |

> [!Note]
> <span data-ttu-id="58a46-225">OData complexe gegevenstypen zoals Object worden niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="58a46-225">OData complex data types e.g. Object are not supported.</span></span>

## <a name="json-example-copy-data-from-odata-source-tooazure-blob"></a><span data-ttu-id="58a46-226">JSON-voorbeeld: gegevens uit OData-bron tooAzure Blob kopiëren</span><span class="sxs-lookup"><span data-stu-id="58a46-226">JSON example: Copy data from OData source tooAzure Blob</span></span>
<span data-ttu-id="58a46-227">In dit voorbeeld voorbeeld JSON definities bevat dat u een pijplijn toocreate gebruiken met behulp van kunt [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md) of [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="58a46-227">This example provides sample JSON definitions that you can use toocreate a pipeline by using [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md) or [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="58a46-228">Ze geven weer hoe toocopy van een OData-gegevensbron tooan Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="58a46-228">They show how toocopy data from an OData source tooan Azure Blob Storage.</span></span> <span data-ttu-id="58a46-229">Gegevens kunnen echter wel gekopieerde tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="58a46-229">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span> <span data-ttu-id="58a46-230">Hallo voorbeeld heeft Hallo Data Factory-entiteiten te volgen:</span><span class="sxs-lookup"><span data-stu-id="58a46-230">hello sample has hello following Data Factory entities:</span></span>

1. <span data-ttu-id="58a46-231">Een gekoppelde service van het type [OData](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="58a46-231">A linked service of type [OData](#linked-service-properties).</span></span>
2. <span data-ttu-id="58a46-232">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="58a46-232">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
3. <span data-ttu-id="58a46-233">Invoer [gegevensset](data-factory-create-datasets.md) van het type [ODataResource](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="58a46-233">An input [dataset](data-factory-create-datasets.md) of type [ODataResource](#dataset-properties).</span></span>
4. <span data-ttu-id="58a46-234">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="58a46-234">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
5. <span data-ttu-id="58a46-235">Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [RelationalSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="58a46-235">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="58a46-236">Hallo-voorbeeld worden gegevens gekopieerd van een query op een OData-bron tooan Azure blob elk uur.</span><span class="sxs-lookup"><span data-stu-id="58a46-236">hello sample copies data from querying against an OData source tooan Azure blob every hour.</span></span> <span data-ttu-id="58a46-237">Hallo JSON-eigenschappen die in deze voorbeelden worden beschreven in de secties na Hallo voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="58a46-237">hello JSON properties used in these samples are described in sections following hello samples.</span></span>

<span data-ttu-id="58a46-238">**OData gekoppelde service:** in dit voorbeeld gebruikt Hallo anonieme verificatie.</span><span class="sxs-lookup"><span data-stu-id="58a46-238">**OData linked service:** This example uses hello Anonymous authentication.</span></span> <span data-ttu-id="58a46-239">Zie [OData gekoppelde service](#linked-service-properties) sectie voor verschillende soorten verificatie die u kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="58a46-239">See [OData linked service](#linked-service-properties) section for different types of authentication you can use.</span></span>

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

<span data-ttu-id="58a46-240">**Gekoppelde Azure Storage-service:**</span><span class="sxs-lookup"><span data-stu-id="58a46-240">**Azure Storage linked service:**</span></span>

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

<span data-ttu-id="58a46-241">**OData-invoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="58a46-241">**OData input dataset:**</span></span>

<span data-ttu-id="58a46-242">Instelling 'extern': 'true' informeert Hallo Data Factory-service die gegevensset Hallo externe toohello data factory is en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="58a46-242">Setting “external”: ”true” informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

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

<span data-ttu-id="58a46-243">Geven **pad** in Hallo gegevensset definitie is optioneel.</span><span class="sxs-lookup"><span data-stu-id="58a46-243">Specifying **path** in hello dataset definition is optional.</span></span>

<span data-ttu-id="58a46-244">**Azure Blob-uitvoergegevensset:**</span><span class="sxs-lookup"><span data-stu-id="58a46-244">**Azure Blob output dataset:**</span></span>

<span data-ttu-id="58a46-245">Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="58a46-245">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span> <span data-ttu-id="58a46-246">pad naar map voor blob Hallo Hallo wordt dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="58a46-246">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="58a46-247">Hallo mappad jaar, maand, dag en uur delen van de begintijd Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="58a46-247">hello folder path uses year, month, day, and hours parts of hello start time.</span></span>

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


<span data-ttu-id="58a46-248">**De kopieeractiviteit in een pijplijn met OData-bron en sink van Blob:**</span><span class="sxs-lookup"><span data-stu-id="58a46-248">**Copy activity in a pipeline with OData source and Blob sink:**</span></span>

<span data-ttu-id="58a46-249">Hallo pijplijn bevat een Kopieeractiviteit die geconfigureerde toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur.</span><span class="sxs-lookup"><span data-stu-id="58a46-249">hello pipeline contains a Copy Activity that is configured toouse hello input and output datasets and is scheduled toorun every hour.</span></span> <span data-ttu-id="58a46-250">Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**RelationalSource** en **sink** type is ingesteld, te**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="58a46-250">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource** and **sink** type is set too**BlobSink**.</span></span> <span data-ttu-id="58a46-251">Hallo SQL-query is opgegeven voor Hallo **query** eigenschap selecteert u de meest recente (nieuwste) gegevens Hallo van Hallo OData-bron.</span><span class="sxs-lookup"><span data-stu-id="58a46-251">hello SQL query specified for hello **query** property selects hello latest (newest) data from hello OData source.</span></span>

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

<span data-ttu-id="58a46-252">Geven **query** in Hallo pijplijn definitie is optioneel.</span><span class="sxs-lookup"><span data-stu-id="58a46-252">Specifying **query** in hello pipeline definition is optional.</span></span> <span data-ttu-id="58a46-253">Hallo **URL** dat Hallo Data Factory-service tooretrieve gegevens gebruikt is: URL is opgegeven in Hallo gekoppelde service (vereist) + pad dat is opgegeven in de Hallo gegevensset (optioneel) + -query in Hallo pijplijn (optioneel).</span><span class="sxs-lookup"><span data-stu-id="58a46-253">hello **URL** that hello Data Factory service uses tooretrieve data is: URL specified in hello linked service (required) + path specified in hello dataset (optional) + query in hello pipeline (optional).</span></span>


### <a name="type-mapping-for-odata"></a><span data-ttu-id="58a46-254">Toewijzing van het type voor OData</span><span class="sxs-lookup"><span data-stu-id="58a46-254">Type mapping for OData</span></span>
<span data-ttu-id="58a46-255">Zoals vermeld in Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel kopieeractiviteit voert automatische typeconversies van brontypen typen toosink Hello 2 stap benadering te volgen:</span><span class="sxs-lookup"><span data-stu-id="58a46-255">As mentioned in hello [data movement activities](data-factory-data-movement-activities.md) article, Copy activity performs automatic type conversions from source types toosink types with hello following 2-step approach:</span></span>

1. <span data-ttu-id="58a46-256">Systeemeigen bron typen too.NET type converteren</span><span class="sxs-lookup"><span data-stu-id="58a46-256">Convert from native source types too.NET type</span></span>
2. <span data-ttu-id="58a46-257">Converteren van .NET-type toonative sink-type</span><span class="sxs-lookup"><span data-stu-id="58a46-257">Convert from .NET type toonative sink type</span></span>

<span data-ttu-id="58a46-258">Bij het verplaatsen van gegevens uit OData-gegevensarchieven, zijn de gegevenstypen OData toegewezen too.NET typen.</span><span class="sxs-lookup"><span data-stu-id="58a46-258">When moving data from OData data stores, OData data types are mapped too.NET types.</span></span>

## <a name="map-source-toosink-columns"></a><span data-ttu-id="58a46-259">Bronkolommen toosink toewijzen</span><span class="sxs-lookup"><span data-stu-id="58a46-259">Map source toosink columns</span></span>
<span data-ttu-id="58a46-260">Zie toolearn over het toewijzen van kolommen in bron gegevensset toocolumns in sink-gegevensset [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="58a46-260">toolearn about mapping columns in source dataset toocolumns in sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="repeatable-read-from-relational-sources"></a><span data-ttu-id="58a46-261">Herhaalbare leesbewerking van relationele bronnen</span><span class="sxs-lookup"><span data-stu-id="58a46-261">Repeatable read from relational sources</span></span>
<span data-ttu-id="58a46-262">Houd bij het kopiëren van gegevens uit een relationele gegevensopslag, herhaalbaarheid rekening tooavoid ongewenste resultaten.</span><span class="sxs-lookup"><span data-stu-id="58a46-262">When copying data from relational data stores, keep repeatability in mind tooavoid unintended outcomes.</span></span> <span data-ttu-id="58a46-263">In Azure Data Factory, kunt u een segment handmatig opnieuw.</span><span class="sxs-lookup"><span data-stu-id="58a46-263">In Azure Data Factory, you can rerun a slice manually.</span></span> <span data-ttu-id="58a46-264">U kunt ook een beleid voor opnieuw proberen voor een gegevensset configureren zodat een segment wordt opnieuw uitgevoerd wanneer een fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="58a46-264">You can also configure retry policy for a dataset so that a slice is rerun when a failure occurs.</span></span> <span data-ttu-id="58a46-265">Wanneer een segment opnieuw in beide gevallen wordt uitgevoerd, moet u ervoor dat dezelfde gegevens Hallo toomake wordt gelezen ongeacht hoe vaak een segment wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="58a46-265">When a slice is rerun in either way, you need toomake sure that hello same data is read no matter how many times a slice is run.</span></span> <span data-ttu-id="58a46-266">Zie [Repeatable van relationele bronnen lezen](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span><span class="sxs-lookup"><span data-stu-id="58a46-266">See [Repeatable read from relational sources](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="58a46-267">Prestaties en het afstemmen</span><span class="sxs-lookup"><span data-stu-id="58a46-267">Performance and Tuning</span></span>
<span data-ttu-id="58a46-268">Zie [uitvoering van de activiteit & afstemmen handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.</span><span class="sxs-lookup"><span data-stu-id="58a46-268">See [Copy Activity Performance & Tuning Guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
