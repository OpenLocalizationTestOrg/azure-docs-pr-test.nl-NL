---
title: gegevens van de aaaMove van Salesforce met behulp van de Data Factory | Microsoft Docs
description: Meer informatie over het toomove gegevens van Salesforce met behulp van Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: dbe3bfd6-fa6a-491a-9638-3a9a10d396d1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: c1bde2a333f5a3c0a995eb8c13ecf585132888b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-salesforce-by-using-azure-data-factory"></a><span data-ttu-id="5a012-103">Gegevens verplaatsen van Salesforce met behulp van Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="5a012-103">Move data from Salesforce by using Azure Data Factory</span></span>
<span data-ttu-id="5a012-104">In dit artikel bevat een overzicht van hoe u Kopieeractiviteit kunt gebruiken in een Azure data factory toocopy worden gegevens uit de gegevensopslag van Salesforce tooany die wordt vermeld onder Hallo Sink kolom in Hallo [ondersteunde gegevensbronnen en put](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabel.</span><span class="sxs-lookup"><span data-stu-id="5a012-104">This article outlines how you can use Copy Activity in an Azure data factory toocopy data from Salesforce tooany data store that is listed under hello Sink column in hello [supported sources and sinks](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table.</span></span> <span data-ttu-id="5a012-105">In dit artikel is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, waarin Kopieeractiviteit en combinaties van ondersteunde gegevens store een algemeen overzicht van de verplaatsing van gegevens biedt.</span><span class="sxs-lookup"><span data-stu-id="5a012-105">This article builds on hello [data movement activities](data-factory-data-movement-activities.md) article, which presents a general overview of data movement with Copy Activity and supported data store combinations.</span></span>

<span data-ttu-id="5a012-106">Azure Data Factory ondersteunt momenteel alleen te verplaatsen van gegevens van Salesforce[ondersteunde gegevensarchieven sink](data-factory-data-movement-activities.md#supported-data-stores-and-formats), maar ondersteunt geen bewegende gegevens van andere gegevens winkels tooSalesforce.</span><span class="sxs-lookup"><span data-stu-id="5a012-106">Azure Data Factory currently supports only moving data from Salesforce too[supported sink data stores](data-factory-data-movement-activities.md#supported-data-stores-and-formats), but does not support moving data from other data stores tooSalesforce.</span></span>

## <a name="supported-versions"></a><span data-ttu-id="5a012-107">Ondersteunde versies</span><span class="sxs-lookup"><span data-stu-id="5a012-107">Supported versions</span></span>
<span data-ttu-id="5a012-108">Deze connector ondersteunt de volgende edities van Salesforce Hallo: ontwikkelaarsversie, Professional Edition, Enterprise Edition of onbeperkte Edition.</span><span class="sxs-lookup"><span data-stu-id="5a012-108">This connector supports hello following editions of Salesforce: Developer Edition, Professional Edition, Enterprise Edition, or Unlimited Edition.</span></span> <span data-ttu-id="5a012-109">En het kopiëren van Salesforce productie, sandbox en aangepast domein ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="5a012-109">And it supports copying from Salesforce production, sandbox and custom domain.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a012-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5a012-110">Prerequisites</span></span>
* <span data-ttu-id="5a012-111">API-machtiging moet zijn ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="5a012-111">API permission must be enabled.</span></span> <span data-ttu-id="5a012-112">Zie [hoe inschakelen API-toegang in Salesforce door machtigingenset?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span><span class="sxs-lookup"><span data-stu-id="5a012-112">See [How do I enable API access in Salesforce by permission set?](https://www.data2crm.com/migration/faqs/enable-api-access-salesforce-permission-set/)</span></span>
* <span data-ttu-id="5a012-113">toocopy gegevens van Salesforce tooon-premises gegevensopslagexemplaren, hebt u ten minste Data Management Gateway 2.0 is geïnstalleerd in uw on-premises omgeving.</span><span class="sxs-lookup"><span data-stu-id="5a012-113">toocopy data from Salesforce tooon-premises data stores, you must have at least Data Management Gateway 2.0 installed in your on-premises environment.</span></span>

## <a name="salesforce-request-limits"></a><span data-ttu-id="5a012-114">SalesForce aanvraaglimieten</span><span class="sxs-lookup"><span data-stu-id="5a012-114">Salesforce request limits</span></span>
<span data-ttu-id="5a012-115">SalesForce heeft limieten voor totaal aantal API-aanvragen en de gelijktijdige API-aanvragen.</span><span class="sxs-lookup"><span data-stu-id="5a012-115">Salesforce has limits for both total API requests and concurrent API requests.</span></span> <span data-ttu-id="5a012-116">Houd er rekening mee Hallo volgende punten:</span><span class="sxs-lookup"><span data-stu-id="5a012-116">Note hello following points:</span></span>

- <span data-ttu-id="5a012-117">Als het aantal gelijktijdige aanvragen Hallo Hallo limiet overschrijdt, beperking plaatsvindt en worden er willekeurige fouten.</span><span class="sxs-lookup"><span data-stu-id="5a012-117">If hello number of concurrent requests exceeds hello limit, throttling occurs and you will see random failures.</span></span>
- <span data-ttu-id="5a012-118">Als het totale aantal aanvragen Hallo Hallo limiet overschrijdt, wordt Hallo Salesforce-account van 24 uur geblokkeerd.</span><span class="sxs-lookup"><span data-stu-id="5a012-118">If hello total number of requests exceeds hello limit, hello Salesforce account will be blocked for 24 hours.</span></span>

<span data-ttu-id="5a012-119">Hallo "REQUEST_LIMIT_EXCEEDED" fout kan ook worden weergegeven in beide scenario's.</span><span class="sxs-lookup"><span data-stu-id="5a012-119">You might also receive hello “REQUEST_LIMIT_EXCEEDED“ error in both scenarios.</span></span> <span data-ttu-id="5a012-120">Zie sectie Hallo 'API aanvraaglimieten' in hello [Salesforce Developer limieten](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) artikel voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5a012-120">See hello "API Request Limits" section in hello [Salesforce Developer Limits](http://resources.docs.salesforce.com/200/20/en-us/sfdc/pdf/salesforce_app_limits_cheatsheet.pdf) article for details.</span></span>

## <a name="getting-started"></a><span data-ttu-id="5a012-121">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="5a012-121">Getting started</span></span>
<span data-ttu-id="5a012-122">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens worden verplaatst van Salesforce met verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="5a012-122">You can create a pipeline with a copy activity that moves data from Salesforce by using different tools/APIs.</span></span>

<span data-ttu-id="5a012-123">Hallo gemakkelijkste manier toocreate een pijplijn is toouse hello **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="5a012-123">hello easiest way toocreate a pipeline is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="5a012-124">Zie [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md) voor een snel overzicht over het maken van een pijplijn met Hallo wizard kopiëren.</span><span class="sxs-lookup"><span data-stu-id="5a012-124">See [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) for a quick walkthrough on creating a pipeline using hello Copy data wizard.</span></span>

<span data-ttu-id="5a012-125">U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="5a012-125">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="5a012-126">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="5a012-126">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span> 

<span data-ttu-id="5a012-127">Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="5a012-127">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span> 

1. <span data-ttu-id="5a012-128">Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="5a012-128">Create **linked services** toolink input and output data stores tooyour data factory.</span></span>
2. <span data-ttu-id="5a012-129">Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="5a012-129">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> 
3. <span data-ttu-id="5a012-130">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="5a012-130">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> 

<span data-ttu-id="5a012-131">Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5a012-131">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="5a012-132">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="5a012-132">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="5a012-133">Zie voor een voorbeeld met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens van Salesforce zijn [JSON-voorbeeld: gegevens kopiëren van Salesforce tooAzure Blob](#json-example-copy-data-from-salesforce-to-azure-blob) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="5a012-133">For a sample with JSON definitions for Data Factory entities that are used toocopy data from Salesforce, see [JSON example: Copy data from Salesforce tooAzure Blob](#json-example-copy-data-from-salesforce-to-azure-blob) section of this article.</span></span> 

<span data-ttu-id="5a012-134">Hallo volgende secties bieden informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory-entiteiten specifieke tooSalesforce zijn:</span><span class="sxs-lookup"><span data-stu-id="5a012-134">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooSalesforce:</span></span> 

## <a name="linked-service-properties"></a><span data-ttu-id="5a012-135">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="5a012-135">Linked service properties</span></span>
<span data-ttu-id="5a012-136">Hallo volgende tabel bevat beschrijvingen van JSON-elementen die specifiek toohello Salesforce gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="5a012-136">hello following table provides descriptions for JSON elements that are specific toohello Salesforce linked service.</span></span>

| <span data-ttu-id="5a012-137">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="5a012-137">Property</span></span> | <span data-ttu-id="5a012-138">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="5a012-138">Description</span></span> | <span data-ttu-id="5a012-139">Vereist</span><span class="sxs-lookup"><span data-stu-id="5a012-139">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5a012-140">type</span><span class="sxs-lookup"><span data-stu-id="5a012-140">type</span></span> |<span data-ttu-id="5a012-141">Hallo type eigenschap moet worden ingesteld op: **Salesforce**.</span><span class="sxs-lookup"><span data-stu-id="5a012-141">hello type property must be set to: **Salesforce**.</span></span> |<span data-ttu-id="5a012-142">Ja</span><span class="sxs-lookup"><span data-stu-id="5a012-142">Yes</span></span> |
| <span data-ttu-id="5a012-143">environmentUrl</span><span class="sxs-lookup"><span data-stu-id="5a012-143">environmentUrl</span></span> | <span data-ttu-id="5a012-144">Hallo-URL van de Salesforce-exemplaar opgeven.</span><span class="sxs-lookup"><span data-stu-id="5a012-144">Specify hello URL of Salesforce instance.</span></span> <br><br> <span data-ttu-id="5a012-145">-Standaard is 'https://login.salesforce.com'.</span><span class="sxs-lookup"><span data-stu-id="5a012-145">- Default is "https://login.salesforce.com".</span></span> <br> <span data-ttu-id="5a012-146">-toocopy gegevens van de sandbox, 'https://test.salesforce.com' opgeven.</span><span class="sxs-lookup"><span data-stu-id="5a012-146">- toocopy data from sandbox, specify "https://test.salesforce.com".</span></span> <br> <span data-ttu-id="5a012-147">-toocopy gegevens van aangepast domein opgeven, bijvoorbeeld 'https://[domain].my.salesforce.com'.</span><span class="sxs-lookup"><span data-stu-id="5a012-147">- toocopy data from custom domain, specify, for example, "https://[domain].my.salesforce.com".</span></span> |<span data-ttu-id="5a012-148">Nee</span><span class="sxs-lookup"><span data-stu-id="5a012-148">No</span></span> |
| <span data-ttu-id="5a012-149">gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="5a012-149">username</span></span> |<span data-ttu-id="5a012-150">Geef een gebruikersnaam voor Hallo-gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="5a012-150">Specify a user name for hello user account.</span></span> |<span data-ttu-id="5a012-151">Ja</span><span class="sxs-lookup"><span data-stu-id="5a012-151">Yes</span></span> |
| <span data-ttu-id="5a012-152">wachtwoord</span><span class="sxs-lookup"><span data-stu-id="5a012-152">password</span></span> |<span data-ttu-id="5a012-153">Geef een wachtwoord voor gebruikersaccount Hallo.</span><span class="sxs-lookup"><span data-stu-id="5a012-153">Specify a password for hello user account.</span></span> |<span data-ttu-id="5a012-154">Ja</span><span class="sxs-lookup"><span data-stu-id="5a012-154">Yes</span></span> |
| <span data-ttu-id="5a012-155">securityToken</span><span class="sxs-lookup"><span data-stu-id="5a012-155">securityToken</span></span> |<span data-ttu-id="5a012-156">Geef een beveiligingstoken voor Hallo-gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="5a012-156">Specify a security token for hello user account.</span></span> <span data-ttu-id="5a012-157">Zie [security token ophalen](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) voor instructies over het tooreset of ophalen van een beveiligingstoken.</span><span class="sxs-lookup"><span data-stu-id="5a012-157">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how tooreset/get a security token.</span></span> <span data-ttu-id="5a012-158">toolearn over beveiligingstokens in het algemeen Zie [beveiligings- en Hallo API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span><span class="sxs-lookup"><span data-stu-id="5a012-158">toolearn about security tokens in general, see [Security and hello API](https://developer.salesforce.com/docs/atlas.en-us.api.meta/api/sforce_api_concepts_security.htm).</span></span> |<span data-ttu-id="5a012-159">Ja</span><span class="sxs-lookup"><span data-stu-id="5a012-159">Yes</span></span> |

## <a name="dataset-properties"></a><span data-ttu-id="5a012-160">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="5a012-160">Dataset properties</span></span>
<span data-ttu-id="5a012-161">Zie voor een volledige lijst van de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets en secties Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="5a012-161">For a full list of sections and properties that are available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="5a012-162">Secties zoals structuur, beschikbaarheid en beleid van een gegevensset JSON zijn identiek voor alle typen gegevensset (Azure blob Azure SQL Azure-tabel en enzovoort).</span><span class="sxs-lookup"><span data-stu-id="5a012-162">Sections such as structure, availability, and policy of a dataset JSON are similar for all dataset types (Azure SQL, Azure blob, Azure table, and so on).</span></span>

<span data-ttu-id="5a012-163">Hallo **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie over Hallo-locatie van gegevens in het gegevensarchief Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="5a012-163">hello **typeProperties** section is different for each type of dataset and provides information about hello location of hello data in hello data store.</span></span> <span data-ttu-id="5a012-164">Hallo typeProperties sectie voor een gegevensset van het type Hallo **RelationalTable** heeft Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="5a012-164">hello typeProperties section for a dataset of hello type **RelationalTable** has hello following properties:</span></span>

| <span data-ttu-id="5a012-165">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="5a012-165">Property</span></span> | <span data-ttu-id="5a012-166">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="5a012-166">Description</span></span> | <span data-ttu-id="5a012-167">Vereist</span><span class="sxs-lookup"><span data-stu-id="5a012-167">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5a012-168">tableName</span><span class="sxs-lookup"><span data-stu-id="5a012-168">tableName</span></span> |<span data-ttu-id="5a012-169">Naam van de tabel Hallo in Salesforce.</span><span class="sxs-lookup"><span data-stu-id="5a012-169">Name of hello table in Salesforce.</span></span> |<span data-ttu-id="5a012-170">Nee (als een **query** van **RelationalSource** is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="5a012-170">No (if a **query** of **RelationalSource** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="5a012-171">Hallo '__c' onderdeel Hallo API-naam is vereist voor elk object dat aangepast.</span><span class="sxs-lookup"><span data-stu-id="5a012-171">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Naam van de Data Factory - verbinding Salesforce - API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

## <a name="copy-activity-properties"></a><span data-ttu-id="5a012-173">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="5a012-173">Copy activity properties</span></span>
<span data-ttu-id="5a012-174">Zie voor een volledige lijst van de eigenschappen die beschikbaar zijn voor het definiëren van activiteiten en secties Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="5a012-174">For a full list of sections and properties that are available for defining activities, see hello [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="5a012-175">Eigenschappen, zoals naam, beschrijving, invoer en uitvoer tabellen en verschillende beleidsregels zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="5a012-175">Properties like name, description, input and output tables, and various policies are available for all types of activities.</span></span>

<span data-ttu-id="5a012-176">Hallo-eigenschappen die beschikbaar zijn in de sectie typeProperties van Hallo-activiteit op Hallo daarentegen Hallo, variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="5a012-176">hello properties that are available in hello typeProperties section of hello activity, on hello other hand, vary with each activity type.</span></span> <span data-ttu-id="5a012-177">Voor de Kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="5a012-177">For Copy Activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="5a012-178">In de kopieeractiviteit, wanneer bron Hallo Hallo type **RelationalSource** (waaronder Salesforce), Hallo volgende eigenschappen beschikbaar zijn in de sectie typeProperties:</span><span class="sxs-lookup"><span data-stu-id="5a012-178">In copy activity, when hello source is of hello type **RelationalSource** (which includes Salesforce), hello following properties are available in typeProperties section:</span></span>

| <span data-ttu-id="5a012-179">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="5a012-179">Property</span></span> | <span data-ttu-id="5a012-180">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="5a012-180">Description</span></span> | <span data-ttu-id="5a012-181">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="5a012-181">Allowed values</span></span> | <span data-ttu-id="5a012-182">Vereist</span><span class="sxs-lookup"><span data-stu-id="5a012-182">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="5a012-183">query</span><span class="sxs-lookup"><span data-stu-id="5a012-183">query</span></span> |<span data-ttu-id="5a012-184">Hallo aangepaste query tooread gegevens worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5a012-184">Use hello custom query tooread data.</span></span> |<span data-ttu-id="5a012-185">Een SQL-92-query of [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span><span class="sxs-lookup"><span data-stu-id="5a012-185">A SQL-92 query or [Salesforce Object Query Language (SOQL)](https://developer.salesforce.com/docs/atlas.en-us.soql_sosl.meta/soql_sosl/sforce_api_calls_soql.htm) query.</span></span> <span data-ttu-id="5a012-186">Bijvoorbeeld `select * from MyTable__c`.</span><span class="sxs-lookup"><span data-stu-id="5a012-186">For example:  `select * from MyTable__c`.</span></span> |<span data-ttu-id="5a012-187">Nee (als hello **tableName** Hallo **gegevensset** is opgegeven)</span><span class="sxs-lookup"><span data-stu-id="5a012-187">No (if hello **tableName** of hello **dataset** is specified)</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="5a012-188">Hallo '__c' onderdeel Hallo API-naam is vereist voor elk object dat aangepast.</span><span class="sxs-lookup"><span data-stu-id="5a012-188">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Naam van de Data Factory - verbinding Salesforce - API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)

## <a name="query-tips"></a><span data-ttu-id="5a012-190">Tips voor query</span><span class="sxs-lookup"><span data-stu-id="5a012-190">Query tips</span></span>
### <a name="retrieving-data-using-where-clause-on-datetime-column"></a><span data-ttu-id="5a012-191">Bij het ophalen van gegevens met behulp van waar component voor datum/tijd-kolom</span><span class="sxs-lookup"><span data-stu-id="5a012-191">Retrieving data using where clause on DateTime column</span></span>
<span data-ttu-id="5a012-192">Geef bij de Hallo SOQL of SQL-query, betalen aandacht toohello verschil van datum/tijd-indeling.</span><span class="sxs-lookup"><span data-stu-id="5a012-192">When specify hello SOQL or SQL query, pay attention toohello DateTime format difference.</span></span> <span data-ttu-id="5a012-193">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="5a012-193">For example:</span></span>

* <span data-ttu-id="5a012-194">**Voorbeeld van SOQL**:`$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="5a012-194">**SOQL sample**: `$$Text.Format('SELECT Id, Name, BillingCity FROM Account WHERE LastModifiedDate >= {0:yyyy-MM-ddTHH:mm:ssZ} AND LastModifiedDate < {1:yyyy-MM-ddTHH:mm:ssZ}', WindowStart, WindowEnd)`</span></span>
* <span data-ttu-id="5a012-195">**SQL-voorbeeld**:</span><span class="sxs-lookup"><span data-stu-id="5a012-195">**SQL sample**:</span></span>
    * <span data-ttu-id="5a012-196">**Met behulp van kopie wizard toospecify Hallo query:**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="5a012-196">**Using copy wizard toospecify hello query:** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\'{0:yyyy-MM-dd HH:mm:ss}\'}} AND LastModifiedDate < {{ts\'{1:yyyy-MM-dd HH:mm:ss}\'}}', WindowStart, WindowEnd)`</span></span>
    * <span data-ttu-id="5a012-197">**Met een JSON toospecify Hallo query bewerken (char goed escape):**`$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span><span class="sxs-lookup"><span data-stu-id="5a012-197">**Using JSON editing toospecify hello query (escape char properly):** `$$Text.Format('SELECT * FROM Account WHERE LastModifiedDate >= {{ts\\'{0:yyyy-MM-dd HH:mm:ss}\\'}} AND LastModifiedDate < {{ts\\'{1:yyyy-MM-dd HH:mm:ss}\\'}}', WindowStart, WindowEnd)`</span></span>

### <a name="retrieving-data-from-salesforce-report"></a><span data-ttu-id="5a012-198">Ophalen van gegevens uit het Salesforce-rapport</span><span class="sxs-lookup"><span data-stu-id="5a012-198">Retrieving data from Salesforce Report</span></span>
<span data-ttu-id="5a012-199">U kunt gegevens ophalen uit het Salesforce-rapporten door te geven van de query als `{call "<report name>"}`, bijvoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="5a012-199">You can retrieve data from Salesforce reports by specifying query as `{call "<report name>"}`,for example,.</span></span> <span data-ttu-id="5a012-200">`"query": "{call \"TestReport\"}"`.</span><span class="sxs-lookup"><span data-stu-id="5a012-200">`"query": "{call \"TestReport\"}"`.</span></span>

### <a name="retrieving-deleted-records-from-salesforce-recycle-bin"></a><span data-ttu-id="5a012-201">Bij het ophalen van records verwijderd uit Salesforce Prullenbak</span><span class="sxs-lookup"><span data-stu-id="5a012-201">Retrieving deleted records from Salesforce Recycle Bin</span></span>
<span data-ttu-id="5a012-202">tooquery hello voorlopig verwijderde records uit Salesforce-Prullenbak, kunt u **' IsDeleted = 1 "** in uw query.</span><span class="sxs-lookup"><span data-stu-id="5a012-202">tooquery hello soft deleted records from Salesforce Recycle Bin, you can specify **"IsDeleted = 1"** in your query.</span></span> <span data-ttu-id="5a012-203">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="5a012-203">For example,</span></span>

* <span data-ttu-id="5a012-204">tooquery alleen Hallo verwijderde records opgeven "Selecteer * uit MyTable__c **waar IsDeleted = 1**'</span><span class="sxs-lookup"><span data-stu-id="5a012-204">tooquery only hello deleted records, specify "select * from MyTable__c **where IsDeleted= 1**"</span></span>
* <span data-ttu-id="5a012-205">alle records Hallo bestaande en Hallo verwijderd, inclusief Hallo tooquery opgeven "Selecteer * uit MyTable__c **waar IsDeleted = 0 of IsDeleted = 1**'</span><span class="sxs-lookup"><span data-stu-id="5a012-205">tooquery all hello records including hello existing and hello deleted, specify "select * from MyTable__c **where IsDeleted = 0 or IsDeleted = 1**"</span></span>

## <a name="json-example-copy-data-from-salesforce-tooazure-blob"></a><span data-ttu-id="5a012-206">JSON-voorbeeld: gegevens kopiëren van Salesforce tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="5a012-206">JSON example: Copy data from Salesforce tooAzure Blob</span></span>
<span data-ttu-id="5a012-207">Hallo volgende voorbeeld wordt een voorbeeld JSON definities waarmee u een pijplijn toocreate kunt met behulp van Hallo [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="5a012-207">hello following example provides sample JSON definitions that you can use toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="5a012-208">Ze geven weer hoe toocopy gegevens van Salesforce tooAzure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="5a012-208">They show how toocopy data from Salesforce tooAzure Blob Storage.</span></span> <span data-ttu-id="5a012-209">Gegevens kunnen echter wel gekopieerde tooany van Hallo put vermeld [hier](data-factory-data-movement-activities.md#supported-data-stores-and-formats) met behulp van Hallo Kopieeractiviteit in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="5a012-209">However, data can be copied tooany of hello sinks stated [here](data-factory-data-movement-activities.md#supported-data-stores-and-formats) using hello Copy Activity in Azure Data Factory.</span></span>   

<span data-ttu-id="5a012-210">Hier volgen Hallo Data Factory-artefacten moet u toocreate tooimplement Hallo scenario.</span><span class="sxs-lookup"><span data-stu-id="5a012-210">Here are hello Data Factory artifacts that you'll need toocreate tooimplement hello scenario.</span></span> <span data-ttu-id="5a012-211">Hallo gedeelten Hallo lijst vindt u meer informatie over deze stappen.</span><span class="sxs-lookup"><span data-stu-id="5a012-211">hello sections that follow hello list provide details about these steps.</span></span>

* <span data-ttu-id="5a012-212">Een gekoppelde service van het type Hallo [Salesforce](#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="5a012-212">A linked service of hello type [Salesforce](#linked-service-properties)</span></span>
* <span data-ttu-id="5a012-213">Een gekoppelde service van het type Hallo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span><span class="sxs-lookup"><span data-stu-id="5a012-213">A linked service of hello type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties)</span></span>
* <span data-ttu-id="5a012-214">Invoer [gegevensset](data-factory-create-datasets.md) van het type Hallo [RelationalTable](#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="5a012-214">An input [dataset](data-factory-create-datasets.md) of hello type [RelationalTable](#dataset-properties)</span></span>
* <span data-ttu-id="5a012-215">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type Hallo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span><span class="sxs-lookup"><span data-stu-id="5a012-215">An output [dataset](data-factory-create-datasets.md) of hello type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties)</span></span>
* <span data-ttu-id="5a012-216">Een [pijplijn](data-factory-create-pipelines.md) met de Kopieeractiviteit die gebruikmaakt van [RelationalSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span><span class="sxs-lookup"><span data-stu-id="5a012-216">A [pipeline](data-factory-create-pipelines.md) with Copy Activity that uses [RelationalSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties)</span></span>

<span data-ttu-id="5a012-217">**SalesForce gekoppelde service**</span><span class="sxs-lookup"><span data-stu-id="5a012-217">**Salesforce linked service**</span></span>

<span data-ttu-id="5a012-218">In dit voorbeeld wordt Hallo **Salesforce** gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="5a012-218">This example uses hello **Salesforce** linked service.</span></span> <span data-ttu-id="5a012-219">Zie Hallo [Salesforce gekoppelde service](#linked-service-properties) gedeelte voor het Hallo-eigenschappen die worden ondersteund door deze gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="5a012-219">See hello [Salesforce linked service](#linked-service-properties) section for hello properties that are supported by this linked service.</span></span>  <span data-ttu-id="5a012-220">Zie [security token ophalen](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) voor instructies over hoe tooreset/get Hallo-beveiligingstoken.</span><span class="sxs-lookup"><span data-stu-id="5a012-220">See [Get security token](https://help.salesforce.com/apex/HTViewHelpDoc?id=user_security_token.htm) for instructions on how tooreset/get hello security token.</span></span>

```json
{
    "name": "SalesforceLinkedService",
    "properties":
    {
        "type": "Salesforce",
        "typeProperties":
        {
            "username": "<user name>",
            "password": "<password>",
            "securityToken": "<security token>"
        }
    }
}
```
<span data-ttu-id="5a012-221">**Een gekoppelde Azure Storage-service**</span><span class="sxs-lookup"><span data-stu-id="5a012-221">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="5a012-222">**SalesForce invoergegevensset**</span><span class="sxs-lookup"><span data-stu-id="5a012-222">**Salesforce input dataset**</span></span>

```json
{
    "name": "SalesforceInput",
    "properties": {
        "linkedServiceName": "SalesforceLinkedService",
        "type": "RelationalTable",
        "typeProperties": {
            "tableName": "AllDataType__c"  
        },
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

<span data-ttu-id="5a012-223">Instelling **externe** te**true** informeert Hallo Data Factory-service die gegevensset Hallo externe toohello data factory is en niet door een activiteit in de gegevensfactory hello wordt geproduceerd.</span><span class="sxs-lookup"><span data-stu-id="5a012-223">Setting **external** too**true** informs hello Data Factory service that hello dataset is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5a012-224">Hallo '__c' onderdeel Hallo API-naam is vereist voor elk object dat aangepast.</span><span class="sxs-lookup"><span data-stu-id="5a012-224">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Naam van de Data Factory - verbinding Salesforce - API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name.png)

<span data-ttu-id="5a012-226">**De Azure Blob-uitvoergegevensset**</span><span class="sxs-lookup"><span data-stu-id="5a012-226">**Azure blob output dataset**</span></span>

<span data-ttu-id="5a012-227">Gegevens worden geschreven tooa nieuwe blob elk uur (frequentie: uur, interval: 1).</span><span class="sxs-lookup"><span data-stu-id="5a012-227">Data is written tooa new blob every hour (frequency: hour, interval: 1).</span></span>

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties":
        {
            "folderPath": "adfgetstarted/alltypes_c"
        },
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

<span data-ttu-id="5a012-228">**Pijplijn met de Kopieeractiviteit**</span><span class="sxs-lookup"><span data-stu-id="5a012-228">**Pipeline with Copy Activity**</span></span>

<span data-ttu-id="5a012-229">Hallo pipeline bevat Kopieeractiviteit die wordt geconfigureerd toouse Hallo invoer- en uitvoergegevenssets en geplande toorun is om het uur.</span><span class="sxs-lookup"><span data-stu-id="5a012-229">hello pipeline contains Copy Activity, which is configured toouse hello input and output datasets, and is scheduled toorun every hour.</span></span> <span data-ttu-id="5a012-230">Hallo in Hallo pijplijn-JSON-definitie, **bron** type is ingesteld, te**RelationalSource**, en Hallo **sink** type is ingesteld, te**BlobSink**.</span><span class="sxs-lookup"><span data-stu-id="5a012-230">In hello pipeline JSON definition, hello **source** type is set too**RelationalSource**, and hello **sink** type is set too**BlobSink**.</span></span>

<span data-ttu-id="5a012-231">Zie [RelationalSource type-eigenschappen](#copy-activity-properties) voor Hallo lijst met eigenschappen die worden ondersteund door Hallo RelationalSource.</span><span class="sxs-lookup"><span data-stu-id="5a012-231">See [RelationalSource type properties](#copy-activity-properties) for hello list of properties that are supported by hello RelationalSource.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2016-06-01T18:00:00",
        "end":"2016-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":[  
        {
            "name": "SalesforceToAzureBlob",
            "description": "Copy from Salesforce tooan Azure blob",
            "type": "Copy",
            "inputs": [
            {
                "name": "SalesforceInput"
            }
            ],
            "outputs": [
            {
                "name": "AzureBlobOutput"
            }
            ],
            "typeProperties": {
                "source": {
                    "type": "RelationalSource",
                    "query": "SELECT Id, Col_AutoNumber__c, Col_Checkbox__c, Col_Currency__c, Col_Date__c, Col_DateTime__c, Col_Email__c, Col_Number__c, Col_Percent__c, Col_Phone__c, Col_Picklist__c, Col_Picklist_MultiSelect__c, Col_Text__c, Col_Text_Area__c, Col_Text_AreaLong__c, Col_Text_AreaRich__c, Col_URL__c, Col_Text_Encrypt__c, Col_Lookup__c FROM AllDataType__c"                
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
> [!IMPORTANT]
> <span data-ttu-id="5a012-232">Hallo '__c' onderdeel Hallo API-naam is vereist voor elk object dat aangepast.</span><span class="sxs-lookup"><span data-stu-id="5a012-232">hello "__c" part of hello API Name is needed for any custom object.</span></span>

![Naam van de Data Factory - verbinding Salesforce - API](media/data-factory-salesforce-connector/data-factory-salesforce-api-name-2.png)


### <a name="type-mapping-for-salesforce"></a><span data-ttu-id="5a012-234">Toewijzing van het type voor Salesforce</span><span class="sxs-lookup"><span data-stu-id="5a012-234">Type mapping for Salesforce</span></span>
| <span data-ttu-id="5a012-235">SalesForce-type</span><span class="sxs-lookup"><span data-stu-id="5a012-235">Salesforce type</span></span> | <span data-ttu-id="5a012-236">. Type op basis van NET</span><span class="sxs-lookup"><span data-stu-id="5a012-236">.NET-based type</span></span> |
| --- | --- |
| <span data-ttu-id="5a012-237">Automatische getal</span><span class="sxs-lookup"><span data-stu-id="5a012-237">Auto Number</span></span> |<span data-ttu-id="5a012-238">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="5a012-238">String</span></span> |
| <span data-ttu-id="5a012-239">Selectievakje</span><span class="sxs-lookup"><span data-stu-id="5a012-239">Checkbox</span></span> |<span data-ttu-id="5a012-240">Booleaanse waarde</span><span class="sxs-lookup"><span data-stu-id="5a012-240">Boolean</span></span> |
| <span data-ttu-id="5a012-241">Valuta</span><span class="sxs-lookup"><span data-stu-id="5a012-241">Currency</span></span> |<span data-ttu-id="5a012-242">dubbele</span><span class="sxs-lookup"><span data-stu-id="5a012-242">Double</span></span> |
| <span data-ttu-id="5a012-243">Date</span><span class="sxs-lookup"><span data-stu-id="5a012-243">Date</span></span> |<span data-ttu-id="5a012-244">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="5a012-244">DateTime</span></span> |
| <span data-ttu-id="5a012-245">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="5a012-245">Date/Time</span></span> |<span data-ttu-id="5a012-246">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="5a012-246">DateTime</span></span> |
| <span data-ttu-id="5a012-247">E-mail</span><span class="sxs-lookup"><span data-stu-id="5a012-247">Email</span></span> |<span data-ttu-id="5a012-248">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="5a012-248">String</span></span> |
| <span data-ttu-id="5a012-249">Id</span><span class="sxs-lookup"><span data-stu-id="5a012-249">Id</span></span> |<span data-ttu-id="5a012-250">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="5a012-250">String</span></span> |
| <span data-ttu-id="5a012-251">Opzoekrelatie</span><span class="sxs-lookup"><span data-stu-id="5a012-251">Lookup Relationship</span></span> |<span data-ttu-id="5a012-252">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="5a012-252">String</span></span> |
| <span data-ttu-id="5a012-253">Meervoudige selectie selectielijst</span><span class="sxs-lookup"><span data-stu-id="5a012-253">Multi-Select Picklist</span></span> |<span data-ttu-id="5a012-254">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="5a012-254">String</span></span> |
| <span data-ttu-id="5a012-255">Aantal</span><span class="sxs-lookup"><span data-stu-id="5a012-255">Number</span></span> |<span data-ttu-id="5a012-256">dubbele</span><span class="sxs-lookup"><span data-stu-id="5a012-256">Double</span></span> |
| <span data-ttu-id="5a012-257">Procent</span><span class="sxs-lookup"><span data-stu-id="5a012-257">Percent</span></span> |<span data-ttu-id="5a012-258">dubbele</span><span class="sxs-lookup"><span data-stu-id="5a012-258">Double</span></span> |
| <span data-ttu-id="5a012-259">Telefoon</span><span class="sxs-lookup"><span data-stu-id="5a012-259">Phone</span></span> |<span data-ttu-id="5a012-260">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="5a012-260">String</span></span> |
| <span data-ttu-id="5a012-261">Selectielijst</span><span class="sxs-lookup"><span data-stu-id="5a012-261">Picklist</span></span> |<span data-ttu-id="5a012-262">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="5a012-262">String</span></span> |
| <span data-ttu-id="5a012-263">Tekst</span><span class="sxs-lookup"><span data-stu-id="5a012-263">Text</span></span> |<span data-ttu-id="5a012-264">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="5a012-264">String</span></span> |
| <span data-ttu-id="5a012-265">Tekstgebied</span><span class="sxs-lookup"><span data-stu-id="5a012-265">Text Area</span></span> |<span data-ttu-id="5a012-266">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="5a012-266">String</span></span> |
| <span data-ttu-id="5a012-267">Tekstgebied (lang)</span><span class="sxs-lookup"><span data-stu-id="5a012-267">Text Area (Long)</span></span> |<span data-ttu-id="5a012-268">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="5a012-268">String</span></span> |
| <span data-ttu-id="5a012-269">Tekstgebied (uitgebreid)</span><span class="sxs-lookup"><span data-stu-id="5a012-269">Text Area (Rich)</span></span> |<span data-ttu-id="5a012-270">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="5a012-270">String</span></span> |
| <span data-ttu-id="5a012-271">Tekst (versleuteld)</span><span class="sxs-lookup"><span data-stu-id="5a012-271">Text (Encrypted)</span></span> |<span data-ttu-id="5a012-272">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="5a012-272">String</span></span> |
| <span data-ttu-id="5a012-273">URL</span><span class="sxs-lookup"><span data-stu-id="5a012-273">URL</span></span> |<span data-ttu-id="5a012-274">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="5a012-274">String</span></span> |

> [!NOTE]
> <span data-ttu-id="5a012-275">toomap kolommen uit de bron gegevensset toocolumns uit sink gegevensset, Zie [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="5a012-275">toomap columns from source dataset toocolumns from sink dataset, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

[!INCLUDE [data-factory-structure-for-rectangualr-datasets](../../includes/data-factory-structure-for-rectangualr-datasets.md)]

## <a name="performance-and-tuning"></a><span data-ttu-id="5a012-276">Prestaties en afstemmen</span><span class="sxs-lookup"><span data-stu-id="5a012-276">Performance and tuning</span></span>
<span data-ttu-id="5a012-277">Zie Hallo [Kopieeractiviteit prestaties en prestatieafstemming handleiding](data-factory-copy-activity-performance.md) toolearn over sleutel factoren die prestaties impact van gegevensverplaatsing (Kopieeractiviteit) in Azure Data Factory en verschillende manieren toooptimize deze.</span><span class="sxs-lookup"><span data-stu-id="5a012-277">See hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) toolearn about key factors that impact performance of data movement (Copy Activity) in Azure Data Factory and various ways toooptimize it.</span></span>
