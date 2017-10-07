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
# <a name="overview-of-service-bus-transaction-processing"></a><span data-ttu-id="4aa16-103">Overzicht van Service Bus-transactieverwerking</span><span class="sxs-lookup"><span data-stu-id="4aa16-103">Overview of Service Bus transaction processing</span></span>
<span data-ttu-id="4aa16-104">Dit artikel wordt beschreven Hallo transactiemogelijkheden van Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="4aa16-104">This article discusses hello transaction capabilities of Azure Service Bus.</span></span> <span data-ttu-id="4aa16-105">Veel van Hallo discussie wordt geïllustreerd door Hallo [atomische transacties met Service Bus-voorbeeld](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions).</span><span class="sxs-lookup"><span data-stu-id="4aa16-105">Much of hello discussion is illustrated by hello [Atomic Transactions with Service Bus sample](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions).</span></span> <span data-ttu-id="4aa16-106">In dit artikel is beperkt tooan overzicht van transactieverwerking en Hallo *verzenden* functie in Service Bus, terwijl Hallo atomische transacties voorbeeld grotere en complexere binnen het bereik is.</span><span class="sxs-lookup"><span data-stu-id="4aa16-106">This article is limited tooan overview of transaction processing and hello *send via* feature in Service Bus, while hello Atomic Transactions sample is broader and more complex in scope.</span></span>

