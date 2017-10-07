---
title: aaaHow toouse Queue storage met PHP | Microsoft Docs
description: Ontdek hoe toouse hello Azure Queue storage-service toocreate en delete-wachtrijen en invoegen, ophalen en verwijderen van berichten. Voorbeelden zijn geschreven in PHP.
documentationcenter: php
services: storage
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 7582b208-4851-4489-a74a-bb952569f55b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 5034faf3b5f28f72d5b56ac1ce7a5723be697ce6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-php"></a>Hoe toouse Queue storage met PHP
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Overzicht
Deze handleiding leert u hoe tooperform algemene scenario's met behulp van hello Azure Queue storage-service. Hallo-voorbeelden zijn geschreven via klassen van Hallo Windows SDK voor PHP. Hallo gedekte scenario's omvatten invoegen, inspecteren, ophalen en en verwijderen van Wachtrijberichten, evenals maken en verwijderen van wachtrijen.

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>Een PHP-toepassing maken
alleen de vereiste voor het maken van een PHP-toepassing die toegang heeft tot de Azure Queue storage Hallo is Hallo verwijzende van klassen van hello Azure SDK voor PHP van binnen uw code. U kunt extra ontwikkeling toocreate uw toepassing, met inbegrip van Kladblok gebruiken.

In deze handleiding gebruikt u opslagfuncties wachtrij die kunnen worden aangeroepen binnen een PHP-toepassing lokaal of in de code die wordt uitgevoerd binnen een Azure-Webrol, werkrol of website.

## <a name="get-hello-azure-client-libraries"></a>Hello Azure-clientbibliotheken ophalen
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-queue-storage"></a>Uw toepassing tooaccess Queue storage configureren
toouse hello API's voor Azure Queue storage, hebt u nodig:

1. Hallo autoloader referentiebestand via Hallo [require_once] instructie.
2. Verwijst naar alle klassen die u kunt gebruiken.

Hallo volgende voorbeeld laat zien hoe tooinclude autoloader bestands- en Hallo Hallo **ServicesBuilder** klasse.

> [!NOTE]
> In dit voorbeeld (en andere voorbeelden in dit artikel) wordt ervan uitgegaan dat u Hallo PHP-clientbibliotheken voor Azure via Composer hebt geïnstalleerd. Als u handmatig Hallo bibliotheken geïnstalleerd, moet u tooreference hello `WindowsAzure.php` autoloader-bestand.
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

In onderstaande Hallo voorbeelden, Hallo `require_once` instructie altijd worden weergegeven, maar alleen Hallo-klassen die nodig voor Hallo voorbeeld tooexecute zijn wordt verwezen.

## <a name="set-up-an-azure-storage-connection"></a>Een Azure-opslag-verbinding instellen
een Azure Queue storage client tooinstantiate, moet u eerst een geldige verbindingsreeks hebben. Hallo-indeling voor de verbindingsreeks voor wachtrij Hallo is als volgt.

Voor toegang tot een service voor live:

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Voor toegang tot Hallo emulator opslag:

```php
UseDevelopmentStorage=true
```

toocreate een Azure-service-client, moet u toouse hello **ServicesBuilder** klasse. U kunt een van volgende technieken hello gebruiken:

* Hallo verbinding doorgeven rechtstreeks tooit string.
* Gebruik **CloudConfigurationManager (CCM)** toocheck meerdere externe voor Hallo-verbindingsreeks gegevensbronnen:
  * Standaard wordt geleverd met ondersteuning voor een externe bron: omgevingsvariabelen.
  * U kunt nieuwe bronnen toevoegen door uit te breiden Hallo **ConnectionStringSource** klasse.

Voor Hallo voorbeelden die hier wordt beschreven, worden de verbindingsreeks Hallo rechtstreeks doorgegeven.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a>Een wachtrij maken
Een **QueueRestProxy** object kunt u een wachtrij maken met behulp van Hallo **createQueue** methode. Wanneer u een wachtrij maakt, kunt u opties in de wachtrij Hallo instellen, maar dit is dus niet vereist. (voorbeeld hieronder toont hoe Hallo tooset metagegevens voor een wachtrij.)

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\CreateQueueOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// OPTIONAL: Set queue metadata.
$createQueueOptions = new CreateQueueOptions();
$createQueueOptions->addMetaData("key1", "value1");
$createQueueOptions->addMetaData("key2", "value2");

