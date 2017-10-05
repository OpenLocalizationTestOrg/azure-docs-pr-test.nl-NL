---
title: Aan de slag met Azure IoT Hub Apparaatbeheer (knooppunt) | Microsoft Docs
description: "Het externe apparaat opnieuw opstarten initiëren met Apparaatbeheer via IoT Hub. U kunt de Azure IoT SDK voor Node.js gebruiken voor het implementeren van een gesimuleerde apparaattoepassing die een directe methode bevat en een service-app die de directe methode aanroept."
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
ms.date: 08/25/2017
ms.author: juanpere
ms.openlocfilehash: 332a3e62cb1ef75e2c6dd5562ee799465c401128
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-device-management-node"></a><span data-ttu-id="a0b82-104">Aan de slag met Apparaatbeheer (knooppunt)</span><span class="sxs-lookup"><span data-stu-id="a0b82-104">Get started with device management (Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="a0b82-105">In deze handleiding ontdekt u hoe u:</span><span class="sxs-lookup"><span data-stu-id="a0b82-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="a0b82-106">De Azure portal gebruiken voor het maken van een IoT-Hub en een apparaat-id maakt in uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="a0b82-106">Use the Azure portal to create an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="a0b82-107">Maak een gesimuleerde apparaattoepassing met een directe methode die het apparaat opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="a0b82-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="a0b82-108">Rechtstreekse methoden worden aangeroepen vanuit de cloud.</span><span class="sxs-lookup"><span data-stu-id="a0b82-108">Direct methods are invoked from the cloud.</span></span>
* <span data-ttu-id="a0b82-109">Een Node.js-consoletoepassing die de directe methode voor opnieuw opstarten in de gesimuleerde apparaattoepassing via uw IoT-hub maken.</span><span class="sxs-lookup"><span data-stu-id="a0b82-109">Create a Node.js console app that calls the reboot direct method in the simulated device app through your IoT hub.</span></span>

<span data-ttu-id="a0b82-110">Aan het einde van deze zelfstudie hebt u twee console Node.js-apps:</span><span class="sxs-lookup"><span data-stu-id="a0b82-110">At the end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="a0b82-111">**dmpatterns_getstarted_device.js**, die verbinding maakt met uw IoT-hub aan de apparaat-id eerder hebt gemaakt, ontvangt u een directe methode voor opnieuw opstarten, simuleert fysieke opnieuw worden opgestart en rapporten van de tijd voor de laatste keer opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="a0b82-111">**dmpatterns_getstarted_device.js**, which connects to your IoT hub with the device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports the time for the last reboot.</span></span>

<span data-ttu-id="a0b82-112">**dmpatterns_getstarted_service.js**, die een directe methode wordt aangeroepen in de gesimuleerde apparaattoepassing geeft het antwoord weer en geeft de bijgewerkte eigenschappen gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="a0b82-112">**dmpatterns_getstarted_service.js**, which calls a direct method in the simulated device app, displays the response, and displays the updated reported properties.</span></span>

<span data-ttu-id="a0b82-113">Voor het voltooien van deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="a0b82-113">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="a0b82-114">Node.js-versie 0.12.x of hoger</span><span class="sxs-lookup"><span data-stu-id="a0b82-114">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="a0b82-115">[Uw ontwikkelingsomgeving voorbereiden] [ lnk-dev-setup] wordt beschreven hoe u Node.js voor deze zelfstudie installeren op Windows of Linux.</span><span class="sxs-lookup"><span data-stu-id="a0b82-115">[Prepare your development environment][lnk-dev-setup] describes how to install Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="a0b82-116">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="a0b82-116">An active Azure account.</span></span> <span data-ttu-id="a0b82-117">(Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)</span><span class="sxs-lookup"><span data-stu-id="a0b82-117">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="a0b82-118">Een gesimuleerde apparaattoepassing maken</span><span class="sxs-lookup"><span data-stu-id="a0b82-118">Create a simulated device app</span></span>
<span data-ttu-id="a0b82-119">In deze sectie wordt u</span><span class="sxs-lookup"><span data-stu-id="a0b82-119">In this section, you will</span></span>

* <span data-ttu-id="a0b82-120">U maakt een Node.js-console-app die reageert op een directe methode die door de cloud wordt aangeroepen.</span><span class="sxs-lookup"><span data-stu-id="a0b82-120">Create a Node.js console app that responds to a direct method called by the cloud</span></span>
* <span data-ttu-id="a0b82-121">Een gesimuleerd apparaat opnieuw activeren</span><span class="sxs-lookup"><span data-stu-id="a0b82-121">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="a0b82-122">Gebruik de gemelde eigenschappen om het apparaat twin query's om apparaten te identificeren en wanneer ze het laatst opnieuw opgestart</span><span class="sxs-lookup"><span data-stu-id="a0b82-122">Use the reported properties to enable device twin queries to identify devices and when they last rebooted</span></span>

