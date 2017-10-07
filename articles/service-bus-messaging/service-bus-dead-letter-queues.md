---
title: wachtrijen voor onbestelbare Bus aaaService | Microsoft Docs
description: Overzicht van Azure Service Bus-wachtrijen voor onbestelbare berichten
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 68b2aa38-dba7-491a-9c26-0289bc15d397
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/17/2017
ms.author: clemensv;sethm
ms.openlocfilehash: 1638272085b8a3a59e8814f6f943caee35a2bfdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-service-bus-dead-letter-queues"></a>Overzicht van Service Bus-wachtrijen voor onbestelbare berichten

Service Bus-wachtrijen en onderwerpabonnementen bieden u een secundaire onderliggende wachtrij aangeroepen een *wachtrij voor onbestelbare berichten* (DLQ). wachtrij voor onbestelbare berichten Hallo hoeft niet toobe expliciet gemaakt en kan niet worden verwijderd of anderszins beheerde onafhankelijk van de belangrijkste Hallo-entiteit.

Dit artikel wordt beschreven wachtrijen voor onbestelbare berichten in de Azure Service Bus. Veel van Hallo discussie wordt geïllustreerd door Hallo [wachtrijen voor onbestelbare berichten voorbeeld](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/DeadletterQueue) op GitHub.
 
## <a name="hello-dead-letter-queue"></a>wachtrij voor onbestelbare berichten Hallo

Hallo-doel van de wachtrij voor onbestelbare berichten Hallo is toohold-berichten die tooany ontvanger kunnen niet worden bezorgd of berichten die niet kunnen worden verwerkt. Berichten kunnen vervolgens worden verwijderd uit Hallo DLQ en gecontroleerd. Een toepassing kan met behulp van een operator wordt oplossen van problemen en het Hallo-bericht verzenden, meld Hallo feit dat er een fout is en corrigerende maatregelen nemen. 

Hallo DLQ vanuit een perspectief API en het protocol is voornamelijk vergelijkbare tooany andere wachtrij, behalve dat berichten kunnen alleen worden verzonden via Hallo onbestelbare gebaar van Hallo bovenliggende entiteit. Bovendien time to live is niet-naleving en u kunt een bericht van een DLQ onbestelbare niet. wachtrij voor onbestelbare berichten Hallo biedt volledige ondersteuning voor levering peek vergrendelen en transactionele bewerkingen.

Houd er rekening mee dat er geen automatische opschoning van Hallo DLQ is. Berichten blijven in Hallo DLQ totdat u ze expliciet uit Hallo DLQ en aanroep ophaalt [Complete()](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_CompleteAsync) op Hallo-bericht van onbestelbare berichten.

## <a name="moving-messages-toohello-dlq"></a>Het verplaatsen van berichten toohello DLQ

Er zijn verschillende activiteiten in de Service Bus die ertoe leiden berichten tooget toohello DLQ van binnen het Hallo dat-engine zelf berichten gepusht. Een toepassing kunt berichten toohello DLQ ook expliciet verplaatsen. 

Als u het Hallo-bericht opgehaald door Hallo broker verplaatst, twee eigenschappen toohello bericht worden toegevoegd als Hallo broker intern versie Hallo roept [wachtrij voor onbestelbare](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeadLetter_System_String_System_String_) methode op het Hallo-bericht: `DeadLetterReason` en `DeadLetterErrorDescription`.

Toepassingen kunnen hun eigen codes definiëren voor Hallo `DeadLetterReason` eigenschap, maar Hallo system sets Hallo waarden te volgen.

| Voorwaarde | DeadLetterReason | DeadLetterErrorDescription |
| --- | --- | --- |
| Altijd |HeaderSizeExceeded |Hallo is grootte voor deze stroom overschreden. |
| ! TopicDescription.<br />EnableFilteringMessagesBeforePublishing en SubscriptionDescription.<br />EnableDeadLetteringOnFilterEvaluationExceptions |uitzondering. GetType(). Naam |uitzondering. Bericht |
| EnableDeadLetteringOnMessageExpiration |TTLExpiredException |Hallo-bericht verlopen en dode is lettered. |
| SubscriptionDescription.RequiresSession |Sessie-id is null. |Sessie ingeschakeld entiteit is niet mogelijk een bericht waarvan sessie-id null is. |
| ! wachtrij voor onbestelbare berichten |MaxTransferHopCountExceeded |Null |
| Toepassing expliciete dode lettering |Opgegeven door toepassing |Opgegeven door toepassing |

