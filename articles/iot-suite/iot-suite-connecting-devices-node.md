---
title: aaaConnect een apparaat met behulp van Node.js | Microsoft Docs
description: Hierin wordt beschreven hoe tooconnect een apparaat toohello Azure IoT Suite vooraf geconfigureerde oplossing voor externe controle met behulp van een toepassing die is geschreven in Node.js.
services: 
suite: iot-suite
documentationcenter: na
author: dominicbetts
manager: timlt
editor: 
ms.assetid: fc50a33f-9fb9-42d7-b1b8-eb5cff19335e
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: dobett
ms.openlocfilehash: 80bf2b70f15f539bfce4f135d533c46dd2b3f5a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-nodejs"></a><span data-ttu-id="904b4-103">Verbinding maken met uw apparaat toohello vooraf geconfigureerde oplossing (Node.js) voor externe controle</span><span class="sxs-lookup"><span data-stu-id="904b4-103">Connect your device toohello remote monitoring preconfigured solution (Node.js)</span></span>
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-nodejs-sample-solution"></a><span data-ttu-id="904b4-104">Een node.js-voorbeeld-oplossing maken</span><span class="sxs-lookup"><span data-stu-id="904b4-104">Create a node.js sample solution</span></span>

<span data-ttu-id="904b4-105">Zorg dat Node.js-versie 0.11.5 of hoger is geïnstalleerd op uw ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="904b4-105">Ensure that Node.js version 0.11.5 or later is installed on your development machine.</span></span> <span data-ttu-id="904b4-106">U kunt uitvoeren `node --version` Hallo opdrachtregel toocheck Hallo versie.</span><span class="sxs-lookup"><span data-stu-id="904b4-106">You can run `node --version` at hello command line toocheck hello version.</span></span>

1. <span data-ttu-id="904b4-107">Maak een map **RemoteMonitoring** op uw ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="904b4-107">Create a folder called **RemoteMonitoring** on your development machine.</span></span> <span data-ttu-id="904b4-108">Navigeer toothis map in uw omgeving vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="904b4-108">Navigate toothis folder in your command-line environment.</span></span>

