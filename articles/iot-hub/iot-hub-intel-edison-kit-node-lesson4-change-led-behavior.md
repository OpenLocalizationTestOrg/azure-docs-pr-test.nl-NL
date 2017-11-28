---
title: 'Verbinding maken met Intel Edison (knooppunt) tooAzure IoT - les 4: Hallo LED knipperen | Microsoft Docs'
description: Hallo-berichten toochange Hallo LED van in- en uitschakelen gedrag aanpassen.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: besturingselement met arduino geleid
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 387cd97e-b05e-43c4-b252-f68ad45d524a
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: caeabe311fd1698f298c6d2b4a203ecad80ef7df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a><span data-ttu-id="cbb3d-104">Hallo in- en uitschakelen gedrag van Hallo LED wijzigen</span><span class="sxs-lookup"><span data-stu-id="cbb3d-104">Change hello on and off behavior of hello LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="cbb3d-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="cbb3d-105">What you will do</span></span>
<span data-ttu-id="cbb3d-106">Hallo-berichten toochange Hallo LED van in- en uitschakelen gedrag aanpassen.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-106">Customize hello messages toochange hello LED’s on and off behavior.</span></span> <span data-ttu-id="cbb3d-107">Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="cbb3d-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="cbb3d-108">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="cbb3d-108">What you will learn</span></span>
<span data-ttu-id="cbb3d-109">Gebruik aanvullende functies toochange Hallo LED van in- en uitgeschakeld gedrag.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-109">Use additional functions toochange hello LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="cbb3d-110">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="cbb3d-110">What you need</span></span>
<span data-ttu-id="cbb3d-111">U moet hebt voltooid [een voorbeeldtoepassing uitvoeren op Intel Edison tooreceive cloud toodevice berichten][receive-cloud-to-device-messages].</span><span class="sxs-lookup"><span data-stu-id="cbb3d-111">You must have successfully completed [Run a sample application on Intel Edison tooreceive cloud toodevice messages][receive-cloud-to-device-messages].</span></span>

## <a name="add-functions-tooappjs-and-gulpfilejs"></a><span data-ttu-id="cbb3d-112">Functies tooapp.js en gulpfile.js toevoegen</span><span class="sxs-lookup"><span data-stu-id="cbb3d-112">Add functions tooapp.js and gulpfile.js</span></span>
1. <span data-ttu-id="cbb3d-113">Hallo-voorbeeldtoepassing openen in Visual Studio code door het uitvoeren van de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="cbb3d-113">Open hello sample application in Visual Studio code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="cbb3d-114">Open Hallo `app.js` bestand en voeg vervolgens Hallo functies volgen na de blinkLED() functie:</span><span class="sxs-lookup"><span data-stu-id="cbb3d-114">Open hello `app.js` file, and then add hello following functions after blinkLED() function:</span></span>

   ```javascript
   function turnOnLED() {
     myLed.write(1);
   }

   function turnOffLED() {
     myLed.write(0);
   }
   ```

   ![bestand App.js, waarbij toegevoegde functies](media/iot-hub-intel-edison-lessons/lesson4/updated_app_node.png)
3. <span data-ttu-id="cbb3d-116">Hallo volgende voorwaarden voordat Hallo 'knipperen' case in Hallo switch case blok Hallo toevoegen `receiveMessageCallback` functie:</span><span class="sxs-lookup"><span data-stu-id="cbb3d-116">Add hello following conditions before hello 'blink' case in hello switch-case block of hello `receiveMessageCallback` function:</span></span>

   ```javascript
   case 'on':
     turnOnLED();
     break;
   case 'off':
     turnOffLED();
     break;
   ```

   <span data-ttu-id="cbb3d-117">U hebt nu Hallo voorbeeld toepassing toorespond toomore instructies via berichten geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-117">Now you’ve configured hello sample application toorespond toomore instructions through messages.</span></span> <span data-ttu-id="cbb3d-118">Hallo 'aan'-instructie Hiermee schakelt u Hallo LED en Hallo "off" instructie Hallo LED uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-118">hello "on" instruction turns on hello LED, and hello "off" instruction turns off hello LED.</span></span>
4. <span data-ttu-id="cbb3d-119">Hallo gulpfile.js bestand openen en voeg vervolgens een nieuwe functie voordat de functie Hallo `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="cbb3d-119">Open hello gulpfile.js file, and then add a new function before hello function `sendMessage`:</span></span>

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
5. <span data-ttu-id="cbb3d-121">In Hallo `sendMessage` werkt, Hallo regel vervangen `var message = buildMessage(sentMessageCount);` met Hallo nieuwe regel wordt weergegeven in het volgende codefragment Hallo:</span><span class="sxs-lookup"><span data-stu-id="cbb3d-121">In hello `sendMessage` function, replace hello line `var message = buildMessage(sentMessageCount);` with hello new line shown in hello following snippet:</span></span>

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="cbb3d-122">Alle Hallo wijzigingen worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-122">Save all hello changes.</span></span>

### <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="cbb3d-123">Implementeren en uitvoeren van de voorbeeldtoepassing Hallo</span><span class="sxs-lookup"><span data-stu-id="cbb3d-123">Deploy and run hello sample application</span></span>
<span data-ttu-id="cbb3d-124">Implementeren en uitvoeren van de voorbeeldtoepassing Hallo op Edison door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="cbb3d-124">Deploy and run hello sample application on Edison by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="cbb3d-125">U ziet Hallo LED inschakelen voor twee seconden en klik vervolgens uitschakelen voor een andere twee seconden.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-125">You should see hello LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="cbb3d-126">Hallo laatste 'stop'-bericht stopt Hallo voorbeeldtoepassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-126">hello last "stop" message stops hello sample application from running.</span></span>

![in- of uitschakelen][on-and-off]

<span data-ttu-id="cbb3d-128">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-128">Congratulations!</span></span> <span data-ttu-id="cbb3d-129">U hebt is aangepast Hallo-berichten die tooEdison uit uw IoT-hub worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-129">You’ve successfully customized hello messages that are sent tooEdison from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="cbb3d-130">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="cbb3d-130">Summary</span></span>
<span data-ttu-id="cbb3d-131">Deze optionele sectie laat zien hoe toocustomize berichten zodat de voorbeeldtoepassing Hallo Hallo in- en uitschakelen gedrag van Hallo LED op een andere manier kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="cbb3d-131">This optional section demonstrates how toocustomize messages so that hello sample application can control hello on and off behavior of hello LED in a different way.</span></span>

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-node-lesson4-send-cloud-to-device-messages.md
[gulpfile]: media/iot-hub-intel-edison-lessons/lesson4/updated_gulpfile_node.png
[on-and-off]: media/iot-hub-intel-edison-lessons/lesson4/gulp_on_and_off_node.png
