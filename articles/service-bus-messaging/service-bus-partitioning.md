---
title: aaaCreate gepartitioneerd Azure Service Bus-wachtrijen en onderwerpen | Microsoft Docs
description: Hierin wordt beschreven hoe toopartition Service Bus-wachtrijen en onderwerpen met meerdere bericht makelaars.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a0c7d5a2-4876-42cb-8344-a1fc988746e7
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;hillaryc
ms.openlocfilehash: 6d42556a0714d6a012dc319f662521c8b0bb958b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="partitioned-queues-and-topics"></a>Gepartitioneerde wachtrijen en onderwerpen
Azure Service Bus maakt gebruik van meerdere bericht beleggingsmakelaars tooprocess berichten en berichten toostore meerdere messaging worden opgeslagen. Een conventionele wachtrij of onderwerp is verwerkt door een enkel bericht broker en opgeslagen in één berichten-store. Service Bus *partities* wachtrijen en onderwerpen, inschakelen of *berichtentiteiten*, toobe gepartitioneerd op meerdere bericht beleggingsmakelaars en berichten-stores. Dit betekent dat de totale doorvoer van een gepartitioneerde entiteit Hallo wordt niet langer beperkt door het Hallo-prestaties van een enkel bericht broker of berichten-store. Bovendien weer een tijdelijke onderbreking van berichten-store niet een gepartitioneerde wachtrij of onderwerp niet beschikbaar. Gepartitioneerde wachtrijen en onderwerpen kunnen bevatten alle uitgebreide Service Bus-functies, zoals ondersteuning voor transacties en sessies.

Zie voor informatie over Service Bus inwendige Hallo [Service Bus-architectuur] [ Service Bus architecture] artikel.

Partitioneren is standaard ingeschakeld bij het maken van de entiteit in alle wachtrijen en onderwerpen in de standaard- en Premium messaging. U kunt standaard laag berichtentiteiten zonder partitioneren maken, maar wachtrijen en onderwerpen in een Premium-naamruimte altijd worden gepartitioneerd; Deze optie kan niet worden uitgeschakeld. 

Het is niet mogelijk toochange Hallo partitioneren optie op een bestaande wachtrij of onderwerp in de lagen Standard of Premium, kunt u alleen Hallo opties instellen bij het maken van Hallo entiteit.

## <a name="how-it-works"></a>Hoe werkt het?

Elke gepartitioneerde wachtrij of onderwerp bestaat uit meerdere fragmenten. Elke fragment is opgeslagen in een andere berichten-store en verwerkt door een ander bericht broker. Wanneer een bericht wordt verzonden tooa gepartitioneerde wachtrij of onderwerp, toegewezen Service Bus Hallo-bericht tooone van Hallo fragmenten. Hallo selectie willekeurig wordt uitgevoerd door de Service Bus of met behulp van een partitiesleutel die afzender Hallo kunt opgeven.

Wanneer een client wil tooreceive een bericht van een gepartitioneerde wachtrij of uit het abonnement tooa gepartitioneerde onderwerp Service Bus-query's alle fragmenten voor berichten, retourneert de eerste Hallo-bericht dat is verkregen van een Hallo messaging winkels toohello ontvanger. Service Bus-caches Hallo andere berichten en retourneert ze als deze aanvullende ontvangt aanvragen ontvangen. Een ontvangende client is niet bekend met Hallo partitioneren; Hallo clientgerichte gedrag van een gepartitioneerde wachtrij of onderwerp (bijvoorbeeld, lezen, voltooid, uitstelt, wachtrij voor onbestelbare, veelgevraagde) is identiek toohello gedrag van een reguliere entiteit.

Er is geen extra kosten bij het verzenden van een bericht of het bericht in een gepartitioneerde wachtrij of onderwerp.

## <a name="enable-partitioning"></a>Partitioneren inschakelen

toouse gepartitioneerd wachtrijen en onderwerpen met Azure Service Bus gebruiken hello Azure SDK versie 2.2 of hoger, of geef `api-version=2013-10` in uw HTTP-aanvragen.

### <a name="standard"></a>Standard

