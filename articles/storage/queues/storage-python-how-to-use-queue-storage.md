---
title: Hoe Queue storage gebruiken met Python | Microsoft Docs
description: Informatie over het gebruik van de Azure Queue-service met Python maken en verwijderen van wachtrijen, en invoegen, ophalen en verwijderen van berichten.
services: storage
documentationcenter: python
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: cc0d2da2-379a-4b58-a234-8852b4e3d99d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: 963c11acb7939993568a774cd281145a8059b5a6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-queue-storage-from-python"></a><span data-ttu-id="263fe-103">Queue Storage gebruiken met Python</span><span class="sxs-lookup"><span data-stu-id="263fe-103">How to use Queue storage from Python</span></span>
[!INCLUDE [storage-selector-queue-include](../../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="263fe-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="263fe-104">Overview</span></span>
<span data-ttu-id="263fe-105">Deze handleiding wordt beschreven hoe u veelvoorkomende scenario's met behulp van de Azure Queue storage-service uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="263fe-105">This guide shows you how to perform common scenarios using the Azure Queue storage service.</span></span> <span data-ttu-id="263fe-106">De voorbeelden zijn geschreven in Python en gebruik de [Microsoft Azure-opslag-SDK voor Python].</span><span class="sxs-lookup"><span data-stu-id="263fe-106">The samples are written in Python and use the [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="263fe-107">De scenario's worden behandeld: **invoegen**, **inspecteren**, **ophalen**, en **verwijderen** wachtrij berichten, evenals **maken en verwijderen van wachtrijen**.</span><span class="sxs-lookup"><span data-stu-id="263fe-107">The scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span> <span data-ttu-id="263fe-108">Raadpleeg de sectie [Vervolgstappen] voor meer informatie over wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="263fe-108">For more information on queues, refer to the [Next Steps] section.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="how-to-create-a-queue"></a><span data-ttu-id="263fe-109">Procedure: Een wachtrij maken</span><span class="sxs-lookup"><span data-stu-id="263fe-109">How To: Create a Queue</span></span>
<span data-ttu-id="263fe-110">De **QueueService** object kunt u samenwerken met wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="263fe-110">The **QueueService** object lets you work with queues.</span></span> <span data-ttu-id="263fe-111">De volgende code maakt een **QueueService** object.</span><span class="sxs-lookup"><span data-stu-id="263fe-111">The following code creates a **QueueService** object.</span></span> <span data-ttu-id="263fe-112">Voeg de volgende boven aan elk Python-bestand waarin u wilt programmatisch toegang biedt tot Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="263fe-112">Add the following near the top of any Python file in which you wish to programmatically access Azure Storage:</span></span>

```python
from azure.storage.queue import QueueService
```

<span data-ttu-id="263fe-113">De volgende code maakt een **QueueService** object met de naam en het account opslagaccountsleutel.</span><span class="sxs-lookup"><span data-stu-id="263fe-113">The following code creates a **QueueService** object using the storage account name and account key.</span></span> <span data-ttu-id="263fe-114">'Myaccount' en 'mykey' vervangen door uw accountnaam en de sleutel.</span><span class="sxs-lookup"><span data-stu-id="263fe-114">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
queue_service = QueueService(account_name='myaccount', account_key='mykey')

queue_service.create_queue('taskqueue')
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="263fe-115">Procedure: Een bericht in een wachtrij invoegen</span><span class="sxs-lookup"><span data-stu-id="263fe-115">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="263fe-116">Voor het invoegen van een bericht in een wachtrij, gebruikt u de **plaatsen\_bericht** methode voor het maken van een nieuw bericht en voeg deze toe aan de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="263fe-116">To insert a message into a queue, use the **put\_message** method to create a new message and add it to the queue.</span></span>

```python
queue_service.put_message('taskqueue', u'Hello World')
```

## <a name="how-to-peek-at-the-next-message"></a><span data-ttu-id="263fe-117">Procedure: Bekijken van het volgende bericht</span><span class="sxs-lookup"><span data-stu-id="263fe-117">How To: Peek at the Next Message</span></span>
<span data-ttu-id="263fe-118">U kunt het bericht vooraan in een wachtrij bekijken zonder het te verwijderen uit de wachtrij door het aanroepen van de **peek\_berichten** methode.</span><span class="sxs-lookup"><span data-stu-id="263fe-118">You can peek at the message in the front of a queue without removing it from the queue by calling the **peek\_messages** method.</span></span> <span data-ttu-id="263fe-119">Standaard **peek\_berichten** peeks op één bericht.</span><span class="sxs-lookup"><span data-stu-id="263fe-119">By default, **peek\_messages** peeks at a single message.</span></span>

```python
messages = queue_service.peek_messages('taskqueue')
for message in messages:
    print(message.content)
```

## <a name="how-to-dequeue-messages"></a><span data-ttu-id="263fe-120">Procedure: Berichten in wachtrij</span><span class="sxs-lookup"><span data-stu-id="263fe-120">How To: Dequeue Messages</span></span>
<span data-ttu-id="263fe-121">Uw code wordt een bericht uit een wachtrij in twee stappen.</span><span class="sxs-lookup"><span data-stu-id="263fe-121">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="263fe-122">Als u aanroept **ophalen\_berichten**, krijgt u het volgende bericht in een wachtrij standaard.</span><span class="sxs-lookup"><span data-stu-id="263fe-122">When you call **get\_messages**, you get the next message in a queue by default.</span></span> <span data-ttu-id="263fe-123">Een bericht dat wordt geretourneerd door **ophalen\_berichten** wordt onzichtbaar voor andere codes die berichten lezen uit deze wachtrij.</span><span class="sxs-lookup"><span data-stu-id="263fe-123">A message returned from **get\_messages** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="263fe-124">Standaard blijft het bericht onzichtbaar gedurende 30 seconden.</span><span class="sxs-lookup"><span data-stu-id="263fe-124">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="263fe-125">Voor het voltooien van het bericht uit de wachtrij te verwijderen, moet u ook aanroepen **verwijderen\_bericht**.</span><span class="sxs-lookup"><span data-stu-id="263fe-125">To finish removing the message from the queue, you must also call **delete\_message**.</span></span> <span data-ttu-id="263fe-126">Dit proces in twee stappen van het verwijderen van een bericht zorgt ervoor dat wanneer uw code niet kan een bericht vanwege problemen met hardware of software te verwerken, een ander exemplaar van uw code kunt het bericht verschijnt en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="263fe-126">This two-step process of removing a message assures that when your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="263fe-127">Uw code haalt **verwijderen\_bericht** direct nadat het bericht is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="263fe-127">Your code calls **delete\_message** right after the message has been processed.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)
```

<span data-ttu-id="263fe-128">Er zijn twee manieren waarop u het ophalen van berichten uit een wachtrij kunt aanpassen.</span><span class="sxs-lookup"><span data-stu-id="263fe-128">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="263fe-129">Ten eerste kunt u berichten batchgewijs (maximaal 32) ophalen.</span><span class="sxs-lookup"><span data-stu-id="263fe-129">First, you can get a batch of messages (up to 32).</span></span> <span data-ttu-id="263fe-130">Ten tweede kunt u een langere of kortere time-out voor onzichtbaarheid instellen, zodat uw code meer of minder tijd krijgt voor het volledig verwerken van elk bericht.</span><span class="sxs-lookup"><span data-stu-id="263fe-130">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time to fully process each message.</span></span> <span data-ttu-id="263fe-131">Het volgende codevoorbeeld wordt de **ophalen\_berichten** methode 16 berichten in één aanroep ophalen.</span><span class="sxs-lookup"><span data-stu-id="263fe-131">The following code example uses the **get\_messages** method to get 16 messages in one call.</span></span> <span data-ttu-id="263fe-132">Vervolgens wordt verwerkt elke bericht met een for-lus.</span><span class="sxs-lookup"><span data-stu-id="263fe-132">Then it processes each message using a for loop.</span></span> <span data-ttu-id="263fe-133">De time-out voor onzichtbaarheid wordt ingesteld op vijf minuten voor elk bericht.</span><span class="sxs-lookup"><span data-stu-id="263fe-133">It also sets the invisibility timeout to five minutes for each message.</span></span>

```python
messages = queue_service.get_messages('taskqueue', num_messages=16, visibility_timeout=5*60)
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)        
```

## <a name="how-to-change-the-contents-of-a-queued-message"></a><span data-ttu-id="263fe-134">Procedure: De inhoud van een bericht in de wachtrij wijzigen</span><span class="sxs-lookup"><span data-stu-id="263fe-134">How To: Change the Contents of a Queued Message</span></span>
<span data-ttu-id="263fe-135">U kunt de inhoud van een bericht in de wachtrij wijzigen.</span><span class="sxs-lookup"><span data-stu-id="263fe-135">You can change the contents of a message in-place in the queue.</span></span> <span data-ttu-id="263fe-136">Als het bericht een werktaak vertegenwoordigt, kunt u deze functie gebruiken om de status van de werktaak bij te werken.</span><span class="sxs-lookup"><span data-stu-id="263fe-136">If the message represents a work task, you could use this feature to update the status of the work task.</span></span> <span data-ttu-id="263fe-137">De code hieronder maakt gebruik van de **bijwerken\_bericht** methode voor het bijwerken van een bericht.</span><span class="sxs-lookup"><span data-stu-id="263fe-137">The code below uses the **update\_message** method to update a message.</span></span> <span data-ttu-id="263fe-138">Time-out voor de zichtbaarheid is ingesteld op 0, wat betekent dat het bericht verschijnt onmiddellijk en de inhoud wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="263fe-138">The visibility timeout is set to 0, meaning the message appears immediately and the content is updated.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    queue_service.update_message('taskqueue', message.id, message.pop_receipt, 0, u'Hello World Again')
```

## <a name="how-to-get-the-queue-length"></a><span data-ttu-id="263fe-139">Procedure: De lengte van de wachtrij ophalen</span><span class="sxs-lookup"><span data-stu-id="263fe-139">How To: Get the Queue Length</span></span>
<span data-ttu-id="263fe-140">U kunt een schatting ophalen van het aantal berichten in de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="263fe-140">You can get an estimate of the number of messages in a queue.</span></span> <span data-ttu-id="263fe-141">De **ophalen\_wachtrij\_metagegevens** methode vraagt de queue-service om terug te keren metagegevens over de wachtrij en de **approximate_message_count**.</span><span class="sxs-lookup"><span data-stu-id="263fe-141">The **get\_queue\_metadata** method asks the queue service to return metadata about the queue, and the **approximate_message_count**.</span></span> <span data-ttu-id="263fe-142">Het resultaat is alleen een benadering omdat berichten kunnen worden toegevoegd of verwijderd nadat de queue-service op uw aanvraag reageert.</span><span class="sxs-lookup"><span data-stu-id="263fe-142">The result is only approximate because messages can be added or removed after the queue service responds to your request.</span></span>

```python
metadata = queue_service.get_queue_metadata('taskqueue')
count = metadata.approximate_message_count
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="263fe-143">Procedure: Een wachtrij verwijderen</span><span class="sxs-lookup"><span data-stu-id="263fe-143">How To: Delete a Queue</span></span>
<span data-ttu-id="263fe-144">Aanroepen voor het verwijderen van een wachtrij en alle berichten hierin de **verwijderen\_wachtrij** methode.</span><span class="sxs-lookup"><span data-stu-id="263fe-144">To delete a queue and all the messages contained in it, call the **delete\_queue** method.</span></span>

```python
queue_service.delete_queue('taskqueue')
```

## <a name="next-steps"></a><span data-ttu-id="263fe-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="263fe-145">Next Steps</span></span>
<span data-ttu-id="263fe-146">Nu u de basisprincipes van Queue storage hebt geleerd, volgt u deze koppelingen voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="263fe-146">Now that you've learned the basics of Queue storage, follow these links to learn more.</span></span>

* [<span data-ttu-id="263fe-147">Python Developer Center</span><span class="sxs-lookup"><span data-stu-id="263fe-147">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="263fe-148">REST-API voor Azure Storage-services</span><span class="sxs-lookup"><span data-stu-id="263fe-148">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="263fe-149">[Blog van het Azure Storage-team]</span><span class="sxs-lookup"><span data-stu-id="263fe-149">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="263fe-150">[Microsoft Azure-opslag-SDK voor Python]</span><span class="sxs-lookup"><span data-stu-id="263fe-150">[Microsoft Azure Storage SDK for Python]</span></span>

[Blog van het Azure Storage-team]: http://blogs.msdn.com/b/windowsazurestorage/
[Microsoft Azure-opslag-SDK voor Python]: https://github.com/Azure/azure-storage-python