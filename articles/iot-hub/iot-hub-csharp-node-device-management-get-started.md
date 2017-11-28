---
title: Aan de slag met Azure IoT Hub Apparaatbeheer (.NET/knooppunt) | Microsoft Docs
description: "Het gebruik van Azure IoT Hub Apparaatbeheer initiëren externe apparaten opnieuw worden opgestart. U kunt het apparaat met Azure IoT SDK voor Node.js gebruiken voor het implementeren van een gesimuleerde apparaattoepassing met een directe methode en de service Azure IoT SDK voor .NET voor het implementeren van een service-app die de directe methode aanroept."
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
ms.openlocfilehash: d97fc5493570985f94c23032c870628d6a089dcd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-device-management-netnode"></a><span data-ttu-id="bf928-104">Aan de slag met Apparaatbeheer (.NET/knooppunt)</span><span class="sxs-lookup"><span data-stu-id="bf928-104">Get started with device management (.NET/Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="bf928-105">In deze handleiding ontdekt u hoe u:</span><span class="sxs-lookup"><span data-stu-id="bf928-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="bf928-106">De Azure portal gebruiken voor het maken van een IoT-Hub en een apparaat-id maakt in uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="bf928-106">Use the Azure portal to create an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="bf928-107">Maak een gesimuleerde apparaattoepassing met een directe methode die het apparaat opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="bf928-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="bf928-108">Rechtstreekse methoden worden aangeroepen vanuit de cloud.</span><span class="sxs-lookup"><span data-stu-id="bf928-108">Direct methods are invoked from the cloud.</span></span>
* <span data-ttu-id="bf928-109">Een .NET-consoletoepassing die de directe methode voor opnieuw opstarten in de gesimuleerde apparaattoepassing via uw IoT-hub maken.</span><span class="sxs-lookup"><span data-stu-id="bf928-109">Create a .NET console app that calls the reboot direct method in the simulated device app through your IoT hub.</span></span>

