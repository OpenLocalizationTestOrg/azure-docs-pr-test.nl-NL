---
title: aaaHow toouse Azure Table storage met Node.js | Microsoft Docs
description: Gestructureerde gegevens opslaan in Hallo cloud met Azure Table storage, een NoSQL-gegevensarchief.
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: fc2e33d2-c5da-4861-8503-53fdc25750de
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 990a71337b806d759d0277a7691712346db7b355
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-nodejs"></a><span data-ttu-id="19ae4-103">Hoe toouse Azure Table storage met Node.js</span><span class="sxs-lookup"><span data-stu-id="19ae4-103">How toouse Azure Table storage from Node.js</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="19ae4-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="19ae4-104">Overview</span></span>
<span data-ttu-id="19ae4-105">Dit onderwerp leest hoe tooperform algemene scenario's met behulp van hello Azure Table-service in een Node.js-toepassing.</span><span class="sxs-lookup"><span data-stu-id="19ae4-105">This topic shows how tooperform common scenarios using hello Azure Table service in a Node.js application.</span></span>

<span data-ttu-id="19ae4-106">Hallo-codevoorbeelden in dit onderwerp wordt ervan uitgegaan dat u hebt al een Node.js-toepassing.</span><span class="sxs-lookup"><span data-stu-id="19ae4-106">hello code examples in this topic assume you already have a Node.js application.</span></span> <span data-ttu-id="19ae4-107">Voor informatie over het toocreate een Node.js-toepassing in Azure, Zie een van de volgende onderwerpen:</span><span class="sxs-lookup"><span data-stu-id="19ae4-107">For information about how toocreate a Node.js application in Azure, see any of these topics:</span></span>

