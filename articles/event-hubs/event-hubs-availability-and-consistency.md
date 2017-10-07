---
title: aaaAvailability en consistentie in Azure Event Hubs | Microsoft Docs
description: Hoe tooprovide Hallo maximale hoeveelheid beschikbaarheid en consistentie met behulp van Azure Event Hubs partities.
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 8f3637a1-bbd7-481e-be49-b3adf9510ba1
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: a8ededaae1589830da21cb8910ca694d2d628bd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-consistency-in-event-hubs"></a><span data-ttu-id="117a2-103">Beschikbaarheid en consistentie in Event Hubs</span><span class="sxs-lookup"><span data-stu-id="117a2-103">Availability and consistency in Event Hubs</span></span>

## <a name="overview"></a><span data-ttu-id="117a2-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="117a2-104">Overview</span></span>
<span data-ttu-id="117a2-105">Maakt gebruik van Azure Event Hubs een [partitioneren model](event-hubs-features.md#partitions) tooimprove beschikbaarheid en garandeert binnen een enkele event hub.</span><span class="sxs-lookup"><span data-stu-id="117a2-105">Azure Event Hubs uses a [partitioning model](event-hubs-features.md#partitions) tooimprove availability and parallelization within a single event hub.</span></span> <span data-ttu-id="117a2-106">Bijvoorbeeld, als een event hub vier partities heeft en een van deze partities van één server tooanother in een bewerking voor de taakverdeling wordt verplaatst, kunt u nog steeds verzenden en ontvangen van de drie andere partities.</span><span class="sxs-lookup"><span data-stu-id="117a2-106">For example, if an event hub has four partitions, and one of those partitions is moved from one server tooanother in a load balancing operation, you can still send and receive from three other partitions.</span></span> <span data-ttu-id="117a2-107">Bovendien meer partities, kunt u toohave meer gelijktijdige lezers verwerken van uw gegevens, de geaggregeerde doorvoer te verbeteren.</span><span class="sxs-lookup"><span data-stu-id="117a2-107">Additionally, having more partitions enables you toohave more concurrent readers processing your data, improving your aggregate throughput.</span></span> <span data-ttu-id="117a2-108">Inzicht in Hallo gevolgen van het partitioneren en rangschikken in een gedistribueerde systeem is een kritieke aspect van het ontwerp van de oplossing.</span><span class="sxs-lookup"><span data-stu-id="117a2-108">Understanding hello implications of partitioning and ordering in a distributed system is a critical aspect of solution design.</span></span>

<span data-ttu-id="117a2-109">toohelp Hallo compromis tussen ordening en beschikbaarheid uitgelegd, Zie Hallo [CAP stelling van](https://en.wikipedia.org/wiki/CAP_theorem), ook wel van Brewer stelling van.</span><span class="sxs-lookup"><span data-stu-id="117a2-109">toohelp explain hello trade-off between ordering and availability, see hello [CAP theorem](https://en.wikipedia.org/wiki/CAP_theorem), also known as Brewer's theorem.</span></span> <span data-ttu-id="117a2-110">Deze stelling van komen aan bod Hallo keuze tussen de consistentie, beschikbaarheid en tolerantie van de partitie.</span><span class="sxs-lookup"><span data-stu-id="117a2-110">This theorem discusses hello choice between consistency, availability, and partition tolerance.</span></span>

<span data-ttu-id="117a2-111">De Brewer stelling van consistentie en beschikbaarheid wordt als volgt gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="117a2-111">Brewer's theorem defines consistency and availability as follows:</span></span>
* <span data-ttu-id="117a2-112">Partitie-tolerantie: Hallo mogelijkheid van een gegevensverwerking system toocontinue verwerken van gegevens, zelfs als er een partitie-fout optreedt.</span><span class="sxs-lookup"><span data-stu-id="117a2-112">Partition tolerance: hello ability of a data processing system toocontinue processing data even if a partition failure occurs.</span></span>
* <span data-ttu-id="117a2-113">Beschikbaarheid: een knooppunt niet mislukken retourneert een redelijke antwoord binnen een redelijk tijdsbestek (met geen fouten of time-outs).</span><span class="sxs-lookup"><span data-stu-id="117a2-113">Availability: a non-failing node returns a reasonable response within a reasonable amount of time (with no errors or timeouts).</span></span>
* <span data-ttu-id="117a2-114">Consistentiecontrole: Lees is gegarandeerd tooreturn Hallo meest recente schrijven voor een bepaalde client.</span><span class="sxs-lookup"><span data-stu-id="117a2-114">Consistency: a read is guaranteed tooreturn hello most recent write for a given client.</span></span>

## <a name="partition-tolerance"></a><span data-ttu-id="117a2-115">Partitie tolerantie</span><span class="sxs-lookup"><span data-stu-id="117a2-115">Partition tolerance</span></span>
<span data-ttu-id="117a2-116">Event Hubs is gebaseerd op een gepartitioneerde gegevensmodel.</span><span class="sxs-lookup"><span data-stu-id="117a2-116">Event Hubs is built on top of a partitioned data model.</span></span> <span data-ttu-id="117a2-117">U kunt het aantal partities Hallo configureren in uw event hub tijdens de installatie, maar u kunt deze waarde later wijzigen.</span><span class="sxs-lookup"><span data-stu-id="117a2-117">You can configure hello number of partitions in your event hub during setup, but you cannot change this value later.</span></span> <span data-ttu-id="117a2-118">Omdat u partities met Event Hubs gebruiken moet, hebt u toomake een beslissing over de beschikbaarheid en consistentie voor uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="117a2-118">Since you must use partitions with Event Hubs, you have toomake a decision about availability and consistency for your application.</span></span>

## <a name="availability"></a><span data-ttu-id="117a2-119">Beschikbaarheid</span><span class="sxs-lookup"><span data-stu-id="117a2-119">Availability</span></span>
<span data-ttu-id="117a2-120">Hallo eenvoudigste manier tooget de slag met Event Hubs is toouse Hallo standaardgedrag.</span><span class="sxs-lookup"><span data-stu-id="117a2-120">hello simplest way tooget started with Event Hubs is toouse hello default behavior.</span></span> <span data-ttu-id="117a2-121">Als u een nieuwe maakt `EventHubClient` object ingesteld en Hallo `Send` methode, uw gebeurtenissen worden automatisch verdeeld tussen de partities in de event hub.</span><span class="sxs-lookup"><span data-stu-id="117a2-121">If you create a new `EventHubClient` object and use hello `Send` method, your events are automatically distributed between partitions in your event hub.</span></span> <span data-ttu-id="117a2-122">Dit gedrag kunt Hallo grootste hoeveelheid tijd.</span><span class="sxs-lookup"><span data-stu-id="117a2-122">This behavior allows for hello greatest amount of up time.</span></span>

<span data-ttu-id="117a2-123">Dit model is voor gebruiksvoorbeelden waarvoor Hallo maximale tijd voorkeur.</span><span class="sxs-lookup"><span data-stu-id="117a2-123">For use cases that require hello maximum up time, this model is preferred.</span></span>

## <a name="consistency"></a><span data-ttu-id="117a2-124">Consistentie</span><span class="sxs-lookup"><span data-stu-id="117a2-124">Consistency</span></span>
<span data-ttu-id="117a2-125">In sommige gevallen kan Hallo ordening van gebeurtenissen belangrijk zijn.</span><span class="sxs-lookup"><span data-stu-id="117a2-125">In some scenarios, hello ordering of events can be important.</span></span> <span data-ttu-id="117a2-126">U kunt bijvoorbeeld uw back-end-systeem tooprocess een bijwerkopdracht voordat een verwijderopdracht.</span><span class="sxs-lookup"><span data-stu-id="117a2-126">For example, you may want your back-end system tooprocess an update command before a delete command.</span></span> <span data-ttu-id="117a2-127">In dat geval kunt u kunt Hallo partitiesleutel ingesteld op een gebeurtenis of gebruik een `PartitionSender` object tooonly verzenden gebeurtenissen tooa bepaalde partitie.</span><span class="sxs-lookup"><span data-stu-id="117a2-127">In this instance, you can either set hello partition key on an event, or use a `PartitionSender` object tooonly send events tooa certain partition.</span></span> <span data-ttu-id="117a2-128">Hiermee zorgt u ervoor dat wanneer deze gebeurtenissen worden gelezen uit het Hallo-partitie, worden gelezen in volgorde.</span><span class="sxs-lookup"><span data-stu-id="117a2-128">Doing so ensures that when these events are read from hello partition, they are read in order.</span></span>

<span data-ttu-id="117a2-129">Houd er rekening mee dat als Hallo bepaalde partitie toowhich die u verzendt niet beschikbaar is, u een foutmelding ontvangt met deze configuratie.</span><span class="sxs-lookup"><span data-stu-id="117a2-129">With this configuration, keep in mind that if hello particular partition toowhich you are sending is unavailable, you will receive an error response.</span></span> <span data-ttu-id="117a2-130">Als u een affiniteit tooa één partitie, hoeft geen verzendt Hallo Event Hubs-service als een punt voor vergelijking, uw gebeurtenis toohello volgende beschikbare partitie.</span><span class="sxs-lookup"><span data-stu-id="117a2-130">As a point of comparison, if you do not have an affinity tooa single partition, hello Event Hubs service sends your event toohello next available partition.</span></span>

<span data-ttu-id="117a2-131">Een mogelijke oplossing tooensure ordening tegelijkertijd ook tijd, zou tooaggregate gebeurtenissen zijn als onderdeel van uw toepassing voor gebeurtenisverwerking.</span><span class="sxs-lookup"><span data-stu-id="117a2-131">One possible solution tooensure ordering, while also maximizing up time, would be tooaggregate events as part of your event processing application.</span></span> <span data-ttu-id="117a2-132">Hallo gemakkelijkste manier tooaccomplish dit toostamp wordt de gebeurtenis met een eigenschap aangepaste sequence number.</span><span class="sxs-lookup"><span data-stu-id="117a2-132">hello easiest way tooaccomplish this is toostamp your event with a custom sequence number property.</span></span> <span data-ttu-id="117a2-133">Hallo volgende code toont een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="117a2-133">hello following code shows an example:</span></span>

```csharp
// Get hello latest sequence number from your application
var sequenceNumber = GetNextSequenceNumber();
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set a custom sequence number property
data.Properties.Add("SequenceNumber", sequenceNumber);
// Send single message async
await eventHubClient.SendAsync(data);
```

<span data-ttu-id="117a2-134">In dit voorbeeld verzendt uw tooone gebeurtenis van de beschikbare partities Hallo in uw event hub en bijbehorende volgnummer Hallo ingesteld van uw toepassing.</span><span class="sxs-lookup"><span data-stu-id="117a2-134">This example sends your event tooone of hello available partitions in your event hub, and sets hello corresponding sequence number from your application.</span></span> <span data-ttu-id="117a2-135">Deze oplossing vereist status toobe door uw toepassing verwerking bewaard, maar uw afzenders biedt een eindpunt dat waarschijnlijker toobe beschikbaar is.</span><span class="sxs-lookup"><span data-stu-id="117a2-135">This solution requires state toobe kept by your processing application, but gives your senders an endpoint that is more likely toobe available.</span></span>

## <a name="next-steps"></a><span data-ttu-id="117a2-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="117a2-136">Next steps</span></span>
<span data-ttu-id="117a2-137">U meer informatie over Event Hubs via Hallo koppelingen te volgen:</span><span class="sxs-lookup"><span data-stu-id="117a2-137">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="117a2-138">Overzicht van Event Hubs-service</span><span class="sxs-lookup"><span data-stu-id="117a2-138">Event Hubs service overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="117a2-139">Een Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="117a2-139">Create an event hub</span></span>](event-hubs-create.md)
