---
title: Hoe Queue storage gebruiken met Node.js | Microsoft Docs
description: Informatie over het gebruik van de Azure Queue-service maken en verwijderen van wachtrijen, en invoegen, ophalen en verwijderen van berichten. Voorbeelden die zijn geschreven in Node.js.
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
ms.openlocfilehash: e30297bd0cc65105c92d6428035d2e6c156448af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-queue-storage-from-nodejs"></a><span data-ttu-id="5330e-104">Queue Storage gebruiken met Node.js</span><span class="sxs-lookup"><span data-stu-id="5330e-104">How to use Queue storage from Node.js</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="5330e-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="5330e-105">Overview</span></span>
<span data-ttu-id="5330e-106">Deze handleiding wordt getoond hoe u veelvoorkomende scenario's met behulp van de Microsoft Azure Queue-service uitvoert.</span><span class="sxs-lookup"><span data-stu-id="5330e-106">This guide shows you how to perform common scenarios using the Microsoft Azure Queue service.</span></span> <span data-ttu-id="5330e-107">De voorbeelden zijn geschreven met behulp van de Node.js-API.</span><span class="sxs-lookup"><span data-stu-id="5330e-107">The samples are written using the Node.js API.</span></span> <span data-ttu-id="5330e-108">De scenario's worden behandeld: **invoegen**, **inspecteren**, **ophalen**, en **verwijderen** wachtrij berichten, evenals **maken en verwijderen van wachtrijen**.</span><span class="sxs-lookup"><span data-stu-id="5330e-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="5330e-109">Een Node.js-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="5330e-109">Create a Node.js Application</span></span>
<span data-ttu-id="5330e-110">Maak een lege Node.js-toepassing.</span><span class="sxs-lookup"><span data-stu-id="5330e-110">Create a blank Node.js application.</span></span> <span data-ttu-id="5330e-111">Zie voor instructies over het maken van een Node.js-toepassing [een Node.js-web-app maken in Azure App Service], [bouwen en implementeren van een Node.js-toepassing naar een Azure Cloud Service] met Windows PowerShell of [bouwen en implementeren van een Node.js-web-app in Azure met behulp van Web Matrix].</span><span class="sxs-lookup"><span data-stu-id="5330e-111">For instructions creating a Node.js application, see [Create a Node.js web app in Azure App Service], [Build and deploy a Node.js application to an Azure Cloud Service] using Windows PowerShell, or [Build and deploy a Node.js web app to Azure using Web Matrix].</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="5330e-112">Uw toepassing configureren voor toegang tot opslag</span><span class="sxs-lookup"><span data-stu-id="5330e-112">Configure Your Application to Access Storage</span></span>
<span data-ttu-id="5330e-113">Voor het gebruik van Azure-opslag, moet u de Azure-opslag-SDK voor Node.js, waaronder een set van gemak bibliotheken die met de storage REST-services communiceren.</span><span class="sxs-lookup"><span data-stu-id="5330e-113">To use Azure storage, you need the Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="5330e-114">Knooppunt Package Manager (NPM) gebruiken om het pakket te verkrijgen</span><span class="sxs-lookup"><span data-stu-id="5330e-114">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="5330e-115">Een opdrachtregelinterface gebruiken zoals **PowerShell** (Windows), **Terminal** (Mac), of **Bash** (Unix), gaat u naar de map waar u uw voorbeeldtoepassing gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5330e-115">Use a command-line interface such as **PowerShell** (Windows,) **Terminal** (Mac,) or **Bash** (Unix), navigate to the folder where you created your sample application.</span></span>
2. <span data-ttu-id="5330e-116">Type **npm Installeer azure-opslag** in het opdrachtvenster.</span><span class="sxs-lookup"><span data-stu-id="5330e-116">Type **npm install azure-storage** in the command window.</span></span> <span data-ttu-id="5330e-117">Uitvoer van de opdracht is vergelijkbaar met het volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="5330e-117">Output from the command is similar to the following example.</span></span>
 
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

