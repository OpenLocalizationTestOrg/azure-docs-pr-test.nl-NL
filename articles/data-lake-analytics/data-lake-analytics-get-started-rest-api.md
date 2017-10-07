---
title: aaaGet de slag met Data Lake Analytics met REST-API | Microsoft Docs
description: WebHDFS REST-API's tooperform bewerkingen op Data Lake Analytics gebruiken
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
ms.openlocfilehash: a0b13d521821fd2d74716cc52485585feb7c51b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-rest-apis"></a><span data-ttu-id="0eef9-103">Aan de slag met Azure Data Lake Analytics met REST-API'S</span><span class="sxs-lookup"><span data-stu-id="0eef9-103">Get started with Azure Data Lake Analytics using REST APIs</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="0eef9-104">Ontdek hoe toouse WebHDFS REST-API's en Data Lake Analytics REST-API's toomanage Data Lake Analytics-accounts, taken en -catalogus.</span><span class="sxs-lookup"><span data-stu-id="0eef9-104">Learn how toouse WebHDFS REST APIs and Data Lake Analytics REST APIs toomanage Data Lake Analytics accounts, jobs, and catalog.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0eef9-105">Vereisten</span><span class="sxs-lookup"><span data-stu-id="0eef9-105">Prerequisites</span></span>
* <span data-ttu-id="0eef9-106">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="0eef9-106">**An Azure subscription**.</span></span> <span data-ttu-id="0eef9-107">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0eef9-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="0eef9-108">**Een Azure Active Directory-toepassing maken**.</span><span class="sxs-lookup"><span data-stu-id="0eef9-108">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="0eef9-109">U hello Azure AD-toepassing tooauthenticate Hallo Data Lake Analytics-toepassing gebruiken met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0eef9-109">You use hello Azure AD application tooauthenticate hello Data Lake Analytics application with Azure AD.</span></span> <span data-ttu-id="0eef9-110">Er zijn verschillende benaderingen tooauthenticate met Azure AD zijn **eindgebruiker verificatie** of **authentication service-naar-serviceconnector**.</span><span class="sxs-lookup"><span data-stu-id="0eef9-110">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="0eef9-111">Voor instructies en meer informatie over het tooauthenticate, Zie [verifiëren met Data Lake Analytics met Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="0eef9-111">For instructions and more information on how tooauthenticate, see [Authenticate with Data Lake Analytics using Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="0eef9-112">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="0eef9-112">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="0eef9-113">Dit artikel wordt cURL toodemonstrate hoe toomake REST-API tegen een Data Lake Analytics-account aanroept.</span><span class="sxs-lookup"><span data-stu-id="0eef9-113">This article uses cURL toodemonstrate how toomake REST API calls against a Data Lake Analytics account.</span></span>

## <a name="authenticate-with-azure-active-directory"></a><span data-ttu-id="0eef9-114">Verifiëren bij Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0eef9-114">Authenticate with Azure Active Directory</span></span>
<span data-ttu-id="0eef9-115">Er zijn twee methoden om te verifiëren bij Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0eef9-115">There are two methods for authenticating with Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="0eef9-116">Eindgebruikersverificatie (interactief)</span><span class="sxs-lookup"><span data-stu-id="0eef9-116">End-user authentication (interactive)</span></span>
<span data-ttu-id="0eef9-117">Met deze methode wordt gevraagd of Hallo gebruiker toolog in en alle Hallo-bewerkingen worden uitgevoerd in de context van de gebruiker Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="0eef9-117">Using this method, application prompts hello user toolog in and all hello operations are performed in hello context of hello user.</span></span> 

<span data-ttu-id="0eef9-118">Volg deze stappen voor interactieve verificatie:</span><span class="sxs-lookup"><span data-stu-id="0eef9-118">Follow these steps for interactive authentication:</span></span>

