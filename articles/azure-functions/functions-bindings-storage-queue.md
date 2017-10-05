---
title: Azure Functions wachtrij opslag bindingen | Microsoft Docs
description: Het gebruik van Azure Storage-triggers en bindingen in de Azure Functions begrijpen.
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
ms.openlocfilehash: e007acd75a2210d54f512e2c6698c90919f0fcd2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-queue-storage-bindings"></a><span data-ttu-id="daac2-104">Azure Functions Queue Storage bindingen</span><span class="sxs-lookup"><span data-stu-id="daac2-104">Azure Functions Queue Storage bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="daac2-105">Dit artikel wordt beschreven hoe u configureert en code Azure Queue storage bindingen in de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="daac2-105">This article describes how to configure and code Azure Queue storage bindings in Azure Functions.</span></span> <span data-ttu-id="daac2-106">Azure Functions ondersteunt activeren en uitvoer van de bindingen voor Azure wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="daac2-106">Azure Functions supports trigger and output bindings for Azure queues.</span></span> <span data-ttu-id="daac2-107">Zie functies die beschikbaar in alle bindingen zijn [Azure Functions triggers en bindingen concepten](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="daac2-107">For features that are available in all bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="queue-storage-trigger"></a><span data-ttu-id="daac2-108">Queue storage trigger</span><span class="sxs-lookup"><span data-stu-id="daac2-108">Queue storage trigger</span></span>
<span data-ttu-id="daac2-109">De trigger van Azure Queue storage kunt u de opslag van een wachtrij voor nieuwe berichten controleren en reageren op deze.</span><span class="sxs-lookup"><span data-stu-id="daac2-109">The Azure Queue storage trigger enables you to monitor a queue storage for new messages and react to them.</span></span> 

<span data-ttu-id="daac2-110">Definieer een wachtrij trigger met de **integreren** tabblad in de portal functies.</span><span class="sxs-lookup"><span data-stu-id="daac2-110">Define a queue trigger using the **Integrate** tab in the Functions portal.</span></span> <span data-ttu-id="daac2-111">De portal maakt de volgende definitie in de **bindingen** sectie van *function.json*:</span><span class="sxs-lookup"><span data-stu-id="daac2-111">The portal creates the following definition in the  **bindings** section of *function.json*:</span></span>

```json
{
    "type": "queueTrigger",
    "direction": "in",
    "name": "<The name used to identify the trigger data in your code>",
    "queueName": "<Name of queue to poll>",
    "connection":"<Name of app setting - see below>"
}
```

* <span data-ttu-id="daac2-112">De `connection` eigenschap moet bevatten de naam van een app-instelling met een verbindingsreeks voor opslag.</span><span class="sxs-lookup"><span data-stu-id="daac2-112">The `connection` property must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="daac2-113">In de Azure portal, de standaard editor in de **integreren** tabblad dit app-instelling die u configureert wanneer u een opslagaccount selecteren.</span><span class="sxs-lookup"><span data-stu-id="daac2-113">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

<span data-ttu-id="daac2-114">Extra instellingen kunnen worden opgegeven in een [host.json bestand](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) naar queue storage-triggers verder te verfijnen.</span><span class="sxs-lookup"><span data-stu-id="daac2-114">Additional settings can be provided in a [host.json file](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json) to further fine-tune queue storage triggers.</span></span> <span data-ttu-id="daac2-115">U kunt bijvoorbeeld de polling-interval in host.json wachtrij wijzigen.</span><span class="sxs-lookup"><span data-stu-id="daac2-115">For example, you can change the queue polling interval in host.json.</span></span>

<a name="triggerusage"></a>

