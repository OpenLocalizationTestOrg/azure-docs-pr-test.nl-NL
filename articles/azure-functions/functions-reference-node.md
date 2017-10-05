---
title: JavaScript-referentie voor ontwikkelaars voor Azure Functions | Microsoft Docs
description: Begrijpen hoe functies ontwikkelen met behulp van JavaScript.
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
ms.openlocfilehash: 7ea81ed47f391fbce1432c2b11ac176ab6c04ae0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-javascript-developer-guide"></a><span data-ttu-id="d3cc7-104">Azure Functions JavaScript-handleiding voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="d3cc7-104">Azure Functions JavaScript developer guide</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d3cc7-105">C#-script</span><span class="sxs-lookup"><span data-stu-id="d3cc7-105">C# script</span></span>](functions-reference-csharp.md)
> * [<span data-ttu-id="d3cc7-106">F # script</span><span class="sxs-lookup"><span data-stu-id="d3cc7-106">F# script</span></span>](functions-reference-fsharp.md)
> * [<span data-ttu-id="d3cc7-107">JavaScript</span><span class="sxs-lookup"><span data-stu-id="d3cc7-107">JavaScript</span></span>](functions-reference-node.md)
> 
> 

<span data-ttu-id="d3cc7-108">De JavaScript-ervaring voor Azure Functions maakt het gemakkelijk te exporteren van een functie die wordt doorgegeven als een `context` voor communicatie met de runtime en voor het ontvangen en verzenden van gegevens via bindingen-object.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-108">The JavaScript experience for Azure Functions makes it easy to export a function, which is passed as a `context` object for communicating with the runtime and for receiving and sending data via bindings.</span></span>

<span data-ttu-id="d3cc7-109">In dit artikel wordt ervan uitgegaan dat u al hebt gelezen de [naslaginformatie voor ontwikkelaars van Azure Functions](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="d3cc7-109">This article assumes that you've already read the [Azure Functions developer reference](functions-reference.md).</span></span>

## <a name="exporting-a-function"></a><span data-ttu-id="d3cc7-110">Exporteren van een functie</span><span class="sxs-lookup"><span data-stu-id="d3cc7-110">Exporting a function</span></span>
<span data-ttu-id="d3cc7-111">Alle JavaScript-functies moeten één exporteren `function` via `module.exports` voor de runtime vinden van de functie en voer deze uit.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-111">All JavaScript functions must export a single `function` via `module.exports` for the runtime to find the function and run it.</span></span> <span data-ttu-id="d3cc7-112">Deze functie moet altijd bevatten een `context` object.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-112">This function must always include a `context` object.</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // Additional inputs can be accessed by the arguments property
    if(arguments.length === 4) {
        context.log('This function has 4 inputs');
    }
};
// or you can include additional inputs in your arguments
module.exports = function(context, myTrigger, myInput, myOtherInput) {
    // function logic goes here :)
};
```

<span data-ttu-id="d3cc7-113">Bindingen van `direction === "in"` worden doorgegeven als argument, wat betekent dat u kunt gebruiken [ `arguments` ](https://msdn.microsoft.com/library/87dw3w1k.aspx) dynamisch afhandelen nieuwe invoer (bijvoorbeeld met behulp van `arguments.length` worden herhaald voor de ingevoerde gegevens).</span><span class="sxs-lookup"><span data-stu-id="d3cc7-113">Bindings of `direction === "in"` are passed along as function arguments, which means that you can use [`arguments`](https://msdn.microsoft.com/library/87dw3w1k.aspx) to dynamically handle new inputs (for example, by using `arguments.length` to iterate over all your inputs).</span></span> <span data-ttu-id="d3cc7-114">Deze functie is handig wanneer u alleen een trigger en er zijn geen extra invoergegevens omdat u voorspelbare toegang uw triggergegevens zonder die verwijzen naar tot uw `context` object.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-114">This functionality is convenient when you have only a trigger and no additional inputs, because you can predictably access your trigger data without referencing your `context` object.</span></span>

<span data-ttu-id="d3cc7-115">De argumenten worden altijd doorgegeven aan de functie in de volgorde waarin ze plaatsvinden in *function.json*, zelfs als u ze niet in de uitvoer-instructie opgeven.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-115">The arguments are always passed along to the function in the order in which they occur in *function.json*, even if you don't specify them in your exports statement.</span></span> <span data-ttu-id="d3cc7-116">Als u hebt bijvoorbeeld `function(context, a, b)` en wijzig dit in `function(context, a)`, kunt u de waarde van krijgen `b` in de functiecode door te verwijzen naar `arguments[3]`.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-116">For example, if you have `function(context, a, b)` and change it to `function(context, a)`, you can still get the value of `b` in function code by referring to `arguments[3]`.</span></span>

<span data-ttu-id="d3cc7-117">Alle bindingen, ongeacht de richting, worden ook doorgegeven op de `context` object (Zie het volgende script).</span><span class="sxs-lookup"><span data-stu-id="d3cc7-117">All bindings, regardless of direction, are also passed along on the `context` object (see the following script).</span></span> 

## <a name="context-object"></a><span data-ttu-id="d3cc7-118">context-object</span><span class="sxs-lookup"><span data-stu-id="d3cc7-118">context object</span></span>
<span data-ttu-id="d3cc7-119">De runtime gebruikt een `context` object voor het doorgeven van gegevens naar en van de functie en kunt u communiceren met de runtime.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-119">The runtime uses a `context` object to pass data to and from your function and to let you communicate with the runtime.</span></span>

<span data-ttu-id="d3cc7-120">Het context-object is altijd de eerste parameter aan een functie en moet worden opgenomen omdat deze methoden, zoals `context.done` en `context.log`, die vereist zijn juist gebruik van de runtime.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-120">The context object is always the first parameter to a function and must be included because it has methods such as `context.done` and `context.log`, which are required to use the runtime correctly.</span></span> <span data-ttu-id="d3cc7-121">U kunt het object naam wat u wilt dat (bijvoorbeeld `ctx` of `c`).</span><span class="sxs-lookup"><span data-stu-id="d3cc7-121">You can name the object whatever you would like (for example, `ctx` or `c`).</span></span>

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // function logic goes here :)
};
```

### <a name="contextbindings-property"></a><span data-ttu-id="d3cc7-122">de eigenschap context.bindings</span><span class="sxs-lookup"><span data-stu-id="d3cc7-122">context.bindings property</span></span>

```
context.bindings
```
<span data-ttu-id="d3cc7-123">Retourneert een benoemde object dat al uw invoer en uitvoer gegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-123">Returns a named object that contains all your input and output data.</span></span> <span data-ttu-id="d3cc7-124">Bijvoorbeeld de volgende bindingsdefinitie in uw *function.json* hebt u toegang de inhoud van de wachtrij van tot de `context.bindings.myInput` object.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-124">For example, the following binding definition in your *function.json* lets you access the contents of the queue from the `context.bindings.myInput` object.</span></span> 

```json
{
    "type":"queue",
    "direction":"in",
    "name":"myInput"
    ...
}
```

```javascript
// myInput contains the input data, which may have properties such as "name"
var author = context.bindings.myInput.name;
// Similarly, you can set your output data
context.bindings.myOutput = { 
        some_text: 'hello world', 
        a_number: 1 };
```

### <a name="contextdone-method"></a><span data-ttu-id="d3cc7-125">context.Done methode</span><span class="sxs-lookup"><span data-stu-id="d3cc7-125">context.done method</span></span>
```
context.done([err],[propertyBag])
```

<span data-ttu-id="d3cc7-126">Informeert de runtime die uw code is voltooid.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-126">Informs the runtime that your code has finished.</span></span> <span data-ttu-id="d3cc7-127">U moet aanroepen `context.done`, of anders de runtime nooit weet dat uw functie voltooid is en de uitvoering wordt time-out.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-127">You must call `context.done`, or else the runtime never knows that your function is complete, and the execution will time out.</span></span> 

<span data-ttu-id="d3cc7-128">De `context.done` methode kunt u weer zowel een gebruiker gedefinieerde fout doorgeven aan de runtime en een eigenschappenverzameling van eigenschappen die het overschrijven van de eigenschappen op de `context.bindings` object.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-128">The `context.done` method allows you to pass back both a user-defined error to the runtime and a property bag of properties that overwrite the properties on the `context.bindings` object.</span></span>

```javascript
// Even though we set myOutput to have:
//  -> text: hello world, number: 123
context.bindings.myOutput = { text: 'hello world', number: 123 };
// If we pass an object to the done function...
context.done(null, { myOutput: { text: 'hello there, world', noNumber: true }});
// the done method will overwrite the myOutput binding to be: 
//  -> text: hello there, world, noNumber: true
```

### <a name="contextlog-method"></a><span data-ttu-id="d3cc7-129">context.log methode</span><span class="sxs-lookup"><span data-stu-id="d3cc7-129">context.log method</span></span>  

```
context.log(message)
```
<span data-ttu-id="d3cc7-130">Hiermee kunt u om te schrijven naar de logboeken van de streaming-console op het standaardniveau voor tracering.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-130">Allows you to write to the streaming console logs at the default trace level.</span></span> <span data-ttu-id="d3cc7-131">Op `context.log`, extra logboekregistratie methoden zijn beschikbaar waarmee u naar het consolelogboek op andere traceringsniveaus schrijven:</span><span class="sxs-lookup"><span data-stu-id="d3cc7-131">On `context.log`, additional logging methods are available that let you write to the console log at other trace levels:</span></span>


| <span data-ttu-id="d3cc7-132">Methode</span><span class="sxs-lookup"><span data-stu-id="d3cc7-132">Method</span></span>                 | <span data-ttu-id="d3cc7-133">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d3cc7-133">Description</span></span>                                |
| ---------------------- | ------------------------------------------ |
| <span data-ttu-id="d3cc7-134">**fout (_bericht_)**</span><span class="sxs-lookup"><span data-stu-id="d3cc7-134">**error(_message_)**</span></span>   | <span data-ttu-id="d3cc7-135">Schrijft naar foutniveau registreren of lager.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-135">Writes to error level logging, or lower.</span></span>   |
| <span data-ttu-id="d3cc7-136">**waarschuwen (_bericht_)**</span><span class="sxs-lookup"><span data-stu-id="d3cc7-136">**warn(_message_)**</span></span>    | <span data-ttu-id="d3cc7-137">Schrijft naar waarschuwingsniveau registreren of lager.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-137">Writes to warning level logging, or lower.</span></span> |
| <span data-ttu-id="d3cc7-138">**Info (_bericht_)**</span><span class="sxs-lookup"><span data-stu-id="d3cc7-138">**info(_message_)**</span></span>    | <span data-ttu-id="d3cc7-139">Schrijft naar info-niveau registreren of lager.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-139">Writes to info level logging, or lower.</span></span>    |
| <span data-ttu-id="d3cc7-140">**uitgebreide (_bericht_)**</span><span class="sxs-lookup"><span data-stu-id="d3cc7-140">**verbose(_message_)**</span></span> | <span data-ttu-id="d3cc7-141">Schrijft naar de uitgebreide logboekregistratie.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-141">Writes to verbose level logging.</span></span>           |

<span data-ttu-id="d3cc7-142">Het volgende voorbeeld wordt geschreven naar de console op het niveau voor het traceren van waarschuwing:</span><span class="sxs-lookup"><span data-stu-id="d3cc7-142">The following example writes to the console at the warning trace level:</span></span>

```javascript
context.log.warn("Something has happened."); 
```
<span data-ttu-id="d3cc7-143">U kunt stellen voor het registreren in het bestand host.json traceerniveau of uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-143">You can set the trace-level threshold for logging in the host.json file, or turn it off.</span></span>  <span data-ttu-id="d3cc7-144">Zie de volgende sectie voor meer informatie over het schrijven naar de logboeken.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-144">For more information about how to write to the logs, see the next section.</span></span>

## <a name="binding-data-type"></a><span data-ttu-id="d3cc7-145">Binding-gegevenstype</span><span class="sxs-lookup"><span data-stu-id="d3cc7-145">Binding data type</span></span>

<span data-ttu-id="d3cc7-146">Gebruik het definiëren van het gegevenstype voor een invoer-binding het `dataType` eigenschap in de definitie van de binding.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-146">To define the data type for an input binding, use the `dataType` property in the binding definition.</span></span> <span data-ttu-id="d3cc7-147">Gebruik bijvoorbeeld om te lezen van de inhoud van een HTTP-aanvraag in binaire indeling, het type `binary`:</span><span class="sxs-lookup"><span data-stu-id="d3cc7-147">For example, to read the content of an HTTP request in binary format, use the type `binary`:</span></span>

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

<span data-ttu-id="d3cc7-148">Andere opties voor `dataType` zijn `stream` en `string`.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-148">Other options for `dataType` are `stream` and `string`.</span></span>

## <a name="writing-trace-output-to-the-console"></a><span data-ttu-id="d3cc7-149">Trace-uitvoer schrijven naar de console</span><span class="sxs-lookup"><span data-stu-id="d3cc7-149">Writing trace output to the console</span></span> 

<span data-ttu-id="d3cc7-150">In de functies, gebruikt u de `context.log` methoden trace-uitvoer schrijven naar de console.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-150">In Functions, you use the `context.log` methods to write trace output to the console.</span></span> <span data-ttu-id="d3cc7-151">Op dit moment kunt u niet gebruiken `console.log` schrijven naar de console.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-151">At this point, you cannot use `console.log` to write to the console.</span></span>

<span data-ttu-id="d3cc7-152">Als u aanroept `context.log()`, het bericht is geschreven naar de console op het standaardniveau van trace die de _info_ traceerniveau.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-152">When you call `context.log()`, your message is written to the console at the default trace level, which is the _info_ trace level.</span></span> <span data-ttu-id="d3cc7-153">De volgende code schrijft naar de console op het info-Traceerniveau:</span><span class="sxs-lookup"><span data-stu-id="d3cc7-153">The following code writes to the console at the info trace level:</span></span>

```javascript
context.log({hello: 'world'});  
```

<span data-ttu-id="d3cc7-154">De bovenstaande code is gelijk aan de volgende code:</span><span class="sxs-lookup"><span data-stu-id="d3cc7-154">The preceding code is equivalent to the following code:</span></span>

```javascript
context.log.info({hello: 'world'});  
```

<span data-ttu-id="d3cc7-155">De volgende code schrijft naar de console op het foutniveau van de:</span><span class="sxs-lookup"><span data-stu-id="d3cc7-155">The following code writes to the console at the error level:</span></span>

```javascript
context.log.error("An error has occurred.");  
```

<span data-ttu-id="d3cc7-156">Omdat _fout_ is de hoogste niveau, deze tracering wordt geschreven naar de uitvoer op alle traceringsniveaus als logboekregistratie is ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-156">Because _error_ is the highest trace level, this trace is written to the output at all trace levels as long as logging is enabled.</span></span>  


<span data-ttu-id="d3cc7-157">Alle `context.log` methoden ondersteunen dezelfde indeling voor parameter die wordt ondersteund door de Node.js [util.format methode](https://nodejs.org/api/util.html#util_util_format_format).</span><span class="sxs-lookup"><span data-stu-id="d3cc7-157">All `context.log` methods support the same parameter format that's supported by the Node.js [util.format method](https://nodejs.org/api/util.html#util_util_format_format).</span></span> <span data-ttu-id="d3cc7-158">Houd rekening met de volgende code, naar de console schrijft met behulp van het standaard Traceerniveau:</span><span class="sxs-lookup"><span data-stu-id="d3cc7-158">Consider the following code, which writes to the console by using the default trace level:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=' + req.originalUrl);
context.log('Request Headers = ' + JSON.stringify(req.headers));
```

<span data-ttu-id="d3cc7-159">U kunt ook de dezelfde code schrijven in de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="d3cc7-159">You can also write the same code in the following format:</span></span>

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);
context.log('Request Headers = ', JSON.stringify(req.headers));
```

### <a name="configure-the-trace-level-for-console-logging"></a><span data-ttu-id="d3cc7-160">Het traceerniveau voor console-logboekregistratie configureren</span><span class="sxs-lookup"><span data-stu-id="d3cc7-160">Configure the trace level for console logging</span></span>

<span data-ttu-id="d3cc7-161">Functies kunt u het traceerniveau drempelwaarde voor het schrijven naar de console kunt u gemakkelijk om te bepalen die anders de traceringen manier worden geschreven naar de console van uw functies definiëren.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-161">Functions lets you define the threshold trace level for writing to the console, which makes it easy to control the way traces are written to the console from your functions.</span></span> <span data-ttu-id="d3cc7-162">U stelt de drempelwaarde voor alle traces geschreven naar de console met de `tracing.consoleLevel` eigenschap in het bestand host.json.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-162">To set the threshold for all traces written to the console, use the `tracing.consoleLevel` property in the host.json file.</span></span> <span data-ttu-id="d3cc7-163">Deze instelling geldt voor alle functies in uw app in de functie.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-163">This setting applies to all functions in your function app.</span></span> <span data-ttu-id="d3cc7-164">Het volgende voorbeeld wordt de tracering drempelwaarde uitgebreide logboekregistratie inschakelen:</span><span class="sxs-lookup"><span data-stu-id="d3cc7-164">The following example sets the trace threshold to enable verbose logging:</span></span>

```json
{ 
    "tracing": {      
        "consoleLevel": "verbose"     
    }
}  
```

<span data-ttu-id="d3cc7-165">Waarden van **consoleLevel** overeenkomen met de namen van de `context.log` methoden.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-165">Values of **consoleLevel** correspond to the names of the `context.log` methods.</span></span> <span data-ttu-id="d3cc7-166">Schakel alle traceerlogboek in de console ingesteld **consoleLevel** naar _uit_.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-166">To disable all trace logging to the console, set **consoleLevel** to _off_.</span></span> <span data-ttu-id="d3cc7-167">Zie voor meer informatie over het bestand host.json de [host.json naslagonderwerp](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span><span class="sxs-lookup"><span data-stu-id="d3cc7-167">For more information about the host.json file, see the [host.json reference topic](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).</span></span>

## <a name="http-triggers-and-bindings"></a><span data-ttu-id="d3cc7-168">HTTP-triggers en bindingen</span><span class="sxs-lookup"><span data-stu-id="d3cc7-168">HTTP triggers and bindings</span></span>

<span data-ttu-id="d3cc7-169">HTTP- en webhook triggers en HTTP-uitvoer bindingen met de aanvraag en -antwoord objecten vertegenwoordigen de HTTP-berichten.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-169">HTTP and webhook triggers and HTTP output bindings use request and response objects to represent the HTTP messaging.</span></span>  

### <a name="request-object"></a><span data-ttu-id="d3cc7-170">Request-object</span><span class="sxs-lookup"><span data-stu-id="d3cc7-170">Request object</span></span>

<span data-ttu-id="d3cc7-171">De `request` object heeft de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="d3cc7-171">The `request` object has the following properties:</span></span>

| <span data-ttu-id="d3cc7-172">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="d3cc7-172">Property</span></span>      | <span data-ttu-id="d3cc7-173">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d3cc7-173">Description</span></span>                                                    |
| ------------- | -------------------------------------------------------------- |
| <span data-ttu-id="d3cc7-174">_hoofdtekst_</span><span class="sxs-lookup"><span data-stu-id="d3cc7-174">_body_</span></span>        | <span data-ttu-id="d3cc7-175">Een object dat de hoofdtekst van de aanvraag bevat.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-175">An object that contains the body of the request.</span></span>               |
| <span data-ttu-id="d3cc7-176">_headers_</span><span class="sxs-lookup"><span data-stu-id="d3cc7-176">_headers_</span></span>     | <span data-ttu-id="d3cc7-177">Een object dat de aanvraagheaders bevat.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-177">An object that contains the request headers.</span></span>                   |
| <span data-ttu-id="d3cc7-178">_methode_</span><span class="sxs-lookup"><span data-stu-id="d3cc7-178">_method_</span></span>      | <span data-ttu-id="d3cc7-179">De HTTP-methode van de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-179">The HTTP method of the request.</span></span>                                |
| <span data-ttu-id="d3cc7-180">_originalUrl_</span><span class="sxs-lookup"><span data-stu-id="d3cc7-180">_originalUrl_</span></span> | <span data-ttu-id="d3cc7-181">De URL van de aanvraag.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-181">The URL of the request.</span></span>                                        |
| <span data-ttu-id="d3cc7-182">_parameters voor_</span><span class="sxs-lookup"><span data-stu-id="d3cc7-182">_params_</span></span>      | <span data-ttu-id="d3cc7-183">Een object dat de routering parameters van de aanvraag bevat.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-183">An object that contains the routing parameters of the request.</span></span> |
| <span data-ttu-id="d3cc7-184">_query_</span><span class="sxs-lookup"><span data-stu-id="d3cc7-184">_query_</span></span>       | <span data-ttu-id="d3cc7-185">Een object dat de queryparameters bevat.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-185">An object that contains the query parameters.</span></span>                  |
| <span data-ttu-id="d3cc7-186">_rawBody_</span><span class="sxs-lookup"><span data-stu-id="d3cc7-186">_rawBody_</span></span>     | <span data-ttu-id="d3cc7-187">De hoofdtekst van het bericht als een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-187">The body of the message as a string.</span></span>                           |


### <a name="response-object"></a><span data-ttu-id="d3cc7-188">Response-object</span><span class="sxs-lookup"><span data-stu-id="d3cc7-188">Response object</span></span>

<span data-ttu-id="d3cc7-189">De `response` object heeft de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="d3cc7-189">The `response` object has the following properties:</span></span>

| <span data-ttu-id="d3cc7-190">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="d3cc7-190">Property</span></span>  | <span data-ttu-id="d3cc7-191">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="d3cc7-191">Description</span></span>                                               |
| --------- | --------------------------------------------------------- |
| <span data-ttu-id="d3cc7-192">_hoofdtekst_</span><span class="sxs-lookup"><span data-stu-id="d3cc7-192">_body_</span></span>    | <span data-ttu-id="d3cc7-193">Een object dat de hoofdtekst van het antwoord bevat.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-193">An object that contains the body of the response.</span></span>         |
| <span data-ttu-id="d3cc7-194">_headers_</span><span class="sxs-lookup"><span data-stu-id="d3cc7-194">_headers_</span></span> | <span data-ttu-id="d3cc7-195">Een object met de antwoordheaders.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-195">An object that contains the response headers.</span></span>             |
| <span data-ttu-id="d3cc7-196">_isRaw_</span><span class="sxs-lookup"><span data-stu-id="d3cc7-196">_isRaw_</span></span>   | <span data-ttu-id="d3cc7-197">Hiermee wordt aangegeven dat opmaak voor het antwoord is overgeslagen.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-197">Indicates that formatting is skipped for the response.</span></span>    |
| <span data-ttu-id="d3cc7-198">_status_</span><span class="sxs-lookup"><span data-stu-id="d3cc7-198">_status_</span></span>  | <span data-ttu-id="d3cc7-199">De HTTP-statuscode van het antwoord.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-199">The HTTP status code of the response.</span></span>                     |

### <a name="accessing-the-request-and-response"></a><span data-ttu-id="d3cc7-200">Toegang tot de aanvraag en -antwoord</span><span class="sxs-lookup"><span data-stu-id="d3cc7-200">Accessing the request and response</span></span> 

<span data-ttu-id="d3cc7-201">Wanneer u met HTTP-triggers werkt, kunt u de HTTP-aanvraag en antwoord-objecten in een van drie manieren openen:</span><span class="sxs-lookup"><span data-stu-id="d3cc7-201">When you work with HTTP triggers, you can access the HTTP request and response objects in any of three ways:</span></span>

+ <span data-ttu-id="d3cc7-202">Van de benoemde invoer en uitvoer bindingen.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-202">From the named input and output bindings.</span></span> <span data-ttu-id="d3cc7-203">Op deze manier kunnen werken de HTTP-trigger en bindingen op dezelfde manier als andere bindingen.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-203">In this way, the HTTP trigger and bindings work the same as any other binding.</span></span> <span data-ttu-id="d3cc7-204">Het volgende voorbeeld wordt het antwoordobject met behulp van een benoemde `response` binding:</span><span class="sxs-lookup"><span data-stu-id="d3cc7-204">The following example sets the response object by using a named `response` binding:</span></span> 

    ```javascript
    context.bindings.response = { status: 201, body: "Insert succeeded." };
    ```

+ <span data-ttu-id="d3cc7-205">Van `req` en `res` eigenschappen op de `context` object.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-205">From `req` and `res` properties on the `context` object.</span></span> <span data-ttu-id="d3cc7-206">Op deze manier kunt u het conventionele patroon voor toegang tot HTTP gegevens uit het contextobject de volledige gebruiken in plaats van `context.bindings.name` patroon.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-206">In this way, you can use the conventional pattern to access HTTP data from the context object, instead of having to use the full `context.bindings.name` pattern.</span></span> <span data-ttu-id="d3cc7-207">Het volgende voorbeeld laat zien hoe voor toegang tot de `req` en `res` objecten op de `context`:</span><span class="sxs-lookup"><span data-stu-id="d3cc7-207">The following example shows how to access the `req` and `res` objects on the `context`:</span></span>

    ```javascript
    // You can access your http request off the context ...
    if(context.req.body.emoji === ':pizza:') context.log('Yay!');
    // and also set your http response
    context.res = { status: 202, body: 'You successfully ordered more coffee!' }; 
    ```

+ <span data-ttu-id="d3cc7-208">Door het aanroepen van `context.done()`.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-208">By calling `context.done()`.</span></span> <span data-ttu-id="d3cc7-209">Een speciaal soort HTTP-binding retourneert de reactie die wordt doorgegeven aan de `context.done()` methode.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-209">A special kind of HTTP binding returns the response that is passed to the `context.done()` method.</span></span> <span data-ttu-id="d3cc7-210">De volgende HTTP-uitvoer binding definieert een `$return` uitvoerparameter:</span><span class="sxs-lookup"><span data-stu-id="d3cc7-210">The following HTTP output binding defines a `$return` output parameter:</span></span>

    ```json
    {
      "type": "http",
      "direction": "out",
      "name": "$return"
    }
    ``` 
    <span data-ttu-id="d3cc7-211">Deze binding uitvoer verwacht op te geven van het antwoord bij het aanroepen van `done()`, als volgt:</span><span class="sxs-lookup"><span data-stu-id="d3cc7-211">This output binding expects you to supply the response when you call `done()`, as follows:</span></span>

    ```javascript
     // Define a valid response object.
    res = { status: 201, body: "Insert succeeded." };
    context.done(null, res);   
    ```  

## <a name="node-version-and-package-management"></a><span data-ttu-id="d3cc7-212">Knooppunt-versie en Package Management</span><span class="sxs-lookup"><span data-stu-id="d3cc7-212">Node version and Package Management</span></span>
<span data-ttu-id="d3cc7-213">De versie van het knooppunt is momenteel vergrendeld op `6.5.0`.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-213">The node version is currently locked at `6.5.0`.</span></span> <span data-ttu-id="d3cc7-214">We bent voor het onderzoeken van het toevoegen van ondersteuning voor meer versies en waardoor het worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-214">We're investigating adding support for more versions and making it configurable.</span></span>

<span data-ttu-id="d3cc7-215">De volgende stappen kunt u pakketten opnemen in uw app in functie:</span><span class="sxs-lookup"><span data-stu-id="d3cc7-215">The following steps let you include packages in your function app:</span></span> 

1. <span data-ttu-id="d3cc7-216">Ga naar `https://<function_app_name>.scm.azurewebsites.net`.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-216">Go to `https://<function_app_name>.scm.azurewebsites.net`.</span></span>

2. <span data-ttu-id="d3cc7-217">Klik op **Console voor foutopsporing** > **CMD**.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-217">Click **Debug Console** > **CMD**.</span></span>

3. <span data-ttu-id="d3cc7-218">Ga naar `D:\home\site\wwwroot`, en sleep uw package.json-bestand naar de **wwwroot** map in het bovenste gedeelte van de pagina.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-218">Go to `D:\home\site\wwwroot`, and then drag your package.json file to the **wwwroot** folder at the top half of the page.</span></span>  
    <span data-ttu-id="d3cc7-219">U kunt ook bestanden uploaden naar uw app in de functie op andere manieren.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-219">You can upload files to your function app in other ways also.</span></span> <span data-ttu-id="d3cc7-220">Zie voor meer informatie [het bijwerken van de functie app-bestanden](functions-reference.md#fileupdate).</span><span class="sxs-lookup"><span data-stu-id="d3cc7-220">For more information, see [How to update function app files](functions-reference.md#fileupdate).</span></span> 

4. <span data-ttu-id="d3cc7-221">Nadat de package.json-bestand is geüpload, voert u de `npm install` opdracht in de **Kudu-console voor uitvoering op afstand**.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-221">After the package.json file is uploaded, run the `npm install` command in the **Kudu remote execution console**.</span></span>  
    <span data-ttu-id="d3cc7-222">Deze actie de pakketten die zijn aangegeven in de package.json-bestand wordt gedownload en de functie-app opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-222">This action downloads the packages indicated in the package.json file and restarts the function app.</span></span>

<span data-ttu-id="d3cc7-223">Nadat de pakketten die u moet zijn geïnstalleerd, u deze importeren naar de functie door het aanroepen van `require('packagename')`, zoals in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d3cc7-223">After the packages you need are installed, you import them to your function by calling `require('packagename')`, as in the following example:</span></span>

```javascript
// Import the underscore.js library
var _ = require('underscore');
var version = process.version; // version === 'v6.5.0'

module.exports = function(context) {
    // Using our imported underscore.js library
    var matched_names = _
        .where(context.bindings.myInput.names, {first: 'Carla'});
```

<span data-ttu-id="d3cc7-224">U moet definiëren een `package.json` bestand in de hoofdmap van uw app functie.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-224">You should define a `package.json` file at the root of your function app.</span></span> <span data-ttu-id="d3cc7-225">Het definiëren van het bestand, kunt alle functies in de app delen de dezelfde in de cache pakketten, waardoor de beste prestaties.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-225">Defining the file lets all functions in the app share the same cached packages, which gives the best performance.</span></span> <span data-ttu-id="d3cc7-226">Als een conflict ontstaat, u het kunt oplossen door toe te voegen een `package.json` bestand in de map van een specifieke functie.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-226">If a version conflict arises, you can resolve it by adding a `package.json` file in the folder of a specific function.</span></span>  

## <a name="environment-variables"></a><span data-ttu-id="d3cc7-227">Omgevingsvariabelen</span><span class="sxs-lookup"><span data-stu-id="d3cc7-227">Environment variables</span></span>
<span data-ttu-id="d3cc7-228">Als u een omgevingsvariabele of een app die waarde instellen, gebruikt `process.env`, zoals weergegeven in het volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d3cc7-228">To get an environment variable or an app setting value, use `process.env`, as shown in the following code example:</span></span>

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
## <a name="considerations-for-javascript-functions"></a><span data-ttu-id="d3cc7-229">Overwegingen voor JavaScript-functies</span><span class="sxs-lookup"><span data-stu-id="d3cc7-229">Considerations for JavaScript functions</span></span>

<span data-ttu-id="d3cc7-230">Wanneer u met JavaScript-functies werkt, rekening houden met het in de volgende twee secties worden.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-230">When you work with JavaScript functions, be aware of the considerations in the following two sections.</span></span>

### <a name="choose-single-core-app-service-plans"></a><span data-ttu-id="d3cc7-231">Kies één core-App Service-abonnementen</span><span class="sxs-lookup"><span data-stu-id="d3cc7-231">Choose single-core App Service plans</span></span>

<span data-ttu-id="d3cc7-232">Wanneer u een functie-app die gebruikmaakt van de App Service-abonnement maakt, wordt u aangeraden dat u een plan single-core in plaats van een plan met meerdere kernen selecteert.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-232">When you create a function app that uses the App Service plan, we recommend that you select a single-core plan rather than a plan with multiple cores.</span></span> <span data-ttu-id="d3cc7-233">Vandaag de dag functies JavaScript-functies efficiënter uitgevoerd op virtuele machines single-core, en met behulp van grotere virtuele machines niet de verwachte prestatieverbeteringen produceren.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-233">Today, Functions runs JavaScript functions more efficiently on single-core VMs, and using larger VMs does not produce the expected performance improvements.</span></span> <span data-ttu-id="d3cc7-234">Indien nodig, zodat u handmatig kunt uitbreiden door meer single-core VM-exemplaren toe te voegen of u automatisch schalen kunt inschakelen.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-234">When necessary, you can manually scale out by adding more single-core VM instances, or you can enable auto-scale.</span></span> <span data-ttu-id="d3cc7-235">Zie voor meer informatie [aantal exemplaren handmatig of automatisch schalen](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d3cc7-235">For more information, see [Scale instance count manually or automatically](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).</span></span>    

### <a name="typescript-and-coffeescript-support"></a><span data-ttu-id="d3cc7-236">Ondersteuning voor machineschrift en CoffeeScript</span><span class="sxs-lookup"><span data-stu-id="d3cc7-236">TypeScript and CoffeeScript support</span></span>
<span data-ttu-id="d3cc7-237">Omdat rechtstreekse ondersteuning nog niet voor het compileren van automatische machineschrift of CoffeeScript via de runtime bestaat, moet deze ondersteuning buiten de runtime worden verwerkt tijdens de implementatie.</span><span class="sxs-lookup"><span data-stu-id="d3cc7-237">Because direct support does not yet exist for auto-compiling TypeScript or CoffeeScript via the runtime, such support needs to be handled outside the runtime, at deployment time.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d3cc7-238">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d3cc7-238">Next steps</span></span>
<span data-ttu-id="d3cc7-239">Zie de volgende bronnen voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="d3cc7-239">For more information, see the following resources:</span></span>

* [<span data-ttu-id="d3cc7-240">Aanbevolen procedures voor Azure Functions</span><span class="sxs-lookup"><span data-stu-id="d3cc7-240">Best practices for Azure Functions</span></span>](functions-best-practices.md)
* [<span data-ttu-id="d3cc7-241">Naslaginformatie over Azure Functions voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="d3cc7-241">Azure Functions developer reference</span></span>](functions-reference.md)
* [<span data-ttu-id="d3cc7-242">Azure Functions C# referentie voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="d3cc7-242">Azure Functions C# developer reference</span></span>](functions-reference-csharp.md)
* [<span data-ttu-id="d3cc7-243">Azure Functions F # referentie voor ontwikkelaars</span><span class="sxs-lookup"><span data-stu-id="d3cc7-243">Azure Functions F# developer reference</span></span>](functions-reference-fsharp.md)
* [<span data-ttu-id="d3cc7-244">Azure Functions-triggers en bindingen</span><span class="sxs-lookup"><span data-stu-id="d3cc7-244">Azure Functions triggers and bindings</span></span>](functions-triggers-bindings.md)

