---
title: een gateway tooAzure IoT-Suite met een Intel NUC aaaConnect | Microsoft Docs
description: "Gebruik Hallo Microsoft IoT commerciële Gateway Kit en Hallo vooraf geconfigureerde oplossing voor externe controle. Gebruik hello Azure IoT Edge gateway tooconnect toohello oplossing voor externe controle, gesimuleerde telemetrie toohello cloud verzenden en reageren toomethods aangeroepen vanuit Hallo oplossing dashboard."
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
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: 46b545fc21b054191c8f78ace20fc628f839a819
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-azure-iot-edge-gateway-toohello-remote-monitoring-preconfigured-solution-and-send-simulated-telemetry"></a>Verbinding maken met uw vooraf geconfigureerde oplossing voor externe controle rand van Azure IoT gateway toohello en gesimuleerde telemetrie verzenden

[!INCLUDE [iot-suite-gateway-kit-selector](../../includes/iot-suite-gateway-kit-selector.md)]

Deze zelfstudie leert u hoe toouse Azure IoT rand toosimulate temperatuur en vochtigheid gegevens toosend toohello externe controle vooraf oplossing geconfigureerde. Hallo-zelfstudie wordt gebruikt:

- Azure IoT rand tooimplement een voorbeeld-gateway.
- Hallo IoT Suite remote monitoring vooraf geconfigureerde oplossing als Hallo cloud-gebaseerde back-end.

## <a name="overview"></a>Overzicht

In deze zelfstudie maakt uitvoeren u Hallo stappen:

- Implementeer een exemplaar van Hallo externe controle vooraf geconfigureerde oplossing tooyour Azure-abonnement. Deze stap implementeert automatisch en meerdere Azure-services configureert.
- Stel uw toocommunicate Intel NUC gateway-apparaat met de computer en het Hallo-oplossing voor externe controle.
- Hallo rand IoT gateway toosend gesimuleerde telemetrie die u op het dashboard van de oplossing Hallo weergeven kunt configureren.

[!INCLUDE [iot-suite-gateway-kit-prerequisites](../../includes/iot-suite-gateway-kit-prerequisites.md)]

[!INCLUDE [iot-suite-provision-remote-monitoring](../../includes/iot-suite-provision-remote-monitoring.md)]

> [!WARNING]
> Hallo externe controle van de bepalingen van de oplossing voor een verzameling Azure-services in uw Azure-abonnement. Hallo implementatie duidt op een echte enterprise-architectuur. tooavoid onnodige Azure-verbruik kosten, verwijderen van uw exemplaar van Hallo vooraf geconfigureerde oplossing op azureiotsuite.com wanneer u klaar bent met het. Als u moet de vooraf geconfigureerde oplossing opnieuw hello, u kunt gemakkelijk het opnieuw maken. Zie voor meer informatie over het verminderen van verbruik tijdens het Hallo voor externe controle van de oplossing wordt uitgevoerd, [configureren van Azure IoT Suite vooraf geconfigureerde oplossingen voor demonstratiedoeleinden][lnk-demo-config].

[!INCLUDE [iot-suite-gateway-kit-view-solution](../../includes/iot-suite-gateway-kit-view-solution.md)]

Herhaal de vorige stappen tooadd Hallo een tweede apparaat met een apparaat-ID, zoals **device02**. Hallo-voorbeeld worden gegevens verzonden van twee gesimuleerde apparaten Hallo gateway toohello oplossing voor externe controle.

