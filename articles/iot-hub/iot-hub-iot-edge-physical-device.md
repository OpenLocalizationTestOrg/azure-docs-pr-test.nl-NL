---
title: een fysiek apparaat met Azure IoT rand aaaUse | Microsoft Docs
description: Hoe toouse een Texas instrumenten SensorTag apparaat toosend tooan iothub via een IoT Edge gateway uitgevoerd op een apparaat frambozen Pi 3. Hallo-gateway is gebouwd met behulp van Azure IoT rand.
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 212dacbf-e5e9-48b2-9c8a-1c14d9e7b913
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: andbuc
ms.openlocfilehash: a2385accdbd99012ad094232653ee47d4e5c7839
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-on-a-raspberry-pi-tooforward-device-to-cloud-messages-tooiot-hub"></a>Gebruik Azure IoT-Edge van een frambozen Pi tooforward apparaat-naar-cloudberichten tooIoT Hub

In dit scenario Hallo [Bluetooth lage energie voorbeeld] [ lnk-ble-samplecode] laat u zien hoe toouse [Azure IoT rand] [ lnk-sdk] naar:

* Apparaat-naar-cloud telemetrie tooIoT Hub vanaf een fysiek apparaat doorsturen.
* Route-opdrachten van IoT Hub tooa fysieke apparaat.

Dit overzicht omvat:

* **Architectuur**: belangrijke architecturale informatie over Hallo Bluetooth lage energie-voorbeeld.
* **Bouwen en uitvoeren van**: Hallo stappen vereist toobuild en Voer Hallo-voorbeeld.

## <a name="architecture"></a>Architectuur

Hallo overzicht toont u hoe toobuild en voer een gateway aan de rand van IoT op een frambozen Pi 3 die wordt uitgevoerd Raspbian Linux. Hallo-gateway is gebouwd met behulp van IoT rand. Hallo-voorbeeld wordt een Texas instrumenten SensorTag Bluetooth laag energieverbruik (uitschakelen) toocollect temperatuur apparaatgegevens gebruikt.

Wanneer u Hallo rand IoT gateway uitvoert het:

* Maakt verbinding tooa SensorTag-apparaten met Hallo Bluetooth laag energieverbruik (uitschakelen)-protocol.
* TooIoT Hub verbinding maakt met behulp van Hallo HTTP-protocol.
* Telemetrie verzendt van Hallo SensorTag apparaat tooIoT Hub.
* Opdrachten van IoT Hub toohello SensorTag apparaat gestuurd.

Hallo gateway bevat Hallo IoT rand modules te volgen:

* Een *uitschakelen module* die met een Aanmeldingsprompt apparaat tooreceive temperatuur gegevens van Hallo-apparaat en verzenden opdrachten toohello apparaat-interfaces.
* Een *uitschakelen cloud toodevice module* die JSON berichten uit IoT Hub in uitschakelen instructies voor het Hallo vertaalt *uitschakelen module*.
* Een *berichtenlogboek module* die alle gateway berichten tooa lokaal bestand registreert.
* Een *identiteit toewijzing module* die tussen uitschakelen apparaat MAC-adressen en Azure IoT Hub apparaat-id's worden omgezet.
* Een *IoT Hub module* die uploadt telemetrie gegevens tooan IoT-hub en ontvangt van apparaatopdrachten van een IoT-hub.
* Een *uitschakelen printer module* die wordt geïnterpreteerd telemetrie van Hallo uitschakelen apparaat en wordt afgedrukt opgemaakte gegevens toohello console tooenable probleemoplossing en foutopsporing.

### <a name="how-data-flows-through-hello-gateway"></a>Hoe gegevens loopt via de gateway Hallo

Hallo volgende blokdiagram illustreert Hallo telemetrie uploaden van gegevensstroom pijplijn:

![Telemetrie uploaden gateway pijplijn](media/iot-hub-iot-edge-physical-device/gateway_ble_upload_data_flow.png)

Hallo-stappen waarmee een telemetrie-item van een apparaat uitschakelen tooIoT onderweg Hub zijn:

