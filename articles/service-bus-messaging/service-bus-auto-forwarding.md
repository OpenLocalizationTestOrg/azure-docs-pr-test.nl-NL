---
title: aaaAuto doorsturen Azure Service Bus-berichtentiteiten | Microsoft Docs
description: Hoe een Service Bus toochain wachtrij of abonnement tooanother wachtrij of onderwerp.
services: service-bus-messaging
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: f7060778-3421-402c-97c7-735dbf6a61e8
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: af18273e4e2f81c5363eb830c7decf313afd8307
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="chaining-service-bus-entities-with-auto-forwarding"></a><span data-ttu-id="4aea4-103">Service Bus-entiteiten met automatisch doorsturen Chaining</span><span class="sxs-lookup"><span data-stu-id="4aea4-103">Chaining Service Bus entities with auto-forwarding</span></span>

<span data-ttu-id="4aea4-104">Hallo Service Bus *automatisch doorsturen* functie kunt u een wachtrij toochain of abonnement tooanother wachtrij of onderwerp dat deel uitmaakt van Hallo dezelfde naamruimte.</span><span class="sxs-lookup"><span data-stu-id="4aea4-104">hello Service Bus *auto-forwarding* feature enables you toochain a queue or subscription tooanother queue or topic that is part of hello same namespace.</span></span> <span data-ttu-id="4aea4-105">Wanneer automatisch doorsturen is ingeschakeld, wordt Service Bus automatisch verwijdert van berichten die worden geplaatst in de eerste wachtrij Hallo of -abonnement (bron) en plaatst deze in de tweede Hallo-wachtrij of onderwerp (doel).</span><span class="sxs-lookup"><span data-stu-id="4aea4-105">When auto-forwarding is enabled, Service Bus automatically removes messages that are placed in hello first queue or subscription (source) and puts them in hello second queue or topic (destination).</span></span> <span data-ttu-id="4aea4-106">Houd er rekening mee dat het nog steeds mogelijk toosend bericht toohello doelentiteit rechtstreeks is.</span><span class="sxs-lookup"><span data-stu-id="4aea4-106">Note that it is still possible toosend a message toohello destination entity directly.</span></span> <span data-ttu-id="4aea4-107">Het is ook niet mogelijk toochain een subwachtrij, zoals een wachtrij voor onbestelbare berichten, tooanother wachtrij of onderwerp.</span><span class="sxs-lookup"><span data-stu-id="4aea4-107">Also, it is not possible toochain a subqueue, such as a deadletter queue, tooanother queue or topic.</span></span>

## <a name="using-auto-forwarding"></a><span data-ttu-id="4aea4-108">Automatisch doorsturen gebruiken</span><span class="sxs-lookup"><span data-stu-id="4aea4-108">Using auto-forwarding</span></span>
<span data-ttu-id="4aea4-109">U kunt automatisch doorsturen inschakelen door de instelling Hallo [QueueDescription.ForwardTo] [ QueueDescription.ForwardTo] of [SubscriptionDescription.ForwardTo] [ SubscriptionDescription.ForwardTo] eigenschappen op Hallo [QueueDescription] [ QueueDescription] of [SubscriptionDescription] [ SubscriptionDescription] objecten voor Hallo-bron, zoals in Hallo volgende voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="4aea4-109">You can enable auto-forwarding by setting hello [QueueDescription.ForwardTo][QueueDescription.ForwardTo] or [SubscriptionDescription.ForwardTo][SubscriptionDescription.ForwardTo] properties on hello [QueueDescription][QueueDescription] or [SubscriptionDescription][SubscriptionDescription] objects for hello source, as in hello following example.</span></span>

```csharp
SubscriptionDescription srcSubscription = new SubscriptionDescription (srcTopic, srcSubscriptionName);
srcSubscription.ForwardTo = destTopic;
namespaceManager.CreateSubscription(srcSubscription));
```

<span data-ttu-id="4aea4-110">Hallo doelentiteit moet bestaan op Hallo moment Hallo bronentiteit wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4aea4-110">hello destination entity must exist at hello time hello source entity is created.</span></span> <span data-ttu-id="4aea4-111">Hallo doelentiteit bestaat niet, dan Service Bus een uitzondering geretourneerd wanneer gestelde toocreate Hallo bronentiteit.</span><span class="sxs-lookup"><span data-stu-id="4aea4-111">If hello destination entity does not exist, Service Bus returns an exception when asked toocreate hello source entity.</span></span>

<span data-ttu-id="4aea4-112">U kunt automatisch doorsturen tooscale uit een onderwerp.</span><span class="sxs-lookup"><span data-stu-id="4aea4-112">You can use auto-forwarding tooscale out an individual topic.</span></span> <span data-ttu-id="4aea4-113">Service Bus-limieten Hallo [aantal abonnementen op een bepaald onderwerp](service-bus-quotas.md) too2, 000.</span><span class="sxs-lookup"><span data-stu-id="4aea4-113">Service Bus limits hello [number of subscriptions on a given topic](service-bus-quotas.md) too2,000.</span></span> <span data-ttu-id="4aea4-114">Door het tweede niveau onderwerpen maken, kunt u gebruikmaken van aanvullende abonnementen.</span><span class="sxs-lookup"><span data-stu-id="4aea4-114">You can accommodate additional subscriptions by creating second-level topics.</span></span> <span data-ttu-id="4aea4-115">Opmerking zelfs als u niet afhankelijk is van Hallo Hallo Service Bus-beperking van het aantal abonnementen, het toevoegen van een tweede verificatieniveau onderwerpen Hallo kunt verbeteren totale doorvoer van uw onderwerp.</span><span class="sxs-lookup"><span data-stu-id="4aea4-115">Note that even if you are not bound by hello Service Bus limitation on hello number of subscriptions, adding a second level of topics can improve hello overall throughput of your topic.</span></span>

![Automatisch doorsturen scenario][0]

<span data-ttu-id="4aea4-117">U kunt ook automatisch doorsturen toodecouple afzenders van berichten van ontvangers.</span><span class="sxs-lookup"><span data-stu-id="4aea4-117">You can also use auto-forwarding toodecouple message senders from receivers.</span></span> <span data-ttu-id="4aea4-118">Neem bijvoorbeeld een ERP-systeem dat uit drie modules bestaat: volgorde verwerking, voorraadbeheer en customer relationship management.</span><span class="sxs-lookup"><span data-stu-id="4aea4-118">For example, consider an ERP system that consists of three modules: order processing, inventory management, and customer relations management.</span></span> <span data-ttu-id="4aea4-119">Elk van deze modules worden berichten die in de wachtrij in een bijbehorende onderwerp zijn gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="4aea4-119">Each of these modules generates messages that are enqueued into a corresponding topic.</span></span> <span data-ttu-id="4aea4-120">Els en Bob zijn vertegenwoordigers die geïnteresseerd zijn in alle berichten die betrekking tootheir klanten hebben.</span><span class="sxs-lookup"><span data-stu-id="4aea4-120">Alice and Bob are sales representatives that are interested in all messages that relate tootheir customers.</span></span> <span data-ttu-id="4aea4-121">tooreceive die berichten, Alice en Bob maken een persoonlijke wachtrij en een abonnement op elk Hallo ERP-onderwerpen die alle berichten tootheir wachtrij automatisch doorsturen.</span><span class="sxs-lookup"><span data-stu-id="4aea4-121">tooreceive those messages, Alice and Bob each create a personal queue and a subscription on each of hello ERP topics that automatically forward all messages tootheir queue.</span></span>

![Automatisch doorsturen scenario][1]

<span data-ttu-id="4aea4-123">Als Els op vakantie, haar persoonlijke wachtrij, in plaats van Hallo ERP onderwerp gaat, wordt opgevuld.</span><span class="sxs-lookup"><span data-stu-id="4aea4-123">If Alice goes on vacation, her personal queue, rather than hello ERP topic, fills up.</span></span> <span data-ttu-id="4aea4-124">In dit scenario, omdat een verkoopmedewerker niet alle berichten ontvangen bereiken geen Hallo ERP onderwerpen ooit quotum.</span><span class="sxs-lookup"><span data-stu-id="4aea4-124">In this scenario, because a sales representative has not received any messages, none of hello ERP topics ever reach quota.</span></span>

## <a name="auto-forwarding-considerations"></a><span data-ttu-id="4aea4-125">Automatisch doorsturen overwegingen</span><span class="sxs-lookup"><span data-stu-id="4aea4-125">Auto-forwarding considerations</span></span>

<span data-ttu-id="4aea4-126">Als Hallo doelentiteit stelt samen te veel berichten en Hallo quotum wordt overschreden, of Hallo doelentiteit is uitgeschakeld, Hallo bronentiteit voegt Hallo-berichten tooits [wachtrij voor onbestelbare berichten](service-bus-dead-letter-queues.md) tot er ruimte in het Hallo-doel is (of Hallo entiteit opnieuw is ingeschakeld).</span><span class="sxs-lookup"><span data-stu-id="4aea4-126">If hello destination entity accumulates too many messages and exceeds hello quota, or hello destination entity is disabled, hello source entity adds hello messages tooits [dead-letter queue](service-bus-dead-letter-queues.md) until there is space in hello destination (or hello entity is re-enabled).</span></span> <span data-ttu-id="4aea4-127">Deze berichten blijven in de wachtrij voor onbestelbare berichten Hallo toolive zodat u moet expliciet ontvangen en van de wachtrij voor onbestelbare berichten Hallo verwerken.</span><span class="sxs-lookup"><span data-stu-id="4aea4-127">Those messages will continue toolive in hello dead-letter queue, so you must explicitly receive and process them from hello dead-letter queue.</span></span>

