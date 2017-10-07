---
title: aaaUse Azure IoT Hub twin apparaateigenschappen (knooppunt) | Microsoft Docs
description: Hoe toouse Azure IoT Hub apparaat horende tooconfigure apparaten. U gebruikt hello Azure IoT SDK's voor Node.js tooimplement een gesimuleerde apparaattoepassing en een service-app die de apparaatconfiguratie van een met behulp van een apparaat-twin wijzigt.
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: d0bcec50-26e6-40f0-8096-733b2f3071ec
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/13/2016
ms.author: elioda
ms.openlocfilehash: 7ebfe2dfa0876bf04fdbaceae55db76456523e8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices-node"></a>Gebruik gewenst eigenschappen tooconfigure apparaten (knooppunt)
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

Aan het einde van de Hallo van deze zelfstudie hebt u twee console Node.js-apps:

* **SimulateDeviceConfiguration.js**, een gesimuleerde apparaattoepassing die wordt gewacht op een gewenste configuratie-update en rapporten Hallo status van een gesimuleerde configuratieproces voor de update.
* **SetDesiredConfigurationAndQuery.js**, een Node.js back-end-app, die ingesteld Hallo gewenste configuratie op een apparaat en query's Hallo update configuratieproces.

> [!NOTE]
> Hallo artikel [Azure IoT SDK's] [ lnk-hub-sdks] bevat informatie over hello Azure IoT SDK's waarmee u toobuild kunt apparaat- en back-end-apps.
> 
> 

toocomplete in deze zelfstudie hebt u Hallo volgende nodig:

* Node.js versie 0.10.x of hoger.
* Een actief Azure-account. (Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)

Als u Hallo gevolgd [aan de slag met apparaat horende] [ lnk-twin-tutorial] zelfstudie, u hebt al een IoT-hub en een apparaat-id genoemd **myDeviceId**; en kunt u toohello overslaan[ Hallo gesimuleerde apparaattoepassing maken] [ lnk-how-to-configure-createapp] sectie.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-simulated-device-app"></a>Hallo gesimuleerde apparaattoepassing maken
In deze sectie maakt u een Node.js-consoletoepassing die verbinding tooyour hub als maakt **myDeviceId**, wordt gewacht op een gewenste configuratie-update en vervolgens rapporten updates op Hallo gesimuleerde update configuratieproces.

1. Maak een nieuwe lege map genaamd **simulatedeviceconfiguration**. In Hallo **simulatedeviceconfiguration** map, een nieuw package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken. Accepteer alle Hallo standaardwaarden:
   
    ```
    npm init
    ```
2. Bij de opdrachtprompt in Hallo **simulatedeviceconfiguration** map na de opdracht tooinstall Hallo Hallo **azure-iot-device**, en **azure-iot-device-mqtt**pakket:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Start een teksteditor en maak een nieuwe **SimulateDeviceConfiguration.js** bestand in Hallo **simulatedeviceconfiguration** map.
4. Hallo na code toohello toevoegen **SimulateDeviceConfiguration.js** -bestand en vervang Hallo **{verbindingsreeks apparaat}** aanduiding voor items met de verbindingsreeks voor Hallo apparaat u hebt gekopieerd wanneer u Hallo gemaakt **myDeviceId** apparaat-id:
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
            if (err) {
                console.error('could not open IotHub client');
            } else {
                client.getTwin(function(err, twin) {
                    if (err) {
                        console.error('could not get twin');
                    } else {
                        console.log('retrieved device twin');
                        twin.properties.reported.telemetryConfig = {
                            configId: "0",
                            sendFrequency: "24h"
                        }
                        twin.on('properties.desired', function(desiredChange) {
                            console.log("received change: "+JSON.stringify(desiredChange));
                            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
                            if (desiredChange.telemetryConfig &&desiredChange.telemetryConfig.configId !== currentTelemetryConfig.configId) {
                                initConfigChange(twin);
                            }
                        });
                    }
                });
            }
        });
   
    Hallo **Client** object beschrijft alle Hallo methoden vereist toointeract met apparaat horende van Hallo-apparaat. vorige code Hallo nadat het Hallo initialiseert **Client** -object is opgehaald Hallo apparaat twin voor **myDeviceId**, en koppelt u een handler voor Hallo-update op de gewenste eigenschappen. Hallo-handler controleert of dat er een wijzigingsaanvraag voor de huidige configuratie door te vergelijken Hallo configIds is, wordt een methode die de configuratiewijziging Hallo begint roept.
   
    Houd er rekening mee dat voor Hallo mogelijk te houden van eenvoud, Hallo vorige code een vastgelegde standaardinstallatielocatie voor de initiële configuratie Hallo gebruikt. Een echte app zou waarschijnlijk dat de configuratie van een lokale opslag laden.
   
   > [!IMPORTANT]
   > Gewenste eigenschap wijzigingsgebeurtenissen altijd één keer worden verzonden op het apparaatverbinding en zorg ervoor dat er sprake is van een werkelijke wijziging in Hallo toocheck gewenst eigenschappen voordat u een actie uitvoert.
   > 
   > 
