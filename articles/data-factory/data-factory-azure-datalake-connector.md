---
title: aaaCopy gegevens tooand van Azure Data Lake Store | Microsoft Docs
description: Meer informatie over hoe toocopy gegevens tooand van Data Lake Store met behulp van Azure Data Factory
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 25b1ff3c-b2fd-48e5-b759-bb2112122e30
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: jingwang
ms.openlocfilehash: 2e78f75f3821738332dacf70f6bf2c16f0136408
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-data-lake-store-by-using-data-factory"></a><span data-ttu-id="4b6b1-103">Kopiëren van gegevens tooand van Data Lake Store via Data Factory</span><span class="sxs-lookup"><span data-stu-id="4b6b1-103">Copy data tooand from Data Lake Store by using Data Factory</span></span>
<span data-ttu-id="4b6b1-104">Dit artikel wordt uitgelegd hoe toouse Kopieeractiviteit in Azure Data Factory toomove gegevens tooand van Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-104">This article explains how toouse Copy Activity in Azure Data Factory toomove data tooand from Azure Data Lake Store.</span></span> <span data-ttu-id="4b6b1-105">Dit is gebaseerd op Hallo [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, een overzicht van de verplaatsing van gegevens met de Kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-105">It builds on hello [Data movement activities](data-factory-data-movement-activities.md) article, an overview of data movement with Copy Activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="4b6b1-106">Ondersteunde scenario 's</span><span class="sxs-lookup"><span data-stu-id="4b6b1-106">Supported scenarios</span></span>
<span data-ttu-id="4b6b1-107">U kunt gegevens kopiëren **van Azure Data Lake Store** toohello gegevensarchieven te volgen:</span><span class="sxs-lookup"><span data-stu-id="4b6b1-107">You can copy data **from Azure Data Lake Store** toohello following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="4b6b1-108">Gegevens kunnen worden gekopieerd van de volgende gegevensarchieven Hallo **tooAzure Data Lake Store**:</span><span class="sxs-lookup"><span data-stu-id="4b6b1-108">You can copy data from hello following data stores **tooAzure Data Lake Store**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="4b6b1-109">Een Data Lake Store-account maken voordat u een pijplijn maakt met de Kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-109">Create a Data Lake Store account before creating a pipeline with Copy Activity.</span></span> <span data-ttu-id="4b6b1-110">Zie voor meer informatie [aan de slag met Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4b6b1-110">For more information, see [Get started with Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="4b6b1-111">Ondersteunde verificatietypen</span><span class="sxs-lookup"><span data-stu-id="4b6b1-111">Supported authentication types</span></span>
<span data-ttu-id="4b6b1-112">Hallo Data Lake Store-connector ondersteunt de volgende verificatietypen:</span><span class="sxs-lookup"><span data-stu-id="4b6b1-112">hello Data Lake Store connector supports these authentication types:</span></span>
* <span data-ttu-id="4b6b1-113">Verificatie van service-principal</span><span class="sxs-lookup"><span data-stu-id="4b6b1-113">Service principal authentication</span></span>
* <span data-ttu-id="4b6b1-114">Verificatie van gebruikersreferenties (OAuth)</span><span class="sxs-lookup"><span data-stu-id="4b6b1-114">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="4b6b1-115">Het is raadzaam dat u service-principal verificatie, met name voor een geplande gegevens opnieuw te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-115">We recommend that you use service principal authentication, especially for a scheduled data copy.</span></span> <span data-ttu-id="4b6b1-116">Verlopen van het token kan gebeuren met verificatie van gebruikersreferenties.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-116">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="4b6b1-117">Zie voor configuratiedetails Hallo [gekoppelde service-eigenschappen](#linked-service-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-117">For configuration details, see hello [Linked service properties](#linked-service-properties) section.</span></span>

## <a name="get-started"></a><span data-ttu-id="4b6b1-118">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="4b6b1-118">Get started</span></span>
<span data-ttu-id="4b6b1-119">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens worden verplaatst van een Azure Data Lake Store met verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-119">You can create a pipeline with a copy activity that moves data to/from an Azure Data Lake Store by using different tools/APIs.</span></span>

<span data-ttu-id="4b6b1-120">Hallo gemakkelijkste manier toocreate een pijplijn toocopy gegevens is toouse hello **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-120">hello easiest way toocreate a pipeline toocopy data is toouse hello **Copy Wizard**.</span></span> <span data-ttu-id="4b6b1-121">Zie voor een zelfstudie over het maken van een pijplijn met behulp van de Wizard kopiëren Hallo [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="4b6b1-121">For a tutorial on creating a pipeline by using hello Copy Wizard, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="4b6b1-122">U kunt ook Hallo toocreate hulpprogramma's voor een pijplijn te volgen: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon** , **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-122">You can also use hello following tools toocreate a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="4b6b1-123">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies toocreate een pijplijn met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions toocreate a pipeline with a copy activity.</span></span>

<span data-ttu-id="4b6b1-124">Of u Hallo-hulpprogramma's of API's gebruiken, kunt u Hallo stappen toocreate een pijplijn die verplaatst gegevens uit een brongegevens tooa sink data store opslaan na uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="4b6b1-124">Whether you use hello tools or APIs, you perform hello following steps toocreate a pipeline that moves data from a source data store tooa sink data store:</span></span>

1. <span data-ttu-id="4b6b1-125">Maak een **gegevensfactory**.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-125">Create a **data factory**.</span></span> <span data-ttu-id="4b6b1-126">Een gegevensfactory kan één of meer pijplijnen bevatten.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="4b6b1-127">Maak **gekoppelde services** toolink en uitvoergegevens winkels tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-127">Create **linked services** toolink input and output data stores tooyour data factory.</span></span> <span data-ttu-id="4b6b1-128">Bijvoorbeeld, als u gegevens uit een Azure blob storage tooan Azure Data Lake Store kopiëren wilt, u twee gekoppelde services toolink uw Azure storage-account en de Azure Data Lake store tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-128">For example, if you are copying data from an Azure blob storage tooan Azure Data Lake Store, you create two linked services toolink your Azure storage account and Azure Data Lake store tooyour data factory.</span></span> <span data-ttu-id="4b6b1-129">Zie voor de gekoppelde service-eigenschappen die specifiek tooAzure Data Lake Store, [gekoppelde service-eigenschappen](#linked-service-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-129">For linked service properties that are specific tooAzure Data Lake Store, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="4b6b1-130">Maak **gegevenssets** toorepresent invoer en uitvoer gegevens voor Hallo voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-130">Create **datasets** toorepresent input and output data for hello copy operation.</span></span> <span data-ttu-id="4b6b1-131">In vermeld in de laatste stap Hallo Hallo voorbeeld maakt u een gegevensset toospecify Hallo blob-container en map met invoergegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-131">In hello example mentioned in hello last step, you create a dataset toospecify hello blob container and folder that contains hello input data.</span></span> <span data-ttu-id="4b6b1-132">En u een andere dataset toospecify Hallo map en het bestandspad in Hallo Data Lake store Hallo gegevens gekopieerd van de blob-opslag Hallo bevat maken.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-132">And, you create another dataset toospecify hello folder and file path in hello Data Lake store that holds hello data copied from hello blob storage.</span></span> <span data-ttu-id="4b6b1-133">Zie voor eigenschappen van gegevensset die specifieke tooAzure Data Lake Store, [eigenschappen van gegevensset](#dataset-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-133">For dataset properties that are specific tooAzure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="4b6b1-134">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="4b6b1-135">In Hallo voorbeeld eerder vermeld, gebruikt u BlobSource als een bron- en AzureDataLakeStoreSink als een sink voor de kopieeractiviteit Hallo.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-135">In hello example mentioned earlier, you use BlobSource as a source and AzureDataLakeStoreSink as a sink for hello copy activity.</span></span> <span data-ttu-id="4b6b1-136">Op dezelfde manier als u van Azure Data Lake Store tooAzure Blob Storage kopiëren wilt, gebruikt u AzureDataLakeStoreSource en BlobSink in Hallo kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-136">Similarly, if you are copying from Azure Data Lake Store tooAzure Blob Storage, you use AzureDataLakeStoreSource  and BlobSink in hello copy activity.</span></span> <span data-ttu-id="4b6b1-137">Zie voor activiteitseigenschappen kopiëren die specifieke tooAzure Data Lake Store, [activiteitseigenschappen kopiëren](#copy-activity-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-137">For copy activity properties that are specific tooAzure Data Lake Store, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="4b6b1-138">Voor informatie over hoe toouse een gegevensarchief als een bron of een sink, klikt u op Hallo-koppeling in de vorige sectie Hallo voor de gegevensopslag.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-138">For details on how toouse a data store as a source or a sink, click hello link in hello previous section for your data store.</span></span>  

<span data-ttu-id="4b6b1-139">Wanneer u de wizard Hallo gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn Hallo) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-139">When you use hello wizard, JSON definitions for these Data Factory entities (linked services, datasets, and hello pipeline) are automatically created for you.</span></span> <span data-ttu-id="4b6b1-140">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van Hallo JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using hello JSON format.</span></span>  <span data-ttu-id="4b6b1-141">Zie voor voorbeelden met JSON-definities voor Data Factory-entiteiten die gebruikt toocopy gegevens van/naar een Azure Data Lake Store zijn, [JSON voorbeelden](#json-examples-for-copying-data-to-and-from-data-lake-store) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-141">For samples with JSON definitions for Data Factory entities that are used toocopy data to/from an Azure Data Lake Store, see [JSON examples](#json-examples-for-copying-data-to-and-from-data-lake-store) section of this article.</span></span>

<span data-ttu-id="4b6b1-142">Hallo volgende secties bevatten informatie over de JSON-eigenschappen die gebruikt toodefine Data Factory entiteiten specifieke tooData Lake Store zijn.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-142">hello following sections provide details about JSON properties that are used toodefine Data Factory entities specific tooData Lake Store.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="4b6b1-143">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="4b6b1-143">Linked service properties</span></span>
<span data-ttu-id="4b6b1-144">Een gekoppelde service een gegevensfactory store tooa gegevens gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-144">A linked service links a data store tooa data factory.</span></span> <span data-ttu-id="4b6b1-145">Maken van een gekoppelde service van het type **AzureDataLakeStore** toolink uw Data Lake Store gegevens tooyour data factory.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-145">You create a linked service of type **AzureDataLakeStore** toolink your Data Lake Store data tooyour data factory.</span></span> <span data-ttu-id="4b6b1-146">Hallo volgende tabel beschrijft de JSON-elementen specifieke tooData Lake Store gekoppelde services.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-146">hello following table describes JSON elements specific tooData Lake Store linked services.</span></span> <span data-ttu-id="4b6b1-147">U kunt kiezen tussen service-principal en verificatie van gebruikersreferenties.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-147">You can choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="4b6b1-148">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="4b6b1-148">Property</span></span> | <span data-ttu-id="4b6b1-149">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4b6b1-149">Description</span></span> | <span data-ttu-id="4b6b1-150">Vereist</span><span class="sxs-lookup"><span data-stu-id="4b6b1-150">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="4b6b1-151">**type**</span><span class="sxs-lookup"><span data-stu-id="4b6b1-151">**type**</span></span> | <span data-ttu-id="4b6b1-152">de eigenschap type Hello te moet worden ingesteld**AzureDataLakeStore**.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-152">hello type property must be set too**AzureDataLakeStore**.</span></span> | <span data-ttu-id="4b6b1-153">Ja</span><span class="sxs-lookup"><span data-stu-id="4b6b1-153">Yes</span></span> |
| <span data-ttu-id="4b6b1-154">**dataLakeStoreUri**</span><span class="sxs-lookup"><span data-stu-id="4b6b1-154">**dataLakeStoreUri**</span></span> | <span data-ttu-id="4b6b1-155">Informatie over hello Azure Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-155">Information about hello Azure Data Lake Store account.</span></span> <span data-ttu-id="4b6b1-156">Deze informatie heeft een van de volgende indelingen Hallo: `https://[accountname].azuredatalakestore.net/webhdfs/v1` of `adl://[accountname].azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-156">This information takes one of hello following formats: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="4b6b1-157">Ja</span><span class="sxs-lookup"><span data-stu-id="4b6b1-157">Yes</span></span> |
| <span data-ttu-id="4b6b1-158">**abonnements-id**</span><span class="sxs-lookup"><span data-stu-id="4b6b1-158">**subscriptionId**</span></span> | <span data-ttu-id="4b6b1-159">Azure-abonnement-ID toowhich Hallo Data Lake Store-account hoort.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-159">Azure subscription ID toowhich hello Data Lake Store account belongs.</span></span> | <span data-ttu-id="4b6b1-160">Vereist voor sink</span><span class="sxs-lookup"><span data-stu-id="4b6b1-160">Required for sink</span></span> |
| <span data-ttu-id="4b6b1-161">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="4b6b1-161">**resourceGroupName**</span></span> | <span data-ttu-id="4b6b1-162">Azure resource group name toowhich Hallo Data Lake Store-account hoort.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-162">Azure resource group name toowhich hello Data Lake Store account belongs.</span></span> | <span data-ttu-id="4b6b1-163">Vereist voor sink</span><span class="sxs-lookup"><span data-stu-id="4b6b1-163">Required for sink</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="4b6b1-164">Verificatie van de service principal (aanbevolen)</span><span class="sxs-lookup"><span data-stu-id="4b6b1-164">Service principal authentication (recommended)</span></span>
<span data-ttu-id="4b6b1-165">toouse service principal verificatie, de registratie een Toepassingsentiteit in Azure Active Directory (Azure AD) en verleen het Hallo toegang krijgen tot de tooData Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-165">toouse service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it hello access tooData Lake Store.</span></span> <span data-ttu-id="4b6b1-166">Zie voor gedetailleerde stappen [authentication Service-naar-serviceconnector](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="4b6b1-166">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="4b6b1-167">Noteer Hallo waarden, waarin u volgende toodefine Hallo gekoppelde service:</span><span class="sxs-lookup"><span data-stu-id="4b6b1-167">Make note of hello following values, which you use toodefine hello linked service:</span></span>
* <span data-ttu-id="4b6b1-168">Toepassings-id</span><span class="sxs-lookup"><span data-stu-id="4b6b1-168">Application ID</span></span>
* <span data-ttu-id="4b6b1-169">Sleutel van toepassing</span><span class="sxs-lookup"><span data-stu-id="4b6b1-169">Application key</span></span> 
* <span data-ttu-id="4b6b1-170">Tenant-id</span><span class="sxs-lookup"><span data-stu-id="4b6b1-170">Tenant ID</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4b6b1-171">Als u van Hallo Wizard kopiëren tooauthor gegevenspijplijnen gebruikmaakt, zorgt u ervoor dat u service-principal Hallo verlenen ten minste een **lezer** rol in toegangsbeheer (identiteits- en toegangsbeheer management) voor Hallo Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-171">If you are using hello Copy Wizard tooauthor data pipelines, make sure that you grant hello service principal at least a **Reader** role in access control (identity and access management) for hello Data Lake Store account.</span></span> <span data-ttu-id="4b6b1-172">Ook ten minste verlenen Hallo service-principal **lezen + Execute** machtiging tooyour Data Lake Store hoofdmap ('/') en de onderliggende items.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-172">Also, grant hello service principal at least **Read + Execute** permission tooyour Data Lake Store root ("/") and its children.</span></span> <span data-ttu-id="4b6b1-173">Anders ziet u mogelijk het Hallo-bericht "hello opgegeven referenties zijn ongeldig."</span><span class="sxs-lookup"><span data-stu-id="4b6b1-173">Otherwise you might see hello message "hello credentials provided are invalid."</span></span><br/><br/>
<span data-ttu-id="4b6b1-174">Nadat u maken of bijwerken van een service-principal in Azure AD, kan het enkele minuten duren voordat Hallo wijzigingen tootake effect.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-174">After you create or update a service principal in Azure AD, it can take a few minutes for hello changes tootake effect.</span></span> <span data-ttu-id="4b6b1-175">Controleer Hallo service-principal en Data Lake Store-besturingselement toegangsbeheerlijst (ACL) configuraties.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-175">Check hello service principal and Data Lake Store access control list (ACL) configurations.</span></span> <span data-ttu-id="4b6b1-176">Als u nog steeds het Hallo-bericht 'hello opgegeven referenties zijn ongeldig' ziet, wacht even en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-176">If you still see hello message "hello credentials provided are invalid," wait a while and try again.</span></span>

<span data-ttu-id="4b6b1-177">Verificatie van de service-principal door te geven van de volgende eigenschappen hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="4b6b1-177">Use service principal authentication by specifying hello following properties:</span></span>

| <span data-ttu-id="4b6b1-178">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="4b6b1-178">Property</span></span> | <span data-ttu-id="4b6b1-179">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4b6b1-179">Description</span></span> | <span data-ttu-id="4b6b1-180">Vereist</span><span class="sxs-lookup"><span data-stu-id="4b6b1-180">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="4b6b1-181">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="4b6b1-181">**servicePrincipalId**</span></span> | <span data-ttu-id="4b6b1-182">Geef Hallo van client-id op.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-182">Specify hello application's client ID.</span></span> | <span data-ttu-id="4b6b1-183">Ja</span><span class="sxs-lookup"><span data-stu-id="4b6b1-183">Yes</span></span> |
| <span data-ttu-id="4b6b1-184">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="4b6b1-184">**servicePrincipalKey**</span></span> | <span data-ttu-id="4b6b1-185">De sleutel van de toepassing hello opgeven.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-185">Specify hello application's key.</span></span> | <span data-ttu-id="4b6b1-186">Ja</span><span class="sxs-lookup"><span data-stu-id="4b6b1-186">Yes</span></span> |
| <span data-ttu-id="4b6b1-187">**tenant**</span><span class="sxs-lookup"><span data-stu-id="4b6b1-187">**tenant**</span></span> | <span data-ttu-id="4b6b1-188">Geef informatie op Hallo tenant (domain name of tenant-ID) in uw toepassing zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-188">Specify hello tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="4b6b1-189">U kunt deze ophalen door zwevende Hallo muis in Hallo rechterbovenhoek Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-189">You can retrieve it by hovering hello mouse in hello upper-right corner of hello Azure portal.</span></span> | <span data-ttu-id="4b6b1-190">Ja</span><span class="sxs-lookup"><span data-stu-id="4b6b1-190">Yes</span></span> |

<span data-ttu-id="4b6b1-191">**Voorbeeld: Service-principal-verificatie**</span><span class="sxs-lookup"><span data-stu-id="4b6b1-191">**Example: Service principal authentication**</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

### <a name="user-credential-authentication"></a><span data-ttu-id="4b6b1-192">Verificatie van gebruikersreferenties</span><span class="sxs-lookup"><span data-stu-id="4b6b1-192">User credential authentication</span></span>
<span data-ttu-id="4b6b1-193">U kunt ook kunt u gebruiker referentie verificatie toocopy uit of tooData Lake Store door te geven Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="4b6b1-193">Alternatively, you can use user credential authentication toocopy from or tooData Lake Store by specifying hello following properties:</span></span>

| <span data-ttu-id="4b6b1-194">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="4b6b1-194">Property</span></span> | <span data-ttu-id="4b6b1-195">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4b6b1-195">Description</span></span> | <span data-ttu-id="4b6b1-196">Vereist</span><span class="sxs-lookup"><span data-stu-id="4b6b1-196">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="4b6b1-197">**autorisatie**</span><span class="sxs-lookup"><span data-stu-id="4b6b1-197">**authorization**</span></span> | <span data-ttu-id="4b6b1-198">Klik op Hallo **autoriseren** knop op Hallo Data Factory-Editor en voer uw referenties die Hallo automatisch gegenereerde autorisatie-URL toothis eigenschap toewijst.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-198">Click hello **Authorize** button in hello Data Factory Editor and enter your credential that assigns hello autogenerated authorization URL toothis property.</span></span> | <span data-ttu-id="4b6b1-199">Ja</span><span class="sxs-lookup"><span data-stu-id="4b6b1-199">Yes</span></span> |
| <span data-ttu-id="4b6b1-200">**sessie-id**</span><span class="sxs-lookup"><span data-stu-id="4b6b1-200">**sessionId**</span></span> | <span data-ttu-id="4b6b1-201">OAuth-sessie-ID van Hallo OAuth-autorisatie-sessie.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-201">OAuth session ID from hello OAuth authorization session.</span></span> <span data-ttu-id="4b6b1-202">Elke sessie-ID is uniek en kan slechts één keer worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-202">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="4b6b1-203">Deze instelling wordt automatisch gegenereerd wanneer u Hallo Data Factory-Editor.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-203">This setting is automatically generated when you use hello Data Factory Editor.</span></span> | <span data-ttu-id="4b6b1-204">Ja</span><span class="sxs-lookup"><span data-stu-id="4b6b1-204">Yes</span></span> |

<span data-ttu-id="4b6b1-205">**Voorbeeld: Verificatie van gebruikersreferenties**</span><span class="sxs-lookup"><span data-stu-id="4b6b1-205">**Example: User credential authentication**</span></span>
```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "sessionId": "<session ID>",
            "authorization": "<authorization URL>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

#### <a name="token-expiration"></a><span data-ttu-id="4b6b1-206">Verlopen van het token</span><span class="sxs-lookup"><span data-stu-id="4b6b1-206">Token expiration</span></span>
<span data-ttu-id="4b6b1-207">Autorisatiecode die u genereren met behulp van Hallo Hallo **autoriseren** knop verloopt na een bepaalde hoeveelheid tijd.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-207">hello authorization code that you generate by using hello **Authorize** button expires after a certain amount of time.</span></span> <span data-ttu-id="4b6b1-208">Hallo volgende bericht betekent dat verificatie Hallo token is verlopen:</span><span class="sxs-lookup"><span data-stu-id="4b6b1-208">hello following message means that hello authentication token has expired:</span></span>

<span data-ttu-id="4b6b1-209">Referentie-bewerkingsfout: invalid_grant - AADSTS70002: fout bij het valideren van referenties.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-209">Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="4b6b1-210">AADSTS70008: Hallo opgegeven toegangsmachtiging is verlopen of ingetrokken.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-210">AADSTS70008: hello provided access grant is expired or revoked.</span></span> <span data-ttu-id="4b6b1-211">Traceer-ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 correlatie-ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 tijdstempel: 2015-12-15 21-09-31Z.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-211">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21-09-31Z.</span></span>

<span data-ttu-id="4b6b1-212">Hallo volgende tabel ziet u Hallo verlopen tijden van verschillende typen gebruikersaccounts:</span><span class="sxs-lookup"><span data-stu-id="4b6b1-212">hello following table shows hello expiration times of different types of user accounts:</span></span>


| <span data-ttu-id="4b6b1-213">Gebruikerstype</span><span class="sxs-lookup"><span data-stu-id="4b6b1-213">User type</span></span> | <span data-ttu-id="4b6b1-214">Verloopt na</span><span class="sxs-lookup"><span data-stu-id="4b6b1-214">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="4b6b1-215">Gebruikersaccounts *niet* beheerd door Azure Active Directory (bijvoorbeeld @hotmail.com of @live.com)</span><span class="sxs-lookup"><span data-stu-id="4b6b1-215">User accounts *not* managed by Azure Active Directory (for example, @hotmail.com or @live.com)</span></span> |<span data-ttu-id="4b6b1-216">12 uur</span><span class="sxs-lookup"><span data-stu-id="4b6b1-216">12 hours</span></span> |
| <span data-ttu-id="4b6b1-217">Gebruikersaccounts worden beheerd door Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b6b1-217">Users accounts managed by Azure Active Directory</span></span> |<span data-ttu-id="4b6b1-218">het is 14 dagen na de laatste segment Hallo uitvoeren</span><span class="sxs-lookup"><span data-stu-id="4b6b1-218">14 days after hello last slice run</span></span> <br/><br/><span data-ttu-id="4b6b1-219">Als een segment op basis van een gekoppelde op basis van het OAuth-service wordt uitgevoerd in de 14 dagen ten minste eenmaal na 90 dagen</span><span class="sxs-lookup"><span data-stu-id="4b6b1-219">90 days, if a slice based on an OAuth-based linked service runs at least once every 14 days</span></span> |

<span data-ttu-id="4b6b1-220">Als u uw wachtwoord vóór Hallo token verlooptijd vallen wijzigt, wordt de Hallo-token onmiddellijk verloopt.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-220">If you change your password before hello token expiration time, hello token expires immediately.</span></span> <span data-ttu-id="4b6b1-221">Hier ziet u eerder in deze sectie het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-221">You will see hello message mentioned earlier in this section.</span></span>

<span data-ttu-id="4b6b1-222">U kunt opnieuw autoriseren hello account met behulp van Hallo **autoriseren** knop wanneer Hallo-token tooredeploy Hallo verloopt gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-222">You can reauthorize hello account by using hello **Authorize** button when hello token expires tooredeploy hello linked service.</span></span> <span data-ttu-id="4b6b1-223">U kunt ook de waarden voor Hallo genereren **sessionId** en **autorisatie** eigenschappen programmatisch met behulp van Hallo volgende code:</span><span class="sxs-lookup"><span data-stu-id="4b6b1-223">You can also generate values for hello **sessionId** and **authorization** properties programmatically by using hello following code:</span></span>


```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```
<span data-ttu-id="4b6b1-224">Zie voor meer informatie over Data Factory-klassen Hallo gebruikt in code Hallo Hallo [AzureDataLakeStoreLinkedService klasse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService klasse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), en [ Klasse AuthorizationSessionGetResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-224">For details about hello Data Factory classes used in hello code, see hello [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics.</span></span> <span data-ttu-id="4b6b1-225">Voeg een verwijzing tooversion `2.9.10826.1824` van `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` voor Hallo `WindowsFormsWebAuthenticationDialog` klasse die wordt gebruikt in Hallo-code.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-225">Add a reference tooversion `2.9.10826.1824` of `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` for hello `WindowsFormsWebAuthenticationDialog` class used in hello code.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="4b6b1-226">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="4b6b1-226">Dataset properties</span></span>
<span data-ttu-id="4b6b1-227">toospecify een gegevensset toorepresent gegevens invoeren in een Data Lake Store, stelt u Hallo **type** eigenschap van het Hallo-gegevensset te**AzureDataLakeStore**.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-227">toospecify a dataset toorepresent input data in a Data Lake Store, you set hello **type** property of hello dataset too**AzureDataLakeStore**.</span></span> <span data-ttu-id="4b6b1-228">Set Hallo **linkedServiceName** eigenschap van de naam van dataset toohello Hallo Hallo Data Lake Store gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-228">Set hello **linkedServiceName** property of hello dataset toohello name of hello Data Lake Store linked service.</span></span> <span data-ttu-id="4b6b1-229">Zie voor een volledige lijst van JSON-secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets Hallo [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-229">For a full list of JSON sections and properties available for defining datasets, see hello [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="4b6b1-230">Secties van een gegevensset in JSON, zoals **structuur**, **beschikbaarheid**, en **beleid**, zijn identiek voor alle typen van de gegevensset (Azure SQL-database, blob van Azure en Azure-tabel voor voorbeeld).</span><span class="sxs-lookup"><span data-stu-id="4b6b1-230">Sections of a dataset in JSON, such as **structure**, **availability**, and **policy**, are similar for all dataset types (Azure SQL database, Azure blob, and Azure table, for example).</span></span> <span data-ttu-id="4b6b1-231">Hallo **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie zoals de locatie en indeling van gegevens in het gegevensarchief Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-231">hello **typeProperties** section is different for each type of dataset and provides information such as location and format of hello data in hello data store.</span></span> 

<span data-ttu-id="4b6b1-232">Hallo **typeProperties** sectie voor een gegevensset van het type **AzureDataLakeStore** bevat Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="4b6b1-232">hello **typeProperties** section for a dataset of type **AzureDataLakeStore** contains hello following properties:</span></span>

| <span data-ttu-id="4b6b1-233">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="4b6b1-233">Property</span></span> | <span data-ttu-id="4b6b1-234">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4b6b1-234">Description</span></span> | <span data-ttu-id="4b6b1-235">Vereist</span><span class="sxs-lookup"><span data-stu-id="4b6b1-235">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="4b6b1-236">**folderPath**</span><span class="sxs-lookup"><span data-stu-id="4b6b1-236">**folderPath**</span></span> |<span data-ttu-id="4b6b1-237">Pad toohello container en map in Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-237">Path toohello container and folder in Data Lake Store.</span></span> |<span data-ttu-id="4b6b1-238">Ja</span><span class="sxs-lookup"><span data-stu-id="4b6b1-238">Yes</span></span> |
| <span data-ttu-id="4b6b1-239">**Bestandsnaam**</span><span class="sxs-lookup"><span data-stu-id="4b6b1-239">**fileName**</span></span> |<span data-ttu-id="4b6b1-240">Naam van het Hallo-bestand in Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-240">Name of hello file in Azure Data Lake Store.</span></span> <span data-ttu-id="4b6b1-241">Hallo **fileName** eigenschap is optioneel en is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-241">hello **fileName** property is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="4b6b1-242">Als u opgeeft **fileName**, Hallo activiteit (inclusief kopiëren) werkt op Hallo specifiek bestand.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-242">If you specify **fileName**, hello activity (including Copy) works on hello specific file.</span></span><br/><br/><span data-ttu-id="4b6b1-243">Wanneer **fileName** niet is opgegeven, kopie bevat alle bestanden in **folderPath** in Hallo invoergegevensset.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-243">When **fileName** is not specified, Copy includes all files in **folderPath** in hello input dataset.</span></span><br/><br/><span data-ttu-id="4b6b1-244">Wanneer **fileName** is niet opgegeven voor een uitvoergegevensset en **preserveHierarchy** niet is opgegeven in activiteit sink Hallo-naam van Hallo gegenereerd bestand heeft Hallo indeling gegevens. _GUID_.txt'.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-244">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, hello name of hello generated file is in hello format Data._Guid_.txt\`.</span></span> <span data-ttu-id="4b6b1-245">Voorbeeld: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-245">For example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.</span></span> |<span data-ttu-id="4b6b1-246">Nee</span><span class="sxs-lookup"><span data-stu-id="4b6b1-246">No</span></span> |
| <span data-ttu-id="4b6b1-247">**partitionedBy**</span><span class="sxs-lookup"><span data-stu-id="4b6b1-247">**partitionedBy**</span></span> |<span data-ttu-id="4b6b1-248">Hallo **partitionedBy** eigenschap is optioneel.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-248">hello **partitionedBy** property is optional.</span></span> <span data-ttu-id="4b6b1-249">U kunt deze toospecify een dynamische pad en bestandsnaam voor timeseries gegevens.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-249">You can use it toospecify a dynamic path and file name for time-series data.</span></span> <span data-ttu-id="4b6b1-250">Bijvoorbeeld: **folderPath** kunnen als parameters worden gebruikt voor elk uur van gegevens.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-250">For example, **folderPath** can be parameterized for every hour of data.</span></span> <span data-ttu-id="4b6b1-251">Zie voor meer informatie en voorbeelden [Hallo eigenschap partitionedBy](#using-partitionedby-property).</span><span class="sxs-lookup"><span data-stu-id="4b6b1-251">For details and examples, see [hello partitionedBy property](#using-partitionedby-property).</span></span> |<span data-ttu-id="4b6b1-252">Nee</span><span class="sxs-lookup"><span data-stu-id="4b6b1-252">No</span></span> |
| <span data-ttu-id="4b6b1-253">**indeling**</span><span class="sxs-lookup"><span data-stu-id="4b6b1-253">**format**</span></span> | <span data-ttu-id="4b6b1-254">Hallo na indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, en  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-254">hello following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, and **ParquetFormat**.</span></span> <span data-ttu-id="4b6b1-255">Set Hallo **type** eigenschap onder **indeling** tooone van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-255">Set hello **type** property under **format** tooone of these values.</span></span> <span data-ttu-id="4b6b1-256">Zie voor meer informatie, Hallo [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [JSON-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [ORC indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren-indeling ](data-factory-supported-file-and-compression-formats.md#parquet-format) secties in Hallo [bestands- en compressie indelingen die worden ondersteund door Azure Data Factory](data-factory-supported-file-and-compression-formats.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-256">For more information, see hello [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [ORC format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections in hello [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span> <br><br> <span data-ttu-id="4b6b1-257">Als u toocopy bestanden wilt ' als-is ' tussen bestandsgebaseerde winkels (binaire kopiëren) overslaan Hallo `format` sectie in beide definities invoer en uitvoer gegevensset.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-257">If you want toocopy files "as-is" between file-based stores (binary copy), skip hello `format` section in both input and output dataset definitions.</span></span> |<span data-ttu-id="4b6b1-258">Nee</span><span class="sxs-lookup"><span data-stu-id="4b6b1-258">No</span></span> |
| <span data-ttu-id="4b6b1-259">**compressie**</span><span class="sxs-lookup"><span data-stu-id="4b6b1-259">**compression**</span></span> | <span data-ttu-id="4b6b1-260">Hallo-type en compressieniveau voor Hallo gegevens opgeven.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-260">Specify hello type and level of compression for hello data.</span></span> <span data-ttu-id="4b6b1-261">Ondersteunde typen zijn **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-261">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="4b6b1-262">Ondersteunde niveaus zijn **optimale** en **snelst**.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-262">Supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="4b6b1-263">Zie voor meer informatie [bestands- en compressie indelingen die worden ondersteund door Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="4b6b1-263">For more information, see [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="4b6b1-264">Nee</span><span class="sxs-lookup"><span data-stu-id="4b6b1-264">No</span></span> |

### <a name="hello-partitionedby-property"></a><span data-ttu-id="4b6b1-265">Hallo partitionedBy eigenschap</span><span class="sxs-lookup"><span data-stu-id="4b6b1-265">hello partitionedBy property</span></span>
<span data-ttu-id="4b6b1-266">Kunt u dynamische **folderPath** en **fileName** eigenschappen voor timeseries gegevens met Hallo **partitionedBy** eigenschap, Data Factory-functies en het systeem variabelen.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-266">You can specify dynamic **folderPath** and **fileName** properties for time-series data with hello **partitionedBy** property, Data Factory functions, and system variables.</span></span> <span data-ttu-id="4b6b1-267">Zie voor meer informatie, Hallo [Azure Data Factory - functies en systeemvariabelen](data-factory-functions-variables.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-267">For details, see hello [Azure Data Factory - functions and system variables](data-factory-functions-variables.md) article.</span></span>


<span data-ttu-id="4b6b1-268">In Hallo bijvoorbeeld na `{Slice}` is vervangen door de waarde Hallo van Hallo Data Factory systeemvariabele `SliceStart` in de opgegeven indeling Hallo (`yyyyMMddHH`).</span><span class="sxs-lookup"><span data-stu-id="4b6b1-268">In hello following example, `{Slice}` is replaced with hello value of hello Data Factory system variable `SliceStart` in hello format specified (`yyyyMMddHH`).</span></span> <span data-ttu-id="4b6b1-269">de naam van de Hallo `SliceStart` toohello begintijd van Hallo segment verwijst.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-269">hello name `SliceStart` refers toohello start time of hello slice.</span></span> <span data-ttu-id="4b6b1-270">Hallo `folderPath` eigenschap verschilt voor elk segment, zoals in `wikidatagateway/wikisampledataout/2014100103` of `wikidatagateway/wikisampledataout/2014100104`.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-270">hello `folderPath` property is different for each slice, as in `wikidatagateway/wikisampledataout/2014100103` or `wikidatagateway/wikisampledataout/2014100104`.</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="4b6b1-271">In het volgende voorbeeld, Hallo jaar, maand, dag en tijd van Hallo `SliceStart` worden uitgepakt in verschillende variabelen die worden gebruikt door Hallo `folderPath` en `fileName` eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="4b6b1-271">In hello following example, hello year, month, day, and time of `SliceStart` are extracted into separate variables that are used by hello `folderPath` and `fileName` properties:</span></span>
```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
<span data-ttu-id="4b6b1-272">Voor meer informatie over tijdreeks gegevenssets planning en segmenten, Zie Hallo [gegevenssets in Azure Data Factory](data-factory-create-datasets.md) en [Data Factory plannen en uitvoeren](data-factory-scheduling-and-execution.md) artikelen.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-272">For more details on time-series datasets, scheduling, and slices, see hello [Datasets in Azure Data Factory](data-factory-create-datasets.md) and [Data Factory scheduling and execution](data-factory-scheduling-and-execution.md) articles.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="4b6b1-273">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="4b6b1-273">Copy activity properties</span></span>
<span data-ttu-id="4b6b1-274">Zie voor een volledige lijst van de eigenschappen die beschikbaar zijn voor het definiëren van activiteiten en secties Hallo [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-274">For a full list of sections and properties available for defining activities, see hello [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="4b6b1-275">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en -beleid zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-275">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="4b6b1-276">eigenschappen die beschikbaar zijn in Hallo Hallo **typeProperties** gedeelte van een activiteit variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-276">hello properties available in hello **typeProperties** section of an activity vary with each activity type.</span></span> <span data-ttu-id="4b6b1-277">Voor een kopieeractiviteit variëren ze, afhankelijk van de soorten Hallo van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-277">For a copy activity, they vary depending on hello types of sources and sinks.</span></span>

<span data-ttu-id="4b6b1-278">**AzureDataLakeStoreSource** ondersteunt de volgende eigenschap in Hallo Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="4b6b1-278">**AzureDataLakeStoreSource** supports hello following property in hello **typeProperties** section:</span></span>

| <span data-ttu-id="4b6b1-279">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="4b6b1-279">Property</span></span> | <span data-ttu-id="4b6b1-280">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4b6b1-280">Description</span></span> | <span data-ttu-id="4b6b1-281">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="4b6b1-281">Allowed values</span></span> | <span data-ttu-id="4b6b1-282">Vereist</span><span class="sxs-lookup"><span data-stu-id="4b6b1-282">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4b6b1-283">**recursieve**</span><span class="sxs-lookup"><span data-stu-id="4b6b1-283">**recursive**</span></span> |<span data-ttu-id="4b6b1-284">Hiermee wordt aangegeven of Hallo gegevens recursief is gelezen vanuit Hallo submappen of alleen vanuit de opgegeven map Hallo.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-284">Indicates whether hello data is read recursively from hello subfolders or only from hello specified folder.</span></span> |<span data-ttu-id="4b6b1-285">True (standaardwaarde), False</span><span class="sxs-lookup"><span data-stu-id="4b6b1-285">True (default value), False</span></span> |<span data-ttu-id="4b6b1-286">Nee</span><span class="sxs-lookup"><span data-stu-id="4b6b1-286">No</span></span> |


<span data-ttu-id="4b6b1-287">**AzureDataLakeStoreSink** ondersteunt de volgende eigenschappen in Hallo Hallo **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="4b6b1-287">**AzureDataLakeStoreSink** supports hello following properties in hello **typeProperties** section:</span></span>

| <span data-ttu-id="4b6b1-288">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="4b6b1-288">Property</span></span> | <span data-ttu-id="4b6b1-289">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4b6b1-289">Description</span></span> | <span data-ttu-id="4b6b1-290">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="4b6b1-290">Allowed values</span></span> | <span data-ttu-id="4b6b1-291">Vereist</span><span class="sxs-lookup"><span data-stu-id="4b6b1-291">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="4b6b1-292">**copyBehavior**</span><span class="sxs-lookup"><span data-stu-id="4b6b1-292">**copyBehavior**</span></span> |<span data-ttu-id="4b6b1-293">Hiermee geeft u Hallo kopie gedrag.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-293">Specifies hello copy behavior.</span></span> |<span data-ttu-id="4b6b1-294"><b>PreserveHierarchy</b>: Hallo bestandshiërarchie in de doelmap Hallo behouden blijft.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-294"><b>PreserveHierarchy</b>: Preserves hello file hierarchy in hello target folder.</span></span> <span data-ttu-id="4b6b1-295">Hallo relatieve pad van de bestandsmap toosource bron is identiek toohello relatieve pad van de bestandsmap tootarget doel.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-295">hello relative path of source file toosource folder is identical toohello relative path of target file tootarget folder.</span></span><br/><br/><span data-ttu-id="4b6b1-296"><b>FlattenHierarchy</b>: alle bestanden uit de bronmap Hallo worden gemaakt in het eerste niveau van de doelmap Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-296"><b>FlattenHierarchy</b>: All files from hello source folder are created in hello first level of hello target folder.</span></span> <span data-ttu-id="4b6b1-297">Hallo doelbestanden worden gemaakt met de automatisch gegenereerde namen.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-297">hello target files are created with autogenerated names.</span></span><br/><br/><span data-ttu-id="4b6b1-298"><b>MergeFiles</b>: alle bestanden uit map Hallo-tooone bronbestand worden samengevoegd.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-298"><b>MergeFiles</b>: Merges all files from hello source folder tooone file.</span></span> <span data-ttu-id="4b6b1-299">Als hello bestand of de blob-naam wordt opgegeven, is de samengevoegde bestandsnaam Hallo Hallo opgegeven naam.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-299">If hello file or blob name is specified, hello merged file name is hello specified name.</span></span> <span data-ttu-id="4b6b1-300">Hallo-bestandsnaam is anders wordt automatisch gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-300">Otherwise, hello file name is autogenerated.</span></span> |<span data-ttu-id="4b6b1-301">Nee</span><span class="sxs-lookup"><span data-stu-id="4b6b1-301">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="4b6b1-302">Voorbeelden van recursieve en copyBehavior</span><span class="sxs-lookup"><span data-stu-id="4b6b1-302">recursive and copyBehavior examples</span></span>
<span data-ttu-id="4b6b1-303">Deze sectie beschrijft Hallo resulterende gedrag van de kopieerbewerking Hallo voor verschillende combinaties van recursieve en copyBehavior waarden.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-303">This section describes hello resulting behavior of hello Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="4b6b1-304">Recursieve</span><span class="sxs-lookup"><span data-stu-id="4b6b1-304">recursive</span></span> | <span data-ttu-id="4b6b1-305">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="4b6b1-305">copyBehavior</span></span> | <span data-ttu-id="4b6b1-306">Resulterende gedrag</span><span class="sxs-lookup"><span data-stu-id="4b6b1-306">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4b6b1-307">De waarde True</span><span class="sxs-lookup"><span data-stu-id="4b6b1-307">true</span></span> |<span data-ttu-id="4b6b1-308">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="4b6b1-308">preserveHierarchy</span></span> |<span data-ttu-id="4b6b1-309">Voor een bronmap Map1 Hello structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="4b6b1-309">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="4b6b1-310">Map1</span><span class="sxs-lookup"><span data-stu-id="4b6b1-310">Folder1</span></span><br/><span data-ttu-id="4b6b1-311">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="4b6b1-311">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="4b6b1-312">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="4b6b1-312">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="4b6b1-313">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="4b6b1-313">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="4b6b1-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="4b6b1-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="4b6b1-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="4b6b1-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="4b6b1-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="4b6b1-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="4b6b1-317">Hallo doelmap Map1 wordt gemaakt met dezelfde structuur, als de bron Hallo Hallo</span><span class="sxs-lookup"><span data-stu-id="4b6b1-317">hello target folder Folder1 is created with hello same structure as hello source</span></span><br/><br/><span data-ttu-id="4b6b1-318">Map1</span><span class="sxs-lookup"><span data-stu-id="4b6b1-318">Folder1</span></span><br/><span data-ttu-id="4b6b1-319">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="4b6b1-319">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="4b6b1-320">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="4b6b1-320">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="4b6b1-321">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="4b6b1-321">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="4b6b1-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="4b6b1-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="4b6b1-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="4b6b1-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="4b6b1-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="4b6b1-325">De waarde True</span><span class="sxs-lookup"><span data-stu-id="4b6b1-325">true</span></span> |<span data-ttu-id="4b6b1-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="4b6b1-326">flattenHierarchy</span></span> |<span data-ttu-id="4b6b1-327">Voor een bronmap Map1 Hello structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="4b6b1-327">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="4b6b1-328">Map1</span><span class="sxs-lookup"><span data-stu-id="4b6b1-328">Folder1</span></span><br/><span data-ttu-id="4b6b1-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="4b6b1-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="4b6b1-330">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="4b6b1-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="4b6b1-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="4b6b1-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="4b6b1-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="4b6b1-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="4b6b1-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="4b6b1-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="4b6b1-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="4b6b1-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="4b6b1-335">Hallo doel Map1 is gemaakt met de Hallo structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="4b6b1-335">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="4b6b1-336">Map1</span><span class="sxs-lookup"><span data-stu-id="4b6b1-336">Folder1</span></span><br/><span data-ttu-id="4b6b1-337">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor File1</span><span class="sxs-lookup"><span data-stu-id="4b6b1-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="4b6b1-338">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor bestand2</span><span class="sxs-lookup"><span data-stu-id="4b6b1-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="4b6b1-339">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor bestand3</span><span class="sxs-lookup"><span data-stu-id="4b6b1-339">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="4b6b1-340">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor File4</span><span class="sxs-lookup"><span data-stu-id="4b6b1-340">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="4b6b1-341">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor File5</span><span class="sxs-lookup"><span data-stu-id="4b6b1-341">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="4b6b1-342">De waarde True</span><span class="sxs-lookup"><span data-stu-id="4b6b1-342">true</span></span> |<span data-ttu-id="4b6b1-343">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="4b6b1-343">mergeFiles</span></span> |<span data-ttu-id="4b6b1-344">Voor een bronmap Map1 Hello structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="4b6b1-344">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="4b6b1-345">Map1</span><span class="sxs-lookup"><span data-stu-id="4b6b1-345">Folder1</span></span><br/><span data-ttu-id="4b6b1-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="4b6b1-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="4b6b1-347">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="4b6b1-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="4b6b1-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="4b6b1-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="4b6b1-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="4b6b1-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="4b6b1-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="4b6b1-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="4b6b1-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="4b6b1-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="4b6b1-352">Hallo doel Map1 is gemaakt met de Hallo structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="4b6b1-352">hello target Folder1 is created with hello following structure:</span></span> <br/><br/><span data-ttu-id="4b6b1-353">Map1</span><span class="sxs-lookup"><span data-stu-id="4b6b1-353">Folder1</span></span><br/><span data-ttu-id="4b6b1-354">&nbsp;&nbsp;&nbsp;&nbsp;File1 bestand2 + bestand3 + File4 + bestand 5 inhoud worden samengevoegd in één bestand met automatisch gegenereerde naam</span><span class="sxs-lookup"><span data-stu-id="4b6b1-354">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="4b6b1-355">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="4b6b1-355">false</span></span> |<span data-ttu-id="4b6b1-356">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="4b6b1-356">preserveHierarchy</span></span> |<span data-ttu-id="4b6b1-357">Voor een bronmap Map1 Hello structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="4b6b1-357">For a source folder Folder1 with hello following structure:</span></span> <br/><br/><span data-ttu-id="4b6b1-358">Map1</span><span class="sxs-lookup"><span data-stu-id="4b6b1-358">Folder1</span></span><br/><span data-ttu-id="4b6b1-359">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="4b6b1-359">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="4b6b1-360">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="4b6b1-360">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="4b6b1-361">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="4b6b1-361">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="4b6b1-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="4b6b1-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="4b6b1-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="4b6b1-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="4b6b1-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="4b6b1-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="4b6b1-365">Hallo doelmap Map1 wordt gemaakt met de Hallo structuur te volgen</span><span class="sxs-lookup"><span data-stu-id="4b6b1-365">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="4b6b1-366">Map1</span><span class="sxs-lookup"><span data-stu-id="4b6b1-366">Folder1</span></span><br/><span data-ttu-id="4b6b1-367">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="4b6b1-367">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="4b6b1-368">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="4b6b1-368">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="4b6b1-369">Subfolder1 bestand3 File4 en File5 zijn niet opgenomen.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-369">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="4b6b1-370">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="4b6b1-370">false</span></span> |<span data-ttu-id="4b6b1-371">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="4b6b1-371">flattenHierarchy</span></span> |<span data-ttu-id="4b6b1-372">Voor een bronmap Map1 Hello structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="4b6b1-372">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="4b6b1-373">Map1</span><span class="sxs-lookup"><span data-stu-id="4b6b1-373">Folder1</span></span><br/><span data-ttu-id="4b6b1-374">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="4b6b1-374">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="4b6b1-375">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="4b6b1-375">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="4b6b1-376">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="4b6b1-376">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="4b6b1-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="4b6b1-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="4b6b1-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="4b6b1-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="4b6b1-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="4b6b1-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="4b6b1-380">Hallo doelmap Map1 wordt gemaakt met de Hallo structuur te volgen</span><span class="sxs-lookup"><span data-stu-id="4b6b1-380">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="4b6b1-381">Map1</span><span class="sxs-lookup"><span data-stu-id="4b6b1-381">Folder1</span></span><br/><span data-ttu-id="4b6b1-382">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor File1</span><span class="sxs-lookup"><span data-stu-id="4b6b1-382">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="4b6b1-383">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor bestand2</span><span class="sxs-lookup"><span data-stu-id="4b6b1-383">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="4b6b1-384">Subfolder1 bestand3 File4 en File5 zijn niet opgenomen.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-384">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="4b6b1-385">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="4b6b1-385">false</span></span> |<span data-ttu-id="4b6b1-386">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="4b6b1-386">mergeFiles</span></span> |<span data-ttu-id="4b6b1-387">Voor een bronmap Map1 Hello structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="4b6b1-387">For a source folder Folder1 with hello following structure:</span></span><br/><br/><span data-ttu-id="4b6b1-388">Map1</span><span class="sxs-lookup"><span data-stu-id="4b6b1-388">Folder1</span></span><br/><span data-ttu-id="4b6b1-389">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="4b6b1-389">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="4b6b1-390">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="4b6b1-390">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="4b6b1-391">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="4b6b1-391">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="4b6b1-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="4b6b1-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="4b6b1-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="4b6b1-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="4b6b1-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="4b6b1-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="4b6b1-395">Hallo doelmap Map1 wordt gemaakt met de Hallo structuur te volgen</span><span class="sxs-lookup"><span data-stu-id="4b6b1-395">hello target folder Folder1 is created with hello following structure</span></span><br/><br/><span data-ttu-id="4b6b1-396">Map1</span><span class="sxs-lookup"><span data-stu-id="4b6b1-396">Folder1</span></span><br/><span data-ttu-id="4b6b1-397">&nbsp;&nbsp;&nbsp;&nbsp;File1 + bestand2 inhoud worden samengevoegd in één bestand met automatisch gegenereerde naam.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-397">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="4b6b1-398">automatisch gegenereerde naam voor File1</span><span class="sxs-lookup"><span data-stu-id="4b6b1-398">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="4b6b1-399">Subfolder1 bestand3 File4 en File5 zijn niet opgenomen.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-399">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="4b6b1-400">Ondersteunde indelingen voor bestands- en compressie</span><span class="sxs-lookup"><span data-stu-id="4b6b1-400">Supported file and compression formats</span></span>
<span data-ttu-id="4b6b1-401">Zie voor meer informatie, Hallo [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-401">For details, see hello [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span>

## <a name="json-examples-for-copying-data-tooand-from-data-lake-store"></a><span data-ttu-id="4b6b1-402">JSON-voorbeelden voor het kopiëren van gegevens tooand van Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4b6b1-402">JSON examples for copying data tooand from Data Lake Store</span></span>
<span data-ttu-id="4b6b1-403">Hallo volgen voorbeelden bieden voorbeeld JSON definities.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-403">hello following examples provide sample JSON definitions.</span></span> <span data-ttu-id="4b6b1-404">U kunt deze voorbeeld definities toocreate een pijplijn met behulp van Hallo [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="4b6b1-404">You can use these sample definitions toocreate a pipeline by using hello [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="4b6b1-405">voorbeelden kunt u zien hoe Hallo toocopy gegevens tooand van Data Lake Store en Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-405">hello examples show how toocopy data tooand from Data Lake Store and Azure Blob storage.</span></span> <span data-ttu-id="4b6b1-406">Echter, de gegevens kunnen worden gekopieerd _rechtstreeks_ vanaf elke Hallo bronnen tooany van Hallo ondersteund Put.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-406">However, data can be copied _directly_ from any of hello sources tooany of hello supported sinks.</span></span> <span data-ttu-id="4b6b1-407">Zie voor meer informatie Hallo sectie 'ondersteunde gegevensarchieven en indelingen' in hello [verplaatsen van gegevens met behulp van de Kopieeractiviteit](data-factory-data-movement-activities.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-407">For more information, see hello section "Supported data stores and formats" in hello [Move data by using Copy Activity](data-factory-data-movement-activities.md) article.</span></span>  

### <a name="example-copy-data-from-azure-blob-storage-tooazure-data-lake-store"></a><span data-ttu-id="4b6b1-408">Voorbeeld: Gegevens kopiëren van Azure Blob Storage tooAzure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="4b6b1-408">Example: Copy data from Azure Blob Storage tooAzure Data Lake Store</span></span>
<span data-ttu-id="4b6b1-409">Hallo voorbeeldcode in dit gedeelte ziet:</span><span class="sxs-lookup"><span data-stu-id="4b6b1-409">hello example code in this section shows:</span></span>

* <span data-ttu-id="4b6b1-410">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4b6b1-410">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="4b6b1-411">Een gekoppelde service van het type [AzureDataLakeStore](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4b6b1-411">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="4b6b1-412">Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4b6b1-412">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="4b6b1-413">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureDataLakeStore](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4b6b1-413">An output [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="4b6b1-414">Een [pijplijn](data-factory-create-pipelines.md) met een kopieeractiviteit die gebruikmaakt van [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) en [AzureDataLakeStoreSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="4b6b1-414">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureDataLakeStoreSink](#copy-activity-properties).</span></span>

<span data-ttu-id="4b6b1-415">Hallo voorbeelden laten zien hoe timeseries gegevens uit Azure Blob Storage is gekopieerd tooData Lake Store om het uur.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-415">hello examples show how time-series data from Azure Blob Storage is copied tooData Lake Store every hour.</span></span> 

<span data-ttu-id="4b6b1-416">**Een gekoppelde Azure Storage-service**</span><span class="sxs-lookup"><span data-stu-id="4b6b1-416">**Azure Storage linked service**</span></span>

```JSON
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

<span data-ttu-id="4b6b1-417">**Gekoppelde service van Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="4b6b1-417">**Azure Data Lake Store linked service**</span></span>

```JSON
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<subscription of ADLS>",
            "resourceGroupName": "<resource group of ADLS>"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="4b6b1-418">Zie voor configuratiedetails Hallo [gekoppelde service-eigenschappen](#linked-service-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-418">For configuration details, see hello [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="4b6b1-419">**De Azure Blob-invoergegevensset**</span><span class="sxs-lookup"><span data-stu-id="4b6b1-419">**Azure blob input dataset**</span></span>

<span data-ttu-id="4b6b1-420">In de Hallo voorbeeld te volgen, gegevens wordt opgehaald uit een nieuwe blob elk uur (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="4b6b1-420">In hello following example, data is picked up from a new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="4b6b1-421">Hallo map pad en de naam voor de blob Hallo worden dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-421">hello folder path and file name for hello blob are dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="4b6b1-422">Hallo mappad gebruikt Hallo jaar, maand en daggedeelte van de begintijd Hallo.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-422">hello folder path uses hello year, month, and day portion of hello start time.</span></span> <span data-ttu-id="4b6b1-423">Hallo-bestandsnaam Hallo uur gedeelte Hallo begintijd gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-423">hello file name uses hello hour portion of hello start time.</span></span> <span data-ttu-id="4b6b1-424">Hallo `"external": true` instelling informeert Hallo Data Factory-service die tabel Hallo externe toohello data factory is en niet wordt geproduceerd door een activiteit in de gegevensfactory Hallo.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-424">hello `"external": true` setting informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```JSON
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

<span data-ttu-id="4b6b1-425">**Azure Data Lake Store uitvoergegevensset**</span><span class="sxs-lookup"><span data-stu-id="4b6b1-425">**Azure Data Lake Store output dataset**</span></span>

<span data-ttu-id="4b6b1-426">Hallo voorbeeld kopieën data tooData Lake Store te volgen.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-426">hello following example copies data tooData Lake Store.</span></span> <span data-ttu-id="4b6b1-427">Nieuwe gegevens worden gekopieerd tooData Lake Store om het uur.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-427">New data is copied tooData Lake Store every hour.</span></span>

```JSON
{
    "name": "AzureDataLakeStoreOutput",
      "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
              "frequency": "Hour",
              "interval": 1
        }
      }
}
```


<span data-ttu-id="4b6b1-428">**Kopieeractiviteit in een pijplijn met een blob-bron- en een Data Lake Store-sink**</span><span class="sxs-lookup"><span data-stu-id="4b6b1-428">**Copy activity in a pipeline with a blob source and a Data Lake Store sink**</span></span>

<span data-ttu-id="4b6b1-429">Hallo voorbeeld te volgen, Hallo pijplijn bevat een kopieeractiviteit die is geconfigureerd toouse Hallo invoer- en uitvoergegevenssets.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-429">In hello following example, hello pipeline contains a copy activity that is configured toouse hello input and output datasets.</span></span> <span data-ttu-id="4b6b1-430">Hallo kopieeractiviteit is geplande toorun om het uur.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-430">hello copy activity is scheduled toorun every hour.</span></span> <span data-ttu-id="4b6b1-431">Hallo in Hallo pijplijn-JSON-definitie, `source` type is ingesteld, te`BlobSource`, en Hallo `sink` type is ingesteld, te`AzureDataLakeStoreSink`.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-431">In hello pipeline JSON definition, hello `source` type is set too`BlobSource`, and hello `sink` type is set too`AzureDataLakeStoreSink`.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":
    {  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline with copy activity",
        "activities":
        [  
              {
                "name": "AzureBlobtoDataLake",
                "description": "Copy Activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureBlobInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureDataLakeStoreOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                      },
                      "sink": {
                        "type": "AzureDataLakeStoreSink"
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

### <a name="example-copy-data-from-azure-data-lake-store-tooan-azure-blob"></a><span data-ttu-id="4b6b1-432">Voorbeeld: Gegevens kopiëren van Azure Data Lake Store tooan Azure-blobopslag</span><span class="sxs-lookup"><span data-stu-id="4b6b1-432">Example: Copy data from Azure Data Lake Store tooan Azure blob</span></span>
<span data-ttu-id="4b6b1-433">Hallo voorbeeldcode in dit gedeelte ziet:</span><span class="sxs-lookup"><span data-stu-id="4b6b1-433">hello example code in this section shows:</span></span>

* <span data-ttu-id="4b6b1-434">Een gekoppelde service van het type [AzureDataLakeStore](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4b6b1-434">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="4b6b1-435">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="4b6b1-435">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="4b6b1-436">Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureDataLakeStore](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4b6b1-436">An input [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="4b6b1-437">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="4b6b1-437">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="4b6b1-438">Een [pijplijn](data-factory-create-pipelines.md) met een kopieeractiviteit die gebruikmaakt van [AzureDataLakeStoreSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="4b6b1-438">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [AzureDataLakeStoreSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="4b6b1-439">Hallo-code opgehaald-timeseries-gegevens uit Data Lake Store tooan Azure blob elk uur.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-439">hello code copies time-series data from Data Lake Store tooan Azure blob every hour.</span></span> 

<span data-ttu-id="4b6b1-440">**Gekoppelde service van Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="4b6b1-440">**Azure Data Lake Store linked service**</span></span>

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeStoreUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>"
        }
    }
}
```

> [!NOTE]
> <span data-ttu-id="4b6b1-441">Zie voor configuratiedetails Hallo [gekoppelde service-eigenschappen](#linked-service-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-441">For configuration details, see hello [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="4b6b1-442">**Een gekoppelde Azure Storage-service**</span><span class="sxs-lookup"><span data-stu-id="4b6b1-442">**Azure Storage linked service**</span></span>

```JSON
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
<span data-ttu-id="4b6b1-443">**Azure Data Lake invoergegevensset**</span><span class="sxs-lookup"><span data-stu-id="4b6b1-443">**Azure Data Lake input dataset**</span></span>

<span data-ttu-id="4b6b1-444">In dit voorbeeld instelling `"external"` te`true` informeert Hallo Data Factory-service die tabel Hallo externe toohello data factory is en niet wordt geproduceerd door een activiteit in de gegevensfactory Hallo.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-444">In this example, setting `"external"` too`true` informs hello Data Factory service that hello table is external toohello data factory and is not produced by an activity in hello data factory.</span></span>

```json
{
    "name": "AzureDataLakeStoreInput",
      "properties":
    {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
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
<span data-ttu-id="4b6b1-445">**De Azure Blob-uitvoergegevensset**</span><span class="sxs-lookup"><span data-stu-id="4b6b1-445">**Azure blob output dataset**</span></span>

<span data-ttu-id="4b6b1-446">In de Hallo voorbeeld te volgen, gegevens worden geschreven tooa nieuwe blob elk uur (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="4b6b1-446">In hello following example, data is written tooa new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="4b6b1-447">pad naar map voor blob Hallo Hallo wordt dynamisch geëvalueerd op basis van de begintijd Hallo van Hallo-segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-447">hello folder path for hello blob is dynamically evaluated based on hello start time of hello slice that is being processed.</span></span> <span data-ttu-id="4b6b1-448">Hallo mappad gebruikt Hallo jaar, maand, dag en uur gedeelte van de begintijd Hallo.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-448">hello folder path uses hello year, month, day, and hours portion of hello start time.</span></span>

```JSON
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

<span data-ttu-id="4b6b1-449">**Een kopieeractiviteit in een pijplijn met een Azure Data Lake Store-bron- en een blob-sink**</span><span class="sxs-lookup"><span data-stu-id="4b6b1-449">**A copy activity in a pipeline with an Azure Data Lake Store source and a blob sink**</span></span>

<span data-ttu-id="4b6b1-450">Hallo voorbeeld te volgen, Hallo pijplijn bevat een kopieeractiviteit die is geconfigureerd toouse Hallo invoer- en uitvoergegevenssets.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-450">In hello following example, hello pipeline contains a copy activity that is configured toouse hello input and output datasets.</span></span> <span data-ttu-id="4b6b1-451">Hallo kopieeractiviteit is geplande toorun om het uur.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-451">hello copy activity is scheduled toorun every hour.</span></span> <span data-ttu-id="4b6b1-452">Hallo in Hallo pijplijn-JSON-definitie, `source` type is ingesteld, te`AzureDataLakeStoreSource`, en Hallo `sink` type is ingesteld, te`BlobSink`.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-452">In hello pipeline JSON definition, hello `source` type is set too`AzureDataLakeStoreSource`, and hello `sink` type is set too`BlobSink`.</span></span>

```json
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
              {
                "name": "AzureDakeLaketoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                  {
                    "name": "AzureDataLakeStoreInput"
                  }
                ],
                "outputs": [
                  {
                    "name": "AzureBlobOutput"
                  }
                ],
                "typeProperties": {
                    "source": {
                        "type": "AzureDataLakeStoreSource",
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

<span data-ttu-id="4b6b1-453">U kunt ook kolommen uit Hallo bron gegevensset toocolumns in Hallo sink gegevensset toewijzen in Hallo kopie activiteitsdefinitie.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-453">In hello copy activity definition, you can also map columns from hello source dataset toocolumns in hello sink dataset.</span></span> <span data-ttu-id="4b6b1-454">Zie voor meer informatie [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="4b6b1-454">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="4b6b1-455">Prestaties en afstemmen</span><span class="sxs-lookup"><span data-stu-id="4b6b1-455">Performance and tuning</span></span>
<span data-ttu-id="4b6b1-456">toolearn over Hallo factoren die van invloed op prestaties van de Kopieeractiviteit en hoe toooptimize, Zie Hallo [Kopieeractiviteit prestaties en prestatieafstemming handleiding](data-factory-copy-activity-performance.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="4b6b1-456">toolearn about hello factors that affect Copy Activity performance and how toooptimize it, see hello [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) article.</span></span>
