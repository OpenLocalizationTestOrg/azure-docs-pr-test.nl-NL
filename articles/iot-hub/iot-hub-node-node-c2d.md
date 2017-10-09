---
title: aaaCloud-naar-apparaat-berichten met Azure IoT Hub (knooppunt) | Microsoft Docs
description: Hoe berichten toosend cloud-naar-apparaat tooa apparaat van een Azure IoT hub met hello Azure IoT SDK's voor Node.js. U wijzigt de berichten van een gesimuleerd apparaat app tooreceive cloud-naar-apparaat en wijzigen van een back-endserver voor apps toosend hello cloud-naar-apparaat-berichten.
services: iot-hub
documentationcenter: nodejs
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3ca8a78f-ade2-46e8-8a49-d5d599cdf1f1
ms.service: iot-hub
ms.devlang: javascript
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 1ccae0cada52193c2abb91504c086cac226e93da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-node"></a>Cloud-naar-apparaat-berichten verzenden met IoT Hub (knooppunt)
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a>Inleiding
Azure IoT Hub is een volledig beheerde service waarmee stabiele en veilige tweerichtingscommunicatie tussen miljoenen apparaten inschakelen en een back-end oplossing. Hallo [aan de slag met IoT Hub] zelfstudie laat zien hoe toocreate een IoT-hub een apparaat-id in het inrichten en code van een gesimuleerde apparaattoepassing dat apparaat-naar-cloud-berichten verzendt.

Deze zelfstudie bouwt voort op [aan de slag met IoT Hub]. Hier ziet u hoe aan:

* Verzenden van uw back-end oplossing, cloud-naar-apparaatberichten tooa één apparaat via IoT Hub.
* Cloud-naar-apparaat-berichten op een apparaat ontvangen.
* Aanvragen van uw back-end oplossing, levering bevestiging (*feedback*) voor tooa apparaat van de berichten uit IoT Hub.

U vindt meer informatie over cloud-naar-apparaat-berichten in Hallo [Ontwikkelaarshandleiding voor IoT Hub][IoT Hub developer guide - C2D].

Aan het einde van de Hallo van deze zelfstudie, moet u twee console Node.js-apps uitvoeren:

* **SimulatedDevice**, een aangepaste versie van het Hallo-app gemaakt in [aan de slag met IoT Hub], die verbinding maakt tooyour IoT-hub en cloud-naar-apparaat-berichten worden ontvangen.
* **SendCloudToDeviceMessage**, die een cloud-naar-apparaat bericht toohello gesimuleerde apparaattoepassing via IoT Hub verzendt en ontvangt u vervolgens de bevestiging levering.

> [!NOTE]
> IoT-Hub heeft SDK-ondersteuning voor veel apparaatplatforms en talen (inclusief C, Java en Javascript) via Azure IoT-apparaat-SDK's. Voor stapsgewijze instructies voor hoe tooconnect uw apparaat toothis-zelfstudie code en over het algemeen tooAzure IoT Hub zien Hallo [Azure IoT Developer Center].
> 
> 

toocomplete in deze zelfstudie, moet u hello te volgen:

* Node.js versie 0.10.x of hoger.
* Een actief Azure-account. (Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)

## <a name="receive-messages-in-hello-simulated-device-app"></a>Berichten ontvangen in de gesimuleerde apparaattoepassing Hallo
In deze sectie maakt u de gesimuleerde apparaattoepassing Hallo u hebt gemaakt in wijzigen [aan de slag met IoT Hub] tooreceive cloud-naar-apparaat-berichten uit Hallo iothub.

1. Met een teksteditor Hallo SimulatedDevice.js bestand openen.
2. Hallo wijzigen **connectCallback** toohandle berichten uit IoT Hub werken. In dit voorbeeld roept Hallo apparaat altijd Hallo **voltooid** werken toonotify IoT Hub dat deze het Hallo-bericht is verwerkt. De nieuwe versie van Hallo **connectCallback** functie eruit Hallo codefragment te volgen:
   
    ```javascript
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
        client.on('message', function (msg) {
          console.log('Id: ' + msg.messageId + ' Body: ' + msg.data);
          client.complete(msg, printResultFor('completed'));
        });
        // Create a message and send it toohello IoT Hub every second
        setInterval(function(){
            var temperature = 20 + (Math.random() * 15);
            var humidity = 60 + (Math.random() * 20);            
            var data = JSON.stringify({ deviceId: 'myFirstNodeDevice', temperature: temperature, humidity: humidity });
            var message = new Message(data);
            message.properties.add('temperatureAlert', (temperature > 30) ? 'true' : 'false');
            console.log("Sending message: " + message.getData());
            client.sendEvent(message, printResultFor('send'));
        }, 1000);
      }
    };
    ```
   
   > [!NOTE]
   > Als u HTTP in plaats van MQTT of AMQP als Hallo transport gebruikt, Hallo **DeviceClient** exemplaar wordt gecontroleerd op berichten uit IoT Hub zelden (minder dan elke 25 minuten). Zie voor meer informatie over Hallo verschillen tussen de protocollen MQTT, AMQP en HTTP-ondersteuning en Iothub beperking Hallo [Ontwikkelaarshandleiding voor IoT Hub][IoT Hub developer guide - C2D].
   > 
   > 

