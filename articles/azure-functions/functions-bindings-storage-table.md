---
title: Azure Storage-tabel functies bindingen | Microsoft Docs
description: Het gebruik van Azure Storage-bindingen in de Azure Functions begrijpen.
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: Azure functions, functies, verwerking van gebeurtenissen, dynamische compute zonder server architectuur
ms.assetid: 65b3437e-2571-4d3f-a996-61a74b50a1c2
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/28/2016
ms.author: chrande
ms.openlocfilehash: bb01be3ee044f60376e0c9c2de7b3dd34f3b7aca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-functions-storage-table-bindings"></a><span data-ttu-id="88529-104">Azure Functions opslag Tabelverbindingen</span><span class="sxs-lookup"><span data-stu-id="88529-104">Azure Functions Storage table bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="88529-105">Dit artikel wordt uitgelegd hoe u configureert en code Azure Storage Tabelverbindingen in de Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="88529-105">This article explains how to configure and code Azure Storage table bindings in Azure Functions.</span></span> <span data-ttu-id="88529-106">Azure Functions ondersteunt invoer en uitvoer van de bindingen voor Azure Storage-tabellen.</span><span class="sxs-lookup"><span data-stu-id="88529-106">Azure Functions supports input and output bindings for Azure Storage tables.</span></span>

<span data-ttu-id="88529-107">De binding van de tabel Storage ondersteunt de volgende scenario's:</span><span class="sxs-lookup"><span data-stu-id="88529-107">The Storage table binding supports the following scenarios:</span></span>

* <span data-ttu-id="88529-108">**Lezen van een enkele rij in een C# of Node.js-functie** : Stel `partitionKey` en `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="88529-108">**Read a single row in a C# or Node.js function** - Set `partitionKey` and `rowKey`.</span></span> <span data-ttu-id="88529-109">De `filter` en `take` eigenschappen worden niet gebruikt in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="88529-109">The `filter` and `take` properties are not used in this scenario.</span></span>
* <span data-ttu-id="88529-110">**Lezen van meerdere rijen in een C#-functie** -de runtime van Functions biedt een `IQueryable<T>` object gekoppeld aan de tabel.</span><span class="sxs-lookup"><span data-stu-id="88529-110">**Read multiple rows in a C# function** - The Functions runtime provides an `IQueryable<T>` object bound to the table.</span></span> <span data-ttu-id="88529-111">Type `T` moet worden afgeleid van `TableEntity` of implementeert `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="88529-111">Type `T` must derive from `TableEntity` or implement `ITableEntity`.</span></span> <span data-ttu-id="88529-112">De `partitionKey`, `rowKey`, `filter`, en `take` eigenschappen niet in dit scenario worden gebruikt; u kunt de `IQueryable` -object om alle filters vereist.</span><span class="sxs-lookup"><span data-stu-id="88529-112">The `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario; you can use the `IQueryable` object to do any filtering required.</span></span> 
* <span data-ttu-id="88529-113">**Lezen van meerdere rijen in een functie knooppunt** : Stel de `filter` en `take` eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="88529-113">**Read multiple rows in a Node function** - Set the `filter` and `take` properties.</span></span> <span data-ttu-id="88529-114">Stelt niet `partitionKey` of `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="88529-114">Don't set `partitionKey` or `rowKey`.</span></span>
* <span data-ttu-id="88529-115">**Schrijven van een of meer rijen in een C#-functie** -de runtime van Functions biedt een `ICollector<T>` of `IAsyncCollector<T>` gekoppeld aan de tabel waar `T` Hiermee geeft u het schema van de entiteiten die u wilt toevoegen.</span><span class="sxs-lookup"><span data-stu-id="88529-115">**Write one or more rows in a C# function** - The Functions runtime provides an `ICollector<T>` or `IAsyncCollector<T>` bound to the table, where `T` specifies the schema of the entities you want to add.</span></span> <span data-ttu-id="88529-116">Normaal gesproken Typ `T` is afgeleid van `TableEntity` of implementeert `ITableEntity`, maar deze hoeft niet te.</span><span class="sxs-lookup"><span data-stu-id="88529-116">Typically, type `T` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="88529-117">De `partitionKey`, `rowKey`, `filter`, en `take` eigenschappen worden niet gebruikt in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="88529-117">The `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="storage-table-input-binding"></a><span data-ttu-id="88529-118">Invoer tabelbinding opslag</span><span class="sxs-lookup"><span data-stu-id="88529-118">Storage table input binding</span></span>
<span data-ttu-id="88529-119">Invoer tabelbinding van Azure Storage kunt u een tabel met opslag in de functie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="88529-119">The Azure Storage table input binding enables you to use a storage table in your function.</span></span> 

