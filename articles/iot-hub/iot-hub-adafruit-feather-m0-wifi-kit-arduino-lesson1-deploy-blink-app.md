---
title: 'Arduino verbinden met Azure IoT - les 1: app implementeren | Microsoft Docs'
description: Klonen van de voorbeeldtoepassing Arduino vanuit GitHub, en voer gulp voor het implementeren van deze toepassing naar uw Adafruit Doezelaar M0 Wi-Fi. Deze voorbeeldtoepassing knippert de GPIO
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
ms.openlocfilehash: 4431808ac6182d194e841c087c8f89f1a12b1911
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a>De Blink-toepassing maken en implementeren
## <a name="what-you-will-do"></a>Wat u doet
Klonen van de voorbeeldtoepassing Arduino vanuit GitHub en het hulpprogramma gulp gebruiken voor het implementeren van de voorbeeldtoepassing op het mededelingenbord Adafruit Doezelaar M0 Wi-Fi Arduino. De voorbeeld-toepassing knipperen de GPIO #13 op barod geleid om twee seconden.

Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina][troubleshooting-page].

## <a name="what-you-will-learn"></a>Wat u leert
* Informatie over het implementeren en uitvoeren van de voorbeeldtoepassing op het mededelingenbord Arduino.

## <a name="what-you-need"></a>Wat u nodig hebt
U moet hebt voltooid de volgende bewerkingen:

* [Uw apparaat configureren][configure-your-device]
* [Download de hulpprogramma 's][get-the-tools]

## <a name="open-the-sample-application"></a>Open de voorbeeldtoepassing
U opent de voorbeeldtoepassing door de volgende stappen uit:

1. Kloon de opslagplaats voorbeeld vanuit GitHub met de volgende opdracht:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-feather-m0-getting-started.git
   ```
2. De voorbeeldtoepassing openen in Visual Studio Code met de volgende opdrachten:

   ```bash
   cd iot-hub-c-feather-m0-getting-started
   cd Lesson1
   code .
   ```

   ![Structuur van de opslagplaats][repo-structure]

De `app.ino` bestand de `app` submap is het belangrijkste bronbestand dat de code voor het besturingselement de LED bevat.

### <a name="install-application-dependencies"></a>Afhankelijkheden voor toepassingen installeren
Installeer de bibliotheken en andere modules die u nodig hebt voor de voorbeeldtoepassing met de volgende opdracht uit te voeren:

```bash
npm install
```

## <a name="configure-the-device-connection"></a>De apparaatverbinding configureren
Volg deze stappen voor het configureren van de apparaatverbinding:

1. De seriële poort van het apparaat met de apparaat-detectie cli verkrijgen:

   ```bash
   devdisco list --usb
   ```

   U moet een uitvoer die vergelijkbaar is met het volgende weergegeven en de usb-COM-poort vinden voor uw kaart Arduino: ![detectie van netwerkapparaten][device-discovery]

2. Open het bestand `config.json` in de map les en voeg de waarde van de COM-poortnummer gevonden:

   ```json
   {
       "device_port" : "COM1"
   }
   ```
   ![Config.JSON][config-json]
   > [!NOTE]
   > Voor de COM-poort op Windows-platform, heeft de indeling van `COM1, COM2, ...`. Op Mac OS of Ubuntu en deze begint met `/dev/`.

## <a name="deploy-and-run-the-sample-application"></a>Implementeren en uitvoeren van de voorbeeldtoepassing
### <a name="install-the-required-tools-for-your-arduino-board"></a>De vereiste hulpprogramma's voor uw kaart Arduino installeren

Installeer de Azure IoT Hub SDK voor uw kaart Arduino met de volgende opdracht:

```bash
gulp install-tools
```

Deze taak kan lang duren om uit te voeren, afhankelijk van uw netwerkverbinding.

> [!NOTE]
> Sluit de Arduino IDE exemplaar dat wordt uitgevoerd bij het uitvoeren van taken gulp: `install-tools`, `run`.

### <a name="deploy-and-run-the-sample-app"></a>Implementeren en uitvoeren van de voorbeeld-app
Implementeren en uitvoeren van de voorbeeldtoepassing met de volgende opdracht:

```bash
gulp run

# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

### <a name="verify-the-app-works"></a>Controleer of de app werkt
Als u niet de LED knippert ziet, raadpleegt u de [probleemoplossingsgids] [ troubleshooting-page] voor oplossingen voor bekende problemen.

![LED knippert][led-blinking]

## <a name="summary"></a>Samenvatting
U hebt geïnstalleerd, de vereiste hulpmiddelen voor het werken met het mededelingenbord Arduino en een voorbeeld van toepassing op het mededelingenbord Arduino knipperen de LED geïmplementeerd. U kunt nu maken, implementeren en uitvoeren van een ander voorbeeld van een toepassing die het mededelingenbord Arduino verbindt met Azure IoT Hub berichten te verzenden en ontvangen.

## <a name="next-steps"></a>Volgende stappen
[Download de Azure-hulpprogramma 's][get-the-azure-tools]

<!-- Images and links -->

[troubleshooting-page]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-blink-arduino-mac.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[led-blinking]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md