---
title: Hoe Queue storage gebruiken met Ruby | Microsoft Docs
description: Informatie over het gebruik van de Azure Queue-service maken en verwijderen van wachtrijen, en invoegen, ophalen en verwijderen van berichten. De voorbeelden in Ruby geschreven.
services: storage
documentationcenter: ruby
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 59c2d81b-db9c-46ee-ade2-2f0caae6b1e6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: b978b65bb3b717362697a41510c5b2b4d057cf1f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-queue-storage-from-ruby"></a><span data-ttu-id="03a05-104">Queue Storage gebruiken met Ruby</span><span class="sxs-lookup"><span data-stu-id="03a05-104">How to use Queue storage from Ruby</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="03a05-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="03a05-105">Overview</span></span>
<span data-ttu-id="03a05-106">Deze handleiding wordt beschreven hoe u veelvoorkomende scenario's met de Microsoft Azure Queue Storage-service uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="03a05-106">This guide shows you how to perform common scenarios using the Microsoft Azure Queue Storage service.</span></span> <span data-ttu-id="03a05-107">De voorbeelden zijn geschreven met de Azure-API voor Ruby.</span><span class="sxs-lookup"><span data-stu-id="03a05-107">The samples are written using the Ruby Azure API.</span></span>
<span data-ttu-id="03a05-108">De scenario's worden behandeld: **invoegen**, **inspecteren**, **ophalen**, en **verwijderen** wachtrij berichten, evenals **maken en verwijderen van wachtrijen**.</span><span class="sxs-lookup"><span data-stu-id="03a05-108">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="03a05-109">Een Ruby-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="03a05-109">Create a Ruby Application</span></span>
<span data-ttu-id="03a05-110">Maak een Ruby toepassing.</span><span class="sxs-lookup"><span data-stu-id="03a05-110">Create a Ruby application.</span></span> <span data-ttu-id="03a05-111">Zie voor instructies [Ruby op Rails webtoepassing op een virtuele machine van Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="03a05-111">For instructions, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="03a05-112">Uw toepassing configureren voor toegang tot opslag</span><span class="sxs-lookup"><span data-stu-id="03a05-112">Configure Your Application to Access Storage</span></span>
<span data-ttu-id="03a05-113">Voor het gebruik van Azure-opslag die u wilt downloaden en gebruiken van het Ruby azure pakket bevat een set met gemak bibliotheken die met de storage REST-services communiceren.</span><span class="sxs-lookup"><span data-stu-id="03a05-113">To use Azure storage, you need to download and use the Ruby azure package, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="03a05-114">RubyGems gebruiken om het pakket te verkrijgen</span><span class="sxs-lookup"><span data-stu-id="03a05-114">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="03a05-115">Een opdrachtregelinterface gebruiken zoals **PowerShell** (Windows), **Terminal** (Mac) of **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="03a05-115">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="03a05-116">Typ 'azure gem installeren' in het opdrachtvenster voor het installeren van de gem en afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="03a05-116">Type "gem install azure" in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="03a05-117">Het pakket importeren</span><span class="sxs-lookup"><span data-stu-id="03a05-117">Import the package</span></span>
<span data-ttu-id="03a05-118">Uw favoriete teksteditor gebruiken, Voeg het volgende toe aan het begin van de Ruby bestand waarop u wilt opslag gebruiken:</span><span class="sxs-lookup"><span data-stu-id="03a05-118">Use your favorite text editor, add the following to the top of the Ruby file where you intend to use storage:</span></span>

```ruby
require "azure"
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="03a05-119">Een Azure-opslag-verbinding instellen</span><span class="sxs-lookup"><span data-stu-id="03a05-119">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="03a05-120">De azure-module leest de omgevingsvariabelen **AZURE\_opslag\_ACCOUNT** en **AZURE\_opslag\_ACCESS_KEY** voor meer informatie verbinding maken met uw Azure storage-account vereist.</span><span class="sxs-lookup"><span data-stu-id="03a05-120">The azure module will read the environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="03a05-121">Als deze omgevingsvariabelen zijn niet ingesteld, moet u de accountgegevens voordat u **Azure::QueueService** met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="03a05-121">If these environment variables are not set, you must specify the account information before using **Azure::QueueService** with the following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your Azure storage access key>"
```

<span data-ttu-id="03a05-122">Als u deze waarden van een klassiek of Resource Manager-opslagaccount in de Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="03a05-122">To obtain these values from a classic or Resource Manager storage account in the Azure portal:</span></span>

1. <span data-ttu-id="03a05-123">Meld u aan bij [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="03a05-123">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="03a05-124">Ga naar het opslagaccount dat u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="03a05-124">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="03a05-125">Klik op de blade instellingen aan de rechterkant **toegangstoetsen**.</span><span class="sxs-lookup"><span data-stu-id="03a05-125">In the Settings blade on the right, click **Access Keys**.</span></span>
4. <span data-ttu-id="03a05-126">In de blade van de toegang tot sleutels die wordt weergegeven, ziet u de toegangssleutel 1 en toegangssleutel 2.</span><span class="sxs-lookup"><span data-stu-id="03a05-126">In the Access keys blade that appears, you'll see the access key 1 and access key 2.</span></span> <span data-ttu-id="03a05-127">U kunt een van beide gebruiken.</span><span class="sxs-lookup"><span data-stu-id="03a05-127">You can use either of these.</span></span> 
5. <span data-ttu-id="03a05-128">Klik op het pictogram kopiëren om de sleutel naar het Klembord kopiëren.</span><span class="sxs-lookup"><span data-stu-id="03a05-128">Click the copy icon to copy the key to the clipboard.</span></span> 

<span data-ttu-id="03a05-129">Als u deze waarden van een klassieke opslagaccount in de klassieke Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="03a05-129">To obtain these values from a classic storage account in the classic Azure portal:</span></span>

1. <span data-ttu-id="03a05-130">Meld u aan bij de [klassieke Azure portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="03a05-130">Log in to the [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="03a05-131">Ga naar het opslagaccount dat u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="03a05-131">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="03a05-132">Klik op **TOEGANGSSLEUTELS beheren** onderaan in het navigatiedeelvenster.</span><span class="sxs-lookup"><span data-stu-id="03a05-132">Click **MANAGE ACCESS KEYS** at the bottom of the navigation pane.</span></span>
4. <span data-ttu-id="03a05-133">In het pop-updialoogvenster ziet u de naam van het opslagaccount, de primaire toegangssleutel en de secundaire toegangssleutel.</span><span class="sxs-lookup"><span data-stu-id="03a05-133">In the pop up dialog, you'll see the storage account name, primary access key and secondary access key.</span></span> <span data-ttu-id="03a05-134">Voor toegangssleutel, kunt u een primaire of secundaire een.</span><span class="sxs-lookup"><span data-stu-id="03a05-134">For access key, you can use either the primary one or the secondary one.</span></span> 
5. <span data-ttu-id="03a05-135">Klik op het pictogram kopiëren om de sleutel naar het Klembord kopiëren.</span><span class="sxs-lookup"><span data-stu-id="03a05-135">Click the copy icon to copy the key to the clipboard.</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="03a05-136">Procedure: Een wachtrij maken</span><span class="sxs-lookup"><span data-stu-id="03a05-136">How To: Create a Queue</span></span>
<span data-ttu-id="03a05-137">De volgende code maakt een **Azure::QueueService** object, waarmee u werkt met wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="03a05-137">The following code creates a **Azure::QueueService** object, which enables you to work with queues.</span></span>

```ruby
azure_queue_service = Azure::QueueService.new
```

<span data-ttu-id="03a05-138">Gebruik de **create_queue()** methode voor het maken van een wachtrij met de opgegeven naam.</span><span class="sxs-lookup"><span data-stu-id="03a05-138">Use the **create_queue()** method to create a queue with the specified name.</span></span>

```ruby
begin
  azure_queue_service.create_queue("test-queue")
rescue
  puts $!
end
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="03a05-139">Procedure: Een bericht in een wachtrij invoegen</span><span class="sxs-lookup"><span data-stu-id="03a05-139">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="03a05-140">Voor het invoegen van een bericht in een wachtrij, gebruikt u de **create_message()** methode voor het maken van een nieuw bericht en voeg deze toe aan de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="03a05-140">To insert a message into a queue, use the **create_message()** method to create a new message and add it to the queue.</span></span>

```ruby
azure_queue_service.create_message("test-queue", "test message")
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="03a05-141">Procedure: Bekijken van het volgende bericht</span><span class="sxs-lookup"><span data-stu-id="03a05-141">How To: Peek at the Next Message</span></span>
<span data-ttu-id="03a05-142">U kunt het bericht vooraan in een wachtrij bekijken zonder het te verwijderen uit de wachtrij door het aanroepen van de **peek\_messages()** methode.</span><span class="sxs-lookup"><span data-stu-id="03a05-142">You can peek at the message in the front of a queue without removing it from the queue by calling the **peek\_messages()** method.</span></span> <span data-ttu-id="03a05-143">Standaard **peek\_messages()** peeks op één bericht.</span><span class="sxs-lookup"><span data-stu-id="03a05-143">By default, **peek\_messages()** peeks at a single message.</span></span> <span data-ttu-id="03a05-144">U kunt ook opgeven hoeveel berichten die u wilt bekijken.</span><span class="sxs-lookup"><span data-stu-id="03a05-144">You can also specify how many messages you want to peek.</span></span>

```ruby
result = azure_queue_service.peek_messages("test-queue",
  {:number_of_messages => 10})
```

## <a name="how-to-dequeue-the-next-message"></a><span data-ttu-id="03a05-145">Procedure: Het volgende bericht uit de wachtrij halen</span><span class="sxs-lookup"><span data-stu-id="03a05-145">How To: Dequeue the Next Message</span></span>
<span data-ttu-id="03a05-146">U kunt een bericht verwijderen uit een wachtrij in twee stappen.</span><span class="sxs-lookup"><span data-stu-id="03a05-146">You can remove a message from a queue in two steps.</span></span>

1. <span data-ttu-id="03a05-147">Als u aanroept **lijst\_messages()**, krijgt u het volgende bericht in een wachtrij standaard.</span><span class="sxs-lookup"><span data-stu-id="03a05-147">When you call **list\_messages()**, you get the next message in a queue by default.</span></span> <span data-ttu-id="03a05-148">U kunt ook opgeven hoeveel berichten die u wilt ophalen.</span><span class="sxs-lookup"><span data-stu-id="03a05-148">You can also specify how many messages you want to get.</span></span> <span data-ttu-id="03a05-149">De berichten die zijn geretourneerd door **lijst\_messages()** wordt onzichtbaar voor andere codes die berichten lezen uit deze wachtrij.</span><span class="sxs-lookup"><span data-stu-id="03a05-149">The messages returned from **list\_messages()** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="03a05-150">U doorgeven de zichtbaarheid time-out in seconden als parameter.</span><span class="sxs-lookup"><span data-stu-id="03a05-150">You pass in the visibility timeout in seconds as a parameter.</span></span>
2. <span data-ttu-id="03a05-151">Voor het voltooien van het bericht uit de wachtrij te verwijderen, moet u ook aanroepen **delete_message()**.</span><span class="sxs-lookup"><span data-stu-id="03a05-151">To finish removing the message from the queue, you must also call **delete_message()**.</span></span>

<span data-ttu-id="03a05-152">Dit proces in twee stappen van het verwijderen van een bericht zorgt ervoor dat wanneer uw code niet kan een bericht vanwege problemen met hardware of software te verwerken, een ander exemplaar van uw code kunt het bericht verschijnt en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="03a05-152">This two-step process of removing a message assures that when your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="03a05-153">Uw code haalt **verwijderen\_message()** direct nadat het bericht is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="03a05-153">Your code calls **delete\_message()** right after the message has been processed.</span></span>

```ruby
messages = azure_queue_service.list_messages("test-queue", 30)
azure_queue_service.delete_message("test-queue", 
  messages[0].id, messages[0].pop_receipt)
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="03a05-154">Procedure: De inhoud van een bericht in de wachtrij wijzigen</span><span class="sxs-lookup"><span data-stu-id="03a05-154">How To: Change the Contents of a Queued Message</span></span>
<span data-ttu-id="03a05-155">U kunt de inhoud van een bericht in de wachtrij wijzigen.</span><span class="sxs-lookup"><span data-stu-id="03a05-155">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="03a05-156">De code hieronder maakt gebruik van de **update_message()** methode voor het bijwerken van een bericht.</span><span class="sxs-lookup"><span data-stu-id="03a05-156">The code below uses the **update_message()** method to update a message.</span></span> <span data-ttu-id="03a05-157">De methode retourneert een tuple waarin de pop ontvangst van het bericht uit de wachtrij en een UTC date tijd-waarde die aangeeft wanneer het bericht zichtbaar in de wachtrij zijn.</span><span class="sxs-lookup"><span data-stu-id="03a05-157">The method will return a tuple which contains the pop receipt of the queue message and a UTC date time value that represents when the message will be visible on the queue.</span></span>

```ruby
message = azure_queue_service.list_messages("test-queue", 30)
pop_receipt, time_next_visible = azure_queue_service.update_message(
  "test-queue", message.id, message.pop_receipt, "updated test message", 
  30)
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="03a05-158">Procedure: Aanvullende opties voor waarbij berichten</span><span class="sxs-lookup"><span data-stu-id="03a05-158">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="03a05-159">Er zijn twee manieren waarop u het ophalen van berichten uit een wachtrij kunt aanpassen.</span><span class="sxs-lookup"><span data-stu-id="03a05-159">There are two ways you can customize message retrieval from a queue.</span></span>

1. <span data-ttu-id="03a05-160">U kunt een batch van bericht ophalen.</span><span class="sxs-lookup"><span data-stu-id="03a05-160">You can get a batch of message.</span></span>
2. <span data-ttu-id="03a05-161">U kunt een time-out langer of korter onzichtbaarheid instellen zodat uw code meer of minder tijd voor het volledig verwerken van elk bericht.</span><span class="sxs-lookup"><span data-stu-id="03a05-161">You can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span>

<span data-ttu-id="03a05-162">Het volgende codevoorbeeld wordt de **lijst\_messages()** methode 15 berichten in één aanroep ophalen.</span><span class="sxs-lookup"><span data-stu-id="03a05-162">The following code example uses the **list\_messages()** method to get 15 messages in one call.</span></span> <span data-ttu-id="03a05-163">Vervolgens wordt afgedrukt en elk bericht wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="03a05-163">Then it prints and deletes each message.</span></span> <span data-ttu-id="03a05-164">De time-out voor onzichtbaarheid wordt ingesteld op vijf minuten voor elk bericht.</span><span class="sxs-lookup"><span data-stu-id="03a05-164">It also sets the invisibility timeout to five minutes for each message.</span></span>

```ruby
azure_queue_service.list_messages("test-queue", 300
  {:number_of_messages => 15}).each do |m|
  puts m.message_text
  azure_queue_service.delete_message("test-queue", m.id, m.pop_receipt)
end
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="03a05-165">Procedure: De lengte van de wachtrij ophalen</span><span class="sxs-lookup"><span data-stu-id="03a05-165">How To: Get the Queue Length</span></span>
<span data-ttu-id="03a05-166">U kunt een schatting van het aantal berichten in de wachtrij ophalen.</span><span class="sxs-lookup"><span data-stu-id="03a05-166">You can get an estimation of the number of messages in the queue.</span></span> <span data-ttu-id="03a05-167">De **ophalen\_wachtrij\_metadata()** methode vraagt de queue-service om het aantal berichten bij benadering en metagegevens over de wachtrij te retourneren.</span><span class="sxs-lookup"><span data-stu-id="03a05-167">The **get\_queue\_metadata()** method asks the queue service to return the approximate message count and metadata about the queue.</span></span>

```ruby
message_count, metadata = azure_queue_service.get_queue_metadata(
  "test-queue")
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="03a05-168">Procedure: Een wachtrij verwijderen</span><span class="sxs-lookup"><span data-stu-id="03a05-168">How To: Delete a Queue</span></span>
<span data-ttu-id="03a05-169">Aanroepen voor het verwijderen van een wachtrij en alle berichten hierin de **verwijderen\_queue()** methode voor het object in de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="03a05-169">To delete a queue and all the messages contained in it, call the **delete\_queue()** method on the queue object.</span></span>

```ruby
azure_queue_service.delete_queue("test-queue")
```

## <a name="next-steps"></a><span data-ttu-id="03a05-170">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="03a05-170">Next Steps</span></span>
<span data-ttu-id="03a05-171">Nu dat u de basisprincipes van queue storage hebt geleerd, volgt u deze koppelingen voor meer informatie over complexere opslagtaken.</span><span class="sxs-lookup"><span data-stu-id="03a05-171">Now that you've learned the basics of queue storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="03a05-172">Ga naar de [Blog Azure Storage-Team](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="03a05-172">Visit the [Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="03a05-173">Ga naar de [Azure SDK voor Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) opslagplaats op GitHub</span><span class="sxs-lookup"><span data-stu-id="03a05-173">Visit the [Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

<span data-ttu-id="03a05-174">Voor een vergelijking tussen de Azure Queue-Service die wordt besproken in dit artikel en de Azure Service Bus-wachtrijen beschreven in de [het gebruik van Service Bus-wachtrijen](/develop/ruby/how-to-guides/service-bus-queues/) artikel, Zie [Azure wachtrijen en Service Bus-wachtrijen - vergeleken en Tegenstelling tot](../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span><span class="sxs-lookup"><span data-stu-id="03a05-174">For a comparison between the Azure Queue Service discussed in this article and Azure Service Bus Queues discussed in the [How to use Service Bus Queues](/develop/ruby/how-to-guides/service-bus-queues/) article, see [Azure Queues and Service Bus Queues - Compared and Contrasted](../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span></span>