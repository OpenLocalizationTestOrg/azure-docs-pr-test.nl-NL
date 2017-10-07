---
title: aaaUse Azure IoT Hub twin apparaateigenschappen (knooppunt) | Microsoft Docs
description: Hoe toouse Azure IoT Hub apparaat horende tooconfigure apparaten. U gebruikt hello Azure IoT SDK's voor Node.js tooimplement een gesimuleerde apparaattoepassing en een service-app die de apparaatconfiguratie van een met behulp van een apparaat-twin wijzigt.
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: d0bcec50-26e6-40f0-8096-733b2f3071ec
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/13/2016
ms.author: elioda
ms.openlocfilehash: 7ebfe2dfa0876bf04fdbaceae55db76456523e8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices-node"></a><span data-ttu-id="7151d-104">Gebruik gewenst eigenschappen tooconfigure apparaten (knooppunt)</span><span class="sxs-lookup"><span data-stu-id="7151d-104">Use desired properties tooconfigure devices (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="7151d-105">Aan het einde van de Hallo van deze zelfstudie hebt u twee console Node.js-apps:</span><span class="sxs-lookup"><span data-stu-id="7151d-105">At hello end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="7151d-106">**SimulateDeviceConfiguration.js**, een gesimuleerde apparaattoepassing die wordt gewacht op een gewenste configuratie-update en rapporten Hallo status van een gesimuleerde configuratieproces voor de update.</span><span class="sxs-lookup"><span data-stu-id="7151d-106">**SimulateDeviceConfiguration.js**, a simulated device app that waits for a desired configuration update and reports hello status of a simulated configuration update process.</span></span>
* <span data-ttu-id="7151d-107">**SetDesiredConfigurationAndQuery.js**, een Node.js back-end-app, die ingesteld Hallo gewenste configuratie op een apparaat en query's Hallo update configuratieproces.</span><span class="sxs-lookup"><span data-stu-id="7151d-107">**SetDesiredConfigurationAndQuery.js**, a Node.js back-end app, which sets hello desired configuration on a device and queries hello configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="7151d-108">Hallo artikel [Azure IoT SDK's] [ lnk-hub-sdks] bevat informatie over hello Azure IoT SDK's waarmee u toobuild kunt apparaat- en back-end-apps.</span><span class="sxs-lookup"><span data-stu-id="7151d-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="7151d-109">toocomplete in deze zelfstudie hebt u Hallo volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="7151d-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="7151d-110">Node.js versie 0.10.x of hoger.</span><span class="sxs-lookup"><span data-stu-id="7151d-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="7151d-111">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="7151d-111">An active Azure account.</span></span> <span data-ttu-id="7151d-112">(Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)</span><span class="sxs-lookup"><span data-stu-id="7151d-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="7151d-113">Als u Hallo gevolgd [aan de slag met apparaat horende] [ lnk-twin-tutorial] zelfstudie, u hebt al een IoT-hub en een apparaat-id genoemd **myDeviceId**; en kunt u toohello overslaan[ Hallo gesimuleerde apparaattoepassing maken] [ lnk-how-to-configure-createapp] sectie.</span><span class="sxs-lookup"><span data-stu-id="7151d-113">If you followed hello [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**; and you can skip toohello [Create hello simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-simulated-device-app"></a><span data-ttu-id="7151d-114">Hallo gesimuleerde apparaattoepassing maken</span><span class="sxs-lookup"><span data-stu-id="7151d-114">Create hello simulated device app</span></span>
<span data-ttu-id="7151d-115">In deze sectie maakt u een Node.js-consoletoepassing die verbinding tooyour hub als maakt **myDeviceId**, wordt gewacht op een gewenste configuratie-update en vervolgens rapporten updates op Hallo gesimuleerde update configuratieproces.</span><span class="sxs-lookup"><span data-stu-id="7151d-115">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, waits for a desired configuration update and then reports updates on hello simulated configuration update process.</span></span>

