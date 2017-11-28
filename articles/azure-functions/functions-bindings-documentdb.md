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
# <a name="azure-functions-cosmos-db-bindings"></a><span data-ttu-id="70a3d-104">Azure Functions Cosmos DB bindingen</span><span class="sxs-lookup"><span data-stu-id="70a3d-104">Azure Functions Cosmos DB bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="70a3d-105">Dit artikel wordt uitgelegd hoe Azure DB die Cosmos-bindingen voor tooconfigure en code in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="70a3d-105">This article explains how tooconfigure and code Azure Cosmos DB bindings in Azure Functions.</span></span> <span data-ttu-id="70a3d-106">Azure Functions ondersteunt invoer en uitvoer van de bindingen voor Cosmos-DB.</span><span class="sxs-lookup"><span data-stu-id="70a3d-106">Azure Functions supports input and output bindings for Cosmos DB.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="70a3d-107">Zie voor meer informatie over Cosmos DB [inleiding tooCosmos DB](../documentdb/documentdb-introduction.md) en [een Cosmos-DB-consoletoepassing bouwen](../documentdb/documentdb-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="70a3d-107">For more information on Cosmos DB, see [Introduction tooCosmos DB](../documentdb/documentdb-introduction.md) and [Build a Cosmos DB console application](../documentdb/documentdb-get-started.md).</span></span>

<a id="docdbinput"></a>

## <a name="documentdb-api-input-binding"></a><span data-ttu-id="70a3d-108">DocumentDB-API invoer binding</span><span class="sxs-lookup"><span data-stu-id="70a3d-108">DocumentDB API input binding</span></span>
<span data-ttu-id="70a3d-109">Hallo DocumentDB API invoer binding een Cosmos-DB-document opgehaald en doorgegeven toohello invoerparameter van het Hallo-functie met de naam.</span><span class="sxs-lookup"><span data-stu-id="70a3d-109">hello DocumentDB API input binding retrieves a Cosmos DB document and passes it toohello named input parameter of hello function.</span></span> <span data-ttu-id="70a3d-110">Hallo-document-ID kan worden vastgesteld gebaseerd op Hallo-trigger die Hallo-functie roept.</span><span class="sxs-lookup"><span data-stu-id="70a3d-110">hello document ID can be determined based on hello trigger that invokes hello function.</span></span> 

<span data-ttu-id="70a3d-111">Hallo invoer DocumentDB API-binding heeft Hallo volgende eigenschappen in *function.json*:</span><span class="sxs-lookup"><span data-stu-id="70a3d-111">hello DocumentDB API input binding has hello following properties in *function.json*:</span></span>

