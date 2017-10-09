---
title: aaaHow toouse Blob-opslag met Node.js | Microsoft Docs
description: Niet-gestructureerde gegevens opslaan in Hallo cloud met Azure Blob storage (objectopslag).
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 8b0df222-1ca8-4967-8248-6d6d720947b8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: e405eecdc60cd1eaa77510e7b29b41269372b65e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-nodejs"></a><span data-ttu-id="50c3a-103">Hoe toouse Blob-opslag met Node.js</span><span class="sxs-lookup"><span data-stu-id="50c3a-103">How toouse Blob storage from Node.js</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="50c3a-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="50c3a-104">Overview</span></span>
<span data-ttu-id="50c3a-105">Dit artikel ziet u hoe tooperform algemene scenario's met behulp van Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="50c3a-105">This article shows you how tooperform common scenarios using Blob storage.</span></span> <span data-ttu-id="50c3a-106">Hallo-voorbeelden zijn geschreven via Hallo Node.js-API.</span><span class="sxs-lookup"><span data-stu-id="50c3a-106">hello samples are written via hello Node.js API.</span></span> <span data-ttu-id="50c3a-107">Hallo scenario's worden behandeld bevatten hoe tooupload, weergeven, downloaden en verwijderen van blobs.</span><span class="sxs-lookup"><span data-stu-id="50c3a-107">hello scenarios covered include how tooupload, list, download, and delete blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="50c3a-108">Een Node.js-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="50c3a-108">Create a Node.js application</span></span>
<span data-ttu-id="50c3a-109">Voor instructies over het toocreate een Node.js-toepassing Zie [een Node.js-web-app maken in Azure App Service], [bouwen en implementeren van een Node.js-toepassing tooan Azure Cloud Service] --met Windows PowerShell , of [bouwen en implementeren van een Node.js web-app tooAzure met behulp van Web Matrix].</span><span class="sxs-lookup"><span data-stu-id="50c3a-109">For instructions on how toocreate a Node.js application, see [Create a Node.js web app in Azure App Service], [Build and deploy a Node.js application tooan Azure Cloud Service] -- using Windows PowerShell, or [Build and deploy a Node.js web app tooAzure using Web Matrix].</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="50c3a-110">Uw toepassing tooaccess opslag configureren</span><span class="sxs-lookup"><span data-stu-id="50c3a-110">Configure your application tooaccess storage</span></span>
<span data-ttu-id="50c3a-111">toouse Azure-opslag, moet u hello Azure-opslag-SDK voor Node.js, waaronder een set van gemak bibliotheken die met de Hallo storage REST-services communiceren.</span><span class="sxs-lookup"><span data-stu-id="50c3a-111">toouse Azure storage, you need hello Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="50c3a-112">Knooppunt Package Manager (NPM) tooobtain Hallo pakket gebruiken</span><span class="sxs-lookup"><span data-stu-id="50c3a-112">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="50c3a-113">Een opdrachtregelinterface gebruiken zoals **PowerShell** (Windows), **Terminal** (Mac) of **Bash** (Unix) toonavigate toohello map waar u uw voorbeeld hebt gemaakt. de toepassing.</span><span class="sxs-lookup"><span data-stu-id="50c3a-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), toonavigate toohello folder where you created your sample application.</span></span>
2. <span data-ttu-id="50c3a-114">Type **npm Installeer azure-opslag** in Hallo-opdrachtvenster.</span><span class="sxs-lookup"><span data-stu-id="50c3a-114">Type **npm install azure-storage** in hello command window.</span></span> <span data-ttu-id="50c3a-115">Uitvoer van de opdracht Hallo is vergelijkbaar toohello volgende codevoorbeeld.</span><span class="sxs-lookup"><span data-stu-id="50c3a-115">Output from hello command is similar toohello following code example.</span></span>

        azure-storage@0.5.0 node_modules\azure-storage
        +-- extend@1.2.1
        +-- xmlbuilder@0.4.3
        +-- mime@1.2.11
        +-- node-uuid@1.4.3
        +-- validator@3.22.2
        +-- underscore@1.4.4
        +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
        +-- xml2js@0.2.7 (sax@0.5.2)
        +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
3. <span data-ttu-id="50c3a-116">U kunt handmatig uitvoeren Hallo **ls** tooverify opdracht die een **knooppunt\_modules** map is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="50c3a-116">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="50c3a-117">Hallo zoeken in die map **azure-opslag** , dit pakket bevat, moet u tooaccess opslag Hallo-bibliotheken.</span><span class="sxs-lookup"><span data-stu-id="50c3a-117">Inside that folder, find hello **azure-storage** package, which contains hello libraries that you need tooaccess storage.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="50c3a-118">Hallo-pakket importeren</span><span class="sxs-lookup"><span data-stu-id="50c3a-118">Import hello package</span></span>
<span data-ttu-id="50c3a-119">Hallo toohello bovenaan hello te volgen in Kladblok of een andere teksteditor toevoegen **server.js** -bestand van de toepassing hello waar u van plan toouse opslag bent:</span><span class="sxs-lookup"><span data-stu-id="50c3a-119">Using Notepad or another text editor, add hello following toohello top of hello **server.js** file of hello application where you intend toouse storage:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="50c3a-120">Een Azure Storage-verbinding instellen</span><span class="sxs-lookup"><span data-stu-id="50c3a-120">Set up an Azure Storage connection</span></span>
<span data-ttu-id="50c3a-121">Hello Azure-module lezen Hallo omgevingsvariabelen `AZURE_STORAGE_ACCOUNT` en `AZURE_STORAGE_ACCESS_KEY`, of `AZURE_STORAGE_CONNECTION_STRING`, vereist tooconnect tooyour Azure storage-account voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="50c3a-121">hello Azure module will read hello environment variables `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY`, or `AZURE_STORAGE_CONNECTION_STRING`, for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="50c3a-122">Als deze omgevingsvariabelen zijn niet ingesteld, moet u de accountgegevens Hallo opgeven bij het aanroepen van **createBlobService**.</span><span class="sxs-lookup"><span data-stu-id="50c3a-122">If these environment variables are not set, you must specify hello account information when calling **createBlobService**.</span></span>

