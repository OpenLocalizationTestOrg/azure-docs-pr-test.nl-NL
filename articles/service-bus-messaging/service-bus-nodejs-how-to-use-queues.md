---
title: aaaHow toouse Service Bus-wachtrijen in Node.js | Microsoft Docs
description: Meer informatie over hoe toouse Service Bus wachtrijen in Azure vanuit een Node.js-app.
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
ms.openlocfilehash: c55354b2061c41aba1093cc3f12ce2a1bc37a3cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-nodejs"></a><span data-ttu-id="a901a-103">Hoe toouse Service Bus wachtrijen met behulp van Node.js</span><span class="sxs-lookup"><span data-stu-id="a901a-103">How toouse Service Bus queues with Node.js</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="a901a-104">Dit artikel wordt beschreven hoe toouse Service Bus wachtrijen met behulp van Node.js.</span><span class="sxs-lookup"><span data-stu-id="a901a-104">This article describes how toouse Service Bus queues with Node.js.</span></span> <span data-ttu-id="a901a-105">Hallo-voorbeelden zijn geschreven in JavaScript en hello Node.js Azure-module gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a901a-105">hello samples are written in JavaScript and use hello Node.js Azure module.</span></span> <span data-ttu-id="a901a-106">Hallo scenario's worden behandeld: **maken van wachtrijen**, **verzenden en ontvangen berichten**, en **verwijderen van wachtrijen**.</span><span class="sxs-lookup"><span data-stu-id="a901a-106">hello scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span> <span data-ttu-id="a901a-107">Zie voor meer informatie over wachtrijen Hallo [Vervolgstappen](#next-steps) sectie.</span><span class="sxs-lookup"><span data-stu-id="a901a-107">For more information on queues, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="a901a-108">Een Node.js-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="a901a-108">Create a Node.js application</span></span>
<span data-ttu-id="a901a-109">Maak een lege Node.js-toepassing.</span><span class="sxs-lookup"><span data-stu-id="a901a-109">Create a blank Node.js application.</span></span> <span data-ttu-id="a901a-110">Voor instructies over het toocreate een Node.js-toepassing Zie [maken en implementeren van een Node.js-toepassing tooan Azure-Website][Create and deploy a Node.js application tooan Azure Website], of [Node.js-Cloudservice] [ Node.js Cloud Service] met Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a901a-110">For instructions on how toocreate a Node.js application, see [Create and deploy a Node.js application tooan Azure Website][Create and deploy a Node.js application tooan Azure Website], or [Node.js Cloud Service][Node.js Cloud Service] using Windows PowerShell.</span></span>

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="a901a-111">Configureren van uw toepassing toouse Service Bus</span><span class="sxs-lookup"><span data-stu-id="a901a-111">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="a901a-112">Azure Service Bus toouse downloaden en gebruiken van Hallo Node.js Azure-pakket.</span><span class="sxs-lookup"><span data-stu-id="a901a-112">toouse Azure Service Bus, download and use hello Node.js Azure package.</span></span> <span data-ttu-id="a901a-113">Dit pakket bevat een set van bibliotheken die met Hallo Service Bus REST-services communiceren.</span><span class="sxs-lookup"><span data-stu-id="a901a-113">This package includes a set of libraries that communicate with hello Service Bus REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="a901a-114">Knooppunt Package Manager (NPM) tooobtain Hallo pakket gebruiken</span><span class="sxs-lookup"><span data-stu-id="a901a-114">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="a901a-115">Gebruik Hallo **Windows PowerShell voor Node.js** opdracht venster toonavigate toohello **c:\\knooppunt\\sbqueues\\WebRole1** map waarin u hebt gemaakt uw Voorbeeld van een toepassing.</span><span class="sxs-lookup"><span data-stu-id="a901a-115">Use hello **Windows PowerShell for Node.js** command window toonavigate toohello **c:\\node\\sbqueues\\WebRole1** folder in which you created your sample application.</span></span>
2. <span data-ttu-id="a901a-116">Type **npm installeren azure** in opdrachtvenster hello, moet die leiden tot uitvoer vergelijkbare toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="a901a-116">Type **npm install azure** in hello command window, which should result in output similar toohello following:</span></span>

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
3. <span data-ttu-id="a901a-117">U kunt handmatig uitvoeren Hallo **ls** tooverify opdracht die een **node_modules** map is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a901a-117">You can manually run hello **ls** command tooverify that a **node_modules** folder was created.</span></span> <span data-ttu-id="a901a-118">Binnen die map zoeken Hallo **azure** , dit pakket bevat, moet u Service Bus-wachtrijen tooaccess Hallo-bibliotheken.</span><span class="sxs-lookup"><span data-stu-id="a901a-118">Inside that folder find hello **azure** package, which contains hello libraries you need tooaccess Service Bus queues.</span></span>