1. <span data-ttu-id="a0b82-123">U maakt een lege map met de naam **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="a0b82-123">Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="a0b82-124">Maak in de map **simulateddevice** een bestand met de naam package.json door achter de opdrachtprompt de volgende opdracht op te geven.</span><span class="sxs-lookup"><span data-stu-id="a0b82-124">In the **manageddevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="a0b82-125">Accepteer alle standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="a0b82-125">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="a0b82-126">Bij de opdrachtprompt in de **manageddevice** map, voer de volgende opdracht voor het installeren van de **azure-iot-device** apparaat-SDK-pakket en **azure-iot-device-mqtt** pakket:</span><span class="sxs-lookup"><span data-stu-id="a0b82-126">At your command prompt in the **manageddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="a0b82-127">Maak met een teksteditor, een **dmpatterns_getstarted_device.js** bestand de **manageddevice** map.</span><span class="sxs-lookup"><span data-stu-id="a0b82-127">Using a text editor, create a **dmpatterns_getstarted_device.js** file in the **manageddevice** folder.</span></span>
4. <span data-ttu-id="a0b82-128">Voeg de volgende 'vereist' instructies aan het begin van de **dmpatterns_getstarted_device.js** bestand:</span><span class="sxs-lookup"><span data-stu-id="a0b82-128">Add the following 'require' statements at the start of the **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="a0b82-129">Voeg een **connectionString**-variabele toe en gebruik deze om een **client**exemplaar te maken.</span><span class="sxs-lookup"><span data-stu-id="a0b82-129">Add a **connectionString** variable and use it to create a **Client** instance.</span></span>  <span data-ttu-id="a0b82-130">De verbindingsreeks vervangen door de verbindingsreeks van uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="a0b82-130">Replace the connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="a0b82-131">De volgende functie voor het implementeren van de directe methode op het apparaat toevoegen</span><span class="sxs-lookup"><span data-stu-id="a0b82-131">Add the following function to implement the direct method on the device</span></span>
   
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
7. <span data-ttu-id="a0b82-132">Maak verbinding met uw IoT-hub en start de listener directe methode:</span><span class="sxs-lookup"><span data-stu-id="a0b82-132">Open the connection to your IoT hub and start the direct method listener:</span></span>
   
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
8. <span data-ttu-id="a0b82-133">Sla op en sluit de **dmpatterns_getstarted_device.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="a0b82-133">Save and close the **dmpatterns_getstarted_device.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="a0b82-134">Om de zaken niet nodeloos ingewikkeld te maken, is in deze handleiding geen beleid voor opnieuw proberen geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="a0b82-134">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="a0b82-135">Bij de productiecode moet u een beleid voor opnieuw proberen implementeren (zoals exponentieel uitstel), zoals aangegeven in het MSDN-artikel [Transient Fault Handling][lnk-transient-faults] (Afhandeling van tijdelijke fouten).</span><span class="sxs-lookup"><span data-stu-id="a0b82-135">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="trigger-a-remote-reboot-on-the-device-using-a-direct-method"></a><span data-ttu-id="a0b82-136">Activeren van een extern opnieuw opstarten op het apparaat met een directe methode</span><span class="sxs-lookup"><span data-stu-id="a0b82-136">Trigger a remote reboot on the device using a direct method</span></span>
<span data-ttu-id="a0b82-137">In deze sectie maakt maken u een Node.js-consoletoepassing die start een extern opnieuw opstarten op een apparaat met een directe methode.</span><span class="sxs-lookup"><span data-stu-id="a0b82-137">In this section, you create a Node.js console app that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="a0b82-138">De app gebruikmaakt van apparaat twin query's voor het detecteren van de laatste keer opnieuw opstarten voor dat apparaat.</span><span class="sxs-lookup"><span data-stu-id="a0b82-138">The app uses device twin queries to discover the last reboot time for that device.</span></span>