## <a name="using-a-queue-trigger"></a><span data-ttu-id="daac2-116">Met behulp van een trigger wachtrij</span><span class="sxs-lookup"><span data-stu-id="daac2-116">Using a queue trigger</span></span>
<span data-ttu-id="daac2-117">In een Node.js-functies, toegang heeft tot de wachtrij gegevens met `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="daac2-117">In Node.js functions, access the queue data using `context.bindings.<name>`.</span></span>


<span data-ttu-id="daac2-118">Toegang tot de nettolading van de wachtrij met een parameter van de methode, zoals in de .NET-functies `CloudQueueMessage paramName`.</span><span class="sxs-lookup"><span data-stu-id="daac2-118">In .NET functions, access the queue payload using a method parameter such as `CloudQueueMessage paramName`.</span></span> <span data-ttu-id="daac2-119">Hier `paramName` is de waarde die u hebt opgegeven in de [trigger configuratie](#trigger).</span><span class="sxs-lookup"><span data-stu-id="daac2-119">Here, `paramName` is the value you specified in the [trigger configuration](#trigger).</span></span> <span data-ttu-id="daac2-120">Bericht uit de wachtrij kan worden gedeserialiseerd met een van de volgende typen:</span><span class="sxs-lookup"><span data-stu-id="daac2-120">The queue message can be deserialized to any of the following types:</span></span>

* <span data-ttu-id="daac2-121">POCO-object.</span><span class="sxs-lookup"><span data-stu-id="daac2-121">POCO object.</span></span> <span data-ttu-id="daac2-122">Gebruik deze optie als de nettolading van de wachtrij een JSON-object is.</span><span class="sxs-lookup"><span data-stu-id="daac2-122">Use if the queue payload is a JSON object.</span></span> <span data-ttu-id="daac2-123">De runtime van Functions deserializes de nettolading in de POCO-object.</span><span class="sxs-lookup"><span data-stu-id="daac2-123">The Functions runtime deserializes the payload into the POCO object.</span></span> 
* `string`
* `byte[]`
* [`CloudQueueMessage`]

<a name="meta"></a>

### <a name="queue-trigger-metadata"></a><span data-ttu-id="daac2-124">Wachtrij trigger metagegevens</span><span class="sxs-lookup"><span data-stu-id="daac2-124">Queue trigger metadata</span></span>
<span data-ttu-id="daac2-125">De trigger wachtrij biedt verschillende eigenschappen voor metagegevens.</span><span class="sxs-lookup"><span data-stu-id="daac2-125">The queue trigger provides several metadata properties.</span></span> <span data-ttu-id="daac2-126">Deze eigenschappen kunnen worden gebruikt als onderdeel van de expressies voor gegevensbinding in andere bindingen of als parameters in uw code.</span><span class="sxs-lookup"><span data-stu-id="daac2-126">These properties can be used as part of binding expressions in other bindings or as parameters in your code.</span></span> <span data-ttu-id="daac2-127">De waarden hebben dezelfde betekenis als [ `CloudQueueMessage` ].</span><span class="sxs-lookup"><span data-stu-id="daac2-127">The values have the same semantics as [`CloudQueueMessage`].</span></span>

* <span data-ttu-id="daac2-128">**QueueTrigger** -nettolading van de wachtrij (als een geldige tekenreeks)</span><span class="sxs-lookup"><span data-stu-id="daac2-128">**QueueTrigger** - queue payload (if a valid string)</span></span>
* <span data-ttu-id="daac2-129">**DequeueCount** -Type `int`.</span><span class="sxs-lookup"><span data-stu-id="daac2-129">**DequeueCount** - Type `int`.</span></span> <span data-ttu-id="daac2-130">Het aantal keren dat dit bericht uit wachtrij is geplaatst.</span><span class="sxs-lookup"><span data-stu-id="daac2-130">The number of times this message has been dequeued.</span></span>
* <span data-ttu-id="daac2-131">**ExpirationTime** -Type `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="daac2-131">**ExpirationTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="daac2-132">De tijd waarop het bericht is verlopen.</span><span class="sxs-lookup"><span data-stu-id="daac2-132">The time that the message expires.</span></span>
* <span data-ttu-id="daac2-133">**Id** -Type `string`.</span><span class="sxs-lookup"><span data-stu-id="daac2-133">**Id** - Type `string`.</span></span> <span data-ttu-id="daac2-134">Wachtrij bericht-ID.</span><span class="sxs-lookup"><span data-stu-id="daac2-134">Queue message ID.</span></span>
* <span data-ttu-id="daac2-135">**InsertionTime** -Type `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="daac2-135">**InsertionTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="daac2-136">De tijd die het bericht is toegevoegd aan de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="daac2-136">The time that the message was added to the queue.</span></span>
* <span data-ttu-id="daac2-137">**NextVisibleTime** -Type `DateTimeOffset?`.</span><span class="sxs-lookup"><span data-stu-id="daac2-137">**NextVisibleTime** - Type `DateTimeOffset?`.</span></span> <span data-ttu-id="daac2-138">De tijd die het bericht vervolgens zichtbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="daac2-138">The time that the message will next be visible.</span></span>
* <span data-ttu-id="daac2-139">**PopReceipt** -Type `string`.</span><span class="sxs-lookup"><span data-stu-id="daac2-139">**PopReceipt** - Type `string`.</span></span> <span data-ttu-id="daac2-140">Pop ontvangst van het bericht.</span><span class="sxs-lookup"><span data-stu-id="daac2-140">The message's pop receipt.</span></span>

<span data-ttu-id="daac2-141">Informatie over het gebruiken van de metagegevens van de wachtrij in [Trigger voorbeeld](#triggersample).</span><span class="sxs-lookup"><span data-stu-id="daac2-141">See how to use the queue metadata in [Trigger sample](#triggersample).</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="daac2-142">Voorbeeld van de trigger</span><span class="sxs-lookup"><span data-stu-id="daac2-142">Trigger sample</span></span>
<span data-ttu-id="daac2-143">Stel dat u hebt de volgende function.json die een trigger wachtrij definieert:</span><span class="sxs-lookup"><span data-stu-id="daac2-143">Suppose you have the following function.json that defines a queue trigger:</span></span>

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

<span data-ttu-id="daac2-144">Zie het voorbeeld taalspecifieke die worden opgehaald en logboeken van de metagegevens van de wachtrij.</span><span class="sxs-lookup"><span data-stu-id="daac2-144">See the language-specific sample that retrieves and logs queue metadata.</span></span>

* [<span data-ttu-id="daac2-145">C#</span><span class="sxs-lookup"><span data-stu-id="daac2-145">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="daac2-146">Node.js</span><span class="sxs-lookup"><span data-stu-id="daac2-146">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="daac2-147">Voorbeeld van de trigger in C#</span><span class="sxs-lookup"><span data-stu-id="daac2-147">Trigger sample in C#</span></span> #
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

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="daac2-148">Voorbeeld van de trigger in Node.js</span><span class="sxs-lookup"><span data-stu-id="daac2-148">Trigger sample in Node.js</span></span>

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

### <a name="handling-poison-queue-messages"></a><span data-ttu-id="daac2-149">Verwerken van verontreinigde berichten</span><span class="sxs-lookup"><span data-stu-id="daac2-149">Handling poison queue messages</span></span>
<span data-ttu-id="daac2-150">Wanneer een functie van de trigger wachtrij mislukt pogingen Azure Functions die functie maximaal vijf keer voor een bepaalde wachtrij-bericht, met inbegrip van de eerste poging.</span><span class="sxs-lookup"><span data-stu-id="daac2-150">When a queue trigger function fails, Azure Functions retries that function up to five times for a given queue message, including the first try.</span></span> <span data-ttu-id="daac2-151">Als alle vijf pogingen mislukken, wordt een bericht met de runtime van functions toegevoegd aan de opslag van een wachtrij met de naam  *&lt;originalqueuename >-verontreinigd*.</span><span class="sxs-lookup"><span data-stu-id="daac2-151">If all five attempts fail, the functions runtime adds a message to a queue storage named *&lt;originalqueuename>-poison*.</span></span> <span data-ttu-id="daac2-152">U kunt schrijven om een functie verwerken van berichten uit de wachtrij verontreinigd door registratie of het verzenden van een melding dat handmatige aandacht nodig is.</span><span class="sxs-lookup"><span data-stu-id="daac2-152">You can write a function to process messages from the poison queue by logging them or sending a  notification that manual attention is needed.</span></span> 

<span data-ttu-id="daac2-153">Voor het afhandelen van verontreinigde berichten handmatig, Controleer de `dequeueCount` van het bericht uit de wachtrij (Zie [wachtrij trigger metagegevens](#meta)).</span><span class="sxs-lookup"><span data-stu-id="daac2-153">To handle poison messages manually, check the `dequeueCount` of the queue message (see [Queue trigger metadata](#meta)).</span></span>

<a name="output"></a>

## <a name="queue-storage-output-binding"></a><span data-ttu-id="daac2-154">Queue storage uitvoer binding</span><span class="sxs-lookup"><span data-stu-id="daac2-154">Queue storage output binding</span></span>
<span data-ttu-id="daac2-155">De Azure queue storage uitvoer binding kunt u berichten schrijven naar een wachtrij.</span><span class="sxs-lookup"><span data-stu-id="daac2-155">The Azure queue storage output binding enables you to write messages to a queue.</span></span> 

<span data-ttu-id="daac2-156">Definieer een wachtrij uitvoer binding met de **integreren** tabblad in de portal functies.</span><span class="sxs-lookup"><span data-stu-id="daac2-156">Define a queue output binding using the **Integrate** tab in the Functions portal.</span></span> <span data-ttu-id="daac2-157">De portal maakt de volgende definitie in de **bindingen** sectie van *function.json*:</span><span class="sxs-lookup"><span data-stu-id="daac2-157">The portal creates the following definition in the  **bindings** section of *function.json*:</span></span>

```json
{
   "type": "queue",
   "direction": "out",
   "name": "<The name used to identify the trigger data in your code>",
   "queueName": "<Name of queue to write to>",
   "connection":"<Name of app setting - see below>"
}
```

* <span data-ttu-id="daac2-158">De `connection` eigenschap moet bevatten de naam van een app-instelling met een verbindingsreeks voor opslag.</span><span class="sxs-lookup"><span data-stu-id="daac2-158">The `connection` property must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="daac2-159">In de Azure portal, de standaard editor in de **integreren** tabblad dit app-instelling die u configureert wanneer u een opslagaccount selecteren.</span><span class="sxs-lookup"><span data-stu-id="daac2-159">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you select a storage account.</span></span>

<a name="outputusage"></a>

## <a name="using-a-queue-output-binding"></a><span data-ttu-id="daac2-160">Binding met behulp van een wachtrij uitvoer</span><span class="sxs-lookup"><span data-stu-id="daac2-160">Using a queue output binding</span></span>
<span data-ttu-id="daac2-161">In een Node.js-functies, opent u de uitvoer wachtrij via `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="daac2-161">In Node.js functions, you access the output queue using `context.bindings.<name>`.</span></span>