1. <span data-ttu-id="7151d-116">Maak een nieuwe lege map genaamd **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="7151d-116">Create a new empty folder called **simulatedeviceconfiguration**.</span></span> <span data-ttu-id="7151d-117">In Hallo **simulatedeviceconfiguration** map, een nieuw package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="7151d-117">In hello **simulatedeviceconfiguration** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="7151d-118">Accepteer alle Hallo standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="7151d-118">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="7151d-119">Bij de opdrachtprompt in Hallo **simulatedeviceconfiguration** map na de opdracht tooinstall Hallo Hallo **azure-iot-device**, en **azure-iot-device-mqtt**pakket:</span><span class="sxs-lookup"><span data-stu-id="7151d-119">At your command prompt in hello **simulatedeviceconfiguration** folder, run hello following command tooinstall hello **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="7151d-120">Start een teksteditor en maak een nieuwe **SimulateDeviceConfiguration.js** bestand in Hallo **simulatedeviceconfiguration** map.</span><span class="sxs-lookup"><span data-stu-id="7151d-120">Using a text editor, create a new **SimulateDeviceConfiguration.js** file in hello **simulatedeviceconfiguration** folder.</span></span>
4. <span data-ttu-id="7151d-121">Hallo na code toohello toevoegen **SimulateDeviceConfiguration.js** -bestand en vervang Hallo **{verbindingsreeks apparaat}** aanduiding voor items met de verbindingsreeks voor Hallo apparaat u hebt gekopieerd wanneer u Hallo gemaakt **myDeviceId** apparaat-id:</span><span class="sxs-lookup"><span data-stu-id="7151d-121">Add hello following code toohello **SimulateDeviceConfiguration.js** file, and substitute hello **{device connection string}** placeholder with hello device connection string you copied when you created hello **myDeviceId** device identity:</span></span>
   
        'use strict';
        var Client = require('azure-iot-device').Client;
        var Protocol = require('azure-iot-device-mqtt').Mqtt;
   
        var connectionString = '{device connection string}';
        var client = Client.fromConnectionString(connectionString, Protocol);
   
        client.open(function(err) {
            if (err) {
                console.error('could not open IotHub client');
            } else {
                client.getTwin(function(err, twin) {
                    if (err) {
                        console.error('could not get twin');
                    } else {
                        console.log('retrieved device twin');
                        twin.properties.reported.telemetryConfig = {
                            configId: "0",
                            sendFrequency: "24h"
                        }
                        twin.on('properties.desired', function(desiredChange) {
                            console.log("received change: "+JSON.stringify(desiredChange));
                            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
                            if (desiredChange.telemetryConfig &&desiredChange.telemetryConfig.configId !== currentTelemetryConfig.configId) {
                                initConfigChange(twin);
                            }
                        });
                    }
                });
            }
        });
   
    <span data-ttu-id="7151d-122">Hallo **Client** object beschrijft alle Hallo methoden vereist toointeract met apparaat horende van Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="7151d-122">hello **Client** object exposes all hello methods required toointeract with device twins from hello device.</span></span> <span data-ttu-id="7151d-123">vorige code Hallo nadat het Hallo initialiseert **Client** -object is opgehaald Hallo apparaat twin voor **myDeviceId**, en koppelt u een handler voor Hallo-update op de gewenste eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="7151d-123">hello previous code, after it initializes hello **Client** object, retrieves hello device twin for **myDeviceId**, and attaches a handler for hello update on desired properties.</span></span> <span data-ttu-id="7151d-124">Hallo-handler controleert of dat er een wijzigingsaanvraag voor de huidige configuratie door te vergelijken Hallo configIds is, wordt een methode die de configuratiewijziging Hallo begint roept.</span><span class="sxs-lookup"><span data-stu-id="7151d-124">hello handler verifies that there is an actual configuration change request by comparing hello configIds, then invokes a method that starts hello configuration change.</span></span>
   
    <span data-ttu-id="7151d-125">Houd er rekening mee dat voor Hallo mogelijk te houden van eenvoud, Hallo vorige code een vastgelegde standaardinstallatielocatie voor de initiële configuratie Hallo gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7151d-125">Note that for hello sake of simplicity, hello previous code uses a hard-coded default for hello inital configuration.</span></span> <span data-ttu-id="7151d-126">Een echte app zou waarschijnlijk dat de configuratie van een lokale opslag laden.</span><span class="sxs-lookup"><span data-stu-id="7151d-126">A real app would probably load that configuration from a local storage.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="7151d-127">Gewenste eigenschap wijzigingsgebeurtenissen altijd één keer worden verzonden op het apparaatverbinding en zorg ervoor dat er sprake is van een werkelijke wijziging in Hallo toocheck gewenst eigenschappen voordat u een actie uitvoert.</span><span class="sxs-lookup"><span data-stu-id="7151d-127">Desired property change events are always emitted once at device connection, make sure toocheck that there is an actual change in hello desired properties before performing any action.</span></span>
   > 
   > 
