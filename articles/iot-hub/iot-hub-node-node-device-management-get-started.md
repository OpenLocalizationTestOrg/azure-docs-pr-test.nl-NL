---
title: aaaGet de slag met Azure IoT Hub Apparaatbeheer (knooppunt) | Microsoft Docs
description: Hoe toouse IoT Hub apparaat management tooinitiate een extern apparaat opnieuw worden opgestart. U gebruikt hello Azure IoT SDK voor Node.js tooimplement een gesimuleerde apparaattoepassing die een directe methode bevat en een service-app die Hallo directe methode aanroept.
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: e044006d-ffd6-469b-bc63-c182ad066e31
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: juanpere
ms.openlocfilehash: 5dd1878e71231850fb95f4170b823f1e86c3ee83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-node"></a>Aan de slag met Apparaatbeheer (knooppunt)

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

In deze handleiding ontdekt u hoe u:

* Gebruik Hallo toocreate met Azure portal een IoT-Hub en een apparaat-id maakt in uw IoT-hub.
* Maak een gesimuleerde apparaattoepassing met een directe methode die het apparaat opnieuw wordt opgestart. Rechtstreekse methoden worden aangeroepen vanuit Hallo cloud.
* Een Node.js-consoletoepassing die Hallo opnieuw opstarten directe methode in Hallo gesimuleerde apparaattoepassing via uw IoT-hub aanroept maken.

Aan het einde van de Hallo van deze zelfstudie hebt u twee console Node.js-apps:

**dmpatterns_getstarted_device.js**, die tooyour IoT-hub verbindt met apparaat-id Hallo eerder hebt gemaakt, ontvangt van een directe methode voor opnieuw opstarten, simuleert fysieke opnieuw worden opgestart en Hallo tijd voor de laatste keer opnieuw opstarten Hallo rapporteert.

**dmpatterns_getstarted_service.js**, die een directe methode wordt aangeroepen in de gesimuleerde apparaattoepassing hello, geeft antwoord Hallo weer en geeft Hallo bijgewerkt gerapporteerd eigenschappen.

toocomplete in deze zelfstudie, moet u hello te volgen:

* Node.js-versie 0.12.x of hoger <br/>  [Uw ontwikkelingsomgeving voorbereiden] [ lnk-dev-setup] wordt beschreven hoe tooinstall Node.js voor deze zelfstudie op Windows of Linux.
* Een actief Azure-account. (Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Een gesimuleerde apparaattoepassing maken
In deze sectie wordt u

* Een Node.js-consoletoepassing die tooa directe methode aangeroepen door Hallo cloud reageert maken
* Een gesimuleerd apparaat opnieuw activeren
* Gebruik Hallo gerapporteerd eigenschappen tooenable apparaat twin query's tooidentify apparaten en wanneer ze laatste opnieuw opgestart

1. U maakt een lege map met de naam **simulateddevice**.  In Hallo **manageddevice** map, een package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken.  Accepteer alle Hallo standaardwaarden:
   
    ```
    npm init
    ```
2. Bij de opdrachtprompt in Hallo **manageddevice** map na de opdracht tooinstall Hallo Hallo **azure-iot-device** apparaat-SDK-pakket en **azure-iot-device-mqtt**pakket:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Maak met een teksteditor, een **dmpatterns_getstarted_device.js** bestand in Hallo **manageddevice** map.
4. Toevoegen van de volgende Hallo 'vereist' instructies toe aan Hallo begin Hallo **dmpatterns_getstarted_device.js** bestand:
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. Voeg een **connectionString** variabele en gebruik deze toocreate een **Client** exemplaar.  Hallo-verbindingsreeks vervangen door de verbindingsreeks van uw apparaat.  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. Hallo functie tooimplement Hallo directe methode volgen op Hallo apparaat toevoegen
   
    ```
    var onReboot = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report hello reboot before hello physical restart
        var date = new Date();
        var patch = {
            iothubDM : {
                reboot : {
                    lastReboot : date.toISOString(),
                }
            }
        };
   
        // Get device Twin
        client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                console.log('twin acquired');
                twin.properties.reported.update(patch, function(err) {
                    if (err) throw err;
                    console.log('Device reboot twin state reported')
                });  
            }
        });
   
        // Add your device's reboot API for physical restart.
        console.log('Rebooting!');
    };
    ```
7. Open Hallo verbinding tooyour IoT-hub en Hallo directe methode listener starten:
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not open IotHub client');
        }  else {
            console.log('Client opened.  Waiting for reboot method.');
            client.onDeviceMethod('reboot', onReboot);
        }
    });
    ```
8. Opslaan en sluiten Hallo **dmpatterns_getstarted_device.js** bestand.

> [!NOTE]
> tookeep dingen eenvoudige, deze zelfstudie wordt niet geïmplementeerd voor een beleid voor opnieuw proberen. In productiecode moet u beleid voor opnieuw proberen (zoals exponentieel uitstel), zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout][lnk-transient-faults].

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a>Activeren van een extern opnieuw opstarten op Hallo-apparaat met een directe methode
In deze sectie maakt maken u een Node.js-consoletoepassing die start een extern opnieuw opstarten op een apparaat met een directe methode. Hallo app gebruikmaakt van apparaat twin query's toodiscover Hallo keer opnieuw opstarten voor dat apparaat.

1. Maak een lege map genaamd **triggerrebootondevice**.  In Hallo **triggerrebootondevice** map, een package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken.  Accepteer alle Hallo standaardwaarden:
   
    ```
    npm init
    ```
2. Bij de opdrachtprompt in Hallo **triggerrebootondevice** map na de opdracht tooinstall Hallo Hallo **azure-iothub** apparaat-SDK-pakket en **azure-iot-device-mqtt** pakket:
   
    ```
    npm install azure-iothub --save
    ```
3. Maak met een teksteditor, een **dmpatterns_getstarted_service.js** bestand in Hallo **triggerrebootondevice** map.
4. Toevoegen van de volgende Hallo 'vereist' instructies toe aan Hallo begin Hallo **dmpatterns_getstarted_service.js** bestand:
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. Hallo na variabelendeclaraties toevoegen en vervang de waarden van de tijdelijke aanduiding Hallo:
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToReboot = 'myDeviceId';
    ```
