---
title: 'Verbinding maken met frambozen Pi (knooppunt) tooAzure IoT - les 4: app wijzigen | Microsoft Docs'
description: Hallo-berichten toochange Hallo LED van in- en uitschakelen gedrag aanpassen.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: besturingselement geleid met raspberry pi raspberry pi geleid besturingselement raspberry pi besturingselement geleid
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 3b42a4ad-0197-42f6-8ca9-04c883e879e8
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 99b542fcb8639add0f5a0f7a49dd8abd0e224a51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a><span data-ttu-id="1c9c3-104">Hallo in- en uitschakelen gedrag van Hallo LED wijzigen</span><span class="sxs-lookup"><span data-stu-id="1c9c3-104">Change hello on and off behavior of hello LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="1c9c3-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="1c9c3-105">What you will do</span></span>
<span data-ttu-id="1c9c3-106">Hallo-berichten toochange Hallo LED van in- en uitschakelen gedrag aanpassen.</span><span class="sxs-lookup"><span data-stu-id="1c9c3-106">Customize hello messages toochange hello LED’s on and off behavior.</span></span> <span data-ttu-id="1c9c3-107">Als u problemen hebt, zoeken naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="1c9c3-107">If you have any problems, seek solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="1c9c3-108">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="1c9c3-108">What you will learn</span></span>
<span data-ttu-id="1c9c3-109">Gebruik aanvullende Node.js functies toochange Hallo LED van in- en uitgeschakeld gedrag.</span><span class="sxs-lookup"><span data-stu-id="1c9c3-109">Use additional Node.js functions toochange hello LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="1c9c3-110">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="1c9c3-110">What you need</span></span>
<span data-ttu-id="1c9c3-111">U moet hebt voltooid [een voorbeeldtoepassing uitvoeren op frambozen Pi tooreceive cloud-naar-apparaatberichten](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md).</span><span class="sxs-lookup"><span data-stu-id="1c9c3-111">You must have successfully completed [Run a sample application on Raspberry Pi tooreceive cloud-to-device messages](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md).</span></span>

## <a name="add-nodejs-functions"></a><span data-ttu-id="1c9c3-112">Node.js-functies toevoegen</span><span class="sxs-lookup"><span data-stu-id="1c9c3-112">Add Node.js functions</span></span>
1. <span data-ttu-id="1c9c3-113">Hallo-voorbeeldtoepassing openen in Visual Studio code door het uitvoeren van de volgende opdrachten Hallo:</span><span class="sxs-lookup"><span data-stu-id="1c9c3-113">Open hello sample application in Visual Studio code by running hello following commands:</span></span>
   
   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="1c9c3-114">Open Hallo `app.js` bestand en voeg vervolgens Hallo functies aan Hallo einde volgen:</span><span class="sxs-lookup"><span data-stu-id="1c9c3-114">Open hello `app.js` file, and then add hello following functions at hello end:</span></span>
   
   ```javascript
   function turnOnLED() {
     wpi.digitalWrite(CONFIG_PIN, 1);
   }
   
   function turnOffLED() {
     wpi.digitalWrite(CONFIG_PIN, 0);
   }
   ```
   
   ![bestand App.js, waarbij toegevoegde functies](media/iot-hub-raspberry-pi-lessons/lesson4/updated_app_js.png)
3. <span data-ttu-id="1c9c3-116">Toevoegen van de volgende voorwaarden voordat Hallo standaard één in Hallo switch case blok Hallo Hallo `receiveMessageCallback` functie:</span><span class="sxs-lookup"><span data-stu-id="1c9c3-116">Add hello following conditions before hello default one in hello switch-case block of hello `receiveMessageCallback` function:</span></span>
   
   ```javascript
   case 'on':
     turnOnLED();
     break;
   case 'off':
     turnOffLED();
     break;
   ```
   
   <span data-ttu-id="1c9c3-117">U hebt nu Hallo voorbeeld toepassing toorespond toomore instructies via berichten geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="1c9c3-117">Now you’ve configured hello sample application toorespond toomore instructions through messages.</span></span> <span data-ttu-id="1c9c3-118">Hallo 'aan'-instructie Hiermee schakelt u Hallo LED en Hallo "off" instructie Hallo LED uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="1c9c3-118">hello "on" instruction turns on hello LED, and hello "off" instruction turns off hello LED.</span></span>
4. <span data-ttu-id="1c9c3-119">Hallo gulpfile.js bestand openen en voeg vervolgens een nieuwe functie voordat de functie Hallo `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="1c9c3-119">Open hello gulpfile.js file, and then add a new function before hello function `sendMessage`:</span></span>
   
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
   
   ![Bestand met toegevoegde functie Gulpfile.js](media/iot-hub-raspberry-pi-lessons/lesson4/updated_gulpfile.png)
5. <span data-ttu-id="1c9c3-121">In Hallo `sendMessage` werkt, Hallo regel vervangen `var message = buildMessage(sentMessageCount);` met Hallo nieuwe regel wordt weergegeven in het volgende codefragment Hallo:</span><span class="sxs-lookup"><span data-stu-id="1c9c3-121">In hello `sendMessage` function, replace hello line `var message = buildMessage(sentMessageCount);` with hello new line shown in hello following snippet:</span></span>
   
   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="1c9c3-122">Alle Hallo wijzigingen worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="1c9c3-122">Save all hello changes.</span></span>

### <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="1c9c3-123">Implementeren en uitvoeren van de voorbeeldtoepassing Hallo</span><span class="sxs-lookup"><span data-stu-id="1c9c3-123">Deploy and run hello sample application</span></span>
<span data-ttu-id="1c9c3-124">Implementeren en uitvoeren van de voorbeeldtoepassing Hallo op Pi door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="1c9c3-124">Deploy and run hello sample application on Pi by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="1c9c3-125">U ziet Hallo LED inschakelen voor twee seconden en klik vervolgens uitschakelen voor een andere twee seconden.</span><span class="sxs-lookup"><span data-stu-id="1c9c3-125">You should see hello LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="1c9c3-126">Hallo laatste 'stop'-bericht stopt Hallo voorbeeldtoepassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="1c9c3-126">hello last "stop" message stops hello sample application from running.</span></span>

![Voorbeeld van een toepassing met in- en uitschakelen berichten](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off.png)

<span data-ttu-id="1c9c3-128">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="1c9c3-128">Congratulations!</span></span> <span data-ttu-id="1c9c3-129">U hebt is aangepast Hallo-berichten die tooPi uit uw IoT-hub worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="1c9c3-129">You’ve successfully customized hello messages that are sent tooPi from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="1c9c3-130">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="1c9c3-130">Summary</span></span>
<span data-ttu-id="1c9c3-131">Deze optionele sectie laat zien hoe toocustomize berichten zodat de voorbeeldtoepassing Hallo Hallo in- en uitschakelen gedrag van Hallo LED op een andere manier kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="1c9c3-131">This optional section demonstrates how toocustomize messages so that hello sample application can control hello on and off behavior of hello LED in a different way.</span></span>

