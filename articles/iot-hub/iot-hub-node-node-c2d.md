---
title: Cloud-naar-apparaat-berichten met Azure IoT Hub (knooppunt) | Microsoft Docs
description: Het cloud-naar-apparaat om berichten te verzenden naar een apparaat van een Azure IoT hub met de Azure IoT SDK's voor Node.js. U kunt een gesimuleerde apparaattoepassing cloud-naar-apparaat-berichten ontvangen en wijzigen van een back-end-app voor het verzenden van de cloud-naar-apparaat-berichten wijzigen.
services: iot-hub
documentationcenter: nodejs
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3ca8a78f-ade2-46e8-8a49-d5d599cdf1f1
ms.service: iot-hub
ms.devlang: javascript
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 4580bda5633f84a7c7af0dc85f3cea4951024836
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-node"></a><span data-ttu-id="63160-104">Cloud-naar-apparaat-berichten verzenden met IoT Hub (knooppunt)</span><span class="sxs-lookup"><span data-stu-id="63160-104">Send cloud-to-device messages with IoT Hub (Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="63160-105">Inleiding</span><span class="sxs-lookup"><span data-stu-id="63160-105">Introduction</span></span>
<span data-ttu-id="63160-106">Azure IoT Hub is een volledig beheerde service waarmee stabiele en veilige tweerichtingscommunicatie tussen miljoenen apparaten inschakelen en een back-end oplossing.</span><span class="sxs-lookup"><span data-stu-id="63160-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="63160-107">De [aan de slag met IoT Hub] zelfstudie laat zien hoe u een iothub maken, een apparaat-id in het inrichten en code van een gesimuleerde apparaattoepassing dat apparaat-naar-cloud-berichten verzendt.</span><span class="sxs-lookup"><span data-stu-id="63160-107">The [Get started with IoT Hub] tutorial shows how to create an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="63160-108">Deze zelfstudie bouwt voort op [aan de slag met IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="63160-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="63160-109">Hier ziet u hoe aan:</span><span class="sxs-lookup"><span data-stu-id="63160-109">It shows you how to:</span></span>

* <span data-ttu-id="63160-110">Van uw back-end oplossing, cloud-naar-apparaat-berichten naar één enkel apparaat via IoT Hub te verzenden.</span><span class="sxs-lookup"><span data-stu-id="63160-110">From your solution back end, send cloud-to-device messages to a single device through IoT Hub.</span></span>
* <span data-ttu-id="63160-111">Cloud-naar-apparaat-berichten op een apparaat ontvangen.</span><span class="sxs-lookup"><span data-stu-id="63160-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="63160-112">Aanvragen van uw back-end oplossing, levering bevestiging (*feedback*) voor berichten die worden verzonden naar een apparaat uit IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="63160-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent to a device from IoT Hub.</span></span>

