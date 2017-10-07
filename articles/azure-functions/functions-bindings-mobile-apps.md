---
title: Bindingen voor aaaAzure functies Mobile Apps | Microsoft Docs
description: Begrijpen hoe Azure Mobile Apps-bindingen toouse in Azure Functions.
services: functions
documentationcenter: na
author: ggailey777
manager: erikre
editor: 
tags: 
keywords: Azure functions, functies, verwerking van gebeurtenissen, dynamische compute zonder server architectuur
ms.assetid: faad1263-0fa5-41a9-964f-aecbc0be706a
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/31/2016
ms.author: glenga
ms.openlocfilehash: d3679a5d5c66705b32e422ec17e3a1e6d6ac063c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-mobile-apps-bindings"></a>Azure Functions Mobile Apps-bindingen
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Dit artikel wordt uitgelegd hoe tooconfigure en code [Azure Mobile Apps](../app-service-mobile/app-service-mobile-value-prop.md) bindingen in de Azure Functions. Azure Functions ondersteunt invoer en uitvoer van de bindingen voor mobiele Apps.

Hallo Mobile Apps-invoer en uitvoer bindingen kunnen u [lezen uit en schrijven toodata tabellen](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#TableOperations) in uw mobiele app.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a name="input"></a>

## <a name="mobile-apps-input-binding"></a>Invoer Mobile Apps-binding
Hallo invoer Mobile Apps-binding wordt een record geladen uit een eindpunt van de mobiele en geeft deze door aan uw functie. In een C# en F # functies, worden eventuele wijzigingen toohello record automatisch back toohello tabel verzonden wanneer het Hallo-functie is afgesloten.

Hallo Mobile Apps invoer tooa functie maakt gebruik van volgende JSON-object in Hallo Hallo `bindings` matrix van function.json:

```json
{
    "name": "<Name of input parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "id" : "<Id of hello record tooretrieve - see below>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "in"
}
```

Let op Hallo volgende:

* `id`kan niet statisch of het kan zijn gebaseerd op Hallo-trigger die Hallo-functie roept. Als u bijvoorbeeld een [wachtrij trigger]() voor de functie vervolgens `"id": "{queueTrigger}"` gebruikt Hallo string-waarde van de wachtrij het Hallo-bericht als Hallo record ID tooretrieve.
* `connection`Hallo-naam van een appinstelling in de functie-app die op zijn beurt Hallo-URL van uw mobiele app bevat moet worden bevatten. Hallo-functie maakt gebruik van deze URL tooconstruct Hallo vereist REST-bewerkingen op uw mobiele app. U [maken van een app-instelling in uw app functie]() die URL van uw mobiele app bevat (ziet eruit als `http://<appname>.azurewebsites.net`), vervolgens Hallo-naam van Hallo app-instelling opgeven in Hallo `connection` eigenschap in de binding van uw invoer. 
* U moet toospecify `apiKey` als u [implementeren van een API-sleutel in uw back-end voor Node.js mobiele app](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), of [implementeren van een API-sleutel in uw back-end .NET mobiele app](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key). toodo dit u [maken van een app-instelling in uw app functie]() dat Hallo API-sleutel bevat, voegt u Hallo `apiKey` eigenschap in uw invoer binding met de naam van de app-instelling Hallo Hallo. 
  
  > [!IMPORTANT]
  > Deze API-sleutel moet niet worden gedeeld met uw mobiele app-clients. Dit moet gedistribueerde veilig tooservice-side '-clients, zoals Azure Functions. 
  > 
  > [!NOTE]
  > Azure Functions slaat uw verbindingsgegevens en API-sleutels als de app-instellingen zodat ze niet zijn ingeschakeld in uw resourcebeheerbibliotheek. Dit beschermt uw vertrouwelijke gegevens.
  > 
  > 

<a name="inputusage"></a>

## <a name="input-usage"></a>Invoer-gebruik
Deze sectie leest u hoe toouse uw Mobile Apps invoer binding in uw functiecode. 

Hallo-record met Hallo opgegeven tabel en record-ID is gevonden, wordt doorgegeven in met de naam Hallo [JObject](http://www.newtonsoft.com/json/help/html/t_newtonsoft_json_linq_jobject.htm) parameter (of in Node.js, is deze Hallo doorgegeven `context.bindings.<name>` object). Wanneer Hallo-record niet gevonden is, is het Hallo-parameter `null`. 

In C# en F # functies, wijzigingen die u aanbrengt toohello invoer-record (invoerparameter) automatisch verzonden back toohello Mobile Apps-tabel wanneer Hallo-functie met succes wordt afgesloten. Gebruik in Node.js-functies, `context.bindings.<name>` tooaccess Hallo invoerrecord. U kunt een record in Node.js niet wijzigen.

<a name="inputsample"></a>

## <a name="input-sample"></a>Voorbeeld van invoer
Stel dat u hebt na function.json hello, haalt die een record in de tabel mobiele App met Hallo Hallo-bericht van wachtrij trigger-id:

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
        "name": "record",
        "type": "mobileTable",
        "tableName": "MyTable",
        "id" : "{queueTrigger}",
        "connection": "My_MobileApp_Url",
        "apiKey": "My_MobileApp_Key",
        "direction": "in"
    }
],
"disabled": false
}
```

Zie Hallo taalspecifieke voorbeeld dat gebruikmaakt van de invoerrecord Hallo Hallo binding. Voorbeelden van C# en F # Hallo Hallo-record ook wijzigen `text` eigenschap.

* [C#](#inputcsharp)
* [Node.js](#inputnodejs)

<a name="inputcsharp"></a>

### <a name="input-sample-in-c"></a>Invoer voorbeeld in C# #

```cs
#r "Newtonsoft.Json"    
using Newtonsoft.Json.Linq;

