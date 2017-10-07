---
title: aaaHow toouse Queue storage met Python | Microsoft Docs
description: Informatie over hoe toouse hello Azure Queue-service van Python toocreate en verwijderen van wachtrijen, en invoegen, ophalen en verwijderen van berichten.
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
ms.openlocfilehash: ce8d999d9fafaef0dab48442560d004c034c0804
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-queue-storage-from-python"></a><span data-ttu-id="7e761-103">Hoe toouse Queue storage met Python</span><span class="sxs-lookup"><span data-stu-id="7e761-103">How toouse Queue storage from Python</span></span>
[!INCLUDE [storage-selector-queue-include](../../includes/storage-selector-queue-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-queues.md)]

## <a name="overview"></a><span data-ttu-id="7e761-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="7e761-104">Overview</span></span>
<span data-ttu-id="7e761-105">Deze handleiding wordt getoond hoe tooperform algemene scenario's met behulp van hello Azure Queue storage-service.</span><span class="sxs-lookup"><span data-stu-id="7e761-105">This guide shows you how tooperform common scenarios using hello Azure Queue storage service.</span></span> <span data-ttu-id="7e761-106">Hallo-voorbeelden zijn geschreven in Python en gebruiken van Hallo [Microsoft Azure-opslag-SDK voor Python].</span><span class="sxs-lookup"><span data-stu-id="7e761-106">hello samples are written in Python and use hello [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="7e761-107">Hallo scenario's worden behandeld: **invoegen**, **inspecteren**, **ophalen**, en **verwijderen** wachtrij berichten, evenals  **maken en verwijderen van wachtrijen**.</span><span class="sxs-lookup"><span data-stu-id="7e761-107">hello scenarios covered include **inserting**, **peeking**, **getting**, and **deleting** queue messages, as well as **creating and deleting queues**.</span></span> <span data-ttu-id="7e761-108">Raadpleeg voor meer informatie over wachtrijen toohello [Vervolgstappen]-sectie.</span><span class="sxs-lookup"><span data-stu-id="7e761-108">For more information on queues, refer toohello [Next Steps] section.</span></span>

[!INCLUDE [storage-queue-concepts-include](../../includes/storage-queue-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="how-to-create-a-queue"></a><span data-ttu-id="7e761-109">Procedure: Een wachtrij maken</span><span class="sxs-lookup"><span data-stu-id="7e761-109">How To: Create a Queue</span></span>
<span data-ttu-id="7e761-110">Hallo **QueueService** object kunt u samenwerken met wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="7e761-110">hello **QueueService** object lets you work with queues.</span></span> <span data-ttu-id="7e761-111">Hallo volgende code maakt een **QueueService** object.</span><span class="sxs-lookup"><span data-stu-id="7e761-111">hello following code creates a **QueueService** object.</span></span> <span data-ttu-id="7e761-112">Voeg de volgende Hallo bij Hallo bovenkant van een Python-bestand waarin u wenst dat tooprogrammatically toegang tot Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="7e761-112">Add hello following near hello top of any Python file in which you wish tooprogrammatically access Azure Storage:</span></span>

```python
from azure.storage.queue import QueueService
```

<span data-ttu-id="7e761-113">Hallo volgende code maakt een **QueueService** -object op met de Hallo naam en opslagaccountsleutel.</span><span class="sxs-lookup"><span data-stu-id="7e761-113">hello following code creates a **QueueService** object using hello storage account name and account key.</span></span> <span data-ttu-id="7e761-114">'Myaccount' en 'mykey' vervangen door uw accountnaam en de sleutel.</span><span class="sxs-lookup"><span data-stu-id="7e761-114">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
queue_service = QueueService(account_name='myaccount', account_key='mykey')

queue_service.create_queue('taskqueue')
```

## <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="7e761-115">Procedure: Een bericht in een wachtrij invoegen</span><span class="sxs-lookup"><span data-stu-id="7e761-115">How To: Insert a Message into a Queue</span></span>
<span data-ttu-id="7e761-116">een bericht in een wachtrij, gebruik Hallo tooinsert **plaatsen\_bericht** methode voor het maken van een nieuw bericht en deze wachtrij toohello toevoegen.</span><span class="sxs-lookup"><span data-stu-id="7e761-116">tooinsert a message into a queue, use hello **put\_message** method to create a new message and add it toohello queue.</span></span>

```python
queue_service.put_message('taskqueue', u'Hello World')
```

## <a name="how-to-peek-at-hello-next-message"></a><span data-ttu-id="7e761-117">Procedure: Inspecteren Hallo het Volgendebericht</span><span class="sxs-lookup"><span data-stu-id="7e761-117">How To: Peek at hello Next Message</span></span>
<span data-ttu-id="7e761-118">U kunt bekijken van Hallo-bericht in Hallo begin van een wachtrij zonder het te verwijderen uit de wachtrij Hallo door aanroepen Hallo **peek\_berichten** methode.</span><span class="sxs-lookup"><span data-stu-id="7e761-118">You can peek at hello message in hello front of a queue without removing it from hello queue by calling hello **peek\_messages** method.</span></span> <span data-ttu-id="7e761-119">Standaard **peek\_berichten** peeks op één bericht.</span><span class="sxs-lookup"><span data-stu-id="7e761-119">By default, **peek\_messages** peeks at a single message.</span></span>

```python
messages = queue_service.peek_messages('taskqueue')
for message in messages:
    print(message.content)
```

## <a name="how-to-dequeue-messages"></a><span data-ttu-id="7e761-120">Procedure: Berichten in wachtrij</span><span class="sxs-lookup"><span data-stu-id="7e761-120">How To: Dequeue Messages</span></span>
<span data-ttu-id="7e761-121">Uw code wordt een bericht uit een wachtrij in twee stappen.</span><span class="sxs-lookup"><span data-stu-id="7e761-121">Your code removes a message from a queue in two steps.</span></span> <span data-ttu-id="7e761-122">Als u aanroept **ophalen\_berichten**, u het volgende Hallo-bericht in een wachtrij standaard ophalen.</span><span class="sxs-lookup"><span data-stu-id="7e761-122">When you call **get\_messages**, you get hello next message in a queue by default.</span></span> <span data-ttu-id="7e761-123">Een bericht dat wordt geretourneerd door **ophalen\_berichten** wordt onzichtbaar tooany andere codes die berichten lezen uit deze wachtrij.</span><span class="sxs-lookup"><span data-stu-id="7e761-123">A message returned from **get\_messages** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="7e761-124">Standaard blijft het bericht onzichtbaar gedurende 30 seconden.</span><span class="sxs-lookup"><span data-stu-id="7e761-124">By default, this message stays invisible for 30 seconds.</span></span> <span data-ttu-id="7e761-125">toofinish verwijderen Hallo-bericht uit de wachtrij hello, moet u ook aanroepen **verwijderen\_bericht**.</span><span class="sxs-lookup"><span data-stu-id="7e761-125">toofinish removing hello message from hello queue, you must also call **delete\_message**.</span></span> <span data-ttu-id="7e761-126">Dit proces in twee stappen van het verwijderen van een bericht zorgt ervoor dat wanneer uw code tooprocess een bericht als gevolg van hardware-of softwarefout mislukt, een ander exemplaar van uw code kunt het bericht verschijnt en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="7e761-126">This two-step process of removing a message assures that when your code fails tooprocess a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="7e761-127">Uw code haalt **verwijderen\_bericht** direct nadat het Hallo-bericht is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="7e761-127">Your code calls **delete\_message** right after hello message has been processed.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)
```

<span data-ttu-id="7e761-128">Er zijn twee manieren waarop u het ophalen van berichten uit een wachtrij kunt aanpassen.</span><span class="sxs-lookup"><span data-stu-id="7e761-128">There are two ways you can customize message retrieval from a queue.</span></span>
<span data-ttu-id="7e761-129">U krijgt eerst een batch met berichten (omhoog too32).</span><span class="sxs-lookup"><span data-stu-id="7e761-129">First, you can get a batch of messages (up too32).</span></span> <span data-ttu-id="7e761-130">Ten tweede kunt u instellen een time-out voor onzichtbaarheid langer of korter, zodat uw code meer of minder tijd toofully elk bericht niet verwerken.</span><span class="sxs-lookup"><span data-stu-id="7e761-130">Second, you can set a longer or shorter invisibility timeout, allowing your code more or less time toofully process each message.</span></span> <span data-ttu-id="7e761-131">Hallo volgende codevoorbeeld wordt de **ophalen\_berichten** methode tooget 16 berichten in één aanroep.</span><span class="sxs-lookup"><span data-stu-id="7e761-131">hello following code example uses the **get\_messages** method tooget 16 messages in one call.</span></span> <span data-ttu-id="7e761-132">Vervolgens wordt verwerkt elke bericht met een for-lus.</span><span class="sxs-lookup"><span data-stu-id="7e761-132">Then it processes each message using a for loop.</span></span> <span data-ttu-id="7e761-133">Time-out voor onzichtbaarheid van Hallo wordt ingesteld op vijf minuten voor elk bericht.</span><span class="sxs-lookup"><span data-stu-id="7e761-133">It also sets hello invisibility timeout to five minutes for each message.</span></span>

```python
messages = queue_service.get_messages('taskqueue', num_messages=16, visibility_timeout=5*60)
for message in messages:
    print(message.content)
    queue_service.delete_message('taskqueue', message.id, message.pop_receipt)        
```

## <a name="how-to-change-hello-contents-of-a-queued-message"></a><span data-ttu-id="7e761-134">Procedure: Hallo inhoud van een bericht in de wachtrij wijzigen</span><span class="sxs-lookup"><span data-stu-id="7e761-134">How To: Change hello Contents of a Queued Message</span></span>
<span data-ttu-id="7e761-135">U kunt Hallo inhoud van een bericht in-place in Hallo wachtrij wijzigen.</span><span class="sxs-lookup"><span data-stu-id="7e761-135">You can change hello contents of a message in-place in hello queue.</span></span> <span data-ttu-id="7e761-136">Als het bericht een werktaak vertegenwoordigt, kunt u deze functie tooupdate de status van de werktaak hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7e761-136">If the message represents a work task, you could use this feature tooupdate the status of hello work task.</span></span> <span data-ttu-id="7e761-137">Hallo-code hieronder maakt gebruik van Hallo **bijwerken\_bericht** methode tooupdate een bericht.</span><span class="sxs-lookup"><span data-stu-id="7e761-137">hello code below uses hello **update\_message** method tooupdate a message.</span></span> <span data-ttu-id="7e761-138">Hallo zichtbaarheid time-out ingesteld too0, wat betekent dat het bericht verschijnt onmiddellijk en Hallo inhoud wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="7e761-138">hello visibility timeout is set too0, meaning the message appears immediately and hello content is updated.</span></span>

```python
messages = queue_service.get_messages('taskqueue')
for message in messages:
    queue_service.update_message('taskqueue', message.id, message.pop_receipt, 0, u'Hello World Again')
```

## <a name="how-to-get-hello-queue-length"></a><span data-ttu-id="7e761-139">Procedure: Hallo wachtrijlengte ophalen</span><span class="sxs-lookup"><span data-stu-id="7e761-139">How To: Get hello Queue Length</span></span>
<span data-ttu-id="7e761-140">U kunt een schatting maken van het aantal berichten Hallo krijgen in een wachtrij.</span><span class="sxs-lookup"><span data-stu-id="7e761-140">You can get an estimate of hello number of messages in a queue.</span></span> <span data-ttu-id="7e761-141">De **ophalen\_wachtrij\_metagegevens** methode vraagt Hallo wachtrij tooreturn metagegevens over Hallo wachtrij en Hallo **approximate_message_count**.</span><span class="sxs-lookup"><span data-stu-id="7e761-141">The **get\_queue\_metadata** method asks hello queue service tooreturn metadata about hello queue, and hello **approximate_message_count**.</span></span> <span data-ttu-id="7e761-142">Hallo-resultaat is alleen een benadering omdat berichten kunnen worden toegevoegd of verwijderd nadat de queue-service tooyour aanvraag reageert.</span><span class="sxs-lookup"><span data-stu-id="7e761-142">hello result is only approximate because messages can be added or removed after the queue service responds tooyour request.</span></span>

```python
metadata = queue_service.get_queue_metadata('taskqueue')
count = metadata.approximate_message_count
```

## <a name="how-to-delete-a-queue"></a><span data-ttu-id="7e761-143">Procedure: Een wachtrij verwijderen</span><span class="sxs-lookup"><span data-stu-id="7e761-143">How To: Delete a Queue</span></span>
<span data-ttu-id="7e761-144">toodelete een wachtrij en alle Hallo-berichten die dit, neemt u contact de **verwijderen\_wachtrij** methode.</span><span class="sxs-lookup"><span data-stu-id="7e761-144">toodelete a queue and all hello messages contained in it, call the **delete\_queue** method.</span></span>

```python
queue_service.delete_queue('taskqueue')
```

## <a name="next-steps"></a><span data-ttu-id="7e761-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7e761-145">Next Steps</span></span>
<span data-ttu-id="7e761-146">Nu u Hallo basisprincipes van Queue storage hebt geleerd, volgt u deze koppelingen toolearn meer.</span><span class="sxs-lookup"><span data-stu-id="7e761-146">Now that you've learned hello basics of Queue storage, follow these links toolearn more.</span></span>

* [<span data-ttu-id="7e761-147">Python Developer Center</span><span class="sxs-lookup"><span data-stu-id="7e761-147">Python Developer Center</span></span>](/develop/python/)
* [<span data-ttu-id="7e761-148">REST-API voor Azure Storage-services</span><span class="sxs-lookup"><span data-stu-id="7e761-148">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="7e761-149">[Blog van het Azure Storage-team]</span><span class="sxs-lookup"><span data-stu-id="7e761-149">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="7e761-150">[Microsoft Azure-opslag-SDK voor Python]</span><span class="sxs-lookup"><span data-stu-id="7e761-150">[Microsoft Azure Storage SDK for Python]</span></span>

[Blog van het Azure Storage-team]: http://blogs.msdn.com/b/windowsazurestorage/
[Microsoft Azure-opslag-SDK voor Python]: https://github.com/Azure/azure-storage-python