5. <span data-ttu-id="7151d-128">Toevoegen van de volgende methoden voordat Hallo Hallo `client.open()` aanroepen:</span><span class="sxs-lookup"><span data-stu-id="7151d-128">Add hello following methods before hello `client.open()` invocation:</span></span>
   
        var initConfigChange = function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.pendingConfig = twin.properties.desired.telemetryConfig;
            currentTelemetryConfig.status = "Pending";
   
            var patch = {
            telemetryConfig: currentTelemetryConfig
            };
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.log('Could not report properties');
                } else {
                    console.log('Reported pending config change: ' + JSON.stringify(patch));
                    setTimeout(function() {completeConfigChange(twin);}, 60000);
                }
            });
        }
   
        var completeConfigChange =  function(twin) {
            var currentTelemetryConfig = twin.properties.reported.telemetryConfig;
            currentTelemetryConfig.configId = currentTelemetryConfig.pendingConfig.configId;
            currentTelemetryConfig.sendFrequency = currentTelemetryConfig.pendingConfig.sendFrequency;
            currentTelemetryConfig.status = "Success";
            delete currentTelemetryConfig.pendingConfig;
   
            var patch = {
                telemetryConfig: currentTelemetryConfig
            };
            patch.telemetryConfig.pendingConfig = null;
   
            twin.properties.reported.update(patch, function(err) {
                if (err) {
                    console.error('Error reporting properties: ' + err);
                } else {
                    console.log('Reported completed config change: ' + JSON.stringify(patch));
                }
            });
        };
   
    <span data-ttu-id="7151d-129">Hallo **initConfigChange** methode updates gerapporteerd eigenschappen Hallo lokale apparaat twin object met de configuratieaanvraag update Hallo en stelt de status te Hallo**in behandeling**, en vervolgens de updates Hallo apparaat Twin op Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="7151d-129">hello **initConfigChange** method updates reported properties on hello local device twin object with hello configuration update request and sets hello status too**Pending**, then updates hello device twin on hello service.</span></span> <span data-ttu-id="7151d-130">Nadat Hallo apparaat twin is bijgewerkt, wordt een langdurige proces dat wordt beëindigd bij uitvoering van Hallo gesimuleerd **completeConfigChange**.</span><span class="sxs-lookup"><span data-stu-id="7151d-130">After successfully updating hello device twin, it simulates a long running process that terminates in hello execution of **completeConfigChange**.</span></span> <span data-ttu-id="7151d-131">Deze methode updates Hallo lokale apparaat twin de eigenschappen te Hallo status instellen gerapporteerd**geslaagd** en verwijderen van Hallo **pendingConfig** object.</span><span class="sxs-lookup"><span data-stu-id="7151d-131">This method updates hello local device twin's reported properties setting hello status too**Success** and removing hello **pendingConfig** object.</span></span> <span data-ttu-id="7151d-132">Hallo apparaat twin op Hallo-service wordt vervolgens bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="7151d-132">It then updates hello device twin on hello service.</span></span>
   
    <span data-ttu-id="7151d-133">Die toosave bandbreedte, gerapporteerd eigenschappen zijn bijgewerkt door te geven alleen Hallo eigenschappen toobe gewijzigd (met de naam **patch** in Hallo bovenstaande code), in plaats van het hele document Hallo vervangen.</span><span class="sxs-lookup"><span data-stu-id="7151d-133">Note that, toosave bandwidth, reported properties are updated by specifying only hello properties toobe modified (named **patch** in hello above code), instead of replacing hello whole document.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="7151d-134">Deze zelfstudie wordt een gedrag voor updates voor gelijktijdige configuratie niet simuleren.</span><span class="sxs-lookup"><span data-stu-id="7151d-134">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="7151d-135">Bepaalde configuratie-update-processen mogelijk wijzigingen van de doelconfiguratie kunnen tooaccommodate terwijl Hallo update wordt uitgevoerd, anderen mogelijk tooqueue deze en andere kunnen weigeren met een fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="7151d-135">Some configuration update processes might be able tooaccommodate changes of target configuration while hello update is running, others might have tooqueue them, and others could reject them with an error condition.</span></span> <span data-ttu-id="7151d-136">Zorg ervoor dat tooconsider Hallo gewenste gedrag voor uw specifieke configuratieproces en Hallo juiste logica toevoegen voordat u begint Hallo configuratiewijziging.</span><span class="sxs-lookup"><span data-stu-id="7151d-136">Make sure tooconsider hello desired behavior for your specific configuration process, and add hello appropriate logic before initiating hello configuration change.</span></span>
   > 
   > 
