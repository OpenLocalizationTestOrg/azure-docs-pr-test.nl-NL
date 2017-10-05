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
# <a name="azure-functions-cosmos-db-bindings"></a><span data-ttu-id="243fb-104">Azure Functions Cosmos DB bindingen</span><span class="sxs-lookup"><span data-stu-id="243fb-104">Azure Functions Cosmos DB bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="243fb-105">Dit artikel wordt uitgelegd hoe u configureert en bindingen van Azure DB die Cosmos code in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="243fb-105">This article explains how to configure and code Azure Cosmos DB bindings in Azure Functions.</span></span> <span data-ttu-id="243fb-106">Azure Functions ondersteunt invoer en uitvoer van de bindingen voor Cosmos-DB.</span><span class="sxs-lookup"><span data-stu-id="243fb-106">Azure Functions supports input and output bindings for Cosmos DB.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="243fb-107">Zie voor meer informatie over Cosmos DB [Inleiding tot Cosmos DB](../documentdb/documentdb-introduction.md) en [een Cosmos-DB-consoletoepassing bouwen](../documentdb/documentdb-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="243fb-107">For more information on Cosmos DB, see [Introduction to Cosmos DB](../documentdb/documentdb-introduction.md) and [Build a Cosmos DB console application](../documentdb/documentdb-get-started.md).</span></span>

<a id="docdbinput"></a>

## <a name="documentdb-api-input-binding"></a><span data-ttu-id="243fb-108">DocumentDB-API invoer binding</span><span class="sxs-lookup"><span data-stu-id="243fb-108">DocumentDB API input binding</span></span>
<span data-ttu-id="243fb-109">De invoer DocumentDB API-binding een Cosmos-DB-document opgehaald en doorgegeven aan de benoemde invoerparameter van de functie.</span><span class="sxs-lookup"><span data-stu-id="243fb-109">The DocumentDB API input binding retrieves a Cosmos DB document and passes it to the named input parameter of the function.</span></span> <span data-ttu-id="243fb-110">De ID kan worden bepaald document is gebaseerd op de trigger die de functie activeert.</span><span class="sxs-lookup"><span data-stu-id="243fb-110">The document ID can be determined based on the trigger that invokes the function.</span></span> 

<span data-ttu-id="243fb-111">De invoer DocumentDB API-binding heeft de volgende eigenschappen *function.json*:</span><span class="sxs-lookup"><span data-stu-id="243fb-111">The DocumentDB API input binding has the following properties in *function.json*:</span></span>

