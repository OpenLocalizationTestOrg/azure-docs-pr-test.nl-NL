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
# <a name="azure-functions-queue-storage-bindings"></a><span data-ttu-id="a4d02-104">Azure Functions Queue Storage bindingen</span><span class="sxs-lookup"><span data-stu-id="a4d02-104">Azure Functions Queue Storage bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="a4d02-105">Dit artikel wordt beschreven hoe tooconfigure en code Azure Queue storage bindingen in de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="a4d02-105">This article describes how tooconfigure and code Azure Queue storage bindings in Azure Functions.</span></span> <span data-ttu-id="a4d02-106">Azure Functions ondersteunt activeren en uitvoer van de bindingen voor Azure wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="a4d02-106">Azure Functions supports trigger and output bindings for Azure queues.</span></span> <span data-ttu-id="a4d02-107">Zie functies die beschikbaar in alle bindingen zijn [Azure Functions triggers en bindingen concepten](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="a4d02-107">For features that are available in all bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="queue-storage-trigger"></a><span data-ttu-id="a4d02-108">Queue storage trigger</span><span class="sxs-lookup"><span data-stu-id="a4d02-108">Queue storage trigger</span></span>
<span data-ttu-id="a4d02-109">Hello Azure Queue storage trigger kunt u de opslag van een wachtrij voor nieuwe berichten toomonitor en toothem reageren.</span><span class="sxs-lookup"><span data-stu-id="a4d02-109">hello Azure Queue storage trigger enables you toomonitor a queue storage for new messages and react toothem.</span></span> 

<span data-ttu-id="a4d02-110">Een wachtrij trigger met Hallo definiëren **integreren** tabblad in Hallo Functions-portal.</span><span class="sxs-lookup"><span data-stu-id="a4d02-110">Define a queue trigger using hello **Integrate** tab in hello Functions portal.</span></span> <span data-ttu-id="a4d02-111">Hallo portal maakt na definitie in Hallo Hallo **bindingen** sectie van *function.json*:</span><span class="sxs-lookup"><span data-stu-id="a4d02-111">hello portal creates hello following definition in hello  **bindings** section of *function.json*:</span></span>

```json
{
    "type": "queueTrigger",
    "direction": "in",
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "queueName": "<Name of queue toopoll>",
    "connection":"<Name of app setting - see below>"
}
```

* <span data-ttu-id="a4d02-112">Hallo `connection` eigenschap Hallo-naam van een app-instelling met een verbindingsreeks voor opslag moet bevatten.</span><span class="sxs-lookup"><span data-stu-id="a4d02-112">hello `connection` property must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="a4d02-113">Hallo in hello Azure-portal, standaardeditor in Hallo **integreren** tabblad dit app-instelling die u configureert wanneer u een opslagaccount selecteren.</span><span class="sxs-lookup"><span data-stu-id="a4d02-113">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

<span data-ttu-id="a4d02-114">Extra instellingen kunnen worden opgegeven in een [host.json bestand](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) toofurther stemmen queue storage-triggers.</span><span class="sxs-lookup"><span data-stu-id="a4d02-114">Additional settings can be provided in a [host.json file](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) toofurther fine-tune queue storage triggers.</span></span> <span data-ttu-id="a4d02-115">U kunt bijvoorbeeld Hallo wachtrij polling-interval in host.json wijzigen.</span><span class="sxs-lookup"><span data-stu-id="a4d02-115">For example, you can change hello queue polling interval in host.json.</span></span>

<a name="triggerusage"></a>

