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
# <a name="azure-functions-javascript-developer-guide"></a>Azure Functions JavaScript-handleiding voor ontwikkelaars
> [!div class="op_single_selector"]
> * [C#-script](functions-reference-csharp.md)
> * [F # script](functions-reference-fsharp.md)
> * [JavaScript](functions-reference-node.md)
> 
> 

Hallo JavaScript-ervaring voor Azure Functions het eenvoudig tooexport een functie die wordt doorgegeven maakt als een `context` voor communicatie met de Hallo runtime en voor het ontvangen en verzenden van gegevens via bindingen-object.

In dit artikel wordt ervan uitgegaan dat u hebt al Hallo gelezen [naslaginformatie voor ontwikkelaars van Azure Functions](functions-reference.md).

## <a name="exporting-a-function"></a>Exporteren van een functie
Alle JavaScript-functies moeten één exporteren `function` via `module.exports` voor Hallo runtime toofind functie Hallo en voer deze uit. Deze functie moet altijd bevatten een `context` object.

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

Bindingen van `direction === "in"` worden doorgegeven als argument, wat betekent dat u kunt gebruiken [ `arguments` ](https://msdn.microsoft.com/library/87dw3w1k.aspx) toodynamically afhandelen van nieuwe invoer (bijvoorbeeld met behulp van `arguments.length` tooiterate via de ingevoerde gegevens). Deze functie is handig wanneer u alleen een trigger en er zijn geen extra invoergegevens omdat u voorspelbare toegang uw triggergegevens zonder die verwijzen naar tot uw `context` object.

Hallo argumenten worden altijd doorgegeven toohello-functie in Hallo volgorde waarin ze voorkomen in *function.json*, zelfs als u ze niet in de uitvoer-instructie opgeven. Als u hebt bijvoorbeeld `function(context, a, b)` en deze te wijzigen`function(context, a)`, u kunt nog steeds Hallo-waarde van `b` in functiecode door ernaar te verwijzen`arguments[3]`.

Alle bindingen, ongeacht de richting, ook op Hallo doorgegeven `context` object (Zie het volgende script Hallo). 

## <a name="context-object"></a>context-object
Hallo runtime gebruikt een `context` object toopass gegevens tooand van uw functie en toolet u contact met de Hallo-runtime opnemen.

Hallo context-object is altijd Hallo eerste parameter tooa functie en moet worden opgenomen omdat deze methoden, zoals `context.done` en `context.log`, die vereist toouse Hallo runtime correct zijn. U kunt een naam Hallo object wat u wilt dat (bijvoorbeeld `ctx` of `c`).

```javascript
// You must include a context, but other arguments are optional
module.exports = function(context) {
    // function logic goes here :)
};
```

### <a name="contextbindings-property"></a>de eigenschap context.bindings

```
context.bindings
```
Retourneert een benoemde object dat al uw invoer en uitvoer gegevens bevat. Bijvoorbeeld, Hallo na de bindingsdefinitie in uw *function.json* hebt u toegang tot inhoud van de wachtrij Hallo van Hallo Hallo `context.bindings.myInput` object. 

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

### <a name="contextdone-method"></a>context.Done methode
```
context.done([err],[propertyBag])
```

Informeert Hallo runtime die uw code is voltooid. U moet aanroepen `context.done`, of anders Hallo runtime nooit weet dat de functie voltooid is en Hallo-uitvoering wordt time-out. 

Hallo `context.done` methode kunt u toopass back- zowel een eigenschappenverzameling van eigenschappen die Hallo-eigenschappen op hallo overschreven als een gebruiker gedefinieerde fout toohello runtime `context.bindings` object.

```javascript
// Even though we set myOutput toohave:
//  -> text: hello world, number: 123
context.bindings.myOutput = { text: 'hello world', number: 123 };
// If we pass an object toohello done function...
context.done(null, { myOutput: { text: 'hello there, world', noNumber: true }});
// hello done method will overwrite hello myOutput binding toobe: 
//  -> text: hello there, world, noNumber: true
```

### <a name="contextlog-method"></a>context.log methode  

```
context.log(message)
```
Hiermee kunt u toowrite toohello console streaminglogboeken op Hallo trace standaardniveau. Op `context.log`, extra logboekregistratie methoden zijn beschikbaar waarmee u toohello consolelogboek op andere traceringsniveaus schrijven:


| Methode                 | Beschrijving                                |
| ---------------------- | ------------------------------------------ |
| **fout (_bericht_)**   | Schrijft tooerror niveau registreren of lager.   |
| **waarschuwen (_bericht_)**    | Schrijft toowarning niveau registreren of lager. |
| **Info (_bericht_)**    | Schrijft tooinfo niveau registreren of lager.    |
| **uitgebreide (_bericht_)** | Logboekregistratie op tooverbose schrijft.           |

Hallo volgende voorbeeld wordt geschreven toohello-console op Hallo waarschuwing Traceerniveau:

```javascript
context.log.warn("Something has happened."); 
```
U kunt Hallo traceerniveau drempelwaarde voor logboekregistratie in Hallo host.json bestand of deze uitschakelen.  Zie de volgende sectie Hallo voor meer informatie over hoe toowrite toohello registreert.

## <a name="binding-data-type"></a>Binding-gegevenstype

toodefine Hallo Hallo gegevenstype voor een invoer-binding gebruiken `dataType` eigenschap in de definitie van de binding Hallo. Bijvoorbeeld: tooread Hallo inhoud van een HTTP-aanvraag in binaire indeling, gebruik Hallo type `binary`:

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

Andere opties voor `dataType` zijn `stream` en `string`.

## <a name="writing-trace-output-toohello-console"></a>Schrijven trace-uitvoer toohello console 

In de functies, gebruikt u Hallo `context.log` methoden toowrite trace-uitvoer toohello console. Op dit moment kunt u niet gebruiken `console.log` toowrite toohello-console.

Als u aanroept `context.log()`, uw bericht geschreven toohello-console op Hallo default traceringsniveau, Hallo _info_ traceerniveau. Hallo schrijft volgende code toohello-console op Hallo info Traceerniveau:

```javascript
context.log({hello: 'world'});  
```

Hallo is voorafgaande code gelijkwaardig toohello code te volgen:

```javascript
context.log.info({hello: 'world'});  
```

Hallo schrijft volgende code toohello-console op Hallo foutniveau:

```javascript
context.log.error("An error has occurred.");  
```

Omdat _fout_ Hallo hoogste trace niveau, deze tracering wordt geschreven toohello uitvoer op alle traceringsniveaus als logboekregistratie is ingeschakeld.  


Alle `context.log` methoden ondersteunen Hallo dezelfde indeling voor parameter die wordt ondersteund door Hallo Node.js [util.format methode](https://nodejs.org/api/util.html#util_util_format_format). Overweeg de volgende code waarmee toohello console schrijft door Hallo standaard traceerniveau Hallo:

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=' + req.originalUrl);
context.log('Request Headers = ' + JSON.stringify(req.headers));
```

U kunt ook schrijven Hallo dezelfde code in de volgende indeling Hallo:

```javascript
context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);
context.log('Request Headers = ', JSON.stringify(req.headers));
```

### <a name="configure-hello-trace-level-for-console-logging"></a>Hallo traceerniveau voor console-logboekregistratie configureren

Functies kunt u definiëren Hallo traceerniveau van drempelwaarde voor het schrijven van toohello console dit maakt het eenvoudig toocontrol Hallo manier traceringen toohello console van uw functies worden geschreven. tooset hello drempelwaarde voor alle traces gebruik Hallo-toohello console geschreven `tracing.consoleLevel` eigenschap in Hallo host.json bestand. Deze instelling geldt tooall functies in uw app in de functie. Hallo wordt volgende voorbeeld Hallo trace drempelwaarde tooenable uitgebreide logboekregistratie:

```json
{ 
    "tracing": {      
        "consoleLevel": "verbose"     
    }
}  
```

Waarden van **consoleLevel** toohello namen van Hallo overeenkomen `context.log` methoden. toodisable alle traceerlogboekregistratie toohello console ingesteld **consoleLevel** too_off_. Zie voor meer informatie over Hallo host.json bestand Hallo [host.json naslagonderwerp](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).

## <a name="http-triggers-and-bindings"></a>HTTP-triggers en bindingen

HTTP- en webhook triggers en HTTP-uitvoer bindingen aanvraag en antwoord objecten toorepresent Hallo HTTP messaging gebruiken.  

### <a name="request-object"></a>Request-object

Hallo `request` object heeft Hallo volgende eigenschappen:

| Eigenschap      | Beschrijving                                                    |
| ------------- | -------------------------------------------------------------- |
| _hoofdtekst_        | Een object dat Hallo hoofdtekst van Hallo-aanvraag bevat.               |
| _headers_     | Een object dat aanvraagheaders Hallo bevat.                   |
| _methode_      | Hallo HTTP-methode van Hallo-aanvraag.                                |
| _originalUrl_ | Hallo-URL van Hallo-aanvraag.                                        |
| _parameters voor_      | Een object dat Hallo routering parameters van Hallo-aanvraag bevat. |
| _query_       | Een object dat de queryparameters Hallo bevat.                  |
| _rawBody_     | Hallo-hoofdtekst van het Hallo-bericht als een tekenreeks.                           |


### <a name="response-object"></a>Response-object

Hallo `response` object heeft Hallo volgende eigenschappen:

| Eigenschap  | Beschrijving                                               |
| --------- | --------------------------------------------------------- |
| _hoofdtekst_    | Een object dat Hallo hoofdtekst van antwoord Hallo bevat.         |
| _headers_ | Een object dat Hallo antwoordheaders bevat.             |
| _isRaw_   | Hiermee wordt aangegeven dat de opmaak wordt overgeslagen voor antwoord Hallo.    |
| _status_  | HTTP-statuscode van antwoord Hallo Hallo.                     |

### <a name="accessing-hello-request-and-response"></a>Toegang tot Hallo-aanvraag en -antwoord 

Wanneer u met HTTP-triggers werkt, kunt u Hallo HTTP-aanvraag en antwoord-objecten in een van drie manieren openen:

+ Naam van Hallo invoer en uitvoer bindingen. Op deze manier Hallo Hallo HTTP-trigger en bindingen werk dezelfde als elke andere binding. Hallo volgende voorbeeld wordt ingesteld Hallo response-object met behulp van een benoemde `response` binding: 

    ```javascript
    context.bindings.response = { status: 201, body: "Insert succeeded." };
    ```

+ Van `req` en `res` eigenschappen op Hallo `context` object. Op deze manier kunt u Hallo conventionele patroon tooaccess HTTP-gegevens van Hallo context-object, in plaats van toouse Hallo volledige `context.bindings.name` patroon. Hallo volgende voorbeeld wordt getoond hoe tooaccess hello `req` en `res` objecten op Hallo `context`:

    ```javascript
    // You can access your http request off hello context ...
    if(context.req.body.emoji === ':pizza:') context.log('Yay!');
    // and also set your http response
    context.res = { status: 202, body: 'You successfully ordered more coffee!' }; 
    ```

+ Door het aanroepen van `context.done()`. Een speciaal soort HTTP-binding retourneert Hallo-antwoord dat wordt doorgegeven toohello `context.done()` methode. Hallo HTTP na uitvoer binding definieert een `$return` uitvoerparameter:

    ```json
    {
      "type": "http",
      "direction": "out",
      "name": "$return"
    }
    ``` 
    Deze binding uitvoer verwacht u toosupply Hallo antwoord bij het aanroepen van `done()`, als volgt:

    ```javascript
     // Define a valid response object.
    res = { status: 201, body: "Insert succeeded." };
    context.done(null, res);   
    ```  

## <a name="node-version-and-package-management"></a>Knooppunt-versie en Package Management
Hallo knooppunt versie is momenteel vergrendeld op `6.5.0`. We bent voor het onderzoeken van het toevoegen van ondersteuning voor meer versies en waardoor het worden geconfigureerd.

Hallo stappen te volgen, kunt u pakketten opnemen in uw app in functie: 

1. Ga te`https://<function_app_name>.scm.azurewebsites.net`.

2. Klik op **Console voor foutopsporing** > **CMD**.

3. Ga te`D:\home\site\wwwroot`, en sleep het bestand package.json toohello **wwwroot** map in de bovenste helft Hallo van Hallo-pagina.  
    U kunt ook bestanden tooyour functie-app op andere manieren uploaden. Zie voor meer informatie [hoe de app-bestanden voor het functioneren van tooupdate](functions-reference.md#fileupdate). 

4. Nadat het Hallo package.json-bestand is geüpload, voert u Hallo `npm install` opdracht in Hallo **Kudu-console voor uitvoering op afstand**.  
    Deze actie hello-pakketten die zijn aangegeven in Hallo package.json-bestand wordt gedownload en Hallo functie-app opnieuw wordt opgestart.

Nadat hello pakketten die u moet zijn geïnstalleerd, u ze importeren tooyour functie door het aanroepen van `require('packagename')`, Hallo voorbeeld te volgen:

```javascript
// Import hello underscore.js library
var _ = require('underscore');
var version = process.version; // version === 'v6.5.0'

module.exports = function(context) {
    // Using our imported underscore.js library
    var matched_names = _
        .where(context.bindings.myInput.names, {first: 'Carla'});
```

U moet definiëren een `package.json` bestand in de hoofdmap Hallo van functie-app. Definiërende Hallo-bestand laat alle functies in Hallo app share Hallo hetzelfde in de cache-pakketten, waardoor de beste prestaties Hallo. Als een conflict ontstaat, u het kunt oplossen door toe te voegen een `package.json` bestand in map Hallo van een specifieke functie.  

## <a name="environment-variables"></a>Omgevingsvariabelen
tooget een omgevingsvariabele of een app-instelling-waarde gebruiken `process.env`, zoals weergegeven in het volgende codevoorbeeld Hallo:

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
## <a name="considerations-for-javascript-functions"></a>Overwegingen voor JavaScript-functies

Wanneer u met JavaScript-functies werkt, rekening houden met Hallo in de volgende twee secties Hallo worden.

### <a name="choose-single-core-app-service-plans"></a>Kies één core-App Service-abonnementen

Wanneer u een functie-app die gebruikmaakt van Hallo App Service-abonnement maakt, wordt u aangeraden dat u een plan single-core in plaats van een plan met meerdere kernen selecteert. Vandaag de dag functies JavaScript-functies efficiënter uitgevoerd op virtuele machines single-core en met behulp van grotere virtuele machines levert geen prestatieverbeteringen Hallo verwacht. Indien nodig, zodat u handmatig kunt uitbreiden door meer single-core VM-exemplaren toe te voegen of u automatisch schalen kunt inschakelen. Zie voor meer informatie [aantal exemplaren handmatig of automatisch schalen](../monitoring-and-diagnostics/insights-how-to-scale.md?toc=%2fazure%2fapp-service-web%2ftoc.json).    

### <a name="typescript-and-coffeescript-support"></a>Ondersteuning voor machineschrift en CoffeeScript
Omdat rechtstreekse ondersteuning nog niet voor het compileren van automatische machineschrift of CoffeeScript via Hallo runtime bestaat, moet deze ondersteuning toobe buiten Hallo-runtime verwerkt tijdens de implementatie. 

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie Hallo resources te volgen:

* [Aanbevolen procedures voor Azure Functions](functions-best-practices.md)
* [Naslaginformatie over Azure Functions voor ontwikkelaars](functions-reference.md)
* [Azure Functions C# referentie voor ontwikkelaars](functions-reference-csharp.md)
* [Azure Functions F # referentie voor ontwikkelaars](functions-reference-fsharp.md)
* [Azure Functions-triggers en bindingen](functions-triggers-bindings.md)

