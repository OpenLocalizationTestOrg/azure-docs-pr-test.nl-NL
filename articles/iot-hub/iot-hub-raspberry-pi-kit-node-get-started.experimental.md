---
title: Raspberry Pi naar cloud (Node.js) - frambozen Pi verbinding maken met Azure IoT Hub | Microsoft Docs
description: Frambozen Pi verbinding met Azure IoT Hub voor frambozen Pi gegevens verzenden naar de Azure-cloud.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure iot raspberry pi, raspberry pi iothub, raspberry pi verzenden gegevens naar de cloud, raspberry pi naar cloud
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
ms.openlocfilehash: 956ed5ab0ed38ddebd978b35eb54bc96567f0d57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="connect-raspberry-pi-to-azure-iot-hub-nodejs"></a>Raspberry Pi verbinden met Azure IoT Hub (Node.js)

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

In deze zelfstudie maakt beginnen u door te leren over het werken met frambozen Pi met Raspbian. Vervolgens leert u hoe u uw apparaten probleemloos verbinding met de cloud via [Azure IoT Hub](iot-hub-what-is-iot-hub.md). Voor voorbeelden van Windows 10 IoT-Core, gaat u naar de [Windows-ontwikkelaarscentrum](http://www.windowsondevices.com/).

Heb je nog een kit? Probeer de [frambozen Pi 3 emulator](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/). Een nieuwe kit kopen of [hier](https://azure.microsoft.com/develop/iot/starter-kits).

## <a name="what-you-do"></a>Wat u doet

* Setup Raspberry Pi.
* Een iothub maken.
* Een apparaat registreren voor Pi in uw IoT-hub.
* Een voorbeeld van een toepassing uitvoeren op Pi sensorgegevens verzenden naar uw IoT-hub.

Verbinding maken met frambozen Pi naar een IoT-hub die u maakt. Vervolgens voert u een voorbeeld van toepassing op Pi temperatuur en vochtigheid om gegevens te verzamelen van een sensor BME280. U kunt ten slotte de sensorgegevens verzendt naar uw IoT-hub.

## <a name="what-you-learn"></a>Wat u leert

* Het maken van een Azure-IoT-hub en het nieuwe apparaat-verbindingsreeks ophalen.
* Klik hier voor meer informatie over het Pi verbinden met een sensor BME280.
* Klik hier voor meer informatie over het verzamelen van sensorgegevens door het uitvoeren van een voorbeeldtoepassing met Pi.
* Hoe sensorgegevens verzendt naar uw IoT-hub.

## <a name="what-you-need"></a>Wat u nodig hebt

![Wat u nodig hebt](media/iot-hub-raspberry-pi-kit-node-get-started/0_starter_kit.jpg)

* De frambozen Pi 2 of frambozen Pi 3-kaart.
* Een actief Azure-abonnement. Als u een Azure-account geen [maken van een gratis Azure-proefaccount](https://azure.microsoft.com/free/) over een paar minuten.
* Een monitor, een USB-toetsenbord en muis die verbinding met Pi maken.
* Een Mac of een PC die Windows of Linux wordt uitgevoerd.
* Een internetverbinding.
* Een 16 GB of hoger microSD-kaart.
* Een USB-SD adapter of microSD-kaart branden van de installatiekopie van het besturingssysteem op de microSD-kaart.
* Een 5-v 2 amp voeding met 6 mond micro USB-kabel.

De volgende items zijn optioneel:

* Een samengesteld Adafruit BME280 temperatuur, druk en vochtigheid sensor.
* Een breadboard.
* 6 F/M meestal bedrading.
* Een gedempt 10 mm LED.

  > [!NOTE] 
  Deze items zijn optioneel, omdat de ondersteuning voor het voorbeeld van code sensorgegevens gesimuleerd.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a>Raspberry Pi instellen

### <a name="install-the-raspbian-operating-system-for-pi"></a>Het besturingssysteem Raspbian voor Pi installeren

Bereid de microSD-kaart voor de installatie van de installatiekopie van het Raspbian.

1. Raspbian downloaden.
   1. [Download Raspbian Jessie met Pixel](https://www.raspberrypi.org/downloads/raspbian/) (het ZIP-bestand).
   1. Pak de installatiekopie van het Raspbian naar een map op uw computer.
1. Installeer Raspbian naar de microSD-kaart.
   1. [Download en installeer het hulpprogramma Etcher SD-kaart brander](https://etcher.io/).
   1. Voer Etcher en selecteer de installatiekopie van het Raspbian die u hebt opgehaald in stap 1.
   1. Selecteer het station microSD-kaart. Houd er rekening mee dat Etcher mogelijk al hebt geselecteerd de juiste station.
   1. Klik op Flash voor het installeren van Raspbian naar de microSD-kaart.
   1. Verwijder de microSD-kaart van uw computer wanneer de installatie voltooid is. Het is veilig worden verwijderd, de microSD-kaart rechtstreeks omdat Etcher automatisch uitwerpen of ontkoppelt de microSD-kaart is voltooid.
   1. Plaats de microSD-kaart in Pi.

### <a name="enable-ssh-and-i2c"></a>SSH- en I2C inschakelen

1. Verbinding maken met Pi de monitor, toetsenbord en muis Pi start en meld u daarna Raspbian met behulp van `pi` als de gebruikersnaam en `raspberry` als het wachtwoord.
1. Klik op het pictogram Raspberry > **voorkeuren** > **frambozen Pi configuratie**.

   ![Het menu Raspbian voorkeuren](media/iot-hub-raspberry-pi-kit-node-get-started/1_raspbian-preferences-menu.png)

1. Op de **Interfaces** tabblad, stelt u **I2C** en **SSH** naar **inschakelen**, en klik vervolgens op **OK**. Als u geen fysieke sensoren hebben en gesimuleerde sensorgegevens wilt gebruiken, is deze stap is optioneel.

   ![I2C en SSH met Raspberry Pi inschakelen](media/iot-hub-raspberry-pi-kit-node-get-started/2_enable-i2c-ssh-on-raspberry-pi.png)

> [!NOTE] 
Voor het inschakelen van SSH en I2C, vindt u meer verwijzing documenten op [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) en [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).

### <a name="connect-the-sensor-to-pi"></a>Verbinding maken met de sensor Pi

Gebruik de bedrading breadboard en meestal als volgt een LED en een BME280 tot Pi verbinden. Als u niet de sensor hebt, kunt u deze sectie overslaan.

![De verbinding frambozen Pi en temperatuursensor](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

De sensor BME280 kunt temperatuur en vochtigheid gegevens verzamelen. En de LED knippert als er een communicatie tussen het apparaat en de cloud. 

Gebruik de volgende bedrading voor sensor-pincodes:

| Start (Sensor & LED)     | Einde (BMC)            | Kleur van de kabel   |
| -----------------------  | ---------------------- | ------------: |
| VDD (Pin 5G)             | 3, 3v PWR (pincode 1)       | Witte kabel   |
| GND (Pin 7G)             | GND (pincode 6)            | Bruine-kabel   |
| SCK (Pin 8G)             | I2C1 SDA (pincode 3)       | Oranje-kabel  |
| SDI (Pin 10G)            | I2C1 SCL (pincode 5)       | Rode-kabel     |
| LED VDD (Pin 18F)        | GPIO 24 (Pin 18)       | Witte kabel   |
| LED GND (Pin 17F)        | GND (Pin 20)           | Zwarte kabel   |

Klik hier voor weergave [frambozen Pi 2 en 3 pincode toewijzingen](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) ter referentie.

Nadat u hebt BME280 is verbonden met uw Pi frambozen, moet zoals hieronder installatiekopie.

![Verbonden Pi en BME280](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-to-the-network"></a>Pi verbinding met het netwerk

Pi inschakelen met behulp van het micro USB-kabel en de voeding. Via het Ethernet-kabel Pi verbinden met het bekabelde netwerk of volgen de [instructies van de frambozen Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) Pi verbinding met uw draadloze netwerk. Nadat uw Pi is verbonden met het netwerk, moet u Noteer de [IP-adres van uw Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).

![Verbonden met een bekabeld netwerk](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> Zorg ervoor dat Pi is verbonden met hetzelfde netwerk bevindt als uw computer. Bijvoorbeeld, als uw computer is verbonden met een draadloos netwerk als Pi is verbonden met een bekabeld netwerk, ziet u mogelijk niet het IP-adres in de uitvoer devdisco.

## <a name="run-a-sample-application-on-pi"></a>Een voorbeeld van een toepassing uitvoeren op Pi

### <a name="clone-sample-application-and-install-the-prerequisite-packages"></a>Klonen van de voorbeeldtoepassing en de vereiste pakketten installeren

1. Gebruik een van de volgende SSH-clients van de hostcomputer verbinding maken met uw frambozen Pi.
    - [PuTTY](http://www.putty.org/) voor Windows. U moet het IP-adres van uw Pi zodat deze verbinding te maken via SSH.
    - De ingebouwde SSH-client op Ubuntu- of Mac OS. U moet uitvoeren `ssh pi@<ip address of pi>` Pi via SSH verbinding maken.

   > [!NOTE] 
   De standaardgebruikersnaam `pi` , en het wachtwoord is `raspberry`.

1. Node.js en NPM naar uw Pi installeren.
   
   Controleer eerst uw Node.js-versie met de volgende opdracht. 
   
   ```bash
   node -v
   ```

   Als de versie lager dan 4.x is of er geen Node.js op uw Pi is, voer de volgende opdracht installeren of bijwerken van Node.js.

   ```bash
   curl -sL http://deb.nodesource.com/setup_4.x | sudo -E bash
   sudo apt-get -y install nodejs
   ```

1. Kloon de voorbeeldtoepassing met de volgende opdracht:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-client-app
   ```

1. Installeer alle pakketten met de volgende opdracht. Omvat Azure IoT-device SDK, BME280 Sensor-bibliotheek en bedrading Pi-bibliotheek.

   ```bash
   cd iot-hub-node-raspberrypi-client-app
   sudo npm install
   ```
   > [!NOTE] 
   Het duurt enkele minuten duren deze denpening installatie proces op de netwerkverbinding.

### <a name="configure-the-sample-application"></a>De voorbeeldtoepassing configureren

1. Open het configuratiebestand met de volgende opdrachten:

   ```bash
   nano config.json
   ```

   ![Configuratiebestand](media/iot-hub-raspberry-pi-kit-node-get-started/6_config-file.png)

   Er zijn twee items in dit bestand kunt u configurate. De eerste is `interval`, definieert het tijdsinterval tussen twee berichten die naar de cloud verzendt. De tweede waarde `simulatedData`, dit is een Booleaanse waarde voor of gesimuleerde sensorgegevens of niet.

   Als u **hoeft niet de sensor**stelt de `simulatedData` van waarde naar `true` ervoor dat de voorbeeldtoepassing maken en gebruiken van gesimuleerde sensorgegevens.

1. Opslaan en sluiten door te drukken besturingselement-O > Enter > Control X.

### <a name="run-the-sample-application"></a>De voorbeeldtoepassing uitvoeren

1. De voorbeeldtoepassing met de volgende opdracht uitvoeren:

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   Zorg ervoor dat u kopiëren en plakken de apparaat-verbindingsreeks in enkele aanhalingstekens.


Hier ziet u de volgende uitvoer waarin de sensorgegevens en de berichten die worden verzonden naar uw IoT-hub.

![Output - sensorgegevens verzonden van frambozen Pi naar uw IoT-hub](media/iot-hub-raspberry-pi-kit-node-get-started/8_run-output.png)

## <a name="next-steps"></a>Volgende stappen

U kunt een voorbeeldtoepassing sensorgegevens verzamelen en verzenden naar uw IoT-hub hebt uitgevoerd.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]