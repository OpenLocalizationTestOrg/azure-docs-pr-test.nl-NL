---
title: aaaHow toouse Queue storage met Node.js | Microsoft Docs
description: Ontdek hoe toocreate toouse hello Azure Queue-service en delete-wachtrijen en invoegen, ophalen en verwijderen van berichten. Voorbeelden die zijn geschreven in Node.js.
services: storage
documentationcenter: nodejs
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: a8a92db0-4333-43dd-a116-28b3147ea401
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 7e9778da4efa69f2e9d8fd480b9b6f5ace85951e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-nodejs"></a><span data-ttu-id="98939-104">Hoe toouse Queue storage met Node.js</span><span class="sxs-lookup"><span data-stu-id="98939-104">How toouse Queue storage from Node.js</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="98939-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="98939-105">Overview</span></span>
<span data-ttu-id="98939-106">Deze handleiding wordt getoond hoe tooperform algemene scenario's met behulp van Microsoft Azure Queue-service Hallo.</span><span class="sxs-lookup"><span data-stu-id="98939-106">This guide shows you how tooperform common scenarios using hello Microsoft Azure Queue service.</span></span> <span data-ttu-id="98939-107">Hallo-voorbeelden zijn geschreven met behulp van Hallo Node.js-API.</span><span class="sxs-lookup"><span data-stu-id="98939-107">hello samples are written using hello Node.js API.</span></span> <span data-ttu-id="98939-108">Hallo scenario's worden behandeld: **invoegen**, **inspecteren**, **ophalen**, en **verwijderen** wachtrij berichten, evenals  **maken en verwijderen van wachtrijen**.</span><span class="sxs-lookup"><span data-stu-id="98939-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="98939-109">Een Node.js-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="98939-109">Create a Node.js Application</span></span>
<span data-ttu-id="98939-110">Maak een lege Node.js-toepassing.</span><span class="sxs-lookup"><span data-stu-id="98939-110">Create a blank Node.js application.</span></span> <span data-ttu-id="98939-111">Zie voor instructies over het maken van een Node.js-toepassing [een Node.js-web-app maken in Azure App Service](../../app-service-web/app-service-web-get-started-nodejs.md), [bouwen en implementeren van een Node.js-toepassing tooan Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) met Windows PowerShell of [ Bouw en implementeer een Node.js web-app tooAzure met behulp van Web Matrix](https://www.microsoft.com/web/webmatrix/).</span><span class="sxs-lookup"><span data-stu-id="98939-111">For instructions creating a Node.js application, see [Create a Node.js web app in Azure App Service](../../app-service-web/app-service-web-get-started-nodejs.md), [Build and deploy a Node.js application tooan Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) using Windows PowerShell, or [Build and deploy a Node.js web app tooAzure using Web Matrix](https://www.microsoft.com/web/webmatrix/).</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="98939-112">Uw toepassing tooAccess opslag configureren</span><span class="sxs-lookup"><span data-stu-id="98939-112">Configure Your Application tooAccess Storage</span></span>
<span data-ttu-id="98939-113">toouse Azure-opslag, moet u hello Azure-opslag-SDK voor Node.js, waaronder een set van gemak bibliotheken die met de Hallo storage REST-services communiceren.</span><span class="sxs-lookup"><span data-stu-id="98939-113">toouse Azure storage, you need hello Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="98939-114">Knooppunt Package Manager (NPM) tooobtain Hallo pakket gebruiken</span><span class="sxs-lookup"><span data-stu-id="98939-114">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="98939-115">Een opdrachtregelinterface gebruiken zoals **PowerShell** (Windows), **Terminal** (Mac), of **Bash** (Unix), gaat u toohello map waar u uw voorbeeldtoepassing hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="98939-115">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate toohello folder where you created your sample application.</span></span>
2. <span data-ttu-id="98939-116">Type **npm Installeer azure-opslag** in Hallo-opdrachtvenster.</span><span class="sxs-lookup"><span data-stu-id="98939-116">Type **npm install azure-storage** in hello command window.</span></span> <span data-ttu-id="98939-117">Uitvoer van de opdracht Hallo is vergelijkbaar toohello voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="98939-117">Output from hello command is similar toohello following example.</span></span>
 
    ```
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
    ```

3. <span data-ttu-id="98939-118">U kunt handmatig uitvoeren Hallo **ls** tooverify opdracht die een **knooppunt\_modules** map is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="98939-118">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="98939-119">In deze map vindt u Hallo **azure-opslag** , dit pakket bevat Hallo-bibliotheken die u moet toegang hebben tot opslag.</span><span class="sxs-lookup"><span data-stu-id="98939-119">Inside that folder you will find hello **azure-storage** package, which contains hello libraries you need to access storage.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="98939-120">Hallo-pakket importeren</span><span class="sxs-lookup"><span data-stu-id="98939-120">Import hello package</span></span>
<span data-ttu-id="98939-121">Hallo na toohello boven in Kladblok of een andere teksteditor toevoegen de **server.js** -bestand van de toepassing hello waar u van plan toouse opslag bent:</span><span class="sxs-lookup"><span data-stu-id="98939-121">Using Notepad or another text editor, add hello following toohello top the **server.js** file of hello application where you intend toouse storage:</span></span>

```
var azure = require('azure-storage');
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="98939-122">Een Azure-opslag-verbinding instellen</span><span class="sxs-lookup"><span data-stu-id="98939-122">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="98939-123">Hello azure module lezen omgevingsvariabelen hello AZURE\_opslag\_ACCOUNT en AZURE\_opslag\_toegang\_sleutel of AZURE\_opslag\_verbinding \_Tekenreeks voor de vereiste informatie op tooconnect tooyour Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="98939-123">hello azure module will read hello environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="98939-124">Als deze omgevingsvariabelen zijn niet ingesteld, moet u de accountgegevens Hallo opgeven bij het aanroepen van **createQueueService**.</span><span class="sxs-lookup"><span data-stu-id="98939-124">If these environment variables are not set, you must specify hello account information when calling **createQueueService**.</span></span>

<span data-ttu-id="98939-125">Voor een voorbeeld van het Hallo-omgevingsvariabelen instellen in Hallo [Azure Portal](https://portal.azure.com) Zie [Node.js web app met behulp van Azure Table Service Hallo] voor een Azure-Website.</span><span class="sxs-lookup"><span data-stu-id="98939-125">For an example of setting hello environment variables in hello [Azure Portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using hello Azure Table Service].</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="98939-126">Procedure: Een wachtrij maken</span><span class="sxs-lookup"><span data-stu-id="98939-126">How To: Create a Queue</span></span>
<span data-ttu-id="98939-127">Hallo volgende code maakt een **QueueService** object, waarmee u toowork met wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="98939-127">hello following code creates a **QueueService** object, which enables you toowork with queues.</span></span>

```
var queueSvc = azure.createQueueService();
```

<span data-ttu-id="98939-128">Gebruik Hallo **createQueueIfNotExists** methode, die de opgegeven wachtrij Hallo retourneert als dit al bestaat of maakt een nieuwe wachtrij met de opgegeven naam Hallo als deze niet al bestaat.</span><span class="sxs-lookup"><span data-stu-id="98939-128">Use hello **createQueueIfNotExists** method, which returns hello specified queue if it already exists or creates a new queue with hello specified name if it does not already exist.</span></span>

```
queueSvc.createQueueIfNotExists('myqueue', function(error, result, response){
  if(!error){
    // Queue created or exists
  }
});
```

<span data-ttu-id="98939-129">Als het Hallo-wachtrij is gemaakt, `result.created` is ingesteld op true.</span><span class="sxs-lookup"><span data-stu-id="98939-129">If hello queue is created, `result.created` is true.</span></span> <span data-ttu-id="98939-130">Als Hallo wachtrij bestaat, `result.created` is ingesteld op false.</span><span class="sxs-lookup"><span data-stu-id="98939-130">If hello queue exists, `result.created` is false.</span></span>

### <a name="filters"></a><span data-ttu-id="98939-131">Filters</span><span class="sxs-lookup"><span data-stu-id="98939-131">Filters</span></span>
<span data-ttu-id="98939-132">Optionele filteren bewerkingen kunnen worden toegepast toooperations uitgevoerd met behulp van **QueueService**.</span><span class="sxs-lookup"><span data-stu-id="98939-132">Optional filtering operations can be applied toooperations performed using **QueueService**.</span></span> <span data-ttu-id="98939-133">Bewerkingen voor het filteren kunt opnemen logboekregistratie, automatisch opnieuw, enzovoort. Filters zijn objecten die een methode met Hallo handtekening te implementeren:</span><span class="sxs-lookup"><span data-stu-id="98939-133">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```
function handle (requestOptions, next)
```

<span data-ttu-id="98939-134">Hallo-methode moet hierna moet u de voorverwerking op Hallo certificaataanvraagopties, toocall doorgeven van een retouraanroep 'volgende' Hello handtekening te volgen:</span><span class="sxs-lookup"><span data-stu-id="98939-134">After doing its preprocessing on hello request options, hello method needs toocall "next" passing a callback with hello following signature:</span></span>

```
function (returnObject, finalCallback, next)
```

<span data-ttu-id="98939-135">In deze retouraanroep en na het verwerken van Hallo returnObject (Hallo reactie van Hallo aanvraag toohello server), Hallo callback tooeither moet vervolgens worden aangeroepen als deze bestaat toocontinue verwerking van andere filters of gewoon finalCallback-aanroep anders tooend up Hallo het aanroepen van de service.</span><span class="sxs-lookup"><span data-stu-id="98939-135">In this callback, and after processing hello returnObject (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or simply invoke finalCallback otherwise tooend up hello service invocation.</span></span>

<span data-ttu-id="98939-136">Twee filters die Pogingslogica implementeren zijn opgenomen in hello Azure SDK voor Node.js, **ExponentialRetryPolicyFilter** en **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="98939-136">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="98939-137">Hallo volgende maakt een **QueueService** object dat gebruikmaakt van Hallo **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="98939-137">hello following creates a **QueueService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var queueSvc = azure.createQueueService().withFilter(retryOperations);
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="98939-138">Procedure: Een bericht in een wachtrij invoegen</span><span class="sxs-lookup"><span data-stu-id="98939-138">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="98939-139">een bericht in een wachtrij, gebruik Hallo tooinsert **createMessage** methode voor het maken van een nieuw bericht en deze wachtrij toohello toevoegen.</span><span class="sxs-lookup"><span data-stu-id="98939-139">tooinsert a message into a queue, use hello **createMessage** method to create a new message and add it toohello queue.</span></span>

```
queueSvc.createMessage('myqueue', "Hello world!", function(error, result, response){
  if(!error){
    // Message inserted
  }
});
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="98939-140">Procedure: Inspecteren Hallo het Volgendebericht</span><span class="sxs-lookup"><span data-stu-id="98939-140">How To: Peek at hello Next Message</span></span>
<span data-ttu-id="98939-141">U kunt bekijken van Hallo-bericht in Hallo begin van een wachtrij zonder het te verwijderen uit de wachtrij Hallo door aanroepen Hallo **peekMessages** methode.</span><span class="sxs-lookup"><span data-stu-id="98939-141">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peekMessages** method.</span></span> <span data-ttu-id="98939-142">Standaard **peekMessages** geeft een enkel bericht weer.</span><span class="sxs-lookup"><span data-stu-id="98939-142">By default, **peekMessages** peeks at a single message.</span></span>

```
queueSvc.peekMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
  }
});
```

<span data-ttu-id="98939-143">Hallo `result` Hallo-bericht bevat.</span><span class="sxs-lookup"><span data-stu-id="98939-143">hello `result` contains hello message.</span></span>

> [!NOTE]
> <span data-ttu-id="98939-144">Met behulp van **peekMessages** wanneer er geen berichten in wachtrij Hallo zijn niet retourneren een foutmelding, maar er zijn geen berichten worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="98939-144">Using **peekMessages** when there are no messages in hello queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-dequeue-hello-next-message"></a><span data-ttu-id="98939-145">Procedure: Hallo het Volgendebericht uit de wachtrij halen</span><span class="sxs-lookup"><span data-stu-id="98939-145">How To: Dequeue hello Next Message</span></span>
<span data-ttu-id="98939-146">Verwerken van een bericht is een proces in twee fasen:</span><span class="sxs-lookup"><span data-stu-id="98939-146">Processing a message is a two-stage process:</span></span>

1. <span data-ttu-id="98939-147">Hallo-bericht in wachtrij.</span><span class="sxs-lookup"><span data-stu-id="98939-147">Dequeue hello message.</span></span>
2. <span data-ttu-id="98939-148">Verwijder het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="98939-148">Delete hello message.</span></span>

<span data-ttu-id="98939-149">gebruik van een bericht toodequeue **getMessages**.</span><span class="sxs-lookup"><span data-stu-id="98939-149">toodequeue a message, use **getMessages**.</span></span> <span data-ttu-id="98939-150">Hierdoor Hallo-berichten in wachtrij Hallo onzichtbaar zodat er geen andere clients kunnen verwerken.</span><span class="sxs-lookup"><span data-stu-id="98939-150">This makes hello messages invisible in hello queue, so no other clients can process them.</span></span> <span data-ttu-id="98939-151">Wanneer een bericht is verwerkt door uw toepassing, aanroepen **deleteMessage** toodelete op Hallo wachtrij.</span><span class="sxs-lookup"><span data-stu-id="98939-151">Once your application has processed a message, call **deleteMessage** toodelete it from hello queue.</span></span> <span data-ttu-id="98939-152">Hallo volgende voorbeeld wordt een bericht en vervolgens wordt verwijderd:</span><span class="sxs-lookup"><span data-stu-id="98939-152">hello following example gets a message, then deletes it:</span></span>

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
    var message = result[0];
    queueSvc.deleteMessage('myqueue', message.messageId, message.popReceipt, function(error, response){
      if(!error){
        //message deleted
      }
    });
  }
});
```

> [!NOTE]
> <span data-ttu-id="98939-153">Standaard wordt een bericht alleen verborgen voor 30 seconden, waarna deze zichtbaar tooother clients.</span><span class="sxs-lookup"><span data-stu-id="98939-153">By default, a message is only hidden for 30 seconds, after which it is visible tooother clients.</span></span> <span data-ttu-id="98939-154">U kunt een andere waarde opgeven met behulp van `options.visibilityTimeout` met **getMessages**.</span><span class="sxs-lookup"><span data-stu-id="98939-154">You can specify a different value by using `options.visibilityTimeout` with **getMessages**.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="98939-155">Met behulp van **getMessages** wanneer er geen berichten in wachtrij Hallo zijn niet retourneren een foutmelding, maar er zijn geen berichten worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="98939-155">Using **getMessages** when there are no messages in hello queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="98939-156">Procedure: Hallo inhoud van een bericht in de wachtrij wijzigen</span><span class="sxs-lookup"><span data-stu-id="98939-156">How To: Change hello Contents of a Queued Message</span></span>
<span data-ttu-id="98939-157">U kunt inhoud van een bericht in-place aan Hallo wachtrij met Hallo wijzigen **updateMessage**.</span><span class="sxs-lookup"><span data-stu-id="98939-157">You can change hello contents of a message in-place in hello queue using **updateMessage**.</span></span> <span data-ttu-id="98939-158">Hallo updates Hallo voorbeeldtekst van een bericht te volgen:</span><span class="sxs-lookup"><span data-stu-id="98939-158">hello following example updates hello text of a message:</span></span>

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Got hello message
    var message = result[0];
    queueSvc.updateMessage('myqueue', message.messageId, message.popReceipt, 10, {messageText: 'new text'}, function(error, result, response){
      if(!error){
        // Message updated successfully
      }
    });
  }
});
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="98939-159">Procedure: Aanvullende opties voor waarbij berichten</span><span class="sxs-lookup"><span data-stu-id="98939-159">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="98939-160">Er zijn twee manieren u ophalen van berichten uit een wachtrij kunt aanpassen:</span><span class="sxs-lookup"><span data-stu-id="98939-160">There are two ways you can customize message retrieval from a queue:</span></span>

* <span data-ttu-id="98939-161">`options.numOfMessages`-Ophalen van een batch met berichten (omhoog too32.)</span><span class="sxs-lookup"><span data-stu-id="98939-161">`options.numOfMessages` - Retrieve a batch of messages (up too32.)</span></span>
* <span data-ttu-id="98939-162">`options.visibilityTimeout`-Er is een time-out voor onzichtbaarheid langer of korter zijn ingesteld.</span><span class="sxs-lookup"><span data-stu-id="98939-162">`options.visibilityTimeout` - Set a longer or shorter invisibility timeout.</span></span>

<span data-ttu-id="98939-163">Hallo volgende voorbeeld wordt Hallo **getMessages** methode tooget 15 berichten in één aanroep.</span><span class="sxs-lookup"><span data-stu-id="98939-163">hello following example uses hello **getMessages** method tooget 15 messages in one call.</span></span> <span data-ttu-id="98939-164">Vervolgens wordt verwerkt elke bericht met een for-lus.</span><span class="sxs-lookup"><span data-stu-id="98939-164">Then it processes each message using a for loop.</span></span> <span data-ttu-id="98939-165">Hallo onzichtbaarheid toofive minuten voor de time-out voor alle berichten die zijn geretourneerd door deze methode wordt ook ingesteld.</span><span class="sxs-lookup"><span data-stu-id="98939-165">It also sets hello invisibility timeout toofive minutes for all messages returned by this method.</span></span>

```
queueSvc.getMessages('myqueue', {numOfMessages: 15, visibilityTimeout: 5 * 60}, function(error, result, response){
  if(!error){
    // Messages retreived
    for(var index in result){
      // text is available in result[index].messageText
      var message = result[index];
      queueSvc.deleteMessage(queueName, message.messageId, message.popReceipt, function(error, response){
        if(!error){
          // Message deleted
        }
      });
    }
  }
});
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="98939-166">Procedure: Hallo wachtrijlengte ophalen</span><span class="sxs-lookup"><span data-stu-id="98939-166">How To: Get hello Queue Length</span></span>
<span data-ttu-id="98939-167">Hallo **getQueueMetadata** metagegevens over Hallo wachtrij, met inbegrip van de geschatte aantal berichten in wachtrij Hallo Hallo retourneert.</span><span class="sxs-lookup"><span data-stu-id="98939-167">hello **getQueueMetadata** returns metadata about hello queue, including hello approximate number of messages waiting in hello queue.</span></span>

