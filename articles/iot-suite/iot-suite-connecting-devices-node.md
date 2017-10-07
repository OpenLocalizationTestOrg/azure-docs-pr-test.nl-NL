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
# <a name="connect-your-device-toohello-remote-monitoring-preconfigured-solution-nodejs"></a>Verbinding maken met uw apparaat toohello vooraf geconfigureerde oplossing (Node.js) voor externe controle
[!INCLUDE [iot-suite-selector-connecting](../../includes/iot-suite-selector-connecting.md)]

## <a name="create-a-nodejs-sample-solution"></a>Een node.js-voorbeeld-oplossing maken

Zorg dat Node.js-versie 0.11.5 of hoger is geïnstalleerd op uw ontwikkelcomputer. U kunt uitvoeren `node --version` Hallo opdrachtregel toocheck Hallo versie.

1. Maak een map **RemoteMonitoring** op uw ontwikkelcomputer. Navigeer toothis map in uw omgeving vanaf de opdrachtregel.

1. Voer Hallo na opdrachten toodownload en installeer hello-pakketten moet u toocomplete Hallo voorbeeld-app:

    ```
    npm init
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. In Hallo **RemoteMonitoring** map maken van een bestand met de naam **remote_monitoring.js**. Open dit bestand in een teksteditor.

1. In Hallo **remote_monitoring.js** bestand, voeg de volgende Hallo `require` instructies:

    ```nodejs
    'use strict';

    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    var Client = require('azure-iot-device').Client;
    var ConnectionString = require('azure-iot-device').ConnectionString;
    var Message = require('azure-iot-device').Message;
    ```

1. Hallo variabelendeclaraties volgen na Hallo toevoegen `require` instructies. Vervang de waarden van de tijdelijke aanduiding Hallo [apparaat-Id] en [apparaatsleutel] met waarden die u voor uw apparaat in Hallo dashboard externe controle oplossing hebt genoteerd. Hallo IoT Hub-hostnaam van Hallo oplossing dashboard tooreplace [IoTHub Name] gebruiken. Als uw IoT Hub-hostnaam bijvoorbeeld **contoso.azure devices.net** is, vervangt u [IoTHub-naam] door **contoso**:

    ```nodejs
    var connectionString = 'HostName=[IoTHub Name].azure-devices.net;DeviceId=[Device Id];SharedAccessKey=[Device Key]';
    var deviceId = ConnectionString.parse(connectionString).DeviceId;
    ```

1. Hallo variabelen toodefine na enkele base telemetriegegevens toevoegen:

    ```nodejs
    var temperature = 50;
    var humidity = 50;
    var externalTemperature = 55;
    ```

1. Hallo helper functie tooprint Bewerkingsresultaten volgende toevoegen:

    ```nodejs
    function printErrorFor(op) {
        return function printError(err) {
            if (err) console.log(op + ' error: ' + err.toString());
        };
    }
    ```

1. Hallo helper functie toouse toorandomize Hallo telemetrie waarden volgende toevoegen:

    ```nodejs
    function generateRandomIncrement() {
        return ((Math.random() * 2) - 1);
    }
    ```

1. Toevoegen na de definitie voor Hallo Hallo **DeviceInfo** object Hallo apparaat verzendt bij het opstarten:

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

1. Voeg de volgende Hallo definitie voor Hallo apparaat twin waarden gerapporteerd. Deze definitie bevat beschrijvingen van de directe methoden Hallo Hallo apparaat ondersteunt:

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

1. Toevoegen van de volgende functie toohandle Hallo Hallo **opnieuw opstarten** directe aanroep van methode:

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

1. Toevoegen van de volgende functie toohandle Hallo Hallo **InitiateFirmwareUpdate** directe aanroep van methode. Deze directe methode maakt gebruik van een parameter toospecify Hallo-locatie van het Hallo-firmware installatiekopie toodownload en initieert Hallo firmware-update op Hallo apparaat asynchroon:

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

1. Hallo code toocreate een clientexemplaar na toevoegen:

    ```nodejs
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. Hallo code voor het volgende toevoegen:

    * Hallo-verbinding openen.
    * Hallo verzenden **DeviceInfo** object.
    * Een handler voor de gewenste eigenschappen instellen.
    * Eigenschappen van de gerapporteerde verzenden.
    * Registreer de handlers voor rechtstreekse Hallo-methoden.
    * Beginnen met het verzenden van telemetrie.

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

1. Hallo wijzigingen toohello opslaan **remote_monitoring.js** bestand.

1. Hallo na een opdrachtprompt toolaunch Hallo-voorbeeldtoepassing-opdracht uitvoeren:
   
    ```
    node remote_monitoring.js
    ```

[!INCLUDE [iot-suite-visualize-connecting](../../includes/iot-suite-visualize-connecting.md)]

[lnk-github-repo]: https://github.com/azure/azure-iot-sdk-node
[lnk-github-prepare]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
