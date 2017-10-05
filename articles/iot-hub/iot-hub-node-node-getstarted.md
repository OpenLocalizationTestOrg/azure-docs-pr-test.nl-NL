---
title: Aan de slag met Azure IoT Hub (Node) | Microsoft Docs
description: Informatie over het verzenden van apparaat-naar-cloud-berichten naar Azure IoT Hub met behulp van IoT SDK's voor Node.js. U maakt gesimuleerde apparaat- en service-apps om uw apparaat te registreren, berichten te verzenden en berichten uit IoT Hub te lezen.
services: iot-hub
documentationcenter: nodejs
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 56618522-9a31-42c6-94bf-55e2233b39ac
ms.service: iot-hub
ms.devlang: javascript
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/22/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b27a34c0f1f127628912ad68a002e15cc838b4d0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="connect-your-simulated-device-to-your-iot-hub-using-node"></a><span data-ttu-id="b3106-104">Uw gesimuleerde apparaat verbinding laten maken met uw IoT Hub met Node</span><span class="sxs-lookup"><span data-stu-id="b3106-104">Connect your simulated device to your IoT hub using Node</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="b3106-105">Nadat u deze zelfstudie volledig hebt doorlopen, beschikt u over drie Node.js-consoletoepassingen:</span><span class="sxs-lookup"><span data-stu-id="b3106-105">At the end of this tutorial, you have three Node.js console apps:</span></span>