* [<span data-ttu-id="19ae4-108">Een Node.js-web-app maken in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="19ae4-108">Create a Node.js web app in Azure App Service</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="19ae4-109">Bouw en implementeer een Node.js web-app tooAzure met WebMatrix</span><span class="sxs-lookup"><span data-stu-id="19ae4-109">Build and deploy a Node.js web app tooAzure using WebMatrix</span></span>](../app-service-web/web-sites-nodejs-use-webmatrix.md)
* <span data-ttu-id="19ae4-110">[Bouw en implementeer een Node.js-toepassing tooan Azure Cloud Service](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (met behulp van Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="19ae4-110">[Build and deploy a Node.js application tooan Azure Cloud Service](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (using Windows PowerShell)</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="configure-your-application-tooaccess-azure-storage"></a><span data-ttu-id="19ae4-111">Configureren van uw toepassing tooaccess Azure Storage</span><span class="sxs-lookup"><span data-stu-id="19ae4-111">Configure your application tooaccess Azure Storage</span></span>
<span data-ttu-id="19ae4-112">toouse Azure Storage, moet u hello Azure-opslag-SDK voor Node.js, waaronder een set van gemak bibliotheken die met de Hallo storage REST-services communiceren.</span><span class="sxs-lookup"><span data-stu-id="19ae4-112">toouse Azure Storage, you need hello Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-node-package-manager-npm-tooinstall-hello-package"></a><span data-ttu-id="19ae4-113">Knooppunt Package Manager (NPM) tooinstall Hallo pakket gebruiken</span><span class="sxs-lookup"><span data-stu-id="19ae4-113">Use Node Package Manager (NPM) tooinstall hello package</span></span>
1. <span data-ttu-id="19ae4-114">Een opdrachtregelinterface gebruiken zoals **PowerShell** (Windows), **Terminal** (Mac) of **Bash** (Unix) en navigeer toohello map waar u uw toepassing hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="19ae4-114">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), and navigate toohello folder where you created your application.</span></span>
2. <span data-ttu-id="19ae4-115">Type **npm Installeer azure-opslag** in Hallo-opdrachtvenster.</span><span class="sxs-lookup"><span data-stu-id="19ae4-115">Type **npm install azure-storage** in hello command window.</span></span> <span data-ttu-id="19ae4-116">Uitvoer van de opdracht Hallo is vergelijkbaar toohello voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="19ae4-116">Output from hello command is similar toohello following example.</span></span>

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
3. <span data-ttu-id="19ae4-117">U kunt handmatig uitvoeren Hallo **ls** tooverify opdracht die een **knooppunt\_modules** map is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="19ae4-117">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="19ae4-118">In deze map vindt u Hallo **azure-opslag** , dit pakket bevat, moet u tooaccess opslag Hallo-bibliotheken.</span><span class="sxs-lookup"><span data-stu-id="19ae4-118">Inside that folder you will find hello **azure-storage** package, which contains hello libraries you need tooaccess storage.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="19ae4-119">Hallo-pakket importeren</span><span class="sxs-lookup"><span data-stu-id="19ae4-119">Import hello package</span></span>
<span data-ttu-id="19ae4-120">Toevoegen van de volgende code toohello bovenaan Hallo Hallo **server.js** bestand in uw toepassing:</span><span class="sxs-lookup"><span data-stu-id="19ae4-120">Add hello following code toohello top of hello **server.js** file in your application:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="19ae4-121">Een Azure Storage-verbinding instellen</span><span class="sxs-lookup"><span data-stu-id="19ae4-121">Set up an Azure Storage connection</span></span>
<span data-ttu-id="19ae4-122">Hello azure module lezen omgevingsvariabelen hello AZURE\_opslag\_ACCOUNT en AZURE\_opslag\_toegang\_sleutel of AZURE\_opslag\_verbinding \_Tekenreeks voor de vereiste informatie op tooconnect tooyour Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="19ae4-122">hello azure module will read hello environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="19ae4-123">Als deze omgevingsvariabelen zijn niet ingesteld, moet u de accountgegevens Hallo opgeven bij het aanroepen van **TableService**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-123">If these environment variables are not set, you must specify hello account information when calling **TableService**.</span></span>

<span data-ttu-id="19ae4-124">Voor een voorbeeld van het Hallo-omgevingsvariabelen instellen in Hallo [Azure-portal](https://portal.azure.com) Zie voor een Azure-Website [Node.js web app met behulp van hello Azure Table-Service](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="19ae4-124">For an example of setting hello environment variables in hello [Azure portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using hello Azure Table Service](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span></span>

## <a name="create-a-table"></a><span data-ttu-id="19ae4-125">Een tabel maken</span><span class="sxs-lookup"><span data-stu-id="19ae4-125">Create a table</span></span>
<span data-ttu-id="19ae4-126">Hallo volgende code maakt een **TableService** object en gebruikt deze toocreate een nieuwe tabel.</span><span class="sxs-lookup"><span data-stu-id="19ae4-126">hello following code creates a **TableService** object and uses it toocreate a new table.</span></span> <span data-ttu-id="19ae4-127">Voeg de volgende Hallo aan de bovenkant Hallo van **server.js**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-127">Add hello following near hello top of **server.js**.</span></span>

```nodejs
var tableSvc = azure.createTableService();
```

<span data-ttu-id="19ae4-128">Hallo aanroep te**createTableIfNotExists** wordt een nieuwe tabel maken met de opgegeven naam Hallo als deze niet al bestaat.</span><span class="sxs-lookup"><span data-stu-id="19ae4-128">hello call too**createTableIfNotExists** will create a new table with hello specified name if it does not already exist.</span></span> <span data-ttu-id="19ae4-129">Hallo wordt volgende voorbeeld een nieuwe tabel MijnTabel "' als deze niet al bestaat:</span><span class="sxs-lookup"><span data-stu-id="19ae4-129">hello following example creates a new table named 'mytable' if it does not already exist:</span></span>

```nodejs
tableSvc.createTableIfNotExists('mytable', function(error, result, response){
  if(!error){
    // Table exists or created
  }
});
```

<span data-ttu-id="19ae4-130">Hallo `result.created` worden `true` als een nieuwe tabel is gemaakt, en `false` als Hallo tabel al bestaat.</span><span class="sxs-lookup"><span data-stu-id="19ae4-130">hello `result.created` will be `true` if a new table is created, and `false` if hello table already exists.</span></span> <span data-ttu-id="19ae4-131">Hallo `response` bevat informatie over het Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="19ae4-131">hello `response` will contain information about hello request.</span></span>

### <a name="filters"></a><span data-ttu-id="19ae4-132">Filters</span><span class="sxs-lookup"><span data-stu-id="19ae4-132">Filters</span></span>
<span data-ttu-id="19ae4-133">Optionele filteren bewerkingen kunnen worden toegepast toooperations uitgevoerd met behulp van **TableService**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-133">Optional filtering operations can be applied toooperations performed using **TableService**.</span></span> <span data-ttu-id="19ae4-134">Bewerkingen voor het filteren kunt opnemen logboekregistratie, automatisch opnieuw, enzovoort. Filters zijn objecten die een methode met Hallo handtekening te implementeren:</span><span class="sxs-lookup"><span data-stu-id="19ae4-134">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="19ae4-135">Hierna moet u de voorverwerking op Hallo aanvraag opties, moet Hallo-methode toocall 'volgende' doorgeven van een retouraanroep Hello handtekening te volgen:</span><span class="sxs-lookup"><span data-stu-id="19ae4-135">After doing its preprocessing on hello request options, hello method needs toocall "next", passing a callback with hello following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="19ae4-136">In deze retouraanroep en na het verwerken van Hallo returnObject (Hallo reactie van Hallo aanvraag toohello server), Hallo callback tooeither moet vervolgens worden aangeroepen als deze bestaat toocontinue verwerking van andere filters of gewoon finalCallback-aanroep anders tooend Hallo het aanroepen van de service.</span><span class="sxs-lookup"><span data-stu-id="19ae4-136">In this callback, and after processing hello returnObject (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or simply invoke finalCallback otherwise tooend hello service invocation.</span></span>

<span data-ttu-id="19ae4-137">Twee filters die Pogingslogica implementeren zijn opgenomen in hello Azure SDK voor Node.js, **ExponentialRetryPolicyFilter** en **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-137">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="19ae4-138">Hallo volgende maakt een **TableService** object dat gebruikmaakt van Hallo **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="19ae4-138">hello following creates a **TableService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var tableSvc = azure.createTableService().withFilter(retryOperations);
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="19ae4-139">Een entiteit tooa tabel toevoegen</span><span class="sxs-lookup"><span data-stu-id="19ae4-139">Add an entity tooa table</span></span>
<span data-ttu-id="19ae4-140">tooadd een entiteit maakt eerst een object dat de entiteitseigenschappen van uw definieert.</span><span class="sxs-lookup"><span data-stu-id="19ae4-140">tooadd an entity, first create an object that defines your entity properties.</span></span> <span data-ttu-id="19ae4-141">Alle entiteiten moeten bevatten een **PartitionKey** en **RowKey**, die de unieke id's voor Hallo entiteit zijn.</span><span class="sxs-lookup"><span data-stu-id="19ae4-141">All entities must contain a **PartitionKey** and **RowKey**, which are unique identifiers for hello entity.</span></span>

* <span data-ttu-id="19ae4-142">**PartitionKey** -bepaalt Hallo partitie die de entiteit Hallo is opgeslagen in</span><span class="sxs-lookup"><span data-stu-id="19ae4-142">**PartitionKey** - determines hello partition that hello entity is stored in</span></span>
* <span data-ttu-id="19ae4-143">**RowKey** - unieke wijze identificeert Hallo entiteit binnen Hallo partitie</span><span class="sxs-lookup"><span data-stu-id="19ae4-143">**RowKey** - uniquely identifies hello entity within hello partition</span></span>

<span data-ttu-id="19ae4-144">Beide **PartitionKey** en **RowKey** moet tekenreekswaarden.</span><span class="sxs-lookup"><span data-stu-id="19ae4-144">Both **PartitionKey** and **RowKey** must be string values.</span></span> <span data-ttu-id="19ae4-145">Zie voor meer informatie [Understanding Hallo Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="19ae4-145">For more information, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="19ae4-146">Hallo Hieronder volgt een voorbeeld van het definiëren van een entiteit.</span><span class="sxs-lookup"><span data-stu-id="19ae4-146">hello following is an example of defining an entity.</span></span> <span data-ttu-id="19ae4-147">Houd er rekening mee dat **dueDate** is gedefinieerd als een soort **Edm.DateTime**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-147">Note that **dueDate** is defined as a type of **Edm.DateTime**.</span></span> <span data-ttu-id="19ae4-148">Geven Hallo-type is optioneel en typen zal worden afgeleid indien niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="19ae4-148">Specifying hello type is optional, and types will be inferred if not specified.</span></span>

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20), '$':'Edm.DateTime'}
};
```

> [!NOTE]
> <span data-ttu-id="19ae4-149">Er is ook een **tijdstempel** veld voor elke record, die door Azure wordt ingesteld wanneer een entiteit wordt ingevoegd of bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="19ae4-149">There is also a **Timestamp** field for each record, which is set by Azure when an entity is inserted or updated.</span></span>
>
>

<span data-ttu-id="19ae4-150">U kunt ook Hallo **entityGenerator** toocreate entiteiten.</span><span class="sxs-lookup"><span data-stu-id="19ae4-150">You can also use hello **entityGenerator** toocreate entities.</span></span> <span data-ttu-id="19ae4-151">Hallo volgende voorbeeld maakt Hallo dezelfde taak entiteit met Hallo **entityGenerator**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-151">hello following example creates hello same task entity using hello **entityGenerator**.</span></span>

```nodejs
var entGen = azure.TableUtilities.entityGenerator;
var task = {
  PartitionKey: entGen.String('hometasks'),
  RowKey: entGen.String('1'),
  description: entGen.String('take out hello trash'),
  dueDate: entGen.DateTime(new Date(Date.UTC(2015, 6, 20))),
};
```

<span data-ttu-id="19ae4-152">een tabel entity tooyour tooadd doorgeven Hallo entiteit object toohello **insertEntity** methode.</span><span class="sxs-lookup"><span data-stu-id="19ae4-152">tooadd an entity tooyour table, pass hello entity object toohello **insertEntity** method.</span></span>

```nodejs
tableSvc.insertEntity('mytable',task, function (error, result, response) {
  if(!error){
    // Entity inserted
  }
});
```

<span data-ttu-id="19ae4-153">Als Hallo-bewerking voltooid is, `result` bevat Hallo [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) Hallo ingevoegd record en `response` bevat informatie over het Hallo-bewerking.</span><span class="sxs-lookup"><span data-stu-id="19ae4-153">If hello operation is successful, `result` will contain hello [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) of hello inserted record and `response` will contain information about hello operation.</span></span>

<span data-ttu-id="19ae4-154">Voorbeeld van een antwoord:</span><span class="sxs-lookup"><span data-stu-id="19ae4-154">Example response:</span></span>

```nodejs
{ '.metadata': { etag: 'W/"datetime\'2015-02-25T01%3A22%3A22.5Z\'"' } }
```

> [!NOTE]
> <span data-ttu-id="19ae4-155">Standaard **insertEntity** resulteert niet in de entiteit ingevoegd Hallo als onderdeel van Hallo `response` informatie.</span><span class="sxs-lookup"><span data-stu-id="19ae4-155">By default, **insertEntity** does not return hello inserted entity as part of hello `response` information.</span></span> <span data-ttu-id="19ae4-156">Als u van plan bent andere bewerkingen uitvoert op deze entiteit of toocache Hallo informatie wilt, kan zijn nuttig toohave geretourneerd als onderdeel van Hallo `result`.</span><span class="sxs-lookup"><span data-stu-id="19ae4-156">If you plan on performing other operations on this entity, or wish toocache hello information, it can be useful toohave it returned as part of hello `result`.</span></span> <span data-ttu-id="19ae4-157">U kunt dit doen door in te schakelen **echoContent** als volgt:</span><span class="sxs-lookup"><span data-stu-id="19ae4-157">You can do this by enabling **echoContent** as follows:</span></span>
>
> `tableSvc.insertEntity('mytable', task, {echoContent: true}, function (error, result, response) {...}`
>
>

## <a name="update-an-entity"></a><span data-ttu-id="19ae4-158">Bijwerken van een entiteit</span><span class="sxs-lookup"><span data-stu-id="19ae4-158">Update an entity</span></span>
<span data-ttu-id="19ae4-159">Er zijn meerdere methoden beschikbaar tooupdate van een bestaande entiteit:</span><span class="sxs-lookup"><span data-stu-id="19ae4-159">There are multiple methods available tooupdate an existing entity:</span></span>

* <span data-ttu-id="19ae4-160">**replaceEntity** -updates van een bestaande entiteit door deze te vervangen</span><span class="sxs-lookup"><span data-stu-id="19ae4-160">**replaceEntity** - updates an existing entity by replacing it</span></span>
* <span data-ttu-id="19ae4-161">**mergeEntity** -updates van een bestaande entiteit door de nieuwe eigenschapswaarden samenvoegen in een bestaande Hallo-entiteit</span><span class="sxs-lookup"><span data-stu-id="19ae4-161">**mergeEntity** - updates an existing entity by merging new property values into hello existing entity</span></span>
* <span data-ttu-id="19ae4-162">**insertOrReplaceEntity** -updates van een bestaande entiteit door deze te vervangen.</span><span class="sxs-lookup"><span data-stu-id="19ae4-162">**insertOrReplaceEntity** - updates an existing entity by replacing it.</span></span> <span data-ttu-id="19ae4-163">Als er is geen entiteit bestaat, wordt een nieuwe ingevoegd</span><span class="sxs-lookup"><span data-stu-id="19ae4-163">If no entity exists, a new one will be inserted</span></span>
* <span data-ttu-id="19ae4-164">**insertOrMergeEntity** -updates van een bestaande entiteit door nieuwe eigenschapswaarden in Hallo bestaande samen te voegen.</span><span class="sxs-lookup"><span data-stu-id="19ae4-164">**insertOrMergeEntity** - updates an existing entity by merging new property values into hello existing.</span></span> <span data-ttu-id="19ae4-165">Als er is geen entiteit bestaat, wordt een nieuwe ingevoegd</span><span class="sxs-lookup"><span data-stu-id="19ae4-165">If no entity exists, a new one will be inserted</span></span>

<span data-ttu-id="19ae4-166">Hallo volgende voorbeeld ziet u het bijwerken van een entiteit met **replaceEntity**:</span><span class="sxs-lookup"><span data-stu-id="19ae4-166">hello following example demonstrates updating an entity using **replaceEntity**:</span></span>

```nodejs
tableSvc.replaceEntity('mytable', updatedTask, function(error, result, response){
  if(!error) {
    // Entity updated
  }
});
```

> [!NOTE]
> <span data-ttu-id="19ae4-167">Standaard wordt bijwerken van een entiteit niet gecontroleerd toosee als Hallo gegevens wordt bijgewerkt eerder is gewijzigd door een ander proces.</span><span class="sxs-lookup"><span data-stu-id="19ae4-167">By default, updating an entity does not check toosee if hello data being updated has previously been modified by another process.</span></span> <span data-ttu-id="19ae4-168">gelijktijdige toosupport-updates:</span><span class="sxs-lookup"><span data-stu-id="19ae4-168">toosupport concurrent updates:</span></span>
>
> 1. <span data-ttu-id="19ae4-169">Haal Hallo ETag van Hallo-object wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="19ae4-169">Get hello ETag of hello object being updated.</span></span> <span data-ttu-id="19ae4-170">Dit wordt geretourneerd als onderdeel van Hallo `response` voor elke entiteit-gerelateerde bewerking en kan worden opgehaald via `response['.metadata'].etag`.</span><span class="sxs-lookup"><span data-stu-id="19ae4-170">This is returned as part of hello `response` for any entity-related operation and can be retrieved through `response['.metadata'].etag`.</span></span>
> 2. <span data-ttu-id="19ae4-171">Bij het uitvoeren van een updatebewerking op een entiteit toevoegen Hallo ETag informatie die eerder werden nieuwe entiteit toohello opgehaald.</span><span class="sxs-lookup"><span data-stu-id="19ae4-171">When performing an update operation on an entity, add hello ETag information previously retrieved toohello new entity.</span></span> <span data-ttu-id="19ae4-172">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="19ae4-172">For example:</span></span>
>
>       <span data-ttu-id="19ae4-173">entity2 [.metadata] .etag = currentEtag;</span><span class="sxs-lookup"><span data-stu-id="19ae4-173">entity2['.metadata'].etag = currentEtag;</span></span>
> 3. <span data-ttu-id="19ae4-174">Hallo updatebewerking niet uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="19ae4-174">Perform hello update operation.</span></span> <span data-ttu-id="19ae4-175">Als Hallo entiteit is gewijzigd sinds u opgehaald Hallo ETag-waarde, zoals een ander exemplaar van uw toepassing een `error` wordt geretourneerd met de mededeling dat Hallo update voorwaarde die is opgegeven in Hallo-aanvraag is niet voldaan aan.</span><span class="sxs-lookup"><span data-stu-id="19ae4-175">If hello entity has been modified since you retrieved hello ETag value, such as another instance of your application, an `error` will be returned stating that hello update condition specified in hello request was not satisfied.</span></span>
>
>

<span data-ttu-id="19ae4-176">Met **replaceEntity** en **mergeEntity**als Hallo-entiteit die wordt bijgewerkt niet bestaat, Hallo updatebewerking zullen mislukken.</span><span class="sxs-lookup"><span data-stu-id="19ae4-176">With **replaceEntity** and **mergeEntity**, if hello entity that is being updated doesn't exist, then hello update operation will fail.</span></span> <span data-ttu-id="19ae4-177">Als u toostore een entiteit wenst ongeacht of deze al bestaat, Gebruik daarom **insertOrReplaceEntity** of **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-177">Therefore if you wish toostore an entity regardless of whether it already exists, use **insertOrReplaceEntity** or **insertOrMergeEntity**.</span></span>

<span data-ttu-id="19ae4-178">Hallo `result` voor geslaagde update bevat operations Hallo **Etag** Hallo bijgewerkt entiteit.</span><span class="sxs-lookup"><span data-stu-id="19ae4-178">hello `result` for successful update operations will contain hello **Etag** of hello updated entity.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="19ae4-179">Werken met groepen van entiteiten</span><span class="sxs-lookup"><span data-stu-id="19ae4-179">Work with groups of entities</span></span>
<span data-ttu-id="19ae4-180">Soms is het zin toosubmit meerdere bewerkingen samen in een batch-tooensure atomic verwerken door Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="19ae4-180">Sometimes it makes sense toosubmit multiple operations together in a batch tooensure atomic processing by hello server.</span></span> <span data-ttu-id="19ae4-181">tooaccomplish die gebruik Hallo **TableBatch** toocreate een batch klasse en gebruik vervolgens Hallo **executeBatch** methode van **TableService** tooperform Hallo operations batch verwerkt.</span><span class="sxs-lookup"><span data-stu-id="19ae4-181">tooaccomplish that, use hello **TableBatch** class toocreate a batch, and then use hello **executeBatch** method of **TableService** tooperform hello batched operations.</span></span>

 <span data-ttu-id="19ae4-182">Hallo volgende voorbeeld ziet u twee entiteiten in een batch te verzenden:</span><span class="sxs-lookup"><span data-stu-id="19ae4-182">hello following example demonstrates submitting two entities in a batch:</span></span>

```nodejs
var task1 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'Take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20)}
};
var task2 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '2'},
  description: {'_':'Wash hello dishes'},
  dueDate: {'_':new Date(2015, 6, 20)}
};

