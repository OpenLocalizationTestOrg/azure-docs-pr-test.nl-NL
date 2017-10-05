---
title: Overzicht van de transactie worden verwerkt in de Azure Service Bus | Microsoft Docs
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
ms.openlocfilehash: a88f2d81ab43e38c9363a67aaefc178b47bfb259
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="overview-of-service-bus-transaction-processing"></a><span data-ttu-id="c3eaf-103">Overzicht van Service Bus-transactieverwerking</span><span class="sxs-lookup"><span data-stu-id="c3eaf-103">Overview of Service Bus transaction processing</span></span>
<span data-ttu-id="c3eaf-104">Dit artikel wordt de transactiemogelijkheden van Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="c3eaf-104">This article discusses the transaction capabilities of Azure Service Bus.</span></span> <span data-ttu-id="c3eaf-105">Veel van de bespreking van de wordt geïllustreerd door het [atomische transacties met Service Bus-voorbeeld](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions).</span><span class="sxs-lookup"><span data-stu-id="c3eaf-105">Much of the discussion is illustrated by the [Atomic Transactions with Service Bus sample](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions).</span></span> <span data-ttu-id="c3eaf-106">In dit artikel is beperkt tot een overzicht van transactieverwerking en de *verzenden* functie in Service Bus, terwijl het voorbeeld atomische transacties grotere en complexere binnen het bereik is.</span><span class="sxs-lookup"><span data-stu-id="c3eaf-106">This article is limited to an overview of transaction processing and the *send via* feature in Service Bus, while the Atomic Transactions sample is broader and more complex in scope.</span></span>

## <a name="transactions-in-service-bus"></a><span data-ttu-id="c3eaf-107">Transacties in de Servicebus</span><span class="sxs-lookup"><span data-stu-id="c3eaf-107">Transactions in Service Bus</span></span>
<span data-ttu-id="c3eaf-108">Een [transactie](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) twee of meer bewerkingen gegroepeerd in een *uitvoering bereik*.</span><span class="sxs-lookup"><span data-stu-id="c3eaf-108">A [transaction](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) groups two or more operations together into an *execution scope*.</span></span> <span data-ttu-id="c3eaf-109">Een dergelijke transactie moet ervoor zorgen dat alle bewerkingen die horen bij een bepaalde groep bewerkingen slagen of gezamenlijk mislukken door aard.</span><span class="sxs-lookup"><span data-stu-id="c3eaf-109">By nature, such a transaction must ensure that all operations belonging to a given group of operations either succeed or fail jointly.</span></span> <span data-ttu-id="c3eaf-110">In dit opzicht transacties fungeren als één eenheid ondergebracht, die vaak aangeduid als *atomisch*.</span><span class="sxs-lookup"><span data-stu-id="c3eaf-110">In this respect transactions act as one unit, which is often referred to as *atomicity*.</span></span> 

<span data-ttu-id="c3eaf-111">Service Bus is een broker transactionele berichten en garandeert een transactionele integriteit voor alle interne bewerkingen op basis van de bericht-stores.</span><span class="sxs-lookup"><span data-stu-id="c3eaf-111">Service Bus is a transactional message broker and ensures transactional integrity for all internal operations against its message stores.</span></span> <span data-ttu-id="c3eaf-112">Alle overdrachten van berichten op de Service Bus, zoals het verplaatsen van berichten naar een [wachtrij voor onbestelbare berichten](service-bus-dead-letter-queues.md) of [automatisch doorsturen](service-bus-auto-forwarding.md) van berichten tussen entiteiten transactionele zijn.</span><span class="sxs-lookup"><span data-stu-id="c3eaf-112">All transfers of messages inside of Service Bus, such as moving messages to a [dead-letter queue](service-bus-dead-letter-queues.md) or [automatic forwarding](service-bus-auto-forwarding.md) of messages between entities, are transactional.</span></span> <span data-ttu-id="c3eaf-113">Als zodanig als Service Bus een bericht accepteert, is al opgeslagen en gelabeld met een volgnummer.</span><span class="sxs-lookup"><span data-stu-id="c3eaf-113">As such, if Service Bus accepts a message, it has already been stored and labeled with a sequence number.</span></span> <span data-ttu-id="c3eaf-114">Daarna de overdracht van een bericht binnen de Service Bus zijn gecoördineerde bewerkingen voor alle entiteiten en wordt geen van beide leiden tot verlies (bron is geslaagd en mislukt doel) of om te worden gedupliceerd (mislukt van de bron en doel is geslaagd) van het bericht.</span><span class="sxs-lookup"><span data-stu-id="c3eaf-114">From then on, any message transfers within Service Bus are coordinated operations across entities, and will neither lead to loss (source succeeds and target fails) or to duplication (source fails and target succeeds) of the message.</span></span>

