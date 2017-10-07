---
title: aaaAzure functies queue storage bindingen | Microsoft Docs
description: Begrijpen hoe Azure Storage toouse triggers en bindingen in Azure Functions.
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: Azure functions, functies, verwerking van gebeurtenissen, dynamische compute zonder server architectuur
ms.assetid: 4e6a837d-e64f-45a0-87b7-aa02688a75f3
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: glenga
ms.openlocfilehash: 438b4f63e823149072c86fdefa7e15bfd2a2c4df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-queue-storage-bindings"></a>Azure Functions Queue Storage bindingen
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Dit artikel wordt beschreven hoe tooconfigure en code Azure Queue storage bindingen in de Azure Functions. Azure Functions ondersteunt activeren en uitvoer van de bindingen voor Azure wachtrijen. Zie functies die beschikbaar in alle bindingen zijn [Azure Functions triggers en bindingen concepten](functions-triggers-bindings.md).

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="queue-storage-trigger"></a>Queue storage trigger
Hello Azure Queue storage trigger kunt u de opslag van een wachtrij voor nieuwe berichten toomonitor en toothem reageren. 

Een wachtrij trigger met Hallo definiëren **integreren** tabblad in Hallo Functions-portal. Hallo portal maakt na definitie in Hallo Hallo **bindingen** sectie van *function.json*:

```json
{
    "type": "queueTrigger",
    "direction": "in",
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "queueName": "<Name of queue toopoll>",
    "connection":"<Name of app setting - see below>"
}
```

* Hallo `connection` eigenschap Hallo-naam van een app-instelling met een verbindingsreeks voor opslag moet bevatten. Hallo in hello Azure-portal, standaardeditor in Hallo **integreren** tabblad dit app-instelling die u configureert wanneer u een opslagaccount selecteren.

Extra instellingen kunnen worden opgegeven in een [host.json bestand](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) toofurther stemmen queue storage-triggers. U kunt bijvoorbeeld Hallo wachtrij polling-interval in host.json wijzigen.

<a name="triggerusage"></a>

## <a name="using-a-queue-trigger"></a>Met behulp van een trigger wachtrij
In een Node.js-functies, toegang heeft tot Hallo wachtrij gegevens met `context.bindings.<name>`.