### <a name="import-hello-module"></a><span data-ttu-id="a901a-119">Hallo-module importeren</span><span class="sxs-lookup"><span data-stu-id="a901a-119">Import hello module</span></span>
<span data-ttu-id="a901a-120">Hallo toohello bovenaan hello te volgen in Kladblok of een andere teksteditor toevoegen **server.js** bestand van de toepassing hello:</span><span class="sxs-lookup"><span data-stu-id="a901a-120">Using Notepad or another text editor, add hello following toohello top of hello **server.js** file of hello application:</span></span>

```javascript
var azure = require('azure');
```

### <a name="set-up-an-azure-service-bus-connection"></a><span data-ttu-id="a901a-121">Een Azure Service Bus-verbinding instellen</span><span class="sxs-lookup"><span data-stu-id="a901a-121">Set up an Azure Service Bus connection</span></span>
<span data-ttu-id="a901a-122">Hello Azure module leest de omgevingsvariabele Hallo `AZURE_SERVICEBUS_CONNECTION_STRING` tooobtain informatie tooconnect tooService Bus vereist.</span><span class="sxs-lookup"><span data-stu-id="a901a-122">hello Azure module reads hello environment variable `AZURE_SERVICEBUS_CONNECTION_STRING` tooobtain information required tooconnect tooService Bus.</span></span> <span data-ttu-id="a901a-123">Als deze omgevingsvariabele niet is ingesteld, moet u de accountgegevens Hallo opgeven bij het aanroepen van `createServiceBusService`.</span><span class="sxs-lookup"><span data-stu-id="a901a-123">If this environment variable is not set, you must specify hello account information when calling `createServiceBusService`.</span></span>

<span data-ttu-id="a901a-124">Zie voor een voorbeeld van het Hallo omgevingsvariabelen instellen in een configuratiebestand voor een Azure Cloud Service [Node.js-Cloudservice met Storage][Node.js Cloud Service with Storage].</span><span class="sxs-lookup"><span data-stu-id="a901a-124">For an example of setting hello environment variables in a configuration file for an Azure Cloud Service, see [Node.js Cloud Service with Storage][Node.js Cloud Service with Storage].</span></span>

<span data-ttu-id="a901a-125">Voor een voorbeeld van het Hallo-omgevingsvariabelen instellen in Hallo [Azure-portal] [ Azure portal] Zie voor een Azure-Website [Node.js-webtoepassing met Storage] [ Node.js Web Application with Storage].</span><span class="sxs-lookup"><span data-stu-id="a901a-125">For an example of setting hello environment variables in hello [Azure portal][Azure portal] for an Azure Website, see [Node.js Web Application with Storage][Node.js Web Application with Storage].</span></span>

## <a name="create-a-queue"></a><span data-ttu-id="a901a-126">Een wachtrij maken</span><span class="sxs-lookup"><span data-stu-id="a901a-126">Create a queue</span></span>
<span data-ttu-id="a901a-127">Hallo **ServiceBusService** object kunt u toowork met Service Bus-wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="a901a-127">hello **ServiceBusService** object enables you toowork with Service Bus queues.</span></span> <span data-ttu-id="a901a-128">Hallo volgende code maakt een **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="a901a-128">hello following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="a901a-129">Voeg deze toe aan de bovenkant Hallo Hallo **server.js** bestand na Hallo instructie tooimport hello Azure-module:</span><span class="sxs-lookup"><span data-stu-id="a901a-129">Add it near hello top of hello **server.js** file, after hello statement tooimport hello Azure module:</span></span>

