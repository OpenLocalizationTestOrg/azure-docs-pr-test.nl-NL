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
# <a name="how-to-use-queue-storage-from-php"></a><span data-ttu-id="d9b03-104">Queue Storage gebruiken met PHP</span><span class="sxs-lookup"><span data-stu-id="d9b03-104">How to use Queue storage from PHP</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="d9b03-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="d9b03-105">Overview</span></span>
<span data-ttu-id="d9b03-106">Deze handleiding wordt beschreven hoe u veelvoorkomende scenario's uitvoeren met behulp van de Azure Queue storage-service.</span><span class="sxs-lookup"><span data-stu-id="d9b03-106">This guide will show you how to perform common scenarios by using the Azure Queue storage service.</span></span> <span data-ttu-id="d9b03-107">De voorbeelden zijn geschreven via klassen uit de Windows SDK voor PHP.</span><span class="sxs-lookup"><span data-stu-id="d9b03-107">The samples are written via classes from the Windows SDK for PHP.</span></span> <span data-ttu-id="d9b03-108">De gedekte scenario's omvatten invoegen, inspecteren, ophalen en en verwijderen van Wachtrijberichten, evenals maken en verwijderen van wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="d9b03-108">The covered scenarios include inserting, peeking, getting, and deleting queue messages, as well as creating and deleting queues.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="d9b03-109">Een PHP-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="d9b03-109">Create a PHP application</span></span>
<span data-ttu-id="d9b03-110">De enige vereiste voor het maken van een PHP-toepassing die toegang heeft tot Azure Queue storage is de verwijzende van klassen van de Azure SDK voor PHP vanuit uw code.</span><span class="sxs-lookup"><span data-stu-id="d9b03-110">The only requirement for creating a PHP application that accesses Azure Queue storage is the referencing of classes from the Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="d9b03-111">Alle ontwikkelingsprogramma's kunt u uw toepassing, met inbegrip van Kladblok maken.</span><span class="sxs-lookup"><span data-stu-id="d9b03-111">You can use any development tools to create your application, including Notepad.</span></span>

<span data-ttu-id="d9b03-112">In deze handleiding gebruikt u opslagfuncties wachtrij die kunnen worden aangeroepen binnen een PHP-toepassing lokaal of in de code die wordt uitgevoerd binnen een Azure-Webrol, werkrol of website.</span><span class="sxs-lookup"><span data-stu-id="d9b03-112">In this guide, you will use Queue storage features that can be called within a PHP application locally, or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="d9b03-113">De clientbibliotheken van Azure ophalen</span><span class="sxs-lookup"><span data-stu-id="d9b03-113">Get the Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-queue-storage"></a><span data-ttu-id="d9b03-114">Uw toepassing configureren voor toegang tot opslag van de wachtrij</span><span class="sxs-lookup"><span data-stu-id="d9b03-114">Configure your application to access Queue storage</span></span>
<span data-ttu-id="d9b03-115">De API's voor Azure Queue storage gebruiken, moet u naar:</span><span class="sxs-lookup"><span data-stu-id="d9b03-115">To use the APIs for Azure Queue storage, you need to:</span></span>

1. <span data-ttu-id="d9b03-116">Met behulp van een verwijzing naar het bestand van de autoloader van de [require_once] instructie.</span><span class="sxs-lookup"><span data-stu-id="d9b03-116">Reference the autoloader file by using the [require_once] statement.</span></span>
2. <span data-ttu-id="d9b03-117">Verwijst naar alle klassen die u kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d9b03-117">Reference any classes that you might use.</span></span>

<span data-ttu-id="d9b03-118">Het volgende voorbeeld laat zien hoe de autoloader-bestand en de verwijzing naar de **ServicesBuilder** klasse.</span><span class="sxs-lookup"><span data-stu-id="d9b03-118">The following example shows how to include the autoloader file and reference the **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="d9b03-119">In dit voorbeeld (en andere voorbeelden in dit artikel) wordt ervan uitgegaan dat u de PHP-clientbibliotheken voor Azure via Composer hebt geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="d9b03-119">This example (and other examples in this article) assumes that you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="d9b03-120">Als u handmatig de bibliotheken geïnstalleerd, moet u verwijzen naar de `WindowsAzure.php` autoloader-bestand.</span><span class="sxs-lookup"><span data-stu-id="d9b03-120">If you installed the libraries manually, you will need to reference the `WindowsAzure.php` autoloader file.</span></span>
> 
> 

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;

