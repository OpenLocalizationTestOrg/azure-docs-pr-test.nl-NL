---
title: Aan de slag met Data Lake Analytics met REST API| Microsoft Docs
description: WebHDFS REST-API's gebruiken om bewerkingen uit te voeren in Data Lake Analytics
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 5e133d92-baaa-44c9-890c-ab2d85c91122
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/03/2017
ms.author: jgao
ms.openlocfilehash: 332d7af2539eea8890745005104ac5b0921c2b7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-rest-apis"></a><span data-ttu-id="4edd0-103">Aan de slag met Azure Data Lake Analytics met REST-API'S</span><span class="sxs-lookup"><span data-stu-id="4edd0-103">Get started with Azure Data Lake Analytics using REST APIs</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="4edd0-104">Meer informatie over hoe u WebHDFS REST API's en Data Lake Analytics REST API's gebruikt voor het beheren van Data Lake Analytics-accounts, -taken en -catalogi.</span><span class="sxs-lookup"><span data-stu-id="4edd0-104">Learn how to use WebHDFS REST APIs and Data Lake Analytics REST APIs to manage Data Lake Analytics accounts, jobs, and catalog.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="4edd0-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4edd0-105">Prerequisites</span></span>
* <span data-ttu-id="4edd0-106">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="4edd0-106">**An Azure subscription**.</span></span> <span data-ttu-id="4edd0-107">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="4edd0-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="4edd0-108">**Een Azure Active Directory-toepassing maken**.</span><span class="sxs-lookup"><span data-stu-id="4edd0-108">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="4edd0-109">U gebruikt de Azure AD-toepassing om de Data Lake Analytics-toepassing te verifiëren in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4edd0-109">You use the Azure AD application to authenticate the Data Lake Analytics application with Azure AD.</span></span> <span data-ttu-id="4edd0-110">Er zijn verschillende manieren om te verifiëren in Azure AD, zoals **verificatie door eindgebruikers** en **service-naar-serviceverificatie**.</span><span class="sxs-lookup"><span data-stu-id="4edd0-110">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="4edd0-111">Zie [Authenticate with Data Lake Analytics using Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md) (Verifiëren met Data Lake Analytics met behulp van Azure Active Directory) voor instructies en meer informatie over verificatie.</span><span class="sxs-lookup"><span data-stu-id="4edd0-111">For instructions and more information on how to authenticate, see [Authenticate with Data Lake Analytics using Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="4edd0-112">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="4edd0-112">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="4edd0-113">In dit artikel wordt cURL gebruikt om te laten zien hoe u REST API-aanroepen maakt voor een Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="4edd0-113">This article uses cURL to demonstrate how to make REST API calls against a Data Lake Analytics account.</span></span>

## <a name="authenticate-with-azure-active-directory"></a><span data-ttu-id="4edd0-114">Verifiëren bij Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4edd0-114">Authenticate with Azure Active Directory</span></span>
<span data-ttu-id="4edd0-115">Er zijn twee methoden om te verifiëren bij Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4edd0-115">There are two methods for authenticating with Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="4edd0-116">Eindgebruikersverificatie (interactief)</span><span class="sxs-lookup"><span data-stu-id="4edd0-116">End-user authentication (interactive)</span></span>
<span data-ttu-id="4edd0-117">Met deze methode wordt de gebruiker via de toepassing gevraagd om zich aan te melden. Alle bewerkingen worden uitgevoerd in de context van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="4edd0-117">Using this method, application prompts the user to log in and all the operations are performed in the context of the user.</span></span> 

<span data-ttu-id="4edd0-118">Volg deze stappen voor interactieve verificatie:</span><span class="sxs-lookup"><span data-stu-id="4edd0-118">Follow these steps for interactive authentication:</span></span>

1. <span data-ttu-id="4edd0-119">Leid de gebruiker via de toepassing om naar de volgende URL:</span><span class="sxs-lookup"><span data-stu-id="4edd0-119">Through your application, redirect the user to the following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<CLIENT-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="4edd0-120">\<REDIRECT-URI> moet zijn gecodeerd om te worden gebruikt in een URL.</span><span class="sxs-lookup"><span data-stu-id="4edd0-120">\<REDIRECT-URI> needs to be encoded for use in a URL.</span></span> <span data-ttu-id="4edd0-121">Dus https://localhost, gebruikt u `https%3A%2F%2Flocalhost`)</span><span class="sxs-lookup"><span data-stu-id="4edd0-121">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="4edd0-122">Voor deze zelfstudie kunt u de waarden van de tijdelijke aanduiding in bovenstaande URL vervangen en deze in de adresbalk van de webbrowser plakken.</span><span class="sxs-lookup"><span data-stu-id="4edd0-122">For the purpose of this tutorial, you can replace the placeholder values in the URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="4edd0-123">U wordt omgeleid om u te verifiëren met uw Azure-aanmelding.</span><span class="sxs-lookup"><span data-stu-id="4edd0-123">You will be redirected to authenticate using your Azure login.</span></span> <span data-ttu-id="4edd0-124">Wanneer u bent aangemeld, wordt het antwoord weergegeven in de adresbalk van de browser.</span><span class="sxs-lookup"><span data-stu-id="4edd0-124">Once you succesfully log in, the response is displayed in the browser's address bar.</span></span> <span data-ttu-id="4edd0-125">Het antwoord heeft de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="4edd0-125">The response will be in the following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="4edd0-126">Leg de autorisatiecode uit het antwoord vast.</span><span class="sxs-lookup"><span data-stu-id="4edd0-126">Capture the authorization code from the response.</span></span> <span data-ttu-id="4edd0-127">Voor deze zelfstudie kunt u de autorisatiecode uit de adresbalk van de webbrowser kopiëren en deze in de POST-aanvraag doorgeven aan het eindpunt van het token, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="4edd0-127">For this tutorial, you can copy the authorization code from the address bar of the web browser and pass it in the POST request to the token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<CLIENT-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="4edd0-128">In dit geval hoeft de \<REDIRECT-URI> niet te worden gecodeerd.</span><span class="sxs-lookup"><span data-stu-id="4edd0-128">In this case, the \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="4edd0-129">Het antwoord is een JSON-object dat een toegangstoken (bijvoorbeeld `"access_token": "<ACCESS_TOKEN>"`) en een vernieuwingstoken (bijvoorbeeld `"refresh_token": "<REFRESH_TOKEN>"`) bevat.</span><span class="sxs-lookup"><span data-stu-id="4edd0-129">The response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="4edd0-130">Uw toepassing gebruikt het toegangstoken om toegang te krijgen tot Azure Data Lake Store en het vernieuwingstoken om een nieuw toegangstoken op te halen wanneer het oude is verlopen.</span><span class="sxs-lookup"><span data-stu-id="4edd0-130">Your application uses the access token when accessing Azure Data Lake Store and the refresh token to get another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="4edd0-131">Wanneer het toegangstoken is verlopen, kunt u als volgt met het vernieuwingstoken een nieuw toegangstoken aanvragen:</span><span class="sxs-lookup"><span data-stu-id="4edd0-131">When the access token expires, you can request a new access token using the refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<CLIENT-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="4edd0-132">Zie [De stroom voor autorisatiecodetoekenning](https://msdn.microsoft.com/library/azure/dn645542.aspx) voor meer informatie over interactieve gebruikersverificatie.</span><span class="sxs-lookup"><span data-stu-id="4edd0-132">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="4edd0-133">Service-naar-serviceverificatie (niet interactief)</span><span class="sxs-lookup"><span data-stu-id="4edd0-133">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="4edd0-134">Met deze methode worden met de toepassing eigen referenties verstrekt om bewerkingen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="4edd0-134">Using this method, application provides its own credentials to perform the operations.</span></span> <span data-ttu-id="4edd0-135">Hiervoor moet u een POST-aanvraag uitgeven, zoals in het voorbeeld hieronder:</span><span class="sxs-lookup"><span data-stu-id="4edd0-135">For this, you must issue a POST request like the one shown below:</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="4edd0-136">De uitvoer van deze aanvraag bevat een verificatietoken (in de onderstaande uitvoer aangegeven met `access-token`) die u vervolgens gaat doorgeven met de REST-API-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="4edd0-136">The output of this request will include an authorization token (denoted by `access-token` in the output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="4edd0-137">Sla dit verificatietoken op in een tekstbestand. U hebt het verderop in dit artikel nodig.</span><span class="sxs-lookup"><span data-stu-id="4edd0-137">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="4edd0-138">In dit artikel wordt de **niet-interactieve** benadering gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4edd0-138">This article uses the **non-interactive** approach.</span></span> <span data-ttu-id="4edd0-139">Zie [Service-naar-service-aanroepen met referenties](https://msdn.microsoft.com/library/azure/dn645543.aspx) voor meer informatie over niet-interactieve (service-naar-service) aanroepen.</span><span class="sxs-lookup"><span data-stu-id="4edd0-139">For more information on non-interactive (service-to-service calls), see [Service to service calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="4edd0-140">Een Data Lake Analytics-account maken</span><span class="sxs-lookup"><span data-stu-id="4edd0-140">Create a Data Lake Analytics account</span></span>
<span data-ttu-id="4edd0-141">U moet een Azure-resourcegroep en een Data Lake Store-account maken voordat u een Data Lake Analytics-account kunt maken.</span><span class="sxs-lookup"><span data-stu-id="4edd0-141">You must create an Azure Resource group, and a Data Lake Store account before you can create a Data Lake Analytics account.</span></span>  <span data-ttu-id="4edd0-142">Zie [Een Data Lake Store-account maken](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).</span><span class="sxs-lookup"><span data-stu-id="4edd0-142">See [Create a Data Lake Store account](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).</span></span>

<span data-ttu-id="4edd0-143">De volgende cURL-opdracht laat zien hoe u een account maakt:</span><span class="sxs-lookup"><span data-stu-id="4edd0-143">The following Curl command shows how to create an account:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<NewAzureDataLakeAnalyticsAccountName>?api-version=2016-11-01 -d@"C:\tutorials\adla\CreateDataLakeAnalyticsAccountRequest.json"

<span data-ttu-id="4edd0-144">Vervang \<`REDACTED`\> door het autorisatietoken, \<`AzureSubscriptionID`\> door uw abonnements-id, \<`AzureResourceGroupName`\> door de naam van een bestaande Azure-resourcegroep en \<`NewAzureDataLakeAnalyticsAccountName`\> door de naam van een nieuw Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="4edd0-144">Replace \<`REDACTED`\> with the authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`NewAzureDataLakeAnalyticsAccountName`\> with a new Data Lake Analytics Account name.</span></span> <span data-ttu-id="4edd0-145">De nettolading van de aanvraag voor deze opdracht zit in het bestand **CreateDatalakeAnalyticsAccountRequest.json** dat is opgegeven voor de parameter `-d` hierboven.</span><span class="sxs-lookup"><span data-stu-id="4edd0-145">The request payload for this command is contained in the **CreateDatalakeAnalyticsAccountRequest.json** file that is provided for the `-d` parameter above.</span></span> <span data-ttu-id="4edd0-146">De inhoud van het bestand input.json ziet er ongeveer als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="4edd0-146">The contents of the input.json file resemble the following:</span></span>

    {  
        "location": "East US 2",  
        "name": "myadla1004",  
        "tags": {},  
        "properties": {  
            "defaultDataLakeStoreAccount": "my1004store",  
            "dataLakeStoreAccounts": [  
                {  
                    "name": "my1004store"  
                }     
            ]
        }  
    }  


## <a name="list-data-lake-analytics-accounts-in-a-subscription"></a><span data-ttu-id="4edd0-147">Data Lake Analytics-accounts vermelden in een abonnement</span><span class="sxs-lookup"><span data-stu-id="4edd0-147">List Data Lake Analytics accounts in a subscription</span></span>
<span data-ttu-id="4edd0-148">De volgende cURL-opdracht laat zien hoe u accounts vermeldt in een abonnement:</span><span class="sxs-lookup"><span data-stu-id="4edd0-148">The following Curl command shows how to list accounts in a subscription:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/providers/Microsoft.DataLakeAnalytics/Accounts?api-version=2016-11-01

<span data-ttu-id="4edd0-149">Vervang \<`REDACTED`\> door het autorisatietoken en \<`AzureSubscriptionID`\> door uw abonnements-id.</span><span class="sxs-lookup"><span data-stu-id="4edd0-149">Replace \<`REDACTED`\> with the authorization token, \<`AzureSubscriptionID`\> with your subscription ID.</span></span> <span data-ttu-id="4edd0-150">De uitvoer is vergelijkbaar met:</span><span class="sxs-lookup"><span data-stu-id="4edd0-150">The output is similar to:</span></span>

    {
        "value": [
            {
            "properties": {
                "provisioningState": "Succeeded",
                "state": "Active",
                "endpoint": "myadla0831.azuredatalakeanalytics.net",
                "accountId": "21e74660-0941-4880-ae72-b143c2615ea9",
                "creationTime": "2016-09-01T12:49:12.7451428Z",
                "lastModifiedTime": "2016-09-01T12:49:12.7451428Z"
            },
            "location": "East US 2",
            "tags": {},
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla0831rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla0831",
            "name": "myadla0831",
            "type": "Microsoft.DataLakeAnalytics/accounts"
            },
            {
            "properties": {
                "provisioningState": "Succeeded",
                "state": "Active",
                "endpoint": "myadla1004.azuredatalakeanalytics.net",
                "accountId": "3ff9b93b-11c4-43c6-83cc-276292eeb350",
                "creationTime": "2016-10-04T20:46:42.287147Z",
                "lastModifiedTime": "2016-10-04T20:46:42.287147Z"
            },
            "location": "East US 2",
            "tags": {},
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004",
            "name": "myadla1004",
            "type": "Microsoft.DataLakeAnalytics/accounts"
            }
        ]
    }

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="4edd0-151">Informatie krijgen over een Data Lake Analytics-account</span><span class="sxs-lookup"><span data-stu-id="4edd0-151">Get information about a Data Lake Analytics account</span></span>
<span data-ttu-id="4edd0-152">De volgende cURL-opdracht laat zien hoe u accountgegevens ophaalt:</span><span class="sxs-lookup"><span data-stu-id="4edd0-152">The following Curl command shows how to get an account information:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>?api-version=2015-11-01

<span data-ttu-id="4edd0-153">Vervang \<`REDACTED`\> door het autorisatietoken, \<`AzureSubscriptionID`\> door uw abonnements-id, \<`AzureResourceGroupName`\> door de naam van een bestaande Azure-resourcegroep en \<`DataLakeAnalyticsAccountName`\> door de naam van een bestaand Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="4edd0-153">Replace \<`REDACTED`\> with the authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with the name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="4edd0-154">De uitvoer is vergelijkbaar met:</span><span class="sxs-lookup"><span data-stu-id="4edd0-154">The output is similar to:</span></span>

    {
        "properties": {
            "defaultDataLakeStoreAccount": "my1004store",
            "dataLakeStoreAccounts": [
            {
                "properties": {
                "suffix": "azuredatalakestore.net"
                },
                "name": "my1004store"
            }
            ],
            "provisioningState": "Creating",
            "state": null,
            "endpoint": null,
            "accountId": "3ff9b93b-11c4-43c6-83cc-276292eeb350",
            "creationTime": null,
            "lastModifiedTime": null
        },
        "location": "East US 2",
        "tags": {},
        "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004",
        "name": "myadla1004",
        "type": "Microsoft.DataLakeAnalytics/accounts"
    }

## <a name="list-data-lake-stores-of-a-data-lake-analytics-account"></a><span data-ttu-id="4edd0-155">Data Lake Stores van een Data Lake Analytics-account vermelden</span><span class="sxs-lookup"><span data-stu-id="4edd0-155">List Data Lake Stores of a Data Lake Analytics account</span></span>
<span data-ttu-id="4edd0-156">De volgende cURL-opdracht laat zien hoe u Data Lake Stores van een account vermeldt:</span><span class="sxs-lookup"><span data-stu-id="4edd0-156">The following Curl command shows how to list Data Lake Stores of an account:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>/DataLakeStoreAccounts/?api-version=2016-11-01

<span data-ttu-id="4edd0-157">Vervang \<`REDACTED`\> door het autorisatietoken, \<`AzureSubscriptionID`\> door uw abonnements-id, \<`AzureResourceGroupName`\> door de naam van een bestaande Azure-resourcegroep en \<`DataLakeAnalyticsAccountName`\> door de naam van een bestaand Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="4edd0-157">Replace \<`REDACTED`\> with the authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with the name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="4edd0-158">De uitvoer is vergelijkbaar met:</span><span class="sxs-lookup"><span data-stu-id="4edd0-158">The output is similar to:</span></span>

    {
        "value": [
            {
            "properties": {
                "suffix": "azuredatalakestore.net"
            },
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004/dataLakeStoreAccounts/my1004store",
            "name": "my1004store",
            "type": "Microsoft.DataLakeAnalytics/accounts/dataLakeStoreAccounts"
            }
        ]
    }

## <a name="submit-u-sql-jobs"></a><span data-ttu-id="4edd0-159">U-SQL-taken verzenden</span><span class="sxs-lookup"><span data-stu-id="4edd0-159">Submit U-SQL jobs</span></span>
<span data-ttu-id="4edd0-160">De volgende cURL-opdracht laat zien hoe u een U-SQL-taak verzendt:</span><span class="sxs-lookup"><span data-stu-id="4edd0-160">The following Curl command shows how to submit a U-SQL job:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs/<NewGUID>?api-version=2016-03-20-preview -d@"C:\tutorials\adla\SubmitADLAJob.json"

<span data-ttu-id="4edd0-161">Vervang \<`REDACTED`\> door het autorisatietoken en \<`DataLakeAnalyticsAccountName`\> door de naam van een bestaand Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="4edd0-161">Replace \<`REDACTED`\> with the authorization token, \<`DataLakeAnalyticsAccountName`\> with the name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="4edd0-162">De nettolading van de aanvraag voor deze opdracht zit in het bestand **SubmitADLAJob.json** dat is opgegeven voor de parameter `-d` hierboven.</span><span class="sxs-lookup"><span data-stu-id="4edd0-162">The request payload for this command is contained in the **SubmitADLAJob.json** file that is provided for the `-d` parameter above.</span></span> <span data-ttu-id="4edd0-163">De inhoud van het bestand input.json ziet er ongeveer als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="4edd0-163">The contents of the input.json file resemble the following:</span></span>

    {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "degreeOfParallelism": 1,
        "priority": 1000,
        "properties": {
            "type": "USql",
            "script": "@searchlog =\n    EXTRACT UserId          int,\n            Start           DateTime,\n            Region          string,\n            Query          
        string,\n            Duration        int?,\n            Urls            string,\n            ClickedUrls     string\n    FROM \"/Samples/Data/SearchLog.tsv\"\n    US
        ING Extractors.Tsv();\n\nOUTPUT @searchlog   \n    TO \"/Output/SearchLog-from-Data-Lake.csv\"\nUSING Outputters.Csv();"
        }
    }

<span data-ttu-id="4edd0-164">De uitvoer is vergelijkbaar met:</span><span class="sxs-lookup"><span data-stu-id="4edd0-164">The output is similar to:</span></span>

    {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "myadl@SPI",
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "2016-10-05T13:54:59.9871859+00:00",
        "state": "Compiling",
        "result": "Succeeded",
        "stateAuditRecords": [
            {
            "newState": "New",
            "timeStamp": "2016-10-05T13:54:59.9871859+00:00",
            "details": "userName:myadl@SPI;submitMachine:N/A"
            }
        ],
        "properties": {
            "owner": "myadl@SPI",
            "resources": [],
            "runtimeVersion": "default",
            "rootProcessNodeId": "00000000-0000-0000-0000-000000000000",
            "algebraFilePath": "adl://myadls0831.azuredatalakestore.net/system/jobservice/jobs/Usql/2016/10/05/13/54/8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a/algebra.xml",
            "compileMode": "Semantic",
            "errorSource": "Unknown",
            "totalCompilationTime": "PT0S",
            "totalPausedTime": "PT0S",
            "totalQueuedTime": "PT0S",
            "totalRunningTime": "PT0S",
            "type": "USql"
        }
    }


## <a name="list-u-sql-jobs"></a><span data-ttu-id="4edd0-165">U-SQL-taken vermelden</span><span class="sxs-lookup"><span data-stu-id="4edd0-165">List U-SQL jobs</span></span>
<span data-ttu-id="4edd0-166">De volgende cURL-opdracht laat zien hoe u U-SQL-taken vermeldt:</span><span class="sxs-lookup"><span data-stu-id="4edd0-166">The following Curl command shows how to list U-SQL jobs:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs?api-version=2016-11-01 

<span data-ttu-id="4edd0-167">Vervang \<`REDACTED`\> door het autorisatietoken en \<`DataLakeAnalyticsAccountName`\> door de naam van een bestaand Data Lake Analytics-account.</span><span class="sxs-lookup"><span data-stu-id="4edd0-167">Replace \<`REDACTED`\> with the authorization token, and \<`DataLakeAnalyticsAccountName`\> with the name of an existing Data Lake Analytics Account.</span></span> 

<span data-ttu-id="4edd0-168">De uitvoer is vergelijkbaar met:</span><span class="sxs-lookup"><span data-stu-id="4edd0-168">The output is similar to:</span></span>

    {
    "value": [
        {
        "jobId": "65cf1691-9dbe-43cd-90ed-1cafbfb406fb",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "someone@microsoft.com",
        "account": null,
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "Wed, 05 Oct 2016 13:46:53 GMT",
        "startTime": "Wed, 05 Oct 2016 13:47:33 GMT",
        "endTime": "Wed, 05 Oct 2016 13:48:07 GMT",
        "state": "Ended",
        "result": "Succeeded",
        "errorMessage": null,
        "storageAccounts": null,
        "stateAuditRecords": null,
        "logFilePatterns": null,
        "properties": null
        },
        {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "someoneadl@SPI",
        "account": null,
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "Wed, 05 Oct 2016 13:54:59 GMT",
        "startTime": "Wed, 05 Oct 2016 13:55:43 GMT",
        "endTime": "Wed, 05 Oct 2016 13:56:11 GMT",
        "state": "Ended",
        "result": "Succeeded",
        "errorMessage": null,
        "storageAccounts": null,
        "stateAuditRecords": null,
        "logFilePatterns": null,
        "properties": null
        }
    ],
    "nextLink": null,
    "count": null
    }


## <a name="get-catalog-items"></a><span data-ttu-id="4edd0-169">Catalogusitems ophalen</span><span class="sxs-lookup"><span data-stu-id="4edd0-169">Get catalog items</span></span>
<span data-ttu-id="4edd0-170">De volgende cURL-opdracht laat zien hoe u de databases ophaalt uit de catalogus:</span><span class="sxs-lookup"><span data-stu-id="4edd0-170">The following Curl command shows how to get the databases from the catalog:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/catalog/usql/databases?api-version=2016-11-01

<span data-ttu-id="4edd0-171">De uitvoer is vergelijkbaar met:</span><span class="sxs-lookup"><span data-stu-id="4edd0-171">The output is similar to:</span></span>

    {
    "@odata.context":"https://myadla0831.azuredatalakeanalytics.net/sqlip/$metadata#databases","value":[
        {
        "computeAccountName":"myadla0831","databaseName":"mytest","version":"f6956327-90b8-4648-ad8b-de3ff09274ea"
        },{
        "computeAccountName":"myadla0831","databaseName":"master","version":"e8bca908-cc73-41a3-9564-e9bcfaa21f4e"
        }
    ]
    }

## <a name="see-also"></a><span data-ttu-id="4edd0-172">Zie ook</span><span class="sxs-lookup"><span data-stu-id="4edd0-172">See also</span></span>
* <span data-ttu-id="4edd0-173">Zie [Websitelogboeken analyseren met Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md) voor een complexere query.</span><span class="sxs-lookup"><span data-stu-id="4edd0-173">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="4edd0-174">Zie [U-SQL-scripts ontwikkelen met Data Lake Tools voor Visual Studio](data-lake-analytics-data-lake-tools-get-started.md) om aan de slag te gaan met het ontwikkelen van U-SQL-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="4edd0-174">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="4edd0-175">Zie [Aan de slag met de Azure Data Lake Analytics U-SQL-taal](data-lake-analytics-u-sql-get-started.md) om U-SQL te leren.</span><span class="sxs-lookup"><span data-stu-id="4edd0-175">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="4edd0-176">Zie [Azure Data Lake Analytics beheren met Azure Portal](data-lake-analytics-manage-use-portal.md) voor informatie over beheertaken.</span><span class="sxs-lookup"><span data-stu-id="4edd0-176">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="4edd0-177">Zie [Overzicht van Azure Data Lake Analytics](data-lake-analytics-overview.md) voor een overzicht van Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="4edd0-177">To get an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>
* <span data-ttu-id="4edd0-178">Als u dezelfde zelfstudie wilt bekijken met een ander hulpprogramma, klikt u op de tabselectors boven aan de pagina.</span><span class="sxs-lookup"><span data-stu-id="4edd0-178">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span></span>

