---
title: aaaSimulate een apparaat met Azure IoT rand (Linux) | Microsoft Docs
description: Hoe Azure IoT rand toouse op Linux toocreate een gesimuleerd apparaat dat telemetrie verzendt via een IoT Edge gateway tooan IoT-hub.
services: iot-hub
documentationcenter: 
author: chipalost
manager: timlt
editor: 
ms.assetid: 11e7bf28-ee3d-48d6-a386-eb506c7a31cf
ms.service: iot-hub
ms.devlang: cpp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/09/2017
ms.author: andbuc
ms.openlocfilehash: 168fb8eda8671d02c63073bdf36dfcd88b397fe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-iot-edge-toosend-device-to-cloud-messages-with-a-simulated-device-linux"></a>Gebruik Azure IoT rand toosend apparaat-naar-cloud-berichten met een gesimuleerd apparaat (Linux)

[!INCLUDE [iot-hub-iot-edge-simulated-selector](../../includes/iot-hub-iot-edge-simulated-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-toorun-hello-sample"></a>Hoe toorun voorbeeld Hallo

Hallo **build.sh** script genereert de uitvoer in Hallo **bouwen** map in het lokale exemplaar van Hallo **iot-edge** opslagplaats. Deze uitvoer bevat Hallo vier IoT Edge-modules die in dit voorbeeld worden gebruikt.

Hallo build script plaatsen de:

* **liblogger.so** in Hallo **modules-build-logboekregistratie** map.
* **libiothub.so** in Hallo **modules-build/iothub** map.
* **lib\_identiteit\_map.so** in Hallo **modules-build/identitymap** map.
* **libsimulated\_device.so** in Hallo **build, modules/gesimuleerde\_apparaat** map.

Gebruik deze paden voor Hallo **pad module** waarden zoals weergegeven in de volgende JSON-instellingenbestand Hallo:

Hallo gesimuleerde\_apparaat\_cloud\_uploaden\_Hallo pad tooa JSON-configuratiebestand als een opdrachtregelargument duurt dit voorbeeld. Hallo volgende voorbeeld van JSON-bestand vindt u in Hallo SDK opslagplaats op **voorbeelden\\gesimuleerde\_apparaat\_cloud\_uploaden\_voorbeeld\\src\\ gesimuleerde\_apparaat\_cloud\_uploaden\_voorbeeld\_lin.json**. Deze configuratie bestand werkt zoals tenzij u Hallo wijzigen build script tooplace Hallo IoT rand modules of uitvoerbare bestanden in niet-standaardlocaties steekproef.

> [!NOTE]
> Hallo module paden zijn relatieve toohello map van waaruit u Hallo gesimuleerde uitvoert\_apparaat\_cloud\_uploaden\_voorbeeld uitvoerbaar bestand, niet Hallo directory waar Hallo uitvoerbare bestand zich bevindt. Hallo JSON voorbeeldconfiguratiebestand standaard toowriting too'deviceCloudUploadGatewaylog.log' in de huidige werkmap.

Open Hallo-bestand in een teksteditor **samples/gesimuleerde\_apparaat\_cloud\_uploaden\_voorbeeld, src/gesimuleerde\_apparaat\_cloud\_uploaden\_lin.json** in het lokale exemplaar van Hallo **iot-edge** opslagplaats. Dit bestand configureert Hallo IoT rand modules in Hallo voorbeeld gateway:

* Hallo **IoTHub** module verbindt tooyour IoT-hub. U configureert toosend gegevens tooyour IoT-hub. In het bijzonder set Hallo **IoTHubName** toohello waardenaam van uw iothub en stel Hallo **IoTHubSuffix** waarde te**azure devices.net**. Set Hallo **Transport** tooone waarde van: **HTTP**, **AMQP**, of **MQTT**. Op dit moment alleen **HTTP** deelt een TCP-verbinding voor alle apparaatberichten. Als u de waarde hello te**AMQP**, of **MQTT**, Hallo gateway onderhoudt een afzonderlijke TCP-verbinding tooIoT Hub voor elk apparaat.
* Hallo **toewijzing** module Hallo MAC-adressen van uw gesimuleerde apparaten tooyour Iothub apparaat-id wordt toegewezen. Zorg ervoor dat **deviceId** waarden overeen Hallo-id's van de twee apparaten die u hebt toegevoegd tooyour iothub en die Hallo Hallo **deviceKey** waarden Hallo sleutels van de twee apparaten bevatten.
* Hallo **BLE1** en **BLE2** modules Hallo gesimuleerde apparaten zijn. Houd er rekening mee hoe hun MAC-adressen overeen adressen in Hallo Hallo **toewijzing** module.
* Hallo **berichtenlogboek** module Logboeken uw gateway activiteit tooa-bestand.
* Hallo **pad module** waarden wordt weergegeven in Hallo voorbeeld wordt ervan uitgegaan dat u Hallo-voorbeeld vanuit Hallo uitvoeren **bouwen** map in het lokale exemplaar van Hallo **iot-edge** opslagplaats.
* Hallo **koppelingen** matrix Hallo onderaan Hallo JSON-bestand in verbindt Hallo **BLE1** en **BLE2** modules toohello **toewijzing** -module en Hallo **toewijzing** module toohello **IoTHub** module. Dit zorgt er ook voor dat alle berichten worden vastgelegd door Hallo **berichtenlogboek** module.

```json
{
    "modules": [
        {
            "name": "IotHub",
          "loader": {
            "name": "native",
            "entrypoint": {
              "module.path": "./modules/iothub/libiothub.so"
            }
            },
            "args": {
              "IoTHubName": "<<insert here IoTHubName>>",
              "IoTHubSuffix": "<<insert here IoTHubSuffix>>",
              "Transport": "HTTP"
            }
          },
        {
            "name": "mapping",
          "loader": {
            "name": "native",
            "entrypoint": {
              "module.path": "./modules/identitymap/libidentity_map.so"
            }
            },
            "args": [
              {
                "macAddress": "01:01:01:01:01:01",
                "deviceId": "<<insert here deviceId>>",
                "deviceKey": "<<insert here deviceKey>>"
              },
              {
                "macAddress": "02:02:02:02:02:02",
                "deviceId": "<<insert here deviceId>>",
                "deviceKey": "<<insert here deviceKey>>"
              }
            ]
          },
        {
            "name": "BLE1",
          "loader": {
            "name": "native",
            "entrypoint": {
              "module.path": "./modules/simulated_device/libsimulated_device.so"
            }
            },
            "args": {
              "macAddress": "01:01:01:01:01:01"
            }
          },
        {
            "name": "BLE2",
          "loader": {
            "name": "native",
            "entrypoint": {
              "module.path": "./modules/simulated_device/libsimulated_device.so"
            }
            },
            "args": {
              "macAddress": "02:02:02:02:02:02"
            }
          },
        {
            "name": "Logger",
          "loader": {
            "name": "native",
            "entrypoint": {
              "module.path": "./modules/logger/liblogger.so"
            }
            },
            "args": {
              "filename": "deviceCloudUploadGatewaylog.log"
            }
          }
    ],
    "links": [
        {
            "source": "*",
            "sink": "Logger"
        },
        {
            "source": "BLE1",
            "sink": "mapping"
        },
        {
            "source": "BLE2",
            "sink": "mapping"
        },
        {
            "source": "mapping",
            "sink": "IotHub"
        }
    ]
}
```

U hebt aangebracht toohello configuratiebestand Hallo wijzigingen opslaan.

toorun Hallo-voorbeeld:

1. Navigeer in uw shell toohello **iot-rand/build** map.
2. Hallo volgende opdracht uitvoeren:
   
    ```sh
    ./samples/simulated_device_cloud_upload/simulated_device_cloud_upload_sample ../samples/simulated_device_cloud_upload/src/simulated_device_cloud_upload_lin.json
    ```
3. Kunt u Hallo [apparaat explorer] [ lnk-device-explorer] of [iothub explorer] [ lnk-iothub-explorer] toomonitor Hallo-berichten die IoT-hub van Hallo ontvangt hulpprogramma gateway. Bijvoorbeeld, kunt met iothub explorer u controleren met behulp van de volgende opdracht Hallo apparaat-naar-cloud-berichten:

    ```sh
    iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
    ```

## <a name="next-steps"></a>Volgende stappen

toogain een uitgebreidere kennis van Azure IoT rand en experiment met enkele codevoorbeelden, gaat u naar de volgende Hallo developer zelfstudies en bronnen:

* [Apparaat-naar-cloud-berichten verzenden vanaf een fysiek apparaat met Azure IoT rand][lnk-physical-device]
* [Azure IoT-rand][lnk-iot-edge]

toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:

* [Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide]
* [Uw IoT-oplossing van Hallo gemalen beveiligen][lnk-securing]

<!-- Links -->
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-physical-device]: iot-hub-iot-edge-physical-device.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md