<span data-ttu-id="50c3a-123">Voor een voorbeeld van het Hallo-omgevingsvariabelen instellen in Hallo [Azure-portal](https://portal.azure.com) Zie voor een Azure-web-app [Node.js web app met behulp van hello Azure Table-Service].</span><span class="sxs-lookup"><span data-stu-id="50c3a-123">For an example of setting hello environment variables in hello [Azure portal](https://portal.azure.com) for an Azure web app, see [Node.js web app using hello Azure Table Service].</span></span>

## <a name="create-a-container"></a><span data-ttu-id="50c3a-124">Een container maken</span><span class="sxs-lookup"><span data-stu-id="50c3a-124">Create a container</span></span>
<span data-ttu-id="50c3a-125">Hallo **BlobService** object kunt u samenwerken met containers en blobs.</span><span class="sxs-lookup"><span data-stu-id="50c3a-125">hello **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="50c3a-126">Hallo volgende code maakt een **BlobService** object.</span><span class="sxs-lookup"><span data-stu-id="50c3a-126">hello following code creates a **BlobService** object.</span></span> <span data-ttu-id="50c3a-127">Voeg de volgende Hallo aan de bovenkant Hallo van **server.js**:</span><span class="sxs-lookup"><span data-stu-id="50c3a-127">Add hello following near hello top of **server.js**:</span></span>

```nodejs
var blobSvc = azure.createBlobService();
```

> [!NOTE]
> <span data-ttu-id="50c3a-128">U kunt toegang tot een blob anoniem met **createBlobServiceAnonymous** en het adres van de host Hallo geven.</span><span class="sxs-lookup"><span data-stu-id="50c3a-128">You can access a blob anonymously by using **createBlobServiceAnonymous** and providing hello host address.</span></span> <span data-ttu-id="50c3a-129">Bijvoorbeeld: `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.</span><span class="sxs-lookup"><span data-stu-id="50c3a-129">For example, use `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.</span></span>
>
>

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="50c3a-130">Gebruik een nieuwe container toocreate **createContainerIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="50c3a-130">toocreate a new container, use **createContainerIfNotExists**.</span></span> <span data-ttu-id="50c3a-131">Hallo maakt volgende codevoorbeeld een nieuwe container met de naam 'mycontainer':</span><span class="sxs-lookup"><span data-stu-id="50c3a-131">hello following code example creates a new container named 'mycontainer':</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', function(error, result, response){
    if(!error){
      // Container exists and is private
    }
});
```

<span data-ttu-id="50c3a-132">Als het Hallo-container pas is gemaakt, `result.created` is ingesteld op true.</span><span class="sxs-lookup"><span data-stu-id="50c3a-132">If hello container is newly created, `result.created` is true.</span></span> <span data-ttu-id="50c3a-133">Als het Hallo-container bestaat al, `result.created` is ingesteld op false.</span><span class="sxs-lookup"><span data-stu-id="50c3a-133">If hello container already exists, `result.created` is false.</span></span> <span data-ttu-id="50c3a-134">`response`bevat informatie over het Hallo-bewerking, inclusief Hallo ETag-informatie voor Hallo-container.</span><span class="sxs-lookup"><span data-stu-id="50c3a-134">`response` contains information about hello operation, including hello ETag information for hello container.</span></span>

### <a name="container-security"></a><span data-ttu-id="50c3a-135">Beveiliging van de container</span><span class="sxs-lookup"><span data-stu-id="50c3a-135">Container security</span></span>
<span data-ttu-id="50c3a-136">Standaard worden nieuwe containers privé zijn en kunnen niet anoniem worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="50c3a-136">By default, new containers are private and cannot be accessed anonymously.</span></span> <span data-ttu-id="50c3a-137">toomake hello container openbare zodat u toegang hebt tot het anoniem, kunt u instellen toegangsniveau Hallo-container te**blob** of **container**.</span><span class="sxs-lookup"><span data-stu-id="50c3a-137">toomake hello container public so that you can access it anonymously, you can set hello container's access level too**blob** or **container**.</span></span>

* <span data-ttu-id="50c3a-138">**BLOB** -kunnen anonieme leestoegang tooblob inhoud en metagegevens in deze container, maar niet toocontainer metagegevens zoals het weergeven van alle blobs in een container</span><span class="sxs-lookup"><span data-stu-id="50c3a-138">**blob** - allows anonymous read access tooblob content and metadata within this container, but not toocontainer metadata such as listing all blobs within a container</span></span>
* <span data-ttu-id="50c3a-139">**container** -kunnen anonieme leestoegang tooblob inhoud en metagegevens, evenals de metagegevens van de container</span><span class="sxs-lookup"><span data-stu-id="50c3a-139">**container** - allows anonymous read access tooblob content and metadata as well as container metadata</span></span>

<span data-ttu-id="50c3a-140">Hallo volgende codevoorbeeld toont instelling Hallo toegangsniveau te**blob**:</span><span class="sxs-lookup"><span data-stu-id="50c3a-140">hello following code example demonstrates setting hello access level too**blob**:</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', {publicAccessLevel : 'blob'}, function(error, result, response){
    if(!error){
      // Container exists and allows
      // anonymous read access tooblob
      // content and metadata within this container
    }
});
```

<span data-ttu-id="50c3a-141">U kunt ook Hallo toegangsniveau van een container wijzigen met behulp van **setContainerAcl** toospecify Hallo-toegangsniveau.</span><span class="sxs-lookup"><span data-stu-id="50c3a-141">Alternatively, you can modify hello access level of a container by using **setContainerAcl** toospecify hello access level.</span></span> <span data-ttu-id="50c3a-142">Hallo volgende code voorbeeld wijzigingen Hallo toegang niveau toocontainer:</span><span class="sxs-lookup"><span data-stu-id="50c3a-142">hello following code example changes hello access level toocontainer:</span></span>

