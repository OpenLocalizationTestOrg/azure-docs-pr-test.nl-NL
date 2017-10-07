---
title: Service Bus-onderwerpen voor aaaHow toouse (Ruby) | Microsoft Docs
description: Meer informatie over hoe toouse Service Bus-onderwerpen en abonnementen in Azure. Codevoorbeelden zijn geschreven voor Ruby-toepassingen.
services: service-bus-messaging
documentationcenter: ruby
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 3ef2295e-7c5f-4c54-a13b-a69c8045d4b6
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 236d6495825e68e336c23e1b500d0764ee512e49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-ruby"></a><span data-ttu-id="ad1a6-104">Hoe toouse Service Bus-onderwerpen en abonnementen, met Ruby</span><span class="sxs-lookup"><span data-stu-id="ad1a6-104">How toouse Service Bus topics and subscriptions with Ruby</span></span>
 
[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="ad1a6-105">Dit artikel wordt beschreven hoe toouse Service Bus-onderwerpen en abonnementen van Ruby toepassingen.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-105">This article describes how toouse Service Bus topics and subscriptions from Ruby applications.</span></span> <span data-ttu-id="ad1a6-106">Hallo scenario's worden behandeld: **maken van onderwerpen en abonnementen, het maken van abonnementsfilters, het verzenden van berichten** tooa onderwerp **ontvangen van berichten van een abonnement**, en  **verwijderen van onderwerpen en abonnementen**.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-106">hello scenarios covered include **creating topics and subscriptions, creating subscription filters, sending messages** tooa topic, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="ad1a6-107">Zie voor meer informatie over onderwerpen en abonnementen Hallo [Vervolgstappen](#next-steps) sectie.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-107">For more information on topics and subscriptions, see hello [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

[!INCLUDE [service-bus-ruby-setup](../../includes/service-bus-ruby-setup.md)]

## <a name="create-a-topic"></a><span data-ttu-id="ad1a6-108">Een onderwerp maken</span><span class="sxs-lookup"><span data-stu-id="ad1a6-108">Create a topic</span></span>
<span data-ttu-id="ad1a6-109">Hallo **Azure::ServiceBusService** object kunt u toowork met onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-109">hello **Azure::ServiceBusService** object enables you toowork with topics.</span></span> <span data-ttu-id="ad1a6-110">Hallo volgende code maakt een **Azure::ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-110">hello following code creates an **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="ad1a6-111">een onderwerp toocreate gebruiken Hallo `create_topic()` methode.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-111">toocreate a topic, use hello `create_topic()` method.</span></span> <span data-ttu-id="ad1a6-112">Hallo volgende voorbeeld maakt een onderwerp of wordt afgedrukt Hallo fouten als er een.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-112">hello following example creates a topic or prints out hello errors if there are any.</span></span>

```ruby
azure_service_bus_service = Azure::ServiceBus::ServiceBusService.new(sb_host, { signer: signer})
begin
  topic = azure_service_bus_service.create_queue("test-topic")
rescue
  puts $!
end
```

<span data-ttu-id="ad1a6-113">U kunt ook doorgeven een **Azure::ServiceBus::Topic** object met extra opties waarmee u toooverride standaardinstellingen onderwerp zoals bericht tijd toolive of Maximale wachtrijgrootte.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-113">You can also pass an **Azure::ServiceBus::Topic** object with additional options, which enable you toooverride default topic settings such as message time toolive or maximum queue size.</span></span> <span data-ttu-id="ad1a6-114">Hallo volgende voorbeeld wordt getoond als de maximale wachtrij Hallo instelt omvang too5 GB en toolive too1 minuut tijd:</span><span class="sxs-lookup"><span data-stu-id="ad1a6-114">hello following example shows setting hello maximum queue size too5 GB and time toolive too1 minute:</span></span>

```ruby
topic = Azure::ServiceBus::Topic.new("test-topic")
topic.max_size_in_megabytes = 5120
topic.default_message_time_to_live = "PT1M"

topic = azure_service_bus_service.create_topic(topic)
```

## <a name="create-subscriptions"></a><span data-ttu-id="ad1a6-115">Abonnementen maken</span><span class="sxs-lookup"><span data-stu-id="ad1a6-115">Create subscriptions</span></span>
<span data-ttu-id="ad1a6-116">Onderwerpabonnementen worden ook gemaakt met de Hallo **Azure::ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-116">Topic subscriptions are also created with hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="ad1a6-117">Abonnementen kunnen worden genoemd en een optioneel filter waarmee Hallo verzameling berichten dat de virtuele wachtrij van het abonnement toohello wordt beperkt.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-117">Subscriptions are named and can have an optional filter that restricts hello set of messages delivered toohello subscription's virtual queue.</span></span>

<span data-ttu-id="ad1a6-118">Abonnementen worden permanent en tooexist zal worden voortgezet totdat beide ze of hello onderwerp ze zijn gekoppeld, worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-118">Subscriptions are persistent and will continue tooexist until either they, or hello topic they are associated with, are deleted.</span></span> <span data-ttu-id="ad1a6-119">Als uw toepassing bevat de logica toocreate een abonnement, moet eerst controleren als Hallo abonnement bestaat al met Hallo getSubscription methode.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-119">If your application contains logic toocreate a subscription, it should first check if hello subscription already exists by using hello getSubscription method.</span></span>

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a><span data-ttu-id="ad1a6-120">Een abonnement maken met de Hallo standaardfilter (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="ad1a6-120">Create a subscription with hello default (MatchAll) filter</span></span>
<span data-ttu-id="ad1a6-121">Hallo **MatchAll** filter is Hallo standaardfilter dat wordt gebruikt als geen filter is opgegeven als een nieuw abonnement wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-121">hello **MatchAll** filter is hello default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="ad1a6-122">Wanneer Hallo **MatchAll** filter wordt gebruikt, worden alle berichten gepubliceerde toohello onderwerp in virtuele wachtrij van Hallo abonnement geplaatst.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-122">When hello **MatchAll** filter is used, all messages published toohello topic are placed in hello subscription's virtual queue.</span></span> <span data-ttu-id="ad1a6-123">Hallo volgende voorbeeld wordt een abonnement genaamd 'all '-berichten en gebruikt standaard Hallo **MatchAll** filter.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-123">hello following example creates a subscription named "all-messages" and uses hello default **MatchAll** filter.</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "all-messages")
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="ad1a6-124">Abonnementen met filters maken</span><span class="sxs-lookup"><span data-stu-id="ad1a6-124">Create subscriptions with filters</span></span>
<span data-ttu-id="ad1a6-125">U kunt ook filters waarmee u welke berichten verzonden tooa onderwerp weergegeven binnen een bepaald abonnement toospecify definiëren.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-125">You can also define filters that enable you toospecify which messages sent tooa topic should show up within a specific subscription.</span></span>

<span data-ttu-id="ad1a6-126">Hallo meest flexibele type filter dat wordt ondersteund door abonnementen is Hallo **Azure::ServiceBus::SqlFilter**, waarmee een subset van SQL92 wordt geïmplementeerd implementeert.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-126">hello most flexible type of filter supported by subscriptions is hello **Azure::ServiceBus::SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="ad1a6-127">SQL-filters worden uitgevoerd op Hallo eigenschappen van Hallo-berichten die gepubliceerd toohello onderwerp zijn.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-127">SQL filters operate on hello properties of hello messages that are published toohello topic.</span></span> <span data-ttu-id="ad1a6-128">Bekijk voor meer informatie over Hallo expressies die kunnen worden gebruikt met een SQL-filter Hallo [SqlFilter](service-bus-messaging-sql-filter.md) syntaxis.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-128">For more details about hello expressions that can be used with a SQL filter, review hello [SqlFilter](service-bus-messaging-sql-filter.md) syntax.</span></span>

<span data-ttu-id="ad1a6-129">U kunt filters tooa abonnement kunt toevoegen met behulp van Hallo `create_rule()` methode Hallo **Azure::ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-129">You can add filters tooa subscription by using hello `create_rule()` method of hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="ad1a6-130">Deze methode kunt u tooadd nieuwe filters tooan bestaande abonnement.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-130">This method enables you tooadd new filters tooan existing subscription.</span></span>

<span data-ttu-id="ad1a6-131">Aangezien het standaardfilter hello wordt automatisch toegepast tooall nieuwe abonnementen, moet u eerst het standaardfilter Hallo verwijderen, of Hallo **MatchAll** overschrijft alle andere filters die u kunt opgeven.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-131">Since hello default filter is applied automatically tooall new subscriptions, you must first remove hello default filter, or hello **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="ad1a6-132">U kunt de standaardregel Hallo verwijderen via Hallo `delete_rule()` methode op Hallo **Azure::ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-132">You can remove hello default rule by using hello `delete_rule()` method on hello **Azure::ServiceBusService** object.</span></span>

<span data-ttu-id="ad1a6-133">Hallo volgende voorbeeld maakt u een abonnement met de naam 'hoog '-berichten met een **Azure::ServiceBus::SqlFilter** die alleen berichten selecteert die een aangepaste `message_number` eigenschap groter is dan 3:</span><span class="sxs-lookup"><span data-stu-id="ad1a6-133">hello following example creates a subscription named "high-messages" with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a custom `message_number` property greater than 3:</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "high-messages")
azure_service_bus_service.delete_rule("test-topic", "high-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("high-messages-rule")
rule.topic = "test-topic"
rule.subscription = "high-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number > 3" })
rule = azure_service_bus_service.create_rule(rule)
```

<span data-ttu-id="ad1a6-134">Op deze manier hello volgende voorbeeld maakt u een abonnement met de naam `low-messages` met een **Azure::ServiceBus::SqlFilter** die alleen berichten selecteert die een `message_number` eigenschap kleiner dan of gelijk too3:</span><span class="sxs-lookup"><span data-stu-id="ad1a6-134">Similarly, hello following example creates a subscription named `low-messages` with an **Azure::ServiceBus::SqlFilter** that only selects messages that have a `message_number` property less than or equal too3:</span></span>

```ruby
subscription = azure_service_bus_service.create_subscription("test-topic", "low-messages")
azure_service_bus_service.delete_rule("test-topic", "low-messages", "$Default")

rule = Azure::ServiceBus::Rule.new("low-messages-rule")
rule.topic = "test-topic"
rule.subscription = "low-messages"
rule.filter = Azure::ServiceBus::SqlFilter.new({
  :sql_expression => "message_number <= 3" })
rule = azure_service_bus_service.create_rule(rule)
```

<span data-ttu-id="ad1a6-135">Wanneer een bericht nu te verzonden`test-topic`, kan altijd worden geleverd tooreceivers geabonneerd toohello `all-messages` onderwerpabonnement en selectief bezorgd tooreceivers geabonneerd toohello `high-messages` en `low-messages` onderwerp abonnementen ( afhankelijk van de inhoud van de Hallo-bericht).</span><span class="sxs-lookup"><span data-stu-id="ad1a6-135">When a message is now sent too`test-topic`, it is always be delivered tooreceivers subscribed toohello `all-messages` topic subscription, and selectively delivered tooreceivers subscribed toohello `high-messages` and `low-messages` topic subscriptions (depending upon hello message content).</span></span>

## <a name="send-messages-tooa-topic"></a><span data-ttu-id="ad1a6-136">Verzenden van berichten tooa onderwerp</span><span class="sxs-lookup"><span data-stu-id="ad1a6-136">Send messages tooa topic</span></span>
<span data-ttu-id="ad1a6-137">een bericht tooa Service Bus-onderwerp toosend, uw toepassing moet gebruiken Hallo `send_topic_message()` methode op Hallo **Azure::ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-137">toosend a message tooa Service Bus topic, your application must use hello `send_topic_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="ad1a6-138">Berichten verzonden tooService Bus-onderwerpen, zijn exemplaren van Hallo **Azure::ServiceBus::BrokeredMessage** objecten.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-138">Messages sent tooService Bus topics are instances of hello **Azure::ServiceBus::BrokeredMessage** objects.</span></span> <span data-ttu-id="ad1a6-139">**Azure::ServiceBus::BrokeredMessage** objecten hebben een aantal standaardeigenschappen (zoals `label` en `time_to_live`), een woordenlijst die wordt gebruikt toohold aangepaste toepassingsspecifieke eigenschappen en een hoofdtekst met tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-139">**Azure::ServiceBus::BrokeredMessage** objects have a set of standard properties (such as `label` and `time_to_live`), a dictionary that is used toohold custom application-specific properties, and a body of string data.</span></span> <span data-ttu-id="ad1a6-140">Een toepassing hello hoofdtekst van het Hallo-bericht worden ingesteld door een string-waarde toohello `send_topic_message()` methode en alle vereiste standaardeigenschappen standaardwaarden worden ingevuld.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-140">An application can set hello body of hello message by passing a string value toohello `send_topic_message()` method and any required standard properties will be populated by default values.</span></span>

<span data-ttu-id="ad1a6-141">Hallo volgende voorbeeld toont hoe vijf toosend test berichten te`test-topic`.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-141">hello following example demonstrates how toosend five test messages too`test-topic`.</span></span> <span data-ttu-id="ad1a6-142">Houd er rekening mee dat Hallo `message_number` waarde van de aangepaste eigenschap van elk bericht varieert op Hallo herhaling van Hallo lus (deze bepaalt welke abonnement ontvangt):</span><span class="sxs-lookup"><span data-stu-id="ad1a6-142">Note that hello `message_number` custom property value of each message varies on hello iteration of hello loop (this determines which subscription receives it):</span></span>

```ruby
5.times do |i|
  message = Azure::ServiceBus::BrokeredMessage.new("test message " + i,
    { :message_number => i })
  azure_service_bus_service.send_topic_message("test-topic", message)
end
```

<span data-ttu-id="ad1a6-143">Service Bus-onderwerpen ondersteunen een maximale berichtgrootte van 256 KB in Hallo [standaardcategorie](service-bus-premium-messaging.md) en 1 MB in Hallo [Premium-laag](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="ad1a6-143">Service Bus topics support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="ad1a6-144">Hallo-kop, die standaard Hallo- en aangepaste toepassingseigenschappen bevat, kan een maximale grootte van 64 KB hebben.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-144">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="ad1a6-145">Er is geen limiet voor het aantal berichten in een onderwerp hello, maar er is een limiet voor de totale grootte van berichten in een onderwerp Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-145">There is no limit on hello number of messages held in a topic but there is a cap on hello total size of hello messages held by a topic.</span></span> <span data-ttu-id="ad1a6-146">De grootte van het onderwerp wordt gedefinieerd tijdens het maken, met een bovengrens van 5 GB.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-146">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="ad1a6-147">Berichten ontvangen van een abonnement</span><span class="sxs-lookup"><span data-stu-id="ad1a6-147">Receive messages from a subscription</span></span>
<span data-ttu-id="ad1a6-148">Berichten worden ontvangen van een abonnement met Hallo `receive_subscription_message()` methode op Hallo **Azure::ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-148">Messages are received from a subscription using hello `receive_subscription_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="ad1a6-149">Standaard berichten zijn read(peak) en zonder het te verwijderen uit het Hallo-abonnement is vergrendeld.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-149">By default, messages are read(peak) and locked without deleting it from hello subscription.</span></span> <span data-ttu-id="ad1a6-150">U kunt lezen en het Hallo-bericht verwijderen uit abonnement Hallo door Hallo instelling `peek_lock` te optie**false**.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-150">You can read and delete hello message from hello subscription by setting hello `peek_lock` option too**false**.</span></span>

<span data-ttu-id="ad1a6-151">Hallo standaardgedrag maakt Hallo lezen en verwijderen van een bewerking met twee fasen, waardoor dit ook mogelijk toosupport toepassingen die geen ontbrekende berichten kunnen tolereren.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-151">hello default behavior makes hello reading and deleting a two-stage operation, which also makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="ad1a6-152">Wanneer Service Bus een aanvraag ontvangt, zoeken naar het volgende bericht toobe Hallo verbruikt, wordt vergrendeld tooprevent andere consumenten het ontvangen en retourneert vervolgens toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-152">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="ad1a6-153">Nadat de toepassing hello klaar is met verwerking van het Hallo-bericht (of veilig heeft opgeslagen voor toekomstige verwerking), is de tweede fase Hallo Hallo voltooid proces ontvangen door het aanroepen van `delete_subscription_message()` methode en het Hallo-bericht toobe verwijderd als een parameter geven.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-153">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling `delete_subscription_message()` method and providing hello message toobe deleted as a parameter.</span></span> <span data-ttu-id="ad1a6-154">Hallo `delete_subscription_message()` methode wordt het Hallo-bericht als verbruikt markeren en verwijderen uit het Hallo-abonnement.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-154">hello `delete_subscription_message()` method will mark hello message as being consumed and remove it from hello subscription.</span></span>

<span data-ttu-id="ad1a6-155">Als hello `:peek_lock` parameter is ingesteld, te**false**, lezen en verwijderen van het Hallo-bericht, wordt het Hallo eenvoudigste model en werkt het beste voor scenario's waarin een toepassing kan tolereren niet verwerken van een bericht in de gebeurtenis Hallo van een is mislukt.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-155">If hello `:peek_lock` parameter is set too**false**, reading and deleting hello message becomes hello simplest model, and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="ad1a6-156">toounderstand dit, Neem bijvoorbeeld een scenario in welke problemen van de consument Hallo Hallo aanvraag ontvangen en vervolgens vastloopt voordat het wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-156">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span> <span data-ttu-id="ad1a6-157">Omdat Service Bus heeft gemarkeerd als verbruikt, vervolgens wanneer Hallo toepassing opnieuw wordt opgestart en verbruik van berichten opnieuw begint het Hallo-bericht, ontbreekt het Hallo-bericht dat was voorafgaande toohello crash verbruikt.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-157">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="ad1a6-158">Hallo volgende voorbeeld laat zien hoe berichten kunnen worden ontvangen en verwerkt met behulp `receive_subscription_message()`.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-158">hello following example demonstrates how messages can be received and processed using `receive_subscription_message()`.</span></span> <span data-ttu-id="ad1a6-159">Hallo voorbeeld eerst ontvangt en verwijdert van een bericht van Hallo `low-messages` abonnement via `:peek_lock` instellen te**false**, en vervolgens wordt een ander bericht van Hallo ontvangen `high-messages` en vervolgens verwijdert het bericht met Hallo `delete_subscription_message()`:</span><span class="sxs-lookup"><span data-stu-id="ad1a6-159">hello example first receives and deletes a message from hello `low-messages` subscription by using `:peek_lock` set too**false**, then it receives another message from hello `high-messages` and then deletes hello message using `delete_subscription_message()`:</span></span>

```ruby
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "low-messages", { :peek_lock => false })
message = azure_service_bus_service.receive_subscription_message(
  "test-topic", "high-messages")
azure_service_bus_service.delete_subscription_message(message)
```

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="ad1a6-160">Hoe toohandle toepassing is vastgelopen en onleesbare berichten</span><span class="sxs-lookup"><span data-stu-id="ad1a6-160">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="ad1a6-161">Service Bus biedt functionaliteit toohelp die u netjes te herstellen bij fouten in uw toepassing of problemen bij het verwerken van een bericht.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-161">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="ad1a6-162">Als een ontvangende toepassing niet kan tooprocess hello bericht voor een bepaalde reden en vervolgens kan worden aangeroepen Hallo `unlock_subscription_message()` methode op Hallo **Azure::ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-162">If a receiver application is unable tooprocess hello message for some reason, then it can call hello `unlock_subscription_message()` method on hello **Azure::ServiceBusService** object.</span></span> <span data-ttu-id="ad1a6-163">Deze tot gevolg dat het Service Bus toounlock Hallo binnen abonnement Hallo-bericht, waardoor het beschikbaar toobe ontvangen, Hallo ofwel door dezelfde toepassing of door een andere consumerende toepassing verbruikt.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-163">This causes Service Bus toounlock hello message within hello subscription and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="ad1a6-164">Daarnaast is er een time-out gekoppeld aan een bericht in het Hallo-abonnement is vergrendeld en als Hallo toepassing tooprocess Hallo-bericht voordat mislukt Hallo vergrendelingstime-out verloopt (bijvoorbeeld als Hallo toepassing vastloopt), en vervolgens de Service Bus wordt ontgrendeld Hallo-bericht automatisch en wordt het beschikbaar toobe opnieuw ontvangen.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-164">There is also a timeout associated with a message locked within hello subscription, and if hello application fails tooprocess hello message before hello lock timeout expires (for example, if hello application crashes), then Service Bus will unlock hello message automatically and make it available toobe received again.</span></span>

<span data-ttu-id="ad1a6-165">In Hallo gebeurtenis die toepassing hello vastgelopen na het verwerken van het Hallo-bericht, maar voordat u Hallo `delete_subscription_message()` methode wordt aangeroepen en vervolgens het Hallo-bericht is opnieuw bezorgd toohello toepassing opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-165">In hello event that hello application crashes after processing hello message but before hello `delete_subscription_message()` method is called, then hello message is redelivered toohello application when it restarts.</span></span> <span data-ttu-id="ad1a6-166">Dit wordt vaak genoemd *tenminste eenmaal verwerken*; dat wil zeggen, elk bericht ten minste één keer wordt verwerkt maar in bepaalde situaties Hallo hetzelfde bericht opnieuw kan worden bezorgd.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-166">This is often called *At Least Once Processing*; that is, each message will be processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="ad1a6-167">Als Hallo scenario kan geen dubbele verwerking tolereren, moeten toepassingsontwikkelaars levering van aanvullende logica tootheir toepassing toohandle dubbele berichten toevoegen.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-167">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="ad1a6-168">Deze logica wordt vaak bereikt met behulp van Hallo `message_id` eigenschap van Hallo-bericht dat gelijk bij meerdere bezorgingspogingen blijft.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-168">This logic is often achieved using hello `message_id` property of hello message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="ad1a6-169">Onderwerpen en abonnementen verwijderen</span><span class="sxs-lookup"><span data-stu-id="ad1a6-169">Delete topics and subscriptions</span></span>
<span data-ttu-id="ad1a6-170">Onderwerpen en abonnementen worden permanent en expliciet moet worden verwijderd via Hallo [Azure-portal] [ Azure portal] of via een programma.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-170">Topics and subscriptions are persistent, and must be explicitly deleted either through hello [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="ad1a6-171">Hallo in het volgende voorbeeld laat zien hoe toodelete Hallo onderwerp met de naam `test-topic`.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-171">hello example below demonstrates how toodelete hello topic named `test-topic`.</span></span>

```ruby
azure_service_bus_service.delete_topic("test-topic")
```

<span data-ttu-id="ad1a6-172">Als u een onderwerp verwijdert, verwijdert tevens abonnementen die zijn geregistreerd bij Hallo onderwerp.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-172">Deleting a topic also deletes any subscriptions that are registered with hello topic.</span></span> <span data-ttu-id="ad1a6-173">Abonnementen kunnen ook afzonderlijk worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-173">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="ad1a6-174">Hallo volgende code laat zien hoe toodelete Hallo abonnement met de naam `high-messages` van Hallo `test-topic` onderwerp:</span><span class="sxs-lookup"><span data-stu-id="ad1a6-174">hello following code demonstrates how toodelete hello subscription named `high-messages` from hello `test-topic` topic:</span></span>

```ruby
azure_service_bus_service.delete_subscription("test-topic", "high-messages")
```

## <a name="next-steps"></a><span data-ttu-id="ad1a6-175">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ad1a6-175">Next steps</span></span>
<span data-ttu-id="ad1a6-176">Nu u de basisprincipes van Service Bus-onderwerpen Hallo hebt geleerd, volgt u deze koppelingen toolearn meer.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-176">Now that you've learned hello basics of Service Bus topics, follow these links toolearn more.</span></span>

* <span data-ttu-id="ad1a6-177">Zie [wachtrijen, onderwerpen en abonnementen](service-bus-queues-topics-subscriptions.md).</span><span class="sxs-lookup"><span data-stu-id="ad1a6-177">See [Queues, topics, and subscriptions](service-bus-queues-topics-subscriptions.md).</span></span>
* <span data-ttu-id="ad1a6-178">API-naslaginformatie voor [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).</span><span class="sxs-lookup"><span data-stu-id="ad1a6-178">API reference for [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter#microsoft_servicebus_messaging_sqlfilter).</span></span>
* <span data-ttu-id="ad1a6-179">Ga naar Hallo [Azure SDK voor Ruby](https://github.com/Azure/azure-sdk-for-ruby) opslagplaats op GitHub.</span><span class="sxs-lookup"><span data-stu-id="ad1a6-179">Visit hello [Azure SDK for Ruby](https://github.com/Azure/azure-sdk-for-ruby) repository on GitHub.</span></span>

[Azure portal]: https://portal.azure.com
