---
title: aaaGet de slag met Azure Data Lake Store met Azure SDK voor Node.js | Microsoft Docs
description: Meer informatie over hoe toouse Node.js toowork met Data Lake Store-accounts en Hallo-bestandssysteem.
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
ms.openlocfilehash: ce36a2e0de4e091a4e85ed784a3381415ef6f9e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-sdk-for-nodejs"></a><span data-ttu-id="1a4d4-103">Aan de slag met Azure Data Lake Store met Azure SDK voor Node.js</span><span class="sxs-lookup"><span data-stu-id="1a4d4-103">Get started with Azure Data Lake Store using Azure SDK for Node.js</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1a4d4-104">Portal</span><span class="sxs-lookup"><span data-stu-id="1a4d4-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="1a4d4-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1a4d4-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="1a4d4-106">.NET-SDK</span><span class="sxs-lookup"><span data-stu-id="1a4d4-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="1a4d4-107">Java-SDK</span><span class="sxs-lookup"><span data-stu-id="1a4d4-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="1a4d4-108">REST API</span><span class="sxs-lookup"><span data-stu-id="1a4d4-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="1a4d4-109">Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="1a4d4-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="1a4d4-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="1a4d4-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="1a4d4-111">Python</span><span class="sxs-lookup"><span data-stu-id="1a4d4-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

