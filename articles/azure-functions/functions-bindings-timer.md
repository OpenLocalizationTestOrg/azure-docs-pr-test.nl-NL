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
# <a name="azure-functions-timer-trigger"></a><span data-ttu-id="de8cf-104">Azure Functions timertrigger</span><span class="sxs-lookup"><span data-stu-id="de8cf-104">Azure Functions timer trigger</span></span>

[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="de8cf-105">Dit artikel wordt uitgelegd hoe timer tooconfigure en code in Azure Functions activeert.</span><span class="sxs-lookup"><span data-stu-id="de8cf-105">This article explains how tooconfigure and code timer triggers in Azure Functions.</span></span> <span data-ttu-id="de8cf-106">Azure Functions heeft een timer trigger binding waarmee u de functiecode op basis van een ingesteld schema uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="de8cf-106">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span></span> 

<span data-ttu-id="de8cf-107">Hallo timertrigger ondersteunt meerdere exemplaren scale-out. Slechts één exemplaar van een bepaalde timerfunctie wordt uitgevoerd in alle exemplaren.</span><span class="sxs-lookup"><span data-stu-id="de8cf-107">hello timer trigger supports multi-instance scale-out. A single instance of a particular timer function is run across all instances.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a id="trigger"></a>

## <a name="timer-trigger"></a><span data-ttu-id="de8cf-108">Timertrigger</span><span class="sxs-lookup"><span data-stu-id="de8cf-108">Timer trigger</span></span>
<span data-ttu-id="de8cf-109">Hallo timer trigger tooa functie maakt gebruik van volgende JSON-object in Hallo Hallo `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="de8cf-109">hello timer trigger tooa function uses hello following JSON object in hello `bindings` array of function.json:</span></span>

```json
{
    "schedule": "<CRON expression - see below>",
    "name": "<Name of trigger parameter in function signature>",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="de8cf-110">waarde van Hallo `schedule` is een [CRON expressie](http://en.wikipedia.org/wiki/Cron#CRON_expression) die deze zes velden bevat:</span><span class="sxs-lookup"><span data-stu-id="de8cf-110">hello value of `schedule` is a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that includes these six fields:</span></span> 

    {second} {minute} {hour} {day} {month} {day-of-week}
&nbsp;
>[!NOTE]   
><span data-ttu-id="de8cf-111">Veel van Hallo cron expressies u online vindt Hallo weglaten `{second}` veld.</span><span class="sxs-lookup"><span data-stu-id="de8cf-111">Many of hello cron expressions you find online omit hello `{second}` field.</span></span> <span data-ttu-id="de8cf-112">Als u van één van beide kopieert, moet u tooadjust voor extra Hallo `{second}` veld.</span><span class="sxs-lookup"><span data-stu-id="de8cf-112">If you copy from one of them, you need tooadjust for hello extra `{second}` field.</span></span> <span data-ttu-id="de8cf-113">Zie voor specifieke voorbeelden [voorbeelden plannen](#examples) hieronder.</span><span class="sxs-lookup"><span data-stu-id="de8cf-113">For specific examples, see [Schedule examples](#examples) below.</span></span>

<span data-ttu-id="de8cf-114">Hallo standaardtijdzone gebruikt met Hallo CRON expressies wordt Coordinated Universal Time (UTC).</span><span class="sxs-lookup"><span data-stu-id="de8cf-114">hello default time zone used with hello CRON expressions is Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="de8cf-115">de CRON-expressie op basis van een andere tijdzone toohave maakt een nieuwe appinstelling voor de functie-app met de naam `WEBSITE_TIME_ZONE`.</span><span class="sxs-lookup"><span data-stu-id="de8cf-115">toohave your CRON expression based on another time zone, create a new app setting for your function app named `WEBSITE_TIME_ZONE`.</span></span> <span data-ttu-id="de8cf-116">Set Hallo toohello waardenaam Hallo gewenst tijdzone zoals weergegeven in Hallo [Microsoft tijdzone Index](https://msdn.microsoft.com/library/ms912391.aspx).</span><span class="sxs-lookup"><span data-stu-id="de8cf-116">Set hello value toohello name of hello desired time zone as shown in hello [Microsoft Time Zone Index](https://msdn.microsoft.com/library/ms912391.aspx).</span></span> 

<span data-ttu-id="de8cf-117">Bijvoorbeeld: *Eastern (standaardtijd)* UTC-05:00.</span><span class="sxs-lookup"><span data-stu-id="de8cf-117">For example, *Eastern Standard Time* is UTC-05:00.</span></span> <span data-ttu-id="de8cf-118">toohave uw timer geactiveerd fire op 10:00 AM GMT dagelijks gebruik Hallo CRON-expressie die voor de UTC-tijdzone-accounts te volgen:</span><span class="sxs-lookup"><span data-stu-id="de8cf-118">toohave your timer trigger fire at 10:00 AM EST every day, use hello following CRON expression that accounts for UTC time zone:</span></span>

```json
"schedule": "0 0 15 * * *",
``` 

<span data-ttu-id="de8cf-119">U kunt ook kunt u een nieuwe appinstelling toevoegen voor de functie-app met de naam `WEBSITE_TIME_ZONE` en stelt u Hallo waarde te**Eastern (standaardtijd)**.</span><span class="sxs-lookup"><span data-stu-id="de8cf-119">Alternatively, you could add a new app setting for your function app named `WEBSITE_TIME_ZONE` and set hello value too**Eastern Standard Time**.</span></span>  <span data-ttu-id="de8cf-120">Hallo na CRON-expressie kan vervolgens worden gebruikt voor 10:00 AM GMT:</span><span class="sxs-lookup"><span data-stu-id="de8cf-120">Then hello following CRON expression could be used for 10:00 AM EST:</span></span> 

```json
"schedule": "0 0 10 * * *",
``` 


<a name="examples"></a>

## <a name="schedule-examples"></a><span data-ttu-id="de8cf-121">Voorbeelden van de planning</span><span class="sxs-lookup"><span data-stu-id="de8cf-121">Schedule examples</span></span>
<span data-ttu-id="de8cf-122">Hier volgen enkele voorbeelden van CRON-expressies die u voor Hallo gebruiken kunt `schedule` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="de8cf-122">Here are some samples of CRON expressions you can use for hello `schedule` property.</span></span> 

<span data-ttu-id="de8cf-123">om de vijf minuten tootrigger:</span><span class="sxs-lookup"><span data-stu-id="de8cf-123">tootrigger once every five minutes:</span></span>

```json
"schedule": "0 */5 * * * *"
```

<span data-ttu-id="de8cf-124">tootrigger eenmaal op Hallo boven aan elk uur:</span><span class="sxs-lookup"><span data-stu-id="de8cf-124">tootrigger once at hello top of every hour:</span></span>

```json
"schedule": "0 0 * * * *",
```

<span data-ttu-id="de8cf-125">elke twee uur tootrigger:</span><span class="sxs-lookup"><span data-stu-id="de8cf-125">tootrigger once every two hours:</span></span>

```json
"schedule": "0 0 */2 * * *",
```

<span data-ttu-id="de8cf-126">tootrigger één keer per uur van too5 09: 00 PM:</span><span class="sxs-lookup"><span data-stu-id="de8cf-126">tootrigger once every hour from 9 AM too5 PM:</span></span>

```json
"schedule": "0 0 9-17 * * *",
```

<span data-ttu-id="de8cf-127">tootrigger op elke dag 9:30 uur:</span><span class="sxs-lookup"><span data-stu-id="de8cf-127">tootrigger At 9:30 AM every day:</span></span>

```json
"schedule": "0 30 9 * * *",
```

<span data-ttu-id="de8cf-128">tootrigger om 9:30 AM elke weekdag:</span><span class="sxs-lookup"><span data-stu-id="de8cf-128">tootrigger At 9:30 AM every weekday:</span></span>

```json
"schedule": "0 30 9 * * 1-5",
```

<a name="usage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="de8cf-129">Gebruik van de trigger</span><span class="sxs-lookup"><span data-stu-id="de8cf-129">Trigger usage</span></span>
<span data-ttu-id="de8cf-130">Wanneer een functie van de trigger timer wordt opgeroepen, Hallo [timerobject](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) wordt doorgegeven in de Hallo-functie.</span><span class="sxs-lookup"><span data-stu-id="de8cf-130">When a timer trigger function is invoked, hello [timer object](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) is passed into hello function.</span></span> <span data-ttu-id="de8cf-131">Hallo is volgende JSON een voorbeeld-weergave van Hallo timer-object.</span><span class="sxs-lookup"><span data-stu-id="de8cf-131">hello following JSON is an example representation of hello timer object.</span></span> 

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

## <a name="trigger-sample"></a><span data-ttu-id="de8cf-132">Voorbeeld van de trigger</span><span class="sxs-lookup"><span data-stu-id="de8cf-132">Trigger sample</span></span>
<span data-ttu-id="de8cf-133">Stel dat er na timertrigger in Hallo Hallo `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="de8cf-133">Suppose you have hello following timer trigger in hello `bindings` array of function.json:</span></span>

```json
{
    "schedule": "0 */5 * * * *",
    "name": "myTimer",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="de8cf-134">Zie Hallo taalspecifieke steekproef die het Hallo-timer object toosee leest of deze later wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="de8cf-134">See hello language-specific sample that reads hello timer object toosee whether it's running late.</span></span>

* [<span data-ttu-id="de8cf-135">C#</span><span class="sxs-lookup"><span data-stu-id="de8cf-135">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="de8cf-136">F#</span><span class="sxs-lookup"><span data-stu-id="de8cf-136">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="de8cf-137">Node.js</span><span class="sxs-lookup"><span data-stu-id="de8cf-137">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="de8cf-138">Voorbeeld van de trigger in C#</span><span class="sxs-lookup"><span data-stu-id="de8cf-138">Trigger sample in C#</span></span> #
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

### <a name="trigger-sample-in-f"></a><span data-ttu-id="de8cf-139">Voorbeeld van de trigger in F #</span><span class="sxs-lookup"><span data-stu-id="de8cf-139">Trigger sample in F#</span></span> #
```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter ) =
    if (myTimer.IsPastDue) then
        log.Info("F# function is running late.")
    let now = DateTime.Now.ToLongTimeString()
    log.Info(sprintf "F# function executed at %s!" now)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="de8cf-140">Voorbeeld van de trigger in Node.js</span><span class="sxs-lookup"><span data-stu-id="de8cf-140">Trigger sample in Node.js</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="de8cf-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="de8cf-141">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

