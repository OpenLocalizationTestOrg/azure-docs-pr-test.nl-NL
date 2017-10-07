---
title: een gateway tooAzure IoT-Suite met een Intel NUC aaaConnect | Microsoft Docs
description: "Gebruik Hallo Microsoft IoT commerciële Gateway Kit en Hallo vooraf geconfigureerde oplossing voor externe controle. Hallo rand van Azure IoT gateway tooenable gebruiken een oplossing voor externe controle van SensorTag apparaat tooconnect toohello, verzenden van telemetrie toohello cloud en toomethods aangeroepen vanuit het dashboard van de oplossing Hallo reageren."
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.openlocfilehash: 6f98ee3c1e2311a8644da9d72d40e671e7cbcf00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-telemetry-from-a-sensortag"></a>Verbinding maken met uw vooraf geconfigureerde oplossing voor externe controle rand van Azure IoT gateway toohello en verzend telemetrie vanuit een SensorTag

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

Deze zelfstudie laat zien hoe Azure IoT rand toosend temperatuur en vochtigheid gegevens uit SensorTag apparaat toohello externe controle toouse vooraf geconfigureerde oplossing. Hallo SensorTag verbindt toohello Intel NUC gateway via Bluetooth. Hallo-zelfstudie wordt gebruikt:

- Azure IoT rand tooimplement een voorbeeld-gateway.
- Hallo IoT Suite remote monitoring vooraf geconfigureerde oplossing als Hallo cloud-gebaseerde back-end.

## <a name="overview"></a>Overzicht

In deze zelfstudie maakt uitvoeren u Hallo stappen:

- Implementeer een exemplaar van Hallo externe controle vooraf geconfigureerde oplossing tooyour Azure-abonnement. Deze stap implementeert automatisch en meerdere Azure-services configureert.
- Stel uw toocommunicate Intel NUC gateway-apparaat met de computer en het Hallo-oplossing voor externe controle.
- Instellen van uw Intel NUC gateway tooreceive telemetrie vanaf een apparaat SensorTag en verzend het toohello voor externe controle dashboard.

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[Texas instrumenten uitschakelen SensorTag][lnk-sensortag]. Deze zelfstudie haalt telemetrische gegevens via Bluetooth van Hallo SensorTag-apparaten.

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Hallo externe controle van de bepalingen van de oplossing voor een verzameling Azure-services in uw Azure-abonnement. Hallo implementatie duidt op een echte enterprise-architectuur. tooavoid onnodige Azure-verbruik kosten, verwijderen van uw exemplaar van Hallo vooraf geconfigureerde oplossing op azureiotsuite.com wanneer u klaar bent met het. Als u moet de vooraf geconfigureerde oplossing opnieuw hello, u kunt gemakkelijk het opnieuw maken. Zie voor meer informatie over het verminderen van verbruik tijdens het Hallo voor externe controle van de oplossing wordt uitgevoerd, [configureren van Azure IoT Suite vooraf geconfigureerde oplossingen voor demonstratiedoeleinden][lnk-demo-config].

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

## <a name="configure-bluetooth-connectivity"></a>Bluetooth-connectiviteit configureren

Configureren van Bluetooth op Hallo Intel NUC tooenable hello SensorTag apparaat tooconnect en verzenden van telemetrie.

### <a name="find-hello-mac-address-of-hello-sensortag"></a>MAC-adres Hallo Hallo SensorTag zoeken

1. Hallo-shell op Hallo Intel NUC, start Hallo opdracht toounblock Hallo Bluetooth-service te volgen:

    ```bash
    sudo rfkill unblock bluetooth
    ```

1. Voer Hallo volgende toostart Hallo Bluetooth-service op Hallo Intel NUC opdrachten en Voer Hallo Bluetooth-shell:

    ```bash
    sudo systemctl start bluetooth
    bluetoothctl
    ```

