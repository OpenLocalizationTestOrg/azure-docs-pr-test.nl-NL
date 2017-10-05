---
title: Aan de slag met Azure Data Lake Store met de REST-API | Microsoft Docs
description: WebHDFS REST-API's gebruiken om bewerkingen uit te voeren in Data Lake Store
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 57ac6501-cb71-4f75-82c2-acc07c562889
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: dc2c8f58e0a2faf1b00f4903148328a5141a8637
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-rest-apis"></a><span data-ttu-id="12972-103">Aan de slag met Azure Data Lake Store met REST-API's</span><span class="sxs-lookup"><span data-stu-id="12972-103">Get started with Azure Data Lake Store using REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="12972-104">Portal</span><span class="sxs-lookup"><span data-stu-id="12972-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="12972-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="12972-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="12972-106">.NET-SDK</span><span class="sxs-lookup"><span data-stu-id="12972-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="12972-107">Java-SDK</span><span class="sxs-lookup"><span data-stu-id="12972-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="12972-108">REST API</span><span class="sxs-lookup"><span data-stu-id="12972-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="12972-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="12972-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="12972-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="12972-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="12972-111">Python</span><span class="sxs-lookup"><span data-stu-id="12972-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="12972-112">In dit artikel leest u hoe u WebHDFS REST-API's en Data Lake Store REST-API's gebruikt voor accountbeheer en om bestandssysteembewerkingen uit te voeren in Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="12972-112">In this article, you will learn how to use WebHDFS REST APIs and Data Lake Store REST APIs to perform account management as well as filesystem operations on Azure Data Lake Store.</span></span> <span data-ttu-id="12972-113">Azure Data Lake Store beschikt over eigen REST-API's voor accountbeheerbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="12972-113">Azure Data Lake Store exposes its own REST APIs for account management operations.</span></span> <span data-ttu-id="12972-114">Omdat Data Lake Store echter compatibel is met het HDFS- en Hadoop-ecosysteem, wordt ook het gebruik van WebHDFS REST-API's voor bestandssysteembewerkingen ondersteund.</span><span class="sxs-lookup"><span data-stu-id="12972-114">However, because Data Lake Store is compatible with HDFS and Hadoop ecosystem, it supports using WebHDFS REST APIs for filesystem operations.</span></span>