<span data-ttu-id="daac2-162">In de .NET-functies, kunt u uitvoeren met een van de volgende typen.</span><span class="sxs-lookup"><span data-stu-id="daac2-162">In .NET functions, you can output to any of the following types.</span></span> <span data-ttu-id="daac2-163">Wanneer er een typeparameter `T`, `T` moet een van de ondersteunde uitvoermethode typen, zoals `string` of een POCO.</span><span class="sxs-lookup"><span data-stu-id="daac2-163">When there is a type parameter `T`, `T` must be one of the supported output types, such as `string` or a POCO.</span></span>

* <span data-ttu-id="daac2-164">`out T`(geserialiseerd als JSON)</span><span class="sxs-lookup"><span data-stu-id="daac2-164">`out T` (serialized as JSON)</span></span>
* `out string`
* `out byte[]`
* <span data-ttu-id="daac2-165">`out` [`CloudQueueMessage`]</span><span class="sxs-lookup"><span data-stu-id="daac2-165">`out` [`CloudQueueMessage`]</span></span> 
* `ICollector<T>`
* `IAsyncCollector<T>`
* [`CloudQueue`](/dotnet/api/microsoft.windowsazure.storage.queue.cloudqueue)

<span data-ttu-id="daac2-166">U kunt het retourtype van methode ook gebruiken als de uitvoer-binding.</span><span class="sxs-lookup"><span data-stu-id="daac2-166">You can also use the method return type as the output binding.</span></span>

