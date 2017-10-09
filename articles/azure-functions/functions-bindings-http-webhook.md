---
title: de HTTP-functies en webhook bindingen aaaAzure | Microsoft Docs
description: Begrijpen hoe toouse HTTP en webhook triggers en bindingen in de Azure Functions.
services: functions
documentationcenter: na
author: mattchenderson
manager: erikre
editor: 
tags: 
keywords: Azure functions, functies, gebeurtenis verwerking, webhooks, dynamische Reken-, zonder server-architectuur, HTTP-API, REST
ms.assetid: 2b12200d-63d8-4ec1-9da8-39831d5a51b1
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/18/2016
ms.author: mahender
ms.openlocfilehash: c23b7a1443d492ed78c595e97d1d778a7ab12416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-http-and-webhook-bindings"></a>Azure Functions HTTP- en webhook bindingen
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Dit artikel wordt uitgelegd hoe tooconfigure en werken met HTTP triggers en bindingen in de Azure Functions.
Met deze, kunt u Azure Functions toobuild zonder Server-API's en antwoorden toowebhooks.

Azure Functions bevat Hallo bindingen te volgen:
- Een [HTTP-trigger](#httptrigger) kunt u een functie met een HTTP-aanvraag worden aangeroepen. Dit kan aangepaste toorespond te zijn[webhooks](#hooktrigger).
- Een [HTTP uitvoer binding](#output) kunt u toorespond toohello aanvraag.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

[!INCLUDE [HTTP client best practices](../../includes/functions-http-client-best-practices.md)]

<a name="httptrigger"></a>

## <a name="http-trigger"></a>HTTP-trigger
Hallo HTTP-trigger wordt de functie uitgevoerd in reactie tooan HTTP-aanvraag. U kunt deze aanpassen toorespond tooa bepaalde URL of een set HTTP-methoden. Een HTTP-trigger kan ook worden geconfigureerd toorespond toowebhooks. 

Als u Hallo functies portal gebruikt, u kunt ook aan de slag meteen met een vooraf gemaakte sjabloon. Selecteer **nieuwe functie** en kiest u 'API & Webhooks' in hello **Scenario** vervolgkeuzelijst. Selecteer een van de sjablonen Hallo en klik op **maken**.

Standaard wordt een HTTP-trigger toohello aanvraag met een HTTP 200 OK-statuscode en een lege hoofdtekst reageren. toomodify Hallo antwoord, configureert een [HTTP uitvoer binding](#output)

### <a name="configuring-an-http-trigger"></a>Configureren van een HTTP-trigger
Een HTTP-trigger is gedefinieerd door een JSON-object vergelijkbare toohello in hello te volgen, waaronder `bindings` matrix van function.json:

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function",
    "methods": [ "get" ],
    "route": "values/{id}"
},
```
Hallo binding ondersteunt Hallo volgende eigenschappen:

* **naam** : vereist - Hallo variabelenaam in functiecode gebruikt voor het Hallo-aanvraag of de hoofdtekst van de aanvraag. Zie [werken met een HTTP-trigger vanuit code](#httptriggerusage).
* **type** : vereist - moet worden ingesteld te 'httpTrigger'.
* **richting** : vereist - moet zijn ingesteld te 'in'.
* _authLevel_ : Hiermee bepaalt u welke sleutels, indien van toepassing, moeten toobe aanwezig is op Hallo-aanvraag in de volgorde tooinvoke Hallo-functie. Zie [werken met sleutels](#keys) hieronder. Hallo-waarde kan zijn dat een van de volgende Hallo:
    * _anonieme_: Er is geen API-sleutel is vereist.
    * _de functie_: een functiespecifieke API-sleutel is vereist. Dit is de standaardwaarde Hallo als niets wordt opgegeven.
    * _beheerder_ : Hallo hoofdsleutel is vereist.
* **methoden** : dit is een matrix van Hallo HTTP-methoden toowhich Hallo functie reageert. Als niet wordt opgegeven, reageert Hallo functie tooall HTTP-methoden. Zie [aanpassen Hallo HTTP-eindpunt](#url).
* **route** : Hiermee definieert u Hallo-Routesjabloon toowhich beheren uw functie reageert URL's aanvragen. Hallo standaardwaarde als niets wordt opgegeven is `<functionname>`. Zie [aanpassen Hallo HTTP-eindpunt](#url).
* **webHookType** : Hiermee configureert u Hallo HTTP-trigger tooact als een webhook reciever voor de opgegeven provider Hallo. Hallo _methoden_ eigenschap mag niet worden ingesteld als u dit hebt gekozen. Zie [reageren toowebhooks](#hooktrigger). Hallo-waarde kan zijn dat een van de volgende Hallo:
    * _genericJson_ : een eindpunt van de webhook algemeen zonder logica voor een specifieke provider.
    * _github_ : Hallo functie tooGitHub webhooks reageert. Hallo _authLevel_ eigenschap mag niet worden ingesteld als u dit hebt gekozen.
    * _vertraging_ : Hallo functie tooSlack webhooks reageert. Hallo _authLevel_ eigenschap mag niet worden ingesteld als u dit hebt gekozen.

<a name="httptriggerusage"></a>
### <a name="working-with-an-http-trigger-from-code"></a>Werken met een HTTP-trigger van code
Voor C# en F #, kunt u ofwel Hallo-type van uw invoer toobe trigger declareren `HttpRequestMessage` of een aangepast type. Als u ervoor kiest `HttpRequestMessage`, en vervolgens wordt u volledige toegang toohello request-object. Voor een aangepast type (zoals een POCO) probeert functies tooparse Hallo aanvraagtekst als JSON toopopulate Hallo objecteigenschappen.

Voor Node.js-functies biedt runtime van Functions Hallo Hallo aanvraagtekst in plaats van Hallo request-object.

Zie [voorbeelden van HTTP-trigger](#httptriggersample) bijvoorbeeld gebruik.


<a name="output"></a>
## <a name="http-response-output-binding"></a>Binding voor de HTTP-antwoord van de uitvoer
Hallo HTTP-uitvoer binding toorespond toohello HTTP-aanvraag afzender gebruiken. Deze binding vereist een HTTP-trigger en kunt u toocustomize Hallo antwoord is gekoppeld aan de aanvraag van trigger Hallo. Als een HTTP-uitvoer binding is niet opgegeven, wordt een HTTP-trigger HTTP 200 OK wordt geretourneerd met een lege hoofdtekst. 

### <a name="configuring-an-http-output-binding"></a>Binding uitvoer voor het configureren van een HTTP
Hallo HTTP uitvoer binding wordt gedefinieerd door een JSON-object vergelijkbare toohello in hello te volgen, waaronder `bindings` matrix van function.json:

```json
{
    "name": "res",
    "type": "http",
    "direction": "out"
}
```
Hallo binding bevat Hallo volgende eigenschappen:

* **naam** : vereist - variabelenaam in functiecode gebruikt voor het antwoord Hallo Hallo. Zie [werken met een HTTP-uitvoer binding vanuit code](#outputusage).
* **type** : vereist - moet worden ingesteld te 'http'.
* **richting** : vereist - moet zijn ingesteld te 'uit'.

<a name="outputusage"></a>
### <a name="working-with-an-http-output-binding-from-code"></a>Werken met een HTTP-uitvoer binding van code
U kunt Hallo uitvoer parameter (bijvoorbeeld ' res') toorespond toohello HTTP- of webhook aanroeper gebruiken. U kunt ook kunt u de standaard `Request.CreateResponse()` (C#) of `context.res` (Node.JS) patroon tooreturn uw antwoord. Zie voor voorbeelden van hoe toouse de laatste methode hello, [voorbeelden van HTTP-trigger](#httptriggersample) en [Webhook trigger voorbeelden](#hooktriggersample).


<a name="hooktrigger"></a>
## <a name="responding-toowebhooks"></a>Toowebhooks reageert
Een HTTP-trigger Hello _webHookType_ eigenschap worden geconfigureerde toorespond te[webhooks](https://en.wikipedia.org/wiki/Webhook). Hallo-basisconfiguratie gebruikt Hallo 'genericJson' instelling. Hiermee beperkt u aanvragen tooonly die via HTTP POST en Hello `application/json` inhoudstype.

Hallo trigger kan ook worden aangepast tooa specifieke webhook provider (bijv, [GitHub](https://developer.github.com/webhooks/) en [Slack](https://api.slack.com/outgoing-webhooks)). Als een provider is opgegeven, kan runtime van Functions Hallo behandelen validatielogica Hallo-provider voor u.  

### <a name="configuring-github-as-a-webhook-provider"></a>GitHub als een webhook-provider configureren
toorespond tooGitHub webhooks, eerst uw functie te maken met een HTTP-Trigger en stel Hallo _webHookType_ eigenschap te 'github'. Kopieer de [URL](#url) en [API-sleutel](#keys) in uw GitHub-opslagplaats **webhook toevoegen** pagina. Zie de GitHub [Webhooks maken](http://go.microsoft.com/fwlink/?LinkID=761099&clcid=0x409) documentatie voor meer informatie.

![](./media/functions-bindings-http-webhook/github-add-webhook.png)

### <a name="configuring-slack-as-a-webhook-provider"></a>Vertraging configureren als een webhook-provider
Hallo toegestane webhook genereert een token voor u in plaats van waarin u kunt opgeven, dus u een sleutel functiespecifieke met Hallo-token van de toegestane vertraging configureren moet. Zie [werken met sleutels](#keys).

<a name="url"></a>
## <a name="customizing-hello-http-endpoint"></a>Hallo HTTP-eindpunt aanpassen
Wanneer u een functie voor een HTTP-trigger of WebHook, is Hallo-functie standaard adresseerbare met een route Hallo vorm:

    http://<yourapp>.azurewebsites.net/api/<funcname> 

U kunt deze route met optionele Hallo `route` -eigenschap op Hallo HTTP-trigger binding de invoer. Als u bijvoorbeeld Hallo na *function.json* -bestand definieert een `route` eigenschap voor een HTTP-trigger:

```json
    {
      "bindings": [
        {
          "type": "httpTrigger",
          "name": "req",
          "direction": "in",
          "methods": [ "get" ],
          "route": "products/{category:alpha}/{id:int?}"
        },
        {
          "type": "http",
          "name": "res",
          "direction": "out"
        }
      ]
    }
```

Met deze configuratie, is Hallo-functie nu adresseerbare Hello route in plaats van de oorspronkelijke route hello te volgen.

    http://<yourapp>.azurewebsites.net/api/products/electronics/357

Hierdoor kan de functiecode Hallo toosupport twee parameters in het Hallo-adres, 'categorie' en 'id'. U kunt een [Web API Route beperking](https://www.asp.net/web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2#constraints) met de parameters. Hallo volgende C#-functiecode maakt gebruik van beide parameters.

```csharp
    public static Task<HttpResponseMessage> Run(HttpRequestMessage req, string category, int? id, 
                                                    TraceWriter log)
    {
        if (id == null)
           return  req.CreateResponse(HttpStatusCode.OK, $"All {category} items were requested.");
        else
           return  req.CreateResponse(HttpStatusCode.OK, $"{category} item with id = {id} has been requested.");
    }
```

Hier volgt Node.js functie code toouse Hallo dezelfde Routeparameters.

```javascript
    module.exports = function (context, req) {

        var category = context.bindingData.category;
        var id = context.bindingData.id;

        if (!id) {
            context.res = {
                // status: 200, /* Defaults too200 */
                body: "All " + category + " items were requested."
            };
        }
        else {
            context.res = {
                // status: 200, /* Defaults too200 */
                body: category + " item with id = " + id + " was requested."
            };
        }

        context.done();
    } 
```

Standaard worden alle routes van de functie voorafgegaan door *api*. U kunt ook aanpassen of verwijderen van Hallo-adresvoorvoegsel dat gebruikmaakt van Hallo `http.routePrefix` eigenschap in uw *host.json* bestand. Hallo volgende voorbeeld wordt verwijderd Hallo *api* routeprefix met behulp van een lege tekenreeks voor Hallo-voorvoegsel in Hallo *host.json* bestand.

```json
    {
      "http": {
        "routePrefix": ""
      }
    }
```

Voor gedetailleerde informatie over het tooupdate hello *host.json* -bestand voor de functie, Zie [hoe de app-bestanden voor het functioneren van tooupdate](functions-reference.md#fileupdate). 

Voor informatie over andere eigenschappen kunt u configureren uw *host.json* bestand, Zie [host.json verwijzing](https://github.com/Azure/azure-webjobs-sdk-script/wiki/host.json).


<a name="keys"></a>
## <a name="working-with-keys"></a>Werken met sleutels
HttpTriggers kunt gebruikmaken van sleutels voor extra beveiliging. Een standaard HttpTrigger kunt deze als een API-sleutel gebruiken sleutel toobe Hallo aanwezig is op verzoek Hallo vereisen. Webhooks kunt sleutels tooauthorize aanvragen in verschillende manieren, afhankelijk van welke Hallo-provider ondersteunt.

Sleutels worden opgeslagen als onderdeel van de functie-app in Azure en zijn versleuteld in rust. tooview uw sleutels, maakt u nieuwe of draai sleutels toonew waarden, gaat u tooone van uw functies binnen Hallo-portal en selecteert u 'Beheren'. 

Er zijn twee soorten sleutels:
- **Hostsleutels**: deze sleutels worden gedeeld door alle functies binnen Hallo functie-app. Wanneer als een API-sleutel gebruikt, kunnen deze functie voor toegang tot tooany binnen Hallo functie-app.
- **Functietoetsen**: deze sleutels toepassen alleen toohello specifieke functies waarin ze zijn gedefinieerd. Wanneer als een API-sleutel gebruikt, kan deze alleen toegang toothat functie.

Elke sleutel met de naam voor de verwijzing en er is een standaard-sleutel (met de naam 'standaard') op Hallo-functie en host-niveau. Hallo **hoofdsleutel** een standaard host-sleutel is met de naam '_master' die is gedefinieerd voor elke functie-app en kan niet worden ingetrokken. Het biedt beheerderstoegang toohello runtime-API's. Met behulp van `"authLevel": "admin"` in Hallo JSON binding vereist deze sleutel toobe die wordt weergegeven op Hallo aanvraag; een andere toets resulteert in een mislukte verificatiepogingen.

> [!NOTE]
> Vervaldatum toohello verhoogde machtigingen verleend door hoofdsleutel hello, u dient deze sleutel delen met derden of distribueren in systeemeigen clienttoepassingen. Wees voorzichtig bij het kiezen van Hallo beheerder autorisatieniveau.
> 
> 

### <a name="api-key-authorization"></a>API-sleutel autorisatie
Een HttpTrigger moet standaard een API-sleutel in Hallo HTTP-aanvraag. Dus de HTTP-aanvraag normaal ziet er als volgt:

    https://<yourapp>.azurewebsites.net/api/<function>?code=<ApiKey>

Hallo-sleutel kan worden opgenomen in een queryreeks-variabele met de naam `code`, zoals hierboven, of kan worden opgenomen in een `x-functions-key` HTTP-header. Hallo-waarde van Hallo sleutel mag een gedefinieerd voor de functie Hallo functietoets of op een host-toets.

U kunt kiezen tooallow aanvragen zonder sleutels of opgeven die hoofdsleutel Hallo moet worden gebruikt door het wijzigen van Hallo `authLevel` eigenschap in JSON-binding hello (Zie [HTTP-trigger](#httptrigger)).

### <a name="keys-and-webhooks"></a>Sleutels en webhooks.
Webhook-autorisatie is verwerkt door Hallo webhook reciever onderdeel, deel van Hallo HttpTrigger en Hallo mechanisme varieert op basis van Hallo webhook type. Elke mechanisme komt, maar afhankelijk zijn van een sleutel. Standaard wordt Hallo functie sleutel met de naam 'standaard' gebruikt. Als u op een andere sleutel toouse wenst, moet u tooconfigure hello webhook provider toosend Hallo sleutelnaam met Hallo-aanvraag in een van de volgende manieren Hallo:

- **Querytekenreeks**: Hallo provider doorgeeft Hallo sleutelnaam in Hallo `clientid` querytekenreeksparameter (bijv, `https://<yourapp>.azurewebsites.net/api/<funcname>?clientid=<keyname>`).
- **Aanvraagheader**: Hallo provider doorgeeft Hallo sleutelnaam in Hallo `x-functions-clientid` header.

> [!NOTE]
> Functietoetsen hebben voorrang op de hostsleutels. Als twee sleutels zijn gedefinieerd met dezelfde naam, Hallo Hallo functietoets wordt gebruikt.
> 
> 


<a name="httptriggersample"></a>
## <a name="http-trigger-samples"></a>Voorbeelden van HTTP-trigger
Stel dat er na HTTP-trigger in Hallo Hallo `bindings` matrix van function.json:

```json
{
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
    "authLevel": "function"
},
```

Zie Hallo taalspecifieke voorbeeldtoepassing die u zoekt een `name` parameter in de queryreeks Hallo of Hallo hoofdtekst van Hallo HTTP-aanvraag.

* [C#](#httptriggercsharp)
* [F#](#httptriggerfsharp)
* [Node.js](#httptriggernodejs)


<a name="httptriggercsharp"></a>
### <a name="http-trigger-sample-in-c"></a>Voorbeeld van de HTTP-trigger in C# #
```csharp
using System.Net;
using System.Threading.Tasks;

public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
{
    log.Info($"C# HTTP trigger function processed a request. RequestUri={req.RequestUri}");

    // parse query parameter
    string name = req.GetQueryNameValuePairs()
        .FirstOrDefault(q => string.Compare(q.Key, "name", true) == 0)
        .Value;

    // Get request body
    dynamic data = await req.Content.ReadAsAsync<object>();

    // Set name tooquery string or body data
    name = name ?? data?.name;

    return name == null
        ? req.CreateResponse(HttpStatusCode.BadRequest, "Please pass a name on hello query string or in hello request body")
        : req.CreateResponse(HttpStatusCode.OK, "Hello " + name);
}
```

U kunt ook tooa POCO binden in plaats van `HttpRequestMessage`. Dit wordt gehydrateerd van Hallo instantie van de aanvraag hello, geparseerd als JSON. Op deze manier kan een type worden doorgegeven antwoorduitvoer toohello HTTP-binding en dit wordt geretourneerd als de antwoordtekst Hallo met een statuscode 200.
```csharp
using System.Net;
using System.Threading.Tasks;

public static string Run(CustomObject req, TraceWriter log)
{
    return "Hello " + req?.name;
}

public class CustomObject {
     public String name {get; set;}
}
}
```

<a name="httptriggerfsharp"></a>
### <a name="http-trigger-sample-in-f"></a>Voorbeeld van de HTTP-trigger in F # #
```fsharp
open System.Net
open System.Net.Http
open FSharp.Interop.Dynamic

let Run(req: HttpRequestMessage) =
    async {
        let q =
            req.GetQueryNameValuePairs()
                |> Seq.tryFind (fun kv -> kv.Key = "name")
        match q with
        | Some kv ->
            return req.CreateResponse(HttpStatusCode.OK, "Hello " + kv.Value)
        | None ->
            let! data = Async.AwaitTask(req.Content.ReadAsAsync<obj>())
            try
                return req.CreateResponse(HttpStatusCode.OK, "Hello " + data?name)
            with e ->
                return req.CreateErrorResponse(HttpStatusCode.BadRequest, "Please pass a name on hello query string or in hello request body")
    } |> Async.StartAsTask
```

U moet een `project.json` bestand met NuGet tooreference hello `FSharp.Interop.Dynamic` en `Dynamitey` assembly's, als volgt:

```json
{
  "frameworks": {
    "net46": {
      "dependencies": {
        "Dynamitey": "1.0.2",
        "FSharp.Interop.Dynamic": "3.0.0"
      }
    }
  }
}
```

Dit NuGet toofetch afhankelijkheden gebruikt en wordt deze in uw script verwijst.

<a name="httptriggernodejs"></a>
### <a name="http-trigger-sample-in-nodejs"></a>Voorbeeld van de HTTP-trigger in Node.JS
```javascript
module.exports = function(context, req) {
    context.log('Node.js HTTP trigger function processed a request. RequestUri=%s', req.originalUrl);

    if (req.query.name || (req.body && req.body.name)) {
        context.res = {
            // status: 200, /* Defaults too200 */
            body: "Hello " + (req.query.name || req.body.name)
        };
    }
    else {
        context.res = {
            status: 400,
            body: "Please pass a name on hello query string or in hello request body"
        };
    }
    context.done();
};
```



<a name="hooktriggersample"></a>
## <a name="webhook-samples"></a>Webhook-voorbeelden
Stel dat er na webhook trigger in Hallo Hallo `bindings` matrix van function.json:

```json
{
    "webHookType": "github",
    "name": "req",
    "type": "httpTrigger",
    "direction": "in",
},
```

Zie Hallo taalspecifieke voorbeeldtoepassing die u GitHub probleem opmerkingen registreert.

* [C#](#hooktriggercsharp)
* [F#](#hooktriggerfsharp)
* [Node.js](#hooktriggernodejs)

<a name="hooktriggercsharp"></a>

### <a name="webhook-sample-in-c"></a>Voorbeeld van de Webhook in C# #
```csharp
#r "Newtonsoft.Json"

using System;
using System.Net;
using System.Threading.Tasks;
using Newtonsoft.Json;

public static async Task<object> Run(HttpRequestMessage req, TraceWriter log)
{
    string jsonContent = await req.Content.ReadAsStringAsync();
    dynamic data = JsonConvert.DeserializeObject(jsonContent);

    log.Info($"WebHook was triggered! Comment: {data.comment.body}");

    return req.CreateResponse(HttpStatusCode.OK, new {
        body = $"New GitHub comment: {data.comment.body}"
    });
}
```

<a name="hooktriggerfsharp"></a>

### <a name="webhook-sample-in-f"></a>Voorbeeld van de Webhook in F # #
```fsharp
open System.Net
open System.Net.Http
open FSharp.Interop.Dynamic
open Newtonsoft.Json

type Response = {
    body: string
}

let Run(req: HttpRequestMessage, log: TraceWriter) =
    async {
        let! content = req.Content.ReadAsStringAsync() |> Async.AwaitTask
        let data = content |> JsonConvert.DeserializeObject
        log.Info(sprintf "GitHub WebHook triggered! %s" data?comment?body)
        return req.CreateResponse(
            HttpStatusCode.OK,
            { body = sprintf "New GitHub comment: %s" data?comment?body })
    } |> Async.StartAsTask
```

<a name="hooktriggernodejs"></a>

### <a name="webhook-sample-in-nodejs"></a>Voorbeeld van de Webhook in Node.JS
```javascript
module.exports = function (context, data) {
    context.log('GitHub WebHook triggered!', data.comment.body);
    context.res = { body: 'New GitHub comment: ' + data.comment.body };
    context.done();
};
```


## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

