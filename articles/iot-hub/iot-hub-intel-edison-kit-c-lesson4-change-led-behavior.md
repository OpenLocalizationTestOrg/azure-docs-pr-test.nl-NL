---
title: 'Intel Edison (C) verbinden met Azure IoT - les 4: de LED knipperen | Microsoft Docs'
description: De berichten te wijzigen van de LED van in- en uitschakelen gedrag aanpassen.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: besturingselement met arduino geleid
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 9826c55a-0e24-4296-ae54-29b7fe66436a
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4852b1cca4c6186ef4857b903b771f76cc20adb8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-on-and-off-behavior-of-the-led"></a><span data-ttu-id="8d42e-104">De on- en uitgeschakeld gedrag van de LED wijzigen</span><span class="sxs-lookup"><span data-stu-id="8d42e-104">Change the on and off behavior of the LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="8d42e-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="8d42e-105">What you will do</span></span>
<span data-ttu-id="8d42e-106">De berichten te wijzigen van de LED van in- en uitschakelen gedrag aanpassen.</span><span class="sxs-lookup"><span data-stu-id="8d42e-106">Customize the messages to change the LED’s on and off behavior.</span></span> <span data-ttu-id="8d42e-107">Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="8d42e-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="8d42e-108">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="8d42e-108">What you will learn</span></span>
<span data-ttu-id="8d42e-109">Aanvullende functies gebruiken om te wijzigen van de LED van in- en uitgeschakeld gedrag.</span><span class="sxs-lookup"><span data-stu-id="8d42e-109">Use additional functions to change the LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="8d42e-110">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="8d42e-110">What you need</span></span>
<span data-ttu-id="8d42e-111">U moet hebt voltooid [een voorbeeldtoepassing uitvoeren op Intel Edison cloud naar apparaat-berichten ontvangen][receive-cloud-to-device-messages].</span><span class="sxs-lookup"><span data-stu-id="8d42e-111">You must have successfully completed [Run a sample application on Intel Edison to receive cloud to device messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-to-mainc-and-gulpfilejs"></a><span data-ttu-id="8d42e-112">Functies toevoegen aan main.c en gulpfile.js</span><span class="sxs-lookup"><span data-stu-id="8d42e-112">Add functions to main.c and gulpfile.js</span></span>
1. <span data-ttu-id="8d42e-113">De voorbeeldtoepassing openen in Visual Studio code met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="8d42e-113">Open the sample application in Visual Studio code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="8d42e-114">Open de `main.c` bestand en voeg vervolgens de volgende functies na de blinkLED() functie:</span><span class="sxs-lookup"><span data-stu-id="8d42e-114">Open the `main.c` file, and then add the following functions after blinkLED() function:</span></span>

   ```c
   static void turnOnLED()
   {
     mraa_gpio_write(context, 1);
   }

   static void turnOffLED()
   {
     mraa_gpio_write(context, 0);
   }
   ```

   ![main.c-bestand met toegevoegde functies](media/iot-hub-intel-edison-lessons/lesson4/updated_app_c.png)

3. <span data-ttu-id="8d42e-116">De volgende condities voordat de `else if` blokkeren van de `receiveMessageCallback` functie:</span><span class="sxs-lookup"><span data-stu-id="8d42e-116">Add the following conditions before the `else if` block of the `receiveMessageCallback` function:</span></span>

   ```c
   else if (0 == strcmp((const char*)value, "\"on\""))
   {
       turnOnLED();
   }
   else if (0 == strcmp((const char*)value, "\"off\""))
   {
       turnOffLED();
   }
   ```

   <span data-ttu-id="8d42e-117">Nu hebt u de voorbeeldtoepassing om te reageren op meer instructies via berichten geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="8d42e-117">Now you’ve configured the sample application to respond to more instructions through messages.</span></span> <span data-ttu-id="8d42e-118">De instructie 'op' Hiermee schakelt u de LED en schakelt u de instructie "off" uit de LED.</span><span class="sxs-lookup"><span data-stu-id="8d42e-118">The "on" instruction turns on the LED, and the "off" instruction turns off the LED.</span></span>
4. <span data-ttu-id="8d42e-119">Open het bestand gulpfile.js en voeg vervolgens een nieuwe functie voordat de functie `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="8d42e-119">Open the gulpfile.js file, and then add a new function before the function `sendMessage`:</span></span>

   ```javascript
   var buildCustomMessage = function (messageId) {
     if ((messageId & 1) && (messageId < MAX_MESSAGE_COUNT)) {
       return new Message(JSON.stringify({ command: 'on', messageId: messageId }));
     } else if (messageId < MAX_MESSAGE_COUNT) {
       return new Message(JSON.stringify({ command: 'off', messageId: messageId }));
     } else {
       return new Message(JSON.stringify({ command: 'stop', messageId: messageId }));
     }
   }
   ```

   ![Bestand met toegevoegde functie Gulpfile.js][gulpfile]
5. <span data-ttu-id="8d42e-121">In de `sendMessage` werken, worden vervangen door de regel `var message = buildMessage(sentMessageCount);` met de nieuwe regel wordt weergegeven in het volgende fragment:</span><span class="sxs-lookup"><span data-stu-id="8d42e-121">In the `sendMessage` function, replace the line `var message = buildMessage(sentMessageCount);` with the new line shown in the following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="8d42e-122">Sla de wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="8d42e-122">Save all the changes.</span></span>

### <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="8d42e-123">Implementeren en uitvoeren van de voorbeeldtoepassing</span><span class="sxs-lookup"><span data-stu-id="8d42e-123">Deploy and run the sample application</span></span>
<span data-ttu-id="8d42e-124">Implementeren en uitvoeren van de voorbeeldtoepassing op Edison met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="8d42e-124">Deploy and run the sample application on Edison by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="8d42e-125">U ziet de LED inschakelen voor twee seconden en klik vervolgens uitschakelen voor een andere twee seconden.</span><span class="sxs-lookup"><span data-stu-id="8d42e-125">You should see the LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="8d42e-126">Het laatste bericht met 'stop' stopt de voorbeeldtoepassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8d42e-126">The last "stop" message stops the sample application from running.</span></span>

![in- of uitschakelen][on-and-off]

<span data-ttu-id="8d42e-128">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="8d42e-128">Congratulations!</span></span> <span data-ttu-id="8d42e-129">U hebt de berichten die worden verzonden naar Edison uit uw IoT-hub is aangepast.</span><span class="sxs-lookup"><span data-stu-id="8d42e-129">You’ve successfully customized the messages that are sent to Edison from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="8d42e-130">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="8d42e-130">Summary</span></span>
<span data-ttu-id="8d42e-131">Deze optionele sectie laat zien hoe berichten aan te passen zodat de voorbeeldtoepassing op een andere manier de in- en uitgeschakeld gedrag van de LED kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="8d42e-131">This optional section demonstrates how to customize messages so that the sample application can control the on and off behavior of the LED in a different way.</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-c-lesson4-send-cloud-to-device-messages.md
[gulpfile]: media/iot-hub-intel-edison-lessons/lesson4/updated_gulpfile_c.png
[on-and-off]: media/iot-hub-intel-edison-lessons/lesson4/gulp_on_and_off_c.png