* <span data-ttu-id="b3106-106">**CreateDeviceIdentity.js**: deze toepassing maakt een apparaat-id en de bijbehorende beveiligingssleutel waarmee uw gesimuleerde apparaat-app verbonden kan worden.</span><span class="sxs-lookup"><span data-stu-id="b3106-106">**CreateDeviceIdentity.js**, which creates a device identity and associated security key to connect your simulated device app.</span></span>
* <span data-ttu-id="b3106-107">**ReadDeviceToCloudMessages.js**: deze toepassing geeft de telemetrie weer die is verzonden door uw gesimuleerde apparaat-app.</span><span class="sxs-lookup"><span data-stu-id="b3106-107">**ReadDeviceToCloudMessages.js**, which displays the telemetry sent by your simulated device app.</span></span>
* <span data-ttu-id="b3106-108">**SimulatedDevice.js**: deze toepassing koppelt uw IoT-hub aan de apparaat-id die u eerder hebt gemaakt en verzendt iedere seconde een telemetriebericht via het MQTT-protocol.</span><span class="sxs-lookup"><span data-stu-id="b3106-108">**SimulatedDevice.js**, which connects to your IoT hub with the device identity created earlier, and sends a telemetry message every second using the MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="b3106-109">Het artikel [Azure IoT-SDK's][lnk-hub-sdks] bevat informatie over de verschillende Azure IoT-SDK's die u kunt gebruiken om beide toepassingen zo te maken dat ze zowel op het apparaat als op de back-end van uw oplossing kunnen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b3106-109">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="b3106-110">Voor het voltooien van deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="b3106-110">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="b3106-111">Node.js versie 0.10.x of hoger.</span><span class="sxs-lookup"><span data-stu-id="b3106-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="b3106-112">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="b3106-112">An active Azure account.</span></span> <span data-ttu-id="b3106-113">(Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)</span><span class="sxs-lookup"><span data-stu-id="b3106-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="b3106-114">U hebt nu uw IoT-hub gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b3106-114">You have now created your IoT hub.</span></span> <span data-ttu-id="b3106-115">U hebt de IoT Hub-hostnaam en -verbindingsreeks die u nodig hebt voor de rest van deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="b3106-115">You have the IoT Hub host name and the IoT Hub connection string that you need to complete the rest of this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="b3106-116">Een apparaat-id maken</span><span class="sxs-lookup"><span data-stu-id="b3106-116">Create a device identity</span></span>
<span data-ttu-id="b3106-117">In dit gedeelte gaat u een Node.js-consoletoepassing maken die een apparaat-id maakt in het identiteitenregister van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="b3106-117">In this section, you create a Node.js console app that creates a device identity in the identity registry in your IoT hub.</span></span> <span data-ttu-id="b3106-118">Een apparaat kan alleen verbinding maken met de IoT Hub als het vermeld staat in het id-register.</span><span class="sxs-lookup"><span data-stu-id="b3106-118">A device can only connect to IoT hub if it has an entry in the identity registry.</span></span> <span data-ttu-id="b3106-119">Zie het gedeelte **Id-register** in de [ontwikkelaarshandleiding voor IoT Hub][lnk-devguide-identity] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b3106-119">For more information, see the **Identity Registry** section of the [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="b3106-120">Wanneer u deze consoletoepassing uitvoert, worden er een unieke apparaat-id en sleutel gegenereerd waarmee uw apparaat zichzelf kan identificeren tijdens het verzenden van apparaat-naar-cloud-berichten naar IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b3106-120">When you run this console app, it generates a unique device ID and key that your device can use to identify itself when it sends device-to-cloud messages to IoT Hub.</span></span>

1. <span data-ttu-id="b3106-121">Maak een nieuwe lege map met de naam **createdeviceidentity**.</span><span class="sxs-lookup"><span data-stu-id="b3106-121">Create a new empty folder called **createdeviceidentity**.</span></span> <span data-ttu-id="b3106-122">In de map **createdeviceidentity** maakt u een package.json-bestand door in het opdrachtprompt de volgende opdracht te geven.</span><span class="sxs-lookup"><span data-stu-id="b3106-122">In the **createdeviceidentity** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="b3106-123">Accepteer alle standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="b3106-123">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="b3106-124">In het opdrachtprompt in de map **createdeviceidentity** voert u de volgende opdracht uit om het **azure-iothub** Service SDK-pakket te installeren:</span><span class="sxs-lookup"><span data-stu-id="b3106-124">At your command prompt in the **createdeviceidentity** folder, run the following command to install the **azure-iothub** Service SDK package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="b3106-125">Maak met een tekstverwerker een **CreateDeviceIdentity.js**-bestand in de map **createdeviceidentity**.</span><span class="sxs-lookup"><span data-stu-id="b3106-125">Using a text editor, create a **CreateDeviceIdentity.js** file in the **createdeviceidentity** folder.</span></span>
4. <span data-ttu-id="b3106-126">Voeg de volgende `require` instructie toe aan het begin van het bestand **CreateDeviceIdentity.js**-bestand:</span><span class="sxs-lookup"><span data-stu-id="b3106-126">Add the following `require` statement at the start of the **CreateDeviceIdentity.js** file:</span></span>
   
    ```
    'use strict';
   
    var iothub = require('azure-iothub');
    ```
5. <span data-ttu-id="b3106-127">Voeg de volgende code toe aan het bestand **CreateDeviceIdentity.js** en vervang de waarde van de tijdelijke aanduiding door de IoT Hub-verbindingsreeks voor de hub die u in de vorige sectie hebt gemaakt:</span><span class="sxs-lookup"><span data-stu-id="b3106-127">Add the following code to the **CreateDeviceIdentity.js** file and replace the placeholder value with the IoT Hub connection string for the hub you created in the previous section:</span></span> 
   
    ```
    var connectionString = '{iothub connection string}';
   
    var registry = iothub.Registry.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="b3106-128">Voeg de volgende code toe om een apparaatdefinitie te maken in het id-register van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="b3106-128">Add the following code to create a device definition in the identity registry in your IoT hub.</span></span> <span data-ttu-id="b3106-129">Met deze code wordt een apparaat gemaakt als de apparaat-id nog niet voorkomt in het id-register. Anders wordt de sleutel van het bestaande apparaat geretourneerd:</span><span class="sxs-lookup"><span data-stu-id="b3106-129">This code creates a device if the device ID does not exist in the identity registry, otherwise it returns the key of the existing device:</span></span>
   
    ```
    var device = {
      deviceId: 'myFirstNodeDevice'
    }
    registry.create(device, function(err, deviceInfo, res) {
      if (err) {
        registry.get(device.deviceId, printDeviceInfo);
      }
      if (deviceInfo) {
        printDeviceInfo(err, deviceInfo, res)
      }
    });
   
    function printDeviceInfo(err, deviceInfo, res) {
      if (deviceInfo) {
        console.log('Device ID: ' + deviceInfo.deviceId);
        console.log('Device key: ' + deviceInfo.authentication.symmetricKey.primaryKey);
      }
    }
    ```
   [!INCLUDE [iot-hub-pii-note-naming-device](../../includes/iot-hub-pii-note-naming-device.md)]

7. <span data-ttu-id="b3106-130">Sla het bestand **CreateDeviceIdentity.js** op en sluit het.</span><span class="sxs-lookup"><span data-stu-id="b3106-130">Save and close **CreateDeviceIdentity.js** file.</span></span>
8. <span data-ttu-id="b3106-131">Als u de toepassing **createdeviceidentity** wilt uitvoeren, geeft u de volgende opdracht op in het opdrachtprompt in de map createdeviceidentity:</span><span class="sxs-lookup"><span data-stu-id="b3106-131">To run the **createdeviceidentity** application, execute the following command at the command prompt in the createdeviceidentity folder:</span></span>
   
    ```
    node CreateDeviceIdentity.js 
    ```
9. <span data-ttu-id="b3106-132">Noteer de **apparaat-id** en de **apparaatsleutel**.</span><span class="sxs-lookup"><span data-stu-id="b3106-132">Make a note of the **Device ID** and **Device key**.</span></span> <span data-ttu-id="b3106-133">U hebt deze waarden later nodig wanneer u een toepassing maakt die verbinding maakt met IoT Hub als apparaat.</span><span class="sxs-lookup"><span data-stu-id="b3106-133">You need these values later when you create an application that connects to IoT Hub as a device.</span></span>

> [!NOTE]
> <span data-ttu-id="b3106-134">In het id-register van IoT Hub worden alleen apparaat-id's opgeslagen waarmee veilig toegang tot de IoT-hub kan worden verkregen.</span><span class="sxs-lookup"><span data-stu-id="b3106-134">The IoT Hub identity registry only stores device identities to enable secure access to the IoT hub.</span></span> <span data-ttu-id="b3106-135">De apparaat-id’s en sleutels worden opgeslagen en gebruikt als beveiligingsreferenties. Met de vlag voor ingeschakeld/uitgeschakeld kunt u toegang tot een afzonderlijk apparaat uitschakelen.</span><span class="sxs-lookup"><span data-stu-id="b3106-135">It stores device IDs and keys to use as security credentials and an enabled/disabled flag that you can use to disable access for an individual device.</span></span> <span data-ttu-id="b3106-136">Als uw toepassing andere apparaatspecifieke metagegevens moet opslaan, moet deze een toepassingsspecifieke opslagmethode gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b3106-136">If your application needs to store other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="b3106-137">Zie de [ontwikkelaarshandleiding voor IoT Hub][lnk-devguide-identity] voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b3106-137">For more information, see the [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

<a id="D2C_node"></a>
## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="b3106-138">Apparaat-naar-cloud-berichten ontvangen</span><span class="sxs-lookup"><span data-stu-id="b3106-138">Receive device-to-cloud messages</span></span>
<span data-ttu-id="b3106-139">In dit gedeelte maakt u een Node.js-consoletoepassing die apparaat-naar-cloud-berichten uit IoT Hub leest.</span><span class="sxs-lookup"><span data-stu-id="b3106-139">In this section, you create a Node.js console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="b3106-140">Een IoT-hub toont een [Event Hub][lnk-event-hubs-overview]-compatibel eindpunt waarmee u apparaat-naar-cloud-berichten kunt lezen.</span><span class="sxs-lookup"><span data-stu-id="b3106-140">An IoT hub exposes an [Event Hubs][lnk-event-hubs-overview]-compatible endpoint to enable you to read device-to-cloud messages.</span></span> <span data-ttu-id="b3106-141">Om de zaken niet nodeloos ingewikkeld te maken, maakt u met deze handleiding een basislezer die niet geschikt is voor hoge doorvoersnelheden.</span><span class="sxs-lookup"><span data-stu-id="b3106-141">To keep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="b3106-142">In de handleiding [Apparaat-naar-cloud-berichten verwerken][lnk-process-d2c-tutorial] leert u hoe u op grote schaal apparaat-naar-cloud-berichten kunt verwerken.</span><span class="sxs-lookup"><span data-stu-id="b3106-142">The [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how to process device-to-cloud messages at scale.</span></span> <span data-ttu-id="b3106-143">In de handleiding [Aan de slag met Event Hubs][lnk-eventhubs-tutorial] leest u meer over het verwerken van berichten van Event Hubs. Deze handleiding is van toepassing op de Event Hub-compatibele eindpunten van IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b3106-143">The [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how to process messages from Event Hubs and is applicable to the IoT Hub Event Hub-compatible endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="b3106-144">Het met Event Hub compatibele eindpunt voor het lezen van apparaat-naar-cloud-berichten maakt altijd gebruik van het AMQP-protocol.</span><span class="sxs-lookup"><span data-stu-id="b3106-144">The Event Hub-compatible endpoint for reading device-to-cloud messages always uses the AMQP protocol.</span></span>
> 
> 

1. <span data-ttu-id="b3106-145">Maak een lege map met de naam **readdevicetocloudmessages**.</span><span class="sxs-lookup"><span data-stu-id="b3106-145">Create an empty folder called **readdevicetocloudmessages**.</span></span> <span data-ttu-id="b3106-146">In de map **readdevicetocloudmessages** maakt u een package.json-bestand door in het opdrachtprompt de volgende opdracht op te geven.</span><span class="sxs-lookup"><span data-stu-id="b3106-146">In the **readdevicetocloudmessages** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="b3106-147">Accepteer alle standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="b3106-147">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="b3106-148">Voer in het opdrachtprompt in de map **readdevicetocloudmessages** de volgende opdracht uit om het pakket **azure-event-hubs** te installeren:</span><span class="sxs-lookup"><span data-stu-id="b3106-148">At your command prompt in the **readdevicetocloudmessages** folder, run the following command to install the **azure-event-hubs** package:</span></span>
   
    ```
    npm install azure-event-hubs --save
    ```
3. <span data-ttu-id="b3106-149">Maak met een tekstverwerker een bestand **ReadDeviceToCloudMessages.js** in de map **readdevicetocloudmessages**.</span><span class="sxs-lookup"><span data-stu-id="b3106-149">Using a text editor, create a **ReadDeviceToCloudMessages.js** file in the **readdevicetocloudmessages** folder.</span></span>
4. <span data-ttu-id="b3106-150">Voeg de volgende `require` instructies toe aan het begin van het bestand **ReadDeviceToCloudMessages.js**:</span><span class="sxs-lookup"><span data-stu-id="b3106-150">Add the following `require` statements at the start of the **ReadDeviceToCloudMessages.js** file:</span></span>
   
    ```
    'use strict';
   
    var EventHubClient = require('azure-event-hubs').Client;
    ```
5. <span data-ttu-id="b3106-151">Voeg de volgende variabeledeclaratie toe en vervang de waarde van de tijdelijke aanduiding door de IoT Hub-verbindingsreeks van uw hub:</span><span class="sxs-lookup"><span data-stu-id="b3106-151">Add the following variable declaration and replace the placeholder value with the IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    ```
6. <span data-ttu-id="b3106-152">Voeg de volgende twee functies toe die de uitvoer naar de console afdrukken:</span><span class="sxs-lookup"><span data-stu-id="b3106-152">Add the following two functions that print output to the console:</span></span>
   
    ```
    var printError = function (err) {
      console.log(err.message);
    };
   
    var printMessage = function (message) {
      console.log('Message received: ');
      console.log(JSON.stringify(message.body));
      console.log('');
    };
    ```
7. <span data-ttu-id="b3106-153">Voeg de volgende code toe om de **EventHubClient** te maken, open de verbinding met uw IoT-Hub en maak voor elke partitie een ontvanger.</span><span class="sxs-lookup"><span data-stu-id="b3106-153">Add the following code to create the **EventHubClient**, open the connection to your IoT Hub, and create a receiver for each partition.</span></span> <span data-ttu-id="b3106-154">Deze toepassing gebruikt een filter bij het maken van een ontvanger, zodat de ontvanger alleen berichten leest die naar IoT Hub worden verzonden wanneer de ontvanger is geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="b3106-154">This application uses a filter when it creates a receiver so that the receiver only reads messages sent to IoT Hub after the receiver starts running.</span></span> <span data-ttu-id="b3106-155">Dit filter is handig in een testomgeving, omdat u zo alleen de huidige reeks berichten ziet.</span><span class="sxs-lookup"><span data-stu-id="b3106-155">This filter is useful in a test environment so you see just the current set of messages.</span></span> <span data-ttu-id="b3106-156">In een productieomgeving moet de code ervoor zorgen dat alle berichten worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="b3106-156">In a production environment, your code should make sure that it processes all the messages.</span></span> <span data-ttu-id="b3106-157">Zie voor meer informatie de zelfstudie [Apparaat-naar-cloud-berichten verwerken][lnk-process-d2c-tutorial]:</span><span class="sxs-lookup"><span data-stu-id="b3106-157">For more information, see the [How to process IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial:</span></span>
   
    ```
    var client = EventHubClient.fromConnectionString(connectionString);
    client.open()
        .then(client.getPartitionIds.bind(client))
        .then(function (partitionIds) {
            return partitionIds.map(function (partitionId) {
                return client.createReceiver('$Default', partitionId, { 'startAfterTime' : Date.now()}).then(function(receiver) {
                    console.log('Created partition receiver: ' + partitionId)
                    receiver.on('errorReceived', printError);
                    receiver.on('message', printMessage);
                });
            });
        })
        .catch(printError);
    ```
8. <span data-ttu-id="b3106-158">Sla het bestand **ReadDeviceToCloudMessages.js** op en sluit het.</span><span class="sxs-lookup"><span data-stu-id="b3106-158">Save and close the **ReadDeviceToCloudMessages.js** file.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="b3106-159">Een gesimuleerde apparaattoepassing maken</span><span class="sxs-lookup"><span data-stu-id="b3106-159">Create a simulated device app</span></span>
<span data-ttu-id="b3106-160">In dit gedeelte maakt u een Node.js-consoletoepassing die een apparaat simuleert dat apparaat-naar-cloud-berichten naar een IoT-hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="b3106-160">In this section, you create a Node.js console app that simulates a device that sends device-to-cloud messages to an IoT hub.</span></span>

1. <span data-ttu-id="b3106-161">Maak een lege map met de naam **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="b3106-161">Create an empty folder called **simulateddevice**.</span></span> <span data-ttu-id="b3106-162">In de map **simulateddevice** maakt u een package.json-bestand door in het opdrachtprompt de volgende opdracht op te geven.</span><span class="sxs-lookup"><span data-stu-id="b3106-162">In the **simulateddevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="b3106-163">Accepteer alle standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="b3106-163">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="b3106-164">In de opdrachtprompt in de map **simulateddevice** voert u de volgende opdracht uit om het **azure-iot-device-amqp** Device SDK-pakket en het **azure-iot-device-mqtt**-pakket te installeren:</span><span class="sxs-lookup"><span data-stu-id="b3106-164">At your command prompt in the **simulateddevice** folder, run the following command to install the **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="b3106-165">Maak met een tekstverwerker een bestand **SimulatedDevice.js** in de map **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="b3106-165">Using a text editor, create a **SimulatedDevice.js** file in the **simulateddevice** folder.</span></span>
4. <span data-ttu-id="b3106-166">Voeg de volgende `require` instructies toe aan het begin van het bestand **SimulatedDevice.js**:</span><span class="sxs-lookup"><span data-stu-id="b3106-166">Add the following `require` statements at the start of the **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var clientFromConnectionString = require('azure-iot-device-mqtt').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    ```
5. <span data-ttu-id="b3106-167">Voeg een **connectionString**-variabele toe en gebruik deze om een **client**exemplaar te maken.</span><span class="sxs-lookup"><span data-stu-id="b3106-167">Add a **connectionString** variable and use it to create a **Client** instance.</span></span> <span data-ttu-id="b3106-168">Vervang **{youriothostname}** door de naam van de IoT-hub die u hebt gemaakt in de sectie *Een IoT-hub maken*.</span><span class="sxs-lookup"><span data-stu-id="b3106-168">Replace **{youriothostname}** with the name of the IoT hub you created the *Create an IoT Hub* section.</span></span> <span data-ttu-id="b3106-169">Vervang **{yourdevicekey}** door de sleutelwaarde die u hebt gegenereerd in de sectie *Een apparaat-id maken*:</span><span class="sxs-lookup"><span data-stu-id="b3106-169">Replace **{yourdevicekey}** with the device key value you generated in the *Create a device identity* section:</span></span>
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myFirstNodeDevice;SharedAccessKey={yourdevicekey}';
   
    var client = clientFromConnectionString(connectionString);
    ```
6. <span data-ttu-id="b3106-170">Voeg de volgende functie toe om uitvoer van de toepassing weer te geven:</span><span class="sxs-lookup"><span data-stu-id="b3106-170">Add the following function to display output from the application:</span></span>
   
    ```
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="b3106-171">Maak een callback en verzend iedere seconde met de functie **setInterval** een bericht naar uw IoT-hub:</span><span class="sxs-lookup"><span data-stu-id="b3106-171">Create a callback and use the **setInterval** function to send a message to your IoT hub every second:</span></span>
   
    ```
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
   
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
8. <span data-ttu-id="b3106-172">Maak verbinding met uw IoT Hub en begin met het verzenden van berichten:</span><span class="sxs-lookup"><span data-stu-id="b3106-172">Open the connection to your IoT Hub and start sending messages:</span></span>
   
    ```
    client.open(connectCallback);
    ```
9. <span data-ttu-id="b3106-173">Sla het bestand **SimulatedDevice.js** op en sluit het.</span><span class="sxs-lookup"><span data-stu-id="b3106-173">Save and close the **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="b3106-174">Om de zaken niet nodeloos ingewikkeld te maken, is in deze handleiding geen beleid voor opnieuw proberen geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="b3106-174">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="b3106-175">Bij de productiecode moet u een beleid voor opnieuw proberen implementeren (zoals exponentieel uitstel), zoals aangegeven in het MSDN-artikel [Transient Fault Handling][lnk-transient-faults] (Afhandeling van tijdelijke fouten).</span><span class="sxs-lookup"><span data-stu-id="b3106-175">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="run-the-apps"></a><span data-ttu-id="b3106-176">De apps uitvoeren</span><span class="sxs-lookup"><span data-stu-id="b3106-176">Run the apps</span></span>
<span data-ttu-id="b3106-177">U kunt nu de apps uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b3106-177">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="b3106-178">Voer in het opdrachtprompt in de map **readdevicetocloudmessages** de volgende opdracht uit om uw IoT Hub te bewaken:</span><span class="sxs-lookup"><span data-stu-id="b3106-178">At a command prompt in the **readdevicetocloudmessages** folder, run the following command to begin monitoring your IoT hub:</span></span>
   
    ```
    node ReadDeviceToCloudMessages.js 
    ```
   
    ![De Node.js-app voor IoT Hub-services voor het bewaken van apparaat-naar-cloud-berichten][7]
2. <span data-ttu-id="b3106-180">Voer in het opdrachtprompt in de map **simulateddevice** de volgende opdracht uit om telemetriegegevens naar uw IoT Hub te verzenden:</span><span class="sxs-lookup"><span data-stu-id="b3106-180">At a command prompt in the **simulateddevice** folder, run the following command to begin sending telemetry data to your IoT hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![De Node.js-app voor IoT Hub-apparaten voor het bewaken van apparaat-naar-cloud-berichten][8]
3. <span data-ttu-id="b3106-182">De tegel **Gebruik** in [Azure Portal][lnk-portal] toont het aantal berichten dat is verzonden naar de IoT-hub:</span><span class="sxs-lookup"><span data-stu-id="b3106-182">The **Usage** tile in the [Azure portal][lnk-portal] shows the number of messages sent to the IoT hub:</span></span>
   
    ![De tegel Gebruik in Azure Portal met het aantal berichten dat is verzonden naar IoT Hub][43]

## <a name="next-steps"></a><span data-ttu-id="b3106-184">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b3106-184">Next steps</span></span>
<span data-ttu-id="b3106-185">In deze handleiding hebt u een nieuwe IoT-hub geconfigureerd in Azure Portal en vervolgens een apparaat-id gemaakt in het id-register van de IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="b3106-185">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="b3106-186">U hebt deze apparaat-id gebruikt om de gesimuleerde apparaattoepassing in staat te stellen apparaat-naar-cloud-berichten te verzenden naar de IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="b3106-186">You used this device identity to enable the simulated device app to send device-to-cloud messages to the IoT hub.</span></span> <span data-ttu-id="b3106-187">Ook hebt u een app gemaakt die de berichten weergeeft die worden ontvangen door de IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="b3106-187">You also created an app that displays the messages received by the IoT hub.</span></span> 

<span data-ttu-id="b3106-188">Als u aan de slag wilt gaan met IoT Hub en andere IoT-scenario's wilt verkennen, leest u deze artikelen:</span><span class="sxs-lookup"><span data-stu-id="b3106-188">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="b3106-189">[Verbinding maken met uw apparaat][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="b3106-189">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="b3106-190">[Aan de slag met apparaatbeheer][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="b3106-190">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="b3106-191">[Aan de slag met Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="b3106-191">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="b3106-192">Raadpleeg de zelfstudie [Apparaat-naar-cloud-berichten verwerken][lnk-process-d2c-tutorial] voor meer informatie over hoe u uw IoT-oplossing uitbreidt en apparaat-naar-cloud-berichten op schaal verwerkt.</span><span class="sxs-lookup"><span data-stu-id="b3106-192">To learn how to extend your IoT solution and process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]


<!-- Images. -->
[7]: ./media/iot-hub-node-node-getstarted/runapp1.png
[8]: ./media/iot-hub-node-node-getstarted/runapp2.png
[43]: ./media/iot-hub-csharp-csharp-getstarted/usage.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-devguide-identity]: iot-hub-devguide-identity-registry.md
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
