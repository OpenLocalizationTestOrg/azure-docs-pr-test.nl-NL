---
title: 'Raspberry Pi (knooppunt) verbinden met Azure IoT - les 4: app wijzigen | Microsoft Docs'
description: De berichten te wijzigen van de LED van in- en uitschakelen gedrag aanpassen.
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
ms.openlocfilehash: b2ae23ac9cc1723936c4b4e1900b95cdcde744df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-on-and-off-behavior-of-the-led"></a><span data-ttu-id="d707f-104">De on- en uitgeschakeld gedrag van de LED wijzigen</span><span class="sxs-lookup"><span data-stu-id="d707f-104">Change the on and off behavior of the LED</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="d707f-105">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="d707f-105">What you will do</span></span>
<span data-ttu-id="d707f-106">De berichten te wijzigen van de LED van in- en uitschakelen gedrag aanpassen.</span><span class="sxs-lookup"><span data-stu-id="d707f-106">Customize the messages to change the LED’s on and off behavior.</span></span> <span data-ttu-id="d707f-107">Als u problemen hebt, oplossingen zoeken op de [probleemoplossing pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="d707f-107">If you have any problems, seek solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="d707f-108">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="d707f-108">What you will learn</span></span>
<span data-ttu-id="d707f-109">Aanvullende Node.js-functies gebruiken voor het wijzigen van de LED van in- en uitgeschakeld gedrag.</span><span class="sxs-lookup"><span data-stu-id="d707f-109">Use additional Node.js functions to change the LED’s on and off behavior.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="d707f-110">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="d707f-110">What you need</span></span>
<span data-ttu-id="d707f-111">U moet hebt voltooid [een voorbeeldtoepassing uitvoeren op frambozen Pi cloud-naar-apparaat-berichten ontvangen](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md).</span><span class="sxs-lookup"><span data-stu-id="d707f-111">You must have successfully completed [Run a sample application on Raspberry Pi to receive cloud-to-device messages](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md).</span></span>

## <a name="add-nodejs-functions"></a><span data-ttu-id="d707f-112">Node.js-functies toevoegen</span><span class="sxs-lookup"><span data-stu-id="d707f-112">Add Node.js functions</span></span>
1. <span data-ttu-id="d707f-113">De voorbeeldtoepassing openen in Visual Studio code met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="d707f-113">Open the sample application in Visual Studio code by running the following commands:</span></span>
   
   ```bash
   cd Lesson4
   code .
   ```
2. <span data-ttu-id="d707f-114">Open de `app.js` bestand en voeg vervolgens de volgende functies aan het einde:</span><span class="sxs-lookup"><span data-stu-id="d707f-114">Open the `app.js` file, and then add the following functions at the end:</span></span>
   
   ```javascript
   function turnOnLED() {
     wpi.digitalWrite(CONFIG_PIN, 1);
   }
   
   function turnOffLED() {
     wpi.digitalWrite(CONFIG_PIN, 0);
   }
   ```
   
   ![bestand App.js, waarbij toegevoegde functies](media/iot-hub-raspberry-pi-lessons/lesson4/updated_app_js.png)
3. <span data-ttu-id="d707f-116">De volgende condities voordat de standaardtabel in het blok switch-aanvraag van de `receiveMessageCallback` functie:</span><span class="sxs-lookup"><span data-stu-id="d707f-116">Add the following conditions before the default one in the switch-case block of the `receiveMessageCallback` function:</span></span>
   
   ```javascript
   case 'on':
     turnOnLED();
     break;
   case 'off':
     turnOffLED();
     break;
   ```
   
   <span data-ttu-id="d707f-117">Nu hebt u de voorbeeldtoepassing om te reageren op meer instructies via berichten geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="d707f-117">Now you’ve configured the sample application to respond to more instructions through messages.</span></span> <span data-ttu-id="d707f-118">De instructie 'op' Hiermee schakelt u de LED en schakelt u de instructie "off" uit de LED.</span><span class="sxs-lookup"><span data-stu-id="d707f-118">The "on" instruction turns on the LED, and the "off" instruction turns off the LED.</span></span>
4. <span data-ttu-id="d707f-119">Open het bestand gulpfile.js en voeg vervolgens een nieuwe functie voordat de functie `sendMessage`:</span><span class="sxs-lookup"><span data-stu-id="d707f-119">Open the gulpfile.js file, and then add a new function before the function `sendMessage`:</span></span>
   
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
5. <span data-ttu-id="d707f-121">In de `sendMessage` werken, worden vervangen door de regel `var message = buildMessage(sentMessageCount);` met de nieuwe regel wordt weergegeven in het volgende fragment:</span><span class="sxs-lookup"><span data-stu-id="d707f-121">In the `sendMessage` function, replace the line `var message = buildMessage(sentMessageCount);` with the new line shown in the following snippet:</span></span>
   
   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. <span data-ttu-id="d707f-122">Sla de wijzigingen op.</span><span class="sxs-lookup"><span data-stu-id="d707f-122">Save all the changes.</span></span>

### <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="d707f-123">Implementeren en uitvoeren van de voorbeeldtoepassing</span><span class="sxs-lookup"><span data-stu-id="d707f-123">Deploy and run the sample application</span></span>
<span data-ttu-id="d707f-124">Implementeren en uitvoeren van de voorbeeldtoepassing op Pi met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="d707f-124">Deploy and run the sample application on Pi by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

<span data-ttu-id="d707f-125">U ziet de LED inschakelen voor twee seconden en klik vervolgens uitschakelen voor een andere twee seconden.</span><span class="sxs-lookup"><span data-stu-id="d707f-125">You should see the LED turn on for two seconds, and then turn off for another two seconds.</span></span> <span data-ttu-id="d707f-126">Het laatste bericht met 'stop' stopt de voorbeeldtoepassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d707f-126">The last "stop" message stops the sample application from running.</span></span>

![Voorbeeld van een toepassing met in- en uitschakelen berichten](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off.png)

<span data-ttu-id="d707f-128">Gefeliciteerd.</span><span class="sxs-lookup"><span data-stu-id="d707f-128">Congratulations!</span></span> <span data-ttu-id="d707f-129">U hebt de berichten die worden verzonden naar Pi uit uw IoT-hub is aangepast.</span><span class="sxs-lookup"><span data-stu-id="d707f-129">You’ve successfully customized the messages that are sent to Pi from your IoT hub.</span></span>

### <a name="summary"></a><span data-ttu-id="d707f-130">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="d707f-130">Summary</span></span>
<span data-ttu-id="d707f-131">Deze optionele sectie laat zien hoe berichten aan te passen zodat de voorbeeldtoepassing op een andere manier de in- en uitgeschakeld gedrag van de LED kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="d707f-131">This optional section demonstrates how to customize messages so that the sample application can control the on and off behavior of the LED in a different way.</span></span>

