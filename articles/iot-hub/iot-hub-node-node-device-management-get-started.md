---
title: aaaGet de slag met Azure IoT Hub Apparaatbeheer (knooppunt) | Microsoft Docs
description: Hoe toouse IoT Hub apparaat management tooinitiate een extern apparaat opnieuw worden opgestart. U gebruikt hello Azure IoT SDK voor Node.js tooimplement een gesimuleerde apparaattoepassing die een directe methode bevat en een service-app die Hallo directe methode aanroept.
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
ms.openlocfilehash: 5dd1878e71231850fb95f4170b823f1e86c3ee83
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-management-node"></a><span data-ttu-id="7d651-104">Aan de slag met Apparaatbeheer (knooppunt)</span><span class="sxs-lookup"><span data-stu-id="7d651-104">Get started with device management (Node)</span></span>

[!INCLUDE [iot-hub-selector-dm-getstarted](../../includes/iot-hub-selector-dm-getstarted.md)]

<span data-ttu-id="7d651-105">In deze handleiding ontdekt u hoe u:</span><span class="sxs-lookup"><span data-stu-id="7d651-105">This tutorial shows you how to:</span></span>

* <span data-ttu-id="7d651-106">Gebruik Hallo toocreate met Azure portal een IoT-Hub en een apparaat-id maakt in uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="7d651-106">Use hello Azure portal toocreate an IoT Hub and create a device identity in your IoT hub.</span></span>
* <span data-ttu-id="7d651-107">Maak een gesimuleerde apparaattoepassing met een directe methode die het apparaat opnieuw wordt opgestart.</span><span class="sxs-lookup"><span data-stu-id="7d651-107">Create a simulated device app that contains a direct method that reboots that device.</span></span> <span data-ttu-id="7d651-108">Rechtstreekse methoden worden aangeroepen vanuit Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="7d651-108">Direct methods are invoked from hello cloud.</span></span>
* <span data-ttu-id="7d651-109">Een Node.js-consoletoepassing die Hallo opnieuw opstarten directe methode in Hallo gesimuleerde apparaattoepassing via uw IoT-hub aanroept maken.</span><span class="sxs-lookup"><span data-stu-id="7d651-109">Create a Node.js console app that calls hello reboot direct method in hello simulated device app through your IoT hub.</span></span>

<span data-ttu-id="7d651-110">Aan het einde van de Hallo van deze zelfstudie hebt u twee console Node.js-apps:</span><span class="sxs-lookup"><span data-stu-id="7d651-110">At hello end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="7d651-111">**dmpatterns_getstarted_device.js**, die tooyour IoT-hub verbindt met apparaat-id Hallo eerder hebt gemaakt, ontvangt van een directe methode voor opnieuw opstarten, simuleert fysieke opnieuw worden opgestart en Hallo tijd voor de laatste keer opnieuw opstarten Hallo rapporteert.</span><span class="sxs-lookup"><span data-stu-id="7d651-111">**dmpatterns_getstarted_device.js**, which connects tooyour IoT hub with hello device identity created earlier, receives a reboot direct method, simulates a physical reboot, and reports hello time for hello last reboot.</span></span>

<span data-ttu-id="7d651-112">**dmpatterns_getstarted_service.js**, die een directe methode wordt aangeroepen in de gesimuleerde apparaattoepassing hello, geeft antwoord Hallo weer en geeft Hallo bijgewerkt gerapporteerd eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="7d651-112">**dmpatterns_getstarted_service.js**, which calls a direct method in hello simulated device app, displays hello response, and displays hello updated reported properties.</span></span>

<span data-ttu-id="7d651-113">toocomplete in deze zelfstudie, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="7d651-113">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="7d651-114">Node.js-versie 0.12.x of hoger</span><span class="sxs-lookup"><span data-stu-id="7d651-114">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="7d651-115">[Uw ontwikkelingsomgeving voorbereiden] [ lnk-dev-setup] wordt beschreven hoe tooinstall Node.js voor deze zelfstudie op Windows of Linux.</span><span class="sxs-lookup"><span data-stu-id="7d651-115">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="7d651-116">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="7d651-116">An active Azure account.</span></span> <span data-ttu-id="7d651-117">(Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)</span><span class="sxs-lookup"><span data-stu-id="7d651-117">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="7d651-118">Een gesimuleerde apparaattoepassing maken</span><span class="sxs-lookup"><span data-stu-id="7d651-118">Create a simulated device app</span></span>
<span data-ttu-id="7d651-119">In deze sectie wordt u</span><span class="sxs-lookup"><span data-stu-id="7d651-119">In this section, you will</span></span>

