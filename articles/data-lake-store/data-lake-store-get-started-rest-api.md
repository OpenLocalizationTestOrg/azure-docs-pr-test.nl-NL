---
title: aaaUse hello REST-API tooget gestart met Data Lake Store | Microsoft Docs
description: Gebruik van WebHDFS REST-API's tooperform bewerkingen op Data Lake Store
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
ms.openlocfilehash: 62fce8293dfee730a61f2a3d37fc138ce7c3afdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-rest-apis"></a><span data-ttu-id="ec642-103">Aan de slag met Azure Data Lake Store met REST-API's</span><span class="sxs-lookup"><span data-stu-id="ec642-103">Get started with Azure Data Lake Store using REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ec642-104">Portal</span><span class="sxs-lookup"><span data-stu-id="ec642-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="ec642-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ec642-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="ec642-106">.NET-SDK</span><span class="sxs-lookup"><span data-stu-id="ec642-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="ec642-107">Java-SDK</span><span class="sxs-lookup"><span data-stu-id="ec642-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="ec642-108">REST API</span><span class="sxs-lookup"><span data-stu-id="ec642-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="ec642-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ec642-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="ec642-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="ec642-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="ec642-111">Python</span><span class="sxs-lookup"><span data-stu-id="ec642-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="ec642-112">In dit artikel leert u hoe toouse WebHDFS REST-API's en Data Lake Store REST-API's tooperform administratief beheer, evenals Bestandssysteembewerkingen op Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ec642-112">In this article, you will learn how toouse WebHDFS REST APIs and Data Lake Store REST APIs tooperform account management as well as filesystem operations on Azure Data Lake Store.</span></span> <span data-ttu-id="ec642-113">Azure Data Lake Store beschikt over eigen REST-API's voor accountbeheerbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="ec642-113">Azure Data Lake Store exposes its own REST APIs for account management operations.</span></span> <span data-ttu-id="ec642-114">Omdat Data Lake Store echter compatibel is met het HDFS- en Hadoop-ecosysteem, wordt ook het gebruik van WebHDFS REST-API's voor bestandssysteembewerkingen ondersteund.</span><span class="sxs-lookup"><span data-stu-id="ec642-114">However, because Data Lake Store is compatible with HDFS and Hadoop ecosystem, it supports using WebHDFS REST APIs for filesystem operations.</span></span>

