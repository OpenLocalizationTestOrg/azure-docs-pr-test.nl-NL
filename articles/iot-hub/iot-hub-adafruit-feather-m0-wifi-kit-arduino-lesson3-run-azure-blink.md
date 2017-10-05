---
title: 'Connect Arduino (C) naar Azure IoT - les 3: voorbeeld uitvoeren | Microsoft Docs'
description: Implementeren en uitvoeren van een voorbeeldtoepassing met Adafruit Doezelaar M0 Wi-Fi dat berichten verzendt naar uw IoT-hub en de LED knippert.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: IOT-cloudservice, arduino verzenden van gegevens naar de cloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 92cce319-2b17-4c9b-889d-deac959e3e7c
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 0c17fe74dbd78abca955f7789a1674ed6333367f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a>Voer een voorbeeldtoepassing om apparaat-naar-cloud-berichten te verzenden
## <a name="what-you-will-do"></a>Wat u doet
In dit artikel wordt beschreven hoe u implementeren en uitvoeren van een voorbeeld van toepassing op het mededelingenbord Adafruit Doezelaar M0 Wi-Fi Arduino dat berichten naar uw IoT-hub verzendt.

Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina][troubleshooting].

## <a name="what-you-will-learn"></a>Wat u leert
U leert hoe u met het hulpprogramma gulp implementeren en uitvoeren van de voorbeeldtoepassing Arduino op het mededelingenbord Arduino.

## <a name="what-you-need"></a>Wat u nodig hebt
* Voordat u deze taak moet is voltooid [maken van een Azure-functie-app en een opslagaccount om te verwerken en opslaan van IoT hub berichten][process-and-store-iot-hub-messages].

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Ophalen van uw IoT-hub en apparaat-verbindingsreeksen
De verbindingsreeks van het apparaat wordt gebruikt voor het mededelingenbord Arduino verbinding met uw IoT-hub. De verbindingsreeks van de IoT-hub wordt gebruikt voor het verbinden van uw IoT-hub met de identiteit van het apparaat dat het mededelingenbord Arduino in de IoT-hub vertegenwoordigt.

* Een overzicht van uw IoT-hubs in de resourcegroep met de volgende Azure CLI-opdracht:

```bash
az iot hub list -g iot-sample --query [].name
```

Gebruik `iot-sample` als de waarde van `{resource group name}` als u de waarde niet wijzigen.

* De IoT hub-verbindingsreeks ophalen met de volgende opdracht in de Azure CLI:

```bash
az iot hub show-connection-string --name {my hub name}
```

`{my hub name}`is de naam die u hebt opgegeven wanneer u uw IoT-hub gemaakt en het mededelingenbord Arduino geregistreerd.

* De apparaat-verbindingsreeks ophalen met de volgende opdracht:

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id mym0wifi
```

Gebruik `mym0wifi` als de waarde van `{device id}` als u de waarde niet wijzigen.
## <a name="configure-the-device-connection"></a>De apparaatverbinding configureren
Volg deze stappen voor het configureren van de apparaatverbinding:

1. De seriële poort van het apparaat met de apparaat-detectie cli verkrijgen:

   ```bash
   devdisco list --usb
   ```

   U moet een uitvoer die vergelijkbaar is met het volgende weergegeven en de usb COM-poort voor het mededelingenbord Arduino vinden:

   ![Detectie van netwerkapparaten][device-discovery]

2. Open het bestand `config.json` in de map les en voeg de waarde van de COM-poortnummer gevonden:

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![Config.JSON][config-json]

   > [!NOTE]
   > Voor de COM-poort op Windows-platform, heeft de indeling van `COM1, COM2, ...`. Op Mac OS of Ubuntu en deze begint met `/dev/`.

3. Het configuratiebestand initialiseren met de volgende opdrachten:

   ```bash
   npm install
   gulp init
   gulp install-tools
   ```
4. Open het configuratiebestand van het apparaat `config-arduino.json` in Visual Studio Code met de volgende opdracht:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```

   ![config arduino.json][config-arduino-json]

5. Controleer de volgende vervangingen in de `config-arduino.json` bestand:

   * Vervang **[Wi-Fi-SSID]** met uw Wi-Fi-SSID die is verbonden met Internet.
   * Vervang **[Wi-Fi-wachtwoord]** met het Wi-Fi-wachtwoord. Verwijder de tekenreeks als uw Wi-Fi geen wachtwoord vereist.
   * Vervang **[apparaat-verbindingsreeks IoT]** met de `device connection string` u hebt verkregen.
   * Vervang **[IoT hub verbindingsreeks]** met de `iot hub connection string` u hebt verkregen.

   > [!NOTE]
   > U hoeft niet `azure_storage_connection_string` in dit artikel. Houd deze zo is.

## <a name="deploy-and-run-the-sample-application"></a>Implementeren en uitvoeren van de voorbeeldtoepassing
Implementeren en uitvoeren van de voorbeeldtoepassing op het mededelingenbord Arduino met de volgende opdracht:

```bash
gulp run
# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

> [!NOTE]
> De standaard gulp taak wordt uitgevoerd `install-tools` en `run` taken sequentieel worden verwerkt. Wanneer u [de knipperen app hebt geïmplementeerd][deployed-the-blink-app], u deze taken afzonderlijk uitgevoerd.

## <a name="verify-that-the-sample-application-works"></a>Controleer of de voorbeeldtoepassing werkt
U ziet de GPIO #0 ingebouwde LED knippert die per twee seconden. Telkens wanneer de LED knippert, wordt de voorbeeldtoepassing verzendt een bericht naar uw IoT-hub en verifieert dat wordt het bericht is verzonden naar uw IoT-hub. Bovendien wordt elk bericht ontvangen door de IoT-hub in het consolevenster. De voorbeeldtoepassing wordt automatisch beëindigd na 20 berichten verzenden.

![Voorbeeld van een toepassing met verzonden en ontvangen van berichten][sample-application-with-sent-and-received-messages]

## <a name="summary"></a>Samenvatting
U hebt geïmplementeerd en de nieuwe knipperen voorbeeldtoepassing uitvoeren op het mededelingenbord Arduino apparaat-naar-cloud-berichten verzenden naar uw IoT-hub. U nu bewaken uw berichten zoals ze zijn geschreven naar het opslagaccount.

## <a name="next-steps"></a>Volgende stappen
[Alleen berichten permanent in Azure Storage][read-messages-persisted-in-azure-storage]
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/config-arduino.png
[deployed-the-blink-app]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_run_arduino.png
[read-messages-persisted-in-azure-storage]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-read-table-storage.md