1. Hallo uitschakelen apparaat genereert een voorbeeld van een temperatuur en verzendt deze via Bluetooth-toohello uitschakelen module in het Hallo-gateway.
1. Hallo uitschakelen module Hallo voorbeeld ontvangt en publiceert deze toohello broker samen met de Hallo MAC-adres van apparaat Hallo.
1. Hallo identiteit toewijzing module dit bericht wordt opgehaald en maakt gebruik van een interne tabel tootranslate Hallo MAC-adres van apparaat Hallo in een IoT Hub apparaat-id. Een IoT Hub apparaat-id bestaat uit een apparaat-ID en de apparaatsleutel.
1. Hallo identiteit toewijzing module publiceert een nieuw bericht met Hallo temperatuur voorbeeldgegevens, Hallo MAC-adres van apparaat hello, Hallo apparaat-ID en Hallo apparaatsleutel.
1. Hallo IoT Hub-module ontvangt dit nieuwe bericht (gegenereerd door Hallo identiteit toewijzing module) en publiceert deze tooIoT Hub.
1. Hallo berichtenlogboek module registreert alle berichten van Hallo broker tooa lokaal bestand.

Hallo volgende blokdiagram illustreert Hallo apparaat opdracht gegevensstroom pijplijn:

![Apparaat opdracht gateway-pipeline](media/iot-hub-iot-edge-physical-device/gateway_ble_command_data_flow.png)

1. Hallo IoT Hub module periodiek Hallo iothub voor nieuwe opdracht-berichten.
1. Wanneer Hallo IoT Hub-module een nieuwe opdrachtbericht ontvangt, publiceert deze deze toohello broker.
1. Hallo identiteit toewijzing module opdracht het Hallo-bericht opgehaald en maakt gebruik van een interne tabel tootranslate Hallo IoT Hub apparaat-ID tooa apparaat MAC-adres. Vervolgens wordt een nieuw bericht met de MAC-adres van het doelapparaat Hallo Hallo in Hallo eigenschappen kaart van het Hallo-bericht gepubliceerd.
1. Hallo uitschakelen Cloud-naar-apparaat module neemt over dit bericht en zet deze om in Hallo juiste uitschakelen instructie voor Hallo uitschakelen module. Vervolgens wordt een nieuw bericht gepubliceerd.
1. Hallo uitschakelen module dit bericht wordt opgehaald en Hallo i/o-instructie worden uitgevoerd door te communiceren met de Hallo uitschakelen apparaat.
1. Hallo berichtenlogboek module registreert alle berichten van Hallo broker tooa schijf-bestand.

## <a name="prerequisites"></a>Vereisten

toocomplete in deze zelfstudie, moet u een actief Azure-abonnement.

> [!NOTE]
> Als u geen account hebt, kunt u binnen een paar minuten een account voor de gratis proefversie maken. Zie [Gratis proefversie van Azure][lnk-free-trial] voor meer informatie.

SSH-client moet u op uw computer tooenable u tooremotely access Hallo-opdracht regel op Hallo frambozen Pi.