<span data-ttu-id="c3eaf-115">Service Bus biedt ondersteuning voor groepering bewerkingen op een enkele Berichtentiteit (wachtrij, onderwerp, abonnement) binnen het bereik van een transactie.</span><span class="sxs-lookup"><span data-stu-id="c3eaf-115">Service Bus supports grouping operations against a single messaging entity (queue, topic, subscription) within the scope of a transaction.</span></span> <span data-ttu-id="c3eaf-116">Bijvoorbeeld, u kunt meerdere berichten verzenden naar een wachtrij uit vanuit een transactiebereik en de berichten worden pas doorgevoerd in de wachtrij logboek wanneer de transactie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="c3eaf-116">For example, you can send several messages to one queue from within a transaction scope, and the messages will only be committed to the queue's log when the transaction successfully completes.</span></span>

## <a name="operations-within-a-transaction-scope"></a><span data-ttu-id="c3eaf-117">Bewerkingen binnen een transactiebereik</span><span class="sxs-lookup"><span data-stu-id="c3eaf-117">Operations within a transaction scope</span></span>
<span data-ttu-id="c3eaf-118">De bewerkingen die kunnen worden uitgevoerd vanuit een transactiebereik zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="c3eaf-118">The operations that can be performed within a transaction scope are as follows:</span></span>