var batch = new azure.TableBatch();

batch.insertEntity(task1, {echoContent: true});
batch.insertEntity(task2, {echoContent: true});

tableSvc.executeBatch('mytable', batch, function (error, result, response) {
  if(!error) {
    // Batch completed
  }
});
```

<span data-ttu-id="19ae4-183">Voor een geslaagde batchbewerkingen, `result` bevat informatie voor elke bewerking in Hallo batch.</span><span class="sxs-lookup"><span data-stu-id="19ae4-183">For successful batch operations, `result` will contain information for each operation in hello batch.</span></span>

### <a name="work-with-batched-operations"></a><span data-ttu-id="19ae4-184">Werken met batchbewerkingen</span><span class="sxs-lookup"><span data-stu-id="19ae4-184">Work with batched operations</span></span>
<span data-ttu-id="19ae4-185">Bewerkingen toegevoegd tooa batch kan worden gecontroleerd door het bekijken van Hallo `operations` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="19ae4-185">Operations added tooa batch can be inspected by viewing hello `operations` property.</span></span> <span data-ttu-id="19ae4-186">U kunt ook Hallo methoden toowork met bewerkingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="19ae4-186">You can also use hello following methods toowork with operations:</span></span>

* <span data-ttu-id="19ae4-187">**Schakel** -Hiermee wist u alle bewerkingen van een batch</span><span class="sxs-lookup"><span data-stu-id="19ae4-187">**clear** - clears all operations from a batch</span></span>
* <span data-ttu-id="19ae4-188">**getOperations** -opgehaald van een bewerking van het Hallo-batch</span><span class="sxs-lookup"><span data-stu-id="19ae4-188">**getOperations** - gets an operation from hello batch</span></span>
* <span data-ttu-id="19ae4-189">**hasOperations** -retourneert true als Hallo batch bewerkingen bevat</span><span class="sxs-lookup"><span data-stu-id="19ae4-189">**hasOperations** - returns true if hello batch contains operations</span></span>
* <span data-ttu-id="19ae4-190">**removeOperations** -Hiermee verwijdert u een bewerking</span><span class="sxs-lookup"><span data-stu-id="19ae4-190">**removeOperations** - removes an operation</span></span>
* <span data-ttu-id="19ae4-191">**de grootte van** -retourneert het aantal bewerkingen in batch Hallo Hallo</span><span class="sxs-lookup"><span data-stu-id="19ae4-191">**size** - returns hello number of operations in hello batch</span></span>

## <a name="retrieve-an-entity-by-key"></a><span data-ttu-id="19ae4-192">Een entiteit sleutel ophalen</span><span class="sxs-lookup"><span data-stu-id="19ae4-192">Retrieve an entity by key</span></span>
<span data-ttu-id="19ae4-193">een specifieke entiteit op basis van Hallo tooreturn **PartitionKey** en **RowKey**, gebruik Hallo **retrieveEntity** methode.</span><span class="sxs-lookup"><span data-stu-id="19ae4-193">tooreturn a specific entity based on hello **PartitionKey** and **RowKey**, use hello **retrieveEntity** method.</span></span>

```nodejs
tableSvc.retrieveEntity('mytable', 'hometasks', '1', function(error, result, response){
  if(!error){
    // result contains hello entity
  }
});
```

<span data-ttu-id="19ae4-194">Zodra deze bewerking voltooid is, `result` Hallo entiteit bevat.</span><span class="sxs-lookup"><span data-stu-id="19ae4-194">Once this operation is complete, `result` will contain hello entity.</span></span>

## <a name="query-a-set-of-entities"></a><span data-ttu-id="19ae4-195">Query uitvoeren op een verzameling entiteiten</span><span class="sxs-lookup"><span data-stu-id="19ae4-195">Query a set of entities</span></span>
<span data-ttu-id="19ae4-196">een tabel tooquery gebruiken Hallo **TableQuery** toobuild van een query-expressie met behulp van de volgende componenten Hallo object:</span><span class="sxs-lookup"><span data-stu-id="19ae4-196">tooquery a table, use hello **TableQuery** object toobuild up a query expression using hello following clauses:</span></span>

* <span data-ttu-id="19ae4-197">**Selecteer** -Hallo velden toobe geretourneerde Hallo query</span><span class="sxs-lookup"><span data-stu-id="19ae4-197">**select** - hello fields toobe returned from hello query</span></span>
* <span data-ttu-id="19ae4-198">**waar** - hello waar component</span><span class="sxs-lookup"><span data-stu-id="19ae4-198">**where** - hello where clause</span></span>

  * <span data-ttu-id="19ae4-199">**en** - een `and` where-voorwaarde</span><span class="sxs-lookup"><span data-stu-id="19ae4-199">**and** - an `and` where condition</span></span>
  * <span data-ttu-id="19ae4-200">**of** - een `or` where-voorwaarde</span><span class="sxs-lookup"><span data-stu-id="19ae4-200">**or** - an `or` where condition</span></span>
* <span data-ttu-id="19ae4-201">**Top** -het aantal items toofetch Hallo</span><span class="sxs-lookup"><span data-stu-id="19ae4-201">**top** - hello number of items toofetch</span></span>

<span data-ttu-id="19ae4-202">Hallo wordt volgende voorbeeld een query die Hallo bovenste vijf items met een PartitionKey van 'hometasks' wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="19ae4-202">hello following example builds a query that will return hello top five items with a PartitionKey of 'hometasks'.</span></span>

```nodejs
var query = new azure.TableQuery()
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

