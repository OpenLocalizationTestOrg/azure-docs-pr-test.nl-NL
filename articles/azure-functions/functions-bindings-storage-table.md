---
title: aaaAzure functies opslag tabel bindingen | Microsoft Docs
description: Begrijpen hoe Azure Storage-bindingen toouse in Azure Functions.
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
ms.openlocfilehash: 90c2a73329139d4ab3504bc0e2c90370133158bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-storage-table-bindings"></a><span data-ttu-id="627c4-104">Azure Functions opslag Tabelverbindingen</span><span class="sxs-lookup"><span data-stu-id="627c4-104">Azure Functions Storage table bindings</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="627c4-105">Dit artikel wordt uitgelegd hoe tabel bindingen in de Azure Functions tooconfigure en Azure Storage-code.</span><span class="sxs-lookup"><span data-stu-id="627c4-105">This article explains how tooconfigure and code Azure Storage table bindings in Azure Functions.</span></span> <span data-ttu-id="627c4-106">Azure Functions ondersteunt invoer en uitvoer van de bindingen voor Azure Storage-tabellen.</span><span class="sxs-lookup"><span data-stu-id="627c4-106">Azure Functions supports input and output bindings for Azure Storage tables.</span></span>

<span data-ttu-id="627c4-107">Hallo opslag tabelbinding ondersteunt Hallo volgen scenario's:</span><span class="sxs-lookup"><span data-stu-id="627c4-107">hello Storage table binding supports hello following scenarios:</span></span>

* <span data-ttu-id="627c4-108">**Lezen van een enkele rij in een C# of Node.js-functie** : Stel `partitionKey` en `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="627c4-108">**Read a single row in a C# or Node.js function** - Set `partitionKey` and `rowKey`.</span></span> <span data-ttu-id="627c4-109">Hallo `filter` en `take` eigenschappen worden niet gebruikt in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="627c4-109">hello `filter` and `take` properties are not used in this scenario.</span></span>
* <span data-ttu-id="627c4-110">**Lezen van meerdere rijen in een C#-functie** -Hallo functies runtime biedt een `IQueryable<T>` object afhankelijk is van de tabel toohello.</span><span class="sxs-lookup"><span data-stu-id="627c4-110">**Read multiple rows in a C# function** - hello Functions runtime provides an `IQueryable<T>` object bound toohello table.</span></span> <span data-ttu-id="627c4-111">Type `T` moet worden afgeleid van `TableEntity` of implementeert `ITableEntity`.</span><span class="sxs-lookup"><span data-stu-id="627c4-111">Type `T` must derive from `TableEntity` or implement `ITableEntity`.</span></span> <span data-ttu-id="627c4-112">Hallo `partitionKey`, `rowKey`, `filter`, en `take` eigenschappen worden niet gebruikt in dit scenario; u kunt Hallo `IQueryable` object toodo filteren vereist.</span><span class="sxs-lookup"><span data-stu-id="627c4-112">hello `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario; you can use hello `IQueryable` object toodo any filtering required.</span></span> 
* <span data-ttu-id="627c4-113">**Lezen van meerdere rijen in een functie knooppunt** : Stel hello `filter` en `take` eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="627c4-113">**Read multiple rows in a Node function** - Set hello `filter` and `take` properties.</span></span> <span data-ttu-id="627c4-114">Stelt niet `partitionKey` of `rowKey`.</span><span class="sxs-lookup"><span data-stu-id="627c4-114">Don't set `partitionKey` or `rowKey`.</span></span>
* <span data-ttu-id="627c4-115">**Schrijven van een of meer rijen in een C#-functie** -Hallo functies runtime biedt een `ICollector<T>` of `IAsyncCollector<T>` gebonden toohello tabel, waarbij `T` Hallo schema geeft Hallo entiteiten gewenste tooadd.</span><span class="sxs-lookup"><span data-stu-id="627c4-115">**Write one or more rows in a C# function** - hello Functions runtime provides an `ICollector<T>` or `IAsyncCollector<T>` bound toohello table, where `T` specifies hello schema of hello entities you want tooadd.</span></span> <span data-ttu-id="627c4-116">Normaal gesproken Typ `T` is afgeleid van `TableEntity` of implementeert `ITableEntity`, maar deze hoeft niet te.</span><span class="sxs-lookup"><span data-stu-id="627c4-116">Typically, type `T` derives from `TableEntity` or implements `ITableEntity`, but it doesn't have to.</span></span> <span data-ttu-id="627c4-117">Hallo `partitionKey`, `rowKey`, `filter`, en `take` eigenschappen worden niet gebruikt in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="627c4-117">hello `partitionKey`, `rowKey`, `filter`, and `take` properties are not used in this scenario.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="storage-table-input-binding"></a><span data-ttu-id="627c4-118">Invoer tabelbinding opslag</span><span class="sxs-lookup"><span data-stu-id="627c4-118">Storage table input binding</span></span>
<span data-ttu-id="627c4-119">Hallo invoer tabelbinding Azure Storage kunt u een tabel opslag in uw functie toouse.</span><span class="sxs-lookup"><span data-stu-id="627c4-119">hello Azure Storage table input binding enables you toouse a storage table in your function.</span></span> 

