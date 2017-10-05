---
title: Azure Functions Mobile Apps-bindingen | Microsoft Docs
description: Het gebruik van de bindingen van Azure Mobile Apps in Azure Functions begrijpen.
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
ms.openlocfilehash: c5e1c02984f9773b263c0bee7685c7d5ff62e658
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-mobile-apps-bindings"></a><span data-ttu-id="387b0-104">Azure Functions Mobile Apps-bindingen</span><span class="sxs-lookup"><span data-stu-id="387b0-104">Azure Functions Mobile Apps bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="387b0-105">Dit artikel wordt uitgelegd hoe u kunt configureren en code [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) bindingen in de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="387b0-105">This article explains how to configure and code [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) bindings in Azure Functions.</span></span> <span data-ttu-id="387b0-106">Azure Functions ondersteunt invoer en uitvoer van de bindingen voor mobiele Apps.</span><span class="sxs-lookup"><span data-stu-id="387b0-106">Azure Functions supports input and output bindings for Mobile Apps.</span></span>

<span data-ttu-id="387b0-107">De Mobile Apps-invoer en uitvoer bindingen kunnen u [lezen van en schrijven naar gegevenstabellen](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) in uw mobiele app.</span><span class="sxs-lookup"><span data-stu-id="387b0-107">The Mobile Apps input and output bindings let you [read from and write to data tables](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) in your mobile app.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="mobile-apps-input-binding"></a><span data-ttu-id="387b0-108">Invoer Mobile Apps-binding</span><span class="sxs-lookup"><span data-stu-id="387b0-108">Mobile Apps input binding</span></span>
<span data-ttu-id="387b0-109">De invoer Mobile Apps-binding wordt een record van een eindpunt van de mobiele geladen en geeft deze door aan uw functie.</span><span class="sxs-lookup"><span data-stu-id="387b0-109">The Mobile Apps input binding loads a record from a mobile table endpoint and passes it into your function.</span></span> <span data-ttu-id="387b0-110">In een C# en F # functies, worden wijzigingen in de record automatisch verzonden terug naar de tabel wanneer de functie is afgesloten.</span><span class="sxs-lookup"><span data-stu-id="387b0-110">In a C# and F# functions, any changes made to the record are automatically sent back to the table when the function exits successfully.</span></span>

<span data-ttu-id="387b0-111">De Mobile Apps-invoer voor een functie maakt gebruik van de volgende JSON-object in de `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="387b0-111">The Mobile Apps input to a function uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "id" : "<Id of the record to retrieve - see below>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "in"
}
```

<span data-ttu-id="387b0-112">Houd rekening met het volgende:</span><span class="sxs-lookup"><span data-stu-id="387b0-112">Note the following:</span></span>