3. <span data-ttu-id="5330e-118">U kunt handmatig uitvoeren de **ls** opdracht om te controleren of een **knooppunt\_modules** map is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5330e-118">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="5330e-119">In deze map vindt u de **azure-opslag** , dit pakket bevat de bibliotheken die u moet toegang hebben tot opslag.</span><span class="sxs-lookup"><span data-stu-id="5330e-119">Inside that folder you will find the **azure-storage** package, which contains the libraries you need to access storage.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="5330e-120">Het pakket importeren</span><span class="sxs-lookup"><span data-stu-id="5330e-120">Import the package</span></span>
<span data-ttu-id="5330e-121">In Kladblok of een andere teksteditor en voeg het volgende toe boven de **server.js** -bestand van de toepassing waarin u van plan bent opslag gebruiken:</span><span class="sxs-lookup"><span data-stu-id="5330e-121">Using Notepad or another text editor, add the following to the top the **server.js** file of the application where you intend to use storage:</span></span>

```
var azure = require('azure-storage');
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="5330e-122">Een Azure-opslag-verbinding instellen</span><span class="sxs-lookup"><span data-stu-id="5330e-122">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="5330e-123">De azure-module leest de omgevingsvariabelen AZURE\_opslag\_ACCOUNT en AZURE\_opslag\_toegang\_sleutel of AZURE\_opslag\_verbinding\_tekenreeks voor de benodigde informatie om te verbinden met uw Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="5330e-123">The azure module will read the environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="5330e-124">Als deze omgevingsvariabelen zijn niet ingesteld, moet u de accountgegevens opgeven bij het aanroepen van **createQueueService**.</span><span class="sxs-lookup"><span data-stu-id="5330e-124">If these environment variables are not set, you must specify the account information when calling **createQueueService**.</span></span>

<span data-ttu-id="5330e-125">Voor een voorbeeld van de omgevingsvariabelen instellen in de [Azure Portal](https://portal.azure.com) Zie voor een Azure-Website [Node.js-web-app met behulp van de Service Azure-tabel].</span><span class="sxs-lookup"><span data-stu-id="5330e-125">For an example of setting the environment variables in the [Azure Portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using the Azure Table Service].</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="5330e-126">Procedure: Een wachtrij maken</span><span class="sxs-lookup"><span data-stu-id="5330e-126">How To: Create a Queue</span></span>
<span data-ttu-id="5330e-127">De volgende code maakt een **QueueService** object, waarmee u werkt met wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="5330e-127">The following code creates a **QueueService** object, which enables you to work with queues.</span></span>

```
var queueSvc = azure.createQueueService();
```

<span data-ttu-id="5330e-128">Gebruik de **createQueueIfNotExists** methode, die de opgegeven wachtrij retourneert als dit al bestaat of maakt een nieuwe wachtrij met de opgegeven naam als deze niet al bestaat.</span><span class="sxs-lookup"><span data-stu-id="5330e-128">Use the **createQueueIfNotExists** method, which returns the specified queue if it already exists or creates a new queue with the specified name if it does not already exist.</span></span>

```
queueSvc.createQueueIfNotExists('myqueue', function(error, result, response){
  if(!error){
    // Queue created or exists
  }
});
```

<span data-ttu-id="5330e-129">Als de wachtrij is gemaakt, `result.created` is ingesteld op true.</span><span class="sxs-lookup"><span data-stu-id="5330e-129">If the queue is created, `result.created` is true.</span></span> <span data-ttu-id="5330e-130">Als de wachtrij bestaat, `result.created` is ingesteld op false.</span><span class="sxs-lookup"><span data-stu-id="5330e-130">If the queue exists, `result.created` is false.</span></span>

### <a name="filters"></a><span data-ttu-id="5330e-131">Filters</span><span class="sxs-lookup"><span data-stu-id="5330e-131">Filters</span></span>
<span data-ttu-id="5330e-132">Optionele filteren bewerkingen kunnen worden toegepast op de bewerkingen die worden uitgevoerd met behulp van **QueueService**.</span><span class="sxs-lookup"><span data-stu-id="5330e-132">Optional filtering operations can be applied to operations performed using **QueueService**.</span></span> <span data-ttu-id="5330e-133">Bewerkingen voor het filteren kunt opnemen logboekregistratie, automatisch opnieuw, enzovoort. Filters zijn objecten die een methode met de handtekening implementeren:</span><span class="sxs-lookup"><span data-stu-id="5330e-133">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```
function handle (requestOptions, next)
```

<span data-ttu-id="5330e-134">Hierna moet u de voorverwerking van de aanvraag-opties, moet de methode aanroepen 'volgende' doorgeven van een retouraanroep met de volgende handtekening:</span><span class="sxs-lookup"><span data-stu-id="5330e-134">After doing its preprocessing on the request options, the method needs to call "next" passing a callback with the following signature:</span></span>

```
function (returnObject, finalCallback, next)
```

<span data-ttu-id="5330e-135">In deze retouraanroep en na het verwerken van de returnObject (de reactie van de aanvraag naar de server), moet de callback volgende aanroepen als deze bestaat als u wilt doorgaan met het verwerken van andere filters of gewoon finalCallback anders om uiteindelijk de aanroep van de service aanroepen.</span><span class="sxs-lookup"><span data-stu-id="5330e-135">In this callback, and after processing the returnObject (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or simply invoke finalCallback otherwise to end up the service invocation.</span></span>

<span data-ttu-id="5330e-136">Twee filters die Pogingslogica implementeren zijn opgenomen in de Azure SDK voor Node.js, **ExponentialRetryPolicyFilter** en **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="5330e-136">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="5330e-137">De volgende code maakt een **QueueService** -object dat gebruikmaakt van de **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="5330e-137">The following creates a **QueueService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var queueSvc = azure.createQueueService().withFilter(retryOperations);
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="5330e-138">Procedure: Een bericht in een wachtrij invoegen</span><span class="sxs-lookup"><span data-stu-id="5330e-138">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="5330e-139">Voor het invoegen van een bericht in een wachtrij, gebruikt u de **createMessage** methode voor het maken van een nieuw bericht en voeg deze toe aan de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="5330e-139">To insert a message into a queue, use the **createMessage** method to create a new message and add it to the queue.</span></span>

```
queueSvc.createMessage('myqueue', "Hello world!", function(error, result, response){
  if(!error){
    // Message inserted
  }
});
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="5330e-140">Procedure: Bekijken van het volgende bericht</span><span class="sxs-lookup"><span data-stu-id="5330e-140">How To: Peek at the Next Message</span></span>
<span data-ttu-id="5330e-141">U kunt het bericht vooraan in een wachtrij bekijken zonder het te verwijderen uit de wachtrij door het aanroepen van de **peekMessages** methode.</span><span class="sxs-lookup"><span data-stu-id="5330e-141">You can peek at the message in the front of a queue without removing it from the queue by calling the **peekMessages** method.</span></span> <span data-ttu-id="5330e-142">Standaard **peekMessages** geeft een enkel bericht weer.</span><span class="sxs-lookup"><span data-stu-id="5330e-142">By default, **peekMessages** peeks at a single message.</span></span>

