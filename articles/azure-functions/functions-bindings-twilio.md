---
title: Azure Functions Twilio-binding | Microsoft Docs
description: Begrijpen hoe Twilio-bindingen met Azure Functions.
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
ms.openlocfilehash: 870e47ec7f8ce41ee4acadc7b8ed59298958acbe
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="send-sms-messages-from-azure-functions-using-the-twilio-output-binding"></a><span data-ttu-id="3a1c9-104">SMS-bericht verzenden berichten van Azure Functions met behulp van de Twilio uitvoer binding</span><span class="sxs-lookup"><span data-stu-id="3a1c9-104">Send SMS messages from Azure Functions using the Twilio output binding</span></span>
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

<span data-ttu-id="3a1c9-105">In dit artikel wordt uitgelegd hoe configureren en gebruiken van Twilio-bindingen met Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="3a1c9-105">This article explains how to configure and use Twilio bindings with Azure Functions.</span></span> 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

<span data-ttu-id="3a1c9-106">Azure Functions ondersteunt Twilio uitvoer bindingen zodat uw functies voor het verzenden van SMS-berichten met een paar regels code en een [Twilio](https://www.twilio.com/) account.</span><span class="sxs-lookup"><span data-stu-id="3a1c9-106">Azure Functions supports Twilio output bindings to enable your functions to send SMS text messages with a few lines of code and a [Twilio](https://www.twilio.com/) account.</span></span> 

## <a name="functionjson-for-the-twilio-output-binding"></a><span data-ttu-id="3a1c9-107">Function.JSON voor de Twilio uitvoer binding</span><span class="sxs-lookup"><span data-stu-id="3a1c9-107">function.json for the Twilio output binding</span></span>
<span data-ttu-id="3a1c9-108">Het bestand function.json biedt de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="3a1c9-108">The function.json file provides the following properties:</span></span>

* <span data-ttu-id="3a1c9-109">`name`: Variabelenaam in functiecode gebruikt voor de Twilio SMS-bericht.</span><span class="sxs-lookup"><span data-stu-id="3a1c9-109">`name` : Variable name used in function code for the Twilio SMS text message.</span></span>
* <span data-ttu-id="3a1c9-110">`type`: moet worden ingesteld op *'twilioSms'*.</span><span class="sxs-lookup"><span data-stu-id="3a1c9-110">`type` : must be set to *"twilioSms"*.</span></span>
* <span data-ttu-id="3a1c9-111">`accountSid`: Met deze waarde moet worden ingesteld op de naam van een App-instelling van de Sid van uw Twilio-Account.</span><span class="sxs-lookup"><span data-stu-id="3a1c9-111">`accountSid` : This value must be set to the name of an App Setting that holds your Twilio Account Sid.</span></span>
* <span data-ttu-id="3a1c9-112">`authToken`: Met deze waarde moet worden ingesteld op de naam van een App-instelling die uw Twilio-verificatietoken bevat.</span><span class="sxs-lookup"><span data-stu-id="3a1c9-112">`authToken` : This value must be set to the name of an App Setting that holds your Twilio authentication token.</span></span>
* <span data-ttu-id="3a1c9-113">`to`: Deze waarde is ingesteld op het telefoonnummer dat naar de SMS-tekst wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="3a1c9-113">`to` : This value is set to the phone number that the SMS text is sent to.</span></span>
* <span data-ttu-id="3a1c9-114">`from`: Deze waarde is ingesteld op het telefoonnummer dat door de SMS-tekst wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="3a1c9-114">`from` : This value is set to the phone number that the SMS text is sent from.</span></span>
* <span data-ttu-id="3a1c9-115">`direction`: moet worden ingesteld op *'out'*.</span><span class="sxs-lookup"><span data-stu-id="3a1c9-115">`direction` : must be set to *"out"*.</span></span>
* <span data-ttu-id="3a1c9-116">`body`: Met deze waarde kan worden gebruikt voor de SMS-bericht harde code als u niet hoeft worden dynamisch ingesteld in de code voor de functie.</span><span class="sxs-lookup"><span data-stu-id="3a1c9-116">`body` : This value can be used to hard code the SMS text message if you don't need to set it dynamically in the code for your function.</span></span> 

<span data-ttu-id="3a1c9-117">Voorbeeld function.json:</span><span class="sxs-lookup"><span data-stu-id="3a1c9-117">Example function.json:</span></span>

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


## <a name="example-c-queue-trigger-with-twilio-output-binding"></a><span data-ttu-id="3a1c9-118">Voorbeeld van C# wachtrij trigger met Twilio uitvoer binding</span><span class="sxs-lookup"><span data-stu-id="3a1c9-118">Example C# queue trigger with Twilio output binding</span></span>
#### <a name="synchronous"></a><span data-ttu-id="3a1c9-119">Synchrone</span><span class="sxs-lookup"><span data-stu-id="3a1c9-119">Synchronous</span></span>
<span data-ttu-id="3a1c9-120">Deze synchrone voorbeeldcode voor een Azure Storage-wachtrij-trigger gebruikt een out-parameter voor een SMS-bericht verzenden naar een klant die een bestelling geplaatst.</span><span class="sxs-lookup"><span data-stu-id="3a1c9-120">This synchronous example code for an Azure Storage queue trigger uses an out parameter to send a text message to a customer who placed an order.</span></span>

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio;

public static void Run(string myQueueItem, out SMSMessage message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a JSON string representing an order that contains the name of a 
    // customer and a mobile number to send text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want to use a hard coded message and number in the binding, you must at least 
    // initialize the SMSMessage variable.
    message = new SMSMessage();

    // A dynamic message can be set instead of the body in the output binding. In this example, we use 
    // the order information to personalize a text message to the mobile number provided for
    // order status updates.
    message.Body = msg;
    message.To = order.mobileNumber;
}
```

#### <a name="asynchronous"></a><span data-ttu-id="3a1c9-121">Asynchrone</span><span class="sxs-lookup"><span data-stu-id="3a1c9-121">Asynchronous</span></span>
<span data-ttu-id="3a1c9-122">Deze asynchrone voorbeeldcode voor een Azure Storage-trigger voor wachtrij verzendt een SMS-bericht naar een klant die een bestelling geplaatst.</span><span class="sxs-lookup"><span data-stu-id="3a1c9-122">This asynchronous example code for an Azure Storage queue trigger sends a text message to a customer who placed an order.</span></span>

```cs
#r "Newtonsoft.Json"
#r "Twilio.Api"

using System;
using Newtonsoft.Json;
using Twilio;

public static async Task Run(string myQueueItem, IAsyncCollector<SMSMessage> message,  TraceWriter log)
{
    log.Info($"C# Queue trigger function processed: {myQueueItem}");

    // In this example the queue item is a JSON string representing an order that contains the name of a 
    // customer and a mobile number to send text updates to.
    dynamic order = JsonConvert.DeserializeObject(myQueueItem);
    string msg = "Hello " + order.name + ", thank you for your order.";

    // Even if you want to use a hard coded message and number in the binding, you must at least 
    // initialize the SMSMessage variable.
    SMSMessage smsText = new SMSMessage();

    // A dynamic message can be set instead of the body in the output binding. In this example, we use 
    // the order information to personalize a text message to the mobile number provided for
    // order status updates.
    smsText.Body = msg;
    smsText.To = order.mobileNumber;

    await message.AddAsync(smsText);
}
```

## <a name="example-nodejs-queue-trigger-with-twilio-output-binding"></a><span data-ttu-id="3a1c9-123">Voorbeeld Node.js wachtrij trigger met Twilio uitvoer binding</span><span class="sxs-lookup"><span data-stu-id="3a1c9-123">Example Node.js queue trigger with Twilio output binding</span></span>
<span data-ttu-id="3a1c9-124">In dit voorbeeld Node.js verzendt een SMS-bericht naar een klant die een bestelling geplaatst.</span><span class="sxs-lookup"><span data-stu-id="3a1c9-124">This Node.js example sends a text message to a customer who placed an order.</span></span>

```javascript
module.exports = function (context, myQueueItem) {
    context.log('Node.js queue trigger function processed work item', myQueueItem);

    // In this example the queue item is a JSON string representing an order that contains the name of a 
    // customer and a mobile number to send text updates to.
    var msg = "Hello " + myQueueItem.name + ", thank you for your order.";

    // Even if you want to use a hard coded message and number in the binding, you must at least 
    // initialize the message binding.
    context.bindings.message = {};

    // A dynamic message can be set instead of the body in the output binding. In this example, we use 
    // the order information to personalize a text message to the mobile number provided for
    // order status updates.
    context.bindings.message = {
        body : msg,
        to : myQueueItem.mobileNumber
    };

    context.done();
};
```

## <a name="next-steps"></a><span data-ttu-id="3a1c9-125">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3a1c9-125">Next steps</span></span>
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

