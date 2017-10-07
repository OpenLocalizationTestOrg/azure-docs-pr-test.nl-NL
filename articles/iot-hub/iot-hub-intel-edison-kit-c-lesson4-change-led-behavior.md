---
title: 'Connect Intel Edison (C) tooAzure IoT - les 4: Hallo LED knipperen | Microsoft Docs'
description: Hallo-berichten toochange Hallo LED van in- en uitschakelen gedrag aanpassen.
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
ms.openlocfilehash: c51acb42aa297ca91cfe76d7b0361ad95e2fb2e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="change-hello-on-and-off-behavior-of-hello-led"></a>Hallo in- en uitschakelen gedrag van Hallo LED wijzigen
## <a name="what-you-will-do"></a>Wat u doet
Hallo-berichten toochange Hallo LED van in- en uitschakelen gedrag aanpassen. Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina][troubleshooting].

## <a name="what-you-will-learn"></a>Wat u leert
Gebruik aanvullende functies toochange Hallo LED van in- en uitgeschakeld gedrag.

## <a name="what-you-need"></a>Wat u nodig hebt
U moet hebt voltooid [een voorbeeldtoepassing uitvoeren op Intel Edison tooreceive cloud toodevice berichten][receive-cloud-to-device-messages].

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
     mraa_gpio_write(context, 1);
   }

   static void turnOffLED()
   {
     mraa_gpio_write(context, 0);
   }
   ```

   ![main.c-bestand met toegevoegde functies](media/iot-hub-intel-edison-lessons/lesson4/updated_app_c.png)

3. Toevoegen van de volgende voorwaarden voordat Hallo Hallo `else if` blok Hallo `receiveMessageCallback` functie:

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

   ![Bestand met toegevoegde functie Gulpfile.js][gulpfile]
5. In Hallo `sendMessage` werkt, Hallo regel vervangen `var message = buildMessage(sentMessageCount);` met Hallo nieuwe regel wordt weergegeven in het volgende codefragment Hallo:

   ```javascript
   var message = buildCustomMessage(sentMessageCount);
   ```
6. Alle Hallo wijzigingen worden opgeslagen.

### <a name="deploy-and-run-hello-sample-application"></a>Implementeren en uitvoeren van de voorbeeldtoepassing Hallo
Implementeren en uitvoeren van de voorbeeldtoepassing Hallo op Edison door het uitvoeren van de volgende opdracht Hallo:

```bash
gulp deploy && gulp run
```

U ziet Hallo LED inschakelen voor twee seconden en klik vervolgens uitschakelen voor een andere twee seconden. Hallo laatste 'stop'-bericht stopt Hallo voorbeeldtoepassing wordt uitgevoerd.

![in- of uitschakelen][on-and-off]

Gefeliciteerd. U hebt is aangepast Hallo-berichten die tooEdison uit uw IoT-hub worden verzonden.

### <a name="summary"></a>Samenvatting
Deze optionele sectie laat zien hoe toocustomize berichten zodat de voorbeeldtoepassing Hallo Hallo in- en uitschakelen gedrag van Hallo LED op een andere manier kunt beheren.

<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[receive-cloud-to-device-messages]: iot-hub-intel-edison-kit-c-lesson4-send-cloud-to-device-messages.md
[gulpfile]: media/iot-hub-intel-edison-lessons/lesson4/updated_gulpfile_c.png
[on-and-off]: media/iot-hub-intel-edison-lessons/lesson4/gulp_on_and_off_c.png