> [!NOTE]
> <span data-ttu-id="12972-115">Raadpleeg de [Naslaginformatie over REST API's van Azure Data Lake Store](https://msdn.microsoft.com/library/mt693424.aspx) voor gedetailleerde informatie over de REST-API-ondersteuning van Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="12972-115">For detailed information on the REST API support for Data Lake Store, see [Azure Data Lake Store REST API Reference](https://msdn.microsoft.com/library/mt693424.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="12972-116">Vereisten</span><span class="sxs-lookup"><span data-stu-id="12972-116">Prerequisites</span></span>
* <span data-ttu-id="12972-117">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="12972-117">**An Azure subscription**.</span></span> <span data-ttu-id="12972-118">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="12972-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="12972-119">**Een Azure Active Directory-toepassing maken**.</span><span class="sxs-lookup"><span data-stu-id="12972-119">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="12972-120">U gebruikt de Azure AD-toepassing om de Data Lake Store-toepassing te verifiëren in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="12972-120">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="12972-121">Er zijn verschillende manieren om te verifiëren in Azure AD, zoals **verificatie door eindgebruikers** en **service-naar-serviceverificatie**.</span><span class="sxs-lookup"><span data-stu-id="12972-121">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="12972-122">Zie [Eindgebruikersverificatie](data-lake-store-end-user-authenticate-using-active-directory.md) of [Service-to-serviceverificatie](data-lake-store-authenticate-using-active-directory.md) voor instructies en meer informatie over verificatie.</span><span class="sxs-lookup"><span data-stu-id="12972-122">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="12972-123">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="12972-123">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="12972-124">In dit artikel wordt cURL gebruikt om te laten zien hoe u REST API-aanroepen maakt voor een Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="12972-124">This article uses cURL to demonstrate how to make REST API calls against a Data Lake Store account.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="12972-125">Hoe verifieer ik met Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="12972-125">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="12972-126">Er zijn twee benaderingen voor verificatie met Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="12972-126">You can use two approaches to authenticate using Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="12972-127">Eindgebruikersverificatie (interactief)</span><span class="sxs-lookup"><span data-stu-id="12972-127">End-user authentication (interactive)</span></span>
<span data-ttu-id="12972-128">In dit scenario wordt de gebruiker via de toepassing gevraagd om zich te melden en worden alle bewerkingen uitgevoerd in de context van de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="12972-128">In this scenario, the application prompts the user to log in and all the operations are performed in the context of the user.</span></span> <span data-ttu-id="12972-129">Voer de volgende stappen uit voor interactieve verificatie.</span><span class="sxs-lookup"><span data-stu-id="12972-129">Perform the following steps for interactive authentication.</span></span>

1. <span data-ttu-id="12972-130">Leid de gebruiker via de toepassing om naar de volgende URL:</span><span class="sxs-lookup"><span data-stu-id="12972-130">Through your application, redirect the user to the following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<APPLICATION-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="12972-131">\<REDIRECT-URI> moet zijn gecodeerd om te worden gebruikt in een URL.</span><span class="sxs-lookup"><span data-stu-id="12972-131">\<REDIRECT-URI> needs to be encoded for use in a URL.</span></span> <span data-ttu-id="12972-132">Dus https://localhost, gebruikt u `https%3A%2F%2Flocalhost`)</span><span class="sxs-lookup"><span data-stu-id="12972-132">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="12972-133">Voor deze zelfstudie kunt u de waarden van de tijdelijke aanduiding in bovenstaande URL vervangen en deze in de adresbalk van de webbrowser plakken.</span><span class="sxs-lookup"><span data-stu-id="12972-133">For the purpose of this tutorial, you can replace the placeholder values in the URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="12972-134">U wordt omgeleid om u te verifiëren met uw Azure-aanmelding.</span><span class="sxs-lookup"><span data-stu-id="12972-134">You will be redirected to authenticate using your Azure login.</span></span> <span data-ttu-id="12972-135">Wanneer u bent aangemeld, wordt het antwoord weergegeven in de adresbalk van de browser.</span><span class="sxs-lookup"><span data-stu-id="12972-135">Once you successfully log in, the response is displayed in the browser's address bar.</span></span> <span data-ttu-id="12972-136">Het antwoord heeft de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="12972-136">The response will be in the following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="12972-137">Leg de autorisatiecode uit het antwoord vast.</span><span class="sxs-lookup"><span data-stu-id="12972-137">Capture the authorization code from the response.</span></span> <span data-ttu-id="12972-138">Voor deze zelfstudie kunt u de autorisatiecode uit de adresbalk van de webbrowser kopiëren en deze in de POST-aanvraag doorgeven aan het eindpunt van het token, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="12972-138">For this tutorial, you can copy the authorization code from the address bar of the web browser and pass it in the POST request to the token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<APPLICATION-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="12972-139">In dit geval hoeft de \<REDIRECT-URI> niet te worden gecodeerd.</span><span class="sxs-lookup"><span data-stu-id="12972-139">In this case, the \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="12972-140">Het antwoord is een JSON-object dat een toegangstoken (bijvoorbeeld `"access_token": "<ACCESS_TOKEN>"`) en een vernieuwingstoken (bijvoorbeeld `"refresh_token": "<REFRESH_TOKEN>"`) bevat.</span><span class="sxs-lookup"><span data-stu-id="12972-140">The response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="12972-141">Uw toepassing gebruikt het toegangstoken om toegang te krijgen tot Azure Data Lake Store en het vernieuwingstoken om een nieuw toegangstoken op te halen wanneer het oude is verlopen.</span><span class="sxs-lookup"><span data-stu-id="12972-141">Your application uses the access token when accessing Azure Data Lake Store and the refresh token to get another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="12972-142">Wanneer het toegangstoken is verlopen, kunt u als volgt met het vernieuwingstoken een nieuw toegangstoken aanvragen:</span><span class="sxs-lookup"><span data-stu-id="12972-142">When the access token expires, you can request a new access token using the refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<APPLICATION-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="12972-143">Zie [De stroom voor autorisatiecodetoekenning](https://msdn.microsoft.com/library/azure/dn645542.aspx) voor meer informatie over interactieve gebruikersverificatie.</span><span class="sxs-lookup"><span data-stu-id="12972-143">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="12972-144">Service-naar-serviceverificatie (niet interactief)</span><span class="sxs-lookup"><span data-stu-id="12972-144">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="12972-145">In dit scenario verstrekt de toepassing zijn eigen referenties om bewerkingen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="12972-145">In this scenario, the the application provides its own credentials to perform the operations.</span></span> <span data-ttu-id="12972-146">Daarvoor moet u een POST-aanvraag uitgeven, zoals in het voorbeeld hieronder.</span><span class="sxs-lookup"><span data-stu-id="12972-146">For this, you must issue a POST request like the one shown below.</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="12972-147">De uitvoer van deze aanvraag bevat een verificatietoken (in de onderstaande uitvoer aangegeven met `access-token`) die u vervolgens gaat doorgeven met de REST-API-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="12972-147">The output of this request will include an authorization token (denoted by `access-token` in the output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="12972-148">Sla dit verificatietoken op in een tekstbestand. U hebt het verderop in dit artikel nodig.</span><span class="sxs-lookup"><span data-stu-id="12972-148">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="12972-149">In dit artikel wordt de **niet-interactieve** benadering gebruikt.</span><span class="sxs-lookup"><span data-stu-id="12972-149">This article uses the **non-interactive** approach.</span></span> <span data-ttu-id="12972-150">Zie [Service-naar-service-aanroepen met referenties](https://msdn.microsoft.com/library/azure/dn645543.aspx) voor meer informatie over niet-interactieve (service-naar-service) aanroepen.</span><span class="sxs-lookup"><span data-stu-id="12972-150">For more information on non-interactive (service-to-service calls), see [Service to service calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="12972-151">Een Data Lake Store-account maken</span><span class="sxs-lookup"><span data-stu-id="12972-151">Create a Data Lake Store account</span></span>
<span data-ttu-id="12972-152">Deze bewerking is gebaseerd op de REST-API-aanroep die [hier](https://msdn.microsoft.com/library/mt694078.aspx) wordt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="12972-152">This operation is based on the REST API call defined [here](https://msdn.microsoft.com/library/mt694078.aspx).</span></span>

<span data-ttu-id="12972-153">Gebruik de volgende cURL-opdracht:</span><span class="sxs-lookup"><span data-stu-id="12972-153">Use the following cURL command.</span></span> <span data-ttu-id="12972-154">Vervang **\<yourstorename>** door de naam van uw Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="12972-154">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview -d@"C:\temp\input.json"

<span data-ttu-id="12972-155">Vervang \<`REDACTED`\> in de bovenstaande opdracht door het verificatietoken dat u eerder hebt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="12972-155">In the above command, replace \<`REDACTED`\> with the authorization token you retrieved earlier.</span></span> <span data-ttu-id="12972-156">De nettolading van de aanvraag voor deze opdracht zit in het bestand **input.json** dat is opgegeven voor de parameter `-d` hierboven.</span><span class="sxs-lookup"><span data-stu-id="12972-156">The request payload for this command is contained in the **input.json** file that is provided for the `-d` parameter above.</span></span> <span data-ttu-id="12972-157">De inhoud van het bestand input.json ziet er ongeveer als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="12972-157">The contents of the input.json file resemble the following:</span></span>

    {
    "location": "eastus2",
    "tags": {
        "department": "finance"
        },
    "properties": {}
    }    

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="12972-158">Mappen maken in een Data Lake Store-account</span><span class="sxs-lookup"><span data-stu-id="12972-158">Create folders in a Data Lake Store account</span></span>
<span data-ttu-id="12972-159">Deze bewerking is gebaseerd op de WebHDFS REST-API-aanroep die [hier](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory) wordt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="12972-159">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).</span></span>

<span data-ttu-id="12972-160">Gebruik de volgende cURL-opdracht:</span><span class="sxs-lookup"><span data-stu-id="12972-160">Use the following cURL command.</span></span> <span data-ttu-id="12972-161">Vervang **\<yourstorename>** door de naam van uw Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="12972-161">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/?op=MKDIRS'

<span data-ttu-id="12972-162">Vervang \<`REDACTED`\> in de bovenstaande opdracht door het verificatietoken dat u eerder hebt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="12972-162">In the above command, replace \<`REDACTED`\> with the authorization token you retrieved earlier.</span></span> <span data-ttu-id="12972-163">Met deze opdracht maakt u een map **mytempdir** onder de hoofdmap van uw Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="12972-163">This command creates a directory called **mytempdir** under the root folder of your Data Lake Store account.</span></span>

<span data-ttu-id="12972-164">Als de bewerking is geslaagd, wordt een antwoord van de volgende strekking weergegeven:</span><span class="sxs-lookup"><span data-stu-id="12972-164">You should see a response like this if the operation completes successfully:</span></span>

    {"boolean":true}

## <a name="list-folders-in-a-data-lake-store-account"></a><span data-ttu-id="12972-165">Mappen weergeven in Data Lake Store-account</span><span class="sxs-lookup"><span data-stu-id="12972-165">List folders in a Data Lake Store account</span></span>
<span data-ttu-id="12972-166">Deze bewerking is gebaseerd op de WebHDFS REST-API-aanroep die [hier](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory) wordt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="12972-166">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).</span></span>

