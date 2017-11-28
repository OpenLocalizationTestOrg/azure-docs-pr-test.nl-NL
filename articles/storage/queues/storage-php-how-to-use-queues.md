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
ms.openlocfilehash: 8daabcc9b3b4de121a309f21bb3325242cff06f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-php"></a><span data-ttu-id="56b71-104">Hoe toouse Queue storage met PHP</span><span class="sxs-lookup"><span data-stu-id="56b71-104">How toouse Queue storage from PHP</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="56b71-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="56b71-105">Overview</span></span>
<span data-ttu-id="56b71-106">Deze handleiding leert u hoe tooperform algemene scenario's met behulp van hello Azure Queue storage-service.</span><span class="sxs-lookup"><span data-stu-id="56b71-106">This guide will show you how tooperform common scenarios by using hello Azure Queue storage service.</span></span> <span data-ttu-id="56b71-107">Hallo-voorbeelden zijn geschreven via klassen van Hallo Windows SDK voor PHP.</span><span class="sxs-lookup"><span data-stu-id="56b71-107">hello samples are written via classes from hello Windows SDK for PHP.</span></span> <span data-ttu-id="56b71-108">Hallo gedekte scenario's omvatten invoegen, inspecteren, ophalen en en verwijderen van Wachtrijberichten, evenals maken en verwijderen van wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="56b71-108">hello covered scenarios include inserting, peeking, getting, and deleting queue messages, as well as creating and deleting queues.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="56b71-109">Een PHP-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="56b71-109">Create a PHP application</span></span>
<span data-ttu-id="56b71-110">alleen de vereiste voor het maken van een PHP-toepassing die toegang heeft tot de Azure Queue storage Hallo is Hallo verwijzende van klassen van hello Azure SDK voor PHP van binnen uw code.</span><span class="sxs-lookup"><span data-stu-id="56b71-110">hello only requirement for creating a PHP application that accesses Azure Queue storage is hello referencing of classes from hello Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="56b71-111">U kunt extra ontwikkeling toocreate uw toepassing, met inbegrip van Kladblok gebruiken.</span><span class="sxs-lookup"><span data-stu-id="56b71-111">You can use any development tools toocreate your application, including Notepad.</span></span>

<span data-ttu-id="56b71-112">In deze handleiding gebruikt u opslagfuncties wachtrij die kunnen worden aangeroepen binnen een PHP-toepassing lokaal of in de code die wordt uitgevoerd binnen een Azure-Webrol, werkrol of website.</span><span class="sxs-lookup"><span data-stu-id="56b71-112">In this guide, you will use Queue storage features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="56b71-113">Hello Azure-clientbibliotheken ophalen</span><span class="sxs-lookup"><span data-stu-id="56b71-113">Get hello Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-queue-storage"></a><span data-ttu-id="56b71-114">Uw toepassing tooaccess Queue storage configureren</span><span class="sxs-lookup"><span data-stu-id="56b71-114">Configure your application tooaccess Queue storage</span></span>
<span data-ttu-id="56b71-115">toouse hello API's voor Azure Queue storage, hebt u nodig:</span><span class="sxs-lookup"><span data-stu-id="56b71-115">toouse hello APIs for Azure Queue storage, you need to:</span></span>

1. <span data-ttu-id="56b71-116">Hallo autoloader referentiebestand via Hallo [require_once] instructie.</span><span class="sxs-lookup"><span data-stu-id="56b71-116">Reference hello autoloader file by using hello [require_once] statement.</span></span>
2. <span data-ttu-id="56b71-117">Verwijst naar alle klassen die u kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="56b71-117">Reference any classes that you might use.</span></span>

<span data-ttu-id="56b71-118">Hallo volgende voorbeeld laat zien hoe tooinclude autoloader bestands- en Hallo Hallo **ServicesBuilder** klasse.</span><span class="sxs-lookup"><span data-stu-id="56b71-118">hello following example shows how tooinclude hello autoloader file and reference hello **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="56b71-119">In dit voorbeeld (en andere voorbeelden in dit artikel) wordt ervan uitgegaan dat u Hallo PHP-clientbibliotheken voor Azure via Composer hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="56b71-119">This example (and other examples in this article) assumes that you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="56b71-120">Als u handmatig Hallo bibliotheken geïnstalleerd, moet u tooreference hello `WindowsAzure.php` autoloader-bestand.</span><span class="sxs-lookup"><span data-stu-id="56b71-120">If you installed hello libraries manually, you will need tooreference hello `WindowsAzure.php` autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

