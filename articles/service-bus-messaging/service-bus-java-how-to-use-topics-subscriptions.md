---
title: aaaHow toouse Azure Service Bus-onderwerpen met Java | Microsoft Docs
description: Service Bus-onderwerpen en abonnementen in Azure gebruiken.
services: service-bus-messaging
documentationcenter: java
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 63d6c8bd-8a22-4292-befc-545ffb52e8eb
ms.service: service-bus-messaging
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 1aad16fdb5d68a5782b85c8dfda9d695babd57ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-service-bus-topics-and-subscriptions-with-java"></a>Hoe toouse Service Bus-onderwerpen en abonnementen met Java

[!INCLUDE [service-bus-selector-topics](../../includes/service-bus-selector-topics.md)]

Deze handleiding wordt beschreven hoe toouse Service Bus-onderwerpen en abonnementen. Hallo-voorbeelden zijn geschreven in Java en gebruiken van Hallo [Azure SDK voor Java][Azure SDK for Java]. Hallo scenario's worden behandeld: **maken van onderwerpen en abonnementen**, **maken van abonnementsfilters**, **verzenden van berichten tooa onderwerp**, **ontvangen berichten van een abonnement**, en **verwijderen van onderwerpen en abonnementen**.

## <a name="what-are-service-bus-topics-and-subscriptions"></a>Wat zijn Service Bus-onderwerpen en -abonnementen?
Service Bus-onderwerpen en -abonnementen bieden ondersteuning voor een berichtencommunicatiemodel op basis van *publiceren/abonneren*. Wanneer u gebruikmaakt van onderwerpen en abonnementen, communiceren onderdelen van een gedistribueerde toepassing niet direct met elkaar. In plaats daarvan wisselen ze berichten uit via een onderwerp dat als intermediair fungeert.

![TopicConcepts](./media/service-bus-java-how-to-use-topics-subscriptions/sb-topics-01.png)

Anders dan bij Service Bus-wachtrijen, waarin elk bericht door een enkele gebruiker wordt verwerkt, bieden onderwerpen en abonnementen een 'één-naar-veel'-communicatiewijze, waarbij een patroon voor publiceren/abonneren wordt gebruikt. Het is mogelijk meerdere abonnementen tooa onderwerp registreren. Wanneer een bericht wordt verzonden tooa onderwerp, wordt deze beschikbaar tooeach abonnement toohandle/proces vervolgens afzonderlijk gemaakt.

Een abonnement tooa onderwerp lijkt op een virtuele wachtrij die kopieën van Hallo-berichten dat is verzonden toohello onderwerp ontvangt. U kunt eventueel registreren filterregels voor een onderwerp op basis van per abonnement, waarmee u kunt toofilter of te beperken welke berichten tooa onderwerp door welke onderwerpabonnementen worden ontvangen.

Service Bus-onderwerpen en abonnementen kunnen u tooscale tooprocess een zeer groot aantal berichten via een zeer groot aantal gebruikers en toepassingen.

## <a name="create-a-service-namespace"></a>Een servicenaamruimte maken
toobegin met Service Bus-onderwerpen en abonnementen in Azure, moet u eerst een naamruimte een scoping container biedt voor het adresseren van Service Bus-resources in uw toepassing te maken.

een naamruimte toocreate:

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

## <a name="configure-your-application-toouse-service-bus"></a>Configureren van uw toepassing toouse Service Bus
Zorg ervoor dat u hebt geïnstalleerd Hallo [Azure SDK voor Java] [ Azure SDK for Java] voordat u dit voorbeeld maakt. Als u Eclipse gebruikt, kunt u Hallo installeren [Azure Toolkit voor Eclipse] [ Azure Toolkit for Eclipse] die hello Azure SDK voor Java bevat. Vervolgens kunt u toevoegen Hallo **Microsoft Azure-beheerbibliotheken voor Java** tooyour project:

![](media/service-bus-java-how-to-use-topics-subscriptions/eclipselibs.png)

