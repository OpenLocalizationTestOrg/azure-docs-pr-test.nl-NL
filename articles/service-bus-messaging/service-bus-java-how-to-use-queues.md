---
title: Azure Service Bus-wachtrijen gebruiken met Java | Microsoft Docs
description: Informatie over het gebruiken van Service Bus-wachtrijen in Azure Codevoorbeelden geschreven in Java.
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
ms.assetid: f701439c-553e-402c-94a7-64400f997d59
ms.service: service-bus-messaging
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 08/10/2017
ms.author: sethm
ms.openlocfilehash: 170f431525ffdc93a01fc085e48e69c3a774968e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-use-service-bus-queues-with-java"></a><span data-ttu-id="3e62b-104">Service Bus-wachtrijen gebruiken met Java</span><span class="sxs-lookup"><span data-stu-id="3e62b-104">How to use Service Bus queues with Java</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="3e62b-105">In dit artikel wordt het gebruik van de Service Bus-wachtrijen beschreven.</span><span class="sxs-lookup"><span data-stu-id="3e62b-105">This article describes how to use Service Bus queues.</span></span> <span data-ttu-id="3e62b-106">De voorbeelden zijn geschreven in Java en gebruik de [Azure SDK voor Java][Azure SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="3e62b-106">The samples are written in Java and use the [Azure SDK for Java][Azure SDK for Java].</span></span> <span data-ttu-id="3e62b-107">De scenario's worden behandeld: **maken van wachtrijen**, **verzenden en ontvangen berichten**, en **verwijderen van wachtrijen**.</span><span class="sxs-lookup"><span data-stu-id="3e62b-107">The scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-to-use-service-bus"></a><span data-ttu-id="3e62b-108">Uw toepassing configureren voor het gebruik van Service Bus</span><span class="sxs-lookup"><span data-stu-id="3e62b-108">Configure your application to use Service Bus</span></span>
<span data-ttu-id="3e62b-109">Zorg ervoor dat u hebt geïnstalleerd het [Azure SDK voor Java] [ Azure SDK for Java] voordat u dit voorbeeld maakt.</span><span class="sxs-lookup"><span data-stu-id="3e62b-109">Make sure you have installed the [Azure SDK for Java][Azure SDK for Java] before building this sample.</span></span> <span data-ttu-id="3e62b-110">Als u Eclipse gebruikt, kunt u de [Azure Toolkit voor Eclipse] [ Azure Toolkit for Eclipse] waarin de Azure SDK voor Java.</span><span class="sxs-lookup"><span data-stu-id="3e62b-110">If you are using Eclipse, you can install the [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes the Azure SDK for Java.</span></span> <span data-ttu-id="3e62b-111">Vervolgens kunt u toevoegen de **Microsoft Azure-beheerbibliotheken voor Java** aan uw project:</span><span class="sxs-lookup"><span data-stu-id="3e62b-111">You can then add the **Microsoft Azure Libraries for Java** to your project:</span></span>

![](./media/service-bus-java-how-to-use-queues/eclipselibs.png)

<span data-ttu-id="3e62b-112">Voeg de volgende `import` instructies aan het begin van de Java-bestand:</span><span class="sxs-lookup"><span data-stu-id="3e62b-112">Add the following `import` statements to the top of the Java file:</span></span>

```java
// Include the following imports to use Service Bus APIs
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

## <a name="create-a-queue"></a><span data-ttu-id="3e62b-113">Een wachtrij maken</span><span class="sxs-lookup"><span data-stu-id="3e62b-113">Create a queue</span></span>
<span data-ttu-id="3e62b-114">Beheerbewerkingen voor Service Bus-wachtrijen kunnen worden uitgevoerd via de **ServiceBusContract** klasse.</span><span class="sxs-lookup"><span data-stu-id="3e62b-114">Management operations for Service Bus queues can be performed via the **ServiceBusContract** class.</span></span> <span data-ttu-id="3e62b-115">Een **ServiceBusContract** object is gemaakt met een juiste configuratie die de SAS-token met machtigingen voor beheer, ingekapseld en de **ServiceBusContract** klasse is het enige dat communicatie met Azure.</span><span class="sxs-lookup"><span data-stu-id="3e62b-115">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions to manage it, and the **ServiceBusContract** class is the sole point of communication with Azure.</span></span>

<span data-ttu-id="3e62b-116">De **ServiceBusService** klasse biedt methoden voor het maken, opsommen en verwijderen van wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="3e62b-116">The **ServiceBusService** class provides methods to create, enumerate, and delete queues.</span></span> <span data-ttu-id="3e62b-117">In het voorbeeld hieronder toont hoe een **ServiceBusService** object kan worden gebruikt voor het maken van een wachtrij met de naam `TestQueue`, met een naamruimte met de naam `HowToSample`:</span><span class="sxs-lookup"><span data-stu-id="3e62b-117">The example below shows how a **ServiceBusService** object can be used to create a queue named `TestQueue`, with a namespace named `HowToSample`:</span></span>

```java
Configuration config =
    ServiceBusConfiguration.configureWithSASAuthentication(
            "HowToSample",
            "RootManageSharedAccessKey",
            "SAS_key_value",
            ".servicebus.windows.net"
            );

ServiceBusContract service = ServiceBusService.create(config);
QueueInfo queueInfo = new QueueInfo("TestQueue");
try
{
    CreateQueueResult result = service.createQueue(queueInfo);
}
catch (ServiceException e)
{
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

<span data-ttu-id="3e62b-118">Er zijn methoden op `QueueInfo` waarmee de eigenschappen van de wachtrij om te worden afgestemd (bijvoorbeeld: instellen van de time-to-live (TTL) standaardwaarde moet worden toegepast op berichten die naar de wachtrij worden verzonden).</span><span class="sxs-lookup"><span data-stu-id="3e62b-118">There are methods on `QueueInfo` that allow properties of the queue to be tuned (for example: to set the default time-to-live (TTL) value to be applied to messages sent to the queue).</span></span> <span data-ttu-id="3e62b-119">Het volgende voorbeeld laat zien hoe een wachtrij met de naam maken `TestQueue` met een maximale grootte van 5 GB:</span><span class="sxs-lookup"><span data-stu-id="3e62b-119">The following example shows how to create a queue named `TestQueue` with a maximum size of 5GB:</span></span>

````java
long maxSizeInMegabytes = 5120;
QueueInfo queueInfo = new QueueInfo("TestQueue");
queueInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateQueueResult result = service.createQueue(queueInfo);
````

<span data-ttu-id="3e62b-120">Let op: u kunt de `listQueues` methode op **ServiceBusContract** objecten om te controleren of een wachtrij met een opgegeven naam al in een Servicenaamruimte bestaat.</span><span class="sxs-lookup"><span data-stu-id="3e62b-120">Note that you can use the `listQueues` method on **ServiceBusContract** objects to check if a queue with a specified name already exists within a service namespace.</span></span>

## <a name="send-messages-to-a-queue"></a><span data-ttu-id="3e62b-121">Berichten verzenden naar een wachtrij</span><span class="sxs-lookup"><span data-stu-id="3e62b-121">Send messages to a queue</span></span>
<span data-ttu-id="3e62b-122">Als u wilt een bericht verzendt naar een Service Bus-wachtrij, beheersbaarheid voor uw toepassing een **ServiceBusContract** object.</span><span class="sxs-lookup"><span data-stu-id="3e62b-122">To send a message to a Service Bus queue, your application obtains a **ServiceBusContract** object.</span></span> <span data-ttu-id="3e62b-123">De volgende code toont hoe u een bericht te verzenden voor de `TestQueue` wachtrij eerder hebt gemaakt de `HowToSample` naamruimte:</span><span class="sxs-lookup"><span data-stu-id="3e62b-123">The following code shows how to send a message for the `TestQueue` queue previously created in the `HowToSample` namespace:</span></span>

```java
try
{
    BrokeredMessage message = new BrokeredMessage("MyMessage");
    service.sendQueueMessage("TestQueue", message);
}
catch (ServiceException e)
{
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

<span data-ttu-id="3e62b-124">Berichten worden verzonden naar en ontvangen van Service Bus-wachtrijen, zijn exemplaren van de [BrokeredMessage] [ BrokeredMessage] klasse.</span><span class="sxs-lookup"><span data-stu-id="3e62b-124">Messages sent to, and received from Service Bus queues are instances of the [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="3e62b-125">[BrokeredMessage] [ BrokeredMessage] objecten hebben een aantal standaardeigenschappen (zoals [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) en [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), een woordenlijst die wordt gebruikt om aangepaste toepassingsspecifieke eigenschappen en een hoofdtekst met willekeurige toepassingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="3e62b-125">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties (such as [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) and [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), a dictionary that is used to hold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="3e62b-126">Een toepassing kunt de hoofdtekst van het bericht instellen door elk serialiseerbaar object doorgeven aan de constructor van het [BrokeredMessage][BrokeredMessage], en de juiste serialisatiefunctie wordt vervolgens gebruikt om het object te serialiseren.</span><span class="sxs-lookup"><span data-stu-id="3e62b-126">An application can set the body of the message by passing any serializable object into the constructor of the [BrokeredMessage][BrokeredMessage], and the appropriate serializer will then be used to serialize the object.</span></span> <span data-ttu-id="3e62b-127">U kunt ook bieden een **java. I/O. InputStream** object.</span><span class="sxs-lookup"><span data-stu-id="3e62b-127">Alternatively, you can provide a **java.IO.InputStream** object.</span></span>

<span data-ttu-id="3e62b-128">Het volgende voorbeeld toont hoe vijf testberichten naar verzendt de `TestQueue` **MessageSender** we verkregen in het vorige codefragment:</span><span class="sxs-lookup"><span data-stu-id="3e62b-128">The following example demonstrates how to send five test messages to the `TestQueue` **MessageSender** we obtained in the previous code snippet:</span></span>

```java
for (int i=0; i<5; i++)
{
     // Create message, passing a string message for the body.
     BrokeredMessage message = new BrokeredMessage("Test message " + i);
     // Set an additional app-specific property.
     message.setProperty("MyProperty", i);
     // Send message to the queue
     service.sendQueueMessage("TestQueue", message);
}
```

<span data-ttu-id="3e62b-129">Service Bus-wachtrijen ondersteunen een maximale berichtgrootte van 256 kB in de [Standard-laag](service-bus-premium-messaging.md) en 1 MB in de [Premium-laag](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="3e62b-129">Service Bus queues support a maximum message size of 256 KB in the [Standard tier](service-bus-premium-messaging.md) and 1 MB in the [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="3e62b-130">De koptekst, die de standaard- en aangepaste toepassingseigenschappen bevat, kan maximaal 64 kB groot zijn.</span><span class="sxs-lookup"><span data-stu-id="3e62b-130">The header, which includes the standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="3e62b-131">Er is geen limiet voor het aantal berichten in een wachtrij, maar er is een limiet voor de totale grootte van de berichten in een wachtrij.</span><span class="sxs-lookup"><span data-stu-id="3e62b-131">There is no limit on the number of messages held in a queue but there is a cap on the total size of the messages held by a queue.</span></span> <span data-ttu-id="3e62b-132">De grootte van de wachtrij wordt gedefinieerd tijdens het aanmaken, met een bovengrens van 5 GB.</span><span class="sxs-lookup"><span data-stu-id="3e62b-132">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="3e62b-133">Berichten ontvangen uit een wachtrij</span><span class="sxs-lookup"><span data-stu-id="3e62b-133">Receive messages from a queue</span></span>
<span data-ttu-id="3e62b-134">De belangrijkste manier om berichten te ontvangen van een wachtrij is met een **ServiceBusContract** object.</span><span class="sxs-lookup"><span data-stu-id="3e62b-134">The primary way to receive messages from a queue is to use a **ServiceBusContract** object.</span></span> <span data-ttu-id="3e62b-135">Ontvangen berichten kunnen werken in twee verschillende modi: **ReceiveAndDelete** en **PeekLock**.</span><span class="sxs-lookup"><span data-stu-id="3e62b-135">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span>

<span data-ttu-id="3e62b-136">Wanneer u de **ReceiveAndDelete** -modus ontvangt een enkele bewerking - dat wil zeggen als Service Bus een leesaanvraag voor een bericht in een wachtrij ontvangt, wordt het bericht als verbruikt gemarkeerd en naar de toepassing wordt geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="3e62b-136">When using the **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message in a queue, it marks the message as being consumed and returns it to the application.</span></span> <span data-ttu-id="3e62b-137">**ReceiveAndDelete** modus (dit is de standaardmodus) is het eenvoudigste model en werkt het beste voor scenario's waarin een toepassing kan tolereren niet verwerken van een bericht bij een storing.</span><span class="sxs-lookup"><span data-stu-id="3e62b-137">**ReceiveAndDelete** mode (which is the default mode) is the simplest model and works best for scenarios in which an application can tolerate not processing a message in the event of a failure.</span></span> <span data-ttu-id="3e62b-138">Neem bijvoorbeeld een scenario waarin de consument de ontvangstaanvraag uitgeeft en het systeem vervolgens vastloopt voordat de aanvraag wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="3e62b-138">To understand this, consider a scenario in which the consumer issues the receive request and then crashes before processing it.</span></span>
<span data-ttu-id="3e62b-139">Omdat Service Bus het bericht als verbruikt heeft gemarkeerd, klikt u vervolgens wanneer de toepassing opnieuw wordt opgestart en het verbruik van berichten opnieuw begint, ontbreekt het bericht dat voor het vastlopen is verbruikt.</span><span class="sxs-lookup"><span data-stu-id="3e62b-139">Because Service Bus will have marked the message as being consumed, then when the application restarts and begins consuming messages again, it will have missed the message that was consumed prior to the crash.</span></span>

<span data-ttu-id="3e62b-140">In **PeekLock** -modus ontvangt, wordt een bewerking met twee fasen, waardoor er mogelijk worden ondersteuning voor toepassingen die geen ontbrekende berichten kunnen tolereren.</span><span class="sxs-lookup"><span data-stu-id="3e62b-140">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible to support applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="3e62b-141">Als Service Bus een aanvraag ontvangt, wordt het volgende te verbruiken bericht gevonden, wordt het bericht vergrendeld om te voorkomen dat andere consumenten het ontvangen en wordt het bericht vervolgens naar de toepassing geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="3e62b-141">When Service Bus receives a request, it finds the next message to be consumed, locks it to prevent other consumers receiving it, and then returns it to the application.</span></span> <span data-ttu-id="3e62b-142">Nadat de toepassing klaar is met verwerking van het bericht (of veilig heeft opgeslagen voor toekomstige verwerking), is de tweede fase van het ontvangstproces voltooid door het aanroepen van **verwijderen** voor het ontvangen bericht.</span><span class="sxs-lookup"><span data-stu-id="3e62b-142">After the application finishes processing the message (or stores it reliably for future processing), it completes the second stage of the receive process by calling **Delete** on the received message.</span></span> <span data-ttu-id="3e62b-143">Wanneer Service Bus de aanroep de **verwijderen** aanroep, wordt het bericht als verbruikt markeren en verwijderen uit de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="3e62b-143">When Service Bus sees the **Delete** call, it will mark the message as being consumed and remove it from the queue.</span></span>

<span data-ttu-id="3e62b-144">Het volgende voorbeeld laat zien hoe berichten kunnen worden ontvangen en verwerkt met behulp **PeekLock** modus (niet de standaardmodus).</span><span class="sxs-lookup"><span data-stu-id="3e62b-144">The following example demonstrates how messages can be received and processed using **PeekLock** mode (not the default mode).</span></span> <span data-ttu-id="3e62b-145">Het volgende voorbeeld wordt een oneindige lus en verwerkt berichten binnenkomen in onze `TestQueue`:</span><span class="sxs-lookup"><span data-stu-id="3e62b-145">The example below does an infinite loop and processes messages as they arrive into our `TestQueue`:</span></span>

```java
try
{
    ReceiveMessageOptions opts = ReceiveMessageOptions.DEFAULT;
    opts.setReceiveMode(ReceiveMode.PEEK_LOCK);

    while(true)  {
         ReceiveQueueMessageResult resultQM =
                 service.receiveQueueMessage("TestQueue", opts);
        BrokeredMessage message = resultQM.getValue();
        if (message != null && message.getMessageId() != null)
        {
            System.out.println("MessageID: " + message.getMessageId());
            // Display the queue message.
            System.out.print("From queue: ");
            byte[] b = new byte[200];
            String s = null;
            int numRead = message.getBody().read(b);
            while (-1 != numRead)
            {
                s = new String(b);
                s = s.trim();
                System.out.print(s);
                numRead = message.getBody().read(b);
            }
            System.out.println();
            System.out.println("Custom Property: " +
                message.getProperty("MyProperty"));
            // Remove message from queue.
            System.out.println("Deleting this message.");
            //service.deleteMessage(message);
        }  
        else  
        {
            System.out.println("Finishing up - no more messages.");
            break;
            // Added to handle no more messages.
            // Could instead wait for more messages to be added.
        }
    }
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
catch (Exception e) {
    System.out.print("Generic exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

## <a name="how-to-handle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="3e62b-146">Het vastlopen van de toepassing en onleesbare berichten afhandelen</span><span class="sxs-lookup"><span data-stu-id="3e62b-146">How to handle application crashes and unreadable messages</span></span>
<span data-ttu-id="3e62b-147">Service Bus biedt functionaliteit om netjes te herstellen bij fouten in uw toepassing of problemen bij het verwerken van een bericht.</span><span class="sxs-lookup"><span data-stu-id="3e62b-147">Service Bus provides functionality to help you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="3e62b-148">Als een ontvangende toepassing kan niet worden verwerkt het bericht om een bepaalde reden, dan kan worden aangeroepen de **unlockMessage** methode voor het ontvangen bericht (in plaats van de **deleteMessage** methode).</span><span class="sxs-lookup"><span data-stu-id="3e62b-148">If a receiver application is unable to process the message for some reason, then it can call the **unlockMessage** method on the received message (instead of the **deleteMessage** method).</span></span> <span data-ttu-id="3e62b-149">Dit zorgt ervoor dat Service Bus het bericht in de wachtrij ontgrendelt en het beschikbaar maakt om opnieuw te worden ontvangen, ofwel door dezelfde consumerende toepassing of door een andere consumerende toepassing.</span><span class="sxs-lookup"><span data-stu-id="3e62b-149">This causes Service Bus to unlock the message within the queue and make it available to be received again, either by the same consuming application or by another consuming application.</span></span>

<span data-ttu-id="3e62b-150">Er is ook een time-out gekoppeld aan een bericht in de wachtrij is vergrendeld en als de toepassing niet kan verwerken van het bericht voordat de time-out van de vergrendeling verloopt (bijvoorbeeld als de toepassing vastloopt), en vervolgens de Service Bus het bericht automatisch ontgrendelt en wordt het beschikbaar worden om opnieuw te ontvangen.</span><span class="sxs-lookup"><span data-stu-id="3e62b-150">There is also a timeout associated with a message locked within the queue, and if the application fails to process the message before the lock timeout expires (for example, if the application crashes), then Service Bus unlocks the message automatically and makes it available to be received again.</span></span>

<span data-ttu-id="3e62b-151">In het geval dat de toepassing is vastgelopen na het verwerken van het bericht, maar voordat de **deleteMessage** verzoek is uitgegeven, en vervolgens het bericht is opnieuw bij de toepassing bezorgd wanneer opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="3e62b-151">In the event that the application crashes after processing the message but before the **deleteMessage** request is issued, then the message is redelivered to the application when it restarts.</span></span> <span data-ttu-id="3e62b-152">Dit wordt vaak genoemd *tenminste eenmaal verwerken*; dat wil zeggen, elk bericht ten minste één keer wordt verwerkt maar in sommige situaties hetzelfde bericht opnieuw kan worden bezorgd.</span><span class="sxs-lookup"><span data-stu-id="3e62b-152">This is often called *At Least Once Processing*; that is, each message is processed at least once but in certain situations the same message may be redelivered.</span></span> <span data-ttu-id="3e62b-153">Als in het scenario dubbele verwerking niet wordt getolereerd, dan moeten toepassingsontwikkelaars extra logica toevoegen aan de toepassing om dubbele berichtbezorging af te handelen.</span><span class="sxs-lookup"><span data-stu-id="3e62b-153">If the scenario cannot tolerate duplicate processing, then application developers should add additional logic to their application to handle duplicate message delivery.</span></span> <span data-ttu-id="3e62b-154">Dit wordt vaak bereikt met behulp van de **getMessageId** methode van het bericht dat gelijk blijft bij meerdere bezorgingspogingen.</span><span class="sxs-lookup"><span data-stu-id="3e62b-154">This is often achieved using the **getMessageId** method of the message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3e62b-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3e62b-155">Next Steps</span></span>
<span data-ttu-id="3e62b-156">Nu u de basisprincipes van Service Bus-wachtrijen hebt geleerd, gaat u naar [wachtrijen, onderwerpen en abonnementen] [ Queues, topics, and subscriptions] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3e62b-156">Now that you've learned the basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="3e62b-157">Raadpleeg het [Java Developer Center](https://azure.microsoft.com/develop/java/) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3e62b-157">For more information, see the [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh694271.aspx
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