1. <span data-ttu-id="904b4-109">Voer Hallo na opdrachten toodownload en installeer hello-pakketten moet u toocomplete Hallo voorbeeld-app:</span><span class="sxs-lookup"><span data-stu-id="904b4-109">Run hello following commands toodownload and install hello packages you need toocomplete hello sample app:</span></span>

    ```
    npm init
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="904b4-110">In Hallo **RemoteMonitoring** map maken van een bestand met de naam **remote_monitoring.js**.</span><span class="sxs-lookup"><span data-stu-id="904b4-110">In hello **RemoteMonitoring** folder, create a file called **remote_monitoring.js**.</span></span> <span data-ttu-id="904b4-111">Open dit bestand in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="904b4-111">Open this file in a text editor.</span></span>

1. <span data-ttu-id="904b4-112">In Hallo **remote_monitoring.js** bestand, voeg de volgende Hallo `require` instructies:</span><span class="sxs-lookup"><span data-stu-id="904b4-112">In hello **remote_monitoring.js** file, add hello following `require` statements:</span></span>

    ```nodejs
    'use strict';

    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    var Client = require('azure-iot-device').Client;
    var ConnectionString = require('azure-iot-device').ConnectionString;
    var Message = require('azure-iot-device').Message;
    ```

1. <span data-ttu-id="904b4-113">Hallo variabelendeclaraties volgen na Hallo toevoegen `require` instructies.</span><span class="sxs-lookup"><span data-stu-id="904b4-113">Add hello following variable declarations after hello `require` statements.</span></span> <span data-ttu-id="904b4-114">Vervang de waarden van de tijdelijke aanduiding Hallo [apparaat-Id] en [apparaatsleutel] met waarden die u voor uw apparaat in Hallo dashboard externe controle oplossing hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="904b4-114">Replace hello placeholder values [Device Id] and [Device Key] with values you noted for your device in hello remote monitoring solution dashboard.</span></span> <span data-ttu-id="904b4-115">Hallo IoT Hub-hostnaam van Hallo oplossing dashboard tooreplace [IoTHub Name] gebruiken.</span><span class="sxs-lookup"><span data-stu-id="904b4-115">Use hello IoT Hub Hostname from hello solution dashboard tooreplace [IoTHub Name].</span></span> <span data-ttu-id="904b4-116">Als uw IoT Hub-hostnaam bijvoorbeeld **contoso.azure devices.net** is, vervangt u [IoTHub-naam] door **contoso**:</span><span class="sxs-lookup"><span data-stu-id="904b4-116">For example, if your IoT Hub Hostname is **contoso.azure-devices.net**, replace [IoTHub Name] with **contoso**:</span></span>

    ```nodejs
    var connectionString = 'HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]';
    var deviceId = ConnectionString.parse(connectionString).DeviceId;
    ```

1. <span data-ttu-id="904b4-117">Hallo variabelen toodefine na enkele base telemetriegegevens toevoegen:</span><span class="sxs-lookup"><span data-stu-id="904b4-117">Add hello following variables toodefine some base telemetry data:</span></span>

    ```nodejs
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    ```

1. <span data-ttu-id="904b4-118">Hallo helper functie tooprint Bewerkingsresultaten volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="904b4-118">Add hello following helper function tooprint operation results:</span></span>

    ```nodejs
    function printErrorFor(op) {
        return function printError(err) {
            if (err) console.log(op + ' error: ' + err.toString());
        };
    }
    ```

1. <span data-ttu-id="904b4-119">Hallo helper functie toouse toorandomize Hallo telemetrie waarden volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="904b4-119">Add hello following helper function toouse toorandomize hello telemetry values:</span></span>

    ```nodejs
    function generateRandomIncrement() {
        return ((Math.random() * 2) - 1);
    }
    ```

1. <span data-ttu-id="904b4-120">Toevoegen na de definitie voor Hallo Hallo **DeviceInfo** object Hallo apparaat verzendt bij het opstarten:</span><span class="sxs-lookup"><span data-stu-id="904b4-120">Add hello following definition for hello **DeviceInfo** object hello device sends on startup:</span></span>

    ```nodejs
    var deviceMetaData = {
        'ObjectType': 'DeviceInfo',
        'IsSimulatedDevice': 0,
        'Version': '1.0',
        'DeviceProperties': {
            'DeviceID': deviceId,
            'HubEnabledState': 1
        }
    };
    ```

1. <span data-ttu-id="904b4-121">Voeg de volgende Hallo definitie voor Hallo apparaat twin waarden gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="904b4-121">Add hello following definition for hello device twin reported values.</span></span> <span data-ttu-id="904b4-122">Deze definitie bevat beschrijvingen van de directe methoden Hallo Hallo apparaat ondersteunt:</span><span class="sxs-lookup"><span data-stu-id="904b4-122">This definition includes descriptions of hello direct methods hello device supports:</span></span>

    ```nodejs
    var reportedProperties = {
        "Device": {
            "DeviceState": "normal",
            "Location": {
                "Latitude": 47.642877,
                "Longitude": -122.125497
            }
        },
        "Config": {
            "TemperatureMeanValue": 56.7,
            "TelemetryInterval": 45
        },
        "System": {
            "Manufacturer": "Contoso Inc.",
            "FirmwareVersion": "2.22",
            "InstalledRAM": "8 MB",
            "ModelNumber": "DB-14",
            "Platform": "Plat 9.75",
            "Processor": "i3-9",
            "SerialNumber": "SER99"
        },
        "Location": {
            "Latitude": 47.642877,
            "Longitude": -122.125497
        },
        "SupportedMethods": {
            "Reboot": "Reboot hello device",
            "InitiateFirmwareUpdate--FwPackageURI-string": "Updates device Firmware. Use parameter FwPackageURI toospecifiy hello URI of hello firmware file"
        },
    }
    ```

1. <span data-ttu-id="904b4-123">Toevoegen van de volgende functie toohandle Hallo Hallo **opnieuw opstarten** directe aanroep van methode:</span><span class="sxs-lookup"><span data-stu-id="904b4-123">Add hello following function toohandle hello **Reboot** direct method call:</span></span>

    ```nodejs
    function onReboot(request, response) {
        // Implement actual logic here.
        console.log('Simulated reboot...');

        // Complete hello response
        response.send(200, "Rebooting device", function(err) {
            if(!!err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```

1. <span data-ttu-id="904b4-124">Toevoegen van de volgende functie toohandle Hallo Hallo **InitiateFirmwareUpdate** directe aanroep van methode.</span><span class="sxs-lookup"><span data-stu-id="904b4-124">Add hello following function toohandle hello **InitiateFirmwareUpdate** direct method call.</span></span> <span data-ttu-id="904b4-125">Deze directe methode maakt gebruik van een parameter toospecify Hallo-locatie van het Hallo-firmware installatiekopie toodownload en initieert Hallo firmware-update op Hallo apparaat asynchroon:</span><span class="sxs-lookup"><span data-stu-id="904b4-125">This direct method uses a parameter toospecify hello location of hello firmware image toodownload, and initiates hello firmware update on hello device asynchronously:</span></span>

    ```nodejs
    function onInitiateFirmwareUpdate(request, response) {
        console.log('Simulated firmware update initiated, using: ' + request.payload.FwPackageURI);

        // Complete hello response
        response.send(200, "Firmware update initiated", function(err) {
            if(!!err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });

        // Add logic here tooperform hello firmware update asynchronously
    }
    ```

1. <span data-ttu-id="904b4-126">Hallo code toocreate een clientexemplaar na toevoegen:</span><span class="sxs-lookup"><span data-stu-id="904b4-126">Add hello following code toocreate a client instance:</span></span>

    ```nodejs
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. <span data-ttu-id="904b4-127">Hallo code voor het volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="904b4-127">Add hello following code to:</span></span>

    * <span data-ttu-id="904b4-128">Hallo-verbinding openen.</span><span class="sxs-lookup"><span data-stu-id="904b4-128">Open hello connection.</span></span>
    * <span data-ttu-id="904b4-129">Hallo verzenden **DeviceInfo** object.</span><span class="sxs-lookup"><span data-stu-id="904b4-129">Send hello **DeviceInfo** object.</span></span>
    * <span data-ttu-id="904b4-130">Een handler voor de gewenste eigenschappen instellen.</span><span class="sxs-lookup"><span data-stu-id="904b4-130">Set up a handler for desired properties.</span></span>
    * <span data-ttu-id="904b4-131">Eigenschappen van de gerapporteerde verzenden.</span><span class="sxs-lookup"><span data-stu-id="904b4-131">Send reported properties.</span></span>
    * <span data-ttu-id="904b4-132">Registreer de handlers voor rechtstreekse Hallo-methoden.</span><span class="sxs-lookup"><span data-stu-id="904b4-132">Register handlers for hello direct methods.</span></span>
    * <span data-ttu-id="904b4-133">Beginnen met het verzenden van telemetrie.</span><span class="sxs-lookup"><span data-stu-id="904b4-133">Start sending telemetry.</span></span>

    ```nodejs
    client.open(function (err) {
        if (err) {
            printErrorFor('open')(err);
        } else {
            console.log('Sending device metadata:\n' + JSON.stringify(deviceMetaData));
            client.sendEvent(new Message(JSON.stringify(deviceMetaData)), printErrorFor('send metadata'));

            // Create device twin
            client.getTwin(function(err, twin) {
                if (err) {
                    console.error('Could not get device twin');
                } else {
                    console.log('Device twin created');

                    twin.on('properties.desired', function(delta) {
                        console.log('Received new desired properties:');
                        console.log(JSON.stringify(delta));
                    });

                    // Send reported properties
                    twin.properties.reported.update(reportedProperties, function(err) {
                        if (err) throw err;
                        console.log('twin state reported');
                    });

                    // Register handlers for direct methods
                    client.onDeviceMethod('Reboot', onReboot);
                    client.onDeviceMethod('InitiateFirmwareUpdate', onInitiateFirmwareUpdate);
                }
            });

            // Start sending telemetry
            var sendInterval = setInterval(function () {
                temperature += generateRandomIncrement();
                externalTemperature += generateRandomIncrement();
                humidity += generateRandomIncrement();

                var data = JSON.stringify({
                    'DeviceID': deviceId,
                    'Temperature': temperature,
                    'Humidity': humidity,
                    'ExternalTemperature': externalTemperature
                });

                console.log('Sending device event data:\n' + data);
                client.sendEvent(new Message(data), printErrorFor('send event'));
            }, 5000);

            client.on('error', function (err) {
                printErrorFor('client')(err);
                if (sendInterval) clearInterval(sendInterval);
                client.close(printErrorFor('client.close'));
            });
        }
    });
    ```

1. <span data-ttu-id="904b4-134">Hallo wijzigingen toohello opslaan **remote_monitoring.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="904b4-134">Save hello changes toohello **remote_monitoring.js** file.</span></span>

1. <span data-ttu-id="904b4-135">Hallo na een opdrachtprompt toolaunch Hallo-voorbeeldtoepassing-opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="904b4-135">Run hello following command at a command prompt toolaunch hello sample application:</span></span>
   
    ```
    node remote_monitoring.js
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-github-repo]: https://github.com/azure/azure-iot-sdk-node
[lnk-github-prepare]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