<span data-ttu-id="bf928-110">Aan het einde van deze zelfstudie hebt u een Node.js-consoletoepassing apparaat en een app in de back-end voor .NET (C#)-console:</span><span class="sxs-lookup"><span data-stu-id="bf928-110">At the end of this tutorial, you have a Node.js console device app and a .NET (C#) console back-end app:</span></span>

<span data-ttu-id="bf928-111">**dmpatterns_getstarted_device.js**, die verbinding maakt met uw IoT-hub aan de apparaat-id eerder hebt gemaakt, ontvangt u een directe methode voor opnieuw opstarten, simuleert fysieke opnieuw worden opgestart en rapporten van de tijd voor de laatste keer opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="bf928-111">**dmpatterns_getstarted_device.js**, which connects to your IoT hub with the device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports the time for the last reboot.</span></span>

<span data-ttu-id="bf928-112">**TriggerReboot**, die een directe methode wordt aangeroepen in de gesimuleerde apparaattoepassing geeft het antwoord weer en geeft de bijgewerkte eigenschappen gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="bf928-112">**TriggerReboot**, which calls a direct method in the simulated device app, displays the response, and displays the updated reported properties.</span></span>

<span data-ttu-id="bf928-113">Voor het voltooien van deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="bf928-113">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="bf928-114">Visual Studio 2015 of Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="bf928-114">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="bf928-115">Node.js-versie 0.12.x of hoger</span><span class="sxs-lookup"><span data-stu-id="bf928-115">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="bf928-116">[Uw ontwikkelingsomgeving voorbereiden] [ lnk-dev-setup] wordt beschreven hoe u Node.js voor deze zelfstudie installeren op Windows of Linux.</span><span class="sxs-lookup"><span data-stu-id="bf928-116">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="bf928-117">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="bf928-117">An active Azure account.</span></span> <span data-ttu-id="bf928-118">(Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)</span><span class="sxs-lookup"><span data-stu-id="bf928-118">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-reboot-on-the-device-using-a-direct-method"></a><span data-ttu-id="bf928-119">Activeren van een extern opnieuw opstarten op het apparaat met een directe methode</span><span class="sxs-lookup"><span data-stu-id="bf928-119">Trigger a remote reboot on the device using a direct method</span></span>
<span data-ttu-id="bf928-120">In deze sectie maakt u een .NET-consoletoepassing (met C#) die een externe opnieuw opstarten op een apparaat met een directe methode start.</span><span class="sxs-lookup"><span data-stu-id="bf928-120">In this section, you create a .NET console app (using C#) that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="bf928-121">De app gebruikmaakt van apparaat twin query's voor het detecteren van de laatste keer opnieuw opstarten voor dat apparaat.</span><span class="sxs-lookup"><span data-stu-id="bf928-121">The app uses device twin queries to discover the last reboot time for that device.</span></span>

1. <span data-ttu-id="bf928-122">Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toe aan de nieuwe oplossing met behulp van de projectsjabloon **Console App (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="bf928-122">In Visual Studio, add a Visual C# Windows Classic Desktop project to a new solution by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="bf928-123">Zorg ervoor dat de versie van .NET Framework minimaal 4.5.1 is.</span><span class="sxs-lookup"><span data-stu-id="bf928-123">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="bf928-124">Noem het project **TriggerReboot**.</span><span class="sxs-lookup"><span data-stu-id="bf928-124">Name the project **TriggerReboot**.</span></span>

    ![Nieuw Windows Classic Desktop-project in Visual C#][img-createapp]

2. <span data-ttu-id="bf928-126">Klik in Solution Explorer met de rechtermuisknop op de **TriggerReboot** project en klik vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="bf928-126">In Solution Explorer, right-click the **TriggerReboot** project, and then click **Manage NuGet Packages**.</span></span>
3. <span data-ttu-id="bf928-127">Klik in de **NuGet Package Manager** op **Browse** en zoek naar **microsoft.azure.devices**. Accepteer de gebruiksvoorwaarden en klik op **Install** om het **Microsoft.Azure.Devices**-pakket te installeren.</span><span class="sxs-lookup"><span data-stu-id="bf928-127">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="bf928-128">Met deze procedure worden de [Azure IoT-service-SDK][lnk-nuget-service-sdk], het NuGet-pakket en de bijbehorende afhankelijkheden gedownload en geïnstalleerd. Ook worden verwijzingen hiernaar toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="bf928-128">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>

    ![Sluit het venster Nuget Package Manager.][img-servicenuget]
4. <span data-ttu-id="bf928-130">Voeg aan het begin van het bestand **Program.cs** de volgende `using` instructies toe:</span><span class="sxs-lookup"><span data-stu-id="bf928-130">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using Microsoft.Azure.Devices.Shared;
        
5. <span data-ttu-id="bf928-131">Voeg de volgende velden toe aan de klasse **Program**:</span><span class="sxs-lookup"><span data-stu-id="bf928-131">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="bf928-132">Vervang de tijdelijke aanduidingswaarde met de IoT Hub-verbindingsreeks voor de hub die u hebt gemaakt in de vorige sectie en het doelapparaat.</span><span class="sxs-lookup"><span data-stu-id="bf928-132">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section and the target device.</span></span>
   
        static RegistryManager registryManager;
        static string connString = "{iot hub connection string}";
        static ServiceClient client;
        static JobClient jobClient;
        static string targetDevice = "{deviceIdForTargetDevice}";
        
6. <span data-ttu-id="bf928-133">Voeg de volgende methode voor de **programma** klasse.</span><span class="sxs-lookup"><span data-stu-id="bf928-133">Add the following method to the **Program** class.</span></span>  <span data-ttu-id="bf928-134">Deze code haalt de apparaat-twin voor het apparaat rebooting en levert de gerapporteerde eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="bf928-134">This code gets the device twin for the rebooting device and outputs the reported properties.</span></span>
   
        public static async Task QueryTwinRebootReported()
        {
            Twin twin = await registryManager.GetTwinAsync(targetDevice);
            Console.WriteLine(twin.Properties.Reported.ToJson());
        }
        
7. <span data-ttu-id="bf928-135">Voeg de volgende methode voor de **programma** klasse.</span><span class="sxs-lookup"><span data-stu-id="bf928-135">Add the following method to the **Program** class.</span></span>  <span data-ttu-id="bf928-136">Deze code wordt het opnieuw opstarten op het apparaat met een directe methode gestart.</span><span class="sxs-lookup"><span data-stu-id="bf928-136">This code initiates the reboot on the device using a direct method.</span></span>

        public static async Task StartReboot()
        {
            client = ServiceClient.CreateFromConnectionString(connString);
            CloudToDeviceMethod method = new CloudToDeviceMethod("reboot");
            method.ResponseTimeout = TimeSpan.FromSeconds(30);

            CloudToDeviceMethodResult result = await client.InvokeDeviceMethodAsync(targetDevice, method);

            Console.WriteLine("Invoked firmware update on device.");
        }

7. <span data-ttu-id="bf928-137">Voeg tot slot de volgende regels toe aan de methode **Main**:</span><span class="sxs-lookup"><span data-stu-id="bf928-137">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connString);
        StartReboot().Wait();
        QueryTwinRebootReported().Wait();
        Console.WriteLine("Press ENTER to exit.");
        Console.ReadLine();
        
8. <span data-ttu-id="bf928-138">De oplossing bouwen.</span><span class="sxs-lookup"><span data-stu-id="bf928-138">Build the solution.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="bf928-139">Een gesimuleerde apparaattoepassing maken</span><span class="sxs-lookup"><span data-stu-id="bf928-139">Create a simulated device app</span></span>
<span data-ttu-id="bf928-140">In deze sectie wordt u</span><span class="sxs-lookup"><span data-stu-id="bf928-140">In this section, you will</span></span>

* <span data-ttu-id="bf928-141">U maakt een Node.js-console-app die reageert op een directe methode die door de cloud wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="bf928-141">Create a Node.js console app that responds to a direct method called by the cloud</span></span>
* <span data-ttu-id="bf928-142">Een gesimuleerd apparaat opnieuw activeren</span><span class="sxs-lookup"><span data-stu-id="bf928-142">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="bf928-143">Gebruik de gemelde eigenschappen om het apparaat twin query's om apparaten te identificeren en wanneer ze het laatst opnieuw opgestart</span><span class="sxs-lookup"><span data-stu-id="bf928-143">Use the reported properties to enable device twin queries to identify devices and when they last rebooted</span></span>

1. <span data-ttu-id="bf928-144">Maak een nieuwe lege map genaamd **manageddevice**.</span><span class="sxs-lookup"><span data-stu-id="bf928-144">Create a new empty folder called **manageddevice**.</span></span>  <span data-ttu-id="bf928-145">Maak in de map **simulateddevice** een bestand met de naam package.json door achter de opdrachtprompt de volgende opdracht op te geven.</span><span class="sxs-lookup"><span data-stu-id="bf928-145">In the **manageddevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="bf928-146">Accepteer alle standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="bf928-146">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="bf928-147">Bij de opdrachtprompt in de **manageddevice** map, voer de volgende opdracht voor het installeren van de **azure-iot-device** apparaat-SDK-pakket en **azure-iot-device-mqtt** pakket:</span><span class="sxs-lookup"><span data-stu-id="bf928-147">At your command prompt in the **manageddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="bf928-148">Start een teksteditor en maak een nieuwe **dmpatterns_getstarted_device.js** bestand de **manageddevice** map.</span><span class="sxs-lookup"><span data-stu-id="bf928-148">Using a text editor, create a new **dmpatterns_getstarted_device.js** file in the **manageddevice** folder.</span></span>
4. <span data-ttu-id="bf928-149">Voeg de volgende 'vereist' instructies aan het begin van de **dmpatterns_getstarted_device.js** bestand:</span><span class="sxs-lookup"><span data-stu-id="bf928-149">Add the following 'require' statements at the start of the **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="bf928-150">Voeg een **connectionString**-variabele toe en gebruik deze om een **client**exemplaar te maken.</span><span class="sxs-lookup"><span data-stu-id="bf928-150">Add a **connectionString** variable and use it to create a **Client** instance.</span></span>  <span data-ttu-id="bf928-151">De verbindingsreeks vervangen door de verbindingsreeks van uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="bf928-151">Replace the connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="bf928-152">De volgende functie voor het implementeren van de directe methode op het apparaat toevoegen</span><span class="sxs-lookup"><span data-stu-id="bf928-152">Add the following function to implement the direct method on the device</span></span>
   
    ```
    var onReboot = function(request, response) {
   
        // Respond the cloud app for the direct method
        response.send(200, 'Reboot started', function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        // Report the reboot before the physical restart
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
7. <span data-ttu-id="bf928-153">Voeg de volgende code voor het openen van de verbinding met uw IoT-hub en de listener directe methode te starten:</span><span class="sxs-lookup"><span data-stu-id="bf928-153">Add the following code to open the connection to your IoT hub and start the direct method listener:</span></span>
   
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
8. <span data-ttu-id="bf928-154">Sla op en sluit de **dmpatterns_getstarted_device.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="bf928-154">Save and close the **dmpatterns_getstarted_device.js** file.</span></span>
   
> [!NOTE]
> <span data-ttu-id="bf928-155">Om de zaken niet nodeloos ingewikkeld te maken, is in deze handleiding geen beleid voor opnieuw proberen geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="bf928-155">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="bf928-156">Bij de productiecode moet u een beleid voor opnieuw proberen implementeren (zoals exponentieel uitstel), zoals aangegeven in het MSDN-artikel [Transient Fault Handling][lnk-transient-faults] (Afhandeling van tijdelijke fouten).</span><span class="sxs-lookup"><span data-stu-id="bf928-156">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>


## <a name="run-the-apps"></a><span data-ttu-id="bf928-157">De apps uitvoeren</span><span class="sxs-lookup"><span data-stu-id="bf928-157">Run the apps</span></span>
<span data-ttu-id="bf928-158">U kunt nu de apps uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="bf928-158">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="bf928-159">Bij de opdrachtprompt in de **manageddevice** map, voer de volgende opdracht om te beginnen met luisteren naar de directe methode voor opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="bf928-159">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="bf928-160">Uitvoeren van de C#-consoletoepassing **TriggerReboot**.</span><span class="sxs-lookup"><span data-stu-id="bf928-160">Run the C# console app **TriggerReboot**.</span></span> <span data-ttu-id="bf928-161">Met de rechtermuisknop op de **TriggerReboot** project, selecteer **Debug**, en selecteer vervolgens **nieuw exemplaar gestart**.</span><span class="sxs-lookup"><span data-stu-id="bf928-161">Right-click the **TriggerReboot** project, select **Debug**, and then select **Start new instance**.</span></span>

3. <span data-ttu-id="bf928-162">U ziet de reactie van het apparaat aan de directe methode in de console.</span><span class="sxs-lookup"><span data-stu-id="bf928-162">You see the device response to the direct method in the console.</span></span>

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png
[img-servicenuget]: media/iot-hub-csharp-node-device-management-get-started/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-device-management-get-started/createnetapp.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups to manage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/