---
title: aaaOverview van Azure Service Bus-wachtrijen, onderwerpen en abonnementen messaging | Microsoft Docs
description: Overzicht van Service Bus-berichtentiteiten.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a306ced4-74e9-47c6-990a-d9c47efa31d5
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/28/2017
ms.author: sethm
ms.openlocfilehash: 73135d2658e341c14dbb114ab938faed91578ff1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-queues-topics-and-subscriptions"></a>Service Bus-wachtrijen, -onderwerpen en -abonnementen

Microsoft Azure Service Bus ondersteunt een set van cloud-gebaseerde, bericht georiënteerd middleware-technologieën waaronder betrouwbare message Queuing- en duurzame publiceren/abonneren messaging. Deze 'brokered' messaging mogelijkheden kunnen worden beschouwd als ontkoppelde messaging-functies die ondersteuning voor publiceren / abonneren, tijdelijke ontkoppeling en scenario's met behulp van Hallo Service Bus messaging-infrastructuur voor taakverdeling. Ontkoppelde communicatie heeft veel voordelen; clients en servers kunnen bijvoorbeeld naar behoefte verbinding maken en hun bewerkingen asynchroon uitvoeren.

Hallo-berichtentiteiten die Hallo core Hallo mogelijkheden in Service Bus-berichtenservice vormen zijn wachtrijen, onderwerpen en abonnementen en regels/acties.

## <a name="queues"></a>Wachtrijen

Wachtrijen bieden *First In, First Out* (FIFO-principe) message delivery tooone of meer concurrerende consumenten. Dat wil zeggen zijn berichten meestal verwachte toobe ontvangen en verwerkt door de ontvangers Hallo in Hallo volgorde waarin ze zijn toohello wachtrij toegevoegd en elk bericht wordt ontvangen en verwerkt door slechts één berichtconsument. Een belangrijk voordeel van het gebruik van wachtrijen is tooachieve 'tijdelijke ontkoppeling' van de onderdelen van toepassing. Met andere woorden, Hallo producenten (afzenders) en consumenten (ontvangers) hebben geen toobe verzenden en ontvangen van berichten op Hallo dezelfde tijd, omdat berichten blijvend worden opgeslagen in de wachtrij Hallo. Bovendien Hallo producent geen toowait op een antwoord van de consumer Hallo in volgorde toocontinue tooprocess en berichten verzenden.

Een bijkomend voordeel is 'load leveling,' waardoor producenten en consumenten toosend kunt en ontvangen berichten met verschillende snelheden. In veel toepassingen varieert de systeembelasting Hallo gedurende een bepaalde periode; Er is echter Hallo benodigde verwerkingstijd voor elke werkeenheid doorgaans constant blijft. Tussen bericht producenten en consumenten met een wachtrij betekent dit dat alleen de toepassing verbruikt Hallo toobe ingerichte toobe kunnen toohandle gemiddelde belasting in plaats van piekbelasting. Hallo diepte van Hallo wachtrij neemt toe of af als de inkomende belasting Hallo varieert. Dit bespaart geld rechtstreeks met inachtneming van toohello hoeveelheid infrastructuur vereist tooservice Hallo toepassing werklast. Als Hallo verkeer toeneemt, meer werkprocessen kunnen toegevoegde tooread uit Hallo wachtrij. Elk bericht wordt verwerkt door slechts één van de werkprocessen Hallo. Bovendien kunt deze pull-gebaseerde taakverdeling optimaal gebruik van Hallo worker computers zelfs als Hallo worker computers met inachtneming van tooprocessing power verschillen, zoals ze op eigen maximale snelheid berichten ophalen. Dit patroon wordt vaak aangeduid als 'concurrerende consumenten' Hallo-patroon.

Met behulp van wachtrijen toointermediate tussen bericht producenten en consumenten biedt een inherente losse koppeling tussen Hallo-onderdelen. Omdat producenten en consumenten niet op de hoogte van elkaar zijn, kan een gebruiker zonder gevolgen voor de producent Hallo worden bijgewerkt.

Maken van een wachtrij is een proces met meerdere stappen. Uitvoeren van beheerbewerkingen voor Service Bus-berichtentiteiten (wachtrijen en onderwerpen) via Hallo [Microsoft.ServiceBus.NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) klasse, die is samengesteld door het basisadres van Service Bus Hallo Hallo opgeven naamruimte en het Hallo-gebruikersreferenties. [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) biedt methoden toocreate, opsommen en verwijderen van de messaging-entiteiten. Na het maken van een [Microsoft.ServiceBus.TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) object uit Hallo SAS-naam en sleutel en een naamruimte service management-object, kunt u Hallo [Microsoft.ServiceBus.NamespaceManager.CreateQueue](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateQueue_System_String_) methode toocreate Hallo wachtrij. Bijvoorbeeld:

