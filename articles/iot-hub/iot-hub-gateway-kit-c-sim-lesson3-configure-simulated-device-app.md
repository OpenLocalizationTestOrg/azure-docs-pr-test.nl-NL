---
title: 'Gesimuleerde apparaat & Azure IoT Gateway - les 3: voorbeeld-app uitvoeren | Microsoft Docs'
description: Voer een gesimuleerd apparaat voorbeeld-app temperatuur om gegevens te verzenden naar uw IoT-hub
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: gegevens in de cloud
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
ms.openlocfilehash: 7df2d730c38a9f715e0fd57b4d436724a5727760
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-run-a-simulated-device-sample-app"></a>Configureren en uitvoeren van een gesimuleerd apparaat voorbeeld-app

## <a name="what-you-will-do"></a>Wat u doet

- Kloon de opslagplaats voorbeeld.
- De Azure CLI gebruiken om uw IoT-hub en logische apparaatgegevens voor de voorbeeldtoepassing gesimuleerde apparaat. Configureren en uitvoeren van de voorbeeldtoepassing gesimuleerde apparaat.

Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-gateway-kit-c-sim-troubleshooting.md).

## <a name="what-you-will-learn"></a>Wat u leert

In dit artikel leert u het:

- Informatie over het configureren en uitvoeren van de voorbeeldtoepassing gesimuleerde apparaat.

## <a name="what-you-need"></a>Wat u nodig hebt

U moet hebt voltooid

- [Een IoT-hub maken en uw apparaat registreren](iot-hub-gateway-kit-c-sim-lesson2-register-device.md)

## <a name="clone-the-sample-repository-to-the-host-computer"></a>Kloon de opslagplaats voorbeeld met de hostcomputer

De voorbeeld-opslagplaats klonen, moet u deze stappen volgen op de hostcomputer:

1. Open een opdrachtprompt in Windows of een terminal in Mac OS of Ubuntu.
2. Voer de volgende opdrachten uit:

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="configure-the-simulated-device-and-your-nuc"></a>Het gesimuleerde apparaat en uw NUC configureren

1. Open het configuratiebestand `config.json` in Visual Studio Code met de volgende opdracht:

   ```bash
   code config.json
   ```

2. Vervang `"has_sensortag": true` met`"has_sensortag": false`

   ![Configuratie hebt u niet een TI SensorTag-apparaat](media/iot-hub-gateway-kit-lessons/lesson3/config_no_sensortag.png)

3. Het configuratiebestand initialiseren met de volgende opdrachten:

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

4. Open `config-gateway.json` in Visual Studio Code met de volgende opdracht:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

5. Zoek de volgende regel code en vervang `[device hostname or IP address]` met IP-adres of de host-naam van de Intel NUC.
   ![schermopname van configuratie-gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)

## <a name="get-the-connection-string-of-your-iot-hub-logical-device"></a>De verbindingsreeks van uw IoT hub logisch apparaat ophalen

Als u de verbindingsreeks voor Azure IoT hub van het logische apparaat, voer de volgende opdracht op de hostcomputer:

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

`{IoT hub name}`is de naam van de IoT-hub die u hebt gebruikt. Iot-gateway gebruiken als de waarde van `{resource group name}` en mydevice gebruiken als de waarde van `{device id}` als u de waarde in les 2 is niet gewijzigd.

## <a name="configure-the-simulated-device-cloud-upload-sample-application"></a>Configureren van de voorbeeldtoepassing gesimuleerd apparaat cloud uploaden

Configureren en uitvoeren van de voorbeeldtoepassing gesimuleerd apparaat cloud uploaden, als volgt te werk op de hostcomputer:

1. Open `config-sensortag.json` in Visual Studio Code met de volgende opdracht:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![schermopname van configuratie sensortag](media/iot-hub-gateway-kit-lessons/lesson3/config_simulated_device.png)

2. Controleer de volgende vervangingen in de code:
   - Vervang `[IoT hub name]` met de naam van de IoT-hub.
   - Vervang `[IoT device connection string]` met de verbindingsreeks van uw IoT hub logisch apparaat.

3. Voer de toepassing uit.

   Implementeren en uitvoeren van de toepassing met de volgende opdracht:

   ```bash
   gulp run
   ```

## <a name="verify-the-sample-application-works"></a>Controleer of de toepassing voorbeeld werkt

U ziet nu de volgende uitvoer:

![de toepassing voorbeelduitvoer gesimuleerd apparaat](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_simudev.png)

De toepassing verzendt temperatuur gegevens naar uw IoT-hub 40 seconden duurt.

## <a name="summary"></a>Samenvatting

U hebt is geconfigureerd en uitvoeren van de voorbeeldtoepassing van gesimuleerd apparaat cloud uploaden die gegevens naar uw IoT-hub met gesimuleerde apparaat verzendt.

## <a name="next-steps"></a>Volgende stappen
[Berichten van de IoT-hub lezen](iot-hub-gateway-kit-c-sim-lesson3-read-messages-from-hub.md)