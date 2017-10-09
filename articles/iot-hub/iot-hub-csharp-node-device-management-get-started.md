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
# <a name="get-started-with-device-management-netnode"></a><span data-ttu-id="84c81-104">Aan de slag met Apparaatbeheer (.NET/knooppunt)</span><span class="sxs-lookup"><span data-stu-id="84c81-104">Get started with device management (.NET/Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="84c81-105">In deze handleiding ontdekt u hoe u:</span><span class="sxs-lookup"><span data-stu-id="84c81-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="84c81-106">Gebruik Hallo toocreate met Azure portal een IoT-Hub en een apparaat-id maakt in uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="84c81-106">Use hello Azure portal toocreate an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="84c81-107">Maak een gesimuleerde apparaattoepassing met een directe methode die het apparaat opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="84c81-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="84c81-108">Rechtstreekse methoden worden aangeroepen vanuit Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="84c81-108">Direct methods are invoked from hello cloud.</span></span>
* <span data-ttu-id="84c81-109">Een .NET-consoletoepassing die Hallo opnieuw opstarten directe methode in Hallo gesimuleerde apparaattoepassing via uw IoT-hub aanroept maken.</span><span class="sxs-lookup"><span data-stu-id="84c81-109">Create a .NET console app that calls hello reboot direct method in hello simulated device app through your IoT hub.</span></span>