> [!NOTE]
> <span data-ttu-id="ec642-115">Zie voor gedetailleerde informatie over Hallo REST-API-ondersteuning voor Data Lake Store [Azure Data Lake Store REST API Reference](https://msdn.microsoft.com/library/mt693424.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec642-115">For detailed information on hello REST API support for Data Lake Store, see [Azure Data Lake Store REST API Reference](https://msdn.microsoft.com/library/mt693424.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="ec642-116">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ec642-116">Prerequisites</span></span>
* <span data-ttu-id="ec642-117">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="ec642-117">**An Azure subscription**.</span></span> <span data-ttu-id="ec642-118">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ec642-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ec642-119">**Een Azure Active Directory-toepassing maken**.</span><span class="sxs-lookup"><span data-stu-id="ec642-119">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="ec642-120">U hello Azure AD-toepassing tooauthenticate Hallo Data Lake Store-toepassing gebruiken met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ec642-120">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="ec642-121">Er zijn verschillende benaderingen tooauthenticate met Azure AD zijn **eindgebruiker verificatie** of **authentication service-naar-serviceconnector**.</span><span class="sxs-lookup"><span data-stu-id="ec642-121">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="ec642-122">Voor instructies en meer informatie over het tooauthenticate, Zie [eindgebruiker verificatie](data-lake-store-end-user-authenticate-using-active-directory.md) of [authentication Service-naar-serviceconnector](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="ec642-122">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="ec642-123">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="ec642-123">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="ec642-124">Dit artikel wordt cURL toodemonstrate hoe toomake REST-API tegen een Data Lake Store-account aanroept.</span><span class="sxs-lookup"><span data-stu-id="ec642-124">This article uses cURL toodemonstrate how toomake REST API calls against a Data Lake Store account.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="ec642-125">Hoe verifieer ik met Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="ec642-125">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="ec642-126">U kunt twee benaderingen tooauthenticate met Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ec642-126">You can use two approaches tooauthenticate using Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="ec642-127">Eindgebruikersverificatie (interactief)</span><span class="sxs-lookup"><span data-stu-id="ec642-127">End-user authentication (interactive)</span></span>
<span data-ttu-id="ec642-128">In dit scenario Hallo toepassing hello gebruiker toolog in wordt gevraagd en alle Hallo-bewerkingen worden uitgevoerd in de context van de gebruiker Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="ec642-128">In this scenario, hello application prompts hello user toolog in and all hello operations are performed in hello context of hello user.</span></span> <span data-ttu-id="ec642-129">Hallo volgende stappen uit voor interactieve verificatie uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ec642-129">Perform hello following steps for interactive authentication.</span></span>

1. <span data-ttu-id="ec642-130">Omleiden via de toepassing hello gebruiker toohello volgende URL:</span><span class="sxs-lookup"><span data-stu-id="ec642-130">Through your application, redirect hello user toohello following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<APPLICATION-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="ec642-131">\<OMLEIDINGS-URI > moet toobe gecodeerd voor gebruik in een URL.</span><span class="sxs-lookup"><span data-stu-id="ec642-131">\<REDIRECT-URI> needs toobe encoded for use in a URL.</span></span> <span data-ttu-id="ec642-132">Dus https://localhost, gebruikt u `https%3A%2F%2Flocalhost`)</span><span class="sxs-lookup"><span data-stu-id="ec642-132">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="ec642-133">U kunt voor doel van deze zelfstudie Hallo Hallo tijdelijke aanduiding voor waarden in Hallo bovenstaande URL vervangen en plak deze in de adresbalk van de webbrowser.</span><span class="sxs-lookup"><span data-stu-id="ec642-133">For hello purpose of this tutorial, you can replace hello placeholder values in hello URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="ec642-134">U zult omgeleid tooauthenticate met behulp van uw Azure-aanmelding.</span><span class="sxs-lookup"><span data-stu-id="ec642-134">You will be redirected tooauthenticate using your Azure login.</span></span> <span data-ttu-id="ec642-135">Zodra u aanmelden, wordt in de adresbalk van de browser Hallo antwoord Hallo weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ec642-135">Once you successfully log in, hello response is displayed in hello browser's address bar.</span></span> <span data-ttu-id="ec642-136">antwoord Hallo niet in de volgende indeling Hallo:</span><span class="sxs-lookup"><span data-stu-id="ec642-136">hello response will be in hello following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="ec642-137">Hallo autorisatiecode uit antwoord Hallo vastleggen.</span><span class="sxs-lookup"><span data-stu-id="ec642-137">Capture hello authorization code from hello response.</span></span> <span data-ttu-id="ec642-138">U kunt voor deze zelfstudie Hallo autorisatiecode uit de adresbalk Hallo van Hallo webbrowser kopiëren en doorgeven in Hallo POST-aanvraag toohello token eindpunt, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="ec642-138">For this tutorial, you can copy hello authorization code from hello address bar of hello web browser and pass it in hello POST request toohello token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<APPLICATION-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="ec642-139">In dit geval Hallo \<OMLEIDINGS-URI > niet te worden gecodeerd.</span><span class="sxs-lookup"><span data-stu-id="ec642-139">In this case, hello \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="ec642-140">Hallo-antwoord is een JSON-object dat een toegangstoken bevat (bijvoorbeeld `"access_token": "<ACCESS_TOKEN>"`) en een vernieuwingstoken (bijvoorbeeld `"refresh_token": "<REFRESH_TOKEN>"`).</span><span class="sxs-lookup"><span data-stu-id="ec642-140">hello response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="ec642-141">Uw toepassing gebruikt Hallo toegangstoken tijdens toegang tot Azure Data Lake Store en Hallo vernieuwen token tooget een andere toegangstoken wanneer een toegangstoken is verlopen.</span><span class="sxs-lookup"><span data-stu-id="ec642-141">Your application uses hello access token when accessing Azure Data Lake Store and hello refresh token tooget another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="ec642-142">Wanneer Hallo toegangstoken is verlopen, kunt u een nieuw toegangstoken met behulp van het vernieuwingstoken hello, zoals hieronder wordt weergegeven aanvragen:</span><span class="sxs-lookup"><span data-stu-id="ec642-142">When hello access token expires, you can request a new access token using hello refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<APPLICATION-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="ec642-143">Zie [De stroom voor autorisatiecodetoekenning](https://msdn.microsoft.com/library/azure/dn645542.aspx) voor meer informatie over interactieve gebruikersverificatie.</span><span class="sxs-lookup"><span data-stu-id="ec642-143">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="ec642-144">Service-naar-serviceverificatie (niet interactief)</span><span class="sxs-lookup"><span data-stu-id="ec642-144">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="ec642-145">In dit scenario Hallo Hallo toepassing zijn eigen referenties verstrekt tooperform Hallo bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="ec642-145">In this scenario, hello hello application provides its own credentials tooperform hello operations.</span></span> <span data-ttu-id="ec642-146">Hiervoor moet u een POST-aanvraag, zoals hieronder wordt weergeven Hallo uitgeven.</span><span class="sxs-lookup"><span data-stu-id="ec642-146">For this, you must issue a POST request like hello one shown below.</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="ec642-147">Hallo-uitvoer van deze aanvraag bevat een verificatietoken (aangeduid met `access-token` in onderstaande Hallo-uitvoer) die u vervolgens gaat doorgeven met de REST-API-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="ec642-147">hello output of this request will include an authorization token (denoted by `access-token` in hello output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="ec642-148">Sla dit verificatietoken op in een tekstbestand. U hebt het verderop in dit artikel nodig.</span><span class="sxs-lookup"><span data-stu-id="ec642-148">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="ec642-149">Dit artikel wordt Hallo **niet-interactieve** benadering.</span><span class="sxs-lookup"><span data-stu-id="ec642-149">This article uses hello **non-interactive** approach.</span></span> <span data-ttu-id="ec642-150">Zie voor meer informatie over niet-interactieve (service-naar-service) aanroepen [tooservice aanroepen met referenties Service](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec642-150">For more information on non-interactive (service-to-service calls), see [Service tooservice calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="ec642-151">Een Data Lake Store-account maken</span><span class="sxs-lookup"><span data-stu-id="ec642-151">Create a Data Lake Store account</span></span>
<span data-ttu-id="ec642-152">Deze bewerking is gebaseerd op Hallo REST-API-aanroep gedefinieerd [hier](https://msdn.microsoft.com/library/mt694078.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec642-152">This operation is based on hello REST API call defined [here](https://msdn.microsoft.com/library/mt694078.aspx).</span></span>

<span data-ttu-id="ec642-153">Hallo volgende cURL-opdracht gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ec642-153">Use hello following cURL command.</span></span> <span data-ttu-id="ec642-154">Vervang **\<yourstorename>** door de naam van uw Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ec642-154">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview -d@"C:\temp\input.json"

<span data-ttu-id="ec642-155">Vervang in Hallo hierboven opdracht \< `REDACTED` \> door het verificatietoken Hallo u eerder hebt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="ec642-155">In hello above command, replace \<`REDACTED`\> with hello authorization token you retrieved earlier.</span></span> <span data-ttu-id="ec642-156">Hallo aanvraag nettolading voor deze opdracht zit in Hallo **input.json** -bestand dat is opgegeven voor het Hallo `-d` parameter hierboven.</span><span class="sxs-lookup"><span data-stu-id="ec642-156">hello request payload for this command is contained in hello **input.json** file that is provided for hello `-d` parameter above.</span></span> <span data-ttu-id="ec642-157">Hallo-inhoud van Hallo input.json bestand lijken Hallo volgende op:</span><span class="sxs-lookup"><span data-stu-id="ec642-157">hello contents of hello input.json file resemble hello following:</span></span>

    {
    "location": "eastus2",
    "tags": {
        "department": "finance"
        },
    "properties": {}
    }    

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="ec642-158">Mappen maken in een Data Lake Store-account</span><span class="sxs-lookup"><span data-stu-id="ec642-158">Create folders in a Data Lake Store account</span></span>
<span data-ttu-id="ec642-159">Deze bewerking is gebaseerd op Hallo WebHDFS REST-API-aanroep gedefinieerd [hier](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).</span><span class="sxs-lookup"><span data-stu-id="ec642-159">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).</span></span>

<span data-ttu-id="ec642-160">Hallo volgende cURL-opdracht gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ec642-160">Use hello following cURL command.</span></span> <span data-ttu-id="ec642-161">Vervang **\<yourstorename>** door de naam van uw Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ec642-161">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/?op=MKDIRS'

<span data-ttu-id="ec642-162">Vervang in Hallo hierboven opdracht \< `REDACTED` \> door het verificatietoken Hallo u eerder hebt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="ec642-162">In hello above command, replace \<`REDACTED`\> with hello authorization token you retrieved earlier.</span></span> <span data-ttu-id="ec642-163">Met deze opdracht maakt u een map **mytempdir** onder de hoofdmap Hallo van uw Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="ec642-163">This command creates a directory called **mytempdir** under hello root folder of your Data Lake Store account.</span></span>

<span data-ttu-id="ec642-164">Als Hallo-bewerking voltooid is, moet u een antwoord als volgt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="ec642-164">You should see a response like this if hello operation completes successfully:</span></span>

    {"boolean":true}

## <a name="list-folders-in-a-data-lake-store-account"></a><span data-ttu-id="ec642-165">Mappen weergeven in Data Lake Store-account</span><span class="sxs-lookup"><span data-stu-id="ec642-165">List folders in a Data Lake Store account</span></span>
<span data-ttu-id="ec642-166">Deze bewerking is gebaseerd op Hallo WebHDFS REST-API-aanroep gedefinieerd [hier](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).</span><span class="sxs-lookup"><span data-stu-id="ec642-166">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).</span></span>

<span data-ttu-id="ec642-167">Hallo volgende cURL-opdracht gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ec642-167">Use hello following cURL command.</span></span> <span data-ttu-id="ec642-168">Vervang **\<yourstorename>** door de naam van uw Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ec642-168">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/?op=LISTSTATUS'

<span data-ttu-id="ec642-169">Vervang in Hallo hierboven opdracht \< `REDACTED` \> door het verificatietoken Hallo u eerder hebt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="ec642-169">In hello above command, replace \<`REDACTED`\> with hello authorization token you retrieved earlier.</span></span>

<span data-ttu-id="ec642-170">Als Hallo-bewerking voltooid is, moet u een antwoord als volgt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="ec642-170">You should see a response like this if hello operation completes successfully:</span></span>

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

## <a name="upload-data-into-a-data-lake-store-account"></a><span data-ttu-id="ec642-171">Gegevens uploaden naar een Data Lake Store-account</span><span class="sxs-lookup"><span data-stu-id="ec642-171">Upload data into a Data Lake Store account</span></span>
<span data-ttu-id="ec642-172">Deze bewerking is gebaseerd op Hallo WebHDFS REST-API-aanroep gedefinieerd [hier](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).</span><span class="sxs-lookup"><span data-stu-id="ec642-172">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).</span></span>

