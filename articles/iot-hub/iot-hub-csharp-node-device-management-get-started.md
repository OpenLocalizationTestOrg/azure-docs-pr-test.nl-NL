---
title: aaaGet de slag met Azure IoT Hub Apparaatbeheer (.NET/knooppunt) | Microsoft Docs
description: Hoe toouse Azure IoT Hub apparaat management tooinitiate een extern apparaat opnieuw worden opgestart. U gebruikt hello Azure IoT-device SDK voor Node.js tooimplement een gesimuleerde apparaattoepassing met een directe methode en hello Azure IoT service SDK voor .NET tooimplement een service-app die Hallo directe methode aanroept.
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
ms.date: 11/17/2016
ms.author: juanpere
ms.openlocfilehash: ea6d50dfac1c222d7836e3bf5503c6c9b8c89dfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-netnode"></a>Aan de slag met Apparaatbeheer (.NET/knooppunt)

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

In deze handleiding ontdekt u hoe u:

* Gebruik Hallo toocreate met Azure portal een IoT-Hub en een apparaat-id maakt in uw IoT-hub.
* Maak een gesimuleerde apparaattoepassing met een directe methode die het apparaat opnieuw wordt opgestart. Rechtstreekse methoden worden aangeroepen vanuit Hallo cloud.
* Een .NET-consoletoepassing die Hallo opnieuw opstarten directe methode in Hallo gesimuleerde apparaattoepassing via uw IoT-hub aanroept maken.

Aan het einde van de Hallo van deze zelfstudie hebt u een Node.js-consoletoepassing apparaat en een app in de back-end voor .NET (C#)-console:

**dmpatterns_getstarted_device.js**, die tooyour IoT-hub verbindt met apparaat-id Hallo eerder hebt gemaakt, ontvangt van een directe methode voor opnieuw opstarten, simuleert fysieke opnieuw worden opgestart en Hallo tijd voor de laatste keer opnieuw opstarten Hallo rapporteert.

**TriggerReboot**, die een directe methode wordt aangeroepen in de gesimuleerde apparaattoepassing hello, geeft antwoord Hallo weer en geeft Hallo bijgewerkt gerapporteerd eigenschappen.

toocomplete in deze zelfstudie, moet u hello te volgen:

* Visual Studio 2015 of Visual Studio 2017.
* Node.js-versie 0.12.x of hoger <br/>  [Uw ontwikkelingsomgeving voorbereiden] [ lnk-dev-setup] wordt beschreven hoe tooinstall Node.js voor deze zelfstudie op Windows of Linux.
* Een actief Azure-account. (Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a>Activeren van een extern opnieuw opstarten op Hallo-apparaat met een directe methode
In deze sectie maakt u een .NET-consoletoepassing (met C#) die een externe opnieuw opstarten op een apparaat met een directe methode start. Hallo app gebruikmaakt van apparaat twin query's toodiscover Hallo keer opnieuw opstarten voor dat apparaat.

1. Voeg in Visual Studio een nieuwe oplossing voor Visual C# Classic Windows Desktop-project tooa met behulp van Hallo **Console-App (.NET Framework)** projectsjabloon. Zorg ervoor dat .NET Framework-versie Hallo 4.5.1 of later. Naam Hallo project **TriggerReboot**.

    ![Nieuw Windows Classic Desktop-project in Visual C#][img-createapp]

2. Klik in Solution Explorer met de rechtermuisknop op Hallo **TriggerReboot** project en klik vervolgens op **NuGet-pakketten beheren**.
3. In Hallo **NuGet Package Manager** Selecteer **Bladeren**, zoeken naar **microsoft.azure.devices**, selecteer **installeren** tooinstall Hallo **Microsoft.Azure.Devices** Inpakken en accepteer de gebruiksvoorwaarden Hallo. Deze procedure downloadt, installeert en voegt u een verwijzing toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet-pakket en de bijbehorende afhankelijkheden.

    ![Sluit het venster Nuget Package Manager.][img-servicenuget]
4. Voeg de volgende Hallo `using` instructies boven Hallo Hallo **Program.cs** bestand:
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
5. Hallo na toohello velden toevoegen **programma** klasse. Vervang Hallo tijdelijke aanduidingswaarde met Hallo IoT Hub-verbindingsreeks voor Hallo-hub die u hebt gemaakt in de vorige sectie Hallo en Hallo doelapparaat.
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
6. Hallo na methode toohello toevoegen **programma** klasse.  Deze code haalt Hallo apparaat twin voor opnieuw opstarten van apparaat- en uitgangen Hallo Hallo gerapporteerd eigenschappen.
   
        public static async Task QueryTwinRebootReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
7. Hallo na methode toohello toevoegen **programma** klasse.  Deze code initieert Hallo opnieuw opstarten op Hallo-apparaat met een directe methode.

        public static async Task StartReboot()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("reboot");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

7. Voeg regels toohello na Hallo **Main** methode:
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartReboot().Wait();
        QueryTwinRebootReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
8. Hallo-oplossing bouwen.

## <a name="create-a-simulated-device-app"></a>Een gesimuleerde apparaattoepassing maken
In deze sectie wordt u

* Een Node.js-consoletoepassing die tooa directe methode aangeroepen door Hallo cloud reageert maken
* Een gesimuleerd apparaat opnieuw activeren
* Gebruik Hallo gerapporteerd eigenschappen tooenable apparaat twin query's tooidentify apparaten en wanneer ze laatste opnieuw opgestart

1. Maak een nieuwe lege map genaamd **manageddevice**.  In Hallo **manageddevice** map, een package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken.  Accepteer alle Hallo standaardwaarden:
   
    ```
    npm init
    ```
2. Bij de opdrachtprompt in Hallo **manageddevice** map na de opdracht tooinstall Hallo Hallo **azure-iot-device** apparaat-SDK-pakket en **azure-iot-device-mqtt**pakket:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Start een teksteditor en maak een nieuwe **dmpatterns_getstarted_device.js** bestand in Hallo **manageddevice** map.
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
7. De volgende Hallo code tooopen Hallo verbinding tooyour IoT-hub en Hallo directe methode listener starten toevoegen:
   
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


## <a name="run-hello-apps"></a>Hallo-apps uitvoeren
U bent nu klaar toorun Hallo apps.

1. Bij de opdrachtprompt Hallo in Hallo **manageddevice** map Hallo opdracht toobegin luisteren naar Hallo opnieuw opstarten directe methode te volgen.
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. Voer Hallo C#-consoletoepassing **TriggerReboot**. Klik met de rechtermuisknop Hallo **TriggerReboot** project, selecteer **Debug**, en selecteer vervolgens **nieuw exemplaar gestart**.

3. U ziet Hallo apparaat antwoord toohello directe methode in Hallo-console.

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png
[img-servicenuget]: media/iot-hub-csharp-node-device-management-get-started/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-device-management-get-started/createnetapp.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups toomanage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/