- <span data-ttu-id="243fb-112">`name`: De id die wordt gebruikt in de functiecode voor het document</span><span class="sxs-lookup"><span data-stu-id="243fb-112">`name` : Identifier name used in function code for the document</span></span>
- <span data-ttu-id="243fb-113">`type`: moet worden ingesteld op 'documentdb'</span><span class="sxs-lookup"><span data-stu-id="243fb-113">`type` : must be set to "documentdb"</span></span>
- <span data-ttu-id="243fb-114">`databaseName`: De database met het document</span><span class="sxs-lookup"><span data-stu-id="243fb-114">`databaseName` : The database containing the document</span></span>
- <span data-ttu-id="243fb-115">`collectionName`: De verzameling met het document</span><span class="sxs-lookup"><span data-stu-id="243fb-115">`collectionName` : The collection containing the document</span></span>
- <span data-ttu-id="243fb-116">`id`: De Id van het document om op te halen.</span><span class="sxs-lookup"><span data-stu-id="243fb-116">`id` : The Id of the document to retrieve.</span></span> <span data-ttu-id="243fb-117">Deze eigenschap ondersteunt de bindingen van parameters. Zie [binden aan aangepaste eigenschappen voor de invoer in een expressie voor gegevensbinding](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) in het artikel [Azure Functions triggers en bindingen concepten](functions-triggers-bindings.md).</span><span class="sxs-lookup"><span data-stu-id="243fb-117">This property supports bindings parameters; see [Bind to custom input properties in a binding expression](functions-triggers-bindings.md#bind-to-custom-input-properties-in-a-binding-expression) in the article [Azure Functions triggers and bindings concepts](functions-triggers-bindings.md).</span></span>
- <span data-ttu-id="243fb-118">`sqlQuery`: Een Cosmos DB SQL-query die wordt gebruikt voor het ophalen van meerdere documenten.</span><span class="sxs-lookup"><span data-stu-id="243fb-118">`sqlQuery` : A Cosmos DB SQL query used for retrieving multiple documents.</span></span> <span data-ttu-id="243fb-119">De query biedt ondersteuning voor runtime-bindingen.</span><span class="sxs-lookup"><span data-stu-id="243fb-119">The query supports runtime bindings.</span></span> <span data-ttu-id="243fb-120">Bijvoorbeeld: `SELECT * FROM c where c.departmentId = {departmentId}`</span><span class="sxs-lookup"><span data-stu-id="243fb-120">For example: `SELECT * FROM c where c.departmentId = {departmentId}`</span></span>
- <span data-ttu-id="243fb-121">`connection`: De naam van de app-instelling met de verbindingsreeks van de Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="243fb-121">`connection` : The name of the app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="243fb-122">`direction`: moet worden ingesteld op `"in"`.</span><span class="sxs-lookup"><span data-stu-id="243fb-122">`direction`  : must be set to `"in"`.</span></span>

<span data-ttu-id="243fb-123">De eigenschappen `id` en `sqlQuery` kunnen niet allebei worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="243fb-123">The properties `id` and `sqlQuery` cannot both be specified.</span></span> <span data-ttu-id="243fb-124">Als geen van beide `id` noch `sqlQuery` is ingesteld, wordt de volledige verzameling worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="243fb-124">If neither `id` nor `sqlQuery` is set, the entire collection is retrieved.</span></span>

## <a name="using-a-documentdb-api-input-binding"></a><span data-ttu-id="243fb-125">Met behulp van een DocumentDB-API invoer binding</span><span class="sxs-lookup"><span data-stu-id="243fb-125">Using a DocumentDB API input binding</span></span>

* <span data-ttu-id="243fb-126">In C# en F # functies, wanneer de functie wordt voltooid, wordt afgesloten worden wijzigingen in het invoerdocument via benoemde invoerparameters automatisch doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="243fb-126">In C# and F# functions, when the function exits successfully, any changes made to the input document via named input parameters are automatically persisted.</span></span> 
* <span data-ttu-id="243fb-127">In de JavaScript-functies worden niet automatisch updates gesteld bij functie beëindigen.</span><span class="sxs-lookup"><span data-stu-id="243fb-127">In JavaScript functions, updates are not made automatically upon function exit.</span></span> <span data-ttu-id="243fb-128">Gebruik in plaats daarvan `context.bindings.<documentName>In` en `context.bindings.<documentName>Out` om updates te maken.</span><span class="sxs-lookup"><span data-stu-id="243fb-128">Instead, use `context.bindings.<documentName>In` and `context.bindings.<documentName>Out` to make updates.</span></span> <span data-ttu-id="243fb-129">Zie de [JavaScript voorbeeld](#injavascript).</span><span class="sxs-lookup"><span data-stu-id="243fb-129">See the [JavaScript sample](#injavascript).</span></span>

<a name="inputsample"></a>

## <a name="input-sample-for-single-document"></a><span data-ttu-id="243fb-130">Invoer voorbeeld voor één document</span><span class="sxs-lookup"><span data-stu-id="243fb-130">Input sample for single document</span></span>
<span data-ttu-id="243fb-131">Stel dat u hebt de volgende invoer DocumentDB API-binding in de `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="243fb-131">Suppose you have the following DocumentDB API input binding in the `bindings` array of function.json:</span></span>

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

<span data-ttu-id="243fb-132">Zie de taalspecifieke-voorbeeldtoepassing die u deze invoer binding gebruikt voor het bijwerken van de tekstwaarde van het document.</span><span class="sxs-lookup"><span data-stu-id="243fb-132">See the language-specific sample that uses this input binding to update the document's text value.</span></span>

* [<span data-ttu-id="243fb-133">C#</span><span class="sxs-lookup"><span data-stu-id="243fb-133">C#</span></span>](#incsharp)
* [<span data-ttu-id="243fb-134">F#</span><span class="sxs-lookup"><span data-stu-id="243fb-134">F#</span></span>](#infsharp)
* [<span data-ttu-id="243fb-135">JavaScript</span><span class="sxs-lookup"><span data-stu-id="243fb-135">JavaScript</span></span>](#injavascript)

<a name="incsharp"></a>
### <a name="input-sample-in-c"></a><span data-ttu-id="243fb-136">Invoer voorbeeld in C#</span><span class="sxs-lookup"><span data-stu-id="243fb-136">Input sample in C#</span></span> #

```cs
// Change input document contents using DocumentDB API input binding 
public static void Run(string myQueueItem, dynamic inputDocument)
{   
  inputDocument.text = "This has changed.";
}
```
<a name="infsharp"></a>

### <a name="input-sample-in-f"></a><span data-ttu-id="243fb-137">Invoer voorbeeld in F #</span><span class="sxs-lookup"><span data-stu-id="243fb-137">Input sample in F#</span></span> #

```fsharp
(* Change input document contents using DocumentDB API input binding *)
open FSharp.Interop.Dynamic
let Run(myQueueItem: string, inputDocument: obj) =
  inputDocument?text <- "This has changed."
```

<span data-ttu-id="243fb-138">Dit voorbeeld vereist een `project.json` -bestand dat Hiermee geeft u de `FSharp.Interop.Dynamic` en `Dynamitey` NuGet afhankelijkheden:</span><span class="sxs-lookup"><span data-stu-id="243fb-138">This sample requires a `project.json` file that specifies the `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

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

<span data-ttu-id="243fb-139">Om toe te voegen een `project.json` bestand, Zie [F # pakket management](functions-reference-fsharp.md#package).</span><span class="sxs-lookup"><span data-stu-id="243fb-139">To add a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="injavascript"></a>

### <a name="input-sample-in-javascript"></a><span data-ttu-id="243fb-140">Invoer voorbeeld in JavaScript</span><span class="sxs-lookup"><span data-stu-id="243fb-140">Input sample in JavaScript</span></span>

```javascript
// Change input document contents using DocumentDB API input binding, using context.bindings.inputDocumentOut
module.exports = function (context) {   
  context.bindings.inputDocumentOut = context.bindings.inputDocumentIn;
  context.bindings.inputDocumentOut.text = "This was updated!";
  context.done();
};
```

## <a name="input-sample-with-multiple-documents"></a><span data-ttu-id="243fb-141">Invoer voorbeeld met meerdere documenten</span><span class="sxs-lookup"><span data-stu-id="243fb-141">Input sample with multiple documents</span></span>

<span data-ttu-id="243fb-142">Stel dat u ophalen van meerdere documenten die zijn opgegeven met een SQL-query met behulp van een wachtrij-trigger wilt voor het aanpassen van de queryparameters.</span><span class="sxs-lookup"><span data-stu-id="243fb-142">Suppose that you wish to retrieve multiple documents specified by a SQL query, using a queue trigger to customize the query parameters.</span></span> 

<span data-ttu-id="243fb-143">In dit voorbeeld wordt de trigger wachtrij een parameter opgegeven `departmentId`. Een wachtrijbericht van `{ "departmentId" : "Finance" }` alle records voor de afdeling Financiën zou retourneren.</span><span class="sxs-lookup"><span data-stu-id="243fb-143">In this example, the queue trigger provides a parameter `departmentId`.A queue message of `{ "departmentId" : "Finance" }` would return all records for the finance department.</span></span> <span data-ttu-id="243fb-144">Gebruik de volgende in *function.json*:</span><span class="sxs-lookup"><span data-stu-id="243fb-144">Use the following in *function.json*:</span></span>

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

### <a name="input-sample-with-multiple-documents-in-c"></a><span data-ttu-id="243fb-145">Invoer voorbeeld met meerdere documenten in C#</span><span class="sxs-lookup"><span data-stu-id="243fb-145">Input sample with multiple documents in C#</span></span>

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

### <a name="input-sample-with-multiple-documents-in-javascript"></a><span data-ttu-id="243fb-146">Invoer voorbeeld met meerdere documenten in JavaScript</span><span class="sxs-lookup"><span data-stu-id="243fb-146">Input sample with multiple documents in JavaScript</span></span>

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

## <span data-ttu-id="243fb-147"><a id="docdboutput"></a>DocumentDB-API uitvoer binding</span><span class="sxs-lookup"><span data-stu-id="243fb-147"><a id="docdboutput"></a>DocumentDB API output binding</span></span>
<span data-ttu-id="243fb-148">De uitvoer van de DocumentDB-API binding kunt schrijven u een nieuw document naar een Azure DB die Cosmos-database.</span><span class="sxs-lookup"><span data-stu-id="243fb-148">The DocumentDB API output binding lets you write a new document to an Azure Cosmos DB database.</span></span> <span data-ttu-id="243fb-149">Deze heeft de volgende eigenschappen in *function.json*:</span><span class="sxs-lookup"><span data-stu-id="243fb-149">It has the following properties in *function.json*:</span></span>

- <span data-ttu-id="243fb-150">`name`: De id die is gebruikt in de functiecode voor het nieuwe document</span><span class="sxs-lookup"><span data-stu-id="243fb-150">`name` : Identifier used in function code for the new document</span></span>
- <span data-ttu-id="243fb-151">`type`: moet worden ingesteld op`"documentdb"`</span><span class="sxs-lookup"><span data-stu-id="243fb-151">`type` : must be set to `"documentdb"`</span></span>
- <span data-ttu-id="243fb-152">`databaseName`: De database met de verzameling waar het nieuwe document wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="243fb-152">`databaseName` : The database containing the collection where the new document will be created.</span></span>
- <span data-ttu-id="243fb-153">`collectionName`: De verzameling waar het nieuwe document wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="243fb-153">`collectionName` : The collection where the new document will be created.</span></span>
- <span data-ttu-id="243fb-154">`createIfNotExists`: Een Booleaanse waarde om aan te geven of de verzameling wordt gemaakt als deze niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="243fb-154">`createIfNotExists` : A boolean value to indicate whether the collection will be created if it does not exist.</span></span> <span data-ttu-id="243fb-155">De standaardwaarde is *false*.</span><span class="sxs-lookup"><span data-stu-id="243fb-155">The default is *false*.</span></span> <span data-ttu-id="243fb-156">De reden voor deze bewerking nieuwe is verzamelingen worden gemaakt met gereserveerde doorvoer, wat gevolgen heeft.</span><span class="sxs-lookup"><span data-stu-id="243fb-156">The reason for this is new collections are created with reserved throughput, which has pricing implications.</span></span> <span data-ttu-id="243fb-157">Voor meer informatie raadpleegt u de [pagina met prijzen](https://azure.microsoft.com/pricing/details/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="243fb-157">For more details, please visit the [pricing page](https://azure.microsoft.com/pricing/details/documentdb/).</span></span>
- <span data-ttu-id="243fb-158">`connection`: De naam van de app-instelling met de verbindingsreeks van de Cosmos-DB</span><span class="sxs-lookup"><span data-stu-id="243fb-158">`connection` : The name of the app setting containing your Cosmos DB connection string</span></span>
- <span data-ttu-id="243fb-159">`direction`: moet worden ingesteld op`"out"`</span><span class="sxs-lookup"><span data-stu-id="243fb-159">`direction` : must be set to `"out"`</span></span>

## <a name="using-a-documentdb-api-output-binding"></a><span data-ttu-id="243fb-160">Binding met een DocumentDB-API uitvoer</span><span class="sxs-lookup"><span data-stu-id="243fb-160">Using a DocumentDB API output binding</span></span>
<span data-ttu-id="243fb-161">Deze sectie wordt beschreven hoe u uw DocumentDB-API-uitvoer in uw functiecode binding.</span><span class="sxs-lookup"><span data-stu-id="243fb-161">This section shows you how to use your DocumentDB API output binding in your function code.</span></span>

<span data-ttu-id="243fb-162">Bij het schrijven naar de output-parameter in de functie standaard wordt een nieuw document gegenereerd in de database, met een automatisch gegenereerde GUID als het document-ID.</span><span class="sxs-lookup"><span data-stu-id="243fb-162">When you write to the output parameter in your function, by default a new document is generated in your database, with an automatically generated GUID as the document ID.</span></span> <span data-ttu-id="243fb-163">U kunt de document-ID van uitvoerdocument opgeven door te geven de `id` JSON-eigenschap in de output-parameter.</span><span class="sxs-lookup"><span data-stu-id="243fb-163">You can specify the document ID of output document by specifying the `id` JSON property in the output parameter.</span></span> 

>[!Note]  
><span data-ttu-id="243fb-164">Wanneer u de ID van een bestaand document opgeeft, wordt deze door het nieuwe uitvoerdocument overschreven.</span><span class="sxs-lookup"><span data-stu-id="243fb-164">When you specify the ID of an existing document, it gets overwritten by the new output document.</span></span> 

<span data-ttu-id="243fb-165">Als u wilt uitvoeren op meerdere documenten, kunt u ook binden aan `ICollector<T>` of `IAsyncCollector<T>` waar `T` is een van de ondersteunde typen.</span><span class="sxs-lookup"><span data-stu-id="243fb-165">To output multiple documents, you can also bind to `ICollector<T>` or `IAsyncCollector<T>` where `T` is one of the supported types.</span></span>

<a name="outputsample"></a>

## <a name="documentdb-api-output-binding-sample"></a><span data-ttu-id="243fb-166">DocumentDB-API uitvoer binding-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="243fb-166">DocumentDB API output binding sample</span></span>
<span data-ttu-id="243fb-167">Stel dat u hebt de volgende DocumentDB API uitvoer binding in de `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="243fb-167">Suppose you have the following DocumentDB API output binding in the `bindings` array of function.json:</span></span>

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

<span data-ttu-id="243fb-168">En u een wachtrij invoer binding voor een wachtrij die JSON in de volgende indeling ontvangt hebben:</span><span class="sxs-lookup"><span data-stu-id="243fb-168">And you have a queue input binding for a queue that receives JSON in the following format:</span></span>

```json
{
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="243fb-169">En u wilt Cosmos DB documenten in de volgende notatie voor elke record te maken:</span><span class="sxs-lookup"><span data-stu-id="243fb-169">And you want to create Cosmos DB documents in the following format for each record:</span></span>

```json
{
  "id": "John Henry-123456",
  "name": "John Henry",
  "employeeId": "123456",
  "address": "A town nearby"
}
```

<span data-ttu-id="243fb-170">Zie het voorbeeld taalspecifieke die gebruikmaakt van deze binding uitvoer documenten toevoegen aan uw database.</span><span class="sxs-lookup"><span data-stu-id="243fb-170">See the language-specific sample that uses this output binding to add documents to your database.</span></span>

* [<span data-ttu-id="243fb-171">C#</span><span class="sxs-lookup"><span data-stu-id="243fb-171">C#</span></span>](#outcsharp)
* [<span data-ttu-id="243fb-172">F#</span><span class="sxs-lookup"><span data-stu-id="243fb-172">F#</span></span>](#outfsharp)
* [<span data-ttu-id="243fb-173">JavaScript</span><span class="sxs-lookup"><span data-stu-id="243fb-173">JavaScript</span></span>](#outjavascript)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="243fb-174">Voorbeeld van uitvoer in C#</span><span class="sxs-lookup"><span data-stu-id="243fb-174">Output sample in C#</span></span> #

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

### <a name="output-sample-in-f"></a><span data-ttu-id="243fb-175">Voorbeeld van uitvoer in F #</span><span class="sxs-lookup"><span data-stu-id="243fb-175">Output sample in F#</span></span> #

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

<span data-ttu-id="243fb-176">Dit voorbeeld vereist een `project.json` -bestand dat Hiermee geeft u de `FSharp.Interop.Dynamic` en `Dynamitey` NuGet afhankelijkheden:</span><span class="sxs-lookup"><span data-stu-id="243fb-176">This sample requires a `project.json` file that specifies the `FSharp.Interop.Dynamic` and `Dynamitey` NuGet dependencies:</span></span>

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

<span data-ttu-id="243fb-177">Om toe te voegen een `project.json` bestand, Zie [F # pakket management](functions-reference-fsharp.md#package).</span><span class="sxs-lookup"><span data-stu-id="243fb-177">To add a `project.json` file, see [F# package management](functions-reference-fsharp.md#package).</span></span>

<a name="outjavascript"></a>

### <a name="output-sample-in-javascript"></a><span data-ttu-id="243fb-178">Voorbeeld van uitvoer in JavaScript</span><span class="sxs-lookup"><span data-stu-id="243fb-178">Output sample in JavaScript</span></span>

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