1. Voer Hallo opdracht toopower op Hallo Bluetooth-domeincontroller te volgen:

    ```bash
    power on
    ```

    Als het Hallo-controller is ingeschakeld, ziet u een bericht **power wijzigen op geslaagd**.

1. Voer Hallo opdracht tooscan voor Bluetooth-apparaten in de buurt te volgen:

    ```bash
    scan on
    ```

1. Druk op Hallo power knop op Hallo SensorTag toomake deze kunnen worden gedetecteerd. Hallo groen LED knippert.

1. Wanneer er een bericht verschijnt in de shell Hallo Hallo controller Hallo SensorTag heeft gedetecteerd, noteer Hallo MAC-adres van het Hallo-apparaat. Hallo MAC-adres ziet eruit als **A0:E6:F8:B5:F6:00**. U moet Hallo MAC-adres verderop in de zelfstudie Hallo wanneer u Hallo gateway configureert.

1. Voer Hallo opdracht tooturn Bluetooth scannen uit te volgen:

    ```bash
    scan off
    ```

1. Hallo na de opdracht tooverify of toohello SensorTag apparaat verbinding kan worden uitgevoerd:

    ```bash
    connect <SensorTag MAC address>
    ```

    Als u verbinding met succes maakt, Hallo shell ziet u het Hallo-bericht **verbinding tot stand gebracht** en informatie over Hallo SensorTag-apparaat wordt afgedrukt. Als u geen verbinding maken, controleert u Hallo die sensortag nog steeds is ingeschakeld.

1. U kunt nu Hallo SensorTag verbreken en Hallo Bluetooth-shell afsluiten door te voeren Hallo volgende opdrachten:

    ```bash
    disconnect
    exit
    ```

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-software](../../includes/iot-suite-gateway-kit-prepare-nuc-software.md)]

## <a name="build-hello-custom-iot-edge-module"></a>Hallo aangepaste IoT Edge-module maken

U kunt nu Hallo aangepaste IoT Edge-module maken waarmee Hallo gateway toosend berichten toohello oplossing voor externe controle. Zie voor meer informatie over het configureren van een gateway en de rand van de IoT-modules [Azure IoT rand concepten][lnk-gateway-concepts].

Download de broncode Hallo voor aangepaste modules die IoT rand Hallo vanuit GitHub Hallo volgende opdrachten gebruiken:

```bash
cd ~
git clone https://github.com/Azure-Samples/iot-remote-monitoring-c-intel-nuc-gateway-getting-started.git
```

Hallo aangepaste IoT Edge-module met behulp van de volgende opdrachten Hallo maken:

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

Hallo build script Hallo libsensor2remotemonitoring.so aangepaste IoT rand module in Hallo build-map geplaatst.

## <a name="configure-and-run-hello-iot-edge-gateway"></a>Configureren en uitvoeren van Hallo rand IoT gateway

U kunt nu Hallo rand IoT gateway toosend telemetrie van uw externe controle dashboard SensorTag apparaat tooyour configureren. Zie voor meer informatie over het configureren van een gateway en de rand van de IoT-modules [Azure IoT rand concepten][lnk-gateway-concepts].

