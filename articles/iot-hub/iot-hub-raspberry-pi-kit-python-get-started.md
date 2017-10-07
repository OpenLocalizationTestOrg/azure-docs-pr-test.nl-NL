---
title: aaaRaspberry Pi toocloud (Python) - verbinding frambozen Pi tooAzure IoT Hub | Microsoft Docs
description: Meer informatie over hoe toosetup en verbinding maken met frambozen Pi tooAzure IoT Hub voor frambozen Pi toosend gegevens toohello Azure-cloudplatform in deze zelfstudie.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Azure iot raspberry pi raspberry pi iot hub, raspberry pi verzenden gegevens toocloud raspberry pi toocloud
ms.service: iot-hub
ms.devlang: python
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 7/31/2017
ms.author: xshi
ms.openlocfilehash: 86f5c91ab9dd4e23c563437827fb7d2d06916d2e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-python"></a>Verbinding maken met frambozen Pi tooAzure IoT Hub (Python)

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

## <a name="set-up-raspberry-pi"></a>Frambozen Pi instellen

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

### <a name="enable-ssh-and-i2c"></a>SSH- en I2C inschakelen

1. Sluit Pi toohello monitor, toetsenbord en muis, Pi starten en meld u daarna Raspbian met behulp van `pi` als Hallo-gebruikersnaam en `raspberry` Hallo wachtwoord.
1. Klik op Hallo Raspberry pictogram > **voorkeuren** > **frambozen Pi configuratie**.

   ![Hallo Raspbian voorkeuren menu](media/iot-hub-raspberry-pi-kit-c-get-started/1_raspbian-preferences-menu.png)

1. Op Hallo **Interfaces** tabblad, stelt u **I2C** en **SSH** te**inschakelen**, en klik vervolgens op **OK**. Als u geen fysieke sensoren hebben en sensorgegevens toouse gesimuleerde wilt, moet deze stap is optioneel.

   ![I2C en SSH met Raspberry Pi inschakelen](media/iot-hub-raspberry-pi-kit-c-get-started/2_enable-spi-ssh-on-raspberry-pi.png)