<span data-ttu-id="ec642-173">Hallo volgende cURL-opdracht gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ec642-173">Use hello following cURL command.</span></span> <span data-ttu-id="ec642-174">Vervang **\<yourstorename>** door de naam van uw Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ec642-174">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -L -T 'C:\temp\list.txt' -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE'

<span data-ttu-id="ec642-175">In Hallo bovenstaande syntaxis **-T** parameter is Hallo-locatie van het Hallo-bestand wordt geüpload.</span><span class="sxs-lookup"><span data-stu-id="ec642-175">In hello above syntax **-T** parameter is hello location of hello file you are uploading.</span></span>

<span data-ttu-id="ec642-176">Hallo-uitvoer is vergelijkbaar toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="ec642-176">hello output is similar toohello following:</span></span>
   
    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE&write=true
    ...
    Content-Length: 0

    HTTP/1.1 100 Continue

    HTTP/1.1 201 Created
    ...

## <a name="read-data-from-a-data-lake-store-account"></a><span data-ttu-id="ec642-177">Gegevens lezen uit een Data Lake Store-account</span><span class="sxs-lookup"><span data-stu-id="ec642-177">Read data from a Data Lake Store account</span></span>
<span data-ttu-id="ec642-178">Deze bewerking is gebaseerd op Hallo WebHDFS REST-API-aanroep gedefinieerd [hier](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).</span><span class="sxs-lookup"><span data-stu-id="ec642-178">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).</span></span>

