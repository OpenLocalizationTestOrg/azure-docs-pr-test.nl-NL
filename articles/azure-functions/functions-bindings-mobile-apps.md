---
title: Bindingen voor aaaAzure functies Mobile Apps | Microsoft Docs
description: Begrijpen hoe Azure Mobile Apps-bindingen toouse in Azure Functions.
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
keywords: Azure functions, functies, verwerking van gebeurtenissen, dynamische compute zonder server architectuur
ms.assetid: faad1263-0fa5-41a9-964f-aecbc0be706a
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/31/2016
ms.author: glenga
ms.openlocfilehash: d3679a5d5c66705b32e422ec17e3a1e6d6ac063c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-mobile-apps-bindings"></a><span data-ttu-id="77172-104">Azure Functions Mobile Apps-bindingen</span><span class="sxs-lookup"><span data-stu-id="77172-104">Azure Functions Mobile Apps bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="77172-105">Dit artikel wordt uitgelegd hoe tooconfigure en code [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) bindingen in de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="77172-105">This article explains how tooconfigure and code [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) bindings in Azure Functions.</span></span> <span data-ttu-id="77172-106">Azure Functions ondersteunt invoer en uitvoer van de bindingen voor mobiele Apps.</span><span class="sxs-lookup"><span data-stu-id="77172-106">Azure Functions supports input and output bindings for Mobile Apps.</span></span>

<span data-ttu-id="77172-107">Hallo Mobile Apps-invoer en uitvoer bindingen kunnen u [lezen uit en schrijven toodata tabellen](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) in uw mobiele app.</span><span class="sxs-lookup"><span data-stu-id="77172-107">hello Mobile Apps input and output bindings let you [read from and write toodata tables](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) in your mobile app.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="mobile-apps-input-binding"></a><span data-ttu-id="77172-108">Invoer Mobile Apps-binding</span><span class="sxs-lookup"><span data-stu-id="77172-108">Mobile Apps input binding</span></span>
<span data-ttu-id="77172-109">Hallo invoer Mobile Apps-binding wordt een record geladen uit een eindpunt van de mobiele en geeft deze door aan uw functie.</span><span class="sxs-lookup"><span data-stu-id="77172-109">hello Mobile Apps input binding loads a record from a mobile table endpoint and passes it into your function.</span></span> <span data-ttu-id="77172-110">In een C# en F # functies, worden eventuele wijzigingen toohello record automatisch back toohello tabel verzonden wanneer het Hallo-functie is afgesloten.</span><span class="sxs-lookup"><span data-stu-id="77172-110">In a C# and F# functions, any changes made toohello record are automatically sent back toohello table when hello function exits successfully.</span></span>

<span data-ttu-id="77172-111">Hallo Mobile Apps invoer tooa functie maakt gebruik van volgende JSON-object in Hallo Hallo `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="77172-111">hello Mobile Apps input tooa function uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "id" : "<Id of hello record tooretrieve - see below>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "in"
}
```

<span data-ttu-id="77172-112">Let op Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="77172-112">Note hello following:</span></span>

