---
title: aaaCreate toepassingen die gebruikmaken van Azure Service Bus-onderwerpen en abonnementen | Microsoft Docs
description: Inleiding toohello voor publiceren / abonneren mogelijkheden die worden aangeboden door Service Bus-onderwerpen en abonnementen.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a48fc9b0-b7b0-464e-8187-a517bf8b4eb4
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/07/2017
ms.author: sethm
ms.openlocfilehash: f6d7de46ace7bd5b49de612db213ced789308d91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-applications-that-use-service-bus-topics-and-subscriptions"></a>Toepassingen die gebruikmaken van Service Bus-onderwerpen en abonnementen maken
Azure Service Bus ondersteunt een set van cloud-gebaseerde, bericht georiënteerd middleware-technologieën waaronder betrouwbare message Queuing- en duurzame publiceren/abonneren messaging. In dit artikel is gebaseerd op Hallo informatie in [maken van toepassingen die gebruikmaken van Service Bus-wachtrijen](service-bus-create-queues.md) en biedt een inleiding toohello publiceren/abonneren mogelijkheden die worden aangeboden door Service Bus-onderwerpen.

## <a name="evolving-retail-scenario"></a>Zich ontwikkelende retail-scenario
In dit artikel blijft Hallo retail-scenario gebruikt in [maken van toepassingen die gebruikmaken van Service Bus-wachtrijen](service-bus-create-queues.md). Intrekken verkoopgegevens uit afzonderlijke punt van verkooppunten (POS)-aansluitingen moet gerouteerde tooan inventaris beheersysteem dat gebruikmaakt van die gegevens toodetermine wanneer stock toobe aangevuld heeft. Elke POS-terminal rapporteert de verkoopgegevens door het verzenden van berichten toohello **DataCollectionQueue** wachtrij, waar ze blijven totdat ze worden ontvangen door het beheersysteem Hallo-inventaris, zoals hier wordt weergegeven:

![Servicebus 1](./media/service-bus-create-topics-subscriptions/IC657161.gif)

Dit scenario wordt een nieuwe vereiste is tooevolve toohello system toegevoegd: Hallo winkeleigenaar wil toobe kunnen toomonitor hoe Hallo store in realtime presteert.

tooaddress deze vereiste Hallo system moet 'Tik op"uitgeschakeld Hallo verkoopgegevens stroom. We willen nog steeds dat elk bericht verzonden door Hallo POS aansluitingen toobe toohello inventaris beheersysteem als voordat verzonden, maar we willen dat een ander exemplaar van elk bericht dat we toopresent Hallo dashboard weergave toohello winkeleigenaar kunnen gebruiken.

In een situatie zoals deze, waarin u elk bericht toobe verbruikt door meerdere partijen nodig kunt u Service Bus *onderwerpen*. Onderwerpen bevatten een patroon voor publiceren/abonneren waarin elk gepubliceerde bericht tooone beschikbaar wordt gesteld of meer abonnementen die zijn geregistreerd bij Hallo onderwerp. In tegenstelling met wachtrijen wordt elk bericht ontvangen door een enkele gebruiker.

Tooa onderwerp-berichten worden verzonden in Hallo dezelfde manier als ze tooa wachtrij worden verzonden. Echter worden berichten niet ontvangen van Hallo onderwerp rechtstreeks; ze worden ontvangen van abonnementen. U kunt een abonnement tooa onderwerp beschouwen als een virtuele wachtrij die kopieën van Hallo-berichten die worden verzonden toothat onderwerp ontvangt. Berichten worden ontvangen van een abonnement Hallo op dezelfde manier als ze worden ontvangen van een wachtrij.

Als u terugkeert toohello retail-scenario, Hallo wachtrij wordt vervangen door een onderwerp en een abonnement wordt toegevoegd, welke systeemonderdeel Hallo inventaris management kunt gebruiken. Hallo system verschijnt nu als volgt:

![Servicebus 2](./media/service-bus-create-topics-subscriptions/IC657165.gif)

Hallo configuratie hier voert dezelfde toohello vorige op basis van een wachtrij ontwerp. Dat wil zeggen toohello onderwerp verzonden berichten worden gerouteerd toohello **inventaris** abonnement, van welke Hallo **voorraadbeheer** ze worden verbruikt.

In de volgorde toosupport Hallo management dashboard maken we een tweede abonnement op Hallo onderwerp, zoals hier wordt weergegeven:

![Servicebus 3](./media/service-bus-create-topics-subscriptions/IC657166.gif)

Met deze configuratie bestaat elk bericht van Hallo POS-aansluitingen beschikbaar tooboth hello **Dashboard** en **inventaris** abonnementen.

