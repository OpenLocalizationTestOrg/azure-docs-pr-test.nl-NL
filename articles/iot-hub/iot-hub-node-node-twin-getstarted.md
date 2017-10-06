---
title: aaaGet de slag met Azure IoT Hub apparaat horende (knooppunt) | Microsoft Docs
description: Hoe toouse Azure IoT Hub apparaat horende tooadd tags en gebruik vervolgens een IoT Hub-query. U gebruikt hello Azure IoT SDK's voor Node.js tooimplement Hallo gesimuleerde apparaattoepassing en een service-app die Hallo-labels toegevoegd en Hallo IoT Hub-query wordt uitgevoerd.
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: 
ms.assetid: 314c88e4-cce1-441c-b75a-d2e08e39ae7d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.openlocfilehash: d60b8c3de85e9285e496b86e27d4ee31a0554a1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-node"></a>Aan de slag met apparaat horende (knooppunt)
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

Aan het einde van de Hallo van deze zelfstudie hebt u twee console Node.js-apps:

* **AddTagsAndQuery.js**, een back-end-app van Node.js, dat labels toegevoegd en wordt opgevraagd horende apparaten.
* **TwinSimulatedDevice.js**, een Node.js-app dat een apparaat simuleert dat tooyour IoT-hub is verbonden met de apparaat-id Hallo eerder hebt gemaakt, en rapporteert de voorwaarde van de verbinding.

> [!NOTE]
> Hallo artikel [Azure IoT SDK's] [ lnk-hub-sdks] bevat informatie over hello Azure IoT SDK's waarmee u toobuild kunt apparaat- en back-end-apps.
> 
> 

toocomplete in deze zelfstudie hebt u Hallo volgende nodig:

* Node.js versie 0.10.x of hoger.
* Een actief Azure-account. (Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-service-app"></a>Hallo-service-app maken
In deze sectie maakt u een Node.js-consoletoepassing die wordt toegevoegd locatie metagegevens toohello apparaat twin die zijn gekoppeld aan **myDeviceId**. Vervolgens query's Hallo apparaat horende opgeslagen ons in IoT-hub Hallo Hallo apparaten zich in Hallo selecteren en vervolgens Hallo toepassingsgroepen die een mobiele verbinding rapporteren.

1. Maak een nieuwe lege map genaamd **addtagsandqueryapp**. In Hallo **addtagsandqueryapp** map, een nieuw package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken. Accepteer alle Hallo standaardwaarden:
   
    ```
    npm init
    ```
2. Bij de opdrachtprompt in Hallo **addtagsandqueryapp** map na de opdracht tooinstall Hallo Hallo **azure-iothub** pakket:
   
    ```
    npm install azure-iothub --save
    ```
3. Start een teksteditor en maak een nieuwe **AddTagsAndQuery.js** bestand in Hallo **addtagsandqueryapp** map.
4. Hallo na code toohello toevoegen **AddTagsAndQuery.js** -bestand en vervang Hallo **{iot hub verbindingsreeks}** aanduiding voor items met Hallo IoT Hub-verbindingsreeks die u tijdens het maken van uw hub hebt gekopieerd:
   
        'use strict';
        var iothub = require('azure-iothub');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var patch = {
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                      }
                    }
                };
   
                twin.update(patch, function(err) {
                  if (err) {
                    console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                  } else {
                    console.log(twin.deviceId + ' twin updated successfully');
                    queryTwins();
                  }
                });
            }
        });
   
    Hallo **register** object beschrijft alle Hallo methoden vereist toointeract met apparaat horende van Hallo-service. Hallo vorige code initialiseert eerst Hallo **register** object, en vervolgens haalt Hallo apparaat twin voor **myDeviceId**, en ten slotte de labels bijgewerkt met informatie over de locatie van de gewenste Hallo.
   
    Na het Hallo Hallo bijwerken tags die erin aanroepen Hallo **queryTwins** functie.
5. Toevoegen van de volgende code achter Hallo Hallo **AddTagsAndQuery.js** tooimplement hello **queryTwins** functie:
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
   
            query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43 using cellular network: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
        };
   
    de vorige code Hallo twee query's uitvoert: Hallo selecteert eerst alleen Hallo apparaat horende apparaten zich in Hallo **Redmond43** installaties en Hallo tweede verfijning Hallo query tooselect alleen Hallo apparaten die ook zijn verbonden via mobiel netwerk.
   
    Houd er rekening mee dat vorige code Hallo bij het maken van Hallo **query** object, geeft u een maximum aantal geretourneerde documenten. Hallo **query** object bevat een **hasMoreResults** Boole-eigenschap waarmee u tooinvoke hello kunt **nextAsTwin** methoden meerdere keren tooretrieve alle resulteert. Een methode aangeroepen **volgende** is beschikbaar voor de resultaten die geen apparaat horende bijvoorbeeld resultaten van query's voor aggregatie.