```
queueSvc.getQueueMetadata('myqueue', function(error, result, response){
  if(!error){
    // Queue length is available in result.approximateMessageCount
  }
});
```

## <a name="how-to-list-queues"></a><span data-ttu-id="98939-168">Procedure: Lijst wachtrijen</span><span class="sxs-lookup"><span data-stu-id="98939-168">How To: List Queues</span></span>
<span data-ttu-id="98939-169">een lijst van wachtrijen, gebruik tooretrieve **listQueuesSegmented**.</span><span class="sxs-lookup"><span data-stu-id="98939-169">tooretrieve a list of queues, use **listQueuesSegmented**.</span></span> <span data-ttu-id="98939-170">tooretrieve een lijst gefilterd op een bepaald voorvoegsel, gebruikt u **listQueuesSegmentedWithPrefix**.</span><span class="sxs-lookup"><span data-stu-id="98939-170">tooretrieve a list filtered by a specific prefix, use **listQueuesSegmentedWithPrefix**.</span></span>

```
queueSvc.listQueuesSegmented(null, function(error, result, response){
  if(!error){
    // result.entries contains hello list of queues
  }
});
```

<span data-ttu-id="98939-171">Als alle wachtrijen kunnen niet worden geretourneerd, `result.continuationToken` kunnen worden gebruikt als eerste parameter van Hallo **listQueuesSegmented** of Hallo van de tweede parameter van **listQueuesSegmentedWithPrefix** tooretrieve meer resultaten.</span><span class="sxs-lookup"><span data-stu-id="98939-171">If all queues cannot be returned, `result.continuationToken` can be used as hello first parameter of **listQueuesSegmented** or hello second parameter of **listQueuesSegmentedWithPrefix** tooretrieve more results.</span></span>

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="98939-172">Procedure: Een wachtrij verwijderen</span><span class="sxs-lookup"><span data-stu-id="98939-172">How To: Delete a Queue</span></span>
<span data-ttu-id="98939-173">toodelete een wachtrij en alle Hallo-berichten die dit, neemt u contact de **deleteQueue** methode op Hallo wachtrij-object.</span><span class="sxs-lookup"><span data-stu-id="98939-173">toodelete a queue and all hello messages contained in it, call the **deleteQueue** method on hello queue object.</span></span>

