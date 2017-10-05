---
title: "Gegevens kopiëren naar en van Azure Data Lake Store | Microsoft Docs"
description: "Informatie over het kopiëren van gegevens naar en van Data Lake Store met behulp van Azure Data Factory"
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
ms.openlocfilehash: 11629fbc83f0554e2097eb4322701654c0bc2028
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="copy-data-to-and-from-data-lake-store-by-using-data-factory"></a><span data-ttu-id="c44d0-103">Gegevens kopiëren naar en van Data Lake Store via Data Factory</span><span class="sxs-lookup"><span data-stu-id="c44d0-103">Copy data to and from Data Lake Store by using Data Factory</span></span>
<span data-ttu-id="c44d0-104">In dit artikel wordt uitgelegd hoe gebruiken Kopieeractiviteit in Azure Data Factory om gegevens te verplaatsen naar en van Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c44d0-104">This article explains how to use Copy Activity in Azure Data Factory to move data to and from Azure Data Lake Store.</span></span> <span data-ttu-id="c44d0-105">Dit is gebaseerd op de [activiteiten voor gegevensverplaatsing](data-factory-data-movement-activities.md) artikel, een overzicht van de verplaatsing van gegevens met de Kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="c44d0-105">It builds on the [Data movement activities](data-factory-data-movement-activities.md) article, an overview of data movement with Copy Activity.</span></span>

## <a name="supported-scenarios"></a><span data-ttu-id="c44d0-106">Ondersteunde scenario 's</span><span class="sxs-lookup"><span data-stu-id="c44d0-106">Supported scenarios</span></span>
<span data-ttu-id="c44d0-107">U kunt gegevens kopiëren **van Azure Data Lake Store** opslaat in de volgende gegevens:</span><span class="sxs-lookup"><span data-stu-id="c44d0-107">You can copy data **from Azure Data Lake Store** to the following data stores:</span></span>

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

<span data-ttu-id="c44d0-108">U kunt gegevens kopiëren van de volgende gegevensarchieven **met Azure Data Lake Store**:</span><span class="sxs-lookup"><span data-stu-id="c44d0-108">You can copy data from the following data stores **to Azure Data Lake Store**:</span></span>

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

