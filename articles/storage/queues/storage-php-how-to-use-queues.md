---
title: Hoe Queue storage gebruiken met PHP | Microsoft Docs
description: Informatie over het gebruik van de Azure Queue storage-service maken en verwijderen van wachtrijen, en invoegen, ophalen en verwijderen van berichten. Voorbeelden zijn geschreven in PHP.
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
ms.openlocfilehash: 12ebb905184e74da534cd44e8314335145f7042d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-queue-storage-from-php"></a>Queue Storage gebruiken met PHP
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a>Overzicht
Deze handleiding wordt beschreven hoe u veelvoorkomende scenario's uitvoeren met behulp van de Azure Queue storage-service. De voorbeelden zijn geschreven via klassen uit de Windows SDK voor PHP. De gedekte scenario's omvatten invoegen, inspecteren, ophalen en en verwijderen van Wachtrijberichten, evenals maken en verwijderen van wachtrijen.

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>Een PHP-toepassing maken
De enige vereiste voor het maken van een PHP-toepassing die toegang heeft tot Azure Queue storage is de verwijzende van klassen van de Azure SDK voor PHP vanuit uw code. Alle ontwikkelingsprogramma's kunt u uw toepassing, met inbegrip van Kladblok maken.

In deze handleiding gebruikt u opslagfuncties wachtrij die kunnen worden aangeroepen binnen een PHP-toepassing lokaal of in de code die wordt uitgevoerd binnen een Azure-Webrol, werkrol of website.