```
queueSvc.deleteQueue(queueName, function(error, response){
  if(!error){
    // Queue has been deleted
  }
});
```

<span data-ttu-id="98939-174">alle berichten uit een wachtrij zonder te verwijderen, gebruikt u tooclear **clearMessages**.</span><span class="sxs-lookup"><span data-stu-id="98939-174">tooclear all messages from a queue without deleting it, use **clearMessages**.</span></span>

## <a name="how-to-work-with-shared-access-signatures"></a><span data-ttu-id="98939-175">How to: werken met handtekeningen voor gedeelde toegang</span><span class="sxs-lookup"><span data-stu-id="98939-175">How to: Work with Shared Access Signatures</span></span>
<span data-ttu-id="98939-176">Shared Access Signatures (SAS) zijn een veilige manier tooprovide gedetailleerde toegang tooqueues zonder dat de naam van het opslagaccount of sleutels.</span><span class="sxs-lookup"><span data-stu-id="98939-176">Shared Access Signatures (SAS) are a secure way tooprovide granular access tooqueues without providing your storage account name or keys.</span></span> <span data-ttu-id="98939-177">SAS zijn vaak gebruikte tooprovide beperkte toegang tooyour wachtrijen, zoals het toestaan van een mobiele app toosubmit berichten.</span><span class="sxs-lookup"><span data-stu-id="98939-177">SAS are often used tooprovide limited access tooyour queues, such as allowing a mobile app toosubmit messages.</span></span>

