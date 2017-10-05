---
title: Azure Functions timertrigger | Microsoft Docs
description: Begrijpen hoe timer triggers in Azure Functions.
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
ms.openlocfilehash: 6a97ab8508f889b77d064a5da70e3c726d62900c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-functions-timer-trigger"></a><span data-ttu-id="3cc58-104">Azure Functions timertrigger</span><span class="sxs-lookup"><span data-stu-id="3cc58-104">Azure Functions timer trigger</span></span>

[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="3cc58-105">Dit artikel wordt uitgelegd hoe u configureert en code timer triggers in Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="3cc58-105">This article explains how to configure and code timer triggers in Azure Functions.</span></span> <span data-ttu-id="3cc58-106">Azure Functions heeft een timer trigger binding waarmee u de functiecode op basis van een ingesteld schema uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3cc58-106">Azure Functions has a timer trigger binding that lets you run your function code based on a defined schedule.</span></span> 

<span data-ttu-id="3cc58-107">De timertrigger ondersteunt meerdere exemplaren scale-out. Slechts één exemplaar van een bepaalde timerfunctie wordt uitgevoerd in alle exemplaren.</span><span class="sxs-lookup"><span data-stu-id="3cc58-107">The timer trigger supports multi-instance scale-out. A single instance of a particular timer function is run across all instances.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<a id="trigger"></a>

## <a name="timer-trigger"></a><span data-ttu-id="3cc58-108">Timertrigger</span><span class="sxs-lookup"><span data-stu-id="3cc58-108">Timer trigger</span></span>
<span data-ttu-id="3cc58-109">De timertrigger aan een functie maakt gebruik van de volgende JSON-object in de `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="3cc58-109">The timer trigger to a function uses the following JSON object in the `bindings` array of function.json:</span></span>

```json
{
    "schedule": "<CRON expression - see below>",
    "name": "<Name of trigger parameter in function signature>",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="3cc58-110">De waarde van `schedule` is een [CRON expressie](http://en.wikipedia.org/wiki/Cron#CRON_expression) die deze zes velden bevat:</span><span class="sxs-lookup"><span data-stu-id="3cc58-110">The value of `schedule` is a [CRON expression](http://en.wikipedia.org/wiki/Cron#CRON_expression) that includes these six fields:</span></span> 

    {second} {minute} {hour} {day} {month} {day-of-week}
&nbsp;
>[!NOTE]   
><span data-ttu-id="3cc58-111">Veel van de cron-expressies die u online vinden weglaten de `{second}` veld.</span><span class="sxs-lookup"><span data-stu-id="3cc58-111">Many of the cron expressions you find online omit the `{second}` field.</span></span> <span data-ttu-id="3cc58-112">Als u van één van beide kopieert, moet u voor de extra aanpassen `{second}` veld.</span><span class="sxs-lookup"><span data-stu-id="3cc58-112">If you copy from one of them, you need to adjust for the extra `{second}` field.</span></span> <span data-ttu-id="3cc58-113">Zie voor specifieke voorbeelden [voorbeelden plannen](#examples) hieronder.</span><span class="sxs-lookup"><span data-stu-id="3cc58-113">For specific examples, see [Schedule examples](#examples) below.</span></span>

<span data-ttu-id="3cc58-114">De standaardtijdzone gebruikt met de CRON-expressies is Coordinated Universal Time (UTC).</span><span class="sxs-lookup"><span data-stu-id="3cc58-114">The default time zone used with the CRON expressions is Coordinated Universal Time (UTC).</span></span> <span data-ttu-id="3cc58-115">Als u wilt dat de CRON-expressie op basis van een andere tijdzone, maakt u een nieuwe appinstelling voor de functie-app met de naam `WEBSITE_TIME_ZONE`.</span><span class="sxs-lookup"><span data-stu-id="3cc58-115">To have your CRON expression based on another time zone, create a new app setting for your function app named `WEBSITE_TIME_ZONE`.</span></span> <span data-ttu-id="3cc58-116">De waarde ingesteld op de naam van de gewenste tijdzone, zoals wordt weergegeven in de [Microsoft tijdzone Index](https://msdn.microsoft.com/library/ms912391.aspx).</span><span class="sxs-lookup"><span data-stu-id="3cc58-116">Set the value to the name of the desired time zone as shown in the [Microsoft Time Zone Index](https://msdn.microsoft.com/library/ms912391.aspx).</span></span> 

<span data-ttu-id="3cc58-117">Bijvoorbeeld: *Eastern (standaardtijd)* UTC-05:00.</span><span class="sxs-lookup"><span data-stu-id="3cc58-117">For example, *Eastern Standard Time* is UTC-05:00.</span></span> <span data-ttu-id="3cc58-118">Om uw timer fire activeren op 10:00 AM GMT elke dag, gebruikt u de volgende CRON-expressie die voor de UTC-tijdzone-accounts:</span><span class="sxs-lookup"><span data-stu-id="3cc58-118">To have your timer trigger fire at 10:00 AM EST every day, use the following CRON expression that accounts for UTC time zone:</span></span>

```json
"schedule": "0 0 15 * * *",
``` 

<span data-ttu-id="3cc58-119">U kunt ook kunt u een nieuwe appinstelling toevoegen voor de functie-app met de naam `WEBSITE_TIME_ZONE` en stel de waarde op **Eastern (standaardtijd)**.</span><span class="sxs-lookup"><span data-stu-id="3cc58-119">Alternatively, you could add a new app setting for your function app named `WEBSITE_TIME_ZONE` and set the value to **Eastern Standard Time**.</span></span>  <span data-ttu-id="3cc58-120">De volgende CRON-expressie kan vervolgens worden gebruikt voor 10:00 AM GMT:</span><span class="sxs-lookup"><span data-stu-id="3cc58-120">Then the following CRON expression could be used for 10:00 AM EST:</span></span> 

```json
"schedule": "0 0 10 * * *",
``` 


<a name="examples"></a>

## <a name="schedule-examples"></a><span data-ttu-id="3cc58-121">Voorbeelden van de planning</span><span class="sxs-lookup"><span data-stu-id="3cc58-121">Schedule examples</span></span>
<span data-ttu-id="3cc58-122">Hier volgen enkele voorbeelden van CRON-expressies die u kunt gebruiken voor de `schedule` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="3cc58-122">Here are some samples of CRON expressions you can use for the `schedule` property.</span></span> 

<span data-ttu-id="3cc58-123">Om de vijf minuten activeren:</span><span class="sxs-lookup"><span data-stu-id="3cc58-123">To trigger once every five minutes:</span></span>

```json
"schedule": "0 */5 * * * *"
```

<span data-ttu-id="3cc58-124">Voor het activeren van één keer aan de bovenkant van elk uur:</span><span class="sxs-lookup"><span data-stu-id="3cc58-124">To trigger once at the top of every hour:</span></span>

```json
"schedule": "0 0 * * * *",
```

<span data-ttu-id="3cc58-125">Voor het activeren van elke twee uur:</span><span class="sxs-lookup"><span data-stu-id="3cc58-125">To trigger once every two hours:</span></span>

```json
"schedule": "0 0 */2 * * *",
```

<span data-ttu-id="3cc58-126">Voor het activeren van één keer per uur van 9: 00 uur tot 5 PM:</span><span class="sxs-lookup"><span data-stu-id="3cc58-126">To trigger once every hour from 9 AM to 5 PM:</span></span>

```json
"schedule": "0 0 9-17 * * *",
```

<span data-ttu-id="3cc58-127">Om te activeren op elke dag 9:30 uur:</span><span class="sxs-lookup"><span data-stu-id="3cc58-127">To trigger At 9:30 AM every day:</span></span>

```json
"schedule": "0 30 9 * * *",
```

<span data-ttu-id="3cc58-128">Om te activeren om 9:30 AM elke weekdag:</span><span class="sxs-lookup"><span data-stu-id="3cc58-128">To trigger At 9:30 AM every weekday:</span></span>

```json
"schedule": "0 30 9 * * 1-5",
```

<a name="usage"></a>

## <a name="trigger-usage"></a><span data-ttu-id="3cc58-129">Gebruik van de trigger</span><span class="sxs-lookup"><span data-stu-id="3cc58-129">Trigger usage</span></span>
<span data-ttu-id="3cc58-130">Wanneer een functie van de trigger timer wordt opgeroepen, de [timerobject](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) wordt doorgegeven aan de functie.</span><span class="sxs-lookup"><span data-stu-id="3cc58-130">When a timer trigger function is invoked, the [timer object](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions/Extensions/Timers/TimerInfo.cs) is passed into the function.</span></span> <span data-ttu-id="3cc58-131">De volgende JSON is een voorbeeld-weergave van het timerobject.</span><span class="sxs-lookup"><span data-stu-id="3cc58-131">The following JSON is an example representation of the timer object.</span></span> 

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

## <a name="trigger-sample"></a><span data-ttu-id="3cc58-132">Voorbeeld van de trigger</span><span class="sxs-lookup"><span data-stu-id="3cc58-132">Trigger sample</span></span>
<span data-ttu-id="3cc58-133">Stel dat u hebt de volgende timertrigger in de `bindings` matrix van function.json:</span><span class="sxs-lookup"><span data-stu-id="3cc58-133">Suppose you have the following timer trigger in the `bindings` array of function.json:</span></span>

```json
{
    "schedule": "0 */5 * * * *",
    "name": "myTimer",
    "type": "timerTrigger",
    "direction": "in"
}
```

<span data-ttu-id="3cc58-134">Zie het voorbeeld taalspecifieke die de timerobject om te zien leest of deze later wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3cc58-134">See the language-specific sample that reads the timer object to see whether it's running late.</span></span>

* [<span data-ttu-id="3cc58-135">C#</span><span class="sxs-lookup"><span data-stu-id="3cc58-135">C#</span></span>](#triggercsharp)
* [<span data-ttu-id="3cc58-136">F#</span><span class="sxs-lookup"><span data-stu-id="3cc58-136">F#</span></span>](#triggerfsharp)
* [<span data-ttu-id="3cc58-137">Node.js</span><span class="sxs-lookup"><span data-stu-id="3cc58-137">Node.js</span></span>](#triggernodejs)

<a name="triggercsharp"></a>

### <a name="trigger-sample-in-c"></a><span data-ttu-id="3cc58-138">Voorbeeld van de trigger in C#</span><span class="sxs-lookup"><span data-stu-id="3cc58-138">Trigger sample in C#</span></span> #
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

### <a name="trigger-sample-in-f"></a><span data-ttu-id="3cc58-139">Voorbeeld van de trigger in F #</span><span class="sxs-lookup"><span data-stu-id="3cc58-139">Trigger sample in F#</span></span> #
```fsharp
let Run(myTimer: TimerInfo, log: TraceWriter ) =
    if (myTimer.IsPastDue) then
        log.Info("F# function is running late.")
    let now = DateTime.Now.ToLongTimeString()
    log.Info(sprintf "F# function executed at %s!" now)
```

<a name="triggernodejs"></a>

### <a name="trigger-sample-in-nodejs"></a><span data-ttu-id="3cc58-140">Voorbeeld van de trigger in Node.js</span><span class="sxs-lookup"><span data-stu-id="3cc58-140">Trigger sample in Node.js</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="3cc58-141">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3cc58-141">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

