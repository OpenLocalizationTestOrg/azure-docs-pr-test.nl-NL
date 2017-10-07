---
title: handleiding voor Azure Event Hubs aaaProgramming | Microsoft Docs
description: Code schrijven voor Azure Event Hubs met behulp van hello Azure .NET SDK.
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 64cbfd3d-4a0e-4455-a90a-7f3d4f080323
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 08/17/2017
ms.author: sethm
ms.openlocfilehash: 43bebd126c2311af9e3daeb52324132b66cf0884
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-programming-guide"></a>Programmeerhandleiding voor Event Hubs

Dit artikel worden enkele algemene scenario's bij het schrijven van code met Azure Event Hubs en hello Azure .NET SDK. Er wordt uitgegaan van een basisbegrip van Event Hubs. Zie voor een conceptueel overzicht van Event Hubs Hallo [overzicht van Event Hubs](event-hubs-what-is-event-hubs.md).

## <a name="event-publishers"></a>Gebeurtenisuitgevers

U verzenden gebeurtenissen tooan event hub via HTTP POST of via een AMQP 1.0-verbinding. keuze van welke toouse Hallo en wanneer is afhankelijk van Hallo specifieke scenario worden toegepast. AMQP 1.0-verbindingen zijn brokered verbindingen in Service Bus. Ze zijn met name geschikt voor scenario‘s met vaak voorkomende hogere berichtvolumes en lagere latentievereisten, omdat ze een permanent berichtenkanaal bieden.

Maken en beheren van Event Hubs met behulp van Hallo [NamespaceManager][] klasse. Wanneer met Hallo .NET API's wordt beheerd, Hallo primaire constructs voor het publiceren van gegevens tooEvent Hubs zijn Hallo [EventHubClient](/dotnet/api/microsoft.servicebus.messaging.eventhubclient) en [EventData][] klassen. [EventHubClient][] biedt AMQP-communicatiekanaal Hallo gedurende welke gebeurtenissen toohello event hub worden verzonden. Hallo [EventData][] klasse vertegenwoordigt een gebeurtenis en gebruikte toopublish berichten tooan event hub is. Deze klasse bevat Hallo hoofdtekst, bepaalde metagegevens en headerinformatie over Hallo-gebeurtenis. Andere eigenschappen toegevoegd toohello [EventData][] object als het een event hub passeert.

## <a name="get-started"></a>Aan de slag

