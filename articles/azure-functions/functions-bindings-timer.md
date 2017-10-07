---
title: timertrigger aaaAzure-functies | Microsoft Docs
description: Begrijpen hoe toouse timer activeert in Azure Functions.
services: functions
documentationcenter: na
author: christopheranderson
manager: erikre
editor: 
tags: 
keywords: Azure functions, functies, verwerking van gebeurtenissen, dynamische compute zonder server architectuur
ms.assetid: d2f013d1-f458-42ae-baf8-1810138118ac
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 02/27/2017
ms.author: glenga
ms.custom: 
ms.openlocfilehash: 17fca22372dbc55d4684c8c099cc97923a7d3cf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-functions-timer-trigger"></a>Azure Functions timertrigger

[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Dit artikel wordt uitgelegd hoe timer tooconfigure en code in Azure Functions activeert. Azure Functions heeft een timer trigger binding waarmee u de functiecode op basis van een ingesteld schema uitvoeren. 

Hallo timertrigger ondersteunt meerdere exemplaren scale-out. Slechts één exemplaar van een bepaalde timerfunctie wordt uitgevoerd in alle exemplaren.

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a id="trigger"></a>

## <a name="timer-trigger"></a>Timertrigger
Hallo timer trigger tooa functie maakt gebruik van volgende JSON-object in Hallo Hallo `bindings` matrix van function.json:

```json
{
    "schedule": "<CRON expression - see below>",
    "name": "<Name of trigger parameter in function signature>",
    "type": "timerTrigger",
    "direction": "in"
}
```

waarde van Hallo `schedule` is een [CRON expressie](http://en.wikipedia.org/wiki/Cron#CRON_expression) die deze zes velden bevat: 

    {second} {minute} {hour} {day} {month} {day-of-week}
&nbsp;
>[!NOTE]   
>Veel van Hallo cron expressies u online vindt Hallo weglaten `{second}` veld. Als u van één van beide kopieert, moet u tooadjust voor extra Hallo `{second}` veld. Zie voor specifieke voorbeelden [voorbeelden plannen](#examples) hieronder.

Hallo standaardtijdzone gebruikt met Hallo CRON expressies wordt Coordinated Universal Time (UTC). de CRON-expressie op basis van een andere tijdzone toohave maakt een nieuwe appinstelling voor de functie-app met de naam `WEBSITE_TIME_ZONE`. Set Hallo toohello waardenaam Hallo gewenst tijdzone zoals weergegeven in Hallo [Microsoft tijdzone Index](https://msdn.microsoft.com/library/ms912391.aspx). 

Bijvoorbeeld: *Eastern (standaardtijd)* UTC-05:00. toohave uw timer geactiveerd fire op 10:00 AM GMT dagelijks gebruik Hallo CRON-expressie die voor de UTC-tijdzone-accounts te volgen:

```json
"schedule": "0 0 15 * * *",
``` 

U kunt ook kunt u een nieuwe appinstelling toevoegen voor de functie-app met de naam `WEBSITE_TIME_ZONE` en stelt u Hallo waarde te**Eastern (standaardtijd)**.  Hallo na CRON-expressie kan vervolgens worden gebruikt voor 10:00 AM GMT: 

```json
"schedule": "0 0 10 * * *",
``` 


<a name="examples"></a>

## <a name="schedule-examples"></a>Voorbeelden van de planning
Hier volgen enkele voorbeelden van CRON-expressies die u voor Hallo gebruiken kunt `schedule` eigenschap. 

om de vijf minuten tootrigger:

```json
"schedule": "0 */5 * * * *"
```

tootrigger eenmaal op Hallo boven aan elk uur:

```json
"schedule": "0 0 * * * *",
```

elke twee uur tootrigger:

```json
"schedule": "0 0 */2 * * *",
```

tootrigger één keer per uur van too5 09: 00 PM:

```json
"schedule": "0 0 9-17 * * *",
```

tootrigger op elke dag 9:30 uur:

```json
"schedule": "0 30 9 * * *",
```

tootrigger om 9:30 AM elke weekdag:

```json
"schedule": "0 30 9 * * 1-5",
```

<a name="usage"></a>

## <a name="trigger-usage"></a>Gebruik van de trigger
Wanneer een functie van de trigger timer wordt opgeroepen, Hallo [timerobject](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) wordt doorgegeven in de Hallo-functie. Hallo is volgende JSON een voorbeeld-weergave van Hallo timer-object. 

```json
{
    "Schedule":{
    },
    "ScheduleStatus": {
        "Last":"2016-10-04T10:15:00.012699+00:00",
        "Next":"2016-10-04T10:20:00+00:00"
    },
    "IsPastDue":false
}
```

<a name="sample"></a>

## <a name="trigger-sample"></a>Voorbeeld van de trigger
Stel dat er na timertrigger in Hallo Hallo `bindings` matrix van function.json:

```json
{
    "schedule": "0 */5 * * * *",
    "name": "myTimer",
    "type": "timerTrigger",
    "direction": "in"
}
```

Zie Hallo taalspecifieke steekproef die het Hallo-timer object toosee leest of deze later wordt uitgevoerd.

* [C#](#triggercsharp)
* [F#](#triggerfsharp)
* [Node.js](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a>Voorbeeld van de trigger in C# #
```csharp
public static void Run(TimerInfo myTimer, TraceWriter log)
{
    if(myTimer.IsPastDue)
    {
        log.Info("Timer is running late!");
    }
    log.Info($"C# Timer trigger function executed at: {DateTime.Now}" );  
}
```

<a name="triggerfsharp"></a>

### <a name="trigger-sample-in-f"></a>Voorbeeld van de trigger in F # #
```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter ) =
    if (myTimer.IsPastDue) then
        log.Info("F# function is running late.")
    let now = DateTime.Now.ToLongTimeString()
    log.Info(sprintf "F# function executed at %s!" now)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a>Voorbeeld van de trigger in Node.js
```JavaScript
module.exports = function (context, myTimer) {
    var timeStamp = new Date().toISOString();

    if(myTimer.isPastDue)
    {
        context.log('Node.js is running late!');
    }
    context.log('Node.js timer trigger function ran!', timeStamp);   

    context.done();
};
```

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

