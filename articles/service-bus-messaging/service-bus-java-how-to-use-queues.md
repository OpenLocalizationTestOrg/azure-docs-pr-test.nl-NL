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
# <a name="how-toouse-service-bus-queues-with-java"></a>Hoe toouse Service Bus wachtrijen met Java
[!INCLUDE [service-bus-selector-queues](../../includes/service-bus-selector-queues.md)]

Dit artikel wordt beschreven hoe toouse Service Bus-wachtrijen. Hallo-voorbeelden zijn geschreven in Java en gebruiken van Hallo [Azure SDK voor Java][Azure SDK for Java]. Hallo scenario's worden behandeld: **maken van wachtrijen**, **verzenden en ontvangen berichten**, en **verwijderen van wachtrijen**.

[!INCLUDE [howto-service-bus-queues](../../includes/howto-service-bus-queues.md)]

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a>Configureren van uw toepassing toouse Service Bus
Zorg ervoor dat u hebt geïnstalleerd Hallo [Azure SDK voor Java] [ Azure SDK for Java] voordat u dit voorbeeld maakt. Als u Eclipse gebruikt, kunt u Hallo installeren [Azure Toolkit voor Eclipse] [ Azure Toolkit for Eclipse] die hello Azure SDK voor Java bevat. Vervolgens kunt u toevoegen Hallo **Microsoft Azure-beheerbibliotheken voor Java** tooyour project:

![](./media/service-bus-java-how-to-use-queues/eclipselibs.png)

Voeg de volgende Hallo `import` instructies toohello boven in Hallo Java-bestand:

```java
// Include hello following imports toouse Service Bus APIs
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

## <a name="create-a-queue"></a>Een wachtrij maken
Beheerbewerkingen voor Service Bus-wachtrijen kunnen worden uitgevoerd via de **ServiceBusContract** klasse. Een **ServiceBusContract** object is gemaakt met een juiste configuratie die door de SAS-token met machtigingen toomanage ingekapseld en Hallo **ServiceBusContract** klasse is de enige punt Hallo communicatie met Azure.

Hallo **ServiceBusService** klasse biedt methoden toocreate, opsommen en verwijderen van wachtrijen. Hallo voorbeeld hieronder toont hoe een **ServiceBusService** -object dat wordt gebruikt toocreate een wachtrij met de naam `TestQueue`, met een naamruimte met de naam `HowToSample`:

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

Er zijn methoden op `QueueInfo` waarmee de eigenschappen van Hallo wachtrij toobe afgestemd (bijvoorbeeld: tooset Hallo standaard time-to-live (TTL) waarde toobe toegepast toomessages toohello wachtrij verzonden). Hallo volgende voorbeeld laat zien hoe toocreate een wachtrij met de naam `TestQueue` met een maximale grootte van 5 GB:

````java
long maxSizeInMegabytes = 5120;
QueueInfo queueInfo = new QueueInfo("TestQueue");
queueInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateQueueResult result = service.createQueue(queueInfo);
````

Dat kunt u gebruikmaken van Hallo `listQueues` methode op **ServiceBusContract** toocheck objecten als een wachtrij met een opgegeven naam al in een Servicenaamruimte bestaat.

## <a name="send-messages-tooa-queue"></a>Berichten tooa wachtrij verzenden
een bericht tooa Service Bus-wachtrij toosend, beheersbaarheid voor uw toepassing een **ServiceBusContract** object. Hallo van de volgende code toont hoe een bericht voor Hallo toosend `TestQueue` wachtrij eerder hebt gemaakt in Hallo `HowToSample` naamruimte:

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

Berichten worden verzonden naar en ontvangen van Service Bus-wachtrijen, zijn exemplaren van Hallo [BrokeredMessage] [ BrokeredMessage] klasse. [BrokeredMessage] [ BrokeredMessage] objecten hebben een aantal standaardeigenschappen (zoals [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) en [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), een woordenlijst die wordt gebruikt toohold aangepaste toepassingsspecifieke eigenschappen en een hoofdtekst met willekeurige toepassingsgegevens. Een toepassing hello hoofdtekst van het Hallo-bericht kunt instellen door elk serialiseerbaar object doorgeven aan de constructor Hallo Hallo [BrokeredMessage][BrokeredMessage], en de bijbehorende serialisatiefunctie hello wordt vervolgens gebruikt tooserialize Hallo-object. U kunt ook bieden een **java. I/O. InputStream** object.

Hallo volgende voorbeeld toont hoe vijf toosend test toothe berichten `TestQueue` **MessageSender** we in de vorige codefragment Hallo verkregen:

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

Service Bus-wachtrijen ondersteunen een maximale berichtgrootte van 256 KB in Hallo [standaardcategorie](service-bus-premium-messaging.md) en 1 MB in Hallo [Premium-laag](service-bus-premium-messaging.md). Hallo-kop, die standaard Hallo- en aangepaste toepassingseigenschappen bevat, kan een maximale grootte van 64 KB hebben. Er is geen limiet voor het aantal berichten in een wachtrij hello, maar er is een limiet voor de totale grootte van berichten in een wachtrij Hallo Hallo. De grootte van de wachtrij wordt gedefinieerd tijdens het aanmaken, met een bovengrens van 5 GB.

## <a name="receive-messages-from-a-queue"></a>Berichten ontvangen uit een wachtrij
Hallo primaire manier tooreceive berichten uit een wachtrij toouse is een **ServiceBusContract** object. Ontvangen berichten kunnen werken in twee verschillende modi: **ReceiveAndDelete** en **PeekLock**.

Bij gebruik van Hallo **ReceiveAndDelete** -modus ontvangt een enkele bewerking - dat wil zeggen als Service Bus een leesaanvraag voor een bericht in een wachtrij ontvangt, wordt markeert het Hallo-bericht als verbruikt en retourneert het toohello toepassing. **ReceiveAndDelete** modus (dit is de standaardmodus Hallo) is Hallo eenvoudigste model en werkt het beste voor scenario's waarin een toepassing kan tolereren niet verwerken van een bericht in de gebeurtenis Hallo van een fout. toounderstand dit, Neem bijvoorbeeld een scenario in welke problemen van de consument Hallo Hallo aanvraag ontvangen en vervolgens vastloopt voordat het wordt verwerkt.
Omdat Service Bus heeft gemarkeerd als verbruikt, vervolgens wanneer Hallo toepassing opnieuw wordt opgestart en verbruik van berichten opnieuw begint het Hallo-bericht, ontbreekt het Hallo-bericht dat was voorafgaande toohello crash verbruikt.

In **PeekLock** -modus ontvangt, wordt een bewerking met twee fasen, waardoor het mogelijk toosupport toepassingen die geen ontbrekende berichten kunnen tolereren. Wanneer Service Bus een aanvraag ontvangt, zoeken naar het volgende bericht toobe Hallo verbruikt, wordt vergrendeld tooprevent andere consumenten het ontvangen en retourneert vervolgens toohello toepassing. Nadat de toepassing hello klaar is met verwerking van het Hallo-bericht (of veilig heeft opgeslagen voor toekomstige verwerking), is de tweede fase Hallo Hallo voltooid proces ontvangen door het aanroepen van **verwijderen** op Hallo ontvangen bericht. Wanneer Service Bus de aanroep Hallo **verwijderen** aanroep, wordt het Hallo-bericht als verbruikt markeren en verwijderen uit de wachtrij Hallo.

Hallo volgende voorbeeld laat zien hoe berichten kunnen worden ontvangen en verwerkt met behulp **PeekLock** modus (geen Hallo standaardmodus). Hello in het volgende voorbeeld wordt een oneindige lus en verwerkt berichten binnenkomen in onze `TestQueue`:

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

## <a name="how-toohandle-application-crashes-and-unreadable-messages"></a>Hoe toohandle toepassing is vastgelopen en onleesbare berichten
Service Bus biedt functionaliteit toohelp die u netjes te herstellen bij fouten in uw toepassing of problemen bij het verwerken van een bericht. Als een ontvangende toepassing niet kan tooprocess hello bericht voor een bepaalde reden en vervolgens kan worden aangeroepen Hallo **unlockMessage** methode voor het ontvangen Hallo-bericht (in plaats van Hallo **deleteMessage** methode). Deze tot gevolg dat het Service Bus toounlock Hallo in wachtrij Hallo-bericht, waardoor het beschikbaar toobe ontvangen, Hallo ofwel door dezelfde toepassing of door een andere consumerende toepassing verbruikt.

Daarnaast is er een time-out gekoppeld aan een bericht in de wachtrij is vergrendeld en als de toepassing hello tooprocess mislukt Hallo bericht voordat de time-out van de vergrendeling verloopt (bijvoorbeeld als Hallo toepassing vastloopt) en Service Bus automatisch Hiermee ontgrendelt u het Hallo-bericht en maakt het beschikbaar toobe opnieuw ontvangen.

In Hallo gebeurtenis die toepassing hello vastgelopen na het verwerken van het Hallo-bericht, maar voordat u Hallo **deleteMessage** verzoek is uitgegeven, dan is het Hallo-bericht opnieuw bezorgd toohello toepassing opnieuw wordt gestart. Dit wordt vaak genoemd *tenminste eenmaal verwerken*; dat wil zeggen dat elk bericht ten minste één keer wordt verwerkt maar in bepaalde situaties Hallo hetzelfde bericht opnieuw kan worden bezorgd. Als Hallo scenario kan geen dubbele verwerking tolereren, moeten toepassingsontwikkelaars levering van aanvullende logica tootheir toepassing toohandle dubbele berichten toevoegen. Dit wordt vaak bereikt met behulp van Hallo **getMessageId** methode voor het Hallo-bericht dat gelijk blijft bij meerdere bezorgingspogingen.

## <a name="next-steps"></a>Volgende stappen
Nu u Hallo basisprincipes van Service Bus-wachtrijen hebt geleerd, gaat u naar [wachtrijen, onderwerpen en abonnementen] [ Queues, topics, and subscriptions] voor meer informatie.

Zie voor meer informatie, Hallo [Java Developer Center](https://azure.microsoft.com/develop/java/).

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: https://msdn.microsoft.com/library/azure/hh694271.aspx
[Queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage
