---
title: aaaJavaScript referentie voor ontwikkelaars voor Azure Functions | Microsoft Docs
description: Begrijpen hoe toodevelop functioneert met behulp van JavaScript.
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: Azure-functies, functies, gebeurtenisverwerking, webhooks, dynamisch berekenen, architectuur zonder server
ms.assetid: 45dedd78-3ff9-411f-bb4b-16d29a11384c
ms.service: functions
ms.devlang: nodejs
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: 6220b42f965b6ee2463341aaf270836623fdf7fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-javascript-developer-guide"></a><span data-ttu-id="96913-104">Azure Functions JavaScript-handleiding voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="96913-104">Azure Functions JavaScript developer guide</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="96913-105">C#-script</span><span class="sxs-lookup"><span data-stu-id="96913-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="96913-106">F # script</span><span class="sxs-lookup"><span data-stu-id="96913-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="96913-107">JavaScript</span><span class="sxs-lookup"><span data-stu-id="96913-107">JavaScript</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="96913-108">Hallo JavaScript-ervaring voor Azure Functions het eenvoudig tooexport een functie die wordt doorgegeven maakt als een `context` voor communicatie met de Hallo runtime en voor het ontvangen en verzenden van gegevens via bindingen-object.</span><span class="sxs-lookup"><span data-stu-id="96913-108">hello JavaScript experience for Azure Functions makes it easy tooexport a function, which is passed as a `context` object for communicating with hello runtime and for receiving and sending data via bindings.</span></span>

<span data-ttu-id="96913-109">In dit artikel wordt ervan uitgegaan dat u hebt al Hallo gelezen [naslaginformatie voor ontwikkelaars van Azure Functions](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="96913-109">This article assumes that you've already read hello [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="exporting-a-function"></a><span data-ttu-id="96913-110">Exporteren van een functie</span><span class="sxs-lookup"><span data-stu-id="96913-110">Exporting a function</span></span>
<span data-ttu-id="96913-111">Alle JavaScript-functies moeten één exporteren `function` via `module.exports` voor Hallo runtime toofind functie Hallo en voer deze uit.</span><span class="sxs-lookup"><span data-stu-id="96913-111">All JavaScript functions must export a single `function` via `module.exports` for hello runtime toofind hello function and run it.</span></span> <span data-ttu-id="96913-112">Deze functie moet altijd bevatten een `context` object.</span><span class="sxs-lookup"><span data-stu-id="96913-112">This function must always include a `context` object.</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // Additional inputs can be accessed by hello arguments property
    if(arguments.length === 4) {
        context.log('This function has 4 inputs');
    }
};
// or you can include additional inputs in your arguments
module.exports = function(context, myTrigger, myInput, myOtherInput) {
    // function logic goes here :)
};
```

<span data-ttu-id="96913-113">Bindingen van `direction === "in"` worden doorgegeven als argument, wat betekent dat u kunt gebruiken [ `arguments` ](https://msdn.microsoft.com/library/87dw3w1k.aspx) toodynamically afhandelen van nieuwe invoer (bijvoorbeeld met behulp van `arguments.length` tooiterate via de ingevoerde gegevens).</span><span class="sxs-lookup"><span data-stu-id="96913-113">Bindings of `direction === "in"` are passed along as function arguments, which means that you can use [`arguments`](https://msdn.microsoft.com/library/87dw3w1k.aspx) toodynamically handle new inputs (for example, by using `arguments.length` tooiterate over all your inputs).</span></span> <span data-ttu-id="96913-114">Deze functie is handig wanneer u alleen een trigger en er zijn geen extra invoergegevens omdat u voorspelbare toegang uw triggergegevens zonder die verwijzen naar tot uw `context` object.</span><span class="sxs-lookup"><span data-stu-id="96913-114">This functionality is convenient when you have only a trigger and no additional inputs, because you can predictably access your trigger data without referencing your `context` object.</span></span>

<span data-ttu-id="96913-115">Hallo argumenten worden altijd doorgegeven toohello-functie in Hallo volgorde waarin ze voorkomen in *function.json*, zelfs als u ze niet in de uitvoer-instructie opgeven.</span><span class="sxs-lookup"><span data-stu-id="96913-115">hello arguments are always passed along toohello function in hello order in which they occur in *function.json*, even if you don't specify them in your exports statement.</span></span> <span data-ttu-id="96913-116">Als u hebt bijvoorbeeld `function(context, a, b)` en deze te wijzigen`function(context, a)`, u kunt nog steeds Hallo-waarde van `b` in functiecode door ernaar te verwijzen`arguments[3]`.</span><span class="sxs-lookup"><span data-stu-id="96913-116">For example, if you have `function(context, a, b)` and change it too`function(context, a)`, you can still get hello value of `b` in function code by referring too`arguments[3]`.</span></span>

<span data-ttu-id="96913-117">Alle bindingen, ongeacht de richting, ook op Hallo doorgegeven `context` object (Zie het volgende script Hallo).</span><span class="sxs-lookup"><span data-stu-id="96913-117">All bindings, regardless of direction, are also passed along on hello `context` object (see hello following script).</span></span> 

## <a name="context-object"></a><span data-ttu-id="96913-118">context-object</span><span class="sxs-lookup"><span data-stu-id="96913-118">context object</span></span>
<span data-ttu-id="96913-119">Hallo runtime gebruikt een `context` object toopass gegevens tooand van uw functie en toolet u contact met de Hallo-runtime opnemen.</span><span class="sxs-lookup"><span data-stu-id="96913-119">hello runtime uses a `context` object toopass data tooand from your function and toolet you communicate with hello runtime.</span></span>

<span data-ttu-id="96913-120">Hallo context-object is altijd Hallo eerste parameter tooa functie en moet worden opgenomen omdat deze methoden, zoals `context.done` en `context.log`, die vereist toouse Hallo runtime correct zijn.</span><span class="sxs-lookup"><span data-stu-id="96913-120">hello context object is always hello first parameter tooa function and must be included because it has methods such as `context.done` and `context.log`, which are required toouse hello runtime correctly.</span></span> <span data-ttu-id="96913-121">U kunt een naam Hallo object wat u wilt dat (bijvoorbeeld `ctx` of `c`).</span><span class="sxs-lookup"><span data-stu-id="96913-121">You can name hello object whatever you would like (for example, `ctx` or `c`).</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // function logic goes here :)
};
```

