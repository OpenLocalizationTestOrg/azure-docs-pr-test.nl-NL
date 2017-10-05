---
title: Azure Functions Cosmos DB bindingen | Microsoft Docs
description: Begrijpen hoe Azure Cosmos DB bindingen in de Azure Functions.
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: Azure functions, functies, verwerking van gebeurtenissen, dynamische compute zonder server architectuur
ms.assetid: 3d8497f0-21f3-437d-ba24-5ece8c90ac85
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 04/18/2016
ms.author: glenga
ms.openlocfilehash: de95b0591eb95e76dbb7ba2382e9e14e1f66cda1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-cosmos-db-bindings"></a>Azure Functions Cosmos DB bindingen
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Dit artikel wordt uitgelegd hoe u configureert en bindingen van Azure DB die Cosmos code in Azure Functions. Azure Functions ondersteunt invoer en uitvoer van de bindingen voor Cosmos-DB.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Zie voor meer informatie over Cosmos DB [Inleiding tot Cosmos DB](../documentdb/documentdb-introduction.md) en [een Cosmos-DB-consoletoepassing bouwen](../documentdb/documentdb-get-started.md).

<a id="docdbinput"></a>

## <a name="documentdb-api-input-binding"></a>DocumentDB-API invoer binding
De invoer DocumentDB API-binding een Cosmos-DB-document opgehaald en doorgegeven aan de benoemde invoerparameter van de functie. De ID kan worden bepaald document is gebaseerd op de trigger die de functie activeert. 

De invoer DocumentDB API-binding heeft de volgende eigenschappen *function.json*:

- `name`: De id die wordt gebruikt in de functiecode voor het document
- `type`: moet worden ingesteld op 'documentdb'
- `databaseName`: De database met het document
- `collectionName`: De verzameling met het document
- `id`: De Id van het document om op te halen. Deze eigenschap ondersteunt de bindingen van parameters. Zie [binden aan aangepaste eigenschappen voor de invoer in een expressie voor gegevensbinding](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) in het artikel [Azure Functions triggers en bindingen concepten](functions-triggers-bindings.md).
- `sqlQuery`: Een Cosmos DB SQL-query die wordt gebruikt voor het ophalen van meerdere documenten. De query biedt ondersteuning voor runtime-bindingen. Bijvoorbeeld: `SELECT * FROM c where c.departmentId = {departmentId}`
- `connection`: De naam van de app-instelling met de verbindingsreeks van de Cosmos-DB
- `direction`: moet worden ingesteld op `"in"`.

De eigenschappen `id` en `sqlQuery` kunnen niet allebei worden opgegeven. Als geen van beide `id` noch `sqlQuery` is ingesteld, wordt de volledige verzameling worden opgehaald.

## <a name="using-a-documentdb-api-input-binding"></a>Met behulp van een DocumentDB-API invoer binding

