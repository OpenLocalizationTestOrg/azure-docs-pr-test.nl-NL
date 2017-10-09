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
# <a name="use-azure-iot-edge-toosend-device-to-cloud-messages-with-a-simulated-device-linux"></a><span data-ttu-id="d54cc-103">Gebruik Azure IoT rand toosend apparaat-naar-cloud-berichten met een gesimuleerd apparaat (Linux)</span><span class="sxs-lookup"><span data-stu-id="d54cc-103">Use Azure IoT Edge toosend device-to-cloud messages with a simulated device (Linux)</span></span>

[!INCLUDE [iot-hub-iot-edge-simulated-selector](../../includes/iot-hub-iot-edge-simulated-selector.md)]

[!INCLUDE [iot-hub-iot-edge-install-build-linux](../../includes/iot-hub-iot-edge-install-build-linux.md)]

## <a name="how-toorun-hello-sample"></a><span data-ttu-id="d54cc-104">Hoe toorun voorbeeld Hallo</span><span class="sxs-lookup"><span data-stu-id="d54cc-104">How toorun hello sample</span></span>

<span data-ttu-id="d54cc-105">Hallo **build.sh** script genereert de uitvoer in Hallo **bouwen** map in het lokale exemplaar van Hallo **iot-edge** opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="d54cc-105">hello **build.sh** script generates its output in hello **build** folder in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="d54cc-106">Deze uitvoer bevat Hallo vier IoT Edge-modules die in dit voorbeeld worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d54cc-106">This output includes hello four IoT Edge modules used in this sample.</span></span>

<span data-ttu-id="d54cc-107">Hallo build script plaatsen de:</span><span class="sxs-lookup"><span data-stu-id="d54cc-107">hello build script places the:</span></span>

* <span data-ttu-id="d54cc-108">**liblogger.so** in Hallo **modules-build-logboekregistratie** map.</span><span class="sxs-lookup"><span data-stu-id="d54cc-108">**liblogger.so** in hello **build/modules/logger** folder.</span></span>
* <span data-ttu-id="d54cc-109">**libiothub.so** in Hallo **modules-build/iothub** map.</span><span class="sxs-lookup"><span data-stu-id="d54cc-109">**libiothub.so** in hello **build/modules/iothub** folder.</span></span>
* <span data-ttu-id="d54cc-110">**lib\_identiteit\_map.so** in Hallo **modules-build/identitymap** map.</span><span class="sxs-lookup"><span data-stu-id="d54cc-110">**lib\_identity\_map.so** in hello **build/modules/identitymap** folder.</span></span>
* <span data-ttu-id="d54cc-111">**libsimulated\_device.so** in Hallo **build, modules/gesimuleerde\_apparaat** map.</span><span class="sxs-lookup"><span data-stu-id="d54cc-111">**libsimulated\_device.so** in hello **build/modules/simulated\_device** folder.</span></span>

<span data-ttu-id="d54cc-112">Gebruik deze paden voor Hallo **pad module** waarden zoals weergegeven in de volgende JSON-instellingenbestand Hallo:</span><span class="sxs-lookup"><span data-stu-id="d54cc-112">Use these paths for hello **module path** values as shown in hello following JSON settings file:</span></span>

<span data-ttu-id="d54cc-113">Hallo gesimuleerde\_apparaat\_cloud\_uploaden\_Hallo pad tooa JSON-configuratiebestand als een opdrachtregelargument duurt dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="d54cc-113">hello simulated\_device\_cloud\_upload\_sample process takes hello path tooa JSON configuration file as a command-line argument.</span></span> <span data-ttu-id="d54cc-114">Hallo volgende voorbeeld van JSON-bestand vindt u in Hallo SDK opslagplaats op **voorbeelden\\gesimuleerde\_apparaat\_cloud\_uploaden\_voorbeeld\\src\\ gesimuleerde\_apparaat\_cloud\_uploaden\_voorbeeld\_lin.json**.</span><span class="sxs-lookup"><span data-stu-id="d54cc-114">hello following example JSON file is provided in hello SDK repository at **samples\\simulated\_device\_cloud\_upload\_sample\\src\\simulated\_device\_cloud\_upload\_sample\_lin.json**.</span></span> <span data-ttu-id="d54cc-115">Deze configuratie bestand werkt zoals tenzij u Hallo wijzigen build script tooplace Hallo IoT rand modules of uitvoerbare bestanden in niet-standaardlocaties steekproef.</span><span class="sxs-lookup"><span data-stu-id="d54cc-115">This configuration file works as is unless you modify hello build script tooplace hello IoT Edge modules or sample executables in non-default locations.</span></span>

