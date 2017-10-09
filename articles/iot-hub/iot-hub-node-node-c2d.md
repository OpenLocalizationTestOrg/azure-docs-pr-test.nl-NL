---
title: aaaCloud-naar-apparaat-berichten met Azure IoT Hub (knooppunt) | Microsoft Docs
description: Hoe berichten toosend cloud-naar-apparaat tooa apparaat van een Azure IoT hub met hello Azure IoT SDK's voor Node.js. U wijzigt de berichten van een gesimuleerd apparaat app tooreceive cloud-naar-apparaat en wijzigen van een back-endserver voor apps toosend hello cloud-naar-apparaat-berichten.
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
ms.openlocfilehash: 1ccae0cada52193c2abb91504c086cac226e93da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-with-iot-hub-node"></a><span data-ttu-id="7f4e3-104">Cloud-naar-apparaat-berichten verzenden met IoT Hub (knooppunt)</span><span class="sxs-lookup"><span data-stu-id="7f4e3-104">Send cloud-to-device messages with IoT Hub (Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d](../../includes/iot-hub-selector-c2d.md)]

## <a name="introduction"></a><span data-ttu-id="7f4e3-105">Inleiding</span><span class="sxs-lookup"><span data-stu-id="7f4e3-105">Introduction</span></span>
<span data-ttu-id="7f4e3-106">Azure IoT Hub is een volledig beheerde service waarmee stabiele en veilige tweerichtingscommunicatie tussen miljoenen apparaten inschakelen en een back-end oplossing.</span><span class="sxs-lookup"><span data-stu-id="7f4e3-106">Azure IoT Hub is a fully managed service that helps enable reliable and secure bi-directional communications between millions of devices and a solution back end.</span></span> <span data-ttu-id="7f4e3-107">Hallo [aan de slag met IoT Hub] zelfstudie laat zien hoe toocreate een IoT-hub een apparaat-id in het inrichten en code van een gesimuleerde apparaattoepassing dat apparaat-naar-cloud-berichten verzendt.</span><span class="sxs-lookup"><span data-stu-id="7f4e3-107">hello [Get started with IoT Hub] tutorial shows how toocreate an IoT hub, provision a device identity in it, and code a simulated device app that sends device-to-cloud messages.</span></span>