1. <span data-ttu-id="0eef9-119">Omleiden via de toepassing hello gebruiker toohello volgende URL:</span><span class="sxs-lookup"><span data-stu-id="0eef9-119">Through your application, redirect hello user toohello following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<CLIENT-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="0eef9-120">\<OMLEIDINGS-URI > moet toobe gecodeerd voor gebruik in een URL.</span><span class="sxs-lookup"><span data-stu-id="0eef9-120">\<REDIRECT-URI> needs toobe encoded for use in a URL.</span></span> <span data-ttu-id="0eef9-121">Dus https://localhost, gebruikt u `https%3A%2F%2Flocalhost`)</span><span class="sxs-lookup"><span data-stu-id="0eef9-121">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="0eef9-122">U kunt voor doel van deze zelfstudie Hallo Hallo tijdelijke aanduiding voor waarden in Hallo bovenstaande URL vervangen en plak deze in de adresbalk van de webbrowser.</span><span class="sxs-lookup"><span data-stu-id="0eef9-122">For hello purpose of this tutorial, you can replace hello placeholder values in hello URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="0eef9-123">U zult omgeleid tooauthenticate met behulp van uw Azure-aanmelding.</span><span class="sxs-lookup"><span data-stu-id="0eef9-123">You will be redirected tooauthenticate using your Azure login.</span></span> <span data-ttu-id="0eef9-124">Nadat u bent aangemeld, wordt in de adresbalk van de browser Hallo antwoord Hallo weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0eef9-124">Once you succesfully log in, hello response is displayed in hello browser's address bar.</span></span> <span data-ttu-id="0eef9-125">antwoord Hallo niet in de volgende indeling Hallo:</span><span class="sxs-lookup"><span data-stu-id="0eef9-125">hello response will be in hello following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="0eef9-126">Hallo autorisatiecode uit antwoord Hallo vastleggen.</span><span class="sxs-lookup"><span data-stu-id="0eef9-126">Capture hello authorization code from hello response.</span></span> <span data-ttu-id="0eef9-127">U kunt voor deze zelfstudie Hallo autorisatiecode uit de adresbalk Hallo van Hallo webbrowser kopiëren en doorgeven in Hallo POST-aanvraag toohello token eindpunt, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="0eef9-127">For this tutorial, you can copy hello authorization code from hello address bar of hello web browser and pass it in hello POST request toohello token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<CLIENT-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="0eef9-128">In dit geval Hallo \<OMLEIDINGS-URI > niet te worden gecodeerd.</span><span class="sxs-lookup"><span data-stu-id="0eef9-128">In this case, hello \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="0eef9-129">Hallo-antwoord is een JSON-object dat een toegangstoken bevat (bijvoorbeeld `"access_token": "<ACCESS_TOKEN>"`) en een vernieuwingstoken (bijvoorbeeld `"refresh_token": "<REFRESH_TOKEN>"`).</span><span class="sxs-lookup"><span data-stu-id="0eef9-129">hello response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="0eef9-130">Uw toepassing gebruikt Hallo toegangstoken tijdens toegang tot Azure Data Lake Store en Hallo vernieuwen token tooget een andere toegangstoken wanneer een toegangstoken is verlopen.</span><span class="sxs-lookup"><span data-stu-id="0eef9-130">Your application uses hello access token when accessing Azure Data Lake Store and hello refresh token tooget another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="0eef9-131">Wanneer Hallo toegangstoken is verlopen, kunt u een nieuw toegangstoken met behulp van het vernieuwingstoken hello, zoals hieronder wordt weergegeven aanvragen:</span><span class="sxs-lookup"><span data-stu-id="0eef9-131">When hello access token expires, you can request a new access token using hello refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<CLIENT-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="0eef9-132">Zie [De stroom voor autorisatiecodetoekenning](https://msdn.microsoft.com/library/azure/dn645542.aspx) voor meer informatie over interactieve gebruikersverificatie.</span><span class="sxs-lookup"><span data-stu-id="0eef9-132">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="0eef9-133">Service-naar-serviceverificatie (niet interactief)</span><span class="sxs-lookup"><span data-stu-id="0eef9-133">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="0eef9-134">Met deze methode toepassing zijn eigen referenties verstrekt tooperform Hallo bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="0eef9-134">Using this method, application provides its own credentials tooperform hello operations.</span></span> <span data-ttu-id="0eef9-135">Hiervoor moet u een POST-aanvraag, zoals hieronder wordt weergeven Hallo uitgeven:</span><span class="sxs-lookup"><span data-stu-id="0eef9-135">For this, you must issue a POST request like hello one shown below:</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="0eef9-136">Hallo-uitvoer van deze aanvraag bevat een verificatietoken (aangeduid met `access-token` in onderstaande Hallo-uitvoer) die u vervolgens gaat doorgeven met de REST-API-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="0eef9-136">hello output of this request will include an authorization token (denoted by `access-token` in hello output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="0eef9-137">Sla dit verificatietoken op in een tekstbestand. U hebt het verderop in dit artikel nodig.</span><span class="sxs-lookup"><span data-stu-id="0eef9-137">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="0eef9-138">Dit artikel wordt Hallo **niet-interactieve** benadering.</span><span class="sxs-lookup"><span data-stu-id="0eef9-138">This article uses hello **non-interactive** approach.</span></span> <span data-ttu-id="0eef9-139">Zie voor meer informatie over niet-interactieve (service-naar-service) aanroepen [tooservice aanroepen met referenties Service](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span><span class="sxs-lookup"><span data-stu-id="0eef9-139">For more information on non-interactive (service-to-service calls), see [Service tooservice calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="0eef9-140">Een Data Lake Analytics-account maken</span><span class="sxs-lookup"><span data-stu-id="0eef9-140">Create a Data Lake Analytics account</span></span>
<span data-ttu-id="0eef9-141">U moet een Azure-resourcegroep en een Data Lake Store-account maken voordat u een Data Lake Analytics-account kunt maken.</span><span class="sxs-lookup"><span data-stu-id="0eef9-141">You must create an Azure Resource group, and a Data Lake Store account before you can create a Data Lake Analytics account.</span></span>  <span data-ttu-id="0eef9-142">Zie [Een Data Lake Store-account maken](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).</span><span class="sxs-lookup"><span data-stu-id="0eef9-142">See [Create a Data Lake Store account](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).</span></span>