<span data-ttu-id="88529-120">De invoer van de tabel opslag aan een functie maakt gebruik van de volgende JSON-objecten in de `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="88529-120">The Storage table input to a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "in",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity to read - see below>",
    "rowKey": "<RowKey of table entity to read - see below>",
    "take": "<Maximum number of entities to read in Node.js - optional>",
    "filter": "<OData filter expression for table input in Node.js - optional>",
    "connection": "<Name of app setting - see below>",
}
```

<span data-ttu-id="88529-121">Houd rekening met het volgende:</span><span class="sxs-lookup"><span data-stu-id="88529-121">Note the following:</span></span> 

* <span data-ttu-id="88529-122">Gebruik `partitionKey` en `rowKey` samen te lezen van één entiteit.</span><span class="sxs-lookup"><span data-stu-id="88529-122">Use `partitionKey` and `rowKey` together to read a single entity.</span></span> <span data-ttu-id="88529-123">Deze eigenschappen zijn optioneel.</span><span class="sxs-lookup"><span data-stu-id="88529-123">These properties are optional.</span></span> 
* <span data-ttu-id="88529-124">`connection`moet de naam van een app-instelling met een verbindingsreeks voor opslag bevatten.</span><span class="sxs-lookup"><span data-stu-id="88529-124">`connection` must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="88529-125">In de Azure portal, de standaard editor in de **integreren** tabblad configureert u deze appinstelling voor wanneer u een opslagruimte maakt account of een bestaande selecteert.</span><span class="sxs-lookup"><span data-stu-id="88529-125">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="88529-126">U kunt ook [configureren van deze app handmatig instellen](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="88529-126">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span>  

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="88529-127">Invoer-gebruik</span><span class="sxs-lookup"><span data-stu-id="88529-127">Input usage</span></span>
<span data-ttu-id="88529-128">In C#-functies, u koppelt aan de invoertabel entiteit (of entiteiten) met behulp van een benoemde parameter in de functiehandtekening, zoals `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="88529-128">In C# functions, you bind to the input table entity (or entities) by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="88529-129">Waar `T` is het gegevenstype dat u wilt deserialiseren van de gegevens in, en `paramName` is de naam die u hebt opgegeven in de [invoer binding](#input).</span><span class="sxs-lookup"><span data-stu-id="88529-129">Where `T` is the data type that you want to deserialize the data into, and `paramName` is the name you specified in the [input binding](#input).</span></span> <span data-ttu-id="88529-130">In Node.js-functies, opent u de invoertabel entiteit (of entiteiten) met behulp van `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="88529-130">In Node.js functions, you access the input table entity (or entities) using `context.bindings.<name>`.</span></span>

<span data-ttu-id="88529-131">De ingevoerde gegevens kunnen worden gedeserialiseerd in Node.js- of C#-functies.</span><span class="sxs-lookup"><span data-stu-id="88529-131">The input data can be deserialized in Node.js or C# functions.</span></span> <span data-ttu-id="88529-132">De gedeserialiseerde objecten hebben `RowKey` en `PartitionKey` eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="88529-132">The deserialized objects have `RowKey` and `PartitionKey` properties.</span></span>

<span data-ttu-id="88529-133">U kunt ook binden aan een van de volgende typen in C#-functies, en de runtime van Functions wordt geprobeerd te deserialiseren met behulp van dat type gegevens in de tabel:</span><span class="sxs-lookup"><span data-stu-id="88529-133">In C# functions, you can also bind to any of the following types, and the Functions runtime will attempt to deserialize the table data using that type:</span></span>

* <span data-ttu-id="88529-134">Type dat wordt geïmplementeerd`ITableEntity`</span><span class="sxs-lookup"><span data-stu-id="88529-134">Any type that implements `ITableEntity`</span></span>
* `IQueryable<T>`

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="88529-135">Voorbeeld van invoer</span><span class="sxs-lookup"><span data-stu-id="88529-135">Input sample</span></span>
<span data-ttu-id="88529-136">Stel, dat u hebt de volgende function.json dat gebruikmaakt van een trigger wachtrij om te lezen van een enkele tabelrij.</span><span class="sxs-lookup"><span data-stu-id="88529-136">Supposed you have the following function.json, which uses a queue trigger to read a single table row.</span></span> <span data-ttu-id="88529-137">De JSON geeft `PartitionKey`  
 `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="88529-137">The JSON specifies `PartitionKey` 
`RowKey`.</span></span> <span data-ttu-id="88529-138">`"rowKey": "{queueTrigger}"`Hiermee wordt aangegeven dat de rijsleutel is afkomstig uit de wachtrij bericht-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="88529-138">`"rowKey": "{queueTrigger}"` indicates that the row key comes from the queue message string.</span></span>

```json
{
  "bindings": [
    {
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
      "name": "myQueueItem",
      "type": "queueTrigger",
      "direction": "in"
    },
    {
      "name": "personEntity",
      "type": "table",
      "tableName": "Person",
      "partitionKey": "Test",
      "rowKey": "{queueTrigger}",
      "connection": "MyStorageConnection",
      "direction": "in"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="88529-139">Zie het voorbeeld taalspecifieke die een met één Tabelentiteit leest.</span><span class="sxs-lookup"><span data-stu-id="88529-139">See the language-specific sample that reads a single table entity.</span></span>

* [<span data-ttu-id="88529-140">C#</span><span class="sxs-lookup"><span data-stu-id="88529-140">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="88529-141">F#</span><span class="sxs-lookup"><span data-stu-id="88529-141">F#</span></span>](#inputfsharp)
* [<span data-ttu-id="88529-142">Node.js</span><span class="sxs-lookup"><span data-stu-id="88529-142">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="88529-143">Invoer voorbeeld in C#</span><span class="sxs-lookup"><span data-stu-id="88529-143">Input sample in C#</span></span> #
```csharp
public static void Run(string myQueueItem, Person personEntity, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    log.Info($"Name in Person entity: {personEntity.Name}");
}

public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
}
```

<a name="inputfsharp"></a>

### <a name="input-sample-in-f"></a><span data-ttu-id="88529-144">Invoer voorbeeld in F #</span><span class="sxs-lookup"><span data-stu-id="88529-144">Input sample in F#</span></span> #
```fsharp
[<CLIMutable>]
type Person = {
  PartitionKey: string
  RowKey: string
  Name: string
}

let Run(myQueueItem: string, personEntity: Person) =
    log.Info(sprintf "F# Queue trigger function processed: %s" myQueueItem)
    log.Info(sprintf "Name in Person entity: %s" personEntity.Name)
```

<a name="inputnodejs"></a>

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="88529-145">Invoer voorbeeld in Node.js</span><span class="sxs-lookup"><span data-stu-id="88529-145">Input sample in Node.js</span></span>
```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);
    context.log('Person entity name: ' + context.bindings.personEntity.Name);
    context.done();
};
```

<a name="output"></a>

## <a name="storage-table-output-binding"></a><span data-ttu-id="88529-146">Table Storage uitvoer binding</span><span class="sxs-lookup"><span data-stu-id="88529-146">Storage table output binding</span></span>
<span data-ttu-id="88529-147">De uitvoer van de Azure Storage-tabel binding kunt tabel u entiteiten schrijven naar een opslag in de functie.</span><span class="sxs-lookup"><span data-stu-id="88529-147">The Azure Storage table output binding enables you to write entities to a Storage table in your function.</span></span> 

<span data-ttu-id="88529-148">De opslag tabel uitvoer voor een functie maakt gebruik van de volgende JSON-objecten in de `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="88529-148">The Storage table output for a function uses the following JSON objects in the `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "out",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity to write - see below>",
    "rowKey": "<RowKey of table entity to write - see below>",
    "connection": "<Name of app setting - see below>",
}
```

<span data-ttu-id="88529-149">Houd rekening met het volgende:</span><span class="sxs-lookup"><span data-stu-id="88529-149">Note the following:</span></span> 

* <span data-ttu-id="88529-150">Gebruik `partitionKey` en `rowKey` samen om te schrijven één entiteit.</span><span class="sxs-lookup"><span data-stu-id="88529-150">Use `partitionKey` and `rowKey` together to write a single entity.</span></span> <span data-ttu-id="88529-151">Deze eigenschappen zijn optioneel.</span><span class="sxs-lookup"><span data-stu-id="88529-151">These properties are optional.</span></span> <span data-ttu-id="88529-152">U kunt ook opgeven `PartitionKey` en `RowKey` wanneer u de entiteitsobjecten in uw functiecode maakt.</span><span class="sxs-lookup"><span data-stu-id="88529-152">You can also specify `PartitionKey` and `RowKey` when you create the entity objects in your function code.</span></span>
* <span data-ttu-id="88529-153">`connection`moet de naam van een app-instelling met een verbindingsreeks voor opslag bevatten.</span><span class="sxs-lookup"><span data-stu-id="88529-153">`connection` must contain the name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="88529-154">In de Azure portal, de standaard editor in de **integreren** tabblad configureert u deze appinstelling voor wanneer u een opslagruimte maakt account of een bestaande selecteert.</span><span class="sxs-lookup"><span data-stu-id="88529-154">In the Azure portal, the standard editor in the **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="88529-155">U kunt ook [configureren van deze app handmatig instellen](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="88529-155">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span> 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="88529-156">Gebruik voor uitvoer</span><span class="sxs-lookup"><span data-stu-id="88529-156">Output usage</span></span>
<span data-ttu-id="88529-157">In C# functies, bindt u aan de tabeluitvoer van de met behulp van de benoemde `out` parameter in de functiehandtekening, zoals `out <T> <name>`, waarbij `T` is het gegevenstype dat u wilt serialiseren van de gegevens in, en `paramName` is de naam die u hebt opgegeven in de [uitvoer binding](#output).</span><span class="sxs-lookup"><span data-stu-id="88529-157">In C# functions, you bind to the table output by using the named `out` parameter in your function signature, like `out <T> <name>`, where `T` is the data type that you want to serialize the data into, and `paramName` is the name you specified in the [output binding](#output).</span></span> <span data-ttu-id="88529-158">In een Node.js-functies, opent u de uitvoer met behulp van tabel `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="88529-158">In Node.js functions, you access the table output using `context.bindings.<name>`.</span></span>

<span data-ttu-id="88529-159">Objecten in Node.js- of C#-functies kunnen worden geserialiseerd.</span><span class="sxs-lookup"><span data-stu-id="88529-159">You can serialize objects in Node.js or C# functions.</span></span> <span data-ttu-id="88529-160">In C# functies, kunt u ook koppelen aan de volgende typen:</span><span class="sxs-lookup"><span data-stu-id="88529-160">In C# functions, you can also bind to the following types:</span></span>

* <span data-ttu-id="88529-161">Type dat wordt geïmplementeerd`ITableEntity`</span><span class="sxs-lookup"><span data-stu-id="88529-161">Any type that implements `ITableEntity`</span></span>
* <span data-ttu-id="88529-162">`ICollector<T>`(om de uitvoer van meerdere entiteiten.</span><span class="sxs-lookup"><span data-stu-id="88529-162">`ICollector<T>` (to output multiple entities.</span></span> <span data-ttu-id="88529-163">Zie [voorbeeld](#outcsharp).)</span><span class="sxs-lookup"><span data-stu-id="88529-163">See [sample](#outcsharp).)</span></span>
* <span data-ttu-id="88529-164">`IAsyncCollector<T>`(async-versie van `ICollector<T>`)</span><span class="sxs-lookup"><span data-stu-id="88529-164">`IAsyncCollector<T>` (async version of `ICollector<T>`)</span></span>
* <span data-ttu-id="88529-165">`CloudTable`(met behulp van de Azure-opslag-SDK.</span><span class="sxs-lookup"><span data-stu-id="88529-165">`CloudTable` (using the Azure Storage SDK.</span></span> <span data-ttu-id="88529-166">Zie [voorbeeld](#readmulti).)</span><span class="sxs-lookup"><span data-stu-id="88529-166">See [sample](#readmulti).)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="88529-167">Voorbeeld van uitvoer</span><span class="sxs-lookup"><span data-stu-id="88529-167">Output sample</span></span>
<span data-ttu-id="88529-168">De volgende *function.json* en *run.csx* voorbeeld ziet u het schrijven van meerdere tabelentiteiten.</span><span class="sxs-lookup"><span data-stu-id="88529-168">The following *function.json* and *run.csx* example shows how to write multiple table entities.</span></span>

```json
{
  "bindings": [
    {
      "name": "input",
      "type": "manualTrigger",
      "direction": "in"
    },
    {
      "tableName": "Person",
      "connection": "MyStorageConnection",
      "name": "tableBinding",
      "type": "table",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="88529-169">Zie het voorbeeld taalspecifieke die meerdere tabelentiteiten worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="88529-169">See the language-specific sample that creates multiple table entities.</span></span>

* [<span data-ttu-id="88529-170">C#</span><span class="sxs-lookup"><span data-stu-id="88529-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="88529-171">F#</span><span class="sxs-lookup"><span data-stu-id="88529-171">F#</span></span>](#outfsharp)
* [<span data-ttu-id="88529-172">Node.js</span><span class="sxs-lookup"><span data-stu-id="88529-172">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="88529-173">Voorbeeld van uitvoer in C#</span><span class="sxs-lookup"><span data-stu-id="88529-173">Output sample in C#</span></span> #
```csharp
public static void Run(string input, ICollector<Person> tableBinding, TraceWriter log)
{
    for (int i = 1; i < 10; i++)
        {
            log.Info($"Adding Person entity {i}");
            tableBinding.Add(
                new Person() { 
                    PartitionKey = "Test", 
                    RowKey = i.ToString(), 
                    Name = "Name" + i.ToString() }
                );
        }

}

public class Person
{
    public string PartitionKey { get; set; }
    public string RowKey { get; set; }
    public string Name { get; set; }
}

```
<a name="outfsharp"></a>

### <a name="output-sample-in-f"></a><span data-ttu-id="88529-174">Voorbeeld van uitvoer in F #</span><span class="sxs-lookup"><span data-stu-id="88529-174">Output sample in F#</span></span> #
```fsharp
[<CLIMutable>]
type Person = {
  PartitionKey: string
  RowKey: string
  Name: string
}

let Run(input: string, tableBinding: ICollector<Person>, log: TraceWriter) =
    for i = 1 to 10 do
        log.Info(sprintf "Adding Person entity %d" i)
        tableBinding.Add(
            { PartitionKey = "Test"
              RowKey = i.ToString()
              Name = "Name" + i.ToString() })
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="88529-175">Voorbeeld van uitvoer in Node.js</span><span class="sxs-lookup"><span data-stu-id="88529-175">Output sample in Node.js</span></span>
```javascript
module.exports = function (context) {

    context.bindings.tableBinding = [];

    for (var i = 1; i < 10; i++) {
        context.bindings.tableBinding.push({
            PartitionKey: "Test",
            RowKey: i.toString(),
            Name: "Name " + i
        });
    }
    
    context.done();
};
```

<a name="readmulti"></a>

## <a name="sample-read-multiple-table-entities-in-c"></a><span data-ttu-id="88529-176">Voorbeeld: Meerdere tabelentiteiten in C# lezen</span><span class="sxs-lookup"><span data-stu-id="88529-176">Sample: Read multiple table entities in C#</span></span>  #
<span data-ttu-id="88529-177">De volgende *function.json* en C#-codevoorbeeld entiteiten voor een partitiesleutel die is opgegeven in het bericht uit de wachtrij staat.</span><span class="sxs-lookup"><span data-stu-id="88529-177">The following *function.json* and C# code example reads entities for a partition key that is specified in the queue message.</span></span>

```json
{
  "bindings": [
    {
      "queueName": "myqueue-items",
      "connection": "MyStorageConnection",
      "name": "myQueueItem",
      "type": "queueTrigger",
      "direction": "in"
    },
    {
      "name": "tableBinding",
      "type": "table",
      "connection": "MyStorageConnection",
      "tableName": "Person",
      "direction": "in"
    }
  ],
  "disabled": false
}
```

<span data-ttu-id="88529-178">De C#-code een verwijzing naar de Azure-opslag-SDK wordt toegevoegd zodat het entiteitstype kan worden afgeleid van `TableEntity`.</span><span class="sxs-lookup"><span data-stu-id="88529-178">The C# code adds a reference to the Azure Storage SDK so that the entity type can derive from `TableEntity`.</span></span>

```csharp
#r "Microsoft.WindowsAzure.Storage"
using Microsoft.WindowsAzure.Storage.Table;

public static void Run(string myQueueItem, IQueryable<Person> tableBinding, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    foreach (Person person in tableBinding.Where(p => p.PartitionKey == myQueueItem).ToList())
    {
        log.Info($"Name: {person.Name}");
    }
}

public class Person : TableEntity
{
    public string Name { get; set; }
}
```

## <a name="next-steps"></a><span data-ttu-id="88529-179">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="88529-179">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