## <a name="show-me-hello-code"></a>Hallo code weergeven
Hallo artikel [maken van toepassingen die gebruikmaken van Service Bus-wachtrijen](service-bus-create-queues.md) wordt beschreven hoe toosign voor een Azure-account en een Servicenaamruimte maken. Hallo gemakkelijkste manier tooreference Service Bus-afhankelijkheden tooinstall Hallo Service Bus is [Nuget-pakket](https://www.nuget.org/packages/WindowsAzure.ServiceBus/). U kunt ook Hallo Service Bus-bibliotheken vinden als onderdeel van hello Azure SDK. Hallo downloaden is beschikbaar op Hallo [-SDK van Azure-downloadpagina](https://azure.microsoft.com/downloads/).

### <a name="create-hello-topic-and-subscriptions"></a>Hallo-onderwerp en abonnementen maken
Beheerbewerkingen voor Service Bus messaging-entiteiten (wachtrijen en publiceren/abonneren onderwerpen) worden uitgevoerd via Hallo [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) klasse. Juiste referenties vereist zijn in de volgorde toocreate een **NamespaceManager** exemplaar voor een bepaalde naamruimte. Service Bus maakt gebruik van een [Shared Access Signature (SAS)](service-bus-sas.md) op basis van het beveiligingsmodel. Hallo [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) klasse vertegenwoordigt een beveiligingstokenprovider met ingebouwde factorymethoden retourneren sommige bekende token providers. We gebruiken een [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) methode toohold Hallo SAS-referenties. Hallo [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) exemplaar vervolgens met het basisadres van Hallo Service Bus-naamruimte en de tokenprovider Hallo Hallo is samengesteld.

Hallo [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) klasse biedt methoden toocreate, opsommen en verwijderen van berichtentiteiten. code die hier wordt weergegeven ziet hoe Hallo Hallo **NamespaceManager** exemplaar is gemaakt en gebruikt toocreate hello **DataCollectionTopic** onderwerp.

```csharp
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", "test-blog", string.Empty);
string name = "RootManageSharedAccessKey";
string key = "abcdefghijklmopqrstuvwxyz";

TokenProvider tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(name, key);
NamespaceManager namespaceManager = new NamespaceManager(uri, tokenProvider);

namespaceManager.CreateTopic("DataCollectionTopic");
```

Houd er rekening mee dat er overloads van Hallo zijn [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_) methode waarmee u tooset eigenschappen van Hallo onderwerp. U kunt bijvoorbeeld instellen dat Hallo time to live (TTL) standaardwaarde voor toohello onderwerp verzonden berichten. Vervolgens voegt u Hallo **inventaris** en **Dashboard** abonnementen.

```csharp
namespaceManager.CreateSubscription("DataCollectionTopic", "Inventory");
namespaceManager.CreateSubscription("DataCollectionTopic", "Dashboard");
```

### <a name="send-messages-toohello-topic"></a>Verzenden van berichten toohello onderwerp
Voor runtime-bewerkingen voor Service Bus-entiteiten; bijvoorbeeld, verzenden en ontvangen berichten, een toepassing moet eerst maken een [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#microsoft_servicebus_messaging_messagingfactory) object. Vergelijkbare toohello [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) klasse hello **MessagingFactory** exemplaar uit het basisadres van Hallo-Servicenaamruimte en tokenprovider Hallo Hallo is gemaakt.

```
MessagingFactory factory = MessagingFactory.Create(uri, tokenProvider);
```

Verzonden berichten tooand ontvangen van Service Bus-onderwerpen, zijn exemplaren van Hallo [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) klasse. Deze klasse bestaat uit een aantal standaardeigenschappen (zoals [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) en [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), een woordenlijst die wordt gebruikt toohold toepassingseigenschappen en een hoofdtekst met willekeurige toepassingsgegevens. Een toepassing hello instantie worden ingesteld door door te geven in elk serialiseerbaar object (hello volgende voorbeeld wordt doorgegeven een **SalesData** -object met Hallo verkoopgegevens uit Hallo POS terminal), worden met bepaalde Hallo [ DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx) tooserialize Hallo-object. U kunt ook een [stroom](https://msdn.microsoft.com/library/system.io.stream.aspx) object kan worden opgegeven.

```csharp
BrokeredMessage bm = new BrokeredMessage(salesData);
bm.Label = "SalesReport";
bm.Properties["StoreName"] = "Redmond";
bm.Properties["MachineID"] = "POS_1";
```

Hallo gemakkelijkste manier toosend berichten toohello onderwerp is toouse [CreateMessageSender](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageSender_System_String_) toocreate een [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) object rechtstreeks vanuit Hallo [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) exemplaar:

```csharp
MessageSender sender = factory.CreateMessageSender("DataCollectionTopic");
sender.Send(bm);
```

### <a name="receive-messages-from-a-subscription"></a>Berichten ontvangen van een abonnement
Vergelijkbare toousing wachtrijen, tooreceive berichten van een abonnement kunt u een [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) -object dat u rechtstreeks vanuit Hallo maken [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) met [ CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_). U kunt een Hallo twee verschillende modi ontvangen (**ReceiveAndDelete** en **PeekLock**), zoals beschreven in [maken van toepassingen die gebruikmaken van Service Bus-wachtrijen](service-bus-create-queues.md).

Houd er rekening mee dat bij het maken van een **MessageReceiver** voor abonnementen, Hallo *entityPath* parameter is van het formulier Hallo `topicPath/subscriptions/subscriptionName`. Daarom toocreate een **MessageReceiver** voor Hallo **inventaris** abonnement Hallo **DataCollectionTopic** onderwerp *entityPath*te moet worden ingesteld`DataCollectionTopic/subscriptions/Inventory`. Hallo code er als volgt:

```csharp
MessageReceiver receiver = factory.CreateMessageReceiver("DataCollectionTopic/subscriptions/Inventory");
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

## <a name="subscription-filters"></a>Abonnementsfilters
Tot nu toe, in dit scenario alle berichten die verstuurd toohello onderwerp bestaan abonnementen beschikbaar tooall geregistreerd. Hallo hier sleutel zinsnede worden 'beschikbaar gesteld." Bij het Service Bus-abonnementen Zie alle berichten die verstuurd toohello onderwerp, kunt u alleen een subset van deze wachtrij berichten toohello virtuele abonnement kunt kopiëren. Dit wordt uitgevoerd met behulp van abonnement *filters*. Wanneer u een abonnement maakt, kunt u opgeven dat een filterexpressie Hallo vorm van een style-predikaat van SQL92 wordt geïmplementeerd dat via het Hallo-eigenschappen van het Hallo-bericht werkt, beide Systeemeigenschappen Hallo (bijvoorbeeld [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label)) en de toepassing hello eigenschappen, zoals **StoreName** in het vorige voorbeeld Hallo.

Hallo scenario tooillustrate in ontwikkeling dit, is een tweede archief toobe toegevoegde tooour retail-scenario. Verkoopgegevens uit alle Hallo POS-aansluitingen van beide winkels nog steeds toobe gerouteerd toohello gecentraliseerde inventaris management-systeem, maar een winkelmanager met Hallo dashboard hulpprogramma is alleen geïnteresseerd in Hallo prestaties van dat archief. U kunt filteren tooachieve dit abonnement. Wanneer Hallo POS-aansluitingen berichten publiceert, ze in te stellen Hallo **StoreName** eigenschap van toepassing op het Hallo-bericht. Bijvoorbeeld twee winkels gegeven **Redmond** en **Seattle**, Hallo POS-aansluitingen in Hallo Redmond opslaan stempel hun verkoopgegevens met berichten een **StoreName** gelijk zijn aan te **Redmond**, terwijl Hallo Seattle opslaan POS aansluitingen gebruik een **StoreName** gelijk zijn aan te**Seattle**. de winkelmanager Hallo Hallo Redmond alleen opslaan wil toosee gegevens uit de POS-aansluitingen. Hallo-systeem weergegeven als volgt:

![Service-Bus4](./media/service-bus-create-topics-subscriptions/IC657167.gif)

tooset deze routering geïnstalleerd, hebt u Hallo **Dashboard** abonnement als volgt:

```csharp
SqlFilter dashboardFilter = new SqlFilter("StoreName = 'Redmond'");
namespaceManager.CreateSubscription("DataCollectionTopic", "Dashboard", dashboardFilter);
```

Met deze [abonnementfilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), alleen berichten met Hallo **StoreName** eigenschappenset te**Redmond** worden virtuele wachtrij van de gekopieerde toohello voor Hallo **Dashboard** abonnement. Er is veel meer toosubscription filteren, maar. Toepassingen kunnen meerdere filterregels voor de per abonnement bij toevoeging toohello mogelijkheid toomodify Hallo eigenschappen van een bericht hebben het doorgeven van het abonnement tooa virtuele wachtrij.

## <a name="summary"></a>Samenvatting
Alle Hallo redenen toouse queuing beschreven in [maken van toepassingen die gebruikmaken van Service Bus-wachtrijen](service-bus-create-queues.md) tootopics, ook specifiek van toepassing:

* Tijdelijke ontkoppeling – bericht producenten en consumenten hebben geen toobe online op Hallo hetzelfde moment.
* Herverdeling van – pieken in load zijn vloeiend moeten worden gemaakt door Hallo onderwerp inschakelen in beslag neemt toepassingen toobe ingericht voor gemiddelde belasting in plaats van piekbelasting.
* Taakverdeling: vergelijkbare tooa wachtrij, u kunt meerdere concurrerende consumenten luistert op één abonnement, met elk bericht doorgegeven tooonly van Hallo consumenten, waardoor taakverdeling hebben.
* Losse koppeling – u kunt ontwikkelen Hallo messaging-netwerk zonder bestaande eindpunten; bijvoorbeeld, u abonnementen toevoegt of filters tooa onderwerp tooallow wijzigen voor nieuwe gebruikers.

## <a name="next-steps"></a>Volgende stappen

Zie [maken van toepassingen die gebruikmaken van Service Bus-wachtrijen](service-bus-create-queues.md) voor meer informatie over hoe toouse in Hallo POS retail-scenario wachtrijen.

