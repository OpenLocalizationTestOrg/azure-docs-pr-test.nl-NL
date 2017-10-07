---
title: 'Connect Arduino (C) tooAzure IoT - les 3: voorbeeld uitvoeren | Microsoft Docs'
description: Implementeren en uitvoeren van een steekproef toepassing tooAdafruit Doezelaar M0 Wi-Fi dat berichten tooyour iothub verzendt en Hallo LED knippert.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: IOT-cloudservice, arduino verzenden gegevens toocloud
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
ms.openlocfilehash: ddca015a3655f8a1a9de2a00e718ec0d28a5affb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a>Uitvoeren van een toepassing voorbeeld toosend apparaat-naar-cloud-berichten
## <a name="what-you-will-do"></a>Wat u doet
Dit artikel wordt beschreven hoe toodeploy en een voorbeeld van een toepassing wordt uitgevoerd op uw Adafruit Doezelaar M0 Wi-Fi Arduino board verzendt berichten tooyour iothub.

Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina][troubleshooting].

## <a name="what-you-will-learn"></a>Wat u leert
U leert hoe toouse hello gulp hulpprogramma toodeploy en Hallo Arduino voorbeeldtoepassing uitvoeren op het mededelingenbord Arduino.

## <a name="what-you-need"></a>Wat u nodig hebt
* Voordat u deze taak moet is voltooid [maken van een Azure-functie-app en een storage account tooprocess en store iothub berichten][process-and-store-iot-hub-messages].

## <a name="get-your-iot-hub-and-device-connection-strings"></a>Ophalen van uw IoT-hub en apparaat-verbindingsreeksen
apparaat-verbindingsreeks Hallo gebruikte tooconnect is uw Arduino mededelingenbord tooyour IoT-hub. Hallo IoT hub-verbindingsreeks is gebruikte tooconnect uw IoT hub toohello apparaat-id die uw Arduino vertegenwoordigt board in Hallo IoT-hub.

* Een overzicht van uw IoT-hubs in uw resourcegroep door het uitvoeren van hello Azure CLI-opdracht te volgen:

```bash
az iot hub list -g iot-sample --query [].name
```

Gebruik `iot-sample` als Hallo-waarde van `{resource group name}` als u Hallo-waarde niet wijzigt.

* Hallo IoT hub-verbindingsreeks ophalen door het uitvoeren van hello Azure CLI-opdracht te volgen:

```bash
az iot hub show-connection-string --name {my hub name}
```

`{my hub name}`Hallo-naam die u hebt opgegeven wanneer u uw IoT-hub gemaakt en het mededelingenbord Arduino geregistreerd is.

* Hallo apparaat-verbindingsreeks ophalen door het uitvoeren van de volgende opdracht Hallo:

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id mym0wifi
```

Gebruik `mym0wifi` als Hallo-waarde van `{device id}` als u Hallo-waarde niet wijzigt.
## <a name="configure-hello-device-connection"></a>Hallo apparaatverbinding configureren
tooconfigure Hallo apparaatverbinding, als volgt te werk:

1. Seriële poort Hallo Hallo-apparaat met Hallo apparaat detectie cli verkrijgen:

   ```bash
   devdisco list --usb
   ```

   U moet een uitvoer die vergelijkbaar toohello volgende wordt weergegeven en Hallo usb COM-poort voor het mededelingenbord Arduino vinden:

   ![Detectie van netwerkapparaten][device-discovery]

2. Open Hallo bestand `config.json` in les map Hallo en toe te voegen waarde Hallo Hallo COM-poortnummer gevonden:

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![Config.JSON][config-json]

   > [!NOTE]
   > Voor Hallo COM-poort op Windows-platform, heeft het Hallo-indeling van `COM1, COM2, ...`. Op Mac OS of Ubuntu en deze begint met `/dev/`.

3. Hallo-configuratiebestand door het uitvoeren van de volgende opdrachten Hallo initialiseren:

   ```bash
   npm install
   gulp init
   gulp install-tools
   ```
4. Open Hallo apparaat configuratiebestand `config-arduino.json` in Visual Studio Code door te voeren Hallo volgende opdracht:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```

   ![config arduino.json][config-arduino-json]

5. Zorg Hallo vervangingen in Hallo na `config-arduino.json` bestand:

   * Vervang **[Wi-Fi-SSID]** met uw Wi-Fi-SSID die toohello Internet verbonden.
   * Vervang **[Wi-Fi-wachtwoord]** met het Wi-Fi-wachtwoord. Hallo tekenreeks verwijderen als uw Wi-Fi geen wachtwoord vereist.
   * Vervang **[apparaat-verbindingsreeks IoT]** Hello `device connection string` u hebt verkregen.
   * Vervang **[IoT hub verbindingsreeks]** Hello `iot hub connection string` u hebt verkregen.

   > [!NOTE]
   > U hoeft niet `azure_storage_connection_string` in dit artikel. Houd deze zo is.

## <a name="deploy-and-run-hello-sample-application"></a>Implementeren en uitvoeren van de voorbeeldtoepassing Hallo
Implementeren en uitvoeren van de voorbeeldtoepassing Hallo op het mededelingenbord Arduino door het uitvoeren van de volgende opdracht Hallo:

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

> [!NOTE]
> Hallo standaard gulp taak wordt uitgevoerd `install-tools` en `run` taken sequentieel worden verwerkt. Wanneer u [Hallo knipperen app geïmplementeerd][deployed-the-blink-app], u deze taken afzonderlijk uitgevoerd.

## <a name="verify-that-hello-sample-application-works"></a>Controleer of de voorbeeldtoepassing Hallo werkt
U ziet Hallo GPIO #0 ingebouwde LED knippert elke twee seconden. Telkens wanneer Hallo LED knippert, wordt de voorbeeldtoepassing Hallo verzendt een bericht tooyour IoT-hub en verifieert dat het Hallo-bericht is verzonden tooyour IoT-hub. Bovendien wordt elk bericht ontvangen door de IoT-hub Hallo afgedrukt in het consolevenster Hallo. Hallo-voorbeeldtoepassing wordt automatisch beëindigd na 20 berichten verzenden.

![Voorbeeld van een toepassing met verzonden en ontvangen van berichten][sample-application-with-sent-and-received-messages]

## <a name="summary"></a>Samenvatting
U hebt geïmplementeerd en nieuwe knipperen Hallo-voorbeeldtoepassing uitvoeren op uw Arduino mededelingenbord toosend apparaat-naar-cloudberichten tooyour iothub. U nu bewaken uw berichten zoals ze zijn toohello storage-account geschreven.

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