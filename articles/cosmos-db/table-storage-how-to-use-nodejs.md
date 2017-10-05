---
title: Hoe Azure Table storage gebruiken met Node.js | Microsoft Docs
description: Sla gestructureerde gegevens op in de cloud met Azure Table Storage, een oplossing voor NoSQL-gegevensopslag.
services: cosmos-db
documentationcenter: nodejs
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: fc2e33d2-c5da-4861-8503-53fdc25750de
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 539212c6abe7738c022d67245f8992516f0899ff
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-azure-table-storage-from-nodejs"></a><span data-ttu-id="1e47d-103">Hoe Azure Table storage gebruiken met Node.js</span><span class="sxs-lookup"><span data-stu-id="1e47d-103">How to use Azure Table storage from Node.js</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="1e47d-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="1e47d-104">Overview</span></span>
<span data-ttu-id="1e47d-105">Dit onderwerp leest hoe u veelvoorkomende scenario's met de Azure Table-service in een Node.js-toepassing uitvoert.</span><span class="sxs-lookup"><span data-stu-id="1e47d-105">This topic shows how to perform common scenarios using the Azure Table service in a Node.js application.</span></span>

<span data-ttu-id="1e47d-106">De codevoorbeelden in dit onderwerp wordt ervan uitgegaan dat u hebt al een Node.js-toepassing.</span><span class="sxs-lookup"><span data-stu-id="1e47d-106">The code examples in this topic assume you already have a Node.js application.</span></span> <span data-ttu-id="1e47d-107">Zie voor informatie over het maken van een Node.js-toepassing in Azure, een van de volgende onderwerpen:</span><span class="sxs-lookup"><span data-stu-id="1e47d-107">For information about how to create a Node.js application in Azure, see any of these topics:</span></span>