<span data-ttu-id="56b71-121">In onderstaande Hallo voorbeelden, Hallo `require_once` instructie altijd worden weergegeven, maar alleen Hallo-klassen die nodig voor Hallo voorbeeld tooexecute zijn wordt verwezen.</span><span class="sxs-lookup"><span data-stu-id="56b71-121">In hello examples below, hello `require_once` statement will be shown always, but only hello classes that are necessary for hello example tooexecute will be referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="56b71-122">Een Azure-opslag-verbinding instellen</span><span class="sxs-lookup"><span data-stu-id="56b71-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="56b71-123">een Azure Queue storage client tooinstantiate, moet u eerst een geldige verbindingsreeks hebben.</span><span class="sxs-lookup"><span data-stu-id="56b71-123">tooinstantiate an Azure Queue storage client, you must first have a valid connection string.</span></span> <span data-ttu-id="56b71-124">Hallo-indeling voor de verbindingsreeks voor wachtrij Hallo is als volgt.</span><span class="sxs-lookup"><span data-stu-id="56b71-124">hello format for hello queue service connection string is as follows.</span></span>

<span data-ttu-id="56b71-125">Voor toegang tot een service voor live:</span><span class="sxs-lookup"><span data-stu-id="56b71-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="56b71-126">Voor toegang tot Hallo emulator opslag:</span><span class="sxs-lookup"><span data-stu-id="56b71-126">For accessing hello emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="56b71-127">toocreate een Azure-service-client, moet u toouse hello **ServicesBuilder** klasse.</span><span class="sxs-lookup"><span data-stu-id="56b71-127">toocreate any Azure service client, you need toouse hello **ServicesBuilder** class.</span></span> <span data-ttu-id="56b71-128">U kunt een van volgende technieken hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="56b71-128">You can use either of hello following techniques:</span></span>

* <span data-ttu-id="56b71-129">Hallo verbinding doorgeven rechtstreeks tooit string.</span><span class="sxs-lookup"><span data-stu-id="56b71-129">Pass hello connection string directly tooit.</span></span>
* <span data-ttu-id="56b71-130">Gebruik **CloudConfigurationManager (CCM)** toocheck meerdere externe voor Hallo-verbindingsreeks gegevensbronnen:</span><span class="sxs-lookup"><span data-stu-id="56b71-130">Use **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="56b71-131">Standaard wordt geleverd met ondersteuning voor een externe bron: omgevingsvariabelen.</span><span class="sxs-lookup"><span data-stu-id="56b71-131">By default, it comes with support for one external source—environmental variables.</span></span>
  * <span data-ttu-id="56b71-132">U kunt nieuwe bronnen toevoegen door uit te breiden Hallo **ConnectionStringSource** klasse.</span><span class="sxs-lookup"><span data-stu-id="56b71-132">You can add new sources by extending hello **ConnectionStringSource** class.</span></span>

<span data-ttu-id="56b71-133">Voor Hallo voorbeelden die hier wordt beschreven, worden de verbindingsreeks Hallo rechtstreeks doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="56b71-133">For hello examples outlined here, hello connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="56b71-134">Een wachtrij maken</span><span class="sxs-lookup"><span data-stu-id="56b71-134">Create a queue</span></span>
<span data-ttu-id="56b71-135">Een **QueueRestProxy** object kunt u een wachtrij maken met behulp van Hallo **createQueue** methode.</span><span class="sxs-lookup"><span data-stu-id="56b71-135">A **QueueRestProxy** object lets you create a queue by using hello **createQueue** method.</span></span> <span data-ttu-id="56b71-136">Wanneer u een wachtrij maakt, kunt u opties in de wachtrij Hallo instellen, maar dit is dus niet vereist.</span><span class="sxs-lookup"><span data-stu-id="56b71-136">When creating a queue, you can set options on hello queue, but doing so is not required.</span></span> <span data-ttu-id="56b71-137">(voorbeeld hieronder toont hoe Hallo tooset metagegevens voor een wachtrij.)</span><span class="sxs-lookup"><span data-stu-id="56b71-137">(hello example below shows how tooset metadata on a queue.)</span></span>

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
> <span data-ttu-id="56b71-138">Niet verstandig hoofdlettergevoeligheid voor metagegevens sleutels.</span><span class="sxs-lookup"><span data-stu-id="56b71-138">You should not rely on case sensitivity for metadata keys.</span></span> <span data-ttu-id="56b71-139">Alle sleutels worden gelezen uit het Hallo-service in kleine letters.</span><span class="sxs-lookup"><span data-stu-id="56b71-139">All keys are read from hello service in lowercase.</span></span>
> 
> 

