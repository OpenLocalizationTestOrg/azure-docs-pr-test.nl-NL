---
title: 'Verbinding maken met Arduino tooAzure IoT - les 1: app implementeren | Microsoft Docs'
description: Hallo voorbeeldtoepassing Arduino vanuit GitHub klonen en voer gulp toodeploy deze toepassing tooyour Adafruit Doezelaar M0 Wi-Fi. Deze voorbeeldtoepassing knippert Hallo GPIO
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: arduino geleid projecten, arduino geleid knipperen, arduino geleid knipperen code, arduino knipperen programma, arduino knipperen voorbeeld
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: b0a7d076-d580-4686-9f7d-c0712750b615
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5bf8e4ae88e070aeacf34bfc43b8d2daeeb1a2fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a>Hallo knipperen toepassing maken en implementeren
## <a name="what-you-will-do"></a>Wat u doet
Hallo voorbeeldtoepassing Arduino vanuit GitHub klonen en Hallo gulp hulpprogramma toodeploy Hallo voorbeeld toepassing tooyour Adafruit Doezelaar M0 Wi-Fi Arduino mededelingenbord gebruiken. Hallo voorbeeld toepassing knipperen Hallo GPIO #13 op barod geleid om twee seconden.

Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina][troubleshooting-page].

## <a name="what-you-will-learn"></a>Wat u leert
* Hoe toodeploy en Voer Hallo voorbeeldtoepassing op het mededelingenbord Arduino.

## <a name="what-you-need"></a>Wat u nodig hebt
U moet hebben voltooid Hallo volgende bewerkingen:

* [Uw apparaat configureren][configure-your-device]
* [Hallo-hulpprogramma's ophalen][get-the-tools]

## <a name="open-hello-sample-application"></a>Open Hallo-voorbeeldtoepassing
tooopen hello voorbeeldtoepassing, als volgt te werk:

1. Hallo voorbeeld opslagplaats vanuit GitHub door het uitvoeren van de volgende opdracht Hallo klonen:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-feather-m0-getting-started.git
   ```
2. Hallo-voorbeeldtoepassing openen in Visual Studio Code door het uitvoeren van de volgende opdrachten Hallo:

   ```bash
   cd iot-hub-c-feather-m0-getting-started
   cd Lesson1
   code .
   ```

   ![Structuur van de opslagplaats][repo-structure]

Hallo `app.ino` bestand in Hallo `app` submap is Hallo sleutel bronbestand die Hallo code toocontrol Hallo LED bevat.

### <a name="install-application-dependencies"></a>Afhankelijkheden voor toepassingen installeren
Hallo-bibliotheken en andere modules die u nodig hebt voor de voorbeeldtoepassing Hallo door het uitvoeren van de volgende opdracht Hallo installeren:

```bash
npm install
```

## <a name="configure-hello-device-connection"></a>Hallo apparaatverbinding configureren
tooconfigure Hallo apparaatverbinding, als volgt te werk:

1. Seriële poort Hallo Hallo-apparaat met Hallo apparaat detectie cli verkrijgen:

   ```bash
   devdisco list --usb
   ```

   U moet een uitvoer die vergelijkbaar toohello volgende wordt weergegeven en het vinden van de Hallo usb COM-poort voor deze kaart Arduino: ![detectie van netwerkapparaten][device-discovery]

2. Open Hallo bestand `config.json` in les map Hallo en toe te voegen waarde Hallo Hallo COM-poortnummer gevonden:

   ```json
   {
       "device_port" : "COM1"
   }
   ```
   ![Config.JSON][config-json]
   > [!NOTE]
   > Voor Hallo COM-poort op Windows-platform, heeft het Hallo-indeling van `COM1, COM2, ...`. Op Mac OS of Ubuntu en deze begint met `/dev/`.

## <a name="deploy-and-run-hello-sample-application"></a>Implementeren en uitvoeren van de voorbeeldtoepassing Hallo
### <a name="install-hello-required-tools-for-your-arduino-board"></a>Hallo vereist hulpprogramma's voor uw kaart Arduino installeren

Installeer hello Azure IoT Hub SDK voor uw kaart Arduino Hallo na de opdracht uitgevoerd:

```bash
gulp install-tools
```

Deze taak kan duren voordat een toocomplete lange tijd, afhankelijk van uw netwerkverbinding.

> [!NOTE]
> Sluit Hallo Arduino IDE-exemplaar wordt uitgevoerd bij het uitvoeren van taken gulp: `install-tools`, `run`.

### <a name="deploy-and-run-hello-sample-app"></a>Implementeren en Hallo voorbeeld-app uitvoeren
Implementeren en uitvoeren van de voorbeeldtoepassing Hallo door het uitvoeren van de volgende opdracht Hallo:

```bash
gulp run

# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

### <a name="verify-hello-app-works"></a>Controleer of de app werkt het Hallo
Als er geen Hallo LED knippert, raadpleegt u Hallo [probleemoplossingsgids] [ troubleshooting-page] voor toocommon oplossingen voor problemen.

![LED knippert][led-blinking]

## <a name="summary"></a>Samenvatting
U hebt geïnstalleerd Hallo vereist extra toowork met het mededelingenbord Arduino en een voorbeeld toepassing tooyour Arduino mededelingenbord tooblink Hallo LED geïmplementeerd. U kunt nu maken, implementeren, en voer een ander voorbeeld van een toepassing die uw Arduino mededelingenbord tooAzure IoT Hub toosend verbinding maakt en berichten ontvangen.

## <a name="next-steps"></a>Volgende stappen
[Hello Azure-hulpprogramma's ophalen][get-the-azure-tools]

<!-- Images and links -->

[troubleshooting-page]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-blink-arduino-mac.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[led-blinking]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md