<span data-ttu-id="12972-167">Gebruik de volgende cURL-opdracht:</span><span class="sxs-lookup"><span data-stu-id="12972-167">Use the following cURL command.</span></span> <span data-ttu-id="12972-168">Vervang **\<yourstorename>** door de naam van uw Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="12972-168">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/?op=LISTSTATUS'

<span data-ttu-id="12972-169">Vervang \<`REDACTED`\> in de bovenstaande opdracht door het verificatietoken dat u eerder hebt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="12972-169">In the above command, replace \<`REDACTED`\> with the authorization token you retrieved earlier.</span></span>

<span data-ttu-id="12972-170">Als de bewerking is geslaagd, wordt een antwoord van de volgende strekking weergegeven:</span><span class="sxs-lookup"><span data-stu-id="12972-170">You should see a response like this if the operation completes successfully:</span></span>

    {
    "FileStatuses": {
        "FileStatus": [{
            "length": 0,
            "pathSuffix": "mytempdir",
            "type": "DIRECTORY",
            "blockSize": 268435456,
            "accessTime": 1458324719512,
            "modificationTime": 1458324719512,
            "replication": 0,
            "permission": "777",
            "owner": "NotSupportYet",
            "group": "NotSupportYet"
        }]
    }
    }

## <a name="upload-data-into-a-data-lake-store-account"></a><span data-ttu-id="12972-171">Gegevens uploaden naar een Data Lake Store-account</span><span class="sxs-lookup"><span data-stu-id="12972-171">Upload data into a Data Lake Store account</span></span>
<span data-ttu-id="12972-172">Deze bewerking is gebaseerd op de WebHDFS REST-API-aanroep die [hier](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File) wordt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="12972-172">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).</span></span>

