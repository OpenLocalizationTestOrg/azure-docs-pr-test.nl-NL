---
title: aaaWrite toepassingen die gebruikmaken van Azure Service Bus-wachtrijen | Microsoft Docs
description: Hoe toowrite een eenvoudige wachtrij gebaseerde toepassing die gebruikmaakt van Azure Service Bus.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 754d91b3-1426-405e-84b4-fd36d65b114a
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: 93b75902a06becd6e33e05298e09f5669d0e2aef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-applications-that-use-service-bus-queues"></a>Toepassingen maken die gebruikmaken van Service Bus-wachtrijen
In dit onderwerp wordt Service Bus-wachtrijen beschreven en ziet u hoe toowrite een eenvoudige wachtrij gebaseerde toepassing die gebruikmaakt van Service Bus.

Neem bijvoorbeeld een scenario van Hallo wereld van retail waarin verkoopgegevens uit afzonderlijke Point-of-Sale (POS) aansluitingen moet tooan inventaris beheersysteem dat wordt gebruikt voor Hallo gegevens toodetermine stock toobe aangevuld heeft doorgestuurd. Deze oplossing gebruikt Service Bus-berichtenservice voor Hallo communicatie tussen Hallo aansluitingen en beheersysteem Hallo-inventaris, zoals geïllustreerd in de volgende afbeelding Hallo:

![Service Bus-wachtrijen afbeelding 1](./media/service-bus-create-queues/IC657161.gif)

Elke POS-terminal rapporteert de verkoopgegevens door het verzenden van berichten toohello **DataCollectionQueue**. Deze berichten blijven in deze wachtrij totdat ze worden opgehaald door beheersysteem Hallo-inventarisatie. Dit patroon wordt vaak aangeduid als *asynchrone messaging*omdat Hallo POS terminal heeft geen toowait op een antwoord van Hallo inventaris management system toocontinue verwerken.

## <a name="why-queuing"></a>Waarom queuing?
Voordat we bekijkt hello-code die is vereist tooset van deze toepassing in, kunt u overwegen Hallo voordelen van het gebruik van een wachtrij in dit scenario in plaats van Hallo POS-aansluitingen communiceren rechtstreeks (synchroon) toohello beheersysteem inventariseren.

### <a name="temporal-decoupling"></a>Tijdelijke ontkoppeling
Met Hallo asynchrone berichtenpatroon producenten en consumenten hoeft niet online toobe op Hallo hetzelfde moment. Hallo berichteninfrastructuur slaat berichten veilig op totdat de verbruikende partij Hallo gereed tooreceive is ze. Dit betekent dat het Hallo-onderdelen van Hallo gedistribueerde toepassing kunnen worden losgekoppeld-hetzij vrijwillig; bijvoorbeeld voor onderhoud, hetzij vanwege het vastlopen van tooa onderdeel, zonder het hele systeem Hallo. Bovendien misschien verbruikt toepassing hello alleen toobe online bepaalde tijdstippen gedurende Hallo dag. Bijvoorbeeld: in dit scenario retail Hallo inventaris beheersysteem mag slechts bestaan toocome online na het einde van de werkdag Hallo Hallo.

### <a name="load-leveling"></a>Herverdeling van taken
In veel toepassingen varieert de systeembelasting gedurende een periode, terwijl Hallo benodigde verwerkingstijd voor elke werkeenheid doorgaans constant blijft. Tussen bericht producenten en consumenten met een wachtrij betekent dat Hallo consumerende toepassing (Hallo worker) heeft slechts toobe ingericht tooservice gemiddeld laden in plaats van een piekbelasting. Hallo diepte van de wachtrij Hallo zal toenemen en contract zoals Hallo binnenkomende load varieert. Dit bespaart geld rechtstreeks met inachtneming van toohello hoeveelheid infrastructuur vereist tooservice Hallo toepassing werklast.

![Service Bus-wachtrijen afbeelding 2](./media/service-bus-create-queues/IC657162.gif)

