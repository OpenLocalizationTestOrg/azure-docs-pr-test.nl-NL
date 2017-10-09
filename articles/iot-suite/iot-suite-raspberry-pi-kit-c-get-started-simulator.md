---
title: aaaConnect een frambozen Pi tooAzure IoT Suite met C met gesimuleerde telemetrie | Microsoft Docs
description: Gebruik Microsoft Azure IoT Starter Kit Hallo voor Hallo frambozen Pi 3 en Azure IoT Suite. Gebruik C tooconnect uw oplossing voor externe controle frambozen Pi toohello, gesimuleerde telemetrie toohello cloud verzenden en toomethods aangeroepen vanuit het dashboard van de oplossing Hallo reageren.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 3c4fa43b381385d1a7896cada34aa3aa0b8e5fb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-simulated-telemetry-using-c"></a>Verbinding maken met uw oplossing voor externe controle frambozen Pi 3 toohello en gesimuleerde telemetrie met C verzenden

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

Deze zelfstudie leert u hoe toouse Hallo frambozen Pi 3 toosimulate temperatuur en vochtigheid gegevens toosend toohello cloud. Hallo-zelfstudie wordt gebruikt:

- Raspbian OS Hallo C programmeertaal en Hallo Microsoft Azure IoT SDK voor C tooimplement een voorbeeld-apparaat.
- Hallo IoT Suite remote monitoring vooraf geconfigureerde oplossing als Hallo cloud-gebaseerde back-end.

[!INCLUDE [iot-suite-raspberry-pi-kit-overview-simulator](../../includes/iot-suite-raspberry-pi-kit-overview-simulator.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Hallo externe controle van de bepalingen van de oplossing voor een verzameling Azure-services in uw Azure-abonnement. Hallo implementatie duidt op een echte enterprise-architectuur. tooavoid onnodige Azure-verbruik kosten, verwijderen van uw exemplaar van Hallo vooraf geconfigureerde oplossing op azureiotsuite.com wanneer u klaar bent met het. Als u moet de vooraf geconfigureerde oplossing opnieuw hello, u kunt gemakkelijk het opnieuw maken. Zie voor meer informatie over het verminderen van verbruik tijdens het Hallo voor externe controle van de oplossing wordt uitgevoerd, [configureren van Azure IoT Suite vooraf geconfigureerde oplossingen voor demonstratiedoeleinden][lnk-demo-config].

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi-simulator](../../includes/iot-suite-raspberry-pi-kit-prepare-pi-simulator.md)]

## <a name="download-and-configure-hello-sample"></a>Downloaden en configureren van Hallo-voorbeeld

U kunt nu downloaden en Hallo-bewaking externe clienttoepassing configureren op uw frambozen Pi.

### <a name="clone-hello-repositories"></a>Hallo-opslagplaatsen klonen

Als u dit nog niet hebt gedaan, vereist kloon Hallo opslagplaatsen door te voeren Hallo opdrachten in een terminal op uw Pi volgen:

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a>Verbindingsreeks Hallo-apparaat bijwerken

Open Hallo voorbeeld-bronbestand in Hallo **nano** editor met behulp van de volgende opdracht Hallo:

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/remote_monitoring/remote_monitoring.c
```

Zoek Hallo volgende regels:

```c
static const char* deviceId = "[Device Id]";
static const char* connectionString = "HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]";
```

Hallo tijdelijke aanduiding voor waarden vervangt door Hallo-apparaat en IoT Hub informatie u gemaakt en opgeslagen op Hallo begin van deze zelfstudie. Sla de wijzigingen (**Ctrl-O**, **Enter**) en sluit de editor af hello (**Ctrl X**).

## <a name="build-hello-sample"></a>Hallo voorbeeld bouwen

Vereiste hello-pakketten voor Hallo Microsoft Azure IoT-apparaat-SDK voor C door het uitvoeren van de volgende opdrachten in een terminal op Hallo frambozen Pi Hallo installeren:

```sh
sudo apt-get update
sudo apt-get install g++ make cmake git libcurl4-openssl-dev libssl-dev uuid-dev
```

U kunt nu Voorbeeldoplossing Hallo bijgewerkt op Hallo frambozen Pi bouwen:

```sh
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/simulator/build.sh
```

U kunt nu Hallo voorbeeld programma uitvoeren op Hallo frambozen Pi. Voer Hallo-opdracht:

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

Hallo is volgende voorbeelduitvoer een voorbeeld van uitvoer van Hallo die u achter de opdrachtprompt Hallo op Hallo frambozen Pi zien:

![De uitvoer van de app Raspberry Pi][img-raspberry-output]

Druk op **Ctrl-C** tooexit Hallo programma op elk gewenst moment.

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-simulator](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-simulator.md)]

## <a name="next-steps"></a>Volgende stappen

Ga naar Hallo [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) voor meer voorbeelden en documentatie over Azure IoT.

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-simulator/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
