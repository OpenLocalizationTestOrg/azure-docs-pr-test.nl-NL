---
title: aaaConnect een frambozen Pi tooAzure IoT Suite met echte sensoren met behulp van Node.js | Microsoft Docs
description: Gebruik Microsoft Azure IoT Starter Kit Hallo voor Hallo frambozen Pi 3 en Azure IoT Suite. Node.js tooconnect uw oplossing voor externe controle frambozen Pi toohello gebruiken, verzenden van telemetrie van sensoren toohello cloud en toomethods aangeroepen vanuit het dashboard van de oplossing Hallo reageren.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 7ffb4a7a8c04b424a1f29170f4739d89f39a2429
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-send-telemetry-from-a-real-sensor-using-nodejs"></a>Verbinding maken met uw oplossing voor externe controle frambozen Pi 3 toohello en verzend telemetrie vanuit een echte sensor met behulp van Node.js

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

Deze zelfstudie leert u hoe toouse hello Microsoft Azure IoT Starter Kit voor frambozen Pi 3 toodevelop temperatuur en vochtigheid lezer die kan communiceren met de Hallo cloud. Hallo-zelfstudie wordt gebruikt:

- Raspbian OS Node.js programmeertaal Hallo en hello van Microsoft Azure IoT SDK voor Node.js tooimplement een voorbeeld-apparaat.
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

### <a name="install-nodejs"></a>Node.js installeren

Installeer Node.js op uw Raspberry Pi. Hallo IoT SDK voor Node.js vereist versie 0.11.5 van Node.js of hoger. Hallo volgende stappen ziet u hoe tooinstall Node.js v6.10.2 op uw Pi frambozen:

1. Hallo opdracht tooupdate na uw frambozen-Pi gebruiken:

    ```sh
    sudo apt-get update
    ```

1. Hallo opdracht toodownload hello Node.js binaire bestanden tooyour frambozen Pi volgende gebruiken:

    ```sh
    wget https://nodejs.org/dist/v6.10.2/node-v6.10.2-linux-armv7l.tar.gz
    ```

1. Gebruik Hallo opdracht tooinstall Hallo binaire bestanden te volgen:

    ```sh
    sudo tar -C /usr/local --strip-components 1 -xzf node-v6.10.2-linux-armv7l.tar.gz
    ```

1. Gebruik Hallo volgende opdracht tooverify die u hebt de Node.js-v6.10.2 is geïnstalleerd:

    ```sh
    node --version
    ```

### <a name="clone-hello-repositories"></a>Hallo-opslagplaatsen klonen

Als u dit nog niet hebt gedaan, vereist kloon Hallo opslagplaatsen door te voeren Hallo opdrachten op uw Pi volgen:

```sh
cd ~
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git`
```

### <a name="update-hello-device-connection-string"></a>Verbindingsreeks Hallo-apparaat bijwerken

Open Hallo voorbeeld-bronbestand in Hallo **nano** editor met behulp van de volgende opdracht Hallo:

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

Hallo regel zoeken:

```javascript
var connectionString = 'HostName=[Your IoT hub name].azure-devices.net;DeviceId=[Your device id];SharedAccessKey=[Your device key]';
```

Hallo tijdelijke aanduiding voor waarden vervangt door Hallo-apparaat en IoT Hub informatie u gemaakt en opgeslagen op Hallo begin van deze zelfstudie. Sla de wijzigingen (**Ctrl-O**, **Enter**) en sluit de editor af hello (**Ctrl X**).

## <a name="run-hello-sample"></a>Hallo-voorbeeld uitvoeren

Voer Hallo deze opdrachten tooinstall Hallo vereiste pakketten voor Hallo-voorbeeld:

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic
npm install
```

U kunt nu Hallo voorbeeld programma uitvoeren op Hallo frambozen Pi. Voer Hallo-opdracht:

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/basic/remote_monitoring.js
```

Hallo is volgende voorbeelduitvoer een voorbeeld van uitvoer van Hallo die u achter de opdrachtprompt Hallo op Hallo frambozen Pi zien:

![De uitvoer van de app Raspberry Pi][img-raspberry-output]

Druk op **Ctrl-C** tooexit Hallo programma op elk gewenst moment.

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry](../../includes/iot-suite-raspberry-pi-kit-view-telemetry.md)]

## <a name="next-steps"></a>Volgende stappen

Ga naar Hallo [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) voor meer voorbeelden en documentatie over Azure IoT.

[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-basic/app-output.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