### <a name="load-balancing"></a>Taakverdeling
Als Hallo verkeer toeneemt, meer werkprocessen kunnen toegevoegde tooread uit Hallo worker wachtrij. Elk bericht wordt verwerkt door slechts één van de werkprocessen Hallo. Bovendien kunt deze pull-gebaseerde taakverdeling voor optimaal gebruik van Hallo worker computers zelfs als Hallo worker computers met inachtneming van tooprocessing power verschillen, zoals ze op eigen maximale snelheid berichten ophalen. Dit patroon wordt vaak aangeduid als Hallo concurrerende gebruikspatroon.

![Service Bus-wachtrijen afbeelding 3](./media/service-bus-create-queues/IC657163.gif)

### <a name="loose-coupling"></a>De koppeling
Message queuing toointermediate tussen bericht producenten en consumenten biedt een intrinsiek of koppeling tussen Hallo-onderdelen. Omdat producenten en consumenten niet op de hoogte van elkaar zijn, kan een gebruiker zonder gevolgen voor de producent Hallo worden bijgewerkt. Bovendien kan Hallo messaging-topologie ontwikkelen zonder bestaande Hallo-eindpunten. Gaan we dit meer wanneer er iets over publiceren/abonneren.

## <a name="show-me-hello-code"></a>Hallo code weergeven
Hallo van de volgende sectie wordt weergegeven hoe toouse Service Bus toobuild deze toepassing.

### <a name="sign-up-for-an-azure-account"></a>Aanmelden voor een Azure-account
U moet een Azure-account in volgorde toostart werken met Service Bus. Als u nog geen een, kunt u zich aanmelden voor een gratis account [hier](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A85619ABF).

### <a name="create-a-namespace"></a>Een naamruimte maken
Wanneer u een abonnement hebt, kunt u [een Servicenaamruimte maken](service-bus-create-namespace-portal.md). Elke naamruimte fungeert als een scoping container voor een set van Service Bus-entiteiten. Geef uw nieuwe naamruimte een unieke naam alle Service Bus-accounts. 

### <a name="install-hello-nuget-package"></a>Hallo NuGet-pakket installeren
toouse hello Service Bus-naamruimte, een toepassing moet verwijzen naar Hallo Service Bus, specifiek Microsoft.ServiceBus.dll-assembly. U vindt deze assembly als onderdeel van Microsoft Azure SDK Hallo en Hallo downloaden is beschikbaar op Hallo [-SDK van Azure-downloadpagina](https://azure.microsoft.com/downloads/). Hallo echter [Service Bus NuGet-pakket](https://www.nuget.org/packages/WindowsAzure.ServiceBus) is Hallo gemakkelijkste manier tooget Hallo Service Bus-API en tooconfigure uw toepassing met alle Hallo Service Bus-afhankelijkheden.

### <a name="create-hello-queue"></a>Hallo wachtrij maken
Beheerbewerkingen voor Service Bus messaging-entiteiten (wachtrijen en publiceren/abonneren onderwerpen) worden uitgevoerd via Hallo [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) klasse. Service Bus maakt gebruik van een [Shared Access Signature (SAS)](service-bus-sas.md) op basis van het beveiligingsmodel. Hallo [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider) klasse vertegenwoordigt een beveiligingstokenprovider met ingebouwde factorymethoden retourneren sommige bekende token providers. We gebruiken een [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) methode toohold Hallo SAS-referenties. Hallo [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) exemplaar vervolgens met het basisadres van Hallo Service Bus-naamruimte en de tokenprovider Hallo Hallo is samengesteld.

Hallo [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) klasse biedt methoden toocreate, opsommen en verwijderen van berichtentiteiten. code die hier wordt weergegeven ziet hoe Hallo Hallo [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) exemplaar is gemaakt en gebruikt toocreate hello **DataCollectionQueue** wachtrij.

```csharp
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", 
                "test-blog", string.Empty);
string name = "RootManageSharedAccessKey";
string key = "abcdefghijklmopqrstuvwxyz";

TokenProvider tokenProvider = 
    TokenProvider.CreateSharedAccessSignatureTokenProvider(name, key);
NamespaceManager namespaceManager = 
    new NamespaceManager(uri, tokenProvider);
namespaceManager.CreateQueue("DataCollectionQueue");
```

Houd er rekening mee dat er overloads van Hallo zijn [CreateQueue](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateQueue_System_String_) methode waarmee de eigenschappen van Hallo wachtrij toobe zijn afgestemd. U kunt bijvoorbeeld instellen dat Hallo time to live (TTL) standaardwaarde voor berichten die toohello wachtrij zijn verzonden.

### <a name="send-messages-toohello-queue"></a>Berichten toohello wachtrij verzenden
Voor runtime-bewerkingen voor Service Bus-entiteiten; bijvoorbeeld, verzenden en ontvangen berichten, een toepassing moet eerst maken een [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) object. Vergelijkbare toohello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager) klasse hello [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) exemplaar uit het basisadres van Hallo-Servicenaamruimte en tokenprovider Hallo Hallo is gemaakt.