```nodejs
blobSvc.setContainerAcl('mycontainer', null /* signedIdentifiers */, {publicAccessLevel : 'container'} /* publicAccessLevel*/, function(error, result, response){
  if(!error){
    // Container access level set too'container'
  }
});
```

<span data-ttu-id="50c3a-143">Hallo resultaat bevat informatie over het Hallo-bewerking, met inbegrip van Hallo stroom **ETag** voor Hallo-container.</span><span class="sxs-lookup"><span data-stu-id="50c3a-143">hello result contains information about hello operation, including hello current **ETag** for hello container.</span></span>

### <a name="filters"></a><span data-ttu-id="50c3a-144">Filters</span><span class="sxs-lookup"><span data-stu-id="50c3a-144">Filters</span></span>
<span data-ttu-id="50c3a-145">U kunt toepassen optionele filteren operations toooperations uitgevoerd met behulp van **BlobService**.</span><span class="sxs-lookup"><span data-stu-id="50c3a-145">You can apply optional filtering operations toooperations performed using **BlobService**.</span></span> <span data-ttu-id="50c3a-146">Bewerkingen voor het filteren kunt opnemen logboekregistratie, automatisch opnieuw, enzovoort. Filters zijn objecten die een methode met Hallo handtekening te implementeren:</span><span class="sxs-lookup"><span data-stu-id="50c3a-146">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="50c3a-147">Hierna moet u de voorverwerking op Hallo aanvraag opties, moet Hallo-methode toocall 'volgende' doorgeven van een retouraanroep Hello handtekening te volgen:</span><span class="sxs-lookup"><span data-stu-id="50c3a-147">After doing its preprocessing on hello request options, hello method needs toocall "next", passing a callback with hello following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="50c3a-148">In deze retouraanroep en na het verwerken van Hallo returnObject (Hallo reactie van Hallo aanvraag toohello server), Hallo callback tooeither moet vervolgens aanroepen als deze bestaat toocontinue verwerking van andere filters of gewoon finalCallback tooend Hallo service aanroepen aanroep.</span><span class="sxs-lookup"><span data-stu-id="50c3a-148">In this callback, and after processing hello returnObject (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or simply invoke finalCallback tooend hello service invocation.</span></span>

<span data-ttu-id="50c3a-149">Twee filters die Pogingslogica implementeren zijn opgenomen in hello Azure SDK voor Node.js, **ExponentialRetryPolicyFilter** en **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="50c3a-149">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="50c3a-150">Hallo volgende maakt een **BlobService** object dat gebruikmaakt van Hallo **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="50c3a-150">hello following creates a **BlobService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var blobSvc = azure.createBlobService().withFilter(retryOperations);
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="50c3a-151">Een blob uploaden naar een container</span><span class="sxs-lookup"><span data-stu-id="50c3a-151">Upload a blob into a container</span></span>
<span data-ttu-id="50c3a-152">Er zijn drie typen blobs: blok-blobs, pagina-blobs en toevoeg-blobs.</span><span class="sxs-lookup"><span data-stu-id="50c3a-152">There are three types of blobs: block blobs, page blobs and append blobs.</span></span> <span data-ttu-id="50c3a-153">Blok-blobs kunnen u toomore efficiënt grote hoeveelheden gegevens te uploaden.</span><span class="sxs-lookup"><span data-stu-id="50c3a-153">Block blobs allow you toomore efficiently upload large data.</span></span> <span data-ttu-id="50c3a-154">Toevoeg-blobs zijn geoptimaliseerd voor toevoegbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="50c3a-154">Append blobs are optimized for append operations.</span></span> <span data-ttu-id="50c3a-155">Pagina-blobs zijn geoptimaliseerd voor lees-en schrijfbewerkingen.</span><span class="sxs-lookup"><span data-stu-id="50c3a-155">Page blobs are optimized for read/write operations.</span></span> <span data-ttu-id="50c3a-156">Zie voor meer informatie [blok-Blobs, toevoeg-Blobs en pagina-Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="50c3a-156">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

### <a name="block-blobs"></a><span data-ttu-id="50c3a-157">Blok-blobs</span><span class="sxs-lookup"><span data-stu-id="50c3a-157">Block blobs</span></span>
<span data-ttu-id="50c3a-158">tooupload gegevens tooa blok-blob, gebruik hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="50c3a-158">tooupload data tooa block blob, use hello following:</span></span>

* <span data-ttu-id="50c3a-159">**createBlockBlobFromLocalFile** - maakt een nieuw blok-blob en uploadt Hallo inhoud van een bestand</span><span class="sxs-lookup"><span data-stu-id="50c3a-159">**createBlockBlobFromLocalFile** - creates a new block blob and uploads hello contents of a file</span></span>
* <span data-ttu-id="50c3a-160">**createBlockBlobFromStream** - maakt een nieuw blok-blob en uploadt Hallo inhoud van een stream</span><span class="sxs-lookup"><span data-stu-id="50c3a-160">**createBlockBlobFromStream** - creates a new block blob and uploads hello contents of a stream</span></span>
* <span data-ttu-id="50c3a-161">**createBlockBlobFromText** - maakt een nieuw blok-blob en uploadt Hallo inhoud van een tekenreeks</span><span class="sxs-lookup"><span data-stu-id="50c3a-161">**createBlockBlobFromText** - creates a new block blob and uploads hello contents of a string</span></span>
* <span data-ttu-id="50c3a-162">**createWriteStreamToBlockBlob** -biedt een schrijven stroom tooa blok-blob</span><span class="sxs-lookup"><span data-stu-id="50c3a-162">**createWriteStreamToBlockBlob** - provides a write stream tooa block blob</span></span>

<span data-ttu-id="50c3a-163">Hallo volgende codevoorbeeld uploadt Hallo inhoud Hallo **test.txt** bestand naar **myblob**.</span><span class="sxs-lookup"><span data-stu-id="50c3a-163">hello following code example uploads hello contents of hello **test.txt** file into **myblob**.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="50c3a-164">Hallo `result` geretourneerd door deze methoden bevat informatie over het Hallo-bewerking, zoals Hallo **ETag** van Hallo blob.</span><span class="sxs-lookup"><span data-stu-id="50c3a-164">hello `result` returned by these methods contains information on hello operation, such as hello **ETag** of hello blob.</span></span>

### <a name="append-blobs"></a><span data-ttu-id="50c3a-165">Toevoeg-blobs</span><span class="sxs-lookup"><span data-stu-id="50c3a-165">Append blobs</span></span>
<span data-ttu-id="50c3a-166">tooupload gegevens tooa nieuwe toevoeg-blob, Hallo volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="50c3a-166">tooupload data tooa new append blob, use hello following:</span></span>

* <span data-ttu-id="50c3a-167">**createAppendBlobFromLocalFile** - maakt een nieuwe toevoeg-blob en uploadt Hallo inhoud van een bestand</span><span class="sxs-lookup"><span data-stu-id="50c3a-167">**createAppendBlobFromLocalFile** - creates a new append blob and uploads hello contents of a file</span></span>
* <span data-ttu-id="50c3a-168">**createAppendBlobFromStream** - maakt een nieuwe toevoeg-blob en uploadt Hallo inhoud van een stream</span><span class="sxs-lookup"><span data-stu-id="50c3a-168">**createAppendBlobFromStream** - creates a new append blob and uploads hello contents of a stream</span></span>
* <span data-ttu-id="50c3a-169">**createAppendBlobFromText** - maakt een nieuwe toevoeg-blob en uploadt Hallo inhoud van een tekenreeks</span><span class="sxs-lookup"><span data-stu-id="50c3a-169">**createAppendBlobFromText** - creates a new append blob and uploads hello contents of a string</span></span>
* <span data-ttu-id="50c3a-170">**createWriteStreamToNewAppendBlob** - maakt een nieuwe toevoeg-blob en geeft vervolgens een stroom toowrite tooit</span><span class="sxs-lookup"><span data-stu-id="50c3a-170">**createWriteStreamToNewAppendBlob** - creates a new append blob and then provides a stream toowrite tooit</span></span>

<span data-ttu-id="50c3a-171">Hallo volgende codevoorbeeld uploadt Hallo inhoud Hallo **test.txt** bestand naar **myappendblob**.</span><span class="sxs-lookup"><span data-stu-id="50c3a-171">hello following code example uploads hello contents of hello **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.createAppendBlobFromLocalFile('mycontainer', 'myappendblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="50c3a-172">tooappend een blok tooan bestaande toevoeg-blob, gebruik hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="50c3a-172">tooappend a block tooan existing append blob, use hello following:</span></span>

* <span data-ttu-id="50c3a-173">**appendFromLocalFile** -Hallo inhoud toevoegen van een bestand tooan bestaande toevoeg-blob</span><span class="sxs-lookup"><span data-stu-id="50c3a-173">**appendFromLocalFile** - append hello contents of a file tooan existing append blob</span></span>
* <span data-ttu-id="50c3a-174">**appendFromStream** -Hallo inhoud toevoegen van een stroom tooan bestaande toevoeg-blob</span><span class="sxs-lookup"><span data-stu-id="50c3a-174">**appendFromStream** - append hello contents of a stream tooan existing append blob</span></span>
* <span data-ttu-id="50c3a-175">**appendFromText** -Hallo inhoud toevoegen van een tekenreeks tooan bestaande toevoeg-blob</span><span class="sxs-lookup"><span data-stu-id="50c3a-175">**appendFromText** - append hello contents of a string tooan existing append blob</span></span>
* <span data-ttu-id="50c3a-176">**appendBlockFromStream** -Hallo inhoud toevoegen van een stroom tooan bestaande toevoeg-blob</span><span class="sxs-lookup"><span data-stu-id="50c3a-176">**appendBlockFromStream** - append hello contents of a stream tooan existing append blob</span></span>
* <span data-ttu-id="50c3a-177">**appendBlockFromText** -Hallo inhoud toevoegen van een tekenreeks tooan bestaande toevoeg-blob</span><span class="sxs-lookup"><span data-stu-id="50c3a-177">**appendBlockFromText** - append hello contents of a string tooan existing append blob</span></span>

> [!NOTE]
> <span data-ttu-id="50c3a-178">appendFromXXX API's worden sommige clientzijde validatie toofail snelle tooavoid onnodige server aanroepen doen.</span><span class="sxs-lookup"><span data-stu-id="50c3a-178">appendFromXXX APIs will do some client-side validation toofail fast tooavoid unnecessary server calls.</span></span> <span data-ttu-id="50c3a-179">appendBlockFromXXX niet het geval.</span><span class="sxs-lookup"><span data-stu-id="50c3a-179">appendBlockFromXXX won't.</span></span>
>
>

<span data-ttu-id="50c3a-180">Hallo volgende codevoorbeeld uploadt Hallo inhoud Hallo **test.txt** bestand naar **myappendblob**.</span><span class="sxs-lookup"><span data-stu-id="50c3a-180">hello following code example uploads hello contents of hello **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.appendFromText('mycontainer', 'myappendblob', 'text toobe appended', function(error, result, response){
  if(!error){
    // text appended
  }
});
```

### <a name="page-blobs"></a><span data-ttu-id="50c3a-181">Pagina-blobs</span><span class="sxs-lookup"><span data-stu-id="50c3a-181">Page blobs</span></span>
<span data-ttu-id="50c3a-182">tooupload gegevens tooa pagina-blob, gebruik hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="50c3a-182">tooupload data tooa page blob, use hello following:</span></span>

* <span data-ttu-id="50c3a-183">**createPageBlob** -maakt een nieuwe pagina-blob met een specifieke lengte</span><span class="sxs-lookup"><span data-stu-id="50c3a-183">**createPageBlob** - creates a new page blob of a specific length</span></span>
* <span data-ttu-id="50c3a-184">**createPageBlobFromLocalFile** - maakt een nieuwe pagina-blob en uploadt Hallo inhoud van een bestand</span><span class="sxs-lookup"><span data-stu-id="50c3a-184">**createPageBlobFromLocalFile** - creates a new page blob and uploads hello contents of a file</span></span>
* <span data-ttu-id="50c3a-185">**createPageBlobFromStream** - maakt een nieuwe pagina-blob en uploadt Hallo inhoud van een stream</span><span class="sxs-lookup"><span data-stu-id="50c3a-185">**createPageBlobFromStream** - creates a new page blob and uploads hello contents of a stream</span></span>
* <span data-ttu-id="50c3a-186">**createWriteStreamToExistingPageBlob** -biedt een schrijven stroom tooan bestaande pagina-blob</span><span class="sxs-lookup"><span data-stu-id="50c3a-186">**createWriteStreamToExistingPageBlob** - provides a write stream tooan existing page blob</span></span>
* <span data-ttu-id="50c3a-187">**createWriteStreamToNewPageBlob** - maakt een nieuwe pagina-blob en geeft vervolgens een stroom toowrite tooit</span><span class="sxs-lookup"><span data-stu-id="50c3a-187">**createWriteStreamToNewPageBlob** - creates a new page blob and then provides a stream toowrite tooit</span></span>

<span data-ttu-id="50c3a-188">Hallo volgende codevoorbeeld uploadt Hallo inhoud Hallo **test.txt** bestand naar **mypageblob**.</span><span class="sxs-lookup"><span data-stu-id="50c3a-188">hello following code example uploads hello contents of hello **test.txt** file into **mypageblob**.</span></span>

```nodejs
blobSvc.createPageBlobFromLocalFile('mycontainer', 'mypageblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

> [!NOTE]
> <span data-ttu-id="50c3a-189">Pagina-blobs bestaan uit 512-byte 'pages'.</span><span class="sxs-lookup"><span data-stu-id="50c3a-189">Page blobs consist of 512-byte 'pages'.</span></span> <span data-ttu-id="50c3a-190">U ontvangt een fout opgetreden tijdens het uploaden van gegevens met een grootte die is geen veelvoud van 512 bytes.</span><span class="sxs-lookup"><span data-stu-id="50c3a-190">You will receive an error when uploading data with a size that is not a multiple of 512.</span></span>
>
>

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="50c3a-191">Lijst Hallo blobs in een container</span><span class="sxs-lookup"><span data-stu-id="50c3a-191">List hello blobs in a container</span></span>
<span data-ttu-id="50c3a-192">toolist hello blobs in een container gebruiken Hallo **listBlobsSegmented** methode.</span><span class="sxs-lookup"><span data-stu-id="50c3a-192">toolist hello blobs in a container, use hello **listBlobsSegmented** method.</span></span> <span data-ttu-id="50c3a-193">Als u de blobs tooreturn met een specifieke voorvoegsel wilt, gebruik **listBlobsSegmentedWithPrefix**.</span><span class="sxs-lookup"><span data-stu-id="50c3a-193">If you'd like tooreturn blobs with a specific prefix, use **listBlobsSegmentedWithPrefix**.</span></span>

```nodejs
blobSvc.listBlobsSegmented('mycontainer', null, function(error, result, response){
  if(!error){
      // result.entries contains hello entries
      // If not all blobs were returned, result.continuationToken has hello continuation token.
  }
});
```

<span data-ttu-id="50c3a-194">Hallo `result` bevat een `entries` verzameling, die is een matrix met objecten die een beschrijving van elke blob.</span><span class="sxs-lookup"><span data-stu-id="50c3a-194">hello `result` contains an `entries` collection, which is an array of objects that describe each blob.</span></span> <span data-ttu-id="50c3a-195">Als u alle blobs kunnen niet worden geretourneerd, Hallo `result` biedt ook een `continuationToken`, die u kunt als Hallo tweede parameter tooretrieve extra vermeldingen.</span><span class="sxs-lookup"><span data-stu-id="50c3a-195">If all blobs cannot be returned, hello `result` also provides a `continuationToken`, which you may use as hello second parameter tooretrieve additional entries.</span></span>

## <a name="download-blobs"></a><span data-ttu-id="50c3a-196">Blobs downloaden</span><span class="sxs-lookup"><span data-stu-id="50c3a-196">Download blobs</span></span>
<span data-ttu-id="50c3a-197">toodownload gegevens van een blob Hallo volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="50c3a-197">toodownload data from a blob, use hello following:</span></span>

* <span data-ttu-id="50c3a-198">**getBlobToLocalFile** -Hallo blob-inhoud toofile schrijft</span><span class="sxs-lookup"><span data-stu-id="50c3a-198">**getBlobToLocalFile** - writes hello blob contents toofile</span></span>
* <span data-ttu-id="50c3a-199">**getBlobToStream** -schrijft Hallo blob inhoud tooa stroom</span><span class="sxs-lookup"><span data-stu-id="50c3a-199">**getBlobToStream** - writes hello blob contents tooa stream</span></span>
* <span data-ttu-id="50c3a-200">**getBlobToText** -schrijft Hallo blob-inhoud tooa tekenreeks</span><span class="sxs-lookup"><span data-stu-id="50c3a-200">**getBlobToText** - writes hello blob contents tooa string</span></span>
* <span data-ttu-id="50c3a-201">**createReadStream** -biedt een tooread stroom van Hallo blob</span><span class="sxs-lookup"><span data-stu-id="50c3a-201">**createReadStream** - provides a stream tooread from hello blob</span></span>

<span data-ttu-id="50c3a-202">Hallo volgende voorbeeldcode laat zien met **getBlobToStream** toodownload Hallo inhoud Hallo **myblob** blob en sla het toohello **uitvoer.txt** bestand met behulp van een Stream:</span><span class="sxs-lookup"><span data-stu-id="50c3a-202">hello following code example demonstrates using **getBlobToStream** toodownload hello contents of hello **myblob** blob and store it toohello **output.txt** file by using a stream:</span></span>

```nodejs
var fs = require('fs');
blobSvc.getBlobToStream('mycontainer', 'myblob', fs.createWriteStream('output.txt'), function(error, result, response){
  if(!error){
    // blob retrieved
  }
});
```

<span data-ttu-id="50c3a-203">Hallo `result` bevat informatie over Hallo blob, met inbegrip van **ETag** informatie.</span><span class="sxs-lookup"><span data-stu-id="50c3a-203">hello `result` contains information about hello blob, including **ETag** information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="50c3a-204">Een blob verwijderen</span><span class="sxs-lookup"><span data-stu-id="50c3a-204">Delete a blob</span></span>
<span data-ttu-id="50c3a-205">Tenslotte toodelete een blob roept **deleteBlob**.</span><span class="sxs-lookup"><span data-stu-id="50c3a-205">Finally, toodelete a blob, call **deleteBlob**.</span></span> <span data-ttu-id="50c3a-206">Hallo met het volgende codevoorbeeld verwijderingen Hallo blob met de naam **myblob**.</span><span class="sxs-lookup"><span data-stu-id="50c3a-206">hello following code example deletes hello blob named **myblob**.</span></span>

```nodejs
blobSvc.deleteBlob(containerName, 'myblob', function(error, response){
  if(!error){
    // Blob has been deleted
  }
});
```

## <a name="concurrent-access"></a><span data-ttu-id="50c3a-207">Gelijktijdige toegang</span><span class="sxs-lookup"><span data-stu-id="50c3a-207">Concurrent access</span></span>
<span data-ttu-id="50c3a-208">toosupport gelijktijdige toegang tooa blob van meerdere clients of meerdere procesexemplaren, kunt u **ETags** of **leases**.</span><span class="sxs-lookup"><span data-stu-id="50c3a-208">toosupport concurrent access tooa blob from multiple clients or multiple process instances, you can use **ETags** or **leases**.</span></span>

* <span data-ttu-id="50c3a-209">**ETag** -biedt een manier toodetect die Hallo blob of de container is gewijzigd door een ander proces</span><span class="sxs-lookup"><span data-stu-id="50c3a-209">**Etag** - provides a way toodetect that hello blob or container has been modified by another process</span></span>
* <span data-ttu-id="50c3a-210">**Lease** : biedt een manier tooobtain exclusieve, verlengd, schrijven of verwijderen van toegang tooa blob voor een bepaalde periode</span><span class="sxs-lookup"><span data-stu-id="50c3a-210">**Lease** - provides a way tooobtain exclusive, renewable, write or delete access tooa blob for a period of time</span></span>

### <a name="etag"></a><span data-ttu-id="50c3a-211">ETag</span><span class="sxs-lookup"><span data-stu-id="50c3a-211">ETag</span></span>
<span data-ttu-id="50c3a-212">ETags gebruiken als u meerdere clients of exemplaren toowrite toohello blok Blob of pagina-Blob tegelijkertijd tooallow nodig.</span><span class="sxs-lookup"><span data-stu-id="50c3a-212">Use ETags if you need tooallow multiple clients or instances toowrite toohello block Blob or page Blob simultaneously.</span></span> <span data-ttu-id="50c3a-213">Hallo kunt ETag u toodetermine als hello container of blob is gewijzigd, omdat u in eerste instantie lezen of deze is gemaakt, zodat u tooavoid overschrijven wijzigingen doorgevoerd door een andere client of een ander proces.</span><span class="sxs-lookup"><span data-stu-id="50c3a-213">hello ETag allows you toodetermine if hello container or blob was modified since you initially read or created it, which allows you tooavoid overwriting changes committed by another client or process.</span></span>

<span data-ttu-id="50c3a-214">U kunt voorwaarden ETag instellen via Hallo optionele `options.accessConditions` parameter.</span><span class="sxs-lookup"><span data-stu-id="50c3a-214">You can set ETag conditions by using hello optional `options.accessConditions` parameter.</span></span> <span data-ttu-id="50c3a-215">Hallo volgende codevoorbeeld alleen uploadt Hallo **test.txt** bestand als Hallo blob bestaat al en ETag-waarde Hallo is opgenomen door `etagToMatch`.</span><span class="sxs-lookup"><span data-stu-id="50c3a-215">hello following code example only uploads hello **test.txt** file if hello blob already exists and has hello ETag value contained by `etagToMatch`.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', { accessConditions: { EtagMatch: etagToMatch} }, function(error, result, response){
    if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="50c3a-216">Wanneer u ETags gebruikt, is het Hallo algemene patroon:</span><span class="sxs-lookup"><span data-stu-id="50c3a-216">When you're using ETags, hello general pattern is:</span></span>

1. <span data-ttu-id="50c3a-217">Hallo ETag verkrijgen als resultaat Hallo van maken, lijst of get-bewerking.</span><span class="sxs-lookup"><span data-stu-id="50c3a-217">Obtain hello ETag as hello result of a create, list, or get operation.</span></span>
2. <span data-ttu-id="50c3a-218">Een actie uitgevoerd, controleren dat die Hallo ETag-waarde is niet gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="50c3a-218">Perform an action, checking that hello ETag value has not been modified.</span></span>

<span data-ttu-id="50c3a-219">Als het Hallo-waarde is gewijzigd, betekent dit dat een andere client of exemplaar gewijzigd Hallo blob of container nadat u hebt verkregen Hallo ETag-waarde.</span><span class="sxs-lookup"><span data-stu-id="50c3a-219">If hello value was modified, this indicates that another client or instance modified hello blob or container since you obtained hello ETag value.</span></span>

### <a name="lease"></a><span data-ttu-id="50c3a-220">Lease</span><span class="sxs-lookup"><span data-stu-id="50c3a-220">Lease</span></span>
<span data-ttu-id="50c3a-221">U kunt een nieuwe lease verkrijgen met behulp van Hallo **acquireLease** methode Hallo blob of de container die u wilt dat tooobtain een lease op te geven.</span><span class="sxs-lookup"><span data-stu-id="50c3a-221">You can acquire a new lease by using hello **acquireLease** method, specifying hello blob or container that you wish tooobtain a lease on.</span></span> <span data-ttu-id="50c3a-222">Bijvoorbeeld, Hallo code na een lease verkrijgt op **myblob**.</span><span class="sxs-lookup"><span data-stu-id="50c3a-222">For example, hello following code acquires a lease on **myblob**.</span></span>

```nodejs
blobSvc.acquireLease('mycontainer', 'myblob', function(error, result, response){
  if(!error) {
    console.log('leaseId: ' + result.id);
  }
});
```

<span data-ttu-id="50c3a-223">Verdere bewerkingen op **myblob** Hallo moet opgeven `options.leaseId` parameter.</span><span class="sxs-lookup"><span data-stu-id="50c3a-223">Subsequent operations on **myblob** must provide hello `options.leaseId` parameter.</span></span> <span data-ttu-id="50c3a-224">Hallo lease ID wordt geretourneerd als `result.id` van **acquireLease**.</span><span class="sxs-lookup"><span data-stu-id="50c3a-224">hello lease ID is returned as `result.id` from **acquireLease**.</span></span>

> [!NOTE]
> <span data-ttu-id="50c3a-225">Standaard is de leaseduur Hallo oneindig.</span><span class="sxs-lookup"><span data-stu-id="50c3a-225">By default, hello lease duration is infinite.</span></span> <span data-ttu-id="50c3a-226">U kunt een duur niet oneindig (tussen 15 en 60 seconden) opgeven door Hallo `options.leaseDuration` parameter.</span><span class="sxs-lookup"><span data-stu-id="50c3a-226">You can specify a non-infinite duration (between 15 and 60 seconds) by providing hello `options.leaseDuration` parameter.</span></span>
>
>

<span data-ttu-id="50c3a-227">gebruik van een lease tooremove **releaseLease**.</span><span class="sxs-lookup"><span data-stu-id="50c3a-227">tooremove a lease, use **releaseLease**.</span></span> <span data-ttu-id="50c3a-228">een lease toobreak maar te voorkomen dat anderen gebruik van een nieuwe lease totdat Hallo oorspronkelijke duur is verlopen, **breakLease**.</span><span class="sxs-lookup"><span data-stu-id="50c3a-228">toobreak a lease, but prevent others from obtaining a new lease until hello original duration has expired, use **breakLease**.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="50c3a-229">Werken met handtekeningen voor gedeelde toegang</span><span class="sxs-lookup"><span data-stu-id="50c3a-229">Work with shared access signatures</span></span>
<span data-ttu-id="50c3a-230">Shared access signatures (SAS) zijn een veilige manier tooprovide gedetailleerde toegang tooblobs en containers zonder dat de naam van het opslagaccount of sleutels.</span><span class="sxs-lookup"><span data-stu-id="50c3a-230">Shared access signatures (SAS) are a secure way tooprovide granular access tooblobs and containers without providing your storage account name or keys.</span></span> <span data-ttu-id="50c3a-231">Shared access signatures zijn vaak gebruikte tooprovide beperkte toegang tooyour gegevens, zoals het toestaan van een mobiele app tooaccess blobs.</span><span class="sxs-lookup"><span data-stu-id="50c3a-231">Shared access signatures are often used tooprovide limited access tooyour data, such as allowing a mobile app tooaccess blobs.</span></span>

> [!NOTE]
> <span data-ttu-id="50c3a-232">Terwijl u kunt ook tooblobs voor anonieme toegang toestaan, handtekeningen voor gedeelde toegang ervoor zorgen dat u toegang tot het tooprovide meer wordt beheerd, moet u Hallo SAS genereren.</span><span class="sxs-lookup"><span data-stu-id="50c3a-232">While you can also allow anonymous access tooblobs, shared access signatures allow you tooprovide more controlled access, as you must generate hello SAS.</span></span>
>
>

<span data-ttu-id="50c3a-233">Een vertrouwde toepassing zoals een cloud-gebaseerde service genereert handtekeningen voor gedeelde toegang met behulp van Hallo **generateSharedAccessSignature** Hallo **BlobService**, en biedt dit tooan niet vertrouwd of semi vertrouwde toepassing zoals een mobiele app.</span><span class="sxs-lookup"><span data-stu-id="50c3a-233">A trusted application such as a cloud-based service generates shared access signatures using hello **generateSharedAccessSignature** of hello **BlobService**, and provides it tooan untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="50c3a-234">Gedeelde toegang handtekeningen worden gegenereerd op basis van beleid, waarin wordt beschreven Hallo start en einddatum tijdens welke Hallo handtekeningen voor gedeelde toegang geldig zijn, evenals Hallo toegang krijgen tot niveau toegekende toohello gedeelde toegang handtekeningen houder.</span><span class="sxs-lookup"><span data-stu-id="50c3a-234">Shared access signatures are generated using a policy, which describes hello start and end dates during which hello shared access signatures are valid, as well as hello access level granted toohello shared access signatures holder.</span></span>

<span data-ttu-id="50c3a-235">Hallo volgende codevoorbeeld genereert een nieuw beleid voor gedeelde toegang waarmee Hallo shared access signatures houder tooperform leesbewerkingen op Hallo **myblob** blob en 100 minuten na aanmaak Hallo-tijd is verstreken.</span><span class="sxs-lookup"><span data-stu-id="50c3a-235">hello following code example generates a new shared access policy that allows hello shared access signatures holder tooperform read operations on hello **myblob** blob, and expires 100 minutes after hello time it is created.</span></span>

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
};

var blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', 'myblob', sharedAccessPolicy);
var host = blobSvc.host;
```

<span data-ttu-id="50c3a-236">Houd er rekening mee dat Hallo hostinformatie worden moet verstrekt, zoals vereist is wanneer Hallo shared access signatures houder ook tooaccess Hallo container probeert.</span><span class="sxs-lookup"><span data-stu-id="50c3a-236">Note that hello host information must be provided also, as it is required when hello shared access signatures holder attempts tooaccess hello container.</span></span>

<span data-ttu-id="50c3a-237">Hallo vervolgens clienttoepassing maakt gebruik van handtekeningen voor gedeelde toegang met **BlobServiceWithSAS** tooperform bewerkingen op Hallo blob.</span><span class="sxs-lookup"><span data-stu-id="50c3a-237">hello client application then uses shared access signatures with **BlobServiceWithSAS** tooperform operations against hello blob.</span></span> <span data-ttu-id="50c3a-238">Hallo volgende Hiermee haalt u informatie over **myblob**.</span><span class="sxs-lookup"><span data-stu-id="50c3a-238">hello following gets information about **myblob**.</span></span>

```nodejs
var sharedBlobSvc = azure.createBlobServiceWithSas(host, blobSAS);
sharedBlobSvc.getBlobProperties('mycontainer', 'myblob', function (error, result, response) {
  if(!error) {
    // retrieved info
  }
});
```

<span data-ttu-id="50c3a-239">Omdat de handtekeningen voor gedeelde Hallo toegang zijn gegenereerd met alleen-lezen toegang als wordt geprobeerd toomodify Hallo blob, wordt er een fout geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="50c3a-239">Since hello shared access signatures were generated with read-only access, if an attempt is made toomodify hello blob, an error will be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="50c3a-240">Toegangsbeheerlijsten</span><span class="sxs-lookup"><span data-stu-id="50c3a-240">Access control lists</span></span>
<span data-ttu-id="50c3a-241">U kunt ook een toegangsbeheerlijst (ACL) tooset Hallo toegangsbeleid voor toegangsbeheer voor SA's gebruiken.</span><span class="sxs-lookup"><span data-stu-id="50c3a-241">You can also use an access control list (ACL) tooset hello access policy for SAS.</span></span> <span data-ttu-id="50c3a-242">Dit is handig als u tooallow meerdere clients tooaccess een container wilt, maar verschillende toegangsbeleid voor elke client bieden.</span><span class="sxs-lookup"><span data-stu-id="50c3a-242">This is useful if you wish tooallow multiple clients tooaccess a container but provide different access policies for each client.</span></span>

<span data-ttu-id="50c3a-243">Een ACL die is geïmplementeerd met behulp van een matrix van toegangsbeleid, met een ID die is gekoppeld aan elk beleid.</span><span class="sxs-lookup"><span data-stu-id="50c3a-243">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="50c3a-244">Hallo volgende codevoorbeeld definieert twee beleidsregels, één voor 'gebruiker1' en één voor 'gebruiker2':</span><span class="sxs-lookup"><span data-stu-id="50c3a-244">hello following code example defines two policies, one for 'user1' and one for 'user2':</span></span>

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.WRITE,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

<span data-ttu-id="50c3a-245">Hallo volgende code voorbeeld opgehaald Hallo huidige ACL voor **mycontainer**, en wordt vervolgens toegevoegd Hallo nieuwe beleidsregels met behulp van **setBlobAcl**.</span><span class="sxs-lookup"><span data-stu-id="50c3a-245">hello following code example gets hello current ACL for **mycontainer**, and then adds hello new policies using **setBlobAcl**.</span></span> <span data-ttu-id="50c3a-246">Met deze aanpak kunt:</span><span class="sxs-lookup"><span data-stu-id="50c3a-246">This approach allows:</span></span>

```nodejs
var extend = require('extend');
blobSvc.getBlobAcl('mycontainer', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    blobSvc.setBlobAcl('mycontainer', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

<span data-ttu-id="50c3a-247">Eenmaal Hallo die ACL is ingesteld, kunt u vervolgens maken op basis van Hallo-ID voor een beleid handtekeningen voor gedeelde toegang.</span><span class="sxs-lookup"><span data-stu-id="50c3a-247">Once hello ACL is set, you can then create shared access signatures based on hello ID for a policy.</span></span> <span data-ttu-id="50c3a-248">Hallo volgende codevoorbeeld maakt nieuwe handtekeningen voor gedeelde toegang voor 'gebruiker2':</span><span class="sxs-lookup"><span data-stu-id="50c3a-248">hello following code example creates new shared access signatures for 'user2':</span></span>

```nodejs
blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="50c3a-249">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="50c3a-249">Next steps</span></span>
<span data-ttu-id="50c3a-250">Zie Hallo volgende bronnen voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="50c3a-250">For more information, see hello following resources.</span></span>

* <span data-ttu-id="50c3a-251">[Azure-opslag-SDK voor knooppunt API-referentiemateriaal][Azure Storage SDK for Node API Reference]</span><span class="sxs-lookup"><span data-stu-id="50c3a-251">[Azure Storage SDK for Node API Reference][Azure Storage SDK for Node API Reference]</span></span>
* <span data-ttu-id="50c3a-252">[Azure Storage-teamblog][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="50c3a-252">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>
* <span data-ttu-id="50c3a-253">[Azure-opslag-SDK voor knooppunt] [ Azure Storage SDK for Node] opslagplaats op GitHub</span><span class="sxs-lookup"><span data-stu-id="50c3a-253">[Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="50c3a-254">Node.js Developer Center</span><span class="sxs-lookup"><span data-stu-id="50c3a-254">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)
* [<span data-ttu-id="50c3a-255">Gegevensoverdracht met Hallo AzCopy-opdrachtregelprogramma</span><span class="sxs-lookup"><span data-stu-id="50c3a-255">Transfer data with hello AzCopy command-line utility</span></span>](storage-use-azcopy.md)

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node

[een Node.js-web-app maken in Azure App Service]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js web app met behulp van hello Azure Table-Service]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md
[bouwen en implementeren van een Node.js web-app tooAzure met behulp van Web Matrix]: ../app-service-web/web-sites-nodejs-use-webmatrix.md
[Using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure portal]: https://portal.azure.com
[bouwen en implementeren van een Node.js-toepassing tooan Azure Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Storage SDK for Node API Reference]: http://dl.windowsazure.com/nodestoragedocs/index.html
