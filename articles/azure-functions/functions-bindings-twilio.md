---
title: aaaAzure functies Twilio binding | Microsoft Docs
description: Begrijpen hoe toouse Twilio bindingen met Azure Functions.
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: Azure functions, functies, verwerking van gebeurtenissen, dynamische compute zonder server architectuur
ms.assetid: a60263aa-3de9-4e1b-a2bb-0b52e70d559b
ms.service: functions
ms.devlang: multiple
ms.topic: reference
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 10/20/2016
ms.author: wesmc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 882853947850e7d6795ca5b2f3fb6b9a83ede182
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="send-sms-messages-from-azure-functions-using-hello-twilio-output-binding"></a><span data-ttu-id="0bbb3-104">SMS-berichten verzenden vanuit Azure Functions Hallo met Twilio uitvoer binding</span><span class="sxs-lookup"><span data-stu-id="0bbb3-104">Send SMS messages from Azure Functions using hello Twilio output binding</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="0bbb3-105">Dit artikel wordt uitgelegd hoe tooconfigure en gebruik Twilio-bindingen met Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="0bbb3-105">This article explains how tooconfigure and use Twilio bindings with Azure Functions.</span></span> 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="0bbb3-106">Azure Functions ondersteunt Twilio uitvoer bindingen tooenable uw tekst functies toosend SMS-berichten met een paar regels code en een [Twilio](https://www.twilio.com/) account.</span><span class="sxs-lookup"><span data-stu-id="0bbb3-106">Azure Functions supports Twilio output bindings tooenable your functions toosend SMS text messages with a few lines of code and a [Twilio](https://www.twilio.com/) account.</span></span> 

## <a name="functionjson-for-hello-twilio-output-binding"></a><span data-ttu-id="0bbb3-107">Function.JSON voor Hallo Twilio uitvoer binding</span><span class="sxs-lookup"><span data-stu-id="0bbb3-107">function.json for hello Twilio output binding</span></span>
<span data-ttu-id="0bbb3-108">Hallo function.json bestand biedt Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="0bbb3-108">hello function.json file provides hello following properties:</span></span>

* <span data-ttu-id="0bbb3-109">`name`: Naam variabele gebruikt in de functiecode voor Hallo Twilio SMS-bericht.</span><span class="sxs-lookup"><span data-stu-id="0bbb3-109">`name` : Variable name used in function code for hello Twilio SMS text message.</span></span>
* <span data-ttu-id="0bbb3-110">`type`: moet te worden ingesteld*'twilioSms'*.</span><span class="sxs-lookup"><span data-stu-id="0bbb3-110">`type` : must be set too*"twilioSms"*.</span></span>
* <span data-ttu-id="0bbb3-111">`accountSid`: Met deze waarde moet worden ingesteld als toohello-naam van een App-instelling van de Sid van uw Twilio-Account.</span><span class="sxs-lookup"><span data-stu-id="0bbb3-111">`accountSid` : This value must be set toohello name of an App Setting that holds your Twilio Account Sid.</span></span>
* <span data-ttu-id="0bbb3-112">`authToken`: Met deze waarde moet worden ingesteld als toohello-naam van een App-instelling die uw Twilio-verificatietoken bevat.</span><span class="sxs-lookup"><span data-stu-id="0bbb3-112">`authToken` : This value must be set toohello name of an App Setting that holds your Twilio authentication token.</span></span>
* <span data-ttu-id="0bbb3-113">`to`: Met deze waarde is ingesteld toohello telefoonnummer op dat naar Hallo SMS-tekstbericht wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="0bbb3-113">`to` : This value is set toohello phone number that hello SMS text is sent to.</span></span>
* <span data-ttu-id="0bbb3-114">`from`: Met deze waarde is ingesteld toohello telefoonnummer op dat door Hallo SMS-tekstbericht wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="0bbb3-114">`from` : This value is set toohello phone number that hello SMS text is sent from.</span></span>
* <span data-ttu-id="0bbb3-115">`direction`: moet te worden ingesteld*'out'*.</span><span class="sxs-lookup"><span data-stu-id="0bbb3-115">`direction` : must be set too*"out"*.</span></span>
* <span data-ttu-id="0bbb3-116">`body`: Met deze waarde mag gebruikte toohard code Hallo SMS-bericht als u geen tooset dynamisch in Hallo code voor de functie.</span><span class="sxs-lookup"><span data-stu-id="0bbb3-116">`body` : This value can be used toohard code hello SMS text message if you don't need tooset it dynamically in hello code for your function.</span></span> 

<span data-ttu-id="0bbb3-117">Voorbeeld function.json:</span><span class="sxs-lookup"><span data-stu-id="0bbb3-117">Example function.json:</span></span>

```json
{
  "type": "twilioSms",
  "name": "message",
  "accountSid": "TwilioAccountSid",
  "authToken": "TwilioAuthToken",
  "to": "+1704XXXXXXX",
  "from": "+1425XXXXXXX",
  "direction": "out",
  "body": "Azure Functions Testing"
}
```


## <a name="example-c-queue-trigger-with-twilio-output-binding"></a><span data-ttu-id="0bbb3-118">Voorbeeld van C# wachtrij trigger met Twilio uitvoer binding</span><span class="sxs-lookup"><span data-stu-id="0bbb3-118">Example C# queue trigger with Twilio output binding</span></span>
#### <a name="synchronous"></a><span data-ttu-id="0bbb3-119">Synchrone</span><span class="sxs-lookup"><span data-stu-id="0bbb3-119">Synchronous</span></span>
<span data-ttu-id="0bbb3-120">Deze voorbeeldcode synchrone voor een Azure Storage-wachtrij-trigger gebruikt een parameter toosend een tekst bericht tooa klant die een bestelling geplaatst.</span><span class="sxs-lookup"><span data-stu-id="0bbb3-120">This synchronous example code for an Azure Storage queue trigger uses an out parameter toosend a text message tooa customer who placed an order.</span></span>

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio;

public static void Run(string myQueueItem, out SMSMessage message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a JSON string representing an order that contains hello name of a 
    // customer and a mobile number toosend text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want toouse a hard coded message and number in hello binding, you must at least 
    // initialize hello SMSMessage variable.
    message = new SMSMessage();

    // A dynamic message can be set instead of hello body in hello output binding. In this example, we use 
    // hello order information toopersonalize a text message toohello mobile number provided for
    // order status updates.
    message.Body = msg;
    message.too= order.mobileNumber;
}
```

#### <a name="asynchronous"></a><span data-ttu-id="0bbb3-121">Asynchrone</span><span class="sxs-lookup"><span data-stu-id="0bbb3-121">Asynchronous</span></span>
<span data-ttu-id="0bbb3-122">Deze asynchrone voorbeeldcode voor een Azure Storage-trigger voor wachtrij stuurt een tekst bericht tooa klant die een bestelling geplaatst.</span><span class="sxs-lookup"><span data-stu-id="0bbb3-122">This asynchronous example code for an Azure Storage queue trigger sends a text message tooa customer who placed an order.</span></span>

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio;

public static async Task Run(string myQueueItem, IAsyncCollector<SMSMessage> message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example hello queue item is a JSON string representing an order that contains hello name of a 
    // customer and a mobile number toosend text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want toouse a hard coded message and number in hello binding, you must at least 
    // initialize hello SMSMessage variable.
    SMSMessage smsText = new SMSMessage();

    // A dynamic message can be set instead of hello body in hello output binding. In this example, we use 
    // hello order information toopersonalize a text message toohello mobile number provided for
    // order status updates.
    smsText.Body = msg;
    smsText.too= order.mobileNumber;

    await message.AddAsync(smsText);
}
```

## <a name="example-nodejs-queue-trigger-with-twilio-output-binding"></a><span data-ttu-id="0bbb3-123">Voorbeeld Node.js wachtrij trigger met Twilio uitvoer binding</span><span class="sxs-lookup"><span data-stu-id="0bbb3-123">Example Node.js queue trigger with Twilio output binding</span></span>
<span data-ttu-id="0bbb3-124">In dit voorbeeld Node.js verzendt een tekst bericht tooa klant die een bestelling geplaatst.</span><span class="sxs-lookup"><span data-stu-id="0bbb3-124">This Node.js example sends a text message tooa customer who placed an order.</span></span>

```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);

    // In this example hello queue item is a JSON string representing an order that contains hello name of a 
    // customer and a mobile number toosend text updates to.
    var msg = "Hello " + myQueueItem.name + ", thank you for your order.";

    // Even if you want toouse a hard coded message and number in hello binding, you must at least 
    // initialize hello message binding.
    context.bindings.message = {};

    // A dynamic message can be set instead of hello body in hello output binding. In this example, we use 
    // hello order information toopersonalize a text message toohello mobile number provided for
    // order status updates.
    context.bindings.message = {
        body : msg,
        too: myQueueItem.mobileNumber
    };

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="0bbb3-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0bbb3-125">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

