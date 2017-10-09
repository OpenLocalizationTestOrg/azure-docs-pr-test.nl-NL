---
title: aaaDevice firmware-update met Azure IoT Hub (knooppunt) | Microsoft Docs
description: Hoe worden Apparaatbeheer toouse op Azure IoT Hub tooinitiate een apparaatfirmware bijwerken. U gebruikt hello Azure IoT SDK's voor Node.js tooimplement een gesimuleerde apparaattoepassing en een app service waarmee Hallo firmware-update wordt geactiveerd.
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: 70b84258-bc9f-43b1-b7cf-de1bb715f2cf
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/06/2017
ms.author: juanpere
ms.openlocfilehash: 99d4b369e7aba334bf713e0c657e6e5d227fb691
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-device-management-tooinitiate-a-device-firmware-update-nodenode"></a><span data-ttu-id="970cb-104">Device management tooinitiate een apparaat firmware-update (knooppunt/knooppunt) gebruiken</span><span class="sxs-lookup"><span data-stu-id="970cb-104">Use device management tooinitiate a device firmware update (Node/Node)</span></span>
[!INCLUDE [iot-hub-selector-firmware-update](../../includes/iot-hub-selector-firmware-update.md)]

## <a name="introduction"></a><span data-ttu-id="970cb-105">Inleiding</span><span class="sxs-lookup"><span data-stu-id="970cb-105">Introduction</span></span>
<span data-ttu-id="970cb-106">In Hallo [aan de slag met Apparaatbeheer] [ lnk-dm-getstarted] zelfstudie hebt u gezien hoe toouse hello [apparaat twin] [ lnk-devtwin] en [direct methoden] [ lnk-c2dmethod] primitieven tooremotely opnieuw opstarten van een apparaat.</span><span class="sxs-lookup"><span data-stu-id="970cb-106">In hello [Get started with device management][lnk-dm-getstarted] tutorial, you saw how toouse hello [device twin][lnk-devtwin] and [direct methods][lnk-c2dmethod] primitives tooremotely reboot a device.</span></span> <span data-ttu-id="970cb-107">Deze zelfstudie maakt gebruik van dezelfde IoT Hub primitieven Hallo en biedt richtlijnen en ziet u hoe een end-to-end toodo gesimuleerde firmware-update.</span><span class="sxs-lookup"><span data-stu-id="970cb-107">This tutorial uses hello same IoT Hub primitives and provides guidance and shows you how toodo an end-to-end simulated firmware update.</span></span>  <span data-ttu-id="970cb-108">Dit patroon wordt gebruikt in Hallo firmware-update-implementatie voor Hallo Intel Edison apparaat.</span><span class="sxs-lookup"><span data-stu-id="970cb-108">This pattern is used in hello firmware update implementation for hello Intel Edison device sample.</span></span>

<span data-ttu-id="970cb-109">In deze handleiding ontdekt u hoe u:</span><span class="sxs-lookup"><span data-stu-id="970cb-109">This tutorial shows you how to:</span></span>

* <span data-ttu-id="970cb-110">Een Node.js-consoletoepassing die Hallo firmwareUpdate directe methode in Hallo gesimuleerde apparaattoepassing via uw IoT-hub aanroept maken.</span><span class="sxs-lookup"><span data-stu-id="970cb-110">Create a Node.js console app that calls hello firmwareUpdate direct method in hello simulated device app through your IoT hub.</span></span>
* <span data-ttu-id="970cb-111">Maakt een gesimuleerd apparaat-app die u implementeert een **firmwareUpdate** directe methode.</span><span class="sxs-lookup"><span data-stu-id="970cb-111">Create a simulated device app that implements a **firmwareUpdate** direct method.</span></span> <span data-ttu-id="970cb-112">Deze methode initieert een fasen proces dat wordt gewacht toodownload Hallo firmware-image, Hallo firmware afbeelding gedownload en ten slotte is van toepassing hello firmware-image.</span><span class="sxs-lookup"><span data-stu-id="970cb-112">This method initiates a multi-stage process that waits toodownload hello firmware image, downloads hello firmware image, and finally applies hello firmware image.</span></span> <span data-ttu-id="970cb-113">Tijdens elke fase van de update Hallo gerapporteerd Hallo apparaat gebruikt Hallo eigenschappen tooreport op uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="970cb-113">During each stage of hello update, hello device uses hello reported properties tooreport on progress.</span></span>