6. Hallo-toepassing met uitvoeren:
   
        node AddTagsAndQuery.js
   
    U ziet één apparaat in Hallo resultaten voor Hallo query vragen voor alle apparaten vinden in **Redmond43** en geen voor de Hallo-query die Hallo beperkt resultaten toodevices die gebruikmaken van een mobiel netwerk.
   
    ![][1]

In de volgende sectie Hallo maakt u een apparaat-app die Hallo connectiviteit informatie rapporteert en wijzigingen resultaat van query in de vorige sectie Hallo HALLO hallo.

## <a name="create-hello-device-app"></a>Hallo apparaattoepassing maken
In deze sectie maakt u een Node.js-consoletoepassing die verbinding tooyour hub als maakt **myDeviceId**, en vervolgens de updates die de apparaat-twin de gerapporteerd toocontain Hallo eigenschapsgegevens dat is verbonden met een mobiel netwerk.

> [!NOTE]
> Op dit moment horende apparaten zijn alleen toegankelijk vanaf apparaten die verbinding tooIoT Hub maken met Hallo MQTT-protocol. Raadpleeg toohello [MQTT ondersteuning] [ lnk-devguide-mqtt] artikel voor instructies over het tooconvert bestaande apparaat app toouse MQTT.
> 
> 

1. Maak een nieuwe lege map genaamd **reportconnectivity**. In Hallo **reportconnectivity** map, een nieuw package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken. Accepteer alle Hallo standaardwaarden:
   
    ```
    npm init
    ```
2. Bij de opdrachtprompt in Hallo **reportconnectivity** map na de opdracht tooinstall Hallo Hallo **azure-iot-device**, en **azure-iot-device-mqtt** pakket :
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Start een teksteditor en maak een nieuwe **ReportConnectivity.js** bestand in Hallo **reportconnectivity** map.
4. Hallo na code toohello toevoegen **ReportConnectivity.js** -bestand en vervang Hallo **{verbindingsreeks apparaat}** aanduiding voor items met de apparaat-verbindingsreeks voor de Hallo u tijdens het maken van Hallo gekopieerd **myDeviceId** apparaat-id:
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
   
            client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                var patch = {
                    connectivity: {
                        type: 'cellular'
                    }
                };
   
                twin.properties.reported.update(patch, function(err) {
                    if (err) {
                        console.error('could not update twin');
                    } else {
                        console.log('twin state reported');
                        process.exit();
                    }
                });
            }
            });
        }
        });
   
    Hallo **Client** object bevat alle Hallo-methoden die u nodig hebt toointeract met apparaat horende van Hallo-apparaat. vorige code Hallo nadat het Hallo initialiseert **Client** -object is opgehaald Hallo apparaat twin voor **myDeviceId** en de bijbehorende gemelde eigenschap bijgewerkt met informatie over Hallo-connectiviteit.
5. Hallo apparaat app uitvoeren
   
        node ReportConnectivity.js
   
    U ziet het Hallo-bericht `twin state reported`.
6. Nu dat hello apparaat de connectiviteit informatie gerapporteerd, moet deze worden weergegeven in beide query's. Ga terug in Hallo **addtagsandqueryapp** Hallo map en voer een query opnieuw:
   
        node AddTagsAndQuery.js
   
    Deze tijd **myDeviceId** moet worden weergegeven in beide queryresultaten.
   
    ![][3]

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie maakt u een nieuwe iothub geconfigureerd in hello Azure-portal en vervolgens een apparaat-id in de id-register Hallo iothub hebt gemaakt. U metagegevens van apparaten als labels toegevoegd vanuit een back-end-app en een gesimuleerd apparaat app tooreport-apparaatgegevens connectiviteit in Hallo apparaat twin geschreven. U hebt ook geleerd hoe tooquery deze informatie Hallo IoT-Hub SQL-achtige query language gebruiken.

Gebruik Hallo resources toolearn hoe volgende aan:

* verzenden van telemetrie vanaf apparaten Hello [aan de slag met IoT Hub] [ lnk-iothub-getstarted] zelfstudie
* apparaten configureren met de gewenste eigenschappen van apparaat twin Hello [gebruik gewenst eigenschappen tooconfigure apparaten] [ lnk-twin-how-to-configure] zelfstudie
* beheren van apparaten interactief (zoals het inschakelen van een ventilator van een gebruiker beheerde app), met Hallo [direct methoden gebruiken] [ lnk-methods-tutorial] zelfstudie.

<!-- images -->
[1]: media/iot-hub-node-node-twin-getstarted/service1.png
[3]: media/iot-hub-node-node-twin-getstarted/service2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/

[lnk-twin-how-to-configure]: iot-hub-node-node-twin-how-to-configure.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
