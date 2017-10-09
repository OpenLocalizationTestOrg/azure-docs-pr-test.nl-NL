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
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-php"></a>Hoe toouse Service Bus-onderwerpen en abonnementen, met PHP

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

Dit artikel ziet u hoe toouse Service Bus-onderwerpen en abonnementen. Hallo-voorbeelden zijn geschreven in PHP en gebruiken van Hallo [Azure SDK voor PHP](../php-download-sdk.md). Hallo scenario's worden behandeld: **maken van onderwerpen en abonnementen**, **maken van abonnementsfilters**, **verzenden van berichten tooa onderwerp**, **ontvangen berichten van een abonnement**, en **verwijderen van onderwerpen en abonnementen**.

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

## <a name="create-a-php-application"></a>Een PHP-toepassing maken
alleen vereiste voor het maken van een PHP-toepassing die toegang heeft tot hello Azure Blob-service tooreference klassen in Hallo is Hallo [Azure SDK voor PHP](../php-download-sdk.md) vanuit uw code. U kunt development tools toocreate uw toepassing of Kladblok.

> [!NOTE]
> Uw PHP-installatie moet ook beschikken over Hallo [OpenSSL-extensie](http://php.net/openssl) geïnstalleerd en ingeschakeld.
> 
> 

Dit artikel wordt beschreven hoe toouse functies die kunnen worden aangeroepen binnen een PHP-toepassing lokaal of in de code die wordt uitgevoerd binnen een Azure-Webrol, werkrol of website-service.

## <a name="get-hello-azure-client-libraries"></a>Hello Azure-clientbibliotheken ophalen
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a>Configureren van uw toepassing toouse Service Bus
toouse hello Service Bus-API's:

1. Hallo autoloader referentiebestand Hallo met [require_once] [ require-once] instructie.
2. Verwijst naar alle klassen die u kunt gebruiken.

Hallo volgende voorbeeld laat zien hoe tooinclude autoloader bestands- en Hallo Hallo **ServiceBusService** klasse.

> [!NOTE]
> In dit voorbeeld (en andere voorbeelden in dit artikel) wordt ervan uitgegaan dat u Hallo PHP-clientbibliotheken voor Azure via Composer hebt geïnstalleerd. Als u handmatig of als een pakket PEER Hallo bibliotheken hebt geïnstalleerd, moet u verwijzen naar Hallo **WindowsAzure.php** autoloader-bestand.
> 
> 

```php
require_once 'vendor\autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

Hallo in Hallo volgen voorbeelden, `require_once` instructie worden altijd weergegeven, maar alleen Hallo klassen nodig zijn voor Hallo voorbeeld tooexecute wordt verwezen.

## <a name="set-up-a-service-bus-connection"></a>Een Service Bus-verbinding instellen
een Service Bus-client moet u eerst tooinstantiate hebben een geldige verbindingsreeks in deze indeling:

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

Waar `Endpoint` is doorgaans Hallo indeling `https://[yourNamespace].servicebus.windows.net`.

toocreate elke Azure-service-client moet u Hallo `ServicesBuilder` klasse. U kunt:

* Hallo verbinding doorgeven rechtstreeks tooit string.
* Gebruik Hallo **CloudConfigurationManager (CCM)** toocheck meerdere externe voor Hallo-verbindingsreeks gegevensbronnen:
  * Standaard wordt geleverd met ondersteuning voor een externe bron - omgevingsvariabelen.
  * U kunt nieuwe bronnen toevoegen door uit te breiden Hallo `ConnectionStringSource` klasse.

Voor Hallo voorbeelden die hier wordt beschreven, de verbindingsreeks Hallo rechtstreeks doorgegeven.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-topic"></a>Een onderwerp maken
U kunt beheerbewerkingen uitvoeren voor Service Bus-onderwerpen via Hallo `ServiceBusRestProxy` klasse. Een `ServiceBusRestProxy` -object is gemaakt via Hallo `ServicesBuilder::createServiceBusService` fabrieksmethode met een geschikte verbindingsreeks die ingekapseld Hallo token machtigingen toomanage deze.

Hallo volgende voorbeeld wordt getoond hoe tooinstantiate een `ServiceBusRestProxy` en roep `ServiceBusRestProxy->createTopic` toocreate een onderwerp met de naam `mytopic` binnen een `MySBNamespace` naamruimte:

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
> U kunt Hallo `listTopics` methode op `ServiceBusRestProxy` toocheck objecten als een onderwerp met een opgegeven naam al in een Servicenaamruimte bestaat.
> 
> 

## <a name="create-a-subscription"></a>Een abonnement maken
Onderwerpabonnementen worden ook gemaakt met de Hallo `ServiceBusRestProxy->createSubscription` methode. Abonnementen kunnen worden genoemd en een optioneel filter waarmee Hallo verzameling virtuele wachtrij van het abonnement toohello doorgegeven berichten wordt beperkt.

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Een abonnement maken met de Hallo standaardfilter (MatchAll)
Hallo **MatchAll** filter is Hallo standaardfilter dat wordt gebruikt als geen filter is opgegeven als een nieuw abonnement wordt gemaakt. Wanneer Hallo **MatchAll** filter wordt gebruikt, worden alle berichten gepubliceerde toohello onderwerp in virtuele wachtrij van Hallo abonnement geplaatst. Hallo volgende voorbeeld maakt u een abonnement genaamd 'mysubscription' en gebruikt standaard Hallo **MatchAll** filter.

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

### <a name="create-subscriptions-with-filters"></a>Abonnementen met filters maken
U kunt ook filters waarmee u welke berichten verzonden tooa onderwerp moet worden weergegeven binnen een bepaald onderwerpabonnement toospecify instellen. Hallo meest flexibele type filter dat wordt ondersteund door abonnementen is Hallo [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter), waarmee een subset van SQL92 wordt geïmplementeerd implementeert. SQL-filters worden uitgevoerd op Hallo eigenschappen van Hallo-berichten die gepubliceerd toohello onderwerp zijn. Zie voor meer informatie over SqlFilters [SqlFilter.SqlExpression eigenschap][sqlfilter].

> [!NOTE]
> Elke regel voor een abonnement binnenkomende berichten verwerkt onafhankelijk, het resultaat berichten toohello-abonnement toe te voegen. Bovendien elk nieuw abonnement heeft een standaardwaarde **regel** object met een filter dat alle berichten uit Hallo onderwerp toohello abonnement toegevoegd. tooreceive alleen berichten weer die overeenkomt met uw filter, moet u de standaardregel Hallo verwijderen. U kunt de standaardregel Hallo verwijderen via Hallo `ServiceBusRestProxy->deleteRule` methode.
> 
> 

Hallo volgende voorbeeld maakt u een abonnement met de naam `HighMessages` met een **SqlFilter** die alleen berichten selecteert die een aangepaste `MessageNumber` eigenschap groter is dan 3. Zie [verzenden berichten tooa onderwerp](#send-messages-to-a-topic) voor informatie over het toevoegen van aangepaste eigenschappen toomessages.

```php
$subscriptionInfo = new SubscriptionInfo("HighMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "HighMessages", '$Default');

$ruleInfo = new RuleInfo("HighMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber > 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "HighMessages", $ruleInfo);
```

Opmerking dat deze code Hallo gebruik van een extra naamruimte vereist: `WindowsAzure\ServiceBus\Models\SubscriptionInfo`.

Op deze manier hello volgende voorbeeld maakt u een abonnement met de naam `LowMessages` met een `SqlFilter` die alleen berichten selecteert die een `MessageNumber` eigenschap kleiner dan of gelijk too3.

```php
$subscriptionInfo = new SubscriptionInfo("LowMessages");
$serviceBusRestProxy->createSubscription("mytopic", $subscriptionInfo);

$serviceBusRestProxy->deleteRule("mytopic", "LowMessages", '$Default');

$ruleInfo = new RuleInfo("LowMessagesRule");
$ruleInfo->withSqlFilter("MessageNumber <= 3");
$ruleResult = $serviceBusRestProxy->createRule("mytopic", "LowMessages", $ruleInfo);
```

Nu wanneer een bericht verzonden toohello `mytopic` onderwerp, wordt het altijd bezorgd tooreceivers geabonneerd toohello `mysubscription` abonnement en selectief bezorgd tooreceivers geabonneerd toohello `HighMessages` en `LowMessages` (abonnementen afhankelijk van de inhoud van de Hallo-bericht).

## <a name="send-messages-tooa-topic"></a>Verzenden van berichten tooa onderwerp
een bericht tooa Service Bus-onderwerp toosend, roept uw toepassing hello `ServiceBusRestProxy->sendTopicMessage` methode. Hallo van de volgende code toont hoe een bericht toohello toosend `mytopic` onderwerp eerder hebt gemaakt in de `MySBNamespace` Servicenaamruimte.

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

Berichten verzonden tooService Bus-onderwerpen, zijn exemplaren van Hallo [BrokeredMessage] [ BrokeredMessage] klasse. [BrokeredMessage] [ BrokeredMessage] objecten hebben een aantal standaardeigenschappen en -methoden, evenals eigenschappen die gebruikt toohold aangepaste toepassingsspecifieke eigenschappen worden kunnen. Hallo volgende voorbeeld laat zien hoe toosend 5 test toohello berichten `mytopic` onderwerp eerder hebt gemaakt. Hallo `setProperty` methode gebruikte tooadd een aangepaste eigenschap is (`MessageNumber`) tooeach bericht. Houd er rekening mee dat Hallo `MessageNumber` waarde van de eigenschap varieert voor elk bericht (u kunt deze waarde toodetermine welke abonnementen ontvangen, zoals wordt weergegeven in Hallo [een abonnement maken](#create-a-subscription) sectie):

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

Service Bus-onderwerpen ondersteunen een maximale berichtgrootte van 256 KB in Hallo [standaardcategorie](service-bus-premium-messaging.md) en 1 MB in Hallo [Premium-laag](service-bus-premium-messaging.md). Hallo-kop, die standaard Hallo- en aangepaste toepassingseigenschappen bevat, kan een maximale grootte van 64 KB hebben. Er is geen limiet voor het aantal berichten in een onderwerp hello, maar er is een limiet voor de totale grootte van berichten in een onderwerp Hallo Hallo. Deze bovengrens voor de grootte van het onderwerp is 5 GB. Zie voor meer informatie over quota [Service Bus-quota][Service Bus quotas].

## <a name="receive-messages-from-a-subscription"></a>Berichten ontvangen van een abonnement
Hallo aanbevolen manier tooreceive berichten van een abonnement is toouse een `ServiceBusRestProxy->receiveSubscriptionMessage` methode. Berichten kunnen worden ontvangen in twee verschillende modi: [ *ReceiveAndDelete* en *PeekLock*](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode). **PeekLock** Hallo standaard is.

Bij gebruik van Hallo [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) -modus ontvangt een één bewerking uitgevoerd; dat wil zeggen als Service Bus een leesaanvraag voor een bericht in een abonnement ontvangt, wordt het Hallo-bericht als verbruikt markeert en toohello wordt geretourneerd de toepassing. [ReceiveAndDelete](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) * modus is Hallo eenvoudigste model en werkt het beste voor scenario's waarin een toepassing kan tolereren niet verwerken van een bericht in de gebeurtenis Hallo van een fout. toounderstand dit, Neem bijvoorbeeld een scenario in welke problemen van de consument Hallo Hallo aanvraag ontvangen en vervolgens vastloopt voordat het wordt verwerkt. Omdat Service Bus heeft gemarkeerd als verbruikt, vervolgens wanneer Hallo toepassing opnieuw wordt opgestart en verbruik van berichten opnieuw begint het Hallo-bericht, ontbreekt het Hallo-bericht dat was voorafgaande toohello crash verbruikt.

In de standaard Hallo [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) -modus ontvangt een bericht wordt een bewerking met twee fasen, waardoor het mogelijk toosupport toepassingen die geen ontbrekende berichten kunnen tolereren. Wanneer Service Bus een aanvraag ontvangt, zoeken naar het volgende bericht toobe Hallo verbruikt, wordt vergrendeld tooprevent andere consumenten het ontvangen en retourneert vervolgens toohello toepassing. Nadat de toepassing hello klaar is met verwerking van het Hallo-bericht (of veilig heeft opgeslagen voor toekomstige verwerking), is de tweede fase Hallo Hallo voltooid proces door ontvangen Hallo-bericht te ontvangen`ServiceBusRestProxy->deleteMessage`. Wanneer Service Bus de aanroep Hallo `deleteMessage` aanroep, wordt het Hallo-bericht als verbruikt markeren en verwijderen uit de wachtrij Hallo.

Hallo volgende voorbeeld wordt getoond hoe tooreceive en verwerken van een bericht met [PeekLock](https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.receivemode) modus (Hallo standaardmodus). 

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

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a>Hoe: vastlopen van de toepassing en onleesbare berichten afhandelen
Service Bus biedt functionaliteit toohelp die u netjes te herstellen bij fouten in uw toepassing of problemen bij het verwerken van een bericht. Als een ontvangende toepassing niet kan tooprocess hello bericht voor een bepaalde reden en vervolgens kan worden aangeroepen Hallo `unlockMessage` methode voor het ontvangen Hallo-bericht (in plaats van Hallo `deleteMessage` methode). Hierdoor wordt ervoor zorgen dat Service Bus toounlock Hallo-bericht in de wachtrij Hallo en beschikbare toobe opnieuw ontvangen, ofwel Hallo door dezelfde toepassing of door een andere consumerende toepassing verbruikt.

Daarnaast is er een time-out gekoppeld aan een bericht in de wachtrij Hallo is vergrendeld en als Hallo toepassing tooprocess Hallo-bericht voordat mislukt Hallo vergrendelingstime-out verloopt (bijvoorbeeld als Hallo toepassing vastloopt), en vervolgens de Service Bus wordt ontgrendeld Hallo-bericht automatisch en wordt het beschikbaar toobe opnieuw ontvangen.

In Hallo gebeurtenis die toepassing hello vastgelopen na het verwerken van het Hallo-bericht, maar voordat u Hallo `deleteMessage` verzoek is uitgegeven, is het Hallo-bericht altijd opnieuw bezorgd toohello toepassing opnieuw wordt gestart. Dit wordt vaak genoemd *tenminste eenmaal* verwerking; dat wil zeggen, elk bericht ten minste één keer wordt verwerkt, maar in bepaalde situaties Hallo hetzelfde bericht opnieuw kan worden bezorgd. Als Hallo scenario kan geen dubbele verwerking tolereren, moeten toepassingsontwikkelaars extra logica tooapplications toohandle dubbele berichtbezorging toevoegen. Dit wordt vaak bereikt met behulp van Hallo `getMessageId` methode voor het Hallo-bericht dat gelijk blijft bij meerdere bezorgingspogingen.

## <a name="delete-topics-and-subscriptions"></a>Onderwerpen en abonnementen verwijderen
toodelete een onderwerp of een abonnement, gebruik Hallo `ServiceBusRestProxy->deleteTopic` of Hallo `ServiceBusRestProxy->deleteSubscripton` methoden, respectievelijk. Houd er rekening mee dat als een onderwerp verwijdert tevens alle abonnementen die zijn geregistreerd bij Hallo onderwerp.

Hallo volgende voorbeeld laat zien hoe toodelete een onderwerp met de naam `mytopic` en de geregistreerde abonnementen.

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

Met behulp van Hallo `deleteSubscription` methode, kunt u een abonnement onafhankelijk verwijderen:

```php
$serviceBusRestProxy->deleteSubscription("mytopic", "mysubscription");
```

## <a name="next-steps"></a>Volgende stappen
Nu u Hallo basisprincipes van Service Bus-wachtrijen hebt geleerd, gaat u naar [wachtrijen, onderwerpen en abonnementen] [ Queues, topics, and subscriptions] voor meer informatie.

[BrokeredMessage]: https://docs.microsoft.com/dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[sqlfilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter
[require-once]: http://php.net/require_once
[Service Bus quotas]: service-bus-quotas.md
