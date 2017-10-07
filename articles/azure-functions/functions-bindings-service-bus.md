---
title: aaaAzure functies Service Bus triggers en bindingen | Microsoft Docs
description: Begrijpen hoe Azure Service Bus toouse triggers en bindingen in Azure Functions.
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: Azure functions, functies, verwerking van gebeurtenissen, dynamische compute zonder server architectuur
ms.assetid: daedacf0-6546-4355-a65c-50873e74f66b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/01/2017
ms.author: glenga
ms.openlocfilehash: dff9e89bd3840b8c11f91cae41e13502afc7aa60
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-service-bus-bindings"></a>Azure Functions Service Bus-bindingen
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Dit artikel wordt uitgelegd hoe tooconfigure en werken met Azure Service Bus-bindingen in de Azure Functions. 

Azure Functions ondersteunt activeren en uitvoer van de bindingen voor Service Bus-wachtrijen en onderwerpen.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="service-bus-trigger"></a>Service Bus-trigger
Gebruik Hallo Service Bus trigger toorespond toomessages van een Service Bus-wachtrij of onderwerp. 

Hallo zijn Service Bus-wachtrij en onderwerp triggers gedefinieerd door de volgende JSON-objecten in Hallo Hallo `bindings` matrix van function.json:

* *wachtrij* trigger:

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "queueName" : "<Name of hello queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

* *onderwerp* trigger:

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "topicName" : "<Name of hello topic>",
        "subscriptionName" : "<Name of hello subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

Let op Hallo volgende:

* Voor `connection`, [maken van een app-instelling in uw app functie](functions-how-to-use-azure-function-app-settings.md) die Hallo connection string tooyour Service Bus-naamruimte bevat, geeft u vervolgens Hallo-naam van de app-instelling Hallo in Hallo `connection` eigenschap in de trigger. Voor het verkrijgen van de verbindingsreeks Hallo Hallo stappen die wordt weergegeven op [Beheerreferenties hello](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).
  Hallo-verbindingsreeks moet voor een Service Bus-naamruimte, niet beperkt tooa specifieke wachtrij of onderwerp.
  Als u niets `connection` leeg is, Hallo trigger wordt ervan uitgegaan dat er een standaard Service Bus-verbindingsreeks is opgegeven in een app instelling met de naam `AzureWebJobsServiceBus`.
* Voor `accessRights`, beschikbare waarden zijn `manage` en `listen`. Hallo standaardwaarde is `manage`, wat aangeeft dat Hallo `connection` heeft Hallo **beheren** machtiging. Als u een verbindingsreeks die geen Hallo **beheren** , machtigingenset `accessRights` te`listen`. Anders beheren Hallo functies runtime mislukken tijdens toodo bewerkingen uit waarbij rechten.