```javascript
var serviceBusService = azure.createServiceBusService();
```

<span data-ttu-id="a901a-130">Door het aanroepen van `createQueueIfNotExists` op Hallo **ServiceBusService** object, Hallo opgegeven wachtrij is geretourneerd (indien aanwezig) of een nieuwe wachtrij met de opgegeven naam hello wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="a901a-130">By calling `createQueueIfNotExists` on hello **ServiceBusService** object, hello specified queue is returned (if it exists), or a new queue with hello specified name is created.</span></span> <span data-ttu-id="a901a-131">Hallo volgende code gebruikt `createQueueIfNotExists` toocreate of verbinding maken met de naam toohello-wachtrij `myqueue`:</span><span class="sxs-lookup"><span data-stu-id="a901a-131">hello following code uses `createQueueIfNotExists` toocreate or connect toohello queue named `myqueue`:</span></span>

```javascript
serviceBusService.createQueueIfNotExists('myqueue', function(error){
    if(!error){
        // Queue exists
    }
});
```

<span data-ttu-id="a901a-132">Hallo `createServiceBusService` methode biedt ook ondersteuning voor extra opties waarmee u toooverride standaard wachtrij-instellingen zoals bericht tijd toolive of Maximale wachtrijgrootte.</span><span class="sxs-lookup"><span data-stu-id="a901a-132">hello `createServiceBusService` method also supports additional options, which enable you toooverride default queue settings such as message time toolive or maximum queue size.</span></span> <span data-ttu-id="a901a-133">Hallo volgende voorbeeld wordt Hallo wachtrij maximale grootte too5 GB en een tijd toolive (TTL)-waarde van 1 minuut:</span><span class="sxs-lookup"><span data-stu-id="a901a-133">hello following example sets hello maximum queue size too5 GB, and a time toolive (TTL) value of 1 minute:</span></span>

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

### <a name="filters"></a><span data-ttu-id="a901a-134">Filters</span><span class="sxs-lookup"><span data-stu-id="a901a-134">Filters</span></span>
<span data-ttu-id="a901a-135">Optionele filteren bewerkingen kunnen worden toegepast toooperations uitgevoerd met behulp van **ServiceBusService**.</span><span class="sxs-lookup"><span data-stu-id="a901a-135">Optional filtering operations can be applied toooperations performed using **ServiceBusService**.</span></span> <span data-ttu-id="a901a-136">Bewerkingen voor het filteren kunt opnemen logboekregistratie, automatisch opnieuw, enzovoort. Filters zijn objecten die een methode met Hallo handtekening te implementeren:</span><span class="sxs-lookup"><span data-stu-id="a901a-136">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```javascript
function handle (requestOptions, next)
```

<span data-ttu-id="a901a-137">Hierna moet u de vooraf verwerken op Hallo aanvraag opties, Hallo-methode moet aanroepen `next`, een retouraanroep wordt doorgegeven met Hallo handtekening te volgen:</span><span class="sxs-lookup"><span data-stu-id="a901a-137">After doing its pre-processing on hello request options, hello method must call `next`, passing a callback with hello following signature:</span></span>

```javascript
function (returnObject, finalCallback, next)
```

<span data-ttu-id="a901a-138">In deze retouraanroep en na verwerking Hallo `returnObject` (hello reactie van Hallo aanvraag toohello server), Hallo callback moet ofwel aanroepen `next` als deze bestaat toocontinue verwerking van andere filters of gewoon aanroepen `finalCallback`, welke ends Hallo service aanroepen.</span><span class="sxs-lookup"><span data-stu-id="a901a-138">In this callback, and after processing hello `returnObject` (hello response from hello request toohello server), hello callback must either invoke `next` if it exists toocontinue processing other filters, or simply invoke `finalCallback`, which ends hello service invocation.</span></span>

