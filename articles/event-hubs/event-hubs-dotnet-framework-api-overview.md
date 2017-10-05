---
title: Overzicht van de .NET Framework-API's van Azure Event Hubs | Microsoft Docs
description: Een overzicht van enkele van de belangrijkste Event Hubs .NET Framework client-API.
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 7f3b6cc0-9600-417f-9e80-2345411bd036
ms.service: event-hubs
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/15/2017
ms.author: sethm
ms.openlocfilehash: bc525e7ca8b21e9e5f1e36b3152d71420b041700
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="event-hubs-net-framework-api-overview"></a><span data-ttu-id="08292-103">Overzicht van Event Hubs .NET Framework-API</span><span class="sxs-lookup"><span data-stu-id="08292-103">Event Hubs .NET Framework API overview</span></span>
<span data-ttu-id="08292-104">In dit artikel ziet u een aantal van de sleutel Event Hubs .NET Framework client-API's.</span><span class="sxs-lookup"><span data-stu-id="08292-104">This article summarizes some of the key Event Hubs .NET Framework client APIs.</span></span> <span data-ttu-id="08292-105">Er zijn twee categorieën: beheer- en runtime-API's.</span><span class="sxs-lookup"><span data-stu-id="08292-105">There are two categories: management and run-time APIs.</span></span> <span data-ttu-id="08292-106">Runtime-API's bestaan uit alle bewerkingen die nodig zijn voor het verzenden en ontvangen van een bericht.</span><span class="sxs-lookup"><span data-stu-id="08292-106">Run-time APIs consist of all operations needed to send and receive a message.</span></span> <span data-ttu-id="08292-107">Beheerbewerkingen kunnen u voor het beheren van een status van de entiteit Event Hubs door maken, bijwerken en verwijderen entiteiten.</span><span class="sxs-lookup"><span data-stu-id="08292-107">Management operations enable you to manage an Event Hubs entity state by creating, updating, and deleting entities.</span></span>

<span data-ttu-id="08292-108">Bewakingsscenario's omvatten beheer of de uitvoering.</span><span class="sxs-lookup"><span data-stu-id="08292-108">Monitoring scenarios span both management and run-time.</span></span> <span data-ttu-id="08292-109">Zie voor gedetailleerde documentatie over de .NET API's, de [Service Bus .NET](/dotnet/api/microsoft.servicebus.messaging) en [EventProcessorHost API](/dotnet/api/microsoft.azure.eventhubs.processor) verwijzingen.</span><span class="sxs-lookup"><span data-stu-id="08292-109">For detailed reference documentation on the .NET APIs, see the [Service Bus .NET](/dotnet/api/microsoft.servicebus.messaging) and [EventProcessorHost API](/dotnet/api/microsoft.azure.eventhubs.processor) references.</span></span>

## <a name="management-apis"></a><span data-ttu-id="08292-110">Management-API 's</span><span class="sxs-lookup"><span data-stu-id="08292-110">Management APIs</span></span>
<span data-ttu-id="08292-111">Als u wilt de volgende beheerbewerkingen uitvoeren, moet u hebben **beheren** machtigingen voor de Event Hubs-naamruimte:</span><span class="sxs-lookup"><span data-stu-id="08292-111">To perform the following management operations, you must have **Manage** permissions on the Event Hubs namespace:</span></span>

### <a name="create"></a><span data-ttu-id="08292-112">Maken</span><span class="sxs-lookup"><span data-stu-id="08292-112">Create</span></span>
```csharp
// Create the event hub
var ehd = new EventHubDescription(eventHubName);
ehd.PartitionCount = SampleManager.numPartitions;
await namespaceManager.CreateEventHubAsync(ehd);
```

### <a name="update"></a><span data-ttu-id="08292-113">Update</span><span class="sxs-lookup"><span data-stu-id="08292-113">Update</span></span>
```csharp
var ehd = await namespaceManager.GetEventHubAsync(eventHubName);

// Create a customer SAS rule with Manage permissions
ehd.UserMetadata = "Some updated info";
var ruleName = "myeventhubmanagerule";
var ruleKey = SharedAccessAuthorizationRule.GenerateRandomKey();
ehd.Authorization.Add(new SharedAccessAuthorizationRule(ruleName, ruleKey, new AccessRights[] {AccessRights.Manage, AccessRights.Listen, AccessRights.Send} )); 
await namespaceManager.UpdateEventHubAsync(ehd);
```

### <a name="delete"></a><span data-ttu-id="08292-114">Verwijderen</span><span class="sxs-lookup"><span data-stu-id="08292-114">Delete</span></span>
```csharp
await namespaceManager.DeleteEventHubAsync("Event Hub name");
```

## <a name="run-time-apis"></a><span data-ttu-id="08292-115">Runtime-API 's</span><span class="sxs-lookup"><span data-stu-id="08292-115">Run-time APIs</span></span>
### <a name="create-publisher"></a><span data-ttu-id="08292-116">Maken van de uitgever</span><span class="sxs-lookup"><span data-stu-id="08292-116">Create publisher</span></span>
```csharp
// EventHubClient model (uses implicit factory instance, so all links on same connection)
var eventHubClient = EventHubClient.Create("Event Hub name");
```

### <a name="publish-message"></a><span data-ttu-id="08292-117">Bericht publiceren</span><span class="sxs-lookup"><span data-stu-id="08292-117">Publish message</span></span>
```csharp
// Create the device/temperature metric
var info = new MetricEvent() { DeviceId = random.Next(SampleManager.NumDevices), Temperature = random.Next(100) };
var data = new EventData(new byte[10]); // Byte array
var data = new EventData(Stream); // Stream 
var data = new EventData(info, serializer) //Object and serializer 
{
    PartitionKey = info.DeviceId.ToString()
};

// Set user properties if needed
data.Properties.Add("Type", "Telemetry_" + DateTime.Now.ToLongTimeString());

// Send single message async
await client.SendAsync(data);
```

