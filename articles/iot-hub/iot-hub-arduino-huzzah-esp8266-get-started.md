---
title: aaaESP8266 toocloud - verbinding Doezelaar HUZZAH ESP8266 tooAzure IoT Hub | Microsoft Docs
description: Meer informatie over hoe toosetup en verbinding Adafruit Doezelaar HUZZAH ESP8266 tooAzure IoT Hub voor toosend gegevens toohello Azure cloud-platform in deze zelfstudie.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: c505aacf-89a8-40ed-a853-493b75bec524
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: xshi
ms.openlocfilehash: 44fd47232488948d21c7aa71bdd865397e41e63e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-huzzah-esp8266-tooazure-iot-hub-in-hello-cloud"></a>Verbinding maken met Adafruit Doezelaar HUZZAH ESP8266 tooAzure IoT-Hub in de cloud Hallo

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Verbinding tussen DHT22 Doezelaar HUZZAH ESP8266 en IoT-Hub](media/iot-hub-arduino-huzzah-esp8266-get-started/1_connection-hdt22-feather-huzzah-iot-hub.png)

## <a name="what-you-do"></a>Wat u doet


Verbinding maken met Adafruit Doezelaar HUZZAH ESP8266 tooan IoT-hub die u maakt. Vervolgens voert u een voorbeeld van toepassing op ESP8266 toocollect Hallo temperatuur en vochtigheid gegevens van een sensor DHT22. Ten slotte verzendt u Hallo sensor gegevens tooyour iothub.

