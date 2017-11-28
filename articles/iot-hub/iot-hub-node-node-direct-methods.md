---
title: aaaAzure IoT Hub directe methoden (knooppunt) | Microsoft Docs
description: Hoe Azure IoT Hub toouse directe methoden. U hello Azure IoT SDK's gebruiken voor Node.js tooimplement een gesimuleerde apparaattoepassing die een directe methode bevat en een service-app die Hallo directe methode aanroept.
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: ea9c73ca-7778-4e38-a8f1-0bee9d142f04
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 12300ba451816fec1f80163b633f6b6e411d9e5c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-on-your-iot-device-with-nodejs"></a><span data-ttu-id="7e305-104">Directe methoden te gebruiken op uw IoT-apparaat met behulp van Node.js</span><span class="sxs-lookup"><span data-stu-id="7e305-104">Use direct methods on your IoT device with Node.js</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="7e305-105">Aan het einde van de Hallo van deze zelfstudie hebt u twee console Node.js-apps:</span><span class="sxs-lookup"><span data-stu-id="7e305-105">At hello end of this tutorial, you have two Node.js console apps:</span></span>

* <span data-ttu-id="7e305-106">**CallMethodOnDevice.js**, die een methode wordt aangeroepen in de gesimuleerde apparaattoepassing Hallo en antwoord Hallo weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7e305-106">**CallMethodOnDevice.js**, which calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="7e305-107">**SimulatedDevice.js**, die tooyour IoT-hub aan Hallo apparaat-id eerder hebt gemaakt, en toohello methode aangeroepen door Hallo cloud reageert.</span><span class="sxs-lookup"><span data-stu-id="7e305-107">**SimulatedDevice.js**, which connects tooyour IoT hub with hello device identity created earlier, and responds toohello method called by hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="7e305-108">Hallo artikel [Azure IoT SDK's] [ lnk-hub-sdks] bevat informatie over hello Azure IoT SDK's waarmee u toobuild beide toorun toepassingen op apparaten en de back-end van uw oplossing kunt.</span><span class="sxs-lookup"><span data-stu-id="7e305-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="7e305-109">toocomplete in deze zelfstudie, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="7e305-109">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="7e305-110">Node.js versie 0.10.x of hoger.</span><span class="sxs-lookup"><span data-stu-id="7e305-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="7e305-111">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="7e305-111">An active Azure account.</span></span> <span data-ttu-id="7e305-112">(Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)</span><span class="sxs-lookup"><span data-stu-id="7e305-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="7e305-113">Een gesimuleerde apparaattoepassing maken</span><span class="sxs-lookup"><span data-stu-id="7e305-113">Create a simulated device app</span></span>
<span data-ttu-id="7e305-114">In deze sectie maakt maken u een Node.js-consoletoepassing die tooa methode aangeroepen door Hallo cloud reageert.</span><span class="sxs-lookup"><span data-stu-id="7e305-114">In this section, you create a Node.js console app that responds tooa method called by hello cloud.</span></span>