<span data-ttu-id="98939-178">Een vertrouwde toepassing zoals een cloud-gebaseerde service genereert een SAS met Hallo **generateSharedAccessSignature** Hallo **QueueService**, en biedt dit tooan niet-vertrouwde of semi vertrouwde toepassing.</span><span class="sxs-lookup"><span data-stu-id="98939-178">A trusted application such as a cloud-based service generates a SAS using hello **generateSharedAccessSignature** of hello **QueueService**, and provides it tooan untrusted or semi-trusted application.</span></span> <span data-ttu-id="98939-179">Bijvoorbeeld: een mobiele app.</span><span class="sxs-lookup"><span data-stu-id="98939-179">For example, a mobile app.</span></span> <span data-ttu-id="98939-180">Hallo SAS is gegenereerd met behulp van een beleid, waarin wordt beschreven Hallo begin- en einddatums tijdens welke Hallo SAS geldig is, evenals Hallo toegang niveau toegekende toohello SAS-houder.</span><span class="sxs-lookup"><span data-stu-id="98939-180">hello SAS is generated using a policy, which describes hello start and end dates during which hello SAS is valid, as well as hello access level granted toohello SAS holder.</span></span>

<span data-ttu-id="98939-181">Hallo volgt genereert een nieuw beleid voor gedeelde toegang waarmee Hallo SAS houder tooadd berichten toohello wachtrij en 100 minuten na aanmaak Hallo-tijd is verstreken.</span><span class="sxs-lookup"><span data-stu-id="98939-181">hello following example generates a new shared access policy that will allow hello SAS holder tooadd messages toohello queue, and expires 100 minutes after hello time it is created.</span></span>