### <a name="contextbindings-property"></a><span data-ttu-id="96913-122">de eigenschap context.bindings</span><span class="sxs-lookup"><span data-stu-id="96913-122">context.bindings property</span></span>

```
context.bindings
```
<span data-ttu-id="96913-123">Retourneert een benoemde object dat al uw invoer en uitvoer gegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="96913-123">Returns a named object that contains all your input and output data.</span></span> <span data-ttu-id="96913-124">Bijvoorbeeld, Hallo na de bindingsdefinitie in uw *function.json* hebt u toegang tot inhoud van de wachtrij Hallo van Hallo Hallo `context.bindings.myInput` object.</span><span class="sxs-lookup"><span data-stu-id="96913-124">For example, hello following binding definition in your *function.json* lets you access hello contents of hello queue from hello `context.bindings.myInput` object.</span></span> 

```json
{
    "type":"queue",
    "direction":"in",
    "name":"myInput"
    ...
}
```

```javascript
// myInput contains hello input data, which may have properties such as "name"
var author = context.bindings.myInput.name;
// Similarly, you can set your output data
context.bindings.myOutput = { 
        some_text: 'hello world', 
        a_number: 1 };
```

### <a name="contextdone-method"></a><span data-ttu-id="96913-125">context.Done methode</span><span class="sxs-lookup"><span data-stu-id="96913-125">context.done method</span></span>
```
context.done([err],[propertyBag])
```

<span data-ttu-id="96913-126">Informeert Hallo runtime die uw code is voltooid.</span><span class="sxs-lookup"><span data-stu-id="96913-126">Informs hello runtime that your code has finished.</span></span> <span data-ttu-id="96913-127">U moet aanroepen `context.done`, of anders Hallo runtime nooit weet dat de functie voltooid is en Hallo-uitvoering wordt time-out.</span><span class="sxs-lookup"><span data-stu-id="96913-127">You must call `context.done`, or else hello runtime never knows that your function is complete, and hello execution will time out.</span></span> 

<span data-ttu-id="96913-128">Hallo `context.done` methode kunt u toopass back- zowel een eigenschappenverzameling van eigenschappen die Hallo-eigenschappen op hallo overschreven als een gebruiker gedefinieerde fout toohello runtime `context.bindings` object.</span><span class="sxs-lookup"><span data-stu-id="96913-128">hello `context.done` method allows you toopass back both a user-defined error toohello runtime and a property bag of properties that overwrite hello properties on hello `context.bindings` object.</span></span>

```javascript
// Even though we set myOutput toohave:
//  -> text: hello world, number: 123
context.bindings.myOutput = { text: 'hello world', number: 123 };
// If we pass an object toohello done function...
context.done(null, { myOutput: { text: 'hello there, world', noNumber: true }});
// hello done method will overwrite hello myOutput binding toobe: 
//  -> text: hello there, world, noNumber: true
```

### <a name="contextlog-method"></a><span data-ttu-id="96913-129">context.log methode</span><span class="sxs-lookup"><span data-stu-id="96913-129">context.log method</span></span>  

