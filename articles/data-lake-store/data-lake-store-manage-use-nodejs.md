---
title: Aan de slag met Azure Data Lake Store met Azure SDK voor Node.js | Microsoft Docs
description: Informatie over het gebruik van Node.js werken met Data Lake Store-accounts en het bestandssysteem.
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 2fee173c-69ae-4e1d-8773-48618cda9e16
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/06/2017
ms.author: nitinme
ms.openlocfilehash: 8c7a2e6ca061bbfa077592efb73d592906c3d070
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-sdk-for-nodejs"></a><span data-ttu-id="5a3aa-103">Aan de slag met Azure Data Lake Store met Azure SDK voor Node.js</span><span class="sxs-lookup"><span data-stu-id="5a3aa-103">Get started with Azure Data Lake Store using Azure SDK for Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="5a3aa-104">Portal</span><span class="sxs-lookup"><span data-stu-id="5a3aa-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="5a3aa-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5a3aa-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="5a3aa-106">.NET-SDK</span><span class="sxs-lookup"><span data-stu-id="5a3aa-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="5a3aa-107">Java-SDK</span><span class="sxs-lookup"><span data-stu-id="5a3aa-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="5a3aa-108">REST API</span><span class="sxs-lookup"><span data-stu-id="5a3aa-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="5a3aa-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5a3aa-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="5a3aa-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="5a3aa-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="5a3aa-111">Python</span><span class="sxs-lookup"><span data-stu-id="5a3aa-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

