---
title: een tooAzure frambozen Pi aaaConnect IoT-Suite met behulp van Node.js toosupport firmware-updates | Microsoft Docs
description: Gebruik Microsoft Azure IoT Starter Kit Hallo voor Hallo frambozen Pi 3 en Azure IoT Suite. Gebruik van Node.js tooconnect uw oplossing voor externe controle frambozen Pi toohello, verzenden van telemetrie van sensoren toohello cloud en voert u een externe firmware-update.
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
ms.openlocfilehash: 43bd3f16ee3d292cd9cffa8bfe7d4ca721e5c39c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-raspberry-pi-3-toohello-remote-monitoring-solution-and-enable-remote-firmware-updates-using-nodejs"></a>Verbinding maken met uw oplossing voor externe controle frambozen Pi 3 toohello en inschakelen van externe firmware-updates met behulp van Node.js

[!INCLUDE [iot-suite-raspberry-pi-kit-selector](../../includes/iot-suite-raspberry-pi-kit-selector.md)]

Deze zelfstudie leert u hoe toouse Microsoft Azure IoT Starter Kit Hallo voor frambozen Pi 3:

* Ontwikkel een temperatuur en vochtigheid lezer die met de Hallo cloud communiceren kan.
* Inschakelen en het uitvoeren van een externe firmware-update tooupdate Hallo-clienttoepassing op Hallo frambozen Pi.

Hallo-zelfstudie wordt gebruikt:

- Raspbian OS Node.js programmeertaal Hallo en hello van Microsoft Azure IoT SDK voor Node.js tooimplement een voorbeeld-apparaat.
- Hallo IoT Suite remote monitoring vooraf geconfigureerde oplossing als Hallo cloud-gebaseerde back-end.

## <a name="overview"></a>Overzicht

In deze zelfstudie maakt uitvoeren u Hallo stappen:

- Implementeer een exemplaar van Hallo externe controle vooraf geconfigureerde oplossing tooyour Azure-abonnement. Deze stap implementeert automatisch en meerdere Azure-services configureert.
- Stel uw apparaat en sensoren toocommunicate met uw computer en het Hallo oplossing voor externe controle.
- Hallo voorbeeld apparaat code tooconnect toohello oplossing voor externe controle bijwerken en verzenden van telemetrie die u op Hallo oplossing dashboard weergeven kunt.
- Hallo voorbeeld apparaat code tooupdate Hallo-clienttoepassing gebruiken.

