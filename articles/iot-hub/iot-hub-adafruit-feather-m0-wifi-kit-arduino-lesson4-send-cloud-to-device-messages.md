---
title: 'Connect Arduino (C) tooAzure IoT - les 4: Cloud-naar-apparaat | Microsoft Docs'
description: Een voorbeeld van een toepassing wordt uitgevoerd op Adafruit Doezelaar M0 Wi-Fi- en monitors binnenkomende berichten uit uw IoT-hub. Een nieuwe gulp taak verzendt berichten tooAdafruit Doezelaar M0 Wi-Fi uit uw IoT hub tooblink Hallo LED.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: arduino besturingselement geleid vanaf web arduino besturingselement geleid via het web
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: a0bf53fb-29fb-485f-ba4a-6c715057b1a2
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: dcddd61ff684f49436103675938d719cb227c409
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a>Uitvoeren van een toepassing voorbeeld tooreceive cloud-naar-apparaat-berichten
In dit artikel kunt u een voorbeeld van toepassing op het mededelingenbord Adafruit Doezelaar M0 Wi-Fi Arduino implementeren.

Hallo-voorbeeldtoepassing controleert binnenkomende berichten van uw IoT-hub. U ook uitvoeren een gulp taak op uw computer toosend berichten tooyour Arduino mededelingenbord van uw IoT-hub. Wanneer de voorbeeldtoepassing Hallo Hallo-berichten ontvangt, knippert het Hallo LED. Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina][troubleshooting].

## <a name="what-you-will-do"></a>Wat u doet
* Sluit Hallo voorbeeld toepassing tooyour iothub.
* Implementeren en uitvoeren van de voorbeeldtoepassing Hallo.
* Berichten verzenden van uw IoT hub tooyour Arduino mededelingenbord tooblink Hallo LED.

## <a name="what-you-will-learn"></a>Wat u leert
In dit artikel leert u het:
* Hoe toomonitor binnenkomende berichten uit uw IoT-hub.
* Hoe toosend cloud-naar-apparaat-berichten uit uw IoT hub tooyour Arduino het mededelingenbord.

## <a name="what-you-need"></a>Wat u nodig hebt
* Het mededelingenbord Arduino instellen voor gebruik. hoe tooset van het mededelingenbord Arduino zien toolearn [configureren van uw apparaat][configure-your-device].
* Een IoT-hub die wordt gemaakt in uw Azure-abonnement. toolearn hoe toocreate uw IoT-hub Zie [maken van uw Azure-IoT-Hub][create-your-azure-iot-hub].

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a>Verbinding maken met de Hallo voorbeeld toepassing tooyour IoT-hub

1. Zorg ervoor dat u in Hallo opslagplaats map `iot-hub-c-feather-m0-getting-started`.

   Hallo-voorbeeldtoepassing openen in Visual Studio Code door het uitvoeren van de volgende opdrachten Hallo:

   ```bash
   cd Lesson4
   code .
   ```

   Kennisgeving Hallo `app.ino` bestand in Hallo `app` submap. Hallo `app.ino` bestand is Hallo sleutel bronbestand die Hallo code toomonitor binnenkomende berichten uit IoT-hub Hallo bevat. Hallo `blinkLED` functie Hallo LED knippert.

   ![Structuur van de opslagplaats in Hallo-voorbeeldtoepassing][repo-structure]

2. Seriële poort Hallo Hallo-apparaat met Hallo apparaat detectie cli verkrijgen:

   ```bash
   devdisco list --usb
   ```

   U moet een uitvoer die vergelijkbaar toohello volgende wordt weergegeven en Hallo usb COM-poort voor het mededelingenbord Arduino vinden:

   ![Detectie van netwerkapparaten][device-discovery]

3. Open Hallo bestand `config.json` in Hallo les map en de waarde van de invoer Hallo Hallo COM-poortnummer gevonden:

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![Config.JSON][config-json]

   > [!NOTE]
   > Voor Hallo COM-poort op Windows-platform, heeft het Hallo-indeling van `COM1, COM2, ...`. Op Mac OS of Ubuntu wordt gestart met `/dev/`.