* <span data-ttu-id="c3eaf-119">**[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: verzenden, SendAsync, SendBatch, SendBatchAsync</span><span class="sxs-lookup"><span data-stu-id="c3eaf-119">**[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: Send, SendAsync, SendBatch, SendBatchAsync</span></span> 
* <span data-ttu-id="c3eaf-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: voltooid, CompleteAsync, afbreken, AbandonAsync, wachtrij voor onbestelbare, DeadletterAsync, uitstelt, DeferAsync, RenewLock, RenewLockAsync</span><span class="sxs-lookup"><span data-stu-id="c3eaf-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync</span></span> 

<span data-ttu-id="c3eaf-121">Ontvangen bewerkingen zijn niet toegevoegd, omdat ervan wordt uitgegaan dat de toepassing krijgt berichten met behulp van de [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) modus binnen enkele lus voor ontvangen of met een [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) callback en vervolgens pas Hiermee opent u een transactiebereik voor het verwerken van het bericht.</span><span class="sxs-lookup"><span data-stu-id="c3eaf-121">Receive operations are not included, because it is assumed that the application acquires messages using the [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, inside some receive loop or with an [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) callback, and only then opens a transaction scope for processing the message.</span></span>

<span data-ttu-id="c3eaf-122">De bestemming van het bericht (voltooid, afbreken, onbestelbare, uitstellen) uitgevoerd binnen het bereik van, en afhankelijk van de algehele uitkomst van de transactie.</span><span class="sxs-lookup"><span data-stu-id="c3eaf-122">The disposition of the message (complete, abandon, dead-letter, defer) then occurs within the scope of, and dependent on, the overall outcome of the transaction.</span></span>

## <a name="transfers-and-send-via"></a><span data-ttu-id="c3eaf-123">Overschrijvingen en 'verzenden '</span><span class="sxs-lookup"><span data-stu-id="c3eaf-123">Transfers and "send via"</span></span>
<span data-ttu-id="c3eaf-124">Om in te schakelen transactionele overdracht van gegevens uit een wachtrij op een processor en vervolgens naar een andere wachtrij, Service Bus ondersteunt *overdrachten*.</span><span class="sxs-lookup"><span data-stu-id="c3eaf-124">To enable transactional handover of data from a queue to a processor, and then to another queue, Service Bus supports *transfers*.</span></span> <span data-ttu-id="c3eaf-125">Een afzender verzendt een bericht eerst naar een wachtrij' transfer' en het bericht in de wachtrij onmiddellijk worden verplaatst naar de bestemmingswachtrij met de dezelfde robuuste overdracht implementatie die afhankelijk is van het automatisch doorsturen van berichten in een overdrachtsbewerking voor.</span><span class="sxs-lookup"><span data-stu-id="c3eaf-125">In a transfer operation, a sender first sends a message to a "transfer queue" and the transfer queue immediately moves the message to the intended destination queue using the same robust transfer implementation that the auto-forward capability relies on.</span></span> <span data-ttu-id="c3eaf-126">Het bericht is nooit doorgevoerd in het logboek van de wachtrij zodanig dat deze zichtbaar is voor de overdracht van de wachtrij consumenten.</span><span class="sxs-lookup"><span data-stu-id="c3eaf-126">The message is never committed to the transfer queue's log in a way that it becomes visible for the transfer queue's consumers.</span></span>

<span data-ttu-id="c3eaf-127">De kracht van deze mogelijkheid transactionele wordt zichtbaar wanneer de wachtrij zelf de bron van de invoer berichten van de afzender is.</span><span class="sxs-lookup"><span data-stu-id="c3eaf-127">The power of this transactional capability becomes apparent when the transfer queue itself is the source of the sender's input messages.</span></span> <span data-ttu-id="c3eaf-128">Met andere woorden, Service Bus kunt overdragen het bericht naar de doelwachtrij 'via' de wachtrij, tijdens het uitvoeren van een complete (of uitstelt, of onbestelbare)-bewerking op het invoerbericht, allemaal in een atomic-bewerking.</span><span class="sxs-lookup"><span data-stu-id="c3eaf-128">In other words, Service Bus can transfer the message to the destination queue "via" the transfer queue, while performing a complete (or defer, or dead-letter) operation on the input message, all in one atomic operation.</span></span> 

### <a name="see-it-in-code"></a><span data-ttu-id="c3eaf-129">Deze weergegeven in de code</span><span class="sxs-lookup"><span data-stu-id="c3eaf-129">See it in code</span></span>
<span data-ttu-id="c3eaf-130">Als u deze overschrijvingen instelt, moet u een afzender die gericht is op de doelwachtrij via de wachtrij maken.</span><span class="sxs-lookup"><span data-stu-id="c3eaf-130">To set up such transfers, you create a message sender that targets the destination queue via the transfer queue.</span></span> <span data-ttu-id="c3eaf-131">U hebt ook een ontvanger waarmee berichten van die dezelfde wachtrij opgehaald.</span><span class="sxs-lookup"><span data-stu-id="c3eaf-131">You will also have a receiver that pulls messages from that same queue.</span></span> <span data-ttu-id="c3eaf-132">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="c3eaf-132">For example:</span></span>

```csharp
var sender = this.messagingFactory.CreateMessageSender(destinationQueue, myQueueName);
var receiver = this.messagingFactory.CreateMessageReceiver(myQueueName);
```

<span data-ttu-id="c3eaf-133">Vervolgens een eenvoudige transactie maakt gebruik van deze elementen, zoals in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="c3eaf-133">A simple transaction then uses these elements, as in the following example:</span></span>

```csharp
var msg = receiver.Receive();

using (scope = new TransactionScope())
{
    // Do whatever work is required 

    var newmsg = ... // package the result 

    msg.Complete(); // mark the message as done
    sender.Send(newmsg); // forward the result

    scope.Complete(); // declare the transaction done
} 
```

## <a name="next-steps"></a><span data-ttu-id="c3eaf-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c3eaf-134">Next steps</span></span>

<span data-ttu-id="c3eaf-135">Zie de volgende artikelen voor meer informatie over Service Bus-wachtrijen:</span><span class="sxs-lookup"><span data-stu-id="c3eaf-135">See the following articles for more information about Service Bus queues:</span></span>

* [<span data-ttu-id="c3eaf-136">Service Bus-entiteiten met automatisch doorsturen Chaining</span><span class="sxs-lookup"><span data-stu-id="c3eaf-136">Chaining Service Bus entities with auto-forwarding</span></span>](service-bus-auto-forwarding.md)
* [<span data-ttu-id="c3eaf-137">Automatisch doorsturen voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c3eaf-137">Auto-forward sample</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AutoForward)
* [<span data-ttu-id="c3eaf-138">Atomische transacties met Service Bus-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="c3eaf-138">Atomic Transactions with Service Bus sample</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions)
* [<span data-ttu-id="c3eaf-139">Azure-wachtrijen en Service Bus-wachtrijen vergeleken</span><span class="sxs-lookup"><span data-stu-id="c3eaf-139">Azure Queues and Service Bus queues compared</span></span>](service-bus-azure-and-service-bus-queues-compared-contrasted.md)
* [<span data-ttu-id="c3eaf-140">Service Bus-wachtrijen gebruiken</span><span class="sxs-lookup"><span data-stu-id="c3eaf-140">How to use Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)