```csharp
// Create management credentials
TokenProvider credentials = TokenProvider.CreateSharedAccessSignatureTokenProvider(sasKeyName,sasKeyValue);
// Create namespace client
NamespaceManager namespaceClient = new NamespaceManager(ServiceBusEnvironment.CreateServiceUri("sb", ServiceNamespace, string.Empty), credentials);
```

U kunt vervolgens een object in de wachtrij en een messagingfactory maken met de Hallo Service Bus-URI als argument. Bijvoorbeeld:

```csharp
QueueDescription myQueue;
myQueue = namespaceClient.CreateQueue("TestQueue");
MessagingFactory factory = MessagingFactory.Create(ServiceBusEnvironment.CreateServiceUri("sb", ServiceNamespace, string.Empty), credentials); 
QueueClient myQueueClient = factory.CreateQueueClient("TestQueue");
```

Vervolgens kunt u berichten toohello wachtrij verzenden. Bijvoorbeeld, als u een lijst met brokered berichten aangeroepen hebt `MessageList`, Hallo code vergelijkbare toohello volgende weergegeven:

```csharp
for (int count = 0; count < 6; count++)
{
    var issue = MessageList[count];
    issue.Label = issue.Properties["IssueTitle"].ToString();
    myQueueClient.Send(issue);
}
```

U ontvangt vervolgens berichten uit de wachtrij Hallo als volgt:

```csharp
while ((message = myQueueClient.Receive(new TimeSpan(hours: 0, minutes: 0, seconds: 5))) != null)
    {
        Console.WriteLine(string.Format("Message received: {0}, {1}, {2}", message.SequenceNumber, message.Label, message.MessageId));
        message.Complete();

        Console.WriteLine("Processing message (sleeping...)");
        Thread.Sleep(1000);
    }
```

In Hallo [ReceiveAndDelete](/dotnet/api/microsoft.servicebus.messaging.receivemode) modus Hallo ontvangen bewerking is één; dat wil zeggen als Service Bus Hallo aanvraag ontvangt, wordt gemarkeerd als verbruikt het Hallo-bericht en retourneert het toohello toepassing. **ReceiveAndDelete** modus is Hallo eenvoudigste model en werkt het beste voor scenario's in welke Hallo toepassing kan tolereren niet verwerken van een bericht in de gebeurtenis Hallo van een fout. toounderstand dit, Neem bijvoorbeeld een scenario in welke problemen van de consument Hallo Hallo aanvraag ontvangen en vervolgens vastloopt voordat het wordt verwerkt. Omdat Service Bus is gemarkeerd als verbruikt, wanneer Hallo toepassing opnieuw wordt opgestart en verbruik van berichten opnieuw begint het Hallo-bericht, ontbreekt het Hallo-bericht dat was voorafgaande toohello crash verbruikt.

In [PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) modus Hallo ontvangen bewerking verandert in twee fasen, waardoor het mogelijk toosupport toepassingen die geen ontbrekende berichten kunnen tolereren. Als Service Bus Hallo aanvraag ontvangt, het Hallo volgende bericht toobe verbruikt wordt gevonden, vergrendeld tooprevent andere consumenten ontvangen, en retourneert vervolgens toohello toepassing. Nadat de toepassing hello klaar is met verwerking van het Hallo-bericht (of veilig heeft opgeslagen voor toekomstige verwerking), is de tweede fase Hallo Hallo voltooid proces ontvangen door het aanroepen van [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) op Hallo ontvangen bericht. Wanneer Service Bus de aanroep Hallo **Complete** aanroep, worden gemarkeerd als verbruikt het Hallo-bericht.

Als de toepassing hello kan tooprocess Hallo bericht voor een bepaalde reden, Hallo kan worden aangeroepen [afbreken](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) methode voor het ontvangen Hallo-bericht (in plaats van [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)). Dit kunt Service Bus toounlock Hallo-bericht en kunt u de beschikbare toobe opnieuw ontvangen, ofwel door dezelfde gebruiker Hallo of door een andere concurrerend consumenten. Ten tweede, er is een time-out gekoppeld Hallo vergrendelen en als de toepassing hello tooprocess mislukt Hallo bericht voordat de time-out van de vergrendeling Hallo verloopt (bijvoorbeeld als Hallo toepassing vastloopt), en vervolgens het Hallo-bericht ontgrendelt met een Service Bus en het beschikbaar toobe maakt opnieuw ontvangen (in wezen uitvoeren van een [afbreken](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) bewerking standaard).