```
queueSvc.peekMessages('myqueue', function(error, result, response){
  if(!error){
    // Message text is in messages[0].messageText
  }
});
```

<span data-ttu-id="5330e-143">De `result` het bericht bevat.</span><span class="sxs-lookup"><span data-stu-id="5330e-143">The `result` contains the message.</span></span>

> [!NOTE]
> <span data-ttu-id="5330e-144">Met behulp van **peekMessages** wanneer er geen berichten in de wachtrij zijn wordt geen fout geretourneerd, maar er zijn geen berichten worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="5330e-144">Using **peekMessages** when there are no messages in the queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-dequeue-the-next-message"></a><span data-ttu-id="5330e-145">Procedure: Het volgende bericht uit de wachtrij halen</span><span class="sxs-lookup"><span data-stu-id="5330e-145">How To: Dequeue the Next Message</span></span>
<span data-ttu-id="5330e-146">Verwerken van een bericht is een proces in twee fasen:</span><span class="sxs-lookup"><span data-stu-id="5330e-146">Processing a message is a two-stage process:</span></span>

1. <span data-ttu-id="5330e-147">Het bericht uit de wachtrij halen.</span><span class="sxs-lookup"><span data-stu-id="5330e-147">Dequeue the message.</span></span>
2. <span data-ttu-id="5330e-148">Verwijder het bericht.</span><span class="sxs-lookup"><span data-stu-id="5330e-148">Delete the message.</span></span>