<span data-ttu-id="19ae4-203">Aangezien **Selecteer** niet wordt gebruikt, alle velden worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="19ae4-203">Since **select** is not used, all fields will be returned.</span></span> <span data-ttu-id="19ae4-204">tooperform Hallo-query op een tabel, gebruik **queryEntities**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-204">tooperform hello query against a table, use **queryEntities**.</span></span> <span data-ttu-id="19ae4-205">Hallo volgende voorbeeld maakt gebruik van deze query tooreturn entiteiten from "MijnTabel".</span><span class="sxs-lookup"><span data-stu-id="19ae4-205">hello following example uses this query tooreturn entities from 'mytable'.</span></span>

```nodejs
tableSvc.queryEntities('mytable',query, null, function(error, result, response) {
  if(!error) {
    // query was successful
  }
});
```

<span data-ttu-id="19ae4-206">Als dit lukt, `result.entries` bevat een matrix van entiteiten die overeenkomen met Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="19ae4-206">If successful, `result.entries` will contain an array of entities that match hello query.</span></span> <span data-ttu-id="19ae4-207">Als het Hallo-query kan niet tooreturn is alle entiteiten `result.continuationToken` worden niet -*null* en kunnen worden gebruikt als de derde parameter van Hallo **queryEntities** tooretrieve meer resultaten.</span><span class="sxs-lookup"><span data-stu-id="19ae4-207">If hello query was unable tooreturn all entities, `result.continuationToken` will be non-*null* and can be used as hello third parameter of **queryEntities** tooretrieve more results.</span></span> <span data-ttu-id="19ae4-208">Gebruik voor de eerste query hello, *null* voor de derde parameter Hallo.</span><span class="sxs-lookup"><span data-stu-id="19ae4-208">For hello initial query, use *null* for hello third parameter.</span></span>