5. Toevoegen van de volgende methoden voordat Hallo Hallo `client.open()` aanroepen:
   
        var initConfigChange = function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.pendingConfig = twin.properties.desired.telemetryConfig;
            currentTelemetryConfig.status = "Pending";
   
            var patch = {
            telemetryConfig: currentTelemetryConfig
            };
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.log('Could not report properties');
                } else {
                    console.log('Reported pending config change: ' + JSON.stringify(patch));
                    setTimeout(function() {completeConfigChange(twin);}, 60000);
                }
            });
        }
   
        var completeConfigChange =  function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.configId = currentTelemetryConfig.pendingConfig.configId;
            currentTelemetryConfig.sendFrequency = currentTelemetryConfig.pendingConfig.sendFrequency;
            currentTelemetryConfig.status = "Success";
            delete currentTelemetryConfig.pendingConfig;
   
            var patch = {
                telemetryConfig: currentTelemetryConfig
            };
            patch.telemetryConfig.pendingConfig = null;
   
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.error('Error reporting properties: ' + err);
                } else {
                    console.log('Reported completed config change: ' + JSON.stringify(patch));
                }
            });
        };
   
    Hallo **initConfigChange** methode updates gerapporteerd eigenschappen Hallo lokale apparaat twin object met de configuratieaanvraag update Hallo en stelt de status te Hallo**in behandeling**, en vervolgens de updates Hallo apparaat Twin op Hallo-service. Nadat Hallo apparaat twin is bijgewerkt, wordt een langdurige proces dat wordt beëindigd bij uitvoering van Hallo gesimuleerd **completeConfigChange**. Deze methode updates Hallo lokale apparaat twin de eigenschappen te Hallo status instellen gerapporteerd**geslaagd** en verwijderen van Hallo **pendingConfig** object. Hallo apparaat twin op Hallo-service wordt vervolgens bijgewerkt.
   
    Die toosave bandbreedte, gerapporteerd eigenschappen zijn bijgewerkt door te geven alleen Hallo eigenschappen toobe gewijzigd (met de naam **patch** in Hallo bovenstaande code), in plaats van het hele document Hallo vervangen.
   
   > [!NOTE]
   > Deze zelfstudie wordt een gedrag voor updates voor gelijktijdige configuratie niet simuleren. Bepaalde configuratie-update-processen mogelijk wijzigingen van de doelconfiguratie kunnen tooaccommodate terwijl Hallo update wordt uitgevoerd, anderen mogelijk tooqueue deze en andere kunnen weigeren met een fout opgetreden. Zorg ervoor dat tooconsider Hallo gewenste gedrag voor uw specifieke configuratieproces en Hallo juiste logica toevoegen voordat u begint Hallo configuratiewijziging.
   > 
   > 
6. Hallo apparaattoepassing uitvoeren:
   
        node SimulateDeviceConfiguration.js
   
    U ziet het Hallo-bericht `retrieved device twin`. Houd Hallo-app die wordt uitgevoerd.

## <a name="create-hello-service-app"></a>Hallo-service-app maken
In deze sectie maakt u een Node.js-consoletoepassing die updates Hallo *gewenst eigenschappen* op Hallo apparaat twin gekoppeld **myDeviceId** met een nieuwe telemetrie configuration-object. Vervolgens vraagt Hallo apparaat horende opgeslagen in Hallo IoT-hub en toont Hallo verschil tussen Hallo gewenst en configuraties van Hallo apparaat gerapporteerd.

1. Maak een nieuwe lege map genaamd **setdesiredandqueryapp**. In Hallo **setdesiredandqueryapp** map, een nieuw package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken. Accepteer alle Hallo standaardwaarden:
   
    ```
    npm init
    ```
2. Bij de opdrachtprompt in Hallo **setdesiredandqueryapp** map na de opdracht tooinstall Hallo Hallo **azure-iothub** pakket:
   
    ```
    npm install azure-iothub node-uuid --save
    ```