<span data-ttu-id="ec642-179">Het lezen van gegevens uit een Data Lake Store is een proces dat uit twee stappen bestaat.</span><span class="sxs-lookup"><span data-stu-id="ec642-179">Reading data from a Data Lake Store account is a two-step process.</span></span>

* <span data-ttu-id="ec642-180">Eerst dient u een GET-aanvraag voor Hallo eindpunt `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span><span class="sxs-lookup"><span data-stu-id="ec642-180">You first submit a GET request against hello endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span></span> <span data-ttu-id="ec642-181">Hiermee herstelt u een locatie toosubmit Hallo volgende GET-aanvraag aan.</span><span class="sxs-lookup"><span data-stu-id="ec642-181">This will return a location toosubmit hello next GET request to.</span></span>
* <span data-ttu-id="ec642-182">Vervolgens dient u Hallo GET-aanvraag voor Hallo eindpunt `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span><span class="sxs-lookup"><span data-stu-id="ec642-182">You then submit hello GET request against hello endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span></span> <span data-ttu-id="ec642-183">Hallo-inhoud van Hallo-bestand wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ec642-183">This will display hello contents of hello file.</span></span>

<span data-ttu-id="ec642-184">Echter, omdat er is geen verschil in Hallo invoerparameters tussen Hallo eerst en hello tweede stap, kunt u Hallo `-L` parameter toosubmit Hallo eerste aanvraag.</span><span class="sxs-lookup"><span data-stu-id="ec642-184">However, because there is no difference in hello input parameters between hello first and hello second step, you can use hello `-L` parameter toosubmit hello first request.</span></span> <span data-ttu-id="ec642-185">`-L`optie in feite twee aanvragen combineert in een en zorgt ervoor dat cURL Hallo aanvraag op de nieuwe locatie Hallo opnieuw.</span><span class="sxs-lookup"><span data-stu-id="ec642-185">`-L` option essentially combines two requests into one and will make cURL redo hello request on hello new location.</span></span> <span data-ttu-id="ec642-186">Ten slotte Hallo-uitvoer van alle Hallo aanvraag aanroepen weergegeven, zoals hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ec642-186">Finally, hello output from all hello request calls is displayed, like shown below.</span></span> <span data-ttu-id="ec642-187">Vervang **\<yourstorename>** door de naam van uw Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ec642-187">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -L GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN'