public static void Run(string myQueueItem, JObject record)
{
    if (record != null)
    {
        record["Text"] = "This has changed.";
    }    
}
```

<!--
<a name="inputfsharp"></a>
### Input sample in F# ## 

```fsharp
#r "Newtonsoft.Json"    
open Newtonsoft.Json.Linq
let Run(myQueueItem: string, record: JObject) =
  inputDocument?text <- "This has changed."
```
-->

<a name="inputnodejs"></a>

### <a name="input-sample-in-nodejs"></a>Invoer voorbeeld in Node.js

```javascript
module.exports = function (context, myQueueItem) {    
    context.log(context.bindings.record);
    context.done();
};
```

<a name="output"></a>

## <a name="mobile-apps-output-binding"></a>Mobile Apps uitvoer binding
Hallo Mobile Apps uitvoer binding toowrite een nieuw record tooa Mobile Apps tabel eindpunt gebruiken.  

Hallo Mobile Apps uitvoer voor een functie maakt gebruik van volgende JSON-object in Hallo Hallo `bindings` matrix van function.json:

```json
{
    "name": "<Name of output parameter in function signature>",
    "type": "mobileTable",
    "tableName": "<Name of your mobile app's data table>",
    "connection": "<Name of app setting that has your mobile app's URL - see below>",
    "apiKey": "<Name of app setting that has your mobile app's API key - see below>",
    "direction": "out"
}
```

Let op Hallo volgende:

* `connection`Hallo-naam van een appinstelling in de functie-app die op zijn beurt Hallo-URL van uw mobiele app bevat moet worden bevatten. Hallo-functie maakt gebruik van deze URL tooconstruct Hallo vereist REST-bewerkingen op uw mobiele app. U [maken van een app-instelling in uw app functie]() die URL van uw mobiele app bevat (ziet eruit als `http://<appname>.azurewebsites.net`), vervolgens Hallo-naam van Hallo app-instelling opgeven in Hallo `connection` eigenschap in de binding van uw invoer. 
* U moet toospecify `apiKey` als u [implementeren van een API-sleutel in uw back-end voor Node.js mobiele app](https://github.com/Azure/azure-mobile-apps-node/tree/master/samples/api-key), of [implementeren van een API-sleutel in uw back-end .NET mobiele app](https://github.com/Azure/azure-mobile-apps-net-server/wiki/Implementing-Application-Key). toodo dit u [maken van een app-instelling in uw app functie]() dat Hallo API-sleutel bevat, voegt u Hallo `apiKey` eigenschap in uw invoer binding met de naam van de app-instelling Hallo Hallo. 
  
  > [!IMPORTANT]
  > Deze API-sleutel moet niet worden gedeeld met uw mobiele app-clients. Dit moet gedistribueerde veilig tooservice-side '-clients, zoals Azure Functions. 
  > 
  > [!NOTE]
  > Azure Functions slaat uw verbindingsgegevens en API-sleutels als de app-instellingen zodat ze niet zijn ingeschakeld in uw resourcebeheerbibliotheek. Dit beschermt uw vertrouwelijke gegevens.
  > 
  > 

<a name="outputusage"></a>

## <a name="output-usage"></a>Gebruik voor uitvoer
Deze sectie leest u hoe toouse uw mobiele Apps uitvoeren in uw functiecode binding. 

Gebruik in C# functies, een benoemde output-parameter van het type `out object` tooaccess Hallo uitvoer record. Gebruik in Node.js-functies, `context.bindings.<name>` tooaccess Hallo uitvoer record.

<a name="outputsample"></a>

## <a name="output-sample"></a>Voorbeeld van uitvoer
Stel dat u hebt Hallo function.json die de trigger van een wachtrij en de uitvoer van een mobiele Apps definieert te volgen:

```json
{
"bindings": [
    {
    "name": "myQueueItem",
    "queueName": "myqueue-items",
    "connection":"",
    "type": "queueTrigger",
    "direction": "in"
    },
    {
    "name": "record",
    "type": "mobileTable",
    "tableName": "MyTable",
    "connection": "My_MobileApp_Url",
    "apiKey": "My_MobileApp_Key",
    "direction": "out"
    }
],
"disabled": false
}
```

Zie Hallo taalspecifieke voorbeeldtoepassing die u een record in Hallo Mobile Apps-eindpunt voor table met Hallo inhoud van de wachtrij het Hallo-bericht maakt.

* [C#](#outcsharp)
* [Node.js](#outnodejs)

<a name="outcsharp"></a>

### <a name="output-sample-in-c"></a>Voorbeeld van uitvoer in C# #

```cs
public static void Run(string myQueueItem, out object record)
{
    record = new {
        Text = $"I'm running in a C# function! {myQueueItem}"
    };
}
```

<!--
<a name="outfsharp"></a>
### Output sample in F# ## 
```fsharp

```
-->
<a name="outnodejs"></a>

### <a name="output-sample-in-nodejs"></a>Voorbeeld van uitvoer in Node.js

```javascript
module.exports = function (context, myQueueItem) {

    context.bindings.record = {
        text : "I'm running in a Node function! Data: '" + myQueueItem + "'"
    }   

    context.done();
};
```

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

