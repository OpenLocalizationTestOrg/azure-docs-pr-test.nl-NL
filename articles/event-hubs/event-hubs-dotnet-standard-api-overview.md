---
title: aaaOverview Hallo Azure Event Hubs .NET Standard-API's | Microsoft Docs
description: Standard API .NET-overzicht
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a173f8e4-556c-42b8-b856-838189f7e636
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: c97acecb35b69039e06ded7203c75fca41ce98f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-net-standard-api-overview"></a><span data-ttu-id="3c485-103">Overzicht van Event Hubs .NET Standard API</span><span class="sxs-lookup"><span data-stu-id="3c485-103">Event Hubs .NET Standard API overview</span></span>
<span data-ttu-id="3c485-104">In dit artikel ziet u een aantal van Hallo sleutel Event Hubs .NET standaard client-API's.</span><span class="sxs-lookup"><span data-stu-id="3c485-104">This article summarizes some of hello key Event Hubs .NET Standard client APIs.</span></span> <span data-ttu-id="3c485-105">Er zijn twee standaard .NET clientbibliotheken:</span><span class="sxs-lookup"><span data-stu-id="3c485-105">There are currently two .NET Standard client libraries:</span></span>
* [<span data-ttu-id="3c485-106">Microsoft.Azure.EventHubs</span><span class="sxs-lookup"><span data-stu-id="3c485-106">Microsoft.Azure.EventHubs</span></span>](/dotnet/api/microsoft.azure.eventhubs)
  *  <span data-ttu-id="3c485-107">Deze bibliotheek bevat alle basic-runtime-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="3c485-107">This library provides all basic runtime operations.</span></span>
* [<span data-ttu-id="3c485-108">Microsoft.Azure.EventHubs.Processor</span><span class="sxs-lookup"><span data-stu-id="3c485-108">Microsoft.Azure.EventHubs.Processor</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor)
  * <span data-ttu-id="3c485-109">Deze bibliotheek bevat aanvullende functionaliteit die staat voor het bijhouden van verwerkte gebeurtenissen en is de eenvoudigste manier tooread Hallo van een event hub.</span><span class="sxs-lookup"><span data-stu-id="3c485-109">This library adds additional functionality that allows for keeping track of processed events, and is hello easiest way tooread from an event hub.</span></span>

## <a name="event-hubs-client"></a><span data-ttu-id="3c485-110">Event Hubs-client</span><span class="sxs-lookup"><span data-stu-id="3c485-110">Event Hubs client</span></span>
<span data-ttu-id="3c485-111">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) is hello primaire object u toosend gebeurtenissen, maak ontvangers en tooget runtime-gegevens.</span><span class="sxs-lookup"><span data-stu-id="3c485-111">[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) is hello primary object you use toosend events, create receivers, and tooget run-time information.</span></span> <span data-ttu-id="3c485-112">Deze client gekoppelde tooa bepaalde event hub is en wordt een nieuwe verbinding toohello Event Hubs-eindpunt.</span><span class="sxs-lookup"><span data-stu-id="3c485-112">This client is linked tooa particular event hub, and creates a new connection toohello Event Hubs endpoint.</span></span>

### <a name="create-an-event-hubs-client"></a><span data-ttu-id="3c485-113">Een Event Hubs-client maken</span><span class="sxs-lookup"><span data-stu-id="3c485-113">Create an Event Hubs client</span></span>
<span data-ttu-id="3c485-114">Een [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) object is gemaakt vanuit een verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="3c485-114">An [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) object is created from a connection string.</span></span> <span data-ttu-id="3c485-115">Hallo eenvoudigste manier tooinstantiate een nieuwe client wordt weergegeven in Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="3c485-115">hello simplest way tooinstantiate a new client is shown in hello following example:</span></span>

```csharp
var eventHubClient = EventHubClient.CreateFromConnectionString("{Event Hubs connection string}");
```

<span data-ttu-id="3c485-116">tooprogrammatically hello verbindingsreeks bewerken, kunt u Hallo [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) klasse en het Hallo-verbindingsreeks te als parameter doorgeven[EventHubClient.CreateFromConnectionString ](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).</span><span class="sxs-lookup"><span data-stu-id="3c485-116">tooprogrammatically edit hello connection string, you can use hello [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) class, and pass hello connection string as a parameter too[EventHubClient.CreateFromConnectionString](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).</span></span>

```csharp
var connectionStringBuilder = new EventHubsConnectionStringBuilder("{Event Hubs connection string}")
{
    EntityPath = EhEntityPath
};

var eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());
```