> [!NOTE]
> <span data-ttu-id="1a4d4-112">Voor het uploaden en downloaden van de grote hoeveelheid gegevens (grote bestanden, een groot aantal bestanden of beide), het is raadzaam dat u Hallo [Python SDK](data-lake-store-get-started-python.md), Hallo [.NET SDK](data-lake-store-get-started-net-sdk.md), [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md), of [Azure PowerShell](data-lake-store-get-started-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="1a4d4-112">For uploading and downloading large amount of data (large files, a large number of files, or both), we recommend that you use hello [Python SDK](data-lake-store-get-started-python.md), hello [.NET SDK](data-lake-store-get-started-net-sdk.md), [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md), or [Azure PowerShell](data-lake-store-get-started-powershell.md).</span></span> <span data-ttu-id="1a4d4-113">Deze opties staat er betere prestaties omdat ze gebruikmaken van meerdere threads tooparallelize Hallo verplaatsing van gegevens.</span><span class="sxs-lookup"><span data-stu-id="1a4d4-113">These options have better performance as they use multiple threads tooparallelize hello data movement.</span></span>
> 
> 

<span data-ttu-id="1a4d4-114">Meer informatie over hoe toouse hello Azure SDK voor Node.js toocreate een Azure Data Lake Store-account en basisbewerkingen uitvoert, zoals maken van mappen, uploaden en downloaden van gegevensbestanden, verwijderen van uw account enzovoort. Zie [Overzicht van Data Lake Store](data-lake-store-overview.md) voor meer informatie over Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1a4d4-114">Learn how toouse hello Azure SDK for Node.js toocreate an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span> <span data-ttu-id="1a4d4-115">Op dit moment hello SDK biedt ondersteuning voor</span><span class="sxs-lookup"><span data-stu-id="1a4d4-115">Currently, hello SDK supports</span></span>

* <span data-ttu-id="1a4d4-116">**Node.js versie: 0.10.0 of hoger**</span><span class="sxs-lookup"><span data-stu-id="1a4d4-116">**Node.js version: 0.10.0 or higher**</span></span>
* <span data-ttu-id="1a4d4-117">**REST-API-versie voor Account: 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="1a4d4-117">**REST API version for Account: 2015-10-01-preview**</span></span>
* <span data-ttu-id="1a4d4-118">**REST-API-versie voor FileSystem: 2015-10-01-preview**</span><span class="sxs-lookup"><span data-stu-id="1a4d4-118">**REST API version for FileSystem: 2015-10-01-preview**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a4d4-119">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1a4d4-119">Prerequisites</span></span>
<span data-ttu-id="1a4d4-120">Voordat u dit artikel, moet u de volgende Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="1a4d4-120">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="1a4d4-121">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="1a4d4-121">**An Azure subscription**.</span></span> <span data-ttu-id="1a4d4-122">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1a4d4-122">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="1a4d4-123">**Een Azure Active Directory-toepassing maken**.</span><span class="sxs-lookup"><span data-stu-id="1a4d4-123">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="1a4d4-124">U hello Azure AD-toepassing tooauthenticate Hallo Data Lake Store-toepassing gebruiken met Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1a4d4-124">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="1a4d4-125">Er zijn verschillende benaderingen tooauthenticate met Azure AD zijn **eindgebruiker verificatie** of **authentication service-naar-serviceconnector**.</span><span class="sxs-lookup"><span data-stu-id="1a4d4-125">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="1a4d4-126">Voor instructies en meer informatie over het tooauthenticate, Zie [eindgebruiker verificatie](data-lake-store-end-user-authenticate-using-active-directory.md) of [authentication Service-naar-serviceconnector](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="1a4d4-126">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="how-tooinstall"></a><span data-ttu-id="1a4d4-127">Hoe tooInstall</span><span class="sxs-lookup"><span data-stu-id="1a4d4-127">How tooInstall</span></span>
```bash
npm install azure-arm-datalake-store
```

## <a name="authenticate-using-azure-active-directory"></a><span data-ttu-id="1a4d4-128">Verifiëren met Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1a4d4-128">Authenticate using Azure Active Directory</span></span>
<span data-ttu-id="1a4d4-129">Hallo codefragmenten hieronder ziet u twee afzonderlijke manieren voor het verifiëren met Data Lake Store gebruikmaken van Azure AD.</span><span class="sxs-lookup"><span data-stu-id="1a4d4-129">hello snippets below show two separate ways of authenticating with Data Lake Store using Azure AD.</span></span> <span data-ttu-id="1a4d4-130">Zie voor een gedetailleerde bespreking van de verschillende methoden toouse voor verificatie met Data Lake Store, [verifiëren met Data Lake Store met Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="1a4d4-130">For a detailed discussion on various methods toouse for authentication with Data Lake Store, see [Authenticate with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

<span data-ttu-id="1a4d4-131">Hallo codefragment onderstaande vereist ook invoeritems zoals Azure AD-domeinnaam, client-ID voor een Azure AD-app, enzovoort. Alle deze gegevens kunnen worden opgehaald uit een Azure AD-toepassing die u moet gemaakt, Hallo details hiervan ook in de bovenstaande koppeling opgenomen zijn.</span><span class="sxs-lookup"><span data-stu-id="1a4d4-131">hello snippet below also requires inputs like Azure AD domain name, client ID for an Azure AD app, etc. All these details can be retrieved from an Azure AD application that you must created, hello details of which are also included in link above.</span></span>

 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-hello-data-lake-store-clients"></a><span data-ttu-id="1a4d4-132">Hallo Data Lake Store-Clients maken</span><span class="sxs-lookup"><span data-stu-id="1a4d4-132">Create hello Data Lake Store Clients</span></span>
```javascript
var adlsManagement = require("azure-arm-datalake-store");
var acccountClient = new adlsManagement.DataLakeStoreAccountClient(credentials, "your-subscription-id");
var filesystemClient = new adlsManagement.DataLakeStoreFileSystemClient(credentials);
```

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="1a4d4-133">Een Data Lake Store-Account maken</span><span class="sxs-lookup"><span data-stu-id="1a4d4-133">Create a Data Lake Store Account</span></span>
```javascript
var util = require('util');
var resourceGroupName = 'testrg';
var accountName = 'testadlsacct';
var location = 'eastus2';

// account object toocreate
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
    /*err has reference toohello actual request and response, so you can see what was sent and received on hello wire.
      hello structure of err looks like this:
      err: {
        code: 'Error Code',
        message: 'Error Message',
        body: 'hello response body if any',
        request: reference tooa stripped version of http request
        response: reference tooa stripped version of hello response
      }
    */
  } else {
    console.log('result is: ' + util.inspect(result, {depth: null}));
  }
});
```

## <a name="create-a-file-with-content"></a><span data-ttu-id="1a4d4-134">Een bestand met inhoud maken</span><span class="sxs-lookup"><span data-stu-id="1a4d4-134">Create a file with content</span></span>
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

## <a name="get-a-list-of-files-and-folders"></a><span data-ttu-id="1a4d4-135">Een lijst met bestanden en mappen</span><span class="sxs-lookup"><span data-stu-id="1a4d4-135">Get a list of files and folders</span></span>
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

## <a name="see-also"></a><span data-ttu-id="1a4d4-136">Zie ook</span><span class="sxs-lookup"><span data-stu-id="1a4d4-136">See also</span></span>
* [<span data-ttu-id="1a4d4-137">Microsoft Azure SDK voor Node.js</span><span class="sxs-lookup"><span data-stu-id="1a4d4-137">Microsoft Azure SDK for Node.js</span></span>](https://github.com/azure/azure-sdk-for-node)
* [<span data-ttu-id="1a4d4-138">Microsoft Azure SDK voor Node.js - Data Lake Analytics Management</span><span class="sxs-lookup"><span data-stu-id="1a4d4-138">Microsoft Azure SDK for Node.js - Data Lake Analytics Management</span></span>](https://www.npmjs.com/package/azure-arm-datalake-analytics)

