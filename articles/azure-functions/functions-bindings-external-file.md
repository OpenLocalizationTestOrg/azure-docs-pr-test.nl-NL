---
title: aaaAzure-bestand met externe functies Bindingen (Preview) | Microsoft Docs
description: Met behulp van extern bestand bindingen in de Azure-functies
services: functions
documentationcenter: 
author: alexkarcher-msft
manager: erikre
editor: 
ms.assetid: 
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 04/12/2017
ms.author: alkarche
ms.openlocfilehash: 583d9c0b871dc68a79614749ba6ac6711fa820fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-external-file-bindings-preview"></a>Azure Functions-bestand met externe Bindingen (Preview)
Dit artikel laat zien hoe toomanipulate bestanden van verschillende SaaS providers (zoals OneDrive, Dropbox) in de functie met behulp van de ingebouwde bindingen. Azure functions ondersteunt activeren, invoer en uitvoer van de bindingen voor extern bestand.

Deze binding API verbindingen tooSaaS providers maakt of bestaande API-verbindingen van de resourcegroep van de functie-App wordt gebruikt.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

## <a name="supported-file-connections"></a>Ondersteunde bestand-verbindingen

|Connector|Trigger|Invoer|Uitvoer|
|:-----|:---:|:---:|:---:|
|[Vak](https://www.box.com)|x|x|x
|[Dropbox](https://www.dropbox.com)|x|x|x
|[FTP](https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp)|x|x|x
|[OneDrive](https://onedrive.live.com)|x|x|x
|[OneDrive voor Bedrijven](https://onedrive.live.com/about/business/)|x|x|x
|[SFTP](https://docs.microsoft.com/azure/connectors/connectors-create-api-sftp)|x|x|x
|[Google Drive](https://www.google.com/drive/)||x|x|

> [!NOTE]
> Externe verbindingen van het bestand kunnen ook worden gebruikt [Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list)

## <a name="external-file-trigger-binding"></a>Bestand met externe binding activeren

Hello Azure extern bestand trigger kunt u een externe map bewaken en de functiecode uitvoeren als er wijzigingen worden gedetecteerd.

Hallo-bestand met externe trigger gebruikt Hallo volgende JSON-objecten in Hallo `bindings` matrix van function.json

```json
{
  "type": "apiHubFileTrigger",
  "name": "<Name of input parameter in function signature>",
  "direction": "in",
  "path": "<folder toomonitor, and optionally a name pattern - see below>",
  "connection": "<name of external file connection - see above>"
}
```
<!---
See one of hello following subheadings for more information:

* [Name patterns](#pattern)
* [File receipts](#receipts)
* [Handling poison files](#poison)
--->

<a name="pattern"></a>

### <a name="name-patterns"></a>Bestandsnaampatronen
U kunt een bestandsnaampatroon opgeven in Hallo `path` eigenschap. Hallo-map waarnaar wordt verwezen, moet bestaan in Hallo SaaS-provider.
Voorbeelden:

```json
"path": "input/original-{name}",
```

Dit pad wilt zoeken naar een bestand met de naam *oorspronkelijke Bestand1.txt* in Hallo *invoer* map en de waarde Hallo Hallo `name` variabele in functiecode zou worden `File1.txt`.

Nog een voorbeeld:

```json
"path": "input/{filename}.{fileextension}",
```

Dit pad zou ook een bestand met de naam vinden *oorspronkelijke Bestand1.txt*, en de waarde van Hallo Hallo `filename` en `fileextension` variabelen in de functiecode zou worden *oorspronkelijke File1* en  *txt*.

U kunt bestandstype Hallo van bestanden met behulp van een vaste waarde voor de bestandsextensie Hallo beperken. Bijvoorbeeld:

```json
"path": "samples/{name}.png",
```

In dit geval wordt alleen *PNG* bestanden in Hallo *voorbeelden* map Hallo activeringsfunctie.

Accolades zijn speciale tekens in de naam van patronen. bestandsnamen toospecify die accolades in Hallo-naam, dubbele Hallo accolades hebben.
Bijvoorbeeld:

```json
"path": "images/{{20140101}}-{name}",
```

Dit pad wilt zoeken naar een bestand met de naam *{20140101}-soundfile.mp3* in Hallo *installatiekopieën* map en Hallo `name` variabele waarde in de functiecode Hallo *soundfile.mp3*.

<a name="receipts"></a>

<!--- ### File receipts
hello Azure Functions runtime makes sure that no external file trigger function gets called more than once for hello same new or updated file.
It does so by maintaining *file receipts* toodetermine if a given file version has been processed.

File receipts are stored in a folder named *azure-webjobs-hosts* in hello Azure storage account for your function app
(specified by hello `AzureWebJobsStorage` app setting). A file receipt has hello following information:

* hello triggered function ("*&lt;function app name>*.Functions.*&lt;function name>*", for example: "functionsf74b96f7.Functions.CopyFile")
* hello folder name
* hello file type ("BlockFile" or "PageFile")
* hello file name
* hello ETag (a file version identifier, for example: "0x8D1DC6E70A277EF")

tooforce reprocessing of a file, delete hello file receipt for that file from hello *azure-webjobs-hosts* folder manually.
--->
<a name="poison"></a>

### <a name="handling-poison-files"></a>Verwerken van verontreinigde bestanden
Als er een extern bestand activeringsfunctie uitvalt, probeert Azure Functions die functie van too5 tijden opnieuw standaard (inclusief de eerste poging Hallo) voor een bepaald bestand.
Als alle 5 pogingen mislukken, functies wordt toegevoegd een tooa opslag berichtenwachtrij met de naam *webjobs-apihubtrigger-poison*. Hallo-bericht van wachtrij voor verontreinigde bestanden is een JSON-object met Hallo volgende eigenschappen:

* FunctionId (Hallo indeling  *&lt;functie app-naam >*. Functies.  *&lt;functienaam >*)
* Bestandstype
* Mapnaam
* Bestandsnaam
* ETag (een bestand versie-id, bijvoorbeeld: '0x8D1DC6E70A277EF')


<a name="triggerusage"></a>

## <a name="trigger-usage"></a>Gebruik van de trigger
In de C# functies, bindt u toohello invoerbestand gegevens met behulp van een benoemde parameter in de functiehandtekening, zoals `<T> <name>`.
Waar `T` is Hallo gegevenstype dat u wilt dat toodeserialize Hallo gegevens in, en `paramName` Hallo-naam die u hebt opgegeven in de [activeert JSON](#trigger). In een Node.js-functies, opent u Hallo invoerbestand gegevens met `context.bindings.<name>`.

Hallo-bestand kan worden gedeserialiseerd in een van de volgende typen Hallo:

* Alle [Object](https://msdn.microsoft.com/library/system.object.aspx) - nuttig voor JSON-geserialiseerd bestandsgegevens.
  Als u een aangepaste invoertype declareren (bijvoorbeeld `FooType`), Azure Functions probeert toodeserialize Hallo JSON-gegevens in het opgegeven type.
* Tekenreeks - nuttig voor tekst-bestandsgegevens.

In C#-functies, kunt u ook tooany van de volgende typen Hallo binden en Hallo functies runtime probeert te deserialiseren Hallo bestandsgegevens met behulp van dat type:

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`

## <a name="trigger-sample"></a>Voorbeeld van de trigger
Stel dat u hebt na function.json hello, definieert die de trigger van een extern bestand:

```json
{
    "disabled": false,
    "bindings": [
        {
            "name": "myFile",
            "type": "apiHubFileTrigger",
            "direction": "in",
            "path": "samples-workitems",
            "connection": "<name of external file connection>"
        }
    ]
}
```

Zie Hallo taalspecifieke steekproef die het Hallo-inhoud van elk bestand dat wordt toegevoegd toohello bewaakte map registreert.

* [C#](#triggercsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-usage-in-c"></a>Gebruik van de trigger in C# #

```cs
public static void Run(string myFile, TraceWriter log)
{
    log.Info($"C# File trigger function processed: {myFile}");
}
```

<!--
<a name="triggerfsharp"></a>
### Trigger usage in F# ##
```fsharp

```
-->

<a name="triggernodejs"></a>

### <a name="trigger-usage-in-nodejs"></a>Gebruik van de trigger in Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js File trigger function processed', context.bindings.myFile);
    context.done();
};
```

<a name="input"></a>

## <a name="external-file-input-binding"></a>Bestand met externe invoer binding
Hello Azure extern bestand invoer binding kunt u een bestand vanaf een externe map in de functie toouse.

Hallo-bestand met externe invoer tooa functie maakt gebruik van volgende JSON-objecten in Hallo Hallo `bindings` matrix van function.json:

```json
{
  "name": "<Name of input parameter in function signature>",
  "type": "apiHubFile",
  "direction": "in",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
},
```

Let op Hallo volgende:

* `path`moet de naam van de map Hallo en Hallo-bestandsnaam bevatten. Als u hebt bijvoorbeeld een [wachtrij trigger](functions-bindings-storage-queue.md) in de functie, kunt u `"path": "samples-workitems/{queueTrigger}"` toopoint tooa bestand in Hallo `samples-workitems` map met een naam die overeenkomt met Hallo-bestandsnaam is opgegeven in de trigger het Hallo-bericht.   

<a name="inputusage"></a>

## <a name="input-usage"></a>Invoer-gebruik
In de C# functies, bindt u toohello invoerbestand gegevens met behulp van een benoemde parameter in de functiehandtekening, zoals `<T> <name>`.
Waar `T` is Hallo gegevenstype dat u wilt dat toodeserialize Hallo gegevens in, en `paramName` Hallo-naam die u hebt opgegeven in de [invoer binding](#input). In een Node.js-functies, opent u Hallo invoerbestand gegevens met `context.bindings.<name>`.

Hallo-bestand kan worden gedeserialiseerd in een van de volgende typen Hallo:

* Alle [Object](https://msdn.microsoft.com/library/system.object.aspx) - nuttig voor JSON-geserialiseerd bestandsgegevens.
  Als u een aangepaste invoertype declareren (bijvoorbeeld `InputType`), Azure Functions probeert toodeserialize Hallo JSON-gegevens in het opgegeven type.
* Tekenreeks - nuttig voor tekst-bestandsgegevens.

In C#-functies, kunt u ook tooany van de volgende typen Hallo binden en Hallo functies runtime probeert te deserialiseren Hallo bestandsgegevens met behulp van dat type:

* `string`
* `byte[]`
* `Stream`
* `StreamReader`
* `TextReader`


<a name="output"></a>

## <a name="external-file-output-binding"></a>Bestand met externe uitvoer binding
Hello Azure-bestand met externe uitvoer binding kunt u toowrite bestanden tooan externe map in de functie.

Hallo-bestand met externe uitvoer voor een functie maakt gebruik van volgende JSON-objecten in Hallo Hallo `bindings` matrix van function.json:

```json
{
  "name": "<Name of output parameter in function signature>",
  "type": "apiHubFile",
  "direction": "out",
  "path": "<Path of input file - see below>",
  "connection": "<name of external file connection>"
}
```

Let op Hallo volgende:

* `path`moet Hallo mapnaam en Hallo bestand naam toowrite te bevatten. Als u hebt bijvoorbeeld een [wachtrij trigger](functions-bindings-storage-queue.md) in de functie, kunt u `"path": "samples-workitems/{queueTrigger}"` toopoint tooa bestand in Hallo `samples-workitems` map met een naam die overeenkomt met Hallo-bestandsnaam is opgegeven in de trigger het Hallo-bericht.   

<a name="outputusage"></a>

## <a name="output-usage"></a>Gebruik voor uitvoer
In de C# functies, bindt u toohello uitvoerbestand door gebruik te maken met de naam Hallo `out` parameter in de functiehandtekening, zoals `out <T> <name>`, waarbij `T` is Hallo gegevenstype dat u wilt dat tooserialize Hallo gegevens in, en `paramName` is Hallo servernaam die u hebt opgegeven in de [uitvoer binding](#output). In een Node.js-functies, opent u Hallo uitvoer-bestand met `context.bindings.<name>`.

U kunt schrijven toohello uitvoerbestand met behulp van een Hallo volgende typen:

* Alle [Object](https://msdn.microsoft.com/library/system.object.aspx) - nuttig voor JSON-serialisatie.
  Als u een aangepaste uitvoertype declareren (bijvoorbeeld `out OutputType paramName`), Azure Functions probeert tooserialize object naar JSON. Als bij het verlaten van de functie Hallo Hallo output-parameter null is, maakt Hallo Functions-runtime-bestand als een null-object.
* String - (`out string paramName`) nuttig voor tekst-bestandsgegevens. Hallo functies runtime maakt een bestand alleen als de tekenreeksparameter niet-null is bij het Hallo-functie wordt afgesloten.

U kunt ook tooany van de volgende typen Hallo in C#-functies uitvoeren:

* `TextWriter`
* `Stream`
* `CloudFileStream`
* `ICloudFile`
* `CloudBlockFile`
* `CloudPageFile`

<a name="outputsample"></a>

<a name="sample"></a>

## <a name="input--output-sample"></a>Invoer en uitvoer-voorbeeld
Stel dat u hebt na function.json hello, die definieert een [opslag wachtrij trigger](functions-bindings-storage-queue.md), voert u een extern bestand en een bestand met externe uitvoer:

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
      "name": "myInputFile",
      "type": "apiHubFile",
      "path": "samples-workitems/{queueTrigger}",
      "connection": "<name of external file connection>",
      "direction": "in"
    },
    {
      "name": "myOutputFile",
      "type": "apiHubFile",
      "path": "samples-workitems/{queueTrigger}-Copy",
      "connection": "<name of external file connection>",
      "direction": "out"
    }
  ],
  "disabled": false
}
```

Zie Hallo taalspecifieke steekproef die het Hallo invoerbestand toohello uitvoerbestand kopieert.

* [C#](#incsharp)
* [Node.js](#innodejs)

<a name="incsharp"></a>

### <a name="usage-in-c"></a>Gebruik in C# #

```cs
public static void Run(string myQueueItem, string myInputFile, out string myOutputFile, TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");
    myOutputFile = myInputFile;
}
```

<!--
<a name="infsharp"></a>
### Input usage in F# ##
```fsharp

```
-->

<a name="innodejs"></a>

### <a name="usage-in-nodejs"></a>Gebruik in Node.js

```javascript
module.exports = function(context) {
    context.log('Node.js Queue trigger function processed', context.bindings.myQueueItem);
    context.bindings.myOutputFile = context.bindings.myInputFile;
    context.done();
};
```

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]