<span data-ttu-id="970cb-114">Aan het einde van de Hallo van deze zelfstudie hebt u twee console Node.js-apps:</span><span class="sxs-lookup"><span data-stu-id="970cb-114">At hello end of this tutorial, you have two Node.js console apps:</span></span>

<span data-ttu-id="970cb-115">**dmpatterns_fwupdate_service.js**, die een directe methode wordt aangeroepen in de gesimuleerde apparaattoepassing hello, geeft antwoord Hallo en wordt regelmatig (elke 500ms) geeft Hallo bijgewerkt gerapporteerd eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="970cb-115">**dmpatterns_fwupdate_service.js**, which calls a direct method in hello simulated device app, displays hello response, and periodically (every 500ms) displays hello updated reported properties.</span></span>

<span data-ttu-id="970cb-116">**dmpatterns_fwupdate_device.js**, die tooyour IoT-hub is verbonden met de apparaat-id Hallo eerder hebt gemaakt, ontvangen een directe methode firmwareUpdate, wordt uitgevoerd via een toosimulate meerdere proces een firmware-update inclusief: wachten op Hallo afbeelding download downloaden van de nieuwe installatiekopie Hallo en ten slotte Hallo-installatiekopie toe te passen.</span><span class="sxs-lookup"><span data-stu-id="970cb-116">**dmpatterns_fwupdate_device.js**, which connects tooyour IoT hub with hello device identity created earlier, receives a firmwareUpdate direct method, runs through a multi-state process toosimulate a firmware update including: waiting for hello image download, downloading hello new image, and finally applying hello image.</span></span>

<span data-ttu-id="970cb-117">toocomplete in deze zelfstudie, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="970cb-117">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="970cb-118">Node.js-versie 0.12.x of hoger</span><span class="sxs-lookup"><span data-stu-id="970cb-118">Node.js version 0.12.x or later,</span></span> <br/>  <span data-ttu-id="970cb-119">[Uw ontwikkelingsomgeving voorbereiden] [ lnk-dev-setup] wordt beschreven hoe tooinstall Node.js voor deze zelfstudie op Windows of Linux.</span><span class="sxs-lookup"><span data-stu-id="970cb-119">[Prepare your development environment][lnk-dev-setup] describes how tooinstall Node.js for this tutorial on either Windows or Linux.</span></span>
* <span data-ttu-id="970cb-120">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="970cb-120">An active Azure account.</span></span> <span data-ttu-id="970cb-121">(Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)</span><span class="sxs-lookup"><span data-stu-id="970cb-121">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="970cb-122">Ga als volgt Hallo [aan de slag met Apparaatbeheer](iot-hub-node-node-device-management-get-started.md) artikel toocreate uw IoT-hub en uw IoT Hub-verbindingsreeks ophalen.</span><span class="sxs-lookup"><span data-stu-id="970cb-122">Follow hello [Get started with device management](iot-hub-node-node-device-management-get-started.md) article toocreate your IoT hub and get your IoT Hub connection string.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="trigger-a-remote-firmware-update-on-hello-device-using-a-direct-method"></a><span data-ttu-id="970cb-123">Activeren van een externe firmware-update op Hallo-apparaat met een directe methode</span><span class="sxs-lookup"><span data-stu-id="970cb-123">Trigger a remote firmware update on hello device using a direct method</span></span>
<span data-ttu-id="970cb-124">In deze sectie maakt u een Node.js-consoletoepassing die een externe firmware-update op een apparaat start.</span><span class="sxs-lookup"><span data-stu-id="970cb-124">In this section, you create a Node.js console app that initiates a remote firmware update on a device.</span></span> <span data-ttu-id="970cb-125">Hallo app gebruikmaakt van een directe methode tooinitiate Hallo-update en maakt gebruik van apparaat twin query's tooperiodically Hallo status Hallo active firmware-update ophalen.</span><span class="sxs-lookup"><span data-stu-id="970cb-125">hello app uses a direct method tooinitiate hello update and uses device twin queries tooperiodically get hello status of hello active firmware update.</span></span>