<span data-ttu-id="a901a-139">Twee filters die Pogingslogica implementeren zijn opgenomen in hello Azure SDK voor Node.js, `ExponentialRetryPolicyFilter` en `LinearRetryPolicyFilter`.</span><span class="sxs-lookup"><span data-stu-id="a901a-139">Two filters that implement retry logic are included with hello Azure SDK for Node.js, `ExponentialRetryPolicyFilter` and `LinearRetryPolicyFilter`.</span></span> <span data-ttu-id="a901a-140">Hallo volgende code maakt een `ServiceBusService` object dat gebruikmaakt van Hallo `ExponentialRetryPolicyFilter`:</span><span class="sxs-lookup"><span data-stu-id="a901a-140">hello following code creates a `ServiceBusService` object that uses hello `ExponentialRetryPolicyFilter`:</span></span>

```javascript
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var serviceBusService = azure.createServiceBusService().withFilter(retryOperations);
```

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="a901a-141">Berichten tooa wachtrij verzenden</span><span class="sxs-lookup"><span data-stu-id="a901a-141">Send messages tooa queue</span></span>
<span data-ttu-id="a901a-142">een bericht tooa Service Bus-wachtrij toosend, roept uw toepassing hello `sendQueueMessage` methode op Hallo **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="a901a-142">toosend a message tooa Service Bus queue, your application calls hello `sendQueueMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="a901a-143">Berichten verzonden te (en ontvangen van) Service Bus-wachtrijen zijn **BrokeredMessage** objecten en hebben een aantal standaardeigenschappen (zoals **Label** en **TimeToLive**), een de woordenlijst die wordt gebruikt toohold aangepaste toepassingsspecifieke eigenschappen en een hoofdtekst met willekeurige toepassingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="a901a-143">Messages sent too(and received from) Service Bus queues are **BrokeredMessage** objects, and have a set of standard properties (such as **Label** and **TimeToLive**), a dictionary that is used toohold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="a901a-144">Een toepassing kunt Hallo hoofdtekst van het Hallo-bericht instellen door een reeks wordt doorgegeven als het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="a901a-144">An application can set hello body of hello message by passing a string as hello message.</span></span> <span data-ttu-id="a901a-145">Alle vereiste eigenschappen standaard worden ingevuld met standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="a901a-145">Any required standard properties are populated with default values.</span></span>

<span data-ttu-id="a901a-146">Hallo volgende voorbeeld laat zien hoe toosend een test toohello berichtenwachtrij genoemd `myqueue` met `sendQueueMessage`:</span><span class="sxs-lookup"><span data-stu-id="a901a-146">hello following example demonstrates how toosend a test message toohello queue named `myqueue` using `sendQueueMessage`:</span></span>

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

<span data-ttu-id="a901a-147">Service Bus-wachtrijen ondersteunen een maximale berichtgrootte van 256 KB in Hallo [standaardcategorie](service-bus-premium-messaging.md) en 1 MB in Hallo [Premium-laag](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="a901a-147">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="a901a-148">Hallo-kop, die standaard Hallo- en aangepaste toepassingseigenschappen bevat, kan een maximale grootte van 64 KB hebben.</span><span class="sxs-lookup"><span data-stu-id="a901a-148">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="a901a-149">Er is geen limiet voor het aantal berichten in een wachtrij hello, maar er is een limiet voor de totale grootte van berichten in een wachtrij Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="a901a-149">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="a901a-150">De grootte van de wachtrij wordt gedefinieerd tijdens het aanmaken, met een bovengrens van 5 GB.</span><span class="sxs-lookup"><span data-stu-id="a901a-150">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="a901a-151">Zie voor meer informatie over quota [Service Bus-quota][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="a901a-151">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="a901a-152">Berichten ontvangen uit een wachtrij</span><span class="sxs-lookup"><span data-stu-id="a901a-152">Receive messages from a queue</span></span>
<span data-ttu-id="a901a-153">Berichten worden ontvangen van een wachtrij met Hallo `receiveQueueMessage` methode op Hallo **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="a901a-153">Messages are received from a queue using hello `receiveQueueMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="a901a-154">Standaard worden berichten uit Hallo wachtrij verwijderd als ze worden gelezen; echter (peek) lezen en vergrendelen Hallo-bericht zonder het te verwijderen uit de wachtrij Hallo door de optionele parameter Hallo instelling `isPeekLock` te**true**.</span><span class="sxs-lookup"><span data-stu-id="a901a-154">By default, messages are deleted from hello queue as they are read; however, you can read (peek) and lock hello message without deleting it from hello queue by setting hello optional parameter `isPeekLock` too**true**.</span></span>