## <a name="using-a-queue-trigger"></a><span data-ttu-id="a4d02-116">Met behulp van een trigger wachtrij</span><span class="sxs-lookup"><span data-stu-id="a4d02-116">Using a queue trigger</span></span>
<span data-ttu-id="a4d02-117">In een Node.js-functies, toegang heeft tot Hallo wachtrij gegevens met `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="a4d02-117">In Node.js functions, access hello queue data using `context.bindings.<name>`.</span></span>


<span data-ttu-id="a4d02-118">Toegang tot Hallo wachtrij nettolading met een parameter van de methode, zoals in de .NET-functies `CloudQueueMessage paramName`.</span><span class="sxs-lookup"><span data-stu-id="a4d02-118">In .NET functions, access hello queue payload using a method parameter such as `CloudQueueMessage paramName`.</span></span> <span data-ttu-id="a4d02-119">Hier `paramName` is Hallo-waarde die u hebt opgegeven in Hallo [trigger configuratie](#trigger).</span><span class="sxs-lookup"><span data-stu-id="a4d02-119">Here, `paramName` is hello value you specified in hello [trigger configuration](#trigger).</span></span> <span data-ttu-id="a4d02-120">Hallo-bericht van wachtrij kan gedeserialiseerde tooany Hallo volgende typen zijn:</span><span class="sxs-lookup"><span data-stu-id="a4d02-120">hello queue message can be deserialized tooany of hello following types:</span></span>

* <span data-ttu-id="a4d02-121">POCO-object.</span><span class="sxs-lookup"><span data-stu-id="a4d02-121">POCO object.</span></span> <span data-ttu-id="a4d02-122">Gebruik deze optie als de nettolading van de wachtrij Hallo een JSON-object is.</span><span class="sxs-lookup"><span data-stu-id="a4d02-122">Use if hello queue payload is a JSON object.</span></span> <span data-ttu-id="a4d02-123">Hallo functies runtime deserializes Hallo nettolading in Hallo POCO-object.</span><span class="sxs-lookup"><span data-stu-id="a4d02-123">hello Functions runtime deserializes hello payload into hello POCO object.</span></span> 
* `string`
* `byte[]`
* [`CloudQueueMessage`]

<a name="meta"></a>

### <a name="queue-trigger-metadata"></a><span data-ttu-id="a4d02-124">Wachtrij trigger metagegevens</span><span class="sxs-lookup"><span data-stu-id="a4d02-124">Queue trigger metadata</span></span>
<span data-ttu-id="a4d02-125">Hallo wachtrij trigger biedt verschillende eigenschappen voor metagegevens.</span><span class="sxs-lookup"><span data-stu-id="a4d02-125">hello queue trigger provides several metadata properties.</span></span> <span data-ttu-id="a4d02-126">Deze eigenschappen kunnen worden gebruikt als onderdeel van de expressies voor gegevensbinding in andere bindingen of als parameters in uw code.</span><span class="sxs-lookup"><span data-stu-id="a4d02-126">These properties can be used as part of binding expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="a4d02-127">Hallo waarden Hallo hebben dezelfde betekenis als [ `CloudQueueMessage` ].</span><span class="sxs-lookup"><span data-stu-id="a4d02-127">hello values have hello same semantics as [`CloudQueueMessage`].</span></span>

* <span data-ttu-id="a4d02-128">**QueueTrigger** -nettolading van de wachtrij (als een geldige tekenreeks)</span><span class="sxs-lookup"><span data-stu-id="a4d02-128">**QueueTrigger** - queue payload (if a valid string)</span></span>
* <span data-ttu-id="a4d02-129">**DequeueCount** -Type `int`.</span><span class="sxs-lookup"><span data-stu-id="a4d02-129">**DequeueCount** - Type `int`.</span></span> <span data-ttu-id="a4d02-130">Hallo aantal keren dat dit bericht uit wachtrij is geplaatst.</span><span class="sxs-lookup"><span data-stu-id="a4d02-130">hello number of times this message has been dequeued.</span></span>
* <span data-ttu-id="a4d02-131">**ExpirationTime** -Type `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="a4d02-131">**ExpirationTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="a4d02-132">Hallo-tijd die het Hallo-bericht is verlopen.</span><span class="sxs-lookup"><span data-stu-id="a4d02-132">hello time that hello message expires.</span></span>
* <span data-ttu-id="a4d02-133">**Id** -Type `string`.</span><span class="sxs-lookup"><span data-stu-id="a4d02-133">**Id** - Type `string`.</span></span> <span data-ttu-id="a4d02-134">Wachtrij bericht-ID.</span><span class="sxs-lookup"><span data-stu-id="a4d02-134">Queue message ID.</span></span>
* <span data-ttu-id="a4d02-135">**InsertionTime** -Type `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="a4d02-135">**InsertionTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="a4d02-136">Hallo-tijd die het Hallo-bericht toohello wachtrij is toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="a4d02-136">hello time that hello message was added toohello queue.</span></span>
* <span data-ttu-id="a4d02-137">**NextVisibleTime** -Type `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="a4d02-137">**NextVisibleTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="a4d02-138">Hallo-tijd die het Hallo-bericht naast zichtbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="a4d02-138">hello time that hello message will next be visible.</span></span>
* <span data-ttu-id="a4d02-139">**PopReceipt** -Type `string`.</span><span class="sxs-lookup"><span data-stu-id="a4d02-139">**PopReceipt** - Type `string`.</span></span> <span data-ttu-id="a4d02-140">Hallo-bericht pop ontvangst.</span><span class="sxs-lookup"><span data-stu-id="a4d02-140">hello message's pop receipt.</span></span>

