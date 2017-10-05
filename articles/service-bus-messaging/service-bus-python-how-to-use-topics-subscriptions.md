---
title: Azure Service Bus-onderwerpen gebruiken met Python | Microsoft Docs
description: Informatie over het gebruik van Azure Service Bus-onderwerpen en abonnementen van Python.
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
ms.openlocfilehash: 15269f9728e9dc45e6436e53b1859f76d4a7a0c9
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-topics-and-subscriptions-with-python"></a><span data-ttu-id="b960a-103">Service Bus-onderwerpen en abonnementen gebruiken met Python</span><span class="sxs-lookup"><span data-stu-id="b960a-103">How to use Service Bus topics and subscriptions with Python</span></span>

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

<span data-ttu-id="b960a-104">In dit artikel wordt beschreven hoe u Service Bus-onderwerpen en -abonnementen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b960a-104">This article describes how to use Service Bus topics and subscriptions.</span></span> <span data-ttu-id="b960a-105">De voorbeelden zijn geschreven in Python en gebruik de [Azure Python SDK-pakket][Azure Python package].</span><span class="sxs-lookup"><span data-stu-id="b960a-105">The samples are written in Python and use the [Azure Python SDK package][Azure Python package].</span></span> <span data-ttu-id="b960a-106">De scenario's worden behandeld: **maken van onderwerpen en abonnementen**, **maken van abonnementsfilters**, **verzenden van berichten naar een onderwerp**, **ontvangen van berichten van een abonnement**, en **verwijderen van onderwerpen en abonnementen**.</span><span class="sxs-lookup"><span data-stu-id="b960a-106">The scenarios covered include **creating topics and subscriptions**, **creating subscription filters**, **sending messages to a topic**, **receiving messages from a subscription**, and **deleting topics and subscriptions**.</span></span> <span data-ttu-id="b960a-107">Zie voor meer informatie over onderwerpen en abonnementen, de [Vervolgstappen](#next-steps) sectie.</span><span class="sxs-lookup"><span data-stu-id="b960a-107">For more information about topics and subscriptions, see the [Next Steps](#next-steps) section.</span></span>

[!INCLUDE [howto-service-bus-topics](../../includes/howto-service-bus-topics.md)]

