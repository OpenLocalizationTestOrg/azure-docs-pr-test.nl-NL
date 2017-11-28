---
title: 'Connect Arduino (C) tooAzure IoT - les 4: app wijzigen | Microsoft Docs'
description: Hallo-berichten toochange Hallo LED van in- en uitschakelen gedrag aanpassen.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: besturingselement met arduino geleid
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: d7a25430-450e-43c4-a3ed-1eed995b8b7e
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 8cc438650f01ae4335d91c94df6a29e0ffbdc508
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a><span data-ttu-id="9985e-104">Hallo in- en uitschakelen gedrag van Hallo LED wijzigen</span><span class="sxs-lookup"><span data-stu-id="9985e-104">Change hello on and off behavior of hello LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="9985e-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="9985e-105">What you will do</span></span>
<span data-ttu-id="9985e-106">Hallo-berichten toochange Hallo LED van in- en uitschakelen gedrag aanpassen.</span><span class="sxs-lookup"><span data-stu-id="9985e-106">Customize hello messages toochange hello LED’s on and off behavior.</span></span> <span data-ttu-id="9985e-107">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) voor uw kaart Adafruit Doezelaar M0 Wi-Fi Arduino.</span><span class="sxs-lookup"><span data-stu-id="9985e-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) for your Adafruit Feather M0 WiFi Arduino board.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="9985e-108">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="9985e-108">What you will learn</span></span>
<span data-ttu-id="9985e-109">Gebruik aanvullende Arduino functies toochange Hallo LED van in- en uitgeschakeld gedrag.</span><span class="sxs-lookup"><span data-stu-id="9985e-109">Use additional Arduino functions toochange hello LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9985e-110">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="9985e-110">What you need</span></span>
<span data-ttu-id="9985e-111">U moet hebt voltooid [een voorbeeldtoepassing uitvoeren op uw cloud Arduino mededelingenbord tooreceive toodevice berichten][receive-cloud-to-device-messages].</span><span class="sxs-lookup"><span data-stu-id="9985e-111">You must have successfully completed [Run a sample application on your Arduino board tooreceive cloud toodevice messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-toomainc-and-gulpfilejs"></a><span data-ttu-id="9985e-112">Functies toomain.c en gulpfile.js toevoegen</span><span class="sxs-lookup"><span data-stu-id="9985e-112">Add functions toomain.c and gulpfile.js</span></span>
1. <span data-ttu-id="9985e-113">Hallo-voorbeeldtoepassing openen in Visual Studio code door het uitvoeren van de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="9985e-113">Open hello sample application in Visual Studio code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="9985e-114">Open Hallo `app.ino` bestand en voeg vervolgens Hallo functies volgen na de blinkLED() functie:</span><span class="sxs-lookup"><span data-stu-id="9985e-114">Open hello `app.ino` file, and then add hello following functions after blinkLED() function:</span></span>

   ```arduino
   static void turnOnLED()
   {
     digitalWrite(LED_PIN, HIGH);
   }

   static void turnOffLED()
   {
     digitalWrite(LED_PIN, LOW);
   }
   ```

   ![App.INO-bestand met toegevoegde functies][app-ino-file]
3. <span data-ttu-id="9985e-116">Toevoegen van de volgende voorwaarden voordat Hallo Hallo `else if` blok Hallo `receiveMessageCallback` functie:</span><span class="sxs-lookup"><span data-stu-id="9985e-116">Add hello following conditions before hello `else if` block of hello `receiveMessageCallback` function:</span></span>

   ```arduino
   else if (strcmp((const char*)value, "\"on\"") == 0)
   {
       turnOnLED();
   }
   else if (0 == strcmp((const char*)value, "\"off\"") == 0)
   {
       turnOffLED();
   }
   ```

   <span data-ttu-id="9985e-117">U hebt nu Hallo voorbeeld toepassing toorespond toomore instructies via berichten geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="9985e-117">Now you’ve configured hello sample application toorespond toomore instructions through messages.</span></span> <span data-ttu-id="9985e-118">Hallo 'aan'-instructie Hiermee schakelt u Hallo LED en Hallo "off" instructie Hallo LED uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="9985e-118">hello "on" instruction turns on hello LED, and hello "off" instruction turns off hello LED.</span></span>
4. <span data-ttu-id="9985e-119">Hallo gulpfile.js bestand openen en voeg vervolgens een nieuwe functie voordat de functie Hallo `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="9985e-119">Open hello gulpfile.js file, and then add a new function before hello function `sendMessage`:</span></span>

   ```javascript
   var buildCustomMessage = function (messageId) {
     if ((messageId & 1) && (messageId < MAX_MESSAGE_COUNT)) {
       return new Message(JSON.stringify({ command: 'on', messageId: messageId }));
     } else if (messageId < MAX_MESSAGE_COUNT) {
       return new Message(JSON.stringify({ command: 'off', messageId: messageId }));
     } else {
       return new Message(JSON.stringify({ command: 'stop', messageId: messageId }));
     }
   };
   ```

   ![Bestand met toegevoegde functie Gulpfile.js][gulp-file-js]
5. <span data-ttu-id="9985e-121">In Hallo `sendMessage` werkt, Hallo regel vervangen `var message = buildMessage(sentMessageCount);` met Hallo nieuwe regel wordt weergegeven in het volgende codefragment Hallo:</span><span class="sxs-lookup"><span data-stu-id="9985e-121">In hello `sendMessage` function, replace hello line `var message = buildMessage(sentMessageCount);` with hello new line shown in hello following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="9985e-122">Alle Hallo wijzigingen worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="9985e-122">Save all hello changes.</span></span>

### <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="9985e-123">Implementeren en uitvoeren van de voorbeeldtoepassing Hallo</span><span class="sxs-lookup"><span data-stu-id="9985e-123">Deploy and run hello sample application</span></span>
<span data-ttu-id="9985e-124">Implementeren en uitvoeren van de voorbeeldtoepassing Hallo op het mededelingenbord Arduino door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="9985e-124">Deploy and run hello sample application on your Arduino board by running hello following command:</span></span>

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="9985e-125">U ziet Hallo LED inschakelen voor twee seconden en klik vervolgens uitschakelen voor een andere twee seconden.</span><span class="sxs-lookup"><span data-stu-id="9985e-125">You should see hello LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="9985e-126">Hallo laatste 'stop'-bericht stopt Hallo voorbeeldtoepassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9985e-126">hello last "stop" message stops hello sample application from running.</span></span>

![in- of uitschakelen][on-and-off]

<span data-ttu-id="9985e-128">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="9985e-128">Congratulations!</span></span> <span data-ttu-id="9985e-129">U hebt is aangepast Hallo-berichten die tooyour Arduino mededelingenbord van uw IoT-hub worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="9985e-129">You’ve successfully customized hello messages that are sent tooyour Arduino board from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="9985e-130">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="9985e-130">Summary</span></span>
<span data-ttu-id="9985e-131">Deze optionele sectie laat zien hoe toocustomize berichten zodat de voorbeeldtoepassing Hallo Hallo in- en uitschakelen gedrag van Hallo LED op een andere manier kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="9985e-131">This optional section demonstrates how toocustomize messages so that hello sample application can control hello on and off behavior of hello LED in a different way.</span></span>

<!-- Images and links -->

[receive-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md
[app-ino-file]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_app_ino.png
[gulp-file-js]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_gulpfile_js.png
[on-and-off]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_on_and_off_arduino.png