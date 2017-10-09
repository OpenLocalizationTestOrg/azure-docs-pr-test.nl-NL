---
title: Azure IoT Hub aaaUse directe methoden (.NET/knooppunt) | Microsoft Docs
description: Hoe Azure IoT Hub toouse directe methoden. U gebruikt hello Azure IoT-device SDK voor Node.js tooimplement een gesimuleerde apparaattoepassing met een directe methode en hello Azure IoT service SDK voor .NET tooimplement een service-app die Hallo directe methode aanroept.
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: nberdy
ms.openlocfilehash: f566f939be840eb308b00ffa4e05c4e5b3fefb39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-netnode"></a>Directe methoden (.NET/knooppunt) gebruiken
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

In deze zelfstudie gaan we een .NET toodevelop en een Node.js-consoletoepassing:

* **CallMethodOnDevice.sln**, een .NET back-end-app, die een methode wordt aangeroepen in de gesimuleerde apparaattoepassing Hallo en antwoord Hallo weergegeven.
* **SimulatedDevice.js**, een Node.js-app, die overeenkomt met een apparaat tooyour IoT-hub te koppelen aan de apparaat-id Hallo eerder hebt gemaakt en toohello methode aangeroepen door Hallo cloud reageert.

> [!NOTE]
> Hallo artikel [Azure IoT SDK's] [ lnk-hub-sdks] bevat informatie over hello Azure IoT SDK's waarmee u toobuild beide toorun toepassingen op apparaten en de back-end van uw oplossing kunt.
> 
> 

toocomplete deze zelfstudie hebt u nodig:

* Visual Studio 2015 of Visual Studio 2017.
* Node.js versie 0.10.x of hoger.
* Een actief Azure-account. (Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a>Een gesimuleerde apparaattoepassing maken
In deze sectie maakt u een Node.js-consoletoepassing die tooa methode aangeroepen door Hallo oplossing terug end reageert.

1. Maak een nieuwe lege map met de naam **simulateddevice**. In Hallo **simulateddevice** map, een package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken. Accepteer alle Hallo standaardwaarden:
   
    ```
    npm init
    ```
2. Bij de opdrachtprompt in Hallo **simulateddevice** map na de opdracht tooinstall Hallo Hallo **azure-iot-device** en **azure-iot-device-mqtt** pakketten:
   
    ```
        npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. Een bestand met een teksteditor maken in Hallo **simulateddevice** map en noem deze **SimulatedDevice.js**.
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
6. Hallo functie tooimplement Hallo directe methode volgen op Hallo apparaat toevoegen:
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written toolog.', function(err) {
            if(err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. Open Hallo verbinding tooyour IoT-hub en Hallo methode listener initialiseren:
   
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

## <a name="call-a-direct-method-on-a-device"></a>Een directe methode is aangeroepen voor een apparaat
In deze sectie maakt maken u een .NET-consoletoepassing die een methode wordt aangeroepen in de gesimuleerde apparaattoepassing Hallo en wordt vervolgens weergegeven antwoord Hallo.

1. Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toohello huidige oplossing met behulp van Hallo **consoletoepassing** projectsjabloon. Zorg ervoor dat .NET Framework-versie Hallo 4.5.1 of later. Naam Hallo project **CallMethodOnDevice**.
   
    ![Nieuw Windows Classic Desktop-project in Visual C#][10]
2. Klik in Solution Explorer met de rechtermuisknop op Hallo **CallMethodOnDevice** project en klik vervolgens op **NuGet-pakketten beheren...** .
3. In Hallo **NuGet Package Manager** Selecteer **Bladeren**, zoeken naar **microsoft.azure.devices**, selecteer **installeren** tooinstall Hallo **Microsoft.Azure.Devices** Inpakken en accepteer de gebruiksvoorwaarden Hallo. Deze procedure downloadt, installeert en voegt u een verwijzing toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet-pakket en de bijbehorende afhankelijkheden.
   
    ![Sluit het venster Nuget Package Manager.][11]

4. Voeg de volgende Hallo `using` instructies boven Hallo Hallo **Program.cs** bestand:
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. Hallo na toohello velden toevoegen **programma** klasse. Vervang Hallo tijdelijke aanduidingswaarde met IoT Hub-verbindingsreeks voor Hallo-hub die u hebt gemaakt in de vorige sectie Hallo Hallo.
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. Hallo na methode toohello toevoegen **programma** klasse:
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line toobe written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    Deze methode wordt aangeroepen voor een directe methode met de naam `writeLine` op Hallo `myDeviceId` apparaat. Vervolgens worden Hallo respons van Hallo-apparaat op Hallo console geschreven. Houd er rekening mee hoe het is mogelijk toospecify een time-outwaarde voor Hallo apparaat toorespond.
7. Voeg regels toohello na Hallo **Main** methode:
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

## <a name="run-hello-applications"></a>Hallo-toepassingen uitvoeren
U bent nu klaar toorun Hallo toepassingen.

1. In Visual Studio Solution Explorer hello, met de rechtermuisknop op uw oplossing en klik op **Opstartprojecten instellen...** . Selecteer **één opstartproject**, en selecteer vervolgens Hallo **CallMethodOnDevice** -project in het vervolgkeuzemenu Hallo.

2. Bij een opdrachtprompt in Hallo **simulateddevice** map Hallo opdracht toostart luisteren naar methodeaanroepen van uw IoT-Hub te volgen:
   
    ```
    node SimulatedDevice.js
    ```
   Wachten op Hallo gesimuleerd apparaat tooopen:![][7]
3. Nu dat het Hallo-apparaat is verbonden en Hallo .NET wacht methode aanroepen, voer **CallMethodOnDevice** app tooinvoke Hallo methode in de gesimuleerde apparaattoepassing Hallo. U ziet Hallo apparaat antwoord is geschreven in Hallo-console.
   
    ![][8]
4. Hallo apparaat reageert vervolgens toohello methode door dit bericht afdrukken:
   
    ![][9]

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie maakt u een nieuwe iothub geconfigureerd in hello Azure-portal en vervolgens een apparaat-id in de id-register Hallo iothub hebt gemaakt. U hebt deze apparaat-id tooenable Hallo gesimuleerd apparaat app tooreact toomethods aangeroepen door Hallo cloud gebruikt. Hebt u ook een app die wordt aangeroepen methoden op Hallo apparaat en geeft weer Hallo-antwoord van Hallo-apparaat hebt gemaakt. 

toocontinue aan de slag met IoT Hub en tooexplore raadpleegt u andere IoT-scenario's:

* [Aan de slag met IoT Hub]
* [Taken plannen op meerdere apparaten][lnk-devguide-jobs]

toolearn hoe tooextend uw IoT-oplossing en schema-methode aanroepen op meerdere apparaten, raadpleegt u Hallo [planning en broadcast taken] [ lnk-tutorial-jobs] zelfstudie.

<!-- Images. -->
[7]: ./media/iot-hub-csharp-node-direct-methods/run-simulated-device.png
[8]: ./media/iot-hub-csharp-node-direct-methods/netserviceapp.png
[9]: ./media/iot-hub-csharp-node-direct-methods/methods-output.png

[10]: ./media/iot-hub-csharp-node-direct-methods/direct-methods-csharp1.png
[11]: ./media/iot-hub-csharp-node-direct-methods/direct-methods-csharp2.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
[Aan de slag met IoT Hub]: iot-hub-node-node-getstarted.md