```

<span data-ttu-id="d9b03-121">In de onderstaande voorbeelden de `require_once` instructie altijd worden weergegeven, maar alleen de klassen die nodig zijn voor het voorbeeld uit te voeren wordt verwezen.</span><span class="sxs-lookup"><span data-stu-id="d9b03-121">In the examples below, the `require_once` statement will be shown always, but only the classes that are necessary for the example to execute will be referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="d9b03-122">Een Azure-opslag-verbinding instellen</span><span class="sxs-lookup"><span data-stu-id="d9b03-122">Set up an Azure storage connection</span></span>
<span data-ttu-id="d9b03-123">U moet een geldige verbindingsreeks hebben voor het concretiseren van een Azure Queue storage-client.</span><span class="sxs-lookup"><span data-stu-id="d9b03-123">To instantiate an Azure Queue storage client, you must first have a valid connection string.</span></span> <span data-ttu-id="d9b03-124">De indeling voor de verbindingsreeks voor de wachtrij is als volgt.</span><span class="sxs-lookup"><span data-stu-id="d9b03-124">The format for the queue service connection string is as follows.</span></span>

<span data-ttu-id="d9b03-125">Voor toegang tot een service voor live:</span><span class="sxs-lookup"><span data-stu-id="d9b03-125">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="d9b03-126">Voor toegang tot de emulator opslag:</span><span class="sxs-lookup"><span data-stu-id="d9b03-126">For accessing the emulator storage:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="d9b03-127">Voor het maken van een Azure-service-client die u wilt gebruiken, de **ServicesBuilder** klasse.</span><span class="sxs-lookup"><span data-stu-id="d9b03-127">To create any Azure service client, you need to use the **ServicesBuilder** class.</span></span> <span data-ttu-id="d9b03-128">U kunt een van de volgende technieken gebruiken:</span><span class="sxs-lookup"><span data-stu-id="d9b03-128">You can use either of the following techniques:</span></span>

* <span data-ttu-id="d9b03-129">De verbindingsreeks rechtstreeks aan deze doorgeven.</span><span class="sxs-lookup"><span data-stu-id="d9b03-129">Pass the connection string directly to it.</span></span>
* <span data-ttu-id="d9b03-130">Gebruik **CloudConfigurationManager (CCM)** om te controleren van meerdere externe bronnen voor de verbindingsreeks:</span><span class="sxs-lookup"><span data-stu-id="d9b03-130">Use **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="d9b03-131">Standaard wordt geleverd met ondersteuning voor een externe bron: omgevingsvariabelen.</span><span class="sxs-lookup"><span data-stu-id="d9b03-131">By default, it comes with support for one external source—environmental variables.</span></span>
  * <span data-ttu-id="d9b03-132">U kunt nieuwe bronnen toevoegen door het uitbreiden van de **ConnectionStringSource** klasse.</span><span class="sxs-lookup"><span data-stu-id="d9b03-132">You can add new sources by extending the **ConnectionStringSource** class.</span></span>

<span data-ttu-id="d9b03-133">Voor de voorbeelden die hier wordt beschreven, worden de verbindingsreeks rechtstreeks doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="d9b03-133">For the examples outlined here, the connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$queueRestProxy = ServicesBuilder::getInstance()->createQueueService($connectionString);
```