<span data-ttu-id="0eef9-143">Hallo volgende Curl-opdracht toont hoe toocreate een account:</span><span class="sxs-lookup"><span data-stu-id="0eef9-143">hello following Curl command shows how toocreate an account:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<NewAzureDataLakeAnalyticsAccountName>?api-version=2016-11-01 -d@"C:\tutorials\adla\CreateDataLakeAnalyticsAccountRequest.json"

<span data-ttu-id="0eef9-144">Vervang \< `REDACTED` \> door het verificatietoken hello, \< `AzureSubscriptionID` \> met uw abonnements-ID \< `AzureResourceGroupName` \> met een bestaande Azure-Resource Groepsnaam, en \< `NewAzureDataLakeAnalyticsAccountName` \> met een nieuwe naam voor de Data Lake Analytics-Account.</span><span class="sxs-lookup"><span data-stu-id="0eef9-144">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`NewAzureDataLakeAnalyticsAccountName`\> with a new Data Lake Analytics Account name.</span></span> <span data-ttu-id="0eef9-145">Hallo aanvraag nettolading voor deze opdracht zit in Hallo **CreateDatalakeAnalyticsAccountRequest.json** -bestand dat is opgegeven voor het Hallo `-d` parameter hierboven.</span><span class="sxs-lookup"><span data-stu-id="0eef9-145">hello request payload for this command is contained in hello **CreateDatalakeAnalyticsAccountRequest.json** file that is provided for hello `-d` parameter above.</span></span> <span data-ttu-id="0eef9-146">Hallo-inhoud van Hallo input.json bestand lijken Hallo volgende op:</span><span class="sxs-lookup"><span data-stu-id="0eef9-146">hello contents of hello input.json file resemble hello following:</span></span>

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


## <a name="list-data-lake-analytics-accounts-in-a-subscription"></a><span data-ttu-id="0eef9-147">Data Lake Analytics-accounts vermelden in een abonnement</span><span class="sxs-lookup"><span data-stu-id="0eef9-147">List Data Lake Analytics accounts in a subscription</span></span>
<span data-ttu-id="0eef9-148">Hallo volgende Curl-opdracht ziet u hoe toolist accounts in een abonnement:</span><span class="sxs-lookup"><span data-stu-id="0eef9-148">hello following Curl command shows how toolist accounts in a subscription:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/providers/Microsoft.DataLakeAnalytics/Accounts?api-version=2016-11-01

