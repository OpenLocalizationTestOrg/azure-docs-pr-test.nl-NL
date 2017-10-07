---
title: aaaOverview van transactie worden verwerkt in de Azure Service Bus | Microsoft Docs
description: Overzicht van Azure Service Bus-atomic-transacties en verzenden via
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 64449247-1026-44ba-b15a-9610f9385ed8
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: clemensv;sethm
ms.openlocfilehash: 5ed4d1fd3a089b8ebcd69a568f4ac863e753aecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-service-bus-transaction-processing"></a>Overzicht van Service Bus-transactieverwerking
Dit artikel wordt beschreven Hallo transactiemogelijkheden van Azure Service Bus. Veel van Hallo discussie wordt geïllustreerd door Hallo [atomische transacties met Service Bus-voorbeeld](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions). In dit artikel is beperkt tooan overzicht van transactieverwerking en Hallo *verzenden* functie in Service Bus, terwijl Hallo atomische transacties voorbeeld grotere en complexere binnen het bereik is.

## <a name="transactions-in-service-bus"></a>Transacties in de Servicebus
Een [transactie](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) twee of meer bewerkingen gegroepeerd in een *uitvoering bereik*. Een dergelijke transactie moet ervoor zorgen dat alle bewerkingen die tooa opgegeven groep bewerkingen behoren slagen of gezamenlijk mislukken door aard. In dit opzicht transacties fungeren als één eenheid ondergebracht, die vaak waarnaar wordt verwezen tooas *atomisch*. 

Service Bus is een broker transactionele berichten en garandeert een transactionele integriteit voor alle interne bewerkingen op basis van de bericht-stores. Alle overdrachten van berichten op de Service Bus, zoals bewegende berichten tooa [wachtrij voor onbestelbare berichten](service-bus-dead-letter-queues.md) of [automatisch doorsturen](service-bus-auto-forwarding.md) van berichten tussen entiteiten transactionele zijn. Als zodanig als Service Bus een bericht accepteert, is al opgeslagen en gelabeld met een volgnummer. Daarna de overdracht van een bericht binnen de Service Bus zijn gecoördineerde bewerkingen over entiteiten en leidt geen van beide tooloss (bron is geslaagd en mislukt als doel) of tooduplication (mislukt van de bron en doel is geslaagd) van het Hallo-bericht.

Service Bus biedt ondersteuning voor groepering bewerkingen op een enkele Berichtentiteit (wachtrij, onderwerp, abonnement) binnen Hallo bereik van een transactie. Bijvoorbeeld, kunt u verschillende berichten tooone wachtrij uit verzenden vanuit een transactiebereik en Hallo-berichten worden alleen van doorgevoerd toohello wachtrij logboek wanneer Hallo transactie is voltooid.

## <a name="operations-within-a-transaction-scope"></a>Bewerkingen binnen een transactiebereik
Hallo-bewerkingen die kunnen worden uitgevoerd vanuit een transactiebereik zijn als volgt:

* **[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: verzenden, SendAsync, SendBatch, SendBatchAsync 
* **[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: voltooid, CompleteAsync, afbreken, AbandonAsync, wachtrij voor onbestelbare, DeadletterAsync, uitstelt, DeferAsync, RenewLock, RenewLockAsync 

Ontvangen bewerkingen zijn niet toegevoegd, omdat ervan wordt uitgegaan dat de toepassing hello berichten met behulp van Hallo verkrijgt [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) modus binnen enkele lus voor ontvangen of met een [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) terugbellen en alleen vervolgens opent een transactie bereik voor de verwerking van het Hallo-bericht.

Hallo bestemming van het Hallo-bericht (voltooid, afbreken, onbestelbare, uitstellen) uitgevoerd binnen bereik van Hallo en die afhankelijk zijn van, hello algehele resultaat van Hallo transactie.

## <a name="transfers-and-send-via"></a>Overschrijvingen en 'verzenden '
tooenable transactionele overdracht van gegevens uit een wachtrij tooa processor en tooanother wachtrij, Servicebus ondersteunt *overdrachten*. In een overdrachtsbewerking een afzender eerst verzendt een bericht tooa 'wachtrij' en wachtrij Hallo verplaatst onmiddellijk Hallo-bericht toohello doelwachtrij met Hallo dezelfde robuuste transfer implementatie die automatisch doorsturen van berichten Hallo afhankelijk is bedoeld op. Hallo-bericht is nooit toegewezen toohello overdracht wachtrij logboek zodanig dat deze zichtbaar is voor consumenten Hallo overdracht wachtrij.

Hallo power van deze mogelijkheid transactionele duidelijk wanneer Hallo wachtrij zelf Hallo bron van de invoer van de afzender van het Hallo-berichten. Met andere woorden, Service Bus kunnen worden overgedragen Hallo-bericht toohello doelwachtrij 'via' hello wachtrij, tijdens het uitvoeren van een complete (of uitstelt, of onbestelbare)-bewerking op invoerbericht Hallo allemaal in een atomic-bewerking. 

### <a name="see-it-in-code"></a>Deze weergegeven in de code
tooset van deze overdracht maakt u een afzender die gericht is op de doelwachtrij Hallo via Hallo wachtrij. U hebt ook een ontvanger waarmee berichten van die dezelfde wachtrij opgehaald. Bijvoorbeeld:

```csharp
var sender = this.messagingFactory.CreateMessageSender(destinationQueue, myQueueName);
var receiver = this.messagingFactory.CreateMessageReceiver(myQueueName);
```

Vervolgens een eenvoudige transactie maakt gebruik van deze elementen, zoals in het volgende voorbeeld Hallo:

```csharp
var msg = receiver.Receive();

using (scope = new TransactionScope())
{
    // Do whatever work is required 

    var newmsg = ... // package hello result 

    msg.Complete(); // mark hello message as done
    sender.Send(newmsg); // forward hello result

    scope.Complete(); // declare hello transaction done
} 
```

## <a name="next-steps"></a>Volgende stappen

Zie de volgende artikelen voor meer informatie over Service Bus-wachtrijen Hallo:

* [Service Bus-entiteiten met automatisch doorsturen Chaining](service-bus-auto-forwarding.md)
* [Automatisch doorsturen voorbeeld](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AutoForward)
* [Atomische transacties met Service Bus-voorbeeld](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions)
* [Azure-wachtrijen en Service Bus-wachtrijen vergeleken](service-bus-azure-and-service-bus-queues-compared-contrasted.md)
* [Hoe toouse Service Bus-wachtrijen](service-bus-dotnet-get-started-with-queues.md)

