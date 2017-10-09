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
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a>Hallo in- en uitschakelen gedrag van Hallo LED wijzigen
## <a name="what-you-will-do"></a>Wat u doet
Hallo-berichten toochange Hallo LED van in- en uitschakelen gedrag aanpassen. Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-raspberry-pi-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Wat u leert
Gebruik aanvullende Node.js functies toochange Hallo LED van in- en uitgeschakeld gedrag.

## <a name="what-you-need"></a>Wat u nodig hebt
U moet hebt voltooid [een voorbeeldtoepassing uitvoeren op frambozen Pi tooreceive cloud toodevice berichten](iot-hub-raspberry-pi-kit-c-lesson4-send-cloud-to-device-messages.md).

## <a name="add-functions-toomainc-and-gulpfilejs"></a>Functies toomain.c en gulpfile.js toevoegen
1. Hallo-voorbeeldtoepassing openen in Visual Studio code door het uitvoeren van de volgende opdrachten Hallo:

   ```bash
   cd Lesson4
   code .
   ```
2. Open Hallo `main.c` bestand en voeg vervolgens Hallo functies volgen na de blinkLED() functie:

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
3. Toevoegen van de volgende voorwaarden voordat Hallo standaard één in Hallo Hallo `if` blok Hallo `receiveMessageCallback` functie:

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
   }
   ```

   ![Bestand met toegevoegde functie Gulpfile.js](media/iot-hub-raspberry-pi-lessons/lesson4/updated_gulpfile_c.png)
5. In Hallo `sendMessage` werkt, Hallo regel vervangen `var message = buildMessage(sentMessageCount);` met Hallo nieuwe regel wordt weergegeven in het volgende codefragment Hallo:

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. Alle Hallo wijzigingen worden opgeslagen.

### <a name="deploy-and-run-hello-sample-application"></a>Implementeren en uitvoeren van de voorbeeldtoepassing Hallo
Implementeren en uitvoeren van de voorbeeldtoepassing Hallo op Pi door het uitvoeren van de volgende opdracht Hallo:

```bash
gulp deploy && gulp run
```

U ziet Hallo LED inschakelen voor twee seconden en klik vervolgens uitschakelen voor een andere twee seconden. Hallo laatste 'stop'-bericht stopt Hallo voorbeeldtoepassing wordt uitgevoerd.

![Voorbeeld van een toepassing met in- en uitschakelen berichten](media/iot-hub-raspberry-pi-lessons/lesson4/gulp_on_and_off_c.png)

Gefeliciteerd. U hebt is aangepast Hallo-berichten die tooPi uit uw IoT-hub worden verzonden.

### <a name="summary"></a>Samenvatting
Deze optionele sectie laat zien hoe toocustomize berichten zodat de voorbeeldtoepassing Hallo Hallo in- en uitschakelen gedrag van Hallo LED op een andere manier kunt beheren.