<span data-ttu-id="4aea4-128">Het verdient de voorkeur dat u een beperkt aantal abonnementen op Hallo eerste niveau onderwerp en veel abonnementen op Hallo tweede niveau onderwerpen hebt voor het koppelen van afzonderlijke onderwerpen tooobtain een samengestelde onderwerp met veel abonnementen.</span><span class="sxs-lookup"><span data-stu-id="4aea4-128">When chaining together individual topics tooobtain a composite topic with many subscriptions, it is recommended that you have a moderate number of subscriptions on hello first-level topic and many subscriptions on hello second-level topics.</span></span> <span data-ttu-id="4aea4-129">Bijvoorbeeld een eerste niveau onderwerp met 20 abonnementen, elk van deze teruggekoppeld tooa tweede niveau onderwerp met 200 abonnementen toestaat voor een hogere doorvoer dan een onderwerp van het eerste niveau met 200 abonnementen elk teruggekoppeld tooa tweede niveau onderwerp met 20 abonnementen .</span><span class="sxs-lookup"><span data-stu-id="4aea4-129">For example, a first-level topic with 20 subscriptions, each of them chained tooa second-level topic with 200 subscriptions, allows for higher throughput than a first-level topic with 200 subscriptions, each chained tooa second-level topic with 20 subscriptions.</span></span>

<span data-ttu-id="4aea4-130">Service Bus stuklijsten één bewerking voor elk bericht.</span><span class="sxs-lookup"><span data-stu-id="4aea4-130">Service Bus bills one operation for each forwarded message.</span></span> <span data-ttu-id="4aea4-131">Bijvoorbeeld, verzendt een bericht tooa onderwerp met 20 abonnementen, elk van deze tooauto doorsturen berichten tooanother wachtrij of onderwerp, wordt in rekening gebracht als 21 bewerkingen als alle abonnementen van het eerste niveau ontvangt een kopie van het Hallo-bericht geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="4aea4-131">For example, sending a message tooa topic with 20 subscriptions, each of them configured tooauto-forward messages tooanother queue or topic, is billed as 21 operations if all first-level subscriptions receive a copy of hello message.</span></span>

<span data-ttu-id="4aea4-132">een abonnement dat is keten tooanother wachtrij of onderwerp toocreate, Hallo maker van Hallo abonnement moet hebben **beheren** machtigingen op het Hallo-bron- en Hallo doelentiteit.</span><span class="sxs-lookup"><span data-stu-id="4aea4-132">toocreate a subscription that is chained tooanother queue or topic, hello creator of hello subscription must have **Manage** permissions on both hello source and hello destination entity.</span></span> <span data-ttu-id="4aea4-133">Verzenden van berichten toohello bron onderwerp vereist alleen **verzenden** machtigingen op Hallo bron onderwerp.</span><span class="sxs-lookup"><span data-stu-id="4aea4-133">Sending messages toohello source topic only requires **Send** permissions on hello source topic.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4aea4-134">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4aea4-134">Next steps</span></span>

<span data-ttu-id="4aea4-135">Zie voor gedetailleerde informatie over het automatisch doorsturen Hallo naslagonderwerpen voor het volgende:</span><span class="sxs-lookup"><span data-stu-id="4aea4-135">For detailed information about auto-forwarding, see hello following reference topics:</span></span>

* <span data-ttu-id="4aea4-136">[ForwardTo][QueueDescription.ForwardTo]</span><span class="sxs-lookup"><span data-stu-id="4aea4-136">[ForwardTo][QueueDescription.ForwardTo]</span></span>
* <span data-ttu-id="4aea4-137">[QueueDescription][QueueDescription]</span><span class="sxs-lookup"><span data-stu-id="4aea4-137">[QueueDescription][QueueDescription]</span></span>
* <span data-ttu-id="4aea4-138">[SubscriptionDescription][SubscriptionDescription]</span><span class="sxs-lookup"><span data-stu-id="4aea4-138">[SubscriptionDescription][SubscriptionDescription]</span></span>

<span data-ttu-id="4aea4-139">toolearn meer informatie over Service Bus-prestatieverbeteringen, Zie</span><span class="sxs-lookup"><span data-stu-id="4aea4-139">toolearn more about Service Bus performance improvements, see</span></span> 

* [<span data-ttu-id="4aea4-140">Aanbevolen procedures voor verbeterde prestaties met behulp van Service Bus-berichtenservice</span><span class="sxs-lookup"><span data-stu-id="4aea4-140">Best Practices for performance improvements using Service Bus Messaging</span></span>](service-bus-performance-improvements.md)
* <span data-ttu-id="4aea4-141">[Gepartitioneerde berichtentiteiten][Partitioned messaging entities].</span><span class="sxs-lookup"><span data-stu-id="4aea4-141">[Partitioned messaging entities][Partitioned messaging entities].</span></span>

[QueueDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.queuedescription.forwardto#Microsoft_ServiceBus_Messaging_QueueDescription_ForwardTo
[SubscriptionDescription.ForwardTo]: /dotnet/api/microsoft.servicebus.messaging.subscriptiondescription.forwardto#Microsoft_ServiceBus_Messaging_SubscriptionDescription_ForwardTo
[QueueDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[SubscriptionDescription]: /dotnet/api/microsoft.servicebus.messaging.queuedescription
[0]: ./media/service-bus-auto-forwarding/IC628631.gif
[1]: ./media/service-bus-auto-forwarding/IC628632.gif
[Partitioned messaging entities]: service-bus-partitioning.md
