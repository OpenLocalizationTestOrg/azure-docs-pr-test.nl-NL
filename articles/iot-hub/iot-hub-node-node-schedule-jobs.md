---
title: aaaSchedule taken met Azure IoT Hub (knooppunt) | Microsoft Docs
description: Hoe een Azure-IoT-Hub tooschedule taak tooinvoke een directe methode op meerdere apparaten. U hello Azure IoT SDK's gebruiken voor Node.js tooimplement Hallo gesimuleerd apparaat-apps en een app toorun Hallo taak.
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 2233356e-b005-4765-ae41-3a4872bda943
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: be293362447fbcddaa3433b66f208f22545fe0c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-node"></a>Planning en broadcast-taken (knooppunt)

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

Azure IoT Hub is een volledig beheerde service waarmee u een back-endserver voor apps toocreate en bijhouden taken die gepland en miljoenen apparaten werken.  Taken kunnen worden gebruikt voor Hallo van de volgende activiteiten:

* Gewenste eigenschappen bijwerken
* Labels bijwerken
* Directe methoden aanroepen

In dat geval een taak verpakt een van deze acties en houdt Hallo voortgang van de uitvoering op basis van een verzameling apparaten, dit wordt gedefinieerd door een apparaat twin query.  Bijvoorbeeld, kunt een back-endserver voor apps gebruiken een taak tooinvoke een methode voor opnieuw opstarten op 10.000 apparaten, is opgegeven door een apparaat twin query en gepland op een later tijdstip.  Deze toepassing kunt vervolgens voortgang bijhouden als elk van deze apparaten ontvangen en Hallo opnieuw opstarten methode uitvoeren.

Meer informatie over elk van deze mogelijkheden in deze artikelen:

* Apparaat-twin en eigenschappen: [aan de slag met apparaat horende] [ lnk-get-started-twin] en [zelfstudie: hoe toouse apparaat eigenschappen twin][lnk-twin-props]
* directe methoden: [IoT Hub developer guide - rechtstreekse methoden] [ lnk-dev-methods] en [zelfstudie: directe methoden][lnk-c2d-methods]

In deze handleiding ontdekt u hoe u:

* Maken van een gesimuleerde apparaattoepassing met een directe methode waarmee **lockDoor** die kan worden aangeroepen door Hallo back-end oplossing.
* Een Node.js-consoletoepassing maken die Hallo aanroepen **lockDoor** directe methode in een gesimuleerde apparaattoepassing Hallo met behulp van een taak en updates Hallo gewenst eigenschappen met behulp van een taak van het apparaat.

Aan het einde van de Hallo van deze zelfstudie hebt u twee console Node.js-apps:

**simDevice.js**, die tooyour IoT-hub aan Hallo apparaat-id en ontvangt een **lockDoor** directe methode.

**scheduleJobService.js**, die een methode wordt aangeroepen direct in Hallo gesimuleerd apparaat app en update Hallo apparaat twin de gewenste eigenschappen met behulp van een taak.

toocomplete in deze zelfstudie, moet u hello te volgen:

* Node.js-versie 0.12.x of hoger <br/>  [Uw ontwikkelingsomgeving voorbereiden] [ lnk-dev-setup] wordt beschreven hoe tooinstall Node.js voor deze zelfstudie op Windows of Linux.
* Een actief Azure-account. (Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Een gesimuleerde apparaattoepassing maken
In deze sectie maken van een Node.js-consoletoepassing die reageert tooa directe methode aangeroepen door Hallo cloud, die een herstart van het gesimuleerde apparaat activeert en maakt gebruik van Hallo gerapporteerd eigenschappen tooenable apparaat twin query's tooidentify apparaten en wanneer ze laatste opnieuw opgestart.

1. Maak een nieuwe lege map genaamd **simDevice**.  In Hallo **simDevice** map, een package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken.  Accepteer alle Hallo standaardwaarden:
   
    ```
    npm init
    ```
2. Bij de opdrachtprompt in Hallo **simDevice** map na de opdracht tooinstall Hallo Hallo **azure-iot-device** apparaat-SDK-pakket en **azure-iot-device-mqtt** pakket:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Start een teksteditor en maak een nieuwe **simDevice.js** bestand in Hallo **simDevice** map.
4. Toevoegen van de volgende Hallo 'vereist' instructies toe aan Hallo begin Hallo **simDevice.js** bestand:
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. Voeg een **connectionString** variabele en gebruik deze toocreate een **Client** exemplaar.  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. Toevoegen van de volgende functie toohandle Hallo Hallo **lockDoor** methode.
   
    ```
    var onLockDoor = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```
7. Toevoegen van de volgende code tooregister Hallo-handler voor Hallo Hallo **lockDoor** methode.
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub. Register handler for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```
8. Opslaan en sluiten Hallo **simDevice.js** bestand.

> [!NOTE]
> tookeep dingen eenvoudige, deze zelfstudie wordt niet geïmplementeerd voor een beleid voor opnieuw proberen. In productiecode moet u beleid voor opnieuw proberen (zoals exponentieel uitstel), zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout][lnk-transient-faults].
> 
> 

## <a name="schedule-jobs-for-calling-a-direct-method-and-updating-a-device-twins-properties"></a>Plannen van taken voor het aanroepen van een directe methode en de eigenschappen voor een apparaat-twin bijwerken
In deze sectie maakt u een Node.js-consoletoepassing die een externe Start **lockDoor** op een apparaat met behulp van een directe methode en update Hallo apparaat twin van eigenschappen.

1. Maak een nieuwe lege map genaamd **scheduleJobService**.  In Hallo **scheduleJobService** map, een package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken.  Accepteer alle Hallo standaardwaarden:
   
    ```
    npm init
    ```
2. Bij de opdrachtprompt in Hallo **scheduleJobService** map na de opdracht tooinstall Hallo Hallo **azure-iothub** apparaat-SDK-pakket en **azure-iot-device-mqtt**pakket:
   
    ```
    npm install azure-iothub uuid --save
    ```
3. Start een teksteditor en maak een nieuwe **scheduleJobService.js** bestand in Hallo **scheduleJobService** map.
4. Toevoegen van de volgende Hallo 'vereist' instructies toe aan Hallo begin Hallo **dmpatterns_gscheduleJobServiceetstarted_service.js** bestand:
   
    ```
    'use strict';
   
    var uuid = require('uuid');
    var JobClient = require('azure-iothub').JobClient;
    ```
5. Hallo na variabelendeclaraties toevoegen en vervang de waarden van de tijdelijke aanduiding Hallo:
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var queryCondition = "deviceId IN ['myDeviceId']";
    var startTime = new Date();
    var maxExecutionTimeInSeconds =  3600;
    var jobClient = JobClient.fromConnectionString(connectionString);
    ```
6. Hallo volgen functie die wordt gebruikt toomonitor Hallo uitvoering van Hallo taak toevoegen:
   
    ```
    function monitorJob (jobId, callback) {
        var jobMonitorInterval = setInterval(function() {
            jobClient.getJob(jobId, function(err, result) {
            if (err) {
                console.error('Could not get job status: ' + err.message);
            } else {
                console.log('Job: ' + jobId + ' - status: ' + result.status);
                if (result.status === 'completed' || result.status === 'failed' || result.status === 'cancelled') {
                clearInterval(jobMonitorInterval);
                callback(null, result);
                }
            }
            });
        }, 5000);
    }
    ```
7. Hallo code tooschedule Hallo taak die Hallo apparaat methode aanroept volgende toevoegen:
   
    ```
    var methodParams = {
        methodName: 'lockDoor',
        payload: null,
        responseTimeoutInSeconds: 15 // Timeout after 15 seconds if device is unable tooprocess method
    };
   
    var methodJobId = uuid.v4();
    console.log('scheduling Device Method job with id: ' + methodJobId);
    jobClient.scheduleDeviceMethod(methodJobId,
                                queryCondition,
                                methodParams,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule device method job: ' + err.message);
        } else {
            monitorJob(methodJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor device method job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
8. Hallo code tooschedule Hallo taak tooupdate Hallo apparaat twin volgende toevoegen:
   
    ```
    var twinPatch = {
        etag: '*',
        desired: {
            building: '43',
            floor: 3
        }
    };
   
    var twinJobId = uuid.v4();
   
    console.log('scheduling Twin Update job with id: ' + twinJobId);
    jobClient.scheduleTwinUpdate(twinJobId,
                                queryCondition,
                                twinPatch,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule twin update job: ' + err.message);
        } else {
            monitorJob(twinJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor twin update job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
9. Opslaan en sluiten Hallo **scheduleJobService.js** bestand.

## <a name="run-hello-applications"></a>Hallo-toepassingen uitvoeren
U bent nu klaar toorun Hallo toepassingen.

1. Bij de opdrachtprompt Hallo in Hallo **simDevice** map Hallo opdracht toobegin luisteren naar Hallo opnieuw opstarten directe methode te volgen.
   
    ```
    node simDevice.js
    ```
2. Bij de opdrachtprompt Hallo in Hallo **scheduleJobService** map Hallo na de opdracht tootrigger Hallo taken toolock Hallo deur en update Hallo twin
   
    ```
    node scheduleJobService.js
    ```
3. U ziet Hallo apparaat antwoord toohello directe methode in Hallo-console.

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie gebruikt u een taak tooschedule een directe methode tooa apparaat en Hallo bijwerken van de Hallo apparaat dubbele eigenschappen.

toocontinue aan de slag met IoT Hub en device management patronen, zoals extern via Hallo lucht firmware-update, Zie:

[Zelfstudie: Hoe toodo een firmware bijwerken][lnk-fwupdate]

aan de slag met IoT Hub toocontinue Zie [aan de slag met Azure IoT rand][lnk-iot-edge].

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