## <a name="add-a-message-tooa-queue"></a><span data-ttu-id="56b71-140">Een berichtenwachtrij tooa toevoegen</span><span class="sxs-lookup"><span data-stu-id="56b71-140">Add a message tooa queue</span></span>
<span data-ttu-id="56b71-141">gebruik van een berichtenwachtrij tooa tooadd **QueueRestProxy -> createMessage**.</span><span class="sxs-lookup"><span data-stu-id="56b71-141">tooadd a message tooa queue, use **QueueRestProxy->createMessage**.</span></span> <span data-ttu-id="56b71-142">Hallo-methode heeft Hallo wachtrijnaam, tekst hello en Berichtopties (die zijn optioneel).</span><span class="sxs-lookup"><span data-stu-id="56b71-142">hello method takes hello queue name, hello message text, and message options (which are optional).</span></span>

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

## <a name="peek-at-hello-next-message"></a><span data-ttu-id="56b71-143">Bekijken van volgende Hallo-bericht</span><span class="sxs-lookup"><span data-stu-id="56b71-143">Peek at hello next message</span></span>
<span data-ttu-id="56b71-144">U kunt bekijken van een bericht (of berichten) vooraan Hallo in een wachtrij zonder het te verwijderen uit de wachtrij Hallo door aan te roepen **QueueRestProxy -> peekMessages**.</span><span class="sxs-lookup"><span data-stu-id="56b71-144">You can peek at a message (or messages) at hello front of a queue without removing it from hello queue by calling **QueueRestProxy->peekMessages**.</span></span> <span data-ttu-id="56b71-145">Standaard Hallo **peekMessage** methode retourneert één bericht, maar u kunt deze waarde wijzigen met behulp van Hallo **PeekMessagesOptions -> setNumberOfMessages** methode.</span><span class="sxs-lookup"><span data-stu-id="56b71-145">By default, hello **peekMessage** method returns a single message, but you can change that value by using hello **PeekMessagesOptions->setNumberOfMessages** method.</span></span>

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

## <a name="de-queue-hello-next-message"></a><span data-ttu-id="56b71-146">Het volgende Hallo-bericht uit de wachtrij</span><span class="sxs-lookup"><span data-stu-id="56b71-146">De-queue hello next message</span></span>
<span data-ttu-id="56b71-147">Uw code wordt een bericht uit een wachtrij in twee stappen.</span><span class="sxs-lookup"><span data-stu-id="56b71-147">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="56b71-148">Eerst u aanroepen **QueueRestProxy -> listMessages**, waardoor Hallo-bericht onzichtbaar tooany andere code die wordt gelezen uit de wachtrij Hallo.</span><span class="sxs-lookup"><span data-stu-id="56b71-148">First, you call **QueueRestProxy->listMessages**, which makes hello message invisible tooany other code that's reading from hello queue.</span></span> <span data-ttu-id="56b71-149">Standaard wordt dit bericht onzichtbaar blijven gedurende 30 seconden.</span><span class="sxs-lookup"><span data-stu-id="56b71-149">By default, this message will stay invisible for 30 seconds.</span></span> <span data-ttu-id="56b71-150">(Als het Hallo-bericht is niet verwijderd in deze periode, deze wordt zichtbaar op Hallo wachtrij opnieuw.) toofinish verwijderen Hallo-bericht uit de wachtrij hello, moet u aanroepen **QueueRestProxy -> deleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="56b71-150">(If hello message is not deleted in this time period, it will become visible on hello queue again.) toofinish removing hello message from hello queue, you must call **QueueRestProxy->deleteMessage**.</span></span> <span data-ttu-id="56b71-151">Dit proces in twee stappen van het verwijderen van een bericht zorgt ervoor dat wanneer uw code mislukt tooprocess een bericht vanwege problemen toohardware of software, een ander exemplaar van uw code krijgt Hallo hetzelfde bericht en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="56b71-151">This two-step process of removing a message assures that when your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="56b71-152">Uw code haalt **deleteMessage** direct nadat het Hallo-bericht is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="56b71-152">Your code calls **deleteMessage** right after hello message has been processed.</span></span>

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