* <span data-ttu-id="77172-113">`id`kan niet statisch of het kan zijn gebaseerd op Hallo-trigger die Hallo-functie roept.</span><span class="sxs-lookup"><span data-stu-id="77172-113">`id` can be static, or it can be based on hello trigger that invokes hello function.</span></span> <span data-ttu-id="77172-114">Als u bijvoorbeeld een [wachtrij trigger]() voor de functie vervolgens `"id": "{queueTrigger}"` gebruikt Hallo string-waarde van de wachtrij het Hallo-bericht als Hallo record ID tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="77172-114">For example, if you use a [queue trigger]() for your function, then `"id": "{queueTrigger}"` uses hello string value of hello queue message as hello record ID tooretrieve.</span></span>
* <span data-ttu-id="77172-115">`connection`Hallo-naam van een appinstelling in de functie-app die op zijn beurt Hallo-URL van uw mobiele app bevat moet worden bevatten.</span><span class="sxs-lookup"><span data-stu-id="77172-115">`connection` should contain hello name of an app setting in your function app, which in turn contains hello URL of your mobile app.</span></span> <span data-ttu-id="77172-116">Hallo-functie maakt gebruik van deze URL tooconstruct Hallo vereist REST-bewerkingen op uw mobiele app.</span><span class="sxs-lookup"><span data-stu-id="77172-116">hello function uses this URL tooconstruct hello required REST operations against your mobile app.</span></span> <span data-ttu-id="77172-117">U [maken van een app-instelling in uw app functie]() die URL van uw mobiele app bevat (ziet eruit als `http://<appname>.azurewebsites.net`), vervolgens Hallo-naam van Hallo app-instelling opgeven in Hallo `connection` eigenschap in de binding van uw invoer.</span><span class="sxs-lookup"><span data-stu-id="77172-117">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify hello name of hello app setting in hello `connection` property in your input binding.</span></span> 
* <span data-ttu-id="77172-118">U moet toospecify `apiKey` als u [implementeren van een API-sleutel in uw back-end voor Node.js mobiele app](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), of [implementeren van een API-sleutel in uw back-end .NET mobiele app](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span><span class="sxs-lookup"><span data-stu-id="77172-118">You need toospecify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="77172-119">toodo dit u [maken van een app-instelling in uw app functie]() dat Hallo API-sleutel bevat, voegt u Hallo `apiKey` eigenschap in uw invoer binding met de naam van de app-instelling Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="77172-119">toodo this, you [create an app setting in your function app]() that contains hello API key, then add hello `apiKey` property in your input binding with hello name of hello app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="77172-120">Deze API-sleutel moet niet worden gedeeld met uw mobiele app-clients.</span><span class="sxs-lookup"><span data-stu-id="77172-120">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="77172-121">Dit moet gedistribueerde veilig tooservice-side '-clients, zoals Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="77172-121">It should only be distributed securely tooservice-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="77172-122">Azure Functions slaat uw verbindingsgegevens en API-sleutels als de app-instellingen zodat ze niet zijn ingeschakeld in uw resourcebeheerbibliotheek.</span><span class="sxs-lookup"><span data-stu-id="77172-122">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="77172-123">Dit beschermt uw vertrouwelijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="77172-123">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="77172-124">Invoer-gebruik</span><span class="sxs-lookup"><span data-stu-id="77172-124">Input usage</span></span>
<span data-ttu-id="77172-125">Deze sectie leest u hoe toouse uw Mobile Apps invoer binding in uw functiecode.</span><span class="sxs-lookup"><span data-stu-id="77172-125">This section shows you how toouse your Mobile Apps input binding in your function code.</span></span> 

<span data-ttu-id="77172-126">Hallo-record met Hallo opgegeven tabel en record-ID is gevonden, wordt doorgegeven in met de naam Hallo [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parameter (of in Node.js, is deze Hallo doorgegeven `context.bindings.<name>` object).</span><span class="sxs-lookup"><span data-stu-id="77172-126">When hello record with hello specified table and record ID is found, it is passed into hello named [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parameter (or, in Node.js, it is passed into hello `context.bindings.<name>` object).</span></span> <span data-ttu-id="77172-127">Wanneer Hallo-record niet gevonden is, is het Hallo-parameter `null`.</span><span class="sxs-lookup"><span data-stu-id="77172-127">When hello record is not found, hello parameter is `null`.</span></span> 

<span data-ttu-id="77172-128">In C# en F # functies, wijzigingen die u aanbrengt toohello invoer-record (invoerparameter) automatisch verzonden back toohello Mobile Apps-tabel wanneer Hallo-functie met succes wordt afgesloten.</span><span class="sxs-lookup"><span data-stu-id="77172-128">In C# and F# functions, any changes you make toohello input record (input parameter) is automatically sent back toohello Mobile Apps table when hello function exits successfully.</span></span> <span data-ttu-id="77172-129">Gebruik in Node.js-functies, `context.bindings.<name>` tooaccess Hallo invoerrecord.</span><span class="sxs-lookup"><span data-stu-id="77172-129">In Node.js functions, use `context.bindings.<name>` tooaccess hello input record.</span></span> <span data-ttu-id="77172-130">U kunt een record in Node.js niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="77172-130">You cannot modify a record in Node.js.</span></span>

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="77172-131">Voorbeeld van invoer</span><span class="sxs-lookup"><span data-stu-id="77172-131">Input sample</span></span>
<span data-ttu-id="77172-132">Stel dat u hebt na function.json hello, haalt die een record in de tabel mobiele App met Hallo Hallo-bericht van wachtrij trigger-id:</span><span class="sxs-lookup"><span data-stu-id="77172-132">Suppose you have hello following function.json, that retrieves a Mobile App table record with hello id of hello queue trigger message:</span></span>

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
        "name": "record",
        "type": "mobileTable",
        "tableName": "MyTable",
        "id" : "{queueTrigger}",
        "connection": "My_MobileApp_Url",
        "apiKey": "My_MobileApp_Key",
        "direction": "in"
    }
],
"disabled": false
}
```

<span data-ttu-id="77172-133">Zie Hallo taalspecifieke voorbeeld dat gebruikmaakt van de invoerrecord Hallo Hallo binding.</span><span class="sxs-lookup"><span data-stu-id="77172-133">See hello language-specific sample that uses hello input record from hello binding.</span></span> <span data-ttu-id="77172-134">Voorbeelden van C# en F # Hallo Hallo-record ook wijzigen `text` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="77172-134">hello C# and F# samples also modify hello record's `text` property.</span></span>

* [<span data-ttu-id="77172-135">C#</span><span class="sxs-lookup"><span data-stu-id="77172-135">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="77172-136">Node.js</span><span class="sxs-lookup"><span data-stu-id="77172-136">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="77172-137">Invoer voorbeeld in C#</span><span class="sxs-lookup"><span data-stu-id="77172-137">Input sample in C#</span></span> #

```cs
#r "Newtonsoft.Json"    
using Newtonsoft.Json.Linq;

