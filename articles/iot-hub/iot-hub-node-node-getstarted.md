---
title: aaaGet de slag met Azure IoT Hub (knooppunt) | Microsoft Docs
description: Meer informatie over hoe toosend apparaat-naar-cloud-berichten tooAzure IoT Hub met IoT SDK's voor Node.js. Gesimuleerde apparaat en service-apps tooregister uw apparaat maken en berichten uit iothub berichten verzenden.
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
ms.openlocfilehash: d0747895365f2359a9c38ea1e85a5881d6efec0b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-simulated-device-tooyour-iot-hub-using-node"></a><span data-ttu-id="74c45-104">Verbinding maken met uw gesimuleerde apparaat tooyour iothub met behulp van knooppunt</span><span class="sxs-lookup"><span data-stu-id="74c45-104">Connect your simulated device tooyour IoT hub using Node</span></span>
[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="74c45-105">Aan het einde van de Hallo van deze zelfstudie hebt u drie Node.js console apps:</span><span class="sxs-lookup"><span data-stu-id="74c45-105">At hello end of this tutorial, you have three Node.js console apps:</span></span>

* <span data-ttu-id="74c45-106">**CreateDeviceIdentity.js**, die een apparaat-id maakt en gekoppelde beveiliging sleutel tooconnect app op uw gesimuleerde apparaat.</span><span class="sxs-lookup"><span data-stu-id="74c45-106">**CreateDeviceIdentity.js**, which creates a device identity and associated security key tooconnect your simulated device app.</span></span>
* <span data-ttu-id="74c45-107">**ReadDeviceToCloudMessages.js**, wordt verzonden door uw gesimuleerde apparaattoepassing Hallo-telemetrie.</span><span class="sxs-lookup"><span data-stu-id="74c45-107">**ReadDeviceToCloudMessages.js**, which displays hello telemetry sent by your simulated device app.</span></span>
* <span data-ttu-id="74c45-108">**SimulatedDevice.js**, die tooyour IoT-hub aan Hallo apparaat-id eerder hebt gemaakt, en verzendt een elke tweede met behulp van protocollen MQTT protocol Hallo telemetrie-bericht.</span><span class="sxs-lookup"><span data-stu-id="74c45-108">**SimulatedDevice.js**, which connects tooyour IoT hub with hello device identity created earlier, and sends a telemetry message every second using hello MQTT protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="74c45-109">Hallo artikel [Azure IoT SDK's] [ lnk-hub-sdks] bevat informatie over hello Azure IoT SDK's waarmee u toobuild beide toorun toepassingen op apparaten en de back-end van uw oplossing kunt.</span><span class="sxs-lookup"><span data-stu-id="74c45-109">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="74c45-110">toocomplete in deze zelfstudie, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="74c45-110">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="74c45-111">Node.js versie 0.10.x of hoger.</span><span class="sxs-lookup"><span data-stu-id="74c45-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="74c45-112">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="74c45-112">An active Azure account.</span></span> <span data-ttu-id="74c45-113">(Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)</span><span class="sxs-lookup"><span data-stu-id="74c45-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="74c45-114">U hebt nu uw IoT-hub gemaakt.</span><span class="sxs-lookup"><span data-stu-id="74c45-114">You have now created your IoT hub.</span></span> <span data-ttu-id="74c45-115">U hebt Hallo IoT Hub-hostnaam en Hallo IoT Hub-verbindingsreeks moet u toocomplete Hallo rest van deze handleiding.</span><span class="sxs-lookup"><span data-stu-id="74c45-115">You have hello IoT Hub host name and hello IoT Hub connection string that you need toocomplete hello rest of this tutorial.</span></span>

## <a name="create-a-device-identity"></a><span data-ttu-id="74c45-116">Een apparaat-id maken</span><span class="sxs-lookup"><span data-stu-id="74c45-116">Create a device identity</span></span>
<span data-ttu-id="74c45-117">In deze sectie maakt maken u een Node.js-consoletoepassing die een apparaat-id in Hallo identiteitenregister van uw IoT-hub maakt.</span><span class="sxs-lookup"><span data-stu-id="74c45-117">In this section, you create a Node.js console app that creates a device identity in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="74c45-118">Een apparaat kan alleen verbinding maken met tooIoT hub als er een vermelding in het identiteitenregister Hallo.</span><span class="sxs-lookup"><span data-stu-id="74c45-118">A device can only connect tooIoT hub if it has an entry in hello identity registry.</span></span> <span data-ttu-id="74c45-119">Zie voor meer informatie, Hallo **Identiteitsregister** sectie Hallo [Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="74c45-119">For more information, see hello **Identity Registry** section of hello [IoT Hub developer guide][lnk-devguide-identity].</span></span> <span data-ttu-id="74c45-120">Wanneer u deze consoletoepassing uitvoert, wordt een unieke apparaat-ID gegenereerd en sleutel waarmee het apparaat tooidentify zelf kunt wanneer het apparaat-naar-cloud verzendt berichten tooIoT Hub.</span><span class="sxs-lookup"><span data-stu-id="74c45-120">When you run this console app, it generates a unique device ID and key that your device can use tooidentify itself when it sends device-to-cloud messages tooIoT Hub.</span></span>

1. <span data-ttu-id="74c45-121">Maak een nieuwe lege map met de naam **createdeviceidentity**.</span><span class="sxs-lookup"><span data-stu-id="74c45-121">Create a new empty folder called **createdeviceidentity**.</span></span> <span data-ttu-id="74c45-122">In Hallo **createdeviceidentity** map, een package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="74c45-122">In hello **createdeviceidentity** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="74c45-123">Accepteer alle Hallo standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="74c45-123">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="74c45-124">Bij de opdrachtprompt in Hallo **createdeviceidentity** map na de opdracht tooinstall Hallo Hallo **azure-iothub** Service SDK-pakket:</span><span class="sxs-lookup"><span data-stu-id="74c45-124">At your command prompt in hello **createdeviceidentity** folder, run hello following command tooinstall hello **azure-iothub** Service SDK package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="74c45-125">Maak met een teksteditor, een **CreateDeviceIdentity.js** bestand in Hallo **createdeviceidentity** map.</span><span class="sxs-lookup"><span data-stu-id="74c45-125">Using a text editor, create a **CreateDeviceIdentity.js** file in hello **createdeviceidentity** folder.</span></span>
4. <span data-ttu-id="74c45-126">Voeg de volgende Hallo `require` instructie aan begin Hallo Hallo **CreateDeviceIdentity.js** bestand:</span><span class="sxs-lookup"><span data-stu-id="74c45-126">Add hello following `require` statement at hello start of hello **CreateDeviceIdentity.js** file:</span></span>
   
    ```
    'use strict';
   
    var iothub = require('azure-iothub');
    ```
5. <span data-ttu-id="74c45-127">Hallo na code toohello toevoegen **CreateDeviceIdentity.js** -bestand en vervang Hallo tijdelijke aanduidingswaarde met IoT Hub-verbindingsreeks voor Hallo-hub die u hebt gemaakt in de vorige sectie Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="74c45-127">Add hello following code toohello **CreateDeviceIdentity.js** file and replace hello placeholder value with hello IoT Hub connection string for hello hub you created in hello previous section:</span></span> 
   
    ```
    var connectionString = '{iothub connection string}';
   
    var registry = iothub.Registry.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="74c45-128">Voeg Hallo code toocreate een definitie van het apparaat in Hallo identiteitenregister van uw IoT-hub te volgen.</span><span class="sxs-lookup"><span data-stu-id="74c45-128">Add hello following code toocreate a device definition in hello identity registry in your IoT hub.</span></span> <span data-ttu-id="74c45-129">Deze code maakt een apparaat als Hallo apparaat-ID bestaat niet in het identiteitenregister hello, anders wordt het Hallo-sleutel van de bestaande apparaat Hallo:</span><span class="sxs-lookup"><span data-stu-id="74c45-129">This code creates a device if hello device ID does not exist in hello identity registry, otherwise it returns hello key of hello existing device:</span></span>
   
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

7. <span data-ttu-id="74c45-130">Sla het bestand **CreateDeviceIdentity.js** op en sluit het.</span><span class="sxs-lookup"><span data-stu-id="74c45-130">Save and close **CreateDeviceIdentity.js** file.</span></span>
8. <span data-ttu-id="74c45-131">Hallo toorun **createdeviceidentity** -toepassing uitvoeren van de volgende opdracht achter de opdrachtprompt Hallo in de map createdeviceidentity Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="74c45-131">toorun hello **createdeviceidentity** application, execute hello following command at hello command prompt in hello createdeviceidentity folder:</span></span>
   
    ```
    node CreateDeviceIdentity.js 
    ```
9. <span data-ttu-id="74c45-132">Maak een notitie van Hallo **apparaat-ID** en **apparaatsleutel**.</span><span class="sxs-lookup"><span data-stu-id="74c45-132">Make a note of hello **Device ID** and **Device key**.</span></span> <span data-ttu-id="74c45-133">U moet deze waarden later bij het maken van een toepassing die tooIoT Hub als apparaat verbinding maakt.</span><span class="sxs-lookup"><span data-stu-id="74c45-133">You need these values later when you create an application that connects tooIoT Hub as a device.</span></span>

> [!NOTE]
> <span data-ttu-id="74c45-134">Hallo id-register IoT Hub bewaart alleen apparaat-id's tooenable veilige toegang toohello IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="74c45-134">hello IoT Hub identity registry only stores device identities tooenable secure access toohello IoT hub.</span></span> <span data-ttu-id="74c45-135">Apparaat-id's en sleutels toouse worden opgeslagen als beveiligingsreferenties en waarmee u toodisable toegang tot een afzonderlijk apparaat kunt vlag voor ingeschakeld/uitgeschakeld.</span><span class="sxs-lookup"><span data-stu-id="74c45-135">It stores device IDs and keys toouse as security credentials and an enabled/disabled flag that you can use toodisable access for an individual device.</span></span> <span data-ttu-id="74c45-136">Als uw toepassing toostore andere apparaatspecifieke metagegevens moet, moet deze een toepassingsspecifieke opslagmethode gebruiken.</span><span class="sxs-lookup"><span data-stu-id="74c45-136">If your application needs toostore other device-specific metadata, it should use an application-specific store.</span></span> <span data-ttu-id="74c45-137">Zie voor meer informatie, Hallo [Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide-identity].</span><span class="sxs-lookup"><span data-stu-id="74c45-137">For more information, see hello [IoT Hub developer guide][lnk-devguide-identity].</span></span>
> 
> 

<a id="D2C_node"></a>
## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="74c45-138">Apparaat-naar-cloud-berichten ontvangen</span><span class="sxs-lookup"><span data-stu-id="74c45-138">Receive device-to-cloud messages</span></span>
<span data-ttu-id="74c45-139">In dit gedeelte maakt u een Node.js-consoletoepassing die apparaat-naar-cloud-berichten uit IoT Hub leest.</span><span class="sxs-lookup"><span data-stu-id="74c45-139">In this section, you create a Node.js console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="74c45-140">Een iothub toont een [Event Hubs][lnk-event-hubs-overview]-compatibel eindpunt tooenable u tooread apparaat-naar-cloud-berichten.</span><span class="sxs-lookup"><span data-stu-id="74c45-140">An IoT hub exposes an [Event Hubs][lnk-event-hubs-overview]-compatible endpoint tooenable you tooread device-to-cloud messages.</span></span> <span data-ttu-id="74c45-141">tookeep dingen eenvoudige, deze zelfstudie maakt u een basislezer die niet geschikt voor een implementatie met hoge doorvoer.</span><span class="sxs-lookup"><span data-stu-id="74c45-141">tookeep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="74c45-142">Hallo [apparaat-naar-cloud-berichten verwerken] [ lnk-process-d2c-tutorial] zelfstudie laat zien hoe tooprocess apparaat-naar-cloud-berichten op grote schaal.</span><span class="sxs-lookup"><span data-stu-id="74c45-142">hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial shows you how tooprocess device-to-cloud messages at scale.</span></span> <span data-ttu-id="74c45-143">Hallo [aan de slag met Event Hubs] [ lnk-eventhubs-tutorial] zelfstudie bevat meer informatie over hoe tooprocess van berichten van Event Hubs en toepasselijke toohello IoT Hub Event Hub-compatibele eindpunten is.</span><span class="sxs-lookup"><span data-stu-id="74c45-143">hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial provides further information on how tooprocess messages from Event Hubs and is applicable toohello IoT Hub Event Hub-compatible endpoints.</span></span>

> [!NOTE]
> <span data-ttu-id="74c45-144">Hallo Event Hub-compatibele eindpunt voor het lezen van apparaat-naar-cloudberichten altijd gebruikt Hallo AMQP-protocol.</span><span class="sxs-lookup"><span data-stu-id="74c45-144">hello Event Hub-compatible endpoint for reading device-to-cloud messages always uses hello AMQP protocol.</span></span>
> 
> 

1. <span data-ttu-id="74c45-145">Maak een lege map met de naam **readdevicetocloudmessages**.</span><span class="sxs-lookup"><span data-stu-id="74c45-145">Create an empty folder called **readdevicetocloudmessages**.</span></span> <span data-ttu-id="74c45-146">In Hallo **readdevicetocloudmessages** map, een package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="74c45-146">In hello **readdevicetocloudmessages** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="74c45-147">Accepteer alle Hallo standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="74c45-147">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="74c45-148">Bij de opdrachtprompt in Hallo **readdevicetocloudmessages** map na de opdracht tooinstall Hallo Hallo **azure-event-hubs** pakket:</span><span class="sxs-lookup"><span data-stu-id="74c45-148">At your command prompt in hello **readdevicetocloudmessages** folder, run hello following command tooinstall hello **azure-event-hubs** package:</span></span>
   
    ```
    npm install azure-event-hubs --save
    ```
3. <span data-ttu-id="74c45-149">Maak met een teksteditor, een **ReadDeviceToCloudMessages.js** bestand in Hallo **readdevicetocloudmessages** map.</span><span class="sxs-lookup"><span data-stu-id="74c45-149">Using a text editor, create a **ReadDeviceToCloudMessages.js** file in hello **readdevicetocloudmessages** folder.</span></span>
4. <span data-ttu-id="74c45-150">Voeg de volgende Hallo `require` instructies aan Hallo start Hallo **ReadDeviceToCloudMessages.js** bestand:</span><span class="sxs-lookup"><span data-stu-id="74c45-150">Add hello following `require` statements at hello start of hello **ReadDeviceToCloudMessages.js** file:</span></span>
   
    ```
    'use strict';
   
    var EventHubClient = require('azure-event-hubs').Client;
    ```
5. <span data-ttu-id="74c45-151">Hallo na variabelendeclaratie toevoegen en vervang Hallo tijdelijke aanduidingswaarde met Hallo IoT Hub-verbindingsreeks voor uw hub:</span><span class="sxs-lookup"><span data-stu-id="74c45-151">Add hello following variable declaration and replace hello placeholder value with hello IoT Hub connection string for your hub:</span></span>
   
    ```
    var connectionString = '{iothub connection string}';
    ```
6. <span data-ttu-id="74c45-152">Na twee functies die uitvoer toohello console afdrukken Hallo toevoegen:</span><span class="sxs-lookup"><span data-stu-id="74c45-152">Add hello following two functions that print output toohello console:</span></span>
   
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
7. <span data-ttu-id="74c45-153">Toevoegen van de volgende code toocreate Hallo Hallo **EventHubClient**Hallo verbinding tooyour IoT Hub en opent een ontvanger voor elke partitie maken.</span><span class="sxs-lookup"><span data-stu-id="74c45-153">Add hello following code toocreate hello **EventHubClient**, open hello connection tooyour IoT Hub, and create a receiver for each partition.</span></span> <span data-ttu-id="74c45-154">Deze toepassing gebruikt een filter bij het maken van een ontvanger zodat hello ontvanger alleen berichten tooIoT Hub leest nadat Hallo ontvanger is geactiveerd.</span><span class="sxs-lookup"><span data-stu-id="74c45-154">This application uses a filter when it creates a receiver so that hello receiver only reads messages sent tooIoT Hub after hello receiver starts running.</span></span> <span data-ttu-id="74c45-155">Dit filter is handig in een testomgeving zodat u alleen Hallo huidige reeks berichten zien.</span><span class="sxs-lookup"><span data-stu-id="74c45-155">This filter is useful in a test environment so you see just hello current set of messages.</span></span> <span data-ttu-id="74c45-156">In een productieomgeving moet uw code ervoor zorgen dat alle Hallo-berichten worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="74c45-156">In a production environment, your code should make sure that it processes all hello messages.</span></span> <span data-ttu-id="74c45-157">Zie voor meer informatie, Hallo [hoe tooprocess IoT Hub apparaat-naar-cloud-berichten] [ lnk-process-d2c-tutorial] zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="74c45-157">For more information, see hello [How tooprocess IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial] tutorial:</span></span>
   
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
8. <span data-ttu-id="74c45-158">Opslaan en sluiten Hallo **ReadDeviceToCloudMessages.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="74c45-158">Save and close hello **ReadDeviceToCloudMessages.js** file.</span></span>

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="74c45-159">Een gesimuleerde apparaattoepassing maken</span><span class="sxs-lookup"><span data-stu-id="74c45-159">Create a simulated device app</span></span>
<span data-ttu-id="74c45-160">In deze sectie maakt u een Node.js-consoletoepassing die een apparaat simuleert dat apparaat-naar-cloudberichten tooan iothub verzendt.</span><span class="sxs-lookup"><span data-stu-id="74c45-160">In this section, you create a Node.js console app that simulates a device that sends device-to-cloud messages tooan IoT hub.</span></span>

1. <span data-ttu-id="74c45-161">Maak een lege map met de naam **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="74c45-161">Create an empty folder called **simulateddevice**.</span></span> <span data-ttu-id="74c45-162">In Hallo **simulateddevice** map, een package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="74c45-162">In hello **simulateddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="74c45-163">Accepteer alle Hallo standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="74c45-163">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="74c45-164">Bij de opdrachtprompt in Hallo **simulateddevice** map na de opdracht tooinstall Hallo Hallo **azure-iot-device** apparaat-SDK-pakket en **azure-iot-device-mqtt**pakket:</span><span class="sxs-lookup"><span data-stu-id="74c45-164">At your command prompt in hello **simulateddevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="74c45-165">Maak met een teksteditor, een **SimulatedDevice.js** bestand in Hallo **simulateddevice** map.</span><span class="sxs-lookup"><span data-stu-id="74c45-165">Using a text editor, create a **SimulatedDevice.js** file in hello **simulateddevice** folder.</span></span>
4. <span data-ttu-id="74c45-166">Voeg de volgende Hallo `require` instructies aan Hallo start Hallo **SimulatedDevice.js** bestand:</span><span class="sxs-lookup"><span data-stu-id="74c45-166">Add hello following `require` statements at hello start of hello **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var clientFromConnectionString = require('azure-iot-device-mqtt').clientFromConnectionString;
    var Message = require('azure-iot-device').Message;
    ```
5. <span data-ttu-id="74c45-167">Voeg een **connectionString** variabele en gebruik deze toocreate een **Client** exemplaar.</span><span class="sxs-lookup"><span data-stu-id="74c45-167">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span> <span data-ttu-id="74c45-168">Vervang **{youriothostname}** met de naam van de Hallo van Hallo IoT-hub die u hebt gemaakt Hallo *een IoT Hub maken* sectie.</span><span class="sxs-lookup"><span data-stu-id="74c45-168">Replace **{youriothostname}** with hello name of hello IoT hub you created hello *Create an IoT Hub* section.</span></span> <span data-ttu-id="74c45-169">Vervang **{yourdevicekey}** met Hallo apparaat sleutelwaarde u hebt gegenereerd in Hallo *maken van een apparaat-id* sectie:</span><span class="sxs-lookup"><span data-stu-id="74c45-169">Replace **{yourdevicekey}** with hello device key value you generated in hello *Create a device identity* section:</span></span>
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId=myFirstNodeDevice;SharedAccessKey={yourdevicekey}';
   
    var client = clientFromConnectionString(connectionString);
    ```
6. <span data-ttu-id="74c45-170">Hallo functie toodisplay uitvoer van de toepassing hello volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="74c45-170">Add hello following function toodisplay output from hello application:</span></span>
   
    ```
    function printResultFor(op) {
      return function printResult(err, res) {
        if (err) console.log(op + ' error: ' + err.toString());
        if (res) console.log(op + ' status: ' + res.constructor.name);
      };
    }
    ```
7. <span data-ttu-id="74c45-171">Maak een callback en gebruik Hallo **setInterval** toosend een bericht tooyour IoT-hub elke seconde werken:</span><span class="sxs-lookup"><span data-stu-id="74c45-171">Create a callback and use hello **setInterval** function toosend a message tooyour IoT hub every second:</span></span>
   
    ```
    var connectCallback = function (err) {
      if (err) {
        console.log('Could not connect: ' + err);
      } else {
        console.log('Client connected');
   
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
8. <span data-ttu-id="74c45-172">Open Hallo verbinding tooyour IoT Hub en beginnen met het verzenden van berichten:</span><span class="sxs-lookup"><span data-stu-id="74c45-172">Open hello connection tooyour IoT Hub and start sending messages:</span></span>
   
    ```
    client.open(connectCallback);
    ```
9. <span data-ttu-id="74c45-173">Opslaan en sluiten Hallo **SimulatedDevice.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="74c45-173">Save and close hello **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="74c45-174">tookeep dingen eenvoudige, deze zelfstudie wordt niet geïmplementeerd voor een beleid voor opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="74c45-174">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="74c45-175">In productiecode moet u beleid voor opnieuw proberen (zoals exponentieel uitstel), zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="74c45-175">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="run-hello-apps"></a><span data-ttu-id="74c45-176">Hallo-apps uitvoeren</span><span class="sxs-lookup"><span data-stu-id="74c45-176">Run hello apps</span></span>
<span data-ttu-id="74c45-177">U bent nu klaar toorun Hallo apps.</span><span class="sxs-lookup"><span data-stu-id="74c45-177">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="74c45-178">Bij een opdrachtprompt in Hallo **readdevicetocloudmessages** map Hallo opdracht toobegin bewaking van uw IoT-hub te volgen:</span><span class="sxs-lookup"><span data-stu-id="74c45-178">At a command prompt in hello **readdevicetocloudmessages** folder, run hello following command toobegin monitoring your IoT hub:</span></span>
   
    ```
    node ReadDeviceToCloudMessages.js 
    ```
   
    ![Node.js IoT Hub service app toomonitor apparaat-naar-cloud-berichten][7]
2. <span data-ttu-id="74c45-180">Bij een opdrachtprompt in Hallo **simulateddevice** map Hallo opdracht toobegin verzenden van telemetrie gegevens tooyour IoT-hub te volgen:</span><span class="sxs-lookup"><span data-stu-id="74c45-180">At a command prompt in hello **simulateddevice** folder, run hello following command toobegin sending telemetry data tooyour IoT hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   
    ![Node.js IoT Hub apparaat-app toosend apparaat-naar-cloud-berichten][8]
3. <span data-ttu-id="74c45-182">Hallo **gebruik** -tegel in Hallo [Azure-portal] [ lnk-portal] toont Hallo aantal verzonden berichten toohello IoT-hub:</span><span class="sxs-lookup"><span data-stu-id="74c45-182">hello **Usage** tile in hello [Azure portal][lnk-portal] shows hello number of messages sent toohello IoT hub:</span></span>
   
    ![Azure portal gebruik tegel met aantal verzonden berichten tooIoT Hub][43]

## <a name="next-steps"></a><span data-ttu-id="74c45-184">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="74c45-184">Next steps</span></span>
<span data-ttu-id="74c45-185">In deze zelfstudie maakt u een nieuwe iothub geconfigureerd in hello Azure-portal en vervolgens een apparaat-id in de id-register Hallo iothub hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="74c45-185">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="74c45-186">U hebt deze apparaat-id tooenable Hallo gesimuleerd apparaat app toosend apparaat-naar-cloudberichten toohello iothub gebruikt.</span><span class="sxs-lookup"><span data-stu-id="74c45-186">You used this device identity tooenable hello simulated device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="74c45-187">Hebt u ook een app die wordt weergegeven Hallo-berichten dat is ontvangen door de Hallo iothub hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="74c45-187">You also created an app that displays hello messages received by hello IoT hub.</span></span> 

<span data-ttu-id="74c45-188">toocontinue aan de slag met IoT Hub en tooexplore raadpleegt u andere IoT-scenario's:</span><span class="sxs-lookup"><span data-stu-id="74c45-188">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="74c45-189">[Verbinding maken met uw apparaat][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="74c45-189">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="74c45-190">[Aan de slag met apparaatbeheer][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="74c45-190">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="74c45-191">[Aan de slag met Azure IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="74c45-191">[Getting started with Azure IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="74c45-192">toolearn hoe tooextend uw IoT-oplossing en proces apparaat-naar-cloud-berichten op grote schaal, zien Hallo [apparaat-naar-cloud-berichten verwerken] [ lnk-process-d2c-tutorial] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="74c45-192">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>
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