3. Start een teksteditor en maak een nieuwe **SetDesiredAndQuery.js** bestand in Hallo **addtagsandqueryapp** map.
4. Hallo na code toohello toevoegen **SetDesiredAndQuery.js** -bestand en vervang Hallo **{iot hub verbindingsreeks}** aanduiding voor items met Hallo IoT Hub-verbindingsreeks die u tijdens het maken van uw hub gekopieerd :
   
        'use strict';
        var iothub = require('azure-iothub');
        var uuid = require('node-uuid');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var newConfigId = uuid.v4();
                var newFrequency = process.argv[2] || "5m";
                var patch = {
                    properties: {
                        desired: {
                            telemetryConfig: {
                                configId: newConfigId,
                                sendFrequency: newFrequency
                            }
                        }
                    }
                }
                twin.update(patch, function(err) {
                    if (err) {
                        console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                    } else {
                        console.log(twin.deviceId + ' twin updated successfully');
                    }
                });
                setInterval(queryTwins, 10000);
            }
        });

    Hallo **register** object beschrijft alle Hallo methoden vereist toointeract met apparaat horende van Hallo-service. vorige code Hallo nadat het Hallo initialiseert **register** -object is opgehaald Hallo apparaat twin voor **myDeviceId**, en de gewenste eigenschappen bijgewerkt met een nieuwe telemetrie configuration-object. Daarna roept Hallo **queryTwins** werken gebeurtenis 10 seconden.

    > [!IMPORTANT]
    > Deze toepassing een IoT Hub query elke 10 seconden ter illustratie. Gebruik een query toogenerate gebruikersgerichte rapporten over veel apparaten, en niet toodetect wijzigingen. Als uw oplossing realtime meldingen over apparaatgebeurtenissen vereist, gebruikt u [twin meldingen][lnk-twin-notifications].
    > 
    >.

1. Toevoegen van de volgende code precies vóór Hallo Hallo `registry.getDeviceTwin()` aanroep tooimplement hello **queryTwins** functie:
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log();
                    results.forEach(function(twin) {
                        var desiredConfig = twin.properties.desired.telemetryConfig;
                        var reportedConfig = twin.properties.reported.telemetryConfig;
                        console.log("Config report for: " + twin.deviceId);
                        console.log("Desired: ");
                        console.log(JSON.stringify(desiredConfig, null, 2));
                        console.log("Reported: ");
                        console.log(JSON.stringify(reportedConfig, null, 2));
                    });
                }
            });
        };
   
    Hallo vorige code query's Hallo apparaat horende opgeslagen in Hallo IoT-hub en afdrukken bestellen Hallo gewenst en telemetrie configuraties gerapporteerd. Raadpleeg toohello [IoT Hub-querytaal] [ lnk-query] toolearn hoe toogenerate rich op alle apparaten in uw rapporten.
2. Met **SimulateDeviceConfiguration.js** toepassing hello met wordt uitgevoerd, worden uitgevoerd:
   
        node SetDesiredAndQuery.js 5m
   
    Er is gemeld Hallo-configuratie wijzigen vanuit **geslaagd** te**in behandeling** te**geslaagd** opnieuw met de nieuwe actief Hallo verzenden frequentie van vijf minuten in plaats van 24 uren.
   
   > [!IMPORTANT]
   > Er is een vertraging van up tooa minuut tussen Hallo apparaat rapport opnieuw en Hallo queryresultaat. Dit is tooenable Hallo query infrastructuur toowork op zeer grote schaal. tooretrieve consistente weergaven van een enkel apparaat twin gebruiken Hallo **getDeviceTwin** methode in Hallo **register** klasse.
   > 
   > 

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie stelt u een gewenste configuratie als *gewenst eigenschappen* vanuit een back-end-app en een gesimuleerd apparaat app toodetect die wijzigen en een updateproces van meerdere stappen zijn status als reporting simuleren geschreven  *Eigenschappen gerapporteerd* toohello apparaat twin.

Gebruik Hallo resources toolearn hoe volgende aan:

* verzenden van telemetrie vanaf apparaten Hello [aan de slag met IoT Hub] [ lnk-iothub-getstarted] zelfstudie
* plannen of uitvoeren van bewerkingen op grote sets van apparaten Zie Hallo [planning en broadcast taken] [ lnk-schedule-jobs] zelfstudie.
* beheren van apparaten interactief (zoals het inschakelen van een ventilator van een gebruiker beheerde app), met Hallo [direct methoden gebruiken] [ lnk-methods-tutorial] zelfstudie.

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: iot-hub-device-management-overview.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-node-node-twin-how-to-configure.md#create-the-simulated-device-app