Voeg de volgende Hallo `import` instructies toohello boven in Hallo Java-bestand:

```java
import com.microsoft.windowsazure.services.servicebus.*;
import com.microsoft.windowsazure.services.servicebus.models.*;
import com.microsoft.windowsazure.core.*;
import javax.xml.datatype.*;
```

Hello Azure-beheerbibliotheken voor Java tooyour pad maken en deze opnemen in uw project implementatie assembly toevoegen.

## <a name="create-a-topic"></a>Een onderwerp maken
Beheerbewerkingen voor Service Bus-onderwerpen kunnen worden uitgevoerd via de **ServiceBusContract** klasse. Een **ServiceBusContract** object is gemaakt met een juiste configuratie die door de SAS-token met machtigingen toomanage ingekapseld en Hallo **ServiceBusContract** klasse is de enige punt Hallo communicatie met Azure.

Hallo **ServiceBusService** klasse biedt methoden toocreate, opsommen en verwijderen van onderwerpen. Hallo volgende voorbeeld ziet u hoe een **ServiceBusService** -object dat wordt gebruikt toocreate een onderwerp met de naam `TestTopic`, met een naamruimte aangeroepen `HowToSample`:

```java
Configuration config =
    ServiceBusConfiguration.configureWithSASAuthentication(
      "HowToSample",
      "RootManageSharedAccessKey",
      "SAS_key_value",
      ".servicebus.windows.net"
      );

ServiceBusContract service = ServiceBusService.create(config);
TopicInfo topicInfo = new TopicInfo("TestTopic");
try  
{
    CreateTopicResult result = service.createTopic(topicInfo);
}
catch (ServiceException e) {
    System.out.print("ServiceException encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

Er zijn methoden op **TopicInfo** waarmee de eigenschappen van Hallo onderwerp moet worden ingesteld (bijvoorbeeld: tooset Hallo standaard time-to-live (TTL) waarde toobe toegepast toomessages toohello onderwerp verzonden). Hallo volgende voorbeeld laat zien hoe toocreate een onderwerp met de naam `TestTopic` met een maximale grootte van 5 GB:

```java
long maxSizeInMegabytes = 5120;  
TopicInfo topicInfo = new TopicInfo("TestTopic");  
topicInfo.setMaxSizeInMegabytes(maxSizeInMegabytes);
CreateTopicResult result = service.createTopic(topicInfo);
```

Dat kunt u gebruikmaken van Hallo **listTopics** methode op **ServiceBusContract** toocheck objecten als een onderwerp met een opgegeven naam al in een Servicenaamruimte bestaat.

## <a name="create-subscriptions"></a>Abonnementen maken
Abonnementen tootopics tevens zijn gemaakt met de Hallo **ServiceBusService** klasse. Abonnementen kunnen worden genoemd en een optioneel filter waarmee Hallo verzameling virtuele wachtrij van het abonnement toohello doorgegeven berichten wordt beperkt.

### <a name="create-a-subscription-with-hello-default-matchall-filter"></a>Een abonnement maken met de Hallo standaardfilter (MatchAll)
Hallo **MatchAll** filter is Hallo standaardfilter dat wordt gebruikt als geen filter is opgegeven als een nieuw abonnement wordt gemaakt. Wanneer Hallo **MatchAll** filter wordt gebruikt, worden alle berichten gepubliceerde toohello onderwerp in de virtuele wachtrij van het abonnement geplaatst. Hallo volgende voorbeeld wordt een abonnement genaamd 'AllMessages' en gebruikt standaard Hallo **MatchAll** filter.

```java
SubscriptionInfo subInfo = new SubscriptionInfo("AllMessages");
CreateSubscriptionResult result =
    service.createSubscription("TestTopic", subInfo);
