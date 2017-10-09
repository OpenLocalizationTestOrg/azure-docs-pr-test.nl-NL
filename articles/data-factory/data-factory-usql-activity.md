---
title: aaaTransform gegevens met behulp van U-SQL-script - Azure | Microsoft Docs
description: Meer informatie over hoe de service voor het berekenen van tooprocess of transformatie gegevens door op Azure Data Lake Analytics U-SQL-scripts.
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e17c1255-62c2-4e2e-bb60-d25274903e80
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: spelluru
ms.openlocfilehash: 51fdb40334d0c131720f65c3a96b4c5045a98b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-by-running-u-sql-scripts-on-azure-data-lake-analytics"></a><span data-ttu-id="4e531-103">Transformeer gegevens door het U-SQL-scripts uitvoeren op Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="4e531-103">Transform data by running U-SQL scripts on Azure Data Lake Analytics</span></span> 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [<span data-ttu-id="4e531-104">Hive-activiteit</span><span class="sxs-lookup"><span data-stu-id="4e531-104">Hive Activity</span></span>](data-factory-hive-activity.md) 
> * [<span data-ttu-id="4e531-105">Pig-activiteit</span><span class="sxs-lookup"><span data-stu-id="4e531-105">Pig Activity</span></span>](data-factory-pig-activity.md)
> * [<span data-ttu-id="4e531-106">MapReduce-activiteit</span><span class="sxs-lookup"><span data-stu-id="4e531-106">MapReduce Activity</span></span>](data-factory-map-reduce.md)
> * [<span data-ttu-id="4e531-107">Hadoop-Streamingactiviteit</span><span class="sxs-lookup"><span data-stu-id="4e531-107">Hadoop Streaming Activity</span></span>](data-factory-hadoop-streaming-activity.md)
> * [<span data-ttu-id="4e531-108">Spark-activiteit</span><span class="sxs-lookup"><span data-stu-id="4e531-108">Spark Activity</span></span>](data-factory-spark.md)
> * [<span data-ttu-id="4e531-109">Machine Learning-batchuitvoeringsactiviteit</span><span class="sxs-lookup"><span data-stu-id="4e531-109">Machine Learning Batch Execution Activity</span></span>](data-factory-azure-ml-batch-execution-activity.md)
> * [<span data-ttu-id="4e531-110">Machine Learning-activiteit resources bijwerken</span><span class="sxs-lookup"><span data-stu-id="4e531-110">Machine Learning Update Resource Activity</span></span>](data-factory-azure-ml-update-resource-activity.md)
> * [<span data-ttu-id="4e531-111">Opgeslagen procedureactiviteit</span><span class="sxs-lookup"><span data-stu-id="4e531-111">Stored Procedure Activity</span></span>](data-factory-stored-proc-activity.md)
> * [<span data-ttu-id="4e531-112">Data Lake Analytics U-SQL-activiteit</span><span class="sxs-lookup"><span data-stu-id="4e531-112">Data Lake Analytics U-SQL Activity</span></span>](data-factory-usql-activity.md)
> * [<span data-ttu-id="4e531-113">Aangepaste activiteit .NET</span><span class="sxs-lookup"><span data-stu-id="4e531-113">.NET Custom Activity</span></span>](data-factory-use-custom-activities.md)

<span data-ttu-id="4e531-114">Een pijplijn in een Azure data factory verwerkt gegevens in gekoppelde storage-services met behulp van gekoppelde compute services.</span><span class="sxs-lookup"><span data-stu-id="4e531-114">A pipeline in an Azure data factory processes data in linked storage services by using linked compute services.</span></span> <span data-ttu-id="4e531-115">Het bevat een reeks activiteiten, waarbij elke activiteit uitvoert voor een specifieke verwerking.</span><span class="sxs-lookup"><span data-stu-id="4e531-115">It contains a sequence of activities where each activity performs a specific processing operation.</span></span> <span data-ttu-id="4e531-116">Dit artikel wordt beschreven Hallo **Data Lake Analytics U-SQL-activiteit** die wordt uitgevoerd een **U-SQL** script op een **Azure Data Lake Analytics** berekenen van de gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="4e531-116">This article describes hello **Data Lake Analytics U-SQL Activity** that runs a **U-SQL** script on an **Azure Data Lake Analytics** compute linked service.</span></span> 

> [!NOTE]
> <span data-ttu-id="4e531-117">Een Azure Data Lake Analytics-account maken voordat u een pijplijn maakt met een Data Lake Analytics U-SQL-activiteit.</span><span class="sxs-lookup"><span data-stu-id="4e531-117">Create an Azure Data Lake Analytics account before creating a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="4e531-118">Zie toolearn over Azure Data Lake Analytics [aan de slag met Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="4e531-118">toolearn about Azure Data Lake Analytics, see [Get started with Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span>
> 
> <span data-ttu-id="4e531-119">Bekijk Hallo [bouwen van uw eerste pijplijn-zelfstudie](data-factory-build-your-first-pipeline.md) voor gedetailleerde stappen toocreate een gegevensfactory, gekoppelde services, gegevenssets en een pijplijn.</span><span class="sxs-lookup"><span data-stu-id="4e531-119">Review hello [Build your first pipeline tutorial](data-factory-build-your-first-pipeline.md) for detailed steps toocreate a data factory, linked services, datasets, and a pipeline.</span></span> <span data-ttu-id="4e531-120">JSON-codefragmenten gebruiken met Data Factory-Editor of Visual Studio of Azure PowerShell toocreate Data Factory-entiteiten.</span><span class="sxs-lookup"><span data-stu-id="4e531-120">Use JSON snippets with Data Factory Editor or Visual Studio or Azure PowerShell toocreate Data Factory entities.</span></span>

## <a name="supported-authentication-types"></a><span data-ttu-id="4e531-121">Ondersteunde verificatietypen</span><span class="sxs-lookup"><span data-stu-id="4e531-121">Supported authentication types</span></span>
<span data-ttu-id="4e531-122">U-SQL-activiteit ondersteunt hieronder verificatietypen tegen Data Lake Analytics:</span><span class="sxs-lookup"><span data-stu-id="4e531-122">U-SQL activity supports below authentication types against Data Lake Analytics:</span></span>
* <span data-ttu-id="4e531-123">Verificatie van service-principal</span><span class="sxs-lookup"><span data-stu-id="4e531-123">Service principal authentication</span></span>
* <span data-ttu-id="4e531-124">Verificatie van gebruikersreferenties (OAuth)</span><span class="sxs-lookup"><span data-stu-id="4e531-124">User credential (OAuth) authentication</span></span> 

<span data-ttu-id="4e531-125">Het is raadzaam dat u service-principal verificatie, met name voor een geplande U-SQL-uitvoering.</span><span class="sxs-lookup"><span data-stu-id="4e531-125">We recommend that you use service principal authentication, especially for a scheduled U-SQL execution.</span></span> <span data-ttu-id="4e531-126">Verlopen van het token kan gebeuren met verificatie van gebruikersreferenties.</span><span class="sxs-lookup"><span data-stu-id="4e531-126">Token expiration behavior can occur with user credential authentication.</span></span> <span data-ttu-id="4e531-127">Zie voor configuratiedetails Hallo [gekoppelde service-eigenschappen](#azure-data-lake-analytics-linked-service) sectie.</span><span class="sxs-lookup"><span data-stu-id="4e531-127">For configuration details, see hello [Linked service properties](#azure-data-lake-analytics-linked-service) section.</span></span>

## <a name="azure-data-lake-analytics-linked-service"></a><span data-ttu-id="4e531-128">Azure Data Lake Analytics gekoppelde Service</span><span class="sxs-lookup"><span data-stu-id="4e531-128">Azure Data Lake Analytics Linked Service</span></span>
<span data-ttu-id="4e531-129">U maakt een **Azure Data Lake Analytics** gekoppelde service toolink een Azure Data Lake Analytics compute-service tooan Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="4e531-129">You create an **Azure Data Lake Analytics** linked service toolink an Azure Data Lake Analytics compute service tooan Azure data factory.</span></span> <span data-ttu-id="4e531-130">Hallo Data Lake Analytics U-SQL-activiteit in de pijplijn Hallo verwijst toothis gekoppelde service.</span><span class="sxs-lookup"><span data-stu-id="4e531-130">hello Data Lake Analytics U-SQL activity in hello pipeline refers toothis linked service.</span></span> 

<span data-ttu-id="4e531-131">Hallo bevat volgende tabel beschrijvingen van Hallo generieke eigenschappen die worden gebruikt in Hallo JSON-definitie.</span><span class="sxs-lookup"><span data-stu-id="4e531-131">hello following table provides descriptions for hello generic properties used in hello JSON definition.</span></span> <span data-ttu-id="4e531-132">U kunt verder tussen service-principal en verificatie van gebruikersreferenties.</span><span class="sxs-lookup"><span data-stu-id="4e531-132">You can further choose between service principal and user credential authentication.</span></span>

| <span data-ttu-id="4e531-133">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="4e531-133">Property</span></span> | <span data-ttu-id="4e531-134">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4e531-134">Description</span></span> | <span data-ttu-id="4e531-135">Vereist</span><span class="sxs-lookup"><span data-stu-id="4e531-135">Required</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4e531-136">**type**</span><span class="sxs-lookup"><span data-stu-id="4e531-136">**type**</span></span> |<span data-ttu-id="4e531-137">Hallo type eigenschap moet worden ingesteld op: **AzureDataLakeAnalytics**.</span><span class="sxs-lookup"><span data-stu-id="4e531-137">hello type property should be set to: **AzureDataLakeAnalytics**.</span></span> |<span data-ttu-id="4e531-138">Ja</span><span class="sxs-lookup"><span data-stu-id="4e531-138">Yes</span></span> |
| <span data-ttu-id="4e531-139">**Accountnaam**</span><span class="sxs-lookup"><span data-stu-id="4e531-139">**accountName**</span></span> |<span data-ttu-id="4e531-140">Azure Data Lake Analytics-accountnaam.</span><span class="sxs-lookup"><span data-stu-id="4e531-140">Azure Data Lake Analytics Account Name.</span></span> |<span data-ttu-id="4e531-141">Ja</span><span class="sxs-lookup"><span data-stu-id="4e531-141">Yes</span></span> |
| <span data-ttu-id="4e531-142">**dataLakeAnalyticsUri**</span><span class="sxs-lookup"><span data-stu-id="4e531-142">**dataLakeAnalyticsUri**</span></span> |<span data-ttu-id="4e531-143">Azure Data Lake Analytics-URI.</span><span class="sxs-lookup"><span data-stu-id="4e531-143">Azure Data Lake Analytics URI.</span></span> |<span data-ttu-id="4e531-144">Nee</span><span class="sxs-lookup"><span data-stu-id="4e531-144">No</span></span> |
| <span data-ttu-id="4e531-145">**abonnements-id**</span><span class="sxs-lookup"><span data-stu-id="4e531-145">**subscriptionId**</span></span> |<span data-ttu-id="4e531-146">Azure-abonnement-id</span><span class="sxs-lookup"><span data-stu-id="4e531-146">Azure subscription id</span></span> |<span data-ttu-id="4e531-147">Nee (als dit niet is opgegeven, abonnement van Hallo data factory wordt gebruikt).</span><span class="sxs-lookup"><span data-stu-id="4e531-147">No (If not specified, subscription of hello data factory is used).</span></span> |
| <span data-ttu-id="4e531-148">**resourceGroupName**</span><span class="sxs-lookup"><span data-stu-id="4e531-148">**resourceGroupName**</span></span> |<span data-ttu-id="4e531-149">Naam van een Azure-resourcegroep</span><span class="sxs-lookup"><span data-stu-id="4e531-149">Azure resource group name</span></span> |<span data-ttu-id="4e531-150">Nee (als dit niet is opgegeven, brongroep van Hallo data factory wordt gebruikt).</span><span class="sxs-lookup"><span data-stu-id="4e531-150">No (If not specified, resource group of hello data factory is used).</span></span> |

### <a name="service-principal-authentication-recommended"></a><span data-ttu-id="4e531-151">Verificatie van de service principal (aanbevolen)</span><span class="sxs-lookup"><span data-stu-id="4e531-151">Service principal authentication (recommended)</span></span>
<span data-ttu-id="4e531-152">toouse service principal verificatie, de registratie een Toepassingsentiteit in Azure Active Directory (Azure AD) en verleen het Hallo toegang krijgen tot de tooData Lake Store.</span><span class="sxs-lookup"><span data-stu-id="4e531-152">toouse service principal authentication, register an application entity in Azure Active Directory (Azure AD) and grant it hello access tooData Lake Store.</span></span> <span data-ttu-id="4e531-153">Zie voor gedetailleerde stappen [authentication Service-naar-serviceconnector](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="4e531-153">For detailed steps, see [Service-to-service authentication](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span> <span data-ttu-id="4e531-154">Noteer Hallo waarden, waarin u volgende toodefine Hallo gekoppelde service:</span><span class="sxs-lookup"><span data-stu-id="4e531-154">Make note of hello following values, which you use toodefine hello linked service:</span></span>
* <span data-ttu-id="4e531-155">Toepassings-id</span><span class="sxs-lookup"><span data-stu-id="4e531-155">Application ID</span></span>
* <span data-ttu-id="4e531-156">Sleutel van toepassing</span><span class="sxs-lookup"><span data-stu-id="4e531-156">Application key</span></span> 
* <span data-ttu-id="4e531-157">Tenant-id</span><span class="sxs-lookup"><span data-stu-id="4e531-157">Tenant ID</span></span>

<span data-ttu-id="4e531-158">Verificatie van de service-principal door te geven van de volgende eigenschappen hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="4e531-158">Use service principal authentication by specifying hello following properties:</span></span>

| <span data-ttu-id="4e531-159">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="4e531-159">Property</span></span> | <span data-ttu-id="4e531-160">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4e531-160">Description</span></span> | <span data-ttu-id="4e531-161">Vereist</span><span class="sxs-lookup"><span data-stu-id="4e531-161">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="4e531-162">**servicePrincipalId**</span><span class="sxs-lookup"><span data-stu-id="4e531-162">**servicePrincipalId**</span></span> | <span data-ttu-id="4e531-163">Geef Hallo van client-id op.</span><span class="sxs-lookup"><span data-stu-id="4e531-163">Specify hello application's client ID.</span></span> | <span data-ttu-id="4e531-164">Ja</span><span class="sxs-lookup"><span data-stu-id="4e531-164">Yes</span></span> |
| <span data-ttu-id="4e531-165">**servicePrincipalKey**</span><span class="sxs-lookup"><span data-stu-id="4e531-165">**servicePrincipalKey**</span></span> | <span data-ttu-id="4e531-166">De sleutel van de toepassing hello opgeven.</span><span class="sxs-lookup"><span data-stu-id="4e531-166">Specify hello application's key.</span></span> | <span data-ttu-id="4e531-167">Ja</span><span class="sxs-lookup"><span data-stu-id="4e531-167">Yes</span></span> |
| <span data-ttu-id="4e531-168">**tenant**</span><span class="sxs-lookup"><span data-stu-id="4e531-168">**tenant**</span></span> | <span data-ttu-id="4e531-169">Geef informatie op Hallo tenant (domain name of tenant-ID) in uw toepassing zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="4e531-169">Specify hello tenant information (domain name or tenant ID) under which your application resides.</span></span> <span data-ttu-id="4e531-170">U kunt deze ophalen door zwevende Hallo muis in Hallo rechterbovenhoek Hallo Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="4e531-170">You can retrieve it by hovering hello mouse in hello upper-right corner of hello Azure portal.</span></span> | <span data-ttu-id="4e531-171">Ja</span><span class="sxs-lookup"><span data-stu-id="4e531-171">Yes</span></span> |

<span data-ttu-id="4e531-172">**Voorbeeld: Service-principal-verificatie**</span><span class="sxs-lookup"><span data-stu-id="4e531-172">**Example: Service principal authentication**</span></span>
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

### <a name="user-credential-authentication"></a><span data-ttu-id="4e531-173">Verificatie van gebruikersreferenties</span><span class="sxs-lookup"><span data-stu-id="4e531-173">User credential authentication</span></span>
<span data-ttu-id="4e531-174">Ook kunt u verificatie van gebruikersreferenties voor Data Lake Analytics door te geven Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="4e531-174">Alternatively, you can use user credential authentication for Data Lake Analytics by specifying hello following properties:</span></span>

| <span data-ttu-id="4e531-175">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="4e531-175">Property</span></span> | <span data-ttu-id="4e531-176">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4e531-176">Description</span></span> | <span data-ttu-id="4e531-177">Vereist</span><span class="sxs-lookup"><span data-stu-id="4e531-177">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="4e531-178">**autorisatie**</span><span class="sxs-lookup"><span data-stu-id="4e531-178">**authorization**</span></span> | <span data-ttu-id="4e531-179">Klik op Hallo **autoriseren** knop op Hallo Data Factory-Editor en voer uw referenties die Hallo automatisch gegenereerde autorisatie-URL toothis eigenschap toewijst.</span><span class="sxs-lookup"><span data-stu-id="4e531-179">Click hello **Authorize** button in hello Data Factory Editor and enter your credential that assigns hello autogenerated authorization URL toothis property.</span></span> | <span data-ttu-id="4e531-180">Ja</span><span class="sxs-lookup"><span data-stu-id="4e531-180">Yes</span></span> |
| <span data-ttu-id="4e531-181">**sessie-id**</span><span class="sxs-lookup"><span data-stu-id="4e531-181">**sessionId**</span></span> | <span data-ttu-id="4e531-182">OAuth-sessie-ID van Hallo OAuth-autorisatie-sessie.</span><span class="sxs-lookup"><span data-stu-id="4e531-182">OAuth session ID from hello OAuth authorization session.</span></span> <span data-ttu-id="4e531-183">Elke sessie-ID is uniek en kan slechts één keer worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4e531-183">Each session ID is unique and can be used only once.</span></span> <span data-ttu-id="4e531-184">Deze instelling wordt automatisch gegenereerd wanneer u Hallo Data Factory-Editor.</span><span class="sxs-lookup"><span data-stu-id="4e531-184">This setting is automatically generated when you use hello Data Factory Editor.</span></span> | <span data-ttu-id="4e531-185">Ja</span><span class="sxs-lookup"><span data-stu-id="4e531-185">Yes</span></span> |

<span data-ttu-id="4e531-186">**Voorbeeld: Verificatie van gebruikersreferenties**</span><span class="sxs-lookup"><span data-stu-id="4e531-186">**Example: User credential authentication**</span></span>
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>", 
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

#### <a name="token-expiration"></a><span data-ttu-id="4e531-187">Verlopen van het token</span><span class="sxs-lookup"><span data-stu-id="4e531-187">Token expiration</span></span>
<span data-ttu-id="4e531-188">Hallo autorisatiecode die u hebt gegenereerd met Hallo **autoriseren** knop verloopt na enige tijd opnieuw.</span><span class="sxs-lookup"><span data-stu-id="4e531-188">hello authorization code you generated by using hello **Authorize** button expires after sometime.</span></span> <span data-ttu-id="4e531-189">Zie de volgende tabel voor Hallo verlopen tijden voor verschillende soorten gebruikersaccounts Hallo.</span><span class="sxs-lookup"><span data-stu-id="4e531-189">See hello following table for hello expiration times for different types of user accounts.</span></span> <span data-ttu-id="4e531-190">Mogelijk ziet u Hallo volgende foutbericht weergegeven wanneer Hallo verificatie **-token verloopt**: referentie-bewerkingsfout: invalid_grant - AADSTS70002: fout bij het valideren van referenties.</span><span class="sxs-lookup"><span data-stu-id="4e531-190">You may see hello following error message when hello authentication **token expires**: Credential operation error: invalid_grant - AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="4e531-191">AADSTS70008: Hallo opgegeven toegangsmachtiging is verlopen of ingetrokken.</span><span class="sxs-lookup"><span data-stu-id="4e531-191">AADSTS70008: hello provided access grant is expired or revoked.</span></span> <span data-ttu-id="4e531-192">Traceer-ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 correlatie-ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 tijdstempel: 2015-12-15 21:09:31Z</span><span class="sxs-lookup"><span data-stu-id="4e531-192">Trace ID: d18629e8-af88-43c5-88e3-d8419eb1fca1 Correlation ID: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Timestamp: 2015-12-15 21:09:31Z</span></span>

| <span data-ttu-id="4e531-193">Gebruikerstype</span><span class="sxs-lookup"><span data-stu-id="4e531-193">User type</span></span> | <span data-ttu-id="4e531-194">Verloopt na</span><span class="sxs-lookup"><span data-stu-id="4e531-194">Expires after</span></span> |
|:--- |:--- |
| <span data-ttu-id="4e531-195">Gebruikersaccounts die niet worden beheerd door Azure Active Directory (@hotmail.com, @live.com, enz.)</span><span class="sxs-lookup"><span data-stu-id="4e531-195">User accounts NOT managed by Azure Active Directory (@hotmail.com, @live.com, etc.)</span></span> |<span data-ttu-id="4e531-196">12 uur</span><span class="sxs-lookup"><span data-stu-id="4e531-196">12 hours</span></span> |
| <span data-ttu-id="4e531-197">Gebruikersaccounts die worden beheerd door Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="4e531-197">Users accounts managed by Azure Active Directory (AAD)</span></span> |<span data-ttu-id="4e531-198">het is 14 dagen na de laatste segment Hallo worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4e531-198">14 days after hello last slice run.</span></span> <br/><br/><span data-ttu-id="4e531-199">negentig dagen weergegeven, als een segment op basis van de gekoppelde service op basis van OAuth ten minste eenmaal in de 14 dagen wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4e531-199">90 days, if a slice based on OAuth-based linked service runs at least once every 14 days.</span></span> |

<span data-ttu-id="4e531-200">tooavoid/los deze fout, opnieuw autoriseren hello met **autoriseren** wanneer hello **-token verloopt** en implementeer gekoppelde Hallo-service opnieuw.</span><span class="sxs-lookup"><span data-stu-id="4e531-200">tooavoid/resolve this error, reauthorize using hello **Authorize** button when hello **token expires** and redeploy hello linked service.</span></span> <span data-ttu-id="4e531-201">U kunt ook de waarden voor genereren **sessionId** en **autorisatie** eigenschappen programmatisch met code als volgt:</span><span class="sxs-lookup"><span data-stu-id="4e531-201">You can also generate values for **sessionId** and **authorization** properties programmatically using code as follows:</span></span>

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

<span data-ttu-id="4e531-202">Zie [AzureDataLakeStoreLinkedService klasse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService klasse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), en [AuthorizationSessionGetResponse klasse](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) onderwerpen voor meer informatie informatie over Hallo Data Factory-klassen in Hallo code gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4e531-202">See [AzureDataLakeStoreLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), and [AuthorizationSessionGetResponse Class](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) topics for details about hello Data Factory classes used in hello code.</span></span> <span data-ttu-id="4e531-203">Voeg een verwijzing naar: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll voor Hallo WindowsFormsWebAuthenticationDialog klasse.</span><span class="sxs-lookup"><span data-stu-id="4e531-203">Add a reference to: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll for hello WindowsFormsWebAuthenticationDialog class.</span></span> 

## <a name="data-lake-analytics-u-sql-activity"></a><span data-ttu-id="4e531-204">Data Lake Analytics U-SQL-activiteit</span><span class="sxs-lookup"><span data-stu-id="4e531-204">Data Lake Analytics U-SQL Activity</span></span>
<span data-ttu-id="4e531-205">Hallo volgende JSON-codefragment definieert een pijplijn met een Data Lake Analytics U-SQL-activiteit.</span><span class="sxs-lookup"><span data-stu-id="4e531-205">hello following JSON snippet defines a pipeline with a Data Lake Analytics U-SQL Activity.</span></span> <span data-ttu-id="4e531-206">Hallo activiteitsdefinitie bevat een verwijzing toohello Azure Data Lake Analytics gekoppelde service die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4e531-206">hello activity definition has a reference toohello Azure Data Lake Analytics linked service you created earlier.</span></span>   

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This is a pipeline toocompute events for en-gb locale and date less than 2012/02/19.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00Z",
        "end": "2015-08-08T01:00:00Z",
        "isPaused": false
    }
}
```

<span data-ttu-id="4e531-207">Hallo volgende tabel beschrijft namen en beschrijvingen van eigenschappen die specifiek toothis activiteit zijn.</span><span class="sxs-lookup"><span data-stu-id="4e531-207">hello following table describes names and descriptions of properties that are specific toothis activity.</span></span> 

| <span data-ttu-id="4e531-208">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="4e531-208">Property</span></span> | <span data-ttu-id="4e531-209">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4e531-209">Description</span></span> | <span data-ttu-id="4e531-210">Vereist</span><span class="sxs-lookup"><span data-stu-id="4e531-210">Required</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="4e531-211">type</span><span class="sxs-lookup"><span data-stu-id="4e531-211">type</span></span> |<span data-ttu-id="4e531-212">de eigenschap type Hello te moet worden ingesteld**DataLakeAnalyticsU SQL**.</span><span class="sxs-lookup"><span data-stu-id="4e531-212">hello type property must be set too**DataLakeAnalyticsU-SQL**.</span></span> |<span data-ttu-id="4e531-213">Ja</span><span class="sxs-lookup"><span data-stu-id="4e531-213">Yes</span></span> |
| <span data-ttu-id="4e531-214">scriptPath</span><span class="sxs-lookup"><span data-stu-id="4e531-214">scriptPath</span></span> |<span data-ttu-id="4e531-215">Pad toofolder met Hallo U-SQL-script.</span><span class="sxs-lookup"><span data-stu-id="4e531-215">Path toofolder that contains hello U-SQL script.</span></span> <span data-ttu-id="4e531-216">Naam van bestand Hallo is hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="4e531-216">Name of hello file is case-sensitive.</span></span> |<span data-ttu-id="4e531-217">Nee (als u een script gebruiken)</span><span class="sxs-lookup"><span data-stu-id="4e531-217">No (if you use script)</span></span> |
| <span data-ttu-id="4e531-218">scriptLinkedService</span><span class="sxs-lookup"><span data-stu-id="4e531-218">scriptLinkedService</span></span> |<span data-ttu-id="4e531-219">Gekoppelde service die is gekoppeld aan Hallo-opslag met Hallo script toohello data factory</span><span class="sxs-lookup"><span data-stu-id="4e531-219">Linked service that links hello storage that contains hello script toohello data factory</span></span> |<span data-ttu-id="4e531-220">Nee (als u een script gebruiken)</span><span class="sxs-lookup"><span data-stu-id="4e531-220">No (if you use script)</span></span> |
| <span data-ttu-id="4e531-221">Script</span><span class="sxs-lookup"><span data-stu-id="4e531-221">script</span></span> |<span data-ttu-id="4e531-222">Geef in plaats van het opgeven van scriptPath en scriptLinkedService inline-script.</span><span class="sxs-lookup"><span data-stu-id="4e531-222">Specify inline script instead of specifying scriptPath and scriptLinkedService.</span></span> <span data-ttu-id="4e531-223">Bijvoorbeeld: `"script": "CREATE DATABASE test"`.</span><span class="sxs-lookup"><span data-stu-id="4e531-223">For example: `"script": "CREATE DATABASE test"`.</span></span> |<span data-ttu-id="4e531-224">Nee (als u scriptPath en scriptLinkedService gebruiken)</span><span class="sxs-lookup"><span data-stu-id="4e531-224">No (if you use scriptPath and scriptLinkedService)</span></span> |
| <span data-ttu-id="4e531-225">degreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="4e531-225">degreeOfParallelism</span></span> |<span data-ttu-id="4e531-226">maximum aantal knooppunten Hallo toorun Hallo taak tegelijkertijd worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4e531-226">hello maximum number of nodes simultaneously used toorun hello job.</span></span> |<span data-ttu-id="4e531-227">Nee</span><span class="sxs-lookup"><span data-stu-id="4e531-227">No</span></span> |
| <span data-ttu-id="4e531-228">Prioriteit</span><span class="sxs-lookup"><span data-stu-id="4e531-228">priority</span></span> |<span data-ttu-id="4e531-229">Hiermee wordt bepaald welke taken uit in de wachtrij moeten geselecteerde toorun eerst.</span><span class="sxs-lookup"><span data-stu-id="4e531-229">Determines which jobs out of all that are queued should be selected toorun first.</span></span> <span data-ttu-id="4e531-230">Hallo Hallo minder, Hallo hogere Hallo prioriteit.</span><span class="sxs-lookup"><span data-stu-id="4e531-230">hello lower hello number, hello higher hello priority.</span></span> |<span data-ttu-id="4e531-231">Nee</span><span class="sxs-lookup"><span data-stu-id="4e531-231">No</span></span> |
| <span data-ttu-id="4e531-232">parameters</span><span class="sxs-lookup"><span data-stu-id="4e531-232">parameters</span></span> |<span data-ttu-id="4e531-233">Parameters voor Hallo U-SQL-script</span><span class="sxs-lookup"><span data-stu-id="4e531-233">Parameters for hello U-SQL script</span></span> |<span data-ttu-id="4e531-234">Nee</span><span class="sxs-lookup"><span data-stu-id="4e531-234">No</span></span> |
| <span data-ttu-id="4e531-235">runtimeVersion</span><span class="sxs-lookup"><span data-stu-id="4e531-235">runtimeVersion</span></span> | <span data-ttu-id="4e531-236">Runtime-versie van Hallo U-SQL-engine toouse</span><span class="sxs-lookup"><span data-stu-id="4e531-236">Runtime version of hello U-SQL engine toouse</span></span> | <span data-ttu-id="4e531-237">Nee</span><span class="sxs-lookup"><span data-stu-id="4e531-237">No</span></span> | 
| <span data-ttu-id="4e531-238">compilationMode</span><span class="sxs-lookup"><span data-stu-id="4e531-238">compilationMode</span></span> | <p><span data-ttu-id="4e531-239">Compilatiemodus van U-SQL.</span><span class="sxs-lookup"><span data-stu-id="4e531-239">Compilation mode of U-SQL.</span></span> <span data-ttu-id="4e531-240">Moet een van de volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="4e531-240">Must be one of these values:</span></span></p> <ul><li><span data-ttu-id="4e531-241">**Semantische:** alleen uitvoeren semantische controles en de benodigde bevestigingen.</span><span class="sxs-lookup"><span data-stu-id="4e531-241">**Semantic:** Only perform semantic checks and necessary sanity checks.</span></span></li><li><span data-ttu-id="4e531-242">**Volledige:** uitvoeren Hallo volledige compilatie, met inbegrip van syntaxiscontrole, optimalisatie, genereren van code, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="4e531-242">**Full:** Perform hello full compilation, including syntax check, optimization, code generation, etc.</span></span></li><li><span data-ttu-id="4e531-243">**SingleBox:** Hallo volledige compilatie, met TargetType instelling tooSingleBox uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="4e531-243">**SingleBox:** Perform hello full compilation, with TargetType setting tooSingleBox.</span></span></li></ul><p><span data-ttu-id="4e531-244">Als u een waarde voor deze eigenschap niet opgeeft, bepaalt Hallo server Hallo optimale compilatiemodus.</span><span class="sxs-lookup"><span data-stu-id="4e531-244">If you don't specify a value for this property, hello server determines hello optimal compilation mode.</span></span> </p>| <span data-ttu-id="4e531-245">Nee</span><span class="sxs-lookup"><span data-stu-id="4e531-245">No</span></span> | 

<span data-ttu-id="4e531-246">Zie [SearchLogProcessing.txt Script definitie](#sample-u-sql-script) voor Hallo script definitie.</span><span class="sxs-lookup"><span data-stu-id="4e531-246">See [SearchLogProcessing.txt Script Definition](#sample-u-sql-script) for hello script definition.</span></span> 

## <a name="sample-input-and-output-datasets"></a><span data-ttu-id="4e531-247">Voorbeeld van invoer- en uitvoergegevenssets</span><span class="sxs-lookup"><span data-stu-id="4e531-247">Sample input and output datasets</span></span>
### <a name="input-dataset"></a><span data-ttu-id="4e531-248">Invoergegevensset</span><span class="sxs-lookup"><span data-stu-id="4e531-248">Input dataset</span></span>
<span data-ttu-id="4e531-249">In dit voorbeeld is de invoergegevens Hallo bevindt zich in een Azure Data Lake Store (SearchLog.tsv-bestand in Hallo datalake/invoer map).</span><span class="sxs-lookup"><span data-stu-id="4e531-249">In this example, hello input data resides in an Azure Data Lake Store (SearchLog.tsv file in hello datalake/input folder).</span></span> 

```json
{
    "name": "DataLakeTable",
    "properties": {
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
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}    
```

### <a name="output-dataset"></a><span data-ttu-id="4e531-250">Uitvoergegevensset</span><span class="sxs-lookup"><span data-stu-id="4e531-250">Output dataset</span></span>
<span data-ttu-id="4e531-251">In dit voorbeeld wordt Hallo uitvoergegevens die wordt geproduceerd door Hallo U-SQL-script opgeslagen in een Azure Data Lake Store (datalake/uitvoermap).</span><span class="sxs-lookup"><span data-stu-id="4e531-251">In this example, hello output data produced by hello U-SQL script is stored in an Azure Data Lake Store (datalake/output folder).</span></span> 

```json
{
    "name": "EventsByRegionTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="sample-data-lake-store-linked-service"></a><span data-ttu-id="4e531-252">Sample Data Lake Store gekoppelde Service</span><span class="sxs-lookup"><span data-stu-id="4e531-252">Sample Data Lake Store Linked Service</span></span>
<span data-ttu-id="4e531-253">Hier is Hallo definitie van Hallo voorbeeld die Azure Data Lake Store service die wordt gebruikt door Hallo i gekoppelde/o-gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="4e531-253">Here is hello definition of hello sample Azure Data Lake Store linked service used by hello input/output datasets.</span></span> 

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
        }
    }
}
```

<span data-ttu-id="4e531-254">Zie [tooand gegevens verplaatsen van Azure Data Lake Store](data-factory-azure-datalake-connector.md) artikel voor een beschrijving van de JSON-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="4e531-254">See [Move data tooand from Azure Data Lake Store](data-factory-azure-datalake-connector.md) article for descriptions of JSON properties.</span></span> 

## <a name="sample-u-sql-script"></a><span data-ttu-id="4e531-255">U-SQL-voorbeeldscript</span><span class="sxs-lookup"><span data-stu-id="4e531-255">Sample U-SQL Script</span></span>

```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM @in
    USING Extractors.Tsv(nullEscape:"#NULL#");

@rs1 =
    SELECT Start, Region, Duration
    FROM @searchlog
WHERE Region == "en-gb";

@rs1 =
    SELECT Start, Region, Duration
    FROM @rs1
    WHERE Start <= DateTime.Parse("2012/02/19");

OUTPUT @rs1   
    too@out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

<span data-ttu-id="4e531-256">waarden voor Hallo  **@in**  en  **@out**  parameters in Hallo U-SQL-script worden doorgegeven dynamisch door ADF Hallo 'parameters' sectie.</span><span class="sxs-lookup"><span data-stu-id="4e531-256">hello values for **@in** and **@out** parameters in hello U-SQL script are passed dynamically by ADF using hello ‘parameters’ section.</span></span> <span data-ttu-id="4e531-257">Zie Hallo 'parameters' in hello pijplijn definitie.</span><span class="sxs-lookup"><span data-stu-id="4e531-257">See hello ‘parameters’ section in hello pipeline definition.</span></span>

<span data-ttu-id="4e531-258">U kunt ook andere eigenschappen zoals degreeOfParallelism en prioriteit opgeven in de definitie van de pijplijn voor Hallo-taken die worden uitgevoerd op Hallo Azure Data Lake Analytics-service.</span><span class="sxs-lookup"><span data-stu-id="4e531-258">You can specify other properties such as degreeOfParallelism and priority as well in your pipeline definition for hello jobs that run on hello Azure Data Lake Analytics service.</span></span>

## <a name="dynamic-parameters"></a><span data-ttu-id="4e531-259">Dynamische parameters</span><span class="sxs-lookup"><span data-stu-id="4e531-259">Dynamic parameters</span></span>
<span data-ttu-id="4e531-260">In Hallo voorbeeld pijplijn definitie zijn in en uit parameters toegewezen met vastgelegde waarden.</span><span class="sxs-lookup"><span data-stu-id="4e531-260">In hello sample pipeline definition, in and out parameters are assigned with hard-coded values.</span></span> 

```json
"parameters": {
    "in": "/datalake/input/SearchLog.tsv",
    "out": "/datalake/output/Result.tsv"
}
```

<span data-ttu-id="4e531-261">Dynamische parameters mogelijke toouse is in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="4e531-261">It is possible toouse dynamic parameters instead.</span></span> <span data-ttu-id="4e531-262">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="4e531-262">For example:</span></span> 

```json
"parameters": {
    "in": "$$Text.Format('/datalake/input/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)",
    "out": "$$Text.Format('/datalake/output/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)"
}
```

<span data-ttu-id="4e531-263">In dit geval invoerbestanden zijn nog steeds opgehaald uit Hallo /datalake/input map en uitvoerbestanden worden gegenereerd in Hallo /datalake/output map.</span><span class="sxs-lookup"><span data-stu-id="4e531-263">In this case, input files are still picked up from hello /datalake/input folder and output files are generated in hello /datalake/output folder.</span></span> <span data-ttu-id="4e531-264">Hallo-bestandsnamen zijn dynamisch, op basis van de begintijd van Hallo segment.</span><span class="sxs-lookup"><span data-stu-id="4e531-264">hello file names are dynamic based on hello slice start time.</span></span>  

