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
# <a name="change-the-on-and-off-behavior-of-the-led"></a>De on- en uitgeschakeld gedrag van de LED wijzigen
## <a name="what-you-will-do"></a>Wat u doet
De berichten te wijzigen van de LED van in- en uitschakelen gedrag aanpassen. Als u problemen hebt, oplossingen zoeken op de [probleemoplossing pagina](iot-hub-raspberry-pi-kit-node-troubleshooting.md).

## <a name="what-you-will-learn"></a>Wat u leert
Aanvullende Node.js-functies gebruiken voor het wijzigen van de LED van in- en uitgeschakeld gedrag.

## <a name="what-you-need"></a>Wat u nodig hebt
U moet hebt voltooid [een voorbeeldtoepassing uitvoeren op frambozen Pi cloud-naar-apparaat-berichten ontvangen](iot-hub-raspberry-pi-kit-node-lesson4-send-cloud-to-device-messages.md).

## <a name="add-nodejs-functions"></a>Node.js-functies toevoegen
1. De voorbeeldtoepassing openen in Visual Studio code met de volgende opdrachten:
   
   ```bash
   cd Lesson4
   code .
   ```
2. Open de `app.js` bestand en voeg vervolgens de volgende functies aan het einde:
   
   ```javascript
   function turnOnLED() {
     wpi.digitalWrite(CONFIG_PIN, 1);
   }
   
   function turnOffLED() {
     wpi.digitalWrite(CONFIG_PIN, 0);
   }
   ```
   
   ![bestand App.js, waarbij toegevoegde functies](media/iot-hub-raspberry-pi-lessons/lesson4/updated_app_js.png)
3. De volgende condities voordat de standaardtabel in het blok switch-aanvraag van de `receiveMessageCallback` functie:
   
   ```javascript
   case 'on':
     turnOnLED();
     break;
   case 'off':
     turnOffLED();
     break;
   ```
   
   Nu hebt u de voorbeeldtoepassing om te reageren op meer instructies via berichten geconfigureerd. De instructie 'op' Hiermee schakelt u de LED en schakelt u de instructie "off" uit de LED.
4. Open het bestand gulpfile.js en voeg vervolgens een nieuwe functie voordat de functie `sendMessage`:
   
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
5. In de `sendMessage` werken, worden vervangen door de regel `var message = buildMessage(sentMessageCount);` met de nieuwe regel wordt weergegeven in het volgende fragment:
   
   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. Sla de wijzigingen op.

### <a name="deploy-and-run-the-sample-application"></a>Implementeren en uitvoeren van de voorbeeldtoepassing
Implementeren en uitvoeren van de voorbeeldtoepassing op Pi met de volgende opdracht:

```bash
gulp deploy && gulp run
```

U ziet de LED inschakelen voor twee seconden en klik vervolgens uitschakelen voor een andere twee seconden. Het laatste bericht met 'stop' stopt de voorbeeldtoepassing wordt uitgevoerd.

![Voorbeeld van een toepassing met in- en uitschakelen berichten](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off.png)

Gefeliciteerd. U hebt de berichten die worden verzonden naar Pi uit uw IoT-hub is aangepast.

### <a name="summary"></a>Samenvatting
Deze optionele sectie laat zien hoe berichten aan te passen zodat de voorbeeldtoepassing op een andere manier de in- en uitgeschakeld gedrag van de LED kunt beheren.