```
context.log(message)
```
<span data-ttu-id="96913-130">Hiermee kunt u toowrite toohello console streaminglogboeken op Hallo trace standaardniveau.</span><span class="sxs-lookup"><span data-stu-id="96913-130">Allows you toowrite toohello streaming console logs at hello default trace level.</span></span> <span data-ttu-id="96913-131">Op `context.log`, extra logboekregistratie methoden zijn beschikbaar waarmee u toohello consolelogboek op andere traceringsniveaus schrijven:</span><span class="sxs-lookup"><span data-stu-id="96913-131">On `context.log`, additional logging methods are available that let you write toohello console log at other trace levels:</span></span>


| <span data-ttu-id="96913-132">Methode</span><span class="sxs-lookup"><span data-stu-id="96913-132">Method</span></span>                 | <span data-ttu-id="96913-133">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="96913-133">Description</span></span>                                |
| ---------------------- | ------------------------------------------ |
| <span data-ttu-id="96913-134">**fout (_bericht_)**</span><span class="sxs-lookup"><span data-stu-id="96913-134">**error(_message_)**</span></span>   | <span data-ttu-id="96913-135">Schrijft tooerror niveau registreren of lager.</span><span class="sxs-lookup"><span data-stu-id="96913-135">Writes tooerror level logging, or lower.</span></span>   |
| <span data-ttu-id="96913-136">**waarschuwen (_bericht_)**</span><span class="sxs-lookup"><span data-stu-id="96913-136">**warn(_message_)**</span></span>    | <span data-ttu-id="96913-137">Schrijft toowarning niveau registreren of lager.</span><span class="sxs-lookup"><span data-stu-id="96913-137">Writes toowarning level logging, or lower.</span></span> |
| <span data-ttu-id="96913-138">**Info (_bericht_)**</span><span class="sxs-lookup"><span data-stu-id="96913-138">**info(_message_)**</span></span>    | <span data-ttu-id="96913-139">Schrijft tooinfo niveau registreren of lager.</span><span class="sxs-lookup"><span data-stu-id="96913-139">Writes tooinfo level logging, or lower.</span></span>    |
| <span data-ttu-id="96913-140">**uitgebreide (_bericht_)**</span><span class="sxs-lookup"><span data-stu-id="96913-140">**verbose(_message_)**</span></span> | <span data-ttu-id="96913-141">Logboekregistratie op tooverbose schrijft.</span><span class="sxs-lookup"><span data-stu-id="96913-141">Writes tooverbose level logging.</span></span>           |

<span data-ttu-id="96913-142">Hallo volgende voorbeeld wordt geschreven toohello-console op Hallo waarschuwing Traceerniveau:</span><span class="sxs-lookup"><span data-stu-id="96913-142">hello following example writes toohello console at hello warning trace level:</span></span>

```javascript
context.log.warn("Something has happened."); 
```
<span data-ttu-id="96913-143">U kunt Hallo traceerniveau drempelwaarde voor logboekregistratie in Hallo host.json bestand of deze uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="96913-143">You can set hello trace-level threshold for logging in hello host.json file, or turn it off.</span></span>  <span data-ttu-id="96913-144">Zie de volgende sectie Hallo voor meer informatie over hoe toowrite toohello registreert.</span><span class="sxs-lookup"><span data-stu-id="96913-144">For more information about how toowrite toohello logs, see hello next section.</span></span>

## <a name="binding-data-type"></a><span data-ttu-id="96913-145">Binding-gegevenstype</span><span class="sxs-lookup"><span data-stu-id="96913-145">Binding data type</span></span>

<span data-ttu-id="96913-146">toodefine Hallo Hallo gegevenstype voor een invoer-binding gebruiken `dataType` eigenschap in de definitie van de binding Hallo.</span><span class="sxs-lookup"><span data-stu-id="96913-146">toodefine hello data type for an input binding, use hello `dataType` property in hello binding definition.</span></span> <span data-ttu-id="96913-147">Bijvoorbeeld: tooread Hallo inhoud van een HTTP-aanvraag in binaire indeling, gebruik Hallo type `binary`:</span><span class="sxs-lookup"><span data-stu-id="96913-147">For example, tooread hello content of an HTTP request in binary format, use hello type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="96913-148">Andere opties voor `dataType` zijn `stream` en `string`.</span><span class="sxs-lookup"><span data-stu-id="96913-148">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="writing-trace-output-toohello-console"></a><span data-ttu-id="96913-149">Schrijven trace-uitvoer toohello console</span><span class="sxs-lookup"><span data-stu-id="96913-149">Writing trace output toohello console</span></span> 

