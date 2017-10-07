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
# <a name="how-toouse-service-bus-queues-with-php"></a>Hoe toouse Service Bus wachtrijen met PHP
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

Deze handleiding ontdekt u hoe toouse Service Bus-wachtrijen. Hallo-voorbeelden zijn geschreven in PHP en gebruiken van Hallo [Azure SDK voor PHP](../php-download-sdk.md). Hallo scenario's worden behandeld: **maken van wachtrijen**, **verzenden en ontvangen berichten**, en **verwijderen van wachtrijen**.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

## <a name="create-a-php-application"></a>Een PHP-toepassing maken
alleen de vereiste voor het maken van een PHP-toepassing die toegang heeft tot hello Azure Blob-service is Hallo Hallo die verwijzen naar klassen in Hallo [Azure SDK voor PHP](../php-download-sdk.md) van binnen uw code. U kunt development tools toocreate uw toepassing of Kladblok.

> [!NOTE]
> Uw PHP-installatie moet ook beschikken over Hallo [OpenSSL-extensie](http://php.net/openssl) geïnstalleerd en ingeschakeld.
> 
> 

In deze handleiding gebruikt u de functies van de service die kunnen worden aangeroepen vanuit binnen een PHP-toepassing lokaal of in de code die wordt uitgevoerd binnen een Azure-Webrol, werkrol of website.

## <a name="get-hello-azure-client-libraries"></a>Hello Azure-clientbibliotheken ophalen
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-toouse-service-bus"></a>Configureren van uw toepassing toouse Service Bus
toouse hello Service Bus-wachtrij-API's, Hallo te volgen:

1. Hallo autoloader referentiebestand Hallo met [require_once] [ require_once] instructie.
2. Verwijst naar alle klassen die u kunt gebruiken.

Hallo volgende voorbeeld laat zien hoe tooinclude autoloader bestands- en Hallo Hallo `ServicesBuilder` klasse.

> [!NOTE]
> In dit voorbeeld (en andere voorbeelden in dit artikel) wordt ervan uitgegaan dat u Hallo PHP-clientbibliotheken voor Azure via Composer hebt geïnstalleerd. Als u handmatig of als een pakket PEER Hallo bibliotheken hebt geïnstalleerd, moet u verwijzen naar Hallo **WindowsAzure.php** autoloader-bestand.
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

In onderstaande Hallo voorbeelden, Hallo `require_once` instructie worden altijd weergegeven, maar alleen Hallo klassen nodig zijn voor Hallo voorbeeld tooexecute wordt verwezen.

## <a name="set-up-a-service-bus-connection"></a>Een Service Bus-verbinding instellen
een Service Bus-clienttoepassing tooinstantiate, moet u eerst hebben een geldige verbindingsreeks in deze indeling:

```
Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]
```

Waar `Endpoint` is doorgaans Hallo indeling `[yourNamespace].servicebus.windows.net`.

toocreate elke Azure-service-client moet u Hallo `ServicesBuilder` klasse. U kunt:

* Hallo verbinding doorgeven rechtstreeks tooit string.
* Gebruik Hallo **CloudConfigurationManager (CCM)** toocheck meerdere externe voor Hallo-verbindingsreeks gegevensbronnen:
  * Standaard wordt geleverd met ondersteuning voor een externe bron - omgevingsvariabelen
  * U kunt nieuwe bronnen toevoegen door uit te breiden Hallo `ConnectionStringSource` klasse

Voor Hallo voorbeelden die hier wordt beschreven, de verbindingsreeks Hallo rechtstreeks doorgegeven.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$connectionString = "Endpoint=[yourEndpoint];SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[Primary Key]";

$serviceBusRestProxy = ServicesBuilder::getInstance()->createServiceBusService($connectionString);
```

## <a name="create-a-queue"></a>Een wachtrij maken
U kunt beheerbewerkingen uitvoeren voor Service Bus-wachtrijen via Hallo `ServiceBusRestProxy` klasse. Een `ServiceBusRestProxy` -object is gemaakt via Hallo `ServicesBuilder::createServiceBusService` fabrieksmethode met een geschikte verbindingsreeks die ingekapseld Hallo token machtigingen toomanage deze.

Hallo volgende voorbeeld wordt getoond hoe tooinstantiate een `ServiceBusRestProxy` en roep `ServiceBusRestProxy->createQueue` toocreate een wachtrij met de naam `myqueue` binnen een `MySBNamespace` Servicenaamruimte:

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
> U kunt Hallo `listQueues` methode op `ServiceBusRestProxy` toocheck objecten als een wachtrij met een opgegeven naam al in een naamruimte bestaat.
> 
> 

## <a name="send-messages-tooa-queue"></a>Berichten tooa wachtrij verzenden
een bericht tooa Service Bus-wachtrij toosend, roept uw toepassing hello `ServiceBusRestProxy->sendQueueMessage` methode. Hallo van de volgende code toont hoe een bericht toohello toosend `myqueue` wachtrij eerder hebt gemaakt in de `MySBNamespace` Servicenaamruimte.

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

Berichten verzonden te (en ontvangen van) Service Bus-wachtrijen, zijn exemplaren van Hallo [BrokeredMessage] [ BrokeredMessage] klasse. [BrokeredMessage] [ BrokeredMessage] objecten hebben een aantal standaardmethoden en eigenschappen die gebruikte toohold aangepaste toepassingsspecifieke eigenschappen en een hoofdtekst met willekeurige toepassingsgegevens.

Service Bus-wachtrijen ondersteunen een maximale berichtgrootte van 256 KB in Hallo [standaardcategorie](service-bus-premium-messaging.md) en 1 MB in Hallo [Premium-laag](service-bus-premium-messaging.md). Hallo-kop, die standaard Hallo- en aangepaste toepassingseigenschappen bevat, kan een maximale grootte van 64 KB hebben. Er is geen limiet voor het aantal berichten in een wachtrij hello, maar er is een limiet voor de totale grootte van berichten in een wachtrij Hallo Hallo. Deze bovengrens voor de grootte van de wachtrij is 5 GB.

## <a name="receive-messages-from-a-queue"></a>Berichten ontvangen uit een wachtrij

Hallo aanbevolen manier tooreceive berichten uit een wachtrij toouse is een `ServiceBusRestProxy->receiveQueueMessage` methode. Berichten kunnen worden ontvangen in twee verschillende modi: [ *ReceiveAndDelete* ](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) en [ *PeekLock*](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock). **PeekLock** Hallo standaard is.

Wanneer u [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) -modus ontvangt een één bewerking uitgevoerd; dat wil zeggen als Service Bus een leesaanvraag voor een bericht in een wachtrij ontvangt, wordt markeert het Hallo-bericht als verbruikt en retourneert het toohello toepassing. [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode.receiveanddelete) modus is Hallo eenvoudigste model en werkt het beste voor scenario's waarin een toepassing kan tolereren niet verwerken van een bericht in de gebeurtenis Hallo van een fout. toounderstand dit, Neem bijvoorbeeld een scenario in welke problemen van de consument Hallo Hallo aanvraag ontvangen en vervolgens vastloopt voordat het wordt verwerkt. Omdat Service Bus heeft gemarkeerd als verbruikt, vervolgens wanneer Hallo toepassing opnieuw wordt opgestart en verbruik van berichten opnieuw begint het Hallo-bericht, ontbreekt het Hallo-bericht dat was voorafgaande toohello crash verbruikt.

In de standaard Hallo [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) -modus ontvangt een bericht wordt een bewerking met twee fasen, waardoor het mogelijk toosupport toepassingen die geen ontbrekende berichten kunnen tolereren. Wanneer Service Bus een aanvraag ontvangt, het Hallo volgende bericht toobe verbruikt vindt, wordt vergrendeld tooprevent andere consumenten ontvangen, en retourneert vervolgens toohello toepassing. Nadat de toepassing hello klaar is met verwerking van het Hallo-bericht (of veilig heeft opgeslagen voor toekomstige verwerking), is de tweede fase Hallo Hallo voltooid proces door ontvangen Hallo-bericht te ontvangen`ServiceBusRestProxy->deleteMessage`. Wanneer Service Bus de aanroep Hallo `deleteMessage` aanroep, wordt het Hallo-bericht als verbruikt markeren en verwijderen uit de wachtrij Hallo.

Hallo volgende voorbeeld wordt getoond hoe tooreceive en verwerken van een bericht met [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode.peeklock) modus (Hallo standaardmodus).

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Hoe toohandle toepassing is vastgelopen en onleesbare berichten

Service Bus biedt functionaliteit toohelp die u netjes te herstellen bij fouten in uw toepassing of problemen bij het verwerken van een bericht. Als een ontvangende toepassing niet kan tooprocess hello bericht voor een bepaalde reden en vervolgens kan worden aangeroepen Hallo `unlockMessage` methode voor het ontvangen Hallo-bericht (in plaats van Hallo `deleteMessage` methode). Hierdoor wordt ervoor zorgen dat Service Bus toounlock Hallo-bericht in de wachtrij Hallo en beschikbare toobe opnieuw ontvangen, ofwel Hallo door dezelfde toepassing of door een andere consumerende toepassing verbruikt.

Daarnaast is er een time-out gekoppeld aan een bericht in de wachtrij Hallo is vergrendeld en als Hallo toepassing tooprocess Hallo-bericht voordat mislukt Hallo vergrendelingstime-out verloopt (bijvoorbeeld als Hallo toepassing vastloopt), en vervolgens de Service Bus wordt ontgrendeld Hallo-bericht automatisch en wordt het beschikbaar toobe opnieuw ontvangen.

In Hallo gebeurtenis die toepassing hello vastgelopen na het verwerken van het Hallo-bericht, maar voordat u Hallo `deleteMessage` verzoek is uitgegeven, is het Hallo-bericht altijd opnieuw bezorgd toohello toepassing opnieuw wordt gestart. Dit wordt vaak genoemd *tenminste eenmaal* verwerking; dat wil zeggen, elk bericht ten minste één keer wordt verwerkt, maar in bepaalde situaties Hallo hetzelfde bericht opnieuw kan worden bezorgd. Als het Hallo-scenario niet kan tolereren dubbele verwerking en vervolgens toe te voegen extra wordt logica tooapplications toohandle dubbele berichtbezorging aanbevolen. Dit wordt vaak bereikt met behulp van Hallo `getMessageId` methode voor het Hallo-bericht dat gelijk blijft bij meerdere bezorgingspogingen.

## <a name="next-steps"></a>Volgende stappen
Nu u Hallo basisprincipes van Service Bus-wachtrijen hebt geleerd, gaat u naar [wachtrijen, onderwerpen en abonnementen] [ Queues, topics, and subscriptions] voor meer informatie.

Bezoek voor meer informatie, ook Hallo [PHP-ontwikkelaarscentrum](https://azure.microsoft.com/develop/php/).

[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[require_once]: http://php.net/require_once