> [!NOTE]
> <span data-ttu-id="d54cc-116">Hallo module paden zijn relatieve toohello map van waaruit u Hallo gesimuleerde uitvoert\_apparaat\_cloud\_uploaden\_voorbeeld uitvoerbaar bestand, niet Hallo directory waar Hallo uitvoerbare bestand zich bevindt.</span><span class="sxs-lookup"><span data-stu-id="d54cc-116">hello module paths are relative toohello directory from where you run hello simulated\_device\_cloud\_upload\_sample executable, not hello directory where hello executable is located.</span></span> <span data-ttu-id="d54cc-117">Hallo JSON voorbeeldconfiguratiebestand standaard toowriting too'deviceCloudUploadGatewaylog.log' in de huidige werkmap.</span><span class="sxs-lookup"><span data-stu-id="d54cc-117">hello sample JSON configuration file defaults toowriting too'deviceCloudUploadGatewaylog.log' in your current working directory.</span></span>

<span data-ttu-id="d54cc-118">Open Hallo-bestand in een teksteditor **samples/gesimuleerde\_apparaat\_cloud\_uploaden\_voorbeeld, src/gesimuleerde\_apparaat\_cloud\_uploaden\_lin.json** in het lokale exemplaar van Hallo **iot-edge** opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="d54cc-118">In a text editor, open hello file **samples/simulated\_device\_cloud\_upload\_sample/src/simulated\_device\_cloud\_upload\_lin.json** in your local copy of hello **iot-edge** repository.</span></span> <span data-ttu-id="d54cc-119">Dit bestand configureert Hallo IoT rand modules in Hallo voorbeeld gateway:</span><span class="sxs-lookup"><span data-stu-id="d54cc-119">This file configures hello IoT Edge modules in hello sample gateway:</span></span>

* <span data-ttu-id="d54cc-120">Hallo **IoTHub** module verbindt tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="d54cc-120">hello **IoTHub** module connects tooyour IoT hub.</span></span> <span data-ttu-id="d54cc-121">U configureert toosend gegevens tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="d54cc-121">You configure it toosend data tooyour IoT hub.</span></span> <span data-ttu-id="d54cc-122">In het bijzonder set Hallo **IoTHubName** toohello waardenaam van uw iothub en stel Hallo **IoTHubSuffix** waarde te**azure devices.net**.</span><span class="sxs-lookup"><span data-stu-id="d54cc-122">Specifically, set hello **IoTHubName** value toohello name of your IoT hub and set hello **IoTHubSuffix** value too**azure-devices.net**.</span></span> <span data-ttu-id="d54cc-123">Set Hallo **Transport** tooone waarde van: **HTTP**, **AMQP**, of **MQTT**.</span><span class="sxs-lookup"><span data-stu-id="d54cc-123">Set hello **Transport** value tooone of: **HTTP**, **AMQP**, or **MQTT**.</span></span> <span data-ttu-id="d54cc-124">Op dit moment alleen **HTTP** deelt een TCP-verbinding voor alle apparaatberichten.</span><span class="sxs-lookup"><span data-stu-id="d54cc-124">Currently, only **HTTP** shares one TCP connection for all device messages.</span></span> <span data-ttu-id="d54cc-125">Als u de waarde hello te**AMQP**, of **MQTT**, Hallo gateway onderhoudt een afzonderlijke TCP-verbinding tooIoT Hub voor elk apparaat.</span><span class="sxs-lookup"><span data-stu-id="d54cc-125">If you set hello value too**AMQP**, or **MQTT**, hello gateway maintains a separate TCP connection tooIoT Hub for each device.</span></span>
* <span data-ttu-id="d54cc-126">Hallo **toewijzing** module Hallo MAC-adressen van uw gesimuleerde apparaten tooyour Iothub apparaat-id wordt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="d54cc-126">hello **mapping** module maps hello MAC addresses of your simulated devices tooyour IoT Hub device ids.</span></span> <span data-ttu-id="d54cc-127">Zorg ervoor dat **deviceId** waarden overeen Hallo-id's van de twee apparaten die u hebt toegevoegd tooyour iothub en die Hallo Hallo **deviceKey** waarden Hallo sleutels van de twee apparaten bevatten.</span><span class="sxs-lookup"><span data-stu-id="d54cc-127">Make sure that **deviceId** values match hello ids of hello two devices you added tooyour IoT hub, and that hello **deviceKey** values contain hello keys of your two devices.</span></span>
* <span data-ttu-id="d54cc-128">Hallo **BLE1** en **BLE2** modules Hallo gesimuleerde apparaten zijn.</span><span class="sxs-lookup"><span data-stu-id="d54cc-128">hello **BLE1** and **BLE2** modules are hello simulated devices.</span></span> <span data-ttu-id="d54cc-129">Houd er rekening mee hoe hun MAC-adressen overeen adressen in Hallo Hallo **toewijzing** module.</span><span class="sxs-lookup"><span data-stu-id="d54cc-129">Note how their MAC addresses match hello addresses in hello **mapping** module.</span></span>
* <span data-ttu-id="d54cc-130">Hallo **berichtenlogboek** module Logboeken uw gateway activiteit tooa-bestand.</span><span class="sxs-lookup"><span data-stu-id="d54cc-130">hello **Logger** module logs your gateway activity tooa file.</span></span>
* <span data-ttu-id="d54cc-131">Hallo **pad module** waarden wordt weergegeven in Hallo voorbeeld wordt ervan uitgegaan dat u Hallo-voorbeeld vanuit Hallo uitvoeren **bouwen** map in het lokale exemplaar van Hallo **iot-edge** opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="d54cc-131">hello **module path** values shown in hello example assume that you run hello sample from hello **build** folder in your local copy of hello **iot-edge** repository.</span></span>
* <span data-ttu-id="d54cc-132">Hallo **koppelingen** matrix Hallo onderaan Hallo JSON-bestand in verbindt Hallo **BLE1** en **BLE2** modules toohello **toewijzing** -module en Hallo **toewijzing** module toohello **IoTHub** module.</span><span class="sxs-lookup"><span data-stu-id="d54cc-132">hello **links** array at hello bottom of hello JSON file connects hello **BLE1** and **BLE2** modules toohello **mapping** module, and hello **mapping** module toohello **IoTHub** module.</span></span> <span data-ttu-id="d54cc-133">Dit zorgt er ook voor dat alle berichten worden vastgelegd door Hallo **berichtenlogboek** module.</span><span class="sxs-lookup"><span data-stu-id="d54cc-133">It also ensures that all messages are logged by hello **Logger** module.</span></span>

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