<span data-ttu-id="63160-113">U vindt meer informatie over cloud-naar-apparaat-berichten in de [Ontwikkelaarshandleiding voor IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="63160-113">You can find more information on cloud-to-device messages in the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="63160-114">Aan het einde van deze zelfstudie, moet u twee console Node.js-apps uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="63160-114">At the end of this tutorial, you run two Node.js console apps:</span></span>

* <span data-ttu-id="63160-115">**SimulatedDevice**, een aangepaste versie van de app gemaakt in [aan de slag met IoT Hub], die verbinding maakt met uw IoT-hub en cloud-naar-apparaat-berichten worden ontvangen.</span><span class="sxs-lookup"><span data-stu-id="63160-115">**SimulatedDevice**, a modified version of the app created in [Get started with IoT Hub], which connects to your IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="63160-116">**SendCloudToDeviceMessage**, die verzendt een bericht cloud-naar-apparaat naar de gesimuleerde apparaattoepassing via IoT Hub en vervolgens ontvangt de bevestiging levering.</span><span class="sxs-lookup"><span data-stu-id="63160-116">**SendCloudToDeviceMessage**, which sends a cloud-to-device message to the simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="63160-117">IoT-Hub heeft SDK-ondersteuning voor veel apparaatplatforms en talen (inclusief C, Java en Javascript) via Azure IoT-apparaat-SDK's.</span><span class="sxs-lookup"><span data-stu-id="63160-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="63160-118">Zie voor stapsgewijze instructies voor het koppelen van uw apparaat in deze zelfstudie code en in het algemeen naar Azure IoT Hub de [Azure IoT Developer Center].</span><span class="sxs-lookup"><span data-stu-id="63160-118">For step-by-step instructions on how to connect your device to this tutorial's code, and generally to Azure IoT Hub, see the [Azure IoT Developer Center].</span></span>
> 
> 

<span data-ttu-id="63160-119">Voor het voltooien van deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="63160-119">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="63160-120">Node.js versie 0.10.x of hoger.</span><span class="sxs-lookup"><span data-stu-id="63160-120">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="63160-121">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="63160-121">An active Azure account.</span></span> <span data-ttu-id="63160-122">(Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)</span><span class="sxs-lookup"><span data-stu-id="63160-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-the-simulated-device-app"></a><span data-ttu-id="63160-123">Berichten ontvangen in de gesimuleerde apparaattoepassing</span><span class="sxs-lookup"><span data-stu-id="63160-123">Receive messages in the simulated device app</span></span>
<span data-ttu-id="63160-124">In deze sectie, wijzigt u de gesimuleerde apparaattoepassing die u hebt gemaakt in [aan de slag met IoT Hub] cloud-naar-apparaat om berichten te ontvangen van de IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="63160-124">In this section, you modify the simulated device app you created in [Get started with IoT Hub] to receive cloud-to-device messages from the IoT hub.</span></span>

1. <span data-ttu-id="63160-125">Met een teksteditor, open het bestand SimulatedDevice.js.</span><span class="sxs-lookup"><span data-stu-id="63160-125">Using a text editor, open the SimulatedDevice.js file.</span></span>
2. <span data-ttu-id="63160-126">Wijzig de **connectCallback** functie voor het afhandelen van berichten uit IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="63160-126">Modify the **connectCallback** function to handle messages sent from IoT Hub.</span></span> <span data-ttu-id="63160-127">In dit voorbeeld wordt het apparaat altijd roept de **voltooid** functie IoT Hub melden dat deze het bericht is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="63160-127">In this example, the device always invokes the **complete** function to notify IoT Hub that it has processed the message.</span></span> <span data-ttu-id="63160-128">De nieuwe versie van de **connectCallback** functie lijkt op het volgende fragment:</span><span class="sxs-lookup"><span data-stu-id="63160-128">Your new version of the **connectCallback** function looks like the following snippet:</span></span>
   
    ```javascript
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
        client.on('message', function (msg) {
          console.log('Id: ' + msg.messageId + ' Body: ' + msg.data);
          client.complete(msg, printResultFor('completed'));
        });
        // Create a message and send it to the IoT Hub every second
        setInterval(function(){
            var temperature = 20 + (Math.random() * 15);
            var humidity = 60 + (Math.random() * 20);            
            var data = JSON.stringify({ deviceId: 'myFirstNodeDevice', temperature: temperature, humidity: humidity });
            var message = new Message(data);
            message.properties.add('temperatureAlert', (temperature > 30) ? 'true' : 'false');
            console.log("Sending message: " + message.getData());
            client.sendEvent(message, printResultFor('send'));
        }, 1000);
      }
    };
    ```
   
   > [!NOTE]
   > <span data-ttu-id="63160-129">Als u HTTP in plaats van de protocollen MQTT of AMQP zijn als het transport de **DeviceClient** exemplaar wordt gecontroleerd op berichten uit IoT Hub zelden (minder dan elke 25 minuten).</span><span class="sxs-lookup"><span data-stu-id="63160-129">If you use HTTP instead of MQTT or AMQP as the transport, the **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="63160-130">Zie voor meer informatie over de verschillen tussen de protocollen MQTT, AMQP en HTTP-ondersteuning en het beperken van Iothub de [Ontwikkelaarshandleiding voor IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="63160-130">For more information about the differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see the [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="63160-131">Een cloud naar apparaat verzenden</span><span class="sxs-lookup"><span data-stu-id="63160-131">Send a cloud-to-device message</span></span>
<span data-ttu-id="63160-132">In deze sectie maakt maken u een Node.js-consoletoepassing dat cloud-naar-apparaat-berichten naar de gesimuleerde apparaattoepassing verzendt.</span><span class="sxs-lookup"><span data-stu-id="63160-132">In this section, you create a Node.js console app that sends cloud-to-device messages to the simulated device app.</span></span> <span data-ttu-id="63160-133">U moet de apparaat-ID van het apparaat dat u hebt toegevoegd in de [aan de slag met IoT Hub] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="63160-133">You need the device ID of the device you added in the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="63160-134">U moet ook de IoT Hub-verbindingsreeks voor uw hub die u kunt vinden in de [Azure-portal].</span><span class="sxs-lookup"><span data-stu-id="63160-134">You also need the IoT Hub connection string for your hub that you can find in the [Azure portal].</span></span>

1. <span data-ttu-id="63160-135">Maak een lege map genaamd **sendcloudtodevicemessage**.</span><span class="sxs-lookup"><span data-stu-id="63160-135">Create an empty folder called **sendcloudtodevicemessage**.</span></span> <span data-ttu-id="63160-136">In de **sendcloudtodevicemessage** map, maakt u een package.json-bestand met de volgende opdracht achter de opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="63160-136">In the **sendcloudtodevicemessage** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="63160-137">Accepteer alle standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="63160-137">Accept all the defaults:</span></span>
   
    ```shell
    npm init
    ```
2. <span data-ttu-id="63160-138">Bij de opdrachtprompt in de **sendcloudtodevicemessage** map, voer de volgende opdracht voor het installeren van de **azure-iothub** pakket:</span><span class="sxs-lookup"><span data-stu-id="63160-138">At your command prompt in the **sendcloudtodevicemessage** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```shell
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="63160-139">Maak met een teksteditor, een **SendCloudToDeviceMessage.js** bestand de **sendcloudtodevicemessage** map.</span><span class="sxs-lookup"><span data-stu-id="63160-139">Using a text editor, create a **SendCloudToDeviceMessage.js** file in the **sendcloudtodevicemessage** folder.</span></span>
4. <span data-ttu-id="63160-140">Voeg de volgende `require` instructies aan het begin van de **SendCloudToDeviceMessage.js** bestand:</span><span class="sxs-lookup"><span data-stu-id="63160-140">Add the following `require` statements at the start of the **SendCloudToDeviceMessage.js** file:</span></span>
   
    ```javascript
    'use strict';
   
    var Client = require('azure-iothub').Client;
    var Message = require('azure-iot-common').Message;
    ```
5. <span data-ttu-id="63160-141">Voeg de volgende code naar **SendCloudToDeviceMessage.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="63160-141">Add the following code to **SendCloudToDeviceMessage.js** file.</span></span> <span data-ttu-id="63160-142">Vervang de waarde van de tijdelijke aanduiding '{iot hub verbindingsreeks}' door de IoT Hub-verbindingsreeks voor de hub die u hebt gemaakt in de [aan de slag met IoT Hub] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="63160-142">Replace the "{iot hub connection string}" placeholder value with the IoT Hub connection string for the hub you created in the [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="63160-143">Vervang de tijdelijke aanduiding voor de '{apparaat-id}' met de apparaat-ID van het apparaat dat u hebt toegevoegd in de [aan de slag met IoT Hub] zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="63160-143">Replace the "{device id}" placeholder with the device ID of the device you added in the [Get started with IoT Hub] tutorial:</span></span>
   
    ```javascript
    var connectionString = '{iot hub connection string}';
    var targetDevice = '{device id}';
   
    var serviceClient = Client.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="63160-144">Voeg de volgende functie om de Bewerkingsresultaten aan de console afdrukken:</span><span class="sxs-lookup"><span data-stu-id="63160-144">Add the following function to print operation results to the console:</span></span>
   
    ```javascript
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="63160-145">Voeg de volgende functie levering Feedbackberichten naar de console afdrukken:</span><span class="sxs-lookup"><span data-stu-id="63160-145">Add the following function to print delivery feedback messages to the console:</span></span>
   
    ```javascript
    function receiveFeedback(err, receiver){
      receiver.on('message', function (msg) {
        console.log('Feedback message:')
        console.log(msg.getData().toString('utf-8'));
      });
    }
    ```
8. <span data-ttu-id="63160-146">Voeg de volgende code voor het verzenden van een bericht naar uw apparaat en verwerken van het Feedbackbericht wanneer het apparaat het cloud-naar-apparaat-bericht erkent:</span><span class="sxs-lookup"><span data-stu-id="63160-146">Add the following code to send a message to your device and handle the feedback message when the device acknowledges the cloud-to-device message:</span></span>
   
    ```javascript
    serviceClient.open(function (err) {
      if (err) {
        console.error('Could not connect: ' + err.message);
      } else {
        console.log('Service client connected');
        serviceClient.getFeedbackReceiver(receiveFeedback);
        var message = new Message('Cloud to device message.');
        message.ack = 'full';
        message.messageId = "My Message ID";
        console.log('Sending message: ' + message.getData());
        serviceClient.send(targetDevice, message, printResultFor('send'));
      }
    });
    ```
9. <span data-ttu-id="63160-147">Opslaan en sluiten **SendCloudToDeviceMessage.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="63160-147">Save and close **SendCloudToDeviceMessage.js** file.</span></span>

## <a name="run-the-applications"></a><span data-ttu-id="63160-148">De toepassingen uitvoeren</span><span class="sxs-lookup"><span data-stu-id="63160-148">Run the applications</span></span>
<span data-ttu-id="63160-149">U kunt nu de toepassingen gaan uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="63160-149">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="63160-150">Bij de opdrachtprompt in de **simulateddevice** map, voer de volgende opdracht voor het verzenden van telemetrie naar IoT Hub en om te luisteren naar de cloud-naar-apparaat-berichten:</span><span class="sxs-lookup"><span data-stu-id="63160-150">At the command prompt in the **simulateddevice** folder, run the following command to send telemetry to IoT Hub and to listen for cloud-to-device messages:</span></span>
   
    ```shell
    node SimulatedDevice.js 
    ```
   
    ![De gesimuleerde apparaattoepassing uitvoeren][img-simulated-device]
2. <span data-ttu-id="63160-152">Bij een opdrachtprompt in de **sendcloudtodevicemessage** map de volgende opdracht om een cloud naar apparaat verzenden en wacht tot de bevestiging van feedback:</span><span class="sxs-lookup"><span data-stu-id="63160-152">At a command prompt in the **sendcloudtodevicemessage** folder, run the following command to send a cloud-to-device message and wait for the acknowledgment feedback:</span></span>
   
    ```shell
    node SendCloudToDeviceMessage.js 
    ```
   
    ![Voer de app voor het verzenden van de opdracht cloud-naar-apparaat][img-send-command]
   
   > [!NOTE]
   > <span data-ttu-id="63160-154">Deze zelfstudie implementeert voor de eenvoud mogelijk te houden, niet een beleid voor opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="63160-154">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="63160-155">In productiecode moet u beleid voor opnieuw proberen (zoals exponentieel uitstel), zoals voorgesteld in het MSDN-artikel implementeren [afhandeling van tijdelijke fout].</span><span class="sxs-lookup"><span data-stu-id="63160-155">In production code, you should implement retry policies (such as exponential backoff), as suggested in the MSDN article [Transient Fault Handling].</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="63160-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="63160-156">Next steps</span></span>
<span data-ttu-id="63160-157">In deze zelfstudie hebt u geleerd hoe cloud-naar-apparaat-berichten verzenden en ontvangen.</span><span class="sxs-lookup"><span data-stu-id="63160-157">In this tutorial, you learned how to send and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="63160-158">Zie voor voorbeelden van volledige end-to-end-oplossingen die gebruikmaken van IoT Hub [Azure IoT Suite].</span><span class="sxs-lookup"><span data-stu-id="63160-158">To see examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="63160-159">Zie voor meer informatie over het ontwikkelen van oplossingen met IoT Hub, de [Ontwikkelaarshandleiding voor IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="63160-159">To learn more about developing solutions with IoT Hub, see the [IoT Hub developer guide].</span></span>

<!-- Images -->
[img-simulated-device]: media/iot-hub-node-node-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-node-node-c2d/sendc2d.png

<!-- Links -->

<span data-ttu-id="63160-160">[aan de slag met IoT Hub]: iot-hub-node-node-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="63160-160">[Get started with IoT Hub]: iot-hub-node-node-getstarted.md</span></span>
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
<span data-ttu-id="63160-161">[Ontwikkelaarshandleiding voor IoT Hub]: iot-hub-devguide.md</span><span class="sxs-lookup"><span data-stu-id="63160-161">[IoT Hub developer guide]: iot-hub-devguide.md</span></span>
<span data-ttu-id="63160-162">[Azure IoT Developer Center]: http://www.azure.com/develop/iot</span><span class="sxs-lookup"><span data-stu-id="63160-162">[Azure IoT Developer Center]: http://www.azure.com/develop/iot</span></span>
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
<span data-ttu-id="63160-163">[afhandeling van tijdelijke fout]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span><span class="sxs-lookup"><span data-stu-id="63160-163">[Transient Fault Handling]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx</span></span>
<span data-ttu-id="63160-164">[Azure-portal]: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="63160-164">[Azure portal]: https://portal.azure.com</span></span>
<span data-ttu-id="63160-165">[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/</span><span class="sxs-lookup"><span data-stu-id="63160-165">[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/</span></span>
