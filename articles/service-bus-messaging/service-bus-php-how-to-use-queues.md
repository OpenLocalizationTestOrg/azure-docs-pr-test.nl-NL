---
title: aaaHow toouse Service Bus-wachtrijen met PHP | Microsoft Docs
description: Meer informatie over hoe toouse Service Bus wachtrijen in Azure. Codevoorbeelden geschreven in PHP.
services: service-bus-messaging
documentationcenter: php
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e29c829b-44c5-4350-8f2e-39e0c380a9f2
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 8cf233176029b679d172eaf713632087beca5e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-php"></a><span data-ttu-id="86c6b-104">Hoe toouse Service Bus wachtrijen met PHP</span><span class="sxs-lookup"><span data-stu-id="86c6b-104">How toouse Service Bus queues with PHP</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="86c6b-105">Deze handleiding ontdekt u hoe toouse Service Bus-wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="86c6b-105">This guide shows you how toouse Service Bus queues.</span></span> <span data-ttu-id="86c6b-106">Hallo-voorbeelden zijn geschreven in PHP en gebruiken van Hallo [Azure SDK voor PHP](../php-download-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="86c6b-106">hello samples are written in PHP and use hello [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="86c6b-107">Hallo scenario's worden behandeld: **maken van wachtrijen**, **verzenden en ontvangen berichten**, en **verwijderen van wachtrijen**.</span><span class="sxs-lookup"><span data-stu-id="86c6b-107">hello scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="86c6b-108">Een PHP-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="86c6b-108">Create a PHP application</span></span>
<span data-ttu-id="86c6b-109">alleen de vereiste voor het maken van een PHP-toepassing die toegang heeft tot hello Azure Blob-service is Hallo Hallo die verwijzen naar klassen in Hallo [Azure SDK voor PHP](../php-download-sdk.md) van binnen uw code.</span><span class="sxs-lookup"><span data-stu-id="86c6b-109">hello only requirement for creating a PHP application that accesses hello Azure Blob service is hello referencing of classes in hello [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="86c6b-110">U kunt development tools toocreate uw toepassing of Kladblok.</span><span class="sxs-lookup"><span data-stu-id="86c6b-110">You can use any development tools toocreate your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="86c6b-111">Uw PHP-installatie moet ook beschikken over Hallo [OpenSSL-extensie](http://php.net/openssl) geïnstalleerd en ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="86c6b-111">Your PHP installation must also have hello [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="86c6b-112">In deze handleiding gebruikt u de functies van de service die kunnen worden aangeroepen vanuit binnen een PHP-toepassing lokaal of in de code die wordt uitgevoerd binnen een Azure-Webrol, werkrol of website.</span><span class="sxs-lookup"><span data-stu-id="86c6b-112">In this guide, you will use service features which can be called from within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="86c6b-113">Hello Azure-clientbibliotheken ophalen</span><span class="sxs-lookup"><span data-stu-id="86c6b-113">Get hello Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="86c6b-114">Configureren van uw toepassing toouse Service Bus</span><span class="sxs-lookup"><span data-stu-id="86c6b-114">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="86c6b-115">toouse hello Service Bus-wachtrij-API's, Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="86c6b-115">toouse hello Service Bus queue APIs, do hello following:</span></span>

1. <span data-ttu-id="86c6b-116">Hallo autoloader referentiebestand Hallo met [require_once] [ require_once] instructie.</span><span class="sxs-lookup"><span data-stu-id="86c6b-116">Reference hello autoloader file using hello [require_once][require_once] statement.</span></span>
2. <span data-ttu-id="86c6b-117">Verwijst naar alle klassen die u kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="86c6b-117">Reference any classes you might use.</span></span>

<span data-ttu-id="86c6b-118">Hallo volgende voorbeeld laat zien hoe tooinclude autoloader bestands- en Hallo Hallo `ServicesBuilder` klasse.</span><span class="sxs-lookup"><span data-stu-id="86c6b-118">hello following example shows how tooinclude hello autoloader file and reference hello `ServicesBuilder` class.</span></span>

> [!NOTE]
> <span data-ttu-id="86c6b-119">In dit voorbeeld (en andere voorbeelden in dit artikel) wordt ervan uitgegaan dat u Hallo PHP-clientbibliotheken voor Azure via Composer hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="86c6b-119">This example (and other examples in this article) assumes you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="86c6b-120">Als u handmatig of als een pakket PEER Hallo bibliotheken hebt geïnstalleerd, moet u verwijzen naar Hallo **WindowsAzure.php** autoloader-bestand.</span><span class="sxs-lookup"><span data-stu-id="86c6b-120">If you installed hello libraries manually or as a PEAR package, you must reference hello **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="86c6b-121">In onderstaande Hallo voorbeelden, Hallo `require_once` instructie worden altijd weergegeven, maar alleen Hallo klassen nodig zijn voor Hallo voorbeeld tooexecute wordt verwezen.</span><span class="sxs-lookup"><span data-stu-id="86c6b-121">In hello examples below, hello `require_once` statement will always be shown, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="86c6b-122">Een Service Bus-verbinding instellen</span><span class="sxs-lookup"><span data-stu-id="86c6b-122">Set up a Service Bus connection</span></span>
<span data-ttu-id="86c6b-123">een Service Bus-clienttoepassing tooinstantiate, moet u eerst hebben een geldige verbindingsreeks in deze indeling:</span><span class="sxs-lookup"><span data-stu-id="86c6b-123">tooinstantiate a Service Bus client, you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="86c6b-124">Waar `Endpoint` is doorgaans Hallo indeling `[yourNamespace].servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="86c6b-124">Where `Endpoint` is typically of hello format `[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="86c6b-125">toocreate elke Azure-service-client moet u Hallo `ServicesBuilder` klasse.</span><span class="sxs-lookup"><span data-stu-id="86c6b-125">toocreate any Azure service client you must use hello `ServicesBuilder` class.</span></span> <span data-ttu-id="86c6b-126">U kunt:</span><span class="sxs-lookup"><span data-stu-id="86c6b-126">You can:</span></span>

* <span data-ttu-id="86c6b-127">Hallo verbinding doorgeven rechtstreeks tooit string.</span><span class="sxs-lookup"><span data-stu-id="86c6b-127">Pass hello connection string directly tooit.</span></span>
* <span data-ttu-id="86c6b-128">Gebruik Hallo **CloudConfigurationManager (CCM)** toocheck meerdere externe voor Hallo-verbindingsreeks gegevensbronnen:</span><span class="sxs-lookup"><span data-stu-id="86c6b-128">Use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="86c6b-129">Standaard wordt geleverd met ondersteuning voor een externe bron - omgevingsvariabelen</span><span class="sxs-lookup"><span data-stu-id="86c6b-129">By default it comes with support for one external source - environmental variables</span></span>
  * <span data-ttu-id="86c6b-130">U kunt nieuwe bronnen toevoegen door uit te breiden Hallo `ConnectionStringSource` klasse</span><span class="sxs-lookup"><span data-stu-id="86c6b-130">You can add new sources by extending hello `ConnectionStringSource` class</span></span>

<span data-ttu-id="86c6b-131">Voor Hallo voorbeelden die hier wordt beschreven, de verbindingsreeks Hallo rechtstreeks doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="86c6b-131">For hello examples outlined here, hello connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="86c6b-132">Een wachtrij maken</span><span class="sxs-lookup"><span data-stu-id="86c6b-132">Create a queue</span></span>
<span data-ttu-id="86c6b-133">U kunt beheerbewerkingen uitvoeren voor Service Bus-wachtrijen via Hallo `ServiceBusRestProxy` klasse.</span><span class="sxs-lookup"><span data-stu-id="86c6b-133">You can perform management operations for Service Bus queues via hello `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="86c6b-134">Een `ServiceBusRestProxy` -object is gemaakt via Hallo `ServicesBuilder::createServiceBusService` fabrieksmethode met een geschikte verbindingsreeks die ingekapseld Hallo token machtigingen toomanage deze.</span><span class="sxs-lookup"><span data-stu-id="86c6b-134">A `ServiceBusRestProxy` object is constructed via hello `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates hello token permissions toomanage it.</span></span>

<span data-ttu-id="86c6b-135">Hallo volgende voorbeeld wordt getoond hoe tooinstantiate een `ServiceBusRestProxy` en roep `ServiceBusRestProxy->createQueue` toocreate een wachtrij met de naam `myqueue` binnen een `MySBNamespace` Servicenaamruimte:</span><span class="sxs-lookup"><span data-stu-id="86c6b-135">hello following example shows how tooinstantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createQueue` toocreate a queue named `myqueue` within a `MySBNamespace` service namespace:</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\QueueInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    $queueInfo = new QueueInfo("myqueue");

    // Create queue.
    $serviceBusRestProxy->createQueue($queueInfo);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

> [!NOTE]
> <span data-ttu-id="86c6b-136">U kunt Hallo `listQueues` methode op `ServiceBusRestProxy` toocheck objecten als een wachtrij met een opgegeven naam al in een naamruimte bestaat.</span><span class="sxs-lookup"><span data-stu-id="86c6b-136">You can use hello `listQueues` method on `ServiceBusRestProxy` objects toocheck if a queue with a specified name already exists within a namespace.</span></span>
> 
> 

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="86c6b-137">Berichten tooa wachtrij verzenden</span><span class="sxs-lookup"><span data-stu-id="86c6b-137">Send messages tooa queue</span></span>
<span data-ttu-id="86c6b-138">een bericht tooa Service Bus-wachtrij toosend, roept uw toepassing hello `ServiceBusRestProxy->sendQueueMessage` methode.</span><span class="sxs-lookup"><span data-stu-id="86c6b-138">toosend a message tooa Service Bus queue, your application calls hello `ServiceBusRestProxy->sendQueueMessage` method.</span></span> <span data-ttu-id="86c6b-139">Hallo van de volgende code toont hoe een bericht toohello toosend `myqueue` wachtrij eerder hebt gemaakt in de `MySBNamespace` Servicenaamruimte.</span><span class="sxs-lookup"><span data-stu-id="86c6b-139">hello following code shows how toosend a message toohello `myqueue` queue previously created within the `MySBNamespace` service namespace.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\BrokeredMessage;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Create message.
    $message = new BrokeredMessage();
    $message->setBody("my message");

    // Send message.
    $serviceBusRestProxy->sendQueueMessage("myqueue", $message);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here: 
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="86c6b-140">Berichten verzonden te (en ontvangen van) Service Bus-wachtrijen, zijn exemplaren van Hallo [BrokeredMessage] [ BrokeredMessage] klasse.</span><span class="sxs-lookup"><span data-stu-id="86c6b-140">Messages sent too(and received from ) Service Bus queues are instances of hello [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="86c6b-141">[BrokeredMessage] [ BrokeredMessage] objecten hebben een aantal standaardmethoden en eigenschappen die gebruikte toohold aangepaste toepassingsspecifieke eigenschappen en een hoofdtekst met willekeurige toepassingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="86c6b-141">[BrokeredMessage][BrokeredMessage] objects have a set of standard methods and properties that are used toohold custom application-specific properties, and a body of arbitrary application data.</span></span>

<span data-ttu-id="86c6b-142">Service Bus-wachtrijen ondersteunen een maximale berichtgrootte van 256 KB in Hallo [standaardcategorie](service-bus-premium-messaging.md) en 1 MB in Hallo [Premium-laag](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="86c6b-142">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="86c6b-143">Hallo-kop, die standaard Hallo- en aangepaste toepassingseigenschappen bevat, kan een maximale grootte van 64 KB hebben.</span><span class="sxs-lookup"><span data-stu-id="86c6b-143">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="86c6b-144">Er is geen limiet voor het aantal berichten in een wachtrij hello, maar er is een limiet voor de totale grootte van berichten in een wachtrij Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="86c6b-144">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="86c6b-145">Deze bovengrens voor de grootte van de wachtrij is 5 GB.</span><span class="sxs-lookup"><span data-stu-id="86c6b-145">This upper limit on queue size is 5 GB.</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="86c6b-146">Berichten ontvangen uit een wachtrij</span><span class="sxs-lookup"><span data-stu-id="86c6b-146">Receive messages from a queue</span></span>

<span data-ttu-id="86c6b-147">Hallo aanbevolen manier tooreceive berichten uit een wachtrij toouse is een `ServiceBusRestProxy->receiveQueueMessage` methode.</span><span class="sxs-lookup"><span data-stu-id="86c6b-147">hello best way tooreceive messages from a queue is toouse a `ServiceBusRestProxy->receiveQueueMessage` method.</span></span> <span data-ttu-id="86c6b-148">Berichten kunnen worden ontvangen in twee verschillende modi: [ *ReceiveAndDelete* ](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) en [ *PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock).</span><span class="sxs-lookup"><span data-stu-id="86c6b-148">Messages can be received in two different modes: [*ReceiveAndDelete*](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) and [*PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock).</span></span> <span data-ttu-id="86c6b-149">**PeekLock** Hallo standaard is.</span><span class="sxs-lookup"><span data-stu-id="86c6b-149">**PeekLock** is hello default.</span></span>

<span data-ttu-id="86c6b-150">Wanneer u [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) -modus ontvangt een één bewerking uitgevoerd; dat wil zeggen als Service Bus een leesaanvraag voor een bericht in een wachtrij ontvangt, wordt markeert het Hallo-bericht als verbruikt en retourneert het toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="86c6b-150">When using [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a queue, it marks hello message as being consumed and returns it toohello application.</span></span> <span data-ttu-id="86c6b-151">[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) modus is Hallo eenvoudigste model en werkt het beste voor scenario's waarin een toepassing kan tolereren niet verwerken van een bericht in de gebeurtenis Hallo van een fout.</span><span class="sxs-lookup"><span data-stu-id="86c6b-151">[ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) mode is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="86c6b-152">toounderstand dit, Neem bijvoorbeeld een scenario in welke problemen van de consument Hallo Hallo aanvraag ontvangen en vervolgens vastloopt voordat het wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="86c6b-152">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="86c6b-153">Omdat Service Bus heeft gemarkeerd als verbruikt, vervolgens wanneer Hallo toepassing opnieuw wordt opgestart en verbruik van berichten opnieuw begint het Hallo-bericht, ontbreekt het Hallo-bericht dat was voorafgaande toohello crash verbruikt.</span><span class="sxs-lookup"><span data-stu-id="86c6b-153">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="86c6b-154">In de standaard Hallo [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) -modus ontvangt een bericht wordt een bewerking met twee fasen, waardoor het mogelijk toosupport toepassingen die geen ontbrekende berichten kunnen tolereren.</span><span class="sxs-lookup"><span data-stu-id="86c6b-154">In hello default [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode, receiving a message becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="86c6b-155">Wanneer Service Bus een aanvraag ontvangt, het Hallo volgende bericht toobe verbruikt vindt, wordt vergrendeld tooprevent andere consumenten ontvangen, en retourneert vervolgens toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="86c6b-155">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers from receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="86c6b-156">Nadat de toepassing hello klaar is met verwerking van het Hallo-bericht (of veilig heeft opgeslagen voor toekomstige verwerking), is de tweede fase Hallo Hallo voltooid proces door ontvangen Hallo-bericht te ontvangen`ServiceBusRestProxy->deleteMessage`.</span><span class="sxs-lookup"><span data-stu-id="86c6b-156">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by passing hello received message too`ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="86c6b-157">Wanneer Service Bus de aanroep Hallo `deleteMessage` aanroep, wordt het Hallo-bericht als verbruikt markeren en verwijderen uit de wachtrij Hallo.</span><span class="sxs-lookup"><span data-stu-id="86c6b-157">When Service Bus sees hello `deleteMessage` call, it will mark hello message as being consumed and remove it from hello queue.</span></span>

<span data-ttu-id="86c6b-158">Hallo volgende voorbeeld wordt getoond hoe tooreceive en verwerken van een bericht met [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) modus (Hallo standaardmodus).</span><span class="sxs-lookup"><span data-stu-id="86c6b-158">hello following example shows how tooreceive and process a message using [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) mode (hello default mode).</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set hello receive mode tooPeekLock (default is ReceiveAndDelete).
    $options = new ReceiveMessageOptions();
    $options->setPeekLock();

    // Receive message.
    $message = $serviceBusRestProxy->receiveQueueMessage("myqueue", $options);
    echo "Body: ".$message->getBody()."<br />";
    echo "MessageID: ".$message->getMessageId()."<br />";

    /*---------------------------
        Process message here.
    ----------------------------*/

    // Delete message. Not necessary if peek lock is not set.
    echo "Message deleted.<br />";
    $serviceBusRestProxy->deleteMessage($message);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // https://docs.microsoft.com/rest/api/storageservices/Common-REST-API-Error-Codes
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="86c6b-159">Hoe toohandle toepassing is vastgelopen en onleesbare berichten</span><span class="sxs-lookup"><span data-stu-id="86c6b-159">How toohandle application crashes and unreadable messages</span></span>

<span data-ttu-id="86c6b-160">Service Bus biedt functionaliteit toohelp die u netjes te herstellen bij fouten in uw toepassing of problemen bij het verwerken van een bericht.</span><span class="sxs-lookup"><span data-stu-id="86c6b-160">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="86c6b-161">Als een ontvangende toepassing niet kan tooprocess hello bericht voor een bepaalde reden en vervolgens kan worden aangeroepen Hallo `unlockMessage` methode voor het ontvangen Hallo-bericht (in plaats van Hallo `deleteMessage` methode).</span><span class="sxs-lookup"><span data-stu-id="86c6b-161">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on hello received message (instead of hello `deleteMessage` method).</span></span> <span data-ttu-id="86c6b-162">Hierdoor wordt ervoor zorgen dat Service Bus toounlock Hallo-bericht in de wachtrij Hallo en beschikbare toobe opnieuw ontvangen, ofwel Hallo door dezelfde toepassing of door een andere consumerende toepassing verbruikt.</span><span class="sxs-lookup"><span data-stu-id="86c6b-162">This will cause Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="86c6b-163">Daarnaast is er een time-out gekoppeld aan een bericht in de wachtrij Hallo is vergrendeld en als Hallo toepassing tooprocess Hallo-bericht voordat mislukt Hallo vergrendelingstime-out verloopt (bijvoorbeeld als Hallo toepassing vastloopt), en vervolgens de Service Bus wordt ontgrendeld Hallo-bericht automatisch en wordt het beschikbaar toobe opnieuw ontvangen.</span><span class="sxs-lookup"><span data-stu-id="86c6b-163">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="86c6b-164">In Hallo gebeurtenis die toepassing hello vastgelopen na het verwerken van het Hallo-bericht, maar voordat u Hallo `deleteMessage` verzoek is uitgegeven, is het Hallo-bericht altijd opnieuw bezorgd toohello toepassing opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="86c6b-164">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` request is issued, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="86c6b-165">Dit wordt vaak genoemd *tenminste eenmaal* verwerking; dat wil zeggen, elk bericht ten minste één keer wordt verwerkt, maar in bepaalde situaties Hallo hetzelfde bericht opnieuw kan worden bezorgd.</span><span class="sxs-lookup"><span data-stu-id="86c6b-165">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="86c6b-166">Als het Hallo-scenario niet kan tolereren dubbele verwerking en vervolgens toe te voegen extra wordt logica tooapplications toohandle dubbele berichtbezorging aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="86c6b-166">If hello scenario cannot tolerate duplicate processing, then adding additional logic tooapplications toohandle duplicate message delivery is recommended.</span></span> <span data-ttu-id="86c6b-167">Dit wordt vaak bereikt met behulp van Hallo `getMessageId` methode voor het Hallo-bericht dat gelijk blijft bij meerdere bezorgingspogingen.</span><span class="sxs-lookup"><span data-stu-id="86c6b-167">This is often achieved using hello `getMessageId` method of hello message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="86c6b-168">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="86c6b-168">Next steps</span></span>
<span data-ttu-id="86c6b-169">Nu u Hallo basisprincipes van Service Bus-wachtrijen hebt geleerd, gaat u naar [wachtrijen, onderwerpen en abonnementen] [ Queues, topics, and subscriptions] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="86c6b-169">Now that you've learned hello basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="86c6b-170">Bezoek voor meer informatie, ook Hallo [PHP-ontwikkelaarscentrum](https://azure.microsoft.com/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="86c6b-170">For more information, also visit hello [PHP Developer Center](https://azure.microsoft.com/develop/php/).</span></span>

[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[require_once]: http://php.net/require_once


