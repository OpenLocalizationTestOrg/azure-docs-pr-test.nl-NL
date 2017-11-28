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
# <a name="azure-functions-service-bus-bindings"></a><span data-ttu-id="11ee9-104">Azure Functions Service Bus-bindingen</span><span class="sxs-lookup"><span data-stu-id="11ee9-104">Azure Functions Service Bus bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="11ee9-105">Dit artikel wordt uitgelegd hoe tooconfigure en werken met Azure Service Bus-bindingen in de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="11ee9-105">This article explains how tooconfigure and work with Azure Service Bus bindings in Azure Functions.</span></span> 

<span data-ttu-id="11ee9-106">Azure Functions ondersteunt activeren en uitvoer van de bindingen voor Service Bus-wachtrijen en onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="11ee9-106">Azure Functions supports trigger and output bindings for Service Bus queues and topics.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="trigger"></a>

## <a name="service-bus-trigger"></a><span data-ttu-id="11ee9-107">Service Bus-trigger</span><span class="sxs-lookup"><span data-stu-id="11ee9-107">Service Bus trigger</span></span>
<span data-ttu-id="11ee9-108">Gebruik Hallo Service Bus trigger toorespond toomessages van een Service Bus-wachtrij of onderwerp.</span><span class="sxs-lookup"><span data-stu-id="11ee9-108">Use hello Service Bus trigger toorespond toomessages from a Service Bus queue or topic.</span></span> 