<span data-ttu-id="0eef9-149">Vervang \< `REDACTED` \> door het verificatietoken hello, \< `AzureSubscriptionID` \> met uw abonnement-ID.</span><span class="sxs-lookup"><span data-stu-id="0eef9-149">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID.</span></span> <span data-ttu-id="0eef9-150">Hallo-uitvoer is vergelijkbaar met:</span><span class="sxs-lookup"><span data-stu-id="0eef9-150">hello output is similar to:</span></span>

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

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="0eef9-151">Informatie krijgen over een Data Lake Analytics-account</span><span class="sxs-lookup"><span data-stu-id="0eef9-151">Get information about a Data Lake Analytics account</span></span>
<span data-ttu-id="0eef9-152">Hallo volgende Curl-opdracht toont hoe de gegevens van een account tooget:</span><span class="sxs-lookup"><span data-stu-id="0eef9-152">hello following Curl command shows how tooget an account information:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>?api-version=2015-11-01

<span data-ttu-id="0eef9-153">Vervang \< `REDACTED` \> door het verificatietoken hello, \< `AzureSubscriptionID` \> met uw abonnements-ID \< `AzureResourceGroupName` \> met een bestaande Azure-Resource Groepsnaam, en \< `DataLakeAnalyticsAccountName` \> met Hallo-naam van een bestaande Data Lake Analytics-Account.</span><span class="sxs-lookup"><span data-stu-id="0eef9-153">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="0eef9-154">Hallo-uitvoer is vergelijkbaar met:</span><span class="sxs-lookup"><span data-stu-id="0eef9-154">hello output is similar to:</span></span>

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

## <a name="list-data-lake-stores-of-a-data-lake-analytics-account"></a><span data-ttu-id="0eef9-155">Data Lake Stores van een Data Lake Analytics-account vermelden</span><span class="sxs-lookup"><span data-stu-id="0eef9-155">List Data Lake Stores of a Data Lake Analytics account</span></span>
<span data-ttu-id="0eef9-156">Hallo volgende Curl-opdracht ziet u hoe toolist Data Lake opslaat van een account:</span><span class="sxs-lookup"><span data-stu-id="0eef9-156">hello following Curl command shows how toolist Data Lake Stores of an account:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>/DataLakeStoreAccounts/?api-version=2016-11-01

<span data-ttu-id="0eef9-157">Vervang \< `REDACTED` \> door het verificatietoken hello, \< `AzureSubscriptionID` \> met uw abonnements-ID \< `AzureResourceGroupName` \> met een bestaande Azure-Resource Groepsnaam, en \< `DataLakeAnalyticsAccountName` \> met Hallo-naam van een bestaande Data Lake Analytics-Account.</span><span class="sxs-lookup"><span data-stu-id="0eef9-157">Replace \<`REDACTED`\> with hello authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="0eef9-158">Hallo-uitvoer is vergelijkbaar met:</span><span class="sxs-lookup"><span data-stu-id="0eef9-158">hello output is similar to:</span></span>

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

## <a name="submit-u-sql-jobs"></a><span data-ttu-id="0eef9-159">U-SQL-taken verzenden</span><span class="sxs-lookup"><span data-stu-id="0eef9-159">Submit U-SQL jobs</span></span>
<span data-ttu-id="0eef9-160">Hallo volgende Curl-opdracht toont hoe toosubmit een U-SQL-taak:</span><span class="sxs-lookup"><span data-stu-id="0eef9-160">hello following Curl command shows how toosubmit a U-SQL job:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs/<NewGUID>?api-version=2016-03-20-preview -d@"C:\tutorials\adla\SubmitADLAJob.json"

<span data-ttu-id="0eef9-161">Vervang \< `REDACTED` \> door het verificatietoken hello, \< `DataLakeAnalyticsAccountName` \> met Hallo-naam van een bestaande Data Lake Analytics-Account.</span><span class="sxs-lookup"><span data-stu-id="0eef9-161">Replace \<`REDACTED`\> with hello authorization token, \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="0eef9-162">Hallo aanvraag nettolading voor deze opdracht zit in Hallo **SubmitADLAJob.json** -bestand dat is opgegeven voor het Hallo `-d` parameter hierboven.</span><span class="sxs-lookup"><span data-stu-id="0eef9-162">hello request payload for this command is contained in hello **SubmitADLAJob.json** file that is provided for hello `-d` parameter above.</span></span> <span data-ttu-id="0eef9-163">Hallo-inhoud van Hallo input.json bestand lijken Hallo volgende op:</span><span class="sxs-lookup"><span data-stu-id="0eef9-163">hello contents of hello input.json file resemble hello following:</span></span>

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
        ING Extractors.Tsv();\n\nOUTPUT @searchlog   \n    too\"/Output/SearchLog-from-Data-Lake.csv\"\nUSING Outputters.Csv();"
        }
    }

