---
title: Toepassingen die gebruikmaken van Azure Service Bus-onderwerpen en abonnementen maken | Microsoft Docs
description: Inleiding tot het publiceren-abonneren mogelijkheden die worden aangeboden door Service Bus-onderwerpen en abonnementen.
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
ms.openlocfilehash: eb01120ce9578f716e5381c107faa93f0b36e358
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="create-applications-that-use-service-bus-topics-and-subscriptions"></a>Toepassingen die gebruikmaken van Service Bus-onderwerpen en abonnementen maken
Azure Service Bus ondersteunt een set van cloud-gebaseerde, bericht georiënteerd middleware-technologieën waaronder betrouwbare message Queuing- en duurzame publiceren/abonneren messaging. In dit artikel is gebaseerd op de informatie in [maken van toepassingen die gebruikmaken van Service Bus-wachtrijen](service-bus-create-queues.md) en biedt een inleiding tot de mogelijkheden voor publiceren/abonneren die worden aangeboden door Service Bus-onderwerpen.

## <a name="evolving-retail-scenario"></a>Zich ontwikkelende retail-scenario
In dit artikel blijft de retail-scenario gebruikt in [maken van toepassingen die gebruikmaken van Service Bus-wachtrijen](service-bus-create-queues.md). Intrekken die verkoopgegevens uit afzonderlijke punt van verkooppunten (POS) aansluitingen moeten worden doorgestuurd naar een inventaris van een beheersysteem dat gebruikmaakt van die gegevens om te bepalen wanneer stock moet worden aangevuld. Elke POS-terminal rapporteert de verkoopgegevens door berichten verzenden naar de **DataCollectionQueue** wachtrij, waar ze blijven totdat ze worden ontvangen door het beheersysteem inventarisatie als volgt te werk:

![Servicebus 1](./media/service-bus-create-topics-subscriptions/IC657161.gif)

Voor het ontwikkelen van dit scenario, een nieuwe vereiste is toegevoegd aan het systeem: de winkeleigenaar wil kunt bijhouden hoe de store presteert in realtime.

Om deze vereiste op te lossen, het systeem moet 'Tik op"uit de stroom verkoopgegevens. We willen nog steeds dat elk bericht verzonden door de POS-aansluitingen worden verzonden naar het beheersysteem inventaris als voordat, maar we willen dat een ander exemplaar van elk bericht die u gebruiken kunt om de dashboardweergave naar de store-eigenaar.

In een situatie zoals deze, waarin u vereisen dat elk bericht om te worden verbruikt door meerdere partijen, kunt u Service Bus *onderwerpen*. Onderwerpen bevatten een patroon voor publiceren/abonneren waarin elk gepubliceerde bericht beschikbaar wordt gesteld aan een of meer abonnementen die zijn geregistreerd bij het onderwerp. In tegenstelling met wachtrijen wordt elk bericht ontvangen door een enkele gebruiker.

Berichten worden verzonden naar een onderwerp op dezelfde manier als ze worden verzonden naar een wachtrij. Echter worden berichten niet ontvangen van het onderwerp rechtstreeks; ze worden ontvangen van abonnementen. U kunt zien van een abonnement op een onderwerp als een virtuele wachtrij die kopieën van de berichten die worden verzonden naar dat onderwerp ontvangt. Berichten worden ontvangen van een abonnement op dezelfde manier als ze worden ontvangen van een wachtrij.

Ga terug naar de retail-scenario, de wachtrij wordt vervangen door een onderwerp en een abonnement wordt toegevoegd, dat de inventariscomponent van de management-systeem kunt gebruiken. Het systeem wordt nu weergegeven als volgt:

![Servicebus 2](./media/service-bus-create-topics-subscriptions/IC657165.gif)

De configuratie van de hier voert dezelfde in het vorige ontwerp op basis van een wachtrij. Dat wil zeggen verzonden berichten aan het onderwerp worden doorgestuurd naar de **inventaris** abonnement, van waaruit de **voorraadbeheer** ze worden verbruikt.

Om het dashboard management te ondersteunen, maken we een tweede abonnement in het onderwerp als volgt te werk:

![Servicebus 3](./media/service-bus-create-topics-subscriptions/IC657166.gif)

Met deze configuratie kunt elk bericht uit de POS-aansluitingen beschikbaar wordt gesteld aan zowel de **Dashboard** en **inventaris** abonnementen.