## <a name="change-hello-contents-of-a-queued-message"></a><span data-ttu-id="56b71-153">Hallo-inhoud van een bericht in de wachtrij wijzigen</span><span class="sxs-lookup"><span data-stu-id="56b71-153">Change hello contents of a queued message</span></span>
<span data-ttu-id="56b71-154">U kunt Hallo inhoud van een bericht in-place in wachtrij Hallo wijzigen door het aanroepen van **QueueRestProxy -> updateMessage**.</span><span class="sxs-lookup"><span data-stu-id="56b71-154">You can change hello contents of a message in-place in hello queue by calling **QueueRestProxy->updateMessage**.</span></span> <span data-ttu-id="56b71-155">Als het Hallo-bericht een werktaak vertegenwoordigt, kunt u deze functie tooupdate Hallo status van de werktaak hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="56b71-155">If hello message represents a work task, you could use this feature tooupdate hello status of hello work task.</span></span> <span data-ttu-id="56b71-156">Hallo na code Hallo-bericht van wachtrij bijgewerkt met nieuwe inhoud en stelt Hallo zichtbaarheid time-out tooextend 60 seconden.</span><span class="sxs-lookup"><span data-stu-id="56b71-156">hello following code updates hello queue message with new contents, and it sets hello visibility timeout tooextend another 60 seconds.</span></span> <span data-ttu-id="56b71-157">Hiermee slaat u Hallo status van de werkitems die is gekoppeld aan het Hallo-bericht en het Hallo-client biedt een andere minuut toocontinue werkt op het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="56b71-157">This saves hello state of work that's associated with hello message, and it gives hello client another minute toocontinue working on hello message.</span></span> <span data-ttu-id="56b71-158">U kunt deze techniek tootrack meerdere stappen bestaande werkstromen op Wachtrijberichten, zonder toostart via van Hallo begin als een verwerkingsstap vanwege problemen met toohardware of software.</span><span class="sxs-lookup"><span data-stu-id="56b71-158">You could use this technique tootrack multi-step workflows on queue messages, without having toostart over from hello beginning if a processing step fails due toohardware or software failure.</span></span> <span data-ttu-id="56b71-159">Doorgaans houdt u ook een aantal voor nieuwe pogingen en als hello bericht opnieuw wordt geprobeerd meer dan  *n*  tijdstippen, verwijdert u het.</span><span class="sxs-lookup"><span data-stu-id="56b71-159">Typically, you would keep a retry count as well, and if hello message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="56b71-160">Dit biedt bescherming tegen berichten die een toepassingsfout activeren telkens wanneer ze worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="56b71-160">This protects against a message that triggers an application error each time it is processed.</span></span>

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