<span data-ttu-id="7f4e3-108">Deze zelfstudie bouwt voort op [aan de slag met IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="7f4e3-108">This tutorial builds on [Get started with IoT Hub].</span></span> <span data-ttu-id="7f4e3-109">Hier ziet u hoe aan:</span><span class="sxs-lookup"><span data-stu-id="7f4e3-109">It shows you how to:</span></span>

* <span data-ttu-id="7f4e3-110">Verzenden van uw back-end oplossing, cloud-naar-apparaatberichten tooa één apparaat via IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7f4e3-110">From your solution back end, send cloud-to-device messages tooa single device through IoT Hub.</span></span>
* <span data-ttu-id="7f4e3-111">Cloud-naar-apparaat-berichten op een apparaat ontvangen.</span><span class="sxs-lookup"><span data-stu-id="7f4e3-111">Receive cloud-to-device messages on a device.</span></span>
* <span data-ttu-id="7f4e3-112">Aanvragen van uw back-end oplossing, levering bevestiging (*feedback*) voor tooa apparaat van de berichten uit IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="7f4e3-112">From your solution back end, request delivery acknowledgement (*feedback*) for messages sent tooa device from IoT Hub.</span></span>

<span data-ttu-id="7f4e3-113">U vindt meer informatie over cloud-naar-apparaat-berichten in Hallo [Ontwikkelaarshandleiding voor IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="7f4e3-113">You can find more information on cloud-to-device messages in hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>

<span data-ttu-id="7f4e3-114">Aan het einde van de Hallo van deze zelfstudie, moet u twee console Node.js-apps uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="7f4e3-114">At hello end of this tutorial, you run two Node.js console apps:</span></span>

* <span data-ttu-id="7f4e3-115">**SimulatedDevice**, een aangepaste versie van het Hallo-app gemaakt in [aan de slag met IoT Hub], die verbinding maakt tooyour IoT-hub en cloud-naar-apparaat-berichten worden ontvangen.</span><span class="sxs-lookup"><span data-stu-id="7f4e3-115">**SimulatedDevice**, a modified version of hello app created in [Get started with IoT Hub], which connects tooyour IoT hub and receives cloud-to-device messages.</span></span>
* <span data-ttu-id="7f4e3-116">**SendCloudToDeviceMessage**, die een cloud-naar-apparaat bericht toohello gesimuleerde apparaattoepassing via IoT Hub verzendt en ontvangt u vervolgens de bevestiging levering.</span><span class="sxs-lookup"><span data-stu-id="7f4e3-116">**SendCloudToDeviceMessage**, which sends a cloud-to-device message toohello simulated device app through IoT Hub, and then receives its delivery acknowledgement.</span></span>

> [!NOTE]
> <span data-ttu-id="7f4e3-117">IoT-Hub heeft SDK-ondersteuning voor veel apparaatplatforms en talen (inclusief C, Java en Javascript) via Azure IoT-apparaat-SDK's.</span><span class="sxs-lookup"><span data-stu-id="7f4e3-117">IoT Hub has SDK support for many device platforms and languages (including C, Java, and Javascript) through Azure IoT device SDKs.</span></span> <span data-ttu-id="7f4e3-118">Voor stapsgewijze instructies voor hoe tooconnect uw apparaat toothis-zelfstudie code en over het algemeen tooAzure IoT Hub zien Hallo [Azure IoT Developer Center].</span><span class="sxs-lookup"><span data-stu-id="7f4e3-118">For step-by-step instructions on how tooconnect your device toothis tutorial's code, and generally tooAzure IoT Hub, see hello [Azure IoT Developer Center].</span></span>
> 
> 

<span data-ttu-id="7f4e3-119">toocomplete in deze zelfstudie, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="7f4e3-119">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="7f4e3-120">Node.js versie 0.10.x of hoger.</span><span class="sxs-lookup"><span data-stu-id="7f4e3-120">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="7f4e3-121">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="7f4e3-121">An active Azure account.</span></span> <span data-ttu-id="7f4e3-122">(Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)</span><span class="sxs-lookup"><span data-stu-id="7f4e3-122">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

## <a name="receive-messages-in-hello-simulated-device-app"></a><span data-ttu-id="7f4e3-123">Berichten ontvangen in de gesimuleerde apparaattoepassing Hallo</span><span class="sxs-lookup"><span data-stu-id="7f4e3-123">Receive messages in hello simulated device app</span></span>
<span data-ttu-id="7f4e3-124">In deze sectie maakt u de gesimuleerde apparaattoepassing Hallo u hebt gemaakt in wijzigen [aan de slag met IoT Hub] tooreceive cloud-naar-apparaat-berichten uit Hallo iothub.</span><span class="sxs-lookup"><span data-stu-id="7f4e3-124">In this section, you modify hello simulated device app you created in [Get started with IoT Hub] tooreceive cloud-to-device messages from hello IoT hub.</span></span>

1. <span data-ttu-id="7f4e3-125">Met een teksteditor Hallo SimulatedDevice.js bestand openen.</span><span class="sxs-lookup"><span data-stu-id="7f4e3-125">Using a text editor, open hello SimulatedDevice.js file.</span></span>
2. <span data-ttu-id="7f4e3-126">Hallo wijzigen **connectCallback** toohandle berichten uit IoT Hub werken.</span><span class="sxs-lookup"><span data-stu-id="7f4e3-126">Modify hello **connectCallback** function toohandle messages sent from IoT Hub.</span></span> <span data-ttu-id="7f4e3-127">In dit voorbeeld roept Hallo apparaat altijd Hallo **voltooid** werken toonotify IoT Hub dat deze het Hallo-bericht is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="7f4e3-127">In this example, hello device always invokes hello **complete** function toonotify IoT Hub that it has processed hello message.</span></span> <span data-ttu-id="7f4e3-128">De nieuwe versie van Hallo **connectCallback** functie eruit Hallo codefragment te volgen:</span><span class="sxs-lookup"><span data-stu-id="7f4e3-128">Your new version of hello **connectCallback** function looks like hello following snippet:</span></span>
   
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
        // Create a message and send it toohello IoT Hub every second
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
   > <span data-ttu-id="7f4e3-129">Als u HTTP in plaats van MQTT of AMQP als Hallo transport gebruikt, Hallo **DeviceClient** exemplaar wordt gecontroleerd op berichten uit IoT Hub zelden (minder dan elke 25 minuten).</span><span class="sxs-lookup"><span data-stu-id="7f4e3-129">If you use HTTP instead of MQTT or AMQP as hello transport, hello **DeviceClient** instance checks for messages from IoT Hub infrequently (less than every 25 minutes).</span></span> <span data-ttu-id="7f4e3-130">Zie voor meer informatie over Hallo verschillen tussen de protocollen MQTT, AMQP en HTTP-ondersteuning en Iothub beperking Hallo [Ontwikkelaarshandleiding voor IoT Hub][IoT Hub developer guide - C2D].</span><span class="sxs-lookup"><span data-stu-id="7f4e3-130">For more information about hello differences between MQTT, AMQP and HTTP support, and IoT Hub throttling, see hello [IoT Hub developer guide][IoT Hub developer guide - C2D].</span></span>
   > 
   > 

## <a name="send-a-cloud-to-device-message"></a><span data-ttu-id="7f4e3-131">Een cloud naar apparaat verzenden</span><span class="sxs-lookup"><span data-stu-id="7f4e3-131">Send a cloud-to-device message</span></span>
<span data-ttu-id="7f4e3-132">In deze sectie maakt maken u een Node.js-consoletoepassing die cloud-naar-apparaatberichten toohello gesimuleerde apparaattoepassing verzendt.</span><span class="sxs-lookup"><span data-stu-id="7f4e3-132">In this section, you create a Node.js console app that sends cloud-to-device messages toohello simulated device app.</span></span> <span data-ttu-id="7f4e3-133">U moet de apparaat-ID van het Hallo-apparaat die u hebt toegevoegd in Hallo Hallo [aan de slag met IoT Hub] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="7f4e3-133">You need hello device ID of hello device you added in hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="7f4e3-134">U moet de verbindingsreeks IoT Hub ook Hallo voor uw hub die u in Hallo vinden kunt [Azure-portal].</span><span class="sxs-lookup"><span data-stu-id="7f4e3-134">You also need hello IoT Hub connection string for your hub that you can find in hello [Azure portal].</span></span>

1. <span data-ttu-id="7f4e3-135">Maak een lege map genaamd **sendcloudtodevicemessage**.</span><span class="sxs-lookup"><span data-stu-id="7f4e3-135">Create an empty folder called **sendcloudtodevicemessage**.</span></span> <span data-ttu-id="7f4e3-136">In Hallo **sendcloudtodevicemessage** map, een package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="7f4e3-136">In hello **sendcloudtodevicemessage** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="7f4e3-137">Accepteer alle Hallo standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="7f4e3-137">Accept all hello defaults:</span></span>
   
    ```shell
    npm init
    ```
2. <span data-ttu-id="7f4e3-138">Bij de opdrachtprompt in Hallo **sendcloudtodevicemessage** map na de opdracht tooinstall Hallo Hallo **azure-iothub** pakket:</span><span class="sxs-lookup"><span data-stu-id="7f4e3-138">At your command prompt in hello **sendcloudtodevicemessage** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```shell
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="7f4e3-139">Maak met een teksteditor, een **SendCloudToDeviceMessage.js** bestand in Hallo **sendcloudtodevicemessage** map.</span><span class="sxs-lookup"><span data-stu-id="7f4e3-139">Using a text editor, create a **SendCloudToDeviceMessage.js** file in hello **sendcloudtodevicemessage** folder.</span></span>
4. <span data-ttu-id="7f4e3-140">Voeg de volgende Hallo `require` instructies aan Hallo start Hallo **SendCloudToDeviceMessage.js** bestand:</span><span class="sxs-lookup"><span data-stu-id="7f4e3-140">Add hello following `require` statements at hello start of hello **SendCloudToDeviceMessage.js** file:</span></span>
   
    ```javascript
    'use strict';
   
    var Client = require('azure-iothub').Client;
    var Message = require('azure-iot-common').Message;
    ```
5. <span data-ttu-id="7f4e3-141">Hallo code te volgen toevoegen**SendCloudToDeviceMessage.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="7f4e3-141">Add hello following code too**SendCloudToDeviceMessage.js** file.</span></span> <span data-ttu-id="7f4e3-142">Vervang '{iot hub verbindingsreeks}' Hallo tijdelijke aanduidingswaarde met IoT Hub-verbindingsreeks voor Hallo-hub die u hebt gemaakt in Hallo Hallo [aan de slag met IoT Hub] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="7f4e3-142">Replace hello "{iot hub connection string}" placeholder value with hello IoT Hub connection string for hello hub you created in hello [Get started with IoT Hub] tutorial.</span></span> <span data-ttu-id="7f4e3-143">Hallo '{apparaat-id}'-tijdelijke aanduiding vervangen door de apparaat-ID Hallo Hallo apparaat dat u hebt toegevoegd in Hallo [aan de slag met IoT Hub] zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="7f4e3-143">Replace hello "{device id}" placeholder with hello device ID of hello device you added in hello [Get started with IoT Hub] tutorial:</span></span>
   
    ```javascript
    var connectionString = '{iot hub connection string}';
    var targetDevice = '{device id}';
   
    var serviceClient = Client.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="7f4e3-144">Hallo functie tooprint bewerking resultaten toohello console volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="7f4e3-144">Add hello following function tooprint operation results toohello console:</span></span>
   
    ```javascript
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="7f4e3-145">Hallo functie tooprint levering feedback berichten toohello console volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="7f4e3-145">Add hello following function tooprint delivery feedback messages toohello console:</span></span>
   
    ```javascript
    function receiveFeedback(err, receiver){
      receiver.on('message', function (msg) {
        console.log('Feedback message:')
        console.log(msg.getData().toString('utf-8'));
      });
    }
    ```
8. <span data-ttu-id="7f4e3-146">Hallo volgende toosend een bericht tooyour apparaat code en feedback het Hallo-bericht verwerken wanneer Hallo apparaat cloud-naar-apparaat het Hallo-bericht erkent toevoegen:</span><span class="sxs-lookup"><span data-stu-id="7f4e3-146">Add hello following code toosend a message tooyour device and handle hello feedback message when hello device acknowledges hello cloud-to-device message:</span></span>
   
    ```javascript
    serviceClient.open(function (err) {
      if (err) {
        console.error('Could not connect: ' + err.message);
      } else {
        console.log('Service client connected');
        serviceClient.getFeedbackReceiver(receiveFeedback);
        var message = new Message('Cloud toodevice message.');
        message.ack = 'full';
        message.messageId = "My Message ID";
        console.log('Sending message: ' + message.getData());
        serviceClient.send(targetDevice, message, printResultFor('send'));
      }
    });
    ```
9. <span data-ttu-id="7f4e3-147">Opslaan en sluiten **SendCloudToDeviceMessage.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="7f4e3-147">Save and close **SendCloudToDeviceMessage.js** file.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="7f4e3-148">Hallo-toepassingen uitvoeren</span><span class="sxs-lookup"><span data-stu-id="7f4e3-148">Run hello applications</span></span>
<span data-ttu-id="7f4e3-149">U bent nu klaar toorun Hallo toepassingen.</span><span class="sxs-lookup"><span data-stu-id="7f4e3-149">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="7f4e3-150">Bij de opdrachtprompt Hallo in Hallo **simulateddevice** map, voert u de volgende Hallo opdracht toosend telemetrie tooIoT Hub en toolisten voor cloud-naar-apparaat-berichten:</span><span class="sxs-lookup"><span data-stu-id="7f4e3-150">At hello command prompt in hello **simulateddevice** folder, run hello following command toosend telemetry tooIoT Hub and toolisten for cloud-to-device messages:</span></span>
   
    ```shell
    node SimulatedDevice.js 
    ```
   
    ![De gesimuleerde apparaattoepassing Hallo uitvoeren][img-simulated-device]
2. <span data-ttu-id="7f4e3-152">Bij een opdrachtprompt in Hallo **sendcloudtodevicemessage** map uitvoeren Hallo opdracht toosend na een cloud-naar-apparaat-bericht en wachten op Hallo bevestiging feedback:</span><span class="sxs-lookup"><span data-stu-id="7f4e3-152">At a command prompt in hello **sendcloudtodevicemessage** folder, run hello following command toosend a cloud-to-device message and wait for hello acknowledgment feedback:</span></span>
   
    ```shell
    node SendCloudToDeviceMessage.js 
    ```
   
    ![Hallo app toosend Hallo cloud-naar-apparaat opdracht uitvoeren][img-send-command]
   
   > [!NOTE]
   > <span data-ttu-id="7f4e3-154">Deze zelfstudie implementeert voor de eenvoud mogelijk te houden, niet een beleid voor opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="7f4e3-154">For simplicity's sake, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="7f4e3-155">In productiecode moet u beleid voor opnieuw proberen (zoals exponentieel uitstel), zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout].</span><span class="sxs-lookup"><span data-stu-id="7f4e3-155">In production code, you should implement retry policies (such as exponential backoff), as suggested in hello MSDN article [Transient Fault Handling].</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="7f4e3-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7f4e3-156">Next steps</span></span>
<span data-ttu-id="7f4e3-157">In deze zelfstudie hebt u geleerd hoe toosend en cloud-naar-apparaat-berichten ontvangen.</span><span class="sxs-lookup"><span data-stu-id="7f4e3-157">In this tutorial, you learned how toosend and receive cloud-to-device messages.</span></span> 

<span data-ttu-id="7f4e3-158">Voorbeelden van volledige end-to-end-oplossingen die gebruikmaken van IoT Hub toosee Zie [Azure IoT Suite].</span><span class="sxs-lookup"><span data-stu-id="7f4e3-158">toosee examples of complete end-to-end solutions that use IoT Hub, see [Azure IoT Suite].</span></span>

<span data-ttu-id="7f4e3-159">toolearn meer informatie over het ontwikkelen van oplossingen met IoT Hub, Zie Hallo [Ontwikkelaarshandleiding voor IoT Hub].</span><span class="sxs-lookup"><span data-stu-id="7f4e3-159">toolearn more about developing solutions with IoT Hub, see hello [IoT Hub developer guide].</span></span>

<!-- Images -->
[img-simulated-device]: media/iot-hub-node-node-c2d/receivec2d.png
[img-send-command]:  media/iot-hub-node-node-c2d/sendc2d.png

<!-- Links -->

[aan de slag met IoT Hub]: iot-hub-node-node-getstarted.md
[IoT Hub developer guide - C2D]: iot-hub-devguide-messaging.md
[Ontwikkelaarshandleiding voor IoT Hub]: iot-hub-devguide.md
[Azure IoT Developer Center]: http://www.azure.com/develop/iot
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[afhandeling van tijdelijke fout]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[Azure-portal]: https://portal.azure.com
[Azure IoT Suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
