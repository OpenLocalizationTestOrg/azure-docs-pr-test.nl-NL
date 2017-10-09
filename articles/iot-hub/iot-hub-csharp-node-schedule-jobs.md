---
title: aaaSchedule taken met Azure IoT Hub (.NET/knooppunt) | Microsoft Docs
description: Hoe een Azure-IoT-Hub tooschedule taak tooinvoke een directe methode op meerdere apparaten. U gebruikt hello Azure IoT-device SDK voor Node.js tooimplement Hallo gesimuleerd apparaat-apps en hello Azure IoT service SDK voor .NET tooimplement een service-app toorun Hallo taak.
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
ms.date: 07/10/2017
ms.author: juanpere
ms.openlocfilehash: f6148b67129dde4580bfe9ccceafd6400fbc5976
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-netnodejs"></a>Planning en broadcast-taken (.NET/Node.js)

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

Gebruik Azure IoT Hub tooschedule en bijhouden taken die miljoenen apparaten worden bijgewerkt. Taken die moeten worden gebruikt:

* Gewenste eigenschappen bijwerken
* Labels bijwerken
* Directe methoden aanroepen

Een taak verpakt een van deze acties en houdt Hallo uitvoering op basis van een verzameling apparaten die is gedefinieerd door een apparaat twin query. Een back-endserver voor apps kunt bijvoorbeeld een taak tooinvoke een directe methode op 10.000 apparaten die opnieuw wordt opgestart Hallo-apparaten. U geeft Hallo set apparaten met een apparaat twin query en Hallo taak toorun plannen op een later tijdstip. Hallo taak houdt voortgang als elk Hallo apparaten ontvangen en Hallo opnieuw opstarten directe methode uitvoeren.

toolearn meer informatie over elk van deze mogelijkheden, Zie:

* Apparaat-twin en eigenschappen: [aan de slag met apparaat horende] [ lnk-get-started-twin] en [zelfstudie: hoe toouse apparaat eigenschappen twin][lnk-twin-props]
* Directe methoden: [IoT Hub developer guide - rechtstreekse methoden] [ lnk-dev-methods] en [zelfstudie: directe methoden gebruiken][lnk-c2d-methods]

In deze handleiding ontdekt u hoe u:

* Maakt een apparaat-app die u een directe methode aangeroepen implementeert **lockDoor** die kan worden aangeroepen door Hallo back-endserver voor apps. Hallo apparaattoepassing ontvangt ook de gewenste wijzigingen van Hallo back-endserver voor apps.
* Maakt een back-end-app die u een taak toocall hello maakt **lockDoor** directe methode op meerdere apparaten. Een andere taak verzendt gewenste eigenschap updates toomultiple apparaten.