In Hallo Standard messaging-laag, kunt u Service Bus-wachtrijen en onderwerpen in 1, 2, 3, 4 of 5 GB-grootten (Hallo standaardwaarde is 1 GB). Service Bus maakt met het partitionering ingeschakeld, 16 kopieën (16 partities) van Hallo entiteit voor elke GB die u opgeeft. Als zodanig als u een wachtrij die is 5 GB groot maken, met 16 partities Hallo Maximale wachtrijgrootte wordt (5 \* 16) = 80 GB. U kunt Hallo maximale grootte van uw gepartitioneerde wachtrij of onderwerp zien door te kijken op de vermelding ervan op Hallo [Azure-portal][Azure portal], in Hallo **overzicht** blade voor die entiteit.

### <a name="premium"></a>Premium

In een naamruimte van de laag Premium kunt u Service Bus-wachtrijen en onderwerpen in 1, 2, 3, 4, 5, 10, 20, 40 of 80 GB grootten (Hallo standaardwaarde is 1 GB). Service Bus maakt twee partities per entiteit met het partitioneren van de standaard ingeschakeld. U kunt Hallo maximale grootte van uw gepartitioneerde wachtrij of onderwerp zien door te kijken op de vermelding ervan op Hallo [Azure-portal][Azure portal], in Hallo **overzicht** blade voor die entiteit.

Zie voor meer informatie over partitioneren in Hallo Premium messaging laag [Service Bus Premium en Standard Messaging](service-bus-premium-messaging.md). 

### <a name="create-a-partitioned-entity"></a>Maak een gepartitioneerde entiteit

Er zijn verschillende manieren toocreate een gepartitioneerde wachtrij of onderwerp. Als u van uw toepassing hello wachtrij of onderwerp maakt, kunt u inschakelen voor Hallo wachtrij of onderwerp partitioneren door respectievelijk instelling Hallo [QueueDescription.EnablePartitioning] [ QueueDescription.EnablePartitioning] of [TopicDescription.EnablePartitioning] [ TopicDescription.EnablePartitioning] eigenschap te**true**. Deze eigenschappen moeten worden ingesteld op Hallo tijd Hallo wachtrij of onderwerp is gemaakt. Zoals eerder gezegd, is het niet mogelijk toochange deze eigenschappen op een bestaande wachtrij of onderwerp. Bijvoorbeeld:

```csharp
// Create partitioned topic
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

U kunt ook kunt u een gepartitioneerde wachtrij of onderwerp in Hallo [Azure-portal] [ Azure portal] of in Visual Studio. Bij het maken van een wachtrij of onderwerp in de portal Hallo Hallo **inschakelen partitioneren** optie in Hallo wachtrij of onderwerp **maken** blade is standaard ingeschakeld. U kunt deze optie in een entiteit standaardcategorie; alleen uitschakelen in Hallo is Premium-laag partitioneren altijd ingeschakeld. Klik in Visual Studio op Hallo **inschakelen partitioneren** checkbox in Hallo **nieuwe wachtrij** of **nieuw onderwerp** in het dialoogvenster.

## <a name="use-of-partition-keys"></a>Gebruik van partitiesleutels
Wanneer een bericht in de wachtrij in een gepartitioneerde wachtrij of onderwerp is, controleert u Service Bus Hallo aanwezigheid van een partitiesleutel. Als er een is gevonden, wordt deze geselecteerd Hallo fragment op basis van die sleutel. Als een partitiesleutel niet wordt gevonden, wordt deze Hallo fragment op basis van een interne algoritme geselecteerd.

### <a name="using-a-partition-key"></a>Met behulp van een partitiesleutel
Sommige scenario's, zoals sessies of transacties, vereisen berichten toobe opgeslagen in een specifieke fragment. Deze scenario's vereisen Hallo gebruik van een partitiesleutel. Alle berichten die gebruik Hallo dezelfde partitiesleutel zijn toegewezen toohello dezelfde fragment. Als het Hallo-fragment tijdelijk niet beschikbaar is, Service Bus een fout geretourneerd.

Afhankelijk van het Hallo-scenario worden verschillende berichteigenschappen als een partitiesleutel gebruikt:

**Sessie-id**: als een bericht Hallo heeft [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] eigenschap instelt, wordt de Service Bus deze eigenschap wordt gebruikt als partitiesleutel Hallo. Op deze manier, alle berichten die deel uitmaken van toohello dezelfde sessie worden afgehandeld door Hallo dezelfde bericht broker. Hierdoor kunnen Service Bus tooguarantee bericht ordening en Hallo consistentie van de sessiestatus.

**PartitionKey**: als een bericht Hallo heeft [BrokeredMessage.PartitionKey] [ BrokeredMessage.PartitionKey] eigenschap, maar niet Hallo [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] eigenschap instelt, wordt de Service Bus gebruikt Hallo [PartitionKey] [ PartitionKey] eigenschap als partitiesleutel Hallo. Als het Hallo-bericht beide Hallo heeft [SessionId] [ SessionId] en Hallo [PartitionKey] [ PartitionKey] set eigenschappen, beide eigenschappen moeten identiek zijn. Als hello [PartitionKey] [ PartitionKey] eigenschap is ingesteld tooa andere waarde dan Hallo [SessionId] [ SessionId] retourneert een ongeldige eigenschap, Service Bus uitzondering van de bewerking. Hallo [PartitionKey] [ PartitionKey] eigenschap moet worden gebruikt als een afzender verzendt een niet-sessie op de hoogte transactionele berichten. Hallo partitiesleutel zorgt ervoor dat alle berichten die zijn verzonden binnen een transactie worden verwerkt door Hallo dezelfde messaging broker.

**MessageId**: als Hallo wachtrij of onderwerp Hallo heeft [QueueDescription.RequiresDuplicateDetection] [ QueueDescription.RequiresDuplicateDetection] eigenschappenset te**true** en Hallo [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] of [BrokeredMessage.PartitionKey] [ BrokeredMessage.PartitionKey] eigenschappen zijn niet ingesteld en vervolgens Hallo [BrokeredMessage.MessageId] [ BrokeredMessage.MessageId] eigenschap fungeert als partitiesleutel Hallo. (Houd er rekening mee dat Hallo Microsoft .NET- en AMQP bibliotheken een bericht-ID automatisch toewijzen als verzendende toepassing hello niet.) In dit geval Hallo alle kopieën van hetzelfde bericht worden afgehandeld door Hallo hetzelfde bericht broker. Dit kunt Service Bus toodetect en verwijderen van dubbele berichten. Als hello [QueueDescription.RequiresDuplicateDetection] [ QueueDescription.RequiresDuplicateDetection] eigenschap is niet ingesteld te**true**, Service Bus wordt geen rekening gehouden Hallo [MessageId] [ MessageId] eigenschap als partitiesleutel.

### <a name="not-using-a-partition-key"></a>Niet met behulp van een partitiesleutel
Hallo ontbreken van een partitiesleutel distribueert Service Bus berichten in een round-robin toewijst tooall Hallo fragmenten Hallo gepartitioneerde wachtrij of onderwerp. Als Hallo gekozen fragment niet beschikbaar is, wijst Service Bus Hallo-bericht tooa verschillende fragment. Op deze manier Hallo verzendbewerking slaagt ondanks Hallo tijdelijk niet beschikbaar berichten-store. U wordt echter niet worden gegarandeerd dat een partitiesleutel biedt ordening Hallo bereiken.

Zie voor een diepgaandere bespreking van Hallo afweging tussen het beschikbaarheid (geen partitiesleutel) en consistentie (met behulp van een partitiesleutel) [in dit artikel](../event-hubs/event-hubs-availability-and-consistency.md). Deze informatie is evenveel van toepassing toopartitioned Service Bus-entiteiten en Event Hubs-partities.

toogive Service Bus voldoende tijd tooenqueue Hallo-bericht naar een andere fragment hello [MessagingFactorySettings.OperationTimeout] [ MessagingFactorySettings.OperationTimeout] waarde die is opgegeven door Hallo-client die door het Hallo-bericht verzonden moet groter zijn dan 15 seconden. Het verdient aanbeveling dat u Hallo ingesteld [OperationTimeout] [ OperationTimeout] eigenschap toohello standaardwaarde van 60 seconden.

Houd er rekening mee dat een partitiesleutel 'pincodes"een bericht tooa specifieke fragment. Als het Hallo-berichten-store die dit fragment bevat niet beschikbaar is, betekent dit dat Service Bus een fout geretourneerd. Hallo ontbreken van een partitiesleutel, Service Bus geen andere fragment kunt kiezen en Hallo-bewerking is geslaagd. Daarom wordt aanbevolen dat u niet een partitiesleutel opgeeft tenzij deze vereist is.

## <a name="advanced-topics-use-transactions-with-partitioned-entities"></a>Onderwerpen over geavanceerde: het gebruik van transacties met gepartitioneerde entiteiten
Berichten die worden verzonden als onderdeel van een transactie moeten een partitiesleutel opgeven. Dit is een van de volgende eigenschappen Hallo: [BrokeredMessage.SessionId][BrokeredMessage.SessionId], [BrokeredMessage.PartitionKey][BrokeredMessage.PartitionKey], of [ BrokeredMessage.MessageId][BrokeredMessage.MessageId]. Alle berichten die worden verzonden als onderdeel van dezelfde transactie moet opgeven Hallo Hallo dezelfde partitiesleutel. Als u een bericht zonder een partitiesleutel binnen een transactie toosend probeert, betekent dit dat Service Bus een ongeldige bewerking-uitzondering geretourneerd. Als u probeert meerdere berichten binnen dezelfde transactie met verschillende Hallo toosend retourneert partitiesleutels, Service Bus een ongeldige bewerking uitzondering. Bijvoorbeeld:

```csharp
CommittableTransaction committableTransaction = new CommittableTransaction();
using (TransactionScope ts = new TransactionScope(committableTransaction))
{
    BrokeredMessage msg = new BrokeredMessage("This is a message");
    msg.PartitionKey = "myPartitionKey";
    messageSender.Send(msg); 
    ts.Complete();
}
committableTransaction.Commit();
```

Als een Hallo-eigenschappen die als een partitiesleutel fungeren is ingesteld, Hallo Service Bus pincodes bericht tooa specifieke fragment. Dit probleem treedt al dan niet een transactie wordt gebruikt. Het verdient aanbeveling dat u geen een partitiesleutel opgeeft als het is niet nodig.

## <a name="using-sessions-with-partitioned-entities"></a>Met behulp van sessies met gepartitioneerde entiteiten
toosend een transactionele berichten tooa sessie-bewuste onderwerp of wachtrij, het Hallo-bericht moet hebben Hallo [BrokeredMessage.SessionId] [ BrokeredMessage.SessionId] eigenschap is ingesteld. Als hello [BrokeredMessage.PartitionKey] [ BrokeredMessage.PartitionKey] eigenschap ook is opgegeven, moet dit identieke toohello [SessionId] [ SessionId] eigenschap. Als deze verschillen, wordt met Service Bus een ongeldige bewerking-uitzondering geretourneerd.

In tegenstelling tot gewone (niet-gepartitioneerde) wachtrijen en onderwerpen is het niet mogelijk toouse een enkele transactie toosend meerdere berichten toodifferent sessies. Als er is geprobeerd, wordt met Service Bus een ongeldige bewerking-uitzondering geretourneerd. Bijvoorbeeld:

```csharp
CommittableTransaction committableTransaction = new CommittableTransaction();
using (TransactionScope ts = new TransactionScope(committableTransaction))
{
    BrokeredMessage msg = new BrokeredMessage("This is a message");
    msg.SessionId = "mySession";
    messageSender.Send(msg); 
    ts.Complete();
}
committableTransaction.Commit();
```

## <a name="automatic-message-forwarding-with-partitioned-entities"></a>Automatische bericht doorsturen met gepartitioneerde entiteiten
Service Bus ondersteunt automatische bericht doorsturen van aan of tussen gepartitioneerde entiteiten. Automatische tooenable-bericht doorsturen, stel Hallo [QueueDescription.ForwardTo] [ QueueDescription.ForwardTo] -eigenschap op Hallo bronwachtrij of abonnement. Als een partitiesleutel is opgegeven voor het Hallo-bericht ([SessionId][SessionId], [PartitionKey][PartitionKey], of [MessageId] [ MessageId]), die de partitiesleutel wordt gebruikt voor Hallo doelentiteit.

## <a name="considerations-and-guidelines"></a>Overwegingen en richtlijnen
* **Hoge consistentie functies**: als een entiteit maakt gebruik van functies zoals sessies, detectie van duplicaten of expliciete controle van de partitiesleutel wordt Hallo messaging bewerkingen altijd gerouteerde toospecific fragmenten zijn. Als een Hallo fragmenten intensief verkeer ondervindt of Hallo onderliggende archief niet in orde is, wordt deze bewerkingen mislukken en beschikbaarheid wordt beperkt. Over het algemeen is Hallo consistentie nog steeds veel hoger zijn dan niet-gepartitioneerde entiteiten; alleen een subset van verkeer ondervindt problemen als tegengestelde tooall Hallo verkeer. Zie voor meer informatie dit [bespreking van de beschikbaarheid en consistentie](../event-hubs/event-hubs-availability-and-consistency.md).
* **Beheer**: bewerkingen zoals het maken, bijwerken en verwijderen moeten worden uitgevoerd op alle Hallo fragmenten van Hallo entiteit. Als een fragment slecht is kan dit leiden tot fouten voor deze bewerkingen. Voor de Get-bewerking hello, moet informatie zoals bericht telt worden samengevoegd uit alle fragmenten. Als een fragment niet in orde is, wordt Hallo entiteit beschikbaarheidsstatus gerapporteerd als beperkt.
* **Laag volume bericht scenario's**: voor dergelijke scenario's, met name wanneer u Hallo HTTP-protocol, moet u wellicht tooperform meerdere ontvangstbewerkingen in volgorde tooobtain alle Hallo-berichten. Voor ontvangstaanvragen, Hallo-front-end voert een receive op alle Hallo fragmenten en plaatst alle Hallo-antwoorden die worden ontvangen. Een aanvraag van de volgende ontvangen op Hallo van dezelfde verbinding wilt profiteren van deze opslaan in cache en latenties ontvangen, lager zal zijn. Als u meerdere verbindingen of HTTP gebruiken, stelt die een nieuwe verbinding voor elke aanvraag. Als zodanig er is geen garantie dat deze op Hallo neerzetten zou hetzelfde knooppunt. Als alle bestaande berichten worden vergrendeld en in de cache opgeslagen in een andere front-end Hallo ontvangen bewerking retourneert **null**. Berichten uiteindelijk verlopen en u ze opnieuw kunt ontvangen. HTTP-keepalive wordt aanbevolen.
* **Bladeren/Peek berichten**: [PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_) altijd retourneert geen Hallo aantal berichten dat is opgegeven in Hallo [MessageCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MessageCount) eigenschap. Er zijn twee veelvoorkomende redenen voor dit. Een reden hiervoor is dat Hallo geaggregeerde grootte van verzameling Hallo berichten overschrijdt de maximale grootte van de Hallo van 256KB. Een andere reden is dat als Hallo wachtrij of onderwerp Hallo [EnablePartitioning eigenschap](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_EnablePartitioning) instellen te**true**, een partitie geen voldoende berichten toocomplete Hallo aangevraagd aantal berichten. In het algemeen als een toepassing wil tooreceive een bepaald aantal berichten, deze moet aanroepen [PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_) herhaaldelijk totdat het aantal berichten ophalen of er geen meer berichten toopeek zijn. Zie voor meer informatie, waaronder codevoorbeelden [QueueClient.PeekBatch](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_PeekBatch_System_Int32_) of [SubscriptionClient.PeekBatch](/dotnet/api/microsoft.servicebus.messaging.subscriptionclient#Microsoft_ServiceBus_Messaging_SubscriptionClient_PeekBatch_System_Int32_).

## <a name="latest-added-features"></a>Meest recente extra functies
* Toevoegen of verwijderen regel wordt nu ondersteund met gepartitioneerde entiteiten. Verschillend zijn van niet-gepartitioneerde entiteiten, deze bewerkingen worden niet ondersteund onder transacties. 
* AMQP wordt nu ondersteund voor het verzenden en ontvangen van berichten tooand van een gepartitioneerde entiteit.
* AMQP wordt nu ondersteund voor Hallo volgende bewerkingen: [Batch verzenden](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_SendBatch_System_Collections_Generic_IEnumerable_Microsoft_ServiceBus_Messaging_BrokeredMessage__), [Batch ontvangen](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_ReceiveBatch_System_Int32_), [ontvangen door volgnummer](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_Receive_System_Int64_), [inspecteren](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_Peek), [ Vernieuwen van de vergrendeling](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_RenewMessageLock_System_Guid_), [bericht plannen](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_ScheduleMessageAsync_Microsoft_ServiceBus_Messaging_BrokeredMessage_System_DateTimeOffset_), [geplande bericht annuleren](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_CancelScheduledMessageAsync_System_Int64_), [regel toevoegen](/dotnet/api/microsoft.servicebus.messaging.ruledescription), [regel verwijderen](/dotnet/api/microsoft.servicebus.messaging.ruledescription), [Sessie vernieuwen vergrendeling](/dotnet/api/microsoft.servicebus.messaging.messagesession#Microsoft_ServiceBus_Messaging_MessageSession_RenewLock), [Set sessiestatus](/dotnet/api/microsoft.servicebus.messaging.messagesession#Microsoft_ServiceBus_Messaging_MessageSession_SetState_System_IO_Stream_), [Get-sessiestatus](/dotnet/api/microsoft.servicebus.messaging.messagesession#Microsoft_ServiceBus_Messaging_MessageSession_GetState), en [opsommen sessies](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_GetMessageSessionsAsync).

## <a name="partitioned-entities-limitations"></a>Gepartitioneerde entiteiten beperkingen
Service Bus legt momenteel Hallo volgen beperkingen op gepartitioneerde wachtrijen en onderwerpen:

* Gepartitioneerde wachtrijen en onderwerpen ondersteunen geen verzenden van berichten die deel uitmaken van toodifferent sessies in één transactie.
* Service Bus kunt momenteel up too100 gepartitioneerd wachtrijen en onderwerpen per naamruimte. Elke gepartitioneerde wachtrij of onderwerp activeringservices, telt aantal Hallo quotum van 10.000 entiteiten per naamruimte (niet van toepassing tooPremium laag).

## <a name="next-steps"></a>Volgende stappen
Zie Hallo bespreking van [AMQP 1.0-ondersteuning voor Service Bus-wachtrijen en onderwerpen gepartitioneerd] [ AMQP 1.0 support for Service Bus partitioned queues and topics] toolearn meer over berichtentiteiten partitioneren. 

[Service Bus architecture]: service-bus-architecture.md
[Azure portal]: https://portal.azure.com
[QueueDescription.EnablePartitioning]: /dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_EnablePartitioning
[TopicDescription.EnablePartitioning]: /dotnet/api/microsoft.servicebus.messaging.topicdescription#Microsoft_ServiceBus_Messaging_TopicDescription_EnablePartitioning
[BrokeredMessage.SessionId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId
[BrokeredMessage.PartitionKey]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_PartitionKey
[SessionId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_SessionId
[PartitionKey]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_PartitionKey
[QueueDescription.RequiresDuplicateDetection]: /dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_RequiresDuplicateDetection
[BrokeredMessage.MessageId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId
[MessageId]: /dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_MessageId
[MessagingFactorySettings.OperationTimeout]: /dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout
[OperationTimeout]: /dotnet/api/microsoft.servicebus.messaging.messagingfactorysettings#Microsoft_ServiceBus_Messaging_MessagingFactorySettings_OperationTimeout
[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[AMQP 1.0 support for Service Bus partitioned queues and topics]: service-bus-partitioned-queues-and-topics-amqp-overview.md