<span data-ttu-id="ec642-188">U ziet een uitvoer vergelijkbare toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="ec642-188">You should see an output similar toohello following:</span></span>

    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/somerandomfile.txt?op=OPEN&read=true
    ...

    HTTP/1.1 200 OK
    ...

    Hello, Data Lake Store user!

## <a name="rename-a-file-in-a-data-lake-store-account"></a><span data-ttu-id="ec642-189">Bestandsnamen wijzigen in een Data Lake Store-account</span><span class="sxs-lookup"><span data-stu-id="ec642-189">Rename a file in a Data Lake Store account</span></span>
<span data-ttu-id="ec642-190">Deze bewerking is gebaseerd op Hallo WebHDFS REST-API-aanroep gedefinieerd [hier](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).</span><span class="sxs-lookup"><span data-stu-id="ec642-190">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).</span></span>

<span data-ttu-id="ec642-191">Gebruik Hallo volgende cURL-opdracht toorename een bestand.</span><span class="sxs-lookup"><span data-stu-id="ec642-191">Use hello following cURL command toorename a file.</span></span> <span data-ttu-id="ec642-192">Vervang **\<yourstorename>** door de naam van uw Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ec642-192">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=RENAME&destination=/mytempdir/myinputfile1.txt'

<span data-ttu-id="ec642-193">U ziet een uitvoer vergelijkbare toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="ec642-193">You should see an output similar toohello following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-file-from-a-data-lake-store-account"></a><span data-ttu-id="ec642-194">Een bestand verwijderen uit een Data Lake Store-account</span><span class="sxs-lookup"><span data-stu-id="ec642-194">Delete a file from a Data Lake Store account</span></span>
<span data-ttu-id="ec642-195">Deze bewerking is gebaseerd op Hallo WebHDFS REST-API-aanroep gedefinieerd [hier](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).</span><span class="sxs-lookup"><span data-stu-id="ec642-195">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).</span></span>

