---
title: aaaHow toouse Azure Service Bus-onderwerpen met behulp van Python | Microsoft Docs
description: Meer informatie over hoe toouse Azure Service Bus-onderwerpen en abonnementen van Python.
services: service-bus-messaging
documentationcenter: python
author: sethmanheim
manager: timlt
editor: 
ms.assetid: c4f1d76c-7567-4b33-9193-3788f82934e4
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 1171cbe8061bb3d73e2ce92ecc0cf45afae37054
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-python"></a><span data-ttu-id="ea7d3-103">Hoe toouse Service Bus-onderwerpen en abonnementen, met Python</span><span class="sxs-lookup"><span data-stu-id="ea7d3-103">How toouse Service Bus topics and subscriptions with Python</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="ea7d3-104">Dit artikel wordt beschreven hoe toouse Service Bus-onderwerpen en abonnementen.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-104">This article describes how toouse Service Bus topics and subscriptions.</span></span> <span data-ttu-id="ea7d3-105">Hallo-voorbeelden zijn geschreven in Python en gebruiken van Hallo [Azure Python SDK-pakket][Azure Python package].</span><span class="sxs-lookup"><span data-stu-id="ea7d3-105">hello samples are written in Python and use hello [Azure Python SDK package][Azure Python package].</span></span> <span data-ttu-id="ea7d3-106">Hallo scenario's worden behandeld: **maken van onderwerpen en abonnementen**, **maken van abonnementsfilters**, **verzenden van berichten tooa onderwerp**, **ontvangen berichten van een abonnement**, en **verwijderen van onderwerpen en abonnementen**.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-106">hello scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages tooa topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="ea7d3-107">Zie voor meer informatie over onderwerpen en abonnementen Hallo [Vervolgstappen](#next-steps) sectie.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-107">For more information about topics and subscriptions, see hello [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