```

### <a name="create-subscriptions-with-filters"></a>Abonnementen met filters maken
U kunt filters waarmee u kunt ook welke berichten verzonden tooa onderwerp weergegeven binnen een bepaald onderwerpabonnement tooscope maken.

Hallo meest flexibele type filter dat wordt ondersteund door abonnementen is de [SqlFilter][SqlFilter], waarmee een subset van SQL92 wordt geïmplementeerd implementeert. SQL-filters worden uitgevoerd op Hallo eigenschappen van Hallo-berichten die gepubliceerd toohello onderwerp zijn. Bekijk voor meer informatie over Hallo expressies die kunnen worden gebruikt met een SQL-filter Hallo [SqlFilter.SqlExpression] [ SqlFilter.SqlExpression] syntaxis.

Hallo volgende voorbeeld maakt u een abonnement met de naam `HighMessages` met een [SqlFilter] [ SqlFilter] -object dat alleen berichten selecteert die een aangepaste **MessageNumber** de eigenschap is groter dan 3:

```java
// Create a "HighMessages" filtered subscription  
SubscriptionInfo subInfo = new SubscriptionInfo("HighMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleGT3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber > 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "HighMessages", ruleInfo);
// Delete hello default rule, otherwise hello new rule won't be invoked.
service.deleteRule("TestTopic", "HighMessages", "$Default");
```

Op deze manier hello volgende voorbeeld maakt u een abonnement met de naam `LowMessages` met een [SqlFilter] [ SqlFilter] -object dat alleen berichten selecteert die een **MessageNumber** eigenschap kleiner dan of gelijk too3:

```java
// Create a "LowMessages" filtered subscription
SubscriptionInfo subInfo = new SubscriptionInfo("LowMessages");
CreateSubscriptionResult result = service.createSubscription("TestTopic", subInfo);
RuleInfo ruleInfo = new RuleInfo("myRuleLE3");
ruleInfo = ruleInfo.withSqlExpressionFilter("MessageNumber <= 3");
CreateRuleResult ruleResult = service.createRule("TestTopic", "LowMessages", ruleInfo);
// Delete hello default rule, otherwise hello new rule won't be invoked.
service.deleteRule("TestTopic", "LowMessages", "$Default");
```

Wanneer een bericht nu te verzonden`TestTopic`, het altijd bezorgd tooreceivers geabonneerd toohello `AllMessages` abonnement en selectief bezorgd tooreceivers geabonneerd toohello `HighMessages` en `LowMessages` (abonnementen afhankelijk van de inhoud van het bericht).

## <a name="send-messages-tooa-topic"></a>Verzenden van berichten tooa onderwerp
een bericht tooa Service Bus-onderwerp toosend, beheersbaarheid voor uw toepassing een **ServiceBusContract** object. Hallo volgende code laat zien hoe een bericht voor Hallo toosend `TestTopic` onderwerp eerder hebt gemaakt in Hallo `HowToSample` naamruimte:

```java
BrokeredMessage message = new BrokeredMessage("MyMessage");
service.sendTopicMessage("TestTopic", message);
```

Berichten tooService Bus-onderwerpen, zijn exemplaren van de [BrokeredMessage] [ BrokeredMessage] klasse. [BrokeredMessage][BrokeredMessage]* objecten hebben een aantal standaardmethoden (zoals **setLabel** en **TimeToLive**), een woordenlijst die wordt gebruikt toohold aangepaste toepassingsspecifieke eigenschappen en een hoofdtekst met willekeurige toepassingsgegevens. Een toepassing kunt Hallo hoofdtekst van het bericht instellen door elk serialiseerbaar object doorgeven aan de constructor Hallo van de [BrokeredMessage][BrokeredMessage], en de juiste Hallo **DataContractSerializer**  gebruikte tooserialize Hallo object zijn. U kunt ook een **java.io.InputStream** kan worden opgegeven.

Hallo volgende voorbeeld toont hoe vijf toosend test toothe berichten `TestTopic` **MessageSender** we verkregen in de bovenstaande Hallo codefragment.
Opmerking hoe Hallo **MessageNumber** eigenschapswaarde van elk bericht varieert op Hallo herhaling van Hallo lus (dit wordt bepaald welke abonnementen ontvangen):

```java
for (int i=0; i<5; i++)  {
// Create message, passing a string message for hello body
BrokeredMessage message = new BrokeredMessage("Test message " + i);
// Set some additional custom app-specific property
message.setProperty("MessageNumber", i);
// Send message toohello topic
service.sendTopicMessage("TestTopic", message);
}
```

Service Bus-onderwerpen ondersteunen een maximale berichtgrootte van 256 KB in Hallo [standaardcategorie](service-bus-premium-messaging.md) en 1 MB in Hallo [Premium-laag](service-bus-premium-messaging.md). Hallo-kop, die standaard Hallo- en aangepaste toepassingseigenschappen bevat, kan een maximale grootte van 64 KB hebben. Er is geen limiet voor het aantal berichten in een onderwerp hello, maar er is een limiet op de totale grootte van berichten in een onderwerp Hallo Hallo. De grootte van het onderwerp wordt gedefinieerd tijdens het maken, met een bovengrens van 5 GB.

## <a name="how-tooreceive-messages-from-a-subscription"></a>Hoe tooreceive berichten van een abonnement
tooreceive berichten van een abonnement gebruiken een **ServiceBusContract** object. Ontvangen berichten kunnen werken in twee verschillende modi: **ReceiveAndDelete** en **PeekLock**.

Bij gebruik van Hallo **ReceiveAndDelete** -modus ontvangt een enkele bewerking - dat wil zeggen, wanneer Service Bus een leesaanvraag voor een bericht ontvangt, wordt gemarkeerd als verbruikt het Hallo-bericht en retourneert het toothe toepassing. **ReceiveAndDelete** modus is Hallo eenvoudigste model en werkt het beste voor scenario's waarin een toepassing kan tolereren niet verwerken van een bericht in de gebeurtenis Hallo van een fout. toounderstand dit, Neem bijvoorbeeld een scenario in welke problemen van de consument Hallo Hallo aanvraag ontvangen en vervolgens vastloopt voordat het wordt verwerkt. Omdat Service Bus het bericht als verbruikt, vervolgens wanneer Hallo toepassing opnieuw wordt opgestart en verbruik van berichten opnieuw begint heeft gemarkeerd, ontbreekt het Hallo-bericht dat was voorafgaande toohello crash verbruikt.

In **PeekLock** -modus ontvangt, wordt een bewerking met twee fasen, waardoor het mogelijk toosupport toepassingen die geen ontbrekende berichten kunnen tolereren. Wanneer Service Bus een aanvraag ontvangt, zoeken naar het volgende bericht toobe Hallo verbruikt, wordt vergrendeld tooprevent andere consumenten het ontvangen en retourneert vervolgens toohello toepassing. Nadat de toepassing hello klaar is met verwerking van het Hallo-bericht (of veilig heeft opgeslagen voor toekomstige verwerking), is de tweede fase Hallo Hallo voltooid proces ontvangen door het aanroepen van **verwijderen** op Hallo ontvangen bericht. Wanneer Service Bus de aanroep Hallo **verwijderen** aanroep, wordt het Hallo-bericht als verbruikt markeren en verwijderen uit het Hallo-onderwerp.

Hallo in het volgende voorbeeld laat zien hoe berichten kunnen worden ontvangen en verwerkt met behulp **PeekLock** modus (geen Hallo standaardmodus). Hallo in het volgende voorbeeld wordt een lus uitgevoerd en verwerkt berichten in Hallo 'HighMessages' abonnement en vervolgens afgesloten wanneer er geen berichten meer zijn (u kunt ook deze kan worden ingesteld toowait op nieuwe berichten).

```java
try
{
    ReceiveMessageOptions opts = ReceiveMessageOptions.DEFAULT;
    opts.setReceiveMode(ReceiveMode.PEEK_LOCK);

    while(true)  {
        ReceiveSubscriptionMessageResult  resultSubMsg =
            service.receiveSubscriptionMessage("TestTopic", "HighMessages", opts);
        BrokeredMessage message = resultSubMsg.getValue();
        if (message != null && message.getMessageId() != null)
        {
            System.out.println("MessageID: " + message.getMessageId());
            // Display hello topic message.
            System.out.print("From topic: ");
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
                message.getProperty("MessageNumber"));
            // Delete message.
            System.out.println("Deleting this message.");
            service.deleteMessage(message);
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
Service Bus biedt functionaliteit toohelp die u netjes te herstellen bij fouten in uw toepassing of problemen bij het verwerken van een bericht. Als een ontvangende toepassing niet kan tooprocess hello bericht voor een bepaalde reden en vervolgens kan worden aangeroepen Hallo **unlockMessage** methode voor het ontvangen Hallo-bericht (in plaats van Hallo **deleteMessage** methode). Hierdoor wordt ervoor zorgen dat Service Bus toounlock Hallo-bericht Hallo onderwerp en beschikbaar toobe opnieuw ontvangen, ofwel Hallo door dezelfde toepassing of door een andere consumerende toepassing verbruikt.

Daarnaast is er een time-out gekoppeld aan een bericht in het onderwerp is vergrendeld en als Hallo toepassing tooprocess Hallo-bericht voordat mislukt de time-out van de vergrendeling verloopt (bijvoorbeeld als Hallo toepassing vastloopt), en vervolgens de Service Bus wordt het Hallo-bericht automatisch ontgrendelen en het beschikbaar toobe ontvangen opnieuw maken.

In Hallo gebeurtenis die toepassing hello vastgelopen na het verwerken van het Hallo-bericht, maar voordat u Hallo **deleteMessage** verzoek is uitgegeven, is het Hallo-bericht altijd opnieuw bezorgd toohello toepassing opnieuw wordt gestart. Dit wordt vaak genoemd **tenminste eenmaal verwerken**, dat wil zeggen elk bericht ten minste één keer wordt verwerkt maar in bepaalde situaties Hallo hetzelfde bericht opnieuw kan worden bezorgd. Als Hallo scenario kan geen dubbele verwerking tolereren, moeten toepassingsontwikkelaars levering van aanvullende logica tootheir toepassing toohandle dubbele berichten toevoegen. Dit wordt vaak bereikt met behulp van Hallo **getMessageId** methode van Hallo-bericht dat gelijk bij meerdere bezorgingspogingen blijft.

## <a name="delete-topics-and-subscriptions"></a>Onderwerpen en abonnementen verwijderen
Hallo primaire manier toodelete onderwerpen en abonnementen is toouse een **ServiceBusContract** object. Als u een onderwerp verwijdert, verwijdert ook alle abonnementen die zijn geregistreerd bij Hallo onderwerp. Abonnementen kunnen ook afzonderlijk worden verwijderd.

```java
// Delete subscriptions
service.deleteSubscription("TestTopic", "AllMessages");
service.deleteSubscription("TestTopic", "HighMessages");
service.deleteSubscription("TestTopic", "LowMessages");

// Delete a topic
service.deleteTopic("TestTopic");
```

## <a name="next-steps"></a>Volgende stappen
Nu u Hallo basisprincipes van Service Bus-wachtrijen hebt geleerd, gaat u naar [Service Bus-wachtrijen, onderwerpen en abonnementen] [ Service Bus queues, topics, and subscriptions] voor meer informatie.

[Azure SDK for Java]: http://azure.microsoft.com/develop/java/
[Azure Toolkit for Eclipse]: ../azure-toolkit-for-eclipse.md
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md
[SqlFilter]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter 
[SqlFilter.SqlExpression]: /dotnet/api/microsoft.servicebus.messaging.sqlfilter#Microsoft_ServiceBus_Messaging_SqlFilter_SqlExpression
[BrokeredMessage]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage

[0]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-13.png
[2]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-04.png
[3]: ./media/service-bus-java-how-to-use-topics-subscriptions/sb-queues-09.png
