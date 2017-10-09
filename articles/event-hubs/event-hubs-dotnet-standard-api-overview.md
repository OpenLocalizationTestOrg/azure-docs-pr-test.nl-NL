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
# <a name="event-hubs-net-standard-api-overview"></a>Overzicht van Event Hubs .NET Standard API
In dit artikel ziet u een aantal van Hallo sleutel Event Hubs .NET standaard client-API's. Er zijn twee standaard .NET clientbibliotheken:
* [Microsoft.Azure.EventHubs](/dotnet/api/microsoft.azure.eventhubs)
  *  Deze bibliotheek bevat alle basic-runtime-bewerkingen.
* [Microsoft.Azure.EventHubs.Processor](/dotnet/api/microsoft.azure.eventhubs.processor)
  * Deze bibliotheek bevat aanvullende functionaliteit die staat voor het bijhouden van verwerkte gebeurtenissen en is de eenvoudigste manier tooread Hallo van een event hub.

## <a name="event-hubs-client"></a>Event Hubs-client
[EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) is hello primaire object u toosend gebeurtenissen, maak ontvangers en tooget runtime-gegevens. Deze client gekoppelde tooa bepaalde event hub is en wordt een nieuwe verbinding toohello Event Hubs-eindpunt.

### <a name="create-an-event-hubs-client"></a>Een Event Hubs-client maken
Een [EventHubClient](/dotnet/api/microsoft.azure.eventhubs.eventhubclient) object is gemaakt vanuit een verbindingsreeks. Hallo eenvoudigste manier tooinstantiate een nieuwe client wordt weergegeven in Hallo voorbeeld te volgen:

```csharp
var eventHubClient = EventHubClient.CreateFromConnectionString("{Event Hubs connection string}");
```

tooprogrammatically hello verbindingsreeks bewerken, kunt u Hallo [EventHubsConnectionStringBuilder](/dotnet/api/microsoft.azure.eventhubs.eventhubsconnectionstringbuilder) klasse en het Hallo-verbindingsreeks te als parameter doorgeven[EventHubClient.CreateFromConnectionString ](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_CreateFromConnectionString_System_String_).

```csharp
var connectionStringBuilder = new EventHubsConnectionStringBuilder("{Event Hubs connection string}")
{
    EntityPath = EhEntityPath
};

var eventHubClient = EventHubClient.CreateFromConnectionString(connectionStringBuilder.ToString());
```

### <a name="send-events"></a>Gebeurtenissen verzenden
toosend gebeurtenissen tooan event hub, gebruik Hallo [EventData](/dotnet/api/microsoft.azure.eventhubs.eventdata) klasse. Hallo-instantie moet een `byte` matrix, of een `byte` segment van de matrix.

```csharp
// Create a new EventData object by encoding a string as a byte array
var data = new EventData(Encoding.UTF8.GetBytes("This is my message..."));
// Set user properties if needed
data.Properties.Add("Type", "Informational");
// Send single message async
await eventHubClient.SendAsync(data);
```

### <a name="receive-events"></a>Gebeurtenissen ontvangen
Hallo aanbevolen manier tooreceive gebeurtenissen van Event Hubs met behulp van Hallo [Event Processor Host](#event-processor-host-apis), waarmee u functionaliteit tooautomatically bijhouden van offset en partitie-informatie. Er zijn echter bepaalde situaties waarin u toouse Hallo flexibiliteit van Hallo core Event Hubs bibliotheek tooreceive gebeurtenissen kunt.

#### <a name="create-a-receiver"></a>Een ontvanger maken
Ontvangers zijn gebonden toospecific partities, zodat in volgorde tooreceive alle gebeurtenissen in een event hub, moet u toocreate meerdere exemplaren. In het algemeen is een goede gewoonte tooget Hallo-partitiegegevens via programmacode, in plaats van hard-coding van Hallo partitie-id's. In order toodo doet, kunt u Hallo [GetRuntimeInformationAsync](/dotnet/api/microsoft.azure.eventhubs.eventhubclient#Microsoft_Azure_EventHubs_EventHubClient_GetRuntimeInformationAsync) methode.

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

Aangezien er gebeurtenissen worden nooit verwijderd uit een event hub (en alleen verlopen), moet u toospecify Hallo juiste beginpunt. Hallo volgende voorbeeld ziet u mogelijke combinaties.

```csharp
// partitionId is assumed toocome from GetRuntimeInformationAsync()

// Using hello constant PartitionReceiver.EndOfStream only receives all messages from this point forward.
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, PartitionReceiver.EndOfStream);

// All messages available
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, "-1");

// From one day ago
var receiver = eventHubClient.CreateReceiver(PartitionReceiver.DefaultConsumerGroupName, partitionId, DateTime.Now.AddDays(-1));
```

#### <a name="consume-an-event"></a>Een gebeurtenis gebruiken
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

## <a name="event-processor-host-apis"></a>Event Processor Host API 's
Deze API's bieden tolerantie tooworker processen die mogelijk niet beschikbaar is, door partities over beschikbare werknemers verdeeld.

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

Hallo volgende is een Voorbeeldimplementatie van Hallo [IEventProcessor](/dotnet/api/microsoft.azure.eventhubs.processor.ieventprocessor).

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

## <a name="next-steps"></a>Volgende stappen
toolearn meer informatie over Event Hubs-scenario's, gaat u naar deze koppelingen:

* [Wat is Azure Event Hubs?](event-hubs-what-is-event-hubs.md)
* [Beschikbare Event Hubs-API 's](event-hubs-api-overview.md)

Hallo .NET API-verwijzingen zijn hier:

* [Microsoft.Azure.EventHubs](/dotnet/api/microsoft.azure.eventhubs)
* [Microsoft.Azure.EventHubs.Processor](/dotnet/api/microsoft.azure.eventhubs.processor)