## <a name="show-me-the-code"></a>De code weergeven
Het artikel [maken van toepassingen die gebruikmaken van Service Bus-wachtrijen](service-bus-create-queues.md) wordt beschreven hoe u zich aanmeldt voor een Azure-account en een Servicenaamruimte maken. De eenvoudigste manier om te verwijzen naar Service Bus-afhankelijkheden voor het installeren van de Service Bus is [Nuget-pakket](https://www.nuget.org/packages/WindowsAzure.ServiceBus/). U kunt ook de Service Bus-bibliotheken vinden als onderdeel van de Azure SDK. Het downloaden is beschikbaar op de [-SDK van Azure-downloadpagina](https://azure.microsoft.com/downloads/).

### <a name="create-the-topic-and-subscriptions"></a>Het onderwerp en abonnementen maken
Beheerbewerkingen voor Service Bus messaging-entiteiten (wachtrijen en publiceren/abonneren onderwerpen) worden uitgevoerd via de [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) klasse. Juiste referenties zijn vereist voor het maken van een **NamespaceManager** exemplaar voor een bepaalde naamruimte. Service Bus maakt gebruik van een [Shared Access Signature (SAS)](service-bus-sas.md) op basis van het beveiligingsmodel. De [TokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#microsoft_servicebus_tokenprovider) klasse vertegenwoordigt een beveiligingstokenprovider met ingebouwde factorymethoden retourneren sommige bekende token providers. We gebruiken een [CreateSharedAccessSignatureTokenProvider](/dotnet/api/microsoft.servicebus.tokenprovider#Microsoft_ServiceBus_TokenProvider_CreateSharedAccessSignatureTokenProvider_System_String_) methode voor het opslaan van de SAS-referenties. De [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) exemplaar vervolgens met het basisadres van de Service Bus-naamruimte en de tokenprovider is samengesteld.

De [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) klasse biedt methoden voor het maken, opsommen en verwijderen van berichtentiteiten. De code die hier toont weergegeven wordt hoe de **NamespaceManager** exemplaar is gemaakt en gebruikt voor het maken van de **DataCollectionTopic** onderwerp.

```csharp
Uri uri = ServiceBusEnvironment.CreateServiceUri("sb", "test-blog", string.Empty);
string name = "RootManageSharedAccessKey";
string key = "abcdefghijklmopqrstuvwxyz";

TokenProvider tokenProvider = TokenProvider.CreateSharedAccessSignatureTokenProvider(name, key);
NamespaceManager namespaceManager = new NamespaceManager(uri, tokenProvider);

namespaceManager.CreateTopic("DataCollectionTopic");
```

Er zijn overloads van de [CreateTopic](/dotnet/api/microsoft.servicebus.namespacemanager#Microsoft_ServiceBus_NamespaceManager_CreateTopic_System_String_) methode waarmee u eigenschappen van het onderwerp in te stellen. U kunt bijvoorbeeld instellen dat de time-to-live (TTL) standaardwaarde voor berichten die worden verzonden naar het onderwerp. Vervolgens voegt u de **inventaris** en **Dashboard** abonnementen.

```csharp
namespaceManager.CreateSubscription("DataCollectionTopic", "Inventory");
namespaceManager.CreateSubscription("DataCollectionTopic", "Dashboard");
```

### <a name="send-messages-to-the-topic"></a>Berichten naar het onderwerp verzenden
Voor runtime-bewerkingen voor Service Bus-entiteiten; bijvoorbeeld, verzenden en ontvangen berichten, een toepassing moet eerst maken een [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#microsoft_servicebus_messaging_messagingfactory) object. Net als bij de [NamespaceManager](/dotnet/api/microsoft.servicebus.namespacemanager#microsoft_servicebus_namespacemanager) klasse, de **MessagingFactory** exemplaar wordt gemaakt van het basisadres van de Servicenaamruimte en de tokenprovider.

```
MessagingFactory factory = MessagingFactory.Create(uri, tokenProvider);
```

Berichten worden verzonden naar en ontvangen van Service Bus-onderwerpen, zijn exemplaren van de [BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage) klasse. Deze klasse bestaat uit een aantal standaardeigenschappen (zoals [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.label?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label) en [TimeToLive](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage.timetolive?view=azureservicebus-4.0.0#Microsoft_ServiceBus_Messaging_BrokeredMessage_TimeToLive)), een woordenlijst die wordt gebruikt om de toepassingseigenschappen van de en een hoofdtekst met willekeurige toepassingsgegevens. Een toepassing kan de instantie ingesteld door door te geven in elk serialiseerbaar object (in het volgende voorbeeld wordt doorgegeven een **SalesData** -object dat staat voor de verkoopgegevens uit de terminal POS), die wordt gebruikt de [DataContractSerializer](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractserializer.aspx) om het object te serialiseren. U kunt ook een [stroom](https://msdn.microsoft.com/library/system.io.stream.aspx) object kan worden opgegeven.

```csharp
BrokeredMessage bm = new BrokeredMessage(salesData);
bm.Label = "SalesReport";
bm.Properties["StoreName"] = "Redmond";
bm.Properties["MachineID"] = "POS_1";
```

De eenvoudigste manier om berichten te verzenden naar het onderwerp is met [CreateMessageSender](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageSender_System_String_) maken een [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender) object rechtstreeks vanuit de [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) exemplaar:

```csharp
MessageSender sender = factory.CreateMessageSender("DataCollectionTopic");
sender.Send(bm);
```

### <a name="receive-messages-from-a-subscription"></a>Berichten ontvangen van een abonnement
Vergelijkbaar met het gebruik van wachtrijen, om berichten te ontvangen van een abonnement kunt u een [MessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagereceiver) -object dat u rechtstreeks vanuit maakt de [MessagingFactory](/dotnet/api/microsoft.servicebus.messaging.messagingfactory) met [ CreateMessageReceiver](/dotnet/api/microsoft.servicebus.messaging.messagingfactory#Microsoft_ServiceBus_Messaging_MessagingFactory_CreateMessageReceiver_System_String_). U kunt een van de twee verschillende modi ontvangen (**ReceiveAndDelete** en **PeekLock**), zoals beschreven in [maken van toepassingen die gebruikmaken van Service Bus-wachtrijen](service-bus-create-queues.md).

Houd er rekening mee dat bij het maken van een **MessageReceiver** voor abonnementen, de *entityPath* parameter is van het formulier `topicPath/subscriptions/subscriptionName`. Daarom maken een **MessageReceiver** voor de **inventaris** abonnement van de **DataCollectionTopic** onderwerp *entityPath* moet worden ingesteld op `DataCollectionTopic/subscriptions/Inventory`. De code er als volgt:

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
Tot nu toe, in dit scenario worden alle berichten die naar het onderwerp beschikbaar gesteld aan alle geregistreerde abonnementen. De belangrijkste woordgroep hier worden 'beschikbaar gesteld." Bij het Service Bus-abonnementen Zie alle berichten die naar het onderwerp, kunt u alleen een subset van deze berichten kunt kopiëren naar de abonnementenwachtrij voor virtuele. Dit wordt uitgevoerd met behulp van abonnement *filters*. Wanneer u een abonnement maakt, kunt u een filterexpressie in de vorm van een style-predikaat van SQL92 wordt geïmplementeerd dat via de eigenschappen van het bericht, de Systeemeigenschappen werkt opgeven (bijvoorbeeld [Label](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_Label)) en de eigenschappen voor toepassingen , zoals **StoreName** in het vorige voorbeeld.

Het scenario ter illustratie in ontwikkeling, is een tweede archief worden toegevoegd aan onze retail-scenario. Verkoopgegevens uit alle van de POS-aansluitingen van beide winkels nog steeds worden doorgestuurd naar het beheersysteem gecentraliseerde voorraad, maar een winkelmanager hulpprogramma voor het dashboard is alleen geïnteresseerd in de prestaties van dat archief. U kunt filteren om dit te bereiken abonnement gebruiken. Houd er rekening mee dat wanneer de POS-aansluitingen berichten publiceert, ze ingesteld de **StoreName** eigenschap van toepassing op het bericht. Bijvoorbeeld twee winkels gegeven **Redmond** en **Seattle**, het POS-aansluitingen in het archief Redmond stempel hun verkoopgegevens berichten met een **StoreName** gelijk zijn aan **Redmond**, terwijl de Seattle opslaan POS aansluitingen gebruik een **StoreName** gelijk zijn aan **Seattle**. De winkelmanager van het archief Redmond wil alleen gegevens uit de POS-aansluitingen bekijken. Het systeem wordt als volgt weergegeven:

![Service-Bus4](./media/service-bus-create-topics-subscriptions/IC657167.gif)

Als u deze routering instelt, maakt u de **Dashboard** abonnement als volgt:

```csharp
SqlFilter dashboardFilter = new SqlFilter("StoreName = 'Redmond'");
namespaceManager.CreateSubscription("DataCollectionTopic", "Dashboard", dashboardFilter);
```

Met deze [abonnementfilter](/dotnet/api/microsoft.servicebus.messaging.sqlfilter), alleen berichten met de **StoreName** eigenschap ingesteld op **Redmond** wordt gekopieerd naar de virtuele wachtrij voor de  **Dashboard** abonnement. Er is veel meer voor het abonnement filteren, maar. Toepassingen kunnen meerdere filterregels voor de per abonnement naast de mogelijkheid om te wijzigen van de eigenschappen van een bericht zoals dit wordt doorgegeven aan de virtuele wachtrij van een abonnement hebben.

## <a name="summary"></a>Samenvatting
Alle van de redenen om te gebruiken dat wordt beschreven in queuing [maken van toepassingen die gebruikmaken van Service Bus-wachtrijen](service-bus-create-queues.md) ook van toepassing op onderwerpen, speciaal:

* Tijdelijke ontkoppeling – bericht producenten en consumenten hoeven niet te op hetzelfde moment online zijn.
* Herverdeling van – pieken in load zijn vloeiend moeten worden gemaakt door het onderwerp zodat consumerende toepassingen moeten worden ingericht voor gemiddelde belasting in plaats van piekbelasting.
* Taakverdeling – net als bij een wachtrij, kunt u meerdere concurrerende consumenten luistert op één abonnement, met elk bericht dat is doorgegeven aan slechts één van de consument, waardoor taakverdeling heeft.
* De koppeling – u kunt het messaging netwerk ontwikkelen zonder bestaande eindpunten; bijvoorbeeld, u abonnementen toevoegt of filters wijzigen naar een onderwerp om toe te staan voor nieuwe gebruikers.

## <a name="next-steps"></a>Volgende stappen

Zie [maken van toepassingen die gebruikmaken van Service Bus-wachtrijen](service-bus-create-queues.md) voor informatie over het gebruik van wachtrijen in het POS retail-scenario.