Aan het einde van de Hallo van deze zelfstudie hebt u een Node.js-consoletoepassing apparaat en een app in de back-end voor .NET (C#)-console:

**simDevice.js** die verbinding tooyour IoT-hub maakt, implementeert Hallo **lockDoor** directe methode en ingangen gewenst eigenschapswijzigingen.

**ScheduleJob** die gebruikmaakt van taken toocall hello **lockDoor** directe methode en update Hallo apparaat twin gewenst eigenschappen op meerdere apparaten.

toocomplete in deze zelfstudie, moet u hello te volgen:

* Visual Studio 2015 of Visual Studio 2017.
* Node.js-versie 0.12.x of hoger. Hallo artikel [uw ontwikkelingsomgeving voorbereiden] [ lnk-dev-setup] wordt beschreven hoe tooinstall Node.js voor deze zelfstudie op Windows of Linux.
* Een actief Azure-account. Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="schedule-jobs-for-calling-a-direct-method-and-sending-device-twin-updates"></a>Taken voor het aanroepen van een directe methode en het verzenden van apparaat twin updates plannen

In deze sectie maakt u een .NET-consoletoepassing maken (met C#) die gebruikmaakt van taken toocall hello **lockDoor** directe methode en de gewenste eigenschap updates toomultiple apparaten verzenden.

1. Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toohello huidige oplossing met behulp van Hallo **consoletoepassing** projectsjabloon. Naam Hallo project **ScheduleJob**.

    ![Nieuw Windows Classic Desktop-project in Visual C#][img-createapp]

1. Klik in Solution Explorer met de rechtermuisknop op Hallo **ScheduleJob** project en klik vervolgens op **NuGet-pakketten beheren...** .
1. In Hallo **NuGet Package Manager** Selecteer **Bladeren**, zoeken naar **microsoft.azure.devices**, selecteer **installeren** tooinstall Hallo **Microsoft.Azure.Devices** Inpakken en accepteer de gebruiksvoorwaarden Hallo. Deze stap downloadt, installeert en voegt u een verwijzing toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet-pakket en de bijbehorende afhankelijkheden.

    ![Sluit het venster Nuget Package Manager.][img-servicenuget]
1. Voeg de volgende Hallo `using` instructies boven Hallo Hallo **Program.cs** bestand:
    
    ```csharp
    using Microsoft.Azure.Devices;
    using Microsoft.Azure.Devices.Shared;
    ```

1. Voeg de volgende Hallo `using` instructie als deze niet al aanwezig in Hallo standaard instructies.

    ```csharp
    using System.Threading.Tasks;
    ```

1. Hallo na toohello velden toevoegen **programma** klasse. Hallo-tijdelijke aanduiding vervangen door Hallo IoT Hub-verbindingsreeks voor Hallo-hub die u hebt gemaakt in de vorige sectie Hallo.

    ```csharp
    static string connString = "{iot hub connection string}";
    static ServiceClient client;
    static JobClient jobClient;
    ```

1. Hallo na methode toohello toevoegen **programma** klasse:

    ```csharp
    public static async Task MonitorJob(string jobId)
    {
        JobResponse result;
        do
        {
            result = await jobClient.GetJobAsync(jobId);
            Console.WriteLine("Job Status : " + result.Status.ToString());
            Thread.Sleep(2000);
        } while ((result.Status != JobStatus.Completed) && (result.Status != JobStatus.Failed));
    }
    ```

1. Hallo na methode toohello toevoegen **programma** klasse:

    ```csharp
    public static async Task StartMethodJob(string jobId)
    {
        CloudToDeviceMethod directMethod = new CloudToDeviceMethod("lockDoor", TimeSpan.FromSeconds(5), TimeSpan.FromSeconds(5));

        JobResponse result = await jobClient.ScheduleDeviceMethodAsync(jobId,
            "deviceId='myDeviceId'",
            directMethod,
            DateTime.Now,
            10);

        Console.WriteLine("Started Method Job");
    }
    ```

1. Hallo na methode toohello toevoegen **programma** klasse:

    ```csharp
    public static async Task StartTwinUpdateJob(string jobId)
    {
        var twin = new Twin();
        twin.Properties.Desired["Building"] = "43";
        twin.Properties.Desired["Floor"] = "3";
        twin.ETag = "*";

        JobResponse result = await jobClient.ScheduleTwinUpdateAsync(jobId,
            "deviceId='myDeviceId'",
            twin,
            DateTime.Now,
            10);

        Console.WriteLine("Started Twin Update Job");
    }
    ```

1. Voeg regels toohello na Hallo **Main** methode:

    ```csharp
    jobClient = JobClient.CreateFromConnectionString(connString);

    string methodJobId = Guid.NewGuid().ToString();

    StartMethodJob(methodJobId);
    MonitorJob(methodJobId).Wait();
    Console.WriteLine("Press ENTER toorun hello next job.");
    Console.ReadLine();

    string twinUpdateJobId = Guid.NewGuid().ToString();

    StartTwinUpdateJob(twinUpdateJobId);
    MonitorJob(twinUpdateJobId).Wait();
    Console.WriteLine("Press ENTER tooexit.");
    Console.ReadLine();
    ```

1. Open in Solution Explorer hello, Hallo **opstartprojecten instellen...**  en zorg ervoor dat Hallo **actie** voor **ScheduleJob** project **Start**. Hallo-oplossing bouwen.

## <a name="create-a-simulated-device-app"></a>Een gesimuleerde apparaattoepassing maken

In deze sectie maken van een Node.js-consoletoepassing die reageert tooa directe methode aangeroepen door Hallo cloud, die een herstart van het gesimuleerde apparaat activeert en maakt gebruik van Hallo gerapporteerd eigenschappen tooenable apparaat twin query's tooidentify apparaten en wanneer ze laatste opnieuw opgestart.

1. Maak een nieuwe lege map genaamd **simDevice**.  In Hallo **simDevice** map, een package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken.  Accepteer alle Hallo standaardwaarden:

    ```cmd/sh
    npm init
    ```

1. Bij de opdrachtprompt in Hallo **simDevice** map na de opdracht tooinstall Hallo Hallo **azure-iot-device** en **azure-iot-device-mqtt** pakketten:

    ```cmd/sh
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. Start een teksteditor en maak een nieuwe **simDevice.js** bestand in Hallo **simDevice** map.

1. Toevoegen van de volgende Hallo 'vereist' instructies toe aan Hallo begin Hallo **simDevice.js** bestand:

    ```nodejs
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```

1. Voeg een **connectionString** variabele en gebruik deze toocreate een **Client** exemplaar. Zorg ervoor dat tooreplace Hallo tijdelijke aanduidingen door waarden juiste tooyour instellen.

    ```nodejs
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. Toevoegen van de volgende functie toohandle Hallo Hallo **lockDoor** methode.

    ```nodejs
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

1. Toevoegen van de volgende code tooregister Hallo-handler voor Hallo Hallo **lockDoor** methode.

    ```nodejs
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub.  Waiting for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```

1. Opslaan en sluiten Hallo **simDevice.js** bestand.

> [!NOTE]
> tookeep dingen eenvoudige, deze zelfstudie wordt niet geïmplementeerd voor een beleid voor opnieuw proberen. In productiecode moet u beleid voor opnieuw proberen (zoals exponentieel uitstel), zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout][lnk-transient-faults].

## <a name="run-hello-apps"></a>Hallo-apps uitvoeren

U bent nu klaar toorun Hallo apps.

1. Bij de opdrachtprompt Hallo in Hallo **simDevice** map Hallo opdracht toobegin luisteren naar Hallo opnieuw opstarten directe methode te volgen.

    ```cmd/sh
    node simDevice.js
    ```

1. Voer Hallo C#-consoletoepassing **ScheduleJob** door met de rechtermuisknop op Hallo **ScheduleJob** -project te selecteren **Debug** en **Start nieuw exemplaar**.

1. Ziet u uitvoer Hallo van apparaat en de back-end-apps.

    ![Hallo-apps tooschedule taken uitvoeren][img-schedulejobs]

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie gebruikt u een taak tooschedule een directe methode tooa apparaat en Hallo bijwerken van de Hallo apparaat dubbele eigenschappen.

aan de slag met IoT Hub en device management patronen, zoals het extern via Hallo lucht firmware-update, lezen toocontinue [zelfstudie: hoe toodo een firmware bijwerken][lnk-fwupdate].

aan de slag met IoT Hub toocontinue Zie [aan de slag met IoT rand][lnk-iot-edge].

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-schedule-jobs/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-schedule-jobs/createnetapp.png
[img-schedulejobs]: media/iot-hub-csharp-node-schedule-jobs/schedulejobs.png

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