1. <span data-ttu-id="970cb-126">Maak een lege map genaamd **triggerfwupdateondevice**.</span><span class="sxs-lookup"><span data-stu-id="970cb-126">Create an empty folder called **triggerfwupdateondevice**.</span></span>  <span data-ttu-id="970cb-127">In Hallo **triggerfwupdateondevice** map, een package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="970cb-127">In hello **triggerfwupdateondevice** folder, create a package.json file using hello following command at your command prompt.</span></span>  <span data-ttu-id="970cb-128">Accepteer alle Hallo standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="970cb-128">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="970cb-129">Bij de opdrachtprompt in Hallo **triggerfwupdateondevice** map na de opdracht tooinstall Hallo Hallo **azure-iot-hub** en **azure-iot-device-mqtt** apparaat SDK-pakketten:</span><span class="sxs-lookup"><span data-stu-id="970cb-129">At your command prompt in hello **triggerfwupdateondevice** folder, run hello following command tooinstall hello **azure-iot-hub** and **azure-iot-device-mqtt** Device SDK packages:</span></span>
   
    ```
    npm install azure-iothub --save
    ```
3. <span data-ttu-id="970cb-130">Maak met een teksteditor, een **dmpatterns_getstarted_service.js** bestand in Hallo **triggerfwupdateondevice** map.</span><span class="sxs-lookup"><span data-stu-id="970cb-130">Using a text editor, create a **dmpatterns_getstarted_service.js** file in hello **triggerfwupdateondevice** folder.</span></span>
4. <span data-ttu-id="970cb-131">Toevoegen van de volgende Hallo 'vereist' instructies toe aan Hallo begin Hallo **dmpatterns_getstarted_service.js** bestand:</span><span class="sxs-lookup"><span data-stu-id="970cb-131">Add hello following 'require' statements at hello start of hello **dmpatterns_getstarted_service.js** file:</span></span>
   
    ```
    'use strict';
   
    var Registry = require('azure-iothub').Registry;
    var Client = require('azure-iothub').Client;
    ```
5. <span data-ttu-id="970cb-132">Hallo na variabelendeclaraties toevoegen en vervang de waarden van de tijdelijke aanduiding Hallo:</span><span class="sxs-lookup"><span data-stu-id="970cb-132">Add hello following variable declarations and replace hello placeholder values:</span></span>
   
    ```
    var connectionString = '{device_connectionstring}';
    var registry = Registry.fromConnectionString(connectionString);
    var client = Client.fromConnectionString(connectionString);
    var deviceToUpdate = 'myDeviceId';
    ```
6. <span data-ttu-id="970cb-133">Hallo volgende toofind werken en Hallo weergavewaarde van Hallo firmwareUpdate toevoegen eigenschap gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="970cb-133">Add hello following function toofind and display hello value of hello firmwareUpdate reported property.</span></span>
   
    ```
    var queryTwinFWUpdateReported = function() {
        registry.getTwin(deviceToUpdate, function(err, twin){
            if (err) {
              console.error('Could not query twins: ' + err.constructor.name + ': ' + err.message);
            } else {
              console.log((JSON.stringify(twin.properties.reported.iothubDM.firmwareUpdate)) + "\n");
            }
        });
    };
    ```
