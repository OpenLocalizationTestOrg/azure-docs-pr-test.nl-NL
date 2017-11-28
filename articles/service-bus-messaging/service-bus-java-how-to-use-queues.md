---
title: aaaHow toouse Azure Service Bus-wachtrijen met Java | Microsoft Docs
description: Meer informatie over hoe toouse Service Bus wachtrijen in Azure. Codevoorbeelden geschreven in Java.
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
ms.openlocfilehash: f68e941438134090c5eee53459e7667bda13ff3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-queues-with-java"></a><span data-ttu-id="3273b-104">Hoe toouse Service Bus wachtrijen met Java</span><span class="sxs-lookup"><span data-stu-id="3273b-104">How toouse Service Bus queues with Java</span></span>
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

<span data-ttu-id="3273b-105">Dit artikel wordt beschreven hoe toouse Service Bus-wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="3273b-105">This article describes how toouse Service Bus queues.</span></span> <span data-ttu-id="3273b-106">Hallo-voorbeelden zijn geschreven in Java en gebruiken van Hallo [Azure SDK voor Java][Azure SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="3273b-106">hello samples are written in Java and use hello [Azure SDK for Java][Azure SDK for Java].</span></span> <span data-ttu-id="3273b-107">Hallo scenario's worden behandeld: **maken van wachtrijen**, **verzenden en ontvangen berichten**, en **verwijderen van wachtrijen**.</span><span class="sxs-lookup"><span data-stu-id="3273b-107">hello scenarios covered include **creating queues**, **sending and receiving messages**, and **deleting queues**.</span></span>

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a><span data-ttu-id="3273b-108">Configureren van uw toepassing toouse Service Bus</span><span class="sxs-lookup"><span data-stu-id="3273b-108">Configure your application toouse Service Bus</span></span>
<span data-ttu-id="3273b-109">Zorg ervoor dat u hebt geïnstalleerd Hallo [Azure SDK voor Java] [ Azure SDK for Java] voordat u dit voorbeeld maakt.</span><span class="sxs-lookup"><span data-stu-id="3273b-109">Make sure you have installed hello [Azure SDK for Java][Azure SDK for Java] before building this sample.</span></span> <span data-ttu-id="3273b-110">Als u Eclipse gebruikt, kunt u Hallo installeren [Azure Toolkit voor Eclipse] [ Azure Toolkit for Eclipse] die hello Azure SDK voor Java bevat.</span><span class="sxs-lookup"><span data-stu-id="3273b-110">If you are using Eclipse, you can install hello [Azure Toolkit for Eclipse][Azure Toolkit for Eclipse] that includes hello Azure SDK for Java.</span></span> <span data-ttu-id="3273b-111">Vervolgens kunt u toevoegen Hallo **Microsoft Azure-beheerbibliotheken voor Java** tooyour project:</span><span class="sxs-lookup"><span data-stu-id="3273b-111">You can then add hello **Microsoft Azure Libraries for Java** tooyour project:</span></span>

![](./media/service-bus-java-how-to-use-queues/eclipselibs.png)

<span data-ttu-id="3273b-112">Voeg de volgende Hallo `import` instructies toohello boven in Hallo Java-bestand:</span><span class="sxs-lookup"><span data-stu-id="3273b-112">Add hello following `import` statements toohello top of hello Java file:</span></span>

```java
// Include hello following imports toouse Service Bus APIs
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

## <a name="create-a-queue"></a><span data-ttu-id="3273b-113">Een wachtrij maken</span><span class="sxs-lookup"><span data-stu-id="3273b-113">Create a queue</span></span>
<span data-ttu-id="3273b-114">Beheerbewerkingen voor Service Bus-wachtrijen kunnen worden uitgevoerd via de **ServiceBusContract** klasse.</span><span class="sxs-lookup"><span data-stu-id="3273b-114">Management operations for Service Bus queues can be performed via the **ServiceBusContract** class.</span></span> <span data-ttu-id="3273b-115">Een **ServiceBusContract** object is gemaakt met een juiste configuratie die door de SAS-token met machtigingen toomanage ingekapseld en Hallo **ServiceBusContract** klasse is de enige punt Hallo communicatie met Azure.</span><span class="sxs-lookup"><span data-stu-id="3273b-115">A **ServiceBusContract** object is constructed with an appropriate configuration that encapsulates the SAS token with permissions toomanage it, and hello **ServiceBusContract** class is hello sole point of communication with Azure.</span></span>

<span data-ttu-id="3273b-116">Hallo **ServiceBusService** klasse biedt methoden toocreate, opsommen en verwijderen van wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="3273b-116">hello **ServiceBusService** class provides methods toocreate, enumerate, and delete queues.</span></span> <span data-ttu-id="3273b-117">Hallo voorbeeld hieronder toont hoe een **ServiceBusService** -object dat wordt gebruikt toocreate een wachtrij met de naam `TestQueue`, met een naamruimte met de naam `HowToSample`:</span><span class="sxs-lookup"><span data-stu-id="3273b-117">hello example below shows how a **ServiceBusService** object can be used toocreate a queue named `TestQueue`, with a namespace named `HowToSample`:</span></span>

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

<span data-ttu-id="3273b-118">Er zijn methoden op `QueueInfo` waarmee de eigenschappen van Hallo wachtrij toobe afgestemd (bijvoorbeeld: tooset Hallo standaard time-to-live (TTL) waarde toobe toegepast toomessages toohello wachtrij verzonden).</span><span class="sxs-lookup"><span data-stu-id="3273b-118">There are methods on `QueueInfo` that allow properties of hello queue toobe tuned (for example: tooset hello default time-to-live (TTL) value toobe applied toomessages sent toohello queue).</span></span> <span data-ttu-id="3273b-119">Hallo volgende voorbeeld laat zien hoe toocreate een wachtrij met de naam `TestQueue` met een maximale grootte van 5 GB:</span><span class="sxs-lookup"><span data-stu-id="3273b-119">hello following example shows how toocreate a queue named `TestQueue` with a maximum size of 5GB:</span></span>

````java
long maxSizeInMegabytes = 5120;
QueueInfo queueInfo = new QueueInfo("TestQueue");
queueInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateQueueResult result = service.createQueue(queueInfo);
````

<span data-ttu-id="3273b-120">Dat kunt u gebruikmaken van Hallo `listQueues` methode op **ServiceBusContract** toocheck objecten als een wachtrij met een opgegeven naam al in een Servicenaamruimte bestaat.</span><span class="sxs-lookup"><span data-stu-id="3273b-120">Note that you can use hello `listQueues` method on **ServiceBusContract** objects toocheck if a queue with a specified name already exists within a service namespace.</span></span>

## <a name="send-messages-tooa-queue"></a><span data-ttu-id="3273b-121">Berichten tooa wachtrij verzenden</span><span class="sxs-lookup"><span data-stu-id="3273b-121">Send messages tooa queue</span></span>
<span data-ttu-id="3273b-122">een bericht tooa Service Bus-wachtrij toosend, beheersbaarheid voor uw toepassing een **ServiceBusContract** object.</span><span class="sxs-lookup"><span data-stu-id="3273b-122">toosend a message tooa Service Bus queue, your application obtains a **ServiceBusContract** object.</span></span> <span data-ttu-id="3273b-123">Hallo van de volgende code toont hoe een bericht voor Hallo toosend `TestQueue` wachtrij eerder hebt gemaakt in Hallo `HowToSample` naamruimte:</span><span class="sxs-lookup"><span data-stu-id="3273b-123">hello following code shows how toosend a message for hello `TestQueue` queue previously created in hello `HowToSample` namespace:</span></span>

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

<span data-ttu-id="3273b-124">Berichten worden verzonden naar en ontvangen van Service Bus-wachtrijen, zijn exemplaren van Hallo [BrokeredMessage] [ BrokeredMessage] klasse.</span><span class="sxs-lookup"><span data-stu-id="3273b-124">Messages sent to, and received from Service Bus queues are instances of hello [BrokeredMessage][BrokeredMessage] class.</span></span> <span data-ttu-id="3273b-125">[BrokeredMessage] [ BrokeredMessage] objecten hebben een aantal standaardeigenschappen (zoals [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) en [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), een woordenlijst die wordt gebruikt toohold aangepaste toepassingsspecifieke eigenschappen en een hoofdtekst met willekeurige toepassingsgegevens.</span><span class="sxs-lookup"><span data-stu-id="3273b-125">[BrokeredMessage][BrokeredMessage] objects have a set of standard properties (such as [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) and [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), a dictionary that is used toohold custom application-specific properties, and a body of arbitrary application data.</span></span> <span data-ttu-id="3273b-126">Een toepassing hello hoofdtekst van het Hallo-bericht kunt instellen door elk serialiseerbaar object doorgeven aan de constructor Hallo Hallo [BrokeredMessage][BrokeredMessage], en de bijbehorende serialisatiefunctie hello wordt vervolgens gebruikt tooserialize Hallo-object.</span><span class="sxs-lookup"><span data-stu-id="3273b-126">An application can set hello body of hello message by passing any serializable object into hello constructor of hello [BrokeredMessage][BrokeredMessage], and hello appropriate serializer will then be used tooserialize hello object.</span></span> <span data-ttu-id="3273b-127">U kunt ook bieden een **java. I/O. InputStream** object.</span><span class="sxs-lookup"><span data-stu-id="3273b-127">Alternatively, you can provide a **java.IO.InputStream** object.</span></span>

<span data-ttu-id="3273b-128">Hallo volgende voorbeeld toont hoe vijf toosend test toothe berichten `TestQueue` **MessageSender** we in de vorige codefragment Hallo verkregen:</span><span class="sxs-lookup"><span data-stu-id="3273b-128">hello following example demonstrates how toosend five test messages toothe `TestQueue` **MessageSender** we obtained in hello previous code snippet:</span></span>

```java
for (int i=0; i<5; i++)
{
     // Create message, passing a string message for hello body.
     BrokeredMessage message = new BrokeredMessage("Test message " + i);
     // Set an additional app-specific property.
     message.setProperty("MyProperty", i);
     // Send message toohello queue
     service.sendQueueMessage("TestQueue", message);
}
```

<span data-ttu-id="3273b-129">Service Bus-wachtrijen ondersteunen een maximale berichtgrootte van 256 KB in Hallo [standaardcategorie](service-bus-premium-messaging.md) en 1 MB in Hallo [Premium-laag](service-bus-premium-messaging.md).</span><span class="sxs-lookup"><span data-stu-id="3273b-129">Service Bus queues support a maximum message size of 256 KB in hello [Standard tier](service-bus-premium-messaging.md) and 1 MB in hello [Premium tier](service-bus-premium-messaging.md).</span></span> <span data-ttu-id="3273b-130">Hallo-kop, die standaard Hallo- en aangepaste toepassingseigenschappen bevat, kan een maximale grootte van 64 KB hebben.</span><span class="sxs-lookup"><span data-stu-id="3273b-130">hello header, which includes hello standard and custom application properties, can have a maximum size of 64 KB.</span></span> <span data-ttu-id="3273b-131">Er is geen limiet voor het aantal berichten in een wachtrij hello, maar er is een limiet voor de totale grootte van berichten in een wachtrij Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="3273b-131">There is no limit on hello number of messages held in a queue but there is a cap on hello total size of hello messages held by a queue.</span></span> <span data-ttu-id="3273b-132">De grootte van de wachtrij wordt gedefinieerd tijdens het aanmaken, met een bovengrens van 5 GB.</span><span class="sxs-lookup"><span data-stu-id="3273b-132">This queue size is defined at creation time, with an upper limit of 5 GB.</span></span>

## <a name="receive-messages-from-a-queue"></a><span data-ttu-id="3273b-133">Berichten ontvangen uit een wachtrij</span><span class="sxs-lookup"><span data-stu-id="3273b-133">Receive messages from a queue</span></span>
<span data-ttu-id="3273b-134">Hallo primaire manier tooreceive berichten uit een wachtrij toouse is een **ServiceBusContract** object.</span><span class="sxs-lookup"><span data-stu-id="3273b-134">hello primary way tooreceive messages from a queue is toouse a **ServiceBusContract** object.</span></span> <span data-ttu-id="3273b-135">Ontvangen berichten kunnen werken in twee verschillende modi: **ReceiveAndDelete** en **PeekLock**.</span><span class="sxs-lookup"><span data-stu-id="3273b-135">Received messages can work in two different modes: **ReceiveAndDelete** and **PeekLock**.</span></span>

<span data-ttu-id="3273b-136">Bij gebruik van Hallo **ReceiveAndDelete** -modus ontvangt een enkele bewerking - dat wil zeggen als Service Bus een leesaanvraag voor een bericht in een wachtrij ontvangt, wordt markeert het Hallo-bericht als verbruikt en retourneert het toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="3273b-136">When using hello **ReceiveAndDelete** mode, receive is a single-shot operation - that is, when Service Bus receives a read request for a message in a queue, it marks hello message as being consumed and returns it toohello application.</span></span> <span data-ttu-id="3273b-137">**ReceiveAndDelete** modus (dit is de standaardmodus Hallo) is Hallo eenvoudigste model en werkt het beste voor scenario's waarin een toepassing kan tolereren niet verwerken van een bericht in de gebeurtenis Hallo van een fout.</span><span class="sxs-lookup"><span data-stu-id="3273b-137">**ReceiveAndDelete** mode (which is hello default mode) is hello simplest model and works best for scenarios in which an application can tolerate not processing a message in hello event of a failure.</span></span> <span data-ttu-id="3273b-138">toounderstand dit, Neem bijvoorbeeld een scenario in welke problemen van de consument Hallo Hallo aanvraag ontvangen en vervolgens vastloopt voordat het wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="3273b-138">toounderstand this, consider a scenario in which hello consumer issues hello receive request and then crashes before processing it.</span></span>
<span data-ttu-id="3273b-139">Omdat Service Bus heeft gemarkeerd als verbruikt, vervolgens wanneer Hallo toepassing opnieuw wordt opgestart en verbruik van berichten opnieuw begint het Hallo-bericht, ontbreekt het Hallo-bericht dat was voorafgaande toohello crash verbruikt.</span><span class="sxs-lookup"><span data-stu-id="3273b-139">Because Service Bus will have marked hello message as being consumed, then when hello application restarts and begins consuming messages again, it will have missed hello message that was consumed prior toohello crash.</span></span>

<span data-ttu-id="3273b-140">In **PeekLock** -modus ontvangt, wordt een bewerking met twee fasen, waardoor het mogelijk toosupport toepassingen die geen ontbrekende berichten kunnen tolereren.</span><span class="sxs-lookup"><span data-stu-id="3273b-140">In **PeekLock** mode, receive becomes a two stage operation, which makes it possible toosupport applications that cannot tolerate missing messages.</span></span> <span data-ttu-id="3273b-141">Wanneer Service Bus een aanvraag ontvangt, zoeken naar het volgende bericht toobe Hallo verbruikt, wordt vergrendeld tooprevent andere consumenten het ontvangen en retourneert vervolgens toohello toepassing.</span><span class="sxs-lookup"><span data-stu-id="3273b-141">When Service Bus receives a request, it finds hello next message toobe consumed, locks it tooprevent other consumers receiving it, and then returns it toohello application.</span></span> <span data-ttu-id="3273b-142">Nadat de toepassing hello klaar is met verwerking van het Hallo-bericht (of veilig heeft opgeslagen voor toekomstige verwerking), is de tweede fase Hallo Hallo voltooid proces ontvangen door het aanroepen van **verwijderen** op Hallo ontvangen bericht.</span><span class="sxs-lookup"><span data-stu-id="3273b-142">After hello application finishes processing hello message (or stores it reliably for future processing), it completes hello second stage of hello receive process by calling **Delete** on hello received message.</span></span> <span data-ttu-id="3273b-143">Wanneer Service Bus de aanroep Hallo **verwijderen** aanroep, wordt het Hallo-bericht als verbruikt markeren en verwijderen uit de wachtrij Hallo.</span><span class="sxs-lookup"><span data-stu-id="3273b-143">When Service Bus sees hello **Delete** call, it will mark hello message as being consumed and remove it from hello queue.</span></span>

<span data-ttu-id="3273b-144">Hallo volgende voorbeeld laat zien hoe berichten kunnen worden ontvangen en verwerkt met behulp **PeekLock** modus (geen Hallo standaardmodus).</span><span class="sxs-lookup"><span data-stu-id="3273b-144">hello following example demonstrates how messages can be received and processed using **PeekLock** mode (not hello default mode).</span></span> <span data-ttu-id="3273b-145">Hello in het volgende voorbeeld wordt een oneindige lus en verwerkt berichten binnenkomen in onze `TestQueue`:</span><span class="sxs-lookup"><span data-stu-id="3273b-145">hello example below does an infinite loop and processes messages as they arrive into our `TestQueue`:</span></span>

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
            // Display hello queue message.
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
            // Added toohandle no more messages.
            // Could instead wait for more messages toobe added.
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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a><span data-ttu-id="3273b-146">Hoe toohandle toepassing is vastgelopen en onleesbare berichten</span><span class="sxs-lookup"><span data-stu-id="3273b-146">How toohandle application crashes and unreadable messages</span></span>
<span data-ttu-id="3273b-147">Service Bus biedt functionaliteit toohelp die u netjes te herstellen bij fouten in uw toepassing of problemen bij het verwerken van een bericht.</span><span class="sxs-lookup"><span data-stu-id="3273b-147">Service Bus provides functionality toohelp you gracefully recover from errors in your application or difficulties processing a message.</span></span> <span data-ttu-id="3273b-148">Als een ontvangende toepassing niet kan tooprocess hello bericht voor een bepaalde reden en vervolgens kan worden aangeroepen Hallo **unlockMessage** methode voor het ontvangen Hallo-bericht (in plaats van Hallo **deleteMessage** methode).</span><span class="sxs-lookup"><span data-stu-id="3273b-148">If a receiver application is unable tooprocess hello message for some reason, then it can call hello **unlockMessage** method on hello received message (instead of hello **deleteMessage** method).</span></span> <span data-ttu-id="3273b-149">Deze tot gevolg dat het Service Bus toounlock Hallo in wachtrij Hallo-bericht, waardoor het beschikbaar toobe ontvangen, Hallo ofwel door dezelfde toepassing of door een andere consumerende toepassing verbruikt.</span><span class="sxs-lookup"><span data-stu-id="3273b-149">This causes Service Bus toounlock hello message within hello queue and make it available toobe received again, either by hello same consuming application or by another consuming application.</span></span>

<span data-ttu-id="3273b-150">Daarnaast is er een time-out gekoppeld aan een bericht in de wachtrij is vergrendeld en als de toepassing hello tooprocess mislukt Hallo bericht voordat de time-out van de vergrendeling verloopt (bijvoorbeeld als Hallo toepassing vastloopt) en Service Bus automatisch Hiermee ontgrendelt u het Hallo-bericht en maakt het beschikbaar toobe opnieuw ontvangen.</span><span class="sxs-lookup"><span data-stu-id="3273b-150">There is also a timeout associated with a message locked within the queue, and if hello application fails tooprocess hello message before the lock timeout expires (for example, if hello application crashes), then Service Bus unlocks hello message automatically and makes it available toobe received again.</span></span>

<span data-ttu-id="3273b-151">In Hallo gebeurtenis die toepassing hello vastgelopen na het verwerken van het Hallo-bericht, maar voordat u Hallo **deleteMessage** verzoek is uitgegeven, dan is het Hallo-bericht opnieuw bezorgd toohello toepassing opnieuw wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="3273b-151">In hello event that hello application crashes after processing hello message but before hello **deleteMessage** request is issued, then hello message is redelivered toohello application when it restarts.</span></span> <span data-ttu-id="3273b-152">Dit wordt vaak genoemd *tenminste eenmaal verwerken*; dat wil zeggen dat elk bericht ten minste één keer wordt verwerkt maar in bepaalde situaties Hallo hetzelfde bericht opnieuw kan worden bezorgd.</span><span class="sxs-lookup"><span data-stu-id="3273b-152">This is often called *At Least Once Processing*; that is, each message is processed at least once but in certain situations hello same message may be redelivered.</span></span> <span data-ttu-id="3273b-153">Als Hallo scenario kan geen dubbele verwerking tolereren, moeten toepassingsontwikkelaars levering van aanvullende logica tootheir toepassing toohandle dubbele berichten toevoegen.</span><span class="sxs-lookup"><span data-stu-id="3273b-153">If hello scenario cannot tolerate duplicate processing, then application developers should add additional logic tootheir application toohandle duplicate message delivery.</span></span> <span data-ttu-id="3273b-154">Dit wordt vaak bereikt met behulp van Hallo **getMessageId** methode voor het Hallo-bericht dat gelijk blijft bij meerdere bezorgingspogingen.</span><span class="sxs-lookup"><span data-stu-id="3273b-154">This is often achieved using hello **getMessageId** method of hello message, which remains constant across delivery attempts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3273b-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3273b-155">Next Steps</span></span>
<span data-ttu-id="3273b-156">Nu u Hallo basisprincipes van Service Bus-wachtrijen hebt geleerd, gaat u naar [wachtrijen, onderwerpen en abonnementen] [ Queues, topics, and subscriptions] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3273b-156">Now that you've learned hello basics of Service Bus queues, see [Queues, topics, and subscriptions][Queues, topics, and subscriptions] for more information.</span></span>

<span data-ttu-id="3273b-157">Zie voor meer informatie, Hallo [Java Developer Center](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="3273b-157">For more information, see hello [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh694271.aspx
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
