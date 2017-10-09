---
title: aaaDevice firmware-update met Azure IoT Hub (knooppunt) | Microsoft Docs
description: Hoe worden Apparaatbeheer toouse op Azure IoT Hub tooinitiate een apparaatfirmware bijwerken. U gebruikt hello Azure IoT SDK's voor Node.js tooimplement een gesimuleerde apparaattoepassing en een app service waarmee Hallo firmware-update wordt geactiveerd.
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 70b84258-bc9f-43b1-b7cf-de1bb715f2cf
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/06/2017
ms.author: juanpere
ms.openlocfilehash: 99d4b369e7aba334bf713e0c657e6e5d227fb691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-device-management-tooinitiate-a-device-firmware-update-nodenode"></a>Device management tooinitiate een apparaat firmware-update (knooppunt/knooppunt) gebruiken
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a>Inleiding
In Hallo [aan de slag met Apparaatbeheer] [ lnk-dm-getstarted] zelfstudie hebt u gezien hoe toouse hello [apparaat twin] [ lnk-devtwin] en [direct methoden] [ lnk-c2dmethod] primitieven tooremotely opnieuw opstarten van een apparaat. Deze zelfstudie maakt gebruik van dezelfde IoT Hub primitieven Hallo en biedt richtlijnen en ziet u hoe een end-to-end toodo gesimuleerde firmware-update.  Dit patroon wordt gebruikt in Hallo firmware-update-implementatie voor Hallo Intel Edison apparaat.

In deze handleiding ontdekt u hoe u:

* Een Node.js-consoletoepassing die Hallo firmwareUpdate directe methode in Hallo gesimuleerde apparaattoepassing via uw IoT-hub aanroept maken.
* Maakt een gesimuleerd apparaat-app die u implementeert een **firmwareUpdate** directe methode. Deze methode initieert een fasen proces dat wordt gewacht toodownload Hallo firmware-image, Hallo firmware afbeelding gedownload en ten slotte is van toepassing hello firmware-image. Tijdens elke fase van de update Hallo gerapporteerd Hallo apparaat gebruikt Hallo eigenschappen tooreport op uitgevoerd.

Aan het einde van de Hallo van deze zelfstudie hebt u twee console Node.js-apps:

**dmpatterns_fwupdate_service.js**, die een directe methode wordt aangeroepen in de gesimuleerde apparaattoepassing hello, geeft antwoord Hallo en wordt regelmatig (elke 500ms) geeft Hallo bijgewerkt gerapporteerd eigenschappen.

**dmpatterns_fwupdate_device.js**, die tooyour IoT-hub is verbonden met de apparaat-id Hallo eerder hebt gemaakt, ontvangen een directe methode firmwareUpdate, wordt uitgevoerd via een toosimulate meerdere proces een firmware-update inclusief: wachten op Hallo afbeelding download downloaden van de nieuwe installatiekopie Hallo en ten slotte Hallo-installatiekopie toe te passen.

toocomplete in deze zelfstudie, moet u hello te volgen:

* Node.js-versie 0.12.x of hoger <br/>  [Uw ontwikkelingsomgeving voorbereiden] [ lnk-dev-setup] wordt beschreven hoe tooinstall Node.js voor deze zelfstudie op Windows of Linux.
* Een actief Azure-account. (Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)

Ga als volgt Hallo [aan de slag met Apparaatbeheer](iot-hub-node-node-device-management-get-started.md) artikel toocreate uw IoT-hub en uw IoT Hub-verbindingsreeks ophalen.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a>Activeren van een externe firmware-update op Hallo-apparaat met een directe methode
In deze sectie maakt u een Node.js-consoletoepassing die een externe firmware-update op een apparaat start. Hallo app gebruikmaakt van een directe methode tooinitiate Hallo-update en maakt gebruik van apparaat twin query's tooperiodically Hallo status Hallo active firmware-update ophalen.

1. Maak een lege map genaamd **triggerfwupdateondevice**.  In Hallo **triggerfwupdateondevice** map, een package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken.  Accepteer alle Hallo standaardwaarden:
   
    ```
    npm init
    ```
2. Bij de opdrachtprompt in Hallo **triggerfwupdateondevice** map na de opdracht tooinstall Hallo Hallo **azure-iot-hub** en **azure-iot-device-mqtt** apparaat SDK-pakketten:
   
    ```
    npm install azure-iothub --save
    ```
3. Maak met een teksteditor, een **dmpatterns_getstarted_service.js** bestand in Hallo **triggerfwupdateondevice** map.
4. Toevoegen van de volgende Hallo 'vereist' instructies toe aan Hallo begin Hallo **dmpatterns_getstarted_service.js** bestand:
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. Hallo na variabelendeclaraties toevoegen en vervang de waarden van de tijdelijke aanduiding Hallo:
   
    ```
    var connectionString = '{device_connectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToUpdate = 'myDeviceId';
    ```
6. Hallo volgende toofind werken en Hallo weergavewaarde van Hallo firmwareUpdate toevoegen eigenschap gerapporteerd.
   
    ```
    var queryTwinFWUpdateReported = function() {
        registry.getTwin(deviceToUpdate, function(err, twin){
            if (err) {
              console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
            } else {
              console.log((JSON.stringify(twin.properties.reported.iothubDM.firmwareUpdate)) + "\n");
            }
        });
    };
    ```
7. Hallo functie tooinvoke hello firmwareUpdate methode tooreboot Hallo doelapparaat volgende toevoegen:
   
    ```
    var startFirmwareUpdateDevice = function() {
      var params = {
          fwPackageUri: 'https://secureurl'
      };
   
      var methodName = "firmwareUpdate";
      var payloadData =  JSON.stringify(params);
   
      var methodParams = {
        methodName: methodName,
        payload: payloadData,
        timeoutInSeconds: 30
      };
   
      client.invokeDeviceMethod(deviceToUpdate, methodParams, function(err, result) {
        if (err) {
          console.error('Could not start hello firmware update on hello device: ' + err.message)
        } 
      });
    };
    ```
8. Ten slotte toevoegen Hallo volgende toocode toostart Hallo firmware-update sequence werken en periodiek weergave Hallo gerapporteerd eigenschappen:
   
    ```
    startFirmwareUpdateDevice();
    setInterval(queryTwinFWUpdateReported, 500);
    ```
9. Opslaan en sluiten Hallo **dmpatterns_fwupdate_service.js** bestand.

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a>Hallo-apps uitvoeren
U bent nu klaar toorun Hallo apps.

1. Bij de opdrachtprompt Hallo in Hallo **manageddevice** map Hallo opdracht toobegin luisteren naar Hallo opnieuw opstarten directe methode te volgen.
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. Bij de opdrachtprompt Hallo in Hallo **triggerfwupdateondevice** map Hallo opdracht tootrigger Hallo afstand na opnieuw opstarten en query's uitvoeren voor Hallo apparaat twin toofind Hallo laatste keer opnieuw opstarten.
   
    ```
    node dmpatterns_fwupdate_service.js
    ```
3. U ziet Hallo apparaat antwoord toohello directe methode in Hallo-console.

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie gebruikt u een directe methode tootrigger een externe firmware-update op een apparaat en de gebruikte Hallo eigenschappen toofollow Hallo voortgang van de firmware-update Hallo gerapporteerd.

toolearn hoe tooextend uw IoT-oplossing en schema-methode aanroepen op meerdere apparaten, raadpleegt u Hallo [planning en broadcast taken] [ lnk-tutorial-jobs] zelfstudie.

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