<span data-ttu-id="a4d02-141">Zie hoe toouse metagegevens in de wachtrij Hallo [Trigger voorbeeld](#triggersample).</span><span class="sxs-lookup"><span data-stu-id="a4d02-141">See how toouse hello queue metadata in [Trigger sample](#triggersample).</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="a4d02-142">Voorbeeld van de trigger</span><span class="sxs-lookup"><span data-stu-id="a4d02-142">Trigger sample</span></span>
<span data-ttu-id="a4d02-143">Stel dat u hebt Hallo function.json die de trigger van een wachtrij definieert te volgen:</span><span class="sxs-lookup"><span data-stu-id="a4d02-143">Suppose you have hello following function.json that defines a queue trigger:</span></span>

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

<span data-ttu-id="a4d02-144">Zie Hallo taalspecifieke steekproef die worden opgehaald en logboeken van de metagegevens van de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="a4d02-144">See hello language-specific sample that retrieves and logs queue metadata.</span></span>

* [<span data-ttu-id="a4d02-145">C#</span><span class="sxs-lookup"><span data-stu-id="a4d02-145">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="a4d02-146">Node.js</span><span class="sxs-lookup"><span data-stu-id="a4d02-146">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="a4d02-147">Voorbeeld van de trigger in C#</span><span class="sxs-lookup"><span data-stu-id="a4d02-147">Trigger sample in C#</span></span> #
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

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="a4d02-148">Voorbeeld van de trigger in Node.js</span><span class="sxs-lookup"><span data-stu-id="a4d02-148">Trigger sample in Node.js</span></span>

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

### <a name="handling-poison-queue-messages"></a><span data-ttu-id="a4d02-149">Verwerken van verontreinigde berichten</span><span class="sxs-lookup"><span data-stu-id="a4d02-149">Handling poison queue messages</span></span>
<span data-ttu-id="a4d02-150">Wanneer een functie van de trigger wachtrij is mislukt, probeert die functie up toofive tijden voor een bepaalde wachtrijbericht Hallo eerst probeer opnieuw in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="a4d02-150">When a queue trigger function fails, Azure Functions retries that function up toofive times for a given queue message, including hello first try.</span></span> <span data-ttu-id="a4d02-151">Als alle vijf pogingen mislukken, Hallo functions-runtime voegt een bericht tooa queue storage met de naam  *&lt;originalqueuename >-verontreinigd*.</span><span class="sxs-lookup"><span data-stu-id="a4d02-151">If all five attempts fail, hello functions runtime adds a message tooa queue storage named *&lt;originalqueuename>-poison*.</span></span> <span data-ttu-id="a4d02-152">U schrijft een functie tooprocess berichten uit Hallo verontreinigd wachtrij registratie of het verzenden van een melding dat handmatige aandacht nodig is.</span><span class="sxs-lookup"><span data-stu-id="a4d02-152">You can write a function tooprocess messages from hello poison queue by logging them or sending a  notification that manual attention is needed.</span></span> 

<span data-ttu-id="a4d02-153">handmatig controleren Hallo toohandle verontreinigde berichten `dequeueCount` van wachtrij het Hallo-bericht (Zie [wachtrij trigger metagegevens](#meta)).</span><span class="sxs-lookup"><span data-stu-id="a4d02-153">toohandle poison messages manually, check hello `dequeueCount` of hello queue message (see [Queue trigger metadata](#meta)).</span></span>

<a name="output"></a>

## <a name="queue-storage-output-binding"></a><span data-ttu-id="a4d02-154">Queue storage uitvoer binding</span><span class="sxs-lookup"><span data-stu-id="a4d02-154">Queue storage output binding</span></span>
<span data-ttu-id="a4d02-155">Hello Azure queue storage uitvoer binding kunt u toowrite berichten tooa wachtrij.</span><span class="sxs-lookup"><span data-stu-id="a4d02-155">hello Azure queue storage output binding enables you toowrite messages tooa queue.</span></span> 

<span data-ttu-id="a4d02-156">Definieer een wachtrij uitvoer binding met Hallo **integreren** tabblad in Hallo Functions-portal.</span><span class="sxs-lookup"><span data-stu-id="a4d02-156">Define a queue output binding using hello **Integrate** tab in hello Functions portal.</span></span> <span data-ttu-id="a4d02-157">Hallo portal maakt na definitie in Hallo Hallo **bindingen** sectie van *function.json*:</span><span class="sxs-lookup"><span data-stu-id="a4d02-157">hello portal creates hello following definition in hello  **bindings** section of *function.json*:</span></span>

```json
{
   "type": "queue",
   "direction": "out",
   "name": "<hello name used tooidentify hello trigger data in your code>",
   "queueName": "<Name of queue toowrite to>",
   "connection":"<Name of app setting - see below>"
}
```

* <span data-ttu-id="a4d02-158">Hallo `connection` eigenschap Hallo-naam van een app-instelling met een verbindingsreeks voor opslag moet bevatten.</span><span class="sxs-lookup"><span data-stu-id="a4d02-158">hello `connection` property must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="a4d02-159">Hallo in hello Azure-portal, standaardeditor in Hallo **integreren** tabblad dit app-instelling die u configureert wanneer u een opslagaccount selecteren.</span><span class="sxs-lookup"><span data-stu-id="a4d02-159">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

<a name="outputusage"></a>

## <a name="using-a-queue-output-binding"></a><span data-ttu-id="a4d02-160">Binding met behulp van een wachtrij uitvoer</span><span class="sxs-lookup"><span data-stu-id="a4d02-160">Using a queue output binding</span></span>
<span data-ttu-id="a4d02-161">In Node.js-functies, opent u met behulp Hallo uitvoer wachtrij `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="a4d02-161">In Node.js functions, you access hello output queue using `context.bindings.<name>`.</span></span>

<span data-ttu-id="a4d02-162">In de .NET-functies, kunt u tooany van de volgende typen Hallo uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a4d02-162">In .NET functions, you can output tooany of hello following types.</span></span> <span data-ttu-id="a4d02-163">Wanneer er een typeparameter `T`, `T` moet een van de typen van de uitvoer hello wordt ondersteund, zoals `string` of een POCO.</span><span class="sxs-lookup"><span data-stu-id="a4d02-163">When there is a type parameter `T`, `T` must be one of hello supported output types, such as `string` or a POCO.</span></span>

* <span data-ttu-id="a4d02-164">`out T`(geserialiseerd als JSON)</span><span class="sxs-lookup"><span data-stu-id="a4d02-164">`out T` (serialized as JSON)</span></span>
* `out string`
* `out byte[]`
* <span data-ttu-id="a4d02-165">`out` [`CloudQueueMessage`]</span><span class="sxs-lookup"><span data-stu-id="a4d02-165">`out` [`CloudQueueMessage`]</span></span> 
* `ICollector<T>`
* `IAsyncCollector<T>`
* [`CloudQueue`](/dotnet/api/microsoft.windowsazure.storage.queue.cloudqueue)

<span data-ttu-id="a4d02-166">U kunt ook retourtype Hallo-methode gebruiken als Hallo uitvoer van de binding.</span><span class="sxs-lookup"><span data-stu-id="a4d02-166">You can also use hello method return type as hello output binding.</span></span>

<a name="outputsample"></a>

## <a name="queue-output-sample"></a><span data-ttu-id="a4d02-167">Voorbeeld van wachtrij-uitvoer</span><span class="sxs-lookup"><span data-stu-id="a4d02-167">Queue output sample</span></span>
<span data-ttu-id="a4d02-168">Hallo volgende *function.json* definieert een HTTP-trigger met een wachtrij binding uitvoer:</span><span class="sxs-lookup"><span data-stu-id="a4d02-168">hello following *function.json* defines an HTTP trigger with a queue output binding:</span></span>

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

<span data-ttu-id="a4d02-169">Zie Hallo taalspecifieke voorbeeldtoepassing die u een wachtrijbericht met Hallo binnenkomende HTTP-nettolading levert.</span><span class="sxs-lookup"><span data-stu-id="a4d02-169">See hello language-specific sample that outputs a queue message with hello incoming HTTP payload.</span></span>

* [<span data-ttu-id="a4d02-170">C#</span><span class="sxs-lookup"><span data-stu-id="a4d02-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="a4d02-171">Node.js</span><span class="sxs-lookup"><span data-stu-id="a4d02-171">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="queue-output-sample-in-c"></a><span data-ttu-id="a4d02-172">Voorbeeld van uitvoer wachtrij in C#</span><span class="sxs-lookup"><span data-stu-id="a4d02-172">Queue output sample in C#</span></span> #

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

<span data-ttu-id="a4d02-173">toosend meerdere berichten gebruiken een `ICollector`:</span><span class="sxs-lookup"><span data-stu-id="a4d02-173">toosend multiple messages, use an `ICollector`:</span></span>

```cs
public static void Run(CustomQueueMessage input, ICollector<CustomQueueMessage> myQueueItem, TraceWriter log)
{
    myQueueItem.Add(input);
    myQueueItem.Add(new CustomQueueMessage { PersonName = "You", Title = "None" });
}
```

<a name="outnodejs"></a>

### <a name="queue-output-sample-in-nodejs"></a><span data-ttu-id="a4d02-174">Voorbeeld van uitvoer wachtrij in Node.js</span><span class="sxs-lookup"><span data-stu-id="a4d02-174">Queue output sample in Node.js</span></span>

```javascript
module.exports = function (context, input) {
    context.done(null, input.body);
};
```

<span data-ttu-id="a4d02-175">Of toosend meerdere berichten</span><span class="sxs-lookup"><span data-stu-id="a4d02-175">Or, toosend multiple messages,</span></span>

```javascript
module.exports = function(context) {
    // Define a message array for hello myQueueItem output binding. 
    context.bindings.myQueueItem = ["message 1","message 2"];
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="a4d02-176">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a4d02-176">Next steps</span></span>

<span data-ttu-id="a4d02-177">Zie voor een voorbeeld van een functie die gebruikmaakt van queue storage-triggers en bindingen [maken van een Azure-functie verbonden tooan Azure service](functions-create-an-azure-connected-function.md).</span><span class="sxs-lookup"><span data-stu-id="a4d02-177">For an example of a function that uses queue storage triggers and bindings, see [Create an Azure Function connected tooan Azure service](functions-create-an-azure-connected-function.md).</span></span>

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

<!-- LINKS -->

['CloudQueueMessage']: /dotnet/api/microsoft.windowsazure.storage.queue.cloudqueuemessage
