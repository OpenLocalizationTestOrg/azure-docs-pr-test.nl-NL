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
# <a name="schedule-and-broadcast-jobs-netnodejs"></a><span data-ttu-id="bcf3a-104">Planning en broadcast-taken (.NET/Node.js)</span><span class="sxs-lookup"><span data-stu-id="bcf3a-104">Schedule and broadcast jobs (.NET/Node.js)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="bcf3a-105">Gebruik Azure IoT Hub tooschedule en bijhouden taken die miljoenen apparaten worden bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-105">Use Azure IoT Hub tooschedule and track jobs that update millions of devices.</span></span> <span data-ttu-id="bcf3a-106">Taken die moeten worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="bcf3a-106">Use jobs to:</span></span>

* <span data-ttu-id="bcf3a-107">Gewenste eigenschappen bijwerken</span><span class="sxs-lookup"><span data-stu-id="bcf3a-107">Update desired properties</span></span>
* <span data-ttu-id="bcf3a-108">Labels bijwerken</span><span class="sxs-lookup"><span data-stu-id="bcf3a-108">Update tags</span></span>
* <span data-ttu-id="bcf3a-109">Directe methoden aanroepen</span><span class="sxs-lookup"><span data-stu-id="bcf3a-109">Invoke direct methods</span></span>

<span data-ttu-id="bcf3a-110">Een taak verpakt een van deze acties en houdt Hallo uitvoering op basis van een verzameling apparaten die is gedefinieerd door een apparaat twin query.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-110">A job wraps one of these actions and tracks hello execution against a set of devices that is defined by a device twin query.</span></span> <span data-ttu-id="bcf3a-111">Een back-endserver voor apps kunt bijvoorbeeld een taak tooinvoke een directe methode op 10.000 apparaten die opnieuw wordt opgestart Hallo-apparaten.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-111">For example, a back-end app can use a job tooinvoke a direct method on 10,000 devices that reboots hello devices.</span></span> <span data-ttu-id="bcf3a-112">U geeft Hallo set apparaten met een apparaat twin query en Hallo taak toorun plannen op een later tijdstip.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-112">You specify hello set of devices with a device twin query and schedule hello job toorun at a future time.</span></span> <span data-ttu-id="bcf3a-113">Hallo taak houdt voortgang als elk Hallo apparaten ontvangen en Hallo opnieuw opstarten directe methode uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-113">hello job tracks progress as each of hello devices receive and execute hello reboot direct method.</span></span>

<span data-ttu-id="bcf3a-114">toolearn meer informatie over elk van deze mogelijkheden, Zie:</span><span class="sxs-lookup"><span data-stu-id="bcf3a-114">toolearn more about each of these capabilities, see:</span></span>

* <span data-ttu-id="bcf3a-115">Apparaat-twin en eigenschappen: [aan de slag met apparaat horende] [ lnk-get-started-twin] en [zelfstudie: hoe toouse apparaat eigenschappen twin][lnk-twin-props]</span><span class="sxs-lookup"><span data-stu-id="bcf3a-115">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How toouse device twin properties][lnk-twin-props]</span></span>
* <span data-ttu-id="bcf3a-116">Directe methoden: [IoT Hub developer guide - rechtstreekse methoden] [ lnk-dev-methods] en [zelfstudie: directe methoden gebruiken][lnk-c2d-methods]</span><span class="sxs-lookup"><span data-stu-id="bcf3a-116">Direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: Use direct methods][lnk-c2d-methods]</span></span>

<span data-ttu-id="bcf3a-117">In deze handleiding ontdekt u hoe u:</span><span class="sxs-lookup"><span data-stu-id="bcf3a-117">This tutorial shows you how to:</span></span>

* <span data-ttu-id="bcf3a-118">Maakt een apparaat-app die u een directe methode aangeroepen implementeert **lockDoor** die kan worden aangeroepen door Hallo back-endserver voor apps.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-118">Create a device app that implements a direct method called **lockDoor** that can be called by hello back-end app.</span></span> <span data-ttu-id="bcf3a-119">Hallo apparaattoepassing ontvangt ook de gewenste wijzigingen van Hallo back-endserver voor apps.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-119">hello device app also receives desired property changes from hello back-end app.</span></span>
* <span data-ttu-id="bcf3a-120">Maakt een back-end-app die u een taak toocall hello maakt **lockDoor** directe methode op meerdere apparaten.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-120">Create a back-end app that creates a job toocall hello **lockDoor** direct method on multiple devices.</span></span> <span data-ttu-id="bcf3a-121">Een andere taak verzendt gewenste eigenschap updates toomultiple apparaten.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-121">Another job sends desired property updates toomultiple devices.</span></span>

