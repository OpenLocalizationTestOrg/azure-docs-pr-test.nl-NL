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
# <a name="send-sms-messages-from-azure-functions-using-hello-twilio-output-binding"></a>SMS-berichten verzenden vanuit Azure Functions Hallo met Twilio uitvoer binding
[!INCLUDE [functions-selector-bindings](../../includes/functions-selector-bindings.md)]

Dit artikel wordt uitgelegd hoe tooconfigure en gebruik Twilio-bindingen met Azure Functions. 

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

Azure Functions ondersteunt Twilio uitvoer bindingen tooenable uw tekst functies toosend SMS-berichten met een paar regels code en een [Twilio](https://www.twilio.com/) account. 

## <a name="functionjson-for-hello-twilio-output-binding"></a>Function.JSON voor Hallo Twilio uitvoer binding
Hallo function.json bestand biedt Hallo volgende eigenschappen:

* `name`: Naam variabele gebruikt in de functiecode voor Hallo Twilio SMS-bericht.
* `type`: moet te worden ingesteld*'twilioSms'*.
* `accountSid`: Met deze waarde moet worden ingesteld als toohello-naam van een App-instelling van de Sid van uw Twilio-Account.
* `authToken`: Met deze waarde moet worden ingesteld als toohello-naam van een App-instelling die uw Twilio-verificatietoken bevat.
* `to`: Met deze waarde is ingesteld toohello telefoonnummer op dat naar Hallo SMS-tekstbericht wordt verzonden.
* `from`: Met deze waarde is ingesteld toohello telefoonnummer op dat door Hallo SMS-tekstbericht wordt verzonden.
* `direction`: moet te worden ingesteld*'out'*.
* `body`: Met deze waarde mag gebruikte toohard code Hallo SMS-bericht als u geen tooset dynamisch in Hallo code voor de functie. 

Voorbeeld function.json:

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


## <a name="example-c-queue-trigger-with-twilio-output-binding"></a>Voorbeeld van C# wachtrij trigger met Twilio uitvoer binding
#### <a name="synchronous"></a>Synchrone
Deze voorbeeldcode synchrone voor een Azure Storage-wachtrij-trigger gebruikt een parameter toosend een tekst bericht tooa klant die een bestelling geplaatst.

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

#### <a name="asynchronous"></a>Asynchrone
Deze asynchrone voorbeeldcode voor een Azure Storage-trigger voor wachtrij stuurt een tekst bericht tooa klant die een bestelling geplaatst.

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

## <a name="example-nodejs-queue-trigger-with-twilio-output-binding"></a>Voorbeeld Node.js wachtrij trigger met Twilio uitvoer binding
In dit voorbeeld Node.js verzendt een tekst bericht tooa klant die een bestelling geplaatst.

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

## <a name="next-steps"></a>Volgende stappen
[!INCLUDE [next steps](../../includes/functions-bindings-next-steps.md)]