[!INCLUDE [iot-suite-raspberry-pi-kit-prerequisites](../../includes/iot-suite-raspberry-pi-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Hallo externe controle van de bepalingen van de oplossing voor een verzameling Azure-services in uw Azure-abonnement. Hallo implementatie duidt op een echte enterprise-architectuur. tooavoid onnodige Azure-verbruik kosten, verwijderen van uw exemplaar van Hallo vooraf geconfigureerde oplossing op azureiotsuite.com wanneer u klaar bent met het. Als u moet de vooraf geconfigureerde oplossing opnieuw hello, u kunt gemakkelijk het opnieuw maken. Zie voor meer informatie over het verminderen van verbruik tijdens het Hallo voor externe controle van de oplossing wordt uitgevoerd, [configureren van Azure IoT Suite vooraf geconfigureerde oplossingen voor demonstratiedoeleinden][lnk-demo-config].

[!INCLUDE [iot-suite-raspberry-pi-kit-view-solution](../../includes/iot-suite-raspberry-pi-kit-view-solution.md)]

[!INCLUDE [iot-suite-raspberry-pi-kit-prepare-pi](../../includes/iot-suite-raspberry-pi-kit-prepare-pi.md)]

## <a name="download-and-configure-hello-sample"></a>Downloaden en configureren van Hallo-voorbeeld

U kunt nu downloaden en Hallo-bewaking externe clienttoepassing configureren op uw frambozen Pi.

### <a name="install-nodejs"></a>Node.js installeren

Als u dit nog niet hebt gedaan, installeert u Node.js op uw frambozen Pi. Hallo IoT SDK voor Node.js vereist versie 0.11.5 van Node.js of hoger. Hallo volgende stappen ziet u hoe tooinstall Node.js v6.10.2 op uw Pi frambozen:

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
git clone --recursive https://github.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit.git
```

### <a name="update-hello-device-connection-string"></a>Verbindingsreeks Hallo-apparaat bijwerken

Open Hallo voorbeeldconfiguratiebestand in Hallo **nano** editor met behulp van de volgende opdracht Hallo:

```sh
nano ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/config/deviceinfo
```

Hallo tijdelijke aanduiding voor waarden vervangt door Hallo apparaat-id en IoT Hub informatie u gemaakt en opgeslagen op Hallo begin van deze zelfstudie.

Wanneer u klaar bent, ziet er als volgt Hallo Hallo inhoud van Hallo deviceinfo bestand:

```conf
yourdeviceid
HostName=youriothubname.azure-devices.net;DeviceId=yourdeviceid;SharedAccessKey=yourdevicekey
```

Sla de wijzigingen (**Ctrl-O**, **Enter**) en sluit de editor af hello (**Ctrl X**).

## <a name="run-hello-sample"></a>Hallo-voorbeeld uitvoeren

Voer Hallo deze opdrachten tooinstall Hallo vereiste pakketten voor Hallo-voorbeeld:

```sh
cd ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advance/1.0
npm install
```

U kunt nu Hallo voorbeeld programma uitvoeren op Hallo frambozen Pi. Voer Hallo-opdracht:

```sh
sudo node ~/iot-remote-monitoring-node-raspberrypi-getstartedkit/advanced/1.0/remote_monitoring.js
```

Hallo is volgende voorbeelduitvoer een voorbeeld van uitvoer van Hallo die u achter de opdrachtprompt Hallo op Hallo frambozen Pi zien:

![De uitvoer van de app Raspberry Pi][img-raspberry-output]

Druk op **Ctrl-C** tooexit Hallo programma op elk gewenst moment.

[!INCLUDE [iot-suite-raspberry-pi-kit-view-telemetry-advanced](../../includes/iot-suite-raspberry-pi-kit-view-telemetry-advanced.md)]

1. Klik in het dashboard van de oplossing hello, **apparaten** toovisit hello **apparaten** pagina. Selecteer uw Pi frambozen in Hallo **lijst met apparaten**. Kies vervolgens **methoden**:

    ![Lijst met apparaten in het dashboard][img-list-devices]

1. Op Hallo **methode Invoke** pagina **InitiateFirmwareUpdate** in Hallo **methode** vervolgkeuzelijst.

1. In Hallo **FWPackageURI** veld **https://raw.githubusercontent.com/Azure-Samples/iot-remote-monitoring-node-raspberrypi-getstartedkit/master/advanced/2.0/raspberry.js**. Dit bestand bevat Hallo-implementatie van versie 2.0 van Hallo firmware.

1. Kies **InvokeMethod**. Hallo-app op Hallo frambozen Pi verzendt een dashboard van de bevestiging terug toohello oplossing. Vervolgens wordt de procedure Hallo firmware-update gestart door nieuwe versie van de firmware Hallo Hallo te downloaden:

    ![Overzicht van de methode weergeven][img-method-history]

## <a name="observe-hello-firmware-update-process"></a>Hallo firmware updateproces observeren

U kunt Hallo firmware updateproces zien terwijl deze wordt uitgevoerd op Hallo apparaat en gerapporteerd door het bekijken van Hallo eigenschappen in het dashboard van de oplossing Hallo:

1. U kunt Hallo voortgang in van het updateproces Hallo op Hallo frambozen Pi bekijken:

    ![Voortgang van bijwerken weergeven][img-update-progress]

    > [!NOTE]
    > Hallo-app voor externe controle opnieuw is opgestart achtergrond bij Hallo-update is voltooid. Gebruik de opdracht Hallo `ps -ef` tooverify wordt uitgevoerd. Als u tooterminate Hallo proces wilt, gebruikt u Hallo `kill` opdracht met Hallo proces-id.

1. U kunt Hallo status van de firmware-update hello, weergeven, zoals gemeld door het Hallo-apparaat in de oplossingsportal Hallo. Hallo volgende schermafbeelding ziet Hallo status en de duur van elke fase van het updateproces Hallo en nieuwe firmwareversie Hallo:

    ![De status van de taak weergeven][img-job-status]

    Als u back-toohello dashboard navigeert, kunt u controleren Hallo apparaat verzendt nog steeds telemetrie Hallo firmware-update te volgen.

> [!WARNING]
> Als u Hallo oplossing uitgevoerd in uw Azure-account voor externe controle laat, wordt u gefactureerd voor Hallo keer die wordt uitgevoerd. Zie voor meer informatie over het verminderen van verbruik tijdens het Hallo voor externe controle van de oplossing wordt uitgevoerd, [configureren van Azure IoT Suite vooraf geconfigureerde oplossingen voor demonstratiedoeleinden][lnk-demo-config]. Hallo vooraf geconfigureerde oplossing uit uw Azure-account verwijderen wanneer u klaar bent met het gebruik van maken.

## <a name="next-steps"></a>Volgende stappen

Ga naar Hallo [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) voor meer voorbeelden en documentatie over Azure IoT.


[img-raspberry-output]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/app-output.png
[img-update-progress]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/updateprogress.png
[img-job-status]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/jobstatus.png
[img-list-devices]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/listdevices.png
[img-method-history]: ./media/iot-suite-raspberry-pi-kit-node-get-started-advanced/methodhistory.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