> [!NOTE] 
> <span data-ttu-id="b960a-108">Als u nodig hebt om Python te installeren of de [Azure Python-pakket][Azure Python package], Zie de [Python installatiehandleiding](../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="b960a-108">If you need to install Python or the [Azure Python package][Azure Python package], see the [Python Installation Guide](../python-how-to-install.md).</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="b960a-109">Een onderwerp maken</span><span class="sxs-lookup"><span data-stu-id="b960a-109">Create a topic</span></span>
<span data-ttu-id="b960a-110">De **ServiceBusService** object kunt u werken met onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="b960a-110">The **ServiceBusService** object enables you to work with topics.</span></span> <span data-ttu-id="b960a-111">Voeg de volgende boven aan elk Python-bestand waarin u wilt programmatisch toegang biedt tot de Service Bus:</span><span class="sxs-lookup"><span data-stu-id="b960a-111">Add the following near the top of any Python file in which you wish to programmatically access Service Bus:</span></span>

```python
from azure.servicebus import ServiceBusService, Message, Topic, Rule, DEFAULT_RULE_NAME
```

<span data-ttu-id="b960a-112">De volgende code maakt een **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="b960a-112">The following code creates a **ServiceBusService** object.</span></span> <span data-ttu-id="b960a-113">Vervang `mynamespace`, `sharedaccesskeyname`, en `sharedaccesskey` met uw werkelijke naamruimte Shared Access Signature (SAS) sleutelwaarde naam en een sleutel.</span><span class="sxs-lookup"><span data-stu-id="b960a-113">Replace `mynamespace`, `sharedaccesskeyname`, and `sharedaccesskey` with your actual namespace, Shared Access Signature (SAS) key name, and key value.</span></span>

```python
bus_service = ServiceBusService(
    service_namespace='mynamespace',
    shared_access_key_name='sharedaccesskeyname',
    shared_access_key_value='sharedaccesskey')
```

<span data-ttu-id="b960a-114">U kunt verkrijgen van de waarden voor de naam van de SAS-sleutel en waarde van de [Azure-portal][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="b960a-114">You can obtain the values for the SAS key name and value from the [Azure portal][Azure portal].</span></span>

```python
bus_service.create_topic('mytopic')
```

<span data-ttu-id="b960a-115">De `create_topic` methode biedt ook ondersteuning voor extra opties waarmee u kunt de standaardinstellingen voor onderwerp zoals bericht of grootte van het maximum aantal onderwerp negeren.</span><span class="sxs-lookup"><span data-stu-id="b960a-115">The `create_topic` method also supports additional options, which enable you to override default topic settings such as message time to live or maximum topic size.</span></span> <span data-ttu-id="b960a-116">Het volgende voorbeeld wordt de grootte van het maximum aantal onderwerp 5 GB, en een tijdstip voor live (TTL)-waarde van 1 minuut:</span><span class="sxs-lookup"><span data-stu-id="b960a-116">The following example sets the maximum topic size to 5 GB, and a time to live (TTL) value of 1 minute:</span></span>

```python
topic_options = Topic()
topic_options.max_size_in_megabytes = '5120'
topic_options.default_message_time_to_live = 'PT1M'

bus_service.create_topic('mytopic', topic_options)
```

## <a name="create-subscriptions"></a><span data-ttu-id="b960a-117">Abonnementen maken</span><span class="sxs-lookup"><span data-stu-id="b960a-117">Create subscriptions</span></span>
<span data-ttu-id="b960a-118">Abonnementen op onderwerpen ook worden gemaakt met de **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="b960a-118">Subscriptions to topics are also created with the **ServiceBusService** object.</span></span> <span data-ttu-id="b960a-119">Abonnementen kunnen worden genoemd en een optioneel filter waarmee de verzameling berichten in de virtuele wachtrij van het abonnement wordt beperkt.</span><span class="sxs-lookup"><span data-stu-id="b960a-119">Subscriptions are named and can have an optional filter that restricts the set of messages delivered to the subscription's virtual queue.</span></span>

> [!NOTE]
> <span data-ttu-id="b960a-120">Abonnementen worden permanent en blijft bestaan totdat ze, of het onderwerp waarop ze zijn aangemeld, worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="b960a-120">Subscriptions are persistent and will continue to exist until either they, or the topic to which they are subscribed, are deleted.</span></span>
> 
> 

### <a name="create-a-subscription-with-the-default-matchall-filter"></a><span data-ttu-id="b960a-121">Een abonnement maken met het standaardfilter (MatchAll)</span><span class="sxs-lookup"><span data-stu-id="b960a-121">Create a subscription with the default (MatchAll) filter</span></span>
<span data-ttu-id="b960a-122">Het **MatchAll**-filter is het standaardfilter dat wordt gebruikt als er bij het maken van een nieuw abonnement geen filter is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="b960a-122">The **MatchAll** filter is the default filter that is used if no filter is specified when a new subscription is created.</span></span> <span data-ttu-id="b960a-123">Wanneer de **MatchAll** filter wordt gebruikt, worden alle berichten die zijn gepubliceerd naar het onderwerp in de virtuele wachtrij van het abonnement geplaatst.</span><span class="sxs-lookup"><span data-stu-id="b960a-123">When the **MatchAll** filter is used, all messages published to the topic are placed in the subscription's virtual queue.</span></span> <span data-ttu-id="b960a-124">Het volgende voorbeeld wordt een abonnement genaamd `AllMessages` en gebruikt de standaardinstallatielocatie **MatchAll** filter.</span><span class="sxs-lookup"><span data-stu-id="b960a-124">The following example creates a subscription named `AllMessages` and uses the default **MatchAll** filter.</span></span>

```python
bus_service.create_subscription('mytopic', 'AllMessages')
```

### <a name="create-subscriptions-with-filters"></a><span data-ttu-id="b960a-125">Abonnementen met filters maken</span><span class="sxs-lookup"><span data-stu-id="b960a-125">Create subscriptions with filters</span></span>
<span data-ttu-id="b960a-126">Ook kunt u filters waarmee u kunt opgeven welke berichten die worden verzonden naar een onderwerp weergegeven binnen een bepaald onderwerpabonnement.</span><span class="sxs-lookup"><span data-stu-id="b960a-126">You can also define filters that enable you to specify which messages sent to a topic should show up within a specific topic subscription.</span></span>

<span data-ttu-id="b960a-127">Het meest flexibele type filter dat wordt ondersteund door abonnementen is een **SqlFilter**, waarmee een subset van SQL92 wordt geïmplementeerd implementeert.</span><span class="sxs-lookup"><span data-stu-id="b960a-127">The most flexible type of filter supported by subscriptions is a **SqlFilter**, which implements a subset of SQL92.</span></span> <span data-ttu-id="b960a-128">SQL-filters worden uitgevoerd voor de eigenschappen van de berichten die worden gepubliceerd naar het onderwerp.</span><span class="sxs-lookup"><span data-stu-id="b960a-128">SQL filters operate on the properties of the messages that are published to the topic.</span></span> <span data-ttu-id="b960a-129">Zie de [SqlFilter.SqlExpression][SqlFilter.SqlExpression]-syntaxis voor meer informatie over de expressies die kunnen worden gebruikt met een SQL-filter.</span><span class="sxs-lookup"><span data-stu-id="b960a-129">For more information about the expressions that can be used with a SQL filter, see the [SqlFilter.SqlExpression][SqlFilter.SqlExpression] syntax.</span></span>

<span data-ttu-id="b960a-130">U kunt filters toevoegen aan een abonnement met behulp van de **maken\_regel** methode van de **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="b960a-130">You can add filters to a subscription by using the **create\_rule** method of the **ServiceBusService** object.</span></span> <span data-ttu-id="b960a-131">Deze methode kunt u nieuwe filters toevoegen aan een bestaand abonnement.</span><span class="sxs-lookup"><span data-stu-id="b960a-131">This method allows you to add new filters to an existing subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="b960a-132">Omdat het standaardfilter automatisch op alle nieuwe abonnementen toegepast wordt, moet u eerst het standaardfilter verwijderen of de **MatchAll** overschrijft alle andere filters die u kunt opgeven.</span><span class="sxs-lookup"><span data-stu-id="b960a-132">Because the default filter is applied automatically to all new subscriptions, you must first remove the default filter or the **MatchAll** will override any other filters you may specify.</span></span> <span data-ttu-id="b960a-133">U kunt de standaardregel verwijderen met behulp van de `delete_rule` methode van de **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="b960a-133">You can remove the default rule by using the `delete_rule` method of the **ServiceBusService** object.</span></span>
> 
> 

<span data-ttu-id="b960a-134">Het volgende voorbeeld wordt een abonnement genaamd `HighMessages` met een **SqlFilter** die alleen berichten selecteert die een aangepaste `messagenumber` eigenschap groter is dan 3:</span><span class="sxs-lookup"><span data-stu-id="b960a-134">The following example creates a subscription named `HighMessages` with a **SqlFilter** that only selects messages that have a custom `messagenumber` property greater than 3:</span></span>

```python
bus_service.create_subscription('mytopic', 'HighMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber > 3'

bus_service.create_rule('mytopic', 'HighMessages', 'HighMessageFilter', rule)
bus_service.delete_rule('mytopic', 'HighMessages', DEFAULT_RULE_NAME)
```

<span data-ttu-id="b960a-135">Op deze manier in het volgende voorbeeld wordt een abonnement genaamd `LowMessages` met een **SqlFilter** die alleen berichten selecteert die een `messagenumber` eigenschap kleiner dan of gelijk aan 3:</span><span class="sxs-lookup"><span data-stu-id="b960a-135">Similarly, the following example creates a subscription named `LowMessages` with a **SqlFilter** that only selects messages that have a `messagenumber` property less than or equal to 3:</span></span>

```python
bus_service.create_subscription('mytopic', 'LowMessages')

rule = Rule()
rule.filter_type = 'SqlFilter'
rule.filter_expression = 'messagenumber <= 3'

bus_service.create_rule('mytopic', 'LowMessages', 'LowMessageFilter', rule)
bus_service.delete_rule('mytopic', 'LowMessages', DEFAULT_RULE_NAME)
```

<span data-ttu-id="b960a-136">Nu wanneer een bericht verzonden naar `mytopic` wordt het altijd bezorgd bij ontvangers die zijn geabonneerd op de **AllMessages** onderwerpabonnement en selectief bezorgd bij ontvangers die zijn geabonneerd op de **HighMessages** en **LowMessages** onderwerpabonnementen (afhankelijk van de inhoud van het bericht).</span><span class="sxs-lookup"><span data-stu-id="b960a-136">Now, when a message is sent to `mytopic` it is always delivered to receivers subscribed to the **AllMessages** topic subscription, and selectively delivered to receivers subscribed to the **HighMessages** and **LowMessages** topic subscriptions (depending on the message content).</span></span>

## <a name="send-messages-to-a-topic"></a><span data-ttu-id="b960a-137">Berichten verzenden naar een onderwerp</span><span class="sxs-lookup"><span data-stu-id="b960a-137">Send messages to a topic</span></span>
<span data-ttu-id="b960a-138">Als u wilt een bericht verzendt naar een Service Bus-onderwerp, de toepassing moet gebruiken de `send_topic_message` methode van de **ServiceBusService** object.</span><span class="sxs-lookup"><span data-stu-id="b960a-138">To send a message to a Service Bus topic, your application must use the `send_topic_message` method of the **ServiceBusService** object.</span></span>

<span data-ttu-id="b960a-139">Het volgende voorbeeld toont hoe vijf testberichten naar verzendt `mytopic`.</span><span class="sxs-lookup"><span data-stu-id="b960a-139">The following example demonstrates how to send five test messages to `mytopic`.</span></span> <span data-ttu-id="b960a-140">Houd er rekening mee dat de `messagenumber` eigenschapswaarde van elk bericht varieert op de herhaling van de lus (deze bepaalt welke abonnementen ontvangen):</span><span class="sxs-lookup"><span data-stu-id="b960a-140">Note that the `messagenumber` property value of each message varies on the iteration of the loop (this determines which subscriptions receive it):</span></span>

```python
for i in range(5):
    msg = Message('Msg {0}'.format(i).encode('utf-8'), custom_properties={'messagenumber':i})
    bus_service.send_topic_message('mytopic', msg)
```

<span data-ttu-id="b960a-141">Service Bus-onderwerpen ondersteunen een maximale grootte van 256 kB in de [Standard-laag](service-bus-premium-messaging.md) en 1 MB in de [Premium-laag](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="b960a-141">Service Bus topics support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="b960a-142">De koptekst, die de standaard- en aangepaste toepassingseigenschappen bevat, kan maximaal 64 kB groot zijn.</span><span class="sxs-lookup"><span data-stu-id="b960a-142">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="b960a-143">Er is geen limiet voor het aantal berichten in een onderwerp, maar er is een limiet voor de totale grootte van de berichten in een onderwerp.</span><span class="sxs-lookup"><span data-stu-id="b960a-143">There is no limit on the number of messages held in a topic but there is a cap on the total size of the messages held by a topic.</span></span> <span data-ttu-id="b960a-144">De grootte van het onderwerp wordt gedefinieerd tijdens het maken, met een bovengrens van 5 GB.</span><span class="sxs-lookup"><span data-stu-id="b960a-144">This topic size is defined at creation time, with an upper limit of 5 GB.</span></span> <span data-ttu-id="b960a-145">Zie voor meer informatie over quota [Service Bus-quota][Service Bus quotas].</span><span class="sxs-lookup"><span data-stu-id="b960a-145">For more information about quotas, see [Service Bus quotas][Service Bus quotas].</span></span>

## <a name="receive-messages-from-a-subscription"></a><span data-ttu-id="b960a-146">Berichten ontvangen van een abonnement</span><span class="sxs-lookup"><span data-stu-id="b960a-146">Receive messages from a subscription</span></span>
<span data-ttu-id="b960a-147">Berichten worden ontvangen van een abonnement met de `receive_subscription_message` methode op de **ServiceBusService** object:</span><span class="sxs-lookup"><span data-stu-id="b960a-147">Messages are received from a subscription using the `receive_subscription_message` method on the **ServiceBusService** object:</span></span>

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=False)
print(msg.body)
```

<span data-ttu-id="b960a-148">Berichten van het abonnement verwijderd als ze worden gelezen wanneer de parameter `peek_lock` is ingesteld op **False**.</span><span class="sxs-lookup"><span data-stu-id="b960a-148">Messages are deleted from the subscription as they are read when the parameter `peek_lock` is set to **False**.</span></span> <span data-ttu-id="b960a-149">U kunt lezen (peek) en het bericht zonder het te verwijderen uit de wachtrij door de parameter vergrendelen `peek_lock` naar **True**.</span><span class="sxs-lookup"><span data-stu-id="b960a-149">You can read (peek) and lock the message without deleting it from the queue by setting the parameter `peek_lock` to **True**.</span></span>

<span data-ttu-id="b960a-150">Het gedrag van lezen van en het bericht is verwijderd als onderdeel van de bewerking receive is het eenvoudigste model en werkt het beste voor scenario's waarin een toepassing kan tolereren niet verwerken van een bericht bij een storing.</span><span class="sxs-lookup"><span data-stu-id="b960a-150">The behavior of reading and deleting the message as part of the receive operation is the simplest model, and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="b960a-151">Neem bijvoorbeeld een scenario waarin de consument de ontvangstaanvraag uitgeeft en het systeem vervolgens vastloopt voordat de aanvraag wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="b960a-151">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span> <span data-ttu-id="b960a-152">Omdat Service Bus het bericht als verbruikt heeft gemarkeerd, klikt u vervolgens wanneer de toepassing opnieuw wordt opgestart en het verbruik van berichten opnieuw begint, ontbreekt het bericht dat voor het vastlopen is verbruikt.</span><span class="sxs-lookup"><span data-stu-id="b960a-152">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="b960a-153">Als de `peek_lock` parameter is ingesteld op **True**, wordt het ontvangen, wordt een bewerking met twee fasen, waardoor er mogelijk worden ondersteuning voor toepassingen die geen ontbrekende berichten kunnen tolereren.</span><span class="sxs-lookup"><span data-stu-id="b960a-153">If the `peek_lock` parameter is set to **True**, the receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="b960a-154">Als Service Bus een aanvraag ontvangt, wordt het volgende te verbruiken bericht gevonden, wordt het bericht vergrendeld om te voorkomen dat andere consumenten het ontvangen en wordt het bericht vervolgens naar de toepassing geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b960a-154">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="b960a-155">Nadat de toepassing klaar is met verwerking van het bericht (of veilig heeft opgeslagen voor toekomstige verwerking), is de tweede fase van het ontvangstproces voltooid door het aanroepen van `delete` methode op de **bericht** object.</span><span class="sxs-lookup"><span data-stu-id="b960a-155">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling `delete` method on the **Message** object.</span></span> <span data-ttu-id="b960a-156">De `delete` methode markeert het bericht als verbruikt en wordt deze verwijderd uit het abonnement.</span><span class="sxs-lookup"><span data-stu-id="b960a-156">The `delete` method marks the message as being consumed and removes it from the subscription.</span></span>

```python
msg = bus_service.receive_subscription_message('mytopic', 'LowMessages', peek_lock=True)
print(msg.body)

msg.delete()
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="b960a-157">Het vastlopen van de toepassing en onleesbare berichten afhandelen</span><span class="sxs-lookup"><span data-stu-id="b960a-157">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="b960a-158">Service Bus biedt functionaliteit om netjes te herstellen bij fouten in uw toepassing of problemen bij het verwerken van een bericht.</span><span class="sxs-lookup"><span data-stu-id="b960a-158">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="b960a-159">Als een ontvangende toepassing kan niet worden verwerkt het bericht om een bepaalde reden, dan kan worden aangeroepen de `unlock` methode op de **bericht** object.</span><span class="sxs-lookup"><span data-stu-id="b960a-159">If a receiver application is unable to process the message for some reason, then it can call the `unlock` method on the **Message** object.</span></span> <span data-ttu-id="b960a-160">Dit zorgt ervoor dat Service Bus het bericht in het abonnement ontgrendelt en beschikbaar zijn om opnieuw te ontvangen, ofwel door dezelfde consumerende toepassing of door een andere consumerende toepassing.</span><span class="sxs-lookup"><span data-stu-id="b960a-160">This will cause Service Bus to unlock the message within the subscription and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="b960a-161">Er is ook een time-out gekoppeld aan een bericht in het abonnement is vergrendeld en als de toepassing niet kan verwerken van het bericht voordat de time-out van de vergrendeling verloopt (bijvoorbeeld als de toepassing vastloopt), en vervolgens de Service Bus het bericht automatisch ontgrendelt en wordt het beschikbaar worden om opnieuw te ontvangen.</span><span class="sxs-lookup"><span data-stu-id="b960a-161">There is also a timeout associated with a message locked within the subscription, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus unlocks the message automatically and makes it available to be received again.</span></span>

<span data-ttu-id="b960a-162">In het geval dat de toepassing is vastgelopen na het verwerken van het bericht, maar voordat de `delete` methode wordt aangeroepen en vervolgens het bericht opnieuw bezorgd bij de toepassing opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="b960a-162">In the event that the application crashes after processing the message but before the `delete` method is called, then the message will be redelivered to the application when it restarts.</span></span> <span data-ttu-id="b960a-163">Dit wordt vaak genoemd *tenminste eenmaal verwerken*, dat wil zeggen elk bericht ten minste één keer wordt verwerkt maar in sommige situaties hetzelfde bericht opnieuw kan worden bezorgd.</span><span class="sxs-lookup"><span data-stu-id="b960a-163">This is often called *At Least Once Processing*, that is, each message will be processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="b960a-164">Als in het scenario dubbele verwerking niet wordt getolereerd, dan moeten toepassingsontwikkelaars extra logica toevoegen aan de toepassing om dubbele berichtbezorging af te handelen.</span><span class="sxs-lookup"><span data-stu-id="b960a-164">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="b960a-165">Dit wordt vaak bereikt met behulp van de **MessageId** eigenschap van het bericht dat gelijk bij meerdere bezorgingspogingen blijft.</span><span class="sxs-lookup"><span data-stu-id="b960a-165">This is often achieved using the **MessageId** property of the message, which will remain constant across delivery attempts.</span></span>

## <a name="delete-topics-and-subscriptions"></a><span data-ttu-id="b960a-166">Onderwerpen en abonnementen verwijderen</span><span class="sxs-lookup"><span data-stu-id="b960a-166">Delete topics and subscriptions</span></span>
<span data-ttu-id="b960a-167">Onderwerpen en abonnementen worden permanent en expliciet moet worden verwijderd via de [Azure-portal] [ Azure portal] of via een programma.</span><span class="sxs-lookup"><span data-stu-id="b960a-167">Topics and subscriptions are persistent, and must be explicitly deleted either through the [Azure portal][Azure portal] or programmatically.</span></span> <span data-ttu-id="b960a-168">Het volgende voorbeeld laat zien hoe u het onderwerp met de naam `mytopic`:</span><span class="sxs-lookup"><span data-stu-id="b960a-168">The following example shows how to delete the topic named `mytopic`:</span></span>

```python
bus_service.delete_topic('mytopic')
```

<span data-ttu-id="b960a-169">Als een onderwerp wordt verwijderd, worden ook alle abonnementen verwijderd die zijn geregistreerd bij het onderwerp.</span><span class="sxs-lookup"><span data-stu-id="b960a-169">Deleting a topic also deletes any subscriptions that are registered with the topic.</span></span> <span data-ttu-id="b960a-170">Abonnementen kunnen ook afzonderlijk worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="b960a-170">Subscriptions can also be deleted independently.</span></span> <span data-ttu-id="b960a-171">De volgende code laat zien hoe u een abonnement met de naam `HighMessages` van de `mytopic` onderwerp:</span><span class="sxs-lookup"><span data-stu-id="b960a-171">The following code shows how to delete a subscription named `HighMessages` from the `mytopic` topic:</span></span>

```python
bus_service.delete_subscription('mytopic', 'HighMessages')
```

## <a name="next-steps"></a><span data-ttu-id="b960a-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b960a-172">Next steps</span></span>
<span data-ttu-id="b960a-173">Nu u de basisprincipes van Service Bus-onderwerpen hebt geleerd, volgt u deze koppelingen voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b960a-173">Now that you've learned the basics of Service Bus topics, follow these links to learn more.</span></span>

* <span data-ttu-id="b960a-174">Zie [wachtrijen, onderwerpen en abonnementen][Queues, topics, and subscriptions].</span><span class="sxs-lookup"><span data-stu-id="b960a-174">See [Queues, topics, and subscriptions][Queues, topics, and subscriptions].</span></span>
* <span data-ttu-id="b960a-175">Referentiemateriaal [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span><span class="sxs-lookup"><span data-stu-id="b960a-175">Reference for [SqlFilter.SqlExpression][SqlFilter.SqlExpression].</span></span>

[Azure portal]: https://portal.azure.com
[Azure Python package]: https://pypi.python.org/pypi/azure  
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter.SqlExpression]: service-bus-messaging-sql-filter.md
[Service Bus quotas]: service-bus-quotas.md 