Hallo .NET-klassen die ondersteuning bieden voor Event Hubs vindt u in Hallo Microsoft.ServiceBus.dll-assembly. Hallo gemakkelijkste manier tooreference Hallo Service Bus-API en tooconfigure uw toepassing met alle Service Bus-afhankelijkheden Hallo is toodownload hello [Service Bus NuGet-pakket](https://www.nuget.org/packages/WindowsAzure.ServiceBus). U kunt ook hello gebruiken [Package Manager Console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) in Visual Studio. toodo uitgeven dus Hallo volgende opdracht in Hallo [Package Manager Console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) venster:

```
Install-Package WindowsAzure.ServiceBus
```

## <a name="create-an-event-hub"></a>Een Event Hub maken
U kunt Hallo [NamespaceManager][] klasse toocreate Event Hubs. Bijvoorbeeld:

```csharp
var manager = new Microsoft.ServiceBus.NamespaceManager("mynamespace.servicebus.windows.net");
var description = manager.CreateEventHub("MyEventHub");
```

In de meeste gevallen wordt aanbevolen dat u Hallo [CreateEventHubIfNotExists][] methoden tooavoid uitzonderingen worden gegenereerd als Hallo-service opnieuw wordt opgestart. Bijvoorbeeld:

```csharp
var description = manager.CreateEventHubIfNotExists("MyEventHub");
```

Alle Event Hubs maken-bewerkingen, inclusief [CreateEventHubIfNotExists][], vereisen **beheren** machtigingen op Hallo naamruimte in kwestie. Als u toolimit Hallo machtigingen van uw toepassingen publicatie- of consumertoepassingen wilt, kunt u voorkomen deze bewerking aanroepen in productiecode maken wanneer u referenties met beperkte machtigingen.

Hallo [EventHubDescription](/dotnet/api/microsoft.servicebus.messaging.eventhubdescription) klasse bevat details over een event hub, met inbegrip van autorisatieregels hello, bewaarinterval Hallo-bericht, partitie-id's, status en pad. U kunt deze klasse tooupdate Hallo-metagegevens voor een event hub.

## <a name="create-an-event-hubs-client"></a>Een Event Hubs-client maken
Hallo primaire klasse voor interactie met Event Hubs is [Microsoft.ServiceBus.Messaging.EventHubClient][EventHubClient]. Deze klasse biedt mogelijkheden voor zowel verzenden als ontvangen. U kunt deze klasse met behulp van Hallo instantiëren [maken](/dotnet/api/microsoft.servicebus.messaging.eventhubclient.create) methode, zoals wordt weergegeven in het volgende voorbeeld Hallo.

```csharp
var client = EventHubClient.Create(description.Path);
```

Deze methode gebruikt Hallo Service Bus-verbindingsinformatie in Hallo bestand App.config in Hallo `appSettings` sectie. Voor een voorbeeld van Hallo `appSettings` XML toostore Hallo Service Bus-verbindingsinformatie gebruikt, Raadpleeg de documentatie Hallo voor Hallo [Microsoft.ServiceBus.Messaging.EventHubClient.Create(System.String)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Create_System_String_) methode.

Een andere optie is toocreate Hallo client vanuit een verbindingsreeks. Deze optie werkt goed bij het gebruik van Azure-werkrollen, omdat u Hallo tekenreeks kunt opslaan in Hallo configuratie-eigenschappen voor Hallo werknemer. Bijvoorbeeld:

```csharp
EventHubClient.CreateFromConnectionString("your_connection_string");
```

Hallo-verbindingsreeks niet in dezelfde notatie zoals deze wordt weergegeven in Hallo App.config-bestand voor de vorige methoden Hallo Hallo:

```
Endpoint=sb://[namespace].servicebus.windows.net/;SharedAccessKeyName=RootManageSharedAccessKey;SharedAccessKey=[key]
```

Ten slotte is het ook mogelijk toocreate een [EventHubClient][] object uit een [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) exemplaar, zoals weergegeven in het volgende voorbeeld Hallo.

```csharp
var factory = MessagingFactory.CreateFromConnectionString("your_connection_string");
var client = factory.CreateEventHubClient("MyEventHub");
```

Het is belangrijk dat extra toonote [EventHubClient][] objecten die zijn gemaakt op basis van een messagingfactory-exemplaar opnieuw wilt gebruiken Hallo dezelfde onderliggende TCP-verbinding. Voor deze objecten geldt daarom een doorvoerlimiet aan clientzijde. Hallo [maken](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Create_System_String_) methode wordt gebruikgemaakt van één messagingfactory. Als u van één afzender een zeer hoge doorvoersnelheid nodig hebt, kunt u meerdere MessagingFactory-exemplaren maken en vervolgens van elk MessagingFactory-exemplaar één [EventHubClient][]-object.

## <a name="send-events-tooan-event-hub"></a>Verzenden van gebeurtenissen tooan event hub
Verzenden van gebeurtenissen tooan event hub door het maken van een [EventData][] exemplaar en deze te verzenden via Hallo [verzenden](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) methode. Deze methode heeft één [EventData][] instantieparameter en verzendt deze synchroon tooan event hub.

## <a name="event-serialization"></a>Gebeurtenisserialisatie
Hallo [EventData][] klasse heeft [vier overbelaste constructors](/dotnet/api/microsoft.servicebus.messaging.eventdata#constructors_) die verschillende parameters, zoals een object en serializer, een bytematrix of een stroom ondernemen. Het is ook mogelijk tooinstantiate hello [EventData][] klasse en de hoofdstroom hello later instellen. Als u JSON gebruikt met [EventData][], kunt u **Encoding.UTF8.GetBytes()** tooretrieve Hallo bytematrix voor een JSON-gecodeerde tekenreeks.

## <a name="partition-key"></a>Partitiesleutel
Hallo [EventData][] klasse heeft een [PartitionKey][] eigenschap waarmee Hallo afzender toospecify een waarde die is gehasht tooproduce de partitietoewijzing van een. Met behulp van een partitiesleutel zorgt ervoor dat alle gebeurtenissen met dezelfde sleutel worden verzonden Hallo Hallo toohello dezelfde partitie in Hallo event hub. Vaak gebruikte partitiesleutels zijn gebruikerssessie-id's en unieke afzender-id‘s. Hallo [PartitionKey][] eigenschap is optioneel en kan worden opgegeven wanneer u Hallo [Microsoft.ServiceBus.Messaging.EventHubClient.Send(Microsoft.ServiceBus.Messaging.EventData)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) of [Microsoft.ServiceBus.Messaging.EventHubClient.SendAsync(Microsoft.ServiceBus.Messaging.EventData)](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendAsync_Microsoft_ServiceBus_Messaging_EventData_) methoden. Als u geen waarde voor opgeeft [PartitionKey][], verzonden gebeurtenissen gedistribueerd toopartitions met behulp van een round robin-model zijn.

### <a name="availability-considerations"></a>Beschikbaarheidsoverwegingen

Met behulp van een partitiesleutel is optioneel en u zorgvuldig overwegen of toouse een. In veel gevallen is met behulp van een partitiesleutel een goede keuze als ordening van gebeurtenissen belangrijk is. Wanneer u een partitiesleutel, deze partities vereisen beschikbaarheid op één knooppunt en storingen kunnen optreden na verloop van tijd; Wanneer compute bijvoorbeeld patch en knooppunten opnieuw opstarten. Als zodanig als u een partitie-ID ingesteld en die partitie niet meer beschikbaar is voor een bepaalde reden, wordt een poging tooaccess Hallo-gegevens in de betreffende partitie mislukken. Als hoge beschikbaarheid zeer belangrijk is, Geef een partitiesleutel; in dat geval gebeurtenissen verzonden toopartitions met behulp van round robin-model Hallo eerder beschreven. In dit scenario maakt u een expliciete keuze tussen beschikbaarheid (geen partitie-ID) en consistentie (vastmaken gebeurtenissen tooa partitie-ID).

Een andere overweging verwerkt vertragingen bij de verwerking van gebeurtenissen. In sommige gevallen kan het betere toodrop gegevens zijn en probeer dan tootry en blijven van verwerking, die kan verder downstreamverwerking vertragingen veroorzaken. Bijvoorbeeld, met een aandelenkoersen is het beter toowait voor volledige, actuele gegevens, maar in een live chatten of VOIP-scenario u liever Hallo gegevens snel, zelfs als deze niet volledig.

Gegeven deze overwegingen beschikbaarheid in deze scenario's kunt u een van de volgende strategieën voor foutafhandeling Hallo:

- Stoppen (stop lezen uit Event Hubs totdat dingen zijn opgelost)
- Drop (berichten zijn niet belangrijk, neerzetten ze)
- Probeer (nieuwe poging hello berichten, zoals u ziet past)
- [Wachtrij voor onbestelbare](../service-bus-messaging/service-bus-dead-letter-queues.md) (gebruik een wachtrij of een andere event hub toodead letter alleen Hallo-berichten kan niet worden verwerkt)

Zie voor meer informatie en een discussie over Hallo verschillen tussen de beschikbaarheid en consistentie [beschikbaarheid en consistentie in Event Hubs](event-hubs-availability-and-consistency.md). 

## <a name="batch-event-send-operations"></a>Batchbewerkingen voor het verzenden van gebeurtenissen
Het verzenden van gebeurtenissen in batches kan de doorvoer aanzienlijk verhogen. Hallo [SendBatch](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendBatch_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__) methode duurt een **IEnumerable** parameter van het type [EventData][] en verzendt Hallo hele batch als een atomic-bewerking toohello event hub.

```csharp
public void SendBatch(IEnumerable<EventData> eventDataList);
```

Houd er rekening mee dat één batch mag niet groter zijn dan limiet van 256 KB Hallo van een gebeurtenis. Bovendien elk bericht in een batch Hallo Hallo gebruikmaakt van dezelfde uitgever-ID. Het is Hallo verantwoordelijkheid van Hallo afzender tooensure die batch Hallo Hallo maximale gebeurtenisgrootte niet overschrijdt. Als dit wel gebeurt, wordt aan clientzijde een **Verzendfout** gegenereerd.

## <a name="send-asynchronously-and-send-at-scale"></a>Asynchroon verzenden en op schaal verzenden
U kunt ook gebeurtenissen tooan event hub asynchroon verzenden. Asynchroon verzenden kan sneller Hallo waarop een client kunnen toosend gebeurtenissen is. Beide Hallo [verzenden](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_Send_Microsoft_ServiceBus_Messaging_EventData_) en [SendBatch](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_SendBatch_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__) methoden zijn beschikbaar in asynchrone versies die resulteren in een [taak](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) object. Terwijl deze doorvoer verhogen kan, het kan ook leiden tot Hallo gebeurtenissen voor clientapparaten toocontinue toosend terwijl deze wordt beperkt door Hallo Event Hubs-service en tot Hallo fouten of verloren berichten leiden kan als dat niet het juiste wijze wordt geïmplementeerd. Bovendien kunt u Hallo [RetryPolicy](/dotnet/api/microsoft.servicebus.messaging.cliententity#Microsoft_ServiceBus_Messaging_ClientEntity_RetryPolicy) -eigenschap op Hallo client toocontrol clientopties-probeer het opnieuw.

## <a name="create-a-partition-sender"></a>Partitieafzender maken
Hoewel het meest voorkomende toosend gebeurtenissen tooan event hub zonder een partitiesleutel, in sommige gevallen kunt u gebeurtenissen toosend rechtstreeks tooa opgegeven partitie. Bijvoorbeeld:

```csharp
var partitionedSender = client.CreatePartitionedSender(description.PartitionIds[0]);
```

[CreatePartitionedSender](/dotnet/api/microsoft.servicebus.messaging.eventhubclient#Microsoft_ServiceBus_Messaging_EventHubClient_CreatePartitionedSender_System_String_) retourneert een [EventHubSender](/dotnet/api/microsoft.servicebus.messaging.eventhubsender) object waarmee u toopublish gebeurtenissen tooa specifieke event hub-partitie kunt.

## <a name="event-consumers"></a>Gebeurtenisconsumers
Event Hubs heeft twee primaire modellen voor gebeurtenisgebruik: directe ontvangers en abstracties van een hoger niveau, zoals [EventProcessorHost][]. Directe ontvangers zijn verantwoordelijk voor hun eigen coördinatie van toegang toopartitions binnen een consumergroep.

### <a name="direct-consumer"></a>Directe consumer
Hallo meest directe manier tooread van een partitie binnen een consumergroep is toouse hello [EventHubReceiver](/dotnet/apie/microsoft.servicebus.messaging.eventhubreceiver) klasse. toocreate een instantie van deze klasse, moet u een exemplaar van Hallo [EventHubConsumerGroup](/dotnet/api/microsoft.servicebus.messaging.eventhubconsumergroup) klasse. Hallo partitie-ID moet Hallo voorbeeld te volgen, worden opgegeven bij het maken van Hallo ontvanger voor Hallo consumergroep.

```csharp
EventHubConsumerGroup group = client.GetDefaultConsumerGroup();
var receiver = group.CreateReceiver(client.GetRuntimeInformation().PartitionIds[0]);
```

Hallo [CreateReceiver](/dotnet/api/microsoft.servicebus.messaging.eventhubconsumergroup#methods_summary) methode heeft verschillende overloads die vergemakkelijken besturen Hallo lezer die wordt gemaakt. Deze methoden omvatten het opgeven van een offset als een tekenreeks of een tijdstempel en mogelijkheid toospecify of tooinclude deze opgegeven offset Hallo geretourneerd stream of starten nadat het Hallo. Nadat u Hallo ontvanger hebt gemaakt, kunt u beginnen gebeurtenissen ontvangen op Hallo object geretourneerd. Hallo [ontvangen](/dotnet/api/microsoft.servicebus.messaging.eventhubreceiver#methods_summary) methode heeft vier overloads die Hallo besturingselement ontvangen bewerkingsparameters, zoals batchgrootte en wachttijd. U kunt Hallo asynchrone versies van deze methoden tooincrease Hallo doorvoer van een consumer. Bijvoorbeeld:

```csharp
bool receive = true;
string myOffset;
while(receive)
{
    var message = receiver.Receive();
    myOffset = message.Offset;
    string body = Encoding.UTF8.GetString(message.GetBytes());
    Console.WriteLine(String.Format("Received message offset: {0} \nbody: {1}", myOffset, body));
}
```

Hallo-berichten worden met opzicht tooa specifieke partitie ontvangen in Hallo volgorde waarin ze toohello event hub zijn verzonden. Hallo-offset is een tekenreeks token gebruikte tooidentify een bericht in een partitie.

Let op: een afzonderlijke partitie in een consumergroep mag niet meer dan 5 lezers tegelijk hebben. Wanneer lezers verbinding maken of de verbinding verbroken, kunnen hun sessies enkele minuten duren voordat de service Hallo herkent dat de verbinding is verbroken te blijven actief. Gedurende deze tijd mislukken opnieuw verbinding te maken tooa partitie. Zie voor een compleet voorbeeld van het schrijven van een directe ontvanger voor Event Hubs, Hallo [Event Hubs directe ontvangers](https://code.msdn.microsoft.com/Event-Hub-Direct-Receivers-13fa95c6) voorbeeld.

### <a name="event-processor-host"></a>Gebeurtenisprocessorhost
Hallo [EventProcessorHost][] klasse gegevens uit Event Hubs verwerkt. Tijdens het bouwen van gebeurtenislezers op Hallo .NET-platform, moet u deze implementatie gebruiken. [EventProcessorHost][] biedt een thread-veilige, beveiligde runtimeomgeving met meerdere processen voor implementaties van gebeurtenisprocessors die ook beheer biedt van controlepunten en partitielease.

Hallo toouse [EventProcessorHost][] klasse, die u kunt implementeren [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor). Deze interface bevat drie methoden:

* [OpenAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_OpenAsync_Microsoft_ServiceBus_Messaging_PartitionContext_)
* [CloseAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_CloseAsync_Microsoft_ServiceBus_Messaging_PartitionContext_Microsoft_ServiceBus_Messaging_CloseReason_)
* [ProcessEventsAsync](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor#Microsoft_ServiceBus_Messaging_IEventProcessor_ProcessEventsAsync_Microsoft_ServiceBus_Messaging_PartitionContext_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_EventData__)

het instantiëren van toostart gebeurtenisverwerking, [EventProcessorHost][], bieden de juiste parameters Hallo voor uw event hub. Roep vervolgens [RegisterEventProcessorAsync](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost#Microsoft_ServiceBus_Messaging_EventProcessorHost_RegisterEventProcessorAsync__1) tooregister uw [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor) implementatie met Hallo-runtime. Op dit moment probeert Hallo host tooacquire een lease op elke partitie in Hallo event hub met behulp van een greedy-algoritme. Deze leases zijn gedurende een bepaald tijdsbestek geldig en moeten daarna worden vernieuwd. Zodra nieuwe knooppunten worker-exemplaren in dit geval online komen, ze reserveringen voor leases en gedurende een bepaalde periode Hallo load verschuift tussen knooppunten elk tooacquire meer leases proberen.

![Gebeurtenisprocessorhost](./media/event-hubs-programming-guide/IC759863.png)

In de loop van de tijd komt er een evenwicht tot stand. Deze dynamische mogelijkheid kan automatisch schalen op basis van CPU toobe toegepast tooconsumers voor schaal omhoog en omlaag schalen. Omdat Event Hubs niet over een direct concept voor berichtentelling, is gemiddelde CPU-gebruik vaak Hallo best mechanisme toomeasure back end- of consumerschaling schaal. Als uitgevers meer gebeurtenissen dan consumers kunnen verwerken toopublish begint, zijn Hallo CPU toename op consumenten gebruikte toocause een automatisch geschaald aantal werkrolexemplaren.

Hallo [EventProcessorHost][] klasse implementeert ook een mechanisme voor Azure storage gebaseerd plaatsen van controlepunten. Dit mechanisme winkels Hallo offset op basis van per partitie, zodat elke consumer welke Hallo laatste controlepunt van Hallo vorige consumer bepalen kan was. Terwijl partities overgang tussen knooppunten via leases dit synchronisatiemechanisme Hallo voor verschuiving van belasting is.

## <a name="publisher-revocation"></a>Uitgever intrekken
Bovendien toohello Runtime-functies van geavanceerde [EventProcessorHost][], Event Hubs kunt u het intrekken van uitgevers in volgorde tooblock specifieke uitgevers geen gebeurtenis tooan event hub te verzenden. Deze functies zijn vooral nuttig als token van een uitgever is aangetast, of een software-update wordt veroorzaakt door ze toobehave verkeerd. In deze omstandigheden kan Hallo uitgever ID, dat deel uitmaakt van de SAS-token, worden geblokkeerd uitgeven van gebeurtenissen.

Voor meer informatie over het intrekken van uitgevers en hoe toosend tooEvent Hubs als een publisher zien Hallo [Event Hubs grote schaal veilig publiceren](https://code.msdn.microsoft.com/Service-Bus-Event-Hub-99ce67ab) voorbeeld.

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over Event Hubs-scenario's, gaat u naar deze koppelingen:

* [Event Hubs-API-overzicht](event-hubs-api-overview.md)
* [Wat is Event Hubs](event-hubs-what-is-event-hubs.md)
* [Beschikbaarheid en consistentie in Event Hubs](event-hubs-availability-and-consistency.md)
* [API-verwijzing voor de gebeurtenisprocessorhost](/dotnet/api/microsoft.servicebus.messaging.eventprocessorhost)

[NamespaceManager]: /dotnet/api/microsoft.servicebus.namespacemanager
[EventHubClient]: /dotnet/api/microsoft.servicebus.messaging.eventhubclient
[EventData]: /dotnet/api/microsoft.servicebus.messaging.eventdata
[CreateEventHubIfNotExists]: /dotnet/api/microsoft.servicebus.namespacemanager.createeventhubifnotexists
[PartitionKey]: /dotnet/api/microsoft.servicebus.messaging.eventdata#Microsoft_ServiceBus_Messaging_EventData_PartitionKey
[EventProcessorHost]: /dotnet/api/microsoft.servicebus.messaging.eventprocessorhost
