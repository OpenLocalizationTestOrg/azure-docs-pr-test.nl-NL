---
title: 'Gesimuleerde apparaat & Azure IoT Gateway - les 3: voorbeeld-app uitvoeren | Microsoft Docs'
description: Voer een gesimuleerd apparaat voorbeeld-app toosend temperatuur tooyour iothub
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: gegevens toocloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5d051d99-9749-4150-b3c8-573b0bda9c52
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: bc2c97919e95e4e3977a8b6ac75162bf2b5017be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a>Configureren en uitvoeren van een gesimuleerd apparaat voorbeeld-app

## <a name="what-you-will-do"></a>Wat u doet

- Kloon Hallo voorbeeld opslagplaats.
- Gebruik uw IoT-hub en logische apparaatgegevens hello Azure CLI tooget voor de voorbeeldtoepassing gesimuleerde apparaat. Configureren en uitvoeren van de voorbeeldtoepassing voor Hallo gesimuleerde apparaat.

Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Wat u leert

In dit artikel leert u het:

- Hoe tooconfigure en Voer Hallo gesimuleerd apparaat voorbeeldtoepassing.

## <a name="what-you-need"></a>Wat u nodig hebt

U moet hebt voltooid

- [Een IoT-hub maken en uw apparaat registreren](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a>Kloon Hallo voorbeeld opslagplaats toohello hostcomputer

tooclone hello voorbeeld opslagplaats als volgt te werk op de hostcomputer Hallo:

1. Open een opdrachtprompt in Windows of een terminal in Mac OS of Ubuntu.
2. Voer Hallo volgende opdrachten:

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-hello-simulated-device-and-your-nuc"></a>Hallo gesimuleerde apparaat en uw NUC configureren

1. Open Hallo-configuratiebestand `config.json` in Visual Studio Code door te voeren Hallo volgende opdracht:

   ```bash
   code config.json
   ```

2. Vervang `"has_sensortag": true` met`"has_sensortag": false`

   ![Configuratie hebt u niet een TI SensorTag-apparaat](media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. Hallo-configuratiebestand door het uitvoeren van de volgende opdrachten Hallo initialiseren:

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. Open `config-gateway.json` in Visual Studio Code door te voeren Hallo volgende opdracht:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. Hallo volgende coderegel zoeken en vervangen `[device hostname or IP address]` met IP-adres of de hostnaam naam Hallo Intel NUC.
   ![schermopname van configuratie-gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)

## <a name="get-hello-connection-string-of-your-iot-hub-logical-device"></a>De verbindingsreeks Hallo van uw IoT hub logisch apparaat ophalen

tooget hello Azure IoT hub-verbindingsreeks van het logische apparaat, uitvoeren van de volgende opdracht op de hostcomputer Hallo Hallo:

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

`{IoT hub name}`is Hallo naam IoT-hub die u hebt gebruikt. Iot-gateway gebruiken als de waarde van Hallo `{resource group name}` en mydevice gebruiken als Hallo-waarde van `{device id}` als u Hallo-waarde in les 2 niet wijzigen.

## <a name="configure-hello-simulated-device-cloud-upload-sample-application"></a>Hallo gesimuleerd apparaat cloud uploaden-voorbeeldtoepassing configureren

tooconfigure en Voer Hallo gesimuleerd apparaat cloud voorbeeldtoepassing uploaden, als volgt te werk op de hostcomputer Hallo:

1. Open `config-sensortag.json` in Visual Studio Code door te voeren Hallo volgende opdracht:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![schermopname van configuratie sensortag](media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. Controleer Hallo vervangingen in Hallo code te volgen:
   - Vervang `[IoT hub name]` met naam Hallo IoT-hub.
   - Vervang `[IoT device connection string]` met de verbindingsreeks Hallo van uw IoT hub logisch apparaat.

3. Hallo-toepassing uitvoeren.

   Implementeren en uitvoeren van de toepassing hello door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   gulp run
   ```

## <a name="verify-hello-sample-application-works"></a>Controleren Hallo voorbeeld toepassing werkt

U ziet nu Hallo volgende uitvoer:

![de toepassing voorbeelduitvoer gesimuleerd apparaat](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

Hallo toepassing verzendt temperatuur gegevens tooyour IoT-hub 40 seconden duurt.

## <a name="summary"></a>Samenvatting

U hebt geconfigureerd en Voer Hallo gesimuleerd apparaat cloud uploaden voorbeeldtoepassing die gegevens tooyour iothub met gesimuleerde apparaat verzendt.

## <a name="next-steps"></a>Volgende stappen
[Berichten van de IoT-hub lezen](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)