<span data-ttu-id="bcf3a-122">Aan het einde van de Hallo van deze zelfstudie hebt u een Node.js-consoletoepassing apparaat en een app in de back-end voor .NET (C#)-console:</span><span class="sxs-lookup"><span data-stu-id="bcf3a-122">At hello end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="bcf3a-123">**simDevice.js** die verbinding tooyour IoT-hub maakt, implementeert Hallo **lockDoor** directe methode en ingangen gewenst eigenschapswijzigingen.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-123">**simDevice.js** that connects tooyour IoT hub, implements hello **lockDoor** direct method, and handles desired property changes.</span></span>

<span data-ttu-id="bcf3a-124">**ScheduleJob** die gebruikmaakt van taken toocall hello **lockDoor** directe methode en update Hallo apparaat twin gewenst eigenschappen op meerdere apparaten.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-124">**ScheduleJob** that uses jobs toocall hello **lockDoor** direct method and update hello device twin desired properties on multiple devices.</span></span>

<span data-ttu-id="bcf3a-125">toocomplete in deze zelfstudie, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="bcf3a-125">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="bcf3a-126">Visual Studio 2015 of Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-126">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="bcf3a-127">Node.js-versie 0.12.x of hoger.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-127">Node.js version 0.12.x or later.</span></span> <span data-ttu-id="bcf3a-128">Hallo artikel [uw ontwikkelingsomgeving voorbereiden] [ lnk-dev-setup] wordt beschreven hoe tooinstall Node.js voor deze zelfstudie op Windows of Linux.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-128">hello article [Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="bcf3a-129">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-129">An active Azure account.</span></span> <span data-ttu-id="bcf3a-130">Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-130">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="schedule-jobs-for-calling-a-direct-method-and-sending-device-twin-updates"></a><span data-ttu-id="bcf3a-131">Taken voor het aanroepen van een directe methode en het verzenden van apparaat twin updates plannen</span><span class="sxs-lookup"><span data-stu-id="bcf3a-131">Schedule jobs for calling a direct method and sending device twin updates</span></span>

<span data-ttu-id="bcf3a-132">In deze sectie maakt u een .NET-consoletoepassing maken (met C#) die gebruikmaakt van taken toocall hello **lockDoor** directe methode en de gewenste eigenschap updates toomultiple apparaten verzenden.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-132">In this section, you create a .NET console app (using C#) that uses jobs toocall hello **lockDoor** direct method and send desired property updates toomultiple devices.</span></span>

1. <span data-ttu-id="bcf3a-133">Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toohello huidige oplossing met behulp van Hallo **consoletoepassing** projectsjabloon.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-133">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="bcf3a-134">Naam Hallo project **ScheduleJob**.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-134">Name hello project **ScheduleJob**.</span></span>

    ![Nieuw Windows Classic Desktop-project in Visual C#][img-createapp]

1. <span data-ttu-id="bcf3a-136">Klik in Solution Explorer met de rechtermuisknop op Hallo **ScheduleJob** project en klik vervolgens op **NuGet-pakketten beheren...** .</span><span class="sxs-lookup"><span data-stu-id="bcf3a-136">In Solution Explorer, right-click hello **ScheduleJob** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="bcf3a-137">In Hallo **NuGet Package Manager** Selecteer **Bladeren**, zoeken naar **microsoft.azure.devices**, selecteer **installeren** tooinstall Hallo **Microsoft.Azure.Devices** Inpakken en accepteer de gebruiksvoorwaarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-137">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="bcf3a-138">Deze stap downloadt, installeert en voegt u een verwijzing toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet-pakket en de bijbehorende afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-138">This step downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Sluit het venster Nuget Package Manager.][img-servicenuget]
1. <span data-ttu-id="bcf3a-140">Voeg de volgende Hallo `using` instructies boven Hallo Hallo **Program.cs** bestand:</span><span class="sxs-lookup"><span data-stu-id="bcf3a-140">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
    
    ```csharp
    using Microsoft.Azure.Devices;
    using Microsoft.Azure.Devices.Shared;
    ```

1. <span data-ttu-id="bcf3a-141">Voeg de volgende Hallo `using` instructie als deze niet al aanwezig in Hallo standaard instructies.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-141">Add hello following `using` statement if not already present in hello default statements.</span></span>

    ```csharp
    using System.Threading.Tasks;
    ```

1. <span data-ttu-id="bcf3a-142">Hallo na toohello velden toevoegen **programma** klasse.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-142">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="bcf3a-143">Hallo-tijdelijke aanduiding vervangen door Hallo IoT Hub-verbindingsreeks voor Hallo-hub die u hebt gemaakt in de vorige sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-143">Replace hello placeholder with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>

    ```csharp
    static string connString = "{iot hub connection string}";
    static ServiceClient client;
    static JobClient jobClient;
    ```

1. <span data-ttu-id="bcf3a-144">Hallo na methode toohello toevoegen **programma** klasse:</span><span class="sxs-lookup"><span data-stu-id="bcf3a-144">Add hello following method toohello **Program** class:</span></span>

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

1. <span data-ttu-id="bcf3a-145">Hallo na methode toohello toevoegen **programma** klasse:</span><span class="sxs-lookup"><span data-stu-id="bcf3a-145">Add hello following method toohello **Program** class:</span></span>

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

1. <span data-ttu-id="bcf3a-146">Hallo na methode toohello toevoegen **programma** klasse:</span><span class="sxs-lookup"><span data-stu-id="bcf3a-146">Add hello following method toohello **Program** class:</span></span>

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

1. <span data-ttu-id="bcf3a-147">Voeg regels toohello na Hallo **Main** methode:</span><span class="sxs-lookup"><span data-stu-id="bcf3a-147">Finally, add hello following lines toohello **Main** method:</span></span>

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

1. <span data-ttu-id="bcf3a-148">Open in Solution Explorer hello, Hallo **opstartprojecten instellen...**  en zorg ervoor dat Hallo **actie** voor **ScheduleJob** project **Start**.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-148">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **ScheduleJob** project is **Start**.</span></span> <span data-ttu-id="bcf3a-149">Hallo-oplossing bouwen.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-149">Build hello solution.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="bcf3a-150">Een gesimuleerde apparaattoepassing maken</span><span class="sxs-lookup"><span data-stu-id="bcf3a-150">Create a simulated device app</span></span>

<span data-ttu-id="bcf3a-151">In deze sectie maken van een Node.js-consoletoepassing die reageert tooa directe methode aangeroepen door Hallo cloud, die een herstart van het gesimuleerde apparaat activeert en maakt gebruik van Hallo gerapporteerd eigenschappen tooenable apparaat twin query's tooidentify apparaten en wanneer ze laatste opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-151">In this section, you create a Node.js console app that responds tooa direct method called by hello cloud, which triggers a simulated device reboot and uses hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted.</span></span>

1. <span data-ttu-id="bcf3a-152">Maak een nieuwe lege map genaamd **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-152">Create a new empty folder called **simDevice**.</span></span>  <span data-ttu-id="bcf3a-153">In Hallo **simDevice** map, een package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-153">In hello **simDevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="bcf3a-154">Accepteer alle Hallo standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="bcf3a-154">Accept all hello defaults:</span></span>

    ```cmd/sh
    npm init
    ```

1. <span data-ttu-id="bcf3a-155">Bij de opdrachtprompt in Hallo **simDevice** map na de opdracht tooinstall Hallo Hallo **azure-iot-device** en **azure-iot-device-mqtt** pakketten:</span><span class="sxs-lookup"><span data-stu-id="bcf3a-155">At your command prompt in hello **simDevice** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>

    ```cmd/sh
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```

1. <span data-ttu-id="bcf3a-156">Start een teksteditor en maak een nieuwe **simDevice.js** bestand in Hallo **simDevice** map.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-156">Using a text editor, create a new **simDevice.js** file in hello **simDevice** folder.</span></span>

1. <span data-ttu-id="bcf3a-157">Toevoegen van de volgende Hallo 'vereist' instructies toe aan Hallo begin Hallo **simDevice.js** bestand:</span><span class="sxs-lookup"><span data-stu-id="bcf3a-157">Add hello following 'require' statements at hello start of hello **simDevice.js** file:</span></span>

    ```nodejs
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```

1. <span data-ttu-id="bcf3a-158">Voeg een **connectionString** variabele en gebruik deze toocreate een **Client** exemplaar.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-158">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span> <span data-ttu-id="bcf3a-159">Zorg ervoor dat tooreplace Hallo tijdelijke aanduidingen door waarden juiste tooyour instellen.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-159">Make sure tooreplace hello placeholders with values appropriate tooyour setup.</span></span>

    ```nodejs
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```

1. <span data-ttu-id="bcf3a-160">Toevoegen van de volgende functie toohandle Hallo Hallo **lockDoor** methode.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-160">Add hello following function toohandle hello **lockDoor** method.</span></span>

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

1. <span data-ttu-id="bcf3a-161">Toevoegen van de volgende code tooregister Hallo-handler voor Hallo Hallo **lockDoor** methode.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-161">Add hello following code tooregister hello handler for hello **lockDoor** method.</span></span>

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

1. <span data-ttu-id="bcf3a-162">Opslaan en sluiten Hallo **simDevice.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-162">Save and close hello **simDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="bcf3a-163">tookeep dingen eenvoudige, deze zelfstudie wordt niet geïmplementeerd voor een beleid voor opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-163">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="bcf3a-164">In productiecode moet u beleid voor opnieuw proberen (zoals exponentieel uitstel), zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="bcf3a-164">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="bcf3a-165">Hallo-apps uitvoeren</span><span class="sxs-lookup"><span data-stu-id="bcf3a-165">Run hello apps</span></span>

<span data-ttu-id="bcf3a-166">U bent nu klaar toorun Hallo apps.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-166">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="bcf3a-167">Bij de opdrachtprompt Hallo in Hallo **simDevice** map Hallo opdracht toobegin luisteren naar Hallo opnieuw opstarten directe methode te volgen.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-167">At hello command prompt in hello **simDevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>

    ```cmd/sh
    node simDevice.js
    ```

1. <span data-ttu-id="bcf3a-168">Voer Hallo C#-consoletoepassing **ScheduleJob** door met de rechtermuisknop op Hallo **ScheduleJob** -project te selecteren **Debug** en **Start nieuw exemplaar**.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-168">Run hello C# console app **ScheduleJob** by right-clicking on hello **ScheduleJob** project, then selecting **Debug** and **Start new instance**.</span></span>

1. <span data-ttu-id="bcf3a-169">Ziet u uitvoer Hallo van apparaat en de back-end-apps.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-169">You see hello output from both device and back-end apps.</span></span>

    ![Hallo-apps tooschedule taken uitvoeren][img-schedulejobs]

## <a name="next-steps"></a><span data-ttu-id="bcf3a-171">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="bcf3a-171">Next steps</span></span>

<span data-ttu-id="bcf3a-172">In deze zelfstudie gebruikt u een taak tooschedule een directe methode tooa apparaat en Hallo bijwerken van de Hallo apparaat dubbele eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="bcf3a-172">In this tutorial, you used a job tooschedule a direct method tooa device and hello update of hello device twin's properties.</span></span>

<span data-ttu-id="bcf3a-173">aan de slag met IoT Hub en device management patronen, zoals het extern via Hallo lucht firmware-update, lezen toocontinue [zelfstudie: hoe toodo een firmware bijwerken][lnk-fwupdate].</span><span class="sxs-lookup"><span data-stu-id="bcf3a-173">toocontinue getting started with IoT Hub and device management patterns such as remote over hello air firmware update, read [Tutorial: How toodo a firmware update][lnk-fwupdate].</span></span>

<span data-ttu-id="bcf3a-174">aan de slag met IoT Hub toocontinue Zie [aan de slag met IoT rand][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="bcf3a-174">toocontinue getting started with IoT Hub, see [Getting started with IoT Edge][lnk-iot-edge].</span></span>

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
