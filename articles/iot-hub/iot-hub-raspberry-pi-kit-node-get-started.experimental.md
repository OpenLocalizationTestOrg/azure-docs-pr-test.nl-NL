---
title: aaaRaspberry Pi toocloud (Node.js) - verbinding frambozen Pi tooAzure IoT Hub | Microsoft Docs
description: Verbinding maken met frambozen Pi tooAzure IoT Hub voor frambozen Pi toosend gegevens toohello Azure-cloud.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure iot raspberry pi raspberry pi iot hub, raspberry pi verzenden gegevens toocloud raspberry pi toocloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: b0e14bfa-8e64-440a-a6ec-e507ca0f76ba
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/27/2017
ms.author: xshi
ms.openlocfilehash: 07bc66983c427eab8118be18d91abb25deb03ad3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-nodejs"></a>Verbinding maken met frambozen Pi tooAzure IoT Hub (Node.js)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

In deze zelfstudie maakt eerst u Hallo basisbeginselen van het werken met frambozen Pi met Raspbian leren. U leert vervolgens hoe uw apparaten toohello cloud in tooseamlessly verbinding maken met behulp van [Azure IoT Hub](iot-hub-what-is-iot-hub.md). Ga voor voorbeelden van Windows 10 IoT-Core, toohello [Windows-ontwikkelaarscentrum](http://www.windowsondevices.com/).

Heb je nog een kit? Probeer Hallo [frambozen Pi 3 emulator](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/). Een nieuwe kit kopen of [hier](https://azure.microsoft.com/develop/iot/starter-kits).

## <a name="what-you-do"></a>Wat u doet

* Setup Raspberry Pi.
* Een iothub maken.
* Een apparaat registreren voor Pi in uw IoT-hub.
* Een voorbeeld van toepassing op tooyour iothub-Pi toosend sensor gegevens uitgevoerd.

Verbinding maken frambozen Pi tooan IoT-hub die u maakt. Vervolgens voert u een voorbeeld van toepassing op Pi toocollect temperatuur en vochtigheid gegevens van een sensor BME280. Ten slotte verzendt u Hallo sensor gegevens tooyour iothub.

## <a name="what-you-learn"></a>Wat u leert

* Hoe toocreate een Azure-IoT-hub en het nieuwe apparaat-verbindingsreeks ophalen.
* Hoe tooconnect Pi met een sensor BME280.
* Hoe toocollect sensorgegevens door het uitvoeren van een voorbeeldtoepassing met Pi.
* Hoe toosend sensor gegevens tooyour IoT-hub.

## <a name="what-you-need"></a>Wat u nodig hebt

![Wat u nodig hebt](media/iot-hub-raspberry-pi-kit-node-get-started/0_starter_kit.jpg)

* Hallo frambozen Pi 2 of frambozen Pi 3 mededelingenbord.
* Een actief Azure-abonnement. Als u een Azure-account geen [maken van een gratis Azure-proefaccount](https://azure.microsoft.com/free/) over een paar minuten.
* Een monitor, een USB-toetsenbord en muis die tooPi verbinding.
* Een Mac of een PC die Windows of Linux wordt uitgevoerd.
* Een internetverbinding.
* Een 16 GB of hoger microSD-kaart.
* Een USB-SD adapter of microSD-kaart tooburn Hallo besturingssysteeminstallatiekopie op Hallo microSD-kaart.
* Een 5-v 2 amp voeding met Hallo 6 mond micro USB-kabel.

Hallo volgende items zijn optioneel:

* Een samengesteld Adafruit BME280 temperatuur, druk en vochtigheid sensor.
* Een breadboard.
* 6 F/M meestal bedrading.
* Een gedempt 10 mm LED.

  > [!NOTE] 
  Deze items zijn optioneel, omdat Hallo code voorbeeld ondersteuning sensorgegevens gesimuleerd.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a>Raspberry Pi instellen

### <a name="install-hello-raspbian-operating-system-for-pi"></a>Hallo Raspbian besturingssysteem voor Pi installeren

Hallo microSD-kaart voor de installatie van Hallo Raspbian afbeelding voorbereiden.

1. Raspbian downloaden.
   1. [Download Raspbian Jessie met Pixel](https://www.raspberrypi.org/downloads/raspbian/) (Hallo ZIP-bestand).
   1. Pak Hallo Raspbian installatiekopie tooa map op uw computer.
1. Installeer Raspbian toohello microSD-kaart.
   1. [Download en installeer Hallo Etcher SD-kaart brander hulpprogramma](https://etcher.io/).
   1. Voer Etcher en Hallo Raspbian installatiekopie die u hebt opgehaald in stap 1.
   1. Selecteer Hallo microSD-kaart station. Houd er rekening mee dat Etcher mogelijk al hebt geselecteerd Hallo juiste station.
   1. Klik op Flash tooinstall Raspbian toohello microSD-kaart.
   1. Hallo microSD-kaart van uw computer verwijderen wanneer de installatie voltooid is. Het is veilig tooremove hello microSD-kaart rechtstreeks omdat Etcher automatisch uitwerpen of Hallo microSD-kaart is voltooid ontkoppelt.
   1. Hallo microSD-kaart invoegen in Pi.

### <a name="enable-ssh-and-i2c"></a>SSH- en I2C inschakelen

1. Sluit Pi toohello monitor, toetsenbord en muis, Pi starten en meld u daarna Raspbian met behulp van `pi` als Hallo-gebruikersnaam en `raspberry` Hallo wachtwoord.
1. Klik op Hallo Raspberry pictogram > **voorkeuren** > **frambozen Pi configuratie**.

   ![Hallo Raspbian voorkeuren menu](media/iot-hub-raspberry-pi-kit-node-get-started/1_raspbian-preferences-menu.png)

1. Op Hallo **Interfaces** tabblad, stelt u **I2C** en **SSH** te**inschakelen**, en klik vervolgens op **OK**. Als u geen fysieke sensoren hebben en sensorgegevens toouse gesimuleerde wilt, moet deze stap is optioneel.

   ![I2C en SSH met Raspberry Pi inschakelen](media/iot-hub-raspberry-pi-kit-node-get-started/2_enable-i2c-ssh-on-raspberry-pi.png)

> [!NOTE] 
tooenable SSH en I2C u meer verwijzing documenten vindt op [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) en [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).

### <a name="connect-hello-sensor-toopi"></a>Hallo sensor tooPi verbinding

Hallo breadboard en meestal kabels tooconnect een LED en een tooPi BME280 als volgt gebruiken. Als u geen Hallo sensor hebt, kunt u deze sectie overslaan.

![Hallo frambozen Pi en sensor verbinding](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

Hallo BME280 sensor kunt temperatuur en vochtigheid gegevens verzamelen. En Hallo LED knippert als er een communicatie tussen apparaten en Hallo cloud. 

Gebruik voor pincodes sensor, Hallo bedrading te volgen:

| Start (Sensor & LED)     | Einde (BMC)            | Kleur van de kabel   |
| -----------------------  | ---------------------- | ------------: |
| VDD (Pin 5G)             | 3, 3v PWR (pincode 1)       | Witte kabel   |
| GND (Pin 7G)             | GND (pincode 6)            | Bruine-kabel   |
| SCK (Pin 8G)             | I2C1 SDA (pincode 3)       | Oranje-kabel  |
| SDI (Pin 10G)            | I2C1 SCL (pincode 5)       | Rode-kabel     |
| LED VDD (Pin 18F)        | GPIO 24 (Pin 18)       | Witte kabel   |
| LED GND (Pin 17F)        | GND (Pin 20)           | Zwarte kabel   |

Klik op tooview [frambozen Pi 2 en 3 pincode toewijzingen](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) ter referentie.

Nadat u verbinding hebt gemaakt BME280 tooyour frambozen Pi, moet zoals hieronder installatiekopie.

![Verbonden Pi en BME280](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a>Pi toohello netwerk verbinden

Pi inschakelen met behulp van Hallo micro USB-kabel en Hallo voeding. Gebruik Hallo Ethernet-kabel tooconnect Pi tooyour bekabelde netwerk of volgen Hallo [instructies uit Hallo frambozen Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour draadloos netwerk. Nadat uw Pi met succes verbonden toohello netwerk is, moet u een notitie van Hallo tootake [IP-adres van uw Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).

![Toowired verbonden netwerk](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> Zorg ervoor dat Pi verbonden toohello netwerk als de computer is. Bijvoorbeeld, als uw computer verbonden tooa draadloze netwerk is wanneer Pi verbonden tooa standaardnetwerk is, ziet u mogelijk niet Hallo IP-adres in Hallo devdisco uitvoer.

## <a name="run-a-sample-application-on-pi"></a>Een voorbeeld van een toepassing uitvoeren op Pi

### <a name="clone-sample-application-and-install-hello-prerequisite-packages"></a>Klonen van de voorbeeldtoepassing en vereiste hello-pakketten installeren

1. Gebruik een van de volgende clients SSH uit uw host computer tooconnect tooyour frambozen Pi Hallo.
    - [PuTTY](http://www.putty.org/) voor Windows. U moet Hallo IP-adres van uw tooconnect Pi via SSH.
    - Hallo ingebouwde SSH-client op Ubuntu- of Mac OS. U moet uitvoeren `ssh pi@<ip address of pi>` tooconnect Pi via SSH.

   > [!NOTE] 
   Hallo standaardgebruikersnaam `pi` , en het Hallo-wachtwoord is `raspberry`.

1. Installeer Node.js en NPM tooyour Pi.
   
   Controleer uw Node.js-versie moet u eerst met de volgende opdracht Hallo. 
   
   ```bash
   node -v
   ```

   Of er is geen Node.js op uw Pi Hallo versie lager is dan 4.x uitvoeren na de opdracht tooinstall Hallo of bijwerken van Node.js.

   ```bash
   curl -sL http://deb.nodesource.com/setup_4.x | sudo -E bash
   sudo apt-get -y install nodejs
   ```

1. Hallo-voorbeeldtoepassing door het uitvoeren van de volgende opdracht Hallo klonen:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-client-app
   ```

1. Installeer alle pakketten met Hallo opdracht te volgen. Omvat Azure IoT-device SDK, BME280 Sensor-bibliotheek en bedrading Pi-bibliotheek.

   ```bash
   cd iot-hub-node-raspberrypi-client-app
   sudo npm install
   ```
   > [!NOTE] 
   Het duurt enkele minuten toofinish dit proces installatie denpening op de netwerkverbinding.

### <a name="configure-hello-sample-application"></a>Hallo-voorbeeldtoepassing configureren

1. Open Hallo config-bestand door het uitvoeren van de volgende opdrachten Hallo:

   ```bash
   nano config.json
   ```

   ![Configuratiebestand](media/iot-hub-raspberry-pi-kit-node-get-started/6_config-file.png)

   Er zijn twee items in dit bestand kunt u configurate. Hallo eerst een is `interval`, definieert een Hallo tijdsinterval tussen twee berichten die toocloud verzenden. tweede Hallo `simulatedData`, dit is een Booleaanse waarde voor of toouse sensorgegevens gesimuleerd.

   Als u **geen Hallo sensor**stelt hello `simulatedData` waarde te`true` toomake Hallo voorbeeld van een toepassing maken en gesimuleerde sensorgegevens gebruiken.

1. Opslaan en sluiten door te drukken besturingselement-O > Enter > Control X.

### <a name="run-hello-sample-application"></a>Hallo-voorbeeldtoepassing uitvoeren

1. Hallo-voorbeeldtoepassing uitvoeren door te voeren van Hallo volgende opdracht:

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   Zorg ervoor dat u kopiëren en plakken Hallo apparaat verbindingsreeks in Hallo tussen enkele aanhalingstekens.


U ziet Hallo volgende resultaat dat wordt weergegeven Hallo sensor gegevens en het Hallo-berichten dat tooyour iothub worden verzonden.

![Output - sensorgegevens uit frambozen Pi tooyour iothub worden verzonden](media/iot-hub-raspberry-pi-kit-node-get-started/8_run-output.png)

## <a name="next-steps"></a>Volgende stappen

U hebt een voorbeeldgegevens toepassing toocollect sensor uitgevoerd en verzend het tooyour IoT-hub.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]