- <span data-ttu-id="70a3d-112">`name`: De id die wordt gebruikt in de functiecode voor Hallo document</span><span class="sxs-lookup"><span data-stu-id="70a3d-112">`name` : Identifier name used in function code for hello document</span></span>
- <span data-ttu-id="70a3d-113">`type`: moet te worden ingesteld 'documentdb'</span><span class="sxs-lookup"><span data-stu-id="70a3d-113">`type` : must be set too"documentdb"</span></span>
- <span data-ttu-id="70a3d-114">`databaseName`: met Hallo document Hallo-database</span><span class="sxs-lookup"><span data-stu-id="70a3d-114">`databaseName` : hello database containing hello document</span></span>
- <span data-ttu-id="70a3d-115">`collectionName`: met Hallo document Hallo-verzameling</span><span class="sxs-lookup"><span data-stu-id="70a3d-115">`collectionName` : hello collection containing hello document</span></span>
- <span data-ttu-id="70a3d-116">`id`: Hallo Hallo document tooretrieve-Id.</span><span class="sxs-lookup"><span data-stu-id="70a3d-116">`id` : hello Id of hello document tooretrieve.</span></span> <span data-ttu-id="70a3d-117">Deze eigenschap ondersteunt de bindingen van parameters. Zie [toocustom invoer eigenschappen in een expressie voor gegevensbinding binden](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) in Hallo artikel [Azure Functions triggers en bindingen concepten](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="70a3d-117">This property supports bindings parameters; see [Bind toocustom input properties in a binding expression](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) in hello article [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>
- <span data-ttu-id="70a3d-118">`sqlQuery`: Een Cosmos DB SQL-query die wordt gebruikt voor het ophalen van meerdere documenten.</span><span class="sxs-lookup"><span data-stu-id="70a3d-118">`sqlQuery` : A Cosmos DB SQL query used for retrieving multiple documents.</span></span> <span data-ttu-id="70a3d-119">Hallo-query ondersteunt runtime-bindingen.</span><span class="sxs-lookup"><span data-stu-id="70a3d-119">hello query supports runtime bindings.</span></span> <span data-ttu-id="70a3d-120">Bijvoorbeeld: `SELECT * FROM c where c.departmentId = {departmentId}`</span><span class="sxs-lookup"><span data-stu-id="70a3d-120">For example: `SELECT * FROM c where c.departmentId = {departmentId}`</span></span>
- <span data-ttu-id="70a3d-121">`connection`: Hallo-naam van Hallo app-instelling met de verbindingsreeks van de Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="70a3d-121">`connection` : hello name of hello app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="70a3d-122">`direction`: moet te worden ingesteld`"in"`.</span><span class="sxs-lookup"><span data-stu-id="70a3d-122">`direction`  : must be set too`"in"`.</span></span>

<span data-ttu-id="70a3d-123">Hallo eigenschappen `id` en `sqlQuery` kunnen niet allebei worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="70a3d-123">hello properties `id` and `sqlQuery` cannot both be specified.</span></span> <span data-ttu-id="70a3d-124">Als geen van beide `id` noch `sqlQuery` is ingesteld, hello volledige verzameling worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="70a3d-124">If neither `id` nor `sqlQuery` is set, hello entire collection is retrieved.</span></span>

## <a name="using-a-documentdb-api-input-binding"></a><span data-ttu-id="70a3d-125">Met behulp van een DocumentDB-API invoer binding</span><span class="sxs-lookup"><span data-stu-id="70a3d-125">Using a DocumentDB API input binding</span></span>

* <span data-ttu-id="70a3d-126">In C# en F # functies, wanneer het Hallo-functie is, wordt afgesloten worden toohello invoerdocument via benoemde invoerparameters wijzigingen automatisch persistent.</span><span class="sxs-lookup"><span data-stu-id="70a3d-126">In C# and F# functions, when hello function exits successfully, any changes made toohello input document via named input parameters are automatically persisted.</span></span> 
* <span data-ttu-id="70a3d-127">In de JavaScript-functies worden niet automatisch updates gesteld bij functie beëindigen.</span><span class="sxs-lookup"><span data-stu-id="70a3d-127">In JavaScript functions, updates are not made automatically upon function exit.</span></span> <span data-ttu-id="70a3d-128">Gebruik in plaats daarvan `context.bindings.<documentName>In` en `context.bindings.<documentName>Out` toomake updates.</span><span class="sxs-lookup"><span data-stu-id="70a3d-128">Instead, use `context.bindings.<documentName>In` and `context.bindings.<documentName>Out` toomake updates.</span></span> <span data-ttu-id="70a3d-129">Zie Hallo [JavaScript voorbeeld](#injavascript).</span><span class="sxs-lookup"><span data-stu-id="70a3d-129">See hello [JavaScript sample](#injavascript).</span></span>

<a name="inputsample"></a>

## <a name="input-sample-for-single-document"></a><span data-ttu-id="70a3d-130">Invoer voorbeeld voor één document</span><span class="sxs-lookup"><span data-stu-id="70a3d-130">Input sample for single document</span></span>
<span data-ttu-id="70a3d-131">Stel dat u hebt de volgende Hallo DocumentDB API binding in Hallo invoer `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="70a3d-131">Suppose you have hello following DocumentDB API input binding in hello `bindings` array of function.json:</span></span>

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

<span data-ttu-id="70a3d-132">Zie Hallo taalspecifieke voorbeeld dat gebruikmaakt van dit invoer binding tooupdate Hallo document tekstwaarde.</span><span class="sxs-lookup"><span data-stu-id="70a3d-132">See hello language-specific sample that uses this input binding tooupdate hello document's text value.</span></span>

* [<span data-ttu-id="70a3d-133">C#</span><span class="sxs-lookup"><span data-stu-id="70a3d-133">C#</span></span>](#incsharp)
* [<span data-ttu-id="70a3d-134">F#</span><span class="sxs-lookup"><span data-stu-id="70a3d-134">F#</span></span>](#infsharp)
* [<span data-ttu-id="70a3d-135">JavaScript</span><span class="sxs-lookup"><span data-stu-id="70a3d-135">JavaScript</span></span>](#injavascript)

<a name="incsharp"></a>
### <a name="input-sample-in-c"></a><span data-ttu-id="70a3d-136">Invoer voorbeeld in C#</span><span class="sxs-lookup"><span data-stu-id="70a3d-136">Input sample in C#</span></span> #

```cs
// Change input document contents using DocumentDB API input binding 
public static void Run(string myQueueItem, dynamic inputDocument)
{   
  inputDocument.text = "This has changed.";
}
```
<a name="infsharp"></a>

### <a name="input-sample-in-f"></a><span data-ttu-id="70a3d-137">Invoer voorbeeld in F #</span><span class="sxs-lookup"><span data-stu-id="70a3d-137">Input sample in F#</span></span> #

```fsharp
(* Change input document contents using DocumentDB API input binding *)
open FSharp.Interop.Dynamic
let Run(myQueueItem: string, inputDocument: obj) =
  inputDocument?text <- "This has changed."
```

<span data-ttu-id="70a3d-138">Dit voorbeeld vereist een `project.json` bestand waarmee Hallo `FSharp.Interop.Dynamic` en `Dynamitey` NuGet afhankelijkheden:</span><span class="sxs-lookup"><span data-stu-id="70a3d-138">This sample requires a `project.json` file that specifies hello `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

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

<span data-ttu-id="70a3d-139">tooadd een `project.json` bestand, Zie [F # pakket management](functions-reference-fsharp.md#package).</span><span class="sxs-lookup"><span data-stu-id="70a3d-139">tooadd a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="injavascript"></a>

### <a name="input-sample-in-javascript"></a><span data-ttu-id="70a3d-140">Invoer voorbeeld in JavaScript</span><span class="sxs-lookup"><span data-stu-id="70a3d-140">Input sample in JavaScript</span></span>

```javascript
// Change input document contents using DocumentDB API input binding, using context.bindings.inputDocumentOut
module.exports = function (context) {   
  context.bindings.inputDocumentOut = context.bindings.inputDocumentIn;
  context.bindings.inputDocumentOut.text = "This was updated!";
  context.done();
};
```

## <a name="input-sample-with-multiple-documents"></a><span data-ttu-id="70a3d-141">Invoer voorbeeld met meerdere documenten</span><span class="sxs-lookup"><span data-stu-id="70a3d-141">Input sample with multiple documents</span></span>

<span data-ttu-id="70a3d-142">Stel dat u wenst tooretrieve meerdere documenten die zijn opgegeven door een SQL-query met behulp van een wachtrij trigger toocustomize Hallo queryparameters.</span><span class="sxs-lookup"><span data-stu-id="70a3d-142">Suppose that you wish tooretrieve multiple documents specified by a SQL query, using a queue trigger toocustomize hello query parameters.</span></span> 

<span data-ttu-id="70a3d-143">In dit voorbeeld Hallo wachtrij trigger wordt een parameter opgegeven `departmentId`. Een wachtrijbericht van `{ "departmentId" : "Finance" }` alle records voor de afdeling Financiën Hallo zou retourneren.</span><span class="sxs-lookup"><span data-stu-id="70a3d-143">In this example, hello queue trigger provides a parameter `departmentId`.A queue message of `{ "departmentId" : "Finance" }` would return all records for hello finance department.</span></span> <span data-ttu-id="70a3d-144">Gebruik de volgende Hallo in *function.json*:</span><span class="sxs-lookup"><span data-stu-id="70a3d-144">Use hello following in *function.json*:</span></span>

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

### <a name="input-sample-with-multiple-documents-in-c"></a><span data-ttu-id="70a3d-145">Invoer voorbeeld met meerdere documenten in C#</span><span class="sxs-lookup"><span data-stu-id="70a3d-145">Input sample with multiple documents in C#</span></span>

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

### <a name="input-sample-with-multiple-documents-in-javascript"></a><span data-ttu-id="70a3d-146">Invoer voorbeeld met meerdere documenten in JavaScript</span><span class="sxs-lookup"><span data-stu-id="70a3d-146">Input sample with multiple documents in JavaScript</span></span>

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

## <span data-ttu-id="70a3d-147"><a id="docdboutput"></a>DocumentDB-API uitvoer binding</span><span class="sxs-lookup"><span data-stu-id="70a3d-147"><a id="docdboutput"></a>DocumentDB API output binding</span></span>
<span data-ttu-id="70a3d-148">Hallo DocumentDB API uitvoer binding kunt u een nieuw document tooan Azure DB die Cosmos-database te schrijven.</span><span class="sxs-lookup"><span data-stu-id="70a3d-148">hello DocumentDB API output binding lets you write a new document tooan Azure Cosmos DB database.</span></span> <span data-ttu-id="70a3d-149">Hieraan de volgende eigenschappen in Hallo *function.json*:</span><span class="sxs-lookup"><span data-stu-id="70a3d-149">It has hello following properties in *function.json*:</span></span>

- <span data-ttu-id="70a3d-150">`name`: De id die is gebruikt in de functiecode voor Hallo nieuw document</span><span class="sxs-lookup"><span data-stu-id="70a3d-150">`name` : Identifier used in function code for hello new document</span></span>
- <span data-ttu-id="70a3d-151">`type`: moet te worden ingesteld`"documentdb"`</span><span class="sxs-lookup"><span data-stu-id="70a3d-151">`type` : must be set too`"documentdb"`</span></span>
- <span data-ttu-id="70a3d-152">`databaseName`: Hallo-database met Hallo verzameling waar Hallo nieuw document wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="70a3d-152">`databaseName` : hello database containing hello collection where hello new document will be created.</span></span>
- <span data-ttu-id="70a3d-153">`collectionName`: Hallo verzameling waar Hallo nieuw document wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="70a3d-153">`collectionName` : hello collection where hello new document will be created.</span></span>
- <span data-ttu-id="70a3d-154">`createIfNotExists`: Een Booleaanse waarde tooindicate of Hallo verzameling wordt gemaakt als deze niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="70a3d-154">`createIfNotExists` : A boolean value tooindicate whether hello collection will be created if it does not exist.</span></span> <span data-ttu-id="70a3d-155">Hallo standaardwaarde is *false*.</span><span class="sxs-lookup"><span data-stu-id="70a3d-155">hello default is *false*.</span></span> <span data-ttu-id="70a3d-156">Hallo reden voor deze bewerking nieuwe is verzamelingen worden gemaakt met gereserveerde doorvoer, wat gevolgen heeft.</span><span class="sxs-lookup"><span data-stu-id="70a3d-156">hello reason for this is new collections are created with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="70a3d-157">Voor meer informatie gaat u naar Hallo [pagina met prijzen](https://azure.microsoft.com/pricing/details/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="70a3d-157">For more details, please visit hello [pricing page](https://azure.microsoft.com/pricing/details/documentdb/).</span></span>
- <span data-ttu-id="70a3d-158">`connection`: Hallo-naam van Hallo app-instelling met de verbindingsreeks van de Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="70a3d-158">`connection` : hello name of hello app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="70a3d-159">`direction`: moet te worden ingesteld`"out"`</span><span class="sxs-lookup"><span data-stu-id="70a3d-159">`direction` : must be set too`"out"`</span></span>

## <a name="using-a-documentdb-api-output-binding"></a><span data-ttu-id="70a3d-160">Binding met een DocumentDB-API uitvoer</span><span class="sxs-lookup"><span data-stu-id="70a3d-160">Using a DocumentDB API output binding</span></span>
<span data-ttu-id="70a3d-161">Deze sectie leest u hoe toouse uw DocumentDB-API uitvoer binding in uw functiecode.</span><span class="sxs-lookup"><span data-stu-id="70a3d-161">This section shows you how toouse your DocumentDB API output binding in your function code.</span></span>

<span data-ttu-id="70a3d-162">Wanneer u schrijft toohello output-parameter in de functie is standaard een nieuw document wordt gegenereerd in de database, met een automatisch gegenereerde GUID als Hallo document ID.</span><span class="sxs-lookup"><span data-stu-id="70a3d-162">When you write toohello output parameter in your function, by default a new document is generated in your database, with an automatically generated GUID as hello document ID.</span></span> <span data-ttu-id="70a3d-163">U kunt Hallo document-ID van uitvoerdocument opgeven door te geven Hallo `id` JSON-eigenschap in Hallo uitvoerparameter.</span><span class="sxs-lookup"><span data-stu-id="70a3d-163">You can specify hello document ID of output document by specifying hello `id` JSON property in hello output parameter.</span></span> 

>[!Note]  
><span data-ttu-id="70a3d-164">Wanneer u een bestaand document Hallo-ID opgeeft, wordt deze overschreven door Hallo nieuw uitvoerdocument.</span><span class="sxs-lookup"><span data-stu-id="70a3d-164">When you specify hello ID of an existing document, it gets overwritten by hello new output document.</span></span> 

<span data-ttu-id="70a3d-165">toooutput meerdere documenten, kunt u ook binden te`ICollector<T>` of `IAsyncCollector<T>` waar `T` een van de typen Hallo ondersteund.</span><span class="sxs-lookup"><span data-stu-id="70a3d-165">toooutput multiple documents, you can also bind too`ICollector<T>` or `IAsyncCollector<T>` where `T` is one of hello supported types.</span></span>

<a name="outputsample"></a>

## <a name="documentdb-api-output-binding-sample"></a><span data-ttu-id="70a3d-166">DocumentDB-API uitvoer binding-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="70a3d-166">DocumentDB API output binding sample</span></span>
<span data-ttu-id="70a3d-167">Stel dat u hebt de volgende Hallo DocumentDB API binding in Hallo uitvoer `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="70a3d-167">Suppose you have hello following DocumentDB API output binding in hello `bindings` array of function.json:</span></span>

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

<span data-ttu-id="70a3d-168">En u een wachtrij invoer binding voor een wachtrij die JSON ontvangt in Hallo volgende indeling hebben:</span><span class="sxs-lookup"><span data-stu-id="70a3d-168">And you have a queue input binding for a queue that receives JSON in hello following format:</span></span>

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="70a3d-169">En u wilt dat toocreate Cosmos DB documenten in Hallo indeling voor elke record te volgen:</span><span class="sxs-lookup"><span data-stu-id="70a3d-169">And you want toocreate Cosmos DB documents in hello following format for each record:</span></span>

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="70a3d-170">Zie Hallo taalspecifieke voorbeeldtoepassing die gebruikmaakt van deze uitvoer binding tooadd documenten tooyour database.</span><span class="sxs-lookup"><span data-stu-id="70a3d-170">See hello language-specific sample that uses this output binding tooadd documents tooyour database.</span></span>

* [<span data-ttu-id="70a3d-171">C#</span><span class="sxs-lookup"><span data-stu-id="70a3d-171">C#</span></span>](#outcsharp)
* [<span data-ttu-id="70a3d-172">F#</span><span class="sxs-lookup"><span data-stu-id="70a3d-172">F#</span></span>](#outfsharp)
* [<span data-ttu-id="70a3d-173">JavaScript</span><span class="sxs-lookup"><span data-stu-id="70a3d-173">JavaScript</span></span>](#outjavascript)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="70a3d-174">Voorbeeld van uitvoer in C#</span><span class="sxs-lookup"><span data-stu-id="70a3d-174">Output sample in C#</span></span> #

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

### <a name="output-sample-in-f"></a><span data-ttu-id="70a3d-175">Voorbeeld van uitvoer in F #</span><span class="sxs-lookup"><span data-stu-id="70a3d-175">Output sample in F#</span></span> #

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

<span data-ttu-id="70a3d-176">Dit voorbeeld vereist een `project.json` bestand waarmee Hallo `FSharp.Interop.Dynamic` en `Dynamitey` NuGet afhankelijkheden:</span><span class="sxs-lookup"><span data-stu-id="70a3d-176">This sample requires a `project.json` file that specifies hello `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

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

<span data-ttu-id="70a3d-177">tooadd een `project.json` bestand, Zie [F # pakket management](functions-reference-fsharp.md#package).</span><span class="sxs-lookup"><span data-stu-id="70a3d-177">tooadd a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="outjavascript"></a>

### <a name="output-sample-in-javascript"></a><span data-ttu-id="70a3d-178">Voorbeeld van uitvoer in JavaScript</span><span class="sxs-lookup"><span data-stu-id="70a3d-178">Output sample in JavaScript</span></span>

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