7. <span data-ttu-id="970cb-134">Hallo functie tooinvoke hello firmwareUpdate methode tooreboot Hallo doelapparaat volgende toevoegen:</span><span class="sxs-lookup"><span data-stu-id="970cb-134">Add hello following function tooinvoke hello firmwareUpdate method tooreboot hello target device:</span></span>
   
    ```
    var startFirmwareUpdateDevice = function() {
      var params = {
          fwPackageUri: 'https://secureurl'
      };
   
      var methodName = "firmwareUpdate";
      var payloadData =  JSON.stringify(params);
   
      var methodParams = {
        methodName: methodName,
        payload: payloadData,
        timeoutInSeconds: 30
      };
   
      client.invokeDeviceMethod(deviceToUpdate, methodParams, function(err, result) {
        if (err) {
          console.error('Could not start hello firmware update on hello device: ' + err.message)
        } 
      });
    };
    ```
8. <span data-ttu-id="970cb-135">Ten slotte toevoegen Hallo volgende toocode toostart Hallo firmware-update sequence werken en periodiek weergave Hallo gerapporteerd eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="970cb-135">Finally, Add hello following function toocode toostart hello firmware update sequence and start periodically showing hello reported properties:</span></span>
   
    ```
    startFirmwareUpdateDevice();
    setInterval(queryTwinFWUpdateReported, 500);
    ```
9. <span data-ttu-id="970cb-136">Opslaan en sluiten Hallo **dmpatterns_fwupdate_service.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="970cb-136">Save and close hello **dmpatterns_fwupdate_service.js** file.</span></span>

[!INCLUDE [iot-hub-device-firmware-update](../../includes/iot-hub-device-firmware-update.md)]

## <a name="run-hello-apps"></a><span data-ttu-id="970cb-137">Hallo-apps uitvoeren</span><span class="sxs-lookup"><span data-stu-id="970cb-137">Run hello apps</span></span>
<span data-ttu-id="970cb-138">U bent nu klaar toorun Hallo apps.</span><span class="sxs-lookup"><span data-stu-id="970cb-138">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="970cb-139">Bij de opdrachtprompt Hallo in Hallo **manageddevice** map Hallo opdracht toobegin luisteren naar Hallo opnieuw opstarten directe methode te volgen.</span><span class="sxs-lookup"><span data-stu-id="970cb-139">At hello command prompt in hello **manageddevice** folder, run hello following command toobegin listening for hello reboot direct method.</span></span>
   
    ```
    node dmpatterns_fwupdate_device.js
    ```
2. <span data-ttu-id="970cb-140">Bij de opdrachtprompt Hallo in Hallo **triggerfwupdateondevice** map Hallo opdracht tootrigger Hallo afstand na opnieuw opstarten en query's uitvoeren voor Hallo apparaat twin toofind Hallo laatste keer opnieuw opstarten.</span><span class="sxs-lookup"><span data-stu-id="970cb-140">At hello command prompt in hello **triggerfwupdateondevice** folder, run hello following command tootrigger hello remote reboot and query for hello device twin toofind hello last reboot time.</span></span>
   
    ```
    node dmpatterns_fwupdate_service.js
    ```
3. <span data-ttu-id="970cb-141">U ziet Hallo apparaat antwoord toohello directe methode in Hallo-console.</span><span class="sxs-lookup"><span data-stu-id="970cb-141">You see hello device response toohello direct method in hello console.</span></span>

## <a name="next-steps"></a><span data-ttu-id="970cb-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="970cb-142">Next steps</span></span>
<span data-ttu-id="970cb-143">In deze zelfstudie gebruikt u een directe methode tootrigger een externe firmware-update op een apparaat en de gebruikte Hallo eigenschappen toofollow Hallo voortgang van de firmware-update Hallo gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="970cb-143">In this tutorial, you used a direct method tootrigger a remote firmware update on a device and used hello reported properties toofollow hello progress of hello firmware update.</span></span>

<span data-ttu-id="970cb-144">toolearn hoe tooextend uw IoT-oplossing en schema-methode aanroepen op meerdere apparaten, raadpleegt u Hallo [planning en broadcast taken] [ lnk-tutorial-jobs] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="970cb-144">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

[lnk-devtwin]: iot-hub-devguide-device-twins.md
[lnk-c2dmethod]: iot-hub-devguide-direct-methods.md
[lnk-dm-getstarted]: iot-hub-node-node-device-management-get-started.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/tree/master/doc/node-devbox-setup.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
