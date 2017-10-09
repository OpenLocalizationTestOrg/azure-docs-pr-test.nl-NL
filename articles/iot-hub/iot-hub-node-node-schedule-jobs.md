---
title: aaaSchedule taken met Azure IoT Hub (knooppunt) | Microsoft Docs
description: Hoe een Azure-IoT-Hub tooschedule taak tooinvoke een directe methode op meerdere apparaten. U hello Azure IoT SDK's gebruiken voor Node.js tooimplement Hallo gesimuleerd apparaat-apps en een app toorun Hallo taak.
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 2233356e-b005-4765-ae41-3a4872bda943
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: be293362447fbcddaa3433b66f208f22545fe0c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-and-broadcast-jobs-node"></a><span data-ttu-id="ecc2b-104">Planning en broadcast-taken (knooppunt)</span><span class="sxs-lookup"><span data-stu-id="ecc2b-104">Schedule and broadcast jobs (Node)</span></span>

[!INCLUDE [iot-hub-selector-schedule-jobs](../../includes/iot-hub-selector-schedule-jobs.md)]

<span data-ttu-id="ecc2b-105">Azure IoT Hub is een volledig beheerde service waarmee u een back-endserver voor apps toocreate en bijhouden taken die gepland en miljoenen apparaten werken.</span><span class="sxs-lookup"><span data-stu-id="ecc2b-105">Azure IoT Hub is a fully managed service that enables a back-end app toocreate and track jobs that schedule and update millions of devices.</span></span>  <span data-ttu-id="ecc2b-106">Taken kunnen worden gebruikt voor Hallo van de volgende activiteiten:</span><span class="sxs-lookup"><span data-stu-id="ecc2b-106">Jobs can be used for hello following actions:</span></span>

* <span data-ttu-id="ecc2b-107">Gewenste eigenschappen bijwerken</span><span class="sxs-lookup"><span data-stu-id="ecc2b-107">Update desired properties</span></span>
* <span data-ttu-id="ecc2b-108">Labels bijwerken</span><span class="sxs-lookup"><span data-stu-id="ecc2b-108">Update tags</span></span>
* <span data-ttu-id="ecc2b-109">Directe methoden aanroepen</span><span class="sxs-lookup"><span data-stu-id="ecc2b-109">Invoke direct methods</span></span>

<span data-ttu-id="ecc2b-110">In dat geval een taak verpakt een van deze acties en houdt Hallo voortgang van de uitvoering op basis van een verzameling apparaten, dit wordt gedefinieerd door een apparaat twin query.</span><span class="sxs-lookup"><span data-stu-id="ecc2b-110">Conceptually, a job wraps one of these actions and tracks hello progress of execution against a set of devices, which is defined by a device twin query.</span></span>  <span data-ttu-id="ecc2b-111">Bijvoorbeeld, kunt een back-endserver voor apps gebruiken een taak tooinvoke een methode voor opnieuw opstarten op 10.000 apparaten, is opgegeven door een apparaat twin query en gepland op een later tijdstip.</span><span class="sxs-lookup"><span data-stu-id="ecc2b-111">For example, a back-end app can use a job tooinvoke a reboot method on 10,000 devices, specified by a device twin query and scheduled at a future time.</span></span>  <span data-ttu-id="ecc2b-112">Deze toepassing kunt vervolgens voortgang bijhouden als elk van deze apparaten ontvangen en Hallo opnieuw opstarten methode uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ecc2b-112">That application can then track progress as each of those devices receive and execute hello reboot method.</span></span>

<span data-ttu-id="ecc2b-113">Meer informatie over elk van deze mogelijkheden in deze artikelen:</span><span class="sxs-lookup"><span data-stu-id="ecc2b-113">Learn more about each of these capabilities in these articles:</span></span>

* <span data-ttu-id="ecc2b-114">Apparaat-twin en eigenschappen: [aan de slag met apparaat horende] [ lnk-get-started-twin] en [zelfstudie: hoe toouse apparaat eigenschappen twin][lnk-twin-props]</span><span class="sxs-lookup"><span data-stu-id="ecc2b-114">Device twin and properties: [Get started with device twins][lnk-get-started-twin] and [Tutorial: How toouse device twin properties][lnk-twin-props]</span></span>
* <span data-ttu-id="ecc2b-115">directe methoden: [IoT Hub developer guide - rechtstreekse methoden] [ lnk-dev-methods] en [zelfstudie: directe methoden][lnk-c2d-methods]</span><span class="sxs-lookup"><span data-stu-id="ecc2b-115">direct methods: [IoT Hub developer guide - direct methods][lnk-dev-methods] and [Tutorial: direct methods][lnk-c2d-methods]</span></span>

<span data-ttu-id="ecc2b-116">In deze handleiding ontdekt u hoe u:</span><span class="sxs-lookup"><span data-stu-id="ecc2b-116">This tutorial shows you how to:</span></span>

* <span data-ttu-id="ecc2b-117">Maken van een gesimuleerde apparaattoepassing met een directe methode waarmee **lockDoor** die kan worden aangeroepen door Hallo back-end oplossing.</span><span class="sxs-lookup"><span data-stu-id="ecc2b-117">Create a simulated device app that has a direct method which enables **lockDoor** which can be called by hello solution back end.</span></span>
* <span data-ttu-id="ecc2b-118">Een Node.js-consoletoepassing maken die Hallo aanroepen **lockDoor** directe methode in een gesimuleerde apparaattoepassing Hallo met behulp van een taak en updates Hallo gewenst eigenschappen met behulp van een taak van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="ecc2b-118">Create a Node.js console app that calls hello **lockDoor** direct method in hello simulated device app using a job and updates hello desired properties using a device job.</span></span>

<span data-ttu-id="ecc2b-119">Aan het einde van de Hallo van deze zelfstudie hebt u twee console Node.js-apps:</span><span class="sxs-lookup"><span data-stu-id="ecc2b-119">At hello end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="ecc2b-120">**simDevice.js**, die tooyour IoT-hub aan Hallo apparaat-id en ontvangt een **lockDoor** directe methode.</span><span class="sxs-lookup"><span data-stu-id="ecc2b-120">**simDevice.js**, which connects tooyour IoT hub with hello device identity and receives a **lockDoor** direct method.</span></span>

<span data-ttu-id="ecc2b-121">**scheduleJobService.js**, die een methode wordt aangeroepen direct in Hallo gesimuleerd apparaat app en update Hallo apparaat twin de gewenste eigenschappen met behulp van een taak.</span><span class="sxs-lookup"><span data-stu-id="ecc2b-121">**scheduleJobService.js**, which calls a direct method in hello simulated device app and update hello device twin's desired properties using a job.</span></span>

<span data-ttu-id="ecc2b-122">toocomplete in deze zelfstudie, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="ecc2b-122">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="ecc2b-123">Node.js-versie 0.12.x of hoger</span><span class="sxs-lookup"><span data-stu-id="ecc2b-123">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="ecc2b-124">[Uw ontwikkelingsomgeving voorbereiden] [ lnk-dev-setup] wordt beschreven hoe tooinstall Node.js voor deze zelfstudie op Windows of Linux.</span><span class="sxs-lookup"><span data-stu-id="ecc2b-124">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="ecc2b-125">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="ecc2b-125">An active Azure account.</span></span> <span data-ttu-id="ecc2b-126">(Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)</span><span class="sxs-lookup"><span data-stu-id="ecc2b-126">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="ecc2b-127">Een gesimuleerde apparaattoepassing maken</span><span class="sxs-lookup"><span data-stu-id="ecc2b-127">Create a simulated device app</span></span>
<span data-ttu-id="ecc2b-128">In deze sectie maken van een Node.js-consoletoepassing die reageert tooa directe methode aangeroepen door Hallo cloud, die een herstart van het gesimuleerde apparaat activeert en maakt gebruik van Hallo gerapporteerd eigenschappen tooenable apparaat twin query's tooidentify apparaten en wanneer ze laatste opnieuw opgestart.</span><span class="sxs-lookup"><span data-stu-id="ecc2b-128">In this section, you create a Node.js console app that responds tooa direct method called by hello cloud, which triggers a simulated device reboot and uses hello reported properties tooenable device twin queries tooidentify devices and when they last rebooted.</span></span>

1. <span data-ttu-id="ecc2b-129">Maak een nieuwe lege map genaamd **simDevice**.</span><span class="sxs-lookup"><span data-stu-id="ecc2b-129">Create a new empty folder called **simDevice**.</span></span>  <span data-ttu-id="ecc2b-130">In Hallo **simDevice** map, een package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="ecc2b-130">In hello **simDevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="ecc2b-131">Accepteer alle Hallo standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="ecc2b-131">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="ecc2b-132">Bij de opdrachtprompt in Hallo **simDevice** map na de opdracht tooinstall Hallo Hallo **azure-iot-device** apparaat-SDK-pakket en **azure-iot-device-mqtt** pakket:</span><span class="sxs-lookup"><span data-stu-id="ecc2b-132">At your command prompt in hello **simDevice** folder, run hello following command tooinstall hello **azure-iot-device** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="ecc2b-133">Start een teksteditor en maak een nieuwe **simDevice.js** bestand in Hallo **simDevice** map.</span><span class="sxs-lookup"><span data-stu-id="ecc2b-133">Using a text editor, create a new **simDevice.js** file in hello **simDevice** folder.</span></span>
4. <span data-ttu-id="ecc2b-134">Toevoegen van de volgende Hallo 'vereist' instructies toe aan Hallo begin Hallo **simDevice.js** bestand:</span><span class="sxs-lookup"><span data-stu-id="ecc2b-134">Add hello following 'require' statements at hello start of hello **simDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Client = require('azure-iot-device').Client;
    var Protocol = require('azure-iot-device-mqtt').Mqtt;
    ```
5. <span data-ttu-id="ecc2b-135">Voeg een **connectionString** variabele en gebruik deze toocreate een **Client** exemplaar.</span><span class="sxs-lookup"><span data-stu-id="ecc2b-135">Add a **connectionString** variable and use it toocreate a **Client** instance.</span></span>  
   
    ```
    var connectionString = 'HostName={youriothostname};DeviceId={yourdeviceid};SharedAccessKey={yourdevicekey}';
    var client = Client.fromConnectionString(connectionString, Protocol);
    ```
6. <span data-ttu-id="ecc2b-136">Toevoegen van de volgende functie toohandle Hallo Hallo **lockDoor** methode.</span><span class="sxs-lookup"><span data-stu-id="ecc2b-136">Add hello following function toohandle hello **lockDoor** method.</span></span>
   
    ```
    var onLockDoor = function(request, response) {
   
        // Respond hello cloud app for hello direct method
        response.send(200, function(err) {
            if (!err) {
                console.error('An error occured when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.');
            }
        });
   
        console.log('Locking Door!');
    };
    ```
7. <span data-ttu-id="ecc2b-137">Toevoegen van de volgende code tooregister Hallo-handler voor Hallo Hallo **lockDoor** methode.</span><span class="sxs-lookup"><span data-stu-id="ecc2b-137">Add hello following code tooregister hello handler for hello **lockDoor** method.</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('Could not connect tooIotHub client.');
        }  else {
            console.log('Client connected tooIoT Hub. Register handler for lockDoor direct method.');
            client.onDeviceMethod('lockDoor', onLockDoor);
        }
    });
    ```
8. <span data-ttu-id="ecc2b-138">Opslaan en sluiten Hallo **simDevice.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="ecc2b-138">Save and close hello **simDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="ecc2b-139">tookeep dingen eenvoudige, deze zelfstudie wordt niet geïmplementeerd voor een beleid voor opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="ecc2b-139">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="ecc2b-140">In productiecode moet u beleid voor opnieuw proberen (zoals exponentieel uitstel), zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="ecc2b-140">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="schedule-jobs-for-calling-a-direct-method-and-updating-a-device-twins-properties"></a><span data-ttu-id="ecc2b-141">Plannen van taken voor het aanroepen van een directe methode en de eigenschappen voor een apparaat-twin bijwerken</span><span class="sxs-lookup"><span data-stu-id="ecc2b-141">Schedule jobs for calling a direct method and updating a device twin's properties</span></span>
<span data-ttu-id="ecc2b-142">In deze sectie maakt u een Node.js-consoletoepassing die een externe Start **lockDoor** op een apparaat met behulp van een directe methode en update Hallo apparaat twin van eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="ecc2b-142">In this section, you create a Node.js console app that initiates a remote **lockDoor** on a device using a direct method and update hello device twin's properties.</span></span>

1. <span data-ttu-id="ecc2b-143">Maak een nieuwe lege map genaamd **scheduleJobService**.</span><span class="sxs-lookup"><span data-stu-id="ecc2b-143">Create a new empty folder called **scheduleJobService**.</span></span>  <span data-ttu-id="ecc2b-144">In Hallo **scheduleJobService** map, een package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="ecc2b-144">In hello **scheduleJobService** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="ecc2b-145">Accepteer alle Hallo standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="ecc2b-145">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="ecc2b-146">Bij de opdrachtprompt in Hallo **scheduleJobService** map na de opdracht tooinstall Hallo Hallo **azure-iothub** apparaat-SDK-pakket en **azure-iot-device-mqtt**pakket:</span><span class="sxs-lookup"><span data-stu-id="ecc2b-146">At your command prompt in hello **scheduleJobService** folder, run hello following command tooinstall hello **azure-iothub** Device SDK package and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iothub uuid --save
    ```
3. <span data-ttu-id="ecc2b-147">Start een teksteditor en maak een nieuwe **scheduleJobService.js** bestand in Hallo **scheduleJobService** map.</span><span class="sxs-lookup"><span data-stu-id="ecc2b-147">Using a text editor, create a new **scheduleJobService.js** file in hello **scheduleJobService** folder.</span></span>
4. <span data-ttu-id="ecc2b-148">Toevoegen van de volgende Hallo 'vereist' instructies toe aan Hallo begin Hallo **dmpatterns_gscheduleJobServiceetstarted_service.js** bestand:</span><span class="sxs-lookup"><span data-stu-id="ecc2b-148">Add hello following 'require' statements at hello start of hello **dmpatterns_gscheduleJobServiceetstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var uuid = require('uuid');
    var JobClient = require('azure-iothub').JobClient;
    ```
5. <span data-ttu-id="ecc2b-149">Hallo na variabelendeclaraties toevoegen en vervang de waarden van de tijdelijke aanduiding Hallo:</span><span class="sxs-lookup"><span data-stu-id="ecc2b-149">Add hello following variable declarations and replace hello placeholder values:</span></span>
   
    ```
    var connectionString = '{iothubconnectionstring}';
    var queryCondition = "deviceId IN ['myDeviceId']";
    var startTime = new Date();
    var maxExecutionTimeInSeconds =  3600;
    var jobClient = JobClient.fromConnectionString(connectionString);
    ```
6. <span data-ttu-id="ecc2b-150">Hallo volgen functie die wordt gebruikt toomonitor Hallo uitvoering van Hallo taak toevoegen:</span><span class="sxs-lookup"><span data-stu-id="ecc2b-150">Add hello following function that will be used toomonitor hello execution of hello job:</span></span>
   
    ```
    function monitorJob (jobId, callback) {
        var jobMonitorInterval = setInterval(function() {
            jobClient.getJob(jobId, function(err, result) {
            if (err) {
                console.error('Could not get job status: ' + err.message);
            } else {
                console.log('Job: ' + jobId + ' - status: ' + result.status);
                if (result.status === 'completed' || result.status === 'failed' || result.status === 'cancelled') {
                clearInterval(jobMonitorInterval);
                callback(null, result);
                }
            }
            });
        }, 5000);
    }
    ```