try    {
    // Create queue.
    $queueRestProxy->createQueue("myqueue", $createQueueOptions);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

> [!NOTE]
> Niet verstandig hoofdlettergevoeligheid voor metagegevens sleutels. Alle sleutels worden gelezen uit het Hallo-service in kleine letters.
> 
> 

## <a name="add-a-message-tooa-queue"></a>Een berichtenwachtrij tooa toevoegen
gebruik van een berichtenwachtrij tooa tooadd **QueueRestProxy -> createMessage**. Hallo-methode heeft Hallo wachtrijnaam, tekst hello en Berichtopties (die zijn optioneel).

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\CreateMessageOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Create message.
    $builder = new ServicesBuilder();
    $queueRestProxy->createMessage("myqueue", "Hello World!");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="peek-at-hello-next-message"></a>Bekijken van volgende Hallo-bericht
U kunt bekijken van een bericht (of berichten) vooraan Hallo in een wachtrij zonder het te verwijderen uit de wachtrij Hallo door aan te roepen **QueueRestProxy -> peekMessages**. Standaard Hallo **peekMessage** methode retourneert één bericht, maar u kunt deze waarde wijzigen met behulp van Hallo **PeekMessagesOptions -> setNumberOfMessages** methode.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\PeekMessagesOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// OPTIONAL: Set peek message options.
$message_options = new PeekMessagesOptions();
$message_options->setNumberOfMessages(1); // Default value is 1.

try    {
    $peekMessagesResult = $queueRestProxy->peekMessages("myqueue", $message_options);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

$messages = $peekMessagesResult->getQueueMessages();

// View messages.
$messageCount = count($messages);
if($messageCount <= 0){
    echo "There are no messages.<br />";
}
else{
    foreach($messages as $message)    {
        echo "Peeked message:<br />";
        echo "Message Id: ".$message->getMessageId()."<br />";
        echo "Date: ".date_format($message->getInsertionDate(), 'Y-m-d')."<br />";
        echo "Message text: ".$message->getMessageText()."<br /><br />";
    }
}
```

## <a name="de-queue-hello-next-message"></a>Het volgende Hallo-bericht uit de wachtrij
Uw code wordt een bericht uit een wachtrij in twee stappen. Eerst u aanroepen **QueueRestProxy -> listMessages**, waardoor Hallo-bericht onzichtbaar tooany andere code die wordt gelezen uit de wachtrij Hallo. Standaard wordt dit bericht onzichtbaar blijven gedurende 30 seconden. (Als het Hallo-bericht is niet verwijderd in deze periode, deze wordt zichtbaar op Hallo wachtrij opnieuw.) toofinish verwijderen Hallo-bericht uit de wachtrij hello, moet u aanroepen **QueueRestProxy -> deleteMessage**. Dit proces in twee stappen van het verwijderen van een bericht zorgt ervoor dat wanneer uw code mislukt tooprocess een bericht vanwege problemen toohardware of software, een ander exemplaar van uw code krijgt Hallo hetzelfde bericht en probeer het opnieuw. Uw code haalt **deleteMessage** direct nadat het Hallo-bericht is verwerkt.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Get message.
$listMessagesResult = $queueRestProxy->listMessages("myqueue");
$messages = $listMessagesResult->getQueueMessages();
$message = $messages[0];

/* ---------------------
    Process message.
   --------------------- */

// Get message ID and pop receipt.
$messageId = $message->getMessageId();
$popReceipt = $message->getPopReceipt();

try    {
    // Delete message.
    $queueRestProxy->deleteMessage("myqueue", $messageId, $popReceipt);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="change-hello-contents-of-a-queued-message"></a>Hallo-inhoud van een bericht in de wachtrij wijzigen
U kunt Hallo inhoud van een bericht in-place in wachtrij Hallo wijzigen door het aanroepen van **QueueRestProxy -> updateMessage**. Als het Hallo-bericht een werktaak vertegenwoordigt, kunt u deze functie tooupdate Hallo status van de werktaak hello gebruiken. Hallo na code Hallo-bericht van wachtrij bijgewerkt met nieuwe inhoud en stelt Hallo zichtbaarheid time-out tooextend 60 seconden. Hiermee slaat u Hallo status van de werkitems die is gekoppeld aan het Hallo-bericht en het Hallo-client biedt een andere minuut toocontinue werkt op het Hallo-bericht. U kunt deze techniek tootrack meerdere stappen bestaande werkstromen op Wachtrijberichten, zonder toostart via van Hallo begin als een verwerkingsstap vanwege problemen met toohardware of software. Doorgaans houdt u ook een aantal voor nieuwe pogingen en als hello bericht opnieuw wordt geprobeerd meer dan  *n*  tijdstippen, verwijdert u het. Dit biedt bescherming tegen berichten die een toepassingsfout activeren telkens wanneer ze worden verwerkt.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Get message.
$listMessagesResult = $queueRestProxy->listMessages("myqueue");
$messages = $listMessagesResult->getQueueMessages();
$message = $messages[0];

// Define new message properties.
$new_message_text = "New message text.";
$new_visibility_timeout = 5; // Measured in seconds.

// Get message ID and pop receipt.
$messageId = $message->getMessageId();
$popReceipt = $message->getPopReceipt();

try    {
    // Update message.
    $queueRestProxy->updateMessage("myqueue",
                                $messageId,
                                $popReceipt,
                                $new_message_text,
                                $new_visibility_timeout);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="additional-options-for-de-queuing-messages"></a>Aanvullende opties voor berichten in de wachtrij plaatsen
Er zijn twee manieren dat u ophalen van berichten uit een wachtrij kunt aanpassen. U krijgt eerst een batch met berichten (omhoog too32). Ten tweede kunt u instellen een time-out langer of korter zichtbaarheid zodat uw code meer of minder tijd toofully elk bericht niet verwerken. Hallo volgende codevoorbeeld maakt gebruik van Hallo **getMessages** methode tooget 16 berichten in één aanroep. Vervolgens wordt elk bericht met behulp van verwerkt een **voor** lus. Hallo onzichtbaarheid toofive minuten voor de time-out voor elk bericht wordt ook ingesteld.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;
use MicrosoftAzure\Storage\Queue\Models\ListMessagesOptions;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

// Set list message options.
$message_options = new ListMessagesOptions();
$message_options->setVisibilityTimeoutInSeconds(300);
$message_options->setNumberOfMessages(16);

// Get messages.
try{
    $listMessagesResult = $queueRestProxy->listMessages("myqueue",
                                                     $message_options);
    $messages = $listMessagesResult->getQueueMessages();

    foreach($messages as $message){

        /* ---------------------
            Process message.
        --------------------- */

        // Get message Id and pop receipt.
        $messageId = $message->getMessageId();
        $popReceipt = $message->getPopReceipt();

        // Delete message.
        $queueRestProxy->deleteMessage("myqueue", $messageId, $popReceipt);
    }
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="get-queue-length"></a>Wachtrijlengte ophalen
U kunt een schatting maken van het aantal berichten Hallo krijgen in een wachtrij. Hallo **QueueRestProxy -> getQueueMetadata** methode vraagt Hallo wachtrij tooreturn metagegevens over Hallo wachtrij. Aanroepen Hallo **getApproximateMessageCount** methode op Hallo geretourneerde object biedt een aantal van het aantal berichten in een wachtrij zijn. Hallo aantal is alleen een benadering omdat berichten kunnen worden toegevoegd of verwijderd nadat de Hallo queue-service reageert tooyour aanvraag.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Get queue metadata.
    $queue_metadata = $queueRestProxy->getQueueMetadata("myqueue");
    $approx_msg_count = $queue_metadata->getApproximateMessageCount();
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}

echo $approx_msg_count;
```

## <a name="delete-a-queue"></a>Een wachtrij verwijderen
toodelete een wachtrij en alle Hallo-berichten in dit aanroepen Hallo **QueueRestProxy -> deleteQueue** methode.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create queue REST proxy.
$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);

try    {
    // Delete queue.
    $queueRestProxy->deleteQueue("myqueue");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179446.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a>Volgende stappen
Nu u Hallo basisprincipes van Azure Queue storage hebt geleerd, volgt u deze koppelingen toolearn over complexere opslagtaken:

* Ga naar Hallo [Azure Storage Team blog](http://blogs.msdn.com/b/windowsazurestorage/).

Zie voor meer informatie, ook Hallo [PHP-ontwikkelaarscentrum](/develop/php/).

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://www.php.net/manual/en/function.require-once.php
[Azure Portal]: https://portal.azure.com

