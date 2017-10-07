---
title: aaaUse een IoT gateway tooconnect een apparaat tooAzure IoT Hub | Microsoft Docs
description: Meer informatie over hoe toouse Intel NUC als een IoT gateway tooconnect een SensorTag TI en verzenden sensor gegevens tooAzure IoT-Hub in Hallo cloud.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: IOT gateway verbinding toocloud apparaat maken
ms.assetid: cb851648-018c-4a7e-860f-b62ed3b493a5
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/25/2017
ms.author: xshi
ms.openlocfilehash: 418af34bf29992d46b76ae59ef548744808664c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-iot-gateway-tooconnect-things-toohello-cloud---sensortag-tooazure-iot-hub"></a>Gebruik IoT gateway tooconnect dingen toohello cloud - SensorTag tooAzure IoT-Hub

> [!NOTE]
> Voordat u deze zelfstudie begint, controleert u of u hebt voltooid [Intel NUC als een IoT-gateway instellen](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md). In [Intel NUC als een IoT-gateway instellen](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md), instellen van Hallo Intel NUC apparaat als een IoT-gateway.

## <a name="what-you-will-learn"></a>Wat u leert

U leert hoe toouse een IoT gateway tooconnect een Texas instrumenten SensorTag (CC2650STK) tooAzure IoT Hub. Hallo IoT gateway verzendt temperatuur en vochtigheid gegevens die worden verzameld van Hallo SensorTag tooAzure IoT Hub.

## <a name="what-you-will-do"></a>Wat u doet

- Een iothub maken.
- Een apparaat in Hallo iothub voor Hallo SensorTag registreren.
- Hallo-verbinding tussen Hallo IoT gateway en Hallo SensorTag inschakelen.
- Voer een Aanmeldingsprompt voorbeeld toepassing toosend SensorTag tooyour iothub.

## <a name="what-you-need"></a>Wat u nodig hebt

