---
title: aaaConnect een frambozen Pi tooAzure IoT Suite met C met echte sensoren | Microsoft Docs
description: Gebruik Microsoft Azure IoT Starter Kit Hallo voor Hallo frambozen Pi 3 en Azure IoT Suite. Gebruik C tooconnect uw oplossing voor externe controle frambozen Pi toohello, verzenden van telemetrie van sensoren toohello cloud en toomethods aangeroepen vanuit het dashboard van de oplossing Hallo reageren.
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
ms.openlocfilehash: 7dac55ae5fde4c6f8e3ea6a7debf9a6822dc07ee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-c"></a>Verbinding maken met uw oplossing voor externe controle frambozen Pi 3 toohello en verzend telemetrie vanuit een echte sensor met C

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

Deze zelfstudie leert u hoe toouse hello Microsoft Azure IoT Starter Kit voor frambozen Pi 3 toodevelop temperatuur en vochtigheid lezer die kan communiceren met de Hallo cloud. Hallo-zelfstudie wordt gebruikt:

- Raspbian OS Hallo C programmeertaal en Hallo Microsoft Azure IoT SDK voor C tooimplement een voorbeeld-apparaat.
- Hallo IoT Suite remote monitoring vooraf geconfigureerde oplossing als Hallo cloud-gebaseerde back-end.

## <a name="overview"></a>Overzicht

In deze zelfstudie maakt uitvoeren u Hallo stappen:

- Implementeer een exemplaar van Hallo externe controle vooraf geconfigureerde oplossing tooyour Azure-abonnement. Deze stap implementeert automatisch en meerdere Azure-services configureert.
- Stel uw apparaat en sensoren toocommunicate met uw computer en het Hallo oplossing voor externe controle.
- Hallo voorbeeld apparaat code tooconnect toohello oplossing voor externe controle bijwerken en verzenden van telemetrie die u op Hallo oplossing dashboard weergeven kunt.

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Hallo externe controle van de bepalingen van de oplossing voor een verzameling Azure-services in uw Azure-abonnement. Hallo implementatie duidt op een echte enterprise-architectuur. tooavoid onnodige Azure-verbruik kosten, verwijderen van uw exemplaar van Hallo vooraf geconfigureerde oplossing op azureiotsuite.com wanneer u klaar bent met het. Als u moet de vooraf geconfigureerde oplossing opnieuw hello, u kunt gemakkelijk het opnieuw maken. Zie voor meer informatie over het verminderen van verbruik tijdens het Hallo voor externe controle van de oplossing wordt uitgevoerd, [configureren van Azure IoT Suite vooraf geconfigureerde oplossingen voor demonstratiedoeleinden][lnk-demo-config].

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a>Downloaden en configureren van Hallo-voorbeeld

U kunt nu downloaden en Hallo-bewaking externe clienttoepassing configureren op uw frambozen Pi.

### <a name="clone-hello-repositories"></a>Hallo-opslagplaatsen klonen

Als u dit nog niet hebt gedaan, vereist kloon Hallo opslagplaatsen door te voeren Hallo opdrachten in een terminal op uw Pi volgen:

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-c-raspberrypi-getstartedkit.git
git clone --recursive https://github.com/WiringPi/WiringPi.git
```

### <a name="update-hello-device-connection-string"></a>Verbindingsreeks Hallo-apparaat bijwerken

Open Hallo voorbeeld-bronbestand in Hallo **nano** editor met behulp van de volgende opdracht Hallo:

```sh
nano ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/remote_monitoring/remote_monitoring.c
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
chmod +x ~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
~/iot-remote-monitoring-c-raspberrypi-getstartedkit/basic/build.sh
```

U kunt nu Hallo voorbeeld programma uitvoeren op Hallo frambozen Pi. Voer Hallo-opdracht:

```sh
sudo ~/cmake/remote_monitoring/remote_monitoring
```

Hallo is volgende voorbeelduitvoer een voorbeeld van uitvoer van Hallo die u achter de opdrachtprompt Hallo op Hallo frambozen Pi zien:

![De uitvoer van de app Raspberry Pi][img-raspberry-output]

Druk op **Ctrl-C** tooexit Hallo programma op elk gewenst moment.

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a>Volgende stappen

Ga naar Hallo [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) voor meer voorbeelden en documentatie over Azure IoT.

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-c-get-started-basic/appoutput.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
