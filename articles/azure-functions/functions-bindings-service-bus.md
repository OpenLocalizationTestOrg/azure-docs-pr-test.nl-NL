---
title: Azure Functions Service Bus-triggers en bindingen | Microsoft Docs
description: Het gebruik van Azure Service Bus-triggers en bindingen in de Azure Functions begrijpen.
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
ms.openlocfilehash: b3ee306cd37ebf88dc9369ccc2dc6c670557fd5a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-service-bus-bindings"></a><span data-ttu-id="e512c-104">Azure Functions Service Bus-bindingen</span><span class="sxs-lookup"><span data-stu-id="e512c-104">Azure Functions Service Bus bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="e512c-105">In dit artikel wordt uitgelegd hoe configureren en werken met Azure Service Bus-bindingen in de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="e512c-105">This article explains how to configure and work with Azure Service Bus bindings in Azure Functions.</span></span> 

<span data-ttu-id="e512c-106">Azure Functions ondersteunt activeren en uitvoer van de bindingen voor Service Bus-wachtrijen en onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="e512c-106">Azure Functions supports trigger and output bindings for Service Bus queues and topics.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="service-bus-trigger"></a><span data-ttu-id="e512c-107">Service Bus-trigger</span><span class="sxs-lookup"><span data-stu-id="e512c-107">Service Bus trigger</span></span>
<span data-ttu-id="e512c-108">Gebruik de Service Bus-trigger om te reageren op berichten van een Service Bus-wachtrij of onderwerp.</span><span class="sxs-lookup"><span data-stu-id="e512c-108">Use the Service Bus trigger to respond to messages from a Service Bus queue or topic.</span></span> 