* <span data-ttu-id="387b0-113">`id`kan niet statisch of het kan zijn gebaseerd op de trigger die de functie activeert.</span><span class="sxs-lookup"><span data-stu-id="387b0-113">`id` can be static, or it can be based on the trigger that invokes the function.</span></span> <span data-ttu-id="387b0-114">Als u bijvoorbeeld een [wachtrij trigger]() voor de functie vervolgens `"id": "{queueTrigger}"` de tekenreekswaarde van het bericht uit de wachtrij als de record-ID gebruikt om op te halen.</span><span class="sxs-lookup"><span data-stu-id="387b0-114">For example, if you use a [queue trigger]() for your function, then `"id": "{queueTrigger}"` uses the string value of the queue message as the record ID to retrieve.</span></span>
* <span data-ttu-id="387b0-115">`connection`moet de naam van een appinstelling in de functie-app die op zijn beurt de URL van uw mobiele app bevat bevatten.</span><span class="sxs-lookup"><span data-stu-id="387b0-115">`connection` should contain the name of an app setting in your function app, which in turn contains the URL of your mobile app.</span></span> <span data-ttu-id="387b0-116">De functie gebruikt deze URL om de REST-bewerkingen op basis van uw mobiele app samen te stellen.</span><span class="sxs-lookup"><span data-stu-id="387b0-116">The function uses this URL to construct the required REST operations against your mobile app.</span></span> <span data-ttu-id="387b0-117">U [maken van een app-instelling in uw app functie]() die URL van uw mobiele app bevat (ziet eruit als `http://<appname>.azurewebsites.net`), geeft u de naam van de app-instelling in de `connection` eigenschap in de binding van uw invoer.</span><span class="sxs-lookup"><span data-stu-id="387b0-117">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify the name of the app setting in the `connection` property in your input binding.</span></span> 
* <span data-ttu-id="387b0-118">U moet opgeven `apiKey` als u [implementeren van een API-sleutel in uw back-end voor Node.js mobiele app](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), of [implementeren van een API-sleutel in uw back-end .NET mobiele app](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span><span class="sxs-lookup"><span data-stu-id="387b0-118">You need to specify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="387b0-119">Hiervoor u [maken van een app-instelling in uw app functie]() die de API-sleutel bevat, voegt u de `apiKey` eigenschap in uw invoer binding met de naam van de app-instelling.</span><span class="sxs-lookup"><span data-stu-id="387b0-119">To do this, you [create an app setting in your function app]() that contains the API key, then add the `apiKey` property in your input binding with the name of the app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="387b0-120">Deze API-sleutel moet niet worden gedeeld met uw mobiele app-clients.</span><span class="sxs-lookup"><span data-stu-id="387b0-120">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="387b0-121">Deze moet alleen worden gedistribueerd veilig aan servicezijde clients, zoals Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="387b0-121">It should only be distributed securely to service-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="387b0-122">Azure Functions slaat uw verbindingsgegevens en API-sleutels als de app-instellingen zodat ze niet zijn ingeschakeld in uw resourcebeheerbibliotheek.</span><span class="sxs-lookup"><span data-stu-id="387b0-122">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="387b0-123">Dit beschermt uw vertrouwelijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="387b0-123">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="387b0-124">Invoer-gebruik</span><span class="sxs-lookup"><span data-stu-id="387b0-124">Input usage</span></span>
<span data-ttu-id="387b0-125">Deze sectie wordt beschreven hoe u uw invoer binding Mobile Apps in uw functiecode.</span><span class="sxs-lookup"><span data-stu-id="387b0-125">This section shows you how to use your Mobile Apps input binding in your function code.</span></span> 

<span data-ttu-id="387b0-126">Wanneer de record met de opgegeven tabel en de record-ID is gevonden, wordt doorgegeven in de benoemde [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parameter (of in Node.js, doorgegeven aan de `context.bindings.<name>` object).</span><span class="sxs-lookup"><span data-stu-id="387b0-126">When the record with the specified table and record ID is found, it is passed into the named [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parameter (or, in Node.js, it is passed into the `context.bindings.<name>` object).</span></span> <span data-ttu-id="387b0-127">Wanneer de record niet gevonden is, wordt de parameter is `null`.</span><span class="sxs-lookup"><span data-stu-id="387b0-127">When the record is not found, the parameter is `null`.</span></span> 

<span data-ttu-id="387b0-128">In C# en F # functies en wijzigingen die u aanbrengt op invoer van de record (invoerparameter) automatisch terug naar de tabel Mobile Apps wordt verzonden wanneer de functie is afgesloten.</span><span class="sxs-lookup"><span data-stu-id="387b0-128">In C# and F# functions, any changes you make to the input record (input parameter) is automatically sent back to the Mobile Apps table when the function exits successfully.</span></span> <span data-ttu-id="387b0-129">Gebruik in Node.js-functies, `context.bindings.<name>` voor toegang tot de invoerrecord.</span><span class="sxs-lookup"><span data-stu-id="387b0-129">In Node.js functions, use `context.bindings.<name>` to access the input record.</span></span> <span data-ttu-id="387b0-130">U kunt een record in Node.js niet wijzigen.</span><span class="sxs-lookup"><span data-stu-id="387b0-130">You cannot modify a record in Node.js.</span></span>

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="387b0-131">Voorbeeld van invoer</span><span class="sxs-lookup"><span data-stu-id="387b0-131">Input sample</span></span>
<span data-ttu-id="387b0-132">Stel dat u hebt de volgende function.json die een record van de mobiele App tabel met de id van het bericht uit de wachtrij trigger ophaalt:</span><span class="sxs-lookup"><span data-stu-id="387b0-132">Suppose you have the following function.json, that retrieves a Mobile App table record with the id of the queue trigger message:</span></span>

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

<span data-ttu-id="387b0-133">Zie het voorbeeld taalspecifieke die gebruikmaakt van de invoerrecord van de binding.</span><span class="sxs-lookup"><span data-stu-id="387b0-133">See the language-specific sample that uses the input record from the binding.</span></span> <span data-ttu-id="387b0-134">De C# en F # voorbeelden te wijzigen van de record `text` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="387b0-134">The C# and F# samples also modify the record's `text` property.</span></span>

* [<span data-ttu-id="387b0-135">C#</span><span class="sxs-lookup"><span data-stu-id="387b0-135">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="387b0-136">Node.js</span><span class="sxs-lookup"><span data-stu-id="387b0-136">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="387b0-137">Invoer voorbeeld in C#</span><span class="sxs-lookup"><span data-stu-id="387b0-137">Input sample in C#</span></span> #

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

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="387b0-138">Invoer voorbeeld in Node.js</span><span class="sxs-lookup"><span data-stu-id="387b0-138">Input sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {    
    context.log(context.bindings.record);
    context.done();
};
```

<a name="output"></a>

## <a name="mobile-apps-output-binding"></a><span data-ttu-id="387b0-139">Mobile Apps uitvoer binding</span><span class="sxs-lookup"><span data-stu-id="387b0-139">Mobile Apps output binding</span></span>
<span data-ttu-id="387b0-140">De Mobile Apps-uitvoer binden aan een nieuwe record schrijven naar een eindpunt van de Mobile Apps gebruiken.</span><span class="sxs-lookup"><span data-stu-id="387b0-140">Use the Mobile Apps output binding to write a new record to a Mobile Apps table endpoint.</span></span>  

<span data-ttu-id="387b0-141">De Mobile Apps uitvoer voor een functie maakt gebruik van de volgende JSON-object in de `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="387b0-141">The Mobile Apps output for a function uses the following JSON object in the `bindings` array of function.json:</span></span>

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

<span data-ttu-id="387b0-142">Houd rekening met het volgende:</span><span class="sxs-lookup"><span data-stu-id="387b0-142">Note the following:</span></span>

* <span data-ttu-id="387b0-143">`connection`moet de naam van een appinstelling in de functie-app die op zijn beurt de URL van uw mobiele app bevat bevatten.</span><span class="sxs-lookup"><span data-stu-id="387b0-143">`connection` should contain the name of an app setting in your function app, which in turn contains the URL of your mobile app.</span></span> <span data-ttu-id="387b0-144">De functie gebruikt deze URL om de REST-bewerkingen op basis van uw mobiele app samen te stellen.</span><span class="sxs-lookup"><span data-stu-id="387b0-144">The function uses this URL to construct the required REST operations against your mobile app.</span></span> <span data-ttu-id="387b0-145">U [maken van een app-instelling in uw app functie]() die URL van uw mobiele app bevat (ziet eruit als `http://<appname>.azurewebsites.net`), geeft u de naam van de app-instelling in de `connection` eigenschap in de binding van uw invoer.</span><span class="sxs-lookup"><span data-stu-id="387b0-145">You [create an app setting in your function app]() that contains your mobile app's URL (which looks like `http://<appname>.azurewebsites.net`), then specify the name of the app setting in the `connection` property in your input binding.</span></span> 
* <span data-ttu-id="387b0-146">U moet opgeven `apiKey` als u [implementeren van een API-sleutel in uw back-end voor Node.js mobiele app](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), of [implementeren van een API-sleutel in uw back-end .NET mobiele app](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span><span class="sxs-lookup"><span data-stu-id="387b0-146">You need to specify `apiKey` if you [implement an API key in your Node.js mobile app backend](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), or [implement an API key in your .NET mobile app backend](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key).</span></span> <span data-ttu-id="387b0-147">Hiervoor u [maken van een app-instelling in uw app functie]() die de API-sleutel bevat, voegt u de `apiKey` eigenschap in uw invoer binding met de naam van de app-instelling.</span><span class="sxs-lookup"><span data-stu-id="387b0-147">To do this, you [create an app setting in your function app]() that contains the API key, then add the `apiKey` property in your input binding with the name of the app setting.</span></span> 
  
  > [!IMPORTANT]
  > <span data-ttu-id="387b0-148">Deze API-sleutel moet niet worden gedeeld met uw mobiele app-clients.</span><span class="sxs-lookup"><span data-stu-id="387b0-148">This API key must not be shared with your mobile app clients.</span></span> <span data-ttu-id="387b0-149">Deze moet alleen worden gedistribueerd veilig aan servicezijde clients, zoals Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="387b0-149">It should only be distributed securely to service-side clients, like Azure Functions.</span></span> 
  > 
  > [!NOTE]
  > <span data-ttu-id="387b0-150">Azure Functions slaat uw verbindingsgegevens en API-sleutels als de app-instellingen zodat ze niet zijn ingeschakeld in uw resourcebeheerbibliotheek.</span><span class="sxs-lookup"><span data-stu-id="387b0-150">Azure Functions stores your connection information and API keys as app settings so that they are not checked into your source control repository.</span></span> <span data-ttu-id="387b0-151">Dit beschermt uw vertrouwelijke gegevens.</span><span class="sxs-lookup"><span data-stu-id="387b0-151">This safeguards your sensitive information.</span></span>
  > 
  > 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="387b0-152">Gebruik voor uitvoer</span><span class="sxs-lookup"><span data-stu-id="387b0-152">Output usage</span></span>
<span data-ttu-id="387b0-153">Deze sectie wordt beschreven hoe u de binding in uw functiecode Mobile Apps-uitvoer.</span><span class="sxs-lookup"><span data-stu-id="387b0-153">This section shows you how to use your Mobile Apps output binding in your function code.</span></span> 

<span data-ttu-id="387b0-154">Gebruik in C# functies, een benoemde output-parameter van het type `out object` de uitvoer-record te openen.</span><span class="sxs-lookup"><span data-stu-id="387b0-154">In C# functions, use a named output parameter of type `out object` to access the output record.</span></span> <span data-ttu-id="387b0-155">Gebruik in Node.js-functies, `context.bindings.<name>` de uitvoer-record te openen.</span><span class="sxs-lookup"><span data-stu-id="387b0-155">In Node.js functions, use `context.bindings.<name>` to access the output record.</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="387b0-156">Voorbeeld van uitvoer</span><span class="sxs-lookup"><span data-stu-id="387b0-156">Output sample</span></span>
<span data-ttu-id="387b0-157">Stel dat u hebt de volgende function.json die de trigger van een wachtrij en de uitvoer van een Mobile Apps definieert:</span><span class="sxs-lookup"><span data-stu-id="387b0-157">Suppose you have the following function.json, that defines a queue trigger and a Mobile Apps output:</span></span>

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

<span data-ttu-id="387b0-158">Zie de taalspecifieke-voorbeeldtoepassing die u een record in het eindpunt van de tabel Mobile Apps met de inhoud van het bericht uit de wachtrij maakt.</span><span class="sxs-lookup"><span data-stu-id="387b0-158">See the language-specific sample that creates a record in the Mobile Apps table endpoint with the content of the queue message.</span></span>

* [<span data-ttu-id="387b0-159">C#</span><span class="sxs-lookup"><span data-stu-id="387b0-159">C#</span></span>](#outcsharp)
* [<span data-ttu-id="387b0-160">Node.js</span><span class="sxs-lookup"><span data-stu-id="387b0-160">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="387b0-161">Voorbeeld van uitvoer in C#</span><span class="sxs-lookup"><span data-stu-id="387b0-161">Output sample in C#</span></span> #

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

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="387b0-162">Voorbeeld van uitvoer in Node.js</span><span class="sxs-lookup"><span data-stu-id="387b0-162">Output sample in Node.js</span></span>

```javascript
module.exports = function (context, myQueueItem) {

    context.bindings.record = {
        text : "I'm running in a Node function! Data: '" + myQueueItem + "'"
    }   

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="387b0-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="387b0-163">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

