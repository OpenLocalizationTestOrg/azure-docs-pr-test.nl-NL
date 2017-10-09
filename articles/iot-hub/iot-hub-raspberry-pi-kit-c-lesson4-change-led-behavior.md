---
title: 'Connect Raspberry PI (C) tooAzure IoT - les 4: app wijzigen | Microsoft Docs'
description: Hallo-berichten toochange Hallo LED van in- en uitschakelen gedrag aanpassen.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: besturingselement geleid met raspberry pi raspberry pi geleid besturingselement raspberry pi besturingselement geleid
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: 0201b8ed-d5e6-4445-9a4d-1305003d1eff
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: f4739c4e9a58b4b0fe964b5c3c81e5918982099f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a><span data-ttu-id="57aa0-104">Hallo in- en uitschakelen gedrag van Hallo LED wijzigen</span><span class="sxs-lookup"><span data-stu-id="57aa0-104">Change hello on and off behavior of hello LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="57aa0-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="57aa0-105">What you will do</span></span>
<span data-ttu-id="57aa0-106">Hallo-berichten toochange Hallo LED van in- en uitschakelen gedrag aanpassen.</span><span class="sxs-lookup"><span data-stu-id="57aa0-106">Customize hello messages toochange hello LED’s on and off behavior.</span></span> <span data-ttu-id="57aa0-107">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="57aa0-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="57aa0-108">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="57aa0-108">What you will learn</span></span>
<span data-ttu-id="57aa0-109">Gebruik aanvullende Node.js functies toochange Hallo LED van in- en uitgeschakeld gedrag.</span><span class="sxs-lookup"><span data-stu-id="57aa0-109">Use additional Node.js functions toochange hello LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="57aa0-110">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="57aa0-110">What you need</span></span>
<span data-ttu-id="57aa0-111">U moet hebt voltooid [een voorbeeldtoepassing uitvoeren op frambozen Pi tooreceive cloud toodevice berichten](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md).</span><span class="sxs-lookup"><span data-stu-id="57aa0-111">You must have successfully completed [Run a sample application on Raspberry Pi tooreceive cloud toodevice messages](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md).</span></span>

## <a name="add-functions-toomainc-and-gulpfilejs"></a><span data-ttu-id="57aa0-112">Functies toomain.c en gulpfile.js toevoegen</span><span class="sxs-lookup"><span data-stu-id="57aa0-112">Add functions toomain.c and gulpfile.js</span></span>
1. <span data-ttu-id="57aa0-113">Hallo-voorbeeldtoepassing openen in Visual Studio code door het uitvoeren van de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="57aa0-113">Open hello sample application in Visual Studio code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="57aa0-114">Open Hallo `main.c` bestand en voeg vervolgens Hallo functies volgen na de blinkLED() functie:</span><span class="sxs-lookup"><span data-stu-id="57aa0-114">Open hello `main.c` file, and then add hello following functions after blinkLED() function:</span></span>

   ```c
   static void turnOnLED()
   {
     digitalWrite(LED_PIN, HIGH);
   }

   static void turnOffLED()
   {
     digitalWrite(LED_PIN, LOW);
   }
   ```

   ![main.c-bestand met toegevoegde functies](media/iot-hub-raspberry-pi-lessons/lesson4/updated_app_c.png)
3. <span data-ttu-id="57aa0-116">Toevoegen van de volgende voorwaarden voordat Hallo standaard één in Hallo Hallo `if` blok Hallo `receiveMessageCallback` functie:</span><span class="sxs-lookup"><span data-stu-id="57aa0-116">Add hello following conditions before hello default one in hello `if` block of hello `receiveMessageCallback` function:</span></span>

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

   <span data-ttu-id="57aa0-117">U hebt nu Hallo voorbeeld toepassing toorespond toomore instructies via berichten geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="57aa0-117">Now you’ve configured hello sample application toorespond toomore instructions through messages.</span></span> <span data-ttu-id="57aa0-118">Hallo 'aan'-instructie Hiermee schakelt u Hallo LED en Hallo "off" instructie Hallo LED uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="57aa0-118">hello "on" instruction turns on hello LED, and hello "off" instruction turns off hello LED.</span></span>
4. <span data-ttu-id="57aa0-119">Hallo gulpfile.js bestand openen en voeg vervolgens een nieuwe functie voordat de functie Hallo `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="57aa0-119">Open hello gulpfile.js file, and then add a new function before hello function `sendMessage`:</span></span>

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

   ![Bestand met toegevoegde functie Gulpfile.js](media/iot-hub-raspberry-pi-lessons/lesson4/updated_gulpfile_c.png)
5. <span data-ttu-id="57aa0-121">In Hallo `sendMessage` werkt, Hallo regel vervangen `var message = buildMessage(sentMessageCount);` met Hallo nieuwe regel wordt weergegeven in het volgende codefragment Hallo:</span><span class="sxs-lookup"><span data-stu-id="57aa0-121">In hello `sendMessage` function, replace hello line `var message = buildMessage(sentMessageCount);` with hello new line shown in hello following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="57aa0-122">Alle Hallo wijzigingen worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="57aa0-122">Save all hello changes.</span></span>

### <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="57aa0-123">Implementeren en uitvoeren van de voorbeeldtoepassing Hallo</span><span class="sxs-lookup"><span data-stu-id="57aa0-123">Deploy and run hello sample application</span></span>
<span data-ttu-id="57aa0-124">Implementeren en uitvoeren van de voorbeeldtoepassing Hallo op Pi door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="57aa0-124">Deploy and run hello sample application on Pi by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="57aa0-125">U ziet Hallo LED inschakelen voor twee seconden en klik vervolgens uitschakelen voor een andere twee seconden.</span><span class="sxs-lookup"><span data-stu-id="57aa0-125">You should see hello LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="57aa0-126">Hallo laatste 'stop'-bericht stopt Hallo voorbeeldtoepassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="57aa0-126">hello last "stop" message stops hello sample application from running.</span></span>

![Voorbeeld van een toepassing met in- en uitschakelen berichten](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off_c.png)

<span data-ttu-id="57aa0-128">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="57aa0-128">Congratulations!</span></span> <span data-ttu-id="57aa0-129">U hebt is aangepast Hallo-berichten die tooPi uit uw IoT-hub worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="57aa0-129">You’ve successfully customized hello messages that are sent tooPi from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="57aa0-130">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="57aa0-130">Summary</span></span>
<span data-ttu-id="57aa0-131">Deze optionele sectie laat zien hoe toocustomize berichten zodat de voorbeeldtoepassing Hallo Hallo in- en uitschakelen gedrag van Hallo LED op een andere manier kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="57aa0-131">This optional section demonstrates how toocustomize messages so that hello sample application can control hello on and off behavior of hello LED in a different way.</span></span>