6. Hallo functie tooinvoke Hallo apparaat methode tooreboot Hallo doelapparaat volgende toevoegen:
   
    ```
    var startRebootDevice = function(twin) {
   
        var methodName = "reboot";
   
        var methodParams = {
            methodName: methodName,
            payload: null,
            timeoutInSeconds: 30
        };
   
        client.invokeDeviceMethod(deviceToReboot, methodParams, function(err, result) {
            if (err) { 
                console.error("Direct method error: "+err.message);
            } else {
                console.log("Successfully invoked hello device tooreboot.");  
            }
        });
    };
    ```
7. Hallo volgende tooquery voor Hallo apparaat werken en ophalen van Hallo keer opnieuw opstarten toevoegen:
   
    ```
    var queryTwinLastReboot = function() {
   
        registry.getTwin(deviceToReboot, function(err, twin){
   
            if (twin.properties.reported.iothubDM != null)
            {
                if (err) {
                    console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
                } else {
                    var lastRebootTime = twin.properties.reported.iothubDM.reboot.lastReboot;
                    console.log('Last reboot time: ' + JSON.stringify(lastRebootTime, null, 2));
                }
            } else 
                console.log('Waiting for device tooreport last reboot time.');
        });
    };
    ```
8. Hallo code toocall Hallo functies waarmee Hallo geactiveerd na opnieuw opstarten directe methode en de query voor Hallo laatste keer opnieuw opstarten toevoegen:
   
    ```
    startRebootDevice();
    setInterval(queryTwinLastReboot, 2000);
    ```
9. Opslaan en sluiten Hallo **dmpatterns_getstarted_service.js** bestand.

## <a name="run-hello-apps"></a>Hallo-apps uitvoeren
U bent nu klaar toorun Hallo apps.

1. Bij de opdrachtprompt Hallo in Hallo **manageddevice** map Hallo opdracht toobegin luisteren naar Hallo opnieuw opstarten directe methode te volgen.
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. Bij de opdrachtprompt Hallo in Hallo **triggerrebootondevice** map Hallo opdracht tootrigger Hallo afstand na opnieuw opstarten en query's uitvoeren voor Hallo apparaat twin toofind Hallo laatste keer opnieuw opstarten.
   
    ```
    node dmpatterns_getstarted_service.js
    ```
3. U ziet Hallo apparaat antwoord toohello directe methode in Hallo-console.

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups toomanage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