- Windows bevat geen een SSH-client. Wordt u aangeraden [PuTTY](http://www.putty.org/).
- De meeste Linux-distributies en Mac OS bevatten Hallo SSH-opdrachtregelprogramma. Zie voor meer informatie [SSH met behulp van Linux- of Mac OS](https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md).

## <a name="prepare-your-hardware"></a>Bereid uw hardware

Deze zelfstudie wordt ervan uitgegaan dat u gebruikt een [Texas instrumenten SensorTag](http://www.ti.com/ww/en/wireless_connectivity/sensortag2015/index.html) apparaat verbonden tooa frambozen Pi 3 Raspbian uitgevoerd.

### <a name="install-raspbian"></a>Raspbian installeren

U kunt een Hallo opties tooinstall Raspbian volgen op uw apparaat frambozen Pi 3 gebruiken.

* tooinstall hello meest recente versie van Raspbian, gebruik Hallo [NOOBS] [ lnk-noobs] grafische gebruikersinterface.
* Handmatig [downloaden] [ lnk-raspbian] en schrijf Hallo nieuwste afbeelding van Hallo Raspbian besturingssysteem tooan SD-kaart.

### <a name="sign-in-and-access-hello-terminal"></a>Aanmelden en Hallo terminal

U hebt twee opties tooaccess een terminal-omgeving op uw Pi frambozen:

* Als u een toetsenbord hebt en verbonden tooyour frambozen Pi bewaken, kunt u Hallo Raspbian GUI tooaccess een terminalvenster gebruiken.

* Hallo opdrachtregel toegang op uw frambozen Pi gebruik van SSH op uw computer.

#### <a name="use-a-terminal-window-in-hello-gui"></a>Een terminalvenster in Hallo GUI gebruiken

Hallo standaardreferenties voor Raspbian zijn gebruikersnaam **pi** en het wachtwoord **frambozen**. In de taakbalk Hallo in Hallo GUI, kunt u Hallo starten **Terminal** hulpprogramma Hallo-pictogram dat op een monitor lijkt.

#### <a name="sign-in-with-ssh"></a>Meld u aan met SSH

U kunt SSH gebruiken voor toegang tot opdrachtregel tooyour frambozen Pi. Hallo artikel [SSH (Secure Shell)] [ lnk-pi-ssh] wordt beschreven hoe tooconfigure SSH op uw Pi frambozen en hoe tooconnect van [Windows] [ lnk-ssh-windows] of [Linux en Mac OS][lnk-ssh-linux].

Aanmelden met gebruikersnaam **pi** en het wachtwoord **frambozen**.

### <a name="install-bluez-537"></a>BlueZ 5.37 installeren

Hallo uitschakelen modules praten toohello Bluetooth-hardware via Hallo BlueZ stack. U moet versie 5.37 van BlueZ voor Hallo modules toowork correct. Deze instructies, Controleer of de juiste versie Hallo van BlueZ is geïnstalleerd.

1. Hallo huidige Bluetooth-daemon stoppen:

    ```sh
    sudo systemctl stop bluetooth
    ```

1. Hallo BlueZ afhankelijkheden installeren:

    ```sh
    sudo apt-get update
    sudo apt-get install bluetooth bluez-tools build-essential autoconf glib2.0 libglib2.0-dev libdbus-1-dev libudev-dev libical-dev libreadline-dev
    ```

1. Hallo BlueZ broncode downloaden van bluez.org:

    ```sh
    wget http://www.kernel.org/pub/linux/bluetooth/bluez-5.37.tar.xz
    ```

1. Pak de broncode Hallo:

    ```sh
    tar -xvf bluez-5.37.tar.xz
    ```

1. Mappen toohello nieuw gemaakte map wijzigen:

    ```sh
    cd bluez-5.37
    ```

1. Hallo BlueZ code toobe gebouwd configureren:

    ```sh
    ./configure --disable-udev --disable-systemd --enable-experimental
    ```

1. Bouw BlueZ:

    ```sh
    make
    ```

1. BlueZ installeren als deze is voltooid bouwcontract:

    ```sh
    sudo make install
    ```

1. Wijziging systemd-serviceconfiguratie voor Bluetooth-zodat deze toohello nieuwe Bluetooth-daemon in Hallo bestand verwijst `/lib/systemd/system/bluetooth.service`. Hallo 'ExecStart' regel vervangen door de volgende tekst hello:

    ```conf
    ExecStart=/usr/local/libexec/bluetooth/bluetoothd -E
    ```

### <a name="enable-connectivity-toohello-sensortag-device-from-your-raspberry-pi-3-device"></a>Connectiviteit toohello SensorTag apparaat vanaf uw apparaat frambozen Pi 3 inschakelen

Actieve Hallo-voorbeeld moet u eerst tooverify dat uw frambozen Pi 3 toohello SensorTag apparaat verbinding kan maken.

1. Zorg ervoor dat Hallo `rfkill` hulpprogramma is geïnstalleerd:

    ```sh
    sudo apt-get install rfkill
    ```

1. Blokkering opheffen van bluetooth op Hallo frambozen Pi 3 en controleer of het versienummer Hallo **5.37**:

    ```sh
    sudo rfkill unblock bluetooth
    bluetoothctl --version
    ```

1. tooenter hello interactieve Bluetooth-shell, start Hallo Bluetooth-service en Hallo uitvoeren **bluetoothctl** opdracht:

    ```sh
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. Voer de opdracht Hallo **inschakelopdrachten** toopower up Hallo Bluetooth-controller. Hallo opdracht retourneert de vergelijkbare toohello volgende uitvoer:

    ```sh
    [NEW] Controller 98:4F:EE:04:1F:DF C3 raspberrypi [default]
    ```

1. Hallo interactieve Bluetooth-shell, Voer Hallo opdracht **scannen op** tooscan voor Bluetooth-apparaten. Hallo opdracht retourneert de vergelijkbare toohello volgende uitvoer:

    ```sh
    Discovery started
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: yes
    ```

1. Hallo SensorTag apparaat detecteerbaar maken door Hallo kleine knop (hello groene LED moet flash) te drukken. Hallo frambozen Pi 3 moet Hallo SensorTag-apparaten detecteren:

    ```sh
    [NEW] Device A0:E6:F8:B5:F6:00 CC2650 SensorTag
    [CHG] Device A0:E6:F8:B5:F6:00 TxPower: 0
    [CHG] Device A0:E6:F8:B5:F6:00 RSSI: -43
    ```

    In dit voorbeeld ziet u dat Hallo MAC-adres van apparaat SensorTag Hallo **A0:E6:F8:B5:F6:00**.

1. Uitschakelen door te voeren Hallo scannen **scannen uitschakelen** opdracht:

    ```sh
    [CHG] Controller 98:4F:EE:04:1F:DF Discovering: no
    Discovery stopped
    ```

1. Verbinding maken met tooyour SensorTag-apparaten met behulp van het MAC-adres door te voeren **verbinding \<MAC-adres\>**. Hallo volgende voorbeelduitvoer wordt voor de duidelijkheid afgekort:

    ```sh
    Attempting tooconnect tooA0:E6:F8:B5:F6:00
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: yes
    Connection successful
    [CHG] Device A0:E6:F8:B5:F6:00 UUIDs: 00001800-0000-1000-8000-00805f9b34fb
    ...
    [NEW] Primary Service
            /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
            Device Information
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 GattServices: /org/bluez/hci0/dev_A0_E6_F8_B5_F6_00/service000c
    ...
    [CHG] Device A0:E6:F8:B5:F6:00 Name: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Alias: SensorTag 2.0
    [CHG] Device A0:E6:F8:B5:F6:00 Modalias: bluetooth:v000Dp0000d0110
    ```

    > Kunt u Hallo GATT kenmerken van Hallo-apparaat opnieuw met Hallo vermelden **lijst kenmerken** opdracht.

1. U kunt nu loskoppelen van Hallo Hallo apparaat **verbreken** opdracht en sluit vervolgens af vanuit Hallo Bluetooth-shell met Hallo **afsluiten** opdracht:

    ```sh
    Attempting toodisconnect from A0:E6:F8:B5:F6:00
    Successful disconnected
    [CHG] Device A0:E6:F8:B5:F6:00 Connected: no
    ```

U bent nu klaar toorun Hallo uitschakelen IoT rand voorbeeld op uw frambozen Pi 3.

## <a name="run-hello-iot-edge-ble-sample"></a>Hallo IoT rand uitschakelen voorbeeld uitvoeren

toorun hello IoT rand uitschakelen voorbeeld moet u drie taken toocomplete:

* Configureer twee voorbeeld-apparaten in uw IoT-Hub.
* IoT-Edge op uw apparaat frambozen Pi 3 bouwen.
* Configureer en Hallo uitschakelen voorbeeld uitvoeren op uw apparaat frambozen Pi 3.

Op moment van schrijven Hallo IoT Edge biedt alleen ondersteuning voor modules uitschakelen in gateways met op Linux.

### <a name="configure-two-sample-devices-in-your-iot-hub"></a>Twee voorbeeld-apparaten in uw IoT-Hub configureren

* [Een iothub maken] [ lnk-create-hub] in uw Azure-abonnement, moet u het Hallo-naam van uw hub toocomplete in dit scenario. Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.
* Toevoegen van een apparaat aangeroepen **SensorTag_01** tooyour IoT-hub en noteer de sleutel-id en het apparaat. Kunt u Hallo [apparaat explorer of iothub-explorer] [ lnk-explorer-tools] van hulpprogramma's voor tooadd dit apparaat toohello IoT-hub gemaakt in de vorige stap Hallo en tooretrieve de sleutel. U kunt dit apparaat toohello SensorTag apparaat toewijzen wanneer u Hallo gateway configureert.

### <a name="build-azure-iot-edge-on-your-raspberry-pi-3"></a>Azure IoT-rand bouwen op uw Raspberry Pi 3

Afhankelijkheden voor Azure IoT rand installeren:

```sh
sudo apt-get install cmake uuid-dev curl libcurl4-openssl-dev libssl-dev
```

Gebruik Hallo deze opdrachten tooclone IoT rand en alle bijbehorende submodules tooyour basismap:

```sh
cd ~
git clone https://github.com/Azure/iot-edge.git
```

Wanneer u een volledige kopie van Hallo IoT rand opslagplaats op uw frambozen Pi 3 hebt, kunt u met behulp van de volgende opdracht uit Hallo-map met de Hallo SDK Hallo bouwen:

```sh
cd ~/iot-edge
./tools/build.sh  --disable-native-remote-modules
```

### <a name="configure-and-run-hello-ble-sample-on-your-raspberry-pi-3"></a>Configureren en Hallo uitschakelen voorbeeld uitgevoerd op uw frambozen Pi 3

toobootstrap en Voer Hallo voorbeeld, moet u elke zijde van de IoT-module die deel uitmaakt in het Hallo-gateway configureren. Deze configuratie is opgegeven in een JSON-bestand en u moet alle vijf deelnemende IoT rand modules configureren. Er is een voorbeeld van een JSON-bestand in Hallo opslagplaats aangeroepen **gateway\_sample.json** die u als startpunt gebruiken kunt voor het bouwen van uw eigen configuratiebestand Hallo. Dit bestand bevindt zich in Hallo **ble_gateway/samples/src** map in de lokale kopie van Hallo IoT Edge-opslagplaats.

Hallo volgende secties wordt beschreven hoe tooedit deze configuratie voor Hallo uitschakelen voorbeeld en wordt ervan uitgegaan dat Hallo IoT Edge-opslagplaats is in Hallo **/home/pi/iot-edge /** map op uw frambozen Pi 3. Als Hallo opslag elders, overeenkomstig Hallo paden aanpassen.

#### <a name="logger-configuration"></a>Berichtenlogboek configuratie

Ervan uitgaande dat Hallo gateway opslagplaats bevindt zich in Hallo **/home/pi/iot-edge /** map Hallo berichtenlogboek module als volgt configureren:

```json
{
  "name": "Logger",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path" : "build/modules/logger/liblogger.so"
    }
  },
  "args":
  {
    "filename": "<</path/to/log-file.log>>"
  }
}
```

#### <a name="ble-module-configuration"></a>De moduleconfiguratie uitschakelen

Hallo voorbeeldconfiguratie voor Hallo uitschakelen apparaat wordt ervan uitgegaan dat een Texas instrumenten SensorTag-apparaat. Een standaard uitschakelen apparaat dat kan worden uitgevoerd als een randapparaat GATT moet werken, maar u tooupdate Hallo GATT kenmerk id's en -gegevens moet mogelijk. Hallo MAC-adres van uw apparaat SensorTag toevoegen:

```json
{
  "name": "SensorTag",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble.so"
    }
  },
  "args": {
    "controller_index": 0,
    "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
    "instructions": [
      {
        "type": "read_once",
        "characteristic_uuid": "00002A24-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A25-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A26-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A27-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A28-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "read_once",
        "characteristic_uuid": "00002A29-0000-1000-8000-00805F9B34FB"
      },
      {
        "type": "write_at_init",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AQ=="
      },
      {
        "type": "read_periodic",
        "characteristic_uuid": "F000AA01-0451-4000-B000-000000000000",
        "interval_in_ms": 1000
      },
      {
        "type": "write_at_exit",
        "characteristic_uuid": "F000AA02-0451-4000-B000-000000000000",
        "data": "AA=="
      }
    ]
  }
}
```

Als u een apparaat SensorTag niet gebruikt, raadpleegt u Hallo-documentatie voor uw apparaat uitschakelen toodetermine of u tooupdate Hallo GATT kenmerk id's en gegevenswaarden moet.

#### <a name="iot-hub-module"></a>IoT Hub-module

Hallo-naam van uw IoT-Hub toevoegen. Hallo-mailachtervoegselwaarde is doorgaans **azure devices.net**:

```json
{
  "name": "IoTHub",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/iothub/libiothub.so"
    }
  },
  "args": {
    "IoTHubName": "<<Azure IoT Hub Name>>",
    "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
    "Transport" : "amqp"
  }
}
```

#### <a name="identity-mapping-module-configuration"></a>Configuratie van de identiteit van toewijzing

Hallo MAC-adres van uw apparaat SensorTag en Hallo apparaat-ID en sleutel Hallo toevoegen **SensorTag_01** apparaat u tooyour IoT Hub hebt toegevoegd:

```json
{
  "name": "mapping",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/identitymap/libidentity_map.so"
    }
  },
  "args": [
    {
      "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
      "deviceId": "<<Azure IoT Hub Device ID>>",
      "deviceKey": "<<Azure IoT Hub Device Key>>"
    }
  ]
}
```

#### <a name="ble-printer-module-configuration"></a>Module printerconfiguratie uitschakelen

```json
{
  "name": "BLE Printer",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/samples/ble_gateway/ble_printer/libble_printer.so"
    }
  },
  "args": null
}
```

#### <a name="blec2d-module-configuration"></a>De Moduleconfiguratie BLEC2D

```json
{
  "name": "BLEC2D",
  "loader": {
    "name" : "native",
    "entrypoint" : {
      "module.path": "build/modules/ble/libble_c2d.so"
    }
  },
  "args": null
}
```

#### <a name="routing-configuration"></a>Configuratie van de routering

Hallo volgende configuratie zorgt er Hallo volgende routering tussen de rand van de IoT-modules:

* Hallo **berichtenlogboek** module ontvangt en registreert alle berichten.
* Hallo **SensorTag** module verzendt berichten tooboth hello **toewijzing** en **uitschakelen Printer** modules.
* Hallo **toewijzing** module verzendt berichten toohello **IoTHub** module toobe verzonden tooyour IoT Hub.
* Hallo **IoTHub** module verzendt berichten back-toohello **toewijzing** module.
* Hallo **toewijzing** module verzendt berichten toohello **BLEC2D** module.
* Hallo **BLEC2D** module verzendt berichten back-toohello **Sensor Tag** module.

```json
"links" : [
    {"source" : "*", "sink" : "Logger" },
    {"source" : "SensorTag", "sink" : "mapping" },
    {"source" : "SensorTag", "sink" : "BLE Printer" },
    {"source" : "mapping", "sink" : "IoTHub" },
    {"source" : "IoTHub", "sink" : "mapping" },
    {"source" : "mapping", "sink" : "BLEC2D" },
    {"source" : "BLEC2D", "sink" : "SensorTag"}
 ]