public static void Run(string myQueueItem, JObject record)
{
    if (record != null)
    {
        record["Text"] = "This has changed.";
    }    
}
```

<!--
<a name="inputfsharp"></a>
### Input sample in F# ## 

```fsharp
#r "Newtonsoft.Json"    
open Newtonsoft.Json.Linq
let Run(myQueueItem: string, record: JObject) =
  inputDocument?text <- "This has changed."
```
-->

<a name="inputnodejs"></a>

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="77172-138">Invoer voorbeeld in Node.js</span><span class="sxs-lookup"><span data-stu-id="77172-138">Input sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {    
    context.log(context.bindings.record);
    context.done();
};
```

<a name="output"></a>

## <a name="mobile-apps-output-binding"></a><span data-ttu-id="77172-139">Mobile Apps uitvoer binding</span><span class="sxs-lookup"><span data-stu-id="77172-139">Mobile Apps output binding</span></span>
<span data-ttu-id="77172-140">Hallo Mobile Apps uitvoer binding toowrite een nieuw record tooa Mobile Apps tabel eindpunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="77172-140">Use hello Mobile Apps output binding toowrite a new record tooa Mobile Apps table endpoint.</span></span>  

<span data-ttu-id="77172-141">Hallo Mobile Apps uitvoer voor een functie maakt gebruik van volgende JSON-object in Hallo Hallo `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="77172-141">hello Mobile Apps output for a function uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of output parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "out"
}
```

<span data-ttu-id="77172-142">Let op Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="77172-142">Note hello following:</span></span>