1. <span data-ttu-id="a0b82-139">Maak een lege map genaamd **triggerrebootondevice**.</span><span class="sxs-lookup"><span data-stu-id="a0b82-139">Create an empty folder called **triggerrebootondevice**.</span></span>  <span data-ttu-id="a0b82-140">In de **triggerrebootondevice** map, maakt u een package.json-bestand met de volgende opdracht achter de opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="a0b82-140">In the **triggerrebootondevice** folder, create a package.json file using the following command at your command prompt.</span></span>  <span data-ttu-id="a0b82-141">Accepteer alle standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="a0b82-141">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="a0b82-142">Bij de opdrachtprompt in de **triggerrebootondevice** map, voer de volgende opdracht voor het installeren van de **azure-iothub** apparaat-SDK-pakket en **azure-iot-device-mqtt** pakket:</span><span class="sxs-lookup"><span data-stu-id="a0b82-142">At your command prompt in the **triggerrebootondevice** folder, run the following command to install the **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="a0b82-143">Maak met een teksteditor, een **dmpatterns_getstarted_service.js** bestand de **triggerrebootondevice** map.</span><span class="sxs-lookup"><span data-stu-id="a0b82-143">Using a text editor, create a **dmpatterns_getstarted_service.js** file in the **triggerrebootondevice** folder.</span></span>
4. <span data-ttu-id="a0b82-144">Voeg de volgende 'vereist' instructies aan het begin van de **dmpatterns_getstarted_service.js** bestand:</span><span class="sxs-lookup"><span data-stu-id="a0b82-144">Add the following 'require' statements at the start of the **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="a0b82-145">Voeg de volgende variabele declaraties en vervang de tijdelijke aanduiding voor waarden:</span><span class="sxs-lookup"><span data-stu-id="a0b82-145">Add the following variable declarations and replace the placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToReboot = 'myDeviceId';
    ```
6. <span data-ttu-id="a0b82-146">De volgende functie voor het aanroepen van de methode van het apparaat opnieuw opstarten van het doelapparaat toevoegen:</span><span class="sxs-lookup"><span data-stu-id="a0b82-146">Add the following function to invoke the device method to reboot the target device:</span></span>
   
    ```
    var startRebootDevice = function(twin) {
   
        var methodName = "reboot";
   
        var methodParams = {
            methodName: methodName,
            payload: null,
            timeoutInSeconds: 30
        };
   
        client.invokeDeviceMethod(deviceToReboot, methodParams, function(err, result) {
            if (err) { 
                console.error("Direct method error: "+err.message);
            } else {
                console.log("Successfully invoked the device to reboot.");  
            }
        });
    };
    ```
7. <span data-ttu-id="a0b82-147">Voeg de volgende functie om een query voor het apparaat en krijgt u de laatste keer dat opnieuw opstarten:</span><span class="sxs-lookup"><span data-stu-id="a0b82-147">Add the following function to query for the device and get the last reboot time:</span></span>
   
    ```
    var queryTwinLastReboot = function() {
   
        registry.getTwin(deviceToReboot, function(err, twin){
   
            if (twin.properties.reported.iothubDM != null)
            {
                if (err) {
                    console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
                } else {
                    var lastRebootTime = twin.properties.reported.iothubDM.reboot.lastReboot;
                    console.log('Last reboot time: ' + JSON.stringify(lastRebootTime, null, 2));
                }
            } else 
                console.log('Waiting for device to report last reboot time.');
        });
    };
    ```
8. <span data-ttu-id="a0b82-148">Voeg de volgende code voor het aanroepen van de functies die de directe methode voor opnieuw opstarten en de query voor het laatst opnieuw activeren:</span><span class="sxs-lookup"><span data-stu-id="a0b82-148">Add the following code to call the functions that trigger the reboot direct method and query for the last reboot time:</span></span>
   
    ```
    startRebootDevice();
    setInterval(queryTwinLastReboot, 2000);
    ```
9. <span data-ttu-id="a0b82-149">Sla op en sluit de **dmpatterns_getstarted_service.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="a0b82-149">Save and close the **dmpatterns_getstarted_service.js** file.</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="a0b82-150">De apps uitvoeren</span><span class="sxs-lookup"><span data-stu-id="a0b82-150">Run the apps</span></span>
<span data-ttu-id="a0b82-151">U kunt nu de apps uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="a0b82-151">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="a0b82-152">Bij de opdrachtprompt in de **manageddevice** map, voer de volgende opdracht om te beginnen met luisteren naar de directe methode voor opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="a0b82-152">At the command prompt in the **manageddevice** folder, run the following command to begin listening for the reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="a0b82-153">Bij de opdrachtprompt in de **triggerrebootondevice** map, voer de volgende opdracht de extern opnieuw opstarten en de query voor het apparaat vinden van de laatste keer opnieuw activeren.</span><span class="sxs-lookup"><span data-stu-id="a0b82-153">At the command prompt in the **triggerrebootondevice** folder, run the following command to trigger the remote reboot and query for the device twin to find the last reboot time.</span></span>
   
    ```
    node dmpatterns_getstarted_service.js
    ```
3. <span data-ttu-id="a0b82-154">U ziet de reactie van het apparaat aan de directe methode in de console.</span><span class="sxs-lookup"><span data-stu-id="a0b82-154">You see the device response to the direct method in the console.</span></span>

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups to manage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