### <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="19ae4-209">Een query uitvoeren op een subset van entiteitseigenschappen</span><span class="sxs-lookup"><span data-stu-id="19ae4-209">Query a subset of entity properties</span></span>
<span data-ttu-id="19ae4-210">Een query tooa tabel ophalen slechts enkele velden van een entiteit.</span><span class="sxs-lookup"><span data-stu-id="19ae4-210">A query tooa table can retrieve just a few fields from an entity.</span></span>
<span data-ttu-id="19ae4-211">Dit verbruikt minder bandbreedte en kan de queryprestaties verbeteren, vooral bij grote entiteiten.</span><span class="sxs-lookup"><span data-stu-id="19ae4-211">This reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="19ae4-212">Gebruik Hallo **Selecteer** component en pass Hallo-namen van Hallo velden toobe geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="19ae4-212">Use hello **select** clause and pass hello names of hello fields toobe returned.</span></span> <span data-ttu-id="19ae4-213">Bijvoorbeeld: hello volgende query retourneert alleen Hallo **beschrijving** en **dueDate** velden.</span><span class="sxs-lookup"><span data-stu-id="19ae4-213">For example, hello following query will return only hello **description** and **dueDate** fields.</span></span>

```nodejs
var query = new azure.TableQuery()
  .select(['description', 'dueDate'])
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

## <a name="delete-an-entity"></a><span data-ttu-id="19ae4-214">Een entiteit verwijderen</span><span class="sxs-lookup"><span data-stu-id="19ae4-214">Delete an entity</span></span>
<span data-ttu-id="19ae4-215">U kunt een entiteit met behulp van de sleutels van de partitie en rij verwijderen.</span><span class="sxs-lookup"><span data-stu-id="19ae4-215">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="19ae4-216">In dit voorbeeld Hallo **task1** object bevat Hallo **RowKey** en **PartitionKey** waarden van Hallo entiteit toobe verwijderd.</span><span class="sxs-lookup"><span data-stu-id="19ae4-216">In this example, hello **task1** object contains hello **RowKey** and **PartitionKey** values of hello entity toobe deleted.</span></span> <span data-ttu-id="19ae4-217">Vervolgens Hallo-object toohello doorgegeven **deleteEntity** methode.</span><span class="sxs-lookup"><span data-stu-id="19ae4-217">Then hello object is passed toohello **deleteEntity** method.</span></span>

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'}
};

tableSvc.deleteEntity('mytable', task, function(error, response){
  if(!error) {
    // Entity deleted
  }
});
```

