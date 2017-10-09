---
title: aaaWork met triggers en bindingen in de Azure Functions | Microsoft Docs
description: Informatie over hoe toouse triggers en bindingen in de Azure Functions tooconnect uw code uitvoering tooonline gebeurtenissen en cloud-gebaseerde services.
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: Azure-functies, functies, gebeurtenisverwerking, webhooks, dynamisch berekenen, architectuur zonder server
ms.assetid: cbc7460a-4d8a-423f-a63e-1cd33fef7252
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/30/2017
ms.author: donnam
ms.openlocfilehash: eb2ebfca172fcc8c0f479adbcfec99e90fc33615
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-triggers-and-bindings-concepts"></a>Azure Functions-triggers en bindingen concepten
Azure Functions kunt u toowrite code in het antwoord tooevents in Azure en andere services via *triggers* en *bindingen*. Dit artikel is een conceptueel overzicht van triggers en bindingen voor alle programmeertalen worden ondersteund. Functies die algemene tooall bindingen zijn worden hier beschreven.

## <a name="overview"></a>Overzicht

Triggers en bindingen zijn een declaratieve manier toodefine hoe een functie is aangeroepen en welke gegevens het werkt met. Een *trigger* definieert hoe een functie wordt aangeroepen. Een functie moet exact één trigger hebben. Triggers hebt gekoppeld aan gegevens, die is gewoonlijk het Hallo-nettolading waarmee Hallo-functie is geactiveerd. 

Invoer en uitvoer *bindingen* bieden een declaratieve manier tooconnect toodata vanuit uw code. Vergelijkbare tootriggers, geeft u verbindingsreeksen en andere eigenschappen in de configuratie van de functie. Bindingen zijn optioneel en een functie kunt meerdere invoer en uitvoer bindingen. 

Met triggers en bindingen kunt u code die is meer algemeen en heeft dit geen hardcode Hallo details over Hallo services waarmee deze communiceert schrijven. Gegevens die afkomstig zijn van de invoerwaarden services simpelweg zijn voor uw functiecode. toooutput gegevensservice tooanother (zoals het maken van een nieuwe rij in de Azure Table Storage), gebruik Hallo geretourneerde waarde van Hallo-methode. Of als u toooutput meerdere waarden moet, gebruikt u een helperobject. Triggers en bindingen hebben een **naam** eigenschap, die een id die u in uw code tooaccess Hallo-binding gebruiken.

U kunt triggers en bindingen configureren in Hallo **integreren** tabblad in hello Azure Functions-portal. Onder Hallo-dekt Hallo gebruikersinterface een bestand met de naam wijzigt *function.json* in Hallo functie map. U kunt dit bestand bewerken door het wijzigen van toohello **geavanceerde editor**.

Hallo volgende tabel toont Hallo triggers en bindingen die worden ondersteund door Azure Functions. 

[!INCLUDE [Full bindings table](../../includes/functions-bindings.md)]

### <a name="example-queue-trigger-and-table-output-binding"></a>Voorbeeld: wachtrij trigger en tabel uitvoer binding

Stel dat u een nieuwe rij tooAzure Table Storage toowrite wilt zien wanneer een nieuw bericht wordt weergegeven in Azure Queue Storage. Dit scenario kan worden geïmplementeerd met behulp van een Azure-wachtrij trigger en een tabel uitvoer binding. 

Een trigger wachtrij vereist Hallo volgende informatie in Hallo **integreren** tabblad:

* Hallo-naam van app-instelling voor Hallo Hallo account verbindingsreeks voor opslag voor Hallo wachtrij met
* de wachtrijnaam Hallo
* Hallo-id in de inhoud van uw code tooread Hallo van wachtrij het Hallo-bericht, zoals `order`.

een binding uitvoer toowrite tooAzure Table Storage gebruiken met Hallo volgende details:

* Hallo-naam van app-instelling voor Hallo Hallo account verbindingsreeks voor opslag voor Hallo tabel met
* Hallo-tabelnaam
* Hallo-id in uw code toocreate items of Hallo geretourneerde waarde van Hallo-functie uitvoert.

Bindingen app-instellingen gebruiken voor verbinding tekenreeksen tooenforce Hallo beste praktijk die *function.json* bevat geen geheimen van de service.

Gebruik vervolgens Hallo-id's die u opgaf toointegrate met Azure Storage in uw code.

