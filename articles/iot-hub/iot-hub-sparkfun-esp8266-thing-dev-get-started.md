---
title: aaaESP8266 toocloud - verbinding Sparkfun ESP8266 ding Dev tooAzure IoT Hub | Microsoft Docs
description: Meer informatie over hoe toosetup en verbinding Sparkfun ESP8266 ding Dev tooAzure IoT Hub voor toosend gegevens toohello Azure cloud-platform in deze zelfstudie.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 587fe292-9602-45b4-95ee-f39bba10e716
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 19b249df23b6df516634853521c6d532f51014da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-sparkfun-esp8266-thing-dev-tooazure-iot-hub-in-hello-cloud"></a>Verbinding maken met Sparkfun ESP8266 ding Dev tooAzure IoT-Hub in de cloud Hallo

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![verbinding tussen DHT22, wat Dev en IoT-Hub](media/iot-hub-sparkfun-thing-dev-get-started/1_connection-hdt22-thing-dev-iot-hub.png)

## <a name="what-you-will-do"></a>Wat u doet

Verbinding maken met Sparkfun ESP8266 ding Dev tooan IoT-hub die u maakt. Voer vervolgens een voorbeeld van toepassing op ESP8266 toocollect temperatuur en vochtigheid gegevens van een sensor DHT22. Ten slotte verzenden Hallo sensor gegevens tooyour IoT-hub.

> [!NOTE]
> Als u andere boards ESP8266 gebruikt, kunt u nog steeds de tooconnect van deze stappen volgen het tooyour IoT-hub. Afhankelijk van het mededelingenbord Hallo ESP8266 u gebruikt, moet u mogelijk tooreconfigure hello `LED_PIN`. Bijvoorbeeld, als u ESP8266 van AI Thinker gebruikt, u kunt wijzigen in `0` te`2`. Een kit nog geen hebt?: klik op [hier](http://azure.com/iotstarterkits)

## <a name="what-you-will-learn"></a>Wat u leert

* Hoe toocreate een IoT-hub en een apparaat registreren voor voor ding ontwikkelaars
* Hoe tooconnect ding Dev met Hallo sensoren en uw computer.
* Hoe toocollect sensorgegevens door het uitvoeren van een voorbeeld van toepassing op wat ontwikkelaars
* Hoe Hallo toosend sensor gegevens tooyour IoT-hub.

## <a name="what-you-will-need"></a>Wat u nodig hebt

![Onderdelen die nodig zijn voor Hallo-zelfstudie](media/iot-hub-sparkfun-thing-dev-get-started/2_parts-needed-for-the-tutorial.png)

toocomplete deze bewerking moet u volgende onderdelen van uw ding Developer Starter Kit Hallo:

* Hello Sparkfun ESP8266 ding Dev mededelingenbord.
* Een USB-Micro tooType een USB-kabel.

U moet ook de volgende Hallo voor uw ontwikkelomgeving:

* Een actief Azure-abonnement. Als u een Azure-account geen [maken van een gratis Azure-proefaccount](https://azure.microsoft.com/free/) over een paar minuten.
* Mac of PC met Windows of Ubuntu.
* Sparkfun ESP8266 ding Dev tooconnect voor draadloos netwerk.
* Internet verbinding toodownload Hallo-configuratiehulpprogramma.
* [Arduino IDE](https://www.arduino.cc/en/main/software) versie 1.6.8 (of nieuwer), eerdere versies werkt niet met Hallo AzureIoT-bibliotheek.

Hallo zijn volgende items optioneel als u een sensor geen hebt. U hebt ook Hallo-optie van het gebruik van gesimuleerde sensorgegevens.

* Een Adafruit DHT22-sensor van temperatuur en vochtigheid.
* Een breadboard.
* M/M meestal bedrading.

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-esp8266-thing-dev-with-hello-sensor-and-your-computer"></a>Verbinding maken met ESP8266 ding Dev met Hallo sensoren en uw computer

### <a name="connect-a-dht22-temperature-and-humidity-sensor-tooesp8266-thing-dev"></a>Verbinding maken met een DHT22 temperatuur en vochtigheid sensor tooESP8266 ding Dev

Hallo breadboard en meestal kabels toomake Hallo verbinding als volgt gebruiken. Als u geen een sensor, deze sectie overslaan omdat u gesimuleerde sensorgegevens in plaats daarvan kunt gebruiken.

![Verbindingen verwijzing](media/iot-hub-sparkfun-thing-dev-get-started/15_connections_on_breadboard.png)

Voor pincodes sensor, we Hallo bedrading volgende gebruiken:

| Start (Sensor)           | Einde (BMC)           | Kleur van de kabel   |
| -----------------------  | ---------------------- | ------------: |
| VDD (Pin 27F)            | 3v (8A pincode)           | Rode-kabel     |
| GEGEVENS (Pin 28 septies)           | GPIO 2 (9A pincode)       | Witte kabel    |
| GND (Pin 30F)            | GND (7J pincode)          | Zwarte kabel   |


- Zie voor meer informatie: [DHT22 sensor setup](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) en [Sparkfun ESP8266 ding Dev-specificatie](https://www.sparkfun.com/products/13711)

Nu moeten uw Sparkfun ESP8266 ding Dev zijn verbonden met een sensor werken.

![verbinding maken met dht22 met ESP8266 ding Dev](media/iot-hub-sparkfun-thing-dev-get-started/8_connect-dht22-thing-dev.png)

### <a name="connect-sparkfun-esp8266-thing-dev-tooyour-computer"></a>Verbind Sparkfun ESP8266 ding Dev tooyour computer

Hallo Micro USB tooType een USB-kabel tooconnect Sparkfun ESP8266 ding Dev tooyour computer als volgt gebruiken.

![Verbind Doezelaar huzzah tooyour computer](media/iot-hub-sparkfun-thing-dev-get-started/9_connect-thing-dev-computer.png)

### <a name="add-serial-port-permissions--ubuntu-only"></a>Machtigingen van de seriële poort – Ubuntu alleen toevoegen

Als u Ubuntu gebruikt, controleert u of dat een normale gebruiker heeft Hallo machtigingen toooperate op Hallo USB-poort van Sparkfun ESP8266 ding ontwikkelaars tooadd seriële poort machtigingen voor een normale gebruiker, als volgt te werk:

1. Voer Hallo opdrachten op een terminal te volgen:

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   Ophalen van een Hallo volgende uitvoer:

   * CRW-rw---1 hoofdmap uucp xxxxxxxx
   * CRW-rw---1 hoofdmap bellen xxxxxxxx

   In de uitvoer van Hallo kennisgeving `uucp` of `dialout` die Hallo eigenaar groepsnaam Hallo USB-poort.

1. Hallo-gebruikersgroep toohello door het uitvoeren van de volgende opdracht Hallo toevoegen:

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   `<group-owner-name>`Hallo eigenaar groepsnaam die u hebt verkregen is in de vorige stap Hallo. `<username>`uw gebruikersnaam Ubuntu is.

1. Ubuntu afmelden en deze opnieuw aanmelden voor Hallo wijziging tootake effect.

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a>Sensorgegevens verzamelen en deze tooyour IoT-hub te verzenden

In deze sectie kunt u gegevens kunt implementeren en uitvoeren van een voorbeeldtoepassing op Sparkfun ESP8266 ding ontwikkelaars Hallo-voorbeeldtoepassing Hallo LED Sparkfun ESP8266 ding Dev knippert en verzendt Hallo temperatuur en vochtigheid gegevens die worden verzameld van Hallo DHT22 sensor tooyour IoT-hub.

### <a name="get-hello-sample-application-from-github"></a>Hallo-voorbeeldtoepassing ophalen van GitHub

Hallo-voorbeeldtoepassing wordt gehost op GitHub. Kloon Hallo voorbeeld opslagplaats waarin de voorbeeldtoepassing Hallo vanuit GitHub. tooclone hello voorbeeld opslagplaats als volgt te werk:

1. Open een opdrachtprompt of een terminalvenster.
1. Ga tooa map waarin u Hallo voorbeeld toepassing toobe opgeslagen.
1. Hallo volgende opdracht uitvoeren:

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-SparkFun-ThingDev-client-app.git
   ```

Hallo-pakket voor Sparkfun ESP8266 ding Dev Arduino IDE installeren:

1. Open Hallo map waarin de voorbeeldtoepassing Hallo is opgeslagen.
1. Hallo app.ino bestand openen in Hallo app map in Arduino IDE.

   ![Hallo-voorbeeldtoepassing in arduino ide openen](media/iot-hub-sparkfun-thing-dev-get-started/10_arduino-ide-open-sample-app.png)

1. Klik in het Hallo Arduino IDE, op **bestand** > **voorkeuren**.
1. In Hallo **voorkeuren** dialoogvenster vak, klikt u op Hallo pictogram volgende toohello **extra Boards Manager-URL's** in het tekstvak.
1. Voer in het pop-upvenster hello, Hallo URL te volgen en klik vervolgens op **OK**.

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![url voor het pakket in arduino ide punt tooa](media/iot-hub-sparkfun-thing-dev-get-started/11_arduino-ide-package-url.png)

1. In Hallo **voorkeur** in het dialoogvenster, klikt u op **OK**.
1. Klik op **extra** > **mededelingenbord** > **Boards Manager**, en zoek vervolgens naar esp8266.
   ESP8266 met een versie van 2.2.0 of later moet worden geïnstalleerd.

   ![Hallo esp8266 pakket is geïnstalleerd](media/iot-hub-sparkfun-thing-dev-get-started/12_arduino-ide-esp8266-installed.png)

1. Klik op **extra** > **mededelingenbord** > **Sparkfun ESP8266 ding Dev**.

### <a name="install-necessary-libraries"></a>Vereiste bibliotheken installeren

1. In Hallo Arduino IDE, klikt u op **schema** > **bibliotheek omvatten** > **bibliotheken beheren**.
1. Zoeken naar Hallo bibliotheeknamen, één voor één te volgen. Voor elk Hallo-bibliotheek die u vindt, klikt u op **installeren**.
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a>Geen een echte DHT22 sensor?

Hallo-voorbeeldtoepassing kunt temperatuur en vochtigheid gegevens simuleren als u een echte DHT22 sensor geen hebt. tooenable hello toepassing toouse gesimuleerde voorbeeldgegevens, als volgt te werk:

1. Open Hallo `config.h` bestand in Hallo `app` map.
1. Zoek Hallo coderegel na en wijzig Hallo-waarde van `false` te`true`:
   ```c
   define SIMULATED_DATA true
   ```
   ![Toepassing hello-toouse gesimuleerde Voorbeeldgegevens configureren](media/iot-hub-sparkfun-thing-dev-get-started/13_arduino-ide-configure-app-use-simulated-data.png)
   
1. Sla met `Control-s`.

### <a name="deploy-hello-sample-application-toosparkfun-esp8266-thing-dev"></a>Hallo voorbeeld toepassing tooSparkfun ESP8266 ding Dev implementeren

1. Klik in het Hallo Arduino IDE, op **hulpprogramma** > **poort**, en klik vervolgens op de seriële poort Hallo voor voor Sparkfun ESP8266 ding ontwikkelaars
1. Klik op **schema** > **uploaden** toobuild en Hallo voorbeeld toepassing tooSparkfun ESP8266 ding ontwikkelaars implementeren

> [!Note]
> Als u Mac OS kan er waarschijnlijk Hallo volgende berichten tijdens het uploaden. `warning: espcomm_sync failed`,`error: espcomm_open failed`. Open uw ternimal-venster en voltooien hieronder acties toosolve dit probleem.
> ```bash
> cd /System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns
> sudo mv AppleUSBFTDI.kext AppleUSBFTDI.disabled
> sudo touch /System/Library/Extensions
> ```

### <a name="enter-your-credentials"></a>Voer uw referenties in

Na het Hallo uploaden is voltooid, voert u Hallo stappen tooenter uw referenties:

1. In Hallo Arduino IDE, klikt u op **extra** > **seriële Monitor**.
1. U ziet Hallo twee vervolgkeuzelijsten op Hallo rechterbenedenhoek in Hallo seriële monitor-venster.
1. Selecteer **er is geen afsluitende regel** voor Hallo links vervolgkeuzelijst.
1. Selecteer **115200 baud** voor Hallo rechts vervolgkeuzelijst.
1. Voer in Hallo-invoervak Hallo boven aan het venster seriële monitor Hallo Hallo volgende informatie als u wordt gevraagd tooprovide, en klik vervolgens op **verzenden**.
   * Wi-Fi-SSID
   * Wi-Fi-wachtwoord
   * Apparaat-verbindingsreeks

> [!Note]
> Hallo referentie-informatie wordt opgeslagen in Hallo EEPROM van Sparkfun ESP8266 ding ontwikkelaars Als u op de herstelknop Hallo op Hallo Sparkfun ESP8266 ding Dev mededelingenbord, Hallo voorbeeldtoepassing wordt u gevraagd als u wilt dat tooerase Hallo informatie. Voer `Y` toohave Hallo informatie gewist en wordt u gevraagd tooprovide Hallo gegevens opnieuw.

### <a name="verify-hello-sample-application-is-running-successfully"></a>Controleer of de voorbeeldtoepassing Hallo correct wordt uitgevoerd

Als u ziet Hallo volgende de uitvoer van het venster seriële monitor Hallo en Hallo knipperende LED Sparkfun ESP8266 ding Dev, Hallo voorbeeldtoepassing correct wordt uitgevoerd.

![uiteindelijke uitvoer arduino IDE](media/iot-hub-sparkfun-thing-dev-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a>Volgende stappen

U hebt een Sparkfun ESP8266 ding Dev tooyour IoT-hub verbonden en verzonden hello vastgelegd sensor gegevens tooyour IoT-hub. 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