> [!NOTE]
> <span data-ttu-id="19ae4-218">Overweeg het gebruik van ETags bij het verwijderen van items, tooensure die Hallo item niet is gewijzigd door een ander proces.</span><span class="sxs-lookup"><span data-stu-id="19ae4-218">Consider using ETags when deleting items, tooensure that hello item hasn't been modified by another process.</span></span> <span data-ttu-id="19ae4-219">Zie [bijwerken van een entiteit](#update-an-entity) voor informatie over het gebruik van ETags.</span><span class="sxs-lookup"><span data-stu-id="19ae4-219">See [Update an entity](#update-an-entity) for information on using ETags.</span></span>
>
>

## <a name="delete-a-table"></a><span data-ttu-id="19ae4-220">Een tabel verwijderen</span><span class="sxs-lookup"><span data-stu-id="19ae4-220">Delete a table</span></span>
<span data-ttu-id="19ae4-221">Hallo volgende code wordt een tabel uit een opslagaccount verwijderd.</span><span class="sxs-lookup"><span data-stu-id="19ae4-221">hello following code deletes a table from a storage account.</span></span>

```nodejs
tableSvc.deleteTable('mytable', function(error, response){
    if(!error){
        // Table deleted
    }
});
```

<span data-ttu-id="19ae4-222">Als u niet zeker of Hallo tabel bestaat weet, gebruikt u **deleteTableIfExists**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-222">If you are uncertain whether hello table exists, use **deleteTableIfExists**.</span></span>