```

toorun hello voorbeeld pass Hallo pad toohello JSON-configuratiebestand als een parameter toohello **uitschakelen\_gateway** binaire. Hallo volgende opdracht wordt ervan uitgegaan dat u gebruikmaakt van Hallo **gateway_sample.json** configuratiebestand. Deze opdracht wordt uitgevoerd van Hallo **iot-edge** map op Hallo frambozen Pi:

```sh
./build/samples/ble_gateway/ble_gateway ./samples/ble_gateway/src/gateway_sample.json
```

Mogelijk moet u toopress Hallo kleine knop op Hallo SensorTag apparaat toomake deze kunnen worden gedetecteerd voordat u Hallo voorbeeld uitvoert.

Wanneer u Hallo voorbeeld uitvoert, kunt u Hallo [apparaat explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) of Hallo [iothub explorer](https://github.com/Azure/iothub-explorer) hulpprogramma toomonitor Hallo berichten Hallo gateway aan de rand van de IoT van Hallo SensorTag apparaat verzendt. Bijvoorbeeld, kunt met iothub explorer u controleren met behulp van de volgende opdracht Hallo apparaat-naar-cloud-berichten:

```sh
iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
```

## <a name="send-cloud-to-device-messages"></a>Cloud-naar-apparaat-berichten verzenden

Hallo uitschakelen module ondersteunt ook verzenden opdrachten uit IoT Hub toohello apparaat. Kunt u Hallo [apparaat explorer](https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer) of Hallo [iothub explorer](https://github.com/Azure/iothub-explorer) hulpprogramma toosend JSON berichten die module Hallo uitschakelen gateway stuurt op toohello uitschakelen apparaat.

Als u van Hallo Texas instrumenten SensorTag-apparaat gebruikmaakt, kunt u op Hallo rode LED, groene LED of alarm door opdrachten uit IoT Hub verzendt. Voordat u opdrachten uit IoT Hub verzendt, moet u eerst Hallo na twee JSON-berichten in volgorde sturen. U kunt vervolgens een van de Hallo opdrachten tooturn op Hallo lichten of alarm verzenden.

1. Opnieuw instellen van alle LED's en Hallo alarm (deze uit te schakelen):

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AA=="
    }
    ```