* <span data-ttu-id="77172-143">`connection`Hallo-naam van een appinstelling in de functie-app die op zijn beurt Hallo-URL van uw mobiele app bevat moet worden bevatten.</span><span class="sxs-lookup"><span data-stu-id="77172-143">`connection` should contain hello name of an app setting in your function app, which in turn contains hello URL of your mobile app.</span></span> <span data-ttu-id="77172-144">Hallo-functie maakt gebruik van deze URL tooconstruct Hallo vereist REST-bewerkingen op uw mobiele app.</span><span class="sxs-lookup"><span data-stu-id="77172-144">hello function uses this URL tooconstruct hello required REST operations against your mobile app.</span></span> <span data-ttu-id="77172-145">U [maken van een app-instelling in uw app functie]() die URL van uw mobiele app bevat (ziet eruit als `http://<appname>.azurewebsites.net`), vervolgens Hallo-naam van Hallo app-instelling opgeven in Hallo `connection` eigenschap in de binding van uw invoer.</span><span class="sxs-lookup"><span data-stu-id="77172-145">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify hello name of hello app setting in hello `connection` property in your input binding.</span></span> 
* <span data-ttu-id="77172-146">U moet toospecify `apiKey` als u [implementeren van een API-sleutel in uw back-end voor Node.js mobiele app](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), of [implementeren van een API-sleutel in uw back-end .NET mobiele app](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span><span class="sxs-lookup"><span data-stu-id="77172-146">You need toospecify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="77172-147">toodo dit u [maken van een app-instelling in uw app functie]() dat Hallo API-sleutel bevat, voegt u Hallo `apiKey` eigenschap in uw invoer binding met de naam van de app-instelling Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="77172-147">toodo this, you [create an app setting in your function app]() that contains hello API key, then add hello `apiKey` property in your input binding with hello name of hello app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="77172-148">Deze API-sleutel moet niet worden gedeeld met uw mobiele app-clients.</span><span class="sxs-lookup"><span data-stu-id="77172-148">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="77172-149">Dit moet gedistribueerde veilig tooservice-side '-clients, zoals Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="77172-149">It should only be distributed securely tooservice-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="77172-150">Azure Functions slaat uw verbindingsgegevens en API-sleutels als de app-instellingen zodat ze niet zijn ingeschakeld in uw resourcebeheerbibliotheek.</span><span class="sxs-lookup"><span data-stu-id="77172-150">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="77172-151">Dit beschermt uw vertrouwelijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="77172-151">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="77172-152">Gebruik voor uitvoer</span><span class="sxs-lookup"><span data-stu-id="77172-152">Output usage</span></span>
<span data-ttu-id="77172-153">Deze sectie leest u hoe toouse uw mobiele Apps uitvoeren in uw functiecode binding.</span><span class="sxs-lookup"><span data-stu-id="77172-153">This section shows you how toouse your Mobile Apps output binding in your function code.</span></span> 

<span data-ttu-id="77172-154">Gebruik in C# functies, een benoemde output-parameter van het type `out object` tooaccess Hallo uitvoer record.</span><span class="sxs-lookup"><span data-stu-id="77172-154">In C# functions, use a named output parameter of type `out object` tooaccess hello output record.</span></span> <span data-ttu-id="77172-155">Gebruik in Node.js-functies, `context.bindings.<name>` tooaccess Hallo uitvoer record.</span><span class="sxs-lookup"><span data-stu-id="77172-155">In Node.js functions, use `context.bindings.<name>` tooaccess hello output record.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="77172-156">Voorbeeld van uitvoer</span><span class="sxs-lookup"><span data-stu-id="77172-156">Output sample</span></span>
<span data-ttu-id="77172-157">Stel dat u hebt Hallo function.json die de trigger van een wachtrij en de uitvoer van een mobiele Apps definieert te volgen:</span><span class="sxs-lookup"><span data-stu-id="77172-157">Suppose you have hello following function.json, that defines a queue trigger and a Mobile Apps output:</span></span>

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
    "name": "record",
    "type": "mobileTable",
    "tableName": "MyTable",
    "connection": "My_MobileApp_Url",
    "apiKey": "My_MobileApp_Key",
    "direction": "out"
    }
],
"disabled": false
}
```

<span data-ttu-id="77172-158">Zie Hallo taalspecifieke voorbeeldtoepassing die u een record in Hallo Mobile Apps-eindpunt voor table met Hallo inhoud van de wachtrij het Hallo-bericht maakt.</span><span class="sxs-lookup"><span data-stu-id="77172-158">See hello language-specific sample that creates a record in hello Mobile Apps table endpoint with hello content of hello queue message.</span></span>

* [<span data-ttu-id="77172-159">C#</span><span class="sxs-lookup"><span data-stu-id="77172-159">C#</span></span>](#outcsharp)
* [<span data-ttu-id="77172-160">Node.js</span><span class="sxs-lookup"><span data-stu-id="77172-160">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="77172-161">Voorbeeld van uitvoer in C#</span><span class="sxs-lookup"><span data-stu-id="77172-161">Output sample in C#</span></span> #

```cs
public static void Run(string myQueueItem, out object record)
{
    record = new {
        Text = $"I'm running in a C# function! {myQueueItem}"
    };
}
```

<!--
<a name="outfsharp"></a>
### Output sample in F# ## 
```fsharp

```
-->
<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="77172-162">Voorbeeld van uitvoer in Node.js</span><span class="sxs-lookup"><span data-stu-id="77172-162">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {

    context.bindings.record = {
        text : "I'm running in a Node function! Data: '" + myQueueItem + "'"
    }   

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="77172-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="77172-163">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