<span data-ttu-id="12972-173">Gebruik de volgende cURL-opdracht:</span><span class="sxs-lookup"><span data-stu-id="12972-173">Use the following cURL command.</span></span> <span data-ttu-id="12972-174">Vervang **\<yourstorename>** door de naam van uw Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="12972-174">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -L -T 'C:\temp\list.txt' -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE'

<span data-ttu-id="12972-175">In de bovenstaande syntaxis geeft de parameter **-T** de locatie aan van het bestand dat u uploadt.</span><span class="sxs-lookup"><span data-stu-id="12972-175">In the above syntax **-T** parameter is the location of the file you are uploading.</span></span>

<span data-ttu-id="12972-176">De uitvoer lijkt op het volgende:</span><span class="sxs-lookup"><span data-stu-id="12972-176">The output is similar to the following:</span></span>
   
    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE&write=true
    ...
    Content-Length: 0

    HTTP/1.1 100 Continue

    HTTP/1.1 201 Created
    ...

## <a name="read-data-from-a-data-lake-store-account"></a><span data-ttu-id="12972-177">Gegevens lezen uit een Data Lake Store-account</span><span class="sxs-lookup"><span data-stu-id="12972-177">Read data from a Data Lake Store account</span></span>
<span data-ttu-id="12972-178">Deze bewerking is gebaseerd op de WebHDFS REST-API-aanroep die [hier](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File) wordt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="12972-178">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).</span></span>

