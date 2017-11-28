---
title: aaaHow toouse Queue storage met Ruby | Microsoft Docs
description: Ontdek hoe toocreate toouse hello Azure Queue-service en delete-wachtrijen en invoegen, ophalen en verwijderen van berichten. De voorbeelden in Ruby geschreven.
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
ms.openlocfilehash: 726c7d2f08b2d5938ee5f9dcdc2735e447388856
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-ruby"></a><span data-ttu-id="49aef-104">Hoe toouse Queue storage met Ruby</span><span class="sxs-lookup"><span data-stu-id="49aef-104">How toouse Queue storage from Ruby</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="49aef-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="49aef-105">Overview</span></span>
<span data-ttu-id="49aef-106">Deze handleiding wordt getoond hoe tooperform algemene scenario's met behulp van Microsoft Azure Queue Storage-service Hallo.</span><span class="sxs-lookup"><span data-stu-id="49aef-106">This guide shows you how tooperform common scenarios using hello Microsoft Azure Queue Storage service.</span></span> <span data-ttu-id="49aef-107">Hallo-voorbeelden zijn geschreven met behulp van Hallo Ruby Azure-API.</span><span class="sxs-lookup"><span data-stu-id="49aef-107">hello samples are written using hello Ruby Azure API.</span></span>
<span data-ttu-id="49aef-108">Hallo scenario's worden behandeld: **invoegen**, **inspecteren**, **ophalen**, en **verwijderen** wachtrij berichten, evenals  **maken en verwijderen van wachtrijen**.</span><span class="sxs-lookup"><span data-stu-id="49aef-108">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="49aef-109">Een Ruby-toepassing maken</span><span class="sxs-lookup"><span data-stu-id="49aef-109">Create a Ruby Application</span></span>
<span data-ttu-id="49aef-110">Maak een Ruby toepassing.</span><span class="sxs-lookup"><span data-stu-id="49aef-110">Create a Ruby application.</span></span> <span data-ttu-id="49aef-111">Zie voor instructies [Ruby op Rails webtoepassing op een virtuele machine van Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="49aef-111">For instructions, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="49aef-112">Uw toepassing tooAccess opslag configureren</span><span class="sxs-lookup"><span data-stu-id="49aef-112">Configure Your Application tooAccess Storage</span></span>
<span data-ttu-id="49aef-113">toouse Azure-opslag, moet u toodownload en gebruik Hallo Ruby azure, dit pakket bevat een set met gemak bibliotheken die met de Hallo storage REST-services communiceren.</span><span class="sxs-lookup"><span data-stu-id="49aef-113">toouse Azure storage, you need toodownload and use hello Ruby azure package, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="49aef-114">RubyGems tooobtain Hallo pakket gebruiken</span><span class="sxs-lookup"><span data-stu-id="49aef-114">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="49aef-115">Een opdrachtregelinterface gebruiken zoals **PowerShell** (Windows), **Terminal** (Mac) of **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="49aef-115">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="49aef-116">Typ 'gem installeren azure' hello opdracht venster tooinstall Hallo gem en afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="49aef-116">Type "gem install azure" in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="49aef-117">Hallo-pakket importeren</span><span class="sxs-lookup"><span data-stu-id="49aef-117">Import hello package</span></span>
<span data-ttu-id="49aef-118">Uw favoriete teksteditor gebruiken, voegt Hallo toohello bovenaan Hallo Ruby bestand waarin u van plan toouse opslag bent te volgen:</span><span class="sxs-lookup"><span data-stu-id="49aef-118">Use your favorite text editor, add hello following toohello top of hello Ruby file where you intend toouse storage:</span></span>

```ruby
require "azure"
```

## <a name="setup-an-azure-storage-connection"></a><span data-ttu-id="49aef-119">Een Azure-opslag-verbinding instellen</span><span class="sxs-lookup"><span data-stu-id="49aef-119">Setup an Azure Storage Connection</span></span>
<span data-ttu-id="49aef-120">Hello azure module lezen Hallo omgevingsvariabelen **AZURE\_opslag\_ACCOUNT** en **AZURE\_opslag\_ACCESS_KEY** voor informatie vereist tooconnect tooyour Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="49aef-120">hello azure module will read hello environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="49aef-121">Als deze omgevingsvariabelen zijn niet ingesteld, moet u de accountgegevens Hallo voordat u **Azure::QueueService** Hello code te volgen:</span><span class="sxs-lookup"><span data-stu-id="49aef-121">If these environment variables are not set, you must specify hello account information before using **Azure::QueueService** with hello following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your Azure storage access key>"
```

<span data-ttu-id="49aef-122">tooobtain deze waarden van een klassiek of Resource Manager-storage-account in hello Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="49aef-122">tooobtain these values from a classic or Resource Manager storage account in hello Azure portal:</span></span>

1. <span data-ttu-id="49aef-123">Meld u bij toohello [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="49aef-123">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="49aef-124">Navigeer toohello gewenste toouse storage-account.</span><span class="sxs-lookup"><span data-stu-id="49aef-124">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="49aef-125">Klik op Hallo instellingenblade op Hallo rechts **toegangstoetsen**.</span><span class="sxs-lookup"><span data-stu-id="49aef-125">In hello Settings blade on hello right, click **Access Keys**.</span></span>
4. <span data-ttu-id="49aef-126">Hallo toegang sleutels blade die wordt weergegeven, ziet u Hallo toegangssleutel 1 en toegangssleutel 2.</span><span class="sxs-lookup"><span data-stu-id="49aef-126">In hello Access keys blade that appears, you'll see hello access key 1 and access key 2.</span></span> <span data-ttu-id="49aef-127">U kunt een van beide gebruiken.</span><span class="sxs-lookup"><span data-stu-id="49aef-127">You can use either of these.</span></span> 
5. <span data-ttu-id="49aef-128">Klik op Hallo kopiëren pictogram toocopy Hallo sleutel toohello Klembord.</span><span class="sxs-lookup"><span data-stu-id="49aef-128">Click hello copy icon toocopy hello key toohello clipboard.</span></span> 

<span data-ttu-id="49aef-129">tooobtain deze waarden van een klassieke storage-account in de klassieke Azure portal Hallo:</span><span class="sxs-lookup"><span data-stu-id="49aef-129">tooobtain these values from a classic storage account in hello classic Azure portal:</span></span>

1. <span data-ttu-id="49aef-130">Meld u bij toohello [klassieke Azure portal](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="49aef-130">Log in toohello [classic Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="49aef-131">Navigeer toohello gewenste toouse storage-account.</span><span class="sxs-lookup"><span data-stu-id="49aef-131">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="49aef-132">Klik op **TOEGANGSSLEUTELS beheren** Hallo Hallo navigatiedeelvenster onderaan in.</span><span class="sxs-lookup"><span data-stu-id="49aef-132">Click **MANAGE ACCESS KEYS** at hello bottom of hello navigation pane.</span></span>
4. <span data-ttu-id="49aef-133">In het dialoogvenster pop hello ziet u opslagaccountnaam hello, de primaire toegangssleutel en de secundaire toegangssleutel.</span><span class="sxs-lookup"><span data-stu-id="49aef-133">In hello pop up dialog, you'll see hello storage account name, primary access key and secondary access key.</span></span> <span data-ttu-id="49aef-134">U kunt voor toegangssleutel, Hallo een primaire of secundaire één Hallo gebruiken.</span><span class="sxs-lookup"><span data-stu-id="49aef-134">For access key, you can use either hello primary one or hello secondary one.</span></span> 
5. <span data-ttu-id="49aef-135">Klik op Hallo kopiëren pictogram toocopy Hallo sleutel toohello Klembord.</span><span class="sxs-lookup"><span data-stu-id="49aef-135">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

## <a name="how-to-create-a-queue"></a><span data-ttu-id="49aef-136">Procedure: Een wachtrij maken</span><span class="sxs-lookup"><span data-stu-id="49aef-136">How To: Create a Queue</span></span>
<span data-ttu-id="49aef-137">Hallo volgende code maakt een **Azure::QueueService** object, waarmee u toowork met wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="49aef-137">hello following code creates a **Azure::QueueService** object, which enables you toowork with queues.</span></span>

```ruby
azure_queue_service = Azure::QueueService.new
```

<span data-ttu-id="49aef-138">Gebruik Hallo **create_queue()** methode toocreate een wachtrij met Hallo opgegeven naam.</span><span class="sxs-lookup"><span data-stu-id="49aef-138">Use hello **create_queue()** method toocreate a queue with hello specified name.</span></span>

```ruby
begin
  azure_queue_service.create_queue("test-queue")
rescue
  puts $!
end
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="49aef-139">Procedure: Een bericht in een wachtrij invoegen</span><span class="sxs-lookup"><span data-stu-id="49aef-139">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="49aef-140">een bericht in een wachtrij, gebruik Hallo tooinsert **create_message()** methode toocreate een nieuw bericht en voeg deze toohello wachtrij.</span><span class="sxs-lookup"><span data-stu-id="49aef-140">tooinsert a message into a queue, use hello **create_message()** method toocreate a new message and add it toohello queue.</span></span>

```ruby
azure_queue_service.create_message("test-queue", "test message")
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="49aef-141">Procedure: Inspecteren Hallo het Volgendebericht</span><span class="sxs-lookup"><span data-stu-id="49aef-141">How To: Peek at hello Next Message</span></span>
<span data-ttu-id="49aef-142">U kunt bekijken van Hallo-bericht in Hallo begin van een wachtrij zonder het te verwijderen uit de wachtrij Hallo door aanroepen Hallo **peek\_messages()** methode.</span><span class="sxs-lookup"><span data-stu-id="49aef-142">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peek\_messages()** method.</span></span> <span data-ttu-id="49aef-143">Standaard **peek\_messages()** peeks op één bericht.</span><span class="sxs-lookup"><span data-stu-id="49aef-143">By default, **peek\_messages()** peeks at a single message.</span></span> <span data-ttu-id="49aef-144">U kunt ook opgeven hoeveel berichten u wilt dat toopeek.</span><span class="sxs-lookup"><span data-stu-id="49aef-144">You can also specify how many messages you want toopeek.</span></span>

```ruby
result = azure_queue_service.peek_messages("test-queue",
  {:number_of_messages => 10})
```

## <a name="how-to-dequeue-hello-next-message"></a><span data-ttu-id="49aef-145">Procedure: Hallo het Volgendebericht uit de wachtrij halen</span><span class="sxs-lookup"><span data-stu-id="49aef-145">How To: Dequeue hello Next Message</span></span>
<span data-ttu-id="49aef-146">U kunt een bericht verwijderen uit een wachtrij in twee stappen.</span><span class="sxs-lookup"><span data-stu-id="49aef-146">You can remove a message from a queue in two steps.</span></span>

1. <span data-ttu-id="49aef-147">Als u aanroept **lijst\_messages()**, u het volgende Hallo-bericht in een wachtrij standaard ophalen.</span><span class="sxs-lookup"><span data-stu-id="49aef-147">When you call **list\_messages()**, you get hello next message in a queue by default.</span></span> <span data-ttu-id="49aef-148">U kunt ook opgeven hoeveel berichten u wilt dat tooget.</span><span class="sxs-lookup"><span data-stu-id="49aef-148">You can also specify how many messages you want tooget.</span></span> <span data-ttu-id="49aef-149">Hallo-berichten dat is geretourneerd door **lijst\_messages()** wordt onzichtbaar tooany andere codes die berichten lezen uit deze wachtrij.</span><span class="sxs-lookup"><span data-stu-id="49aef-149">hello messages returned from **list\_messages()** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="49aef-150">U doorgeven Hallo zichtbaarheid time-out in seconden als parameter.</span><span class="sxs-lookup"><span data-stu-id="49aef-150">You pass in hello visibility timeout in seconds as a parameter.</span></span>
2. <span data-ttu-id="49aef-151">toofinish verwijderen Hallo-bericht uit de wachtrij hello, moet u ook aanroepen **delete_message()**.</span><span class="sxs-lookup"><span data-stu-id="49aef-151">toofinish removing hello message from hello queue, you must also call **delete_message()**.</span></span>

<span data-ttu-id="49aef-152">Dit proces in twee stappen van het verwijderen van een bericht zorgt ervoor dat wanneer uw code mislukt tooprocess een bericht vanwege problemen toohardware of software, een ander exemplaar van uw code krijgt Hallo hetzelfde bericht en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="49aef-152">This two-step process of removing a message assures that when your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="49aef-153">Uw code haalt **verwijderen\_message()** direct nadat het Hallo-bericht is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="49aef-153">Your code calls **delete\_message()** right after hello message has been processed.</span></span>

```ruby
messages = azure_queue_service.list_messages("test-queue", 30)
azure_queue_service.delete_message("test-queue", 
  messages[0].id, messages[0].pop_receipt)
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="49aef-154">Procedure: Hallo inhoud van een bericht in de wachtrij wijzigen</span><span class="sxs-lookup"><span data-stu-id="49aef-154">How To: Change hello Contents of a Queued Message</span></span>
<span data-ttu-id="49aef-155">U kunt Hallo inhoud van een bericht in-place in Hallo wachtrij wijzigen.</span><span class="sxs-lookup"><span data-stu-id="49aef-155">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="49aef-156">Hallo-code hieronder maakt gebruik van Hallo **update_message()** methode tooupdate een bericht.</span><span class="sxs-lookup"><span data-stu-id="49aef-156">hello code below uses hello **update_message()** method tooupdate a message.</span></span> <span data-ttu-id="49aef-157">Hallo-methode retourneert een tuple die Hallo pop ontvangst van de wachtrij het Hallo-bericht bevat en een UTC date tijd-waarde die aangeeft wanneer het Hallo-bericht op Hallo wachtrij zichtbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="49aef-157">hello method will return a tuple which contains hello pop receipt of hello queue message and a UTC date time value that represents when hello message will be visible on hello queue.</span></span>

```ruby
message = azure_queue_service.list_messages("test-queue", 30)
pop_receipt, time_next_visible = azure_queue_service.update_message(
  "test-queue", message.id, message.pop_receipt, "updated test message", 
  30)
```

## <a name="how-to-additional-options-for-dequeuing-messages"></a><span data-ttu-id="49aef-158">Procedure: Aanvullende opties voor waarbij berichten</span><span class="sxs-lookup"><span data-stu-id="49aef-158">How To: Additional Options for Dequeuing Messages</span></span>
<span data-ttu-id="49aef-159">Er zijn twee manieren waarop u het ophalen van berichten uit een wachtrij kunt aanpassen.</span><span class="sxs-lookup"><span data-stu-id="49aef-159">There are two ways you can customize message retrieval from a queue.</span></span>

1. <span data-ttu-id="49aef-160">U kunt een batch van bericht ophalen.</span><span class="sxs-lookup"><span data-stu-id="49aef-160">You can get a batch of message.</span></span>
2. <span data-ttu-id="49aef-161">U kunt een time-out langer of korter onzichtbaarheid instellen zodat uw code meer of minder tijd toofully elk bericht niet verwerken.</span><span class="sxs-lookup"><span data-stu-id="49aef-161">You can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span>

<span data-ttu-id="49aef-162">Hallo volgende codevoorbeeld maakt gebruik van Hallo **lijst\_messages()** methode tooget 15 berichten in één aanroep.</span><span class="sxs-lookup"><span data-stu-id="49aef-162">hello following code example uses hello **list\_messages()** method tooget 15 messages in one call.</span></span> <span data-ttu-id="49aef-163">Vervolgens wordt afgedrukt en elk bericht wordt verwijderd.</span><span class="sxs-lookup"><span data-stu-id="49aef-163">Then it prints and deletes each message.</span></span> <span data-ttu-id="49aef-164">Hallo onzichtbaarheid toofive minuten voor de time-out voor elk bericht wordt ook ingesteld.</span><span class="sxs-lookup"><span data-stu-id="49aef-164">It also sets hello invisibility timeout toofive minutes for each message.</span></span>

```ruby
azure_queue_service.list_messages("test-queue", 300
  {:number_of_messages => 15}).each do |m|
  puts m.message_text
  azure_queue_service.delete_message("test-queue", m.id, m.pop_receipt)
end
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="49aef-165">Procedure: Hallo wachtrijlengte ophalen</span><span class="sxs-lookup"><span data-stu-id="49aef-165">How To: Get hello Queue Length</span></span>
<span data-ttu-id="49aef-166">U kunt een schatting van het aantal berichten Hallo ophalen in de wachtrij Hallo.</span><span class="sxs-lookup"><span data-stu-id="49aef-166">You can get an estimation of hello number of messages in hello queue.</span></span> <span data-ttu-id="49aef-167">Hallo **ophalen\_wachtrij\_metadata()** methode vraagt Hallo wachtrij tooreturn Hallo bericht geschatte aantal en metagegevens over Hallo wachtrij.</span><span class="sxs-lookup"><span data-stu-id="49aef-167">hello **get\_queue\_metadata()** method asks hello queue service tooreturn hello approximate message count and metadata about hello queue.</span></span>

```ruby
message_count, metadata = azure_queue_service.get_queue_metadata(
  "test-queue")
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="49aef-168">Procedure: Een wachtrij verwijderen</span><span class="sxs-lookup"><span data-stu-id="49aef-168">How To: Delete a Queue</span></span>
<span data-ttu-id="49aef-169">een wachtrij en alle Hallo-berichten toodelete opgenomen in deze aanroep Hallo **verwijderen\_queue()** methode op Hallo wachtrij-object.</span><span class="sxs-lookup"><span data-stu-id="49aef-169">toodelete a queue and all hello messages contained in it, call hello **delete\_queue()** method on hello queue object.</span></span>

```ruby
azure_queue_service.delete_queue("test-queue")
```

## <a name="next-steps"></a><span data-ttu-id="49aef-170">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="49aef-170">Next Steps</span></span>
<span data-ttu-id="49aef-171">Nu u Hallo basisprincipes van queue storage hebt geleerd, volgt u deze koppelingen toolearn over complexere opslagtaken.</span><span class="sxs-lookup"><span data-stu-id="49aef-171">Now that you've learned hello basics of queue storage, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="49aef-172">Ga naar Hallo [Blog van Azure Storage-Team](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="49aef-172">Visit hello [Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="49aef-173">Ga naar Hallo [Azure SDK voor Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) opslagplaats op GitHub</span><span class="sxs-lookup"><span data-stu-id="49aef-173">Visit hello [Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

<span data-ttu-id="49aef-174">Voor een vergelijking tussen hello Azure Queue-Service die wordt besproken in dit artikel en de Azure Service Bus-wachtrijen in Hallo besproken [hoe toouse Service Bus-wachtrijen](/develop/ruby/how-to-guides/service-bus-queues/) artikel, Zie [Azure wachtrijen en Service Bus-wachtrijen - vergeleken en Tegenstelling tot](../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span><span class="sxs-lookup"><span data-stu-id="49aef-174">For a comparison between hello Azure Queue Service discussed in this article and Azure Service Bus Queues discussed in hello [How toouse Service Bus Queues](/develop/ruby/how-to-guides/service-bus-queues/) article, see [Azure Queues and Service Bus Queues - Compared and Contrasted](../service-bus-messaging/service-bus-azure-and-service-bus-queues-compared-contrasted.md)</span></span>
