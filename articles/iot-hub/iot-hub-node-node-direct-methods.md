---
title: aaaAzure IoT Hub directe methoden (knooppunt) | Microsoft Docs
description: Hoe Azure IoT Hub toouse directe methoden. U hello Azure IoT SDK's gebruiken voor Node.js tooimplement een gesimuleerde apparaattoepassing die een directe methode bevat en een service-app die Hallo directe methode aanroept.
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: ea9c73ca-7778-4e38-a8f1-0bee9d142f04
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 12300ba451816fec1f80163b633f6b6e411d9e5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-on-your-iot-device-with-nodejs"></a>Directe methoden te gebruiken op uw IoT-apparaat met behulp van Node.js
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

Aan het einde van de Hallo van deze zelfstudie hebt u twee console Node.js-apps:

* **CallMethodOnDevice.js**, die een methode wordt aangeroepen in de gesimuleerde apparaattoepassing Hallo en antwoord Hallo weergegeven.
* **SimulatedDevice.js**, die tooyour IoT-hub aan Hallo apparaat-id eerder hebt gemaakt, en toohello methode aangeroepen door Hallo cloud reageert.

> [!NOTE]
> Hallo artikel [Azure IoT SDK's] [ lnk-hub-sdks] bevat informatie over hello Azure IoT SDK's waarmee u toobuild beide toorun toepassingen op apparaten en de back-end van uw oplossing kunt.
> 
> 

toocomplete in deze zelfstudie, moet u hello te volgen:

* Node.js versie 0.10.x of hoger.
* Een actief Azure-account. (Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Een gesimuleerde apparaattoepassing maken
In deze sectie maakt maken u een Node.js-consoletoepassing die tooa methode aangeroepen door Hallo cloud reageert.

1. Maak een nieuwe lege map met de naam **simulateddevice**. In Hallo **simulateddevice** map, een package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken. Accepteer alle Hallo standaardwaarden:
   
    ```
    npm init
    ```
2. Bij de opdrachtprompt in Hallo **simulateddevice** map na de opdracht tooinstall Hallo Hallo **azure-iot-device** apparaat-SDK-pakket en **azure-iot-device-mqtt**pakket:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Start een teksteditor en maak een nieuwe **SimulatedDevice.js** bestand in Hallo **simulateddevice** map.
4. Voeg de volgende Hallo `require` instructies aan Hallo start Hallo **SimulatedDevice.js** bestand:
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. Voeg een **connectionString** variabele en gebruik deze toocreate een **DeviceClient** exemplaar. Vervang **{verbindingsreeks apparaat}** met Hallo verbindingsreeks voor apparaat u hebt gegenereerd in Hallo *maken van een apparaat-id* sectie:
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. Hallo functie tooimplement Hallo methode volgen op Hallo apparaat toevoegen:
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written toolog.', function(err) {
            if(err) {
                console.error('An error ocurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. Open Hallo verbinding tooyour IoT-hub en geïnitialiseerd Hallo methode listener starten:
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
            client.onDeviceMethod('writeLine', onWriteLine);
        }
    });
    ```
8. Opslaan en sluiten Hallo **SimulatedDevice.js** bestand.

> [!NOTE]
> tookeep dingen eenvoudige, deze zelfstudie wordt niet geïmplementeerd voor een beleid voor opnieuw proberen. In productiecode moet u beleid voor opnieuw proberen (zoals verbinding opnieuw), zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout][lnk-transient-faults].
> 
> 

## <a name="call-a-method-on-a-device"></a>Een methode is aangeroepen voor een apparaat
In deze sectie maakt maken u een Node.js-consoletoepassing die een methode wordt aangeroepen in de gesimuleerde apparaattoepassing Hallo en wordt vervolgens weergegeven antwoord Hallo.

1. Maak een nieuwe lege map genaamd **callmethodondevice**. In Hallo **callmethodondevice** map, een package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken. Accepteer alle Hallo standaardwaarden:
   
    ```
    npm init
    ```
2. Bij de opdrachtprompt in Hallo **callmethodondevice** map na de opdracht tooinstall Hallo Hallo **azure-iothub** pakket:
   
    ```
    npm install azure-iothub --save
    ```
3. Maak met een teksteditor, een **CallMethodOnDevice.js** bestand in Hallo **callmethodondevice** map.
4. Voeg de volgende Hallo `require` instructies aan Hallo start Hallo **CallMethodOnDevice.js** bestand:
   
    ```
    'use strict';
   
    var Client = require('azure-iothub').Client;
    ```
5. Hallo na variabelendeclaratie toevoegen en vervang Hallo tijdelijke aanduidingswaarde met Hallo IoT Hub-verbindingsreeks voor uw hub:
   
    ```
    var connectionString = '{iothub connection string}';
    var methodName = 'writeLine';
    var deviceId = 'myDeviceId';
    ```
6. Hallo client tooopen Hallo verbinding tooyour iothub maken.
   
    ```
    var client = Client.fromConnectionString(connectionString);
    ```
7. Hallo functie tooinvoke Hallo apparaat methode afdrukken Hallo apparaat antwoord toohello console en volgende toevoegen:
   
    ```
    var methodParams = {
        methodName: methodName,
        payload: 'hello world',
        timeoutInSeconds: 30
    };
   
    client.invokeDeviceMethod(deviceId, methodParams, function (err, result) {
        if (err) {
            console.error('Failed tooinvoke method \'' + methodName + '\': ' + err.message);
        } else {
            console.log(methodName + ' on ' + deviceId + ':');
            console.log(JSON.stringify(result, null, 2));
        }
    });
    ```
8. Opslaan en sluiten Hallo **CallMethodOnDevice.js** bestand.

## <a name="run-hello-apps"></a>Hallo-apps uitvoeren
U bent nu klaar toorun Hallo apps.

1. Bij een opdrachtprompt in Hallo **simulateddevice** map Hallo opdracht toostart luisteren naar methodeaanroepen van uw IoT-Hub te volgen:
   
    ```
    node SimulatedDevice.js
    ```
   
    ![][7]
2. Bij een opdrachtprompt in Hallo **callmethodondevice** map Hallo opdracht toobegin bewaking van uw IoT-hub te volgen:
   
    ```
    node CallMethodOnDevice.js 
    ```
   
    ![][8]
3. Hier ziet u Hallo apparaat toohello methode reageren door het afdrukken van het Hallo-bericht en Hallo-toepassing die weergave Hallo antwoord voor Hallo methode vanuit Hallo apparaat aangeroepen:
   
    ![][9]

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie maakt u een nieuwe iothub geconfigureerd in hello Azure-portal en vervolgens een apparaat-id in de id-register Hallo iothub hebt gemaakt. U hebt deze apparaat-id tooenable Hallo gesimuleerd apparaat app tooreact toomethods aangeroepen door Hallo cloud gebruikt. Hebt u ook een app die wordt aangeroepen methoden op Hallo apparaat en geeft weer Hallo-antwoord van Hallo-apparaat hebt gemaakt. 

toocontinue aan de slag met IoT Hub en tooexplore raadpleegt u andere IoT-scenario's:

* [Aan de slag met IoT Hub]
* [Taken plannen op meerdere apparaten][lnk-devguide-jobs]

toolearn hoe tooextend uw IoT-oplossing en schema-methode aanroepen op meerdere apparaten, raadpleegt u Hallo [planning en broadcast taken] [ lnk-tutorial-jobs] zelfstudie.

<!-- Images. -->
[7]: ./media/iot-hub-node-node-direct-methods/run-simulated-device.png
[8]: ./media/iot-hub-node-node-direct-methods/run-callmethodondevice.png
[9]: ./media/iot-hub-node-node-direct-methods/methods-output.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
[Aan de slag met IoT Hub]: iot-hub-node-node-getstarted.md
