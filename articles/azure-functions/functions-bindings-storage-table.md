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
# <a name="azure-functions-storage-table-bindings"></a>Azure Functions opslag Tabelverbindingen
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Dit artikel wordt uitgelegd hoe tabel bindingen in de Azure Functions tooconfigure en Azure Storage-code. Azure Functions ondersteunt invoer en uitvoer van de bindingen voor Azure Storage-tabellen.

Hallo opslag tabelbinding ondersteunt Hallo volgen scenario's:

* **Lezen van een enkele rij in een C# of Node.js-functie** : Stel `partitionKey` en `rowKey`. Hallo `filter` en `take` eigenschappen worden niet gebruikt in dit scenario.
* **Lezen van meerdere rijen in een C#-functie** -Hallo functies runtime biedt een `IQueryable<T>` object afhankelijk is van de tabel toohello. Type `T` moet worden afgeleid van `TableEntity` of implementeert `ITableEntity`. Hallo `partitionKey`, `rowKey`, `filter`, en `take` eigenschappen worden niet gebruikt in dit scenario; u kunt Hallo `IQueryable` object toodo filteren vereist. 
* **Lezen van meerdere rijen in een functie knooppunt** : Stel hello `filter` en `take` eigenschappen. Stelt niet `partitionKey` of `rowKey`.
* **Schrijven van een of meer rijen in een C#-functie** -Hallo functies runtime biedt een `ICollector<T>` of `IAsyncCollector<T>` gebonden toohello tabel, waarbij `T` Hallo schema geeft Hallo entiteiten gewenste tooadd. Normaal gesproken Typ `T` is afgeleid van `TableEntity` of implementeert `ITableEntity`, maar deze hoeft niet te. Hallo `partitionKey`, `rowKey`, `filter`, en `take` eigenschappen worden niet gebruikt in dit scenario.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="storage-table-input-binding"></a>Invoer tabelbinding opslag
Hallo invoer tabelbinding Azure Storage kunt u een tabel opslag in uw functie toouse. 

Hallo opslagfunctie tabel invoer tooa gebruikt Hallo volgende JSON-objecten in Hallo `bindings` matrix van function.json:

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

Let op Hallo volgende: 

