---
title: aaaGet de slag met Azure IoT Hub (knooppunt) | Microsoft Docs
description: Meer informatie over hoe toosend apparaat-naar-cloud-berichten tooAzure IoT Hub met IoT SDK's voor Node.js. Gesimuleerde apparaat en service-apps tooregister uw apparaat maken en berichten uit iothub berichten verzenden.
services: iot-hub
documentationcenter: nodejs
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 56618522-9a31-42c6-94bf-55e2233b39ac
ms.service: iot-hub
ms.devlang: javascript
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0747895365f2359a9c38ea1e85a5881d6efec0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-node"></a>Verbinding maken met uw gesimuleerde apparaat tooyour iothub met behulp van knooppunt
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

Aan het einde van de Hallo van deze zelfstudie hebt u drie Node.js console apps:

* **CreateDeviceIdentity.js**, die een apparaat-id maakt en gekoppelde beveiliging sleutel tooconnect app op uw gesimuleerde apparaat.
* **ReadDeviceToCloudMessages.js**, wordt verzonden door uw gesimuleerde apparaattoepassing Hallo-telemetrie.
* **SimulatedDevice.js**, die tooyour IoT-hub aan Hallo apparaat-id eerder hebt gemaakt, en verzendt een elke tweede met behulp van protocollen MQTT protocol Hallo telemetrie-bericht.