<span data-ttu-id="12972-179">Het lezen van gegevens uit een Data Lake Store is een proces dat uit twee stappen bestaat.</span><span class="sxs-lookup"><span data-stu-id="12972-179">Reading data from a Data Lake Store account is a two-step process.</span></span>

* <span data-ttu-id="12972-180">Eerst dient u een GET-aanvraag in voor het eindpunt `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span><span class="sxs-lookup"><span data-stu-id="12972-180">You first submit a GET request against the endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span></span> <span data-ttu-id="12972-181">Deze retourneert een locatie waarnaar u de volgende GET-aanvraag moet verzenden.</span><span class="sxs-lookup"><span data-stu-id="12972-181">This will return a location to submit the next GET request to.</span></span>
* <span data-ttu-id="12972-182">Vervolgens dient u de GET-aanvraag in voor het eindpunt `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span><span class="sxs-lookup"><span data-stu-id="12972-182">You then submit the GET request against the endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span></span> <span data-ttu-id="12972-183">Hiermee wordt de inhoud van het bestand weergegeven.</span><span class="sxs-lookup"><span data-stu-id="12972-183">This will display the contents of the file.</span></span>

<span data-ttu-id="12972-184">Omdat de invoerparameters in de eerste en tweede stap echter gelijk zijn, kunt u de parameter `-L` gebruiken om de eerste aanvraag in te dienen.</span><span class="sxs-lookup"><span data-stu-id="12972-184">However, because there is no difference in the input parameters between the first and the second step, you can use the `-L` parameter to submit the first request.</span></span> <span data-ttu-id="12972-185">`-L` combineert in feite twee aanvragen in één en zorgt ervoor dat cURL de aanvraag opnieuw uitvoert op de nieuwe locatie.</span><span class="sxs-lookup"><span data-stu-id="12972-185">`-L` option essentially combines two requests into one and will make cURL redo the request on the new location.</span></span> <span data-ttu-id="12972-186">Ten slotte wordt de uitvoer van alle aanroepen van de aanvraag weergegeven, zoals u hieronder kunt zien.</span><span class="sxs-lookup"><span data-stu-id="12972-186">Finally, the output from all the request calls is displayed, like shown below.</span></span> <span data-ttu-id="12972-187">Vervang **\<yourstorename>** door de naam van uw Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="12972-187">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -L GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN'