* [<span data-ttu-id="1e47d-108">Een Node.js-web-app maken in Azure App Service</span><span class="sxs-lookup"><span data-stu-id="1e47d-108">Create a Node.js web app in Azure App Service</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="1e47d-109">Bouwen en implementeren van een Node.js-web-app in Azure met WebMatrix</span><span class="sxs-lookup"><span data-stu-id="1e47d-109">Build and deploy a Node.js web app to Azure using WebMatrix</span></span>](../app-service-web/web-sites-nodejs-use-webmatrix.md)
* <span data-ttu-id="1e47d-110">[Bouw en implementeer een Node.js-toepassing naar een Azure Cloud Service](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (met behulp van Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="1e47d-110">[Build and deploy a Node.js application to an Azure Cloud Service](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (using Windows PowerShell)</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="configure-your-application-to-access-azure-storage"></a><span data-ttu-id="1e47d-111">Uw toepassing configureren voor toegang tot Azure Storage</span><span class="sxs-lookup"><span data-stu-id="1e47d-111">Configure your application to access Azure Storage</span></span>
<span data-ttu-id="1e47d-112">Voor het gebruik van Azure Storage, moet u de Azure-opslag-SDK voor Node.js, waaronder een set van gemak bibliotheken die met de storage REST-services communiceren.</span><span class="sxs-lookup"><span data-stu-id="1e47d-112">To use Azure Storage, you need the Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-node-package-manager-npm-to-install-the-package"></a><span data-ttu-id="1e47d-113">Knooppunt Package Manager (NPM) gebruiken voor het installeren van het pakket</span><span class="sxs-lookup"><span data-stu-id="1e47d-113">Use Node Package Manager (NPM) to install the package</span></span>
1. <span data-ttu-id="1e47d-114">Een opdrachtregelinterface gebruiken zoals **PowerShell** (Windows), **Terminal** (Mac) of **Bash** (Unix) en navigeer naar de map waar u uw toepassing hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1e47d-114">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), and navigate to the folder where you created your application.</span></span>
2. <span data-ttu-id="1e47d-115">Type **npm Installeer azure-opslag** in het opdrachtvenster.</span><span class="sxs-lookup"><span data-stu-id="1e47d-115">Type **npm install azure-storage** in the command window.</span></span> <span data-ttu-id="1e47d-116">Uitvoer van de opdracht is vergelijkbaar met het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="1e47d-116">Output from the command is similar to the following example.</span></span>

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
3. <span data-ttu-id="1e47d-117">U kunt handmatig uitvoeren de **ls** opdracht om te controleren of een **knooppunt\_modules** map is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="1e47d-117">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="1e47d-118">In deze map vindt u de **azure-opslag** , dit pakket bevat de bibliotheken die u moet toegang hebben tot opslag.</span><span class="sxs-lookup"><span data-stu-id="1e47d-118">Inside that folder you will find the **azure-storage** package, which contains the libraries you need to access storage.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="1e47d-119">Het pakket importeren</span><span class="sxs-lookup"><span data-stu-id="1e47d-119">Import the package</span></span>
<span data-ttu-id="1e47d-120">De volgende code toevoegen aan de bovenkant van de **server.js** bestand in uw toepassing:</span><span class="sxs-lookup"><span data-stu-id="1e47d-120">Add the following code to the top of the **server.js** file in your application:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="1e47d-121">Een Azure Storage-verbinding instellen</span><span class="sxs-lookup"><span data-stu-id="1e47d-121">Set up an Azure Storage connection</span></span>
<span data-ttu-id="1e47d-122">De azure-module leest de omgevingsvariabelen AZURE\_opslag\_ACCOUNT en AZURE\_opslag\_toegang\_sleutel of AZURE\_opslag\_verbinding\_tekenreeks voor de benodigde informatie om te verbinden met uw Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="1e47d-122">The azure module will read the environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="1e47d-123">Als deze omgevingsvariabelen zijn niet ingesteld, moet u de accountgegevens opgeven bij het aanroepen van **TableService**.</span><span class="sxs-lookup"><span data-stu-id="1e47d-123">If these environment variables are not set, you must specify the account information when calling **TableService**.</span></span>

<span data-ttu-id="1e47d-124">Voor een voorbeeld van de omgevingsvariabelen instellen in de [Azure-portal](https://portal.azure.com) Zie voor een Azure-Website [Node.js-web-app met behulp van de Service Azure-tabel](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="1e47d-124">For an example of setting the environment variables in the [Azure portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using the Azure Table Service](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span></span>

## <a name="create-a-table"></a><span data-ttu-id="1e47d-125">Een tabel maken</span><span class="sxs-lookup"><span data-stu-id="1e47d-125">Create a table</span></span>
<span data-ttu-id="1e47d-126">De volgende code maakt een **TableService** object en gebruikt deze om een nieuwe tabel maken.</span><span class="sxs-lookup"><span data-stu-id="1e47d-126">The following code creates a **TableService** object and uses it to create a new table.</span></span> <span data-ttu-id="1e47d-127">Voeg de volgende boven aan **server.js**.</span><span class="sxs-lookup"><span data-stu-id="1e47d-127">Add the following near the top of **server.js**.</span></span>

```nodejs
var tableSvc = azure.createTableService();
```

<span data-ttu-id="1e47d-128">De aanroep van **createTableIfNotExists** wordt een nieuwe tabel maken met de opgegeven naam als deze niet al bestaat.</span><span class="sxs-lookup"><span data-stu-id="1e47d-128">The call to **createTableIfNotExists** will create a new table with the specified name if it does not already exist.</span></span> <span data-ttu-id="1e47d-129">Het volgende voorbeeld wordt een nieuwe tabel MijnTabel "' als deze niet al bestaat:</span><span class="sxs-lookup"><span data-stu-id="1e47d-129">The following example creates a new table named 'mytable' if it does not already exist:</span></span>

```nodejs
tableSvc.createTableIfNotExists('mytable', function(error, result, response){
  if(!error){
    // Table exists or created
  }
});
```

<span data-ttu-id="1e47d-130">De `result.created` worden `true` als een nieuwe tabel is gemaakt, en `false` als de tabel al bestaat.</span><span class="sxs-lookup"><span data-stu-id="1e47d-130">The `result.created` will be `true` if a new table is created, and `false` if the table already exists.</span></span> <span data-ttu-id="1e47d-131">De `response` bevat informatie over de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="1e47d-131">The `response` will contain information about the request.</span></span>

### <a name="filters"></a><span data-ttu-id="1e47d-132">Filters</span><span class="sxs-lookup"><span data-stu-id="1e47d-132">Filters</span></span>
<span data-ttu-id="1e47d-133">Optionele filteren bewerkingen kunnen worden toegepast op de bewerkingen die worden uitgevoerd met behulp van **TableService**.</span><span class="sxs-lookup"><span data-stu-id="1e47d-133">Optional filtering operations can be applied to operations performed using **TableService**.</span></span> <span data-ttu-id="1e47d-134">Bewerkingen voor het filteren kunt opnemen logboekregistratie, automatisch opnieuw, enzovoort. Filters zijn objecten die een methode met de handtekening implementeren:</span><span class="sxs-lookup"><span data-stu-id="1e47d-134">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="1e47d-135">Hierna moet u de voorverwerking van de aanvraag-opties, de methode moet 'next', niet aanroepen voor het doorgeven van een retouraanroep met de volgende handtekening:</span><span class="sxs-lookup"><span data-stu-id="1e47d-135">After doing its preprocessing on the request options, the method needs to call "next", passing a callback with the following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="1e47d-136">In deze retouraanroep en na het verwerken van de returnObject (de reactie van de aanvraag naar de server), moet de callback volgende aanroepen als deze bestaat als u wilt doorgaan met het verwerken van andere filters of gewoon finalCallback anders om te beëindigen van de aanroep van de service aanroepen.</span><span class="sxs-lookup"><span data-stu-id="1e47d-136">In this callback, and after processing the returnObject (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or simply invoke finalCallback otherwise to end the service invocation.</span></span>

<span data-ttu-id="1e47d-137">Twee filters die Pogingslogica implementeren zijn opgenomen in de Azure SDK voor Node.js, **ExponentialRetryPolicyFilter** en **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="1e47d-137">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="1e47d-138">De volgende code maakt een **TableService** -object dat gebruikmaakt van de **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="1e47d-138">The following creates a **TableService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var tableSvc = azure.createTableService().withFilter(retryOperations);
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="1e47d-139">Een entiteit toevoegen aan een tabel</span><span class="sxs-lookup"><span data-stu-id="1e47d-139">Add an entity to a table</span></span>
<span data-ttu-id="1e47d-140">Als u wilt een entiteit toevoegen, moet u eerst een object dat de entiteitseigenschappen van uw bepaalt maken.</span><span class="sxs-lookup"><span data-stu-id="1e47d-140">To add an entity, first create an object that defines your entity properties.</span></span> <span data-ttu-id="1e47d-141">Alle entiteiten moeten bevatten een **PartitionKey** en **RowKey**, die de unieke id's voor de entiteit zijn.</span><span class="sxs-lookup"><span data-stu-id="1e47d-141">All entities must contain a **PartitionKey** and **RowKey**, which are unique identifiers for the entity.</span></span>

* <span data-ttu-id="1e47d-142">**PartitionKey** -bepaalt de partitie die de entiteit is opgeslagen in</span><span class="sxs-lookup"><span data-stu-id="1e47d-142">**PartitionKey** - determines the partition that the entity is stored in</span></span>
* <span data-ttu-id="1e47d-143">**RowKey** - unieke wijze identificeert de entiteit in de partitie</span><span class="sxs-lookup"><span data-stu-id="1e47d-143">**RowKey** - uniquely identifies the entity within the partition</span></span>

<span data-ttu-id="1e47d-144">Beide **PartitionKey** en **RowKey** moet tekenreekswaarden.</span><span class="sxs-lookup"><span data-stu-id="1e47d-144">Both **PartitionKey** and **RowKey** must be string values.</span></span> <span data-ttu-id="1e47d-145">Zie voor meer informatie [inzicht in de tabel Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="1e47d-145">For more information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="1e47d-146">Hier volgt een voorbeeld van het definiëren van een entiteit.</span><span class="sxs-lookup"><span data-stu-id="1e47d-146">The following is an example of defining an entity.</span></span> <span data-ttu-id="1e47d-147">Houd er rekening mee dat **dueDate** is gedefinieerd als een soort **Edm.DateTime**.</span><span class="sxs-lookup"><span data-stu-id="1e47d-147">Note that **dueDate** is defined as a type of **Edm.DateTime**.</span></span> <span data-ttu-id="1e47d-148">Op te geven is optioneel en typen zal worden afgeleid indien niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="1e47d-148">Specifying the type is optional, and types will be inferred if not specified.</span></span>

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'take out the trash'},
  dueDate: {'_':new Date(2015, 6, 20), '$':'Edm.DateTime'}
};
```

> [!NOTE]
> <span data-ttu-id="1e47d-149">Er is ook een **tijdstempel** veld voor elke record, die door Azure wordt ingesteld wanneer een entiteit wordt ingevoegd of bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="1e47d-149">There is also a **Timestamp** field for each record, which is set by Azure when an entity is inserted or updated.</span></span>
>
>

<span data-ttu-id="1e47d-150">U kunt ook de **entityGenerator** -entiteiten maken.</span><span class="sxs-lookup"><span data-stu-id="1e47d-150">You can also use the **entityGenerator** to create entities.</span></span> <span data-ttu-id="1e47d-151">Het volgende voorbeeld wordt de dezelfde taak entiteit met behulp van de **entityGenerator**.</span><span class="sxs-lookup"><span data-stu-id="1e47d-151">The following example creates the same task entity using the **entityGenerator**.</span></span>

```nodejs
var entGen = azure.TableUtilities.entityGenerator;
var task = {
  PartitionKey: entGen.String('hometasks'),
  RowKey: entGen.String('1'),
  description: entGen.String('take out the trash'),
  dueDate: entGen.DateTime(new Date(Date.UTC(2015, 6, 20))),
};
```

<span data-ttu-id="1e47d-152">Voor een entiteit toevoegen aan de tabel, geeft u de entiteitsobject aan de **insertEntity** methode.</span><span class="sxs-lookup"><span data-stu-id="1e47d-152">To add an entity to your table, pass the entity object to the **insertEntity** method.</span></span>

```nodejs
tableSvc.insertEntity('mytable',task, function (error, result, response) {
  if(!error){
    // Entity inserted
  }
});
```

<span data-ttu-id="1e47d-153">Als de bewerking voltooid is, `result` bevat de [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) van de ingevoegde record en `response` bevat informatie over het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="1e47d-153">If the operation is successful, `result` will contain the [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) of the inserted record and `response` will contain information about the operation.</span></span>

<span data-ttu-id="1e47d-154">Voorbeeld van een antwoord:</span><span class="sxs-lookup"><span data-stu-id="1e47d-154">Example response:</span></span>

```nodejs
{ '.metadata': { etag: 'W/"datetime\'2015-02-25T01%3A22%3A22.5Z\'"' } }
```

> [!NOTE]
> <span data-ttu-id="1e47d-155">Standaard **insertEntity** resulteert niet in de entiteit ingevoegd als onderdeel van de `response` informatie.</span><span class="sxs-lookup"><span data-stu-id="1e47d-155">By default, **insertEntity** does not return the inserted entity as part of the `response` information.</span></span> <span data-ttu-id="1e47d-156">Als u van plan bent andere bewerkingen uitvoert op deze entiteit of u wenst de informatie in de cache, kan het handig zijn om deze opgehaald als onderdeel van de `result`.</span><span class="sxs-lookup"><span data-stu-id="1e47d-156">If you plan on performing other operations on this entity, or wish to cache the information, it can be useful to have it returned as part of the `result`.</span></span> <span data-ttu-id="1e47d-157">U kunt dit doen door in te schakelen **echoContent** als volgt:</span><span class="sxs-lookup"><span data-stu-id="1e47d-157">You can do this by enabling **echoContent** as follows:</span></span>
>
> `tableSvc.insertEntity('mytable', task, {echoContent: true}, function (error, result, response) {...}`
>
>

## <a name="update-an-entity"></a><span data-ttu-id="1e47d-158">Bijwerken van een entiteit</span><span class="sxs-lookup"><span data-stu-id="1e47d-158">Update an entity</span></span>
<span data-ttu-id="1e47d-159">Er zijn meerdere methoden beschikbaar voor het bijwerken van een bestaande entiteit:</span><span class="sxs-lookup"><span data-stu-id="1e47d-159">There are multiple methods available to update an existing entity:</span></span>

* <span data-ttu-id="1e47d-160">**replaceEntity** -updates van een bestaande entiteit door deze te vervangen</span><span class="sxs-lookup"><span data-stu-id="1e47d-160">**replaceEntity** - updates an existing entity by replacing it</span></span>
* <span data-ttu-id="1e47d-161">**mergeEntity** -updates van een bestaande entiteit door de nieuwe eigenschapswaarden samenvoegt met de bestaande entiteit</span><span class="sxs-lookup"><span data-stu-id="1e47d-161">**mergeEntity** - updates an existing entity by merging new property values into the existing entity</span></span>
* <span data-ttu-id="1e47d-162">**insertOrReplaceEntity** -updates van een bestaande entiteit door deze te vervangen.</span><span class="sxs-lookup"><span data-stu-id="1e47d-162">**insertOrReplaceEntity** - updates an existing entity by replacing it.</span></span> <span data-ttu-id="1e47d-163">Als er is geen entiteit bestaat, wordt een nieuwe ingevoegd</span><span class="sxs-lookup"><span data-stu-id="1e47d-163">If no entity exists, a new one will be inserted</span></span>
* <span data-ttu-id="1e47d-164">**insertOrMergeEntity** -updates van een bestaande entiteit door nieuwe eigenschapswaarden in de bestaande samen te voegen.</span><span class="sxs-lookup"><span data-stu-id="1e47d-164">**insertOrMergeEntity** - updates an existing entity by merging new property values into the existing.</span></span> <span data-ttu-id="1e47d-165">Als er is geen entiteit bestaat, wordt een nieuwe ingevoegd</span><span class="sxs-lookup"><span data-stu-id="1e47d-165">If no entity exists, a new one will be inserted</span></span>

<span data-ttu-id="1e47d-166">Het volgende voorbeeld toont het bijwerken van een entiteit met **replaceEntity**:</span><span class="sxs-lookup"><span data-stu-id="1e47d-166">The following example demonstrates updating an entity using **replaceEntity**:</span></span>

```nodejs
tableSvc.replaceEntity('mytable', updatedTask, function(error, result, response){
  if(!error) {
    // Entity updated
  }
});
```

> [!NOTE]
> <span data-ttu-id="1e47d-167">Standaard wordt bijwerken van een entiteit niet gecontroleerd of de gegevens worden bijgewerkt eerder is gewijzigd door een ander proces.</span><span class="sxs-lookup"><span data-stu-id="1e47d-167">By default, updating an entity does not check to see if the data being updated has previously been modified by another process.</span></span> <span data-ttu-id="1e47d-168">Ter ondersteuning van gelijktijdige updates:</span><span class="sxs-lookup"><span data-stu-id="1e47d-168">To support concurrent updates:</span></span>
>
> 1. <span data-ttu-id="1e47d-169">Haal de ETag van het object wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="1e47d-169">Get the ETag of the object being updated.</span></span> <span data-ttu-id="1e47d-170">Dit wordt geretourneerd als onderdeel van de `response` voor elke entiteit-gerelateerde bewerking en kan worden opgehaald via `response['.metadata'].etag`.</span><span class="sxs-lookup"><span data-stu-id="1e47d-170">This is returned as part of the `response` for any entity-related operation and can be retrieved through `response['.metadata'].etag`.</span></span>
> 2. <span data-ttu-id="1e47d-171">Bij het uitvoeren van een updatebewerking op een entiteit toevoegen de ETag-informatie naar de nieuwe entiteit die eerder werden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="1e47d-171">When performing an update operation on an entity, add the ETag information previously retrieved to the new entity.</span></span> <span data-ttu-id="1e47d-172">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="1e47d-172">For example:</span></span>
>
>       <span data-ttu-id="1e47d-173">entity2 [.metadata] .etag = currentEtag;</span><span class="sxs-lookup"><span data-stu-id="1e47d-173">entity2['.metadata'].etag = currentEtag;</span></span>
> 3. <span data-ttu-id="1e47d-174">De updatebewerking niet uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="1e47d-174">Perform the update operation.</span></span> <span data-ttu-id="1e47d-175">Als de entiteit is gewijzigd sinds u de ETag-waarde opgehaald zoals een ander exemplaar van uw toepassing een `error` wordt geretourneerd met de mededeling dat de update-voorwaarde die is opgegeven in de aanvraag is niet voldaan aan.</span><span class="sxs-lookup"><span data-stu-id="1e47d-175">If the entity has been modified since you retrieved the ETag value, such as another instance of your application, an `error` will be returned stating that the update condition specified in the request was not satisfied.</span></span>
>
>

<span data-ttu-id="1e47d-176">Met **replaceEntity** en **mergeEntity**, als de entiteit die wordt bijgewerkt niet bestaat, mislukt de updatebewerking.</span><span class="sxs-lookup"><span data-stu-id="1e47d-176">With **replaceEntity** and **mergeEntity**, if the entity that is being updated doesn't exist, then the update operation will fail.</span></span> <span data-ttu-id="1e47d-177">Dus als u wilt opslaan van een entiteit ongeacht of deze al bestaat, gebruikt u **insertOrReplaceEntity** of **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="1e47d-177">Therefore if you wish to store an entity regardless of whether it already exists, use **insertOrReplaceEntity** or **insertOrMergeEntity**.</span></span>

<span data-ttu-id="1e47d-178">De `result` voor geslaagde update operations bevat de **Etag** van de bijgewerkte entiteit.</span><span class="sxs-lookup"><span data-stu-id="1e47d-178">The `result` for successful update operations will contain the **Etag** of the updated entity.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="1e47d-179">Werken met groepen van entiteiten</span><span class="sxs-lookup"><span data-stu-id="1e47d-179">Work with groups of entities</span></span>
<span data-ttu-id="1e47d-180">Soms is het zinvol verzenden meerdere bewerkingen samen in een batch om ervoor te zorgen atomic verwerking door de server.</span><span class="sxs-lookup"><span data-stu-id="1e47d-180">Sometimes it makes sense to submit multiple operations together in a batch to ensure atomic processing by the server.</span></span> <span data-ttu-id="1e47d-181">Gebruik hiertoe die de **TableBatch** klasse voor het maken van een batch en gebruik vervolgens de **executeBatch** methode van **TableService** de batch-bewerkingen uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="1e47d-181">To accomplish that, use the **TableBatch** class to create a batch, and then use the **executeBatch** method of **TableService** to perform the batched operations.</span></span>

 <span data-ttu-id="1e47d-182">Het volgende voorbeeld ziet u twee entiteiten in een batch te verzenden:</span><span class="sxs-lookup"><span data-stu-id="1e47d-182">The following example demonstrates submitting two entities in a batch:</span></span>

```nodejs
var task1 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'Take out the trash'},
  dueDate: {'_':new Date(2015, 6, 20)}
};
var task2 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '2'},
  description: {'_':'Wash the dishes'},
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

<span data-ttu-id="1e47d-183">Voor een geslaagde batchbewerkingen, `result` bevat informatie voor elke bewerking in de batch.</span><span class="sxs-lookup"><span data-stu-id="1e47d-183">For successful batch operations, `result` will contain information for each operation in the batch.</span></span>

### <a name="work-with-batched-operations"></a><span data-ttu-id="1e47d-184">Werken met batchbewerkingen</span><span class="sxs-lookup"><span data-stu-id="1e47d-184">Work with batched operations</span></span>
<span data-ttu-id="1e47d-185">Bewerkingen die zijn toegevoegd aan een batch kunnen worden gecontroleerd door de `operations` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="1e47d-185">Operations added to a batch can be inspected by viewing the `operations` property.</span></span> <span data-ttu-id="1e47d-186">U kunt ook de volgende methoden gebruiken om te werken met bewerkingen:</span><span class="sxs-lookup"><span data-stu-id="1e47d-186">You can also use the following methods to work with operations:</span></span>

* <span data-ttu-id="1e47d-187">**Schakel** -Hiermee wist u alle bewerkingen van een batch</span><span class="sxs-lookup"><span data-stu-id="1e47d-187">**clear** - clears all operations from a batch</span></span>
* <span data-ttu-id="1e47d-188">**getOperations** -krijgt een bewerking van de batch</span><span class="sxs-lookup"><span data-stu-id="1e47d-188">**getOperations** - gets an operation from the batch</span></span>
* <span data-ttu-id="1e47d-189">**hasOperations** -retourneert true als de batch bewerkingen bevat</span><span class="sxs-lookup"><span data-stu-id="1e47d-189">**hasOperations** - returns true if the batch contains operations</span></span>
* <span data-ttu-id="1e47d-190">**removeOperations** -Hiermee verwijdert u een bewerking</span><span class="sxs-lookup"><span data-stu-id="1e47d-190">**removeOperations** - removes an operation</span></span>
* <span data-ttu-id="1e47d-191">**de grootte van** -retourneert het aantal bewerkingen in de batch</span><span class="sxs-lookup"><span data-stu-id="1e47d-191">**size** - returns the number of operations in the batch</span></span>

## <a name="retrieve-an-entity-by-key"></a><span data-ttu-id="1e47d-192">Een entiteit sleutel ophalen</span><span class="sxs-lookup"><span data-stu-id="1e47d-192">Retrieve an entity by key</span></span>
<span data-ttu-id="1e47d-193">Om te retourneren van een specifieke entiteit op basis van de **PartitionKey** en **RowKey**, gebruiken de **retrieveEntity** methode.</span><span class="sxs-lookup"><span data-stu-id="1e47d-193">To return a specific entity based on the **PartitionKey** and **RowKey**, use the **retrieveEntity** method.</span></span>

```nodejs
tableSvc.retrieveEntity('mytable', 'hometasks', '1', function(error, result, response){
  if(!error){
    // result contains the entity
  }
});
```

<span data-ttu-id="1e47d-194">Zodra deze bewerking voltooid is, `result` de entiteit bevat.</span><span class="sxs-lookup"><span data-stu-id="1e47d-194">Once this operation is complete, `result` will contain the entity.</span></span>

## <a name="query-a-set-of-entities"></a><span data-ttu-id="1e47d-195">Query uitvoeren op een verzameling entiteiten</span><span class="sxs-lookup"><span data-stu-id="1e47d-195">Query a set of entities</span></span>
<span data-ttu-id="1e47d-196">Om te vragen een tabel, gebruikt u de **TableQuery** object voor het bouwen van een query-expressie met behulp van de volgende componenten:</span><span class="sxs-lookup"><span data-stu-id="1e47d-196">To query a table, use the **TableQuery** object to build up a query expression using the following clauses:</span></span>

* <span data-ttu-id="1e47d-197">**Selecteer** -de velden moeten worden geretourneerd van de query</span><span class="sxs-lookup"><span data-stu-id="1e47d-197">**select** - the fields to be returned from the query</span></span>
* <span data-ttu-id="1e47d-198">**waar** -where component</span><span class="sxs-lookup"><span data-stu-id="1e47d-198">**where** - the where clause</span></span>

  * <span data-ttu-id="1e47d-199">**en** - een `and` where-voorwaarde</span><span class="sxs-lookup"><span data-stu-id="1e47d-199">**and** - an `and` where condition</span></span>
  * <span data-ttu-id="1e47d-200">**of** - een `or` where-voorwaarde</span><span class="sxs-lookup"><span data-stu-id="1e47d-200">**or** - an `or` where condition</span></span>
* <span data-ttu-id="1e47d-201">**Top** -het aantal items ophalen</span><span class="sxs-lookup"><span data-stu-id="1e47d-201">**top** - the number of items to fetch</span></span>

<span data-ttu-id="1e47d-202">Het volgende voorbeeld wordt een query de bovenste vijf items met een PartitionKey van 'hometasks retourneert'.</span><span class="sxs-lookup"><span data-stu-id="1e47d-202">The following example builds a query that will return the top five items with a PartitionKey of 'hometasks'.</span></span>

```nodejs
var query = new azure.TableQuery()
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

<span data-ttu-id="1e47d-203">Aangezien **Selecteer** niet wordt gebruikt, alle velden worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="1e47d-203">Since **select** is not used, all fields will be returned.</span></span> <span data-ttu-id="1e47d-204">Als u wilt uitvoeren van de query op een tabel, **queryEntities**.</span><span class="sxs-lookup"><span data-stu-id="1e47d-204">To perform the query against a table, use **queryEntities**.</span></span> <span data-ttu-id="1e47d-205">Het volgende voorbeeld maakt gebruik van deze query retourneren van entiteiten op "MijnTabel".</span><span class="sxs-lookup"><span data-stu-id="1e47d-205">The following example uses this query to return entities from 'mytable'.</span></span>

```nodejs
tableSvc.queryEntities('mytable',query, null, function(error, result, response) {
  if(!error) {
    // query was successful
  }
});
```

<span data-ttu-id="1e47d-206">Als dit lukt, `result.entries` bevat een matrix van entiteiten die overeenkomen met de query.</span><span class="sxs-lookup"><span data-stu-id="1e47d-206">If successful, `result.entries` will contain an array of entities that match the query.</span></span> <span data-ttu-id="1e47d-207">Als de query kan niet alle entiteiten retourneren `result.continuationToken` worden niet -*null* en kan worden gebruikt als de derde parameter van **queryEntities** meer resultaten ophalen.</span><span class="sxs-lookup"><span data-stu-id="1e47d-207">If the query was unable to return all entities, `result.continuationToken` will be non-*null* and can be used as the third parameter of **queryEntities** to retrieve more results.</span></span> <span data-ttu-id="1e47d-208">Gebruik voor de eerste query *null* voor de derde parameter.</span><span class="sxs-lookup"><span data-stu-id="1e47d-208">For the initial query, use *null* for the third parameter.</span></span>

### <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="1e47d-209">Een query uitvoeren op een subset van entiteitseigenschappen</span><span class="sxs-lookup"><span data-stu-id="1e47d-209">Query a subset of entity properties</span></span>
<span data-ttu-id="1e47d-210">Een query naar een tabel ophalen slechts enkele velden van een entiteit.</span><span class="sxs-lookup"><span data-stu-id="1e47d-210">A query to a table can retrieve just a few fields from an entity.</span></span>
<span data-ttu-id="1e47d-211">Dit verbruikt minder bandbreedte en kan de queryprestaties verbeteren, vooral bij grote entiteiten.</span><span class="sxs-lookup"><span data-stu-id="1e47d-211">This reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="1e47d-212">Gebruik de **Selecteer** component en geef de namen van de velden moeten worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="1e47d-212">Use the **select** clause and pass the names of the fields to be returned.</span></span> <span data-ttu-id="1e47d-213">De volgende query wordt bijvoorbeeld alleen de **beschrijving** en **dueDate** velden.</span><span class="sxs-lookup"><span data-stu-id="1e47d-213">For example, the following query will return only the **description** and **dueDate** fields.</span></span>

```nodejs
var query = new azure.TableQuery()
  .select(['description', 'dueDate'])
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

## <a name="delete-an-entity"></a><span data-ttu-id="1e47d-214">Een entiteit verwijderen</span><span class="sxs-lookup"><span data-stu-id="1e47d-214">Delete an entity</span></span>
<span data-ttu-id="1e47d-215">U kunt een entiteit met behulp van de sleutels van de partitie en rij verwijderen.</span><span class="sxs-lookup"><span data-stu-id="1e47d-215">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="1e47d-216">In dit voorbeeld wordt de **task1** object bevat de **RowKey** en **PartitionKey** waarden van de entiteit moet worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="1e47d-216">In this example, the **task1** object contains the **RowKey** and **PartitionKey** values of the entity to be deleted.</span></span> <span data-ttu-id="1e47d-217">Klik in het object wordt doorgegeven aan de **deleteEntity** methode.</span><span class="sxs-lookup"><span data-stu-id="1e47d-217">Then the object is passed to the **deleteEntity** method.</span></span>

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
> <span data-ttu-id="1e47d-218">Overweeg het gebruik van ETags bij het verwijderen van items, om ervoor te zorgen dat het item niet is gewijzigd door een ander proces.</span><span class="sxs-lookup"><span data-stu-id="1e47d-218">Consider using ETags when deleting items, to ensure that the item hasn't been modified by another process.</span></span> <span data-ttu-id="1e47d-219">Zie [bijwerken van een entiteit](#update-an-entity) voor informatie over het gebruik van ETags.</span><span class="sxs-lookup"><span data-stu-id="1e47d-219">See [Update an entity](#update-an-entity) for information on using ETags.</span></span>
>
>

## <a name="delete-a-table"></a><span data-ttu-id="1e47d-220">Een tabel verwijderen</span><span class="sxs-lookup"><span data-stu-id="1e47d-220">Delete a table</span></span>
<span data-ttu-id="1e47d-221">De volgende code wordt een tabel uit een opslagaccount verwijderd.</span><span class="sxs-lookup"><span data-stu-id="1e47d-221">The following code deletes a table from a storage account.</span></span>

```nodejs
tableSvc.deleteTable('mytable', function(error, response){
    if(!error){
        // Table deleted
    }
});
```

<span data-ttu-id="1e47d-222">Als u niet zeker of de tabel bestaat weet, gebruikt u **deleteTableIfExists**.</span><span class="sxs-lookup"><span data-stu-id="1e47d-222">If you are uncertain whether the table exists, use **deleteTableIfExists**.</span></span>

## <a name="use-continuation-tokens"></a><span data-ttu-id="1e47d-223">Voortzetting tokens gebruiken</span><span class="sxs-lookup"><span data-stu-id="1e47d-223">Use continuation tokens</span></span>
<span data-ttu-id="1e47d-224">Wanneer u in de tabellen voor grote hoeveelheden resultaten zoekt, zoekt u voortzetting tokens.</span><span class="sxs-lookup"><span data-stu-id="1e47d-224">When you are querying tables for large amounts of results, look for continuation tokens.</span></span> <span data-ttu-id="1e47d-225">Mogelijk zijn er grote hoeveelheden gegevens beschikbaar voor uw query die u niet beseft waarschijnlijk als u niet bouwen wilt herkennen als een vervolgtoken aanwezig is.</span><span class="sxs-lookup"><span data-stu-id="1e47d-225">There may be large amounts of data available for your query that you might not realize if you do not build to recognize when a continuation token is present.</span></span>

<span data-ttu-id="1e47d-226">De resultaten object geretourneerd tijdens het opvragen van entiteiten stelt een `continuationToken` eigenschap bij dergelijke token aanwezig is.</span><span class="sxs-lookup"><span data-stu-id="1e47d-226">The results object returned during querying entities sets a `continuationToken` property when such a token is present.</span></span> <span data-ttu-id="1e47d-227">Vervolgens kunt u dit bij het uitvoeren van een query om te blijven over de partitie en tabel entiteiten verplaatst.</span><span class="sxs-lookup"><span data-stu-id="1e47d-227">You can then use this when performing a query to continue to move across the partition and table entities.</span></span>

<span data-ttu-id="1e47d-228">Wanneer een query uitvoert, kan een parameter continuationToken tussen het objectexemplaar query en de callback-functie worden opgegeven:</span><span class="sxs-lookup"><span data-stu-id="1e47d-228">When querying, a continuationToken parameter may be provided between the query object instance and the callback function:</span></span>

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

<span data-ttu-id="1e47d-229">Als u de `continuationToken` object, vindt u eigenschappen zoals `nextPartitionKey`, `nextRowKey` en `targetLocation`, die kan worden gebruikt voor alle resultaten doorlopen.</span><span class="sxs-lookup"><span data-stu-id="1e47d-229">If you inspect the `continuationToken` object, you will find properties such as `nextPartitionKey`, `nextRowKey` and `targetLocation`, which can be used to iterate through all the results.</span></span>

<span data-ttu-id="1e47d-230">Er is een voorbeeld van een voortzetting binnen de Azure Storage Node.js-opslagplaats op GitHub.</span><span class="sxs-lookup"><span data-stu-id="1e47d-230">There is also a continuation sample within the Azure Storage Node.js repo on GitHub.</span></span> <span data-ttu-id="1e47d-231">Zoek naar `examples/samples/continuationsample.js`.</span><span class="sxs-lookup"><span data-stu-id="1e47d-231">Look for `examples/samples/continuationsample.js`.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="1e47d-232">Werken met handtekeningen voor gedeelde toegang</span><span class="sxs-lookup"><span data-stu-id="1e47d-232">Work with shared access signatures</span></span>
<span data-ttu-id="1e47d-233">Shared access signatures (SAS) zijn geen veilige manier toegang te bieden gedetailleerde tot tabellen zonder dat de naam van het opslagaccount of sleutels.</span><span class="sxs-lookup"><span data-stu-id="1e47d-233">Shared access signatures (SAS) are a secure way to provide granular access to tables without providing your storage account name or keys.</span></span> <span data-ttu-id="1e47d-234">SAS worden vaak gebruikt voor beperkte toegang tot uw gegevens, zoals het toestaan van een mobiele app records wilt zoeken.</span><span class="sxs-lookup"><span data-stu-id="1e47d-234">SAS are often used to provide limited access to your data, such as allowing a mobile app to query records.</span></span>

<span data-ttu-id="1e47d-235">Een vertrouwde toepassing zoals een cloud-gebaseerde service genereert een SAS met de **generateSharedAccessSignature** van de **TableService**, en biedt dit aan een niet-vertrouwde of semi vertrouwde toepassing zoals een mobiele app.</span><span class="sxs-lookup"><span data-stu-id="1e47d-235">A trusted application such as a cloud-based service generates a SAS using the **generateSharedAccessSignature** of the **TableService**, and provides it to an untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="1e47d-236">De SAS is gegenereerd met een beleid in, die beschrijft de begin- en einddatums gedurende welke de SAS geldig is, evenals het toegangsniveau verleend aan de SAS-houder.</span><span class="sxs-lookup"><span data-stu-id="1e47d-236">The SAS is generated using a policy, which describes the start and end dates during which the SAS is valid, as well as the access level granted to the SAS holder.</span></span>

<span data-ttu-id="1e47d-237">Het volgende voorbeeld genereert een nieuw beleid voor gedeelde toegang die zorgen de SAS-houder aan query ('r') in de tabel dat ervoor en 100 minuten na het tijdstip waarop dat deze is gemaakt is verlopen.</span><span class="sxs-lookup"><span data-stu-id="1e47d-237">The following example generates a new shared access policy that will allow the SAS holder to query ('r') the table, and expires 100 minutes after the time it is created.</span></span>

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

<span data-ttu-id="1e47d-238">Houd er rekening mee dat de informatie over de host moet ook worden opgegeven als deze vereist is wanneer de SAS-houder probeert te krijgen van de tabel.</span><span class="sxs-lookup"><span data-stu-id="1e47d-238">Note that the host information must be provided also, as it is required when the SAS holder attempts to access the table.</span></span>

<span data-ttu-id="1e47d-239">Vervolgens kunt u de clienttoepassing gebruikmaakt van de SAS met **TableServiceWithSAS** bewerkingen op de tabel uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="1e47d-239">The client application then uses the SAS with **TableServiceWithSAS** to perform operations against the table.</span></span> <span data-ttu-id="1e47d-240">Het volgende voorbeeld maakt verbinding met de tabel en een query uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="1e47d-240">The following example connects to the table and performs a query.</span></span>

```nodejs
var sharedTableService = azure.createTableServiceWithSas(host, tableSAS);
var query = azure.TableQuery()
  .where('PartitionKey eq ?', 'hometasks');

sharedTableService.queryEntities(query, null, function(error, result, response) {
  if(!error) {
    // result contains the entities
  }
});
```

<span data-ttu-id="1e47d-241">Aangezien de SAS is gegenereerd met alleen query toegang als er een poging wilt invoegen, bijwerken of verwijderen van entiteiten zijn aangebracht, wordt een fout geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="1e47d-241">Since the SAS was generated with only query access, if an attempt were made to insert, update, or delete entities, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="1e47d-242">Access Control Lists</span><span class="sxs-lookup"><span data-stu-id="1e47d-242">Access Control Lists</span></span>
<span data-ttu-id="1e47d-243">U kunt ook een lijst met ACL (Access Control) het toegangsbeleid instellen voor een SAS.</span><span class="sxs-lookup"><span data-stu-id="1e47d-243">You can also use an Access Control List (ACL) to set the access policy for a SAS.</span></span> <span data-ttu-id="1e47d-244">Dit is handig als u toestaan dat meerdere clients toegang tot de tabel wilt, maar bieden verschillende toegangsbeleid voor elke client.</span><span class="sxs-lookup"><span data-stu-id="1e47d-244">This is useful if you wish to allow multiple clients to access the table, but provide different access policies for each client.</span></span>

<span data-ttu-id="1e47d-245">Een ACL die is geïmplementeerd met behulp van een matrix van toegangsbeleid, met een ID die is gekoppeld aan elk beleid.</span><span class="sxs-lookup"><span data-stu-id="1e47d-245">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="1e47d-246">Het volgende voorbeeld definieert twee beleidsregels, één voor 'gebruiker1' en één voor 'gebruiker2':</span><span class="sxs-lookup"><span data-stu-id="1e47d-246">The following example defines two policies, one for 'user1' and one for 'user2':</span></span>

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

<span data-ttu-id="1e47d-247">Het volgende voorbeeld wordt de huidige ACL voor de **hometasks** tabel en voegt vervolgens het nieuwe beleid met behulp van **setTableAcl**.</span><span class="sxs-lookup"><span data-stu-id="1e47d-247">The following example gets the current ACL for the **hometasks** table, and then adds the new policies using **setTableAcl**.</span></span> <span data-ttu-id="1e47d-248">Met deze aanpak kunt:</span><span class="sxs-lookup"><span data-stu-id="1e47d-248">This approach allows:</span></span>

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

<span data-ttu-id="1e47d-249">Als de ACL is ingesteld, kunt u vervolgens een SAS op basis van de ID voor een beleid maken.</span><span class="sxs-lookup"><span data-stu-id="1e47d-249">Once the ACL has been set, you can then create a SAS based on the ID for a policy.</span></span> <span data-ttu-id="1e47d-250">Het volgende voorbeeld wordt een nieuwe SAS voor 'gebruiker2':</span><span class="sxs-lookup"><span data-stu-id="1e47d-250">The following example creates a new SAS for 'user2':</span></span>

```nodejs
tableSAS = tableSvc.generateSharedAccessSignature('hometasks', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="1e47d-251">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1e47d-251">Next steps</span></span>
<span data-ttu-id="1e47d-252">Zie de volgende bronnen voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="1e47d-252">For more information, see the following resources.</span></span>

* <span data-ttu-id="1e47d-253">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is een gratis, zelfstandige app van Microsoft waarmee u visueel met Azure Storage-gegevens kunt werken in Windows, macOS en Linux.</span><span class="sxs-lookup"><span data-stu-id="1e47d-253">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="1e47d-254">[Azure-opslag-SDK voor knooppunt](https://github.com/Azure/azure-storage-node) opslagplaats op GitHub.</span><span class="sxs-lookup"><span data-stu-id="1e47d-254">[Azure Storage SDK for Node](https://github.com/Azure/azure-storage-node) repository on GitHub.</span></span>
* [<span data-ttu-id="1e47d-255">Node.js Developer Center</span><span class="sxs-lookup"><span data-stu-id="1e47d-255">Node.js Developer Center</span></span>](/develop/nodejs/)
* [<span data-ttu-id="1e47d-256">Maken en implementeren van een Node.js-toepassing naar een Azure-website</span><span class="sxs-lookup"><span data-stu-id="1e47d-256">Create and deploy a Node.js application to an Azure website</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)