```
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};

var queueSAS = queueSvc.generateSharedAccessSignature('myqueue', sharedAccessPolicy);
var host = queueSvc.host;
```

<span data-ttu-id="98939-182">Houd er rekening mee dat Hallo hostinformatie worden moet verstrekt, zoals vereist is wanneer Hallo SAS houder ook tooaccess Hallo wachtrij probeert.</span><span class="sxs-lookup"><span data-stu-id="98939-182">Note that hello host information must be provided also, as it is required when hello SAS holder attempts tooaccess hello queue.</span></span>

<span data-ttu-id="98939-183">Hallo-clienttoepassing en gebruik Hallo SAS met **QueueServiceWithSAS** tooperform bewerkingen op Hallo wachtrij.</span><span class="sxs-lookup"><span data-stu-id="98939-183">hello client application then uses hello SAS with **QueueServiceWithSAS** tooperform operations against hello queue.</span></span> <span data-ttu-id="98939-184">Hallo volgt verbindt toohello wachtrij en een bericht wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="98939-184">hello following example connects toohello queue and creates a message.</span></span>

```
var sharedQueueService = azure.createQueueServiceWithSas(host, queueSAS);
sharedQueueService.createMessage('myqueue', 'Hello world from SAS!', function(error, result, response){
  if(!error){
    //message added
  }
});
```