### <a name="send-events"></a><span data-ttu-id="3c485-117">Gebeurtenissen verzenden</span><span class="sxs-lookup"><span data-stu-id="3c485-117">Send events</span></span>
<span data-ttu-id="3c485-118">toosend gebeurtenissen tooan event hub, gebruik Hallo [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) klasse.</span><span class="sxs-lookup"><span data-stu-id="3c485-118">toosend events tooan event hub, use hello [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) class.</span></span> <span data-ttu-id="3c485-119">Hallo-instantie moet een `byte` matrix, of een `byte` segment van de matrix.</span><span class="sxs-lookup"><span data-stu-id="3c485-119">hello body must be a `byte` array, or a `byte` array segment.</span></span>

```csharp
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set user properties if needed
data.Properties.Add("Type", "Informational");
// Send single message async
await eventHubClient.SendAsync(data);
```

### <a name="receive-events"></a><span data-ttu-id="3c485-120">Gebeurtenissen ontvangen</span><span class="sxs-lookup"><span data-stu-id="3c485-120">Receive events</span></span>
<span data-ttu-id="3c485-121">Hallo aanbevolen manier tooreceive gebeurtenissen van Event Hubs met behulp van Hallo [Event Processor Host](#event-processor-host-apis), waarmee u functionaliteit tooautomatically bijhouden van offset en partitie-informatie.</span><span class="sxs-lookup"><span data-stu-id="3c485-121">hello recommended way tooreceive events from Event Hubs is using hello [Event Processor Host](#event-processor-host-apis), which provides functionality tooautomatically keep track of offset, and partition information.</span></span> <span data-ttu-id="3c485-122">Er zijn echter bepaalde situaties waarin u toouse Hallo flexibiliteit van Hallo core Event Hubs bibliotheek tooreceive gebeurtenissen kunt.</span><span class="sxs-lookup"><span data-stu-id="3c485-122">However, there are certain situations in which you may want toouse hello flexibility of hello core Event Hubs library tooreceive events.</span></span>

#### <a name="create-a-receiver"></a><span data-ttu-id="3c485-123">Een ontvanger maken</span><span class="sxs-lookup"><span data-stu-id="3c485-123">Create a receiver</span></span>
<span data-ttu-id="3c485-124">Ontvangers zijn gebonden toospecific partities, zodat in volgorde tooreceive alle gebeurtenissen in een event hub, moet u toocreate meerdere exemplaren.</span><span class="sxs-lookup"><span data-stu-id="3c485-124">Receivers are tied toospecific partitions, so in order tooreceive all events in an event hub, you will need toocreate multiple instances.</span></span> <span data-ttu-id="3c485-125">In het algemeen is een goede gewoonte tooget Hallo-partitiegegevens via programmacode, in plaats van hard-coding van Hallo partitie-id's.</span><span class="sxs-lookup"><span data-stu-id="3c485-125">Generally speaking, it is a good practice tooget hello partition information programatically, rather than hard-coding hello partition ids.</span></span> <span data-ttu-id="3c485-126">In order toodo doet, kunt u Hallo [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) methode.</span><span class="sxs-lookup"><span data-stu-id="3c485-126">In order toodo so, you can use hello [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) method.</span></span>

```csharp
// Create a list tookeep track of hello receivers
var receivers = new List<PartitionReceiver>();
// Use hello eventHubClient created above tooget hello runtime information
var runTimeInformation = await eventHubClient.GetRuntimeInformationAsync();
// Loop over hello resulting partition ids
foreach (var partitionId in runTimeInformation.PartitionIds)
{
    // Create hello receiver
    var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);
    // Add hello receiver toohello list
    receivers.Add(receiver);
}
```

<span data-ttu-id="3c485-127">Aangezien er gebeurtenissen worden nooit verwijderd uit een event hub (en alleen verlopen), moet u toospecify Hallo juiste beginpunt.</span><span class="sxs-lookup"><span data-stu-id="3c485-127">Since events are never removed from an event hub (and only expire), you need toospecify hello proper starting point.</span></span> <span data-ttu-id="3c485-128">Hallo volgende voorbeeld ziet u mogelijke combinaties.</span><span class="sxs-lookup"><span data-stu-id="3c485-128">hello following example shows possible combinations.</span></span>

```csharp
// partitionId is assumed toocome from GetRuntimeInformationAsync()

// Using hello constant PartitionReceiver.EndOfStream only receives all messages from this point forward.
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);

// All messages available
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, "-1");

// From one day ago
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, DateTime.Now.AddDays(-1));
```

#### <a name="consume-an-event"></a><span data-ttu-id="3c485-129">Een gebeurtenis gebruiken</span><span class="sxs-lookup"><span data-stu-id="3c485-129">Consume an event</span></span>
```csharp
// Receive a maximum of 100 messages in this call tooReceiveAsync
var ehEvents = await receiver.ReceiveAsync(100);
// ReceiveAsync can return null if there are no messages
if (ehEvents != null)
{
    // Since ReceiveAsync can return more than a single event you will need a loop tooprocess
    foreach (var ehEvent in ehEvents)
    {
        // Decode hello byte array segment
        var message = UnicodeEncoding.UTF8.GetString(ehEvent.Body.Array);
        // Load hello custom property that we set in hello send example
        var customType = ehEvent.Properties["Type"];
        // Implement processing logic here
    }
}       
```

## <a name="event-processor-host-apis"></a><span data-ttu-id="3c485-130">Event Processor Host API 's</span><span class="sxs-lookup"><span data-stu-id="3c485-130">Event Processor Host APIs</span></span>
<span data-ttu-id="3c485-131">Deze API's bieden tolerantie tooworker processen die mogelijk niet beschikbaar is, door partities over beschikbare werknemers verdeeld.</span><span class="sxs-lookup"><span data-stu-id="3c485-131">These APIs provide resiliency tooworker processes that may become unavailable, by distributing partitions across available workers.</span></span>

```csharp
// Checkpointing is done within hello SimpleEventProcessor and on a per-consumerGroup per-partition basis, workers resume from where they last left off.

// Read these connection strings from a secure location
var ehConnectionString = "{Event Hubs connection string}";
var ehEntityPath = "{event hub path/name}";
var storageConnectionString = "{Storage connection string}";
var storageContainerName = "{Storage account container name}";

var eventProcessorHost = new EventProcessorHost(
    ehEntityPath,
    PartitionReceiver.DefaultConsumerGroupName,
    ehConnectionString,
    storageConnectionString,
    storageContainerName);

// Start/register an EventProcessorHost
await eventProcessorHost.RegisterEventProcessorAsync<SimpleEventProcessor>();

// Disposes of hello Event Processor Host
await eventProcessorHost.UnregisterEventProcessorAsync();
```

<span data-ttu-id="3c485-132">Hallo volgende is een Voorbeeldimplementatie van Hallo [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).</span><span class="sxs-lookup"><span data-stu-id="3c485-132">hello following is a sample implementation of hello [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).</span></span>

```csharp
public class SimpleEventProcessor : IEventProcessor
{
    public Task CloseAsync(PartitionContext context, CloseReason reason)
    {
        Console.WriteLine($"Processor Shutting Down. Partition '{context.PartitionId}', Reason: '{reason}'.");
        return Task.CompletedTask;
    }

    public Task OpenAsync(PartitionContext context)
    {
        Console.WriteLine($"SimpleEventProcessor initialized. Partition: '{context.PartitionId}'");
        return Task.CompletedTask;
    }

    public Task ProcessErrorAsync(PartitionContext context, Exception error)
    {
        Console.WriteLine($"Error on Partition: {context.PartitionId}, Error: {error.Message}");
        return Task.CompletedTask;
    }

    public Task ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
    {
        foreach (var eventData in messages)
        {
            var data = Encoding.UTF8.GetString(eventData.Body.Array, eventData.Body.Offset, eventData.Body.Count);
            Console.WriteLine($"Message received. Partition: '{context.PartitionId}', Data: '{data}'");
        }

        return context.CheckpointAsync();
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="3c485-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3c485-133">Next steps</span></span>
<span data-ttu-id="3c485-134">toolearn meer informatie over Event Hubs-scenario's, gaat u naar deze koppelingen:</span><span class="sxs-lookup"><span data-stu-id="3c485-134">toolearn more about Event Hubs scenarios, visit these links:</span></span>

* [<span data-ttu-id="3c485-135">Wat is Azure Event Hubs?</span><span class="sxs-lookup"><span data-stu-id="3c485-135">What is Azure Event Hubs?</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="3c485-136">Beschikbare Event Hubs-API 's</span><span class="sxs-lookup"><span data-stu-id="3c485-136">Available Event Hubs apis</span></span>](event-hubs-api-overview.md)

<span data-ttu-id="3c485-137">Hallo .NET API-verwijzingen zijn hier:</span><span class="sxs-lookup"><span data-stu-id="3c485-137">hello .NET API references are here:</span></span>

* [<span data-ttu-id="3c485-138">Microsoft.Azure.EventHubs</span><span class="sxs-lookup"><span data-stu-id="3c485-138">Microsoft.Azure.EventHubs</span></span>](/dotnet/api/microsoft.azure.eventhubs)
* [<span data-ttu-id="3c485-139">Microsoft.Azure.EventHubs.Processor</span><span class="sxs-lookup"><span data-stu-id="3c485-139">Microsoft.Azure.EventHubs.Processor</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor)