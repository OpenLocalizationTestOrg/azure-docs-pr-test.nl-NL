---
title: aaaGet de slag met Azure IoT Hub apparaat horende (knooppunt) | Microsoft Docs
description: Hoe toouse Azure IoT Hub apparaat horende tooadd tags en gebruik vervolgens een IoT Hub-query. U gebruikt hello Azure IoT SDK's voor Node.js tooimplement Hallo gesimuleerde apparaattoepassing en een service-app die Hallo-labels toegevoegd en Hallo IoT Hub-query wordt uitgevoerd.
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: 
ms.assetid: 314c88e4-cce1-441c-b75a-d2e08e39ae7d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.openlocfilehash: d60b8c3de85e9285e496b86e27d4ee31a0554a1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-node"></a><span data-ttu-id="c1d11-104">Aan de slag met apparaat horende (knooppunt)</span><span class="sxs-lookup"><span data-stu-id="c1d11-104">Get started with device twins (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="c1d11-105">Aan het einde van de Hallo van deze zelfstudie hebt u twee console Node.js-apps:</span><span class="sxs-lookup"><span data-stu-id="c1d11-105">At hello end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="c1d11-106">**AddTagsAndQuery.js**, een back-end-app van Node.js, dat labels toegevoegd en wordt opgevraagd horende apparaten.</span><span class="sxs-lookup"><span data-stu-id="c1d11-106">**AddTagsAndQuery.js**, a Node.js back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="c1d11-107">**TwinSimulatedDevice.js**, een Node.js-app dat een apparaat simuleert dat tooyour IoT-hub is verbonden met de apparaat-id Hallo eerder hebt gemaakt, en rapporteert de voorwaarde van de verbinding.</span><span class="sxs-lookup"><span data-stu-id="c1d11-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects tooyour IoT hub with hello device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="c1d11-108">Hallo artikel [Azure IoT SDK's] [ lnk-hub-sdks] bevat informatie over hello Azure IoT SDK's waarmee u toobuild kunt apparaat- en back-end-apps.</span><span class="sxs-lookup"><span data-stu-id="c1d11-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="c1d11-109">toocomplete in deze zelfstudie hebt u Hallo volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="c1d11-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="c1d11-110">Node.js versie 0.10.x of hoger.</span><span class="sxs-lookup"><span data-stu-id="c1d11-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="c1d11-111">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="c1d11-111">An active Azure account.</span></span> <span data-ttu-id="c1d11-112">(Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)</span><span class="sxs-lookup"><span data-stu-id="c1d11-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-service-app"></a><span data-ttu-id="c1d11-113">Hallo-service-app maken</span><span class="sxs-lookup"><span data-stu-id="c1d11-113">Create hello service app</span></span>
<span data-ttu-id="c1d11-114">In deze sectie maakt u een Node.js-consoletoepassing die wordt toegevoegd locatie metagegevens toohello apparaat twin die zijn gekoppeld aan **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="c1d11-114">In this section, you create a Node.js console app that adds location metadata toohello device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="c1d11-115">Vervolgens query's Hallo apparaat horende opgeslagen ons in IoT-hub Hallo Hallo apparaten zich in Hallo selecteren en vervolgens Hallo toepassingsgroepen die een mobiele verbinding rapporteren.</span><span class="sxs-lookup"><span data-stu-id="c1d11-115">It then queries hello device twins stored in hello IoT hub selecting hello devices located in hello US, and then hello ones that are reporting a cellular connection.</span></span>

1. <span data-ttu-id="c1d11-116">Maak een nieuwe lege map genaamd **addtagsandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="c1d11-116">Create a new empty folder called **addtagsandqueryapp**.</span></span> <span data-ttu-id="c1d11-117">In Hallo **addtagsandqueryapp** map, een nieuw package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="c1d11-117">In hello **addtagsandqueryapp** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="c1d11-118">Accepteer alle Hallo standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="c1d11-118">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="c1d11-119">Bij de opdrachtprompt in Hallo **addtagsandqueryapp** map na de opdracht tooinstall Hallo Hallo **azure-iothub** pakket:</span><span class="sxs-lookup"><span data-stu-id="c1d11-119">At your command prompt in hello **addtagsandqueryapp** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="c1d11-120">Start een teksteditor en maak een nieuwe **AddTagsAndQuery.js** bestand in Hallo **addtagsandqueryapp** map.</span><span class="sxs-lookup"><span data-stu-id="c1d11-120">Using a text editor, create a new **AddTagsAndQuery.js** file in hello **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="c1d11-121">Hallo na code toohello toevoegen **AddTagsAndQuery.js** -bestand en vervang Hallo **{iot hub verbindingsreeks}** aanduiding voor items met Hallo IoT Hub-verbindingsreeks die u tijdens het maken van uw hub hebt gekopieerd:</span><span class="sxs-lookup"><span data-stu-id="c1d11-121">Add hello following code toohello **AddTagsAndQuery.js** file, and substitute hello **{iot hub connection string}** placeholder with hello IoT Hub connection string you copied when you created your hub:</span></span>
   
        'use strict';
        var iothub = require('azure-iothub');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var patch = {
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                      }
                    }
                };
   
                twin.update(patch, function(err) {
                  if (err) {
                    console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                  } else {
                    console.log(twin.deviceId + ' twin updated successfully');
                    queryTwins();
                  }
                });
            }
        });
   
    <span data-ttu-id="c1d11-122">Hallo **register** object beschrijft alle Hallo methoden vereist toointeract met apparaat horende van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="c1d11-122">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="c1d11-123">Hallo vorige code initialiseert eerst Hallo **register** object, en vervolgens haalt Hallo apparaat twin voor **myDeviceId**, en ten slotte de labels bijgewerkt met informatie over de locatie van de gewenste Hallo.</span><span class="sxs-lookup"><span data-stu-id="c1d11-123">hello previous code first initializes hello **Registry** object, then retrieves hello device twin for **myDeviceId**, and finally updates its tags with hello desired location information.</span></span>
   
    <span data-ttu-id="c1d11-124">Na het Hallo Hallo bijwerken tags die erin aanroepen Hallo **queryTwins** functie.</span><span class="sxs-lookup"><span data-stu-id="c1d11-124">After hello updating hello tags it calls hello **queryTwins** function.</span></span>
5. <span data-ttu-id="c1d11-125">Toevoegen van de volgende code achter Hallo Hallo **AddTagsAndQuery.js** tooimplement hello **queryTwins** functie:</span><span class="sxs-lookup"><span data-stu-id="c1d11-125">Add hello following code at hello end of  **AddTagsAndQuery.js** tooimplement hello **queryTwins** function:</span></span>
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
   
            query = registry.createQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log("Devices in Redmond43 using cellular network: " + results.map(function(twin) {return twin.deviceId}).join(','));
                }
            });
        };
   
    <span data-ttu-id="c1d11-126">de vorige code Hallo twee query's uitvoert: Hallo selecteert eerst alleen Hallo apparaat horende apparaten zich in Hallo **Redmond43** installaties en Hallo tweede verfijning Hallo query tooselect alleen Hallo apparaten die ook zijn verbonden via mobiel netwerk.</span><span class="sxs-lookup"><span data-stu-id="c1d11-126">hello previous code executes two queries: hello first selects only hello device twins of devices located in hello **Redmond43** plant, and hello second refines hello query tooselect only hello devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="c1d11-127">Houd er rekening mee dat vorige code Hallo bij het maken van Hallo **query** object, geeft u een maximum aantal geretourneerde documenten.</span><span class="sxs-lookup"><span data-stu-id="c1d11-127">Note that hello previous code, when it creates hello **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="c1d11-128">Hallo **query** object bevat een **hasMoreResults** Boole-eigenschap waarmee u tooinvoke hello kunt **nextAsTwin** methoden meerdere keren tooretrieve alle resulteert.</span><span class="sxs-lookup"><span data-stu-id="c1d11-128">hello **query** object contains a **hasMoreResults** boolean property that you can use tooinvoke hello **nextAsTwin** methods multiple times tooretrieve all results.</span></span> <span data-ttu-id="c1d11-129">Een methode aangeroepen **volgende** is beschikbaar voor de resultaten die geen apparaat horende bijvoorbeeld resultaten van query's voor aggregatie.</span><span class="sxs-lookup"><span data-stu-id="c1d11-129">A method called **next** is available for results that are not device twins for example, results of aggregation queries.</span></span>
6. <span data-ttu-id="c1d11-130">Hallo-toepassing met uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="c1d11-130">Run hello application with:</span></span>
   
        node AddTagsAndQuery.js
   
    <span data-ttu-id="c1d11-131">U ziet één apparaat in Hallo resultaten voor Hallo query vragen voor alle apparaten vinden in **Redmond43** en geen voor de Hallo-query die Hallo beperkt resultaten toodevices die gebruikmaken van een mobiel netwerk.</span><span class="sxs-lookup"><span data-stu-id="c1d11-131">You should see one device in hello results for hello query asking for all devices located in **Redmond43** and none for hello query that restricts hello results toodevices that use a cellular network.</span></span>
   
    ![][1]

<span data-ttu-id="c1d11-132">In de volgende sectie Hallo maakt u een apparaat-app die Hallo connectiviteit informatie rapporteert en wijzigingen resultaat van query in de vorige sectie Hallo HALLO hallo.</span><span class="sxs-lookup"><span data-stu-id="c1d11-132">In hello next section you create a device app that reports hello connectivity information and changes hello result of hello query in hello previous section.</span></span>

## <a name="create-hello-device-app"></a><span data-ttu-id="c1d11-133">Hallo apparaattoepassing maken</span><span class="sxs-lookup"><span data-stu-id="c1d11-133">Create hello device app</span></span>
<span data-ttu-id="c1d11-134">In deze sectie maakt u een Node.js-consoletoepassing die verbinding tooyour hub als maakt **myDeviceId**, en vervolgens de updates die de apparaat-twin de gerapporteerd toocontain Hallo eigenschapsgegevens dat is verbonden met een mobiel netwerk.</span><span class="sxs-lookup"><span data-stu-id="c1d11-134">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, and then updates its device twin's reported properties toocontain hello information that it is connected using a cellular network.</span></span>

> [!NOTE]
> <span data-ttu-id="c1d11-135">Op dit moment horende apparaten zijn alleen toegankelijk vanaf apparaten die verbinding tooIoT Hub maken met Hallo MQTT-protocol.</span><span class="sxs-lookup"><span data-stu-id="c1d11-135">At this time, device twins are accessible only from devices that connect tooIoT Hub using hello MQTT protocol.</span></span> <span data-ttu-id="c1d11-136">Raadpleeg toohello [MQTT ondersteuning] [ lnk-devguide-mqtt] artikel voor instructies over het tooconvert bestaande apparaat app toouse MQTT.</span><span class="sxs-lookup"><span data-stu-id="c1d11-136">Please refer toohello [MQTT support][lnk-devguide-mqtt] article for instructions on how tooconvert existing device app toouse MQTT.</span></span>
> 
> 

1. <span data-ttu-id="c1d11-137">Maak een nieuwe lege map genaamd **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="c1d11-137">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="c1d11-138">In Hallo **reportconnectivity** map, een nieuw package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="c1d11-138">In hello **reportconnectivity** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="c1d11-139">Accepteer alle Hallo standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="c1d11-139">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="c1d11-140">Bij de opdrachtprompt in Hallo **reportconnectivity** map na de opdracht tooinstall Hallo Hallo **azure-iot-device**, en **azure-iot-device-mqtt** pakket :</span><span class="sxs-lookup"><span data-stu-id="c1d11-140">At your command prompt in hello **reportconnectivity** folder, run hello following command tooinstall hello **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="c1d11-141">Start een teksteditor en maak een nieuwe **ReportConnectivity.js** bestand in Hallo **reportconnectivity** map.</span><span class="sxs-lookup"><span data-stu-id="c1d11-141">Using a text editor, create a new **ReportConnectivity.js** file in hello **reportconnectivity** folder.</span></span>
4. <span data-ttu-id="c1d11-142">Hallo na code toohello toevoegen **ReportConnectivity.js** -bestand en vervang Hallo **{verbindingsreeks apparaat}** aanduiding voor items met de apparaat-verbindingsreeks voor de Hallo u tijdens het maken van Hallo gekopieerd **myDeviceId** apparaat-id:</span><span class="sxs-lookup"><span data-stu-id="c1d11-142">Add hello following code toohello **ReportConnectivity.js** file, and substitute hello **{device connection string}** placeholder with hello device connection string you copied when you created hello **myDeviceId** device identity:</span></span>
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
   
            client.getTwin(function(err, twin) {
            if (err) {
                console.error('could not get twin');
            } else {
                var patch = {
                    connectivity: {
                        type: 'cellular'
                    }
                };
   
                twin.properties.reported.update(patch, function(err) {
                    if (err) {
                        console.error('could not update twin');
                    } else {
                        console.log('twin state reported');
                        process.exit();
                    }
                });
            }
            });
        }
        });
   
    <span data-ttu-id="c1d11-143">Hallo **Client** object bevat alle Hallo-methoden die u nodig hebt toointeract met apparaat horende van Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="c1d11-143">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="c1d11-144">vorige code Hallo nadat het Hallo initialiseert **Client** -object is opgehaald Hallo apparaat twin voor **myDeviceId** en de bijbehorende gemelde eigenschap bijgewerkt met informatie over Hallo-connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="c1d11-144">hello previous code, after it initializes hello **Client** object, retrieves hello device twin for **myDeviceId** and updates its reported property with hello connectivity information.</span></span>
5. <span data-ttu-id="c1d11-145">Hallo apparaat app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="c1d11-145">Run hello device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="c1d11-146">U ziet het Hallo-bericht `twin state reported`.</span><span class="sxs-lookup"><span data-stu-id="c1d11-146">You should see hello message `twin state reported`.</span></span>
6. <span data-ttu-id="c1d11-147">Nu dat hello apparaat de connectiviteit informatie gerapporteerd, moet deze worden weergegeven in beide query's.</span><span class="sxs-lookup"><span data-stu-id="c1d11-147">Now that hello device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="c1d11-148">Ga terug in Hallo **addtagsandqueryapp** Hallo map en voer een query opnieuw:</span><span class="sxs-lookup"><span data-stu-id="c1d11-148">Go back in hello **addtagsandqueryapp** folder and run hello queries again:</span></span>
   
        node AddTagsAndQuery.js
   
    <span data-ttu-id="c1d11-149">Deze tijd **myDeviceId** moet worden weergegeven in beide queryresultaten.</span><span class="sxs-lookup"><span data-stu-id="c1d11-149">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][3]

## <a name="next-steps"></a><span data-ttu-id="c1d11-150">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c1d11-150">Next steps</span></span>
<span data-ttu-id="c1d11-151">In deze zelfstudie maakt u een nieuwe iothub geconfigureerd in hello Azure-portal en vervolgens een apparaat-id in de id-register Hallo iothub hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="c1d11-151">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="c1d11-152">U metagegevens van apparaten als labels toegevoegd vanuit een back-end-app en een gesimuleerd apparaat app tooreport-apparaatgegevens connectiviteit in Hallo apparaat twin geschreven.</span><span class="sxs-lookup"><span data-stu-id="c1d11-152">You added device metadata as tags from a back-end app, and wrote a simulated device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="c1d11-153">U hebt ook geleerd hoe tooquery deze informatie Hallo IoT-Hub SQL-achtige query language gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c1d11-153">You also learned how tooquery this information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="c1d11-154">Gebruik Hallo resources toolearn hoe volgende aan:</span><span class="sxs-lookup"><span data-stu-id="c1d11-154">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="c1d11-155">verzenden van telemetrie vanaf apparaten Hello [aan de slag met IoT Hub] [ lnk-iothub-getstarted] zelfstudie</span><span class="sxs-lookup"><span data-stu-id="c1d11-155">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="c1d11-156">apparaten configureren met de gewenste eigenschappen van apparaat twin Hello [gebruik gewenst eigenschappen tooconfigure apparaten] [ lnk-twin-how-to-configure] zelfstudie</span><span class="sxs-lookup"><span data-stu-id="c1d11-156">configure devices using device twin's desired properties with hello [Use desired properties tooconfigure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="c1d11-157">beheren van apparaten interactief (zoals het inschakelen van een ventilator van een gebruiker beheerde app), met Hallo [direct methoden gebruiken] [ lnk-methods-tutorial] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="c1d11-157">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[1]: media/iot-hub-node-node-twin-getstarted/service1.png
[3]: media/iot-hub-node-node-twin-getstarted/service2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/

[lnk-twin-how-to-configure]: iot-hub-node-node-twin-how-to-configure.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md

[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