<span data-ttu-id="98939-185">Aangezien hello SAS is gegenereerd met de toegang voor toevoegen als een poging is gedaan tooread, bijwerken of verwijderen van berichten, wordt een fout geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="98939-185">Since hello SAS was generated with add access, if an attempt were made tooread, update or delete messages, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="98939-186">Toegangsbeheerlijsten</span><span class="sxs-lookup"><span data-stu-id="98939-186">Access control lists</span></span>
<span data-ttu-id="98939-187">U kunt ook een lijst met ACL (Access Control) tooset Hallo-beleid gebruiken voor een SAS.</span><span class="sxs-lookup"><span data-stu-id="98939-187">You can also use an Access Control List (ACL) tooset hello access policy for a SAS.</span></span> <span data-ttu-id="98939-188">Dit is handig als u tooallow meerdere clients tooaccess Hallo wachtrij wilt, maar verschillende toegangsbeleid voor elke client bieden.</span><span class="sxs-lookup"><span data-stu-id="98939-188">This is useful if you wish tooallow multiple clients tooaccess hello queue, but provide different access policies for each client.</span></span>

<span data-ttu-id="98939-189">Een ACL die is geïmplementeerd met behulp van een matrix van toegangsbeleid, met een ID die is gekoppeld aan elk beleid.</span><span class="sxs-lookup"><span data-stu-id="98939-189">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="98939-190">Hallo volgende voorbeeld definieert twee beleidsregels; een voor 'gebruiker1' en één voor 'gebruiker2':</span><span class="sxs-lookup"><span data-stu-id="98939-190">hello  following example defines two policies; one for 'user1' and one for 'user2':</span></span>