## <a name="create-a-queue"></a><span data-ttu-id="d9b03-134">Een wachtrij maken</span><span class="sxs-lookup"><span data-stu-id="d9b03-134">Create a queue</span></span>
<span data-ttu-id="d9b03-135">Een **QueueRestProxy** object kunt u een wachtrij maken met behulp van de **createQueue** methode.</span><span class="sxs-lookup"><span data-stu-id="d9b03-135">A **QueueRestProxy** object lets you create a queue by using the **createQueue** method.</span></span> <span data-ttu-id="d9b03-136">Wanneer u een wachtrij maakt, kunt u opties in de wachtrij instellen, maar dit is dus niet vereist.</span><span class="sxs-lookup"><span data-stu-id="d9b03-136">When creating a queue, you can set options on the queue, but doing so is not required.</span></span> <span data-ttu-id="d9b03-137">(Het volgende voorbeeld toont hoe metagegevens instelt op een wachtrij.)</span><span class="sxs-lookup"><span data-stu-id="d9b03-137">(The example below shows how to set metadata on a queue.)</span></span>

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
> <span data-ttu-id="d9b03-138">Niet verstandig hoofdlettergevoeligheid voor metagegevens sleutels.</span><span class="sxs-lookup"><span data-stu-id="d9b03-138">You should not rely on case sensitivity for metadata keys.</span></span> <span data-ttu-id="d9b03-139">Alle sleutels worden gelezen uit de service in kleine letters.</span><span class="sxs-lookup"><span data-stu-id="d9b03-139">All keys are read from the service in lowercase.</span></span>
> 
> 

## <a name="add-a-message-to-a-queue"></a><span data-ttu-id="d9b03-140">Een bericht toevoegen aan een wachtrij</span><span class="sxs-lookup"><span data-stu-id="d9b03-140">Add a message to a queue</span></span>
<span data-ttu-id="d9b03-141">U kunt een bericht toevoegen aan een wachtrij met **QueueRestProxy -> createMessage**.</span><span class="sxs-lookup"><span data-stu-id="d9b03-141">To add a message to a queue, use **QueueRestProxy->createMessage**.</span></span> <span data-ttu-id="d9b03-142">De methode heeft de naam van de wachtrij de berichttekst en Berichtopties (die zijn optioneel).</span><span class="sxs-lookup"><span data-stu-id="d9b03-142">The method takes the queue name, the message text, and message options (which are optional).</span></span>

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

## <a name="peek-at-the-next-message"></a><span data-ttu-id="d9b03-143">Bekijken van het volgende bericht</span><span class="sxs-lookup"><span data-stu-id="d9b03-143">Peek at the next message</span></span>
<span data-ttu-id="d9b03-144">U kunt bekijken van een bericht (of berichten) vooraan in een wachtrij zonder het te verwijderen uit de wachtrij door aan te roepen **QueueRestProxy -> peekMessages**.</span><span class="sxs-lookup"><span data-stu-id="d9b03-144">You can peek at a message (or messages) at the front of a queue without removing it from the queue by calling **QueueRestProxy->peekMessages**.</span></span> <span data-ttu-id="d9b03-145">Standaard de **peekMessage** methode retourneert één bericht, maar u kunt deze waarde wijzigen met behulp van de **PeekMessagesOptions -> setNumberOfMessages** methode.</span><span class="sxs-lookup"><span data-stu-id="d9b03-145">By default, the **peekMessage** method returns a single message, but you can change that value by using the **PeekMessagesOptions->setNumberOfMessages** method.</span></span>

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

## <a name="de-queue-the-next-message"></a><span data-ttu-id="d9b03-146">Het volgende bericht uit de wachtrij verwijderen</span><span class="sxs-lookup"><span data-stu-id="d9b03-146">De-queue the next message</span></span>
<span data-ttu-id="d9b03-147">Uw code wordt een bericht uit een wachtrij in twee stappen.</span><span class="sxs-lookup"><span data-stu-id="d9b03-147">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="d9b03-148">Eerst u aanroepen **QueueRestProxy -> listMessages**, waardoor het bericht onzichtbaar voor andere code die wordt gelezen uit de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="d9b03-148">First, you call **QueueRestProxy->listMessages**, which makes the message invisible to any other code that's reading from the queue.</span></span> <span data-ttu-id="d9b03-149">Standaard wordt dit bericht onzichtbaar blijven gedurende 30 seconden.</span><span class="sxs-lookup"><span data-stu-id="d9b03-149">By default, this message will stay invisible for 30 seconds.</span></span> <span data-ttu-id="d9b03-150">(Als het bericht is niet verwijderd in deze periode, deze wordt zichtbaar in de wachtrij opnieuw.) Voor het voltooien van het bericht uit de wachtrij te verwijderen, moet u aanroepen **QueueRestProxy -> deleteMessage**.</span><span class="sxs-lookup"><span data-stu-id="d9b03-150">(If the message is not deleted in this time period, it will become visible on the queue again.) To finish removing the message from the queue, you must call **QueueRestProxy->deleteMessage**.</span></span> <span data-ttu-id="d9b03-151">Dit proces in twee stappen van het verwijderen van een bericht zorgt ervoor dat wanneer uw code niet kan een bericht vanwege problemen met hardware of software te verwerken, een ander exemplaar van uw code kunt het bericht verschijnt en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="d9b03-151">This two-step process of removing a message assures that when your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="d9b03-152">Uw code haalt **deleteMessage** direct nadat het bericht is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="d9b03-152">Your code calls **deleteMessage** right after the message has been processed.</span></span>

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