```csharp
 BrokeredMessage bm = new BrokeredMessage(salesData);
 bm.Label = "SalesReport";
 bm.Properties["StoreName"] = "Redmond";
 bm.Properties["MachineID"] = "POS_1";
```

Berichten worden verzonden naar en ontvangen van Service Bus-wachtrijen, zijn exemplaren van Hallo [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) klasse. Deze klasse bestaat uit een aantal standaardeigenschappen (zoals [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) en [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), een woordenlijst die wordt gebruikt toohold toepassingseigenschappen en een hoofdtekst met willekeurige toepassingsgegevens. Een toepassing hello instantie worden ingesteld door door te geven in elk serialiseerbaar object (hello volgende voorbeeld wordt doorgegeven een **SalesData** -object met Hallo verkoopgegevens uit Hallo POS terminal), worden met bepaalde Hallo [ DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx) tooserialize Hallo-object. U kunt ook een [stroom](https://msdn.microsoft.com/library/system.io.stream.aspx) object kan worden opgegeven.

Hallo gemakkelijkste manier toosend berichten tooa wachtrij gegeven in ons geval Hallo **DataCollectionQueue**, is toouse [CreateMessageSender](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageSender_System_String_) toocreate een [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) object rechtstreeks vanuit Hallo [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) exemplaar.

```csharp
MessageSender sender = factory.CreateMessageSender("DataCollectionQueue");
sender.Send(bm);
```

### <a name="receiving-messages-from-hello-queue"></a>Ontvangen van berichten uit de wachtrij Hallo
tooreceive berichten uit de wachtrij hello, kunt u een [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) -object dat u rechtstreeks vanuit Hallo maken [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) met [CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_). Bericht ontvangers kunnen werken in twee verschillende modi: **ReceiveAndDelete** en **PeekLock**. Hallo [ReceiveMode](/dotnet/api/microsoft.servicebus.messaging.receivemode) wordt ingesteld wanneer het Hallo-bericht ontvanger is gemaakt, als een parameter toohello [CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory?redirectedfrom=MSDN#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_Microsoft_ServiceBus_Messaging_ReceiveMode_) aanroepen.

Wanneer u Hallo **ReceiveAndDelete** modus Hallo ontvangen is een één bewerking uitgevoerd; dat wil zeggen als Service Bus Hallo aanvraag ontvangt, wordt gemarkeerd als verbruikt het Hallo-bericht en retourneert het toohello toepassing. **ReceiveAndDelete** modus is Hallo eenvoudigste model en werkt het beste voor scenario's in welke Hallo toepassing niet verwerken van een bericht tolereren kan als een fout toooccur zijn. toounderstand dit, Neem bijvoorbeeld een scenario in welke problemen van de consument Hallo Hallo aanvraag ontvangen en vervolgens vastloopt voordat het wordt verwerkt. Omdat Service Bus gemarkeerd als verbruikt het Hallo-bericht, wanneer Hallo toepassing opnieuw wordt gestart en het verbruik van berichten opnieuw hebt gestart, ontbreekt het Hallo-bericht dat voordat Hallo vastlopen is verbruikt.

In **PeekLock** modus Hallo ontvangen, wordt een bewerking met twee fasen, waardoor het mogelijk toosupport toepassingen die geen ontbrekende berichten kunnen tolereren. Als Service Bus Hallo aanvraag ontvangt, zoeken naar het volgende bericht toobe Hallo verbruikt, wordt vergrendeld tooprevent andere consumenten het ontvangen en retourneert vervolgens toohello toepassing. Nadat de toepassing hello klaar is met verwerking van het Hallo-bericht (of veilig heeft opgeslagen voor toekomstige verwerking), is de tweede fase Hallo Hallo voltooid proces ontvangen door het aanroepen van [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) op Hallo ontvangen bericht. Wanneer Service Bus de aanroep Hallo [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) aanroep, worden gemarkeerd als verbruikt het Hallo-bericht.

Er zijn twee andere resultaten mogelijk. Eerst als Hallo toepassing niet kan tooprocess hello bericht voor een bepaalde reden, kan worden aangeroepen [afbreken](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) op ontvangen Hallo-bericht (in plaats van [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete)). Dit zorgt ervoor dat Service Bus toounlock Hallo-bericht en kunt u de beschikbare toobe opnieuw ontvangen, ofwel door dezelfde gebruiker Hallo of door een andere voltooit consumer. Ten tweede er is een time-out gekoppeld aan Hallo vergrendelen en als toepassing hello Hallo-bericht kan niet worden verwerkt voordat Hallo time-out vergrendeling verloopt (bijvoorbeeld als Hallo toepassing vastloopt), en vervolgens de Service Bus wordt ontgrendeld Hallo-bericht, waardoor het beschikbaar toobe opnieuw ontvangen (in wezen uitvoeren van een [afbreken](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Abandon) bewerking standaard).

Houd er rekening mee dat als hello toepassing is vastgelopen na het Hallo-bericht worden verwerkt, maar voordat u Hallo [Complete](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Complete) verzoek is uitgegeven, is het Hallo-bericht opnieuw bezorgd toohello toepassing opnieuw wordt gestart. Dit wordt vaak aangeduid als * tenminste eenmaal * verwerken. Dit betekent dat elk bericht ten minste één keer wordt verwerkt, maar in bepaalde situaties Hallo hetzelfde bericht opnieuw kan worden bezorgd. Als Hallo scenario kan geen dubbele verwerking tolereren, is de aanvullende logica Hallo toepassing toodetect dubbele vereist. Dit kan worden bereikt op basis van Hallo [MessageId](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId) eigenschap van het Hallo-bericht. Hallo-waarde van deze eigenschap gelijk blijft bij meerdere bezorgingspogingen. Dit wordt aangeduid als *exact één keer* verwerken.

Hallo code die hier wordt weergegeven, ontvangt en verwerkt een bericht met Hallo **PeekLock** modus Hallo standaard als er geen [ReceiveMode](/dotnet/api/microsoft.servicebus.messaging.receivemode) waarde expliciet wordt aangeboden.

```csharp
MessageReceiver receiver = factory.CreateMessageReceiver("DataCollectionQueue");
BrokeredMessage receivedMessage = receiver.Receive();
try
{
    ProcessMessage(receivedMessage);
    receivedMessage.Complete();
}
catch (Exception e)
{
    receivedMessage.Abandon();
}
```

### <a name="use-hello-queue-client"></a>Hallo wachtrij-client gebruiken
Hallo voorbeelden eerder in deze sectie gemaakt [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) en [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) objecten rechtstreeks vanuit Hallo [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) toosend en kunnen berichten ontvangen uit de wachtrij hello, respectievelijk. Een alternatieve methode is toouse een [QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient) object, die ondersteuning biedt zowel bij het verzenden en ontvangen van bewerkingen in toevoeging toomore geavanceerde functies, zoals sessies.

```csharp
QueueClient queueClient = factory.CreateQueueClient("DataCollectionQueue");
queueClient.Send(bm);

BrokeredMessage message = queueClient.Receive();

try
{
    ProcessMessage(message);
    message.Complete();
}
catch (Exception e)
{
    message.Abandon();
} 
```

## <a name="next-steps"></a>Volgende stappen
Nu u Hallo basisprincipes van wachtrijen hebt geleerd, gaat u naar [toepassingen die gebruikmaken van Service Bus-onderwerpen en abonnementen maken](service-bus-create-topics-subscriptions.md) toocontinue deze discussie met Hallo mogelijkheden voor publiceren/abonneren van Service Bus-onderwerpen en abonnementen.

