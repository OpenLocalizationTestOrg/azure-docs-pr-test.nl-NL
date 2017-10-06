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
# <a name="azure-functions-event-hubs-bindings"></a>Azure Functions Event Hubs-bindingen
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Dit artikel wordt uitgelegd hoe tooconfigure en gebruik [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) bindingen voor Azure Functions.
Azure Functions ondersteunt activeren en uitvoer van de bindingen voor Event Hubs.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Als u nieuwe tooAzure Event Hubs, Zie Hallo [overzicht van Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md).

<a name="trigger"></a>

## <a name="event-hub-trigger"></a>Event hub trigger
Gebruik Hallo Event Hubs gebeurtenis toorespond tooan tooan event hub gebeurtenisstroom verzonden. U moet leestoegang toohello event hub tooset up Hallo trigger hebben.

Hallo Event Hubs functie trigger gebruikt de volgende JSON-object in Hallo Hallo `bindings` matrix van function.json:

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

`consumerGroup`is een optionele eigenschap gebruikt tooset hello [consumergroep](../event-hubs/event-hubs-features.md#event-consumers) toosubscribe tooevents in Hallo hub gebruikt. Als u dit weglaat, Hallo `$Default` consumergroep wordt gebruikt.  
`connection`moet Hallo-naam van een app-instelling met naamruimte Hallo connection string toohello gebeurtenis van de hub.
Kopieer deze verbindingsreeks door te klikken op Hallo **verbindingsgegevens** knop voor Hallo *naamruimte*, niet Hallo event hub zelf. Deze verbindingsreeks heeft moet ten minste machtigingen tooactivate Hallo trigger lezen.

[Extra instellingen](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) kan worden opgegeven in een host.json bestand toofurther fijn stemmen Event Hubs-triggers.  

<a name="triggerusage"></a>

## <a name="trigger-usage"></a>Gebruik van de trigger
Wanneer een functie van Event Hubs trigger wordt geactiveerd, wordt in de functie Hallo Hallo-bericht dat deze wordt geactiveerd doorgegeven als een tekenreeks.

<a name="triggersample"></a>

## <a name="trigger-sample"></a>Voorbeeld van de trigger
Stel dat u volgende Event Hubs in Hallo activeren Hallo hebt `bindings` matrix van function.json:

```json
{
  "type": "eventHubTrigger",
  "name": "myEventHubMessage",
  "direction": "in",
  "path": "MyEventHub",
  "connection": "myEventHubReadConnectionString"
}
```

Zie Hallo taalspecifieke steekproef die het Hallo-berichttekst van Hallo event hub trigger registreert.

* [C#](#triggercsharp)
* [F#](#triggerfsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>Voorbeeld van de trigger in C# #

```cs
using System;

public static void Run(string myEventHubMessage, TraceWriter log)
{
    log.Info($"C# Event Hub trigger function processed a message: {myEventHubMessage}");
}
```

U kunt ook Hallo-gebeurtenis ontvangen een [EventData](/dotnet/api/microsoft.servicebus.messaging.eventdata) object, waarmee u toegang tot toohello gebeurtenis metagegevens.

```cs
#r "Microsoft.ServiceBus"
using System.Text;
using Microsoft.ServiceBus.Messaging;

public static void Run(EventData myEventHubMessage, TraceWriter log)
{
    log.Info($"{Encoding.UTF8.GetString(myEventHubMessage.GetBytes())}");
}
```

gebeurtenissen in een batch tooreceive Hallo methodehandtekening ook wijzigen`string[]` of `EventData[]`.

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

### <a name="trigger-sample-in-f"></a>Voorbeeld van de trigger in F # #

```fsharp
let Run(myEventHubMessage: string, log: TraceWriter) =
    log.Info(sprintf "F# eventhub trigger function processed work item: %s" myEventHubMessage)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a>Voorbeeld van de trigger in Node.js

```javascript
module.exports = function (context, myEventHubMessage) {
    context.log('Node.js eventhub trigger function processed work item', myEventHubMessage);    
    context.done();
};
```

<a name="output"></a>

## <a name="event-hubs-output-binding"></a>Event Hubs uitvoer binding
Gebruik Hallo Event Hubs uitvoer binding toowrite gebeurtenissen tooan event hub stroom gebeurtenissen. U moet verzenden machtiging tooan event hub toowrite gebeurtenissen tooit hebben.

Hallo uitvoer binding gebruikt Hallo volgende JSON-object in Hallo `bindings` matrix van function.json:

```json
{
    "type": "eventHub",
    "name": "<Name of output parameter in function signature>",
    "path": "<Name of event hub>",
    "connection": "<Name of app setting with connection string - see below>"
    "direction": "out"
}
```

`connection`moet Hallo-naam van een app-instelling met naamruimte Hallo connection string toohello gebeurtenis van de hub.
Kopieer deze verbindingsreeks door te klikken op Hallo **verbindingsgegevens** knop voor Hallo *naamruimte*, niet Hallo event hub zelf. Deze verbindingsreeks moet verzenden machtigingen toosend hello toohello gebeurtenis berichtenstroom hebben.

## <a name="output-usage"></a>Gebruik voor uitvoer
Deze sectie leest u hoe toouse de Event Hubs uitvoer binding in uw functiecode.

U kunt berichten toohello geconfigureerd event hub uitvoer Hello parametertypen te volgen:

* `out string`
* `ICollector<string>`(toooutput meerdere berichten)
* `IAsyncCollector<string>`(async-versie van `ICollector<T>`)

<a name="outputsample"></a>

## <a name="output-sample"></a>Voorbeeld van uitvoer
Stel dat u hebt de volgende Hallo Event Hubs binding in Hallo uitvoer `bindings` matrix van function.json:

```json
{
    "type": "eventHub",
    "name": "outputEventHubMessage",
    "path": "myeventhub",
    "connection": "MyEventHubSend",
    "direction": "out"
}
```

Zie Hallo taalspecifieke voorbeeldtoepassing die u een gebeurtenis toohello zelfs stroom schrijft.

* [C#](#outcsharp)
* [F#](#outfsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Voorbeeld van uitvoer in C# #

```cs
using System;

public static void Run(TimerInfo myTimer, out string outputEventHubMessage, TraceWriter log)
{
    String msg = $"TimerTriggerCSharp1 executed at: {DateTime.Now}";
    log.Verbose(msg);   
    outputEventHubMessage = msg;
}
```

Of toocreate meerdere berichten:

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

### <a name="output-sample-in-f"></a>Voorbeeld van uitvoer in F # #

```fsharp
let Run(myTimer: TimerInfo, outputEventHubMessage: byref<string>, log: TraceWriter) =
    let msg = sprintf "TimerTriggerFSharp1 executed at: %s" DateTime.Now.ToString()
    log.Verbose(msg);
    outputEventHubMessage <- msg;
```

<a name="outnodejs"></a>

### <a name="output-sample-for-nodejs"></a>Voorbeeld van uitvoer voor Node.js

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();
    context.log('Event Hub message created at: ', timeStamp);   
    context.bindings.outputEventHubMessage = "Event Hub message created at: " + timeStamp;
    context.done();
};
```

Of toosend meerdere berichten

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

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