## <a name="send-a-cloud-to-device-message"></a>Een cloud naar apparaat verzenden
In deze sectie maakt maken u een Node.js-consoletoepassing die cloud-naar-apparaatberichten toohello gesimuleerde apparaattoepassing verzendt. U moet de apparaat-ID van het Hallo-apparaat die u hebt toegevoegd in Hallo Hallo [aan de slag met IoT Hub] zelfstudie. U moet de verbindingsreeks IoT Hub ook Hallo voor uw hub die u in Hallo vinden kunt [Azure-portal].

1. Maak een lege map genaamd **sendcloudtodevicemessage**. In Hallo **sendcloudtodevicemessage** map, een package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken. Accepteer alle Hallo standaardwaarden:
   
    ```shell
    npm init
    ```
2. Bij de opdrachtprompt in Hallo **sendcloudtodevicemessage** map na de opdracht tooinstall Hallo Hallo **azure-iothub** pakket:
   
    ```shell
    npm install azure-iothub --save
    ```
3. Maak met een teksteditor, een **SendCloudToDeviceMessage.js** bestand in Hallo **sendcloudtodevicemessage** map.
4. Voeg de volgende Hallo `require` instructies aan Hallo start Hallo **SendCloudToDeviceMessage.js** bestand:
   
    ```javascript
    'use strict';
   
    var Client = require('azure-iothub').Client;
    var Message = require('azure-iot-common').Message;
    ```
5. Hallo code te volgen toevoegen**SendCloudToDeviceMessage.js** bestand. Vervang '{iot hub verbindingsreeks}' Hallo tijdelijke aanduidingswaarde met IoT Hub-verbindingsreeks voor Hallo-hub die u hebt gemaakt in Hallo Hallo [aan de slag met IoT Hub] zelfstudie. Hallo '{apparaat-id}'-tijdelijke aanduiding vervangen door de apparaat-ID Hallo Hallo apparaat dat u hebt toegevoegd in Hallo [aan de slag met IoT Hub] zelfstudie:
   
    ```javascript
    var connectionString = '{iot hub connection string}';
    var targetDevice = '{device id}';
   
    var serviceClient = Client.fromConnectionString(connectionString);
    ```
6. Hallo functie tooprint bewerking resultaten toohello console volgende toevoegen:
   
    ```javascript
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. Hallo functie tooprint levering feedback berichten toohello console volgende toevoegen:
   
    ```javascript
    function receiveFeedback(err, receiver){
      receiver.on('message', function (msg) {
        console.log('Feedback message:')
        console.log(msg.getData().toString('utf-8'));
      });
    }
    ```
8. Hallo volgende toosend een bericht tooyour apparaat code en feedback het Hallo-bericht verwerken wanneer Hallo apparaat cloud-naar-apparaat het Hallo-bericht erkent toevoegen:
   
    ```javascript
    serviceClient.open(function (err) {
      if (err) {
        console.error('Could not connect: ' + err.message);
      } else {
        console.log('Service client connected');
        serviceClient.getFeedbackReceiver(receiveFeedback);
        var message = new Message('Cloud toodevice message.');
        message.ack = 'full';
        message.messageId = "My Message ID";
        console.log('Sending message: ' + message.getData());
        serviceClient.send(targetDevice, message, printResultFor('send'));
      }
    });
    ```
9. Opslaan en sluiten **SendCloudToDeviceMessage.js** bestand.

## <a name="run-hello-applications"></a>Hallo-toepassingen uitvoeren
U bent nu klaar toorun Hallo toepassingen.

1. Bij de opdrachtprompt Hallo in Hallo **simulateddevice** map, voert u de volgende Hallo opdracht toosend telemetrie tooIoT Hub en toolisten voor cloud-naar-apparaat-berichten:
   
    ```shell
    node SimulatedDevice.js 
    ```
   
    ![De gesimuleerde apparaattoepassing Hallo uitvoeren][img-simulated-device]
2. Bij een opdrachtprompt in Hallo **sendcloudtodevicemessage** map uitvoeren Hallo opdracht toosend na een cloud-naar-apparaat-bericht en wachten op Hallo bevestiging feedback:
   
    ```shell
    node SendCloudToDeviceMessage.js 
    ```
   
    ![Hallo app toosend Hallo cloud-naar-apparaat opdracht uitvoeren][img-send-command]
   
   > [!NOTE]
   > Deze zelfstudie implementeert voor de eenvoud mogelijk te houden, niet een beleid voor opnieuw proberen. In productiecode moet u beleid voor opnieuw proberen (zoals exponentieel uitstel), zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout].
   > 
   > 

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt u geleerd hoe toosend en cloud-naar-apparaat-berichten ontvangen. 

Voorbeelden van volledige end-to-end-oplossingen die gebruikmaken van IoT Hub toosee Zie [Azure IoT Suite].

toolearn meer informatie over het ontwikkelen van oplossingen met IoT Hub, Zie Hallo [Ontwikkelaarshandleiding voor IoT Hub].

<!-- Images -->
[img-simulated-device]: media/iot-hub-node-node-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-node-node-c2d/sendc2d.png

<!-- Links -->

[aan de slag met IoT Hub]: iot-hub-node-node-getstarted.md
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
[Ontwikkelaarshandleiding voor IoT Hub]: iot-hub-devguide.md
[Azure IoT Developer Center]: http://www.azure.com/develop/iot
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[afhandeling van tijdelijke fout]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure-portal]: https://portal.azure.com
[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
