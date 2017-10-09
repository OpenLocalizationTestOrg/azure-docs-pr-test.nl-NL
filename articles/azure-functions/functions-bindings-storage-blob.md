---
title: aaaAzure functies Blob Storage bindingen | Microsoft Docs
description: Begrijpen hoe Azure Storage toouse triggers en bindingen in Azure Functions.
services: functions
documentationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: Azure functions, functies, verwerking van gebeurtenissen, dynamische compute zonder server architectuur
ms.assetid: aba8976c-6568-4ec7-86f5-410efd6b0fb9
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: cef44bd2154d0b97cca9220b6c5024a5b620c80d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-blob-storage-bindings"></a>Azure Functions Blob storage-bindingen
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Dit artikel wordt uitgelegd hoe tooconfigure en werken met Azure Blob storage bindingen in de Azure Functions. Azure Functions ondersteunt worden geactiveerd, invoer en uitvoer van de bindingen voor Azure Blob-opslag. Zie functies die beschikbaar in alle bindingen zijn [Azure Functions triggers en bindingen concepten](functions-triggers-bindings.md).

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

> [!NOTE]
> Een [blob storage-account](../storage/common/storage-create-storage-account.md#blob-storage-accounts) wordt niet ondersteund. BLOB storage triggers en bindingen vereisen een algemeen opslagaccount. 
> 

<a name="trigger"></a>
<a name="storage-blob-trigger"></a>
## <a name="blob-storage-triggers-and-bindings"></a>BLOB storage triggers en bindingen

Hallo Azure Blob storage-trigger gebruikt, wordt de functiecode aangeroepen wanneer een nieuwe of bijgewerkte blob wordt gedetecteerd. Hallo blob-inhoud worden geleverd als invoer toohello-functie.

Definieer een blob storage-trigger met Hallo **integreren** tabblad in Hallo Functions-portal. Hallo portal maakt na definitie in Hallo Hallo **bindingen** sectie van *function.json*:

```json
{
    "name": "<hello name used tooidentify hello trigger data in your code>",
    "type": "blobTrigger",
    "direction": "in",
    "path": "<container toomonitor, and optionally a blob name pattern - see below>",
    "connection": "<Name of app setting - see below>"
}
```

BLOB-invoer en uitvoer bindingen zijn gedefinieerd met behulp van `blob` als het bindingstype Hallo:

```json
{
  "name": "<hello name used tooidentify hello blob input in your code>",
  "type": "blob",
  "direction": "in", // other supported directions are "inout" and "out"
  "path": "<Path of input blob - see below>",
  "connection":"<Name of app setting - see below>"
},
```

* Hallo `path` ondersteunt de eigenschap binding expressies en filterparameters. Zie [patronen naam](#pattern).
* Hallo `connection` eigenschap Hallo-naam van een app-instelling met een verbindingsreeks voor opslag moet bevatten. Hallo in hello Azure-portal, standaardeditor in Hallo **integreren** tabblad dit app-instelling die u configureert wanneer u een opslagaccount selecteren.

> [!NOTE]
> Wanneer u een blob-trigger op een plan verbruik, kunnen er up tooa 10 minuten vertraging bij de verwerking van nieuwe blobs nadat een functie-app niet actief is geworden. Nadat het Hallo-functie-app wordt uitgevoerd, worden onmiddellijk blobs verwerkt. Dit eerste tooavoid uitstellen, kunt u een Hallo volgende opties:
> - Gebruik een App Service-abonnement met altijd op ingeschakeld.
> - Gebruik een ander mechanisme tootrigger Hallo blob verwerken, zoals een wachtrijbericht die Hallo blob-naam bevat. Zie voor een voorbeeld [wachtrij trigger met blob invoer binding](#input-sample).

<a name="pattern"></a>

### <a name="name-patterns"></a>Bestandsnaampatronen
U kunt een naampatroon blob opgeven in Hallo `path` eigenschap, die een filter of binding-expressie. Zie [Binding expressies en patronen](functions-triggers-bindings.md#binding-expressions-and-patterns).

Bijvoorbeeld gebruiken toofilter tooblobs die beginnen met Hallo tekenreeks 'oorspronkelijke' hello definitie te volgen. Dit pad zoeken naar een blob met de naam *oorspronkelijke Blob1.txt* in Hallo *invoer* container en de waarde Hallo Hallo `name` variabele in functiecode is `Blob1`.

```json
"path": "input/original-{name}",
```

toobind toohello blob-bestandsnaam en extensie afzonderlijk twee patronen te gebruiken. Dit pad ook zoeken naar een blob met de naam *oorspronkelijke Blob1.txt*, en de waarde van Hallo Hallo `blobname` en `blobextension` variabelen in de functiecode zijn *oorspronkelijke Blob1* en *txt*.

```json
"path": "input/{blobname}.{blobextension}",
```

U kunt Hallo bestandstype blobs beperken met behulp van een vaste waarde voor de bestandsextensie Hallo. Bijvoorbeeld: tootrigger alleen op PNG-bestanden, gebruik Hallo patroon volgen:

```json
"path": "samples/{name}.png",
```

Accolades zijn speciale tekens in de naam van patronen. toospecify blob-namen die accolades in de naam van de hello hebben, escape Hallo accolades u twee gebruiken. Hallo volgende voorbeeld wordt gezocht naar een blob met de naam *{20140101}-soundfile.mp3* in Hallo *installatiekopieën* container en Hallo `name` variabelewaarde in Hallo functiecode is  *soundfile.mp3*. 

```json
"path": "images/{{20140101}}-{name}",
```

### <a name="trigger-metadata"></a>Trigger metagegevens

Hallo blob trigger biedt verschillende eigenschappen voor metagegevens. Deze eigenschappen kunnen worden gebruikt als onderdeel van de expressies bindingen in andere bindingen of als parameters in uw code. Deze waarden Hallo hebben dezelfde betekenis als [CloudBlob](https://docs.microsoft.com/en-us/dotnet/api/microsoft.windowsazure.storage.blob.cloudblob?view=azure-dotnet).

- **BlobTrigger**. Typ `string`. Hallo activerende blobpad
- **URI**. Typ `System.Uri`. Hallo-blob-URI voor de primaire locatie Hallo.
- **Eigenschappen**. Typ `Microsoft.WindowsAzure.Storage.Blob.BlobProperties`. Hallo van blob-Systeemeigenschappen.
- **Metagegevens**. Typ `IDictionary<string,string>`. Hallo gebruiker gedefinieerde metagegevens voor Hallo blob.

<a name="receipts"></a>

### <a name="blob-receipts"></a>BLOB ontvangstbevestigingen
Hello Azure Functions-runtime zorgt ervoor dat er geen blob-activeringsfunctie meer dan één keer wordt aangeroepen voor dezelfde nieuwe of bijgewerkte blob Hallo. toodetermine als een versie van de opgegeven blob is verwerkt, houdt *blob ontvangstbevestigingen*.

Azure Functions winkels blob ontvangstbevestigingen in een container met de naam *webjobs-azure-hosts* in hello Azure storage-account voor de functie-app (gedefinieerd door de app-instelling Hallo `AzureWebJobsStorage`). De ontvangst van een blob heeft Hallo volgende informatie:

* Hallo functie geactiveerd ('*&lt;functie app-naam >*. Functies.  *&lt;functienaam >*', bijvoorbeeld: 'MyFunctionApp.Functions.CopyBlob')
* Hallo-containernaam
* Hallo blobtype ('BlockBlob' of 'PageBlob')
* Hallo blob-naam
* Hallo ETag (een blob-id, bijvoorbeeld: '0x8D1DC6E70A277EF')

Hallo blob ontvangst voor blob tooforce opnieuw verwerken van een blob verwijderen uit Hallo *webjobs-azure-hosts* container handmatig.

<a name="poison"></a>

### <a name="handling-poison-blobs"></a>Verwerken van verontreinigde blobs
Als een functie van de trigger blob is mislukt voor een bepaalde functies van Azure-blob pogingen die een totaal van 5 maal standaard functioneren. 

Als alle 5 pogingen mislukken, Azure Functions wordt toegevoegd een tooa opslag berichtenwachtrij met de naam *webjobs-blobtrigger-poison*. Hallo-bericht van wachtrij voor verontreinigde blobs is een JSON-object met Hallo volgende eigenschappen:

* FunctionId (Hallo indeling  *&lt;functie app-naam >*. Functies.  *&lt;functienaam >*)
* BlobType ('BlockBlob' of 'PageBlob')
* ContainerName
* BlobName
* ETag (een blob-id, bijvoorbeeld: '0x8D1DC6E70A277EF')

### <a name="blob-polling-for-large-containers"></a>Er wordt gedelegeerd voor grote containers BLOB
Als Hallo blob-container wordt bewaakt meer dan 10.000 blobs bevat, meld Hallo functies runtime scant bestanden toowatch voor nieuwe of gewijzigde blobs. Dit proces is niet realtime. Een functie mogelijk niet ophalen geactiveerd tot enkele minuten of langer nadat Hallo blob is gemaakt. Bovendien [opslag logboeken worden gemaakt op een 'best effort'](/rest/api/storageservices/About-Storage-Analytics-Logging) basis. Er is geen garantie dat alle gebeurtenissen worden vastgelegd. Onder bepaalde omstandigheden wellicht Logboeken niet opgehaald. Als u sneller of betrouwbaarder blob verwerking vereist, kunt u een [wachtrijbericht](../storage/queues/storage-dotnet-how-to-use-queues.md) bij het maken van Hallo blob. Vervolgens gebruikt u een [wachtrij trigger](functions-bindings-storage-queue.md) in plaats van een blob trigger tooprocess Hallo blob.

<a name="triggerusage"></a>

## <a name="using-a-blob-trigger-and-input-binding"></a>Met behulp van een blob-trigger en invoer binding
In .NET-functies, toegang tot blobgegevens Hallo met een parameter van de methode, zoals `Stream paramName`. Hier `paramName` is Hallo-waarde die u hebt opgegeven in Hallo [trigger configuratie](#trigger). In de Node.js-functies toegang Hallo invoer blob-gegevens met `context.bindings.<name>`.

In .NET, kunt u tooany typen Hallo Hallo onderstaande binden. Als gebruikt als een invoer-binding, is enkele van deze typen vereisen een `inout` richting in binding *function.json*. Deze richting wordt niet ondersteund door Hallo standaardeditor, zodat u Hallo geavanceerde editor moet gebruiken.

* `TextReader`
* `Stream`
* `ICloudBlob`('inout' binding richting vereist)
* `CloudBlockBlob`('inout' binding richting vereist)
* `CloudPageBlob`('inout' binding richting vereist)
* `CloudAppendBlob`('inout' binding richting vereist)

Als tekst blobs worden verwacht, kunt u ook .NET tooa binden `string` type. Dit wordt alleen aanbevolen als Hallo blob klein is, zoals Hallo gehele blob-inhoud in het geheugen geladen. In het algemeen is het beter toouse een `Stream` of `CloudBlockBlob` type.

## <a name="trigger-sample"></a>Voorbeeld van de trigger
Stel dat u hebt Hallo function.json die een blob storage-trigger definieert te volgen:

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "myBlob",
            "type": "blobTrigger",
            "direction": "in",
            "path": "samples-workitems",
            "connection":"MyStorageAccount"
        }
    ]
}
```

Zie Hallo taalspecifieke steekproef die het Hallo-inhoud van elke blob die wordt toegevoegd toohello bewaakte container registreert.

* [C#](#triggercsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="blob-trigger-examples-in-c"></a>Voorbeelden van BLOB-trigger in C# #

```cs
// Blob trigger sample using a Stream binding
public static void Run(Stream myBlob, TraceWriter log)
{
   log.Info($"C# Blob trigger function Processed blob\n Name:{name} \n Size: {myBlob.Length} Bytes");
}
```

```cs
// Blob trigger binding tooa CloudBlockBlob
#r "Microsoft.WindowsAzure.Storage"

using Microsoft.WindowsAzure.Storage.Blob;

public static void Run(CloudBlockBlob myBlob, string name, TraceWriter log)
{
    log.Info($"C# Blob trigger function Processed blob\n Name:{name}\nURI:{myBlob.StorageUri}");
}
```

<a name="triggernodejs"></a>

### <a name="trigger-example-in-nodejs"></a>Voorbeeld van de trigger in Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js Blob trigger function processed', context.bindings.myBlob);
    context.done();
};
```
<a name="outputusage"></a>
<a name="storage-blob-output-binding"></a>

## <a name="using-a-blob-output-binding"></a>Binding met een blob uitvoer

.NET-functies, moet u gebruiken een `out string` parameter in uw functiehandtekening of gebruik een van de typen Hallo in Hallo lijst te volgen. In Node.js-functies, opent u met behulp Hallo uitvoer blob `context.bindings.<name>`.

In de .NET-functies kunt u tooany Hallo typen volgende uitvoeren:

* `out string`
* `TextWriter`
* `Stream`
* `CloudBlobStream`
* `ICloudBlob`
* `CloudBlockBlob` 
* `CloudPageBlob` 

<a name="input-sample"></a>

## <a name="queue-trigger-with-blob-input-and-output-sample"></a>Wachtrij-trigger met blob-invoer en uitvoer voorbeeld
Stel dat u hebt na function.json hello, die definieert een [Queue Storage trigger](functions-bindings-storage-queue.md), een blob-opslag-invoer en uitvoer van een blob-opslag. Gebruik van de kennisgeving Hallo Hallo `queueTrigger` metagegevenseigenschap. in de blob Hallo invoer en uitvoer `path` eigenschappen:

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
      "name": "myInputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "MyStorageConnection",
      "direction": "in"
    },
    {
      "name": "myOutputBlob",
      "type": "blob",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "MyStorageConnection",
      "direction": "out"
    }
  ],
  "disabled": false
}
``` 

Zie Hallo taalspecifieke steekproef die het Hallo blob-invoerbron toohello uitvoer blob kopieert.

* [C#](#incsharp)
* [Node.js](#innodejs)

<a name="incsharp"></a>

### <a name="blob-binding-example-in-c"></a>Voorbeeld van BLOB-binding in C# #

```cs
// Copy blob from input toooutput, based on a queue trigger
public static void Run(string myQueueItem, Stream myInputBlob, out string myOutputBlob, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputBlob = myInputBlob;
}
```

<a name="innodejs"></a>

### <a name="blob-binding-example-in-nodejs"></a>Voorbeeld van BLOB-binding in Node.js

```javascript
// Copy blob from input toooutput, based on a queue trigger
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputBlob = context.bindings.myInputBlob;
    context.done();
};
```

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