> [!NOTE] 
tooenable SSH en I2C u meer verwijzing documenten vindt op [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) en [RASPI-CONFIG](https://www.raspberrypi.org/documentation/configuration/raspi-config.md).

### <a name="connect-hello-sensor-toopi"></a>Hallo sensor tooPi verbinding

Hallo breadboard en meestal kabels tooconnect een LED en een tooPi BME280 als volgt gebruiken. Als u geen Hallo sensor, [deze sectie overslaan](#connect-pi-to-the-network).

![Hallo frambozen Pi en sensor verbinding](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

Hallo BME280 sensor kunt temperatuur en vochtigheid gegevens verzamelen. En Hallo LED knippert als er een communicatie tussen apparaten en Hallo cloud. 

Gebruik voor pincodes sensor, Hallo bedrading te volgen:

| Start (Sensor & LED)     | Einde (BMC)            | Kleur van de kabel   |
| -----------------------  | ---------------------- | ------------: |
| VDD (Pin 5G)             | 3, 3v PWR (pincode 1)       | Witte kabel   |
| GND (Pin 7G)             | GND (pincode 6)            | Bruine-kabel   |
| SDI (Pin 10G)            | I2C1 SDA (pincode 3)       | Rode-kabel     |
| SCK (Pin 8G)             | I2C1 SCL (pincode 5)       | Oranje-kabel  |
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

### <a name="install-hello-prerequisite-packages"></a>Vereiste hello-pakketten installeren

Gebruik een van de volgende clients SSH uit uw host computer tooconnect tooyour frambozen Pi Hallo.
   
   **Windows-gebruikers**
   1. Download en installeer [PuTTY](http://www.putty.org/) voor Windows. 
   1. Kopieer Hallo IP-adres van de sectie Pi in Hallo Host name (of IP-adres) en selecteer SSH als Hallo verbindingstype.
   
   
   **Mac- en Ubuntu-gebruikers**
   
   Hallo ingebouwde SSH-client op Ubuntu- of Mac OS gebruiken. Mogelijk moet u toorun `ssh pi@<ip address of pi>` tooconnect Pi via SSH.
   > [!NOTE] 
   Hallo standaardgebruikersnaam `pi` , en het Hallo-wachtwoord is `raspberry`.


### <a name="configure-hello-sample-application"></a>Hallo-voorbeeldtoepassing configureren

1. Hallo-voorbeeldtoepassing door het uitvoeren van de volgende opdracht Hallo klonen:

   ```bash
   cd ~
   git clone https://github.com/Azure-Samples/iot-hub-python-raspberrypi-client-app.git
   ```
1. Open Hallo config-bestand door het uitvoeren van de volgende opdrachten Hallo:

   ```bash
   cd iot-hub-python-raspberrypi-client-app
   nano config.py
   ```

   Er zijn 5 macro's in dit bestand kunt u configurate. Hallo eerst een is `MESSAGE_TIMESPAN`, definieert een Hallo tijdsinterval (in milliseconden) tussen twee berichten die toocloud verzenden. tweede Hallo `SIMULATED_DATA`, dit is een Booleaanse waarde voor of toouse sensorgegevens gesimuleerd. `I2C_ADDRESS`Hallo I2C-adres dat is verbonden met uw BME280 sensor is. `GPIO_PIN_ADDRESS`Hallo GPIO adres is voor uw LED. Hallo laatste een is `BLINK_TIMESPAN`, die Hallo timespan gedefinieerd wanneer uw LED is ingeschakeld in milliseconden.

   Als u **geen Hallo sensor**stelt hello `SIMULATED_DATA` waarde te`True` toomake Hallo voorbeeld van een toepassing maken en gesimuleerde sensorgegevens gebruiken.

1. Opslaan en sluiten door te drukken besturingselement-O > Enter > Control X.

### <a name="build-and-run-hello-sample-application"></a>Hallo voorbeeldtoepassing bouwen en uitvoeren

1. Hallo-voorbeeldtoepassing bouwen door het uitvoeren van de volgende opdracht Hallo. Omdat hello Azure IoT SDK's voor Python wrappers boven op Hallo C-SDK van Azure IoT-apparaat, moet u toocompile Hallo C bibliotheken als toogenerate Hallo Python-bibliotheken van broncode moet of wilt u.

   ```bash
   sudo chmod u+x setup.sh
   sudo ./setup.sh
   ```
   > [!NOTE] 
   U kunt ook opgeven Hallo-versie die u wilt dat door het uitvoeren van `sudo ./setup.sh [--python-version|-p] [2.7|3.4|3.5]`. Als u het script zonder parameter uitvoert, Hallo script Hallo-versie van python geïnstalleerd automatisch detecteren (zoekvolgorde 2.7 -> 3.4 3.5 ->). Zorg ervoor dat uw versie van Python consistent blijft tijdens het bouwen en uitvoeren. 
   
   > [!NOTE] 
   Over het bouwen van Hallo Python-clientbibliotheek (iothub_client.so) op Linux-apparaten die minder dan 1 GB RAM-geheugen, ziet u mogelijk bouwen zitten 98% tijdens het bouwen van iothub_client_python.cpp zoals hieronder wordt weergegeven `[ 98%] Building CXX object python/src/CMakeFiles/iothub_client_python.dir/iothub_client_python.cpp.o`. Als u dit probleem ondervindt, Controleer Hallo geheugenverbruik van het Hallo-apparaten met `free -m command` in een andere terminalvenster gedurende die tijd. Als u onvoldoende geheugen tijdens het compileren van iothub_client_python.cpp bestand uitvoert, hebt u mogelijk verhogen Hallo wisselen ruimte tooget tootemporarily meer beschikbaar geheugen toosuccessfully bouwen Hallo Python clientzijde apparaat SDK-bibliotheek.
   
1. Hallo-voorbeeldtoepassing uitvoeren door te voeren van Hallo volgende opdracht:

   ```bash
   python app.py '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   Zorg ervoor dat u kopiëren en plakken Hallo apparaat verbindingsreeks in Hallo tussen enkele aanhalingstekens. En als u python Hallo 3 gebruiken, dan kunt u de opdracht Hallo `python3 app.py '<your Azure IoT hub device connection string>'`.


   U ziet Hallo volgende resultaat dat wordt weergegeven Hallo sensor gegevens en het Hallo-berichten dat tooyour iothub worden verzonden.

   ![Output - sensorgegevens uit frambozen Pi tooyour iothub worden verzonden](media/iot-hub-raspberry-pi-kit-c-get-started/success.png
)

## <a name="next-steps"></a>Volgende stappen

U hebt een voorbeeldgegevens toepassing toocollect sensor uitgevoerd en verzend het tooyour IoT-hub. toosee Hallo-berichten dat uw Pi frambozen tooyour IoT-hub of verzenden berichten tooyour frambozen Pi heeft verzonden in een opdrachtregelinterface Zie Hallo [beheren cloud apparaat messaging met iothub explorer zelfstudie](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
