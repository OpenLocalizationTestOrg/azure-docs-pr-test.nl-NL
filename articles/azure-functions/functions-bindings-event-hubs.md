---
title: aaaAzure functies Event Hubs bindingen | Microsoft Docs
description: Begrijpen hoe toouse Azure Event Hubs bindingen in de Azure Functions.
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
ms.openlocfilehash: e864f032ad5ac58d318c9843c3844b5642733a70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-event-hubs-bindings"></a><span data-ttu-id="b5dcb-104">Azure Functions Event Hubs-bindingen</span><span class="sxs-lookup"><span data-stu-id="b5dcb-104">Azure Functions Event Hubs bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="b5dcb-105">Dit artikel wordt uitgelegd hoe tooconfigure en gebruik [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) bindingen voor Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="b5dcb-105">This article explains how tooconfigure and use [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) bindings for Azure Functions.</span></span>
<span data-ttu-id="b5dcb-106">Azure Functions ondersteunt activeren en uitvoer van de bindingen voor Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="b5dcb-106">Azure Functions supports trigger and output bindings for Event Hubs.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="b5dcb-107">Als u nieuwe tooAzure Event Hubs, Zie Hallo [overzicht van Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).</span><span class="sxs-lookup"><span data-stu-id="b5dcb-107">If you are new tooAzure Event Hubs, see hello [Event Hubs overview](../event-hubs/event-hubs-what-is-event-hubs.md).</span></span>

<a name="trigger"></a>

## <a name="event-hub-trigger"></a><span data-ttu-id="b5dcb-108">Event hub trigger</span><span class="sxs-lookup"><span data-stu-id="b5dcb-108">Event hub trigger</span></span>
<span data-ttu-id="b5dcb-109">Gebruik Hallo Event Hubs gebeurtenis toorespond tooan tooan event hub gebeurtenisstroom verzonden.</span><span class="sxs-lookup"><span data-stu-id="b5dcb-109">Use hello Event Hubs trigger toorespond tooan event sent tooan event hub event stream.</span></span> <span data-ttu-id="b5dcb-110">U moet leestoegang toohello event hub tooset up Hallo trigger hebben.</span><span class="sxs-lookup"><span data-stu-id="b5dcb-110">You must have read access toohello event hub tooset up hello trigger.</span></span>

<span data-ttu-id="b5dcb-111">Hallo Event Hubs functie trigger gebruikt de volgende JSON-object in Hallo Hallo `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="b5dcb-111">hello Event Hubs function trigger uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHubTrigger",
    "name": "<Name of trigger parameter in function signature>",
    "direction": "in",
    "path": "<Name of hello event hub>",
    "consumerGroup": "Consumer group toouse - see below",
    "connection": "<Name of app setting with connection string - see below>"
}
```

