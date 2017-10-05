---
title: Azure Functions Event Hubs-bindingen | Microsoft Docs
description: Het gebruik van Azure Event Hubs bindingen in de Azure Functions begrijpen.
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: Azure functions, functies, verwerking van gebeurtenissen, dynamische compute zonder server architectuur
ms.assetid: daf81798-7acc-419a-bc32-b5a41c6db56b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 06/20/2017
ms.author: wesmc
ms.openlocfilehash: 19021bef8b7156b3049f43b0275c0ed0c6b22514
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-event-hubs-bindings"></a><span data-ttu-id="225ed-104">Azure Functions Event Hubs-bindingen</span><span class="sxs-lookup"><span data-stu-id="225ed-104">Azure Functions Event Hubs bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="225ed-105">In dit artikel wordt uitgelegd hoe u configureert en gebruikt [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) bindingen voor Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="225ed-105">This article explains how to configure and use [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) bindings for Azure Functions.</span></span>
<span data-ttu-id="225ed-106">Azure Functions ondersteunt activeren en uitvoer van de bindingen voor Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="225ed-106">Azure Functions supports trigger and output bindings for Event Hubs.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="225ed-107">Als u niet bekend met Azure Event Hubs bent, raadpleegt u de [overzicht van Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="225ed-107">If you are new to Azure Event Hubs, see the [Event Hubs overview](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

<a name="trigger"></a>

## <a name="event-hub-trigger"></a><span data-ttu-id="225ed-108">Event hub trigger</span><span class="sxs-lookup"><span data-stu-id="225ed-108">Event hub trigger</span></span>
<span data-ttu-id="225ed-109">Gebruik de Event Hubs-trigger om te reageren op een gebeurtenis verzonden naar de gebeurtenisstroom van een event hub.</span><span class="sxs-lookup"><span data-stu-id="225ed-109">Use the Event Hubs trigger to respond to an event sent to an event hub event stream.</span></span> <span data-ttu-id="225ed-110">U moet leestoegang hebben tot de event hub voor het instellen van de trigger.</span><span class="sxs-lookup"><span data-stu-id="225ed-110">You must have read access to the event hub to set up the trigger.</span></span>

<span data-ttu-id="225ed-111">De trigger Event Hubs-functie maakt gebruik van de volgende JSON-object in de `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="225ed-111">The Event Hubs function trigger uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHubTrigger",
    "name": "<Name of trigger parameter in function signature>",
    "direction": "in",
    "path": "<Name of the event hub>",
    "consumerGroup": "Consumer group to use - see below",
    "connection": "<Name of app setting with connection string - see below>"
}
```

<span data-ttu-id="225ed-112">`consumerGroup`is een optionele eigenschap gebruikt om de [consumergroep](../event-hubs/event-hubs-features.md#event-consumers) gebruikt om u te abonneren op gebeurtenissen in de hub.</span><span class="sxs-lookup"><span data-stu-id="225ed-112">`consumerGroup` is an optional property used to set the [consumer group](../event-hubs/event-hubs-features.md#event-consumers) used to subscribe to events in the hub.</span></span> <span data-ttu-id="225ed-113">Als u dit weglaat, de `$Default` consumergroep wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="225ed-113">If omitted, the `$Default` consumer group is used.</span></span>  
<span data-ttu-id="225ed-114">`connection`moet de naam van een app-instelling met de verbindingsreeks naar de event hub-naamruimte.</span><span class="sxs-lookup"><span data-stu-id="225ed-114">`connection` must be the name of an app setting that contains the connection string to the event hub's namespace.</span></span>
<span data-ttu-id="225ed-115">Kopieer deze verbindingsreeks door te klikken op de **verbindingsgegevens** knop voor de *naamruimte*, niet de event hub zelf.</span><span class="sxs-lookup"><span data-stu-id="225ed-115">Copy this connection string by clicking the **Connection Information** button for the *namespace*, not the event hub itself.</span></span> <span data-ttu-id="225ed-116">Deze verbindingsreeks moet ten minste leesmachtigingen hebben voor de trigger wordt geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="225ed-116">This connection string must have at least read permissions to activate the trigger.</span></span>

<span data-ttu-id="225ed-117">[Extra instellingen](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) kan worden opgegeven in een bestand host.json verder verbeteren van de Event Hubs-triggers.</span><span class="sxs-lookup"><span data-stu-id="225ed-117">[Additional settings](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) can be provided in a host.json file to further fine tune Event Hubs triggers.</span></span>  

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="225ed-118">Gebruik van de trigger</span><span class="sxs-lookup"><span data-stu-id="225ed-118">Trigger usage</span></span>
<span data-ttu-id="225ed-119">Wanneer een functie van Event Hubs trigger wordt geactiveerd, wordt het bericht dat deze wordt geactiveerd als een tekenreeks in de functie doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="225ed-119">When an Event Hubs trigger function is triggered, the message that triggers it is passed into the function as a string.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="225ed-120">Voorbeeld van de trigger</span><span class="sxs-lookup"><span data-stu-id="225ed-120">Trigger sample</span></span>
<span data-ttu-id="225ed-121">Stel dat u hebt de volgende Event Hubs activeren de `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="225ed-121">Suppose you have the following Event Hubs trigger in the `bindings` array of function.json:</span></span>

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```

<span data-ttu-id="225ed-122">Zie de taalspecifieke-voorbeeldtoepassing die u de berichttekst van de event hub-trigger registreert.</span><span class="sxs-lookup"><span data-stu-id="225ed-122">See the language-specific sample that logs the message body of the event hub trigger.</span></span>

* [<span data-ttu-id="225ed-123">C#</span><span class="sxs-lookup"><span data-stu-id="225ed-123">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="225ed-124">F#</span><span class="sxs-lookup"><span data-stu-id="225ed-124">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="225ed-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="225ed-125">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="225ed-126">Voorbeeld van de trigger in C#</span><span class="sxs-lookup"><span data-stu-id="225ed-126">Trigger sample in C#</span></span> #

```cs
using System;

public static void Run(string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

<span data-ttu-id="225ed-127">U kunt ook ontvangen de gebeurtenis als een [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) object, waarmee u toegang krijgt tot de metagegevens van de gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="225ed-127">You can also receive the event as an [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) object, which gives you access to the event metadata.</span></span>

```cs
#r "Microsoft.ServiceBus"
using System.Text;
using Microsoft.ServiceBus.Messaging;

public static void Run(EventData myEventHubMessage, TraceWriter log)
{
    log.Info($"{Encoding.UTF8.GetString(myEventHubMessage.GetBytes())}");
}
```

<span data-ttu-id="225ed-128">Voor het ontvangen van gebeurtenissen in een batch, wijzigt de methodehandtekening voor `string[]` of `EventData[]`.</span><span class="sxs-lookup"><span data-stu-id="225ed-128">To receive events in a batch, change the method signature to `string[]` or `EventData[]`.</span></span>

```cs
public static void Run(string[] eventHubMessages, TraceWriter log)
{
    foreach (var message in eventHubMessages)
    {
        log.Info($"C# Event Hub trigger function processed a message: {message}");
    }
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a><span data-ttu-id="225ed-129">Voorbeeld van de trigger in F #</span><span class="sxs-lookup"><span data-stu-id="225ed-129">Trigger sample in F#</span></span> #

```fsharp
let Run(myEventHubMessage: string, log: TraceWriter) =
    log.Info(sprintf "F# eventhub trigger function processed work item: %s" myEventHubMessage)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="225ed-130">Voorbeeld van de trigger in Node.js</span><span class="sxs-lookup"><span data-stu-id="225ed-130">Trigger sample in Node.js</span></span>

```javascript
module.exports = function (context, myEventHubMessage) {
    context.log('Node.js eventhub trigger function processed work item', myEventHubMessage);    
    context.done();
};
```

<a name="output"></a>

## <a name="event-hubs-output-binding"></a><span data-ttu-id="225ed-131">Event Hubs uitvoer binding</span><span class="sxs-lookup"><span data-stu-id="225ed-131">Event Hubs output binding</span></span>
<span data-ttu-id="225ed-132">De uitvoer van de Event Hubs binding gebeurtenissen schrijven naar de gebeurtenisstroom van een event hub gebruiken.</span><span class="sxs-lookup"><span data-stu-id="225ed-132">Use the Event Hubs output binding to write events to an event hub event stream.</span></span> <span data-ttu-id="225ed-133">U moet gemachtigd verzenden naar een event hub gebeurtenissen om ernaar te schrijven.</span><span class="sxs-lookup"><span data-stu-id="225ed-133">You must have send permission to an event hub to write events to it.</span></span>

<span data-ttu-id="225ed-134">De uitvoer-binding gebruikt de volgende JSON-object in de `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="225ed-134">The output binding uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "<Name of output parameter in function signature>",
    "path": "<Name of event hub>",
    "connection": "<Name of app setting with connection string - see below>"
    "direction": "out"
}
```

<span data-ttu-id="225ed-135">`connection`moet de naam van een app-instelling met de verbindingsreeks naar de event hub-naamruimte.</span><span class="sxs-lookup"><span data-stu-id="225ed-135">`connection` must be the name of an app setting that contains the connection string to the event hub's namespace.</span></span>
<span data-ttu-id="225ed-136">Kopieer deze verbindingsreeks door te klikken op de **verbindingsgegevens** knop voor de *naamruimte*, niet de event hub zelf.</span><span class="sxs-lookup"><span data-stu-id="225ed-136">Copy this connection string by clicking the **Connection Information** button for the *namespace*, not the event hub itself.</span></span> <span data-ttu-id="225ed-137">Deze verbindingsreeks moet verzenden machtigingen hebben voor het bericht naar de stroom gebeurtenissen sturen.</span><span class="sxs-lookup"><span data-stu-id="225ed-137">This connection string must have send permissions to send the message to the event stream.</span></span>

## <a name="output-usage"></a><span data-ttu-id="225ed-138">Gebruik voor uitvoer</span><span class="sxs-lookup"><span data-stu-id="225ed-138">Output usage</span></span>
<span data-ttu-id="225ed-139">Deze sectie wordt beschreven hoe u de uitvoer van uw Event Hubs in uw functiecode binding.</span><span class="sxs-lookup"><span data-stu-id="225ed-139">This section shows you how to use your Event Hubs output binding in your function code.</span></span>

<span data-ttu-id="225ed-140">U kunt berichten naar de geconfigureerde event hub uitvoeren met de volgende parametertypen:</span><span class="sxs-lookup"><span data-stu-id="225ed-140">You can output messages to the configured event hub with the following parameter types:</span></span>

* `out string`
* <span data-ttu-id="225ed-141">`ICollector<string>`(om uit te voeren op meerdere berichten)</span><span class="sxs-lookup"><span data-stu-id="225ed-141">`ICollector<string>` (to output multiple messages)</span></span>
* <span data-ttu-id="225ed-142">`IAsyncCollector<string>`(async-versie van `ICollector<T>`)</span><span class="sxs-lookup"><span data-stu-id="225ed-142">`IAsyncCollector<string>` (async version of `ICollector<T>`)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="225ed-143">Voorbeeld van uitvoer</span><span class="sxs-lookup"><span data-stu-id="225ed-143">Output sample</span></span>
<span data-ttu-id="225ed-144">Stel dat u hebt de volgende Event Hubs uitvoer binding in de `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="225ed-144">Suppose you have the following Event Hubs output binding in the `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

<span data-ttu-id="225ed-145">Zie het voorbeeld taalspecifieke die een gebeurtenis naar de zelfs stroom geschreven.</span><span class="sxs-lookup"><span data-stu-id="225ed-145">See the language-specific sample that writes an event to the even stream.</span></span>

* [<span data-ttu-id="225ed-146">C#</span><span class="sxs-lookup"><span data-stu-id="225ed-146">C#</span></span>](#outcsharp)
* [<span data-ttu-id="225ed-147">F#</span><span class="sxs-lookup"><span data-stu-id="225ed-147">F#</span></span>](#outfsharp)
* [<span data-ttu-id="225ed-148">Node.js</span><span class="sxs-lookup"><span data-stu-id="225ed-148">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="225ed-149">Voorbeeld van uitvoer in C#</span><span class="sxs-lookup"><span data-stu-id="225ed-149">Output sample in C#</span></span> #

```cs
using System;

public static void Run(TimerInfo myTimer, out string outputEventHubMessage, TraceWriter log)
{
    String msg = $"TimerTriggerCSharp1 executed at: {DateTime.Now}";
    log.Verbose(msg);   
    outputEventHubMessage = msg;
}
```

<span data-ttu-id="225ed-150">Of om meerdere berichten te maken:</span><span class="sxs-lookup"><span data-stu-id="225ed-150">Or, to create multiple messages:</span></span>

```cs
public static void Run(TimerInfo myTimer, ICollector<string> outputEventHubMessage, TraceWriter log)
{
    string message = $"Event Hub message created at: {DateTime.Now}";
    log.Info(message);
    outputEventHubMessage.Add("1 " + message);
    outputEventHubMessage.Add("2 " + message);
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a><span data-ttu-id="225ed-151">Voorbeeld van uitvoer in F #</span><span class="sxs-lookup"><span data-stu-id="225ed-151">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, outputEventHubMessage: byref<string>, log: TraceWriter) =
    let msg = sprintf "TimerTriggerFSharp1 executed at: %s" DateTime.Now.ToString()
    log.Verbose(msg);
    outputEventHubMessage <- msg;
```

<a name="outnodejs"></a>

### <a name="output-sample-for-nodejs"></a><span data-ttu-id="225ed-152">Voorbeeld van uitvoer voor Node.js</span><span class="sxs-lookup"><span data-stu-id="225ed-152">Output sample for Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();
    context.log('Event Hub message created at: ', timeStamp);   
    context.bindings.outputEventHubMessage = "Event Hub message created at: " + timeStamp;
    context.done();
};
```

<span data-ttu-id="225ed-153">Of om meerdere berichten te verzenden</span><span class="sxs-lookup"><span data-stu-id="225ed-153">Or, to send multiple messages,</span></span>

```javascript
module.exports = function(context) {
    var timeStamp = new Date().toISOString();
    var message = 'Event Hub message created at: ' + timeStamp;

    context.bindings.outputEventHubMessage = [];

    context.bindings.outputEventHubMessage.push("1 " + message);
    context.bindings.outputEventHubMessage.push("2 " + message);
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="225ed-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="225ed-154">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