> [!TIP]
> In deze zelfstudie gebruikt u Hallo standaard `vi` teksteditor op Hallo Intel NUC. Als u niet hebt gebruikt `vi` , moet u een inleidende zelfstudie, zoals uitvoeren [Unix - Hallo vi zelfstudie Editor] [ lnk-vi-tutorial] toofamiliarize uzelf met deze editor. U kunt ook installeren Hallo gebruikersvriendelijker [nano](https://www.nano-editor.org/) editor met Hallo opdracht `smart install nano -y`.

Open Hallo voorbeeldconfiguratiebestand in Hallo **vi** editor met behulp van de volgende opdracht Hallo:

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic/remote_monitoring.json
```

Zoek de volgende regels in de configuratie voor Hallo IoTHub module Hallo Hallo:

```json
"args": {
  "IoTHubName": "<<Azure IoT Hub Name>>",
  "IoTHubSuffix": "<<Azure IoT Hub Suffix>>",
  "Transport": "http"
}
```

Hallo-tijdelijke aanduiding voor waarden met IoT Hub informatie u gemaakt en opgeslagen op Hallo Hallo begin van deze zelfstudie wordt vervangen. Hallo-waarde voor IoTHubName eruit **yourrmsolution37e08**, en het Hallo-waarde voor IoTSuffix is doorgaans **azure devices.net**.

Zoek de volgende regels in de configuratie voor Hallo toewijzing module Hallo Hallo:

```json
args": [
  {
    "macAddress": "<<AA:BB:CC:DD:EE:FF>>",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

Vervang Hallo **macAddress** aanduiding voor items met Hallo MAC-adres van uw SensorTag die u eerder hebt genoteerd. Vervang Hallo **deviceID** en **deviceKey** tijdelijke aanduidingen door Hallo-id's en sleutels voor Hallo twee apparaten die u eerder in het Hallo-oplossing voor externe controle hebt gemaakt.

Zoek de volgende regels in de configuratie voor Hallo SensorTag module Hallo Hallo:

```json
"args": {
  "controller_index": 0,
  "device_mac_address": "<<AA:BB:CC:DD:EE:FF>>",
  ...
}
```

Vervang Hallo **apparaat\_mac\_adres** aanduiding voor items met Hallo MAC-adres van uw SensorTag die u eerder hebt genoteerd.

Sla uw wijzigingen op.

U kunt nu uitvoeren met behulp van de volgende opdrachten Hallo Hallo-gateway:

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/basic
/usr/share/azureiotgatewaysdk/samples/ble_gateway/ble_gateway remote_monitoring.json
```

Hallo gateway aan de rand van IoT op Hallo Intel NUC gestart en verzendt telemetrie van Hallo SensorTag toohello oplossing voor externe controle:

![Rand IoT gateway verzendt telemetrie van Hallo SensorTag][img-telemetry]

Druk op **Ctrl-C** tooexit Hallo programma op elk gewenst moment.

## <a name="view-hello-telemetry"></a>Hallo telemetrie van paginaweergaven

Hallo gateway verzendt nu telemetrie vanaf Hallo SensorTag apparaat toohello oplossing voor externe controle. U kunt Hallo telemetrie weergeven op Hallo oplossing dashboard. U kunt ook opdrachten tooyour SensorTag-apparaten via de gateway Hallo verzenden vanuit Hallo oplossing dashboard.

- Navigeer toohello oplossing dashboard.
- Selecteer Hallo apparaat u hebt geconfigureerd in het Hallo-gateway met Hallo SensorTag in Hallo **apparaat tooView** vervolgkeuzelijst.
- Hallo telemetrie van Hallo SensorTag-apparaten wordt weergegeven op Hallo-dashboard.

![Telemetrie weergegeven van Hallo SensorTag-apparaten][img-telemetry-display]

> [!WARNING]
> Als u Hallo oplossing uitgevoerd in uw Azure-account voor externe controle laat, wordt u gefactureerd voor Hallo keer die wordt uitgevoerd. Zie voor meer informatie over het verminderen van verbruik tijdens het Hallo voor externe controle van de oplossing wordt uitgevoerd, [configureren van Azure IoT Suite vooraf geconfigureerde oplossingen voor demonstratiedoeleinden][lnk-demo-config]. Hallo vooraf geconfigureerde oplossing uit uw Azure-account verwijderen wanneer u klaar bent met het gebruik van maken.


## <a name="next-steps"></a>Volgende stappen

Ga naar Hallo [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) voor meer voorbeelden en documentatie over Azure IoT.

[img-telemetry]: ./media/iot-suite-gateway-kit-get-started-sensortag/appoutput.png


[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-sensortag/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md
[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-sensortag]: http://www.ti.com/ww/en/wireless_connectivity/sensortag/
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started