1. <span data-ttu-id="7e305-115">Maak een nieuwe lege map met de naam **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="7e305-115">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="7e305-116">In Hallo **simulateddevice** map, een package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="7e305-116">In hello **simulateddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="7e305-117">Accepteer alle Hallo standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="7e305-117">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="7e305-118">Bij de opdrachtprompt in Hallo **simulateddevice** map na de opdracht tooinstall Hallo Hallo **azure-iot-device** apparaat-SDK-pakket en **azure-iot-device-mqtt**pakket:</span><span class="sxs-lookup"><span data-stu-id="7e305-118">At your command prompt in hello **simulateddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="7e305-119">Start een teksteditor en maak een nieuwe **SimulatedDevice.js** bestand in Hallo **simulateddevice** map.</span><span class="sxs-lookup"><span data-stu-id="7e305-119">Using a text editor, create a new **SimulatedDevice.js** file in hello **simulateddevice** folder.</span></span>
4. <span data-ttu-id="7e305-120">Voeg de volgende Hallo `require` instructies aan Hallo start Hallo **SimulatedDevice.js** bestand:</span><span class="sxs-lookup"><span data-stu-id="7e305-120">Add hello following `require` statements at hello start of hello **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="7e305-121">Voeg een **connectionString** variabele en gebruik deze toocreate een **DeviceClient** exemplaar.</span><span class="sxs-lookup"><span data-stu-id="7e305-121">Add a **connectionString** variable and use it toocreate a **DeviceClient** instance.</span></span> <span data-ttu-id="7e305-122">Vervang **{verbindingsreeks apparaat}** met Hallo verbindingsreeks voor apparaat u hebt gegenereerd in Hallo *maken van een apparaat-id* sectie:</span><span class="sxs-lookup"><span data-stu-id="7e305-122">Replace **{device connection string}** with hello device connection string you generated in hello *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="7e305-123">Hallo functie tooimplement Hallo methode volgen op Hallo apparaat toevoegen:</span><span class="sxs-lookup"><span data-stu-id="7e305-123">Add hello following function tooimplement hello method on hello device:</span></span>
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written toolog.', function(err) {
            if(err) {
                console.error('An error ocurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. <span data-ttu-id="7e305-124">Open Hallo verbinding tooyour IoT-hub en geïnitialiseerd Hallo methode listener starten:</span><span class="sxs-lookup"><span data-stu-id="7e305-124">Open hello connection tooyour IoT hub and start initialize hello method listener:</span></span>
   
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
8. <span data-ttu-id="7e305-125">Opslaan en sluiten Hallo **SimulatedDevice.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="7e305-125">Save and close hello **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="7e305-126">tookeep dingen eenvoudige, deze zelfstudie wordt niet geïmplementeerd voor een beleid voor opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="7e305-126">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="7e305-127">In productiecode moet u beleid voor opnieuw proberen (zoals verbinding opnieuw), zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="7e305-127">In production code, you should implement retry policies (such as connection retry), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-method-on-a-device"></a><span data-ttu-id="7e305-128">Een methode is aangeroepen voor een apparaat</span><span class="sxs-lookup"><span data-stu-id="7e305-128">Call a method on a device</span></span>
<span data-ttu-id="7e305-129">In deze sectie maakt maken u een Node.js-consoletoepassing die een methode wordt aangeroepen in de gesimuleerde apparaattoepassing Hallo en wordt vervolgens weergegeven antwoord Hallo.</span><span class="sxs-lookup"><span data-stu-id="7e305-129">In this section, you create a Node.js console app that calls a method in hello simulated device app and then displays hello response.</span></span>

1. <span data-ttu-id="7e305-130">Maak een nieuwe lege map genaamd **callmethodondevice**.</span><span class="sxs-lookup"><span data-stu-id="7e305-130">Create a new empty folder called **callmethodondevice**.</span></span> <span data-ttu-id="7e305-131">In Hallo **callmethodondevice** map, een package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="7e305-131">In hello **callmethodondevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="7e305-132">Accepteer alle Hallo standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="7e305-132">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="7e305-133">Bij de opdrachtprompt in Hallo **callmethodondevice** map na de opdracht tooinstall Hallo Hallo **azure-iothub** pakket:</span><span class="sxs-lookup"><span data-stu-id="7e305-133">At your command prompt in hello **callmethodondevice** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="7e305-134">Maak met een teksteditor, een **CallMethodOnDevice.js** bestand in Hallo **callmethodondevice** map.</span><span class="sxs-lookup"><span data-stu-id="7e305-134">Using a text editor, create a **CallMethodOnDevice.js** file in hello **callmethodondevice** folder.</span></span>
4. <span data-ttu-id="7e305-135">Voeg de volgende Hallo `require` instructies aan Hallo start Hallo **CallMethodOnDevice.js** bestand:</span><span class="sxs-lookup"><span data-stu-id="7e305-135">Add hello following `require` statements at hello start of hello **CallMethodOnDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="7e305-136">Hallo na variabelendeclaratie toevoegen en vervang Hallo tijdelijke aanduidingswaarde met Hallo IoT Hub-verbindingsreeks voor uw hub:</span><span class="sxs-lookup"><span data-stu-id="7e305-136">Add hello following variable declaration and replace hello placeholder value with hello IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    var methodName = 'writeLine';
    var deviceId = 'myDeviceId';
    ```
6. <span data-ttu-id="7e305-137">Hallo client tooopen Hallo verbinding tooyour iothub maken.</span><span class="sxs-lookup"><span data-stu-id="7e305-137">Create hello client tooopen hello connection tooyour IoT hub.</span></span>
   
    ```
    var client = Client.fromConnectionString(connectionString);
    ```
7. <span data-ttu-id="7e305-138">Hallo functie tooinvoke Hallo apparaat methode afdrukken Hallo apparaat antwoord toohello console en volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="7e305-138">Add hello following function tooinvoke hello device method and print hello device response toohello console:</span></span>
   
    ```
    var methodParams = {
        methodName: methodName,
        payload: 'hello world',
        timeoutInSeconds: 30
    };
   
    client.invokeDeviceMethod(deviceId, methodParams, function (err, result) {
        if (err) {
            console.error('Failed tooinvoke method \'' + methodName + '\': ' + err.message);
        } else {
            console.log(methodName + ' on ' + deviceId + ':');
            console.log(JSON.stringify(result, null, 2));
        }
    });
    ```
8. <span data-ttu-id="7e305-139">Opslaan en sluiten Hallo **CallMethodOnDevice.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="7e305-139">Save and close hello **CallMethodOnDevice.js** file.</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="7e305-140">Hallo-apps uitvoeren</span><span class="sxs-lookup"><span data-stu-id="7e305-140">Run hello apps</span></span>
<span data-ttu-id="7e305-141">U bent nu klaar toorun Hallo apps.</span><span class="sxs-lookup"><span data-stu-id="7e305-141">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="7e305-142">Bij een opdrachtprompt in Hallo **simulateddevice** map Hallo opdracht toostart luisteren naar methodeaanroepen van uw IoT-Hub te volgen:</span><span class="sxs-lookup"><span data-stu-id="7e305-142">At a command prompt in hello **simulateddevice** folder, run hello following command toostart listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![][7]
2. <span data-ttu-id="7e305-143">Bij een opdrachtprompt in Hallo **callmethodondevice** map Hallo opdracht toobegin bewaking van uw IoT-hub te volgen:</span><span class="sxs-lookup"><span data-stu-id="7e305-143">At a command prompt in hello **callmethodondevice** folder, run hello following command toobegin monitoring your IoT hub:</span></span>
   
    ```
    node CallMethodOnDevice.js 
    ```
   
    ![][8]
3. <span data-ttu-id="7e305-144">Hier ziet u Hallo apparaat toohello methode reageren door het afdrukken van het Hallo-bericht en Hallo-toepassing die weergave Hallo antwoord voor Hallo methode vanuit Hallo apparaat aangeroepen:</span><span class="sxs-lookup"><span data-stu-id="7e305-144">You will see hello device react toohello method by printing out hello message and hello application which called hello method display hello response from hello device:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="7e305-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7e305-145">Next steps</span></span>
<span data-ttu-id="7e305-146">In deze zelfstudie maakt u een nieuwe iothub geconfigureerd in hello Azure-portal en vervolgens een apparaat-id in de id-register Hallo iothub hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7e305-146">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="7e305-147">U hebt deze apparaat-id tooenable Hallo gesimuleerd apparaat app tooreact toomethods aangeroepen door Hallo cloud gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7e305-147">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="7e305-148">Hebt u ook een app die wordt aangeroepen methoden op Hallo apparaat en geeft weer Hallo-antwoord van Hallo-apparaat hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7e305-148">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span> 

<span data-ttu-id="7e305-149">toocontinue aan de slag met IoT Hub en tooexplore raadpleegt u andere IoT-scenario's:</span><span class="sxs-lookup"><span data-stu-id="7e305-149">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="7e305-150">[Aan de slag met IoT Hub]</span><span class="sxs-lookup"><span data-stu-id="7e305-150">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="7e305-151">[Taken plannen op meerdere apparaten][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="7e305-151">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="7e305-152">toolearn hoe tooextend uw IoT-oplossing en schema-methode aanroepen op meerdere apparaten, raadpleegt u Hallo [planning en broadcast taken] [ lnk-tutorial-jobs] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="7e305-152">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-node-node-direct-methods/run-simulated-device.png
[8]: ./media/iot-hub-node-node-direct-methods/run-callmethodondevice.png
[9]: ./media/iot-hub-node-node-direct-methods/methods-output.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
[Aan de slag met IoT Hub]: iot-hub-node-node-getstarted.md