> [!NOTE]
> <span data-ttu-id="5a3aa-112">Voor het uploaden en downloaden van de grote hoeveelheid gegevens (grote bestanden, een groot aantal bestanden of beide), het is raadzaam dat u de [Python SDK](data-lake-store-get-started-python.md), wordt de [.NET SDK](data-lake-store-get-started-net-sdk.md), [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md), of [Azure PowerShell](data-lake-store-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="5a3aa-112">For uploading and downloading large amount of data (large files, a large number of files, or both), we recommend that you use the [Python SDK](data-lake-store-get-started-python.md), the [.NET SDK](data-lake-store-get-started-net-sdk.md), [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md), or [Azure PowerShell](data-lake-store-get-started-powershell.md).</span></span> <span data-ttu-id="5a3aa-113">Met deze opties profiteert u van betere prestaties, omdat er meerdere threads worden gebruikt om de gegevensverplaatsing parallel te laten verlopen.</span><span class="sxs-lookup"><span data-stu-id="5a3aa-113">These options have better performance as they use multiple threads to parallelize the data movement.</span></span>
> 
> 

<span data-ttu-id="5a3aa-114">Ontdek hoe u met de Azure SDK voor Node.js een Azure Data Lake Store-account maken en basisbewerkingen uitvoert, zoals maken van mappen, uploaden en downloaden van gegevensbestanden, verwijderen van uw account, enzovoort. Zie [Overzicht van Data Lake Store](data-lake-store-overview.md) voor meer informatie over Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="5a3aa-114">Learn how to use the Azure SDK for Node.js to create an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span> <span data-ttu-id="5a3aa-115">Op dit moment is de SDK biedt ondersteuning voor</span><span class="sxs-lookup"><span data-stu-id="5a3aa-115">Currently, the SDK supports</span></span>

* <span data-ttu-id="5a3aa-116">**Node.js versie: 0.10.0 of hoger**</span><span class="sxs-lookup"><span data-stu-id="5a3aa-116">**Node.js version: 0.10.0 or higher**</span></span>
* <span data-ttu-id="5a3aa-117">**REST-API-versie voor Account: 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="5a3aa-117">**REST API version for Account: 2015-10-01-preview**</span></span>
* <span data-ttu-id="5a3aa-118">**REST-API-versie voor FileSystem: 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="5a3aa-118">**REST API version for FileSystem: 2015-10-01-preview**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5a3aa-119">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5a3aa-119">Prerequisites</span></span>
<span data-ttu-id="5a3aa-120">Voordat u dit artikel gaat lezen, moet u beschikken over het volgende:</span><span class="sxs-lookup"><span data-stu-id="5a3aa-120">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="5a3aa-121">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="5a3aa-121">**An Azure subscription**.</span></span> <span data-ttu-id="5a3aa-122">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="5a3aa-122">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="5a3aa-123">**Een Azure Active Directory-toepassing maken**.</span><span class="sxs-lookup"><span data-stu-id="5a3aa-123">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="5a3aa-124">U gebruikt de Azure AD-toepassing om de Data Lake Store-toepassing te verifiëren in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5a3aa-124">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="5a3aa-125">Er zijn verschillende manieren om te verifiëren in Azure AD, zoals **verificatie door eindgebruikers** en **service-naar-serviceverificatie**.</span><span class="sxs-lookup"><span data-stu-id="5a3aa-125">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="5a3aa-126">Zie [Eindgebruikersverificatie](data-lake-store-end-user-authenticate-using-active-directory.md) of [Service-to-serviceverificatie](data-lake-store-authenticate-using-active-directory.md) voor instructies en meer informatie over verificatie.</span><span class="sxs-lookup"><span data-stu-id="5a3aa-126">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="how-to-install"></a><span data-ttu-id="5a3aa-127">Installeren</span><span class="sxs-lookup"><span data-stu-id="5a3aa-127">How to Install</span></span>
```bash
npm install azure-arm-datalake-store
```

## <a name="authenticate-using-azure-active-directory"></a><span data-ttu-id="5a3aa-128">Verifiëren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5a3aa-128">Authenticate using Azure Active Directory</span></span>
<span data-ttu-id="5a3aa-129">De codefragmenten hieronder ziet u twee afzonderlijke manieren voor het verifiëren met Data Lake Store met behulp van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="5a3aa-129">The snippets below show two separate ways of authenticating with Data Lake Store using Azure AD.</span></span> <span data-ttu-id="5a3aa-130">Zie voor een gedetailleerde discussie over de verschillende methoden voor verificatie met Data Lake Store [verifiëren met Data Lake Store met Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="5a3aa-130">For a detailed discussion on various methods to use for authentication with Data Lake Store, see [Authenticate with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="5a3aa-131">Het onderstaande codefragment is ook vereist voor invoer zoals Azure AD-domeinnaam, client-ID voor een Azure AD-app, enzovoort. Alle deze gegevens kunnen worden opgehaald uit een Azure AD-toepassing die u moet gemaakt, waarvan de details ook in de bovenstaande koppeling opgenomen worden.</span><span class="sxs-lookup"><span data-stu-id="5a3aa-131">The snippet below also requires inputs like Azure AD domain name, client ID for an Azure AD app, etc. All these details can be retrieved from an Azure AD application that you must created, the details of which are also included in link above.</span></span>

 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-the-data-lake-store-clients"></a><span data-ttu-id="5a3aa-132">De Data Lake Store-Clients maken</span><span class="sxs-lookup"><span data-stu-id="5a3aa-132">Create the Data Lake Store Clients</span></span>
```javascript
var adlsManagement = require("azure-arm-datalake-store");
var acccountClient = new adlsManagement.DataLakeStoreAccountClient(credentials, "your-subscription-id");
var filesystemClient = new adlsManagement.DataLakeStoreFileSystemClient(credentials);
```

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="5a3aa-133">Een Data Lake Store-Account maken</span><span class="sxs-lookup"><span data-stu-id="5a3aa-133">Create a Data Lake Store Account</span></span>
```javascript
var util = require('util');
var resourceGroupName = 'testrg';
var accountName = 'testadlsacct';
var location = 'eastus2';

// account object to create
var accountToCreate = {
  tags: {
    testtag1: 'testvalue1',
    testtag2: 'testvalue2'
  },
  name: accountName,
  location: location
};

client.account.create(resourceGroupName, accountName, accountToCreate, function (err, result, request, response) {
  if (err) {
    console.log(err);
    /*err has reference to the actual request and response, so you can see what was sent and received on the wire.
      The structure of err looks like this:
      err: {
        code: 'Error Code',
        message: 'Error Message',
        body: 'The response body if any',
        request: reference to a stripped version of http request
        response: reference to a stripped version of the response
      }
    */
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="create-a-file-with-content"></a><span data-ttu-id="5a3aa-134">Een bestand met inhoud maken</span><span class="sxs-lookup"><span data-stu-id="5a3aa-134">Create a file with content</span></span>
```javascript
var util = require('util');
var accountName = 'testadlsacct';
var fileToCreate = '/myfolder/myfile.txt';
var options = {
  streamContents: new Buffer('some string content')
}

filesystemClient.fileSystem.listFileStatus(accountName, fileToCreate, options, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    // no result is returned, only a 201 response for success.
    console.log('response is: ' + util.inspect(response, {depth: null}));
  }
});
```

## <a name="get-a-list-of-files-and-folders"></a><span data-ttu-id="5a3aa-135">Een lijst met bestanden en mappen</span><span class="sxs-lookup"><span data-stu-id="5a3aa-135">Get a list of files and folders</span></span>
```javascript
var util = require('util');
var accountName = 'testadlsacct';
var pathToEnumerate = '/myfolder';
filesystemClient.fileSystem.listFileStatus(accountName, pathToEnumerate, function (err, result, request, response) {
  if (err) {
    console.log(err);
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="see-also"></a><span data-ttu-id="5a3aa-136">Zie ook</span><span class="sxs-lookup"><span data-stu-id="5a3aa-136">See also</span></span>
* [<span data-ttu-id="5a3aa-137">Microsoft Azure SDK voor Node.js</span><span class="sxs-lookup"><span data-stu-id="5a3aa-137">Microsoft Azure SDK for Node.js</span></span>](https://github.com/azure/azure-sdk-for-node)
* [<span data-ttu-id="5a3aa-138">Microsoft Azure SDK voor Node.js - Data Lake Analytics Management</span><span class="sxs-lookup"><span data-stu-id="5a3aa-138">Microsoft Azure SDK for Node.js - Data Lake Analytics Management</span></span>](https://www.npmjs.com/package/azure-arm-datalake-analytics)