<span data-ttu-id="5330e-149">Gebruiken om een bericht uit de wachtrij halen, **getMessages**.</span><span class="sxs-lookup"><span data-stu-id="5330e-149">To dequeue a message, use **getMessages**.</span></span> <span data-ttu-id="5330e-150">Dit maakt de berichten onzichtbaar in de wachtrij, zodat er geen andere clients kunnen verwerken.</span><span class="sxs-lookup"><span data-stu-id="5330e-150">This makes the messages invisible in the queue, so no other clients can process them.</span></span> <span data-ttu-id="5330e-151">Wanneer een bericht is verwerkt door uw toepassing, aanroepen **deleteMessage** te verwijderen uit de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="5330e-151">Once your application has processed a message, call **deleteMessage** to delete it from the queue.</span></span> <span data-ttu-id="5330e-152">Het volgende voorbeeld wordt een bericht en vervolgens wordt verwijderd:</span><span class="sxs-lookup"><span data-stu-id="5330e-152">The following example gets a message, then deletes it:</span></span>

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
> <span data-ttu-id="5330e-153">Standaard wordt een bericht alleen verborgen gedurende 30 seconden, waarna deze zichtbaar voor andere clients is.</span><span class="sxs-lookup"><span data-stu-id="5330e-153">By default, a message is only hidden for 30 seconds, after which it is visible to other clients.</span></span> <span data-ttu-id="5330e-154">U kunt een andere waarde opgeven met behulp van `options.visibilityTimeout` met **getMessages**.</span><span class="sxs-lookup"><span data-stu-id="5330e-154">You can specify a different value by using `options.visibilityTimeout` with **getMessages**.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="5330e-155">Met behulp van **getMessages** wanneer er geen berichten in de wachtrij zijn wordt geen fout geretourneerd, maar er zijn geen berichten worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="5330e-155">Using **getMessages** when there are no messages in the queue will not return an error, however no messages will be returned.</span></span>
> 
> 

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="5330e-156">Procedure: De inhoud van een bericht in de wachtrij wijzigen</span><span class="sxs-lookup"><span data-stu-id="5330e-156">How To: Change the Contents of a Queued Message</span></span>
<span data-ttu-id="5330e-157">U kunt de inhoud van een bericht in-place in de wachtrij met behulp wijzigen **updateMessage**.</span><span class="sxs-lookup"><span data-stu-id="5330e-157">You can change the contents of a message in-place in the queue using **updateMessage**.</span></span> <span data-ttu-id="5330e-158">De tekst van een bericht wordt bijgewerkt door het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="5330e-158">The following example updates the text of a message:</span></span>