6. <span data-ttu-id="7151d-137">Hallo apparaattoepassing uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="7151d-137">Run hello device app:</span></span>
   
        node SimulateDeviceConfiguration.js
   
    <span data-ttu-id="7151d-138">U ziet het Hallo-bericht `retrieved device twin`.</span><span class="sxs-lookup"><span data-stu-id="7151d-138">You should see hello message `retrieved device twin`.</span></span> <span data-ttu-id="7151d-139">Houd Hallo-app die wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="7151d-139">Keep hello app running.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="7151d-140">Hallo-service-app maken</span><span class="sxs-lookup"><span data-stu-id="7151d-140">Create hello service app</span></span>
<span data-ttu-id="7151d-141">In deze sectie maakt u een Node.js-consoletoepassing die updates Hallo *gewenst eigenschappen* op Hallo apparaat twin gekoppeld **myDeviceId** met een nieuwe telemetrie configuration-object.</span><span class="sxs-lookup"><span data-stu-id="7151d-141">In this section, you will create a Node.js console app that updates hello *desired properties* on hello device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="7151d-142">Vervolgens vraagt Hallo apparaat horende opgeslagen in Hallo IoT-hub en toont Hallo verschil tussen Hallo gewenst en configuraties van Hallo apparaat gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="7151d-142">It then queries hello device twins stored in hello IoT hub and shows hello difference between hello desired and reported configurations of hello device.</span></span>