- Zelfstudie [Intel NUC als een IoT-gateway instellen](iot-hub-gateway-kit-c-lesson1-set-up-nuc.md) voltooid in die u Intel NUC als een IoT-gateway instelt.
- * Een actief Azure-abonnement. Als u een Azure-account geen [maken van een gratis Azure-proefaccount](https://azure.microsoft.com/free/) over een paar minuten.
- Een SSH-client die wordt uitgevoerd op de hostcomputer. PuTTY wordt aanbevolen voor Windows. Linux- en Mac OS al worden geleverd met een SSH-client.
- Hallo IP-adres en Hallo gebruikersnaam en wachtwoord tooaccess Hallo gateway vanuit Hallo SSH-client.
- Een internetverbinding.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

> [!NOTE]
> Hier registreren u dit nieuwe apparaat voor uw SensorTag

## <a name="enable-hello-connection-between-hello-iot-gateway-and-hello-sensortag"></a>Hallo-verbinding tussen Hallo IoT gateway en Hallo SensorTag inschakelen

In deze sectie kunt u Hallo volgende taken uitvoeren:

- Hallo MAC-adres van Hallo SensorTag voor Bluetooth-verbinding niet ophalen.
- Een Bluetooth-verbinding van Hallo IoT gateway toohello SensorTag starten.

### <a name="get-hello-mac-address-of-hello-sensortag-for-bluetooth-connection"></a>Hallo MAC-adres van Hallo SensorTag voor Bluetooth-verbinding ophalen

1. Op de hostcomputer Hallo Hallo SSH-client wordt uitgevoerd en verbinding maken met toohello IoT gateway.
1. De blokkering opheffen Bluetooth Hallo na de opdracht uitgevoerd:

   ```bash
   sudo rfkill unblock bluetooth
   ```

1. Hallo Bluetooth-service starten op Hallo IoT gateway en voert u een Bluetooth-shell tooconfigure Bluetooth door te voeren Hallo volgende opdrachten:

   ```bash
   sudo systemctl start bluetooth
   bluetoothctl
   ```

1. Power op Hallo Bluetooth domeincontroller door te voeren Hallo Hallo Bluetooth-shell-opdracht te volgen:

   ```bash
   power on
   ```

   ![Hallo Bluetooth-controller hebben op Hallo IoT gateway met bluetoothctl inschakelen](./media/iot-hub-iot-gateway-connect-device-to-cloud/8_power-on-bluetooth-controller-at-bluetooth-shell-bluetoothctl.png)

1. Start scannen op in de buurt Bluetooth-apparaten door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   scan on
   ```

   ![In de buurt Bluetooth-apparaten met bluetoothctl scannen](./media/iot-hub-iot-gateway-connect-device-to-cloud/9_start-scan-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

1. Druk op Hallo knop op Hallo SensorTag koppelen. Hallo groen geleid op Hallo SensorTag flitsen.
1. U ziet op Hallo Bluetooth-shell, Hallo die sensortag is gevonden. Noteer Hallo MAC-adres van Hallo SensorTag. In dit voorbeeld Hallo MAC-adres van Hallo SensorTag is `24:71:89:C0:7F:82`.
1. Hallo scan uitschakelen door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   scan off
   ```

   ![In de buurt Bluetooth-apparaten met bluetoothctl scannen stopzetten](./media/iot-hub-iot-gateway-connect-device-to-cloud/10_stop-scanning-nearby-bluetooth-devices-at-bluetooth-shell-bluetoothctl.png)

### <a name="initiate-a-bluetooth-connection-from-hello-iot-gateway-toohello-sensortag"></a>Een Bluetooth-verbinding van Hallo IoT gateway toohello SensorTag starten

1. Verbinding maken met toohello SensorTag door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   connect <MAC address>
   ```

   ![Verbinding maken met toohello SensorTag met bluetoothctl](./media/iot-hub-iot-gateway-connect-device-to-cloud/11_connect-to-sensortag-at-bluetooth-shell-bluetoothctl.png)

1. Hallo SensorTag verbreken en Hallo Bluetooth-shell afsluiten door te voeren Hallo volgende opdrachten:

   ```bash
   disconnect
   exit
   ```

   ![Hallo SensorTag met bluetoothctl verbreken](./media/iot-hub-iot-gateway-connect-device-to-cloud/12_disconnect-from-sensortag-at-bluetooth-shell-bluetoothctl.png)

Hallo-verbinding tussen Hallo SensorTag en Hallo IoT gateway hebt ingeschakeld.

## <a name="run-a-ble-sample-application-toosend-sensortag-data-tooyour-iot-hub"></a>Voer een Aanmeldingsprompt voorbeeld toepassing toosend SensorTag tooyour iothub

Hallo Bluetooth laag energieverbruik (uitschakelen) voorbeeldtoepassing wordt verstrekt door Azure IoT rand. Hallo-voorbeeldtoepassing verzamelt gegevens van verbinding uitschakelen en Hallo gegevens tooyou IoT-hub te verzenden. voorbeeldtoepassing toorun hello, moet u:

1. Hallo-voorbeeldtoepassing configureren.
1. Hallo-voorbeeldtoepassing uitvoeren op Hallo IoT gateway.

### <a name="configure-hello-sample-application"></a>Hallo-voorbeeldtoepassing configureren

1. Map van de voorbeeldtoepassing Hallo toohello gaan door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   cd /usr/share/azureiotgatewaysdk/samples/ble_gateway
   ```

1. Hallo-configuratiebestand openen door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   vi ble_gateway.json
   ```

1. Vul in het configuratiebestand hello, Hallo volgende waarden:

   **IoTHubName**: Hallo-naam van uw IoT-hub.

   **IoTHubSuffix**: IoTHubSuffix ophalen uit de Hallo primaire sleutel van Hallo apparaat verbindingsreeks die u hebt genoteerd omlaag. Zorg dat u primaire sleutel voor Hallo van Hallo apparaat verbindingsreeks ophalen, Hallo geen primaire sleutel van de verbindingsreeks van uw IoT-hub. Hallo primaire sleutel van de verbindingsreeks Hallo-apparaat is Hallo notatie `HostName=IOTHUBNAME.IOTHUBSUFFIX;DeviceId=DEVICEID;SharedAccessKey=SHAREDACCESSKEY`.

   **Transport**: Hallo standaardwaarde is `amqp`. Deze waarde weergegeven Hallo protocol tijdens transpotation. Kan de zijn `http`, `amqp`, of `mqtt`.

   **macAddress**: Hallo MAC-adres van Hallo SensorTag die u hebt genoteerd omlaag.

   **deviceID**: ID van Hallo-apparaat dat u hebt gemaakt in uw IoT-hub.

   **deviceKey**: Hallo primaire sleutel van de verbindingsreeks Hallo-apparaat.

   ![Het configuratiebestand voltooid Hallo Hallo voorbeeldtoepassing uitschakelen](./media/iot-hub-iot-gateway-connect-device-to-cloud/13_edit-config-file-of-ble-sample.png)

1. Druk op `ESC` en het type `:wq` toosave Hallo-bestand.

### <a name="run-hello-sample-application"></a>Hallo-voorbeeldtoepassing uitvoeren

1. Zorg ervoor dat Hallo die sensortag is ingeschakeld.
1. Hallo volgende opdracht uitvoeren:

   ```bash
   ./ble_gateway ble_gateway.json
   ```

## <a name="next-steps"></a>Volgende stappen

[Gebruik IoT gateway voor gegevenstransformatie sensor met Azure IoT rand](iot-hub-gateway-kit-c-use-iot-gateway-for-data-conversion.md)