> [!NOTE] 
> <span data-ttu-id="ea7d3-108">Als u tooinstall Python of Hallo nodig [Azure Python-pakket][Azure Python package], Zie Hallo [Python installatiehandleiding](../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="ea7d3-108">If you need tooinstall Python or hello [Azure Python package][Azure Python package], see hello [Python Installation Guide](../python-how-to-install.md).</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="ea7d3-109">Een onderwerp maken</span><span class="sxs-lookup"><span data-stu-id="ea7d3-109">Create a topic</span></span>
<span data-ttu-id="ea7d3-110">Hallo **ServiceBusService** object kunt u toowork met onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-110">hello **ServiceBusService** object enables you toowork with topics.</span></span> <span data-ttu-id="ea7d3-111">Voeg de volgende Hallo bij Hallo bovenkant van een Python-bestand waarin u wenst dat tooprogrammatically access Service Bus:</span><span class="sxs-lookup"><span data-stu-id="ea7d3-111">Add hello following near hello top of any Python file in which you wish tooprogrammatically access Service Bus:</span></span>

```python
from azure.servicebus import ServiceBusService, Message, Topic, Rule, DEFAULT_RULE_NAME
```

<span data-ttu-id="ea7d3-112">Hallo volgende code maakt een **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-112">hello following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="ea7d3-113">Vervang `mynamespace`, `sharedaccesskeyname`, en `sharedaccesskey` met uw werkelijke naamruimte Shared Access Signature (SAS) sleutelwaarde naam en een sleutel.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-113">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your actual namespace, Shared Access Signature (SAS) key name, and key value.</span></span>

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

<span data-ttu-id="ea7d3-114">U kunt ophalen Hallo waarden voor Hallo SAS-sleutelnaam en de waarde Hallo [Azure-portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="ea7d3-114">You can obtain hello values for hello SAS key name and value from hello [Azure portal][Azure portal].</span></span>

```python
bus_service.create_topic('mytopic')
```

<span data-ttu-id="ea7d3-115">Hallo `create_topic` methode biedt ook ondersteuning voor extra opties waarmee u toooverride standaardinstellingen onderwerp zoals bericht tijd onderwerp toolive of de maximale grootte.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-115">hello `create_topic` method also supports additional options, which enable you toooverride default topic settings such as message time toolive or maximum topic size.</span></span> <span data-ttu-id="ea7d3-116">Hallo volgende voorbeeld wordt Hallo onderwerp maximale grootte too5 GB en een tijd toolive (TTL)-waarde van 1 minuut:</span><span class="sxs-lookup"><span data-stu-id="ea7d3-116">hello following example sets hello maximum topic size too5 GB, and a time toolive (TTL) value of 1 minute:</span></span>

```python
topic_options = Topic()
topic_options.max_size_in_megabytes = '5120'
topic_options.default_message_time_to_live = 'PT1M'

bus_service.create_topic('mytopic', topic_options)
```

## <a name="create-subscriptions"></a><span data-ttu-id="ea7d3-117">Abonnementen maken</span><span class="sxs-lookup"><span data-stu-id="ea7d3-117">Create subscriptions</span></span>
<span data-ttu-id="ea7d3-118">Abonnementen tootopics tevens zijn gemaakt met de Hallo **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-118">Subscriptions tootopics are also created with hello **ServiceBusService** object.</span></span> <span data-ttu-id="ea7d3-119">Abonnementen kunnen worden genoemd en een optioneel filter waarmee Hallo verzameling berichten dat de virtuele wachtrij van het abonnement toohello wordt beperkt.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-119">Subscriptions are named and can have an optional filter that restricts hello set of messages delivered toohello subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="ea7d3-120">Abonnementen worden permanent en tooexist zal worden voortgezet totdat beide ze of hello onderwerp toowhich ze bent geabonneerd, worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-120">Subscriptions are persistent and will continue tooexist until either they, or hello topic toowhich they are subscribed, are deleted.</span></span>
> 
> 

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="ea7d3-121">Een abonnement maken met de Hallo standaardfilter (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="ea7d3-121">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="ea7d3-122">Hallo **MatchAll** filter is Hallo standaardfilter dat wordt gebruikt als geen filter is opgegeven als een nieuw abonnement wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-122">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="ea7d3-123">Wanneer Hallo **MatchAll** filter wordt gebruikt, worden alle berichten gepubliceerde toohello onderwerp in virtuele wachtrij van Hallo abonnement geplaatst.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-123">When hello **MatchAll** filter is used, all messages published toohello topic are placed in hello subscription's virtual queue.</span></span> <span data-ttu-id="ea7d3-124">Hallo volgende voorbeeld maakt u een abonnement met de naam `AllMessages` en gebruikt standaard Hallo **MatchAll** filter.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-124">hello following example creates a subscription named `AllMessages` and uses hello default **MatchAll** filter.</span></span>

```python
bus_service.create_subscription('mytopic', 'AllMessages')
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="ea7d3-125">Abonnementen met filters maken</span><span class="sxs-lookup"><span data-stu-id="ea7d3-125">Create subscriptions with filters</span></span>
<span data-ttu-id="ea7d3-126">U kunt ook filters waarmee u welke berichten verzonden tooa onderwerp weergegeven binnen een bepaald onderwerpabonnement toospecify definiëren.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-126">You can also define filters that enable you toospecify which messages sent tooa topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="ea7d3-127">Hallo meest flexibele type filter dat wordt ondersteund door abonnementen is een **SqlFilter**, waarmee een subset van SQL92 wordt geïmplementeerd implementeert.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-127">hello most flexible type of filter supported by subscriptions is a **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="ea7d3-128">SQL-filters worden uitgevoerd op Hallo eigenschappen van Hallo-berichten die gepubliceerd toohello onderwerp zijn.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-128">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="ea7d3-129">Zie voor meer informatie over Hallo expressies die kunnen worden gebruikt met een SQL-filter Hallo [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] syntaxis.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-129">For more information about hello expressions that can be used with a SQL filter, see hello [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="ea7d3-130">U kunt filters tooa abonnement kunt toevoegen met behulp van Hallo **maken\_regel** methode Hallo **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-130">You can add filters tooa subscription by using hello **create\_rule** method of hello **ServiceBusService** object.</span></span> <span data-ttu-id="ea7d3-131">Deze methode kunt u tooadd nieuwe filters tooan bestaande abonnement.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-131">This method allows you tooadd new filters tooan existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="ea7d3-132">Omdat het standaardfilter hello wordt automatisch toegepast tooall nieuwe abonnementen, moet u eerst het standaardfilter Hallo of Hallo verwijderen **MatchAll** overschrijft alle andere filters die u kunt opgeven.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-132">Because hello default filter is applied automatically tooall new subscriptions, you must first remove hello default filter or hello **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="ea7d3-133">U kunt de standaardregel Hallo verwijderen via Hallo `delete_rule` methode Hallo **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-133">You can remove hello default rule by using hello `delete_rule` method of hello **ServiceBusService** object.</span></span>
> 
> 

<span data-ttu-id="ea7d3-134">Hallo volgende voorbeeld maakt u een abonnement met de naam `HighMessages` met een **SqlFilter** die alleen berichten selecteert die een aangepaste `messagenumber` eigenschap groter is dan 3:</span><span class="sxs-lookup"><span data-stu-id="ea7d3-134">hello following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `messagenumber` property greater than 3:</span></span>

```python
bus_service.create_subscription('mytopic', 'HighMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber > 3'

bus_service.create_rule('mytopic', 'HighMessages', 'HighMessageFilter', rule)
bus_service.delete_rule('mytopic', 'HighMessages', DEFAULT_RULE_NAME)
```

<span data-ttu-id="ea7d3-135">Op deze manier hello volgende voorbeeld maakt u een abonnement met de naam `LowMessages` met een **SqlFilter** die alleen berichten selecteert die een `messagenumber` eigenschap kleiner dan of gelijk too3:</span><span class="sxs-lookup"><span data-stu-id="ea7d3-135">Similarly, hello following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a `messagenumber` property less than or equal too3:</span></span>

```python
bus_service.create_subscription('mytopic', 'LowMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber <= 3'

bus_service.create_rule('mytopic', 'LowMessages', 'LowMessageFilter', rule)
bus_service.delete_rule('mytopic', 'LowMessages', DEFAULT_RULE_NAME)
```

<span data-ttu-id="ea7d3-136">Nu wanneer een bericht verzonden te`mytopic` wordt het tooreceivers geabonneerd toohello altijd bezorgd **AllMessages** onderwerpabonnement en selectief bezorgd tooreceivers geabonneerd toohello **HighMessages**  en **LowMessages** onderwerpabonnementen (afhankelijk van de inhoud van Hallo-bericht).</span><span class="sxs-lookup"><span data-stu-id="ea7d3-136">Now, when a message is sent too`mytopic` it is always delivered tooreceivers subscribed toohello **AllMessages** topic subscription, and selectively delivered tooreceivers subscribed toohello **HighMessages** and **LowMessages** topic subscriptions (depending on hello message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="ea7d3-137">Verzenden van berichten tooa onderwerp</span><span class="sxs-lookup"><span data-stu-id="ea7d3-137">Send messages tooa topic</span></span>
<span data-ttu-id="ea7d3-138">een bericht tooa Service Bus-onderwerp toosend, uw toepassing moet gebruiken Hallo `send_topic_message` methode Hallo **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-138">toosend a message tooa Service Bus topic, your application must use hello `send_topic_message` method of hello **ServiceBusService** object.</span></span>

<span data-ttu-id="ea7d3-139">Hallo volgende voorbeeld toont hoe vijf toosend test berichten te`mytopic`.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-139">hello following example demonstrates how toosend five test messages too`mytopic`.</span></span> <span data-ttu-id="ea7d3-140">Houd er rekening mee dat Hallo `messagenumber` eigenschapswaarde van elk bericht varieert op Hallo herhaling van Hallo lus (deze bepaalt welke abonnementen ontvangen):</span><span class="sxs-lookup"><span data-stu-id="ea7d3-140">Note that hello `messagenumber` property value of each message varies on hello iteration of hello loop (this determines which subscriptions receive it):</span></span>

```python
for i in range(5):
    msg = Message('Msg {0}'.format(i).encode('utf-8'), custom_properties={'messagenumber':i})
    bus_service.send_topic_message('mytopic', msg)
```

<span data-ttu-id="ea7d3-141">Service Bus-onderwerpen ondersteunen een maximale berichtgrootte van 256 KB in Hallo [standaardcategorie](service-bus-premium-messaging.md) en 1 MB in Hallo [Premium-laag](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="ea7d3-141">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="ea7d3-142">Hallo-kop, die standaard Hallo- en aangepaste toepassingseigenschappen bevat, kan een maximale grootte van 64 KB hebben.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-142">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="ea7d3-143">Er is geen limiet voor het aantal berichten in een onderwerp hello, maar er is een limiet voor de totale grootte van berichten in een onderwerp Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-143">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="ea7d3-144">De grootte van het onderwerp wordt gedefinieerd tijdens het maken, met een bovengrens van 5 GB.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-144">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="ea7d3-145">Zie voor meer informatie over quota [Service Bus-quota][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="ea7d3-145">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="ea7d3-146">Berichten ontvangen van een abonnement</span><span class="sxs-lookup"><span data-stu-id="ea7d3-146">Receive messages from a subscription</span></span>
<span data-ttu-id="ea7d3-147">Berichten worden ontvangen van een abonnement met Hallo `receive_subscription_message` methode op Hallo **ServiceBusService** object:</span><span class="sxs-lookup"><span data-stu-id="ea7d3-147">Messages are received from a subscription using hello `receive_subscription_message` method on hello **ServiceBusService** object:</span></span>

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=False)
print(msg.body)
```

<span data-ttu-id="ea7d3-148">Berichten worden verwijderd uit het Hallo-abonnement als ze worden gelezen wanneer de parameter Hallo `peek_lock` te is ingesteld**False**.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-148">Messages are deleted from hello subscription as they are read when hello parameter `peek_lock` is set too**False**.</span></span> <span data-ttu-id="ea7d3-149">U kunt lezen (peek) en het Hallo-bericht zonder het te verwijderen uit de wachtrij Hallo door instelling Hallo parameter vergrendelen `peek_lock` te**True**.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-149">You can read (peek) and lock hello message without deleting it from hello queue by setting hello parameter `peek_lock` too**True**.</span></span>

<span data-ttu-id="ea7d3-150">Hallo gedrag van lezen en Hallo-bericht is verwijderd als onderdeel van Hallo ontvangstbewerking is Hallo eenvoudigste model en werkt het beste voor scenario's waarin een toepassing kan tolereren niet verwerken van een bericht in de gebeurtenis Hallo van een fout.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-150">hello behavior of reading and deleting hello message as part of hello receive operation is hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="ea7d3-151">toounderstand dit, Neem bijvoorbeeld een scenario in welke problemen van de consument Hallo Hallo aanvraag ontvangen en vervolgens vastloopt voordat het wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-151">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="ea7d3-152">Omdat Service Bus heeft gemarkeerd als verbruikt, vervolgens wanneer Hallo toepassing opnieuw wordt opgestart en verbruik van berichten opnieuw begint het Hallo-bericht, ontbreekt het Hallo-bericht dat was voorafgaande toohello crash verbruikt.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-152">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="ea7d3-153">Als hello `peek_lock` parameter is ingesteld, te**True**, Hallo ontvangen, wordt een bewerking met twee fasen, waardoor het mogelijk toosupport toepassingen die geen ontbrekende berichten kunnen tolereren.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-153">If hello `peek_lock` parameter is set too**True**, hello receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="ea7d3-154">Wanneer Service Bus een aanvraag ontvangt, zoeken naar het volgende bericht toobe Hallo verbruikt, wordt vergrendeld tooprevent andere consumenten het ontvangen en retourneert vervolgens toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-154">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="ea7d3-155">Nadat de toepassing hello klaar is met verwerking van het Hallo-bericht (of veilig heeft opgeslagen voor toekomstige verwerking), is de tweede fase Hallo Hallo voltooid proces ontvangen door het aanroepen van `delete` methode op Hallo **bericht** object.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-155">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling `delete` method on hello **Message** object.</span></span> <span data-ttu-id="ea7d3-156">Hallo `delete` methode markeert het Hallo-bericht als verbruikt en wordt deze verwijderd uit het Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-156">hello `delete` method marks hello message as being consumed and removes it from hello subscription.</span></span>

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="ea7d3-157">Hoe toohandle toepassing is vastgelopen en onleesbare berichten</span><span class="sxs-lookup"><span data-stu-id="ea7d3-157">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="ea7d3-158">Service Bus biedt functionaliteit toohelp die u netjes te herstellen bij fouten in uw toepassing of problemen bij het verwerken van een bericht.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-158">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="ea7d3-159">Als een ontvangende toepassing niet kan tooprocess hello bericht voor een bepaalde reden en vervolgens kan worden aangeroepen Hallo `unlock` methode op Hallo **bericht** object.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-159">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlock` method on hello **Message** object.</span></span> <span data-ttu-id="ea7d3-160">Hierdoor wordt ervoor zorgen dat Service Bus toounlock Hallo-bericht binnen Hallo-abonnement en beschikbaar toobe opnieuw ontvangen, ofwel Hallo door dezelfde toepassing of door een andere consumerende toepassing verbruikt.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-160">This will cause Service Bus toounlock hello message within hello subscription and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="ea7d3-161">Daarnaast is er een time-out gekoppeld aan een bericht in het Hallo-abonnement is vergrendeld en als de toepassing hello tooprocess Hallo-bericht voordat mislukt Hallo vergrendelingstime-out verloopt (bijvoorbeeld als Hallo toepassing vastloopt), en vervolgens de Service Bus Hiermee ontgrendelt u het Hallo-bericht automatisch en wordt het beschikbaar toobe opnieuw ontvangen.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-161">There is also a timeout associated with a message locked within hello subscription, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message automatically and makes it available toobe received again.</span></span>

<span data-ttu-id="ea7d3-162">In Hallo gebeurtenis die toepassing hello vastgelopen na het verwerken van het Hallo-bericht, maar voordat u Hallo `delete` methode wordt aangeroepen, is het Hallo-bericht altijd opnieuw bezorgd toohello toepassing opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-162">In hello event that hello application crashes after processing hello message but before hello `delete` method is called, then hello message will be redelivered toohello application when it restarts.</span></span> <span data-ttu-id="ea7d3-163">Dit wordt vaak genoemd *tenminste eenmaal verwerken*, dat wil zeggen elk bericht ten minste één keer wordt verwerkt maar in bepaalde situaties Hallo hetzelfde bericht opnieuw kan worden bezorgd.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-163">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="ea7d3-164">Als Hallo scenario kan geen dubbele verwerking tolereren, moeten toepassingsontwikkelaars levering van aanvullende logica tootheir toepassing toohandle dubbele berichten toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-164">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="ea7d3-165">Dit wordt vaak bereikt met behulp van Hallo **MessageId** eigenschap van Hallo-bericht dat gelijk bij meerdere bezorgingspogingen blijft.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-165">This is often achieved using hello **MessageId** property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="ea7d3-166">Onderwerpen en abonnementen verwijderen</span><span class="sxs-lookup"><span data-stu-id="ea7d3-166">Delete topics and subscriptions</span></span>
<span data-ttu-id="ea7d3-167">Onderwerpen en abonnementen worden permanent en expliciet moet worden verwijderd via Hallo [Azure-portal] [ Azure portal] of via een programma.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-167">Topics and subscriptions are persistent, and must be explicitly deleted either through hello [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="ea7d3-168">Hallo volgende voorbeeld laat zien hoe toodelete Hallo onderwerp met de naam `mytopic`:</span><span class="sxs-lookup"><span data-stu-id="ea7d3-168">hello following example shows how toodelete hello topic named `mytopic`:</span></span>

```python
bus_service.delete_topic('mytopic')
```

<span data-ttu-id="ea7d3-169">Als u een onderwerp verwijdert, verwijdert tevens abonnementen die zijn geregistreerd bij Hallo onderwerp.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-169">Deleting a topic also deletes any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="ea7d3-170">Abonnementen kunnen ook afzonderlijk worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-170">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="ea7d3-171">Hallo volgende code toont hoe toodelete een abonnement met de naam `HighMessages` van Hallo `mytopic` onderwerp:</span><span class="sxs-lookup"><span data-stu-id="ea7d3-171">hello following code shows how toodelete a subscription named `HighMessages` from hello `mytopic` topic:</span></span>

```python
bus_service.delete_subscription('mytopic', 'HighMessages')
```

## <a name="next-steps"></a><span data-ttu-id="ea7d3-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ea7d3-172">Next steps</span></span>
<span data-ttu-id="ea7d3-173">Nu u de basisprincipes van Service Bus-onderwerpen Hallo hebt geleerd, volgt u deze koppelingen toolearn meer.</span><span class="sxs-lookup"><span data-stu-id="ea7d3-173">Now that you've learned hello basics of Service Bus topics, follow these links toolearn more.</span></span>

* <span data-ttu-id="ea7d3-174">Zie [wachtrijen, onderwerpen en abonnementen][Queues, topics, and subscriptions].</span><span class="sxs-lookup"><span data-stu-id="ea7d3-174">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="ea7d3-175">Referentiemateriaal [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span><span class="sxs-lookup"><span data-stu-id="ea7d3-175">Reference for [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span></span>

[Azure portal]: https://portal.azure.com
[Azure Python package]: https://pypi.python.org/pypi/azure  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Service Bus quotas]: service-bus-quotas.md 
