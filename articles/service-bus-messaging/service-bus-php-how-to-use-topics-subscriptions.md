---
title: aaaHow toouse Service Bus-onderwerpen met PHP | Microsoft Docs
description: Meer informatie over hoe toouse Service Bus-onderwerpen met PHP in Azure.
services: service-bus-messaging
documentationcenter: php
author: sethmanheim
manager: timlt
editor: 
ms.assetid: faaa4bbd-f6ef-42ff-aca7-fc4353976449
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/27/2017
ms.author: sethm
ms.openlocfilehash: 0ca8625fa3edc5854c0d6c1c2f6adab6a2d42f91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-php"></a><span data-ttu-id="ad96f-103">Hoe toouse Service Bus-onderwerpen en abonnementen, met PHP</span><span class="sxs-lookup"><span data-stu-id="ad96f-103">How toouse Service Bus topics and subscriptions with PHP</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="ad96f-104">Dit artikel ziet u hoe toouse Service Bus-onderwerpen en abonnementen.</span><span class="sxs-lookup"><span data-stu-id="ad96f-104">This article shows you how toouse Service Bus topics and subscriptions.</span></span> <span data-ttu-id="ad96f-105">Hallo-voorbeelden zijn geschreven in PHP en gebruiken van Hallo [Azure SDK voor PHP](../php-download-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="ad96f-105">hello samples are written in PHP and use hello [Azure SDK for PHP](../php-download-sdk.md).</span></span> <span data-ttu-id="ad96f-106">Hallo scenario's worden behandeld: **maken van onderwerpen en abonnementen**, **maken van abonnementsfilters**, **verzenden van berichten tooa onderwerp**, **ontvangen berichten van een abonnement**, en **verwijderen van onderwerpen en abonnementen**.</span><span class="sxs-lookup"><span data-stu-id="ad96f-106">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages tooa topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="ad96f-107">Een PHP-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="ad96f-107">Create a PHP application</span></span>
<span data-ttu-id="ad96f-108">alleen vereiste voor het maken van een PHP-toepassing die toegang heeft tot hello Azure Blob-service tooreference klassen in Hallo is Hallo [Azure SDK voor PHP](../php-download-sdk.md) vanuit uw code.</span><span class="sxs-lookup"><span data-stu-id="ad96f-108">hello only requirement for creating a PHP application that accesses hello Azure Blob service is tooreference classes in hello [Azure SDK for PHP](../php-download-sdk.md) from within your code.</span></span> <span data-ttu-id="ad96f-109">U kunt development tools toocreate uw toepassing of Kladblok.</span><span class="sxs-lookup"><span data-stu-id="ad96f-109">You can use any development tools toocreate your application, or Notepad.</span></span>

> [!NOTE]
> <span data-ttu-id="ad96f-110">Uw PHP-installatie moet ook beschikken over Hallo [OpenSSL-extensie](http://php.net/openssl) geïnstalleerd en ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="ad96f-110">Your PHP installation must also have hello [OpenSSL extension](http://php.net/openssl) installed and enabled.</span></span>
> 
> 

<span data-ttu-id="ad96f-111">Dit artikel wordt beschreven hoe toouse functies die kunnen worden aangeroepen binnen een PHP-toepassing lokaal of in de code die wordt uitgevoerd binnen een Azure-Webrol, werkrol of website-service.</span><span class="sxs-lookup"><span data-stu-id="ad96f-111">This article describes how toouse service features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="ad96f-112">Hello Azure-clientbibliotheken ophalen</span><span class="sxs-lookup"><span data-stu-id="ad96f-112">Get hello Azure client libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="ad96f-113">Configureren van uw toepassing toouse Service Bus</span><span class="sxs-lookup"><span data-stu-id="ad96f-113">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="ad96f-114">toouse hello Service Bus-API's:</span><span class="sxs-lookup"><span data-stu-id="ad96f-114">toouse hello Service Bus APIs:</span></span>

1. <span data-ttu-id="ad96f-115">Hallo autoloader referentiebestand Hallo met [require_once] [ require-once] instructie.</span><span class="sxs-lookup"><span data-stu-id="ad96f-115">Reference hello autoloader file using hello [require_once][require-once] statement.</span></span>
2. <span data-ttu-id="ad96f-116">Verwijst naar alle klassen die u kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ad96f-116">Reference any classes you might use.</span></span>

<span data-ttu-id="ad96f-117">Hallo volgende voorbeeld laat zien hoe tooinclude autoloader bestands- en Hallo Hallo **ServiceBusService** klasse.</span><span class="sxs-lookup"><span data-stu-id="ad96f-117">hello following example shows how tooinclude hello autoloader file and reference hello **ServiceBusService** class.</span></span>

> [!NOTE]
> <span data-ttu-id="ad96f-118">In dit voorbeeld (en andere voorbeelden in dit artikel) wordt ervan uitgegaan dat u Hallo PHP-clientbibliotheken voor Azure via Composer hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ad96f-118">This example (and other examples in this article) assumes you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="ad96f-119">Als u handmatig of als een pakket PEER Hallo bibliotheken hebt geïnstalleerd, moet u verwijzen naar Hallo **WindowsAzure.php** autoloader-bestand.</span><span class="sxs-lookup"><span data-stu-id="ad96f-119">If you installed hello libraries manually or as a PEAR package, you must reference hello **WindowsAzure.php** autoloader file.</span></span>
> 
> 

```php
require_once 'vendor\autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="ad96f-120">Hallo in Hallo volgen voorbeelden, `require_once` instructie worden altijd weergegeven, maar alleen Hallo klassen nodig zijn voor Hallo voorbeeld tooexecute wordt verwezen.</span><span class="sxs-lookup"><span data-stu-id="ad96f-120">In hello following examples, hello `require_once` statement will always be shown, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-a-service-bus-connection"></a><span data-ttu-id="ad96f-121">Een Service Bus-verbinding instellen</span><span class="sxs-lookup"><span data-stu-id="ad96f-121">Set up a Service Bus connection</span></span>
<span data-ttu-id="ad96f-122">een Service Bus-client moet u eerst tooinstantiate hebben een geldige verbindingsreeks in deze indeling:</span><span class="sxs-lookup"><span data-stu-id="ad96f-122">tooinstantiate a Service Bus client you must first have a valid connection string in this format:</span></span>

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

<span data-ttu-id="ad96f-123">Waar `Endpoint` is doorgaans Hallo indeling `https://[yourNamespace].servicebus.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="ad96f-123">Where `Endpoint` is typically of hello format `https://[yourNamespace].servicebus.windows.net`.</span></span>

<span data-ttu-id="ad96f-124">toocreate elke Azure-service-client moet u Hallo `ServicesBuilder` klasse.</span><span class="sxs-lookup"><span data-stu-id="ad96f-124">toocreate any Azure service client you must use hello `ServicesBuilder` class.</span></span> <span data-ttu-id="ad96f-125">U kunt:</span><span class="sxs-lookup"><span data-stu-id="ad96f-125">You can:</span></span>

* <span data-ttu-id="ad96f-126">Hallo verbinding doorgeven rechtstreeks tooit string.</span><span class="sxs-lookup"><span data-stu-id="ad96f-126">Pass hello connection string directly tooit.</span></span>
* <span data-ttu-id="ad96f-127">Gebruik Hallo **CloudConfigurationManager (CCM)** toocheck meerdere externe voor Hallo-verbindingsreeks gegevensbronnen:</span><span class="sxs-lookup"><span data-stu-id="ad96f-127">Use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="ad96f-128">Standaard wordt geleverd met ondersteuning voor een externe bron - omgevingsvariabelen.</span><span class="sxs-lookup"><span data-stu-id="ad96f-128">By default it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="ad96f-129">U kunt nieuwe bronnen toevoegen door uit te breiden Hallo `ConnectionStringSource` klasse.</span><span class="sxs-lookup"><span data-stu-id="ad96f-129">You can add new sources by extending hello `ConnectionStringSource` class.</span></span>

<span data-ttu-id="ad96f-130">Voor Hallo voorbeelden die hier wordt beschreven, de verbindingsreeks Hallo rechtstreeks doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="ad96f-130">For hello examples outlined here, hello connection string is passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-topic"></a><span data-ttu-id="ad96f-131">Een onderwerp maken</span><span class="sxs-lookup"><span data-stu-id="ad96f-131">Create a topic</span></span>
<span data-ttu-id="ad96f-132">U kunt beheerbewerkingen uitvoeren voor Service Bus-onderwerpen via Hallo `ServiceBusRestProxy` klasse.</span><span class="sxs-lookup"><span data-stu-id="ad96f-132">You can perform management operations for Service Bus topics via hello `ServiceBusRestProxy` class.</span></span> <span data-ttu-id="ad96f-133">Een `ServiceBusRestProxy` -object is gemaakt via Hallo `ServicesBuilder::createServiceBusService` fabrieksmethode met een geschikte verbindingsreeks die ingekapseld Hallo token machtigingen toomanage deze.</span><span class="sxs-lookup"><span data-stu-id="ad96f-133">A `ServiceBusRestProxy` object is constructed via hello `ServicesBuilder::createServiceBusService` factory method with an appropriate connection string that encapsulates hello token permissions toomanage it.</span></span>

<span data-ttu-id="ad96f-134">Hallo volgende voorbeeld wordt getoond hoe tooinstantiate een `ServiceBusRestProxy` en roep `ServiceBusRestProxy->createTopic` toocreate een onderwerp met de naam `mytopic` binnen een `MySBNamespace` naamruimte:</span><span class="sxs-lookup"><span data-stu-id="ad96f-134">hello following example shows how tooinstantiate a `ServiceBusRestProxy` and call `ServiceBusRestProxy->createTopic` toocreate a topic named `mytopic` within a `MySBNamespace` namespace:</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\TopicInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {        
    // Create topic.
    $topicInfo = new TopicInfo("mytopic");
    $serviceBusRestProxy->createTopic($topicInfo);
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
> <span data-ttu-id="ad96f-135">U kunt Hallo `listTopics` methode op `ServiceBusRestProxy` toocheck objecten als een onderwerp met een opgegeven naam al in een Servicenaamruimte bestaat.</span><span class="sxs-lookup"><span data-stu-id="ad96f-135">You can use hello `listTopics` method on `ServiceBusRestProxy` objects toocheck if a topic with a specified name already exists within a service namespace.</span></span>
> 
> 

## <a name="create-a-subscription"></a><span data-ttu-id="ad96f-136">Een abonnement maken</span><span class="sxs-lookup"><span data-stu-id="ad96f-136">Create a subscription</span></span>
<span data-ttu-id="ad96f-137">Onderwerpabonnementen worden ook gemaakt met de Hallo `ServiceBusRestProxy->createSubscription` methode.</span><span class="sxs-lookup"><span data-stu-id="ad96f-137">Topic subscriptions are also created with hello `ServiceBusRestProxy->createSubscription` method.</span></span> <span data-ttu-id="ad96f-138">Abonnementen kunnen worden genoemd en een optioneel filter waarmee Hallo verzameling virtuele wachtrij van het abonnement toohello doorgegeven berichten wordt beperkt.</span><span class="sxs-lookup"><span data-stu-id="ad96f-138">Subscriptions are named and can have an optional filter that restricts hello set of messages passed toohello subscription's virtual queue.</span></span>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="ad96f-139">Een abonnement maken met de Hallo standaardfilter (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="ad96f-139">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="ad96f-140">Hallo **MatchAll** filter is Hallo standaardfilter dat wordt gebruikt als geen filter is opgegeven als een nieuw abonnement wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ad96f-140">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="ad96f-141">Wanneer Hallo **MatchAll** filter wordt gebruikt, worden alle berichten gepubliceerde toohello onderwerp in virtuele wachtrij van Hallo abonnement geplaatst.</span><span class="sxs-lookup"><span data-stu-id="ad96f-141">When hello **MatchAll** filter is used, all messages published toohello topic are placed in hello subscription's virtual queue.</span></span> <span data-ttu-id="ad96f-142">Hallo volgende voorbeeld maakt u een abonnement genaamd 'mysubscription' en gebruikt standaard Hallo **MatchAll** filter.</span><span class="sxs-lookup"><span data-stu-id="ad96f-142">hello following example creates a subscription named 'mysubscription' and uses hello default **MatchAll** filter.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\SubscriptionInfo;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Create subscription.
    $subscriptionInfo = new SubscriptionInfo("mysubscription");
    $serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);
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

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="ad96f-143">Abonnementen met filters maken</span><span class="sxs-lookup"><span data-stu-id="ad96f-143">Create subscriptions with filters</span></span>
<span data-ttu-id="ad96f-144">U kunt ook filters waarmee u welke berichten verzonden tooa onderwerp moet worden weergegeven binnen een bepaald onderwerpabonnement toospecify instellen.</span><span class="sxs-lookup"><span data-stu-id="ad96f-144">You can also set up filters that enable you toospecify which messages sent tooa topic should appear within a specific topic subscription.</span></span> <span data-ttu-id="ad96f-145">Hallo meest flexibele type filter dat wordt ondersteund door abonnementen is Hallo [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), waarmee een subset van SQL92 wordt geïmplementeerd implementeert.</span><span class="sxs-lookup"><span data-stu-id="ad96f-145">hello most flexible type of filter supported by subscriptions is hello [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), which implements a subset of SQL92.</span></span> <span data-ttu-id="ad96f-146">SQL-filters worden uitgevoerd op Hallo eigenschappen van Hallo-berichten die gepubliceerd toohello onderwerp zijn.</span><span class="sxs-lookup"><span data-stu-id="ad96f-146">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="ad96f-147">Zie voor meer informatie over SqlFilters [SqlFilter.SqlExpression eigenschap][sqlfilter].</span><span class="sxs-lookup"><span data-stu-id="ad96f-147">For more information about SqlFilters, see [SqlFilter.SqlExpression Property][sqlfilter].</span></span>

> [!NOTE]
> <span data-ttu-id="ad96f-148">Elke regel voor een abonnement binnenkomende berichten verwerkt onafhankelijk, het resultaat berichten toohello-abonnement toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="ad96f-148">Each rule on a subscription processes incoming messages independently, adding their result messages toohello subscription.</span></span> <span data-ttu-id="ad96f-149">Bovendien elk nieuw abonnement heeft een standaardwaarde **regel** object met een filter dat alle berichten uit Hallo onderwerp toohello abonnement toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="ad96f-149">In addition, each new subscription has a default **Rule** object with a filter that adds all messages from hello topic toohello subscription.</span></span> <span data-ttu-id="ad96f-150">tooreceive alleen berichten weer die overeenkomt met uw filter, moet u de standaardregel Hallo verwijderen.</span><span class="sxs-lookup"><span data-stu-id="ad96f-150">tooreceive only messages matching your filter, you must remove hello default rule.</span></span> <span data-ttu-id="ad96f-151">U kunt de standaardregel Hallo verwijderen via Hallo `ServiceBusRestProxy->deleteRule` methode.</span><span class="sxs-lookup"><span data-stu-id="ad96f-151">You can remove hello default rule by using hello `ServiceBusRestProxy->deleteRule` method.</span></span>
> 
> 

<span data-ttu-id="ad96f-152">Hallo volgende voorbeeld maakt u een abonnement met de naam `HighMessages` met een **SqlFilter** die alleen berichten selecteert die een aangepaste `MessageNumber` eigenschap groter is dan 3.</span><span class="sxs-lookup"><span data-stu-id="ad96f-152">hello following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `MessageNumber` property greater than 3.</span></span> <span data-ttu-id="ad96f-153">Zie [verzenden berichten tooa onderwerp](#send-messages-to-a-topic) voor informatie over het toevoegen van aangepaste eigenschappen toomessages.</span><span class="sxs-lookup"><span data-stu-id="ad96f-153">See [Send messages tooa topic](#send-messages-to-a-topic) for information about adding custom properties toomessages.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("HighMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "HighMessages", '$Default');

$ruleInfo = new RuleInfo("HighMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber > 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "HighMessages", $ruleInfo);
```

<span data-ttu-id="ad96f-154">Opmerking dat deze code Hallo gebruik van een extra naamruimte vereist: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.</span><span class="sxs-lookup"><span data-stu-id="ad96f-154">Note that this code requires hello use of an additional namespace: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.</span></span>

<span data-ttu-id="ad96f-155">Op deze manier hello volgende voorbeeld maakt u een abonnement met de naam `LowMessages` met een `SqlFilter` die alleen berichten selecteert die een `MessageNumber` eigenschap kleiner dan of gelijk too3.</span><span class="sxs-lookup"><span data-stu-id="ad96f-155">Similarly, hello following example creates a subscription named `LowMessages` with a `SqlFilter` that only selects messages that have a `MessageNumber` property less than or equal too3.</span></span>

```php
$subscriptionInfo = new SubscriptionInfo("LowMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "LowMessages", '$Default');

$ruleInfo = new RuleInfo("LowMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber <= 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "LowMessages", $ruleInfo);
```

<span data-ttu-id="ad96f-156">Nu wanneer een bericht verzonden toohello `mytopic` onderwerp, wordt het altijd bezorgd tooreceivers geabonneerd toohello `mysubscription` abonnement en selectief bezorgd tooreceivers geabonneerd toohello `HighMessages` en `LowMessages` (abonnementen afhankelijk van de inhoud van de Hallo-bericht).</span><span class="sxs-lookup"><span data-stu-id="ad96f-156">Now, when a message is sent toohello `mytopic` topic, it is always delivered tooreceivers subscribed toohello `mysubscription` subscription, and selectively delivered tooreceivers subscribed toohello `HighMessages` and `LowMessages` subscriptions (depending upon hello message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="ad96f-157">Verzenden van berichten tooa onderwerp</span><span class="sxs-lookup"><span data-stu-id="ad96f-157">Send messages tooa topic</span></span>
<span data-ttu-id="ad96f-158">een bericht tooa Service Bus-onderwerp toosend, roept uw toepassing hello `ServiceBusRestProxy->sendTopicMessage` methode.</span><span class="sxs-lookup"><span data-stu-id="ad96f-158">toosend a message tooa Service Bus topic, your application calls hello `ServiceBusRestProxy->sendTopicMessage` method.</span></span> <span data-ttu-id="ad96f-159">Hallo van de volgende code toont hoe een bericht toohello toosend `mytopic` onderwerp eerder hebt gemaakt in de `MySBNamespace` Servicenaamruimte.</span><span class="sxs-lookup"><span data-stu-id="ad96f-159">hello following code shows how toosend a message toohello `mytopic` topic previously created within the `MySBNamespace` service namespace.</span></span>

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
    $serviceBusRestProxy->sendTopicMessage("mytopic", $message);
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

<span data-ttu-id="ad96f-160">Berichten verzonden tooService Bus-onderwerpen, zijn exemplaren van Hallo [BrokeredMessage] [ BrokeredMessage] klasse.</span><span class="sxs-lookup"><span data-stu-id="ad96f-160">Messages sent tooService Bus topics are instances of hello [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="ad96f-161">[BrokeredMessage] [ BrokeredMessage] objecten hebben een aantal standaardeigenschappen en -methoden, evenals eigenschappen die gebruikt toohold aangepaste toepassingsspecifieke eigenschappen worden kunnen.</span><span class="sxs-lookup"><span data-stu-id="ad96f-161">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties and methods, as well as properties that can be used toohold custom application-specific properties.</span></span> <span data-ttu-id="ad96f-162">Hallo volgende voorbeeld laat zien hoe toosend 5 test toohello berichten `mytopic` onderwerp eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ad96f-162">hello following example shows how toosend 5 test messages toohello `mytopic` topic previously created.</span></span> <span data-ttu-id="ad96f-163">Hallo `setProperty` methode gebruikte tooadd een aangepaste eigenschap is (`MessageNumber`) tooeach bericht.</span><span class="sxs-lookup"><span data-stu-id="ad96f-163">hello `setProperty` method is used tooadd a custom property (`MessageNumber`) tooeach message.</span></span> <span data-ttu-id="ad96f-164">Houd er rekening mee dat Hallo `MessageNumber` waarde van de eigenschap varieert voor elk bericht (u kunt deze waarde toodetermine welke abonnementen ontvangen, zoals wordt weergegeven in Hallo [een abonnement maken](#create-a-subscription) sectie):</span><span class="sxs-lookup"><span data-stu-id="ad96f-164">Note that hello `MessageNumber` property value varies on each message (you can use this value toodetermine which subscriptions receive it, as shown in hello [Create a subscription](#create-a-subscription) section):</span></span>

```php
for($i = 0; $i < 5; $i++){
    // Create message.
    $message = new BrokeredMessage();
    $message->setBody("my message ".$i);

    // Set custom property.
    $message->setProperty("MessageNumber", $i);

    // Send message.
    $serviceBusRestProxy->sendTopicMessage("mytopic", $message);
}
```

<span data-ttu-id="ad96f-165">Service Bus-onderwerpen ondersteunen een maximale berichtgrootte van 256 KB in Hallo [standaardcategorie](service-bus-premium-messaging.md) en 1 MB in Hallo [Premium-laag](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="ad96f-165">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="ad96f-166">Hallo-kop, die standaard Hallo- en aangepaste toepassingseigenschappen bevat, kan een maximale grootte van 64 KB hebben.</span><span class="sxs-lookup"><span data-stu-id="ad96f-166">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="ad96f-167">Er is geen limiet voor het aantal berichten in een onderwerp hello, maar er is een limiet voor de totale grootte van berichten in een onderwerp Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="ad96f-167">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="ad96f-168">Deze bovengrens voor de grootte van het onderwerp is 5 GB.</span><span class="sxs-lookup"><span data-stu-id="ad96f-168">This upper limit on topic size is 5 GB.</span></span> <span data-ttu-id="ad96f-169">Zie voor meer informatie over quota [Service Bus-quota][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="ad96f-169">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="ad96f-170">Berichten ontvangen van een abonnement</span><span class="sxs-lookup"><span data-stu-id="ad96f-170">Receive messages from a subscription</span></span>
<span data-ttu-id="ad96f-171">Hallo aanbevolen manier tooreceive berichten van een abonnement is toouse een `ServiceBusRestProxy->receiveSubscriptionMessage` methode.</span><span class="sxs-lookup"><span data-stu-id="ad96f-171">hello best way tooreceive messages from a subscription is toouse a `ServiceBusRestProxy->receiveSubscriptionMessage` method.</span></span> <span data-ttu-id="ad96f-172">Berichten kunnen worden ontvangen in twee verschillende modi: [ *ReceiveAndDelete* en *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span><span class="sxs-lookup"><span data-stu-id="ad96f-172">Messages can be received in two different modes: [*ReceiveAndDelete* and *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode).</span></span> <span data-ttu-id="ad96f-173">**PeekLock** Hallo standaard is.</span><span class="sxs-lookup"><span data-stu-id="ad96f-173">**PeekLock** is hello default.</span></span>

<span data-ttu-id="ad96f-174">Bij gebruik van Hallo [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) -modus ontvangt een één bewerking uitgevoerd; dat wil zeggen als Service Bus een leesaanvraag voor een bericht in een abonnement ontvangt, wordt het Hallo-bericht als verbruikt markeert en toohello wordt geretourneerd de toepassing.</span><span class="sxs-lookup"><span data-stu-id="ad96f-174">When using hello [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receive is a single-shot operation; that is, when Service Bus receives a read request for a message in a subscription, it marks hello message as being consumed and returns it toohello application.</span></span> <span data-ttu-id="ad96f-175">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * modus is Hallo eenvoudigste model en werkt het beste voor scenario's waarin een toepassing kan tolereren niet verwerken van een bericht in de gebeurtenis Hallo van een fout.</span><span class="sxs-lookup"><span data-stu-id="ad96f-175">[ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * mode is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="ad96f-176">toounderstand dit, Neem bijvoorbeeld een scenario in welke problemen van de consument Hallo Hallo aanvraag ontvangen en vervolgens vastloopt voordat het wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="ad96f-176">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="ad96f-177">Omdat Service Bus heeft gemarkeerd als verbruikt, vervolgens wanneer Hallo toepassing opnieuw wordt opgestart en verbruik van berichten opnieuw begint het Hallo-bericht, ontbreekt het Hallo-bericht dat was voorafgaande toohello crash verbruikt.</span><span class="sxs-lookup"><span data-stu-id="ad96f-177">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="ad96f-178">In de standaard Hallo [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) -modus ontvangt een bericht wordt een bewerking met twee fasen, waardoor het mogelijk toosupport toepassingen die geen ontbrekende berichten kunnen tolereren.</span><span class="sxs-lookup"><span data-stu-id="ad96f-178">In hello default [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, receiving a message becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="ad96f-179">Wanneer Service Bus een aanvraag ontvangt, zoeken naar het volgende bericht toobe Hallo verbruikt, wordt vergrendeld tooprevent andere consumenten het ontvangen en retourneert vervolgens toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="ad96f-179">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="ad96f-180">Nadat de toepassing hello klaar is met verwerking van het Hallo-bericht (of veilig heeft opgeslagen voor toekomstige verwerking), is de tweede fase Hallo Hallo voltooid proces door ontvangen Hallo-bericht te ontvangen`ServiceBusRestProxy->deleteMessage`.</span><span class="sxs-lookup"><span data-stu-id="ad96f-180">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by passing hello received message too`ServiceBusRestProxy->deleteMessage`.</span></span> <span data-ttu-id="ad96f-181">Wanneer Service Bus de aanroep Hallo `deleteMessage` aanroep, wordt het Hallo-bericht als verbruikt markeren en verwijderen uit de wachtrij Hallo.</span><span class="sxs-lookup"><span data-stu-id="ad96f-181">When Service Bus sees hello `deleteMessage` call, it will mark hello message as being consumed and remove it from hello queue.</span></span>

<span data-ttu-id="ad96f-182">Hallo volgende voorbeeld wordt getoond hoe tooreceive en verwerken van een bericht met [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) modus (Hallo standaardmodus).</span><span class="sxs-lookup"><span data-stu-id="ad96f-182">hello following example shows how tooreceive and process a message using [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) mode (hello default mode).</span></span> 

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use WindowsAzure\Common\ServiceException;
use WindowsAzure\ServiceBus\Models\ReceiveMessageOptions;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {
    // Set receive mode tooPeekLock (default is ReceiveAndDelete)
    $options = new ReceiveMessageOptions();
    $options->setPeekLock();

    // Get message.
    $message = $serviceBusRestProxy->receiveSubscriptionMessage("mytopic", "mysubscription", $options);

    echo "Body: ".$message->getBody()."<br />";
    echo "MessageID: ".$message->getMessageId()."<br />";

    /*---------------------------
        Process message here.
    ----------------------------*/

    // Delete message. Not necessary if peek lock is not set.
    echo "Deleting message...<br />";
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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="ad96f-183">Hoe: vastlopen van de toepassing en onleesbare berichten afhandelen</span><span class="sxs-lookup"><span data-stu-id="ad96f-183">How to: handle application crashes and unreadable messages</span></span>
<span data-ttu-id="ad96f-184">Service Bus biedt functionaliteit toohelp die u netjes te herstellen bij fouten in uw toepassing of problemen bij het verwerken van een bericht.</span><span class="sxs-lookup"><span data-stu-id="ad96f-184">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="ad96f-185">Als een ontvangende toepassing niet kan tooprocess hello bericht voor een bepaalde reden en vervolgens kan worden aangeroepen Hallo `unlockMessage` methode voor het ontvangen Hallo-bericht (in plaats van Hallo `deleteMessage` methode).</span><span class="sxs-lookup"><span data-stu-id="ad96f-185">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlockMessage` method on hello received message (instead of hello `deleteMessage` method).</span></span> <span data-ttu-id="ad96f-186">Hierdoor wordt ervoor zorgen dat Service Bus toounlock Hallo-bericht in de wachtrij Hallo en beschikbare toobe opnieuw ontvangen, ofwel Hallo door dezelfde toepassing of door een andere consumerende toepassing verbruikt.</span><span class="sxs-lookup"><span data-stu-id="ad96f-186">This will cause Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="ad96f-187">Daarnaast is er een time-out gekoppeld aan een bericht in de wachtrij Hallo is vergrendeld en als Hallo toepassing tooprocess Hallo-bericht voordat mislukt Hallo vergrendelingstime-out verloopt (bijvoorbeeld als Hallo toepassing vastloopt), en vervolgens de Service Bus wordt ontgrendeld Hallo-bericht automatisch en wordt het beschikbaar toobe opnieuw ontvangen.</span><span class="sxs-lookup"><span data-stu-id="ad96f-187">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="ad96f-188">In Hallo gebeurtenis die toepassing hello vastgelopen na het verwerken van het Hallo-bericht, maar voordat u Hallo `deleteMessage` verzoek is uitgegeven, is het Hallo-bericht altijd opnieuw bezorgd toohello toepassing opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="ad96f-188">In hello event that hello application crashes after processing hello message but before hello `deleteMessage` request is issued, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="ad96f-189">Dit wordt vaak genoemd *tenminste eenmaal* verwerking; dat wil zeggen, elk bericht ten minste één keer wordt verwerkt, maar in bepaalde situaties Hallo hetzelfde bericht opnieuw kan worden bezorgd.</span><span class="sxs-lookup"><span data-stu-id="ad96f-189">This is often called *At Least Once* processing; that is, each message is processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="ad96f-190">Als Hallo scenario kan geen dubbele verwerking tolereren, moeten toepassingsontwikkelaars extra logica tooapplications toohandle dubbele berichtbezorging toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ad96f-190">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tooapplications toohandle duplicate message delivery.</span></span> <span data-ttu-id="ad96f-191">Dit wordt vaak bereikt met behulp van Hallo `getMessageId` methode voor het Hallo-bericht dat gelijk blijft bij meerdere bezorgingspogingen.</span><span class="sxs-lookup"><span data-stu-id="ad96f-191">This is often achieved using hello `getMessageId` method of hello message, which remains constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="ad96f-192">Onderwerpen en abonnementen verwijderen</span><span class="sxs-lookup"><span data-stu-id="ad96f-192">Delete topics and subscriptions</span></span>
<span data-ttu-id="ad96f-193">toodelete een onderwerp of een abonnement, gebruik Hallo `ServiceBusRestProxy->deleteTopic` of Hallo `ServiceBusRestProxy->deleteSubscripton` methoden, respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="ad96f-193">toodelete a topic or a subscription, use hello `ServiceBusRestProxy->deleteTopic` or hello `ServiceBusRestProxy->deleteSubscripton` methods, respectively.</span></span> <span data-ttu-id="ad96f-194">Houd er rekening mee dat als een onderwerp verwijdert tevens alle abonnementen die zijn geregistreerd bij Hallo onderwerp.</span><span class="sxs-lookup"><span data-stu-id="ad96f-194">Note that deleting a topic also deletes any subscriptions that are registered with hello topic.</span></span>

<span data-ttu-id="ad96f-195">Hallo volgende voorbeeld laat zien hoe toodelete een onderwerp met de naam `mytopic` en de geregistreerde abonnementen.</span><span class="sxs-lookup"><span data-stu-id="ad96f-195">hello following example shows how toodelete a topic named `mytopic` and its registered subscriptions.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\ServiceBus\ServiceBusService;
use WindowsAzure\ServiceBus\ServiceBusSettings;
use WindowsAzure\Common\ServiceException;

// Create Service Bus REST proxy.
$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);

try    {        
    // Delete topic.
    $serviceBusRestProxy->deleteTopic("mytopic");
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

<span data-ttu-id="ad96f-196">Met behulp van Hallo `deleteSubscription` methode, kunt u een abonnement onafhankelijk verwijderen:</span><span class="sxs-lookup"><span data-stu-id="ad96f-196">By using hello `deleteSubscription` method, you can delete a subscription independently:</span></span>

```php
$serviceBusRestProxy->deleteSubscription("mytopic", "mysubscription");
```

## <a name="next-steps"></a><span data-ttu-id="ad96f-197">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ad96f-197">Next steps</span></span>
<span data-ttu-id="ad96f-198">Nu u Hallo basisprincipes van Service Bus-wachtrijen hebt geleerd, gaat u naar [wachtrijen, onderwerpen en abonnementen] [ Queues, topics, and subscriptions] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ad96f-198">Now that you've learned hello basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

[BrokeredMessage]: https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[sqlfilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter
[require-once]: http://php.net/require_once
[Service Bus quotas]: service-bus-quotas.md