1. I/o's configureren als 'extern':

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA66-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

U kunt nu een Hallo opdrachten tooturn volgen op Hallo lichten of alarm op Hallo SensorTag apparaat verzenden:

* Hallo rode LED inschakelen:

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "AQ=="
    }
    ```

* Hallo groen LED inschakelen:

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "Ag=="
    }
    ```

* Hallo alarm inschakelen:

    ```json
    {
      "type": "write_once",
      "characteristic_uuid": "F000AA65-0451-4000-B000-000000000000",
      "data": "BA=="
    }
    ```

## <a name="next-steps"></a>Volgende stappen

Als u toogain een uitgebreidere kennis van IoT-rand wilt en Experimenteer met enkele codevoorbeelden, gaat u naar de volgende Hallo developer zelfstudies en bronnen:

* [Azure IoT-rand][lnk-sdk]

toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:

* [Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide]

<!-- Links -->
[lnk-ble-samplecode]: https://github.com/Azure/iot-edge/tree/master/samples/ble_gateway
[lnk-free-trial]: https://azure.microsoft.com/pricing/free-trial/
[lnk-explorer-tools]: https://github.com/Azure/azure-iot-sdks/blob/master/doc/manage_iot_hub.md
[lnk-sdk]: https://github.com/Azure/iot-edge/
[lnk-noobs]: https://www.raspberrypi.org/documentation/installation/noobs.md
[lnk-raspbian]: https://www.raspberrypi.org/downloads/raspbian/
[lnk-devguide]: iot-hub-devguide.md
[lnk-create-hub]: iot-hub-create-through-portal.md 
[lnk-pi-ssh]: https://www.raspberrypi.org/documentation/remote-access/ssh/README.md
[lnk-ssh-windows]: https://www.raspberrypi.org/documentation/remote-access/ssh/windows.md
[lnk-ssh-linux]: https://www.raspberrypi.org/documentation/remote-access/ssh/unix.md