<span data-ttu-id="96913-150">In de functies, gebruikt u Hallo `context.log` methoden toowrite trace-uitvoer toohello console.</span><span class="sxs-lookup"><span data-stu-id="96913-150">In Functions, you use hello `context.log` methods toowrite trace output toohello console.</span></span> <span data-ttu-id="96913-151">Op dit moment kunt u niet gebruiken `console.log` toowrite toohello-console.</span><span class="sxs-lookup"><span data-stu-id="96913-151">At this point, you cannot use `console.log` toowrite toohello console.</span></span>

<span data-ttu-id="96913-152">Als u aanroept `context.log()`, uw bericht geschreven toohello-console op Hallo default traceringsniveau, Hallo _info_ traceerniveau.</span><span class="sxs-lookup"><span data-stu-id="96913-152">When you call `context.log()`, your message is written toohello console at hello default trace level, which is hello _info_ trace level.</span></span> <span data-ttu-id="96913-153">Hallo schrijft volgende code toohello-console op Hallo info Traceerniveau:</span><span class="sxs-lookup"><span data-stu-id="96913-153">hello following code writes toohello console at hello info trace level:</span></span>

```javascript
context.log({hello: 'world'});  
```

<span data-ttu-id="96913-154">Hallo is voorafgaande code gelijkwaardig toohello code te volgen:</span><span class="sxs-lookup"><span data-stu-id="96913-154">hello preceding code is equivalent toohello following code:</span></span>

```javascript
context.log.info({hello: 'world'});  
```

<span data-ttu-id="96913-155">Hallo schrijft volgende code toohello-console op Hallo foutniveau:</span><span class="sxs-lookup"><span data-stu-id="96913-155">hello following code writes toohello console at hello error level:</span></span>

```javascript
context.log.error("An error has occurred.");  
```

<span data-ttu-id="96913-156">Omdat _fout_ Hallo hoogste trace niveau, deze tracering wordt geschreven toohello uitvoer op alle traceringsniveaus als logboekregistratie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="96913-156">Because _error_ is hello highest trace level, this trace is written toohello output at all trace levels as long as logging is enabled.</span></span>  