<span data-ttu-id="a901a-155">Hallo standaardgedrag van lezen en Hallo-bericht is verwijderd als onderdeel van Hallo ontvangstbewerking is Hallo eenvoudigste model en werkt het beste voor scenario's waarin een toepassing kan tolereren niet verwerken van een bericht in de gebeurtenis Hallo van een fout.</span><span class="sxs-lookup"><span data-stu-id="a901a-155">hello default behavior of reading and deleting hello message as part of hello receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="a901a-156">toounderstand dit, Neem bijvoorbeeld een scenario in welke problemen van de consument Hallo Hallo aanvraag ontvangen en vervolgens vastloopt voordat het wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="a901a-156">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="a901a-157">Omdat Service Bus heeft gemarkeerd als verbruikt, vervolgens wanneer Hallo toepassing opnieuw wordt opgestart en verbruik van berichten opnieuw begint het Hallo-bericht, ontbreekt het Hallo-bericht dat was voorafgaande toohello crash verbruikt.</span><span class="sxs-lookup"><span data-stu-id="a901a-157">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="a901a-158">Als hello `isPeekLock` parameter is ingesteld, te**true**, Hallo ontvangen, wordt een bewerking met twee fasen, waardoor het mogelijk toosupport toepassingen die geen ontbrekende berichten kunnen tolereren.</span><span class="sxs-lookup"><span data-stu-id="a901a-158">If hello `isPeekLock` parameter is set too**true**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="a901a-159">Wanneer Service Bus een aanvraag ontvangt, zoeken naar het volgende bericht toobe Hallo verbruikt, wordt vergrendeld tooprevent andere consumenten het ontvangen en retourneert vervolgens toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="a901a-159">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="a901a-160">Nadat de toepassing hello klaar is met verwerking van het Hallo-bericht (of veilig heeft opgeslagen voor toekomstige verwerking), is de tweede fase Hallo Hallo voltooid proces ontvangen door het aanroepen van `deleteMessage` methode en het Hallo-bericht toobe verwijderd als een parameter geven.</span><span class="sxs-lookup"><span data-stu-id="a901a-160">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling `deleteMessage` method and providing hello message toobe deleted as a parameter.</span></span> <span data-ttu-id="a901a-161">Hallo `deleteMessage` methode markeert het Hallo-bericht als verbruikt en wordt deze verwijderd uit de wachtrij Hallo.</span><span class="sxs-lookup"><span data-stu-id="a901a-161">hello `deleteMessage` method marks hello message as being consumed and removes it from hello queue.</span></span>