<span data-ttu-id="0eef9-164">Hallo-uitvoer is vergelijkbaar met:</span><span class="sxs-lookup"><span data-stu-id="0eef9-164">hello output is similar to:</span></span>

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


## <a name="list-u-sql-jobs"></a><span data-ttu-id="0eef9-165">U-SQL-taken vermelden</span><span class="sxs-lookup"><span data-stu-id="0eef9-165">List U-SQL jobs</span></span>
<span data-ttu-id="0eef9-166">Hallo volgende Curl-opdracht toont hoe U-SQL toolist taken:</span><span class="sxs-lookup"><span data-stu-id="0eef9-166">hello following Curl command shows how toolist U-SQL jobs:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs?api-version=2016-11-01 

<span data-ttu-id="0eef9-167">Vervang \< `REDACTED` \> door het verificatietoken hello, en \< `DataLakeAnalyticsAccountName` \> met Hallo-naam van een bestaande Data Lake Analytics-Account.</span><span class="sxs-lookup"><span data-stu-id="0eef9-167">Replace \<`REDACTED`\> with hello authorization token, and \<`DataLakeAnalyticsAccountName`\> with hello name of an existing Data Lake Analytics Account.</span></span> 

<span data-ttu-id="0eef9-168">Hallo-uitvoer is vergelijkbaar met:</span><span class="sxs-lookup"><span data-stu-id="0eef9-168">hello output is similar to:</span></span>

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


## <a name="get-catalog-items"></a><span data-ttu-id="0eef9-169">Catalogusitems ophalen</span><span class="sxs-lookup"><span data-stu-id="0eef9-169">Get catalog items</span></span>
<span data-ttu-id="0eef9-170">Hallo volgende Curl-opdracht ziet u hoe tooget Hallo databases van catalogus Hallo:</span><span class="sxs-lookup"><span data-stu-id="0eef9-170">hello following Curl command shows how tooget hello databases from hello catalog:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/catalog/usql/databases?api-version=2016-11-01

<span data-ttu-id="0eef9-171">Hallo-uitvoer is vergelijkbaar met:</span><span class="sxs-lookup"><span data-stu-id="0eef9-171">hello output is similar to:</span></span>

    {
    "@odata.context":"https://myadla0831.azuredatalakeanalytics.net/sqlip/$metadata#databases","value":[
        {
        "computeAccountName":"myadla0831","databaseName":"mytest","version":"f6956327-90b8-4648-ad8b-de3ff09274ea"
        },{
        "computeAccountName":"myadla0831","databaseName":"master","version":"e8bca908-cc73-41a3-9564-e9bcfaa21f4e"
        }
    ]
    }

## <a name="see-also"></a><span data-ttu-id="0eef9-172">Zie ook</span><span class="sxs-lookup"><span data-stu-id="0eef9-172">See also</span></span>
* <span data-ttu-id="0eef9-173">Zie voor een complexere query toosee [websitelogboeken analyseren met Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="0eef9-173">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="0eef9-174">tooget gestart met het ontwikkelen van U-SQL-toepassingen, Zie [U-SQL-scripts ontwikkelen met Data Lake Tools voor Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0eef9-174">tooget started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="0eef9-175">toolearn U-SQL, Zie [aan de slag met Azure Data Lake Analytics U-SQL-taal](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0eef9-175">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="0eef9-176">Zie [Azure Data Lake Analytics beheren met Azure Portal](data-lake-analytics-manage-use-portal.md) voor informatie over beheertaken.</span><span class="sxs-lookup"><span data-stu-id="0eef9-176">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="0eef9-177">Zie tooget een overzicht van Data Lake Analytics [overzicht van Azure Data Lake Analytics](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0eef9-177">tooget an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>
* <span data-ttu-id="0eef9-178">toosee Hallo dezelfde zelfstudie met een ander hulpprogramma, klikt u op Hallo-tabselectors op Hallo Hallo pagina bovenaan.</span><span class="sxs-lookup"><span data-stu-id="0eef9-178">toosee hello same tutorial using other tools, click hello tab selectors on hello top of hello page.</span></span>