<span data-ttu-id="12972-188">Als het goed is, wordt ongeveer de volgende uitvoer weergegeven:</span><span class="sxs-lookup"><span data-stu-id="12972-188">You should see an output similar to the following:</span></span>

    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/somerandomfile.txt?op=OPEN&read=true
    ...

    HTTP/1.1 200 OK
    ...

    Hello, Data Lake Store user!

## <a name="rename-a-file-in-a-data-lake-store-account"></a><span data-ttu-id="12972-189">Bestandsnamen wijzigen in een Data Lake Store-account</span><span class="sxs-lookup"><span data-stu-id="12972-189">Rename a file in a Data Lake Store account</span></span>
<span data-ttu-id="12972-190">Deze bewerking is gebaseerd op de WebHDFS REST-API-aanroep die [hier](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory) wordt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="12972-190">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).</span></span>

<span data-ttu-id="12972-191">Als u de naam van een bestand wil wijzigen, gebruikt u de volgende cURL-opdracht.</span><span class="sxs-lookup"><span data-stu-id="12972-191">Use the following cURL command to rename a file.</span></span> <span data-ttu-id="12972-192">Vervang **\<yourstorename>** door de naam van uw Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="12972-192">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=RENAME&destination=/mytempdir/myinputfile1.txt'

<span data-ttu-id="12972-193">Als het goed is, wordt ongeveer de volgende uitvoer weergegeven:</span><span class="sxs-lookup"><span data-stu-id="12972-193">You should see an output similar to the following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-file-from-a-data-lake-store-account"></a><span data-ttu-id="12972-194">Een bestand verwijderen uit een Data Lake Store-account</span><span class="sxs-lookup"><span data-stu-id="12972-194">Delete a file from a Data Lake Store account</span></span>
<span data-ttu-id="12972-195">Deze bewerking is gebaseerd op de WebHDFS REST-API-aanroep die [hier](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory) wordt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="12972-195">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).</span></span>

<span data-ttu-id="12972-196">Gebruik de volgende cURL-opdracht als u een bestand wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="12972-196">Use the following cURL command to delete a file.</span></span> <span data-ttu-id="12972-197">Vervang **\<yourstorename>** door de naam van uw Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="12972-197">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile1.txt?op=DELETE'

<span data-ttu-id="12972-198">Als het goed is, wordt ongeveer de volgende uitvoer weergegeven:</span><span class="sxs-lookup"><span data-stu-id="12972-198">You should see an output like the following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="12972-199">Een Data Lake Store-account verwijderen</span><span class="sxs-lookup"><span data-stu-id="12972-199">Delete a Data Lake Store account</span></span>
<span data-ttu-id="12972-200">Deze bewerking is gebaseerd op de REST-API-aanroep die [hier](https://msdn.microsoft.com/library/mt694075.aspx) wordt gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="12972-200">This operation is based on the REST API call defined [here](https://msdn.microsoft.com/library/mt694075.aspx).</span></span>

<span data-ttu-id="12972-201">Gebruik de volgende cURL-opdracht als u een Data Lake Store-account wilt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="12972-201">Use the following cURL command to delete a Data Lake Store account.</span></span> <span data-ttu-id="12972-202">Vervang **\<yourstorename>** door de naam van uw Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="12972-202">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview

<span data-ttu-id="12972-203">Als het goed is, wordt ongeveer de volgende uitvoer weergegeven:</span><span class="sxs-lookup"><span data-stu-id="12972-203">You should see an output like the following:</span></span>

    HTTP/1.1 200 OK
    ...
    ...

## <a name="see-also"></a><span data-ttu-id="12972-204">Zie ook</span><span class="sxs-lookup"><span data-stu-id="12972-204">See also</span></span>
* [<span data-ttu-id="12972-205">Open Source Big Data-toepassingen die compatibel zijn met Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="12972-205">Open Source Big Data applications compatible with Azure Data Lake Store</span></span>](data-lake-store-compatible-oss-other-applications.md)