## <a name="change-the-contents-of-a-queued-message"></a><span data-ttu-id="d9b03-153">De inhoud van een bericht in de wachtrij wijzigen</span><span class="sxs-lookup"><span data-stu-id="d9b03-153">Change the contents of a queued message</span></span>
<span data-ttu-id="d9b03-154">U kunt de inhoud van een bericht in-place in de wachtrij wijzigen door het aanroepen van **QueueRestProxy -> updateMessage**.</span><span class="sxs-lookup"><span data-stu-id="d9b03-154">You can change the contents of a message in-place in the queue by calling **QueueRestProxy->updateMessage**.</span></span> <span data-ttu-id="d9b03-155">Als het bericht een werktaak vertegenwoordigt, kunt u deze functie gebruiken om de status van de werktaak bij te werken.</span><span class="sxs-lookup"><span data-stu-id="d9b03-155">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="d9b03-156">De volgende code bericht uit de wachtrij bijgewerkt met nieuwe inhoud en stelt time-out voor de zichtbaarheid 60 seconden verlengd.</span><span class="sxs-lookup"><span data-stu-id="d9b03-156">The following code updates the queue message with new contents, and it sets the visibility timeout to extend another 60 seconds.</span></span> <span data-ttu-id="d9b03-157">Hiermee slaat u de status van de werkitems die is gekoppeld aan het bericht en geeft de client een extra minuut om te blijven werken voor het bericht.</span><span class="sxs-lookup"><span data-stu-id="d9b03-157">This saves the state of work that's associated with the message, and it gives the client another minute to continue working on the message.</span></span> <span data-ttu-id="d9b03-158">U kunt deze techniek gebruiken om uit meerdere stappen bestaande werkstromen in berichten in de wachtrij te volgen zonder dat u helemaal opnieuw hoeft te beginnen als een verwerkingsstap vanwege een hardware- of softwarefout is mislukt.</span><span class="sxs-lookup"><span data-stu-id="d9b03-158">You could use this technique to track multi-step workflows on queue messages, without having to start over from the beginning if a processing step fails due to hardware or software failure.</span></span> <span data-ttu-id="d9b03-159">Doorgaans houdt u ook het aantal nieuwe pogingen bij en als het bericht meer dan *n* keer opnieuw is geprobeerd, verwijdert u het.</span><span class="sxs-lookup"><span data-stu-id="d9b03-159">Typically, you would keep a retry count as well, and if the message is retried more than *n* times, you would delete it.</span></span> <span data-ttu-id="d9b03-160">Dit biedt bescherming tegen berichten die een toepassingsfout activeren telkens wanneer ze worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="d9b03-160">This protects against a message that triggers an application error each time it is processed.</span></span>

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