<span data-ttu-id="e512c-109">De Service Bus-wachtrij en onderwerp triggers zijn gedefinieerd door de volgende JSON-objecten in de `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="e512c-109">The Service Bus queue and topic triggers are defined by the following JSON objects in the `bindings` array of function.json:</span></span>

* <span data-ttu-id="e512c-110">*wachtrij* trigger:</span><span class="sxs-lookup"><span data-stu-id="e512c-110">*queue* trigger:</span></span>

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "queueName" : "<Name of the queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

* <span data-ttu-id="e512c-111">*onderwerp* trigger:</span><span class="sxs-lookup"><span data-stu-id="e512c-111">*topic* trigger:</span></span>

    ```json
    {
        "name" : "<Name of input parameter in function signature>",
        "topicName" : "<Name of the topic>",
        "subscriptionName" : "<Name of the subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBusTrigger",
        "direction" : "in"
    }
    ```

<span data-ttu-id="e512c-112">Houd rekening met het volgende:</span><span class="sxs-lookup"><span data-stu-id="e512c-112">Note the following:</span></span>

* <span data-ttu-id="e512c-113">Voor `connection`, [maken van een app-instelling in uw app functie](functions-how-to-use-azure-function-app-settings.md) die de verbindingsreeks naar uw Service Bus-naamruimte bevat, geeft u de naam van de app-instelling in de `connection` eigenschap in de trigger.</span><span class="sxs-lookup"><span data-stu-id="e512c-113">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains the connection string to your Service Bus namespace, then specify the name of the app setting in the `connection` property in your trigger.</span></span> <span data-ttu-id="e512c-114">Verkrijgen van de verbindingsreeks door de stappen die wordt weergegeven op [Beheerreferenties](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span><span class="sxs-lookup"><span data-stu-id="e512c-114">You obtain the connection string by following the steps shown at [Obtain the management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="e512c-115">De verbindingsreeks moet voor een Service Bus-naamruimte niet beperkt tot een specifieke wachtrij of onderwerp.</span><span class="sxs-lookup"><span data-stu-id="e512c-115">The connection string must be for a Service Bus namespace, not limited to a specific queue or topic.</span></span>
  <span data-ttu-id="e512c-116">Als u niets `connection` leeg is, wordt de trigger wordt ervan uitgegaan dat er een standaard Service Bus-verbindingsreeks is opgegeven in een app instelling met de naam `AzureWebJobsServiceBus`.</span><span class="sxs-lookup"><span data-stu-id="e512c-116">If you leave `connection` empty, the trigger assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="e512c-117">Voor `accessRights`, beschikbare waarden zijn `manage` en `listen`.</span><span class="sxs-lookup"><span data-stu-id="e512c-117">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="e512c-118">De standaardwaarde is `manage`, wat aangeeft dat de `connection` heeft de **beheren** machtiging.</span><span class="sxs-lookup"><span data-stu-id="e512c-118">The default is `manage`, which indicates that the `connection` has the **Manage** permission.</span></span> <span data-ttu-id="e512c-119">Als u een verbindingsreeks die u niet beschikt over de **beheren** , machtigingenset `accessRights` naar `listen`.</span><span class="sxs-lookup"><span data-stu-id="e512c-119">If you use a connection string that does not have the **Manage** permission, set `accessRights` to `listen`.</span></span> <span data-ttu-id="e512c-120">De runtime mislukken kan voor bewerkingen waarvoor probeert functies beheren anders rechten.</span><span class="sxs-lookup"><span data-stu-id="e512c-120">Otherwise, the Functions runtime might fail trying to do operations that require manage rights.</span></span>

## <a name="trigger-behavior"></a><span data-ttu-id="e512c-121">Gedrag van de trigger</span><span class="sxs-lookup"><span data-stu-id="e512c-121">Trigger behavior</span></span>
* <span data-ttu-id="e512c-122">**Single-threading** - standaard de functies runtime-processen die meerdere tegelijkertijd berichten.</span><span class="sxs-lookup"><span data-stu-id="e512c-122">**Single-threading** - By default, the Functions runtime processes multiple messages concurrently.</span></span> <span data-ttu-id="e512c-123">Stel rechtstreeks runtime slechts een enkele wachtrij of onderwerp bericht tegelijkertijd wordt verwerkt, `serviceBus.maxConcurrentCalls` op 1 in *host.json*.</span><span class="sxs-lookup"><span data-stu-id="e512c-123">To direct the runtime to process only a single queue or topic message at a time, set `serviceBus.maxConcurrentCalls` to 1 in *host.json*.</span></span> 
  <span data-ttu-id="e512c-124">Voor informatie over *host.json*, Zie [mapstructuur](functions-reference.md#folder-structure) en [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="e512c-124">For information about *host.json*, see [Folder Structure](functions-reference.md#folder-structure) and [host.json](https://github .com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>
* <span data-ttu-id="e512c-125">**Verwerking van gevaarlijke berichten** -Service Bus biedt een eigen verwerken van verontreinigde berichten die niet kan worden beheerd of geconfigureerd in de configuratie van Azure Functions of code.</span><span class="sxs-lookup"><span data-stu-id="e512c-125">**Poison message handling** - Service Bus does its own poison message handling, which can't be controlled or configured in Azure Functions configuration or code.</span></span> 
* <span data-ttu-id="e512c-126">**PeekLock gedrag** -de runtime van Functions ontvangt een bericht in [ `PeekLock` modus](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) en aanroepen `Complete` op het bericht als de functie wordt voltooid of aanroepen `Abandon` als de functie mislukt.</span><span class="sxs-lookup"><span data-stu-id="e512c-126">**PeekLock behavior** - The Functions runtime receives a message in [`PeekLock` mode](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) and calls `Complete` on the message if the function finishes successfully, or calls `Abandon` if the function fails.</span></span> 
  <span data-ttu-id="e512c-127">Als de functie wordt uitgevoerd langer dan de `PeekLock` een time-out opgetreden, de vergrendeling wordt automatisch verlengd.</span><span class="sxs-lookup"><span data-stu-id="e512c-127">If the function runs longer than the `PeekLock` timeout, the lock is automatically renewed.</span></span>

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="e512c-128">Gebruik van de trigger</span><span class="sxs-lookup"><span data-stu-id="e512c-128">Trigger usage</span></span>
<span data-ttu-id="e512c-129">Deze sectie laat zien hoe uw Service Bus-trigger te gebruiken in uw functiecode.</span><span class="sxs-lookup"><span data-stu-id="e512c-129">This section shows you how to use your Service Bus trigger in your function code.</span></span> 

<span data-ttu-id="e512c-130">In C# en F #, kan het bericht Service Bus-trigger worden gedeserialiseerd met een van de volgende invoertypen:</span><span class="sxs-lookup"><span data-stu-id="e512c-130">In C# and F#, the Service Bus trigger message can be deserialized to any of the following input types:</span></span>

* <span data-ttu-id="e512c-131">`string`-nuttig voor string-berichten</span><span class="sxs-lookup"><span data-stu-id="e512c-131">`string` - useful for string messages</span></span>
* <span data-ttu-id="e512c-132">`byte[]`-handig voor binaire gegevens</span><span class="sxs-lookup"><span data-stu-id="e512c-132">`byte[]` - useful for binary data</span></span>
* <span data-ttu-id="e512c-133">Alle [Object](https://msdn.microsoft.com/library/system.object.aspx) - handig voor gegevens JSON-geserialiseerd.</span><span class="sxs-lookup"><span data-stu-id="e512c-133">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized data.</span></span>
  <span data-ttu-id="e512c-134">Als u een aangepaste invoertype zoals declareren `CustomType`, Azure Functions geprobeerd te deserialiseren van de JSON-gegevens in het opgegeven type.</span><span class="sxs-lookup"><span data-stu-id="e512c-134">If you declare a custom input type, such as `CustomType`, Azure Functions tries to deserialize the JSON data into your specified type.</span></span>
* <span data-ttu-id="e512c-135">`BrokeredMessage`-kunt u het gedeserialiseerde bericht met de [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) methode.</span><span class="sxs-lookup"><span data-stu-id="e512c-135">`BrokeredMessage` - gives you the deserialized message with the [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) method.</span></span>

<span data-ttu-id="e512c-136">In Node.js, wordt het bericht Service Bus-trigger in de functie als een tekenreeks- of JSON-object doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="e512c-136">In Node.js, the Service Bus trigger message is passed into the function as either a string or JSON object.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="e512c-137">Voorbeeld van de trigger</span><span class="sxs-lookup"><span data-stu-id="e512c-137">Trigger sample</span></span>
<span data-ttu-id="e512c-138">Stel dat u hebt de volgende function.json:</span><span class="sxs-lookup"><span data-stu-id="e512c-138">Suppose you have the following function.json:</span></span>

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

<span data-ttu-id="e512c-139">Zie het voorbeeld taalspecifieke die een Service Bus-wachtrijbericht verwerkt.</span><span class="sxs-lookup"><span data-stu-id="e512c-139">See the language-specific sample that processes a Service Bus queue message.</span></span>

* [<span data-ttu-id="e512c-140">C#</span><span class="sxs-lookup"><span data-stu-id="e512c-140">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="e512c-141">F#</span><span class="sxs-lookup"><span data-stu-id="e512c-141">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="e512c-142">Node.js</span><span class="sxs-lookup"><span data-stu-id="e512c-142">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="e512c-143">Voorbeeld van de trigger in C#</span><span class="sxs-lookup"><span data-stu-id="e512c-143">Trigger sample in C#</span></span> #

```cs
public static void Run(string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a><span data-ttu-id="e512c-144">Voorbeeld van de trigger in F #</span><span class="sxs-lookup"><span data-stu-id="e512c-144">Trigger sample in F#</span></span> #

```fsharp
let Run(myQueueItem: string, log: TraceWriter) =
    log.Info(sprintf "F# ServiceBus queue trigger function processed message: %s" myQueueItem)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="e512c-145">Voorbeeld van de trigger in Node.js</span><span class="sxs-lookup"><span data-stu-id="e512c-145">Trigger sample in Node.js</span></span>

```javascript
module.exports = function(context, myQueueItem) {
    context.log('Node.js ServiceBus queue trigger function processed message', myQueueItem);
    context.done();
};
```

<a name="output"></a>

## <a name="service-bus-output-binding"></a><span data-ttu-id="e512c-146">Service Bus uitvoer binding</span><span class="sxs-lookup"><span data-stu-id="e512c-146">Service Bus output binding</span></span>
<span data-ttu-id="e512c-147">De Service Bus-wachtrij en onderwerp uitvoer voor een functie gebruiken de volgende JSON-objecten in de `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="e512c-147">The Service Bus queue and topic output for a function use the following JSON objects in the `bindings` array of function.json:</span></span>

* <span data-ttu-id="e512c-148">*wachtrij* uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e512c-148">*queue* output:</span></span>

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "queueName" : "<Name of the queue>",
        "connection" : "<Name of app setting that has your queue's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```
* <span data-ttu-id="e512c-149">*onderwerp* uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e512c-149">*topic* output:</span></span>

    ```json
    {
        "name" : "<Name of output parameter in function signature>",
        "topicName" : "<Name of the topic>",
        "subscriptionName" : "<Name of the subscription>",
        "connection" : "<Name of app setting that has your topic's connection string - see below>",
        "accessRights" : "<Access rights for the connection string - see below>",
        "type" : "serviceBus",
        "direction" : "out"
    }
    ```

<span data-ttu-id="e512c-150">Houd rekening met het volgende:</span><span class="sxs-lookup"><span data-stu-id="e512c-150">Note the following:</span></span>

* <span data-ttu-id="e512c-151">Voor `connection`, [maken van een app-instelling in uw app functie](functions-how-to-use-azure-function-app-settings.md) die de verbindingsreeks naar uw Service Bus-naamruimte bevat, geeft u de naam van de app-instelling in de `connection` eigenschap in de uitvoer-binding.</span><span class="sxs-lookup"><span data-stu-id="e512c-151">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains the connection string to your Service Bus namespace, then specify the name of the app setting in the `connection` property in your output binding.</span></span> <span data-ttu-id="e512c-152">Verkrijgen van de verbindingsreeks door de stappen die wordt weergegeven op [Beheerreferenties](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span><span class="sxs-lookup"><span data-stu-id="e512c-152">You obtain the connection string by following the steps shown at [Obtain the management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="e512c-153">De verbindingsreeks moet voor een Service Bus-naamruimte niet beperkt tot een specifieke wachtrij of onderwerp.</span><span class="sxs-lookup"><span data-stu-id="e512c-153">The connection string must be for a Service Bus namespace, not limited to a specific queue or topic.</span></span>
  <span data-ttu-id="e512c-154">Als u niets `connection` leeg is, wordt de uitvoer-binding wordt ervan uitgegaan dat er een standaard Service Bus-verbindingsreeks is opgegeven in een app instelling met de naam `AzureWebJobsServiceBus`.</span><span class="sxs-lookup"><span data-stu-id="e512c-154">If you leave `connection` empty, the output binding assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="e512c-155">Voor `accessRights`, beschikbare waarden zijn `manage` en `listen`.</span><span class="sxs-lookup"><span data-stu-id="e512c-155">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="e512c-156">De standaardwaarde is `manage`, wat aangeeft dat de `connection` heeft de **beheren** machtiging.</span><span class="sxs-lookup"><span data-stu-id="e512c-156">The default is `manage`, which indicates that the `connection` has the **Manage** permission.</span></span> <span data-ttu-id="e512c-157">Als u een verbindingsreeks die u niet beschikt over de **beheren** , machtigingenset `accessRights` naar `listen`.</span><span class="sxs-lookup"><span data-stu-id="e512c-157">If you use a connection string that does not have the **Manage** permission, set `accessRights` to `listen`.</span></span> <span data-ttu-id="e512c-158">De runtime mislukken kan voor bewerkingen waarvoor probeert functies beheren anders rechten.</span><span class="sxs-lookup"><span data-stu-id="e512c-158">Otherwise, the Functions runtime might fail trying to do operations that require manage rights.</span></span>

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="e512c-159">Gebruik voor uitvoer</span><span class="sxs-lookup"><span data-stu-id="e512c-159">Output usage</span></span>
<span data-ttu-id="e512c-160">In C# en F # kunt Azure Functions een Service Bus-wachtrijbericht maken van elk van de volgende typen:</span><span class="sxs-lookup"><span data-stu-id="e512c-160">In C# and F#, Azure Functions can create a Service Bus queue message from any of the following types:</span></span>

* <span data-ttu-id="e512c-161">Alle [Object](https://msdn.microsoft.com/library/system.object.aspx) -parameterdefinitie ziet eruit als `out T paramName` (C#).</span><span class="sxs-lookup"><span data-stu-id="e512c-161">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - Parameter definition looks like `out T paramName` (C#).</span></span>
  <span data-ttu-id="e512c-162">Functies deserializes het object in een JSON-bericht.</span><span class="sxs-lookup"><span data-stu-id="e512c-162">Functions deserializes the object into a JSON message.</span></span> <span data-ttu-id="e512c-163">Als de uitvoerwaarde is null wanneer de functie wordt afgesloten, wordt het bericht in functies gemaakt met een null-object.</span><span class="sxs-lookup"><span data-stu-id="e512c-163">If the output value is null when the function exits, Functions creates the message with a null object.</span></span>
* <span data-ttu-id="e512c-164">`string`-Parameterdefinitie ziet eruit als `out string paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="e512c-164">`string` - Parameter definition looks like `out string paraName` (C#).</span></span> <span data-ttu-id="e512c-165">Als de parameterwaarde is niet-null wanneer de functie wordt afgesloten, wordt een bericht door functies gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e512c-165">If the parameter value is non-null when the function exits, Functions creates a message.</span></span>
* <span data-ttu-id="e512c-166">`byte[]`-Parameterdefinitie ziet eruit als `out byte[] paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="e512c-166">`byte[]` - Parameter definition looks like `out byte[] paraName` (C#).</span></span> <span data-ttu-id="e512c-167">Als de parameterwaarde is niet-null wanneer de functie wordt afgesloten, wordt een bericht door functies gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e512c-167">If the parameter value is non-null when the function exits, Functions creates a message.</span></span>
* <span data-ttu-id="e512c-168">`BrokeredMessage`Parameterdefinitie ziet eruit als `out BrokeredMessage paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="e512c-168">`BrokeredMessage` Parameter definition looks like `out BrokeredMessage paraName` (C#).</span></span> <span data-ttu-id="e512c-169">Als de parameterwaarde is niet-null wanneer de functie wordt afgesloten, wordt een bericht door functies gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e512c-169">If the parameter value is non-null when the function exits, Functions creates a message.</span></span>

<span data-ttu-id="e512c-170">U kunt gebruiken voor het maken van meerdere berichten in een C#-functie, `ICollector<T>` of `IAsyncCollector<T>`.</span><span class="sxs-lookup"><span data-stu-id="e512c-170">For creating multiple messages in a C# function, you can use `ICollector<T>` or `IAsyncCollector<T>`.</span></span> <span data-ttu-id="e512c-171">Een bericht wordt gemaakt bij het aanroepen van de `Add` methode.</span><span class="sxs-lookup"><span data-stu-id="e512c-171">A message is created when you call the `Add` method.</span></span>

<span data-ttu-id="e512c-172">U kunt een tekenreeks, een bytematrix of een Javascript-object (gedeserialiseerd naar JSON) in Node.js, toewijzen aan `context.binding.<paramName>`.</span><span class="sxs-lookup"><span data-stu-id="e512c-172">In Node.js, you can assign a string, a byte array, or a Javascript object (deserialized into JSON) to `context.binding.<paramName>`.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="e512c-173">Voorbeeld van uitvoer</span><span class="sxs-lookup"><span data-stu-id="e512c-173">Output sample</span></span>
<span data-ttu-id="e512c-174">Stel dat u hebt de volgende function.json die een Service Bus-wachtrij-uitvoer definieert:</span><span class="sxs-lookup"><span data-stu-id="e512c-174">Suppose you have the following function.json, that defines a Service Bus queue output:</span></span>

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

<span data-ttu-id="e512c-175">Zie de taalspecifieke-voorbeeldtoepassing die u een bericht naar de service bus-wachtrij verzendt.</span><span class="sxs-lookup"><span data-stu-id="e512c-175">See the language-specific sample that sends a message to the service bus queue.</span></span>

* [<span data-ttu-id="e512c-176">C#</span><span class="sxs-lookup"><span data-stu-id="e512c-176">C#</span></span>](#outcsharp)
* [<span data-ttu-id="e512c-177">F#</span><span class="sxs-lookup"><span data-stu-id="e512c-177">F#</span></span>](#outfsharp)
* [<span data-ttu-id="e512c-178">Node.js</span><span class="sxs-lookup"><span data-stu-id="e512c-178">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="e512c-179">Voorbeeld van uitvoer in C#</span><span class="sxs-lookup"><span data-stu-id="e512c-179">Output sample in C#</span></span> #

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, out string outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue = message;
}
```

<span data-ttu-id="e512c-180">Of om meerdere berichten te maken:</span><span class="sxs-lookup"><span data-stu-id="e512c-180">Or, to create multiple messages:</span></span>

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

### <a name="output-sample-in-f"></a><span data-ttu-id="e512c-181">Voorbeeld van uitvoer in F #</span><span class="sxs-lookup"><span data-stu-id="e512c-181">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter, outputSbQueue: byref<string>) =
    let message = sprintf "Service Bus queue message created at: %s" (DateTime.Now.ToString())
    log.Info(message)
    outputSbQueue = message
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="e512c-182">Voorbeeld van uitvoer in Node.js</span><span class="sxs-lookup"><span data-stu-id="e512c-182">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = message;
    context.done();
};
```

<span data-ttu-id="e512c-183">Of om meerdere berichten te maken:</span><span class="sxs-lookup"><span data-stu-id="e512c-183">Or, to create multiple messages:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e512c-184">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e512c-184">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