<span data-ttu-id="d54cc-134">U hebt aangebracht toohello configuratiebestand Hallo wijzigingen opslaan.</span><span class="sxs-lookup"><span data-stu-id="d54cc-134">Save hello changes you made toohello configuration file.</span></span>

<span data-ttu-id="d54cc-135">toorun Hallo-voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d54cc-135">toorun hello sample:</span></span>

1. <span data-ttu-id="d54cc-136">Navigeer in uw shell toohello **iot-rand/build** map.</span><span class="sxs-lookup"><span data-stu-id="d54cc-136">In your shell, navigate toohello **iot-edge/build** folder.</span></span>
2. <span data-ttu-id="d54cc-137">Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="d54cc-137">Run hello following command:</span></span>
   
    ```sh
    ./samples/simulated_device_cloud_upload/simulated_device_cloud_upload_sample ../samples/simulated_device_cloud_upload/src/simulated_device_cloud_upload_lin.json
    ```
3. <span data-ttu-id="d54cc-138">Kunt u Hallo [apparaat explorer] [ lnk-device-explorer] of [iothub explorer] [ lnk-iothub-explorer] toomonitor Hallo-berichten die IoT-hub van Hallo ontvangt hulpprogramma gateway.</span><span class="sxs-lookup"><span data-stu-id="d54cc-138">You can use hello [device explorer][lnk-device-explorer] or [iothub-explorer][lnk-iothub-explorer] tool toomonitor hello messages that IoT hub receives from hello gateway.</span></span> <span data-ttu-id="d54cc-139">Bijvoorbeeld, kunt met iothub explorer u controleren met behulp van de volgende opdracht Hallo apparaat-naar-cloud-berichten:</span><span class="sxs-lookup"><span data-stu-id="d54cc-139">For example, using iothub-explorer you can monitor device-to-cloud messages using hello following command:</span></span>

    ```sh
    iothub-explorer monitor-events --login "HostName={Your iot hub name}.azure-devices.net;SharedAccessKeyName=iothubowner;SharedAccessKey={Your IoT Hub key}"
    ```

## <a name="next-steps"></a><span data-ttu-id="d54cc-140">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d54cc-140">Next steps</span></span>

<span data-ttu-id="d54cc-141">toogain een uitgebreidere kennis van Azure IoT rand en experiment met enkele codevoorbeelden, gaat u naar de volgende Hallo developer zelfstudies en bronnen:</span><span class="sxs-lookup"><span data-stu-id="d54cc-141">toogain a more advanced understanding of Azure IoT Edge and experiment with some code examples, visit hello following developer tutorials and resources:</span></span>

* <span data-ttu-id="d54cc-142">[Apparaat-naar-cloud-berichten verzenden vanaf een fysiek apparaat met Azure IoT rand][lnk-physical-device]</span><span class="sxs-lookup"><span data-stu-id="d54cc-142">[Send device-to-cloud messages from a physical device with Azure IoT Edge][lnk-physical-device]</span></span>
* <span data-ttu-id="d54cc-143">[Azure IoT-rand][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="d54cc-143">[Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="d54cc-144">toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:</span><span class="sxs-lookup"><span data-stu-id="d54cc-144">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="d54cc-145">[Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="d54cc-145">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="d54cc-146">[Uw IoT-oplossing van Hallo gemalen beveiligen][lnk-securing]</span><span class="sxs-lookup"><span data-stu-id="d54cc-146">[Secure your IoT solution from hello ground up][lnk-securing]</span></span>

<!-- Links -->
[lnk-iot-edge]: https://github.com/Azure/iot-edge/
[lnk-physical-device]: iot-hub-iot-edge-physical-device.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-securing]: iot-hub-security-ground-up.md
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/Azure/iothub-explorer/blob/master/readme.md