<span data-ttu-id="96913-157">Alle `context.log` methoden ondersteunen Hallo dezelfde indeling voor parameter die wordt ondersteund door Hallo Node.js [util.format methode](https://nodejs.org/api/util.html#util_util_format_format).</span><span class="sxs-lookup"><span data-stu-id="96913-157">All `context.log` methods support hello same parameter format that's supported by hello Node.js [util.format method](https://nodejs.org/api/util.html#util_util_format_format).</span></span> <span data-ttu-id="96913-158">Overweeg de volgende code waarmee toohello console schrijft door Hallo standaard traceerniveau Hallo:</span><span class="sxs-lookup"><span data-stu-id="96913-158">Consider hello following code, which writes toohello console by using hello default trace level:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=' + req.originalUrl);
context.log('Request Headers = ' + JSON.stringify(req.headers));
```

<span data-ttu-id="96913-159">U kunt ook schrijven Hallo dezelfde code in de volgende indeling Hallo:</span><span class="sxs-lookup"><span data-stu-id="96913-159">You can also write hello same code in hello following format:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);
context.log('Request Headers = ', JSON.stringify(req.headers));
```

### <a name="configure-hello-trace-level-for-console-logging"></a><span data-ttu-id="96913-160">Hallo traceerniveau voor console-logboekregistratie configureren</span><span class="sxs-lookup"><span data-stu-id="96913-160">Configure hello trace level for console logging</span></span>

<span data-ttu-id="96913-161">Functies kunt u definiëren Hallo traceerniveau van drempelwaarde voor het schrijven van toohello console dit maakt het eenvoudig toocontrol Hallo manier traceringen toohello console van uw functies worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="96913-161">Functions lets you define hello threshold trace level for writing toohello console, which makes it easy toocontrol hello way traces are written toohello console from your functions.</span></span> <span data-ttu-id="96913-162">tooset hello drempelwaarde voor alle traces gebruik Hallo-toohello console geschreven `tracing.consoleLevel` eigenschap in Hallo host.json bestand.</span><span class="sxs-lookup"><span data-stu-id="96913-162">tooset hello threshold for all traces written toohello console, use hello `tracing.consoleLevel` property in hello host.json file.</span></span> <span data-ttu-id="96913-163">Deze instelling geldt tooall functies in uw app in de functie.</span><span class="sxs-lookup"><span data-stu-id="96913-163">This setting applies tooall functions in your function app.</span></span> <span data-ttu-id="96913-164">Hallo wordt volgende voorbeeld Hallo trace drempelwaarde tooenable uitgebreide logboekregistratie:</span><span class="sxs-lookup"><span data-stu-id="96913-164">hello following example sets hello trace threshold tooenable verbose logging:</span></span>

```json
{ 
    "tracing": {      
        "consoleLevel": "verbose"     
    }
}  
```

<span data-ttu-id="96913-165">Waarden van **consoleLevel** toohello namen van Hallo overeenkomen `context.log` methoden.</span><span class="sxs-lookup"><span data-stu-id="96913-165">Values of **consoleLevel** correspond toohello names of hello `context.log` methods.</span></span> <span data-ttu-id="96913-166">toodisable alle traceerlogboekregistratie toohello console ingesteld **consoleLevel** too_off_.</span><span class="sxs-lookup"><span data-stu-id="96913-166">toodisable all trace logging toohello console, set **consoleLevel** too_off_.</span></span> <span data-ttu-id="96913-167">Zie voor meer informatie over Hallo host.json bestand Hallo [host.json naslagonderwerp](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="96913-167">For more information about hello host.json file, see hello [host.json reference topic](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>

## <a name="http-triggers-and-bindings"></a><span data-ttu-id="96913-168">HTTP-triggers en bindingen</span><span class="sxs-lookup"><span data-stu-id="96913-168">HTTP triggers and bindings</span></span>

<span data-ttu-id="96913-169">HTTP- en webhook triggers en HTTP-uitvoer bindingen aanvraag en antwoord objecten toorepresent Hallo HTTP messaging gebruiken.</span><span class="sxs-lookup"><span data-stu-id="96913-169">HTTP and webhook triggers and HTTP output bindings use request and response objects toorepresent hello HTTP messaging.</span></span>  

### <a name="request-object"></a><span data-ttu-id="96913-170">Request-object</span><span class="sxs-lookup"><span data-stu-id="96913-170">Request object</span></span>

<span data-ttu-id="96913-171">Hallo `request` object heeft Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="96913-171">hello `request` object has hello following properties:</span></span>

| <span data-ttu-id="96913-172">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="96913-172">Property</span></span>      | <span data-ttu-id="96913-173">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="96913-173">Description</span></span>                                                    |
| ------------- | -------------------------------------------------------------- |
| <span data-ttu-id="96913-174">_hoofdtekst_</span><span class="sxs-lookup"><span data-stu-id="96913-174">_body_</span></span>        | <span data-ttu-id="96913-175">Een object dat Hallo hoofdtekst van Hallo-aanvraag bevat.</span><span class="sxs-lookup"><span data-stu-id="96913-175">An object that contains hello body of hello request.</span></span>               |
| <span data-ttu-id="96913-176">_headers_</span><span class="sxs-lookup"><span data-stu-id="96913-176">_headers_</span></span>     | <span data-ttu-id="96913-177">Een object dat aanvraagheaders Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="96913-177">An object that contains hello request headers.</span></span>                   |
| <span data-ttu-id="96913-178">_methode_</span><span class="sxs-lookup"><span data-stu-id="96913-178">_method_</span></span>      | <span data-ttu-id="96913-179">Hallo HTTP-methode van Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="96913-179">hello HTTP method of hello request.</span></span>                                |
| <span data-ttu-id="96913-180">_originalUrl_</span><span class="sxs-lookup"><span data-stu-id="96913-180">_originalUrl_</span></span> | <span data-ttu-id="96913-181">Hallo-URL van Hallo-aanvraag.</span><span class="sxs-lookup"><span data-stu-id="96913-181">hello URL of hello request.</span></span>                                        |
| <span data-ttu-id="96913-182">_parameters voor_</span><span class="sxs-lookup"><span data-stu-id="96913-182">_params_</span></span>      | <span data-ttu-id="96913-183">Een object dat Hallo routering parameters van Hallo-aanvraag bevat.</span><span class="sxs-lookup"><span data-stu-id="96913-183">An object that contains hello routing parameters of hello request.</span></span> |
| <span data-ttu-id="96913-184">_query_</span><span class="sxs-lookup"><span data-stu-id="96913-184">_query_</span></span>       | <span data-ttu-id="96913-185">Een object dat de queryparameters Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="96913-185">An object that contains hello query parameters.</span></span>                  |
| <span data-ttu-id="96913-186">_rawBody_</span><span class="sxs-lookup"><span data-stu-id="96913-186">_rawBody_</span></span>     | <span data-ttu-id="96913-187">Hallo-hoofdtekst van het Hallo-bericht als een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="96913-187">hello body of hello message as a string.</span></span>                           |


### <a name="response-object"></a><span data-ttu-id="96913-188">Response-object</span><span class="sxs-lookup"><span data-stu-id="96913-188">Response object</span></span>

<span data-ttu-id="96913-189">Hallo `response` object heeft Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="96913-189">hello `response` object has hello following properties:</span></span>

| <span data-ttu-id="96913-190">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="96913-190">Property</span></span>  | <span data-ttu-id="96913-191">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="96913-191">Description</span></span>                                               |
| --------- | --------------------------------------------------------- |
| <span data-ttu-id="96913-192">_hoofdtekst_</span><span class="sxs-lookup"><span data-stu-id="96913-192">_body_</span></span>    | <span data-ttu-id="96913-193">Een object dat Hallo hoofdtekst van antwoord Hallo bevat.</span><span class="sxs-lookup"><span data-stu-id="96913-193">An object that contains hello body of hello response.</span></span>         |
| <span data-ttu-id="96913-194">_headers_</span><span class="sxs-lookup"><span data-stu-id="96913-194">_headers_</span></span> | <span data-ttu-id="96913-195">Een object dat Hallo antwoordheaders bevat.</span><span class="sxs-lookup"><span data-stu-id="96913-195">An object that contains hello response headers.</span></span>             |
| <span data-ttu-id="96913-196">_isRaw_</span><span class="sxs-lookup"><span data-stu-id="96913-196">_isRaw_</span></span>   | <span data-ttu-id="96913-197">Hiermee wordt aangegeven dat de opmaak wordt overgeslagen voor antwoord Hallo.</span><span class="sxs-lookup"><span data-stu-id="96913-197">Indicates that formatting is skipped for hello response.</span></span>    |
| <span data-ttu-id="96913-198">_status_</span><span class="sxs-lookup"><span data-stu-id="96913-198">_status_</span></span>  | <span data-ttu-id="96913-199">HTTP-statuscode van antwoord Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="96913-199">hello HTTP status code of hello response.</span></span>                     |

### <a name="accessing-hello-request-and-response"></a><span data-ttu-id="96913-200">Toegang tot Hallo-aanvraag en -antwoord</span><span class="sxs-lookup"><span data-stu-id="96913-200">Accessing hello request and response</span></span> 

<span data-ttu-id="96913-201">Wanneer u met HTTP-triggers werkt, kunt u Hallo HTTP-aanvraag en antwoord-objecten in een van drie manieren openen:</span><span class="sxs-lookup"><span data-stu-id="96913-201">When you work with HTTP triggers, you can access hello HTTP request and response objects in any of three ways:</span></span>

+ <span data-ttu-id="96913-202">Naam van Hallo invoer en uitvoer bindingen.</span><span class="sxs-lookup"><span data-stu-id="96913-202">From hello named input and output bindings.</span></span> <span data-ttu-id="96913-203">Op deze manier Hallo Hallo HTTP-trigger en bindingen werk dezelfde als elke andere binding.</span><span class="sxs-lookup"><span data-stu-id="96913-203">In this way, hello HTTP trigger and bindings work hello same as any other binding.</span></span> <span data-ttu-id="96913-204">Hallo volgende voorbeeld wordt ingesteld Hallo response-object met behulp van een benoemde `response` binding:</span><span class="sxs-lookup"><span data-stu-id="96913-204">hello following example sets hello response object by using a named `response` binding:</span></span> 

    ```javascript
    context.bindings.response = { status: 201, body: "Insert succeeded." };
    ```

+ <span data-ttu-id="96913-205">Van `req` en `res` eigenschappen op Hallo `context` object.</span><span class="sxs-lookup"><span data-stu-id="96913-205">From `req` and `res` properties on hello `context` object.</span></span> <span data-ttu-id="96913-206">Op deze manier kunt u Hallo conventionele patroon tooaccess HTTP-gegevens van Hallo context-object, in plaats van toouse Hallo volledige `context.bindings.name` patroon.</span><span class="sxs-lookup"><span data-stu-id="96913-206">In this way, you can use hello conventional pattern tooaccess HTTP data from hello context object, instead of having toouse hello full `context.bindings.name` pattern.</span></span> <span data-ttu-id="96913-207">Hallo volgende voorbeeld wordt getoond hoe tooaccess hello `req` en `res` objecten op Hallo `context`:</span><span class="sxs-lookup"><span data-stu-id="96913-207">hello following example shows how tooaccess hello `req` and `res` objects on hello `context`:</span></span>

    ```javascript
    // You can access your http request off hello context ...
    if(context.req.body.emoji === ':pizza:') context.log('Yay!');
    // and also set your http response
    context.res = { status: 202, body: 'You successfully ordered more coffee!' }; 
    ```

+ <span data-ttu-id="96913-208">Door het aanroepen van `context.done()`.</span><span class="sxs-lookup"><span data-stu-id="96913-208">By calling `context.done()`.</span></span> <span data-ttu-id="96913-209">Een speciaal soort HTTP-binding retourneert Hallo-antwoord dat wordt doorgegeven toohello `context.done()` methode.</span><span class="sxs-lookup"><span data-stu-id="96913-209">A special kind of HTTP binding returns hello response that is passed toohello `context.done()` method.</span></span> <span data-ttu-id="96913-210">Hallo HTTP na uitvoer binding definieert een `$return` uitvoerparameter:</span><span class="sxs-lookup"><span data-stu-id="96913-210">hello following HTTP output binding defines a `$return` output parameter:</span></span>

    ```json
    {
      "type": "http",
      "direction": "out",
      "name": "$return"
    }
    ``` 
    <span data-ttu-id="96913-211">Deze binding uitvoer verwacht u toosupply Hallo antwoord bij het aanroepen van `done()`, als volgt:</span><span class="sxs-lookup"><span data-stu-id="96913-211">This output binding expects you toosupply hello response when you call `done()`, as follows:</span></span>

    ```javascript
     // Define a valid response object.
    res = { status: 201, body: "Insert succeeded." };
    context.done(null, res);   
    ```  

## <a name="node-version-and-package-management"></a><span data-ttu-id="96913-212">Knooppunt-versie en Package Management</span><span class="sxs-lookup"><span data-stu-id="96913-212">Node version and Package Management</span></span>
<span data-ttu-id="96913-213">Hallo knooppunt versie is momenteel vergrendeld op `6.5.0`.</span><span class="sxs-lookup"><span data-stu-id="96913-213">hello node version is currently locked at `6.5.0`.</span></span> <span data-ttu-id="96913-214">We bent voor het onderzoeken van het toevoegen van ondersteuning voor meer versies en waardoor het worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="96913-214">We're investigating adding support for more versions and making it configurable.</span></span>

<span data-ttu-id="96913-215">Hallo stappen te volgen, kunt u pakketten opnemen in uw app in functie:</span><span class="sxs-lookup"><span data-stu-id="96913-215">hello following steps let you include packages in your function app:</span></span> 

1. <span data-ttu-id="96913-216">Ga te`https://<function_app_name>.scm.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="96913-216">Go too`https://<function_app_name>.scm.azurewebsites.net`.</span></span>

2. <span data-ttu-id="96913-217">Klik op **Console voor foutopsporing** > **CMD**.</span><span class="sxs-lookup"><span data-stu-id="96913-217">Click **Debug Console** > **CMD**.</span></span>

3. <span data-ttu-id="96913-218">Ga te`D:\home\site\wwwroot`, en sleep het bestand package.json toohello **wwwroot** map in de bovenste helft Hallo van Hallo-pagina.</span><span class="sxs-lookup"><span data-stu-id="96913-218">Go too`D:\home\site\wwwroot`, and then drag your package.json file toohello **wwwroot** folder at hello top half of hello page.</span></span>  
    <span data-ttu-id="96913-219">U kunt ook bestanden tooyour functie-app op andere manieren uploaden.</span><span class="sxs-lookup"><span data-stu-id="96913-219">You can upload files tooyour function app in other ways also.</span></span> <span data-ttu-id="96913-220">Zie voor meer informatie [hoe de app-bestanden voor het functioneren van tooupdate](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="96913-220">For more information, see [How tooupdate function app files](functions-reference.md#fileupdate).</span></span> 

4. <span data-ttu-id="96913-221">Nadat het Hallo package.json-bestand is geüpload, voert u Hallo `npm install` opdracht in Hallo **Kudu-console voor uitvoering op afstand**.</span><span class="sxs-lookup"><span data-stu-id="96913-221">After hello package.json file is uploaded, run hello `npm install` command in hello **Kudu remote execution console**.</span></span>  
    <span data-ttu-id="96913-222">Deze actie hello-pakketten die zijn aangegeven in Hallo package.json-bestand wordt gedownload en Hallo functie-app opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="96913-222">This action downloads hello packages indicated in hello package.json file and restarts hello function app.</span></span>

<span data-ttu-id="96913-223">Nadat hello pakketten die u moet zijn geïnstalleerd, u ze importeren tooyour functie door het aanroepen van `require('packagename')`, Hallo voorbeeld te volgen:</span><span class="sxs-lookup"><span data-stu-id="96913-223">After hello packages you need are installed, you import them tooyour function by calling `require('packagename')`, as in hello following example:</span></span>

```javascript
// Import hello underscore.js library
var _ = require('underscore');
var version = process.version; // version === 'v6.5.0'

module.exports = function(context) {
    // Using our imported underscore.js library
    var matched_names = _
        .where(context.bindings.myInput.names, {first: 'Carla'});
```

<span data-ttu-id="96913-224">U moet definiëren een `package.json` bestand in de hoofdmap Hallo van functie-app.</span><span class="sxs-lookup"><span data-stu-id="96913-224">You should define a `package.json` file at hello root of your function app.</span></span> <span data-ttu-id="96913-225">Definiërende Hallo-bestand laat alle functies in Hallo app share Hallo hetzelfde in de cache-pakketten, waardoor de beste prestaties Hallo.</span><span class="sxs-lookup"><span data-stu-id="96913-225">Defining hello file lets all functions in hello app share hello same cached packages, which gives hello best performance.</span></span> <span data-ttu-id="96913-226">Als een conflict ontstaat, u het kunt oplossen door toe te voegen een `package.json` bestand in map Hallo van een specifieke functie.</span><span class="sxs-lookup"><span data-stu-id="96913-226">If a version conflict arises, you can resolve it by adding a `package.json` file in hello folder of a specific function.</span></span>  

## <a name="environment-variables"></a><span data-ttu-id="96913-227">Omgevingsvariabelen</span><span class="sxs-lookup"><span data-stu-id="96913-227">Environment variables</span></span>
<span data-ttu-id="96913-228">tooget een omgevingsvariabele of een app-instelling-waarde gebruiken `process.env`, zoals weergegeven in het volgende codevoorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="96913-228">tooget an environment variable or an app setting value, use `process.env`, as shown in hello following code example:</span></span>

```javascript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    context.log('Node.js timer trigger function ran!', timeStamp);   
    context.log(GetEnvironmentVariable("AzureWebJobsStorage"));
    context.log(GetEnvironmentVariable("WEBSITE_SITE_NAME"));

    context.done();
};

function GetEnvironmentVariable(name)
{
    return name + ": " + process.env[name];
}
```
## <a name="considerations-for-javascript-functions"></a><span data-ttu-id="96913-229">Overwegingen voor JavaScript-functies</span><span class="sxs-lookup"><span data-stu-id="96913-229">Considerations for JavaScript functions</span></span>

<span data-ttu-id="96913-230">Wanneer u met JavaScript-functies werkt, rekening houden met Hallo in de volgende twee secties Hallo worden.</span><span class="sxs-lookup"><span data-stu-id="96913-230">When you work with JavaScript functions, be aware of hello considerations in hello following two sections.</span></span>

### <a name="choose-single-core-app-service-plans"></a><span data-ttu-id="96913-231">Kies één core-App Service-abonnementen</span><span class="sxs-lookup"><span data-stu-id="96913-231">Choose single-core App Service plans</span></span>

<span data-ttu-id="96913-232">Wanneer u een functie-app die gebruikmaakt van Hallo App Service-abonnement maakt, wordt u aangeraden dat u een plan single-core in plaats van een plan met meerdere kernen selecteert.</span><span class="sxs-lookup"><span data-stu-id="96913-232">When you create a function app that uses hello App Service plan, we recommend that you select a single-core plan rather than a plan with multiple cores.</span></span> <span data-ttu-id="96913-233">Vandaag de dag functies JavaScript-functies efficiënter uitgevoerd op virtuele machines single-core en met behulp van grotere virtuele machines levert geen prestatieverbeteringen Hallo verwacht.</span><span class="sxs-lookup"><span data-stu-id="96913-233">Today, Functions runs JavaScript functions more efficiently on single-core VMs, and using larger VMs does not produce hello expected performance improvements.</span></span> <span data-ttu-id="96913-234">Indien nodig, zodat u handmatig kunt uitbreiden door meer single-core VM-exemplaren toe te voegen of u automatisch schalen kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="96913-234">When necessary, you can manually scale out by adding more single-core VM instances, or you can enable auto-scale.</span></span> <span data-ttu-id="96913-235">Zie voor meer informatie [aantal exemplaren handmatig of automatisch schalen](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="96913-235">For more information, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span></span>    

### <a name="typescript-and-coffeescript-support"></a><span data-ttu-id="96913-236">Ondersteuning voor machineschrift en CoffeeScript</span><span class="sxs-lookup"><span data-stu-id="96913-236">TypeScript and CoffeeScript support</span></span>
<span data-ttu-id="96913-237">Omdat rechtstreekse ondersteuning nog niet voor het compileren van automatische machineschrift of CoffeeScript via Hallo runtime bestaat, moet deze ondersteuning toobe buiten Hallo-runtime verwerkt tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="96913-237">Because direct support does not yet exist for auto-compiling TypeScript or CoffeeScript via hello runtime, such support needs toobe handled outside hello runtime, at deployment time.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="96913-238">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="96913-238">Next steps</span></span>
<span data-ttu-id="96913-239">Zie voor meer informatie Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="96913-239">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="96913-240">Aanbevolen procedures voor Azure Functions</span><span class="sxs-lookup"><span data-stu-id="96913-240">Best practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="96913-241">Naslaginformatie over Azure Functions voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="96913-241">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="96913-242">Azure Functions C# referentie voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="96913-242">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="96913-243">Azure Functions F # referentie voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="96913-243">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="96913-244">Azure Functions-triggers en bindingen</span><span class="sxs-lookup"><span data-stu-id="96913-244">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