```
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.PROCESS,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.QueueUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

<span data-ttu-id="98939-191">Hallo volgende voorbeeld wordt de huidige ACL voor Hallo **rapportberichten**, voegt u vervolgens Hallo nieuwe beleidsregels met behulp van **setQueueAcl**.</span><span class="sxs-lookup"><span data-stu-id="98939-191">hello following example gets hello current ACL for **myqueue**, then adds hello new policies using **setQueueAcl**.</span></span> <span data-ttu-id="98939-192">Met deze aanpak kunt:</span><span class="sxs-lookup"><span data-stu-id="98939-192">This approach allows:</span></span>

```
var extend = require('extend');
queueSvc.getQueueAcl('myqueue', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    queueSvc.setQueueAcl('myqueue', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

<span data-ttu-id="98939-193">Eenmaal Hallo die ACL is ingesteld, kunt u vervolgens maken een SAS op basis van Hallo-ID voor een beleid.</span><span class="sxs-lookup"><span data-stu-id="98939-193">Once hello ACL has been set, you can then create a SAS based on hello ID for a policy.</span></span> <span data-ttu-id="98939-194">Hallo volgende voorbeeld maakt een nieuwe SAS voor 'gebruiker2':</span><span class="sxs-lookup"><span data-stu-id="98939-194">hello following example creates a new SAS for 'user2':</span></span>

```
queueSAS = queueSvc.generateSharedAccessSignature('myqueue', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="98939-195">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="98939-195">Next Steps</span></span>
<span data-ttu-id="98939-196">Nu u Hallo basisprincipes van queue storage hebt geleerd, volgt u deze koppelingen toolearn over complexere opslagtaken.</span><span class="sxs-lookup"><span data-stu-id="98939-196">Now that you've learned hello basics of queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="98939-197">Ga naar Hallo [Azure Storage Team Blog] [Azure Storage Team Blog].</span><span class="sxs-lookup"><span data-stu-id="98939-197">Visit hello [Azure Storage Team Blog][Azure Storage Team Blog].</span></span>
* <span data-ttu-id="98939-198">Ga naar Hallo [Azure-opslag-SDK voor knooppunt] [ Azure Storage SDK for Node] opslagplaats op GitHub.</span><span class="sxs-lookup"><span data-stu-id="98939-198">Visit hello [Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub.</span></span>

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node
[using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure Portal]: https://portal.azure.com<span data-ttu-id="98939-199">
[Een Node.js-web-app maken in Azure App Service](../../app-service-web/app-service-web-get-started-nodejs.md) </span><span class="sxs-lookup"><span data-stu-id="98939-199">
[Create a Node.js web app in Azure App Service](../../app-service-web/app-service-web-get-started-nodejs.md) </span></span>  
<span data-ttu-id="98939-200">[Node.js web-app met behulp van hello Azure Table-Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)
</span><span class="sxs-lookup"><span data-stu-id="98939-200">[Node.js web app using hello Azure Table Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)
</span></span>  


<span data-ttu-id="98939-201">[Bouw en implementeer een Node.js-toepassing tooan Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) </span><span class="sxs-lookup"><span data-stu-id="98939-201">[Build and deploy a Node.js application tooan Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) </span></span>  
<span data-ttu-id="98939-202">[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/ [bouwen en implementeren van een Node.js web-app tooAzure met behulp van Web Matrix]: https://www.microsoft.com/web/webmatrix/</span><span class="sxs-lookup"><span data-stu-id="98939-202">[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/ [Build and deploy a Node.js web app tooAzure using Web Matrix]: https://www.microsoft.com/web/webmatrix/</span></span>   