## <a name="use-continuation-tokens"></a><span data-ttu-id="19ae4-223">Voortzetting tokens gebruiken</span><span class="sxs-lookup"><span data-stu-id="19ae4-223">Use continuation tokens</span></span>
<span data-ttu-id="19ae4-224">Wanneer u in de tabellen voor grote hoeveelheden resultaten zoekt, zoekt u voortzetting tokens.</span><span class="sxs-lookup"><span data-stu-id="19ae4-224">When you are querying tables for large amounts of results, look for continuation tokens.</span></span> <span data-ttu-id="19ae4-225">Mogelijk zijn er grote hoeveelheden gegevens beschikbaar voor uw query dat u niet beseft waarschijnlijk als u niet toorecognize maken kan wanneer een vervolgtoken aanwezig is.</span><span class="sxs-lookup"><span data-stu-id="19ae4-225">There may be large amounts of data available for your query that you might not realize if you do not build toorecognize when a continuation token is present.</span></span>

<span data-ttu-id="19ae4-226">Hallo resultaten object geretourneerd tijdens het opvragen van entiteiten stelt een `continuationToken` eigenschap bij dergelijke token aanwezig is.</span><span class="sxs-lookup"><span data-stu-id="19ae4-226">hello results object returned during querying entities sets a `continuationToken` property when such a token is present.</span></span> <span data-ttu-id="19ae4-227">U kunt deze vervolgens gebruiken bij het uitvoeren van een query toocontinue toomove over Hallo partitie en tabel entiteiten.</span><span class="sxs-lookup"><span data-stu-id="19ae4-227">You can then use this when performing a query toocontinue toomove across hello partition and table entities.</span></span>

<span data-ttu-id="19ae4-228">Wanneer een query uitvoert, kan een parameter continuationToken tussen Hallo query objectexemplaar en Hallo callback-functie worden opgegeven:</span><span class="sxs-lookup"><span data-stu-id="19ae4-228">When querying, a continuationToken parameter may be provided between hello query object instance and hello callback function:</span></span>

```nodejs
var nextContinuationToken = null;
dc.table.queryEntities(tableName,
    query,
    nextContinuationToken,
    function (error, results) {
        if (error) throw error;

        // iterate through results.entries with results

        if (results.continuationToken) {
            nextContinuationToken = results.continuationToken;
        }

    });
```

<span data-ttu-id="19ae4-229">Als u Hallo inspecteren `continuationToken` object, vindt u eigenschappen zoals `nextPartitionKey`, `nextRowKey` en `targetLocation`, wat kan gebruikte tooiterate via alle Hallo resultaten zijn.</span><span class="sxs-lookup"><span data-stu-id="19ae4-229">If you inspect hello `continuationToken` object, you will find properties such as `nextPartitionKey`, `nextRowKey` and `targetLocation`, which can be used tooiterate through all hello results.</span></span>

<span data-ttu-id="19ae4-230">Er is een voorbeeld van een voortzetting binnen hello Azure Storage Node.js-opslagplaats op GitHub.</span><span class="sxs-lookup"><span data-stu-id="19ae4-230">There is also a continuation sample within hello Azure Storage Node.js repo on GitHub.</span></span> <span data-ttu-id="19ae4-231">Zoek naar `examples/samples/continuationsample.js`.</span><span class="sxs-lookup"><span data-stu-id="19ae4-231">Look for `examples/samples/continuationsample.js`.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="19ae4-232">Werken met handtekeningen voor gedeelde toegang</span><span class="sxs-lookup"><span data-stu-id="19ae4-232">Work with shared access signatures</span></span>
<span data-ttu-id="19ae4-233">Shared access signatures (SAS) zijn een veilige manier tooprovide gedetailleerde toegang tootables zonder dat de naam van het opslagaccount of sleutels.</span><span class="sxs-lookup"><span data-stu-id="19ae4-233">Shared access signatures (SAS) are a secure way tooprovide granular access tootables without providing your storage account name or keys.</span></span> <span data-ttu-id="19ae4-234">SAS zijn vaak gebruikte tooprovide beperkte toegang tooyour gegevens, zoals het toestaan van een mobiele app tooquery records.</span><span class="sxs-lookup"><span data-stu-id="19ae4-234">SAS are often used tooprovide limited access tooyour data, such as allowing a mobile app tooquery records.</span></span>

<span data-ttu-id="19ae4-235">Een vertrouwde toepassing zoals een cloud-gebaseerde service genereert een SAS met Hallo **generateSharedAccessSignature** Hallo **TableService**, en biedt dit tooan niet-vertrouwde of semi vertrouwde toepassing zoals een mobiele app.</span><span class="sxs-lookup"><span data-stu-id="19ae4-235">A trusted application such as a cloud-based service generates a SAS using hello **generateSharedAccessSignature** of hello **TableService**, and provides it tooan untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="19ae4-236">Hallo SAS is gegenereerd met behulp van een beleid, waarin wordt beschreven Hallo begin- en einddatums tijdens welke Hallo SAS geldig is, evenals Hallo toegang niveau toegekende toohello SAS-houder.</span><span class="sxs-lookup"><span data-stu-id="19ae4-236">hello SAS is generated using a policy, which describes hello start and end dates during which hello SAS is valid, as well as hello access level granted toohello SAS holder.</span></span>

<span data-ttu-id="19ae4-237">Hallo volgende voorbeeld genereert een nieuw beleid voor gedeelde toegang waarmee Hallo SAS houder tooquery (r) Hallo tabel en 100 minuten na aanmaak Hallo-tijd is verstreken.</span><span class="sxs-lookup"><span data-stu-id="19ae4-237">hello following example generates a new shared access policy that will allow hello SAS holder tooquery ('r') hello table, and expires 100 minutes after hello time it is created.</span></span>

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
};