```cs
#r "Newtonsoft.Json"

using Newtonsoft.Json.Linq;

// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello method return value creates a new row in Table Storage
public static Person Run(JObject order, TraceWriter log)
{
    return new Person() { 
            PartitionKey = "Orders", 
            RowKey = Guid.NewGuid().ToString(),  
            Name = order["Name"].ToString(),
            MobileNumber = order["MobileNumber"].ToString() };  
}
 
public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
    public string MobileNumber { get; set; }
}
```

```javascript
// From an incoming queue message that is a JSON object, add fields and write tooTable Storage
// hello second parameter toocontext.done is used as hello value for hello new row
module.exports = function (context, order) {
    order.PartitionKey = "Orders";
    order.RowKey = generateRandomId(); 

    context.done(null, order);
};

function generateRandomId() {
    return Math.random().toString(36).substring(2, 15) +
        Math.random().toString(36).substring(2, 15);
}
```

Hier volgt Hallo *function.json* die overeenkomt met toohello voorafgaand aan code. Houd er rekening mee dat dezelfde configuratie kan worden gebruikt, ongeacht de taal van functie-implementatie Hallo HALLO hallo.

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "myqueue-items",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    },
    {
      "name": "$return",
      "type": "table",
      "direction": "out",
      "tableName": "outTable",
      "connection": "MY_TABLE_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```
inhoud van de Hallo tooview en bewerken van *function.json* in hello Azure-portal, klikt u op Hallo **geavanceerde editor** optie op Hallo **integreren** tabblad van de functie.

Zie voor meer voorbeelden van code en meer informatie over de integratie met Azure Storage [Azure Functions triggers en bindingen voor Azure Storage](functions-bindings-storage.md).

### <a name="binding-direction"></a>Richting van de binding

Alle triggers en bindingen hebben een `direction` eigenschap:

- Voor triggers is Hallo richting altijd`in`
- Invoer- en uitvoergegevens bindingen gebruiken `in` en`out`
- Sommige bindingen ondersteuning voor een speciale richting `inout`. Als u `inout`, alleen Hallo **geavanceerde editor** is beschikbaar in Hallo **integreren** tabblad.

## <a name="using-hello-function-return-type-tooreturn-a-single-output"></a>Met behulp van Hallo functie retourtype tooreturn één uitvoer

Hallo voorgaande voorbeeld ziet u hoe toouse Hallo functie retourwaarde tooprovide tooa binding die wordt bereikt door middel van de speciale parameter Hallo uitvoer `$return`. (Dit wordt alleen ondersteund in de talen die u een retourwaarde, zoals C#, JavaScript en F hebt #.) Als een functie meerdere bindingen van de uitvoer heeft, gebruikt u `$return` voor slechts één Hallo uitvoer bindingen. 

```json
// excerpt of function.json
{
    "name": "$return",
    "type": "blob",
    "direction": "out",
    "path": "output-container/{id}"
}
```

Hallo-voorbeelden hieronder tonen retourneren hoe typen worden gebruikt met bindingen in C#, JavaScript en F # uitvoer.

```cs
// C# example: use method return value for output binding
public static string Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```cs
// C# example: async method, using return value for output binding
public static Task<string> Run(WorkItem input, TraceWriter log)
{
    string json = string.Format("{{ \"id\": \"{0}\" }}", input.Id);
    log.Info($"C# script processed queue message. Item={json}");
    return json;
}
```

```javascript
// JavaScript: return a value in hello second parameter toocontext.done
module.exports = function (context, input) {
    var json = JSON.stringify(input);
    context.log('Node.js script processed queue message', json);
    context.done(null, json);
}
```

```fsharp
// F# example: use return value for output binding
let Run(input: WorkItem, log: TraceWriter) =
    let json = String.Format("{{ \"id\": \"{0}\" }}", input.Id)   
    log.Info(sprintf "F# script processed queue message '%s'" json)
    json
```

## <a name="binding-datatype-property"></a>De eigenschap dataType binding

Gebruik in .NET Hallo typen toodefine Hallo-gegevenstype voor invoergegevens. Gebruik bijvoorbeeld `string` toobind toohello tekst van de trigger van een wachtrij en een byte-matrix tooread als binair.

Gebruik voor de talen die dynamisch worden getypeerd zoals JavaScript, Hallo `dataType` eigenschap in de definitie van de binding Hallo. Bijvoorbeeld: tooread Hallo inhoud van een HTTP-aanvraag in binaire indeling, gebruik Hallo type `binary`:

```json
{
    "type": "httpTrigger",
    "name": "req",
    "direction": "in",
    "dataType": "binary"
}
```

Andere opties voor `dataType` zijn `stream` en `string`.

## <a name="resolving-app-settings"></a>Het omzetten van app-instellingen
Als een best practice moeten geheimen en verbindingsreeksen worden beheerd met behulp van app-instellingen, in plaats van configuratiebestanden. Dit beperkt toegang toothese geheimen en maakt het veilige toostore *function.json* in een openbare resourcebeheerbibliotheek.

App-instellingen zijn ook handig wanneer u wilt dat toochange configuratie op basis van Hallo-omgeving. In een testomgeving kunt u bijvoorbeeld toomonitor een andere wachtrij of blob storage-container.

Appinstellingen zijn opgelost wanneer een waarde procenttekens, zoals tussen `%MyAppSetting%`. Houd er rekening mee dat Hallo `connection` eigenschap van triggers en bindingen is een speciaal geval en -waarden als de app-instellingen automatisch worden opgelost. 

Hallo volgende voorbeeld wordt een wachtrij-trigger die gebruikmaakt van een app-instelling `%input-queue-name%` toodefine Hallo wachtrij tootrigger op.

```json
{
  "bindings": [
    {
      "name": "order",
      "type": "queueTrigger",
      "direction": "in",
      "queueName": "%input-queue-name%",
      "connection": "MY_STORAGE_ACCT_APP_SETTING"
    }
  ]
}
```

## <a name="trigger-metadata-properties"></a>Eigenschappen van de trigger-metagegevens

In de nettolading voor toevoeging toohello geleverd door een trigger (zoals Hallo wachtrijbericht waarmee een functie is geactiveerd), veel triggers bieden aanvullende metagegevenswaarden. Deze waarden kunnen worden gebruikt als de invoerparameters in C# en F # of eigenschappen op Hallo `context.bindings` -object in JavaScript. 

Een wachtrij-trigger ondersteunt bijvoorbeeld Hallo volgende eigenschappen:

* QueueTrigger - activering van de inhoud van het bericht als een geldige tekenreeks
* DequeueCount
* expirationTime
* Id
* InsertionTime
* NextVisibleTime
* PopReceipt

Details van de eigenschappen van de metagegevens voor elke trigger worden beschreven in de bijbehorende naslagonderwerp Hallo. Documentatie is ook beschikbaar in Hallo **integreren** tabblad van het Hallo-portal in Hallo **documentatie** hieronder configuratiegebied Hallo-binding.  

Bijvoorbeeld, omdat het blob-triggers vertragingen voordoen, kunt u een wachtrij trigger toorun uw-functie (Zie [Blob Storage Trigger](functions-bindings-storage-blob.md#storage-blob-trigger). Hallo-bericht van wachtrij zou Hallo blob filename tootrigger op bevatten. Met behulp van Hallo `queueTrigger` metagegevenseigenschap, kunt u dit gedrag in uw configuratie, in plaats van uw code.

```json
  "bindings": [
    {
      "name": "myQueueItem",
      "type": "queueTrigger",
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
    },
    {
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "direction": "in",
      "connection": "MyStorageConnection"
    }
  ]
```

Eigenschappen van de metagegevens van een trigger kunnen ook worden gebruikt een *bindende expressie* voor een andere binding, als beschreven in Hallo volgende sectie.

## <a name="binding-expressions-and-patterns"></a>Expressies voor gegevensbinding en patronen

Een van de meest krachtige functies Hallo van triggers en bindingen is *bindingsexpressies*. U kunt patroon expressies die vervolgens kunnen worden gebruikt binnen uw binding definiëren in andere bindingen of uw code. Metagegevens van de trigger kan ook worden gebruikt in expressies als weergeven in voorbeeld in de voorgaande sectie Hallo Hallo binding.

Stel bijvoorbeeld dat u wilt dat tooresize afbeeldingen in bepaalde blob storage-container, vergelijkbare toohello **Image-aanwijzer Formaat** sjabloon in Hallo **nieuwe functie** pagina. Ga te**nieuwe functie** -> taal **C#** -> Scenario **voorbeelden** -> **ImageResizer CSharp**. 

Hier volgt Hallo *function.json* definitie:

```json
{
  "bindings": [
    {
      "name": "image",
      "type": "blobTrigger",
      "path": "sample-images/{filename}",
      "direction": "in",
      "connection": "MyStorageConnection"
    },
    {
      "name": "imageSmall",
      "type": "blob",
      "path": "sample-images-sm/{filename}",
      "direction": "out",
      "connection": "MyStorageConnection"
    }
  ],
}
```

U ziet dat Hallo `filename` parameter wordt gebruikt in zowel de definitie van de trigger blob Hallo als Hallo blob uitvoer van de binding. Deze parameter kan ook worden gebruikt in de functiecode.

```csharp
// C# example of binding too{filename}
public static void Run(Stream image, string filename, Stream imageSmall, TraceWriter log)  
{
    log.Info($"Blob trigger processing: {filename}");
    // ...
} 
```

<!--TODO: add JavaScript example -->
<!-- Blocked by bug https://github.com/Azure/Azure-Functions/issues/248 -->


### <a name="random-guids"></a>Willekeurige GUID 's
Azure Functions bevat een gemak-syntaxis voor het genereren van GUID's in uw bindingen, via Hallo `{rand-guid}` bindende expressie. Hallo wordt volgende voorbeeld een unieke blob-naam van deze toogenerate: 

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{rand-guid}"
}
```

### <a name="current-time"></a>Huidige tijd

U kunt een expressie voor gegevensbinding Hallo `DateTime`, die wordt omgezet te`DateTime.UtcNow`.

```json
{
  "type": "blob",
  "name": "blobOutput",
  "direction": "out",
  "path": "my-output-container/{DateTime}"
}
```

## <a name="bind-toocustom-input-properties-in-a-binding-expression"></a>Invoereigenschappen toocustom binding in een expressie voor gegevensbinding

Bindingsexpressies kan ook verwijzen naar eigenschappen die zijn gedefinieerd in Hallo trigger nettolading zelf. U kunt bijvoorbeeld toodynamically bind tooa blob storage-bestand van een bestandsnaam is opgegeven in een webhook.

Bijvoorbeeld Hallo na *function.json* maakt gebruik van een eigenschap genaamd `BlobName` van Hallo trigger nettolading:

```json
{
  "bindings": [
    {
      "name": "info",
      "type": "httpTrigger",
      "direction": "in",
      "webHookType": "genericJson",
    },
    {
      "name": "blobContents",
      "type": "blob",
      "direction": "in",
      "path": "strings/{BlobName}",
      "connection": "AzureWebJobsStorage"
    },
    {
      "name": "res",
      "type": "http",
      "direction": "out"
    }
  ]
}
```

tooaccomplish deze in C#- en F #, moet u een POCO die definieert Hallo velden die zullen worden gedeserialiseerd in Hallo trigger nettolading definiëren.

```csharp
using System.Net;

public class BlobInfo
{
    public string BlobName { get; set; }
}
  
public static HttpResponseMessage Run(HttpRequestMessage req, BlobInfo info, string blobContents)
{
    if (blobContents == null) {
        return req.CreateResponse(HttpStatusCode.NotFound);
    } 

    return req.CreateResponse(HttpStatusCode.OK, new {
        data = $"{blobContents}"
    });
}
```

JSON-deserialisatie wordt automatisch uitgevoerd in JavaScript, en kunt u rechtstreeks Hallo eigenschappen gebruiken.

```javascript
module.exports = function (context, info) {
    if ('BlobName' in info) {
        context.res = {
            body: { 'data': context.bindings.blobContents }
        }
    }
    else {
        context.res = {
            status: 404
        };
    }
    context.done();
}
```

## <a name="configuring-binding-data-at-runtime"></a>Configureren van die gegevens bindt tijdens runtime

In C# en andere .NET-talen, kunt u een patroon imperatieve binding gebruiken als declaratieve bindingen in tegenstelling tot toohello *function.json*. Imperatieve binding is handig als bindparameters toobe berekend tijdens runtime in plaats van ontwerp moeten. toolearn meer, Zie [Binding tijdens runtime via imperatieve bindingen](functions-reference-csharp.md#imperative-bindings) in Hallo C#-referentie voor ontwikkelaars.

## <a name="next-steps"></a>Volgende stappen
Zie voor meer informatie over een specifieke binding Hallo artikelen te volgen:

- [HTTP en webhooks](functions-bindings-http-webhook.md)
- [Timer](functions-bindings-timer.md)
- [Queue Storage](functions-bindings-storage-queue.md)
- [Blob Storage](functions-bindings-storage-blob.md)
- [Table Storage](functions-bindings-storage-table.md)
- [Event Hub](functions-bindings-event-hubs.md)
- [Service Bus](functions-bindings-service-bus.md)
- [Cosmos DB](functions-bindings-documentdb.md)
- [SendGrid](functions-bindings-sendgrid.md)
- [Twilio](functions-bindings-twilio.md)
- [Notification Hubs](functions-bindings-notification-hubs.md)
- [Mobile Apps](functions-bindings-mobile-apps.md)
- [Extern bestand](functions-bindings-external-file.md)