Houd er rekening mee dat in Hallo gebeurtenis die Hallo van toepassing is vastgelopen na het verwerken van het Hallo-bericht, maar voordat Hallo **Complete** verzoek is uitgegeven, wordt het Hallo-bericht is opnieuw bezorgd toohello toepassing opnieuw wordt gestart. Dit wordt vaak genoemd *tenminste eenmaal* verwerking; dat wil zeggen, elk bericht ten minste één keer wordt verwerkt. Echter, in bepaalde situaties Hallo hetzelfde bericht opnieuw kan worden bezorgd. Als Hallo scenario kan geen dubbele verwerking tolereren en vervolgens extra logica is vereist in Hallo toepassing toodetect duplicaten die kunnen worden bereikt op basis van Hallo **MessageId** eigenschap van het Hallo-bericht dat gelijk blijft bij een constante meerdere bezorgingspogingen. Dit staat bekend als *exact één keer* verwerken.

## <a name="topics-and-subscriptions"></a>Onderwerpen en abonnementen
In contrast tooqueues, waarin elk bericht wordt verwerkt door een enkele gebruiker *onderwerpen* en *abonnementen* biedt een een-op-veel-vorm van communicatie, in een *publiceren/abonneren* patroon. Kan handig zijn voor het schalen van grote aantallen ontvangers toovery, elk gepubliceerde bericht bestaat beschikbaar tooeach abonnement geregistreerd bij Hallo onderwerp. Berichten worden verzonden tooa onderwerp en geleverde tooone of meer gekoppelde abonnementen, afhankelijk van filterregels kunnen worden ingesteld op basis van per abonnement. Hallo abonnementen kunnen meer filters toorestrict Hallo-berichten dat ze tooreceive wilt gebruiken. Berichten worden verzonden tooa onderwerp in Hallo dezelfde manier waarop ze worden verzonden tooa wachtrij, maar berichten worden niet ontvangen van Hallo onderwerp rechtstreeks. In plaats daarvan worden ze ontvangen van abonnementen. Het onderwerpabonnement van een lijkt op een virtuele wachtrij die kopieën van Hallo-berichten die worden verzonden toohello onderwerp ontvangt. Berichten worden ontvangen van een abonnement identiek toohello manier waarop ze worden ontvangen van een wachtrij.

Ter vergelijking, Hallo-bericht verzenden functionaliteit van een wachtrij toegewezen rechtstreeks tooa onderwerp en de functionaliteit hiervan bericht ontvangen tooa abonnement wordt toegewezen. Onder andere betekent dit dat abonnementen Hallo dezelfde patronen eerder in deze sectie met inachtneming van tooqueues beschreven ondersteunen: concurrerend consumenten, tijdelijke ontkoppeling, load leveling en taakverdeling.

Maken van een onderwerp is vergelijkbaar toocreating een wachtrij, zoals wordt weergegeven in het voorbeeld in de vorige sectie Hallo Hallo. Hallo service URI maken en gebruik vervolgens Hallo [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) klasse toocreate Hallo naamruimte client. Vervolgens kunt u een onderwerp met Hallo maken [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_) methode. Bijvoorbeeld:

```csharp
TopicDescription dataCollectionTopic = namespaceClient.CreateTopic("DataCollectionTopic");
```

Vervolgens voegt u abonnementen naar wens:

```csharp
SubscriptionDescription myAgentSubscription = namespaceClient.CreateSubscription(myTopic.Path, "Inventory");
SubscriptionDescription myAuditSubscription = namespaceClient.CreateSubscription(myTopic.Path, "Dashboard");
```

Vervolgens kunt u een client onderwerp maken. Bijvoorbeeld:

```csharp
MessagingFactory factory = MessagingFactory.Create(serviceUri, tokenProvider);
TopicClient myTopicClient = factory.CreateTopicClient(myTopic.Path)
```

Met behulp van de afzender Hallo-bericht, kunt u verzenden en ontvangen berichten tooand van Hallo onderwerp, zoals wordt weergegeven in de vorige sectie Hallo. Bijvoorbeeld:

```csharp
foreach (BrokeredMessage message in messageList)
{
    myTopicClient.Send(message);
    Console.WriteLine(
    string.Format("Message sent: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
}
```