* <span data-ttu-id="7d651-120">Een Node.js-consoletoepassing die tooa directe methode aangeroepen door Hallo cloud reageert maken</span><span class="sxs-lookup"><span data-stu-id="7d651-120">Create a Node.js console app that responds tooa direct method called by hello cloud</span></span>
* <span data-ttu-id="7d651-121">Een gesimuleerd apparaat opnieuw activeren</span><span class="sxs-lookup"><span data-stu-id="7d651-121">Trigger a simulated device reboot</span></span>
* <span data-ttu-id="7d651-122">Gebruik Hallo gerapporteerd eigenschappen tooenable apparaat twin query's tooidentify apparaten en wanneer ze laatste opnieuw opgestart</span><span class="sxs-lookup"><span data-stu-id="7d651-122">Use hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted</span></span>

1. <span data-ttu-id="7d651-123">U maakt een lege map met de naam **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="7d651-123">Create an empty folder called **manageddevice**.</span></span>  <span data-ttu-id="7d651-124">In Hallo **manageddevice** map, een package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="7d651-124">In hello **manageddevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="7d651-125">Accepteer alle Hallo standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="7d651-125">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="7d651-126">Bij de opdrachtprompt in Hallo **manageddevice** map na de opdracht tooinstall Hallo Hallo **azure-iot-device** apparaat-SDK-pakket en **azure-iot-device-mqtt**pakket:</span><span class="sxs-lookup"><span data-stu-id="7d651-126">At your command prompt in hello **manageddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="7d651-127">Maak met een teksteditor, een **dmpatterns_getstarted_device.js** bestand in Hallo **manageddevice** map.</span><span class="sxs-lookup"><span data-stu-id="7d651-127">Using a text editor, create a **dmpatterns_getstarted_device.js** file in hello **manageddevice** folder.</span></span>
4. <span data-ttu-id="7d651-128">Toevoegen van de volgende Hallo 'vereist' instructies toe aan Hallo begin Hallo **dmpatterns_getstarted_device.js** bestand:</span><span class="sxs-lookup"><span data-stu-id="7d651-128">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_device.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="7d651-129">Voeg een **connectionString** variabele en gebruik deze toocreate een **Client** exemplaar.</span><span class="sxs-lookup"><span data-stu-id="7d651-129">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span>  <span data-ttu-id="7d651-130">Hallo-verbindingsreeks vervangen door de verbindingsreeks van uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="7d651-130">Replace hello connection string with your device connection string.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myDeviceId;SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="7d651-131">Hallo functie tooimplement Hallo directe methode volgen op Hallo apparaat toevoegen</span><span class="sxs-lookup"><span data-stu-id="7d651-131">Add hello following function tooimplement hello direct method on hello device</span></span>
   
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
7. <span data-ttu-id="7d651-132">Open Hallo verbinding tooyour IoT-hub en Hallo directe methode listener starten:</span><span class="sxs-lookup"><span data-stu-id="7d651-132">Open hello connection tooyour IoT hub and start hello direct method listener:</span></span>
   
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
8. <span data-ttu-id="7d651-133">Opslaan en sluiten Hallo **dmpatterns_getstarted_device.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="7d651-133">Save and close hello **dmpatterns_getstarted_device.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="7d651-134">tookeep dingen eenvoudige, deze zelfstudie wordt niet geïmplementeerd voor een beleid voor opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="7d651-134">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="7d651-135">In productiecode moet u beleid voor opnieuw proberen (zoals exponentieel uitstel), zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="7d651-135">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="trigger-a-remote-reboot-on-hello-device-using-a-direct-method"></a><span data-ttu-id="7d651-136">Activeren van een extern opnieuw opstarten op Hallo-apparaat met een directe methode</span><span class="sxs-lookup"><span data-stu-id="7d651-136">Trigger a remote reboot on hello device using a direct method</span></span>
<span data-ttu-id="7d651-137">In deze sectie maakt maken u een Node.js-consoletoepassing die start een extern opnieuw opstarten op een apparaat met een directe methode.</span><span class="sxs-lookup"><span data-stu-id="7d651-137">In this section, you create a Node.js console app that initiates a remote reboot on a device using a direct method.</span></span> <span data-ttu-id="7d651-138">Hallo app gebruikmaakt van apparaat twin query's toodiscover Hallo keer opnieuw opstarten voor dat apparaat.</span><span class="sxs-lookup"><span data-stu-id="7d651-138">hello app uses device twin queries toodiscover hello last reboot time for that device.</span></span>

