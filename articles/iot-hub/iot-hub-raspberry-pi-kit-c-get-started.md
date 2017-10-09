---
title: aaaRaspberry Pi toocloud (C) - verbinding frambozen Pi tooAzure IoT Hub | Microsoft Docs
description: Meer informatie over hoe toosetup en verbinding maken met frambozen Pi tooAzure IoT Hub voor frambozen Pi toosend gegevens toohello Azure-cloudplatform in deze zelfstudie.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Azure iot raspberry pi raspberry pi iot hub, raspberry pi verzenden gegevens toocloud raspberry pi toocloud
ms.assetid: 68c0e730-1dc8-4e26-ac6b-573b217b302d
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/12/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 05086890458e196d7fdc87a53fcabb9386245d6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-c"></a>Verbinding maken met frambozen Pi tooAzure IoT Hub (C)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

In deze zelfstudie maakt eerst u Hallo basisbeginselen van het werken met frambozen Pi met Raspbian leren. U leert vervolgens hoe uw apparaten toohello cloud in tooseamlessly verbinding maken met behulp van [Azure IoT Hub](iot-hub-what-is-iot-hub.md). Ga voor voorbeelden van Windows 10 IoT-Core, toohello [Windows-ontwikkelaarscentrum](http://www.windowsondevices.com/).

Heb je nog een kit? Probeer [frambozen Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md). Een nieuwe kit kopen of [hier](https://azure.microsoft.com/develop/iot/starter-kits).

## <a name="what-you-do"></a>Wat u doet

* Een iothub maken.
* Een apparaat registreren voor Pi in uw IoT-hub.
* Setup Raspberry Pi.
* Een voorbeeld van toepassing op tooyour iothub-Pi toosend sensor gegevens uitgevoerd.

Verbinding maken frambozen Pi tooan IoT-hub die u maakt. Vervolgens voert u een voorbeeld van toepassing op Pi toocollect temperatuur en vochtigheid gegevens van een sensor BME280. Ten slotte verzendt u Hallo sensor gegevens tooyour iothub.

## <a name="what-you-learn"></a>Wat u leert

* Hoe toocreate een Azure-IoT-hub en het nieuwe apparaat-verbindingsreeks ophalen.
* Hoe tooconnect Pi met een sensor BME280.
* Hoe toocollect sensorgegevens door het uitvoeren van een voorbeeldtoepassing met Pi.
* Hoe toosend sensor gegevens tooyour IoT-hub.

## <a name="what-you-need"></a>Wat u nodig hebt

![Wat u nodig hebt](media/iot-hub-raspberry-pi-kit-c-get-started/0_starter_kit.jpg)

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
   1. [Raspbian Jessie met bureaublad downloaden](https://www.raspberrypi.org/downloads/raspbian/) (Hallo ZIP-bestand).
   1. Pak Hallo Raspbian installatiekopie tooa map op uw computer.
1. Installeer Raspbian toohello microSD-kaart.
   1. [Download en installeer Hallo Etcher SD-kaart brander hulpprogramma](https://etcher.io/).
   1. Voer Etcher en Hallo Raspbian installatiekopie die u hebt opgehaald in stap 1.
   1. Selecteer Hallo microSD-kaart station. Houd er rekening mee dat Etcher mogelijk al hebt geselecteerd Hallo juiste station.
   1. Klik op Flash tooinstall Raspbian toohello microSD-kaart.
   1. Hallo microSD-kaart van uw computer verwijderen wanneer de installatie voltooid is. Het is veilig tooremove hello microSD-kaart rechtstreeks omdat Etcher automatisch uitwerpen of Hallo microSD-kaart is voltooid ontkoppelt.
   1. Hallo microSD-kaart invoegen in Pi.

### <a name="enable-ssh-and-spi"></a>SSH- en SPI inschakelen

1. Sluit Pi toohello monitor, toetsenbord en muis, Pi starten en meld u daarna Raspbian met behulp van `pi` als Hallo-gebruikersnaam en `raspberry` Hallo wachtwoord.
1. Klik op Hallo Raspberry pictogram > **voorkeuren** > **frambozen Pi configuratie**.

   ![Hallo Raspbian voorkeuren menu](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. Op Hallo **Interfaces** tabblad, stelt u **SPI** en **SSH** te**inschakelen**, en klik vervolgens op **OK**. Als u geen fysieke sensoren hebben en sensorgegevens toouse gesimuleerde wilt, moet deze stap is optioneel.

   ![SPI en SSH met Raspberry Pi inschakelen](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
tooenable SSH en SPI u meer verwijzing documenten vindt op [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) en [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).

### <a name="connect-hello-sensor-toopi"></a>Hallo sensor tooPi verbinding

Hallo breadboard en meestal kabels tooconnect een LED en een tooPi BME280 als volgt gebruiken. Als u geen Hallo sensor, [deze sectie overslaan](#connect-pi-to-the-network).

![Hallo frambozen Pi en sensor verbinding](media/iot-hub-raspberry-pi-kit-c-get-started/3_raspberry-pi-sensor-connection.png)

Hallo BME280 sensor kunt temperatuur en vochtigheid gegevens verzamelen. En Hallo LED knippert als er een communicatie tussen apparaten en Hallo cloud. 

Gebruik voor pincodes sensor, Hallo bedrading te volgen:

| Start (Sensor & LED)     | Einde (BMC)            | Kleur van de kabel   |
| -----------------------  | ---------------------- | ------------: |
| LED VDD (Pin 5G)         | GPIO 4 (pincode 7)         | Witte kabel   |
| LED GND (Pin 6G)         | GND (pincode 6)            | Zwarte kabel   |
| VDD (Pin 18F)            | 3, 3v PWR (Pin 17)      | Witte kabel   |
| GND (Pin 20F)            | GND (Pin 20)           | Zwarte kabel   |
| SCK (Pin 21F)            | SPI0 SCLK (Pin 23)     | Oranje-kabel  |
| SDO (Pin 22F)            | SPI0 MISO (Pin 21)     | Gele-kabel  |
| SDI (Pin 23F)            | SPI0 MOSI (Pin 19)     | Groen-kabel   |
| CS (Pin 24F)             | SPI0 CS (pincode 24)       | Blauw-kabel    |

Klik op tooview [frambozen Pi 2 en 3 pincode toewijzingen](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) ter referentie.

Nadat u verbinding hebt gemaakt BME280 tooyour frambozen Pi, moet zoals hieronder installatiekopie.

![Verbonden Pi en BME280](media/iot-hub-raspberry-pi-kit-c-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a>Pi toohello netwerk verbinden

Pi inschakelen met behulp van Hallo micro USB-kabel en Hallo voeding. Gebruik Hallo Ethernet-kabel tooconnect Pi tooyour bekabelde netwerk of volgen Hallo [instructies uit Hallo frambozen Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour draadloos netwerk. Nadat uw Pi met succes verbonden toohello netwerk is, moet u een notitie van Hallo tootake [IP-adres van uw Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).

![Toowired verbonden netwerk](media/iot-hub-raspberry-pi-kit-c-get-started/5_power-on-pi.jpg)


## <a name="run-a-sample-application-on-pi"></a>Een voorbeeld van een toepassing uitvoeren op Pi

### <a name="install-hello-prerequisite-packages"></a>Vereiste hello-pakketten installeren

1. Gebruik een van de volgende clients SSH uit uw host computer tooconnect tooyour frambozen Pi Hallo.
   
   **Windows-gebruikers**
   1. Download en installeer [PuTTY](http://www.putty.org/) voor Windows. 
   1. Kopieer Hallo IP-adres van de sectie Pi in Hallo Host name (of IP-adres) en selecteer SSH als Hallo verbindingstype.
   
   ![PuTTy](media/iot-hub-raspberry-pi-kit-node-get-started/7_putty-windows.png)
   
   **Mac- en Ubuntu-gebruikers**
   
   Hallo ingebouwde SSH-client op Ubuntu- of Mac OS gebruiken. Mogelijk moet u toorun `ssh pi@<ip address of pi>` tooconnect Pi via SSH.
   > [!NOTE] 
   Hallo standaardgebruikersnaam `pi` , en het Hallo-wachtwoord is `raspberry`.

1. Vereiste hello-pakketten voor Hallo Microsoft Azure IoT-apparaat-SDK voor C en Cmake door het uitvoeren van de volgende opdrachten Hallo installeren:

   ```bash
   grep -q -F 'deb http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' /etc/apt/sources.list || sudo sh -c "echo 'deb http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' >> /etc/apt/sources.list"
   grep -q -F 'deb-src http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' /etc/apt/sources.list || sudo sh -c "echo 'deb-src http://ppa.launchpad.net/aziotsdklinux/ppa-azureiot/ubuntu vivid main' >> /etc/apt/sources.list"
   sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys FDA6A393E4C2257F
   sudo apt-get update
   sudo apt-get install -y azure-iot-sdk-c-dev cmake libcurl4-openssl-dev git-core
   git clone git://git.drogon.net/wiringPi
   cd ./wiringPi
   ./build
   ```


### <a name="configure-hello-sample-application"></a>Hallo-voorbeeldtoepassing configureren

1. Hallo-voorbeeldtoepassing door het uitvoeren van de volgende opdracht Hallo klonen:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-raspberrypi-client-app
   ```
1. Open Hallo config-bestand door het uitvoeren van de volgende opdrachten Hallo:

   ```bash
   cd iot-hub-c-raspberrypi-client-app
   nano config.h
   ```

   ![Configuratiebestand](media/iot-hub-raspberry-pi-kit-c-get-started/6_config-file.png)

   Er zijn twee macro's in dit bestand kunt u configurate. Hallo eerst een is `INTERVAL`, definieert een Hallo tijdsinterval (in milliseconden) tussen twee berichten die toocloud verzenden. tweede Hallo `SIMULATED_DATA`, dit is een Booleaanse waarde voor of toouse sensorgegevens gesimuleerd.

   Als u **geen Hallo sensor**stelt hello `SIMULATED_DATA` waarde te`1` toomake Hallo voorbeeld van een toepassing maken en gesimuleerde sensorgegevens gebruiken.

1. Opslaan en sluiten door te drukken besturingselement-O > Enter > Control X.

### <a name="build-and-run-hello-sample-application"></a>Hallo voorbeeldtoepassing bouwen en uitvoeren

1. Hallo-voorbeeldtoepassing bouwen door het uitvoeren van de volgende opdracht Hallo:

   ```bash
   cmake . && make
   ```
   ![Uitvoer bouwen](media/iot-hub-raspberry-pi-kit-c-get-started/7_build-output.png)

1. Hallo-voorbeeldtoepassing uitvoeren door te voeren van Hallo volgende opdracht:

   ```bash
   sudo ./app '<DEVICE CONNECTION STRING>'
   ```

   > [!NOTE] 
   Zorg ervoor dat u kopiëren en plakken Hallo apparaat verbindingsreeks in Hallo tussen enkele aanhalingstekens.


U ziet Hallo volgende resultaat dat wordt weergegeven Hallo sensor gegevens en het Hallo-berichten dat tooyour iothub worden verzonden.

![Output - sensorgegevens uit frambozen Pi tooyour iothub worden verzonden](media/iot-hub-raspberry-pi-kit-c-get-started/8_run-output.png)

## <a name="next-steps"></a>Volgende stappen

U hebt een voorbeeldgegevens toepassing toocollect sensor uitgevoerd en verzend het tooyour IoT-hub. toosee Hallo-berichten dat uw Pi frambozen tooyour IoT-hub of verzenden berichten tooyour frambozen Pi heeft verzonden in een opdrachtregelinterface Zie Hallo [beheren cloud apparaat messaging met iothub explorer zelfstudie](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