## <a name="get-the-azure-client-libraries"></a>De clientbibliotheken van Azure ophalen
[!INCLUDE [get-client-libraries](../../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-queue-storage"></a>Uw toepassing configureren voor toegang tot opslag van de wachtrij
De API's voor Azure Queue storage gebruiken, moet u naar:

1. Met behulp van een verwijzing naar het bestand van de autoloader van de [require_once] instructie.
2. Verwijst naar alle klassen die u kunt gebruiken.

Het volgende voorbeeld laat zien hoe de autoloader-bestand en de verwijzing naar de **ServicesBuilder** klasse.

> [!NOTE]
> In dit voorbeeld (en andere voorbeelden in dit artikel) wordt ervan uitgegaan dat u de PHP-clientbibliotheken voor Azure via Composer hebt geïnstalleerd. Als u handmatig de bibliotheken geïnstalleerd, moet u verwijzen naar de `WindowsAzure.php` autoloader-bestand.
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

In de onderstaande voorbeelden de `require_once` instructie altijd worden weergegeven, maar alleen de klassen die nodig zijn voor het voorbeeld uit te voeren wordt verwezen.

## <a name="set-up-an-azure-storage-connection"></a>Een Azure-opslag-verbinding instellen
U moet een geldige verbindingsreeks hebben voor het concretiseren van een Azure Queue storage-client. De indeling voor de verbindingsreeks voor de wachtrij is als volgt.

Voor toegang tot een service voor live:

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Voor toegang tot de emulator opslag:

```php
UseDevelopmentStorage=true
```

Voor het maken van een Azure-service-client die u wilt gebruiken, de **ServicesBuilder** klasse. U kunt een van de volgende technieken gebruiken:

* De verbindingsreeks rechtstreeks aan deze doorgeven.
* Gebruik **CloudConfigurationManager (CCM)** om te controleren van meerdere externe bronnen voor de verbindingsreeks:
  * Standaard wordt geleverd met ondersteuning voor een externe bron: omgevingsvariabelen.
  * U kunt nieuwe bronnen toevoegen door het uitbreiden van de **ConnectionStringSource** klasse.

Voor de voorbeelden die hier wordt beschreven, worden de verbindingsreeks rechtstreeks doorgegeven.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a>Een wachtrij maken
Een **QueueRestProxy** object kunt u een wachtrij maken met behulp van de **createQueue** methode. Wanneer u een wachtrij maakt, kunt u opties in de wachtrij instellen, maar dit is dus niet vereist. (Het volgende voorbeeld toont hoe metagegevens instelt op een wachtrij.)

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
> Niet verstandig hoofdlettergevoeligheid voor metagegevens sleutels. Alle sleutels worden gelezen uit de service in kleine letters.
> 
> 

## <a name="add-a-message-to-a-queue"></a>Een bericht toevoegen aan een wachtrij
U kunt een bericht toevoegen aan een wachtrij met **QueueRestProxy -> createMessage**. De methode heeft de naam van de wachtrij de berichttekst en Berichtopties (die zijn optioneel).

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

## <a name="peek-at-the-next-message"></a>Bekijken van het volgende bericht
U kunt bekijken van een bericht (of berichten) vooraan in een wachtrij zonder het te verwijderen uit de wachtrij door aan te roepen **QueueRestProxy -> peekMessages**. Standaard de **peekMessage** methode retourneert één bericht, maar u kunt deze waarde wijzigen met behulp van de **PeekMessagesOptions -> setNumberOfMessages** methode.

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

## <a name="de-queue-the-next-message"></a>Het volgende bericht uit de wachtrij verwijderen
Uw code wordt een bericht uit een wachtrij in twee stappen. Eerst u aanroepen **QueueRestProxy -> listMessages**, waardoor het bericht onzichtbaar voor andere code die wordt gelezen uit de wachtrij. Standaard wordt dit bericht onzichtbaar blijven gedurende 30 seconden. (Als het bericht is niet verwijderd in deze periode, deze wordt zichtbaar in de wachtrij opnieuw.) Voor het voltooien van het bericht uit de wachtrij te verwijderen, moet u aanroepen **QueueRestProxy -> deleteMessage**. Dit proces in twee stappen van het verwijderen van een bericht zorgt ervoor dat wanneer uw code niet kan een bericht vanwege problemen met hardware of software te verwerken, een ander exemplaar van uw code kunt het bericht verschijnt en probeer het opnieuw. Uw code haalt **deleteMessage** direct nadat het bericht is verwerkt.

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

## <a name="change-the-contents-of-a-queued-message"></a>De inhoud van een bericht in de wachtrij wijzigen
U kunt de inhoud van een bericht in-place in de wachtrij wijzigen door het aanroepen van **QueueRestProxy -> updateMessage**. Als het bericht een werktaak vertegenwoordigt, kunt u deze functie gebruiken om de status van de werktaak bij te werken. De volgende code bericht uit de wachtrij bijgewerkt met nieuwe inhoud en stelt time-out voor de zichtbaarheid 60 seconden verlengd. Hiermee slaat u de status van de werkitems die is gekoppeld aan het bericht en geeft de client een extra minuut om te blijven werken voor het bericht. U kunt deze techniek gebruiken om uit meerdere stappen bestaande werkstromen in berichten in de wachtrij te volgen zonder dat u helemaal opnieuw hoeft te beginnen als een verwerkingsstap vanwege een hardware- of softwarefout is mislukt. Doorgaans houdt u ook het aantal nieuwe pogingen bij en als het bericht meer dan *n* keer opnieuw is geprobeerd, verwijdert u het. Dit biedt bescherming tegen berichten die een toepassingsfout activeren telkens wanneer ze worden verwerkt.

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
Er zijn twee manieren dat u ophalen van berichten uit een wachtrij kunt aanpassen. Ten eerste kunt u berichten batchgewijs (maximaal 32) ophalen. Ten tweede kunt u instellen een time-out langer of korter zichtbaarheid zodat uw code meer of minder tijd voor het volledig verwerken van elk bericht. Het volgende codevoorbeeld wordt de **getMessages** methode 16 berichten in één aanroep ophalen. Vervolgens wordt elk bericht met behulp van verwerkt een **voor** lus. De time-out voor onzichtbaarheid wordt ingesteld op vijf minuten voor elk bericht.

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
U kunt een schatting ophalen van het aantal berichten in de wachtrij. De **QueueRestProxy -> getQueueMetadata** methode vraagt de queue-service om terug te keren metagegevens over de wachtrij. Het aanroepen van de **getApproximateMessageCount** methode voor het geretourneerde object biedt een aantal van het aantal berichten in een wachtrij zijn. Het aantal is alleen een benadering omdat berichten kunnen worden toegevoegd of verwijderd nadat de queue-service op uw aanvraag reageert.

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
Aanroepen voor het verwijderen van een wachtrij en de berichten in de **QueueRestProxy -> deleteQueue** methode.

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
Nu dat u de basisprincipes van Azure Queue storage hebt geleerd, volgt u deze koppelingen voor meer informatie over complexere opslagtaken:

* Ga naar de [Azure Storage Team blog](http://blogs.msdn.com/b/windowsazurestorage/).

Zie voor meer informatie, ook de [PHP-ontwikkelaarscentrum](/develop/php/).

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://www.php.net/manual/en/function.require-once.php
[Azure Portal]: https://portal.azure.com

