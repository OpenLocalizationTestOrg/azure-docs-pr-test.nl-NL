---
title: 'SensorTag apparaat & Azure IoT Gateway - les 3: voorbeeld-app uitvoeren | Microsoft Docs'
description: Voer een voorbeeldtoepassing uitschakelen gegevens ontvangt uit SensorTag uitschakelen en uw IoT-hub.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: uitschakelen app, de app controleren sensor, gegevensverzameling sensor, gegevens van sensoren sensorgegevens in de cloud
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
ms.openlocfilehash: f6fa158dbe1d48be7d493efa6217e1e0a759d2f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="configure-and-run-a-ble-sample-application"></a>Configureren en uitvoeren van een voorbeeldtoepassing uitschakelen

## <a name="what-you-will-do"></a>Wat u doet

- Kloon de opslagplaats voorbeeld. 
- De verbinding tussen de SensorTag en Intel NUC instellen. 
- De Azure CLI gebruiken om uw IoT-hub en SensorTag-informatie voor een voorbeeldtoepassing uitschakelen (Bluetooth lage energie). Configureren en uitvoeren van de voorbeeldtoepassing uitschakelen. 

Als u problemen hebt, moet u uitkijken voor oplossingen op de [probleemoplossing pagina](iot-hub-gateway-kit-c-troubleshooting.md).

## <a name="what-you-will-learn"></a>Wat u leert

In dit artikel leert u het:

- Informatie over het configureren en uitvoeren van de voorbeeldtoepassing uitschakelen.

## <a name="what-you-need"></a>Wat u nodig hebt

U moet hebt voltooid

- [Het maken van een IoT-hub en SensorTag registreren](iot-hub-gateway-kit-c-lesson2-register-device.md)

## <a name="clone-the-sample-repository-to-the-host-computer"></a>Kloon de opslagplaats voorbeeld met de hostcomputer

De voorbeeld-opslagplaats klonen, moet u deze stappen volgen op de hostcomputer:

1. Open een opdrachtpromptvenster in Windows of een terminal in Mac OS of Ubuntu.
2. Voer de volgende opdrachten uit:

   ```bash
   git clone https://github.com/Azure-samples/iot-hub-c-intel-nuc-gateway-getting-started
   cd iot-hub-c-intel-nuc-gateway-getting-started
   ```

## <a name="set-up-the-connectivity-between-sensortag-and-intel-nuc"></a>De verbinding tussen de SensorTag en Intel NUC instellen

Volg deze stappen op de host voordat u de connectiviteit kunt instellen:

1. Het configuratiebestand initialiseren met de volgende opdrachten:

   ```bash
   cd Lesson3
   npm install
   gulp init
   ```

2. Open `config-gateway.json` in Visual Studio Code met de volgende opdracht:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-gateway.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-gateway.json
   ```

3. Zoek de volgende regel code en vervang `[device hostname or IP address]` met de naam voor IP-adres of de hostnaam van Intel NUC.
   ![schermopname van configuratie-gateway](media/iot-hub-gateway-kit-lessons/lesson3/config_gateway.png)

4. Help-hulpprogramma's installeren op Intel NUC met de volgende opdracht:

   ```bash
   gulp install-tools
   ```

5. Schakel SensorTag door op de knop power als in de volgende afbeelding en de groene LED moet knipperen.

   ![Sensor Tag inschakelen](media/iot-hub-gateway-kit-lessons/lesson3/turn on_off sensortag.jpg)

6. Scannen SensorTag-apparaten met de volgende opdrachten:

   ```bash
   gulp discover-sensortag
   ```

7. Test de connectiviteit tussen de SensorTag en Intel NUC met de volgende opdracht:

   ```bash
   gulp test-connectivity --mac {mac address}
   ```

   Vervang `{mac address}` met de MAC-adres dat u hebt verkregen in de vorige stap.

## <a name="get-the-connection-string-of-sensortag"></a>De verbindingsreeks van SensorTag ophalen

Als u de verbindingsreeks voor Azure IoT hub van SensorTag, voer de volgende opdracht op de hostcomputer:

```bash
az iot device show-connection-string --hub-name {IoT hub name} --device-id mydevice --resource-group iot-gateway
```

`{IoT hub name}`is de naam van de IoT-hub die u hebt gebruikt. Iot-gateway gebruiken als de waarde van `{resource group name}` en mydevice gebruiken als de waarde van `{device id}` als u de waarde in les 2 is niet gewijzigd.

## <a name="configure-the-ble-sample-application"></a>Configureren van de voorbeeldtoepassing uitschakelen

Als u wilt configureren en uitvoeren van de voorbeeldtoepassing uitschakelen, moet u deze stappen volgen op de hostcomputer:

1. Open `config-sensortag.json` in Visual Studio Code met de volgende opdracht:

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-sensortag.json
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-sensortag.json
   ```

   ![schermopname van configuratie sensortag](media/iot-hub-gateway-kit-lessons/lesson3/config_sensortag.png)

2. Controleer de volgende vervangingen in de code:
   - Vervang `[IoT hub name]` met de naam van de IoT-hub die u hebt gebruikt.
   - Vervang `[IoT device connection string]` met de verbindingsreeks van SensorTag die u hebt verkregen.
   - Vervang `[device_mac_address]` met het MAC-adres van de SensorTag die u hebt verkregen.

3. Voer de voorbeeldtoepassing uitschakelen.

   Voor het uitvoeren van de voorbeeldtoepassing uitschakelen, moet u deze stappen volgen op de hostcomputer:

   1. SensorTag inschakelen.

   2. Implementeren en uitvoeren van de voorbeeldtoepassing uitschakelen op Intel NUC met de volgende opdracht:
   
      ```bash
      gulp run
      ```

## <a name="verify-that-the-ble-sample-application-works"></a>Controleer of de voorbeeldtoepassing uitschakelen werkt

U ziet nu de volgende uitvoer:

![De toepassing voorbeelduitvoer uitschakelen](media/iot-hub-gateway-kit-lessons/lesson3/BLE_running.png)

De voorbeeldtoepassing houdt temperatuur gegevens worden verzameld en verzonden naar uw IoT-hub. De voorbeeldtoepassing wordt automatisch beëindigd na het verzenden van 40 seconden.

## <a name="summary"></a>Samenvatting

U hebt is de verbinding tussen de SensorTag en Intel NUC instellen en uitvoeren van een voorbeeldtoepassing uitschakelen die worden verzameld en gegevens van SensorTag naar uw IoT-hub verzendt. U kunt meer informatie over het controleren of uw IoT-hub heeft de gegevens worden ontvangen.

## <a name="next-steps"></a>Volgende stappen
[Berichten van de IoT-hub lezen](iot-hub-gateway-kit-c-lesson3-read-messages-from-hub.md)