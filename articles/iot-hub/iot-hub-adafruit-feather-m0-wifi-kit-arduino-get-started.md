---
title: 'M0 toocloud: verbinding maken met Doezelaar M0 Wi-Fi tooAzure IoT Hub | Microsoft Docs'
description: Meer informatie over hoe tooset boven en verbinding maken met Adafruit Doezelaar M0 Wi-Fi tooAzure IoT Hub toosend gegevens toohello Azure cloud-platform in deze zelfstudie.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 51befcdb-332b-416f-a6a1-8aabdb67f283
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/16/2017
ms.author: xshi
ms.openlocfilehash: 6aabeb961a50ba5d3934f77eb1ccda4af1bf64c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-m0-wifi-tooazure-iot-hub-in-hello-cloud"></a>Verbinding maken met Adafruit Doezelaar M0 Wi-Fi tooAzure IoT-Hub in de cloud Hallo
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Verbinding tussen een BME280, Doezelaar M0 Wi-Fi en IoT-Hub](media/iot-hub-adafruit-feather-m0-wifi-get-started/1_connection-m0-feather-m0-iot-hub.png)

In deze zelfstudie maakt eerst u Hallo basisbeginselen van het werken met het mededelingenbord Arduino leren. U leert vervolgens hoe uw apparaten toohello cloud in tooseamlessly verbinding maken met behulp van [Azure IoT Hub](iot-hub-what-is-iot-hub.md).

## <a name="what-you-do"></a>Wat u doet

Verbinding maken met Adafruit Doezelaar M0 Wi-Fi tooan IoT-hub die u maakt. Vervolgens voert u een voorbeeld van toepassing op M0 Wi-Fi toocollect Hallo temperatuur en vochtigheid gegevens uit een BME280. Ten slotte verzendt u Hallo sensor gegevens tooyour iothub.


## <a name="what-you-learn"></a>Wat u leert

* Hoe toocreate een IoT-hub en een apparaat registreren voor Doezelaar M0 Wi-Fi
* Hoe tooconnect Doezelaar M0 Wi-Fi met Hallo sensoren en uw computer
* Hoe toocollect sensorgegevens door het uitvoeren van een voorbeeld van toepassing op Doezelaar M0 Wi-Fi
* Hoe toosend Hallo sensor gegevens tooyour IoT-hub

## <a name="what-you-need"></a>Wat u nodig hebt

![Onderdelen die nodig zijn voor Hallo-zelfstudie](media/iot-hub-adafruit-feather-m0-wifi-get-started/2_parts-needed-for-the-tutorial.png)

toocomplete deze bewerking moet u volgende onderdelen van uw Doezelaar M0 Wi-Fi Starter Kit Hallo:

* Hallo Doezelaar M0 Wi-Fi mededelingenbord
* Een USB-Micro tooType een USB-kabel

U moet ook Hallo dingen voor uw ontwikkelomgeving te volgen:

* Een actief Azure-abonnement. Als u een Azure-account geen [maken van een gratis Azure-proefaccount](https://azure.microsoft.com/free/) over een paar minuten.
* Een Mac of een PC met Windows of Ubuntu.
* Een draadloos netwerk voor Doezelaar M0 Wi-Fi-tooconnect aan.
* Een Internet verbinding toodownload Hallo configuratiehulpprogramma.
* [Arduino IDE](https://www.arduino.cc/en/main/software) versie 1.6.8 of hoger. Eerdere versies werken niet met hello Azure IoT Hub-bibliotheek.

Als u een sensor hebt, is Hallo volgende items zijn optioneel. U hebt ook een optie van het gebruik van gesimuleerde sensorgegevens Hallo:

* Een BME280 temperatuur en vochtigheid sensor
* Een breadboard
* M/M meestal kabels

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-m0-wifi-with-hello-sensor-and-your-computer"></a>Verbinding maken met Doezelaar M0 Wi-Fi met Hallo sensoren en uw computer
In deze sectie maakt verbinding u Hallo sensoren tooyour mededelingenbord. U sluit uw apparaat tooyour computer voor verdere gebruik.

### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-m0-wifi"></a>Verbinding maken met een DHT22 temperatuur en vochtigheid sensor tooFeather M0 Wi-Fi

Hallo breadboard en meestal kabels toomake Hallo verbinding gebruiken. Als u geen een sensor, deze sectie overslaan omdat u gesimuleerde sensorgegevens in plaats daarvan kunt gebruiken.

![Verbindingen verwijzing](media/iot-hub-adafruit-feather-m0-wifi-get-started/3_connections_on_breadboard.png)


Gebruik voor pincodes sensor, Hallo bedrading te volgen:


| Start (sensor)           | Einde (BMC)            | Kleur van de kabel   |
| -----------------------  | ---------------------- | ------------: |
| VDD (Pin 27A)            | 3v (3A pincode)            | Rode-kabel     |
| GND (Pin 29 bis)            | GND (6A pincode)           | Zwarte kabel   |
| SCK (pincode 30)            | SCK (Pin 12A)          | Gele-kabel  |
| SDO (Pin 31A)            | MI (Pin 14A)           | Witte kabel   |
| SDI (Pin 32 bis)            | M0 (Pin 13A)           | Blauw-kabel    |
| CS (Pin 33A)             | GPIO 5 (Pin 15J)       | Oranje-kabel  |

Zie voor meer informatie [Adafruit BME280 vochtigheid + barometerdruk + temperatuur Sensor evenement](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) en [Adafruit Doezelaar M0 Wi-Fi pin-outs gegeven](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts).



Nu moeten uw Doezelaar M0 Wi-Fi zijn verbonden met een sensor werken.

![DHT22 verbinden met Doezelaar Huzzah](media/iot-hub-adafruit-feather-m0-wifi-get-started/4_connect-bme280-feather-m0-wifi.png)

### <a name="connect-feather-m0-wifi-tooyour-computer"></a>Verbind Doezelaar M0 Wi-Fi tooyour computer

Hallo Micro USB tooType een USB-kabel tooconnect Doezelaar M0 Wi-Fi tooyour computer gebruiken, zoals wordt weergegeven:

![Verbind Doezelaar Huzzah tooyour computer](media/iot-hub-adafruit-feather-m0-wifi-get-started/5_connect-feather-m0-wifi-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a>Machtigingen van de seriële poort (alleen Ubuntu) toevoegen

Als u Ubuntu gebruikt, moet u Hallo machtigingen toooperate op Hallo USB-poort van Doezelaar M0 Wi-Fi. machtigingen van de seriële poort tooadd, als volgt te werk:


1. Voer op een terminal Hallo volgende opdrachten:

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   Ophalen van een Hallo volgende uitvoer:

   * CRW-rw---1 hoofdmap uucp xxxxxxxx
   * CRW-rw---1 hoofdmap bellen xxxxxxxx

   U ziet dat in de uitvoer van Hallo `uucp` of `dialout` Hallo groepsnaam eigenaar Hallo USB-poort is.

2. tooadd hello toohello gebruikersgroep, Hallo volgende opdracht uitvoeren:

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   In de vorige stap hello, die u hebt verkregen Hallo eigenaar groepsnaam `<group-owner-name>`. De gebruikersnaam Ubuntu `<username>`.

3. Meld u af bij Ubuntu voor Hallo wijziging tooappear, en vervolgens weer aanmelden.

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a>Sensorgegevens verzamelen en deze tooyour IoT-hub te verzenden

In deze sectie die u kunt implementeren en uitvoeren van een voorbeeld van toepassing op Doezelaar M0 Wi-Fi. Hallo-voorbeeldtoepassing maakt Hallo LED knipperen aan Doezelaar M0 Wi-Fi. Verzendt vervolgens Hallo temperatuur en vochtigheid gegevens die worden verzameld van Hallo BME280 sensor tooyour IoT-hub.

### <a name="get-hello-sample-application-from-github-and-prepare-hello-arduino-ide"></a>Hallo-voorbeeldtoepassing ophalen van GitHub en Hallo Arduino IDE voorbereiden

Hallo-voorbeeldtoepassing wordt gehost op GitHub. Kloon Hallo voorbeeld opslagplaats waarin de voorbeeldtoepassing Hallo vanuit GitHub. tooclone hello voorbeeld opslagplaats als volgt te werk:

1. Open een opdrachtprompt of een terminalvenster.

2. Ga tooa map waarin u Hallo voorbeeld toepassing toobe opgeslagen.
3. Hallo volgende opdracht uitvoeren:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-Feather-M0-WiFi-client-app.git
   ```

### <a name="install-hello-package-for-feather-m0-wifi-in-hello-arduino-ide"></a>Hallo-pakket voor Doezelaar M0 Wi-Fi in Hallo Arduino IDE installeren

1. Open Hallo map waarin de voorbeeldtoepassing Hallo is opgeslagen.

2. Hallo app.ino bestand openen in Hallo app map in Hallo Arduino IDE.

   ![Hallo-voorbeeldtoepassing in Arduino IDE openen](media/iot-hub-adafruit-feather-m0-wifi-get-started/6_arduino-ide-open-sample-app.png)


1. Klik op **bestand** > **voorkeuren** (Windows of Linux) of **Arduino** > **voorkeuren** (Mac) en kopieert en koppeling hieronder Hallo in Hallo plakken **extra Boards Manager-URL's** optie in Hallo Arduino IDE-voorkeuren.
   
   ```
   https://adafruit.github.io/arduino-board-index/package_adafruit_index.json, https://adafruit.github.io/arduino-board-index/package_adafruit_index.json
   ```

1. Klik op **extra** > **mededelingenbord** > **Boards Manager**, en installeer vervolgens Hallo `Arduino SAMD Boards` versie `1.6.2` of hoger. 

1. Klik dan in hetzelfde venster hello, installeert u `Adafruit SAMD Boards` tooadd Hallo mededelingenbord bestand definities van het pakket.

   ![Hallo esp8266 pakket is geïnstalleerd](media/iot-hub-adafruit-feather-m0-wifi-get-started/7_arduino-ide-package-url.png)

4. Klik op **extra** > **mededelingenbord** > **Adafruit M0 Wi-Fi**.

5. Stuurprogramma's installeren (voor Windows). Wanneer u Doezelaar M0 Wi-Fi aansluit, moet u mogelijk een stuurprogramma tooinstall. Klik op [Hallo downloadkoppeling op Hallo webpagina](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) toodownload Hallo stuurprogramma installatieprogramma. Ga als volgt Hallo stappen tooinstall Hallo stuurprogramma's.

### <a name="install-necessary-libraries"></a>Vereiste bibliotheken installeren

1. In Hallo Arduino IDE, klikt u op **schema** > **bibliotheek omvatten** > **bibliotheken beheren**.

2. Zoeken naar Hallo bibliotheeknamen, één voor één te volgen. Voor elke bibliotheek die u vindt, klikt u op **installeren**:

   * `RTCZero`
   * `NTPClient`
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_HTTP`
   * `ArduinoJson`
   * `Adafruit BME280 Library`
   * `Adafruit Unified Sensor`

3. Handmatig installeren `Adafruit_WINC1500`. Ga te[deze website](https://github.com/adafruit/Adafruit_WINC1500) en klik op **klonen of downloaden** > **ZIP downloaden**. In uw IDE Arduino gaat te**schema** > **bibliotheek omvatten** > **.zip bibliotheek toevoegen** en Hallo zip-bestand toe te voegen.

### <a name="use-hello-sample-application-if-you-dont-have-a-real-bme280-sensor"></a>Hallo-voorbeeldtoepassing gebruiken als u een echte BME280-temperatuursensor hebt

Als u een echte BME280 sensor geen hebt, kunt de voorbeeldtoepassing Hallo temperatuur en vochtigheid gegevens simuleren. tooset up Hallo toepassing toouse gesimuleerde voorbeeldgegevens, als volgt te werk:

1. Open Hallo `config.h` bestand in Hallo `app` map.

2. Zoek Hallo coderegel na en wijzig Hallo-waarde van `false` te`true`:

   ```c
   define SIMULATED_DATA true
   ```
   ![Toepassing hello-toouse gesimuleerde Voorbeeldgegevens configureren](media/iot-hub-adafruit-feather-m0-wifi-get-started/8_arduino-ide-configure-app-use-simulated-data.png)

3. Hallo opslaan met `Control-s`.

### <a name="deploy-hello-sample-application-toofeather-m0-wifi"></a>Hallo voorbeeld toepassing tooFeather M0 Wi-Fi implementeren

1. Klik in het Hallo Arduino IDE, op **hulpprogramma** > **poort**, en klik vervolgens op de seriële poort Hallo voor Doezelaar M0 Wi-Fi.

2. Klik op **schema** > **uploaden** toobuild en Hallo voorbeeld toepassing tooFeather M0 Wi-Fi implementeren.

### <a name="enter-your-credentials"></a>Voer uw referenties in

Nadat het Hallo uploaden is voltooid, volgt u deze stappen tooenter uw referenties:

1. In Hallo Arduino IDE, klikt u op **extra** > **seriële Monitor**.

2. Selecteer in de Hallo rechterbenedenhoek van het venster seriële monitor Hallo, **er is geen afsluitende regel** in Hallo vervolgkeuzelijst aan de linkerkant Hallo.
3. Selecteer **115200 baud** in Hallo vervolgkeuzelijst op de juiste Hallo.
4. Voer in invoervak Hallo Hallo boven Hallo volgende informatie als u bent tooprovide gevraagd en klik op **verzenden**:

   * Wi-Fi-SSID
   * Wi-Fi-wachtwoord
   * Apparaat-verbindingsreeks

> [!Note]
> Hallo referentie-informatie wordt opgeslagen in Hallo EEPROM Doezelaar M0 WiFi. Als u op de herstelknop Hallo op Hallo mededelingenbord Doezelaar M0 Wi-Fi, desgewenst Hallo voorbeeldtoepassing tooerase Hallo informatie. Voer `Y` tooerase Hallo informatie. U wordt gevraagd tooprovide Hallo informatie een tweede keer.

### <a name="verify-that-hello-sample-application-is-running-successfully"></a>Controleren of de voorbeeldtoepassing Hallo met succes wordt uitgevoerd

Als u ziet Hallo volgende de uitvoer van het venster seriële monitor Hallo en Hallo knipperende LED Doezelaar M0 Wi-Fi, Hallo voorbeeldtoepassing correct wordt uitgevoerd:

![Uiteindelijke uitvoer Arduino IDE](media/iot-hub-adafruit-feather-m0-wifi-get-started/9_arduino-ide-final-output.png)

## <a name="next-steps"></a>Volgende stappen

U hebt verbonden Doezelaar M0 Wi-Fi tooyour IoT-hub en verzonden hello vastgelegd sensor gegevens tooyour IoT-hub. 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

