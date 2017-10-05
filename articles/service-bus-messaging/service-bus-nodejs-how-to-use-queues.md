---
title: Het gebruik van Service Bus-wachtrijen in Node.js | Microsoft Docs
description: Informatie over het gebruik van Service Bus-wachtrijen in Azure vanuit een Node.js-app.
services: service-bus-messaging
documentationcenter: nodejs
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a87a00f9-9aba-4c49-a0df-f900a8b67b3f
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: fe2c02534996d99c190593a419a4823888f03d31
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-service-bus-queues-with-nodejs"></a><span data-ttu-id="96043-103">Service Bus-wachtrijen gebruiken met Node.js</span><span class="sxs-lookup"><span data-stu-id="96043-103">How to use Service Bus queues with Node.js</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="96043-104">Dit artikel wordt beschreven hoe u Service Bus-wachtrijen met behulp van Node.js.</span><span class="sxs-lookup"><span data-stu-id="96043-104">This article describes how to use Service Bus queues with Node.js.</span></span> <span data-ttu-id="96043-105">De voorbeelden zijn geschreven in JavaScript en gebruiken van de Node.js-Azure-module.</span><span class="sxs-lookup"><span data-stu-id="96043-105">The samples are written in JavaScript and use the Node.js Azure module.</span></span> <span data-ttu-id="96043-106">De scenario's worden behandeld: **maken van wachtrijen**, **verzenden en ontvangen berichten**, en **verwijderen van wachtrijen**.</span><span class="sxs-lookup"><span data-stu-id="96043-106">The scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span> <span data-ttu-id="96043-107">Zie voor meer informatie over wachtrijen de [Vervolgstappen](#next-steps) sectie.</span><span class="sxs-lookup"><span data-stu-id="96043-107">For more information on queues, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="96043-108">Een Node.js-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="96043-108">Create a Node.js application</span></span>
<span data-ttu-id="96043-109">Maak een lege Node.js-toepassing.</span><span class="sxs-lookup"><span data-stu-id="96043-109">Create a blank Node.js application.</span></span> <span data-ttu-id="96043-110">Zie voor instructies over het maken van een Node.js-toepassing [maken en implementeren van een Node.js-toepassing naar een Azure-Website][Create and deploy a Node.js application to an Azure Website], of [Node.js-Cloudservice] [ Node.js Cloud Service] met Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="96043-110">For instructions on how to create a Node.js application, see [Create and deploy a Node.js application to an Azure Website][Create and deploy a Node.js application to an Azure Website], or [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell.</span></span>

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="96043-111">Uw toepassing configureren voor het gebruik van Service Bus</span><span class="sxs-lookup"><span data-stu-id="96043-111">Configure your application to use Service Bus</span></span>
<span data-ttu-id="96043-112">Download en gebruik van het pakket Node.js Azure voor het gebruik van Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="96043-112">To use Azure Service Bus, download and use the Node.js Azure package.</span></span> <span data-ttu-id="96043-113">Dit pakket bevat een set van bibliotheken die met de Service Bus REST-services communiceren.</span><span class="sxs-lookup"><span data-stu-id="96043-113">This package includes a set of libraries that communicate with the Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="96043-114">Knooppunt Package Manager (NPM) gebruiken om het pakket te verkrijgen</span><span class="sxs-lookup"><span data-stu-id="96043-114">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="96043-115">Gebruik de **Windows PowerShell voor Node.js** opdrachtvenster om te navigeren naar de **c:\\knooppunt\\sbqueues\\WebRole1** map waarin u uw voorbeeldtoepassing hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="96043-115">Use the **Windows PowerShell for Node.js** command window to navigate to the **c:\\node\\sbqueues\\WebRole1** folder in which you created your sample application.</span></span>
2. <span data-ttu-id="96043-116">Type **npm installeren azure** in het opdrachtvenster die moet resulteren in de uitvoer ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="96043-116">Type **npm install azure** in the command window, which should result in output similar to the following:</span></span>

    ```
    azure@0.7.5 node_modules\azure
        ├── dateformat@1.0.2-1.2.3
        ├── xmlbuilder@0.4.2
        ├── node-uuid@1.2.0
        ├── mime@1.2.9
        ├── underscore@1.4.4
        ├── validator@1.1.1
        ├── tunnel@0.0.2
        ├── wns@0.5.3
        ├── xml2js@0.2.7 (sax@0.5.2)
        └── request@2.21.0 (json-stringify-safe@4.0.0, forever-agent@0.5.0, aws-sign@0.3.0, tunnel-agent@0.3.0, oauth-sign@0.3.0, qs@0.6.5, cookie-jar@0.3.0, node-uuid@1.4.0, http-signature@0.9.11, form-data@0.0.8, hawk@0.13.1)
    ```
3. <span data-ttu-id="96043-117">U kunt handmatig uitvoeren de **ls** opdracht om te controleren of een **node_modules** map is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="96043-117">You can manually run the **ls** command to verify that a **node_modules** folder was created.</span></span> <span data-ttu-id="96043-118">In deze map te zoeken naar de **azure** , dit pakket de bibliotheken die u nodig hebt bevat voor toegang tot de Service Bus-wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="96043-118">Inside that folder find the **azure** package, which contains the libraries you need to access Service Bus queues.</span></span>

### <a name="import-the-module"></a><span data-ttu-id="96043-119">Importeer de module</span><span class="sxs-lookup"><span data-stu-id="96043-119">Import the module</span></span>
<span data-ttu-id="96043-120">Het volgende in Kladblok of een andere teksteditor toevoegen aan de bovenkant van de **server.js** -bestand van de toepassing:</span><span class="sxs-lookup"><span data-stu-id="96043-120">Using Notepad or another text editor, add the following to the top of the **server.js** file of the application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-an-azure-service-bus-connection"></a><span data-ttu-id="96043-121">Een Azure Service Bus-verbinding instellen</span><span class="sxs-lookup"><span data-stu-id="96043-121">Set up an Azure Service Bus connection</span></span>
<span data-ttu-id="96043-122">De Azure-module leest de omgevingsvariabele `AZURE_SERVICEBUS_CONNECTION_STRING` informatie vereist om verbinding met Service Bus te verkrijgen.</span><span class="sxs-lookup"><span data-stu-id="96043-122">The Azure module reads the environment variable `AZURE_SERVICEBUS_CONNECTION_STRING` to obtain information required to connect to Service Bus.</span></span> <span data-ttu-id="96043-123">Als deze omgevingsvariabele niet is ingesteld, moet u de accountgegevens opgeven bij het aanroepen van `createServiceBusService`.</span><span class="sxs-lookup"><span data-stu-id="96043-123">If this environment variable is not set, you must specify the account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="96043-124">Zie voor een voorbeeld van de omgevingsvariabelen instellen in een configuratiebestand voor een Azure Cloud Service [Node.js-Cloudservice met Storage][Node.js Cloud Service with Storage].</span><span class="sxs-lookup"><span data-stu-id="96043-124">For an example of setting the environment variables in a configuration file for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="96043-125">Voor een voorbeeld van de omgevingsvariabelen instellen in de [Azure-portal] [ Azure portal] Zie voor een Azure-Website [Node.js-webtoepassing met Storage][Node.js Web Application with Storage].</span><span class="sxs-lookup"><span data-stu-id="96043-125">For an example of setting the environment variables in the [Azure portal][Azure portal] for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="96043-126">Een wachtrij maken</span><span class="sxs-lookup"><span data-stu-id="96043-126">Create a queue</span></span>
<span data-ttu-id="96043-127">De **ServiceBusService** object kunt u werken met Service Bus-wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="96043-127">The **ServiceBusService** object enables you to work with Service Bus queues.</span></span> <span data-ttu-id="96043-128">De volgende code maakt een **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="96043-128">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="96043-129">Voeg deze toe aan de bovenkant van de **server.js** bestand na de instructie voor het importeren van de Azure-module:</span><span class="sxs-lookup"><span data-stu-id="96043-129">Add it near the top of the **server.js** file, after the statement to import the Azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="96043-130">Door het aanroepen van `createQueueIfNotExists` op de **ServiceBusService** object, de opgegeven wachtrij is geretourneerd (indien aanwezig) of een nieuwe wachtrij met de opgegeven naam is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="96043-130">By calling `createQueueIfNotExists` on the **ServiceBusService** object, the specified queue is returned (if it exists), or a new queue with the specified name is created.</span></span> <span data-ttu-id="96043-131">De volgende code gebruikt `createQueueIfNotExists` maken of verbinding maken met de wachtrij met de naam `myqueue`:</span><span class="sxs-lookup"><span data-stu-id="96043-131">The following code uses `createQueueIfNotExists` to create or connect to the queue named `myqueue`:</span></span>

```javascript
serviceBusService.createQueueIfNotExists('myqueue', function(error){
    if(!error){
        // Queue exists
    }
});
```

<span data-ttu-id="96043-132">De `createServiceBusService` methode biedt ook ondersteuning voor extra opties waarmee u kunt de standaardinstellingen voor wachtrij zoals de live of Maximale wachtrijgrootte bericht negeren.</span><span class="sxs-lookup"><span data-stu-id="96043-132">The `createServiceBusService` method also supports additional options, which enable you to override default queue settings such as message time to live or maximum queue size.</span></span> <span data-ttu-id="96043-133">Het volgende voorbeeld wordt de maximale wachtrijgrootte ingesteld op 5 GB en een tijd met live (TTL)-waarde van 1 minuut:</span><span class="sxs-lookup"><span data-stu-id="96043-133">The following example sets the maximum queue size to 5 GB, and a time to live (TTL) value of 1 minute:</span></span>

```javascript
var queueOptions = {
      MaxSizeInMegabytes: '5120',
      DefaultMessageTimeToLive: 'PT1M'
    };

serviceBusService.createQueueIfNotExists('myqueue', queueOptions, function(error){
    if(!error){
        // Queue exists
    }
});
```

### <a name="filters"></a><span data-ttu-id="96043-134">Filters</span><span class="sxs-lookup"><span data-stu-id="96043-134">Filters</span></span>
<span data-ttu-id="96043-135">Optionele filteren bewerkingen kunnen worden toegepast op de bewerkingen die worden uitgevoerd met behulp van **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="96043-135">Optional filtering operations can be applied to operations performed using **ServiceBusService**.</span></span> <span data-ttu-id="96043-136">Bewerkingen voor het filteren kunt opnemen logboekregistratie, automatisch opnieuw, enzovoort. Filters zijn objecten die een methode met de handtekening implementeren:</span><span class="sxs-lookup"><span data-stu-id="96043-136">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="96043-137">Hierna moet u de vooraf verwerken van de aanvraag-opties, de methode moet aanroepen `next`, een retouraanroep met de volgende handtekening doorgeven:</span><span class="sxs-lookup"><span data-stu-id="96043-137">After doing its pre-processing on the request options, the method must call `next`, passing a callback with the following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="96043-138">In deze retouraanroep en na de verwerking de `returnObject` (de reactie van de aanvraag naar de server), de callback moet ofwel aanroepen `next` als deze bestaat als u wilt doorgaan met het verwerken van andere filters of gewoon aanroepen `finalCallback`, die het oproepen van de service eindigt.</span><span class="sxs-lookup"><span data-stu-id="96043-138">In this callback, and after processing the `returnObject` (the response from the request to the server), the callback must either invoke `next` if it exists to continue processing other filters, or simply invoke `finalCallback`, which ends the service invocation.</span></span>

<span data-ttu-id="96043-139">Twee filters die Pogingslogica implementeren zijn opgenomen in de Azure SDK voor Node.js, `ExponentialRetryPolicyFilter` en `LinearRetryPolicyFilter`.</span><span class="sxs-lookup"><span data-stu-id="96043-139">Two filters that implement retry logic are included with the Azure SDK for Node.js, `ExponentialRetryPolicyFilter` and `LinearRetryPolicyFilter`.</span></span> <span data-ttu-id="96043-140">De volgende code maakt een `ServiceBusService` -object dat gebruikmaakt van de `ExponentialRetryPolicyFilter`:</span><span class="sxs-lookup"><span data-stu-id="96043-140">The following code creates a `ServiceBusService` object that uses the `ExponentialRetryPolicyFilter`:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="send-messages-to-a-queue"></a><span data-ttu-id="96043-141">Berichten verzenden naar een wachtrij</span><span class="sxs-lookup"><span data-stu-id="96043-141">Send messages to a queue</span></span>
<span data-ttu-id="96043-142">Een bericht te verzenden naar een Service Bus-wachtrij, het aanroepen van uw toepassing de `sendQueueMessage` methode op de **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="96043-142">To send a message to a Service Bus queue, your application calls the `sendQueueMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="96043-143">Berichten verzonden naar (en ontvangen van) Service Bus-wachtrijen zijn **BrokeredMessage** objecten en hebben een aantal standaardeigenschappen (zoals **Label** en **TimeToLive**), een woordenlijst die wordt gebruikt om aangepaste toepassingsspecifieke eigenschappen te bewaren en een hoofdtekst met willekeurige toepassingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="96043-143">Messages sent to (and received from) Service Bus queues are **BrokeredMessage** objects, and have a set of standard properties (such as **Label** and **TimeToLive**), a dictionary that is used to hold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="96043-144">Een toepassing kan de hoofdtekst van het bericht ingesteld door een reeks wordt doorgegeven als het bericht.</span><span class="sxs-lookup"><span data-stu-id="96043-144">An application can set the body of the message by passing a string as the message.</span></span> <span data-ttu-id="96043-145">Alle vereiste eigenschappen standaard worden ingevuld met standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="96043-145">Any required standard properties are populated with default values.</span></span>

<span data-ttu-id="96043-146">Het volgende voorbeeld laat zien hoe een testbericht verzenden naar de wachtrij met de naam `myqueue` met `sendQueueMessage`:</span><span class="sxs-lookup"><span data-stu-id="96043-146">The following example demonstrates how to send a test message to the queue named `myqueue` using `sendQueueMessage`:</span></span>

```javascript
var message = {
    body: 'Test message',
    customProperties: {
        testproperty: 'TestValue'
    }};
serviceBusService.sendQueueMessage('myqueue', message, function(error){
    if(!error){
        // message sent
    }
});
```

<span data-ttu-id="96043-147">Service Bus-wachtrijen ondersteunen een maximale berichtgrootte van 256 kB in de [Standard-laag](service-bus-premium-messaging.md) en 1 MB in de [Premium-laag](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="96043-147">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="96043-148">De koptekst, die de standaard- en aangepaste toepassingseigenschappen bevat, kan maximaal 64 kB groot zijn.</span><span class="sxs-lookup"><span data-stu-id="96043-148">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="96043-149">Er is geen limiet voor het aantal berichten in een wachtrij, maar er is een limiet voor de totale grootte van de berichten in een wachtrij.</span><span class="sxs-lookup"><span data-stu-id="96043-149">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="96043-150">De grootte van de wachtrij wordt gedefinieerd tijdens het aanmaken, met een bovengrens van 5 GB.</span><span class="sxs-lookup"><span data-stu-id="96043-150">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="96043-151">Zie voor meer informatie over quota [Service Bus-quota][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="96043-151">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="96043-152">Berichten ontvangen uit een wachtrij</span><span class="sxs-lookup"><span data-stu-id="96043-152">Receive messages from a queue</span></span>
<span data-ttu-id="96043-153">Berichten worden ontvangen van een wachtrij met de `receiveQueueMessage` methode op de **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="96043-153">Messages are received from a queue using the `receiveQueueMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="96043-154">Standaard worden berichten uit de wachtrij verwijderd als ze worden gelezen; u kunt echter (peek) lezen en vergrendelen van het bericht zonder het te verwijderen uit de wachtrij door de optionele parameter `isPeekLock` naar **true**.</span><span class="sxs-lookup"><span data-stu-id="96043-154">By default, messages are deleted from the queue as they are read; however, you can read (peek) and lock the message without deleting it from the queue by setting the optional parameter `isPeekLock` to **true**.</span></span>

<span data-ttu-id="96043-155">Het standaardgedrag van lezen van en het bericht is verwijderd als onderdeel van de bewerking receive is het eenvoudigste model en werkt het beste voor scenario's waarin een toepassing kan tolereren niet verwerken van een bericht bij een storing.</span><span class="sxs-lookup"><span data-stu-id="96043-155">The default behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="96043-156">Neem bijvoorbeeld een scenario waarin de consument de ontvangstaanvraag uitgeeft en het systeem vervolgens vastloopt voordat de aanvraag wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="96043-156">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="96043-157">Omdat Service Bus het bericht als verbruikt heeft gemarkeerd, klikt u vervolgens wanneer de toepassing opnieuw wordt opgestart en het verbruik van berichten opnieuw begint, ontbreekt het bericht dat voor het vastlopen is verbruikt.</span><span class="sxs-lookup"><span data-stu-id="96043-157">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="96043-158">Als de `isPeekLock` parameter is ingesteld op **true**, wordt het ontvangen, wordt een bewerking met twee fasen, waardoor er mogelijk worden ondersteuning voor toepassingen die geen ontbrekende berichten kunnen tolereren.</span><span class="sxs-lookup"><span data-stu-id="96043-158">If the `isPeekLock` parameter is set to **true**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="96043-159">Als Service Bus een aanvraag ontvangt, wordt het volgende te verbruiken bericht gevonden, wordt het bericht vergrendeld om te voorkomen dat andere consumenten het ontvangen en wordt het bericht vervolgens naar de toepassing geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="96043-159">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="96043-160">Nadat de toepassing klaar is met verwerking van het bericht (of veilig heeft opgeslagen voor toekomstige verwerking), is de tweede fase van het ontvangstproces voltooid door het aanroepen van `deleteMessage` methode en het geven van het bericht moet worden verwijderd als een parameter.</span><span class="sxs-lookup"><span data-stu-id="96043-160">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling `deleteMessage` method and providing the message to be deleted as a parameter.</span></span> <span data-ttu-id="96043-161">De `deleteMessage` methode markeert het bericht als verbruikt en wordt deze verwijderd uit de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="96043-161">The `deleteMessage` method marks the message as being consumed and removes it from the queue.</span></span>

<span data-ttu-id="96043-162">Het volgende voorbeeld laat zien hoe ontvangen en verwerken van berichten met `receiveQueueMessage`.</span><span class="sxs-lookup"><span data-stu-id="96043-162">The following example demonstrates how to receive and process messages using `receiveQueueMessage`.</span></span> <span data-ttu-id="96043-163">In het voorbeeld eerst ontvangt een bericht wordt verwijderd en vervolgens ontvangt een bericht met `isPeekLock` ingesteld op **true**, verwijdert u vervolgens het bericht met `deleteMessage`:</span><span class="sxs-lookup"><span data-stu-id="96043-163">The example first receives and deletes a message, and then receives a message using `isPeekLock` set to **true**, then deletes the message using `deleteMessage`:</span></span>

```javascript
serviceBusService.receiveQueueMessage('myqueue', function(error, receivedMessage){
    if(!error){
        // Message received and deleted
    }
});
serviceBusService.receiveQueueMessage('myqueue', { isPeekLock: true }, function(error, lockedMessage){
    if(!error){
        // Message received and locked
        serviceBusService.deleteMessage(lockedMessage, function (deleteError){
            if(!deleteError){
                // Message deleted
            }
        });
    }
});
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="96043-164">Het vastlopen van de toepassing en onleesbare berichten afhandelen</span><span class="sxs-lookup"><span data-stu-id="96043-164">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="96043-165">Service Bus biedt functionaliteit om netjes te herstellen bij fouten in uw toepassing of problemen bij het verwerken van een bericht.</span><span class="sxs-lookup"><span data-stu-id="96043-165">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="96043-166">Als een ontvangende toepassing kan niet worden verwerkt het bericht om een bepaalde reden, dan kan worden aangeroepen de `unlockMessage` methode op de **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="96043-166">If a receiver application is unable to process the message for some reason, then it can call the `unlockMessage` method on the **ServiceBusService** object.</span></span> <span data-ttu-id="96043-167">Dit zorgt ervoor dat Service Bus het bericht in de wachtrij ontgrendelt en beschikbaar zijn om opnieuw te ontvangen, ofwel door dezelfde consumerende toepassing of door een andere consumerende toepassing.</span><span class="sxs-lookup"><span data-stu-id="96043-167">This will cause Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="96043-168">Er is ook een time-out gekoppeld aan een bericht in de wachtrij is vergrendeld en als de toepassing niet kan verwerken van het bericht voordat de time-out van de vergrendeling verloopt (bijvoorbeeld als de toepassing vastloopt), en vervolgens de Service Bus wordt het bericht automatisch ontgrendelen en beschikbaar zijn om opnieuw te ontvangen.</span><span class="sxs-lookup"><span data-stu-id="96043-168">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (e.g., if the application crashes), then Service Bus will unlock the message automatically and make it available to be received again.</span></span>

<span data-ttu-id="96043-169">In het geval dat de toepassing is vastgelopen na het verwerken van het bericht, maar voordat de `deleteMessage` methode wordt aangeroepen en vervolgens het bericht opnieuw bezorgd bij de toepassing opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="96043-169">In the event that the application crashes after processing the message but before the `deleteMessage` method is called, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="96043-170">Dit wordt vaak genoemd *tenminste eenmaal verwerken*, dat wil zeggen elk bericht ten minste één keer wordt verwerkt maar in sommige situaties hetzelfde bericht opnieuw kan worden bezorgd.</span><span class="sxs-lookup"><span data-stu-id="96043-170">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="96043-171">Als in het scenario dubbele verwerking niet wordt getolereerd, dan moeten toepassingsontwikkelaars extra logica toevoegen aan de toepassing om dubbele berichtbezorging af te handelen.</span><span class="sxs-lookup"><span data-stu-id="96043-171">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="96043-172">Dit wordt vaak bereikt met behulp van de **MessageId** eigenschap van het bericht dat gelijk bij meerdere bezorgingspogingen blijft.</span><span class="sxs-lookup"><span data-stu-id="96043-172">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="96043-173">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="96043-173">Next steps</span></span>
<span data-ttu-id="96043-174">Zie de volgende bronnen voor meer informatie over wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="96043-174">To learn more about queues, see the following resources.</span></span>

* <span data-ttu-id="96043-175">[Wachtrijen, onderwerpen en abonnementen][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="96043-175">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>
* <span data-ttu-id="96043-176">[Azure SDK voor knooppunt] [ Azure SDK for Node] opslagplaats op GitHub</span><span class="sxs-lookup"><span data-stu-id="96043-176">[Azure SDK for Node][Azure SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="96043-177">Node.js Developer Center</span><span class="sxs-lookup"><span data-stu-id="96043-177">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com

[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Create and deploy a Node.js application to an Azure Website]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-how-to-use-nodejs.md
[Service Bus quotas]: service-bus-quotas.md