## <a name="exceeding-maxdeliverycount"></a>Meer dan MaxDeliveryCount
Wachtrijen en abonnementen hebben een [QueueDescription.MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MaxDeliveryCount) en [SubscriptionDescription.MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription#Microsoft_ServiceBus_Messaging_SubscriptionDescription_MaxDeliveryCount) eigenschap respectievelijk; hello standaardwaarde is 10. Wanneer een bericht is bezorgd onder een vergrendeling ([ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode)), maar is een expliciet verlaten of Hallo vergrendeling is verlopen, Hallo-bericht [BrokeredMessage.DeliveryCount](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeliveryCount) is verhoogd. Wanneer [DeliveryCount](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage#Microsoft_ServiceBus_Messaging_BrokeredMessage_DeliveryCount) overschrijdt [MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MaxDeliveryCount), het Hallo-bericht is verplaatst toohello DLQ, geven Hallo `MaxDeliveryCountExceeded` redencode.

Dit gedrag kan niet worden uitgeschakeld, maar u kunt instellen [MaxDeliveryCount](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_MaxDeliveryCount) tooa zeer groot aantal.

## <a name="exceeding-timetolive"></a>TimeToLive overschrijdt
Wanneer Hallo [QueueDescription.EnableDeadLetteringOnMessageExpiration](/dotnet/api/microsoft.servicebus.messaging.queuedescription#Microsoft_ServiceBus_Messaging_QueueDescription_EnableDeadLetteringOnMessageExpiration) of [SubscriptionDescription.EnableDeadLetteringOnMessageExpiration](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription#Microsoft_ServiceBus_Messaging_SubscriptionDescription_EnableDeadLetteringOnMessageExpiration) eigenschap is ingesteld, te**waar** (Hallo standaardwaarde is **false**), alle verlopende berichten worden verplaatst toohello DLQ, geven Hallo `TTLExpiredException` redencode.

Houd er rekening mee dat verlopen berichten worden alleen opgeschoond en toohello DLQ daarom verplaatst als er ten minste één actieve ontvanger binnenhalen op Hallo hoofdwachtrij of abonnement. Dit gedrag is inherent aan het ontwerp.

## <a name="errors-while-processing-subscription-rules"></a>Fouten tijdens het verwerken van abonnementsregels
Wanneer Hallo [SubscriptionDescription.EnableDeadLetteringOnFilterEvaluationExceptions](/dotnet/api/microsoft.servicebus.messaging.subscriptiondescription#Microsoft_ServiceBus_Messaging_SubscriptionDescription_EnableDeadLetteringOnFilterEvaluationExceptions) eigenschap voor een abonnement is ingeschakeld, eventuele fouten die zich voordoen tijdens een abonnement SQL filterregel wordt uitgevoerd, worden vastgelegd in Hallo DLQ samen met de Hallo foutieve bericht.

## <a name="application-level-dead-lettering"></a>Op toepassingsniveau verwerking van onbestelbare berichten
In aanvulling toohello systeem geleverde verwerking van onbestelbare berichten functies, kunnen toepassingen gebruikmaken van Hallo DLQ tooexplicitly afwijzen onaanvaardbaar berichten. Dit omvat mogelijk berichten die correct kunnen niet worden verwerkt vanwege tooany soort systeemprobleem, berichten waarin een verkeerd ingedeelde nettoladingen of berichten die niet door de verificatie als sommige berichtniveau beveiligingsschema wordt gebruikt.

## <a name="dead-lettering-in-forwardto-or-sendvia-scenarios"></a>Verwerking van onbestelbare berichten in scenario's ForwardTo of SendVia

Berichten worden verzonden toohello onbestelbare wachtrij onder Hallo volgende voorwaarden:

- Een bericht wordt doorgegeven via meer dan 3 wachtrijen of onderwerpen die [aaneengeschakeld](service-bus-auto-forwarding.md).
- Hallo bestemmingswachtrij of onderwerp is uitgeschakeld of verwijderd.
- Hallo bestemmingswachtrij of onderwerp overschrijdt Hallo maximale entiteit.

tooretrieve deze berichten onbestelbare lettered kunt u een ontvanger met Hallo [FormatTransferDeadletterPath](/dotnet/api/microsoft.servicebus.messaging.queueclient#Microsoft_ServiceBus_Messaging_QueueClient_FormatTransferDeadLetterPath_System_String_) hulpprogramma methode.

## <a name="example"></a>Voorbeeld
Hallo volgende codefragment maakt een ontvanger bericht. In Hallo lus voor ontvangen van voor de hoofdwachtrij hello, Hallo code haalt het Hallo-bericht met [Receive(TimeSpan.Zero)](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_Receive_System_TimeSpan_), waarin elk bericht direct beschikbaar wordt Hallo broker tooinstantly return gevraagd of tooreturn met geen resultaat. Als het Hallo-code wordt een bericht ontvangt, het onmiddellijk verlaat, die wordt verhoogd Hallo `DeliveryCount`. Zodra het systeem Hallo Hallo-bericht toohello DLQ verplaatst, Hallo hoofdwachtrij leeg is en Hallo lus wordt afgesloten, als [ReceiveAsync](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_ReceiveAsync_System_TimeSpan_) retourneert **null**.

```csharp
var receiver = await receiverFactory.CreateMessageReceiverAsync(queueName, ReceiveMode.PeekLock);
while(true)
{
    var msg = await receiver.ReceiveAsync(TimeSpan.Zero);
    if (msg != null)
    {
        Console.WriteLine("Picked up message; DeliveryCount {0}", msg.DeliveryCount);
        await msg.AbandonAsync();
    }
    else
    {
        break;
    }
}
```

## <a name="next-steps"></a>Volgende stappen
Zie de volgende artikelen voor meer informatie over Service Bus-wachtrijen Hallo:

* [Aan de slag met Service Bus-wachtrijen](service-bus-dotnet-get-started-with-queues.md)
* [Azure-wachtrijen en Service Bus-wachtrijen vergeleken](service-bus-azure-and-service-bus-queues-compared-contrasted.md)