<span data-ttu-id="ec642-196">Gebruik Hallo volgende cURL-opdracht toodelete een bestand.</span><span class="sxs-lookup"><span data-stu-id="ec642-196">Use hello following cURL command toodelete a file.</span></span> <span data-ttu-id="ec642-197">Vervang **\<yourstorename>** door de naam van uw Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ec642-197">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile1.txt?op=DELETE'

<span data-ttu-id="ec642-198">Hier ziet u uitvoer Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="ec642-198">You should see an output like hello following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="ec642-199">Een Data Lake Store-account verwijderen</span><span class="sxs-lookup"><span data-stu-id="ec642-199">Delete a Data Lake Store account</span></span>
<span data-ttu-id="ec642-200">Deze bewerking is gebaseerd op Hallo REST-API-aanroep gedefinieerd [hier](https://msdn.microsoft.com/library/mt694075.aspx).</span><span class="sxs-lookup"><span data-stu-id="ec642-200">This operation is based on hello REST API call defined [here](https://msdn.microsoft.com/library/mt694075.aspx).</span></span>

<span data-ttu-id="ec642-201">Gebruik Hallo volgende cURL-opdracht toodelete een Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="ec642-201">Use hello following cURL command toodelete a Data Lake Store account.</span></span> <span data-ttu-id="ec642-202">Vervang **\<yourstorename>** door de naam van uw Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="ec642-202">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview

<span data-ttu-id="ec642-203">Hier ziet u uitvoer Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="ec642-203">You should see an output like hello following:</span></span>

    HTTP/1.1 200 OK
    ...
    ...

## <a name="see-also"></a><span data-ttu-id="ec642-204">Zie ook</span><span class="sxs-lookup"><span data-stu-id="ec642-204">See also</span></span>
* [<span data-ttu-id="ec642-205">Open Source Big Data-toepassingen die compatibel zijn met Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="ec642-205">Open Source Big Data applications compatible with Azure Data Lake Store</span></span>](data-lake-store-compatible-oss-other-applications.md)