## <a name="trigger-behavior"></a>Gedrag van de trigger
* **Single-threading** - standaard Hallo functies runtime-processen die meerdere tegelijkertijd berichten. toodirect hello runtime tooprocess slechts één wachtrij of onderwerp bericht op een tijdstip ingesteld `serviceBus.maxConcurrentCalls` too1 in *host.json*. 
  Voor informatie over *host.json*, Zie [mapstructuur](functions-reference.md#folder-structure) en [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).
* **Verwerking van gevaarlijke berichten** -Service Bus biedt een eigen verwerken van verontreinigde berichten die niet kan worden beheerd of geconfigureerd in de configuratie van Azure Functions of code. 
* **PeekLock gedrag** -runtime van Functions Hallo ontvangt een bericht in [ `PeekLock` modus](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) en aanroepen `Complete` op het Hallo-bericht als Hallo-functie wordt voltooid of aanroepen `Abandon` als hello de functie is mislukt. 
  Als het Hallo-functie wordt uitgevoerd langer dan Hallo `PeekLock` time-out Hallo vergrendeling automatisch wordt vernieuwd.

<a name="triggerusage"></a>

## <a name="trigger-usage"></a>Gebruik van de trigger
Deze sectie leest u hoe toouse uw Service Bus activeren in uw functiecode. 

In C# en F # kan Hallo-bericht van Service Bus trigger gedeserialiseerde tooany Hallo invoertypen volgende zijn:

* `string`-nuttig voor string-berichten
* `byte[]`-handig voor binaire gegevens
* Alle [Object](https://msdn.microsoft.com/library/system.object.aspx) - handig voor gegevens JSON-geserialiseerd.
  Als u een aangepaste invoertype zoals declareren `CustomType`, Azure Functions probeert toodeserialize Hallo JSON-gegevens in het opgegeven type.
* `BrokeredMessage`-biedt u Hallo-bericht met Hallo gedeserialiseerd [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) methode.

Hallo-bericht van Service Bus trigger wordt in Node.js, in de functie Hallo als een tekenreeks- of JSON-object doorgegeven.

<a name="triggersample"></a>

## <a name="trigger-sample"></a>Voorbeeld van de trigger
Stel dat u hebt Hallo function.json te volgen:

```json
{
"bindings": [
    {
    "queueName": "testqueue",
    "connection": "MyServiceBusConnection",
    "name": "myQueueItem",
    "type": "serviceBusTrigger",
    "direction": "in"
    }
],
"disabled": false
}
```

Zie Hallo taalspecifieke steekproef die een Service Bus-wachtrijbericht verwerkt.

* [C#](#triggercsharp)
* [F#](#triggerfsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>Voorbeeld van de trigger in C# #

```cs
public static void Run(string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a>Voorbeeld van de trigger in F # #

```fsharp
let Run(myQueueItem: string, log: TraceWriter) =
    log.Info(sprintf "F# ServiceBus queue trigger function processed message: %s" myQueueItem)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a>Voorbeeld van de trigger in Node.js

```javascript
module.exports = function(context, myQueueItem) {
    context.log('Node.js ServiceBus queue trigger function processed message', myQueueItem);
    context.done();
};
```

<a name="output"></a>

## <a name="service-bus-output-binding"></a>Service Bus uitvoer binding
Hallo Service Bus-wachtrij en onderwerp uitvoer voor een functie gebruiken Hallo volgende JSON-objecten in Hallo `bindings` matrix van function.json:

* *wachtrij* uitvoer:

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "queueName" : "<Name of hello queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```
* *onderwerp* uitvoer:

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "topicName" : "<Name of hello topic>",
        "subscriptionName" : "<Name of hello subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for hello connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```

Let op Hallo volgende:

* Voor `connection`, [maken van een app-instelling in uw app functie](functions-how-to-use-azure-function-app-settings.md) die Hallo connection string tooyour Service Bus-naamruimte bevat, geeft u vervolgens Hallo-naam van de app-instelling Hallo in Hallo `connection` eigenschap in de uitvoer binding. Voor het verkrijgen van de verbindingsreeks Hallo Hallo stappen die wordt weergegeven op [Beheerreferenties hello](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).
  Hallo-verbindingsreeks moet voor een Service Bus-naamruimte, niet beperkt tooa specifieke wachtrij of onderwerp.
  Als u niets `connection` leeg is, hello uitvoer binding wordt ervan uitgegaan dat er een standaard Service Bus-verbindingsreeks is opgegeven in een app instelling met de naam `AzureWebJobsServiceBus`.
* Voor `accessRights`, beschikbare waarden zijn `manage` en `listen`. Hallo standaardwaarde is `manage`, wat aangeeft dat Hallo `connection` heeft Hallo **beheren** machtiging. Als u een verbindingsreeks die geen Hallo **beheren** , machtigingenset `accessRights` te`listen`. Anders beheren Hallo functies runtime mislukken tijdens toodo bewerkingen uit waarbij rechten.

<a name="outputusage"></a>

## <a name="output-usage"></a>Gebruik voor uitvoer
Azure Functions kunt het bericht van een Service Bus-wachtrij maken uit een van de volgende typen Hallo in C# en F #:

* Alle [Object](https://msdn.microsoft.com/library/system.object.aspx) -parameterdefinitie ziet eruit als `out T paramName` (C#).
  Functies deserializes Hallo-object in een JSON-bericht. Als bij het verlaten van de functie Hallo Hallo uitvoerwaarde null is, maakt functies Hallo-bericht met een null-object.
* `string`-Parameterdefinitie ziet eruit als `out string paraName` (C#). Als het Hallo-parameterwaarde is niet-null wanneer het Hallo-functie wordt afgesloten, wordt een bericht door functies gemaakt.
* `byte[]`-Parameterdefinitie ziet eruit als `out byte[] paraName` (C#). Als het Hallo-parameterwaarde is niet-null wanneer het Hallo-functie wordt afgesloten, wordt een bericht door functies gemaakt.
* `BrokeredMessage`Parameterdefinitie ziet eruit als `out BrokeredMessage paraName` (C#). Als het Hallo-parameterwaarde is niet-null wanneer het Hallo-functie wordt afgesloten, wordt een bericht door functies gemaakt.

U kunt gebruiken voor het maken van meerdere berichten in een C#-functie, `ICollector<T>` of `IAsyncCollector<T>`. Een bericht wordt gemaakt bij het aanroepen van Hallo `Add` methode.

In Node.js, kunt u een tekenreeks, een bytematrix of een Javascript-object (gedeserialiseerd naar JSON) te toewijzen`context.binding.<paramName>`.

<a name="outputsample"></a>

## <a name="output-sample"></a>Voorbeeld van uitvoer
Stel dat u hebt Hallo function.json die een Service Bus-wachtrij-uitvoer definieert te volgen:

```json
{
    "bindings": [
        {
            "schedule": "0/15 * * * * *",
            "name": "myTimer",
            "runsOnStartup": true,
            "type": "timerTrigger",
            "direction": "in"
        },
        {
            "name": "outputSbQueue",
            "type": "serviceBus",
            "queueName": "testqueue",
            "connection": "MyServiceBusConnection",
            "direction": "out"
        }
    ],
    "disabled": false
}
```

Zie Hallo taalspecifieke voorbeeldtoepassing die u een bericht toohello service bus-wachtrij verzendt.

* [C#](#outcsharp)
* [F#](#outfsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Voorbeeld van uitvoer in C# #

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, out string outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue = message;
}
```

Of toocreate meerdere berichten:

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, ICollector<string> outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue.Add("1 " + message);
    outputSbQueue.Add("2 " + message);
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a>Voorbeeld van uitvoer in F # #

```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter, outputSbQueue: byref<string>) =
    let message = sprintf "Service Bus queue message created at: %s" (DateTime.Now.ToString())
    log.Info(message)
    outputSbQueue = message
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a>Voorbeeld van uitvoer in Node.js

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = message;
    context.done();
};
```

Of toocreate meerdere berichten:

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = [];
    context.bindings.outputSbQueueMsg.push("1 " + message);
    context.bindings.outputSbQueueMsg.push("2 " + message);
    context.done();
};
```

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