## <a name="additional-options-for-de-queuing-messages"></a><span data-ttu-id="d9b03-161">Aanvullende opties voor berichten in de wachtrij plaatsen</span><span class="sxs-lookup"><span data-stu-id="d9b03-161">Additional options for de-queuing messages</span></span>
<span data-ttu-id="d9b03-162">Er zijn twee manieren dat u ophalen van berichten uit een wachtrij kunt aanpassen.</span><span class="sxs-lookup"><span data-stu-id="d9b03-162">There are two ways that you can customize message retrieval from a queue.</span></span> <span data-ttu-id="d9b03-163">Ten eerste kunt u berichten batchgewijs (maximaal 32) ophalen.</span><span class="sxs-lookup"><span data-stu-id="d9b03-163">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="d9b03-164">Ten tweede kunt u instellen een time-out langer of korter zichtbaarheid zodat uw code meer of minder tijd voor het volledig verwerken van elk bericht.</span><span class="sxs-lookup"><span data-stu-id="d9b03-164">Second, you can set a longer or shorter visibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="d9b03-165">Het volgende codevoorbeeld wordt de **getMessages** methode 16 berichten in één aanroep ophalen.</span><span class="sxs-lookup"><span data-stu-id="d9b03-165">The following code example uses the **getMessages** method to get 16 messages in one call.</span></span> <span data-ttu-id="d9b03-166">Vervolgens wordt elk bericht met behulp van verwerkt een **voor** lus.</span><span class="sxs-lookup"><span data-stu-id="d9b03-166">Then it processes each message by using a **for** loop.</span></span> <span data-ttu-id="d9b03-167">De time-out voor onzichtbaarheid wordt ingesteld op vijf minuten voor elk bericht.</span><span class="sxs-lookup"><span data-stu-id="d9b03-167">It also sets the invisibility timeout to five minutes for each message.</span></span>

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

## <a name="get-queue-length"></a><span data-ttu-id="d9b03-168">Wachtrijlengte ophalen</span><span class="sxs-lookup"><span data-stu-id="d9b03-168">Get queue length</span></span>
<span data-ttu-id="d9b03-169">U kunt een schatting ophalen van het aantal berichten in de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="d9b03-169">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="d9b03-170">De **QueueRestProxy -> getQueueMetadata** methode vraagt de queue-service om terug te keren metagegevens over de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="d9b03-170">The **QueueRestProxy->getQueueMetadata** method asks the queue service to return metadata about the queue.</span></span> <span data-ttu-id="d9b03-171">Het aanroepen van de **getApproximateMessageCount** methode voor het geretourneerde object biedt een aantal van het aantal berichten in een wachtrij zijn.</span><span class="sxs-lookup"><span data-stu-id="d9b03-171">Calling the **getApproximateMessageCount** method on the returned object provides a count of how many messages are in a queue.</span></span> <span data-ttu-id="d9b03-172">Het aantal is alleen een benadering omdat berichten kunnen worden toegevoegd of verwijderd nadat de queue-service op uw aanvraag reageert.</span><span class="sxs-lookup"><span data-stu-id="d9b03-172">The count is only approximate because messages can be added or removed after the queue service responds to your request.</span></span>

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

## <a name="delete-a-queue"></a><span data-ttu-id="d9b03-173">Een wachtrij verwijderen</span><span class="sxs-lookup"><span data-stu-id="d9b03-173">Delete a queue</span></span>
<span data-ttu-id="d9b03-174">Aanroepen voor het verwijderen van een wachtrij en de berichten in de **QueueRestProxy -> deleteQueue** methode.</span><span class="sxs-lookup"><span data-stu-id="d9b03-174">To delete a queue and all the messages in it, call the **QueueRestProxy->deleteQueue** method.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="d9b03-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d9b03-175">Next steps</span></span>
<span data-ttu-id="d9b03-176">Nu dat u de basisprincipes van Azure Queue storage hebt geleerd, volgt u deze koppelingen voor meer informatie over complexere opslagtaken:</span><span class="sxs-lookup"><span data-stu-id="d9b03-176">Now that you've learned the basics of Azure Queue storage, follow these links to learn about more complex storage tasks:</span></span>

* <span data-ttu-id="d9b03-177">Ga naar de [Azure Storage Team blog](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="d9b03-177">Visit the [Azure Storage Team blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>

<span data-ttu-id="d9b03-178">Zie voor meer informatie, ook de [PHP-ontwikkelaarscentrum](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="d9b03-178">For more information, see also the [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[require_once]: http://www.php.net/manual/en/function.require-once.php
[Azure Portal]: https://portal.azure.com

