---
title: aaaUse Azure IoT Hub twin apparaateigenschappen (.NET/knooppunt) | Microsoft Docs
description: Hoe toouse Azure IoT Hub apparaat horende tooconfigure apparaten. U gebruikt hello Azure IoT-apparaat SDK voor Node.js tooimplement een gesimuleerde apparaattoepassing en hello Azure IoT service SDK voor .NET tooimplement een service-app die de apparaatconfiguratie van een met behulp van een apparaat-twin wijzigt.
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 3c627476-f982-43c9-bd17-e0698c5d236d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: elioda
ms.openlocfilehash: 840a1b2e45f4763131299577583aa89015dcdd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices"></a>Eigenschappen van de gewenste tooconfigure apparaten gebruiken
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

Aan het einde van de Hallo van deze zelfstudie hebt u twee console apps:

* **SimulateDeviceConfiguration.js**, een gesimuleerde apparaattoepassing die wordt gewacht op een gewenste configuratie-update en rapporten Hallo status van een gesimuleerde configuratieproces voor de update.
* **SetDesiredConfigurationAndQuery**, een .NET back-end-app, die ingesteld Hallo gewenste configuratie op een apparaat en query's Hallo update configuratieproces.

> [!NOTE]
> Hallo artikel [Azure IoT SDK's] [ lnk-hub-sdks] bevat informatie over hello Azure IoT SDK's waarmee u toobuild kunt apparaat- en back-end-apps.
> 
> 

toocomplete in deze zelfstudie hebt u Hallo volgende nodig:

* Visual Studio 2015 of Visual Studio 2017.
* Node.js versie 0.10.x of hoger.
* Een actief Azure-account. Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.

Als u Hallo gevolgd [aan de slag met apparaat horende] [ lnk-twin-tutorial] zelfstudie, u hebt al een IoT-hub en een apparaat-id genoemd **myDeviceId**. In dat geval kunt u overslaan toohello [maken Hallo gesimuleerde apparaattoepassing] [ lnk-how-to-configure-createapp] sectie.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-hello-simulated-device-app"></a>Hallo gesimuleerde apparaattoepassing maken
In deze sectie maakt u een Node.js-consoletoepassing die verbinding tooyour hub als maakt **myDeviceId**, wordt gewacht op een gewenste configuratie-update en vervolgens rapporten updates op Hallo gesimuleerde update configuratieproces.

1. Maak een nieuwe lege map genaamd **simulatedeviceconfiguration**. In Hallo **simulatedeviceconfiguration** map, een nieuw package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken. Accepteer alle Hallo standaardwaarden.
   
    ```
    npm init
    ```
1. Bij de opdrachtprompt in Hallo **simulatedeviceconfiguration** map na de opdracht tooinstall Hallo Hallo **azure-iot-device** en **azure-iot-device-mqtt**pakketten:
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. Start een teksteditor en maak een nieuwe **SimulateDeviceConfiguration.js** bestand in Hallo **simulatedeviceconfiguration** map.
1. Hallo na code toohello toevoegen **SimulateDeviceConfiguration.js** -bestand en vervang Hallo **{verbindingsreeks apparaat}** aanduiding voor items met de verbindingsreeks voor Hallo apparaat u hebt gekopieerd wanneer u Hallo gemaakt **myDeviceId** apparaat-id:
   
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
   
    Hallo **Client** object beschrijft alle Hallo methoden vereist toointeract met apparaat horende van Hallo-apparaat. Deze code initialiseert Hallo **Client** -object is opgehaald Hallo apparaat twin voor **myDeviceId**, en koppelt u een handler voor Hallo update op *gewenst eigenschappen*. Hallo-handler controleert of dat er een wijzigingsaanvraag voor de huidige configuratie door te vergelijken Hallo configIds is, wordt een methode die de configuratiewijziging Hallo begint roept.
   
    Houd er rekening mee dat voor Hallo mogelijk te houden van eenvoud, deze code maakt gebruik van een standaard vastgelegde voor de initiële configuratie Hallo. Een echte app zou waarschijnlijk dat de configuratie van een lokale opslag laden.
   
   > [!IMPORTANT]
   > Gewenste eigenschap wijzigingsgebeurtenissen zijn altijd één keer op het apparaatverbinding verzonden. Zorg ervoor dat er sprake is van een werkelijke wijziging in Hallo toocheck gewenst eigenschappen voordat u een actie uitvoert.
   > 
   > 
1. Toevoegen van de volgende methoden voordat Hallo Hallo `client.open()` aanroepen:
   
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
   
    Hallo **initConfigChange** methode updates Hallo gerapporteerd eigenschappen op Hallo lokale twin apparaatobject met Hallo configuratie updatestatus aanvraag en sets hello te**in behandeling**, en vervolgens updates Hallo apparaat-twin op Hallo-service. Nadat Hallo apparaat twin is bijgewerkt, wordt een langdurige proces dat wordt beëindigd bij uitvoering van Hallo gesimuleerd **completeConfigChange**. Deze methode werkt Hallo gemelde eigenschappen van lokale status hello te stellen**geslaagd** en verwijderen van Hallo **pendingConfig** object. Hallo apparaat twin op Hallo-service wordt vervolgens bijgewerkt.
   
    Die toosave bandbreedte, gerapporteerd eigenschappen zijn bijgewerkt door te geven alleen Hallo eigenschappen toobe gewijzigd (met de naam **patch** in Hallo bovenstaande code), in plaats van het hele document Hallo vervangen.
   
   > [!NOTE]
   > Deze zelfstudie wordt een gedrag voor updates voor gelijktijdige configuratie niet simuleren. Bepaalde configuratie-update-processen mogelijk wijzigingen van de doelconfiguratie kunnen tooaccommodate terwijl Hallo update wordt uitgevoerd, enkele mogelijk tooqueue ze en sommige kan weigeren met een fout opgetreden. Zorg ervoor dat tooconsider Hallo gewenste gedrag voor uw specifieke configuratieproces en Hallo juiste logica toevoegen voordat u begint Hallo configuratiewijziging.
   > 
   > 
1. Hallo apparaattoepassing uitvoeren:
   
        node SimulateDeviceConfiguration.js
   
    U ziet het Hallo-bericht `retrieved device twin`. Houd Hallo-app die wordt uitgevoerd.

## <a name="create-hello-service-app"></a>Hallo-service-app maken
In deze sectie maakt u een .NET-consoletoepassing die updates Hallo *gewenst eigenschappen* op Hallo apparaat twin gekoppeld **myDeviceId** met een nieuwe telemetrie configuration-object. Vervolgens vraagt Hallo apparaat horende opgeslagen in Hallo IoT-hub en toont Hallo verschil tussen Hallo gewenst en configuraties van Hallo apparaat gerapporteerd.

1. Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toohello huidige oplossing met behulp van Hallo **consoletoepassing** projectsjabloon. Naam Hallo project **SetDesiredConfigurationAndQuery**.
   
    ![Nieuw Windows Classic Desktop-project in Visual C#][img-createapp]
1. Klik in Solution Explorer met de rechtermuisknop op Hallo **SetDesiredConfigurationAndQuery** project en klik vervolgens op **NuGet-pakketten beheren...** .
1. In Hallo **NuGet Package Manager** Selecteer **Bladeren**, zoeken naar **microsoft.azure.devices**, selecteer **installeren** tooinstall Hallo **Microsoft.Azure.Devices** Inpakken en accepteer de gebruiksvoorwaarden Hallo. Deze procedure downloadt, installeert en voegt u een verwijzing toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet-pakket en de bijbehorende afhankelijkheden.
   
    ![Sluit het venster Nuget Package Manager.][img-servicenuget]
1. Voeg de volgende Hallo `using` instructies boven Hallo Hallo **Program.cs** bestand:
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. Hallo na toohello velden toevoegen **programma** klasse. Vervang Hallo tijdelijke aanduidingswaarde met IoT Hub-verbindingsreeks voor Hallo-hub die u hebt gemaakt in de vorige sectie Hallo Hallo.
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. Hallo na methode toohello toevoegen **programma** klasse:
   
        static private async Task SetDesiredConfigurationAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch = new {
                    properties = new {
                        desired = new {
                            telemetryConfig = new {
                                configId = Guid.NewGuid().ToString(),
                                sendFrequency = "5m"
                            }
                        }
                    }
                };
   
            await registryManager.UpdateTwinAsync(twin.DeviceId, JsonConvert.SerializeObject(patch), twin.ETag);
            Console.WriteLine("Updated desired configuration");
   
            try
            {
                while (true)
                {
                    var query = registryManager.CreateQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'");
                    var results = await query.GetNextAsTwinAsync();
                    foreach (var result in results)
                    {
                        Console.WriteLine("Config report for: {0}", result.DeviceId);
                        Console.WriteLine("Desired telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Desired["telemetryConfig"], Formatting.Indented));
                        Console.WriteLine("Reported telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Reported["telemetryConfig"], Formatting.Indented));
                        Console.WriteLine();
                    }
                    Thread.Sleep(10000);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Exception: {ex.Message}");
            }
        }
   
    Hallo **register** object beschrijft alle Hallo methoden vereist toointeract met apparaat horende van Hallo-service. Deze code initialiseert Hallo **register** -object is opgehaald Hallo apparaat twin voor **myDeviceId**, en werkt vervolgens de gewenste eigenschappen met een nieuwe telemetrie configuration-object.
    Daarna wordt opgevraagd Hallo apparaat horende opgeslagen in de IoT-hub Hallo elke 10 seconden en afdrukken bestellen Hallo gewenst en telemetrie configuraties gerapporteerd. Raadpleeg toohello [IoT Hub-querytaal] [ lnk-query] toolearn hoe toogenerate rich op alle apparaten in uw rapporten.
   
   > [!IMPORTANT]
   > Deze toepassing een IoT Hub query elke 10 seconden ter illustratie. Gebruik een query toogenerate gebruikersgerichte rapporten over veel apparaten, en niet toodetect wijzigingen. Als uw oplossing realtime meldingen over apparaatgebeurtenissen vereist, gebruikt u [twin meldingen][lnk-twin-notifications].
   > 
   > 
1. Voeg regels toohello na Hallo **Main** methode:
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery().Wait();
        Console.WriteLine("Press any key tooquit.");
        Console.ReadLine();
1. Open in Solution Explorer hello, Hallo **opstartprojecten instellen...**  en zorg ervoor dat Hallo **actie** voor **SetDesiredConfigurationAndQuery** project **Start**. Hallo-oplossing bouwen.
1. Met **SimulateDeviceConfiguration.js** Hallo .NET-toepassing wordt uitgevoerd, worden uitgevoerd vanuit Visual Studio met **F5** en ziet u Hallo gemelde configuratiewijziging van **geslaagd** te**in behandeling** te**geslaagd** opnieuw met de nieuwe actief Hallo verzenden frequentie van vijf minuten in plaats van 24 uur.

 ![Apparaten die zijn geconfigureerd][img-deviceconfigured]
   
   > [!IMPORTANT]
   > Er is een vertraging van up tooa minuut tussen Hallo apparaat rapport opnieuw en Hallo queryresultaat. Dit is tooenable Hallo query infrastructuur toowork op zeer grote schaal. tooretrieve consistente weergaven van een enkel apparaat twin gebruiken Hallo **getDeviceTwin** methode in Hallo **register** klasse.
   > 
   > 

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie stelt u een gewenste configuratie als *gewenst eigenschappen* van Hallo oplossing back-end en een apparaat app toodetect die wijzigen en een updateproces van meerdere stappen rapportage van de status ervan via Hallo gerapporteerd simuleren geschreven Eigenschappen.

Gebruik Hallo resources toolearn hoe volgende aan:

* verzenden van telemetrie vanaf apparaten Hello [aan de slag met IoT Hub] [ lnk-iothub-getstarted] zelfstudie
* plannen of uitvoeren van bewerkingen op grote sets van apparaten Zie Hallo [planning en broadcast taken] [ lnk-schedule-jobs] zelfstudie.
* beheren van apparaten interactief (zoals het inschakelen van een ventilator van een gebruiker beheerde app), met Hallo [direct methoden gebruiken] [ lnk-methods-tutorial] zelfstudie.

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-twin-how-to-configure/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-twin-how-to-configure/createnetapp.png
[img-deviceconfigured]: media/iot-hub-csharp-node-twin-how-to-configure/deviceconfigured.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/1.1.0/

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
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-csharp-node-twin-how-to-configure.md#create-the-simulated-device-app
