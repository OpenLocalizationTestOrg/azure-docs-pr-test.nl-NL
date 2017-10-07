---
title: aaaAzure functies Cosmos DB bindingen | Microsoft Docs
description: Begrijpen hoe toouse Azure Cosmos DB bindingen in de Azure Functions.
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
ms.openlocfilehash: 76b89e8296db1dd28dff9528903b1f6a28f55232
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-cosmos-db-bindings"></a>Azure Functions Cosmos DB bindingen
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Dit artikel wordt uitgelegd hoe Azure DB die Cosmos-bindingen voor tooconfigure en code in Azure Functions. Azure Functions ondersteunt invoer en uitvoer van de bindingen voor Cosmos-DB.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Zie voor meer informatie over Cosmos DB [inleiding tooCosmos DB](../documentdb/documentdb-introduction.md) en [een Cosmos-DB-consoletoepassing bouwen](../documentdb/documentdb-get-started.md).

<a id="docdbinput"></a>

## <a name="documentdb-api-input-binding"></a>DocumentDB-API invoer binding
Hallo DocumentDB API invoer binding een Cosmos-DB-document opgehaald en doorgegeven toohello invoerparameter van het Hallo-functie met de naam. Hallo-document-ID kan worden vastgesteld gebaseerd op Hallo-trigger die Hallo-functie roept. 

Hallo invoer DocumentDB API-binding heeft Hallo volgende eigenschappen in *function.json*:

- `name`: De id die wordt gebruikt in de functiecode voor Hallo document
- `type`: moet te worden ingesteld 'documentdb'
- `databaseName`: met Hallo document Hallo-database
- `collectionName`: met Hallo document Hallo-verzameling
- `id`: Hallo Hallo document tooretrieve-Id. Deze eigenschap ondersteunt de bindingen van parameters. Zie [toocustom invoer eigenschappen in een expressie voor gegevensbinding binden](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) in Hallo artikel [Azure Functions triggers en bindingen concepten](functions-triggers-bindings.md).
- `sqlQuery`: Een Cosmos DB SQL-query die wordt gebruikt voor het ophalen van meerdere documenten. Hallo-query ondersteunt runtime-bindingen. Bijvoorbeeld: `SELECT * FROM c where c.departmentId = {departmentId}`
- `connection`: Hallo-naam van Hallo app-instelling met de verbindingsreeks van de Cosmos-DB
- `direction`: moet te worden ingesteld`"in"`.

Hallo eigenschappen `id` en `sqlQuery` kunnen niet allebei worden opgegeven. Als geen van beide `id` noch `sqlQuery` is ingesteld, hello volledige verzameling worden opgehaald.

## <a name="using-a-documentdb-api-input-binding"></a>Met behulp van een DocumentDB-API invoer binding

* In C# en F # functies, wanneer het Hallo-functie is, wordt afgesloten worden toohello invoerdocument via benoemde invoerparameters wijzigingen automatisch persistent. 
* In de JavaScript-functies worden niet automatisch updates gesteld bij functie beëindigen. Gebruik in plaats daarvan `context.bindings.<documentName>In` en `context.bindings.<documentName>Out` toomake updates. Zie Hallo [JavaScript voorbeeld](#injavascript).

<a name="inputsample"></a>

## <a name="input-sample-for-single-document"></a>Invoer voorbeeld voor één document
Stel dat u hebt de volgende Hallo DocumentDB API binding in Hallo invoer `bindings` matrix van function.json:

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

Zie Hallo taalspecifieke voorbeeld dat gebruikmaakt van dit invoer binding tooupdate Hallo document tekstwaarde.

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

Dit voorbeeld vereist een `project.json` bestand waarmee Hallo `FSharp.Interop.Dynamic` en `Dynamitey` NuGet afhankelijkheden:

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

tooadd een `project.json` bestand, Zie [F # pakket management](functions-reference-fsharp.md#package).

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

Stel dat u wenst tooretrieve meerdere documenten die zijn opgegeven door een SQL-query met behulp van een wachtrij trigger toocustomize Hallo queryparameters. 

In dit voorbeeld Hallo wachtrij trigger wordt een parameter opgegeven `departmentId`. Een wachtrijbericht van `{ "departmentId" : "Finance" }` alle records voor de afdeling Financiën Hallo zou retourneren. Gebruik de volgende Hallo in *function.json*:

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
Hallo DocumentDB API uitvoer binding kunt u een nieuw document tooan Azure DB die Cosmos-database te schrijven. Hieraan de volgende eigenschappen in Hallo *function.json*:

- `name`: De id die is gebruikt in de functiecode voor Hallo nieuw document
- `type`: moet te worden ingesteld`"documentdb"`
- `databaseName`: Hallo-database met Hallo verzameling waar Hallo nieuw document wordt gemaakt.
- `collectionName`: Hallo verzameling waar Hallo nieuw document wordt gemaakt.
- `createIfNotExists`: Een Booleaanse waarde tooindicate of Hallo verzameling wordt gemaakt als deze niet bestaat. Hallo standaardwaarde is *false*. Hallo reden voor deze bewerking nieuwe is verzamelingen worden gemaakt met gereserveerde doorvoer, wat gevolgen heeft. Voor meer informatie gaat u naar Hallo [pagina met prijzen](https://azure.microsoft.com/pricing/details/documentdb/).
- `connection`: Hallo-naam van Hallo app-instelling met de verbindingsreeks van de Cosmos-DB
- `direction`: moet te worden ingesteld`"out"`

## <a name="using-a-documentdb-api-output-binding"></a>Binding met een DocumentDB-API uitvoer
Deze sectie leest u hoe toouse uw DocumentDB-API uitvoer binding in uw functiecode.

Wanneer u schrijft toohello output-parameter in de functie is standaard een nieuw document wordt gegenereerd in de database, met een automatisch gegenereerde GUID als Hallo document ID. U kunt Hallo document-ID van uitvoerdocument opgeven door te geven Hallo `id` JSON-eigenschap in Hallo uitvoerparameter. 

>[!Note]  
>Wanneer u een bestaand document Hallo-ID opgeeft, wordt deze overschreven door Hallo nieuw uitvoerdocument. 

toooutput meerdere documenten, kunt u ook binden te`ICollector<T>` of `IAsyncCollector<T>` waar `T` een van de typen Hallo ondersteund.

<a name="outputsample"></a>

## <a name="documentdb-api-output-binding-sample"></a>DocumentDB-API uitvoer binding-voorbeeld
Stel dat u hebt de volgende Hallo DocumentDB API binding in Hallo uitvoer `bindings` matrix van function.json:

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

En u een wachtrij invoer binding voor een wachtrij die JSON ontvangt in Hallo volgende indeling hebben:

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

En u wilt dat toocreate Cosmos DB documenten in Hallo indeling voor elke record te volgen:

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

Zie Hallo taalspecifieke voorbeeldtoepassing die gebruikmaakt van deze uitvoer binding tooadd documenten tooyour database.

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

Dit voorbeeld vereist een `project.json` bestand waarmee Hallo `FSharp.Interop.Dynamic` en `Dynamitey` NuGet afhankelijkheden:

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

tooadd een `project.json` bestand, Zie [F # pakket management](functions-reference-fsharp.md#package).

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