<span data-ttu-id="a901a-162">Hallo volgende voorbeeld laat zien hoe tooreceive en proces berichten met behulp van `receiveQueueMessage`.</span><span class="sxs-lookup"><span data-stu-id="a901a-162">hello following example demonstrates how tooreceive and process messages using `receiveQueueMessage`.</span></span> <span data-ttu-id="a901a-163">Hallo voorbeeld eerst ontvangt een bericht wordt verwijderd en vervolgens ontvangt een bericht met `isPeekLock` instellen te**true**, en vervolgens verwijdert Hallo bericht met `deleteMessage`:</span><span class="sxs-lookup"><span data-stu-id="a901a-163">hello example first receives and deletes a message, and then receives a message using `isPeekLock` set too**true**, then deletes hello message using `deleteMessage`:</span></span>

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="a901a-164">Hoe toohandle toepassing is vastgelopen en onleesbare berichten</span><span class="sxs-lookup"><span data-stu-id="a901a-164">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="a901a-165">Service Bus biedt functionaliteit toohelp die u netjes te herstellen bij fouten in uw toepassing of problemen bij het verwerken van een bericht.</span><span class="sxs-lookup"><span data-stu-id="a901a-165">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="a901a-166">Als een ontvangende toepassing niet kan tooprocess hello bericht voor een bepaalde reden en vervolgens kan worden aangeroepen Hallo `unlockMessage` methode op Hallo **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="a901a-166">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on hello **ServiceBusService** object.</span></span> <span data-ttu-id="a901a-167">Dit wordt veroorzaakt toounlock Service Bus het bericht in de wachtrij Hallo en beschikbare toobe opnieuw ontvangen, ofwel Hallo door dezelfde toepassing of door een andere consumerende toepassing verbruikt.</span><span class="sxs-lookup"><span data-stu-id="a901a-167">This will cause Service Bus toounlock the message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="a901a-168">Daarnaast is er een time-out gekoppeld aan een bericht in de wachtrij Hallo is vergrendeld en als Hallo toepassing mislukt tooprocess Hallo-bericht voordat Hallo time-out van de vergrendeling verloopt (bijvoorbeeld als Hallo toepassing vastloopt), en vervolgens de Service Bus wordt het Hallo-bericht automatisch ontgrendelen en het beschikbaar toobe ontvangen opnieuw maken.</span><span class="sxs-lookup"><span data-stu-id="a901a-168">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (e.g., if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="a901a-169">In Hallo gebeurtenis die toepassing hello vastgelopen na het verwerken van het Hallo-bericht, maar voordat u Hallo `deleteMessage` methode wordt aangeroepen, is het Hallo-bericht altijd opnieuw bezorgd toohello toepassing opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="a901a-169">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="a901a-170">Dit wordt vaak genoemd *tenminste eenmaal verwerken*, dat wil zeggen elk bericht ten minste één keer wordt verwerkt maar in bepaalde situaties Hallo hetzelfde bericht opnieuw kan worden bezorgd.</span><span class="sxs-lookup"><span data-stu-id="a901a-170">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="a901a-171">Als Hallo scenario kan geen dubbele verwerking tolereren, moeten toepassingsontwikkelaars levering van aanvullende logica tootheir toepassing toohandle dubbele berichten toevoegen.</span><span class="sxs-lookup"><span data-stu-id="a901a-171">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="a901a-172">Dit wordt vaak bereikt met behulp van Hallo **MessageId** eigenschap van Hallo-bericht dat gelijk bij meerdere bezorgingspogingen blijft.</span><span class="sxs-lookup"><span data-stu-id="a901a-172">This is often achieved using hello **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a901a-173">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a901a-173">Next steps</span></span>
<span data-ttu-id="a901a-174">toolearn meer informatie over wachtrijen, Zie Hallo resources te volgen.</span><span class="sxs-lookup"><span data-stu-id="a901a-174">toolearn more about queues, see hello following resources.</span></span>

* <span data-ttu-id="a901a-175">[Wachtrijen, onderwerpen en abonnementen][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="a901a-175">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>
* <span data-ttu-id="a901a-176">[Azure SDK voor knooppunt] [ Azure SDK for Node] opslagplaats op GitHub</span><span class="sxs-lookup"><span data-stu-id="a901a-176">[Azure SDK for Node][Azure SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="a901a-177">Node.js Developer Center</span><span class="sxs-lookup"><span data-stu-id="a901a-177">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)

[Azure SDK for Node]: https://github.com/Azure/azure-sdk-for-node
[Azure portal]: https://portal.azure.com

[Node.js Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Create and deploy a Node.js application tooan Azure Website]: ../app-service-web/app-service-web-get-started-nodejs.md
[Node.js Cloud Service with Storage]:../cosmos-db/table-storage-cloud-service-nodejs.md
[Node.js Web Application with Storage]:../cosmos-db/table-storage-how-to-use-nodejs.md
[Service Bus quotas]: service-bus-quotas.md