<a name="outputsample"></a>

## <a name="queue-output-sample"></a><span data-ttu-id="daac2-167">Voorbeeld van wachtrij-uitvoer</span><span class="sxs-lookup"><span data-stu-id="daac2-167">Queue output sample</span></span>
<span data-ttu-id="daac2-168">De volgende *function.json* definieert een HTTP-trigger met een wachtrij binding uitvoer:</span><span class="sxs-lookup"><span data-stu-id="daac2-168">The following *function.json* defines an HTTP trigger with a queue output binding:</span></span>

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

<span data-ttu-id="daac2-169">Zie het voorbeeld taalspecifieke die een wachtrijbericht met de nettolading van de binnenkomende HTTP-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="daac2-169">See the language-specific sample that outputs a queue message with the incoming HTTP payload.</span></span>

* [<span data-ttu-id="daac2-170">C#</span><span class="sxs-lookup"><span data-stu-id="daac2-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="daac2-171">Node.js</span><span class="sxs-lookup"><span data-stu-id="daac2-171">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="queue-output-sample-in-c"></a><span data-ttu-id="daac2-172">Voorbeeld van uitvoer wachtrij in C#</span><span class="sxs-lookup"><span data-stu-id="daac2-172">Queue output sample in C#</span></span> #

```cs
// C# example of HTTP trigger binding to a custom POCO, with a queue output binding
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

<span data-ttu-id="daac2-173">Meerdere om berichten te verzenden, gebruikt u een `ICollector`:</span><span class="sxs-lookup"><span data-stu-id="daac2-173">To send multiple messages, use an `ICollector`:</span></span>

```cs
public static void Run(CustomQueueMessage input, ICollector<CustomQueueMessage> myQueueItem, TraceWriter log)
{
    myQueueItem.Add(input);
    myQueueItem.Add(new CustomQueueMessage { PersonName = "You", Title = "None" });
}
```

<a name="outnodejs"></a>

### <a name="queue-output-sample-in-nodejs"></a><span data-ttu-id="daac2-174">Voorbeeld van uitvoer wachtrij in Node.js</span><span class="sxs-lookup"><span data-stu-id="daac2-174">Queue output sample in Node.js</span></span>

```javascript
module.exports = function (context, input) {
    context.done(null, input.body);
};
```

<span data-ttu-id="daac2-175">Of om meerdere berichten te verzenden</span><span class="sxs-lookup"><span data-stu-id="daac2-175">Or, to send multiple messages,</span></span>

```javascript
module.exports = function(context) {
    // Define a message array for the myQueueItem output binding. 
    context.bindings.myQueueItem = ["message 1","message 2"];
    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="daac2-176">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="daac2-176">Next steps</span></span>

<span data-ttu-id="daac2-177">Zie voor een voorbeeld van een functie die gebruikmaakt van queue storage-triggers en bindingen [maken een Azure-functie die is verbonden met een Azure-service](functions-create-an-azure-connected-function.md).</span><span class="sxs-lookup"><span data-stu-id="daac2-177">For an example of a function that uses queue storage triggers and bindings, see [Create an Azure Function connected to an Azure service](functions-create-an-azure-connected-function.md).</span></span>

[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

<!-- LINKS -->

['CloudQueueMessage']: /dotnet/api/microsoft.windowsazure.storage.queue.cloudqueuemessage