<span data-ttu-id="84c81-110">Aan het einde van de Hallo van deze zelfstudie hebt u een Node.js-consoletoepassing apparaat en een app in de back-end voor .NET (C#)-console:</span><span class="sxs-lookup"><span data-stu-id="84c81-110">At hello end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="84c81-111">**dmpatterns_getstarted_device.js**, die tooyour IoT-hub verbindt met apparaat-id Hallo eerder hebt gemaakt, ontvangt van een directe methode voor opnieuw opstarten, simuleert fysieke opnieuw worden opgestart en Hallo tijd voor de laatste keer opnieuw opstarten Hallo rapporteert.</span><span class="sxs-lookup"><span data-stu-id="84c81-111">**dmpatterns_getstarted_device.js**, which connects tooyour IoT hub with hello device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports hello time for hello last reboot.</span></span>

<span data-ttu-id="84c81-112">**TriggerReboot**, die een directe methode wordt aangeroepen in de gesimuleerde apparaattoepassing hello, geeft antwoord Hallo weer en geeft Hallo bijgewerkt gerapporteerd eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="84c81-112">**TriggerReboot**, which calls a direct method in hello simulated device app, displays hello response, and displays hello updated reported properties.</span></span>

<span data-ttu-id="84c81-113">toocomplete in deze zelfstudie, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="84c81-113">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="84c81-114">Visual Studio 2015 of Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="84c81-114">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="84c81-115">Node.js-versie 0.12.x of hoger</span><span class="sxs-lookup"><span data-stu-id="84c81-115">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="84c81-116">[Uw ontwikkelingsomgeving voorbereiden] [ lnk-dev-setup] wordt beschreven hoe tooinstall Node.js voor deze zelfstudie op Windows of Linux.</span><span class="sxs-lookup"><span data-stu-id="84c81-116">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="84c81-117">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="84c81-117">An active Azure account.</span></span> <span data-ttu-id="84c81-118">(Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)</span><span class="sxs-lookup"><span data-stu-id="84c81-118">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a><span data-ttu-id="84c81-119">Activeren van een extern opnieuw opstarten op Hallo-apparaat met een directe methode</span><span class="sxs-lookup"><span data-stu-id="84c81-119">Trigger a remote reboot on hello device using a direct method</span></span>
<span data-ttu-id="84c81-120">In deze sectie maakt u een .NET-consoletoepassing (met C#) die een externe opnieuw opstarten op een apparaat met een directe methode start.</span><span class="sxs-lookup"><span data-stu-id="84c81-120">In this section, you create a .NET console app (using C#) that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="84c81-121">Hallo app gebruikmaakt van apparaat twin query's toodiscover Hallo keer opnieuw opstarten voor dat apparaat.</span><span class="sxs-lookup"><span data-stu-id="84c81-121">hello app uses device twin queries toodiscover hello last reboot time for that device.</span></span>

1. <span data-ttu-id="84c81-122">Voeg in Visual Studio een nieuwe oplossing voor Visual C# Classic Windows Desktop-project tooa met behulp van Hallo **Console-App (.NET Framework)** projectsjabloon.</span><span class="sxs-lookup"><span data-stu-id="84c81-122">In Visual Studio, add a Visual C# Windows Classic Desktop project tooa new solution by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="84c81-123">Zorg ervoor dat .NET Framework-versie Hallo 4.5.1 of later.</span><span class="sxs-lookup"><span data-stu-id="84c81-123">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="84c81-124">Naam Hallo project **TriggerReboot**.</span><span class="sxs-lookup"><span data-stu-id="84c81-124">Name hello project **TriggerReboot**.</span></span>

    ![Nieuw Windows Classic Desktop-project in Visual C#][img-createapp]

2. <span data-ttu-id="84c81-126">Klik in Solution Explorer met de rechtermuisknop op Hallo **TriggerReboot** project en klik vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="84c81-126">In Solution Explorer, right-click hello **TriggerReboot** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="84c81-127">In Hallo **NuGet Package Manager** Selecteer **Bladeren**, zoeken naar **microsoft.azure.devices**, selecteer **installeren** tooinstall Hallo **Microsoft.Azure.Devices** Inpakken en accepteer de gebruiksvoorwaarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="84c81-127">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="84c81-128">Deze procedure downloadt, installeert en voegt u een verwijzing toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet-pakket en de bijbehorende afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="84c81-128">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Sluit het venster Nuget Package Manager.][img-servicenuget]
4. <span data-ttu-id="84c81-130">Voeg de volgende Hallo `using` instructies boven Hallo Hallo **Program.cs** bestand:</span><span class="sxs-lookup"><span data-stu-id="84c81-130">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
5. <span data-ttu-id="84c81-131">Hallo na toohello velden toevoegen **programma** klasse.</span><span class="sxs-lookup"><span data-stu-id="84c81-131">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="84c81-132">Vervang Hallo tijdelijke aanduidingswaarde met Hallo IoT Hub-verbindingsreeks voor Hallo-hub die u hebt gemaakt in de vorige sectie Hallo en Hallo doelapparaat.</span><span class="sxs-lookup"><span data-stu-id="84c81-132">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section and hello target device.</span></span>
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
6. <span data-ttu-id="84c81-133">Hallo na methode toohello toevoegen **programma** klasse.</span><span class="sxs-lookup"><span data-stu-id="84c81-133">Add hello following method toohello **Program** class.</span></span>  <span data-ttu-id="84c81-134">Deze code haalt Hallo apparaat twin voor opnieuw opstarten van apparaat- en uitgangen Hallo Hallo gerapporteerd eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="84c81-134">This code gets hello device twin for hello rebooting device and outputs hello reported properties.</span></span>
   
        public static async Task QueryTwinRebootReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
7. <span data-ttu-id="84c81-135">Hallo na methode toohello toevoegen **programma** klasse.</span><span class="sxs-lookup"><span data-stu-id="84c81-135">Add hello following method toohello **Program** class.</span></span>  <span data-ttu-id="84c81-136">Deze code initieert Hallo opnieuw opstarten op Hallo-apparaat met een directe methode.</span><span class="sxs-lookup"><span data-stu-id="84c81-136">This code initiates hello reboot on hello device using a direct method.</span></span>

        public static async Task StartReboot()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("reboot");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

7. <span data-ttu-id="84c81-137">Voeg regels toohello na Hallo **Main** methode:</span><span class="sxs-lookup"><span data-stu-id="84c81-137">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartReboot().Wait();
        QueryTwinRebootReported().Wait();
        Console.WriteLine("Press ENTER tooexit.");
        Console.ReadLine();
        
8. <span data-ttu-id="84c81-138">Hallo-oplossing bouwen.</span><span class="sxs-lookup"><span data-stu-id="84c81-138">Build hello solution.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="84c81-139">Een gesimuleerde apparaattoepassing maken</span><span class="sxs-lookup"><span data-stu-id="84c81-139">Create a simulated device app</span></span>
<span data-ttu-id="84c81-140">In deze sectie wordt u</span><span class="sxs-lookup"><span data-stu-id="84c81-140">In this section, you will</span></span>

* <span data-ttu-id="84c81-141">Een Node.js-consoletoepassing die tooa directe methode aangeroepen door Hallo cloud reageert maken</span><span class="sxs-lookup"><span data-stu-id="84c81-141">Create a Node.js console app that responds tooa direct method called by hello cloud</span></span>
* <span data-ttu-id="84c81-142">Een gesimuleerd apparaat opnieuw activeren</span><span class="sxs-lookup"><span data-stu-id="84c81-142">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="84c81-143">Gebruik Hallo gerapporteerd eigenschappen tooenable apparaat twin query's tooidentify apparaten en wanneer ze laatste opnieuw opgestart</span><span class="sxs-lookup"><span data-stu-id="84c81-143">Use hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted</span></span>

1. <span data-ttu-id="84c81-144">Maak een nieuwe lege map genaamd **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="84c81-144">Create a new empty folder called **manageddevice**.</span></span>  <span data-ttu-id="84c81-145">In Hallo **manageddevice** map, een package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="84c81-145">In hello **manageddevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="84c81-146">Accepteer alle Hallo standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="84c81-146">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="84c81-147">Bij de opdrachtprompt in Hallo **manageddevice** map na de opdracht tooinstall Hallo Hallo **azure-iot-device** apparaat-SDK-pakket en **azure-iot-device-mqtt**pakket:</span><span class="sxs-lookup"><span data-stu-id="84c81-147">At your command prompt in hello **manageddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="84c81-148">Start een teksteditor en maak een nieuwe **dmpatterns_getstarted_device.js** bestand in Hallo **manageddevice** map.</span><span class="sxs-lookup"><span data-stu-id="84c81-148">Using a text editor, create a new **dmpatterns_getstarted_device.js** file in hello **manageddevice** folder.</span></span>
4. <span data-ttu-id="84c81-149">Toevoegen van de volgende Hallo 'vereist' instructies toe aan Hallo begin Hallo **dmpatterns_getstarted_device.js** bestand:</span><span class="sxs-lookup"><span data-stu-id="84c81-149">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="84c81-150">Voeg een **connectionString** variabele en gebruik deze toocreate een **Client** exemplaar.</span><span class="sxs-lookup"><span data-stu-id="84c81-150">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span>  <span data-ttu-id="84c81-151">Hallo-verbindingsreeks vervangen door de verbindingsreeks van uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="84c81-151">Replace hello connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="84c81-152">Hallo functie tooimplement Hallo directe methode volgen op Hallo apparaat toevoegen</span><span class="sxs-lookup"><span data-stu-id="84c81-152">Add hello following function tooimplement hello direct method on hello device</span></span>
   
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
7. <span data-ttu-id="84c81-153">De volgende Hallo code tooopen Hallo verbinding tooyour IoT-hub en Hallo directe methode listener starten toevoegen:</span><span class="sxs-lookup"><span data-stu-id="84c81-153">Add hello following code tooopen hello connection tooyour IoT hub and start hello direct method listener:</span></span>
   
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
8. <span data-ttu-id="84c81-154">Opslaan en sluiten Hallo **dmpatterns_getstarted_device.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="84c81-154">Save and close hello **dmpatterns_getstarted_device.js** file.</span></span>
   
> [!NOTE]
> <span data-ttu-id="84c81-155">tookeep dingen eenvoudige, deze zelfstudie wordt niet geïmplementeerd voor een beleid voor opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="84c81-155">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="84c81-156">In productiecode moet u beleid voor opnieuw proberen (zoals exponentieel uitstel), zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="84c81-156">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>


## <a name="run-hello-apps"></a><span data-ttu-id="84c81-157">Hallo-apps uitvoeren</span><span class="sxs-lookup"><span data-stu-id="84c81-157">Run hello apps</span></span>
<span data-ttu-id="84c81-158">U bent nu klaar toorun Hallo apps.</span><span class="sxs-lookup"><span data-stu-id="84c81-158">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="84c81-159">Bij de opdrachtprompt Hallo in Hallo **manageddevice** map Hallo opdracht toobegin luisteren naar Hallo opnieuw opstarten directe methode te volgen.</span><span class="sxs-lookup"><span data-stu-id="84c81-159">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="84c81-160">Voer Hallo C#-consoletoepassing **TriggerReboot**.</span><span class="sxs-lookup"><span data-stu-id="84c81-160">Run hello C# console app **TriggerReboot**.</span></span> <span data-ttu-id="84c81-161">Klik met de rechtermuisknop Hallo **TriggerReboot** project, selecteer **Debug**, en selecteer vervolgens **nieuw exemplaar gestart**.</span><span class="sxs-lookup"><span data-stu-id="84c81-161">Right-click hello **TriggerReboot** project, select **Debug**, and then select **Start new instance**.</span></span>

3. <span data-ttu-id="84c81-162">U ziet Hallo apparaat antwoord toohello directe methode in Hallo-console.</span><span class="sxs-lookup"><span data-stu-id="84c81-162">You see hello device response toohello direct method in hello console.</span></span>

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