7. <span data-ttu-id="ecc2b-151">Hallo code tooschedule Hallo taak die Hallo apparaat methode aanroept volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="ecc2b-151">Add hello following code tooschedule hello job that calls hello device method:</span></span>
   
    ```
    var methodParams = {
        methodName: 'lockDoor',
        payload: null,
        responseTimeoutInSeconds: 15 // Timeout after 15 seconds if device is unable tooprocess method
    };
   
    var methodJobId = uuid.v4();
    console.log('scheduling Device Method job with id: ' + methodJobId);
    jobClient.scheduleDeviceMethod(methodJobId,
                                queryCondition,
                                methodParams,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule device method job: ' + err.message);
        } else {
            monitorJob(methodJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor device method job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
8. <span data-ttu-id="ecc2b-152">Hallo code tooschedule Hallo taak tooupdate Hallo apparaat twin volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="ecc2b-152">Add hello following code tooschedule hello job tooupdate hello device twin:</span></span>
   
    ```
    var twinPatch = {
        etag: '*',
        desired: {
            building: '43',
            floor: 3
        }
    };
   
    var twinJobId = uuid.v4();
   
    console.log('scheduling Twin Update job with id: ' + twinJobId);
    jobClient.scheduleTwinUpdate(twinJobId,
                                queryCondition,
                                twinPatch,
                                startTime,
                                maxExecutionTimeInSeconds,
                                function(err) {
        if (err) {
            console.error('Could not schedule twin update job: ' + err.message);
        } else {
            monitorJob(twinJobId, function(err, result) {
                if (err) {
                    console.error('Could not monitor twin update job: ' + err.message);
                } else {
                    console.log(JSON.stringify(result, null, 2));
                }
            });
        }
    });
    ```
9. <span data-ttu-id="ecc2b-153">Opslaan en sluiten Hallo **scheduleJobService.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="ecc2b-153">Save and close hello **scheduleJobService.js** file.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="ecc2b-154">Hallo-toepassingen uitvoeren</span><span class="sxs-lookup"><span data-stu-id="ecc2b-154">Run hello applications</span></span>
<span data-ttu-id="ecc2b-155">U bent nu klaar toorun Hallo toepassingen.</span><span class="sxs-lookup"><span data-stu-id="ecc2b-155">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="ecc2b-156">Bij de opdrachtprompt Hallo in Hallo **simDevice** map Hallo opdracht toobegin luisteren naar Hallo opnieuw opstarten directe methode te volgen.</span><span class="sxs-lookup"><span data-stu-id="ecc2b-156">At hello command prompt in hello **simDevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node simDevice.js
    ```
2. <span data-ttu-id="ecc2b-157">Bij de opdrachtprompt Hallo in Hallo **scheduleJobService** map Hallo na de opdracht tootrigger Hallo taken toolock Hallo deur en update Hallo twin</span><span class="sxs-lookup"><span data-stu-id="ecc2b-157">At hello command prompt in hello **scheduleJobService** folder, run hello following command tootrigger hello jobs toolock hello door and update hello twin</span></span>
   
    ```
    node scheduleJobService.js
    ```
3. <span data-ttu-id="ecc2b-158">U ziet Hallo apparaat antwoord toohello directe methode in Hallo-console.</span><span class="sxs-lookup"><span data-stu-id="ecc2b-158">You see hello device response toohello direct method in hello console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ecc2b-159">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ecc2b-159">Next steps</span></span>
<span data-ttu-id="ecc2b-160">In deze zelfstudie gebruikt u een taak tooschedule een directe methode tooa apparaat en Hallo bijwerken van de Hallo apparaat dubbele eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="ecc2b-160">In this tutorial, you used a job tooschedule a direct method tooa device and hello update of hello device twin's properties.</span></span>

<span data-ttu-id="ecc2b-161">toocontinue aan de slag met IoT Hub en device management patronen, zoals extern via Hallo lucht firmware-update, Zie:</span><span class="sxs-lookup"><span data-stu-id="ecc2b-161">toocontinue getting started with IoT Hub and device management patterns such as remote over hello air firmware update, see:</span></span>

<span data-ttu-id="ecc2b-162">[Zelfstudie: Hoe toodo een firmware bijwerken][lnk-fwupdate]</span><span class="sxs-lookup"><span data-stu-id="ecc2b-162">[Tutorial: How toodo a firmware update][lnk-fwupdate]</span></span>

<span data-ttu-id="ecc2b-163">aan de slag met IoT Hub toocontinue Zie [aan de slag met Azure IoT rand][lnk-iot-edge].</span><span class="sxs-lookup"><span data-stu-id="ecc2b-163">toocontinue getting started with IoT Hub, see [Getting started with Azure IoT Edge][lnk-iot-edge].</span></span>

[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-props]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-fwupdate]: iot-hub-node-node-firmware-update.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