## <a name="additional-options-for-de-queuing-messages"></a><span data-ttu-id="56b71-161">Aanvullende opties voor berichten in de wachtrij plaatsen</span><span class="sxs-lookup"><span data-stu-id="56b71-161">Additional options for de-queuing messages</span></span>
<span data-ttu-id="56b71-162">Er zijn twee manieren dat u ophalen van berichten uit een wachtrij kunt aanpassen.</span><span class="sxs-lookup"><span data-stu-id="56b71-162">There are two ways that you can customize message retrieval from a queue.</span></span> <span data-ttu-id="56b71-163">U krijgt eerst een batch met berichten (omhoog too32).</span><span class="sxs-lookup"><span data-stu-id="56b71-163">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="56b71-164">Ten tweede kunt u instellen een time-out langer of korter zichtbaarheid zodat uw code meer of minder tijd toofully elk bericht niet verwerken.</span><span class="sxs-lookup"><span data-stu-id="56b71-164">Second, you can set a longer or shorter visibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="56b71-165">Hallo volgende codevoorbeeld maakt gebruik van Hallo **getMessages** methode tooget 16 berichten in één aanroep.</span><span class="sxs-lookup"><span data-stu-id="56b71-165">hello following code example uses hello **getMessages** method tooget 16 messages in one call.</span></span> <span data-ttu-id="56b71-166">Vervolgens wordt elk bericht met behulp van verwerkt een **voor** lus.</span><span class="sxs-lookup"><span data-stu-id="56b71-166">Then it processes each message by using a **for** loop.</span></span> <span data-ttu-id="56b71-167">Hallo onzichtbaarheid toofive minuten voor de time-out voor elk bericht wordt ook ingesteld.</span><span class="sxs-lookup"><span data-stu-id="56b71-167">It also sets hello invisibility timeout toofive minutes for each message.</span></span>

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

## <a name="get-queue-length"></a><span data-ttu-id="56b71-168">Wachtrijlengte ophalen</span><span class="sxs-lookup"><span data-stu-id="56b71-168">Get queue length</span></span>
<span data-ttu-id="56b71-169">U kunt een schatting maken van het aantal berichten Hallo krijgen in een wachtrij.</span><span class="sxs-lookup"><span data-stu-id="56b71-169">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="56b71-170">Hallo **QueueRestProxy -> getQueueMetadata** methode vraagt Hallo wachtrij tooreturn metagegevens over Hallo wachtrij.</span><span class="sxs-lookup"><span data-stu-id="56b71-170">hello **QueueRestProxy->getQueueMetadata** method asks hello queue service tooreturn metadata about hello queue.</span></span> <span data-ttu-id="56b71-171">Aanroepen Hallo **getApproximateMessageCount** methode op Hallo geretourneerde object biedt een aantal van het aantal berichten in een wachtrij zijn.</span><span class="sxs-lookup"><span data-stu-id="56b71-171">Calling hello **getApproximateMessageCount** method on hello returned object provides a count of how many messages are in a queue.</span></span> <span data-ttu-id="56b71-172">Hallo aantal is alleen een benadering omdat berichten kunnen worden toegevoegd of verwijderd nadat de Hallo queue-service reageert tooyour aanvraag.</span><span class="sxs-lookup"><span data-stu-id="56b71-172">hello count is only approximate because messages can be added or removed after hello queue service responds tooyour request.</span></span>

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

## <a name="delete-a-queue"></a><span data-ttu-id="56b71-173">Een wachtrij verwijderen</span><span class="sxs-lookup"><span data-stu-id="56b71-173">Delete a queue</span></span>
<span data-ttu-id="56b71-174">toodelete een wachtrij en alle Hallo-berichten in dit aanroepen Hallo **QueueRestProxy -> deleteQueue** methode.</span><span class="sxs-lookup"><span data-stu-id="56b71-174">toodelete a queue and all hello messages in it, call hello **QueueRestProxy->deleteQueue** method.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="56b71-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="56b71-175">Next steps</span></span>
<span data-ttu-id="56b71-176">Nu u Hallo basisprincipes van Azure Queue storage hebt geleerd, volgt u deze koppelingen toolearn over complexere opslagtaken:</span><span class="sxs-lookup"><span data-stu-id="56b71-176">Now that you've learned hello basics of Azure Queue storage, follow these links toolearn about more complex storage tasks:</span></span>

* <span data-ttu-id="56b71-177">Ga naar Hallo [Azure Storage Team blog](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="56b71-177">Visit hello [Azure Storage Team blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>

<span data-ttu-id="56b71-178">Zie voor meer informatie, ook Hallo [PHP-ontwikkelaarscentrum](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="56b71-178">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://www.php.net/manual/en/function.require-once.php
[Azure Portal]: https://portal.azure.com

