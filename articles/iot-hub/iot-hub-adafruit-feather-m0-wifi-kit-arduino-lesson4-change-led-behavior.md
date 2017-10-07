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
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a>Hallo in- en uitschakelen gedrag van Hallo LED wijzigen
## <a name="what-you-will-do"></a>Wat u doet
Hallo-berichten toochange Hallo LED van in- en uitschakelen gedrag aanpassen. Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md) voor uw kaart Adafruit Doezelaar M0 Wi-Fi Arduino.

## <a name="what-you-will-learn"></a>Wat u leert
Gebruik aanvullende Arduino functies toochange Hallo LED van in- en uitgeschakeld gedrag.

## <a name="what-you-need"></a>Wat u nodig hebt
U moet hebt voltooid [een voorbeeldtoepassing uitvoeren op uw cloud Arduino mededelingenbord tooreceive toodevice berichten][receive-cloud-to-device-messages].

## <a name="add-functions-toomainc-and-gulpfilejs"></a>Functies toomain.c en gulpfile.js toevoegen
1. Hallo-voorbeeldtoepassing openen in Visual Studio code door het uitvoeren van de volgende opdrachten Hallo:

   ```bash
   cd Lesson4
   code .
   ```
2. Open Hallo `app.ino` bestand en voeg vervolgens Hallo functies volgen na de blinkLED() functie:

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
3. Toevoegen van de volgende voorwaarden voordat Hallo Hallo `else if` blok Hallo `receiveMessageCallback` functie:

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

   U hebt nu Hallo voorbeeld toepassing toorespond toomore instructies via berichten geconfigureerd. Hallo 'aan'-instructie Hiermee schakelt u Hallo LED en Hallo "off" instructie Hallo LED uitgeschakeld.
4. Hallo gulpfile.js bestand openen en voeg vervolgens een nieuwe functie voordat de functie Hallo `sendMessage`:

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
5. In Hallo `sendMessage` werkt, Hallo regel vervangen `var message = buildMessage(sentMessageCount);` met Hallo nieuwe regel wordt weergegeven in het volgende codefragment Hallo:

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. Alle Hallo wijzigingen worden opgeslagen.

### <a name="deploy-and-run-hello-sample-application"></a>Implementeren en uitvoeren van de voorbeeldtoepassing Hallo
Implementeren en uitvoeren van de voorbeeldtoepassing Hallo op het mededelingenbord Arduino door het uitvoeren van de volgende opdracht Hallo:

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

U ziet Hallo LED inschakelen voor twee seconden en klik vervolgens uitschakelen voor een andere twee seconden. Hallo laatste 'stop'-bericht stopt Hallo voorbeeldtoepassing wordt uitgevoerd.

![in- of uitschakelen][on-and-off]

Gefeliciteerd. U hebt is aangepast Hallo-berichten die tooyour Arduino mededelingenbord van uw IoT-hub worden verzonden.

### <a name="summary"></a>Samenvatting
Deze optionele sectie laat zien hoe toocustomize berichten zodat de voorbeeldtoepassing Hallo Hallo in- en uitschakelen gedrag van Hallo LED op een andere manier kunt beheren.

<!-- Images and links -->

[receive-cloud-to-device-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-send-cloud-to-device-messages.md
[app-ino-file]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_app_ino.png
[gulp-file-js]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/updated_gulpfile_js.png
[on-and-off]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_on_and_off_arduino.png