Toegang tot Hallo wachtrij nettolading met een parameter van de methode, zoals in de .NET-functies `CloudQueueMessage paramName`. Hier `paramName` is Hallo-waarde die u hebt opgegeven in Hallo [trigger configuratie](#trigger). Hallo-bericht van wachtrij kan gedeserialiseerde tooany Hallo volgende typen zijn:

* POCO-object. Gebruik deze optie als de nettolading van de wachtrij Hallo een JSON-object is. Hallo functies runtime deserializes Hallo nettolading in Hallo POCO-object. 
* `string`
* `byte[]`
* [`CloudQueueMessage`]

<a name="meta"></a>

### <a name="queue-trigger-metadata"></a>Wachtrij trigger metagegevens
Hallo wachtrij trigger biedt verschillende eigenschappen voor metagegevens. Deze eigenschappen kunnen worden gebruikt als onderdeel van de expressies voor gegevensbinding in andere bindingen of als parameters in uw code. Hallo waarden Hallo hebben dezelfde betekenis als [ `CloudQueueMessage` ].

* **QueueTrigger** -nettolading van de wachtrij (als een geldige tekenreeks)
* **DequeueCount** -Type `int`. Hallo aantal keren dat dit bericht uit wachtrij is geplaatst.
* **ExpirationTime** -Type `DateTimeOffset?`. Hallo-tijd die het Hallo-bericht is verlopen.
* **Id** -Type `string`. Wachtrij bericht-ID.
* **InsertionTime** -Type `DateTimeOffset?`. Hallo-tijd die het Hallo-bericht toohello wachtrij is toegevoegd.
* **NextVisibleTime** -Type `DateTimeOffset?`. Hallo-tijd die het Hallo-bericht naast zichtbaar zijn.
* **PopReceipt** -Type `string`. Hallo-bericht pop ontvangst.

Zie hoe toouse metagegevens in de wachtrij Hallo [Trigger voorbeeld](#triggersample).

<a name="triggersample"></a>

## <a name="trigger-sample"></a>Voorbeeld van de trigger
Stel dat u hebt Hallo function.json die de trigger van een wachtrij definieert te volgen:

```json
{
    "disabled": false,
    "bindings": [
        {
            "type": "queueTrigger",
            "direction": "in",
            "name": "myQueueItem",
            "queueName": "myqueue-items",
            "connection":"MyStorageConnectionString"
        }
    ]
}
```

Zie Hallo taalspecifieke steekproef die worden opgehaald en logboeken van de metagegevens van de wachtrij.

* [C#](#triggercsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>Voorbeeld van de trigger in C# #
```csharp
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Queue;
using System;

public static void Run(CloudQueueMessage myQueueItem, 
    DateTimeOffset expirationTime, 
    DateTimeOffset insertionTime, 
    DateTimeOffset nextVisibleTime,
    string queueTrigger,
    string id,
    string popReceipt,
    int dequeueCount,
    TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem.AsString}\n" +
        $"queueTrigger={queueTrigger}\n" +
        $"expirationTime={expirationTime}\n" +
        $"insertionTime={insertionTime}\n" +
        $"nextVisibleTime={nextVisibleTime}\n" +
        $"id={id}\n" +
        $"popReceipt={popReceipt}\n" + 
        $"dequeueCount={dequeueCount}");
}
```

<!--
<a name="triggerfsharp"></a>
### Trigger sample in F# ## 
```fsharp

```
-->

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a>Voorbeeld van de trigger in Node.js

```javascript
module.exports = function (context) {
    context.log('Node.js queue trigger function processed work item', context.bindings.myQueueItem);
    context.log('queueTrigger =', context.bindingData.queueTrigger);
    context.log('expirationTime =', context.bindingData.expirationTime);
    context.log('insertionTime =', context.bindingData.insertionTime);
    context.log('nextVisibleTime =', context.bindingData.nextVisibleTime);
    context.log('id=', context.bindingData.id);
    context.log('popReceipt =', context.bindingData.popReceipt);
    context.log('dequeueCount =', context.bindingData.dequeueCount);
    context.done();
};
```

### <a name="handling-poison-queue-messages"></a>Verwerken van verontreinigde berichten
Wanneer een functie van de trigger wachtrij is mislukt, probeert die functie up toofive tijden voor een bepaalde wachtrijbericht Hallo eerst probeer opnieuw in Azure Functions. Als alle vijf pogingen mislukken, Hallo functions-runtime voegt een bericht tooa queue storage met de naam  *&lt;originalqueuename >-verontreinigd*. U schrijft een functie tooprocess berichten uit Hallo verontreinigd wachtrij registratie of het verzenden van een melding dat handmatige aandacht nodig is. 

handmatig controleren Hallo toohandle verontreinigde berichten `dequeueCount` van wachtrij het Hallo-bericht (Zie [wachtrij trigger metagegevens](#meta)).

<a name="output"></a>

## <a name="queue-storage-output-binding"></a>Queue storage uitvoer binding
Hello Azure queue storage uitvoer binding kunt u toowrite berichten tooa wachtrij. 

Definieer een wachtrij uitvoer binding met Hallo **integreren** tabblad in Hallo Functions-portal. Hallo portal maakt na definitie in Hallo Hallo **bindingen** sectie van *function.json*:

```json
{
   "type": "queue",
   "direction": "out",
   "name": "<hello name used tooidentify hello trigger data in your code>",
   "queueName": "<Name of queue toowrite to>",
   "connection":"<Name of app setting - see below>"
}
```

* Hallo `connection` eigenschap Hallo-naam van een app-instelling met een verbindingsreeks voor opslag moet bevatten. Hallo in hello Azure-portal, standaardeditor in Hallo **integreren** tabblad dit app-instelling die u configureert wanneer u een opslagaccount selecteren.

<a name="outputusage"></a>

## <a name="using-a-queue-output-binding"></a>Binding met behulp van een wachtrij uitvoer
In Node.js-functies, opent u met behulp Hallo uitvoer wachtrij `context.bindings.<name>`.

In de .NET-functies, kunt u tooany van de volgende typen Hallo uitvoeren. Wanneer er een typeparameter `T`, `T` moet een van de typen van de uitvoer hello wordt ondersteund, zoals `string` of een POCO.

* `out T`(geserialiseerd als JSON)
* `out string`
* `out byte[]`
* `out` [`CloudQueueMessage`] 
* `ICollector<T>`
* `IAsyncCollector<T>`
* [`CloudQueue`](/dotnet/api/microsoft.windowsazure.storage.queue.cloudqueue)

U kunt ook retourtype Hallo-methode gebruiken als Hallo uitvoer van de binding.

<a name="outputsample"></a>

## <a name="queue-output-sample"></a>Voorbeeld van wachtrij-uitvoer
Hallo volgende *function.json* definieert een HTTP-trigger met een wachtrij binding uitvoer:

```json
{
  "bindings": [
    {
      "type": "httpTrigger",
      "direction": "in",
      "authLevel": "function",
      "name": "input"
    },
    {
      "type": "http",
      "direction": "out",
      "name": "return"
    },
    {
      "type": "queue",
      "direction": "out",
      "name": "$return",
      "queueName": "outqueue",
      "connection": "MyStorageConnectionString",
    }
  ]
}
``` 

Zie Hallo taalspecifieke voorbeeldtoepassing die u een wachtrijbericht met Hallo binnenkomende HTTP-nettolading levert.

* [C#](#outcsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="queue-output-sample-in-c"></a>Voorbeeld van uitvoer wachtrij in C# #

```cs
// C# example of HTTP trigger binding tooa custom POCO, with a queue output binding
public class CustomQueueMessage
{
    public string PersonName { get; set; }
    public string Title { get; set; }
}

public static CustomQueueMessage Run(CustomQueueMessage input, TraceWriter log)
{
    return input;
}
```

toosend meerdere berichten gebruiken een `ICollector`:

```cs
public static void Run(CustomQueueMessage input, ICollector<CustomQueueMessage> myQueueItem, TraceWriter log)
{
    myQueueItem.Add(input);
    myQueueItem.Add(new CustomQueueMessage { PersonName = "You", Title = "None" });
}
```

<a name="outnodejs"></a>

### <a name="queue-output-sample-in-nodejs"></a>Voorbeeld van uitvoer wachtrij in Node.js

```javascript
module.exports = function (context, input) {
    context.done(null, input.body);
};
```

Of toosend meerdere berichten

```javascript
module.exports = function(context) {
    // Define a message array for hello myQueueItem output binding. 
    context.bindings.myQueueItem = ["message 1","message 2"];
    context.done();
};
```

## <a name="next-steps"></a>Volgende stappen

Zie voor een voorbeeld van een functie die gebruikmaakt van queue storage-triggers en bindingen [maken van een Azure-functie verbonden tooan Azure service](functions-create-an-azure-connected-function.md).

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

<!-- LINKS -->

['CloudQueueMessage']: /dotnet/api/microsoft.windowsazure.storage.queue.cloudqueuemessage