Vergelijkbare tooqueues, berichten worden ontvangen van een abonnement met een [SubscriptionClient](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient) object in plaats van een [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) object. Hallo abonnement client doorgeeft Hallo-naam van onderwerp Hallo Hallo-naam van het Hallo-abonnement, maken en (optioneel) Hallo modus ontvangen als parameters. Bijvoorbeeld met Hallo **inventaris** abonnement:

```csharp
// Create hello subscription client
MessagingFactory factory = MessagingFactory.Create(serviceUri, tokenProvider); 

SubscriptionClient agentSubscriptionClient = factory.CreateSubscriptionClient("IssueTrackingTopic", "Inventory", ReceiveMode.PeekLock);
SubscriptionClient auditSubscriptionClient = factory.CreateSubscriptionClient("IssueTrackingTopic", "Dashboard", ReceiveMode.ReceiveAndDelete); 

while ((message = agentSubscriptionClient.Receive(TimeSpan.FromSeconds(5))) != null)
{
    Console.WriteLine("\nReceiving message from Inventory...");
    Console.WriteLine(string.Format("Message received: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
    message.Complete();
}          

// Create a receiver using ReceiveAndDelete mode
while ((message = auditSubscriptionClient.Receive(TimeSpan.FromSeconds(5))) != null)
{
    Console.WriteLine("\nReceiving message from Dashboard...");
    Console.WriteLine(string.Format("Message received: Id = {0}, Body = {1}", message.MessageId, message.GetBody<string>()));
}
```

### <a name="rules-and-actions"></a>Regels en acties
In veel scenario's, moeten de berichten met specifieke kenmerken op verschillende manieren worden verwerkt. tooenable, kunt u abonnementen toofind berichten die hebben eigenschappen gewenst en voert u de eigenschappen van bepaalde wijzigingen toothose configureren. Bij het Service Bus-abonnementen Zie alle berichten die verstuurd toohello onderwerp, kunt u alleen een subset van deze wachtrij berichten toohello virtuele abonnement kopiëren. Dit wordt bereikt met behulp van abonnementsfilters. Dergelijke wijzigingen worden genoemd *filteren acties*. Wanneer een abonnement is gemaakt, kunt u opgeven dat een filterexpressie die wordt toegepast op Hallo eigenschappen van het Hallo-bericht, beide Systeemeigenschappen Hallo (bijvoorbeeld **Label**) en aangepaste toepassingseigenschappen (bijvoorbeeld **StoreName**.) Hallo filterexpressie SQL is optioneel in dit geval; zonder een filterexpressie SQL wordt geen filteractie gedefinieerd voor een abonnement worden uitgevoerd op alle Hallo-berichten voor dat abonnement.

Met behulp van het vorige voorbeeld hello, toofilter berichten afkomstig is alleen van **Store1**, maakt u Hallo Dashboard abonnement als volgt:

```csharp
namespaceManager.CreateSubscription("IssueTrackingTopic", "Dashboard", new SqlFilter("StoreName = 'Store1'"));
```

Met dit abonnementsfilter aanwezig is, alleen berichten met Hallo `StoreName` eigenschappenset te`Store1` zijn virtuele wachtrij van de gekopieerde toohello voor Hallo `Dashboard` abonnement.

Zie voor meer informatie over mogelijke filterwaarden Hallo-documentatie voor Hallo [SqlFilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter) en [SqlRuleAction](/dotnet/api/microsoft.servicebus.messaging.sqlruleaction) klassen. Zie ook Hallo [Brokered Messaging: geavanceerde Filters](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749) en [onderwerp Filters](https://github.com/Azure-Samples/azure-servicebus-messaging-samples/tree/master/TopicFilters) voorbeelden.

## <a name="next-steps"></a>Volgende stappen
Zie Hallo volgende onderwerpen voor meer informatie over en voorbeelden van het gebruik van Service Bus-berichtenservice geavanceerde.

* [Overzicht van Service Bus-berichten](service-bus-messaging-overview.md)
* [Service Bus Brokered Messaging .NET-zelfstudie](service-bus-brokered-tutorial-dotnet.md)
* [Service Bus brokered messaging REST-zelfstudie](service-bus-brokered-tutorial-rest.md)
* [Onderwerpfilters](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/TopicFilters)
* [Brokered Messaging: Geavanceerde Filters voorbeeld](http://code.msdn.microsoft.com/Brokered-Messaging-6b0d2749)

