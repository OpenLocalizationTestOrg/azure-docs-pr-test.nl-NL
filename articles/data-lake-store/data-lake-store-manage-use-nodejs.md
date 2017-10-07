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
# <a name="get-started-with-azure-data-lake-store-using-azure-sdk-for-nodejs"></a>Aan de slag met Azure Data Lake Store met Azure SDK voor Node.js
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET-SDK](data-lake-store-get-started-net-sdk.md)
> * [Java-SDK](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
> 

> [!NOTE]
> Voor het uploaden en downloaden van de grote hoeveelheid gegevens (grote bestanden, een groot aantal bestanden of beide), het is raadzaam dat u Hallo [Python SDK](data-lake-store-get-started-python.md), Hallo [.NET SDK](data-lake-store-get-started-net-sdk.md), [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md), of [Azure PowerShell](data-lake-store-get-started-powershell.md). Deze opties staat er betere prestaties omdat ze gebruikmaken van meerdere threads tooparallelize Hallo verplaatsing van gegevens.
> 
> 

Meer informatie over hoe toouse hello Azure SDK voor Node.js toocreate een Azure Data Lake Store-account en basisbewerkingen uitvoert, zoals maken van mappen, uploaden en downloaden van gegevensbestanden, verwijderen van uw account enzovoort. Zie [Overzicht van Data Lake Store](data-lake-store-overview.md) voor meer informatie over Data Lake Store. Op dit moment hello SDK biedt ondersteuning voor

* **Node.js versie: 0.10.0 of hoger**
* **REST-API-versie voor Account: 2015-10-01-preview**
* **REST-API-versie voor FileSystem: 2015-10-01-preview**

## <a name="prerequisites"></a>Vereisten
Voordat u dit artikel, moet u de volgende Hallo hebben:

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).
* **Een Azure Active Directory-toepassing maken**. U hello Azure AD-toepassing tooauthenticate Hallo Data Lake Store-toepassing gebruiken met Azure AD. Er zijn verschillende benaderingen tooauthenticate met Azure AD zijn **eindgebruiker verificatie** of **authentication service-naar-serviceconnector**. Voor instructies en meer informatie over het tooauthenticate, Zie [eindgebruiker verificatie](data-lake-store-end-user-authenticate-using-active-directory.md) of [authentication Service-naar-serviceconnector](data-lake-store-authenticate-using-active-directory.md).

## <a name="how-tooinstall"></a>Hoe tooInstall
```bash
npm install azure-arm-datalake-store
```

## <a name="authenticate-using-azure-active-directory"></a>Verifiëren met Azure Active Directory
Hallo codefragmenten hieronder ziet u twee afzonderlijke manieren voor het verifiëren met Data Lake Store gebruikmaken van Azure AD. Zie voor een gedetailleerde bespreking van de verschillende methoden toouse voor verificatie met Data Lake Store, [verifiëren met Data Lake Store met Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).

Hallo codefragment onderstaande vereist ook invoeritems zoals Azure AD-domeinnaam, client-ID voor een Azure AD-app, enzovoort. Alle deze gegevens kunnen worden opgehaald uit een Azure AD-toepassing die u moet gemaakt, Hallo details hiervan ook in de bovenstaande koppeling opgenomen zijn.

 ```javascript
 var msrestAzure = require('ms-rest-azure');
 //user authentication
 var credentials = new msRestAzure.UserTokenCredentials('your-client-id', 'your-domain', 'your-username', 'your-password', 'your-redirect-uri');
 //service principal authentication
 var credentials = new msRestAzure.ApplicationTokenCredentials('your-client-id', 'your-domain', 'your-secret');
 ```

## <a name="create-hello-data-lake-store-clients"></a>Hallo Data Lake Store-Clients maken
```javascript
var adlsManagement = require("azure-arm-datalake-store");
var acccountClient = new adlsManagement.DataLakeStoreAccountClient(credentials, "your-subscription-id");
var filesystemClient = new adlsManagement.DataLakeStoreFileSystemClient(credentials);
```

## <a name="create-a-data-lake-store-account"></a>Een Data Lake Store-Account maken
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

## <a name="create-a-file-with-content"></a>Een bestand met inhoud maken
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

## <a name="get-a-list-of-files-and-folders"></a>Een lijst met bestanden en mappen
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

## <a name="see-also"></a>Zie ook
* [Microsoft Azure SDK voor Node.js](https://github.com/azure/azure-sdk-for-node)
* [Microsoft Azure SDK voor Node.js - Data Lake Analytics Management](https://www.npmjs.com/package/azure-arm-datalake-analytics)