### <a name="create-consumer"></a><span data-ttu-id="08292-118">Consument maken</span><span class="sxs-lookup"><span data-stu-id="08292-118">Create consumer</span></span>
```csharp
// Create the Event Hubs client
var eventHubClient = EventHubClient.Create(EventHubName);

// Get the default consumer group
var defaultConsumerGroup = eventHubClient.GetDefaultConsumerGroup();

// All messages
var consumer = await defaultConsumerGroup.CreateReceiverAsync(partitionId: index);

// From one day ago
var consumer = await defaultConsumerGroup.CreateReceiverAsync(partitionId: index, startingDateTimeUtc:DateTime.Now.AddDays(-1));

// From specific offset, -1 means oldest
var consumer = await defaultConsumerGroup.CreateReceiverAsync(partitionId: index,startingOffset:-1); 
```

### <a name="consume-message"></a><span data-ttu-id="08292-119">Bericht gebruiken</span><span class="sxs-lookup"><span data-stu-id="08292-119">Consume message</span></span>
```csharp
var message = await consumer.ReceiveAsync();

// Provide a serializer
var info = message.GetBody<Type>(Serializer)

// Get a byte[]
var info = message.GetBytes(); 
msg = UnicodeEncoding.UTF8.GetString(info);
```

## <a name="event-processor-host-apis"></a><span data-ttu-id="08292-120">Event Processor Host API 's</span><span class="sxs-lookup"><span data-stu-id="08292-120">Event Processor Host APIs</span></span>
<span data-ttu-id="08292-121">Deze API's bieden tolerantie voor werkprocessen die mogelijk niet beschikbaar is, door partities over beschikbare werknemers verdeeld.</span><span class="sxs-lookup"><span data-stu-id="08292-121">These APIs provide resiliency to worker processes that may become unavailable, by distributing partitions across available workers.</span></span>

```csharp
// Checkpointing is done within the SimpleEventProcessor and on a per-consumerGroup per-partition basis, workers resume from where they last left off.
// Use the EventData.Offset value for checkpointing yourself, this value is unique per partition.

var eventHubConnectionString = System.Configuration.ConfigurationManager.AppSettings["Microsoft.ServiceBus.ConnectionString"];
var blobConnectionString = System.Configuration.ConfigurationManager.AppSettings["AzureStorageConnectionString"]; // Required for checkpoint/state

var eventHubDescription = new EventHubDescription(EventHubName);
var host = new EventProcessorHost(WorkerName, EventHubName, defaultConsumerGroup.GroupName, eventHubConnectionString, blobConnectionString);
await host.RegisterEventProcessorAsync<SimpleEventProcessor>();

// To close
await host.UnregisterEventProcessorAsync();
```

<span data-ttu-id="08292-122">De [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor) interface wordt als volgt gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="08292-122">The [IEventProcessor](/dotnet/api/microsoft.servicebus.messaging.ieventprocessor) interface is defined as follows:</span></span>

```csharp
public class SimpleEventProcessor : IEventProcessor
{
    IDictionary<string, string> map;
    PartitionContext partitionContext;

    public SimpleEventProcessor()
    {
        this.map = new Dictionary<string, string>();
    }

    public Task OpenAsync(PartitionContext context)
    {
        this.partitionContext = context;

        return Task.FromResult<object>(null);
    }

    public async Task ProcessEventsAsync(PartitionContext context, IEnumerable<EventData> messages)
    {
        foreach (EventData message in messages)
        {
            // Process messages here
        }

        // Checkpoint when appropriate
        await context.CheckpointAsync();

    }

    public async Task CloseAsync(PartitionContext context, CloseReason reason)
    {
        if (reason == CloseReason.Shutdown)
        {
            await context.CheckpointAsync();
        }
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="08292-123">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="08292-123">Next steps</span></span>
<span data-ttu-id="08292-124">Volg deze koppelingen voor meer informatie over Event Hubs-scenario‘s:</span><span class="sxs-lookup"><span data-stu-id="08292-124">To learn more about Event Hubs scenarios, visit these links:</span></span>

* [<span data-ttu-id="08292-125">Wat is Azure Event Hubs?</span><span class="sxs-lookup"><span data-stu-id="08292-125">What is Azure Event Hubs?</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="08292-126">Programmeerhandleiding voor Event Hubs</span><span class="sxs-lookup"><span data-stu-id="08292-126">Event Hubs programming guide</span></span>](event-hubs-programming-guide.md)

<span data-ttu-id="08292-127">De .NET API-verwijzingen zijn hier:</span><span class="sxs-lookup"><span data-stu-id="08292-127">The .NET API references are here:</span></span>

* [<span data-ttu-id="08292-128">Microsoft.ServiceBus.Messaging</span><span class="sxs-lookup"><span data-stu-id="08292-128">Microsoft.ServiceBus.Messaging</span></span>](/dotnet/api/microsoft.servicebus.messaging)
* [<span data-ttu-id="08292-129">Microsoft.Azure.EventHubs.EventProcessorHost</span><span class="sxs-lookup"><span data-stu-id="08292-129">Microsoft.Azure.EventHubs.EventProcessorHost</span></span>](/dotnet/api/microsoft.azure.eventhubs.processor.eventprocessorhost)
