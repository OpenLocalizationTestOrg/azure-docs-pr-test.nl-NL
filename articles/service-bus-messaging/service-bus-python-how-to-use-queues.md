---
title: aaaHow toouse Azure Service Bus-wachtrijen met behulp van Python | Microsoft Docs
description: Meer informatie over hoe Azure Service Bus toouse wachtrijen met Python.
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: 
ms.assetid: b95ee5cd-3b31-459c-a7f3-cf8bcf77858b
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm;lmazuel
ms.openlocfilehash: bceb84d04ff3445c3087a9c246c583d6630f07af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-python"></a><span data-ttu-id="1ec25-103">Hoe toouse Service Bus wachtrijen met behulp van Python</span><span class="sxs-lookup"><span data-stu-id="1ec25-103">How toouse Service Bus queues with Python</span></span>

[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="1ec25-104">Dit artikel wordt beschreven hoe toouse Service Bus-wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="1ec25-104">This article describes how toouse Service Bus queues.</span></span> <span data-ttu-id="1ec25-105">Hallo-voorbeelden zijn geschreven in Python en gebruiken van Hallo [Python Azure Service Bus-pakket][Python Azure Service Bus package].</span><span class="sxs-lookup"><span data-stu-id="1ec25-105">hello samples are written in Python and use hello [Python Azure Service Bus package][Python Azure Service Bus package].</span></span> <span data-ttu-id="1ec25-106">Hallo scenario's worden behandeld: **maken van wachtrijen, verzenden en ontvangen berichten**, en **verwijderen van wachtrijen**.</span><span class="sxs-lookup"><span data-stu-id="1ec25-106">hello scenarios covered include **creating queues, sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

> [!NOTE]
> <span data-ttu-id="1ec25-107">tooinstall Python of Hallo [Python Azure Service Bus-pakket][Python Azure Service Bus package], Zie Hallo [Python installatiehandleiding](../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="1ec25-107">tooinstall Python or hello [Python Azure Service Bus package][Python Azure Service Bus package], see hello [Python Installation Guide](../python-how-to-install.md).</span></span>
> 
> 

## <a name="create-a-queue"></a><span data-ttu-id="1ec25-108">Een wachtrij maken</span><span class="sxs-lookup"><span data-stu-id="1ec25-108">Create a queue</span></span>
<span data-ttu-id="1ec25-109">Hallo **ServiceBusService** object kunt u toowork met wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="1ec25-109">hello **ServiceBusService** object enables you toowork with queues.</span></span> <span data-ttu-id="1ec25-110">Hallo volgende code bij Hallo bovenkant van een Python-bestand waarin u tooprogrammatically access Service Bus wilt toevoegen:</span><span class="sxs-lookup"><span data-stu-id="1ec25-110">Add hello following code near hello top of any Python file in which you wish tooprogrammatically access Service Bus:</span></span>

```python
from azure.servicebus import ServiceBusService, Message, Queue
```

<span data-ttu-id="1ec25-111">Hallo volgende code maakt een **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="1ec25-111">hello following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="1ec25-112">Vervang `mynamespace`, `sharedaccesskeyname`, en `sharedaccesskey` met uw naamruimte, naam van shared access signature (SAS)-sleutel en waarde.</span><span class="sxs-lookup"><span data-stu-id="1ec25-112">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your namespace, shared access signature (SAS) key name, and value.</span></span>

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

<span data-ttu-id="1ec25-113">Hallo waarden voor Hallo SAS-sleutelnaam en -waarde kunnen worden gevonden in Hallo [Azure-portal] [ Azure portal] verbindingsinformatie, of in Visual Studio Hallo **eigenschappen** deelvenster bij het selecteren van Hallo Service Bus-naamruimte in Server Explorer (zoals weergegeven in de vorige sectie Hallo).</span><span class="sxs-lookup"><span data-stu-id="1ec25-113">hello values for hello SAS key name and value can be found in hello [Azure portal][Azure portal] connection information, or in hello Visual Studio **Properties** pane when selecting hello Service Bus namespace in Server Explorer (as shown in hello previous section).</span></span>

```python
bus_service.create_queue('taskqueue')
```

<span data-ttu-id="1ec25-114">Hallo `create_queue` methode biedt ook ondersteuning voor extra opties waarmee u toooverride standaard wachtrij-instellingen zoals bericht toolive TTL (time) of de maximale wachtrijgrootte.</span><span class="sxs-lookup"><span data-stu-id="1ec25-114">hello `create_queue` method also supports additional options, which enable you toooverride default queue settings such as message time toolive (TTL) or maximum queue size.</span></span> <span data-ttu-id="1ec25-115">Hallo volgende voorbeeld wordt Hallo wachtrij maximale grootte too5 GB en Hallo TTL-waarde too1 minuut:</span><span class="sxs-lookup"><span data-stu-id="1ec25-115">hello following example sets hello maximum queue size too5 GB, and hello TTL value too1 minute:</span></span>

```python
queue_options = Queue()
queue_options.max_size_in_megabytes = '5120'
queue_options.default_message_time_to_live = 'PT1M'

bus_service.create_queue('taskqueue', queue_options)
```

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="1ec25-116">Berichten tooa wachtrij verzenden</span><span class="sxs-lookup"><span data-stu-id="1ec25-116">Send messages tooa queue</span></span>
<span data-ttu-id="1ec25-117">een bericht tooa Service Bus-wachtrij toosend, roept uw toepassing hello `send_queue_message` methode op Hallo **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="1ec25-117">toosend a message tooa Service Bus queue, your application calls hello `send_queue_message` method on hello **ServiceBusService** object.</span></span>

<span data-ttu-id="1ec25-118">Hallo volgende voorbeeld laat zien hoe toosend een test toohello berichtenwachtrij genoemd `taskqueue` met `send_queue_message`:</span><span class="sxs-lookup"><span data-stu-id="1ec25-118">hello following example demonstrates how toosend a test message toohello queue named `taskqueue` using `send_queue_message`:</span></span>

```python
msg = Message(b'Test Message')
bus_service.send_queue_message('taskqueue', msg)
```

<span data-ttu-id="1ec25-119">Service Bus-wachtrijen ondersteunen een maximale berichtgrootte van 256 KB in Hallo [standaardcategorie](service-bus-premium-messaging.md) en 1 MB in Hallo [Premium-laag](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="1ec25-119">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="1ec25-120">Hallo-kop, die standaard Hallo- en aangepaste toepassingseigenschappen bevat, kan een maximale grootte van 64 KB hebben.</span><span class="sxs-lookup"><span data-stu-id="1ec25-120">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="1ec25-121">Er is geen limiet voor het aantal berichten in een wachtrij hello, maar er is een limiet voor de totale grootte van berichten in een wachtrij Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="1ec25-121">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="1ec25-122">De grootte van de wachtrij wordt gedefinieerd tijdens het aanmaken, met een bovengrens van 5 GB.</span><span class="sxs-lookup"><span data-stu-id="1ec25-122">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="1ec25-123">Zie voor meer informatie over quota [Service Bus-quota][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="1ec25-123">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="1ec25-124">Berichten ontvangen uit een wachtrij</span><span class="sxs-lookup"><span data-stu-id="1ec25-124">Receive messages from a queue</span></span>
<span data-ttu-id="1ec25-125">Berichten worden ontvangen van een wachtrij met Hallo `receive_queue_message` methode op Hallo **ServiceBusService** object:</span><span class="sxs-lookup"><span data-stu-id="1ec25-125">Messages are received from a queue using hello `receive_queue_message` method on hello **ServiceBusService** object:</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=False)
print(msg.body)
```

<span data-ttu-id="1ec25-126">Berichten worden verwijderd uit de wachtrij Hallo als ze worden gelezen wanneer de parameter Hallo `peek_lock` te is ingesteld**False**.</span><span class="sxs-lookup"><span data-stu-id="1ec25-126">Messages are deleted from hello queue as they are read when hello parameter `peek_lock` is set too**False**.</span></span> <span data-ttu-id="1ec25-127">U kunt lezen (peek) en het Hallo-bericht zonder het te verwijderen uit de wachtrij Hallo door instelling Hallo parameter vergrendelen `peek_lock` te**True**.</span><span class="sxs-lookup"><span data-stu-id="1ec25-127">You can read (peek) and lock hello message without deleting it from hello queue by setting hello parameter `peek_lock` too**True**.</span></span>

<span data-ttu-id="1ec25-128">Hallo gedrag van lezen en Hallo-bericht is verwijderd als onderdeel van Hallo ontvangstbewerking is Hallo eenvoudigste model en werkt het beste voor scenario's waarin een toepassing kan tolereren niet verwerken van een bericht in de gebeurtenis Hallo van een fout.</span><span class="sxs-lookup"><span data-stu-id="1ec25-128">hello behavior of reading and deleting hello message as part of hello receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="1ec25-129">toounderstand dit, Neem bijvoorbeeld een scenario in welke problemen van de consument Hallo Hallo aanvraag ontvangen en vervolgens vastloopt voordat het wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="1ec25-129">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="1ec25-130">Omdat Service Bus heeft gemarkeerd als verbruikt, vervolgens wanneer Hallo toepassing opnieuw wordt opgestart en verbruik van berichten opnieuw begint het Hallo-bericht, ontbreekt het Hallo-bericht dat was voorafgaande toohello crash verbruikt.</span><span class="sxs-lookup"><span data-stu-id="1ec25-130">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="1ec25-131">Als hello `peek_lock` parameter is ingesteld, te**True**, Hallo ontvangen, wordt een bewerking met twee fasen, waardoor het mogelijk toosupport toepassingen die geen ontbrekende berichten kunnen tolereren.</span><span class="sxs-lookup"><span data-stu-id="1ec25-131">If hello `peek_lock` parameter is set too**True**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="1ec25-132">Wanneer Service Bus een aanvraag ontvangt, zoeken naar het volgende bericht toobe Hallo verbruikt, wordt vergrendeld tooprevent andere consumenten het ontvangen en retourneert vervolgens toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="1ec25-132">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="1ec25-133">Nadat de toepassing hello klaar is met verwerking van het Hallo-bericht (of veilig heeft opgeslagen voor toekomstige verwerking), is de tweede fase Hallo Hallo voltooid proces ontvangen door de aanroepende Hallo **verwijderen** methode op Hallo **bericht** object.</span><span class="sxs-lookup"><span data-stu-id="1ec25-133">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling hello **delete** method on hello **Message** object.</span></span> <span data-ttu-id="1ec25-134">Hallo **verwijderen** methode wordt het Hallo-bericht als verbruikt markeren en verwijderen uit de wachtrij Hallo.</span><span class="sxs-lookup"><span data-stu-id="1ec25-134">hello **delete** method will mark hello message as being consumed and remove it from hello queue.</span></span>

```python
msg = bus_service.receive_queue_message('taskqueue', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="1ec25-135">Hoe toohandle toepassing is vastgelopen en onleesbare berichten</span><span class="sxs-lookup"><span data-stu-id="1ec25-135">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="1ec25-136">Service Bus biedt functionaliteit toohelp die u netjes te herstellen bij fouten in uw toepassing of problemen bij het verwerken van een bericht.</span><span class="sxs-lookup"><span data-stu-id="1ec25-136">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="1ec25-137">Als een ontvangende toepassing niet kan tooprocess hello bericht voor een bepaalde reden en vervolgens kan worden aangeroepen Hallo **ontgrendelen** methode op Hallo **bericht** object.</span><span class="sxs-lookup"><span data-stu-id="1ec25-137">If a receiver application is unable tooprocess hello message for some reason, then it can call hello **unlock** method on hello **Message** object.</span></span> <span data-ttu-id="1ec25-138">Hierdoor wordt ervoor zorgen dat Service Bus toounlock Hallo-bericht in de wachtrij Hallo en beschikbare toobe opnieuw ontvangen, ofwel Hallo door dezelfde toepassing of door een andere consumerende toepassing verbruikt.</span><span class="sxs-lookup"><span data-stu-id="1ec25-138">This will cause Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="1ec25-139">Daarnaast is er een time-out gekoppeld aan een bericht in de wachtrij Hallo is vergrendeld en als Hallo toepassing mislukt tooprocess Hallo-bericht voordat Hallo time-out van de vergrendeling verloopt (bijvoorbeeld als Hallo toepassing vastloopt), en vervolgens de Service Bus wordt het Hallo-bericht automatisch ontgrendelen en het beschikbaar toobe ontvangen opnieuw maken.</span><span class="sxs-lookup"><span data-stu-id="1ec25-139">There is also a timeout associated with a message locked within hello queue, and if hello application fails tooprocess hello message before hello lock timeout expires (e.g., if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="1ec25-140">In Hallo gebeurtenis die toepassing hello vastgelopen na het verwerken van het Hallo-bericht, maar voordat u Hallo **verwijderen** methode wordt aangeroepen, is het Hallo-bericht altijd opnieuw bezorgd toohello toepassing opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="1ec25-140">In hello event that hello application crashes after processing hello message but before hello **delete** method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="1ec25-141">Dit wordt vaak genoemd **tenminste eenmaal verwerken**, dat wil zeggen elk bericht ten minste één keer wordt verwerkt maar in bepaalde situaties Hallo hetzelfde bericht opnieuw kan worden bezorgd.</span><span class="sxs-lookup"><span data-stu-id="1ec25-141">This is often called **At Least Once Processing**, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="1ec25-142">Als Hallo scenario kan geen dubbele verwerking tolereren, moeten toepassingsontwikkelaars levering van aanvullende logica tootheir toepassing toohandle dubbele berichten toevoegen.</span><span class="sxs-lookup"><span data-stu-id="1ec25-142">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="1ec25-143">Dit wordt vaak bereikt met behulp van Hallo **MessageId** eigenschap van Hallo-bericht dat gelijk bij meerdere bezorgingspogingen blijft.</span><span class="sxs-lookup"><span data-stu-id="1ec25-143">This is often achieved using hello **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1ec25-144">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1ec25-144">Next steps</span></span>
<span data-ttu-id="1ec25-145">Nu u Hallo basisprincipes van Service Bus-wachtrijen hebt geleerd, gaat u naar deze artikelen toolearn meer.</span><span class="sxs-lookup"><span data-stu-id="1ec25-145">Now that you have learned hello basics of Service Bus queues, see these articles toolearn more.</span></span>

* <span data-ttu-id="1ec25-146">[Wachtrijen, onderwerpen en abonnementen][Queues, topics, and subscriptions]</span><span class="sxs-lookup"><span data-stu-id="1ec25-146">[Queues, topics, and subscriptions][Queues, topics, and subscriptions]</span></span>

[Azure portal]: https://portal.azure.com
[Python Azure Service Bus package]: https://pypi.python.org/pypi/azure-servicebus  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[Service Bus quotas]: service-bus-quotas.md