## <a name="transactions-in-service-bus"></a><span data-ttu-id="4aa16-107">Transacties in de Servicebus</span><span class="sxs-lookup"><span data-stu-id="4aa16-107">Transactions in Service Bus</span></span>
<span data-ttu-id="4aa16-108">Een [transactie](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) twee of meer bewerkingen gegroepeerd in een *uitvoering bereik*.</span><span class="sxs-lookup"><span data-stu-id="4aa16-108">A [transaction](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions#what-are-transactions) groups two or more operations together into an *execution scope*.</span></span> <span data-ttu-id="4aa16-109">Een dergelijke transactie moet ervoor zorgen dat alle bewerkingen die tooa opgegeven groep bewerkingen behoren slagen of gezamenlijk mislukken door aard.</span><span class="sxs-lookup"><span data-stu-id="4aa16-109">By nature, such a transaction must ensure that all operations belonging tooa given group of operations either succeed or fail jointly.</span></span> <span data-ttu-id="4aa16-110">In dit opzicht transacties fungeren als één eenheid ondergebracht, die vaak waarnaar wordt verwezen tooas *atomisch*.</span><span class="sxs-lookup"><span data-stu-id="4aa16-110">In this respect transactions act as one unit, which is often referred tooas *atomicity*.</span></span> 

<span data-ttu-id="4aa16-111">Service Bus is een broker transactionele berichten en garandeert een transactionele integriteit voor alle interne bewerkingen op basis van de bericht-stores.</span><span class="sxs-lookup"><span data-stu-id="4aa16-111">Service Bus is a transactional message broker and ensures transactional integrity for all internal operations against its message stores.</span></span> <span data-ttu-id="4aa16-112">Alle overdrachten van berichten op de Service Bus, zoals bewegende berichten tooa [wachtrij voor onbestelbare berichten](service-bus-dead-letter-queues.md) of [automatisch doorsturen](service-bus-auto-forwarding.md) van berichten tussen entiteiten transactionele zijn.</span><span class="sxs-lookup"><span data-stu-id="4aa16-112">All transfers of messages inside of Service Bus, such as moving messages tooa [dead-letter queue](service-bus-dead-letter-queues.md) or [automatic forwarding](service-bus-auto-forwarding.md) of messages between entities, are transactional.</span></span> <span data-ttu-id="4aa16-113">Als zodanig als Service Bus een bericht accepteert, is al opgeslagen en gelabeld met een volgnummer.</span><span class="sxs-lookup"><span data-stu-id="4aa16-113">As such, if Service Bus accepts a message, it has already been stored and labeled with a sequence number.</span></span> <span data-ttu-id="4aa16-114">Daarna de overdracht van een bericht binnen de Service Bus zijn gecoördineerde bewerkingen over entiteiten en leidt geen van beide tooloss (bron is geslaagd en mislukt als doel) of tooduplication (mislukt van de bron en doel is geslaagd) van het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="4aa16-114">From then on, any message transfers within Service Bus are coordinated operations across entities, and will neither lead tooloss (source succeeds and target fails) or tooduplication (source fails and target succeeds) of hello message.</span></span>

<span data-ttu-id="4aa16-115">Service Bus biedt ondersteuning voor groepering bewerkingen op een enkele Berichtentiteit (wachtrij, onderwerp, abonnement) binnen Hallo bereik van een transactie.</span><span class="sxs-lookup"><span data-stu-id="4aa16-115">Service Bus supports grouping operations against a single messaging entity (queue, topic, subscription) within hello scope of a transaction.</span></span> <span data-ttu-id="4aa16-116">Bijvoorbeeld, kunt u verschillende berichten tooone wachtrij uit verzenden vanuit een transactiebereik en Hallo-berichten worden alleen van doorgevoerd toohello wachtrij logboek wanneer Hallo transactie is voltooid.</span><span class="sxs-lookup"><span data-stu-id="4aa16-116">For example, you can send several messages tooone queue from within a transaction scope, and hello messages will only be committed toohello queue's log when hello transaction successfully completes.</span></span>

## <a name="operations-within-a-transaction-scope"></a><span data-ttu-id="4aa16-117">Bewerkingen binnen een transactiebereik</span><span class="sxs-lookup"><span data-stu-id="4aa16-117">Operations within a transaction scope</span></span>
<span data-ttu-id="4aa16-118">Hallo-bewerkingen die kunnen worden uitgevoerd vanuit een transactiebereik zijn als volgt:</span><span class="sxs-lookup"><span data-stu-id="4aa16-118">hello operations that can be performed within a transaction scope are as follows:</span></span>

* <span data-ttu-id="4aa16-119">**[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: verzenden, SendAsync, SendBatch, SendBatchAsync</span><span class="sxs-lookup"><span data-stu-id="4aa16-119">**[QueueClient](/dotnet/api/microsoft.servicebus.messaging.queueclient), [MessageSender](/dotnet/api/microsoft.servicebus.messaging.messagesender), [TopicClient](/dotnet/api/microsoft.servicebus.messaging.topicclient)**: Send, SendAsync, SendBatch, SendBatchAsync</span></span> 
* <span data-ttu-id="4aa16-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: voltooid, CompleteAsync, afbreken, AbandonAsync, wachtrij voor onbestelbare, DeadletterAsync, uitstelt, DeferAsync, RenewLock, RenewLockAsync</span><span class="sxs-lookup"><span data-stu-id="4aa16-120">**[BrokeredMessage](/dotnet/api/microsoft.servicebus.messaging.brokeredmessage)**: Complete, CompleteAsync, Abandon, AbandonAsync, Deadletter, DeadletterAsync, Defer, DeferAsync, RenewLock, RenewLockAsync</span></span> 

<span data-ttu-id="4aa16-121">Ontvangen bewerkingen zijn niet toegevoegd, omdat ervan wordt uitgegaan dat de toepassing hello berichten met behulp van Hallo verkrijgt [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) modus binnen enkele lus voor ontvangen of met een [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) terugbellen en alleen vervolgens opent een transactie bereik voor de verwerking van het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="4aa16-121">Receive operations are not included, because it is assumed that hello application acquires messages using hello [ReceiveMode.PeekLock](/dotnet/api/microsoft.servicebus.messaging.receivemode) mode, inside some receive loop or with an [OnMessage](/dotnet/api/microsoft.servicebus.messaging.messagereceiver#Microsoft_ServiceBus_Messaging_MessageReceiver_OnMessage_System_Action_Microsoft_ServiceBus_Messaging_BrokeredMessage__Microsoft_ServiceBus_Messaging_OnMessageOptions_) callback, and only then opens a transaction scope for processing hello message.</span></span>

<span data-ttu-id="4aa16-122">Hallo bestemming van het Hallo-bericht (voltooid, afbreken, onbestelbare, uitstellen) uitgevoerd binnen bereik van Hallo en die afhankelijk zijn van, hello algehele resultaat van Hallo transactie.</span><span class="sxs-lookup"><span data-stu-id="4aa16-122">hello disposition of hello message (complete, abandon, dead-letter, defer) then occurs within hello scope of, and dependent on, hello overall outcome of hello transaction.</span></span>

## <a name="transfers-and-send-via"></a><span data-ttu-id="4aa16-123">Overschrijvingen en 'verzenden '</span><span class="sxs-lookup"><span data-stu-id="4aa16-123">Transfers and "send via"</span></span>
<span data-ttu-id="4aa16-124">tooenable transactionele overdracht van gegevens uit een wachtrij tooa processor en tooanother wachtrij, Servicebus ondersteunt *overdrachten*.</span><span class="sxs-lookup"><span data-stu-id="4aa16-124">tooenable transactional handover of data from a queue tooa processor, and then tooanother queue, Service Bus supports *transfers*.</span></span> <span data-ttu-id="4aa16-125">In een overdrachtsbewerking een afzender eerst verzendt een bericht tooa 'wachtrij' en wachtrij Hallo verplaatst onmiddellijk Hallo-bericht toohello doelwachtrij met Hallo dezelfde robuuste transfer implementatie die automatisch doorsturen van berichten Hallo afhankelijk is bedoeld op.</span><span class="sxs-lookup"><span data-stu-id="4aa16-125">In a transfer operation, a sender first sends a message tooa "transfer queue" and hello transfer queue immediately moves hello message toohello intended destination queue using hello same robust transfer implementation that hello auto-forward capability relies on.</span></span> <span data-ttu-id="4aa16-126">Hallo-bericht is nooit toegewezen toohello overdracht wachtrij logboek zodanig dat deze zichtbaar is voor consumenten Hallo overdracht wachtrij.</span><span class="sxs-lookup"><span data-stu-id="4aa16-126">hello message is never committed toohello transfer queue's log in a way that it becomes visible for hello transfer queue's consumers.</span></span>

<span data-ttu-id="4aa16-127">Hallo power van deze mogelijkheid transactionele duidelijk wanneer Hallo wachtrij zelf Hallo bron van de invoer van de afzender van het Hallo-berichten.</span><span class="sxs-lookup"><span data-stu-id="4aa16-127">hello power of this transactional capability becomes apparent when hello transfer queue itself is hello source of hello sender's input messages.</span></span> <span data-ttu-id="4aa16-128">Met andere woorden, Service Bus kunnen worden overgedragen Hallo-bericht toohello doelwachtrij 'via' hello wachtrij, tijdens het uitvoeren van een complete (of uitstelt, of onbestelbare)-bewerking op invoerbericht Hallo allemaal in een atomic-bewerking.</span><span class="sxs-lookup"><span data-stu-id="4aa16-128">In other words, Service Bus can transfer hello message toohello destination queue "via" hello transfer queue, while performing a complete (or defer, or dead-letter) operation on hello input message, all in one atomic operation.</span></span> 

### <a name="see-it-in-code"></a><span data-ttu-id="4aa16-129">Deze weergegeven in de code</span><span class="sxs-lookup"><span data-stu-id="4aa16-129">See it in code</span></span>
<span data-ttu-id="4aa16-130">tooset van deze overdracht maakt u een afzender die gericht is op de doelwachtrij Hallo via Hallo wachtrij.</span><span class="sxs-lookup"><span data-stu-id="4aa16-130">tooset up such transfers, you create a message sender that targets hello destination queue via hello transfer queue.</span></span> <span data-ttu-id="4aa16-131">U hebt ook een ontvanger waarmee berichten van die dezelfde wachtrij opgehaald.</span><span class="sxs-lookup"><span data-stu-id="4aa16-131">You will also have a receiver that pulls messages from that same queue.</span></span> <span data-ttu-id="4aa16-132">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="4aa16-132">For example:</span></span>

```csharp
var sender = this.messagingFactory.CreateMessageSender(destinationQueue, myQueueName);
var receiver = this.messagingFactory.CreateMessageReceiver(myQueueName);
```

<span data-ttu-id="4aa16-133">Vervolgens een eenvoudige transactie maakt gebruik van deze elementen, zoals in het volgende voorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="4aa16-133">A simple transaction then uses these elements, as in hello following example:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="4aa16-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4aa16-134">Next steps</span></span>

<span data-ttu-id="4aa16-135">Zie de volgende artikelen voor meer informatie over Service Bus-wachtrijen Hallo:</span><span class="sxs-lookup"><span data-stu-id="4aa16-135">See hello following articles for more information about Service Bus queues:</span></span>

* [<span data-ttu-id="4aa16-136">Service Bus-entiteiten met automatisch doorsturen Chaining</span><span class="sxs-lookup"><span data-stu-id="4aa16-136">Chaining Service Bus entities with auto-forwarding</span></span>](service-bus-auto-forwarding.md)
* [<span data-ttu-id="4aa16-137">Automatisch doorsturen voorbeeld</span><span class="sxs-lookup"><span data-stu-id="4aa16-137">Auto-forward sample</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AutoForward)
* [<span data-ttu-id="4aa16-138">Atomische transacties met Service Bus-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="4aa16-138">Atomic Transactions with Service Bus sample</span></span>](https://github.com/Azure/azure-service-bus/tree/master/samples/DotNet/Microsoft.ServiceBus.Messaging/AtomicTransactions)
* [<span data-ttu-id="4aa16-139">Azure-wachtrijen en Service Bus-wachtrijen vergeleken</span><span class="sxs-lookup"><span data-stu-id="4aa16-139">Azure Queues and Service Bus queues compared</span></span>](service-bus-azure-and-service-bus-queues-compared-contrasted.md)
* [<span data-ttu-id="4aa16-140">Hoe toouse Service Bus-wachtrijen</span><span class="sxs-lookup"><span data-stu-id="4aa16-140">How toouse Service Bus queues</span></span>](service-bus-dotnet-get-started-with-queues.md)