> [!NOTE]
> Als u andere boards ESP8266 gebruikt, kunt u nog steeds de tooconnect van deze stappen volgen het tooyour IoT-hub. Afhankelijk van het mededelingenbord Hallo ESP8266 u gebruikt, moet u mogelijk tooreconfigure hello `LED_PIN`. Bijvoorbeeld, als u ESP8266 van AI-Thinker, u wijzigt in `0` te`2`. Heb je nog een kit? Het ophalen van Hallo [Azure-website](http://azure.com/iotstarterkits).




## <a name="what-you-learn"></a>Wat u leert

* Hoe toocreate een IoT-hub en een apparaat registreren voor Doezelaar HUZZAH ESP8266
* Hoe tooconnect Doezelaar HUZZAH ESP8266 met Hallo sensoren en uw computer
* Hoe toocollect sensorgegevens door het uitvoeren van een voorbeeld van toepassing op Doezelaar HUZZAH ESP8266
* Hoe toosend Hallo sensor gegevens tooyour IoT-hub

## <a name="what-you-need"></a>Wat u nodig hebt

![Onderdelen die nodig zijn voor Hallo-zelfstudie](media/iot-hub-arduino-huzzah-esp8266-get-started/2_parts-needed-for-the-tutorial.png)

toocomplete deze bewerking moet u volgende onderdelen van uw Doezelaar HUZZAH ESP8266 Starter Kit Hallo:

* Hallo Doezelaar HUZZAH ESP8266 mededelingenbord
* Een USB-Micro tooType een USB-kabel

U moet ook Hallo dingen voor uw ontwikkelomgeving te volgen:

* Een actief Azure-abonnement. Als u een Azure-account geen [maken van een gratis Azure-proefaccount](https://azure.microsoft.com/free/) over een paar minuten.
* Mac of PC met Windows of Ubuntu.
* Doezelaar HUZZAH ESP8266 tooconnect voor draadloos netwerk.
* Internet verbinding toodownload Hallo-configuratiehulpprogramma.
* [Arduino IDE](https://www.arduino.cc/en/main/software) versie 1.6.8 of hoger. Eerdere versies werken niet met Hallo AzureIoT-bibliotheek.

Hallo zijn volgende items optioneel als u een sensor geen hebt. U hebt ook Hallo-optie van het gebruik van gesimuleerde sensorgegevens.

* Een Adafruit DHT22 temperatuur en vochtigheid-temperatuursensor
* Een breadboard
* M/M meestal kabels


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-huzzah-esp8266-with-hello-sensor-and-your-computer"></a>Verbinding maken met Doezelaar HUZZAH ESP8266 met Hallo sensoren en uw computer
In deze sectie maakt verbinding u Hallo sensoren tooyour mededelingenbord. U sluit uw apparaat tooyour computer voor verdere gebruik.
### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-huzzah-esp8266"></a>Verbinding maken met een DHT22 temperatuur en vochtigheid sensor tooFeather HUZZAH ESP8266

Hallo breadboard en meestal kabels toomake Hallo verbinding als volgt gebruiken. Als u geen een sensor, deze sectie overslaan omdat u gesimuleerde sensorgegevens in plaats daarvan kunt gebruiken.

![Verbindingen verwijzing](media/iot-hub-arduino-huzzah-esp8266-get-started/15_connections_on_breadboard.png)


Gebruik voor pincodes sensor, Hallo bedrading te volgen:


| Start (Sensor)           | Einde (BMC)           | Kleur van de kabel   |
| -----------------------  | ---------------------- | ------------: |
| VDD (Pin 31F)            | 3v (vastmaken 58H)           | Rode-kabel     |
| GEGEVENS (Pin 32F)           | GPIO 2 (Pin 46)       | Blauw-kabel    |
| GND (Pin 34F)            | GND (PIn 56I)          | Zwarte kabel   |

Zie voor meer informatie [Adafruit DHT22 sensor setup](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) en [Adafruit Doezelaar HUZZAH Esp8266 pin-outs gegeven](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).



Nu moeten uw Doezelaar Huzzah ESP8266 zijn verbonden met een sensor werken.

![DHT22 verbinden met Doezelaar Huzzah](media/iot-hub-arduino-huzzah-esp8266-get-started/8_connect-dht22-feather-huzzah.png)

### <a name="connect-feather-huzzah-esp8266-tooyour-computer"></a>Verbind Doezelaar HUZZAH ESP8266 tooyour computer

Zoals u volgende, Hallo Micro USB tooType een USB-kabel tooconnect Doezelaar HUZZAH ESP8266 tooyour computer gebruiken.

![Verbind Doezelaar Huzzah tooyour computer](media/iot-hub-arduino-huzzah-esp8266-get-started/9_connect-feather-huzzah-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a>Machtigingen van de seriële poort (alleen Ubuntu) toevoegen


Als u Ubuntu gebruikt, moet u Hallo machtigingen toooperate op Hallo USB-poort van Doezelaar HUZZAH ESP8266. machtigingen van de seriële poort tooadd, als volgt te werk:


1. Voer Hallo opdrachten op een terminal te volgen:

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   Ophalen van een Hallo volgende uitvoer:

   * CRW-rw---1 hoofdmap uucp xxxxxxxx
   * CRW-rw---1 hoofdmap bellen xxxxxxxx

   U ziet dat in de uitvoer van Hallo `uucp` of `dialout` Hallo groepsnaam eigenaar Hallo USB-poort is.

1. Hallo-gebruikersgroep toohello door het uitvoeren van de volgende opdracht Hallo toevoegen:

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   `<group-owner-name>`Hallo eigenaar groepsnaam die u hebt verkregen is in de vorige stap Hallo. `<username>`uw gebruikersnaam Ubuntu is.

1. Meld u af bij Ubuntu en vervolgens opnieuw aan te melden voor Hallo wijziging tooappear.

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a>Sensorgegevens verzamelen en deze tooyour IoT-hub te verzenden

In deze sectie die u kunt implementeren en uitvoeren van een voorbeeld van toepassing op Doezelaar HUZZAH ESP8266. Hallo-voorbeeldtoepassing knippert Hallo LED Doezelaar HUZZAH ESP8266 en verzendt Hallo temperatuur en vochtigheid gegevens die worden verzameld van Hallo DHT22 sensor tooyour IoT-hub.

### <a name="get-hello-sample-application-from-github"></a>Hallo-voorbeeldtoepassing ophalen van GitHub

Hallo-voorbeeldtoepassing wordt gehost op GitHub. Kloon Hallo voorbeeld opslagplaats waarin de voorbeeldtoepassing Hallo vanuit GitHub. tooclone hello voorbeeld opslagplaats als volgt te werk:

1. Open een opdrachtprompt of een terminalvenster.
1. Ga tooa map waarin u Hallo voorbeeld toepassing toobe opgeslagen.
1. Hallo volgende opdracht uitvoeren:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-feather-huzzah-client-app.git
   ```

Hallo-pakket voor Doezelaar HUZZAH ESP8266 op Hallo Arduino IDE installeren:

1. Open Hallo map waarin de voorbeeldtoepassing Hallo is opgeslagen.
1. Hallo app.ino bestand openen in Hallo app map in Hallo Arduino IDE.

   ![Hallo-voorbeeldtoepassing in Arduino IDE openen](media/iot-hub-arduino-huzzah-esp8266-get-started/10_arduino-ide-open-sample-app.png)

1. Klik in het Hallo Arduino IDE, op **bestand** > **voorkeuren**.
1. In Hallo **voorkeuren** dialoogvenster vak, klikt u op Hallo pictogram volgende toohello **extra Boards Manager-URL's** vak.
1. Voer in het pop-upvenster hello, Hallo URL te volgen en klik vervolgens op **OK**.

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![Url voor het pakket in Arduino IDE punt tooa](media/iot-hub-arduino-huzzah-esp8266-get-started/11_arduino-ide-package-url.png)

1. In Hallo **voorkeur** in het dialoogvenster, klikt u op **OK**.
1. Klik op **extra** > **mededelingenbord** > **Boards Manager**, en zoek vervolgens naar esp8266.

   Boards Manager geeft aan dat ESP8266 met een versie van 2.2.0 of hoger is geïnstalleerd.

   ![Hallo esp8266 pakket is geïnstalleerd](media/iot-hub-arduino-huzzah-esp8266-get-started/12_arduino-ide-esp8266-installed.png)

1. Klik op **extra** > **mededelingenbord** > **Adafruit HUZZAH ESP8266**.

### <a name="install-necessary-libraries"></a>Vereiste bibliotheken installeren

1. In Hallo Arduino IDE, klikt u op **schema** > **bibliotheek omvatten** > **bibliotheken beheren**.
1. Zoeken naar Hallo bibliotheeknamen, één voor één te volgen. Voor elke bibliotheek die u vindt, klikt u op **installeren**.
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a>Geen een echte DHT22 sensor?

Hallo-voorbeeldtoepassing kunt temperatuur en vochtigheid gegevens simuleren als u een echte DHT22 sensor geen hebt. tooset up Hallo toepassing toouse gesimuleerde voorbeeldgegevens, als volgt te werk:

1. Open Hallo `config.h` bestand in Hallo `app` map.
1. Zoek Hallo coderegel na en wijzig Hallo-waarde van `false` te`true`:
   ```c
   define SIMULATED_DATA true
   ```
   ![Toepassing hello-toouse gesimuleerde Voorbeeldgegevens configureren](media/iot-hub-arduino-huzzah-esp8266-get-started/13_arduino-ide-configure-app-use-simulated-data.png)

1. Hallo opslaan met `Control-s`.

### <a name="deploy-hello-sample-application-toofeather-huzzah-esp8266"></a>Hallo voorbeeld toepassing tooFeather HUZZAH ESP8266 implementeren

1. Klik in het Hallo Arduino IDE, op **hulpprogramma** > **poort**, en klik vervolgens op de seriële poort Hallo voor Doezelaar HUZZAH ESP8266.
1. Klik op **schema** > **uploaden** toobuild en Hallo voorbeeld toepassing tooFeather HUZZAH ESP8266 implementeren.

### <a name="enter-your-credentials"></a>Voer uw referenties in

Nadat het Hallo uploaden is voltooid, volgt u deze stappen tooenter uw referenties:

1. In Hallo Arduino IDE, klikt u op **extra** > **seriële Monitor**.
1. Let op Hallo twee vervolgkeuzelijsten in de rechterbenedenhoek Hallo in Hallo seriële monitor-venster.
1. Selecteer **er is geen afsluitende regel** voor Hallo links vervolgkeuzelijst.
1. Selecteer **115200 baud** voor Hallo rechts vervolgkeuzelijst.
1. Voer in Hallo-invoervak Hallo boven aan het venster seriële monitor Hallo Hallo volgende informatie als u wordt gevraagd tooprovide, en klik vervolgens op **verzenden**.
   * Wi-Fi-SSID
   * Wi-Fi-wachtwoord
   * Apparaat-verbindingsreeks

> [!Note]
> Hallo referentie-informatie wordt opgeslagen in Hallo EEPROM Doezelaar HUZZAH ESP8266. Als u op de herstelknop Hallo op Hallo Doezelaar HUZZAH ESP8266 mededelingenbord, desgewenst Hallo voorbeeldtoepassing tooerase Hallo informatie. Voer `Y` toohave Hallo informatie gewist. U wordt gevraagd tooprovide Hallo informatie een tweede keer.

### <a name="verify-hello-sample-application-is-running-successfully"></a>Controleer of de voorbeeldtoepassing Hallo correct wordt uitgevoerd

Als u ziet Hallo volgende de uitvoer van het venster seriële monitor Hallo en Hallo knipperende LED Doezelaar HUZZAH ESP8266, Hallo voorbeeldtoepassing correct wordt uitgevoerd.

![Uiteindelijke uitvoer Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a>Volgende stappen

U hebt een Doezelaar HUZZAH ESP8266 tooyour IoT-hub verbonden, en verzonden hello vastgelegd sensor gegevens tooyour IoT-hub. 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