<span data-ttu-id="b5dcb-112">`consumerGroup`is een optionele eigenschap gebruikt tooset hello [consumergroep](../event-hubs/event-hubs-features.md#event-consumers) toosubscribe tooevents in Hallo hub gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b5dcb-112">`consumerGroup` is an optional property used tooset hello [consumer group](../event-hubs/event-hubs-features.md#event-consumers) used toosubscribe tooevents in hello hub.</span></span> <span data-ttu-id="b5dcb-113">Als u dit weglaat, Hallo `$Default` consumergroep wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b5dcb-113">If omitted, hello `$Default` consumer group is used.</span></span>  
<span data-ttu-id="b5dcb-114">`connection`moet Hallo-naam van een app-instelling met naamruimte Hallo connection string toohello gebeurtenis van de hub.</span><span class="sxs-lookup"><span data-stu-id="b5dcb-114">`connection` must be hello name of an app setting that contains hello connection string toohello event hub's namespace.</span></span>
<span data-ttu-id="b5dcb-115">Kopieer deze verbindingsreeks door te klikken op Hallo **verbindingsgegevens** knop voor Hallo *naamruimte*, niet Hallo event hub zelf.</span><span class="sxs-lookup"><span data-stu-id="b5dcb-115">Copy this connection string by clicking hello **Connection Information** button for hello *namespace*, not hello event hub itself.</span></span> <span data-ttu-id="b5dcb-116">Deze verbindingsreeks heeft moet ten minste machtigingen tooactivate Hallo trigger lezen.</span><span class="sxs-lookup"><span data-stu-id="b5dcb-116">This connection string must have at least read permissions tooactivate hello trigger.</span></span>

<span data-ttu-id="b5dcb-117">[Extra instellingen](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) kan worden opgegeven in een host.json bestand toofurther fijn stemmen Event Hubs-triggers.</span><span class="sxs-lookup"><span data-stu-id="b5dcb-117">[Additional settings](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) can be provided in a host.json file toofurther fine tune Event Hubs triggers.</span></span>  

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="b5dcb-118">Gebruik van de trigger</span><span class="sxs-lookup"><span data-stu-id="b5dcb-118">Trigger usage</span></span>
<span data-ttu-id="b5dcb-119">Wanneer een functie van Event Hubs trigger wordt geactiveerd, wordt in de functie Hallo Hallo-bericht dat deze wordt geactiveerd doorgegeven als een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="b5dcb-119">When an Event Hubs trigger function is triggered, hello message that triggers it is passed into hello function as a string.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="b5dcb-120">Voorbeeld van de trigger</span><span class="sxs-lookup"><span data-stu-id="b5dcb-120">Trigger sample</span></span>
<span data-ttu-id="b5dcb-121">Stel dat u volgende Event Hubs in Hallo activeren Hallo hebt `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="b5dcb-121">Suppose you have hello following Event Hubs trigger in hello `bindings` array of function.json:</span></span>

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```

<span data-ttu-id="b5dcb-122">Zie Hallo taalspecifieke steekproef die het Hallo-berichttekst van Hallo event hub trigger registreert.</span><span class="sxs-lookup"><span data-stu-id="b5dcb-122">See hello language-specific sample that logs hello message body of hello event hub trigger.</span></span>

* [<span data-ttu-id="b5dcb-123">C#</span><span class="sxs-lookup"><span data-stu-id="b5dcb-123">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="b5dcb-124">F#</span><span class="sxs-lookup"><span data-stu-id="b5dcb-124">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="b5dcb-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="b5dcb-125">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="b5dcb-126">Voorbeeld van de trigger in C#</span><span class="sxs-lookup"><span data-stu-id="b5dcb-126">Trigger sample in C#</span></span> #

```cs
using System;

public static void Run(string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

<span data-ttu-id="b5dcb-127">U kunt ook Hallo-gebeurtenis ontvangen een [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) object, waarmee u toegang tot toohello gebeurtenis metagegevens.</span><span class="sxs-lookup"><span data-stu-id="b5dcb-127">You can also receive hello event as an [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) object, which gives you access toohello event metadata.</span></span>

```cs
#r "Microsoft.ServiceBus"
using System.Text;
using Microsoft.ServiceBus.Messaging;

public static void Run(EventData myEventHubMessage, TraceWriter log)
{
    log.Info($"{Encoding.UTF8.GetString(myEventHubMessage.GetBytes())}");
}
```

<span data-ttu-id="b5dcb-128">gebeurtenissen in een batch tooreceive Hallo methodehandtekening ook wijzigen`string[]` of `EventData[]`.</span><span class="sxs-lookup"><span data-stu-id="b5dcb-128">tooreceive events in a batch, change hello method signature too`string[]` or `EventData[]`.</span></span>

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

### <a name="trigger-sample-in-f"></a><span data-ttu-id="b5dcb-129">Voorbeeld van de trigger in F #</span><span class="sxs-lookup"><span data-stu-id="b5dcb-129">Trigger sample in F#</span></span> #

```fsharp
let Run(myEventHubMessage: string, log: TraceWriter) =
    log.Info(sprintf "F# eventhub trigger function processed work item: %s" myEventHubMessage)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="b5dcb-130">Voorbeeld van de trigger in Node.js</span><span class="sxs-lookup"><span data-stu-id="b5dcb-130">Trigger sample in Node.js</span></span>

```javascript
module.exports = function (context, myEventHubMessage) {
    context.log('Node.js eventhub trigger function processed work item', myEventHubMessage);    
    context.done();
};
```

<a name="output"></a>

## <a name="event-hubs-output-binding"></a><span data-ttu-id="b5dcb-131">Event Hubs uitvoer binding</span><span class="sxs-lookup"><span data-stu-id="b5dcb-131">Event Hubs output binding</span></span>
<span data-ttu-id="b5dcb-132">Gebruik Hallo Event Hubs uitvoer binding toowrite gebeurtenissen tooan event hub stroom gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="b5dcb-132">Use hello Event Hubs output binding toowrite events tooan event hub event stream.</span></span> <span data-ttu-id="b5dcb-133">U moet verzenden machtiging tooan event hub toowrite gebeurtenissen tooit hebben.</span><span class="sxs-lookup"><span data-stu-id="b5dcb-133">You must have send permission tooan event hub toowrite events tooit.</span></span>

<span data-ttu-id="b5dcb-134">Hallo uitvoer binding gebruikt Hallo volgende JSON-object in Hallo `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="b5dcb-134">hello output binding uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "<Name of output parameter in function signature>",
    "path": "<Name of event hub>",
    "connection": "<Name of app setting with connection string - see below>"
    "direction": "out"
}
```

<span data-ttu-id="b5dcb-135">`connection`moet Hallo-naam van een app-instelling met naamruimte Hallo connection string toohello gebeurtenis van de hub.</span><span class="sxs-lookup"><span data-stu-id="b5dcb-135">`connection` must be hello name of an app setting that contains hello connection string toohello event hub's namespace.</span></span>
<span data-ttu-id="b5dcb-136">Kopieer deze verbindingsreeks door te klikken op Hallo **verbindingsgegevens** knop voor Hallo *naamruimte*, niet Hallo event hub zelf.</span><span class="sxs-lookup"><span data-stu-id="b5dcb-136">Copy this connection string by clicking hello **Connection Information** button for hello *namespace*, not hello event hub itself.</span></span> <span data-ttu-id="b5dcb-137">Deze verbindingsreeks moet verzenden machtigingen toosend hello toohello gebeurtenis berichtenstroom hebben.</span><span class="sxs-lookup"><span data-stu-id="b5dcb-137">This connection string must have send permissions toosend hello message toohello event stream.</span></span>

## <a name="output-usage"></a><span data-ttu-id="b5dcb-138">Gebruik voor uitvoer</span><span class="sxs-lookup"><span data-stu-id="b5dcb-138">Output usage</span></span>
<span data-ttu-id="b5dcb-139">Deze sectie leest u hoe toouse de Event Hubs uitvoer binding in uw functiecode.</span><span class="sxs-lookup"><span data-stu-id="b5dcb-139">This section shows you how toouse your Event Hubs output binding in your function code.</span></span>

<span data-ttu-id="b5dcb-140">U kunt berichten toohello geconfigureerd event hub uitvoer Hello parametertypen te volgen:</span><span class="sxs-lookup"><span data-stu-id="b5dcb-140">You can output messages toohello configured event hub with hello following parameter types:</span></span>

* `out string`
* <span data-ttu-id="b5dcb-141">`ICollector<string>`(toooutput meerdere berichten)</span><span class="sxs-lookup"><span data-stu-id="b5dcb-141">`ICollector<string>` (toooutput multiple messages)</span></span>
* <span data-ttu-id="b5dcb-142">`IAsyncCollector<string>`(async-versie van `ICollector<T>`)</span><span class="sxs-lookup"><span data-stu-id="b5dcb-142">`IAsyncCollector<string>` (async version of `ICollector<T>`)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="b5dcb-143">Voorbeeld van uitvoer</span><span class="sxs-lookup"><span data-stu-id="b5dcb-143">Output sample</span></span>
<span data-ttu-id="b5dcb-144">Stel dat u hebt de volgende Hallo Event Hubs binding in Hallo uitvoer `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="b5dcb-144">Suppose you have hello following Event Hubs output binding in hello `bindings` array of function.json:</span></span>

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

<span data-ttu-id="b5dcb-145">Zie Hallo taalspecifieke voorbeeldtoepassing die u een gebeurtenis toohello zelfs stroom schrijft.</span><span class="sxs-lookup"><span data-stu-id="b5dcb-145">See hello language-specific sample that writes an event toohello even stream.</span></span>

* [<span data-ttu-id="b5dcb-146">C#</span><span class="sxs-lookup"><span data-stu-id="b5dcb-146">C#</span></span>](#outcsharp)
* [<span data-ttu-id="b5dcb-147">F#</span><span class="sxs-lookup"><span data-stu-id="b5dcb-147">F#</span></span>](#outfsharp)
* [<span data-ttu-id="b5dcb-148">Node.js</span><span class="sxs-lookup"><span data-stu-id="b5dcb-148">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="b5dcb-149">Voorbeeld van uitvoer in C#</span><span class="sxs-lookup"><span data-stu-id="b5dcb-149">Output sample in C#</span></span> #

```cs
using System;

public static void Run(TimerInfo myTimer, out string outputEventHubMessage, TraceWriter log)
{
    String msg = $"TimerTriggerCSharp1 executed at: {DateTime.Now}";
    log.Verbose(msg);   
    outputEventHubMessage = msg;
}
```

<span data-ttu-id="b5dcb-150">Of toocreate meerdere berichten:</span><span class="sxs-lookup"><span data-stu-id="b5dcb-150">Or, toocreate multiple messages:</span></span>

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

### <a name="output-sample-in-f"></a><span data-ttu-id="b5dcb-151">Voorbeeld van uitvoer in F #</span><span class="sxs-lookup"><span data-stu-id="b5dcb-151">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, outputEventHubMessage: byref<string>, log: TraceWriter) =
    let msg = sprintf "TimerTriggerFSharp1 executed at: %s" DateTime.Now.ToString()
    log.Verbose(msg);
    outputEventHubMessage <- msg;
```

<a name="outnodejs"></a>

### <a name="output-sample-for-nodejs"></a><span data-ttu-id="b5dcb-152">Voorbeeld van uitvoer voor Node.js</span><span class="sxs-lookup"><span data-stu-id="b5dcb-152">Output sample for Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();
    context.log('Event Hub message created at: ', timeStamp);   
    context.bindings.outputEventHubMessage = "Event Hub message created at: " + timeStamp;
    context.done();
};
```

<span data-ttu-id="b5dcb-153">Of toosend meerdere berichten</span><span class="sxs-lookup"><span data-stu-id="b5dcb-153">Or, toosend multiple messages,</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="b5dcb-154">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b5dcb-154">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