<span data-ttu-id="627c4-120">Hallo opslagfunctie tabel invoer tooa gebruikt Hallo volgende JSON-objecten in Hallo `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="627c4-120">hello Storage table input tooa function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "in",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity tooread - see below>",
    "rowKey": "<RowKey of table entity tooread - see below>",
    "take": "<Maximum number of entities tooread in Node.js - optional>",
    "filter": "<OData filter expression for table input in Node.js - optional>",
    "connection": "<Name of app setting - see below>",
}
```

<span data-ttu-id="627c4-121">Let op Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="627c4-121">Note hello following:</span></span> 

* <span data-ttu-id="627c4-122">Gebruik `partitionKey` en `rowKey` samen tooread één entiteit.</span><span class="sxs-lookup"><span data-stu-id="627c4-122">Use `partitionKey` and `rowKey` together tooread a single entity.</span></span> <span data-ttu-id="627c4-123">Deze eigenschappen zijn optioneel.</span><span class="sxs-lookup"><span data-stu-id="627c4-123">These properties are optional.</span></span> 
* <span data-ttu-id="627c4-124">`connection`Hallo-naam van een app-instelling met een verbindingsreeks voor opslag moet worden bevatten.</span><span class="sxs-lookup"><span data-stu-id="627c4-124">`connection` must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="627c4-125">Hallo in hello Azure-portal, standaardeditor in Hallo **integreren** tabblad configureert u deze appinstelling voor wanneer u een opslagruimte maakt account of een bestaande selecteert.</span><span class="sxs-lookup"><span data-stu-id="627c4-125">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="627c4-126">U kunt ook [configureren van deze app handmatig instellen](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="627c4-126">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span>  

<a name="inputusage"></a>

## <a name="input-usage"></a><span data-ttu-id="627c4-127">Invoer-gebruik</span><span class="sxs-lookup"><span data-stu-id="627c4-127">Input usage</span></span>
<span data-ttu-id="627c4-128">In de C# functies, bindt u toohello invoer tabel entiteit (of entiteiten) met behulp van een benoemde parameter in de functiehandtekening, zoals `<T> <name>`.</span><span class="sxs-lookup"><span data-stu-id="627c4-128">In C# functions, you bind toohello input table entity (or entities) by using a named parameter in your function signature, like `<T> <name>`.</span></span>
<span data-ttu-id="627c4-129">Waar `T` is Hallo gegevenstype dat u wilt dat toodeserialize Hallo gegevens in, en `paramName` is Hallo-naam die u hebt opgegeven in Hallo [invoer binding](#input).</span><span class="sxs-lookup"><span data-stu-id="627c4-129">Where `T` is hello data type that you want toodeserialize hello data into, and `paramName` is hello name you specified in hello [input binding](#input).</span></span> <span data-ttu-id="627c4-130">In een Node.js-functies, opent u de Hallo invoer tabel entiteit (of entiteiten) met behulp van `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="627c4-130">In Node.js functions, you access hello input table entity (or entities) using `context.bindings.<name>`.</span></span>

<span data-ttu-id="627c4-131">Hallo invoergegevens kunnen worden gedeserialiseerd in Node.js- of C#-functies.</span><span class="sxs-lookup"><span data-stu-id="627c4-131">hello input data can be deserialized in Node.js or C# functions.</span></span> <span data-ttu-id="627c4-132">Hallo gedeserialiseerd objecten hebben `RowKey` en `PartitionKey` eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="627c4-132">hello deserialized objects have `RowKey` and `PartitionKey` properties.</span></span>

<span data-ttu-id="627c4-133">U kunt ook tooany van de volgende typen Hallo binden in C#-functies, en Hallo functies runtime wordt geprobeerd te deserialiseren Hallo tabelgegevens met behulp van dat type:</span><span class="sxs-lookup"><span data-stu-id="627c4-133">In C# functions, you can also bind tooany of hello following types, and hello Functions runtime will attempt too deserialize hello table data using that type:</span></span>

* <span data-ttu-id="627c4-134">Type dat wordt geïmplementeerd`ITableEntity`</span><span class="sxs-lookup"><span data-stu-id="627c4-134">Any type that implements `ITableEntity`</span></span>
* `IQueryable<T>`

<a name="inputsample"></a>

## <a name="input-sample"></a><span data-ttu-id="627c4-135">Voorbeeld van invoer</span><span class="sxs-lookup"><span data-stu-id="627c4-135">Input sample</span></span>
<span data-ttu-id="627c4-136">Stel, dat u hebt Hallo function.json dat gebruikmaakt van een wachtrij trigger tooread een enkele tabelrij te volgen.</span><span class="sxs-lookup"><span data-stu-id="627c4-136">Supposed you have hello following function.json, which uses a queue trigger tooread a single table row.</span></span> <span data-ttu-id="627c4-137">Hallo JSON geeft `PartitionKey`  
 `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="627c4-137">hello JSON specifies `PartitionKey` 
`RowKey`.</span></span> <span data-ttu-id="627c4-138">`"rowKey": "{queueTrigger}"`Hiermee wordt aangegeven dat rijsleutel Hallo afkomstig is van Hallo wachtrij bericht tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="627c4-138">`"rowKey": "{queueTrigger}"` indicates that hello row key comes from hello queue message string.</span></span>

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

<span data-ttu-id="627c4-139">Zie Hallo taalspecifieke voorbeeldquery die een met één Tabelentiteit leest.</span><span class="sxs-lookup"><span data-stu-id="627c4-139">See hello language-specific sample that reads a single table entity.</span></span>

* [<span data-ttu-id="627c4-140">C#</span><span class="sxs-lookup"><span data-stu-id="627c4-140">C#</span></span>](#inputcsharp)
* [<span data-ttu-id="627c4-141">F#</span><span class="sxs-lookup"><span data-stu-id="627c4-141">F#</span></span>](#inputfsharp)
* [<span data-ttu-id="627c4-142">Node.js</span><span class="sxs-lookup"><span data-stu-id="627c4-142">Node.js</span></span>](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a><span data-ttu-id="627c4-143">Invoer voorbeeld in C#</span><span class="sxs-lookup"><span data-stu-id="627c4-143">Input sample in C#</span></span> #
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

### <a name="input-sample-in-f"></a><span data-ttu-id="627c4-144">Invoer voorbeeld in F #</span><span class="sxs-lookup"><span data-stu-id="627c4-144">Input sample in F#</span></span> #
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

### <a name="input-sample-in-nodejs"></a><span data-ttu-id="627c4-145">Invoer voorbeeld in Node.js</span><span class="sxs-lookup"><span data-stu-id="627c4-145">Input sample in Node.js</span></span>
```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);
    context.log('Person entity name: ' + context.bindings.personEntity.Name);
    context.done();
};
```

<a name="output"></a>

## <a name="storage-table-output-binding"></a><span data-ttu-id="627c4-146">Table Storage uitvoer binding</span><span class="sxs-lookup"><span data-stu-id="627c4-146">Storage table output binding</span></span>
<span data-ttu-id="627c4-147">Hello Azure Storage tabel uitvoer binding kunt u toowrite entiteiten tooa opslag tabel in de functie.</span><span class="sxs-lookup"><span data-stu-id="627c4-147">hello Azure Storage table output binding enables you toowrite entities tooa Storage table in your function.</span></span> 

<span data-ttu-id="627c4-148">Hallo tabeluitvoer van opslag voor een functie gebruikt de volgende JSON-objecten in Hallo Hallo `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="627c4-148">hello Storage table output for a function uses hello following JSON objects in hello `bindings` array of function.json:</span></span>

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "table",
    "direction": "out",
    "tableName": "<Name of Storage table>",
    "partitionKey": "<PartitionKey of table entity toowrite - see below>",
    "rowKey": "<RowKey of table entity toowrite - see below>",
    "connection": "<Name of app setting - see below>",
}
```

<span data-ttu-id="627c4-149">Let op Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="627c4-149">Note hello following:</span></span> 

* <span data-ttu-id="627c4-150">Gebruik `partitionKey` en `rowKey` samen toowrite één entiteit.</span><span class="sxs-lookup"><span data-stu-id="627c4-150">Use `partitionKey` and `rowKey` together toowrite a single entity.</span></span> <span data-ttu-id="627c4-151">Deze eigenschappen zijn optioneel.</span><span class="sxs-lookup"><span data-stu-id="627c4-151">These properties are optional.</span></span> <span data-ttu-id="627c4-152">U kunt ook opgeven `PartitionKey` en `RowKey` wanneer u Hallo entiteitsobjecten maken in uw functiecode.</span><span class="sxs-lookup"><span data-stu-id="627c4-152">You can also specify `PartitionKey` and `RowKey` when you create hello entity objects in your function code.</span></span>
* <span data-ttu-id="627c4-153">`connection`Hallo-naam van een app-instelling met een verbindingsreeks voor opslag moet worden bevatten.</span><span class="sxs-lookup"><span data-stu-id="627c4-153">`connection` must contain hello name of an app setting that contains a storage connection string.</span></span> <span data-ttu-id="627c4-154">Hallo in hello Azure-portal, standaardeditor in Hallo **integreren** tabblad configureert u deze appinstelling voor wanneer u een opslagruimte maakt account of een bestaande selecteert.</span><span class="sxs-lookup"><span data-stu-id="627c4-154">In hello Azure portal, hello standard editor in hello **Integrate** tab configures this app setting for you when you create a Storage account or selects an existing one.</span></span> <span data-ttu-id="627c4-155">U kunt ook [configureren van deze app handmatig instellen](functions-how-to-use-azure-function-app-settings.md#settings).</span><span class="sxs-lookup"><span data-stu-id="627c4-155">You can also [configure this app setting manually](functions-how-to-use-azure-function-app-settings.md#settings).</span></span> 

<a name="outputusage"></a>

## <a name="output-usage"></a><span data-ttu-id="627c4-156">Gebruik voor uitvoer</span><span class="sxs-lookup"><span data-stu-id="627c4-156">Output usage</span></span>
<span data-ttu-id="627c4-157">In de C# functies, bindt u toohello tabeluitvoer door gebruik te maken met de naam Hallo `out` parameter in de functiehandtekening, zoals `out <T> <name>`, waarbij `T` is Hallo gegevenstype dat u wilt dat tooserialize Hallo gegevens in, en `paramName` is Hallo servernaam die u hebt opgegeven in Hallo [uitvoer binding](#output).</span><span class="sxs-lookup"><span data-stu-id="627c4-157">In C# functions, you bind toohello table output by using hello named `out` parameter in your function signature, like `out <T> <name>`, where `T` is hello data type that you want tooserialize hello data into, and `paramName` is hello name you specified in hello [output binding](#output).</span></span> <span data-ttu-id="627c4-158">In een Node.js-functies, opent u Hallo tabel uitvoer met behulp van `context.bindings.<name>`.</span><span class="sxs-lookup"><span data-stu-id="627c4-158">In Node.js functions, you access hello table output using `context.bindings.<name>`.</span></span>

<span data-ttu-id="627c4-159">Objecten in Node.js- of C#-functies kunnen worden geserialiseerd.</span><span class="sxs-lookup"><span data-stu-id="627c4-159">You can serialize objects in Node.js or C# functions.</span></span> <span data-ttu-id="627c4-160">In C#-functies, kunt u ook na typen toohello binden:</span><span class="sxs-lookup"><span data-stu-id="627c4-160">In C# functions, you can also bind toohello following types:</span></span>

* <span data-ttu-id="627c4-161">Type dat wordt geïmplementeerd`ITableEntity`</span><span class="sxs-lookup"><span data-stu-id="627c4-161">Any type that implements `ITableEntity`</span></span>
* <span data-ttu-id="627c4-162">`ICollector<T>`(toooutput meerdere entiteiten.</span><span class="sxs-lookup"><span data-stu-id="627c4-162">`ICollector<T>` (toooutput multiple entities.</span></span> <span data-ttu-id="627c4-163">Zie [voorbeeld](#outcsharp).)</span><span class="sxs-lookup"><span data-stu-id="627c4-163">See [sample](#outcsharp).)</span></span>
* <span data-ttu-id="627c4-164">`IAsyncCollector<T>`(async-versie van `ICollector<T>`)</span><span class="sxs-lookup"><span data-stu-id="627c4-164">`IAsyncCollector<T>` (async version of `ICollector<T>`)</span></span>
* <span data-ttu-id="627c4-165">`CloudTable`(met behulp van hello Azure-opslag-SDK.</span><span class="sxs-lookup"><span data-stu-id="627c4-165">`CloudTable` (using hello Azure Storage SDK.</span></span> <span data-ttu-id="627c4-166">Zie [voorbeeld](#readmulti).)</span><span class="sxs-lookup"><span data-stu-id="627c4-166">See [sample](#readmulti).)</span></span>

<a name="outputsample"></a>

## <a name="output-sample"></a><span data-ttu-id="627c4-167">Voorbeeld van uitvoer</span><span class="sxs-lookup"><span data-stu-id="627c4-167">Output sample</span></span>
<span data-ttu-id="627c4-168">Hallo volgende *function.json* en *run.csx* voorbeeld wordt getoond hoe toowrite meerdere tabelentiteiten.</span><span class="sxs-lookup"><span data-stu-id="627c4-168">hello following *function.json* and *run.csx* example shows how toowrite multiple table entities.</span></span>

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

<span data-ttu-id="627c4-169">Zie Hallo taalspecifieke steekproef die wordt gemaakt van meerdere tabelentiteiten.</span><span class="sxs-lookup"><span data-stu-id="627c4-169">See hello language-specific sample that creates multiple table entities.</span></span>

* [<span data-ttu-id="627c4-170">C#</span><span class="sxs-lookup"><span data-stu-id="627c4-170">C#</span></span>](#outcsharp)
* [<span data-ttu-id="627c4-171">F#</span><span class="sxs-lookup"><span data-stu-id="627c4-171">F#</span></span>](#outfsharp)
* [<span data-ttu-id="627c4-172">Node.js</span><span class="sxs-lookup"><span data-stu-id="627c4-172">Node.js</span></span>](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a><span data-ttu-id="627c4-173">Voorbeeld van uitvoer in C#</span><span class="sxs-lookup"><span data-stu-id="627c4-173">Output sample in C#</span></span> #
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

### <a name="output-sample-in-f"></a><span data-ttu-id="627c4-174">Voorbeeld van uitvoer in F #</span><span class="sxs-lookup"><span data-stu-id="627c4-174">Output sample in F#</span></span> #
```fsharp
[<CLIMutable>]
type Person = {
  PartitionKey: string
  RowKey: string
  Name: string
}