1. <span data-ttu-id="7d651-139">Maak een lege map genaamd **triggerrebootondevice**.</span><span class="sxs-lookup"><span data-stu-id="7d651-139">Create an empty folder called **triggerrebootondevice**.</span></span>  <span data-ttu-id="7d651-140">In Hallo **triggerrebootondevice** map, een package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="7d651-140">In hello **triggerrebootondevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="7d651-141">Accepteer alle Hallo standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="7d651-141">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="7d651-142">Bij de opdrachtprompt in Hallo **triggerrebootondevice** map na de opdracht tooinstall Hallo Hallo **azure-iothub** apparaat-SDK-pakket en **azure-iot-device-mqtt** pakket:</span><span class="sxs-lookup"><span data-stu-id="7d651-142">At your command prompt in hello **triggerrebootondevice** folder, run hello following command tooinstall hello **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="7d651-143">Maak met een teksteditor, een **dmpatterns_getstarted_service.js** bestand in Hallo **triggerrebootondevice** map.</span><span class="sxs-lookup"><span data-stu-id="7d651-143">Using a text editor, create a **dmpatterns_getstarted_service.js** file in hello **triggerrebootondevice** folder.</span></span>
4. <span data-ttu-id="7d651-144">Toevoegen van de volgende Hallo 'vereist' instructies toe aan Hallo begin Hallo **dmpatterns_getstarted_service.js** bestand:</span><span class="sxs-lookup"><span data-stu-id="7d651-144">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="7d651-145">Hallo na variabelendeclaraties toevoegen en vervang de waarden van de tijdelijke aanduiding Hallo:</span><span class="sxs-lookup"><span data-stu-id="7d651-145">Add hello following variable declarations and replace hello placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToReboot = 'myDeviceId';
    ```
6. <span data-ttu-id="7d651-146">Hallo functie tooinvoke Hallo apparaat methode tooreboot Hallo doelapparaat volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="7d651-146">Add hello following function tooinvoke hello device method tooreboot hello target device:</span></span>
   
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
                console.log("Successfully invoked hello device tooreboot.");  
            }
        });
    };
    ```
7. <span data-ttu-id="7d651-147">Hallo volgende tooquery voor Hallo apparaat werken en ophalen van Hallo keer opnieuw opstarten toevoegen:</span><span class="sxs-lookup"><span data-stu-id="7d651-147">Add hello following function tooquery for hello device and get hello last reboot time:</span></span>
   
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
                console.log('Waiting for device tooreport last reboot time.');
        });
    };
    ```
8. <span data-ttu-id="7d651-148">Hallo code toocall Hallo functies waarmee Hallo geactiveerd na opnieuw opstarten directe methode en de query voor Hallo laatste keer opnieuw opstarten toevoegen:</span><span class="sxs-lookup"><span data-stu-id="7d651-148">Add hello following code toocall hello functions that trigger hello reboot direct method and query for hello last reboot time:</span></span>
   
    ```
    startRebootDevice();
    setInterval(queryTwinLastReboot, 2000);
    ```
9. <span data-ttu-id="7d651-149">Opslaan en sluiten Hallo **dmpatterns_getstarted_service.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="7d651-149">Save and close hello **dmpatterns_getstarted_service.js** file.</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="7d651-150">Hallo-apps uitvoeren</span><span class="sxs-lookup"><span data-stu-id="7d651-150">Run hello apps</span></span>
<span data-ttu-id="7d651-151">U bent nu klaar toorun Hallo apps.</span><span class="sxs-lookup"><span data-stu-id="7d651-151">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="7d651-152">Bij de opdrachtprompt Hallo in Hallo **manageddevice** map Hallo opdracht toobegin luisteren naar Hallo opnieuw opstarten directe methode te volgen.</span><span class="sxs-lookup"><span data-stu-id="7d651-152">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_getstarted_device.js
    ```
2. <span data-ttu-id="7d651-153">Bij de opdrachtprompt Hallo in Hallo **triggerrebootondevice** map Hallo opdracht tootrigger Hallo afstand na opnieuw opstarten en query's uitvoeren voor Hallo apparaat twin toofind Hallo laatste keer opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="7d651-153">At hello command prompt in hello **triggerrebootondevice** folder, run hello following command tootrigger hello remote reboot and query for hello device twin toofind hello last reboot time.</span></span>
   
    ```
    node dmpatterns_getstarted_service.js
    ```
3. <span data-ttu-id="7d651-154">U ziet Hallo apparaat antwoord toohello directe methode in Hallo-console.</span><span class="sxs-lookup"><span data-stu-id="7d651-154">You see hello device response toohello direct method in hello console.</span></span>

[!INCLUDE [iot-hub-dm-followup](../../includes/iot-hub-dm-followup.md)]

<!-- images and links -->
[img-output]: media/iot-hub-get-started-with-dm/image6.png
[img-dm-ui]: media/iot-hub-get-started-with-dm/dmui.png

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[Azure portal]: https://portal.azure.com/
[Using resource groups toomanage your Azure resources]: ../azure-portal/resource-group-portal.md
[lnk-dm-github]: https://github.com/Azure/azure-iot-device-management

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
