---
title: Azure IoT Hub directe methoden (knooppunt) | Microsoft Docs
description: Het gebruik van Azure IoT Hub rechtstreekse methoden. U kunt Azure IoT SDK's voor Node.js gebruiken voor het implementeren van een gesimuleerde apparaattoepassing die een directe methode bevat en een service-app die de directe methode aanroept.
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
ms.openlocfilehash: 83725c3ae3fd3807f2469be888e270ba078a8972
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="use-direct-methods-on-your-iot-device-with-nodejs"></a><span data-ttu-id="2e885-104">Directe methoden te gebruiken op uw IoT-apparaat met behulp van Node.js</span><span class="sxs-lookup"><span data-stu-id="2e885-104">Use direct methods on your IoT device with Node.js</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="2e885-105">Aan het einde van deze zelfstudie hebt u twee console Node.js-apps:</span><span class="sxs-lookup"><span data-stu-id="2e885-105">At the end of this tutorial, you have two Node.js console apps:</span></span>

* <span data-ttu-id="2e885-106">**CallMethodOnDevice.js**, die een methode wordt aangeroepen in de gesimuleerde apparaattoepassing en het antwoord weergegeven.</span><span class="sxs-lookup"><span data-stu-id="2e885-106">**CallMethodOnDevice.js**, which calls a method in the simulated device app and displays the response.</span></span>
* <span data-ttu-id="2e885-107">**SimulatedDevice.js**, die verbinding maakt met uw IoT-hub aan de apparaat-id eerder hebt gemaakt en reageert op de methode aangeroepen door de cloud.</span><span class="sxs-lookup"><span data-stu-id="2e885-107">**SimulatedDevice.js**, which connects to your IoT hub with the device identity created earlier, and responds to the method called by the cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="2e885-108">Het artikel [Azure IoT-SDK's][lnk-hub-sdks] bevat informatie over de verschillende Azure IoT-SDK's die u kunt gebruiken om beide toepassingen zo te maken dat ze zowel op het apparaat als op de back-end van uw oplossing kunnen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="2e885-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="2e885-109">Voor het voltooien van deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="2e885-109">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="2e885-110">Node.js versie 0.10.x of hoger.</span><span class="sxs-lookup"><span data-stu-id="2e885-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="2e885-111">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="2e885-111">An active Azure account.</span></span> <span data-ttu-id="2e885-112">(Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)</span><span class="sxs-lookup"><span data-stu-id="2e885-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="2e885-113">Een gesimuleerde apparaattoepassing maken</span><span class="sxs-lookup"><span data-stu-id="2e885-113">Create a simulated device app</span></span>
<span data-ttu-id="2e885-114">In deze sectie maakt u een Node.js-consoletoepassing dat met een methode aangeroepen door de cloud overeenkomt.</span><span class="sxs-lookup"><span data-stu-id="2e885-114">In this section, you create a Node.js console app that responds to a method called by the cloud.</span></span>

1. <span data-ttu-id="2e885-115">Maak een nieuwe lege map met de naam **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="2e885-115">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="2e885-116">In de map **simulateddevice** maakt u een package.json-bestand door in het opdrachtprompt de volgende opdracht op te geven.</span><span class="sxs-lookup"><span data-stu-id="2e885-116">In the **simulateddevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="2e885-117">Accepteer alle standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="2e885-117">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="2e885-118">In de opdrachtprompt in de map **simulateddevice** voert u de volgende opdracht uit om het **azure-iot-device-amqp** Device SDK-pakket en het **azure-iot-device-mqtt**-pakket te installeren:</span><span class="sxs-lookup"><span data-stu-id="2e885-118">At your command prompt in the **simulateddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="2e885-119">Maak met een tekstverwerker een nieuw bestand **SimulatedDevice.js** in de map **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="2e885-119">Using a text editor, create a new **SimulatedDevice.js** file in the **simulateddevice** folder.</span></span>
4. <span data-ttu-id="2e885-120">Voeg de volgende `require` instructies toe aan het begin van het bestand **SimulatedDevice.js**:</span><span class="sxs-lookup"><span data-stu-id="2e885-120">Add the following `require` statements at the start of the **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="2e885-121">Voeg een **connectionString** variabele en deze gebruiken voor het maken een **DeviceClient** exemplaar.</span><span class="sxs-lookup"><span data-stu-id="2e885-121">Add a **connectionString** variable and use it to create a **DeviceClient** instance.</span></span> <span data-ttu-id="2e885-122">Vervang **{verbindingsreeks apparaat}** tekenreeks met de apparaatverbinding u hebt gegenereerd tijdens de *maken van een apparaat-id* sectie:</span><span class="sxs-lookup"><span data-stu-id="2e885-122">Replace **{device connection string}** with the device connection string you generated in the *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="2e885-123">Voeg de volgende functie voor het implementeren van de methode op het apparaat toe:</span><span class="sxs-lookup"><span data-stu-id="2e885-123">Add the following function to implement the method on the device:</span></span>
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written to log.', function(err) {
            if(err) {
                console.error('An error ocurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. <span data-ttu-id="2e885-124">Open de verbinding met uw IoT-hub en begin initialiseren de listener voor methode:</span><span class="sxs-lookup"><span data-stu-id="2e885-124">Open the connection to your IoT hub and start initialize the method listener:</span></span>
   
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
8. <span data-ttu-id="2e885-125">Sla het bestand **SimulatedDevice.js** op en sluit het.</span><span class="sxs-lookup"><span data-stu-id="2e885-125">Save and close the **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="2e885-126">Om de zaken niet nodeloos ingewikkeld te maken, is in deze handleiding geen beleid voor opnieuw proberen geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="2e885-126">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="2e885-127">In productiecode moet u beleid voor opnieuw proberen (zoals verbinding opnieuw), zoals voorgesteld in het MSDN-artikel implementeren [afhandeling van tijdelijke fout][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="2e885-127">In production code, you should implement retry policies (such as connection retry), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-method-on-a-device"></a><span data-ttu-id="2e885-128">Een methode is aangeroepen voor een apparaat</span><span class="sxs-lookup"><span data-stu-id="2e885-128">Call a method on a device</span></span>
<span data-ttu-id="2e885-129">In deze sectie maakt u een Node.js-consoletoepassing die een methode wordt aangeroepen in de gesimuleerde apparaattoepassing en wordt vervolgens het antwoord.</span><span class="sxs-lookup"><span data-stu-id="2e885-129">In this section, you create a Node.js console app that calls a method in the simulated device app and then displays the response.</span></span>

1. <span data-ttu-id="2e885-130">Maak een nieuwe lege map genaamd **callmethodondevice**.</span><span class="sxs-lookup"><span data-stu-id="2e885-130">Create a new empty folder called **callmethodondevice**.</span></span> <span data-ttu-id="2e885-131">In de **callmethodondevice** map, maakt u een package.json-bestand met de volgende opdracht achter de opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="2e885-131">In the **callmethodondevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="2e885-132">Accepteer alle standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="2e885-132">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="2e885-133">Bij de opdrachtprompt in de **callmethodondevice** map, voer de volgende opdracht voor het installeren van de **azure-iothub** pakket:</span><span class="sxs-lookup"><span data-stu-id="2e885-133">At your command prompt in the **callmethodondevice** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="2e885-134">Maak met een teksteditor, een **CallMethodOnDevice.js** bestand de **callmethodondevice** map.</span><span class="sxs-lookup"><span data-stu-id="2e885-134">Using a text editor, create a **CallMethodOnDevice.js** file in the **callmethodondevice** folder.</span></span>
4. <span data-ttu-id="2e885-135">Voeg de volgende `require` instructies aan het begin van de **CallMethodOnDevice.js** bestand:</span><span class="sxs-lookup"><span data-stu-id="2e885-135">Add the following `require` statements at the start of the **CallMethodOnDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="2e885-136">Voeg de volgende variabeledeclaratie toe en vervang de waarde van de tijdelijke aanduiding door de IoT Hub-verbindingsreeks van uw hub:</span><span class="sxs-lookup"><span data-stu-id="2e885-136">Add the following variable declaration and replace the placeholder value with the IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    var methodName = 'writeLine';
    var deviceId = 'myDeviceId';
    ```
6. <span data-ttu-id="2e885-137">De client voor het openen van de verbinding met uw iothub maken.</span><span class="sxs-lookup"><span data-stu-id="2e885-137">Create the client to open the connection to your IoT hub.</span></span>
   
    ```
    var client = Client.fromConnectionString(connectionString);
    ```
7. <span data-ttu-id="2e885-138">Voeg de volgende functie zodat deze de apparaat-methode worden aangeroepen en de reactie van het apparaat naar de console afdrukken:</span><span class="sxs-lookup"><span data-stu-id="2e885-138">Add the following function to invoke the device method and print the device response to the console:</span></span>
   
    ```
    var methodParams = {
        methodName: methodName,
        payload: 'hello world',
        timeoutInSeconds: 30
    };
   
    client.invokeDeviceMethod(deviceId, methodParams, function (err, result) {
        if (err) {
            console.error('Failed to invoke method \'' + methodName + '\': ' + err.message);
        } else {
            console.log(methodName + ' on ' + deviceId + ':');
            console.log(JSON.stringify(result, null, 2));
        }
    });
    ```
8. <span data-ttu-id="2e885-139">Sla op en sluit de **CallMethodOnDevice.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="2e885-139">Save and close the **CallMethodOnDevice.js** file.</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="2e885-140">De apps uitvoeren</span><span class="sxs-lookup"><span data-stu-id="2e885-140">Run the apps</span></span>
<span data-ttu-id="2e885-141">U kunt nu de apps uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="2e885-141">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="2e885-142">Bij een opdrachtprompt in de **simulateddevice** map, voer de volgende opdracht om te beginnen met luisteren voor methodeaanroepen vanuit uw IoT-Hub:</span><span class="sxs-lookup"><span data-stu-id="2e885-142">At a command prompt in the **simulateddevice** folder, run the following command to start listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![][7]
2. <span data-ttu-id="2e885-143">Bij een opdrachtprompt in de **callmethodondevice** map, voer de volgende opdracht om te beginnen met bewaken van uw IoT-hub:</span><span class="sxs-lookup"><span data-stu-id="2e885-143">At a command prompt in the **callmethodondevice** folder, run the following command to begin monitoring your IoT hub:</span></span>
   
    ```
    node CallMethodOnDevice.js 
    ```
   
    ![][8]
3. <span data-ttu-id="2e885-144">Hier ziet u het apparaat aan de methode reageren door het afdrukken van het bericht en de toepassing die het antwoord van de weergave van de methode van het apparaat aangeroepen:</span><span class="sxs-lookup"><span data-stu-id="2e885-144">You will see the device react to the method by printing out the message and the application which called the method display the response from the device:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="2e885-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2e885-145">Next steps</span></span>
<span data-ttu-id="2e885-146">In deze handleiding hebt u een nieuwe IoT-hub geconfigureerd in Azure Portal en vervolgens een apparaat-id gemaakt in het id-register van de IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="2e885-146">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="2e885-147">U hebt deze apparaat-id gebruikt om in te schakelen van de gesimuleerde apparaattoepassing om te reageren op de methoden die worden aangeroepen door de cloud.</span><span class="sxs-lookup"><span data-stu-id="2e885-147">You used this device identity to enable the simulated device app to react to methods invoked by the cloud.</span></span> <span data-ttu-id="2e885-148">Hebt u ook een app roept methoden op het apparaat en de reactie van het apparaat wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="2e885-148">You also created an app that invokes methods on the device and displays the response from the device.</span></span> 

<span data-ttu-id="2e885-149">Als u aan de slag wilt gaan met IoT Hub en andere IoT-scenario's wilt verkennen, leest u deze artikelen:</span><span class="sxs-lookup"><span data-stu-id="2e885-149">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="2e885-150">[Aan de slag met IoT Hub]</span><span class="sxs-lookup"><span data-stu-id="2e885-150">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="2e885-151">[Taken plannen op meerdere apparaten][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="2e885-151">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="2e885-152">Zie voor meer informatie over het uitbreiden van uw IoT-oplossing en schema-methode op meerdere apparaten aanroepen, de [planning en broadcast taken] [ lnk-tutorial-jobs] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="2e885-152">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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