> [!NOTE]
> Hallo artikel [Azure IoT SDK's] [ lnk-hub-sdks] bevat informatie over hello Azure IoT SDK's waarmee u toobuild beide toorun toepassingen op apparaten en de back-end van uw oplossing kunt.
> 
> 

toocomplete in deze zelfstudie, moet u hello te volgen:

* Node.js versie 0.10.x of hoger.
* Een actief Azure-account. (Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

U hebt nu uw IoT-hub gemaakt. U hebt Hallo IoT Hub-hostnaam en Hallo IoT Hub-verbindingsreeks moet u toocomplete Hallo rest van deze handleiding.

## <a name="create-a-device-identity"></a>Een apparaat-id maken
In deze sectie maakt maken u een Node.js-consoletoepassing die een apparaat-id in Hallo identiteitenregister van uw IoT-hub maakt. Een apparaat kan alleen verbinding maken met tooIoT hub als er een vermelding in het identiteitenregister Hallo. Zie voor meer informatie, Hallo **Identiteitsregister** sectie Hallo [Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide-identity]. Wanneer u deze consoletoepassing uitvoert, wordt een unieke apparaat-ID gegenereerd en sleutel waarmee het apparaat tooidentify zelf kunt wanneer het apparaat-naar-cloud verzendt berichten tooIoT Hub.

1. Maak een nieuwe lege map met de naam **createdeviceidentity**. In Hallo **createdeviceidentity** map, een package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken. Accepteer alle Hallo standaardwaarden:
   
    ```
    npm init
    ```
2. Bij de opdrachtprompt in Hallo **createdeviceidentity** map na de opdracht tooinstall Hallo Hallo **azure-iothub** Service SDK-pakket:
   
    ```
    npm install azure-iothub --save
    ```
3. Maak met een teksteditor, een **CreateDeviceIdentity.js** bestand in Hallo **createdeviceidentity** map.
4. Voeg de volgende Hallo `require` instructie aan begin Hallo Hallo **CreateDeviceIdentity.js** bestand:
   
    ```
    'use strict';
   
    var iothub = require('azure-iothub');
    ```
5. Hallo na code toohello toevoegen **CreateDeviceIdentity.js** -bestand en vervang Hallo tijdelijke aanduidingswaarde met IoT Hub-verbindingsreeks voor Hallo-hub die u hebt gemaakt in de vorige sectie Hallo Hallo: 
   
    ```
    var connectionString = '{iothub connection string}';
   
    var registry = iothub.Registry.fromConnectionString(connectionString);
    ```
6. Voeg Hallo code toocreate een definitie van het apparaat in Hallo identiteitenregister van uw IoT-hub te volgen. Deze code maakt een apparaat als Hallo apparaat-ID bestaat niet in het identiteitenregister hello, anders wordt het Hallo-sleutel van de bestaande apparaat Hallo:
   
    ```
    var device = {
      deviceId: 'myFirstNodeDevice'
    }
    registry.create(device, function(err, deviceInfo, res) {
      if (err) {
        registry.get(device.deviceId, printDeviceInfo);
      }
      if (deviceInfo) {
        printDeviceInfo(err, deviceInfo, res)
      }
    });
   
    function printDeviceInfo(err, deviceInfo, res) {
      if (deviceInfo) {
        console.log('Device ID: ' + deviceInfo.deviceId);
        console.log('Device key: ' + deviceInfo.authentication.symmetricKey.primaryKey);
      }
    }
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

7. Sla het bestand **CreateDeviceIdentity.js** op en sluit het.
8. Hallo toorun **createdeviceidentity** -toepassing uitvoeren van de volgende opdracht achter de opdrachtprompt Hallo in de map createdeviceidentity Hallo Hallo:
   
    ```
    node CreateDeviceIdentity.js 
    ```
9. Maak een notitie van Hallo **apparaat-ID** en **apparaatsleutel**. U moet deze waarden later bij het maken van een toepassing die tooIoT Hub als apparaat verbinding maakt.

> [!NOTE]
> Hallo id-register IoT Hub bewaart alleen apparaat-id's tooenable veilige toegang toohello IoT-hub. Apparaat-id's en sleutels toouse worden opgeslagen als beveiligingsreferenties en waarmee u toodisable toegang tot een afzonderlijk apparaat kunt vlag voor ingeschakeld/uitgeschakeld. Als uw toepassing toostore andere apparaatspecifieke metagegevens moet, moet deze een toepassingsspecifieke opslagmethode gebruiken. Zie voor meer informatie, Hallo [Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide-identity].
> 
> 

<a id="D2C_node"></a>
## <a name="receive-device-to-cloud-messages"></a>Apparaat-naar-cloud-berichten ontvangen
In dit gedeelte maakt u een Node.js-consoletoepassing die apparaat-naar-cloud-berichten uit IoT Hub leest. Een iothub toont een [Event Hubs][lnk-event-hubs-overview]-compatibel eindpunt tooenable u tooread apparaat-naar-cloud-berichten. tookeep dingen eenvoudige, deze zelfstudie maakt u een basislezer die niet geschikt voor een implementatie met hoge doorvoer. Hallo [apparaat-naar-cloud-berichten verwerken] [ lnk-process-d2c-tutorial] zelfstudie laat zien hoe tooprocess apparaat-naar-cloud-berichten op grote schaal. Hallo [aan de slag met Event Hubs] [ lnk-eventhubs-tutorial] zelfstudie bevat meer informatie over hoe tooprocess van berichten van Event Hubs en toepasselijke toohello IoT Hub Event Hub-compatibele eindpunten is.

> [!NOTE]
> Hallo Event Hub-compatibele eindpunt voor het lezen van apparaat-naar-cloudberichten altijd gebruikt Hallo AMQP-protocol.
> 
> 

1. Maak een lege map met de naam **readdevicetocloudmessages**. In Hallo **readdevicetocloudmessages** map, een package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken. Accepteer alle Hallo standaardwaarden:
   
    ```
    npm init
    ```
2. Bij de opdrachtprompt in Hallo **readdevicetocloudmessages** map na de opdracht tooinstall Hallo Hallo **azure-event-hubs** pakket:
   
    ```
    npm install azure-event-hubs --save
    ```
3. Maak met een teksteditor, een **ReadDeviceToCloudMessages.js** bestand in Hallo **readdevicetocloudmessages** map.
4. Voeg de volgende Hallo `require` instructies aan Hallo start Hallo **ReadDeviceToCloudMessages.js** bestand:
   
    ```
    'use strict';
   
    var EventHubClient = require('azure-event-hubs').Client;
    ```
5. Hallo na variabelendeclaratie toevoegen en vervang Hallo tijdelijke aanduidingswaarde met Hallo IoT Hub-verbindingsreeks voor uw hub:
   
    ```
    var connectionString = '{iothub connection string}';
    ```
6. Na twee functies die uitvoer toohello console afdrukken Hallo toevoegen:
   
    ```
    var printError = function (err) {
      console.log(err.message);
    };
   
    var printMessage = function (message) {
      console.log('Message received: ');
      console.log(JSON.stringify(message.body));
      console.log('');
    };
    ```
7. Toevoegen van de volgende code toocreate Hallo Hallo **EventHubClient**Hallo verbinding tooyour IoT Hub en opent een ontvanger voor elke partitie maken. Deze toepassing gebruikt een filter bij het maken van een ontvanger zodat hello ontvanger alleen berichten tooIoT Hub leest nadat Hallo ontvanger is geactiveerd. Dit filter is handig in een testomgeving zodat u alleen Hallo huidige reeks berichten zien. In een productieomgeving moet uw code ervoor zorgen dat alle Hallo-berichten worden verwerkt. Zie voor meer informatie, Hallo [hoe tooprocess IoT Hub apparaat-naar-cloud-berichten] [ lnk-process-d2c-tutorial] zelfstudie:
   
    ```
    var client = EventHubClient.fromConnectionString(connectionString);
    client.open()
        .then(client.getPartitionIds.bind(client))
        .then(function (partitionIds) {
            return partitionIds.map(function (partitionId) {
                return client.createReceiver('$Default', partitionId, { 'startAfterTime' : Date.now()}).then(function(receiver) {
                    console.log('Created partition receiver: ' + partitionId)
                    receiver.on('errorReceived', printError);
                    receiver.on('message', printMessage);
                });
            });
        })
        .catch(printError);
    ```
8. Opslaan en sluiten Hallo **ReadDeviceToCloudMessages.js** bestand.

## <a name="create-a-simulated-device-app"></a>Een gesimuleerde apparaattoepassing maken
In deze sectie maakt u een Node.js-consoletoepassing die een apparaat simuleert dat apparaat-naar-cloudberichten tooan iothub verzendt.

1. Maak een lege map met de naam **simulateddevice**. In Hallo **simulateddevice** map, een package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken. Accepteer alle Hallo standaardwaarden:
   
    ```
    npm init
    ```
2. Bij de opdrachtprompt in Hallo **simulateddevice** map na de opdracht tooinstall Hallo Hallo **azure-iot-device** apparaat-SDK-pakket en **azure-iot-device-mqtt**pakket:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Maak met een teksteditor, een **SimulatedDevice.js** bestand in Hallo **simulateddevice** map.
4. Voeg de volgende Hallo `require` instructies aan Hallo start Hallo **SimulatedDevice.js** bestand:
   
    ```
    'use strict';
   
    var clientFromConnectionString = require('azure-iot-device-mqtt').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    ```
5. Voeg een **connectionString** variabele en gebruik deze toocreate een **Client** exemplaar. Vervang **{youriothostname}** met de naam van de Hallo van Hallo IoT-hub die u hebt gemaakt Hallo *een IoT Hub maken* sectie. Vervang **{yourdevicekey}** met Hallo apparaat sleutelwaarde u hebt gegenereerd in Hallo *maken van een apparaat-id* sectie:
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myFirstNodeDevice;SharedAccessKey={yourdevicekey}';
   
    var client = clientFromConnectionString(connectionString);
    ```
6. Hallo functie toodisplay uitvoer van de toepassing hello volgende toevoegen:
   
    ```
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. Maak een callback en gebruik Hallo **setInterval** toosend een bericht tooyour IoT-hub elke seconde werken:
   
    ```
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
   
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
8. Open Hallo verbinding tooyour IoT Hub en beginnen met het verzenden van berichten:
   
    ```
    client.open(connectCallback);
    ```
9. Opslaan en sluiten Hallo **SimulatedDevice.js** bestand.

> [!NOTE]
> tookeep dingen eenvoudige, deze zelfstudie wordt niet geïmplementeerd voor een beleid voor opnieuw proberen. In productiecode moet u beleid voor opnieuw proberen (zoals exponentieel uitstel), zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout][lnk-transient-faults].
> 
> 

## <a name="run-hello-apps"></a>Hallo-apps uitvoeren
U bent nu klaar toorun Hallo apps.

1. Bij een opdrachtprompt in Hallo **readdevicetocloudmessages** map Hallo opdracht toobegin bewaking van uw IoT-hub te volgen:
   
    ```
    node ReadDeviceToCloudMessages.js 
    ```
   
    ![Node.js IoT Hub service app toomonitor apparaat-naar-cloud-berichten][7]
2. Bij een opdrachtprompt in Hallo **simulateddevice** map Hallo opdracht toobegin verzenden van telemetrie gegevens tooyour IoT-hub te volgen:
   
    ```
    node SimulatedDevice.js
    ```
   
    ![Node.js IoT Hub apparaat-app toosend apparaat-naar-cloud-berichten][8]
3. Hallo **gebruik** -tegel in Hallo [Azure-portal] [ lnk-portal] toont Hallo aantal verzonden berichten toohello IoT-hub:
   
    ![Azure portal gebruik tegel met aantal verzonden berichten tooIoT Hub][43]

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie maakt u een nieuwe iothub geconfigureerd in hello Azure-portal en vervolgens een apparaat-id in de id-register Hallo iothub hebt gemaakt. U hebt deze apparaat-id tooenable Hallo gesimuleerd apparaat app toosend apparaat-naar-cloudberichten toohello iothub gebruikt. Hebt u ook een app die wordt weergegeven Hallo-berichten dat is ontvangen door de Hallo iothub hebt gemaakt. 

toocontinue aan de slag met IoT Hub en tooexplore raadpleegt u andere IoT-scenario's:

* [Verbinding maken met uw apparaat][lnk-connect-device]
* [Aan de slag met apparaatbeheer][lnk-device-management]
* [Aan de slag met Azure IoT Edge][lnk-iot-edge]

toolearn hoe tooextend uw IoT-oplossing en proces apparaat-naar-cloud-berichten op grote schaal, zien Hallo [apparaat-naar-cloud-berichten verwerken] [ lnk-process-d2c-tutorial] zelfstudie.
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]


<!-- Images. -->
[7]: ./media/iot-hub-node-node-getstarted/runapp1.png
[8]: ./media/iot-hub-node-node-getstarted/runapp2.png
[43]: ./media/iot-hub-csharp-csharp-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