```
queueSvc.getMessages('myqueue', function(error, result, response){
  if(!error){
    // Got the message
    var message = result[0];
    queueSvc.updateMessage('myqueue', message.messageId, message.popReceipt, 10, {messageText: 'new text'}, function(error, result, response){
      if(!error){
        // Message updated successfully
      }
    });
  }
});
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="5330e-159">Procedure: Aanvullende opties voor waarbij berichten</span><span class="sxs-lookup"><span data-stu-id="5330e-159">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="5330e-160">Er zijn twee manieren u ophalen van berichten uit een wachtrij kunt aanpassen:</span><span class="sxs-lookup"><span data-stu-id="5330e-160">There are two ways you can customize message retrieval from a queue:</span></span>

* <span data-ttu-id="5330e-161">`options.numOfMessages`-Ophalen van een batch met berichten (maximaal 32).</span><span class="sxs-lookup"><span data-stu-id="5330e-161">`options.numOfMessages` - Retrieve a batch of messages (up to 32.)</span></span>
* <span data-ttu-id="5330e-162">`options.visibilityTimeout`-Er is een time-out voor onzichtbaarheid langer of korter zijn ingesteld.</span><span class="sxs-lookup"><span data-stu-id="5330e-162">`options.visibilityTimeout` - Set a longer or shorter invisibility timeout.</span></span>

<span data-ttu-id="5330e-163">Het volgende voorbeeld wordt de **getMessages** methode 15 berichten in één aanroep ophalen.</span><span class="sxs-lookup"><span data-stu-id="5330e-163">The following example uses the **getMessages** method to get 15 messages in one call.</span></span> <span data-ttu-id="5330e-164">Vervolgens wordt verwerkt elke bericht met een for-lus.</span><span class="sxs-lookup"><span data-stu-id="5330e-164">Then it processes each message using a for loop.</span></span> <span data-ttu-id="5330e-165">De time-out voor onzichtbaarheid wordt ingesteld op vijf minuten voor alle berichten die zijn geretourneerd door deze methode.</span><span class="sxs-lookup"><span data-stu-id="5330e-165">It also sets the invisibility timeout to five minutes for all messages returned by this method.</span></span>

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

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="5330e-166">Procedure: De lengte van de wachtrij ophalen</span><span class="sxs-lookup"><span data-stu-id="5330e-166">How To: Get the Queue Length</span></span>
<span data-ttu-id="5330e-167">De **getQueueMetadata** retourneert metagegevens over de wachtrij, waaronder het geschatte aantal berichten in de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="5330e-167">The **getQueueMetadata** returns metadata about the queue, including the approximate number of messages waiting in the queue.</span></span>

```
queueSvc.getQueueMetadata('myqueue', function(error, result, response){
  if(!error){
    // Queue length is available in result.approximateMessageCount
  }
});
```

## <a name="how-to-list-queues"></a><span data-ttu-id="5330e-168">Procedure: Lijst wachtrijen</span><span class="sxs-lookup"><span data-stu-id="5330e-168">How To: List Queues</span></span>
<span data-ttu-id="5330e-169">Gebruik voor het ophalen van een lijst van wachtrijen, **listQueuesSegmented**.</span><span class="sxs-lookup"><span data-stu-id="5330e-169">To retrieve a list of queues, use **listQueuesSegmented**.</span></span> <span data-ttu-id="5330e-170">Gebruik voor het ophalen van een lijst gefilterd op een bepaald voorvoegsel **listQueuesSegmentedWithPrefix**.</span><span class="sxs-lookup"><span data-stu-id="5330e-170">To retrieve a list filtered by a specific prefix, use **listQueuesSegmentedWithPrefix**.</span></span>

```
queueSvc.listQueuesSegmented(null, function(error, result, response){
  if(!error){
    // result.entries contains the list of queues
  }
});
```

<span data-ttu-id="5330e-171">Als alle wachtrijen kunnen niet worden geretourneerd, `result.continuationToken` kan worden gebruikt als de eerste parameter van **listQueuesSegmented** of de tweede parameter van **listQueuesSegmentedWithPrefix** meer resultaten ophalen.</span><span class="sxs-lookup"><span data-stu-id="5330e-171">If all queues cannot be returned, `result.continuationToken` can be used as the first parameter of **listQueuesSegmented** or the second parameter of **listQueuesSegmentedWithPrefix** to retrieve more results.</span></span>

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="5330e-172">Procedure: Een wachtrij verwijderen</span><span class="sxs-lookup"><span data-stu-id="5330e-172">How To: Delete a Queue</span></span>
<span data-ttu-id="5330e-173">Aanroepen voor het verwijderen van een wachtrij en alle berichten hierin de **deleteQueue** methode voor het object in de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="5330e-173">To delete a queue and all the messages contained in it, call the **deleteQueue** method on the queue object.</span></span>

```
queueSvc.deleteQueue(queueName, function(error, response){
  if(!error){
    // Queue has been deleted
  }
});
```

<span data-ttu-id="5330e-174">Schakel alle berichten uit een wachtrij zonder het te verwijderen, gebruik **clearMessages**.</span><span class="sxs-lookup"><span data-stu-id="5330e-174">To clear all messages from a queue without deleting it, use **clearMessages**.</span></span>

## <a name="how-to-work-with-shared-access-signatures"></a><span data-ttu-id="5330e-175">How to: werken met handtekeningen voor gedeelde toegang</span><span class="sxs-lookup"><span data-stu-id="5330e-175">How to: Work with Shared Access Signatures</span></span>
<span data-ttu-id="5330e-176">Shared Access Signatures (SAS) zijn geen veilige manier toegang te bieden gedetailleerde tot wachtrijen zonder dat de naam van het opslagaccount of sleutels.</span><span class="sxs-lookup"><span data-stu-id="5330e-176">Shared Access Signatures (SAS) are a secure way to provide granular access to queues without providing your storage account name or keys.</span></span> <span data-ttu-id="5330e-177">SAS worden vaak gebruikt voor beperkte toegang tot uw wachtrijen, zoals het toestaan van een mobiele app om berichten te versturen.</span><span class="sxs-lookup"><span data-stu-id="5330e-177">SAS are often used to provide limited access to your queues, such as allowing a mobile app to submit messages.</span></span>

<span data-ttu-id="5330e-178">Een vertrouwde toepassing zoals een cloud-gebaseerde service genereert een SAS met de **generateSharedAccessSignature** van de **QueueService**, en biedt dit aan een niet-vertrouwde of semi vertrouwde toepassing.</span><span class="sxs-lookup"><span data-stu-id="5330e-178">A trusted application such as a cloud-based service generates a SAS using the **generateSharedAccessSignature** of the **QueueService**, and provides it to an untrusted or semi-trusted application.</span></span> <span data-ttu-id="5330e-179">Bijvoorbeeld: een mobiele app.</span><span class="sxs-lookup"><span data-stu-id="5330e-179">For example, a mobile app.</span></span> <span data-ttu-id="5330e-180">De SAS is gegenereerd met een beleid in, die beschrijft de begin- en einddatums gedurende welke de SAS geldig is, evenals het toegangsniveau verleend aan de SAS-houder.</span><span class="sxs-lookup"><span data-stu-id="5330e-180">The SAS is generated using a policy, which describes the start and end dates during which the SAS is valid, as well as the access level granted to the SAS holder.</span></span>

<span data-ttu-id="5330e-181">Het volgende voorbeeld genereert een nieuw beleid voor gedeelde toegang die ervoor zorgen dat de SAS-houder berichten toevoegen aan de wachtrij en 100 minuten na het tijdstip waarop dat deze is gemaakt is verlopen.</span><span class="sxs-lookup"><span data-stu-id="5330e-181">The following example generates a new shared access policy that will allow the SAS holder to add messages to the queue, and expires 100 minutes after the time it is created.</span></span>

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

<span data-ttu-id="5330e-182">Houd er rekening mee dat de informatie over de host moet ook worden opgegeven als deze vereist is wanneer de SAS-houder probeert te krijgen van de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="5330e-182">Note that the host information must be provided also, as it is required when the SAS holder attempts to access the queue.</span></span>

<span data-ttu-id="5330e-183">Vervolgens kunt u de clienttoepassing gebruikmaakt van de SAS met **QueueServiceWithSAS** bewerkingen op basis van de wachtrij uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="5330e-183">The client application then uses the SAS with **QueueServiceWithSAS** to perform operations against the queue.</span></span> <span data-ttu-id="5330e-184">Het volgende voorbeeld maakt verbinding met de wachtrij en een bericht wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5330e-184">The following example connects to the queue and creates a message.</span></span>

```
var sharedQueueService = azure.createQueueServiceWithSas(host, queueSAS);
sharedQueueService.createMessage('myqueue', 'Hello world from SAS!', function(error, result, response){
  if(!error){
    //message added
  }
});
```

<span data-ttu-id="5330e-185">Aangezien de SAS is gegenereerd met de toegang voor toevoegen als een poging is gedaan te lezen, bijwerken of verwijderen van berichten, wordt een fout geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="5330e-185">Since the SAS was generated with add access, if an attempt were made to read, update or delete messages, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="5330e-186">Toegangsbeheerlijsten</span><span class="sxs-lookup"><span data-stu-id="5330e-186">Access control lists</span></span>
<span data-ttu-id="5330e-187">U kunt ook een lijst met ACL (Access Control) het toegangsbeleid instellen voor een SAS.</span><span class="sxs-lookup"><span data-stu-id="5330e-187">You can also use an Access Control List (ACL) to set the access policy for a SAS.</span></span> <span data-ttu-id="5330e-188">Dit is handig als u toestaan dat meerdere clients toegang tot de wachtrij wilt, maar bieden verschillende toegangsbeleid voor elke client.</span><span class="sxs-lookup"><span data-stu-id="5330e-188">This is useful if you wish to allow multiple clients to access the queue, but provide different access policies for each client.</span></span>

<span data-ttu-id="5330e-189">Een ACL die is geïmplementeerd met behulp van een matrix van toegangsbeleid, met een ID die is gekoppeld aan elk beleid.</span><span class="sxs-lookup"><span data-stu-id="5330e-189">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="5330e-190">Het volgende voorbeeld definieert twee beleidsregels; een voor 'gebruiker1' en één voor 'gebruiker2':</span><span class="sxs-lookup"><span data-stu-id="5330e-190">The  following example defines two policies; one for 'user1' and one for 'user2':</span></span>

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

<span data-ttu-id="5330e-191">Het volgende voorbeeld wordt de huidige ACL voor **rapportberichten**, voegt u vervolgens het nieuwe beleid met behulp van **setQueueAcl**.</span><span class="sxs-lookup"><span data-stu-id="5330e-191">The following example gets the current ACL for **myqueue**, then adds the new policies using **setQueueAcl**.</span></span> <span data-ttu-id="5330e-192">Met deze aanpak kunt:</span><span class="sxs-lookup"><span data-stu-id="5330e-192">This approach allows:</span></span>

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

<span data-ttu-id="5330e-193">Als de ACL is ingesteld, kunt u vervolgens een SAS op basis van de ID voor een beleid maken.</span><span class="sxs-lookup"><span data-stu-id="5330e-193">Once the ACL has been set, you can then create a SAS based on the ID for a policy.</span></span> <span data-ttu-id="5330e-194">Het volgende voorbeeld wordt een nieuwe SAS voor 'gebruiker2':</span><span class="sxs-lookup"><span data-stu-id="5330e-194">The following example creates a new SAS for 'user2':</span></span>

```
queueSAS = queueSvc.generateSharedAccessSignature('myqueue', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="5330e-195">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5330e-195">Next Steps</span></span>
<span data-ttu-id="5330e-196">Nu dat u de basisprincipes van queue storage hebt geleerd, volgt u deze koppelingen voor meer informatie over complexere opslagtaken.</span><span class="sxs-lookup"><span data-stu-id="5330e-196">Now that you've learned the basics of queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="5330e-197">Ga naar de [Blog Azure Storage-Team][Azure Storage Team Blog].</span><span class="sxs-lookup"><span data-stu-id="5330e-197">Visit the [Azure Storage Team Blog][Azure Storage Team Blog].</span></span>
* <span data-ttu-id="5330e-198">Ga naar de [Azure-opslag-SDK voor knooppunt] [ Azure Storage SDK for Node] opslagplaats op GitHub.</span><span class="sxs-lookup"><span data-stu-id="5330e-198">Visit the [Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub.</span></span>

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node
[using the REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure Portal]: https://portal.azure.com
<span data-ttu-id="5330e-199">[een Node.js-web-app maken in Azure App Service]: ../app-service-web/app-service-web-get-started-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="5330e-199">[Create a Node.js web app in Azure App Service]: ../app-service-web/app-service-web-get-started-nodejs.md</span></span>
<span data-ttu-id="5330e-200">[Node.js-web-app met behulp van de Service Azure-tabel]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md</span><span class="sxs-lookup"><span data-stu-id="5330e-200">[Node.js web app using the Azure Table Service]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md</span></span>


<span data-ttu-id="5330e-201">[bouwen en implementeren van een Node.js-toepassing naar een Azure Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md</span><span class="sxs-lookup"><span data-stu-id="5330e-201">[Build and deploy a Node.js application to an Azure Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md</span></span>
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
<span data-ttu-id="5330e-202">[bouwen en implementeren van een Node.js-web-app in Azure met behulp van Web Matrix]: ../app-service-web/web-sites-nodejs-use-webmatrix.md</span><span class="sxs-lookup"><span data-stu-id="5330e-202">[Build and deploy a Node.js web app to Azure using Web Matrix]: ../app-service-web/web-sites-nodejs-use-webmatrix.md</span></span>
