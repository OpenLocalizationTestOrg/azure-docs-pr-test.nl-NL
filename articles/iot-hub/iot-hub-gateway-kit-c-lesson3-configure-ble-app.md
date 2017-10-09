---
title: 'SensorTag apparaat & Azure IoT Gateway - les 3: voorbeeld-app uitvoeren | Microsoft Docs'
description: Voer een Aanmeldingsprompt toepassing tooreceive voorbeeldgegevens uit SensorTag uitschakelen en uw IoT-hub.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: uitschakelen app, de app controleren sensor, gegevensverzameling sensor, gegevens van sensoren, sensor gegevens toocloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: b33e53a1-1df7-4412-ade1-45185aec5bef
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 4a8acdeadd402ffc82d3b766e1ec03a77ddcebb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-run-a-ble-sample-application"></a>Configureren en uitvoeren van een voorbeeldtoepassing uitschakelen

## <a name="what-you-will-do"></a>Wat u doet

- Kloon Hallo voorbeeld opslagplaats. 
- Hallo-connectiviteit tussen SensorTag en Intel NUC instellen. 
- Gebruik hello Azure CLI tooget uw iothub en SensorTag-informatie voor een voorbeeldtoepassing uitschakelen (Bluetooth lage energie). Configureren en Hallo uitschakelen voorbeeldtoepassing uitvoeren. 

Als u problemen hebt, zoekt u naar oplossingen op Hallo [probleemoplossing pagina](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Wat u leert

In dit artikel leert u het:

- Hoe tooconfigure en Voer Hallo uitschakelen voorbeeldtoepassing.

## <a name="what-you-need"></a>Wat u nodig hebt

U moet hebt voltooid

- [Het maken van een IoT-hub en SensorTag registreren](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="clone-hello-sample-repository-toohello-host-computer"></a>Kloon Hallo voorbeeld opslagplaats toohello hostcomputer

tooclone hello voorbeeld opslagplaats als volgt te werk op de hostcomputer Hallo:

1. Open een opdrachtpromptvenster in Windows of een terminal in Mac OS of Ubuntu.
2. Voer Hallo volgende opdrachten:

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="set-up-hello-connectivity-between-sensortag-and-intel-nuc"></a>Hallo-connectiviteit tussen SensorTag en Intel NUC instellen

tooset hello connectiviteit, als volgt te werk op de hostcomputer Hallo:

1. Hallo-configuratiebestand door het uitvoeren van de volgende opdrachten Hallo initialiseren:

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

2. Open `config-gateway.json` in Visual Studio Code door te voeren Hallo volgende opdracht:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

3. Hallo volgende coderegel zoeken en vervangen `[device hostname or IP address]` met Hallo IP-adres of de hostnaam naam van Intel NUC.
   ![schermopname van configuratie-gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)

4. Help-hulpprogramma's installeren op Intel NUC door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   gulp install-tools
   ```

5. Schakel SensorTag door te drukken Hallo / uit-knop als Hallo volgende afbeelding en Hallo die groene LED moet knipperen.

   ![Sensor Tag inschakelen](media/iot-hub-gateway-kit-lessons/lesson3/turn on_off sensortag.jpg)

6. SensorTag-apparaten door het uitvoeren van de volgende opdrachten Hallo scannen:

   ```bash
   gulp discover-sensortag
   ```

7. Hallo-connectiviteit tussen Hallo SensorTag en Intel NUC testen door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   gulp test-connectivity --mac {mac address}
   ```

   Vervang `{mac address}` Hello MAC-adres dat u hebt verkregen in de vorige stap Hallo.

## <a name="get-hello-connection-string-of-sensortag"></a>De verbindingsreeks Hallo van SensorTag ophalen

tooget hello Azure IoT hub-verbindingsreeks van SensorTag, uitvoeren van de volgende opdracht op de hostcomputer Hallo Hallo:

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

`{IoT hub name}`is Hallo naam IoT-hub die u hebt gebruikt. Iot-gateway gebruiken als de waarde van Hallo `{resource group name}` en mydevice gebruiken als Hallo-waarde van `{device id}` als u Hallo-waarde in les 2 niet wijzigen.

## <a name="configure-hello-ble-sample-application"></a>Hallo uitschakelen voorbeeldtoepassing configureren

tooconfigure en Voer Hallo uitschakelen voorbeeldtoepassing, volg deze stappen op de hostcomputer Hallo:

1. Open `config-sensortag.json` in Visual Studio Code door te voeren Hallo volgende opdracht:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![schermopname van configuratie sensortag](media/iot-hub-gateway-kit-lessons/lesson3/config_sensortag.png)

2. Controleer Hallo vervangingen in Hallo code te volgen:
   - Vervang `[IoT hub name]` met Hallo naam IoT-hub die u hebt gebruikt.
   - Vervang `[IoT device connection string]` met de verbindingsreeks Hallo van SensorTag die u hebt verkregen.
   - Vervang `[device_mac_address]` Hello MAC-adres van Hallo SensorTag die u hebt verkregen.

3. Hallo uitschakelen voorbeeldtoepassing uitvoeren.

   toorun hello voorbeeldtoepassing uitschakelen als volgt te werk op de hostcomputer Hallo:

   1. SensorTag inschakelen.

   2. Implementeren en uitvoeren van de voorbeeldtoepassing voor Hallo uitschakelen op Intel NUC door het uitvoeren van de volgende opdracht Hallo:
   
      ```bash
      gulp run
      ```

## <a name="verify-that-hello-ble-sample-application-works"></a>Controleer of Hallo uitschakelen voorbeeldtoepassing werkt

U ziet nu Hallo volgende uitvoer:

![De toepassing voorbeelduitvoer uitschakelen](media/iot-hub-gateway-kit-lessons/lesson3/BLE_running.png)

Hallo-voorbeeldtoepassing blijft temperatuur gegevens verzamelen en deze tooyour iothub heeft verzonden. Hallo-voorbeeldtoepassing wordt automatisch beëindigd na het verzenden van 40 seconden.

## <a name="summary"></a>Samenvatting

U hebt met succes Hallo connectiviteit tussen SensorTag en Intel NUC instellen en uitvoeren van een voorbeeldtoepassing uitschakelen die worden verzameld en verzonden gegevens uit SensorTag tooyour iothub. U bent klaar toolearn hoe tooverify die uw IoT-hub heeft ontvangen gegevens Hallo.

## <a name="next-steps"></a>Volgende stappen
[Berichten van de IoT-hub lezen](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)