1. <span data-ttu-id="7151d-143">Maak een nieuwe lege map genaamd **setdesiredandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="7151d-143">Create a new empty folder called **setdesiredandqueryapp**.</span></span> <span data-ttu-id="7151d-144">In Hallo **setdesiredandqueryapp** map, een nieuw package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="7151d-144">In hello **setdesiredandqueryapp** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="7151d-145">Accepteer alle Hallo standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="7151d-145">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="7151d-146">Bij de opdrachtprompt in Hallo **setdesiredandqueryapp** map na de opdracht tooinstall Hallo Hallo **azure-iothub** pakket:</span><span class="sxs-lookup"><span data-stu-id="7151d-146">At your command prompt in hello **setdesiredandqueryapp** folder, run hello following command tooinstall hello **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub node-uuid --save
    ```
3. <span data-ttu-id="7151d-147">Start een teksteditor en maak een nieuwe **SetDesiredAndQuery.js** bestand in Hallo **addtagsandqueryapp** map.</span><span class="sxs-lookup"><span data-stu-id="7151d-147">Using a text editor, create a new **SetDesiredAndQuery.js** file in hello **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="7151d-148">Hallo na code toohello toevoegen **SetDesiredAndQuery.js** -bestand en vervang Hallo **{iot hub verbindingsreeks}** aanduiding voor items met Hallo IoT Hub-verbindingsreeks die u tijdens het maken van uw hub gekopieerd :</span><span class="sxs-lookup"><span data-stu-id="7151d-148">Add hello following code toohello **SetDesiredAndQuery.js** file, and substitute hello **{iot hub connection string}** placeholder with hello IoT Hub connection string you copied when you created your hub:</span></span>
   
        'use strict';
        var iothub = require('azure-iothub');
        var uuid = require('node-uuid');
        var connectionString = '{iot hub connection string}';
        var registry = iothub.Registry.fromConnectionString(connectionString);
   
        registry.getTwin('myDeviceId', function(err, twin){
            if (err) {
                console.error(err.constructor.name + ': ' + err.message);
            } else {
                var newConfigId = uuid.v4();
                var newFrequency = process.argv[2] || "5m";
                var patch = {
                    properties: {
                        desired: {
                            telemetryConfig: {
                                configId: newConfigId,
                                sendFrequency: newFrequency
                            }
                        }
                    }
                }
                twin.update(patch, function(err) {
                    if (err) {
                        console.error('Could not update twin: ' + err.constructor.name + ': ' + err.message);
                    } else {
                        console.log(twin.deviceId + ' twin updated successfully');
                    }
                });
                setInterval(queryTwins, 10000);
            }
        });

    <span data-ttu-id="7151d-149">Hallo **register** object beschrijft alle Hallo methoden vereist toointeract met apparaat horende van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="7151d-149">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="7151d-150">vorige code Hallo nadat het Hallo initialiseert **register** -object is opgehaald Hallo apparaat twin voor **myDeviceId**, en de gewenste eigenschappen bijgewerkt met een nieuwe telemetrie configuration-object.</span><span class="sxs-lookup"><span data-stu-id="7151d-150">hello previous code, after it initializes hello **Registry** object, retrieves hello device twin for **myDeviceId**, and updates its desired properties with a new telemetry configuration object.</span></span> <span data-ttu-id="7151d-151">Daarna roept Hallo **queryTwins** werken gebeurtenis 10 seconden.</span><span class="sxs-lookup"><span data-stu-id="7151d-151">After that, it calls hello **queryTwins** function event 10 seconds.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="7151d-152">Deze toepassing een IoT Hub query elke 10 seconden ter illustratie.</span><span class="sxs-lookup"><span data-stu-id="7151d-152">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="7151d-153">Gebruik een query toogenerate gebruikersgerichte rapporten over veel apparaten, en niet toodetect wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="7151d-153">Use queries toogenerate user-facing reports across many devices, and not toodetect changes.</span></span> <span data-ttu-id="7151d-154">Als uw oplossing realtime meldingen over apparaatgebeurtenissen vereist, gebruikt u [twin meldingen][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="7151d-154">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
    > 
    ><span data-ttu-id="7151d-155">.</span><span class="sxs-lookup"><span data-stu-id="7151d-155">.</span></span>

1. <span data-ttu-id="7151d-156">Toevoegen van de volgende code precies vóór Hallo Hallo `registry.getDeviceTwin()` aanroep tooimplement hello **queryTwins** functie:</span><span class="sxs-lookup"><span data-stu-id="7151d-156">Add hello following code right before hello `registry.getDeviceTwin()` invocation tooimplement hello **queryTwins** function:</span></span>
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed toofetch hello results: ' + err.message);
                } else {
                    console.log();
                    results.forEach(function(twin) {
                        var desiredConfig = twin.properties.desired.telemetryConfig;
                        var reportedConfig = twin.properties.reported.telemetryConfig;
                        console.log("Config report for: " + twin.deviceId);
                        console.log("Desired: ");
                        console.log(JSON.stringify(desiredConfig, null, 2));
                        console.log("Reported: ");
                        console.log(JSON.stringify(reportedConfig, null, 2));
                    });
                }
            });
        };
   
    <span data-ttu-id="7151d-157">Hallo vorige code query's Hallo apparaat horende opgeslagen in Hallo IoT-hub en afdrukken bestellen Hallo gewenst en telemetrie configuraties gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="7151d-157">hello previous code queries hello device twins stored in hello IoT hub and prints hello desired and reported telemetry configurations.</span></span> <span data-ttu-id="7151d-158">Raadpleeg toohello [IoT Hub-querytaal] [ lnk-query] toolearn hoe toogenerate rich op alle apparaten in uw rapporten.</span><span class="sxs-lookup"><span data-stu-id="7151d-158">Refer toohello [IoT Hub query language][lnk-query] toolearn how toogenerate rich reports across all your devices.</span></span>
2. <span data-ttu-id="7151d-159">Met **SimulateDeviceConfiguration.js** toepassing hello met wordt uitgevoerd, worden uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="7151d-159">With **SimulateDeviceConfiguration.js** running, run hello application with:</span></span>
   
        node SetDesiredAndQuery.js 5m
   
    <span data-ttu-id="7151d-160">Er is gemeld Hallo-configuratie wijzigen vanuit **geslaagd** te**in behandeling** te**geslaagd** opnieuw met de nieuwe actief Hallo verzenden frequentie van vijf minuten in plaats van 24 uren.</span><span class="sxs-lookup"><span data-stu-id="7151d-160">You should see hello reported configuration change from **Success** too**Pending** too**Success** again with hello new active send frequency of five minutes instead of 24 hours.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="7151d-161">Er is een vertraging van up tooa minuut tussen Hallo apparaat rapport opnieuw en Hallo queryresultaat.</span><span class="sxs-lookup"><span data-stu-id="7151d-161">There is a delay of up tooa minute between hello device report operation and hello query result.</span></span> <span data-ttu-id="7151d-162">Dit is tooenable Hallo query infrastructuur toowork op zeer grote schaal.</span><span class="sxs-lookup"><span data-stu-id="7151d-162">This is tooenable hello query infrastructure toowork at very high scale.</span></span> <span data-ttu-id="7151d-163">tooretrieve consistente weergaven van een enkel apparaat twin gebruiken Hallo **getDeviceTwin** methode in Hallo **register** klasse.</span><span class="sxs-lookup"><span data-stu-id="7151d-163">tooretrieve consistent views of a single device twin use hello **getDeviceTwin** method in hello **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="7151d-164">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7151d-164">Next steps</span></span>
<span data-ttu-id="7151d-165">In deze zelfstudie stelt u een gewenste configuratie als *gewenst eigenschappen* vanuit een back-end-app en een gesimuleerd apparaat app toodetect die wijzigen en een updateproces van meerdere stappen zijn status als reporting simuleren geschreven  *Eigenschappen gerapporteerd* toohello apparaat twin.</span><span class="sxs-lookup"><span data-stu-id="7151d-165">In this tutorial, you set a desired configuration as *desired properties* from a back-end app, and wrote a simulated device app toodetect that change and simulate a multi-step update process reporting its status as *reported properties* toohello device twin.</span></span>

<span data-ttu-id="7151d-166">Gebruik Hallo resources toolearn hoe volgende aan:</span><span class="sxs-lookup"><span data-stu-id="7151d-166">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="7151d-167">verzenden van telemetrie vanaf apparaten Hello [aan de slag met IoT Hub] [ lnk-iothub-getstarted] zelfstudie</span><span class="sxs-lookup"><span data-stu-id="7151d-167">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="7151d-168">plannen of uitvoeren van bewerkingen op grote sets van apparaten Zie Hallo [planning en broadcast taken] [ lnk-schedule-jobs] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="7151d-168">schedule or perform operations on large sets of devices see hello [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="7151d-169">beheren van apparaten interactief (zoals het inschakelen van een ventilator van een gebruiker beheerde app), met Hallo [direct methoden gebruiken] [ lnk-methods-tutorial] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="7151d-169">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-dm-overview]: iot-hub-device-management-overview.md
[lnk-twin-tutorial]: iot-hub-node-node-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-node-node-twin-how-to-configure.md#create-the-simulated-device-app