[!INCLUDE [iot-suite-gateway-kit-prepare-nuc-connectivity](../../includes/iot-suite-gateway-kit-prepare-nuc-connectivity.md)]

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
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
chmod u+x build.sh
sed -i -e 's/\r$//' build.sh
./build.sh
```

Hallo build script Hallo libsimulator.so aangepaste IoT rand module in Hallo build-map geplaatst.

## <a name="configure-and-run-hello-iot-edge-gateway"></a>Configureren en uitvoeren van Hallo rand IoT gateway

U kunt nu Hallo rand IoT gateway toosend gesimuleerde telemetrie tooyour dashboard externe controle configureren. Zie voor meer informatie over het configureren van een gateway en de rand van de IoT-modules [Azure IoT rand concepten][lnk-gateway-concepts].

> [!TIP]
> In deze zelfstudie gebruikt u Hallo standaard `vi` teksteditor op Hallo Intel NUC. Als u niet hebt gebruikt `vi` , moet u een inleidende zelfstudie, zoals uitvoeren [Unix - Hallo vi zelfstudie Editor] [ lnk-vi-tutorial] toofamiliarize uzelf met deze editor. U kunt ook installeren Hallo gebruikersvriendelijker [nano](https://www.nano-editor.org/) editor met Hallo opdracht `smart install nano -y`.

Open Hallo voorbeeldconfiguratiebestand in Hallo **vi** editor met behulp van de volgende opdracht Hallo:

```bash
vi ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator/remote_monitoring.json
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
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  },
  {
    "macAddress": "AA:BB:CC:DD:EE:FF",
    "deviceId": "<<Azure IoT Hub Device ID>>",
    "deviceKey": "<<Azure IoT Hub Device Key>>"
  }
]
```

Vervang Hallo **deviceID** en **deviceKey** tijdelijke aanduidingen door Hallo-id's en sleutels voor Hallo twee apparaten die u eerder in het Hallo-oplossing voor externe controle hebt gemaakt.

Sla uw wijzigingen op.

U kunt nu Hallo gateway aan de rand van de IoT Hallo volgen met de opdrachten uitvoeren:

```bash
cd ~/iot-remote-monitoring-c-intel-nuc-gateway-getting-started/simulator
/usr/share/azureiotgatewaysdk/samples/simulated_device_cloud_upload/simulated_device_cloud_upload remote_monitoring.json
```

Hallo-gateway op Hallo Intel NUC gestart en verzendt gesimuleerde telemetrie toohello oplossing voor externe controle:

![Gateway aan de rand van de IoT gesimuleerde telemetrie genereert][img-simulated telemetry]

Druk op **Ctrl-C** tooexit Hallo programma op elk gewenst moment.

## <a name="view-hello-telemetry"></a>Hallo telemetrie van paginaweergaven

Hallo rand IoT gateway verzendt nu gesimuleerde telemetrie toohello oplossing voor externe controle. U kunt Hallo telemetrie weergeven op Hallo oplossing dashboard.

- Navigeer toohello oplossing dashboard.
- Selecteer een van Hallo twee apparaten die u hebt geconfigureerd in de gateway in Hallo Hallo **apparaat tooView** vervolgkeuzelijst.
- Hallo telemetrie van Hallo gatewayapparaten wordt weergegeven op Hallo-dashboard.

![Telemetrie weergegeven van Hallo gesimuleerde gateway-apparaten][img-telemetry-display]

> [!WARNING]
> Als u Hallo oplossing uitgevoerd in uw Azure-account voor externe controle laat, wordt u gefactureerd voor Hallo keer die wordt uitgevoerd. Zie voor meer informatie over het verminderen van verbruik tijdens het Hallo voor externe controle van de oplossing wordt uitgevoerd, [configureren van Azure IoT Suite vooraf geconfigureerde oplossingen voor demonstratiedoeleinden][lnk-demo-config]. Hallo vooraf geconfigureerde oplossing uit uw Azure-account verwijderen wanneer u klaar bent met het gebruik van maken.

## <a name="next-steps"></a>Volgende stappen

Ga naar Hallo [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) voor meer voorbeelden en documentatie over Azure IoT.

[img-simulated telemetry]: ./media/iot-suite-gateway-kit-get-started-simulator/appoutput.png

[img-telemetry-display]: ./media/iot-suite-gateway-kit-get-started-simulator/telemetry.png

[lnk-demo-config]: https://github.com/Azure/azure-iot-remote-monitoring/blob/master/Docs/configure-preconfigured-demo.md

[lnk-vi-tutorial]: http://www.tutorialspoint.com/unix/unix-vi-editor.htm
[lnk-gateway-concepts]: https://docs.microsoft.com/azure/iot-hub/iot-hub-linux-iot-edge-get-started