let Run(input: string, tableBinding: ICollector<Person>, log: TraceWriter) =
    for i = 1 too10 do
        log.Info(sprintf "Adding Person entity %d" i)
        tableBinding.Add(
            { PartitionKey = "Test"
              RowKey = i.ToString()
              Name = "Name" + i.ToString() })
```

<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a><span data-ttu-id="627c4-175">Voorbeeld van uitvoer in Node.js</span><span class="sxs-lookup"><span data-stu-id="627c4-175">Output sample in Node.js</span></span>
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

## <a name="sample-read-multiple-table-entities-in-c"></a><span data-ttu-id="627c4-176">Voorbeeld: Meerdere tabelentiteiten in C# lezen</span><span class="sxs-lookup"><span data-stu-id="627c4-176">Sample: Read multiple table entities in C#</span></span>  #
<span data-ttu-id="627c4-177">Hallo volgende *function.json* en C#-codevoorbeeld leest entiteiten voor een partitiesleutel die is opgegeven in de wachtrij het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="627c4-177">hello following *function.json* and C# code example reads entities for a partition key that is specified in hello queue message.</span></span>

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

<span data-ttu-id="627c4-178">Hallo C#-code een verwijzing toohello Azure-opslag-SDK wordt toegevoegd zodat Hallo entiteitstype kan worden afgeleid van `TableEntity`.</span><span class="sxs-lookup"><span data-stu-id="627c4-178">hello C# code adds a reference toohello Azure Storage SDK so that hello entity type can derive from `TableEntity`.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="627c4-179">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="627c4-179">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

