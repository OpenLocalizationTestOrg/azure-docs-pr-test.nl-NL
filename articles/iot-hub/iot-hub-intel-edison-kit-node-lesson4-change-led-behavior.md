---
title: 'Intel Edison (knooppunt) verbinden met Azure IoT - les 4: de LED knipperen | Microsoft Docs'
description: De berichten te wijzigen van de LED van in- en uitschakelen gedrag aanpassen.
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
ms.openlocfilehash: fa99050dad62534e2825e93f1170d2f3ecf5a3ba
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="change-the-on-and-off-behavior-of-the-led"></a>De on- en uitgeschakeld gedrag van de LED wijzigen
## <a name="what-you-will-do"></a>Wat u doet
De berichten te wijzigen van de LED van in- en uitschakelen gedrag aanpassen. Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina][troubleshooting].

## <a name="what-you-will-learn"></a>Wat u leert
Aanvullende functies gebruiken om te wijzigen van de LED van in- en uitgeschakeld gedrag.

## <a name="what-you-need"></a>Wat u nodig hebt
U moet hebt voltooid [een voorbeeldtoepassing uitvoeren op Intel Edison cloud naar apparaat-berichten ontvangen][receive-cloud-to-device-messages].

## <a name="add-functions-to-appjs-and-gulpfilejs"></a>Functies toevoegen aan app.js en gulpfile.js
1. De voorbeeldtoepassing openen in Visual Studio code met de volgende opdrachten:

   ```bash
   cd Lesson4
   code .
   ```
2. Open de `app.js` bestand en voeg vervolgens de volgende functies na de blinkLED() functie:

   ```javascript
   function turnOnLED() {
     myLed.write(1);
   }

   function turnOffLED() {
     myLed.write(0);
   }
   ```

   ![bestand App.js, waarbij toegevoegde functies](media/iot-hub-intel-edison-lessons/lesson4/updated_app_node.png)
3. De volgende condities voordat de aanvraag 'knipperen' in het blok switch-aanvraag van de `receiveMessageCallback` functie:

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

   ![Bestand met toegevoegde functie Gulpfile.js][gulpfile]
5. In de `sendMessage` werken, worden vervangen door de regel `var message = buildMessage(sentMessageCount);` met de nieuwe regel wordt weergegeven in het volgende fragment:

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. Sla de wijzigingen op.

### <a name="deploy-and-run-the-sample-application"></a>Implementeren en uitvoeren van de voorbeeldtoepassing
Implementeren en uitvoeren van de voorbeeldtoepassing op Edison met de volgende opdracht:

```bash
gulp deploy && gulp run
```

U ziet de LED inschakelen voor twee seconden en klik vervolgens uitschakelen voor een andere twee seconden. Het laatste bericht met 'stop' stopt de voorbeeldtoepassing wordt uitgevoerd.

![in- of uitschakelen][on-and-off]

Gefeliciteerd. U hebt de berichten die worden verzonden naar Edison uit uw IoT-hub is aangepast.

### <a name="summary"></a>Samenvatting
Deze optionele sectie laat zien hoe berichten aan te passen zodat de voorbeeldtoepassing op een andere manier de in- en uitgeschakeld gedrag van de LED kunt beheren.

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-node-lesson4-send-cloud-to-device-messages.md
[gulpfile]: media/iot-hub-intel-edison-lessons/lesson4/updated_gulpfile_node.png
[on-and-off]: media/iot-hub-intel-edison-lessons/lesson4/gulp_on_and_off_node.png