* Gebruik `partitionKey` en `rowKey` samen tooread één entiteit. Deze eigenschappen zijn optioneel. 
* `connection`Hallo-naam van een app-instelling met een verbindingsreeks voor opslag moet worden bevatten. Hallo in hello Azure-portal, standaardeditor in Hallo **integreren** tabblad configureert u deze appinstelling voor wanneer u een opslagruimte maakt account of een bestaande selecteert. U kunt ook [configureren van deze app handmatig instellen](functions-how-to-use-azure-function-app-settings.md#settings).  

<a name="inputusage"></a>

## <a name="input-usage"></a>Invoer-gebruik
In de C# functies, bindt u toohello invoer tabel entiteit (of entiteiten) met behulp van een benoemde parameter in de functiehandtekening, zoals `<T> <name>`.
Waar `T` is Hallo gegevenstype dat u wilt dat toodeserialize Hallo gegevens in, en `paramName` is Hallo-naam die u hebt opgegeven in Hallo [invoer binding](#input). In een Node.js-functies, opent u de Hallo invoer tabel entiteit (of entiteiten) met behulp van `context.bindings.<name>`.

Hallo invoergegevens kunnen worden gedeserialiseerd in Node.js- of C#-functies. Hallo gedeserialiseerd objecten hebben `RowKey` en `PartitionKey` eigenschappen.

U kunt ook tooany van de volgende typen Hallo binden in C#-functies, en Hallo functies runtime wordt geprobeerd te deserialiseren Hallo tabelgegevens met behulp van dat type:

* Type dat wordt geïmplementeerd`ITableEntity`
* `IQueryable<T>`

<a name="inputsample"></a>

## <a name="input-sample"></a>Voorbeeld van invoer
Stel, dat u hebt Hallo function.json dat gebruikmaakt van een wachtrij trigger tooread een enkele tabelrij te volgen. Hallo JSON geeft `PartitionKey`  
 `RowKey`. `"rowKey": "{queueTrigger}"`Hiermee wordt aangegeven dat rijsleutel Hallo afkomstig is van Hallo wachtrij bericht tekenreeks.

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

Zie Hallo taalspecifieke voorbeeldquery die een met één Tabelentiteit leest.

* [C#](#inputcsharp)
* [F#](#inputfsharp)
* [Node.js](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a>Invoer voorbeeld in C# #
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

### <a name="input-sample-in-f"></a>Invoer voorbeeld in F # #
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

### <a name="input-sample-in-nodejs"></a>Invoer voorbeeld in Node.js
```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);
    context.log('Person entity name: ' + context.bindings.personEntity.Name);
    context.done();
};
```

<a name="output"></a>

## <a name="storage-table-output-binding"></a>Table Storage uitvoer binding
Hello Azure Storage tabel uitvoer binding kunt u toowrite entiteiten tooa opslag tabel in de functie. 

Hallo tabeluitvoer van opslag voor een functie gebruikt de volgende JSON-objecten in Hallo Hallo `bindings` matrix van function.json:

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

Let op Hallo volgende: 

* Gebruik `partitionKey` en `rowKey` samen toowrite één entiteit. Deze eigenschappen zijn optioneel. U kunt ook opgeven `PartitionKey` en `RowKey` wanneer u Hallo entiteitsobjecten maken in uw functiecode.
* `connection`Hallo-naam van een app-instelling met een verbindingsreeks voor opslag moet worden bevatten. Hallo in hello Azure-portal, standaardeditor in Hallo **integreren** tabblad configureert u deze appinstelling voor wanneer u een opslagruimte maakt account of een bestaande selecteert. U kunt ook [configureren van deze app handmatig instellen](functions-how-to-use-azure-function-app-settings.md#settings). 

<a name="outputusage"></a>

## <a name="output-usage"></a>Gebruik voor uitvoer
In de C# functies, bindt u toohello tabeluitvoer door gebruik te maken met de naam Hallo `out` parameter in de functiehandtekening, zoals `out <T> <name>`, waarbij `T` is Hallo gegevenstype dat u wilt dat tooserialize Hallo gegevens in, en `paramName` is Hallo servernaam die u hebt opgegeven in Hallo [uitvoer binding](#output). In een Node.js-functies, opent u Hallo tabel uitvoer met behulp van `context.bindings.<name>`.

Objecten in Node.js- of C#-functies kunnen worden geserialiseerd. In C#-functies, kunt u ook na typen toohello binden:

* Type dat wordt geïmplementeerd`ITableEntity`
* `ICollector<T>`(toooutput meerdere entiteiten. Zie [voorbeeld](#outcsharp).)
* `IAsyncCollector<T>`(async-versie van `ICollector<T>`)
* `CloudTable`(met behulp van hello Azure-opslag-SDK. Zie [voorbeeld](#readmulti).)

<a name="outputsample"></a>

## <a name="output-sample"></a>Voorbeeld van uitvoer
Hallo volgende *function.json* en *run.csx* voorbeeld wordt getoond hoe toowrite meerdere tabelentiteiten.

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

Zie Hallo taalspecifieke steekproef die wordt gemaakt van meerdere tabelentiteiten.

* [C#](#outcsharp)
* [F#](#outfsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Voorbeeld van uitvoer in C# #
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

### <a name="output-sample-in-f"></a>Voorbeeld van uitvoer in F # #
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

### <a name="output-sample-in-nodejs"></a>Voorbeeld van uitvoer in Node.js
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

## <a name="sample-read-multiple-table-entities-in-c"></a>Voorbeeld: Meerdere tabelentiteiten in C# lezen  #
Hallo volgende *function.json* en C#-codevoorbeeld leest entiteiten voor een partitiesleutel die is opgegeven in de wachtrij het Hallo-bericht.

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

Hallo C#-code een verwijzing toohello Azure-opslag-SDK wordt toegevoegd zodat Hallo entiteitstype kan worden afgeleid van `TableEntity`.

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

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