* In C# en F # functies, wanneer de functie wordt voltooid, wordt afgesloten worden wijzigingen in het invoerdocument via benoemde invoerparameters automatisch doorgevoerd. 
* In de JavaScript-functies worden niet automatisch updates gesteld bij functie beëindigen. Gebruik in plaats daarvan `context.bindings.<documentName>In` en `context.bindings.<documentName>Out` om updates te maken. Zie de [JavaScript voorbeeld](#injavascript).

<a name="inputsample"></a>

## <a name="input-sample-for-single-document"></a>Invoer voorbeeld voor één document
Stel dat u hebt de volgende invoer DocumentDB API-binding in de `bindings` matrix van function.json:

```json
{
  "name": "inputDocument",
  "type": "documentDB",
  "databaseName": "MyDatabase",
  "collectionName": "MyCollection",
  "id" : "{queueTrigger}",
  "connection": "MyAccount_COSMOSDB",     
  "direction": "in"
}
```

Zie de taalspecifieke-voorbeeldtoepassing die u deze invoer binding gebruikt voor het bijwerken van de tekstwaarde van het document.

* [C#](#incsharp)
* [F#](#infsharp)
* [JavaScript](#injavascript)

<a name="incsharp"></a>
### <a name="input-sample-in-c"></a>Invoer voorbeeld in C# #

```cs
// Change input document contents using DocumentDB API input binding 
public static void Run(string myQueueItem, dynamic inputDocument)
{   
  inputDocument.text = "This has changed.";
}
```
<a name="infsharp"></a>

### <a name="input-sample-in-f"></a>Invoer voorbeeld in F # #

```fsharp
(* Change input document contents using DocumentDB API input binding *)
open FSharp.Interop.Dynamic
let Run(myQueueItem: string, inputDocument: obj) =
  inputDocument?text <- "This has changed."
```

Dit voorbeeld vereist een `project.json` -bestand dat Hiermee geeft u de `FSharp.Interop.Dynamic` en `Dynamitey` NuGet afhankelijkheden:

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

Om toe te voegen een `project.json` bestand, Zie [F # pakket management](functions-reference-fsharp.md#package).

<a name="injavascript"></a>

### <a name="input-sample-in-javascript"></a>Invoer voorbeeld in JavaScript

```javascript
// Change input document contents using DocumentDB API input binding, using context.bindings.inputDocumentOut
module.exports = function (context) {   
  context.bindings.inputDocumentOut = context.bindings.inputDocumentIn;
  context.bindings.inputDocumentOut.text = "This was updated!";
  context.done();
};
```

## <a name="input-sample-with-multiple-documents"></a>Invoer voorbeeld met meerdere documenten

Stel dat u ophalen van meerdere documenten die zijn opgegeven met een SQL-query met behulp van een wachtrij-trigger wilt voor het aanpassen van de queryparameters. 

In dit voorbeeld wordt de trigger wachtrij een parameter opgegeven `departmentId`. Een wachtrijbericht van `{ "departmentId" : "Finance" }` alle records voor de afdeling Financiën zou retourneren. Gebruik de volgende in *function.json*:

```
{
    "name": "documents",
    "type": "documentdb",
    "direction": "in",
    "databaseName": "MyDb",
    "collectionName": "MyCollection",
    "sqlQuery": "SELECT * from c where c.departmentId = {departmentId}"
    "connection": "CosmosDBConnection"
}
```

### <a name="input-sample-with-multiple-documents-in-c"></a>Invoer voorbeeld met meerdere documenten in C#

```csharp
public static void Run(QueuePayload myQueueItem, IEnumerable<dynamic> documents)
{   
    foreach (var doc in documents)
    {
        // operate on each document
    }    
}

public class QueuePayload
{
    public string departmentId { get; set; }
}
```

### <a name="input-sample-with-multiple-documents-in-javascript"></a>Invoer voorbeeld met meerdere documenten in JavaScript

```javascript
module.exports = function (context, input) {    
    var documents = context.bindings.documents;
    for (var i = 0; i < documents.length; i++) {
        var document = documents[i];
        // operate on each document
    }       
    context.done();
};
```

## <a id="docdboutput"></a>DocumentDB-API uitvoer binding
De uitvoer van de DocumentDB-API binding kunt schrijven u een nieuw document naar een Azure DB die Cosmos-database. Deze heeft de volgende eigenschappen in *function.json*:

- `name`: De id die is gebruikt in de functiecode voor het nieuwe document
- `type`: moet worden ingesteld op`"documentdb"`
- `databaseName`: De database met de verzameling waar het nieuwe document wordt gemaakt.
- `collectionName`: De verzameling waar het nieuwe document wordt gemaakt.
- `createIfNotExists`: Een Booleaanse waarde om aan te geven of de verzameling wordt gemaakt als deze niet bestaat. De standaardwaarde is *false*. De reden voor deze bewerking nieuwe is verzamelingen worden gemaakt met gereserveerde doorvoer, wat gevolgen heeft. Voor meer informatie raadpleegt u de [pagina met prijzen](https://azure.microsoft.com/pricing/details/documentdb/).
- `connection`: De naam van de app-instelling met de verbindingsreeks van de Cosmos-DB
- `direction`: moet worden ingesteld op`"out"`

## <a name="using-a-documentdb-api-output-binding"></a>Binding met een DocumentDB-API uitvoer
Deze sectie wordt beschreven hoe u uw DocumentDB-API-uitvoer in uw functiecode binding.

Bij het schrijven naar de output-parameter in de functie standaard wordt een nieuw document gegenereerd in de database, met een automatisch gegenereerde GUID als het document-ID. U kunt de document-ID van uitvoerdocument opgeven door te geven de `id` JSON-eigenschap in de output-parameter. 

>[!Note]  
>Wanneer u de ID van een bestaand document opgeeft, wordt deze door het nieuwe uitvoerdocument overschreven. 

Als u wilt uitvoeren op meerdere documenten, kunt u ook binden aan `ICollector<T>` of `IAsyncCollector<T>` waar `T` is een van de ondersteunde typen.

<a name="outputsample"></a>

## <a name="documentdb-api-output-binding-sample"></a>DocumentDB-API uitvoer binding-voorbeeld
Stel dat u hebt de volgende DocumentDB API uitvoer binding in de `bindings` matrix van function.json:

```json
{
  "name": "employeeDocument",
  "type": "documentDB",
  "databaseName": "MyDatabase",
  "collectionName": "MyCollection",
  "createIfNotExists": true,
  "connection": "MyAccount_COSMOSDB",     
  "direction": "out"
}
```

En u een wachtrij invoer binding voor een wachtrij die JSON in de volgende indeling ontvangt hebben:

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

En u wilt Cosmos DB documenten in de volgende notatie voor elke record te maken:

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

Zie het voorbeeld taalspecifieke die gebruikmaakt van deze binding uitvoer documenten toevoegen aan uw database.

* [C#](#outcsharp)
* [F#](#outfsharp)
* [JavaScript](#outjavascript)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Voorbeeld van uitvoer in C# #

```cs
#r "Newtonsoft.Json"

using System;
using Newtonsoft.Json;
using Newtonsoft.Json.Linq;

public static void Run(string myQueueItem, out object employeeDocument, TraceWriter log)
{
  log.Info($"C# Queue trigger function processed: {myQueueItem}");

  dynamic employee = JObject.Parse(myQueueItem);

  employeeDocument = new {
    id = employee.name + "-" + employee.employeeId,
    name = employee.name,
    employeeId = employee.employeeId,
    address = employee.address
  };
}
```

<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a>Voorbeeld van uitvoer in F # #

```fsharp
open FSharp.Interop.Dynamic
open Newtonsoft.Json

type Employee = {
  id: string
  name: string
  employeeId: string
  address: string
}

let Run(myQueueItem: string, employeeDocument: byref<obj>, log: TraceWriter) =
  log.Info(sprintf "F# Queue trigger function processed: %s" myQueueItem)
  let employee = JObject.Parse(myQueueItem)
  employeeDocument <-
    { id = sprintf "%s-%s" employee?name employee?employeeId
      name = employee?name
      employeeId = employee?employeeId
      address = employee?address }
```

Dit voorbeeld vereist een `project.json` -bestand dat Hiermee geeft u de `FSharp.Interop.Dynamic` en `Dynamitey` NuGet afhankelijkheden:

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

Om toe te voegen een `project.json` bestand, Zie [F # pakket management](functions-reference-fsharp.md#package).

<a name="outjavascript"></a>

### <a name="output-sample-in-javascript"></a>Voorbeeld van uitvoer in JavaScript

```javascript
module.exports = function (context) {

  context.bindings.employeeDocument = JSON.stringify({ 
    id: context.bindings.myQueueItem.name + "-" + context.bindings.myQueueItem.employeeId,
    name: context.bindings.myQueueItem.name,
    employeeId: context.bindings.myQueueItem.employeeId,
    address: context.bindings.myQueueItem.address
  });

  context.done();
};
```