> [!NOTE]
> <span data-ttu-id="c44d0-109">Een Data Lake Store-account maken voordat u een pijplijn maakt met de Kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="c44d0-109">Create a Data Lake Store account before creating a pipeline with Copy Activity.</span></span> <span data-ttu-id="c44d0-110">Zie voor meer informatie [aan de slag met Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c44d0-110">For more information, see [Get started with Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="c44d0-111">Ondersteunde verificatietypen</span><span class="sxs-lookup"><span data-stu-id="c44d0-111">Supported authentication types</span></span>
<span data-ttu-id="c44d0-112">De Data Lake Store-connector ondersteunt de volgende verificatietypen:</span><span class="sxs-lookup"><span data-stu-id="c44d0-112">The Data Lake Store connector supports these authentication types:</span></span>
* <span data-ttu-id="c44d0-113">Verificatie van service-principal</span><span class="sxs-lookup"><span data-stu-id="c44d0-113">Service principal authentication</span></span>
* <span data-ttu-id="c44d0-114">Verificatie van gebruikersreferenties (OAuth)</span><span class="sxs-lookup"><span data-stu-id="c44d0-114">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="c44d0-115">Het is raadzaam dat u service-principal verificatie, met name voor een geplande gegevens opnieuw te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="c44d0-115">We recommend that you use service principal authentication, especially for a scheduled data copy.</span></span> <span data-ttu-id="c44d0-116">Verlopen van het token kan gebeuren met verificatie van gebruikersreferenties.</span><span class="sxs-lookup"><span data-stu-id="c44d0-116">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="c44d0-117">Zie voor configuratiedetails de [gekoppelde service-eigenschappen](#linked-service-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="c44d0-117">For configuration details, see the [Linked service properties](#linked-service-properties) section.</span></span>

## <a name="get-started"></a><span data-ttu-id="c44d0-118">Aan de slag</span><span class="sxs-lookup"><span data-stu-id="c44d0-118">Get started</span></span>
<span data-ttu-id="c44d0-119">U kunt een pijplijn maken met een kopieeractiviteit waarmee gegevens worden verplaatst van een Azure Data Lake Store met verschillende hulpprogramma's voor API's.</span><span class="sxs-lookup"><span data-stu-id="c44d0-119">You can create a pipeline with a copy activity that moves data to/from an Azure Data Lake Store by using different tools/APIs.</span></span>

<span data-ttu-id="c44d0-120">De eenvoudigste manier om u te maken van een pijplijn om gegevens te kopiëren is met de **Wizard kopiëren**.</span><span class="sxs-lookup"><span data-stu-id="c44d0-120">The easiest way to create a pipeline to copy data is to use the **Copy Wizard**.</span></span> <span data-ttu-id="c44d0-121">Zie voor een zelfstudie over het maken van een pijplijn met behulp van de Wizard kopiëren [zelfstudie: een pijplijn maken met de Wizard kopiëren](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="c44d0-121">For a tutorial on creating a pipeline by using the Copy Wizard, see [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md).</span></span>

<span data-ttu-id="c44d0-122">U kunt ook de volgende hulpprogramma's gebruiken voor het maken van een pijplijn: **Azure-portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager-sjabloon**, **.NET API**, en **REST-API**.</span><span class="sxs-lookup"><span data-stu-id="c44d0-122">You can also use the following tools to create a pipeline: **Azure portal**, **Visual Studio**, **Azure PowerShell**, **Azure Resource Manager template**, **.NET API**, and **REST API**.</span></span> <span data-ttu-id="c44d0-123">Zie [kopie activiteit zelfstudie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) voor stapsgewijze instructies voor een pijplijn maken met een kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="c44d0-123">See [Copy activity tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for step-by-step instructions to create a pipeline with a copy activity.</span></span>

<span data-ttu-id="c44d0-124">Of u de hulpprogramma's of API's gebruiken, moet u de volgende stappen voor het maken van een pijplijn die de gegevens vanuit een brongegevensarchief naar een gegevensarchief sink verplaatst uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="c44d0-124">Whether you use the tools or APIs, you perform the following steps to create a pipeline that moves data from a source data store to a sink data store:</span></span>

1. <span data-ttu-id="c44d0-125">Maak een **gegevensfactory**.</span><span class="sxs-lookup"><span data-stu-id="c44d0-125">Create a **data factory**.</span></span> <span data-ttu-id="c44d0-126">Een gegevensfactory kan één of meer pijplijnen bevatten.</span><span class="sxs-lookup"><span data-stu-id="c44d0-126">A data factory may contain one or more pipelines.</span></span> 
2. <span data-ttu-id="c44d0-127">Maak **gekoppelde services** slaat om invoer- en gegevens te koppelen aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="c44d0-127">Create **linked services** to link input and output data stores to your data factory.</span></span> <span data-ttu-id="c44d0-128">Bijvoorbeeld, als u gegevens uit een Azure blob-opslag met een Azure Data Lake Store kopieert, maakt u twee gekoppelde services als u wilt uw Azure storage-account en de Azure Data Lake store koppelen aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="c44d0-128">For example, if you are copying data from an Azure blob storage to an Azure Data Lake Store, you create two linked services to link your Azure storage account and Azure Data Lake store to your data factory.</span></span> <span data-ttu-id="c44d0-129">Zie voor de gekoppelde service-eigenschappen die specifiek voor Azure Data Lake Store zijn, [gekoppelde service-eigenschappen](#linked-service-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="c44d0-129">For linked service properties that are specific to Azure Data Lake Store, see [linked service properties](#linked-service-properties) section.</span></span> 
2. <span data-ttu-id="c44d0-130">Maak **gegevenssets** vertegenwoordigt de invoer- en -gegevens voor de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="c44d0-130">Create **datasets** to represent input and output data for the copy operation.</span></span> <span data-ttu-id="c44d0-131">In het voorbeeld in de laatste stap wordt vermeld, maakt u een gegevensset om op te geven van de blob-container en de map waarin de invoergegevens.</span><span class="sxs-lookup"><span data-stu-id="c44d0-131">In the example mentioned in the last step, you create a dataset to specify the blob container and folder that contains the input data.</span></span> <span data-ttu-id="c44d0-132">En maken van een andere gegevensset opgeven van de map en het bestandspad in de Data Lake store de gegevens gekopieerd van de blob-opslag bevat.</span><span class="sxs-lookup"><span data-stu-id="c44d0-132">And, you create another dataset to specify the folder and file path in the Data Lake store that holds the data copied from the blob storage.</span></span> <span data-ttu-id="c44d0-133">Zie voor eigenschappen van gegevensset die specifiek voor Azure Data Lake Store zijn, [eigenschappen van gegevensset](#dataset-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="c44d0-133">For dataset properties that are specific to Azure Data Lake Store, see [dataset properties](#dataset-properties) section.</span></span>
3. <span data-ttu-id="c44d0-134">Maak een **pijplijn** met een kopieeractiviteit waarmee een gegevensset als invoer en een gegevensset als uitvoer.</span><span class="sxs-lookup"><span data-stu-id="c44d0-134">Create a **pipeline** with a copy activity that takes a dataset as an input and a dataset as an output.</span></span> <span data-ttu-id="c44d0-135">In het voorbeeld eerder vermeld, gebruikt u BlobSource als een bron- en AzureDataLakeStoreSink als een sink voor de kopieeractiviteit.</span><span class="sxs-lookup"><span data-stu-id="c44d0-135">In the example mentioned earlier, you use BlobSource as a source and AzureDataLakeStoreSink as a sink for the copy activity.</span></span> <span data-ttu-id="c44d0-136">Op dezelfde manier als u van Azure Data Lake Store naar Azure Blob Storage kopiëren wilt, gebruikt u AzureDataLakeStoreSource en BlobSink in de kopieerbewerking.</span><span class="sxs-lookup"><span data-stu-id="c44d0-136">Similarly, if you are copying from Azure Data Lake Store to Azure Blob Storage, you use AzureDataLakeStoreSource  and BlobSink in the copy activity.</span></span> <span data-ttu-id="c44d0-137">Zie voor activiteitseigenschappen kopiëren die specifiek voor Azure Data Lake Store zijn, [activiteitseigenschappen kopiëren](#copy-activity-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="c44d0-137">For copy activity properties that are specific to Azure Data Lake Store, see [copy activity properties](#copy-activity-properties) section.</span></span> <span data-ttu-id="c44d0-138">Klik op de koppeling in de vorige sectie voor de gegevensopslag voor meer informatie over het gebruik van een gegevensarchief als een bron of een sink.</span><span class="sxs-lookup"><span data-stu-id="c44d0-138">For details on how to use a data store as a source or a sink, click the link in the previous section for your data store.</span></span>  

<span data-ttu-id="c44d0-139">Wanneer u de wizard gebruikt, worden de JSON-definities voor deze Data Factory-entiteiten (gekoppelde services, gegevenssets en pijplijn) automatisch voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c44d0-139">When you use the wizard, JSON definitions for these Data Factory entities (linked services, datasets, and the pipeline) are automatically created for you.</span></span> <span data-ttu-id="c44d0-140">Wanneer u extra/API's (met uitzondering van de .NET API) gebruikt, kunt u deze Data Factory-entiteiten definiëren met behulp van de JSON-indeling.</span><span class="sxs-lookup"><span data-stu-id="c44d0-140">When you use tools/APIs (except .NET API), you define these Data Factory entities by using the JSON format.</span></span>  <span data-ttu-id="c44d0-141">Zie voor voorbeelden met JSON-definities voor Data Factory-entiteiten die worden gebruikt om gegevens te kopiëren naar/van een Azure Data Lake Store, [JSON voorbeelden](#json-examples-for-copying-data-to-and-from-data-lake-store) sectie van dit artikel.</span><span class="sxs-lookup"><span data-stu-id="c44d0-141">For samples with JSON definitions for Data Factory entities that are used to copy data to/from an Azure Data Lake Store, see [JSON examples](#json-examples-for-copying-data-to-and-from-data-lake-store) section of this article.</span></span>

<span data-ttu-id="c44d0-142">De volgende secties bevatten informatie over de JSON-eigenschappen die worden gebruikt voor het definiëren van Data Factory-entiteiten specifieke naar Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c44d0-142">The following sections provide details about JSON properties that are used to define Data Factory entities specific to Data Lake Store.</span></span>

## <a name="linked-service-properties"></a><span data-ttu-id="c44d0-143">Eigenschappen van de gekoppelde service</span><span class="sxs-lookup"><span data-stu-id="c44d0-143">Linked service properties</span></span>
<span data-ttu-id="c44d0-144">Een gekoppelde service gegevensopslag is gekoppeld aan een gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="c44d0-144">A linked service links a data store to a data factory.</span></span> <span data-ttu-id="c44d0-145">Maken van een gekoppelde service van het type **AzureDataLakeStore** uw Data Lake Store om gegevens te koppelen aan uw gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="c44d0-145">You create a linked service of type **AzureDataLakeStore** to link your Data Lake Store data to your data factory.</span></span> <span data-ttu-id="c44d0-146">De volgende tabel beschrijft de JSON-elementen die specifiek zijn voor Data Lake Store gekoppelde services.</span><span class="sxs-lookup"><span data-stu-id="c44d0-146">The following table describes JSON elements specific to Data Lake Store linked services.</span></span> <span data-ttu-id="c44d0-147">U kunt kiezen tussen service-principal en verificatie van gebruikersreferenties.</span><span class="sxs-lookup"><span data-stu-id="c44d0-147">You can choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="c44d0-148">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="c44d0-148">Property</span></span> | <span data-ttu-id="c44d0-149">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c44d0-149">Description</span></span> | <span data-ttu-id="c44d0-150">Vereist</span><span class="sxs-lookup"><span data-stu-id="c44d0-150">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="c44d0-151">**type**</span><span class="sxs-lookup"><span data-stu-id="c44d0-151">**type**</span></span> | <span data-ttu-id="c44d0-152">De eigenschap type moet worden ingesteld op **AzureDataLakeStore**.</span><span class="sxs-lookup"><span data-stu-id="c44d0-152">The type property must be set to **AzureDataLakeStore**.</span></span> | <span data-ttu-id="c44d0-153">Ja</span><span class="sxs-lookup"><span data-stu-id="c44d0-153">Yes</span></span> |
| <span data-ttu-id="c44d0-154">**dataLakeStoreUri**</span><span class="sxs-lookup"><span data-stu-id="c44d0-154">**dataLakeStoreUri**</span></span> | <span data-ttu-id="c44d0-155">Informatie over het Azure Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="c44d0-155">Information about the Azure Data Lake Store account.</span></span> <span data-ttu-id="c44d0-156">Deze informatie heeft een van de volgende indelingen: `https://[accountname].azuredatalakestore.net/webhdfs/v1` of `adl://[accountname].azuredatalakestore.net/`.</span><span class="sxs-lookup"><span data-stu-id="c44d0-156">This information takes one of the following formats: `https://[accountname].azuredatalakestore.net/webhdfs/v1` or `adl://[accountname].azuredatalakestore.net/`.</span></span> | <span data-ttu-id="c44d0-157">Ja</span><span class="sxs-lookup"><span data-stu-id="c44d0-157">Yes</span></span> |
| <span data-ttu-id="c44d0-158">**abonnements-id**</span><span class="sxs-lookup"><span data-stu-id="c44d0-158">**subscriptionId**</span></span> | <span data-ttu-id="c44d0-159">Azure-abonnement-ID waartoe het Data Lake Store-account behoort.</span><span class="sxs-lookup"><span data-stu-id="c44d0-159">Azure subscription ID to which the Data Lake Store account belongs.</span></span> | <span data-ttu-id="c44d0-160">Vereist voor sink</span><span class="sxs-lookup"><span data-stu-id="c44d0-160">Required for sink</span></span> |
| <span data-ttu-id="c44d0-161">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="c44d0-161">**resourceGroupName**</span></span> | <span data-ttu-id="c44d0-162">Naam Azure resourcegroep waartoe het Data Lake Store-account behoort.</span><span class="sxs-lookup"><span data-stu-id="c44d0-162">Azure resource group name to which the Data Lake Store account belongs.</span></span> | <span data-ttu-id="c44d0-163">Vereist voor sink</span><span class="sxs-lookup"><span data-stu-id="c44d0-163">Required for sink</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="c44d0-164">Verificatie van de service principal (aanbevolen)</span><span class="sxs-lookup"><span data-stu-id="c44d0-164">Service principal authentication (recommended)</span></span>
<span data-ttu-id="c44d0-165">Registreren van een Toepassingsentiteit in Azure Active Directory (Azure AD) voor het gebruik van verificatie van de service-principal en wordt de toegang verlenen tot Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c44d0-165">To use service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it the access to Data Lake Store.</span></span> <span data-ttu-id="c44d0-166">Zie voor gedetailleerde stappen [authentication Service-naar-serviceconnector](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="c44d0-166">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="c44d0-167">Noteer de volgende waarden die u gebruikt voor het definiëren van de gekoppelde service:</span><span class="sxs-lookup"><span data-stu-id="c44d0-167">Make note of the following values, which you use to define the linked service:</span></span>
* <span data-ttu-id="c44d0-168">Toepassings-id</span><span class="sxs-lookup"><span data-stu-id="c44d0-168">Application ID</span></span>
* <span data-ttu-id="c44d0-169">Sleutel van toepassing</span><span class="sxs-lookup"><span data-stu-id="c44d0-169">Application key</span></span> 
* <span data-ttu-id="c44d0-170">Tenant-id</span><span class="sxs-lookup"><span data-stu-id="c44d0-170">Tenant ID</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c44d0-171">Als u de Wizard kopiëren gebruikt voor het schrijven van gegevenspijplijnen, zorgt u ervoor dat u de service-principal verlenen ten minste een **lezer** rol in toegangsbeheer (identiteits- en toegangsbeheer management) voor het Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="c44d0-171">If you are using the Copy Wizard to author data pipelines, make sure that you grant the service principal at least a **Reader** role in access control (identity and access management) for the Data Lake Store account.</span></span> <span data-ttu-id="c44d0-172">Verleen de service-principal ook ten minste **lezen + Execute** machtiging voor de hoofdmap van uw Data Lake Store ('/') en de onderliggende items.</span><span class="sxs-lookup"><span data-stu-id="c44d0-172">Also, grant the service principal at least **Read + Execute** permission to your Data Lake Store root ("/") and its children.</span></span> <span data-ttu-id="c44d0-173">Anders mogelijk ziet u het bericht "de opgegeven referenties zijn ongeldig."</span><span class="sxs-lookup"><span data-stu-id="c44d0-173">Otherwise you might see the message "The credentials provided are invalid."</span></span><br/><br/>
<span data-ttu-id="c44d0-174">Nadat u maken of bijwerken van een service-principal in Azure AD, kan het enkele minuten om de wijzigingen van kracht te laten duren.</span><span class="sxs-lookup"><span data-stu-id="c44d0-174">After you create or update a service principal in Azure AD, it can take a few minutes for the changes to take effect.</span></span> <span data-ttu-id="c44d0-175">Controleer de service-principal en Data Lake Store-besturingselement toegangsbeheerlijst (ACL) configuraties.</span><span class="sxs-lookup"><span data-stu-id="c44d0-175">Check the service principal and Data Lake Store access control list (ACL) configurations.</span></span> <span data-ttu-id="c44d0-176">Als u nog steeds ziet u het bericht 'de opgegeven referenties zijn ongeldig.' Wacht even en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="c44d0-176">If you still see the message "The credentials provided are invalid," wait a while and try again.</span></span>

<span data-ttu-id="c44d0-177">Verificatie van de service-principal gebruiken door te geven van de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="c44d0-177">Use service principal authentication by specifying the following properties:</span></span>

| <span data-ttu-id="c44d0-178">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="c44d0-178">Property</span></span> | <span data-ttu-id="c44d0-179">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c44d0-179">Description</span></span> | <span data-ttu-id="c44d0-180">Vereist</span><span class="sxs-lookup"><span data-stu-id="c44d0-180">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="c44d0-181">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="c44d0-181">**servicePrincipalId**</span></span> | <span data-ttu-id="c44d0-182">Geef de toepassing client-ID.</span><span class="sxs-lookup"><span data-stu-id="c44d0-182">Specify the application's client ID.</span></span> | <span data-ttu-id="c44d0-183">Ja</span><span class="sxs-lookup"><span data-stu-id="c44d0-183">Yes</span></span> |
| <span data-ttu-id="c44d0-184">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="c44d0-184">**servicePrincipalKey**</span></span> | <span data-ttu-id="c44d0-185">De sleutel van de toepassing opgeven.</span><span class="sxs-lookup"><span data-stu-id="c44d0-185">Specify the application's key.</span></span> | <span data-ttu-id="c44d0-186">Ja</span><span class="sxs-lookup"><span data-stu-id="c44d0-186">Yes</span></span> |
| <span data-ttu-id="c44d0-187">**tenant**</span><span class="sxs-lookup"><span data-stu-id="c44d0-187">**tenant**</span></span> | <span data-ttu-id="c44d0-188">De tenant-gegevens (domain name of tenant-ID) opgeven onder uw toepassing zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="c44d0-188">Specify the tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="c44d0-189">U kunt deze ophalen door de muis in de rechterbovenhoek van de Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c44d0-189">You can retrieve it by hovering the mouse in the upper-right corner of the Azure portal.</span></span> | <span data-ttu-id="c44d0-190">Ja</span><span class="sxs-lookup"><span data-stu-id="c44d0-190">Yes</span></span> |

<span data-ttu-id="c44d0-191">**Voorbeeld: Service-principal-verificatie**</span><span class="sxs-lookup"><span data-stu-id="c44d0-191">**Example: Service principal authentication**</span></span>
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

### <a name="user-credential-authentication"></a><span data-ttu-id="c44d0-192">Verificatie van gebruikersreferenties</span><span class="sxs-lookup"><span data-stu-id="c44d0-192">User credential authentication</span></span>
<span data-ttu-id="c44d0-193">U kunt ook kunt u verificatie van gebruikersreferenties voor het kopiëren van of naar Data Lake Store door te geven van de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="c44d0-193">Alternatively, you can use user credential authentication to copy from or to Data Lake Store by specifying the following properties:</span></span>

| <span data-ttu-id="c44d0-194">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="c44d0-194">Property</span></span> | <span data-ttu-id="c44d0-195">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c44d0-195">Description</span></span> | <span data-ttu-id="c44d0-196">Vereist</span><span class="sxs-lookup"><span data-stu-id="c44d0-196">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="c44d0-197">**autorisatie**</span><span class="sxs-lookup"><span data-stu-id="c44d0-197">**authorization**</span></span> | <span data-ttu-id="c44d0-198">Klik op de **autoriseren** in de Data Factory-Editor en voer uw referenties op waarmee de automatisch gegenereerde autorisatie-URL worden toegewezen aan deze eigenschap.</span><span class="sxs-lookup"><span data-stu-id="c44d0-198">Click the **Authorize** button in the Data Factory Editor and enter your credential that assigns the autogenerated authorization URL to this property.</span></span> | <span data-ttu-id="c44d0-199">Ja</span><span class="sxs-lookup"><span data-stu-id="c44d0-199">Yes</span></span> |
| <span data-ttu-id="c44d0-200">**sessie-id**</span><span class="sxs-lookup"><span data-stu-id="c44d0-200">**sessionId**</span></span> | <span data-ttu-id="c44d0-201">OAuth-sessie-ID van de OAuth-autorisatie-sessie.</span><span class="sxs-lookup"><span data-stu-id="c44d0-201">OAuth session ID from the OAuth authorization session.</span></span> <span data-ttu-id="c44d0-202">Elke sessie-ID is uniek en kan slechts één keer worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c44d0-202">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="c44d0-203">Deze instelling wordt automatisch gegenereerd wanneer u de Data Factory-Editor.</span><span class="sxs-lookup"><span data-stu-id="c44d0-203">This setting is automatically generated when you use the Data Factory Editor.</span></span> | <span data-ttu-id="c44d0-204">Ja</span><span class="sxs-lookup"><span data-stu-id="c44d0-204">Yes</span></span> |

<span data-ttu-id="c44d0-205">**Voorbeeld: Verificatie van gebruikersreferenties**</span><span class="sxs-lookup"><span data-stu-id="c44d0-205">**Example: User credential authentication**</span></span>
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

#### <a name="token-expiration"></a><span data-ttu-id="c44d0-206">Verlopen van het token</span><span class="sxs-lookup"><span data-stu-id="c44d0-206">Token expiration</span></span>
<span data-ttu-id="c44d0-207">De autorisatiecode die u met behulp van genereren de **autoriseren** knop verloopt na een bepaalde hoeveelheid tijd.</span><span class="sxs-lookup"><span data-stu-id="c44d0-207">The authorization code that you generate by using the **Authorize** button expires after a certain amount of time.</span></span> <span data-ttu-id="c44d0-208">Het volgende bericht betekent dat de verificatietoken is verlopen:</span><span class="sxs-lookup"><span data-stu-id="c44d0-208">The following message means that the authentication token has expired:</span></span>

<span data-ttu-id="c44d0-209">Referentie-bewerkingsfout: invalid_grant - AADSTS70002: fout bij het valideren van referenties.</span><span class="sxs-lookup"><span data-stu-id="c44d0-209">Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="c44d0-210">AADSTS70008: De toegewezen toegangsmachtiging is verlopen of ingetrokken.</span><span class="sxs-lookup"><span data-stu-id="c44d0-210">AADSTS70008: The provided access grant is expired or revoked.</span></span> <span data-ttu-id="c44d0-211">Traceer-ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 correlatie-ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 tijdstempel: 2015-12-15 21-09-31Z.</span><span class="sxs-lookup"><span data-stu-id="c44d0-211">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21-09-31Z.</span></span>

<span data-ttu-id="c44d0-212">De volgende tabel ziet u de vervaldatum tijden van verschillende typen gebruikersaccounts:</span><span class="sxs-lookup"><span data-stu-id="c44d0-212">The following table shows the expiration times of different types of user accounts:</span></span>


| <span data-ttu-id="c44d0-213">Gebruikerstype</span><span class="sxs-lookup"><span data-stu-id="c44d0-213">User type</span></span> | <span data-ttu-id="c44d0-214">Verloopt na</span><span class="sxs-lookup"><span data-stu-id="c44d0-214">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="c44d0-215">Gebruikersaccounts *niet* beheerd door Azure Active Directory (bijvoorbeeld @hotmail.com of @live.com)</span><span class="sxs-lookup"><span data-stu-id="c44d0-215">User accounts *not* managed by Azure Active Directory (for example, @hotmail.com or @live.com)</span></span> |<span data-ttu-id="c44d0-216">12 uur</span><span class="sxs-lookup"><span data-stu-id="c44d0-216">12 hours</span></span> |
| <span data-ttu-id="c44d0-217">Gebruikersaccounts worden beheerd door Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c44d0-217">Users accounts managed by Azure Active Directory</span></span> |<span data-ttu-id="c44d0-218">het is 14 dagen na het laatste segment uitvoeren</span><span class="sxs-lookup"><span data-stu-id="c44d0-218">14 days after the last slice run</span></span> <br/><br/><span data-ttu-id="c44d0-219">Als een segment op basis van een gekoppelde op basis van het OAuth-service wordt uitgevoerd in de 14 dagen ten minste eenmaal na 90 dagen</span><span class="sxs-lookup"><span data-stu-id="c44d0-219">90 days, if a slice based on an OAuth-based linked service runs at least once every 14 days</span></span> |

<span data-ttu-id="c44d0-220">Als u uw wachtwoord voordat de verlooptijd van de token wijzigen, is het token verloopt onmiddellijk.</span><span class="sxs-lookup"><span data-stu-id="c44d0-220">If you change your password before the token expiration time, the token expires immediately.</span></span> <span data-ttu-id="c44d0-221">U ziet het bericht dat eerder is vermeld in deze sectie.</span><span class="sxs-lookup"><span data-stu-id="c44d0-221">You will see the message mentioned earlier in this section.</span></span>

<span data-ttu-id="c44d0-222">U kunt het account opnieuw autoriseren met behulp van de **autoriseren** knop wanneer het token is verlopen opnieuw te implementeren, de gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="c44d0-222">You can reauthorize the account by using the **Authorize** button when the token expires to redeploy the linked service.</span></span> <span data-ttu-id="c44d0-223">U kunt ook genereren waarden voor de **sessionId** en **autorisatie** eigenschappen programmatisch met behulp van de volgende code:</span><span class="sxs-lookup"><span data-stu-id="c44d0-223">You can also generate values for the **sessionId** and **authorization** properties programmatically by using the following code:</span></span>


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
<span data-ttu-id="c44d0-224">Zie voor meer informatie over de Data Factory-klassen gebruikt in de code de [AzureDataLakeStoreLinkedService klasse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService klasse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), en [ Klasse AuthorizationSessionGetResponse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="c44d0-224">For details about the Data Factory classes used in the code, see the [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics.</span></span> <span data-ttu-id="c44d0-225">Voeg een verwijzing naar versie `2.9.10826.1824` van `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` voor de `WindowsFormsWebAuthenticationDialog` klasse die in de code wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="c44d0-225">Add a reference to version `2.9.10826.1824` of `Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll` for the `WindowsFormsWebAuthenticationDialog` class used in the code.</span></span>

## <a name="dataset-properties"></a><span data-ttu-id="c44d0-226">Eigenschappen van gegevensset</span><span class="sxs-lookup"><span data-stu-id="c44d0-226">Dataset properties</span></span>
<span data-ttu-id="c44d0-227">Als een dataset staat voor invoergegevens in een Data Lake Store opgeven, die u stelt de **type** eigenschap van de gegevensset **AzureDataLakeStore**.</span><span class="sxs-lookup"><span data-stu-id="c44d0-227">To specify a dataset to represent input data in a Data Lake Store, you set the **type** property of the dataset to **AzureDataLakeStore**.</span></span> <span data-ttu-id="c44d0-228">Stel de **linkedServiceName** eigenschap van de gegevensset op de naam van de Data Lake Store gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="c44d0-228">Set the **linkedServiceName** property of the dataset to the name of the Data Lake Store linked service.</span></span> <span data-ttu-id="c44d0-229">Zie voor een volledige lijst van JSON-secties en de eigenschappen die beschikbaar zijn voor het definiëren van gegevenssets de [gegevenssets maken](data-factory-create-datasets.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="c44d0-229">For a full list of JSON sections and properties available for defining datasets, see the [Creating datasets](data-factory-create-datasets.md) article.</span></span> <span data-ttu-id="c44d0-230">Secties van een gegevensset in JSON, zoals **structuur**, **beschikbaarheid**, en **beleid**, zijn identiek voor alle typen van de gegevensset (Azure SQL-database, blob van Azure en Azure-tabel voor voorbeeld).</span><span class="sxs-lookup"><span data-stu-id="c44d0-230">Sections of a dataset in JSON, such as **structure**, **availability**, and **policy**, are similar for all dataset types (Azure SQL database, Azure blob, and Azure table, for example).</span></span> <span data-ttu-id="c44d0-231">De **typeProperties** sectie verschilt voor elk type gegevensset en bevat informatie zoals de locatie en indeling van de gegevens in het gegevensarchief.</span><span class="sxs-lookup"><span data-stu-id="c44d0-231">The **typeProperties** section is different for each type of dataset and provides information such as location and format of the data in the data store.</span></span> 

<span data-ttu-id="c44d0-232">De **typeProperties** sectie voor een gegevensset van het type **AzureDataLakeStore** bevat de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="c44d0-232">The **typeProperties** section for a dataset of type **AzureDataLakeStore** contains the following properties:</span></span>

| <span data-ttu-id="c44d0-233">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="c44d0-233">Property</span></span> | <span data-ttu-id="c44d0-234">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c44d0-234">Description</span></span> | <span data-ttu-id="c44d0-235">Vereist</span><span class="sxs-lookup"><span data-stu-id="c44d0-235">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="c44d0-236">**folderPath**</span><span class="sxs-lookup"><span data-stu-id="c44d0-236">**folderPath**</span></span> |<span data-ttu-id="c44d0-237">Pad naar de container en map in Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c44d0-237">Path to the container and folder in Data Lake Store.</span></span> |<span data-ttu-id="c44d0-238">Ja</span><span class="sxs-lookup"><span data-stu-id="c44d0-238">Yes</span></span> |
| <span data-ttu-id="c44d0-239">**Bestandsnaam**</span><span class="sxs-lookup"><span data-stu-id="c44d0-239">**fileName**</span></span> |<span data-ttu-id="c44d0-240">Naam van het bestand in Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c44d0-240">Name of the file in Azure Data Lake Store.</span></span> <span data-ttu-id="c44d0-241">De **fileName** eigenschap is optioneel en is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="c44d0-241">The **fileName** property is optional and case-sensitive.</span></span> <br/><br/><span data-ttu-id="c44d0-242">Als u opgeeft **fileName**, de activiteit (inclusief kopiëren) werkt op het specifieke bestand.</span><span class="sxs-lookup"><span data-stu-id="c44d0-242">If you specify **fileName**, the activity (including Copy) works on the specific file.</span></span><br/><br/><span data-ttu-id="c44d0-243">Wanneer **fileName** niet is opgegeven, kopie bevat alle bestanden in **folderPath** in de invoer gegevensset.</span><span class="sxs-lookup"><span data-stu-id="c44d0-243">When **fileName** is not specified, Copy includes all files in **folderPath** in the input dataset.</span></span><br/><br/><span data-ttu-id="c44d0-244">Wanneer **fileName** is niet opgegeven voor een uitvoergegevensset en **preserveHierarchy** niet is opgegeven in activiteit sink, de naam van het gegenereerde bestand is in de indeling van gegevens. _GUID_.txt'.</span><span class="sxs-lookup"><span data-stu-id="c44d0-244">When **fileName** is not specified for an output dataset and **preserveHierarchy** is not specified in activity sink, the name of the generated file is in the format Data._Guid_.txt\`.</span></span> <span data-ttu-id="c44d0-245">Voorbeeld: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.</span><span class="sxs-lookup"><span data-stu-id="c44d0-245">For example: Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt.</span></span> |<span data-ttu-id="c44d0-246">Nee</span><span class="sxs-lookup"><span data-stu-id="c44d0-246">No</span></span> |
| <span data-ttu-id="c44d0-247">**partitionedBy**</span><span class="sxs-lookup"><span data-stu-id="c44d0-247">**partitionedBy**</span></span> |<span data-ttu-id="c44d0-248">De **partitionedBy** eigenschap is optioneel.</span><span class="sxs-lookup"><span data-stu-id="c44d0-248">The **partitionedBy** property is optional.</span></span> <span data-ttu-id="c44d0-249">U kunt deze gebruiken om op te geven van een dynamische pad en bestandsnaam op voor timeseries gegevens.</span><span class="sxs-lookup"><span data-stu-id="c44d0-249">You can use it to specify a dynamic path and file name for time-series data.</span></span> <span data-ttu-id="c44d0-250">Bijvoorbeeld: **folderPath** kunnen als parameters worden gebruikt voor elk uur van gegevens.</span><span class="sxs-lookup"><span data-stu-id="c44d0-250">For example, **folderPath** can be parameterized for every hour of data.</span></span> <span data-ttu-id="c44d0-251">Zie voor meer informatie en voorbeelden [de eigenschap partitionedBy](#using-partitionedby-property).</span><span class="sxs-lookup"><span data-stu-id="c44d0-251">For details and examples, see [The partitionedBy property](#using-partitionedby-property).</span></span> |<span data-ttu-id="c44d0-252">Nee</span><span class="sxs-lookup"><span data-stu-id="c44d0-252">No</span></span> |
| <span data-ttu-id="c44d0-253">**indeling**</span><span class="sxs-lookup"><span data-stu-id="c44d0-253">**format**</span></span> | <span data-ttu-id="c44d0-254">De volgende indelingstypen worden ondersteund: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, en  **ParquetFormat**.</span><span class="sxs-lookup"><span data-stu-id="c44d0-254">The following format types are supported: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**, and **ParquetFormat**.</span></span> <span data-ttu-id="c44d0-255">Stel de **type** eigenschap onder **indeling** op een van deze waarden.</span><span class="sxs-lookup"><span data-stu-id="c44d0-255">Set the **type** property under **format** to one of these values.</span></span> <span data-ttu-id="c44d0-256">Zie voor meer informatie de [tekstindeling](data-factory-supported-file-and-compression-formats.md#text-format), [JSON-indeling](data-factory-supported-file-and-compression-formats.md#json-format), [Avro-indeling](data-factory-supported-file-and-compression-formats.md#avro-format), [ORC indeling](data-factory-supported-file-and-compression-formats.md#orc-format), en [parketvloeren-indeling ](data-factory-supported-file-and-compression-formats.md#parquet-format) secties in de [bestands- en compressie indelingen die worden ondersteund door Azure Data Factory](data-factory-supported-file-and-compression-formats.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="c44d0-256">For more information, see the [Text format](data-factory-supported-file-and-compression-formats.md#text-format), [JSON format](data-factory-supported-file-and-compression-formats.md#json-format), [Avro format](data-factory-supported-file-and-compression-formats.md#avro-format), [ORC format](data-factory-supported-file-and-compression-formats.md#orc-format), and [Parquet Format](data-factory-supported-file-and-compression-formats.md#parquet-format) sections in the [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span> <br><br> <span data-ttu-id="c44d0-257">Als u wilt kopiëren van bestanden ' als-is ' overslaan tussen bestandsgebaseerde winkels (binaire kopiëren), de `format` sectie in beide definities invoer en uitvoer gegevensset.</span><span class="sxs-lookup"><span data-stu-id="c44d0-257">If you want to copy files "as-is" between file-based stores (binary copy), skip the `format` section in both input and output dataset definitions.</span></span> |<span data-ttu-id="c44d0-258">Nee</span><span class="sxs-lookup"><span data-stu-id="c44d0-258">No</span></span> |
| <span data-ttu-id="c44d0-259">**compressie**</span><span class="sxs-lookup"><span data-stu-id="c44d0-259">**compression**</span></span> | <span data-ttu-id="c44d0-260">Geef het type en de compressie van de gegevens.</span><span class="sxs-lookup"><span data-stu-id="c44d0-260">Specify the type and level of compression for the data.</span></span> <span data-ttu-id="c44d0-261">Ondersteunde typen zijn **GZip**, **Deflate**, **BZip2**, en **ZipDeflate**.</span><span class="sxs-lookup"><span data-stu-id="c44d0-261">Supported types are **GZip**, **Deflate**, **BZip2**, and **ZipDeflate**.</span></span> <span data-ttu-id="c44d0-262">Ondersteunde niveaus zijn **optimale** en **snelst**.</span><span class="sxs-lookup"><span data-stu-id="c44d0-262">Supported levels are **Optimal** and **Fastest**.</span></span> <span data-ttu-id="c44d0-263">Zie voor meer informatie [bestands- en compressie indelingen die worden ondersteund door Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span><span class="sxs-lookup"><span data-stu-id="c44d0-263">For more information, see [File and compression formats supported by Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support).</span></span> |<span data-ttu-id="c44d0-264">Nee</span><span class="sxs-lookup"><span data-stu-id="c44d0-264">No</span></span> |

### <a name="the-partitionedby-property"></a><span data-ttu-id="c44d0-265">De eigenschap partitionedBy</span><span class="sxs-lookup"><span data-stu-id="c44d0-265">The partitionedBy property</span></span>
<span data-ttu-id="c44d0-266">Kunt u dynamische **folderPath** en **fileName** eigenschappen voor timeseries gegevens met de **partitionedBy** eigenschap, Data Factory-functies en systeemvariabelen.</span><span class="sxs-lookup"><span data-stu-id="c44d0-266">You can specify dynamic **folderPath** and **fileName** properties for time-series data with the **partitionedBy** property, Data Factory functions, and system variables.</span></span> <span data-ttu-id="c44d0-267">Zie voor meer informatie de [Azure Data Factory - functies en systeemvariabelen](data-factory-functions-variables.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="c44d0-267">For details, see the [Azure Data Factory - functions and system variables](data-factory-functions-variables.md) article.</span></span>


<span data-ttu-id="c44d0-268">In het volgende voorbeeld `{Slice}` is vervangen door de waarde van de Data Factory systeemvariabele `SliceStart` in de opgegeven indeling (`yyyyMMddHH`).</span><span class="sxs-lookup"><span data-stu-id="c44d0-268">In the following example, `{Slice}` is replaced with the value of the Data Factory system variable `SliceStart` in the format specified (`yyyyMMddHH`).</span></span> <span data-ttu-id="c44d0-269">De naam van de `SliceStart` verwijst naar de begintijd van het segment.</span><span class="sxs-lookup"><span data-stu-id="c44d0-269">The name `SliceStart` refers to the start time of the slice.</span></span> <span data-ttu-id="c44d0-270">De `folderPath` eigenschap verschilt voor elk segment, zoals in `wikidatagateway/wikisampledataout/2014100103` of `wikidatagateway/wikisampledataout/2014100104`.</span><span class="sxs-lookup"><span data-stu-id="c44d0-270">The `folderPath` property is different for each slice, as in `wikidatagateway/wikisampledataout/2014100103` or `wikidatagateway/wikisampledataout/2014100104`.</span></span>

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```

<span data-ttu-id="c44d0-271">In het volgende voorbeeld, het jaar, maand, dag en tijd van `SliceStart` worden uitgepakt in verschillende variabelen die worden gebruikt door de `folderPath` en `fileName` eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="c44d0-271">In the following example, the year, month, day, and time of `SliceStart` are extracted into separate variables that are used by the `folderPath` and `fileName` properties:</span></span>
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
<span data-ttu-id="c44d0-272">Zie voor meer informatie over tijdreeks gegevenssets, planning en segmenten de [gegevenssets in Azure Data Factory](data-factory-create-datasets.md) en [Data Factory plannen en uitvoeren](data-factory-scheduling-and-execution.md) artikelen.</span><span class="sxs-lookup"><span data-stu-id="c44d0-272">For more details on time-series datasets, scheduling, and slices, see the [Datasets in Azure Data Factory](data-factory-create-datasets.md) and [Data Factory scheduling and execution](data-factory-scheduling-and-execution.md) articles.</span></span> 


## <a name="copy-activity-properties"></a><span data-ttu-id="c44d0-273">Eigenschappen van de activiteit kopiëren</span><span class="sxs-lookup"><span data-stu-id="c44d0-273">Copy activity properties</span></span>
<span data-ttu-id="c44d0-274">Zie voor een volledige lijst met secties en de eigenschappen die beschikbaar zijn voor het definiëren van activiteiten, de [pijplijnen maken](data-factory-create-pipelines.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="c44d0-274">For a full list of sections and properties available for defining activities, see the [Creating pipelines](data-factory-create-pipelines.md) article.</span></span> <span data-ttu-id="c44d0-275">Eigenschappen op, zoals naam, beschrijving, invoer en uitvoer tabellen en -beleid zijn beschikbaar voor alle typen activiteiten.</span><span class="sxs-lookup"><span data-stu-id="c44d0-275">Properties such as name, description, input and output tables, and policy are available for all types of activities.</span></span>

<span data-ttu-id="c44d0-276">De eigenschappen die beschikbaar zijn in de **typeProperties** gedeelte van een activiteit variëren met elk activiteitstype.</span><span class="sxs-lookup"><span data-stu-id="c44d0-276">The properties available in the **typeProperties** section of an activity vary with each activity type.</span></span> <span data-ttu-id="c44d0-277">Voor een kopieeractiviteit variëren ze, afhankelijk van de typen van bronnen en Put.</span><span class="sxs-lookup"><span data-stu-id="c44d0-277">For a copy activity, they vary depending on the types of sources and sinks.</span></span>

<span data-ttu-id="c44d0-278">**AzureDataLakeStoreSource** ondersteunt de volgende eigenschap in de **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="c44d0-278">**AzureDataLakeStoreSource** supports the following property in the **typeProperties** section:</span></span>

| <span data-ttu-id="c44d0-279">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="c44d0-279">Property</span></span> | <span data-ttu-id="c44d0-280">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c44d0-280">Description</span></span> | <span data-ttu-id="c44d0-281">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="c44d0-281">Allowed values</span></span> | <span data-ttu-id="c44d0-282">Vereist</span><span class="sxs-lookup"><span data-stu-id="c44d0-282">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c44d0-283">**recursieve**</span><span class="sxs-lookup"><span data-stu-id="c44d0-283">**recursive**</span></span> |<span data-ttu-id="c44d0-284">Hiermee wordt aangegeven of de gegevens recursief is gelezen uit de submappen of alleen uit de opgegeven map.</span><span class="sxs-lookup"><span data-stu-id="c44d0-284">Indicates whether the data is read recursively from the subfolders or only from the specified folder.</span></span> |<span data-ttu-id="c44d0-285">True (standaardwaarde), False</span><span class="sxs-lookup"><span data-stu-id="c44d0-285">True (default value), False</span></span> |<span data-ttu-id="c44d0-286">Nee</span><span class="sxs-lookup"><span data-stu-id="c44d0-286">No</span></span> |


<span data-ttu-id="c44d0-287">**AzureDataLakeStoreSink** ondersteunt de volgende eigenschappen in de **typeProperties** sectie:</span><span class="sxs-lookup"><span data-stu-id="c44d0-287">**AzureDataLakeStoreSink** supports the following properties in the **typeProperties** section:</span></span>

| <span data-ttu-id="c44d0-288">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="c44d0-288">Property</span></span> | <span data-ttu-id="c44d0-289">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="c44d0-289">Description</span></span> | <span data-ttu-id="c44d0-290">Toegestane waarden</span><span class="sxs-lookup"><span data-stu-id="c44d0-290">Allowed values</span></span> | <span data-ttu-id="c44d0-291">Vereist</span><span class="sxs-lookup"><span data-stu-id="c44d0-291">Required</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="c44d0-292">**copyBehavior**</span><span class="sxs-lookup"><span data-stu-id="c44d0-292">**copyBehavior**</span></span> |<span data-ttu-id="c44d0-293">Hiermee geeft u het gedrag van de kopie.</span><span class="sxs-lookup"><span data-stu-id="c44d0-293">Specifies the copy behavior.</span></span> |<span data-ttu-id="c44d0-294"><b>PreserveHierarchy</b>: behoudt de bestandshiërarchie in de doelmap.</span><span class="sxs-lookup"><span data-stu-id="c44d0-294"><b>PreserveHierarchy</b>: Preserves the file hierarchy in the target folder.</span></span> <span data-ttu-id="c44d0-295">Het relatieve pad van het bronbestand naar de bronmap is identiek aan het relatieve pad van doelbestand naar doelmap.</span><span class="sxs-lookup"><span data-stu-id="c44d0-295">The relative path of source file to source folder is identical to the relative path of target file to target folder.</span></span><br/><br/><span data-ttu-id="c44d0-296"><b>FlattenHierarchy</b>: alle bestanden uit de bronmap worden gemaakt in het eerste niveau van de doelmap.</span><span class="sxs-lookup"><span data-stu-id="c44d0-296"><b>FlattenHierarchy</b>: All files from the source folder are created in the first level of the target folder.</span></span> <span data-ttu-id="c44d0-297">De doelbestanden worden gemaakt met de automatisch gegenereerde namen.</span><span class="sxs-lookup"><span data-stu-id="c44d0-297">The target files are created with autogenerated names.</span></span><br/><br/><span data-ttu-id="c44d0-298"><b>MergeFiles</b>: alle bestanden uit de bronmap op één bestand worden samengevoegd.</span><span class="sxs-lookup"><span data-stu-id="c44d0-298"><b>MergeFiles</b>: Merges all files from the source folder to one file.</span></span> <span data-ttu-id="c44d0-299">Als de naam van het bestand of blob is opgegeven, is de samengevoegde bestandsnaam de opgegeven naam.</span><span class="sxs-lookup"><span data-stu-id="c44d0-299">If the file or blob name is specified, the merged file name is the specified name.</span></span> <span data-ttu-id="c44d0-300">De bestandsnaam is anders wordt automatisch gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="c44d0-300">Otherwise, the file name is autogenerated.</span></span> |<span data-ttu-id="c44d0-301">Nee</span><span class="sxs-lookup"><span data-stu-id="c44d0-301">No</span></span> |

### <a name="recursive-and-copybehavior-examples"></a><span data-ttu-id="c44d0-302">Voorbeelden van recursieve en copyBehavior</span><span class="sxs-lookup"><span data-stu-id="c44d0-302">recursive and copyBehavior examples</span></span>
<span data-ttu-id="c44d0-303">Deze sectie beschrijft het resulterende gedrag van de kopieerbewerking voor verschillende combinaties van recursieve en copyBehavior waarden.</span><span class="sxs-lookup"><span data-stu-id="c44d0-303">This section describes the resulting behavior of the Copy operation for different combinations of recursive and copyBehavior values.</span></span>

| <span data-ttu-id="c44d0-304">Recursieve</span><span class="sxs-lookup"><span data-stu-id="c44d0-304">recursive</span></span> | <span data-ttu-id="c44d0-305">copyBehavior</span><span class="sxs-lookup"><span data-stu-id="c44d0-305">copyBehavior</span></span> | <span data-ttu-id="c44d0-306">Resulterende gedrag</span><span class="sxs-lookup"><span data-stu-id="c44d0-306">Resulting behavior</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c44d0-307">De waarde True</span><span class="sxs-lookup"><span data-stu-id="c44d0-307">true</span></span> |<span data-ttu-id="c44d0-308">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="c44d0-308">preserveHierarchy</span></span> |<span data-ttu-id="c44d0-309">Voor een bronmap Map1 met de volgende structuur:</span><span class="sxs-lookup"><span data-stu-id="c44d0-309">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="c44d0-310">Map1</span><span class="sxs-lookup"><span data-stu-id="c44d0-310">Folder1</span></span><br/><span data-ttu-id="c44d0-311">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="c44d0-311">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="c44d0-312">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="c44d0-312">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="c44d0-313">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="c44d0-313">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="c44d0-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="c44d0-314">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="c44d0-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="c44d0-315">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="c44d0-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="c44d0-316">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="c44d0-317">de doelmap Map1 wordt gemaakt met dezelfde structuur als de bron</span><span class="sxs-lookup"><span data-stu-id="c44d0-317">the target folder Folder1 is created with the same structure as the source</span></span><br/><br/><span data-ttu-id="c44d0-318">Map1</span><span class="sxs-lookup"><span data-stu-id="c44d0-318">Folder1</span></span><br/><span data-ttu-id="c44d0-319">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="c44d0-319">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="c44d0-320">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="c44d0-320">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="c44d0-321">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="c44d0-321">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="c44d0-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="c44d0-322">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="c44d0-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="c44d0-323">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="c44d0-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span><span class="sxs-lookup"><span data-stu-id="c44d0-324">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5.</span></span> |
| <span data-ttu-id="c44d0-325">De waarde True</span><span class="sxs-lookup"><span data-stu-id="c44d0-325">true</span></span> |<span data-ttu-id="c44d0-326">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="c44d0-326">flattenHierarchy</span></span> |<span data-ttu-id="c44d0-327">Voor een bronmap Map1 met de volgende structuur:</span><span class="sxs-lookup"><span data-stu-id="c44d0-327">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="c44d0-328">Map1</span><span class="sxs-lookup"><span data-stu-id="c44d0-328">Folder1</span></span><br/><span data-ttu-id="c44d0-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="c44d0-329">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="c44d0-330">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="c44d0-330">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="c44d0-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="c44d0-331">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="c44d0-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="c44d0-332">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="c44d0-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="c44d0-333">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="c44d0-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="c44d0-334">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="c44d0-335">het doel Map1 wordt gemaakt met de volgende structuur:</span><span class="sxs-lookup"><span data-stu-id="c44d0-335">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="c44d0-336">Map1</span><span class="sxs-lookup"><span data-stu-id="c44d0-336">Folder1</span></span><br/><span data-ttu-id="c44d0-337">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor File1</span><span class="sxs-lookup"><span data-stu-id="c44d0-337">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="c44d0-338">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor bestand2</span><span class="sxs-lookup"><span data-stu-id="c44d0-338">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><span data-ttu-id="c44d0-339">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor bestand3</span><span class="sxs-lookup"><span data-stu-id="c44d0-339">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File3</span></span><br/><span data-ttu-id="c44d0-340">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor File4</span><span class="sxs-lookup"><span data-stu-id="c44d0-340">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File4</span></span><br/><span data-ttu-id="c44d0-341">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor File5</span><span class="sxs-lookup"><span data-stu-id="c44d0-341">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File5</span></span> |
| <span data-ttu-id="c44d0-342">De waarde True</span><span class="sxs-lookup"><span data-stu-id="c44d0-342">true</span></span> |<span data-ttu-id="c44d0-343">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="c44d0-343">mergeFiles</span></span> |<span data-ttu-id="c44d0-344">Voor een bronmap Map1 met de volgende structuur:</span><span class="sxs-lookup"><span data-stu-id="c44d0-344">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="c44d0-345">Map1</span><span class="sxs-lookup"><span data-stu-id="c44d0-345">Folder1</span></span><br/><span data-ttu-id="c44d0-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="c44d0-346">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="c44d0-347">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="c44d0-347">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="c44d0-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="c44d0-348">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="c44d0-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="c44d0-349">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="c44d0-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="c44d0-350">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="c44d0-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="c44d0-351">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="c44d0-352">het doel Map1 wordt gemaakt met de volgende structuur:</span><span class="sxs-lookup"><span data-stu-id="c44d0-352">the target Folder1 is created with the following structure:</span></span> <br/><br/><span data-ttu-id="c44d0-353">Map1</span><span class="sxs-lookup"><span data-stu-id="c44d0-353">Folder1</span></span><br/><span data-ttu-id="c44d0-354">&nbsp;&nbsp;&nbsp;&nbsp;File1 bestand2 + bestand3 + File4 + bestand 5 inhoud worden samengevoegd in één bestand met automatisch gegenereerde naam</span><span class="sxs-lookup"><span data-stu-id="c44d0-354">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 + File3 + File4 + File 5 contents are merged into one file with auto-generated file name</span></span> |
| <span data-ttu-id="c44d0-355">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="c44d0-355">false</span></span> |<span data-ttu-id="c44d0-356">preserveHierarchy</span><span class="sxs-lookup"><span data-stu-id="c44d0-356">preserveHierarchy</span></span> |<span data-ttu-id="c44d0-357">Voor een bronmap Map1 met de volgende structuur:</span><span class="sxs-lookup"><span data-stu-id="c44d0-357">For a source folder Folder1 with the following structure:</span></span> <br/><br/><span data-ttu-id="c44d0-358">Map1</span><span class="sxs-lookup"><span data-stu-id="c44d0-358">Folder1</span></span><br/><span data-ttu-id="c44d0-359">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="c44d0-359">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="c44d0-360">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="c44d0-360">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="c44d0-361">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="c44d0-361">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="c44d0-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="c44d0-362">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="c44d0-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="c44d0-363">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="c44d0-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="c44d0-364">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="c44d0-365">de doelmap Map1 wordt gemaakt met de volgende structuur</span><span class="sxs-lookup"><span data-stu-id="c44d0-365">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="c44d0-366">Map1</span><span class="sxs-lookup"><span data-stu-id="c44d0-366">Folder1</span></span><br/><span data-ttu-id="c44d0-367">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="c44d0-367">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="c44d0-368">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="c44d0-368">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><br/><br/><span data-ttu-id="c44d0-369">Subfolder1 bestand3 File4 en File5 zijn niet opgenomen.</span><span class="sxs-lookup"><span data-stu-id="c44d0-369">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="c44d0-370">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="c44d0-370">false</span></span> |<span data-ttu-id="c44d0-371">flattenHierarchy</span><span class="sxs-lookup"><span data-stu-id="c44d0-371">flattenHierarchy</span></span> |<span data-ttu-id="c44d0-372">Voor een bronmap Map1 met de volgende structuur:</span><span class="sxs-lookup"><span data-stu-id="c44d0-372">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="c44d0-373">Map1</span><span class="sxs-lookup"><span data-stu-id="c44d0-373">Folder1</span></span><br/><span data-ttu-id="c44d0-374">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="c44d0-374">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="c44d0-375">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="c44d0-375">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="c44d0-376">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="c44d0-376">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="c44d0-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="c44d0-377">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="c44d0-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="c44d0-378">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="c44d0-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="c44d0-379">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="c44d0-380">de doelmap Map1 wordt gemaakt met de volgende structuur</span><span class="sxs-lookup"><span data-stu-id="c44d0-380">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="c44d0-381">Map1</span><span class="sxs-lookup"><span data-stu-id="c44d0-381">Folder1</span></span><br/><span data-ttu-id="c44d0-382">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor File1</span><span class="sxs-lookup"><span data-stu-id="c44d0-382">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File1</span></span><br/><span data-ttu-id="c44d0-383">&nbsp;&nbsp;&nbsp;&nbsp;automatisch gegenereerde naam voor bestand2</span><span class="sxs-lookup"><span data-stu-id="c44d0-383">&nbsp;&nbsp;&nbsp;&nbsp;auto-generated name for File2</span></span><br/><br/><br/><span data-ttu-id="c44d0-384">Subfolder1 bestand3 File4 en File5 zijn niet opgenomen.</span><span class="sxs-lookup"><span data-stu-id="c44d0-384">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |
| <span data-ttu-id="c44d0-385">ONWAAR</span><span class="sxs-lookup"><span data-stu-id="c44d0-385">false</span></span> |<span data-ttu-id="c44d0-386">mergeFiles</span><span class="sxs-lookup"><span data-stu-id="c44d0-386">mergeFiles</span></span> |<span data-ttu-id="c44d0-387">Voor een bronmap Map1 met de volgende structuur:</span><span class="sxs-lookup"><span data-stu-id="c44d0-387">For a source folder Folder1 with the following structure:</span></span><br/><br/><span data-ttu-id="c44d0-388">Map1</span><span class="sxs-lookup"><span data-stu-id="c44d0-388">Folder1</span></span><br/><span data-ttu-id="c44d0-389">&nbsp;&nbsp;&nbsp;&nbsp;File1</span><span class="sxs-lookup"><span data-stu-id="c44d0-389">&nbsp;&nbsp;&nbsp;&nbsp;File1</span></span><br/><span data-ttu-id="c44d0-390">&nbsp;&nbsp;&nbsp;&nbsp;Bestand2</span><span class="sxs-lookup"><span data-stu-id="c44d0-390">&nbsp;&nbsp;&nbsp;&nbsp;File2</span></span><br/><span data-ttu-id="c44d0-391">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span><span class="sxs-lookup"><span data-stu-id="c44d0-391">&nbsp;&nbsp;&nbsp;&nbsp;Subfolder1</span></span><br/><span data-ttu-id="c44d0-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Bestand3</span><span class="sxs-lookup"><span data-stu-id="c44d0-392">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File3</span></span><br/><span data-ttu-id="c44d0-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span><span class="sxs-lookup"><span data-stu-id="c44d0-393">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File4</span></span><br/><span data-ttu-id="c44d0-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span><span class="sxs-lookup"><span data-stu-id="c44d0-394">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;File5</span></span><br/><br/><span data-ttu-id="c44d0-395">de doelmap Map1 wordt gemaakt met de volgende structuur</span><span class="sxs-lookup"><span data-stu-id="c44d0-395">the target folder Folder1 is created with the following structure</span></span><br/><br/><span data-ttu-id="c44d0-396">Map1</span><span class="sxs-lookup"><span data-stu-id="c44d0-396">Folder1</span></span><br/><span data-ttu-id="c44d0-397">&nbsp;&nbsp;&nbsp;&nbsp;File1 + bestand2 inhoud worden samengevoegd in één bestand met automatisch gegenereerde naam.</span><span class="sxs-lookup"><span data-stu-id="c44d0-397">&nbsp;&nbsp;&nbsp;&nbsp;File1 + File2 contents are merged into one file with auto-generated file name.</span></span> <span data-ttu-id="c44d0-398">automatisch gegenereerde naam voor File1</span><span class="sxs-lookup"><span data-stu-id="c44d0-398">auto-generated name for File1</span></span><br/><br/><span data-ttu-id="c44d0-399">Subfolder1 bestand3 File4 en File5 zijn niet opgenomen.</span><span class="sxs-lookup"><span data-stu-id="c44d0-399">Subfolder1 with File3, File4, and File5 are not picked up.</span></span> |

## <a name="supported-file-and-compression-formats"></a><span data-ttu-id="c44d0-400">Ondersteunde indelingen voor bestands- en compressie</span><span class="sxs-lookup"><span data-stu-id="c44d0-400">Supported file and compression formats</span></span>
<span data-ttu-id="c44d0-401">Zie voor meer informatie de [bestands- en compressie-notaties in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="c44d0-401">For details, see the [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md) article.</span></span>

## <a name="json-examples-for-copying-data-to-and-from-data-lake-store"></a><span data-ttu-id="c44d0-402">JSON-voorbeelden voor het kopiëren van gegevens naar en van Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c44d0-402">JSON examples for copying data to and from Data Lake Store</span></span>
<span data-ttu-id="c44d0-403">De volgende voorbeelden geven voorbeeld JSON definities.</span><span class="sxs-lookup"><span data-stu-id="c44d0-403">The following examples provide sample JSON definitions.</span></span> <span data-ttu-id="c44d0-404">U kunt deze definities voorbeeld een pijplijn maken met behulp van de [Azure-portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), of [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c44d0-404">You can use these sample definitions to create a pipeline by using the [Azure portal](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), or [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).</span></span> <span data-ttu-id="c44d0-405">De voorbeelden laten zien hoe om gegevens te kopiëren naar en van Data Lake Store en Azure Blob storage.</span><span class="sxs-lookup"><span data-stu-id="c44d0-405">The examples show how to copy data to and from Data Lake Store and Azure Blob storage.</span></span> <span data-ttu-id="c44d0-406">Echter, de gegevens kunnen worden gekopieerd _rechtstreeks_ uit een van de bronnen aan een van de ondersteunde Put.</span><span class="sxs-lookup"><span data-stu-id="c44d0-406">However, data can be copied _directly_ from any of the sources to any of the supported sinks.</span></span> <span data-ttu-id="c44d0-407">Zie voor meer informatie de sectie 'ondersteunde gegevensarchieven en indelingen' in de [verplaatsen van gegevens met behulp van de Kopieeractiviteit](data-factory-data-movement-activities.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="c44d0-407">For more information, see the section "Supported data stores and formats" in the [Move data by using Copy Activity](data-factory-data-movement-activities.md) article.</span></span>  

### <a name="example-copy-data-from-azure-blob-storage-to-azure-data-lake-store"></a><span data-ttu-id="c44d0-408">Voorbeeld: Gegevens kopiëren van Azure Blob-opslag naar Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="c44d0-408">Example: Copy data from Azure Blob Storage to Azure Data Lake Store</span></span>
<span data-ttu-id="c44d0-409">De voorbeeldcode in dit gedeelte ziet:</span><span class="sxs-lookup"><span data-stu-id="c44d0-409">The example code in this section shows:</span></span>

* <span data-ttu-id="c44d0-410">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c44d0-410">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="c44d0-411">Een gekoppelde service van het type [AzureDataLakeStore](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c44d0-411">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="c44d0-412">Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c44d0-412">An input [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="c44d0-413">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureDataLakeStore](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c44d0-413">An output [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="c44d0-414">Een [pijplijn](data-factory-create-pipelines.md) met een kopieeractiviteit die gebruikmaakt van [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) en [AzureDataLakeStoreSink](#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="c44d0-414">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) and [AzureDataLakeStoreSink](#copy-activity-properties).</span></span>

<span data-ttu-id="c44d0-415">De voorbeelden laten zien hoe timeseries gegevens uit Azure Blob Storage is gekopieerd naar Data Lake Store om het uur.</span><span class="sxs-lookup"><span data-stu-id="c44d0-415">The examples show how time-series data from Azure Blob Storage is copied to Data Lake Store every hour.</span></span> 

<span data-ttu-id="c44d0-416">**Een gekoppelde Azure Storage-service**</span><span class="sxs-lookup"><span data-stu-id="c44d0-416">**Azure Storage linked service**</span></span>

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

<span data-ttu-id="c44d0-417">**Gekoppelde service van Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="c44d0-417">**Azure Data Lake Store linked service**</span></span>

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
> <span data-ttu-id="c44d0-418">Zie voor configuratiedetails de [gekoppelde service-eigenschappen](#linked-service-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="c44d0-418">For configuration details, see the [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="c44d0-419">**De Azure Blob-invoergegevensset**</span><span class="sxs-lookup"><span data-stu-id="c44d0-419">**Azure blob input dataset**</span></span>

<span data-ttu-id="c44d0-420">In het volgende voorbeeld gegevens wordt opgehaald uit een nieuwe blob elk uur (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="c44d0-420">In the following example, data is picked up from a new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="c44d0-421">Pad en naam van de map voor de blob worden dynamisch geëvalueerd op basis van de begintijd van het segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="c44d0-421">The folder path and file name for the blob are dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="c44d0-422">Het mappad maakt gebruik van het jaar, maand en daggedeelte van de begintijd.</span><span class="sxs-lookup"><span data-stu-id="c44d0-422">The folder path uses the year, month, and day portion of the start time.</span></span> <span data-ttu-id="c44d0-423">De bestandsnaam wordt gebruikt voor het uurgedeelte van de begintijd.</span><span class="sxs-lookup"><span data-stu-id="c44d0-423">The file name uses the hour portion of the start time.</span></span> <span data-ttu-id="c44d0-424">De `"external": true` instelling informeert de Data Factory-service dat de tabel aan de gegevensfactory extern en niet wordt geproduceerd door een activiteit in de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="c44d0-424">The `"external": true` setting informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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

<span data-ttu-id="c44d0-425">**Azure Data Lake Store uitvoergegevensset**</span><span class="sxs-lookup"><span data-stu-id="c44d0-425">**Azure Data Lake Store output dataset**</span></span>

<span data-ttu-id="c44d0-426">Het volgende voorbeeld worden gegevens gekopieerd naar Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c44d0-426">The following example copies data to Data Lake Store.</span></span> <span data-ttu-id="c44d0-427">Nieuwe gegevens worden gekopieerd naar Data Lake Store om het uur.</span><span class="sxs-lookup"><span data-stu-id="c44d0-427">New data is copied to Data Lake Store every hour.</span></span>

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


<span data-ttu-id="c44d0-428">**Kopieeractiviteit in een pijplijn met een blob-bron- en een Data Lake Store-sink**</span><span class="sxs-lookup"><span data-stu-id="c44d0-428">**Copy activity in a pipeline with a blob source and a Data Lake Store sink**</span></span>

<span data-ttu-id="c44d0-429">De pijplijn bevat in het volgende voorbeeld wordt een kopieeractiviteit die is geconfigureerd voor gebruik van de invoer- en uitvoergegevenssets.</span><span class="sxs-lookup"><span data-stu-id="c44d0-429">In the following example, the pipeline contains a copy activity that is configured to use the input and output datasets.</span></span> <span data-ttu-id="c44d0-430">De kopieerbewerking is gepland voor elk uur uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c44d0-430">The copy activity is scheduled to run every hour.</span></span> <span data-ttu-id="c44d0-431">In de pijplijn-JSON-definitie de `source` type is ingesteld op `BlobSource`, en de `sink` type is ingesteld op `AzureDataLakeStoreSink`.</span><span class="sxs-lookup"><span data-stu-id="c44d0-431">In the pipeline JSON definition, the `source` type is set to `BlobSource`, and the `sink` type is set to `AzureDataLakeStoreSink`.</span></span>

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

### <a name="example-copy-data-from-azure-data-lake-store-to-an-azure-blob"></a><span data-ttu-id="c44d0-432">Voorbeeld: Gegevens kopiëren van Azure Data Lake Store naar een Azure-blob</span><span class="sxs-lookup"><span data-stu-id="c44d0-432">Example: Copy data from Azure Data Lake Store to an Azure blob</span></span>
<span data-ttu-id="c44d0-433">De voorbeeldcode in dit gedeelte ziet:</span><span class="sxs-lookup"><span data-stu-id="c44d0-433">The example code in this section shows:</span></span>

* <span data-ttu-id="c44d0-434">Een gekoppelde service van het type [AzureDataLakeStore](#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c44d0-434">A linked service of type [AzureDataLakeStore](#linked-service-properties).</span></span>
* <span data-ttu-id="c44d0-435">Een gekoppelde service van het type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span><span class="sxs-lookup"><span data-stu-id="c44d0-435">A linked service of type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).</span></span>
* <span data-ttu-id="c44d0-436">Invoer [gegevensset](data-factory-create-datasets.md) van het type [AzureDataLakeStore](#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c44d0-436">An input [dataset](data-factory-create-datasets.md) of type [AzureDataLakeStore](#dataset-properties).</span></span>
* <span data-ttu-id="c44d0-437">Uitvoer [gegevensset](data-factory-create-datasets.md) van het type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span><span class="sxs-lookup"><span data-stu-id="c44d0-437">An output [dataset](data-factory-create-datasets.md) of type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).</span></span>
* <span data-ttu-id="c44d0-438">Een [pijplijn](data-factory-create-pipelines.md) met een kopieeractiviteit die gebruikmaakt van [AzureDataLakeStoreSource](#copy-activity-properties) en [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span><span class="sxs-lookup"><span data-stu-id="c44d0-438">A [pipeline](data-factory-create-pipelines.md) with a copy activity that uses [AzureDataLakeStoreSource](#copy-activity-properties) and [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).</span></span>

<span data-ttu-id="c44d0-439">De code opgehaald-timeseries-gegevens in Data Lake Store met een Azure-blob elk uur.</span><span class="sxs-lookup"><span data-stu-id="c44d0-439">The code copies time-series data from Data Lake Store to an Azure blob every hour.</span></span> 

<span data-ttu-id="c44d0-440">**Gekoppelde service van Azure Data Lake Store**</span><span class="sxs-lookup"><span data-stu-id="c44d0-440">**Azure Data Lake Store linked service**</span></span>

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
> <span data-ttu-id="c44d0-441">Zie voor configuratiedetails de [gekoppelde service-eigenschappen](#linked-service-properties) sectie.</span><span class="sxs-lookup"><span data-stu-id="c44d0-441">For configuration details, see the [Linked service properties](#linked-service-properties) section.</span></span>
>

<span data-ttu-id="c44d0-442">**Een gekoppelde Azure Storage-service**</span><span class="sxs-lookup"><span data-stu-id="c44d0-442">**Azure Storage linked service**</span></span>

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
<span data-ttu-id="c44d0-443">**Azure Data Lake invoergegevensset**</span><span class="sxs-lookup"><span data-stu-id="c44d0-443">**Azure Data Lake input dataset**</span></span>

<span data-ttu-id="c44d0-444">In dit voorbeeld instelling `"external"` naar `true` informeert de Data Factory-service dat de tabel aan de gegevensfactory extern en niet wordt geproduceerd door een activiteit in de gegevensfactory.</span><span class="sxs-lookup"><span data-stu-id="c44d0-444">In this example, setting `"external"` to `true` informs the Data Factory service that the table is external to the data factory and is not produced by an activity in the data factory.</span></span>

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
<span data-ttu-id="c44d0-445">**De Azure Blob-uitvoergegevensset**</span><span class="sxs-lookup"><span data-stu-id="c44d0-445">**Azure blob output dataset**</span></span>

<span data-ttu-id="c44d0-446">In het volgende voorbeeld gegevens worden geschreven naar een nieuwe blob elk uur (`"frequency": "Hour", "interval": 1`).</span><span class="sxs-lookup"><span data-stu-id="c44d0-446">In the following example, data is written to a new blob every hour (`"frequency": "Hour", "interval": 1`).</span></span> <span data-ttu-id="c44d0-447">Het pad naar de blob wordt dynamisch geëvalueerd op basis van de begintijd van het segment dat wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="c44d0-447">The folder path for the blob is dynamically evaluated based on the start time of the slice that is being processed.</span></span> <span data-ttu-id="c44d0-448">Het mappad maakt gebruik van het jaar, maand, dag en uur gedeelte van de begintijd.</span><span class="sxs-lookup"><span data-stu-id="c44d0-448">The folder path uses the year, month, day, and hours portion of the start time.</span></span>

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

<span data-ttu-id="c44d0-449">**Een kopieeractiviteit in een pijplijn met een Azure Data Lake Store-bron- en een blob-sink**</span><span class="sxs-lookup"><span data-stu-id="c44d0-449">**A copy activity in a pipeline with an Azure Data Lake Store source and a blob sink**</span></span>

<span data-ttu-id="c44d0-450">De pijplijn bevat in het volgende voorbeeld wordt een kopieeractiviteit die is geconfigureerd voor gebruik van de invoer- en uitvoergegevenssets.</span><span class="sxs-lookup"><span data-stu-id="c44d0-450">In the following example, the pipeline contains a copy activity that is configured to use the input and output datasets.</span></span> <span data-ttu-id="c44d0-451">De kopieerbewerking is gepland voor elk uur uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c44d0-451">The copy activity is scheduled to run every hour.</span></span> <span data-ttu-id="c44d0-452">In de pijplijn-JSON-definitie de `source` type is ingesteld op `AzureDataLakeStoreSource`, en de `sink` type is ingesteld op `BlobSink`.</span><span class="sxs-lookup"><span data-stu-id="c44d0-452">In the pipeline JSON definition, the `source` type is set to `AzureDataLakeStoreSource`, and the `sink` type is set to `BlobSink`.</span></span>

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

<span data-ttu-id="c44d0-453">U kunt ook kolommen uit de bron-gegevensset naar kolommen in de gegevensset sink toewijzen in de definitie van de activiteit kopiëren.</span><span class="sxs-lookup"><span data-stu-id="c44d0-453">In the copy activity definition, you can also map columns from the source dataset to columns in the sink dataset.</span></span> <span data-ttu-id="c44d0-454">Zie voor meer informatie [toewijzing gegevensset kolommen in Azure Data Factory](data-factory-map-columns.md).</span><span class="sxs-lookup"><span data-stu-id="c44d0-454">For details, see [Mapping dataset columns in Azure Data Factory](data-factory-map-columns.md).</span></span>

## <a name="performance-and-tuning"></a><span data-ttu-id="c44d0-455">Prestaties en afstemmen</span><span class="sxs-lookup"><span data-stu-id="c44d0-455">Performance and tuning</span></span>
<span data-ttu-id="c44d0-456">Zie voor meer informatie over de factoren die invloed hebben op prestaties van de Kopieeractiviteit en optimaliseren het, de [Kopieeractiviteit prestaties en prestatieafstemming handleiding](data-factory-copy-activity-performance.md) artikel.</span><span class="sxs-lookup"><span data-stu-id="c44d0-456">To learn about the factors that affect Copy Activity performance and how to optimize it, see the [Copy Activity performance and tuning guide](data-factory-copy-activity-performance.md) article.</span></span>