var tableSAS = tableSvc.generateSharedAccessSignature('mytable', sharedAccessPolicy);
var host = tableSvc.host;
```

<span data-ttu-id="19ae4-238">Houd er rekening mee dat Hallo hostinformatie worden moet verstrekt, zoals vereist is wanneer Hallo SAS houder ook tooaccess Hallo tabel probeert.</span><span class="sxs-lookup"><span data-stu-id="19ae4-238">Note that hello host information must be provided also, as it is required when hello SAS holder attempts tooaccess hello table.</span></span>

<span data-ttu-id="19ae4-239">Hallo-clienttoepassing en gebruik Hallo SAS met **TableServiceWithSAS** tooperform bewerkingen op Hallo tabel.</span><span class="sxs-lookup"><span data-stu-id="19ae4-239">hello client application then uses hello SAS with **TableServiceWithSAS** tooperform operations against hello table.</span></span> <span data-ttu-id="19ae4-240">Hallo volgt verbindt toohello tabel en een query uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="19ae4-240">hello following example connects toohello table and performs a query.</span></span>

```nodejs
var sharedTableService = azure.createTableServiceWithSas(host, tableSAS);
var query = azure.TableQuery()
  .where('PartitionKey eq ?', 'hometasks');

sharedTableService.queryEntities(query, null, function(error, result, response) {
  if(!error) {
    // result contains hello entities
  }
});
```

<span data-ttu-id="19ae4-241">Aangezien hello SAS is gegenereerd met alleen query toegang als er een poging tooinsert, bijwerken of verwijderen van entiteiten zijn aangebracht, wordt een fout geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="19ae4-241">Since hello SAS was generated with only query access, if an attempt were made tooinsert, update, or delete entities, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="19ae4-242">Access Control Lists</span><span class="sxs-lookup"><span data-stu-id="19ae4-242">Access Control Lists</span></span>
<span data-ttu-id="19ae4-243">U kunt ook een lijst met ACL (Access Control) tooset Hallo-beleid gebruiken voor een SAS.</span><span class="sxs-lookup"><span data-stu-id="19ae4-243">You can also use an Access Control List (ACL) tooset hello access policy for a SAS.</span></span> <span data-ttu-id="19ae4-244">Dit is handig als u tooallow meerdere clients tooaccess Hallo tabel wilt, maar verschillende toegangsbeleid voor elke client bieden.</span><span class="sxs-lookup"><span data-stu-id="19ae4-244">This is useful if you wish tooallow multiple clients tooaccess hello table, but provide different access policies for each client.</span></span>

<span data-ttu-id="19ae4-245">Een ACL die is geïmplementeerd met behulp van een matrix van toegangsbeleid, met een ID die is gekoppeld aan elk beleid.</span><span class="sxs-lookup"><span data-stu-id="19ae4-245">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="19ae4-246">Hallo volgende voorbeeld definieert twee beleidsregels, één voor 'gebruiker1' en één voor 'gebruiker2':</span><span class="sxs-lookup"><span data-stu-id="19ae4-246">hello following example defines two policies, one for 'user1' and one for 'user2':</span></span>

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

<span data-ttu-id="19ae4-247">Hallo voorbeeld opgehaald na huidige ACL voor Hallo Hallo **hometasks** tabel en wordt vervolgens toegevoegd Hallo nieuwe beleidsregels met behulp van **setTableAcl**.</span><span class="sxs-lookup"><span data-stu-id="19ae4-247">hello following example gets hello current ACL for hello **hometasks** table, and then adds hello new policies using **setTableAcl**.</span></span> <span data-ttu-id="19ae4-248">Met deze aanpak kunt:</span><span class="sxs-lookup"><span data-stu-id="19ae4-248">This approach allows:</span></span>

```nodejs
var extend = require('extend');
tableSvc.getTableAcl('hometasks', function(error, result, response) {
if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    tableSvc.setTableAcl('hometasks', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

<span data-ttu-id="19ae4-249">Eenmaal Hallo die ACL is ingesteld, kunt u vervolgens maken een SAS op basis van Hallo-ID voor een beleid.</span><span class="sxs-lookup"><span data-stu-id="19ae4-249">Once hello ACL has been set, you can then create a SAS based on hello ID for a policy.</span></span> <span data-ttu-id="19ae4-250">Hallo volgende voorbeeld maakt een nieuwe SAS voor 'gebruiker2':</span><span class="sxs-lookup"><span data-stu-id="19ae4-250">hello following example creates a new SAS for 'user2':</span></span>

```nodejs
tableSAS = tableSvc.generateSharedAccessSignature('hometasks', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="19ae4-251">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="19ae4-251">Next steps</span></span>
<span data-ttu-id="19ae4-252">Zie Hallo volgende bronnen voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="19ae4-252">For more information, see hello following resources.</span></span>

* <span data-ttu-id="19ae4-253">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is een gratis, zelfstandige app van Microsoft waarmee u toowork visueel met Azure Storage-gegevens op Windows-, Mac OS- en Linux.</span><span class="sxs-lookup"><span data-stu-id="19ae4-253">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="19ae4-254">[Azure-opslag-SDK voor knooppunt](https://github.com/Azure/azure-storage-node) opslagplaats op GitHub.</span><span class="sxs-lookup"><span data-stu-id="19ae4-254">[Azure Storage SDK for Node](https://github.com/Azure/azure-storage-node) repository on GitHub.</span></span>
* [<span data-ttu-id="19ae4-255">Node.js Developer Center</span><span class="sxs-lookup"><span data-stu-id="19ae4-255">Node.js Developer Center</span></span>](/develop/nodejs/)
* [<span data-ttu-id="19ae4-256">Maken en implementeren van een Node.js-toepassing tooan Azure-website</span><span class="sxs-lookup"><span data-stu-id="19ae4-256">Create and deploy a Node.js application tooan Azure website</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)