4. Hallo-configuratiebestand door het uitvoeren van de volgende opdrachten Hallo initialiseren:

   ```bash
   # For Windows command prompt
   npm install
   gulp init
   gulp install-tools
   ```

5. Zorg Hallo vervangingen in Hallo na `config-arduino.json` bestand:

   Als u de stappen in Hallo voltooid [een Azure-functie-app en storage-account maken] [ create-an-azure-function-app-and-storage-account] op deze computer, alle Hallo-configuraties worden overgenomen, zodat u kunt Hallo stap toohello taak voor het implementeren van overslaan en Hallo-voorbeeldtoepassing wordt uitgevoerd. Als u de stappen in Hallo voltooid [een Azure-functie-app en storage-account maken] [ create-an-azure-function-app-and-storage-account] op een andere computer, moet u tooreplace Hallo tijdelijke aanduidingen in Hallo `config-arduino.json` bestand. Hallo `config-arduino.json` bestand bevindt zich in de submap Hallo van de basismap.

   ![Inhoud van Hallo config arduino.json bestand][config-arduino-json]

   * Vervang **[Wi-Fi-SSID]** met uw Wi-Fi-SSID die toohello Internet verbonden.
   * Vervang **[Wi-Fi-wachtwoord]** met het Wi-Fi-wachtwoord. Hallo tekenreeks verwijderen als uw Wi-Fi geen wachtwoord vereist.
   * Vervang **[apparaat-verbindingsreeks IoT]** met Hallo apparaat verbindingsreeks die u door het uitvoeren van Hallo `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` opdracht.
   * Vervang **[IoT hub verbindingsreeks]** Hello verbindingsreeks van het IoT-hub die u door het uitvoeren van Hallo `az iot hub show-connection-string --name {my hub name}` opdracht.

## <a name="deploy-and-run-hello-sample-application"></a>Implementeren en uitvoeren van de voorbeeldtoepassing Hallo
Implementeren en uitvoeren van de voorbeeldtoepassing Hallo op het mededelingenbord Arduino door het uitvoeren van de volgende opdrachten Hallo:

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

Hallo gulp opdracht implementeert Hallo voorbeeld toepassing tooyour Arduino mededelingenbord. Vervolgens het Hallo toepassing uitvoert op het mededelingenbord Arduino en een afzonderlijke taak op de host computer toosend 20 knipperen berichten tooyour Arduino mededelingenbord van uw IoT-hub.

Na het Hallo-voorbeeldtoepassing wordt uitgevoerd, start het luisteren toomessages uit uw IoT-hub. Ondertussen verzendt Hallo gulp taak aantal 'knipperen' e-mailberichten van uw IoT hub tooyour Arduino mededelingenbord. Voor elk bericht knipperen die Hallo mededelingenbord ontvangt, de voorbeeldtoepassing Hallo Hallo roept `blinkLED` functie tooblink Hallo LED.

U ziet Hallo LED elke twee seconden knipperen zoals Hallo gulp taak 20 berichten uit uw IoT hub tooyour Arduino mededelingenbord verzendt. Hallo laatste is een een 'stop'-bericht dat wordt gestopt Hallo-toepassing wordt uitgevoerd.

![Voorbeeld van een toepassing met de opdracht gulp en berichten knipperen][sample-application]

## <a name="summary"></a>Samenvatting
U hebt berichten uit uw IoT hub tooyour Arduino mededelingenbord tooblink Hallo LED verzonden. de volgende taak Hallo is optioneel: Hallo in- en uitschakelen gedrag van Hallo LED wijzigen.

## <a name="next-steps"></a>Volgende stappen
[Hallo in- en uitschakelen gedrag van Hallo LED wijzigen][change-the-on-and-off-led-behavior]


<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/repo_structure_arduino.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[create-an-azure-function-app-and-storage-account]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/config-arduino.png
[sample-application]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_blink_arduino.png
[change-the-on-and-off-led-behavior]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-change-led-behavior.md