<span data-ttu-id="11ee9-109">Hallo zijn Service Bus-wachtrij en onderwerp triggers gedefinieerd door de volgende JSON-objecten in Hallo Hallo `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="11ee9-109">hello Service Bus queue and topic triggers are defined by hello following JSON objects in hello `bindings` array of function.json:</span></span>

* <span data-ttu-id="11ee9-110">*wachtrij* trigger:</span><span class="sxs-lookup"><span data-stu-id="11ee9-110">*queue* trigger:</span></span>

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

* <span data-ttu-id="11ee9-111">*onderwerp* trigger:</span><span class="sxs-lookup"><span data-stu-id="11ee9-111">*topic* trigger:</span></span>

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

<span data-ttu-id="11ee9-112">Let op Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="11ee9-112">Note hello following:</span></span>

* <span data-ttu-id="11ee9-113">Voor `connection`, [maken van een app-instelling in uw app functie](functions-how-to-use-azure-function-app-settings.md) die Hallo connection string tooyour Service Bus-naamruimte bevat, geeft u vervolgens Hallo-naam van de app-instelling Hallo in Hallo `connection` eigenschap in de trigger.</span><span class="sxs-lookup"><span data-stu-id="11ee9-113">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains hello connection string tooyour Service Bus namespace, then specify hello name of hello app setting in hello `connection` property in your trigger.</span></span> <span data-ttu-id="11ee9-114">Voor het verkrijgen van de verbindingsreeks Hallo Hallo stappen die wordt weergegeven op [Beheerreferenties hello](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span><span class="sxs-lookup"><span data-stu-id="11ee9-114">You obtain hello connection string by following hello steps shown at [Obtain hello management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="11ee9-115">Hallo-verbindingsreeks moet voor een Service Bus-naamruimte, niet beperkt tooa specifieke wachtrij of onderwerp.</span><span class="sxs-lookup"><span data-stu-id="11ee9-115">hello connection string must be for a Service Bus namespace, not limited tooa specific queue or topic.</span></span>
  <span data-ttu-id="11ee9-116">Als u niets `connection` leeg is, Hallo trigger wordt ervan uitgegaan dat er een standaard Service Bus-verbindingsreeks is opgegeven in een app instelling met de naam `AzureWebJobsServiceBus`.</span><span class="sxs-lookup"><span data-stu-id="11ee9-116">If you leave `connection` empty, hello trigger assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="11ee9-117">Voor `accessRights`, beschikbare waarden zijn `manage` en `listen`.</span><span class="sxs-lookup"><span data-stu-id="11ee9-117">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="11ee9-118">Hallo standaardwaarde is `manage`, wat aangeeft dat Hallo `connection` heeft Hallo **beheren** machtiging.</span><span class="sxs-lookup"><span data-stu-id="11ee9-118">hello default is `manage`, which indicates that hello `connection` has hello **Manage** permission.</span></span> <span data-ttu-id="11ee9-119">Als u een verbindingsreeks die geen Hallo **beheren** , machtigingenset `accessRights` te`listen`.</span><span class="sxs-lookup"><span data-stu-id="11ee9-119">If you use a connection string that does not have hello **Manage** permission, set `accessRights` too`listen`.</span></span> <span data-ttu-id="11ee9-120">Anders beheren Hallo functies runtime mislukken tijdens toodo bewerkingen uit waarbij rechten.</span><span class="sxs-lookup"><span data-stu-id="11ee9-120">Otherwise, hello Functions runtime might fail trying toodo operations that require manage rights.</span></span>

## <a name="trigger-behavior"></a><span data-ttu-id="11ee9-121">Gedrag van de trigger</span><span class="sxs-lookup"><span data-stu-id="11ee9-121">Trigger behavior</span></span>
* <span data-ttu-id="11ee9-122">**Single-threading** - standaard Hallo functies runtime-processen die meerdere tegelijkertijd berichten.</span><span class="sxs-lookup"><span data-stu-id="11ee9-122">**Single-threading** - By default, hello Functions runtime processes multiple messages concurrently.</span></span> <span data-ttu-id="11ee9-123">toodirect hello runtime tooprocess slechts één wachtrij of onderwerp bericht op een tijdstip ingesteld `serviceBus.maxConcurrentCalls` too1 in *host.json*.</span><span class="sxs-lookup"><span data-stu-id="11ee9-123">toodirect hello runtime tooprocess only a single queue or topic message at a time, set `serviceBus.maxConcurrentCalls` too1 in *host.json*.</span></span> 
  <span data-ttu-id="11ee9-124">Voor informatie over *host.json*, Zie [mapstructuur](functions-reference.md#folder-structure) en [host.json](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="11ee9-124">For information about *host.json*, see [Folder Structure](functions-reference.md#folder-structure) and [host.json](https://github .com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>
* <span data-ttu-id="11ee9-125">**Verwerking van gevaarlijke berichten** -Service Bus biedt een eigen verwerken van verontreinigde berichten die niet kan worden beheerd of geconfigureerd in de configuratie van Azure Functions of code.</span><span class="sxs-lookup"><span data-stu-id="11ee9-125">**Poison message handling** - Service Bus does its own poison message handling, which can't be controlled or configured in Azure Functions configuration or code.</span></span> 
* <span data-ttu-id="11ee9-126">**PeekLock gedrag** -runtime van Functions Hallo ontvangt een bericht in [ `PeekLock` modus](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) en aanroepen `Complete` op het Hallo-bericht als Hallo-functie wordt voltooid of aanroepen `Abandon` als hello de functie is mislukt.</span><span class="sxs-lookup"><span data-stu-id="11ee9-126">**PeekLock behavior** - hello Functions runtime receives a message in [`PeekLock` mode](../service-bus-messaging/service-bus-performance-improvements.md#receive-mode) and calls `Complete` on hello message if hello function finishes successfully, or calls `Abandon` if hello function fails.</span></span> 
  <span data-ttu-id="11ee9-127">Als het Hallo-functie wordt uitgevoerd langer dan Hallo `PeekLock` time-out Hallo vergrendeling automatisch wordt vernieuwd.</span><span class="sxs-lookup"><span data-stu-id="11ee9-127">If hello function runs longer than hello `PeekLock` timeout, hello lock is automatically renewed.</span></span>

<a name="triggerusage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="11ee9-128">Gebruik van de trigger</span><span class="sxs-lookup"><span data-stu-id="11ee9-128">Trigger usage</span></span>
<span data-ttu-id="11ee9-129">Deze sectie leest u hoe toouse uw Service Bus activeren in uw functiecode.</span><span class="sxs-lookup"><span data-stu-id="11ee9-129">This section shows you how toouse your Service Bus trigger in your function code.</span></span> 

<span data-ttu-id="11ee9-130">In C# en F # kan Hallo-bericht van Service Bus trigger gedeserialiseerde tooany Hallo invoertypen volgende zijn:</span><span class="sxs-lookup"><span data-stu-id="11ee9-130">In C# and F#, hello Service Bus trigger message can be deserialized tooany of hello following input types:</span></span>

* <span data-ttu-id="11ee9-131">`string`-nuttig voor string-berichten</span><span class="sxs-lookup"><span data-stu-id="11ee9-131">`string` - useful for string messages</span></span>
* <span data-ttu-id="11ee9-132">`byte[]`-handig voor binaire gegevens</span><span class="sxs-lookup"><span data-stu-id="11ee9-132">`byte[]` - useful for binary data</span></span>
* <span data-ttu-id="11ee9-133">Alle [Object](https://msdn.microsoft.com/library/system.object.aspx) - handig voor gegevens JSON-geserialiseerd.</span><span class="sxs-lookup"><span data-stu-id="11ee9-133">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - useful for JSON-serialized data.</span></span>
  <span data-ttu-id="11ee9-134">Als u een aangepaste invoertype zoals declareren `CustomType`, Azure Functions probeert toodeserialize Hallo JSON-gegevens in het opgegeven type.</span><span class="sxs-lookup"><span data-stu-id="11ee9-134">If you declare a custom input type, such as `CustomType`, Azure Functions tries toodeserialize hello JSON data into your specified type.</span></span>
* <span data-ttu-id="11ee9-135">`BrokeredMessage`-biedt u Hallo-bericht met Hallo gedeserialiseerd [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) methode.</span><span class="sxs-lookup"><span data-stu-id="11ee9-135">`BrokeredMessage` - gives you hello deserialized message with hello [BrokeredMessage.GetBody<T>()](https://msdn.microsoft.com/library/hh144211.aspx) method.</span></span>

<span data-ttu-id="11ee9-136">Hallo-bericht van Service Bus trigger wordt in Node.js, in de functie Hallo als een tekenreeks- of JSON-object doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="11ee9-136">In Node.js, hello Service Bus trigger message is passed into hello function as either a string or JSON object.</span></span>

<a name="triggersample"></a>

## <a name="trigger-sample"></a><span data-ttu-id="11ee9-137">Voorbeeld van de trigger</span><span class="sxs-lookup"><span data-stu-id="11ee9-137">Trigger sample</span></span>
<span data-ttu-id="11ee9-138">Stel dat u hebt Hallo function.json te volgen:</span><span class="sxs-lookup"><span data-stu-id="11ee9-138">Suppose you have hello following function.json:</span></span>

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

<span data-ttu-id="11ee9-139">Zie Hallo taalspecifieke steekproef die een Service Bus-wachtrijbericht verwerkt.</span><span class="sxs-lookup"><span data-stu-id="11ee9-139">See hello language-specific sample that processes a Service Bus queue message.</span></span>

* [<span data-ttu-id="11ee9-140">C#</span><span class="sxs-lookup"><span data-stu-id="11ee9-140">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="11ee9-141">F#</span><span class="sxs-lookup"><span data-stu-id="11ee9-141">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="11ee9-142">Node.js</span><span class="sxs-lookup"><span data-stu-id="11ee9-142">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="11ee9-143">Voorbeeld van de trigger in C#</span><span class="sxs-lookup"><span data-stu-id="11ee9-143">Trigger sample in C#</span></span> #

```cs
public static void Run(string myQueueItem, TraceWriter log)
{
    log.Info($"C# ServiceBus queue trigger function processed message: {myQueueItem}");
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a><span data-ttu-id="11ee9-144">Voorbeeld van de trigger in F #</span><span class="sxs-lookup"><span data-stu-id="11ee9-144">Trigger sample in F#</span></span> #

```fsharp
let Run(myQueueItem: string, log: TraceWriter) =
    log.Info(sprintf "F# ServiceBus queue trigger function processed message: %s" myQueueItem)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="11ee9-145">Voorbeeld van de trigger in Node.js</span><span class="sxs-lookup"><span data-stu-id="11ee9-145">Trigger sample in Node.js</span></span>

```javascript
module.exports = function(context, myQueueItem) {
    context.log('Node.js ServiceBus queue trigger function processed message', myQueueItem);
    context.done();
};
```

<a name="output"></a>

## <a name="service-bus-output-binding"></a><span data-ttu-id="11ee9-146">Service Bus uitvoer binding</span><span class="sxs-lookup"><span data-stu-id="11ee9-146">Service Bus output binding</span></span>
<span data-ttu-id="11ee9-147">Hallo Service Bus-wachtrij en onderwerp uitvoer voor een functie gebruiken Hallo volgende JSON-objecten in Hallo `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="11ee9-147">hello Service Bus queue and topic output for a function use hello following JSON objects in hello `bindings` array of function.json:</span></span>

* <span data-ttu-id="11ee9-148">*wachtrij* uitvoer:</span><span class="sxs-lookup"><span data-stu-id="11ee9-148">*queue* output:</span></span>

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
* <span data-ttu-id="11ee9-149">*onderwerp* uitvoer:</span><span class="sxs-lookup"><span data-stu-id="11ee9-149">*topic* output:</span></span>

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

<span data-ttu-id="11ee9-150">Let op Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="11ee9-150">Note hello following:</span></span>

* <span data-ttu-id="11ee9-151">Voor `connection`, [maken van een app-instelling in uw app functie](functions-how-to-use-azure-function-app-settings.md) die Hallo connection string tooyour Service Bus-naamruimte bevat, geeft u vervolgens Hallo-naam van de app-instelling Hallo in Hallo `connection` eigenschap in de uitvoer binding.</span><span class="sxs-lookup"><span data-stu-id="11ee9-151">For `connection`, [create an app setting in your function app](functions-how-to-use-azure-function-app-settings.md) that contains hello connection string tooyour Service Bus namespace, then specify hello name of hello app setting in hello `connection` property in your output binding.</span></span> <span data-ttu-id="11ee9-152">Voor het verkrijgen van de verbindingsreeks Hallo Hallo stappen die wordt weergegeven op [Beheerreferenties hello](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span><span class="sxs-lookup"><span data-stu-id="11ee9-152">You obtain hello connection string by following hello steps shown at [Obtain hello management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md#obtain-the-management-credentials).</span></span>
  <span data-ttu-id="11ee9-153">Hallo-verbindingsreeks moet voor een Service Bus-naamruimte, niet beperkt tooa specifieke wachtrij of onderwerp.</span><span class="sxs-lookup"><span data-stu-id="11ee9-153">hello connection string must be for a Service Bus namespace, not limited tooa specific queue or topic.</span></span>
  <span data-ttu-id="11ee9-154">Als u niets `connection` leeg is, hello uitvoer binding wordt ervan uitgegaan dat er een standaard Service Bus-verbindingsreeks is opgegeven in een app instelling met de naam `AzureWebJobsServiceBus`.</span><span class="sxs-lookup"><span data-stu-id="11ee9-154">If you leave `connection` empty, hello output binding assumes that a default Service Bus connection string is specified in an app setting named `AzureWebJobsServiceBus`.</span></span>
* <span data-ttu-id="11ee9-155">Voor `accessRights`, beschikbare waarden zijn `manage` en `listen`.</span><span class="sxs-lookup"><span data-stu-id="11ee9-155">For `accessRights`, available values are `manage` and `listen`.</span></span> <span data-ttu-id="11ee9-156">Hallo standaardwaarde is `manage`, wat aangeeft dat Hallo `connection` heeft Hallo **beheren** machtiging.</span><span class="sxs-lookup"><span data-stu-id="11ee9-156">hello default is `manage`, which indicates that hello `connection` has hello **Manage** permission.</span></span> <span data-ttu-id="11ee9-157">Als u een verbindingsreeks die geen Hallo **beheren** , machtigingenset `accessRights` te`listen`.</span><span class="sxs-lookup"><span data-stu-id="11ee9-157">If you use a connection string that does not have hello **Manage** permission, set `accessRights` too`listen`.</span></span> <span data-ttu-id="11ee9-158">Anders beheren Hallo functies runtime mislukken tijdens toodo bewerkingen uit waarbij rechten.</span><span class="sxs-lookup"><span data-stu-id="11ee9-158">Otherwise, hello Functions runtime might fail trying toodo operations that require manage rights.</span></span>

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="11ee9-159">Gebruik voor uitvoer</span><span class="sxs-lookup"><span data-stu-id="11ee9-159">Output usage</span></span>
<span data-ttu-id="11ee9-160">Azure Functions kunt het bericht van een Service Bus-wachtrij maken uit een van de volgende typen Hallo in C# en F #:</span><span class="sxs-lookup"><span data-stu-id="11ee9-160">In C# and F#, Azure Functions can create a Service Bus queue message from any of hello following types:</span></span>

* <span data-ttu-id="11ee9-161">Alle [Object](https://msdn.microsoft.com/library/system.object.aspx) -parameterdefinitie ziet eruit als `out T paramName` (C#).</span><span class="sxs-lookup"><span data-stu-id="11ee9-161">Any [Object](https://msdn.microsoft.com/library/system.object.aspx) - Parameter definition looks like `out T paramName` (C#).</span></span>
  <span data-ttu-id="11ee9-162">Functies deserializes Hallo-object in een JSON-bericht.</span><span class="sxs-lookup"><span data-stu-id="11ee9-162">Functions deserializes hello object into a JSON message.</span></span> <span data-ttu-id="11ee9-163">Als bij het verlaten van de functie Hallo Hallo uitvoerwaarde null is, maakt functies Hallo-bericht met een null-object.</span><span class="sxs-lookup"><span data-stu-id="11ee9-163">If hello output value is null when hello function exits, Functions creates hello message with a null object.</span></span>
* <span data-ttu-id="11ee9-164">`string`-Parameterdefinitie ziet eruit als `out string paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="11ee9-164">`string` - Parameter definition looks like `out string paraName` (C#).</span></span> <span data-ttu-id="11ee9-165">Als het Hallo-parameterwaarde is niet-null wanneer het Hallo-functie wordt afgesloten, wordt een bericht door functies gemaakt.</span><span class="sxs-lookup"><span data-stu-id="11ee9-165">If hello parameter value is non-null when hello function exits, Functions creates a message.</span></span>
* <span data-ttu-id="11ee9-166">`byte[]`-Parameterdefinitie ziet eruit als `out byte[] paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="11ee9-166">`byte[]` - Parameter definition looks like `out byte[] paraName` (C#).</span></span> <span data-ttu-id="11ee9-167">Als het Hallo-parameterwaarde is niet-null wanneer het Hallo-functie wordt afgesloten, wordt een bericht door functies gemaakt.</span><span class="sxs-lookup"><span data-stu-id="11ee9-167">If hello parameter value is non-null when hello function exits, Functions creates a message.</span></span>
* <span data-ttu-id="11ee9-168">`BrokeredMessage`Parameterdefinitie ziet eruit als `out BrokeredMessage paraName` (C#).</span><span class="sxs-lookup"><span data-stu-id="11ee9-168">`BrokeredMessage` Parameter definition looks like `out BrokeredMessage paraName` (C#).</span></span> <span data-ttu-id="11ee9-169">Als het Hallo-parameterwaarde is niet-null wanneer het Hallo-functie wordt afgesloten, wordt een bericht door functies gemaakt.</span><span class="sxs-lookup"><span data-stu-id="11ee9-169">If hello parameter value is non-null when hello function exits, Functions creates a message.</span></span>

<span data-ttu-id="11ee9-170">U kunt gebruiken voor het maken van meerdere berichten in een C#-functie, `ICollector<T>` of `IAsyncCollector<T>`.</span><span class="sxs-lookup"><span data-stu-id="11ee9-170">For creating multiple messages in a C# function, you can use `ICollector<T>` or `IAsyncCollector<T>`.</span></span> <span data-ttu-id="11ee9-171">Een bericht wordt gemaakt bij het aanroepen van Hallo `Add` methode.</span><span class="sxs-lookup"><span data-stu-id="11ee9-171">A message is created when you call hello `Add` method.</span></span>

<span data-ttu-id="11ee9-172">In Node.js, kunt u een tekenreeks, een bytematrix of een Javascript-object (gedeserialiseerd naar JSON) te toewijzen`context.binding.<paramName>`.</span><span class="sxs-lookup"><span data-stu-id="11ee9-172">In Node.js, you can assign a string, a byte array, or a Javascript object (deserialized into JSON) too`context.binding.<paramName>`.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="11ee9-173">Voorbeeld van uitvoer</span><span class="sxs-lookup"><span data-stu-id="11ee9-173">Output sample</span></span>
<span data-ttu-id="11ee9-174">Stel dat u hebt Hallo function.json die een Service Bus-wachtrij-uitvoer definieert te volgen:</span><span class="sxs-lookup"><span data-stu-id="11ee9-174">Suppose you have hello following function.json, that defines a Service Bus queue output:</span></span>

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

<span data-ttu-id="11ee9-175">Zie Hallo taalspecifieke voorbeeldtoepassing die u een bericht toohello service bus-wachtrij verzendt.</span><span class="sxs-lookup"><span data-stu-id="11ee9-175">See hello language-specific sample that sends a message toohello service bus queue.</span></span>

* [<span data-ttu-id="11ee9-176">C#</span><span class="sxs-lookup"><span data-stu-id="11ee9-176">C#</span></span>](#outcsharp)
* [<span data-ttu-id="11ee9-177">F#</span><span class="sxs-lookup"><span data-stu-id="11ee9-177">F#</span></span>](#outfsharp)
* [<span data-ttu-id="11ee9-178">Node.js</span><span class="sxs-lookup"><span data-stu-id="11ee9-178">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="11ee9-179">Voorbeeld van uitvoer in C#</span><span class="sxs-lookup"><span data-stu-id="11ee9-179">Output sample in C#</span></span> #

```cs
public static void Run(TimerInfo myTimer, TraceWriter log, out string outputSbQueue)
{
    string message = $"Service Bus queue message created at: {DateTime.Now}";
    log.Info(message); 
    outputSbQueue = message;
}
```

<span data-ttu-id="11ee9-180">Of toocreate meerdere berichten:</span><span class="sxs-lookup"><span data-stu-id="11ee9-180">Or, toocreate multiple messages:</span></span>

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

### <a name="output-sample-in-f"></a><span data-ttu-id="11ee9-181">Voorbeeld van uitvoer in F #</span><span class="sxs-lookup"><span data-stu-id="11ee9-181">Output sample in F#</span></span> #

```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter, outputSbQueue: byref<string>) =
    let message = sprintf "Service Bus queue message created at: %s" (DateTime.Now.ToString())
    log.Info(message)
    outputSbQueue = message
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="11ee9-182">Voorbeeld van uitvoer in Node.js</span><span class="sxs-lookup"><span data-stu-id="11ee9-182">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myTimer) {
    var message = 'Service Bus queue message created at ' + timeStamp;
    context.log(message);   
    context.bindings.outputSbQueueMsg = message;
    context.done();
};
```

<span data-ttu-id="11ee9-183">Of toocreate meerdere berichten:</span><span class="sxs-lookup"><span data-stu-id="11ee9-183">Or, toocreate multiple messages:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="11ee9-184">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="11ee9-184">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

