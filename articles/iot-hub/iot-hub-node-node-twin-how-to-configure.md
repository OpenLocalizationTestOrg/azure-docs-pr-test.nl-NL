---
title: Gebruik Azure IoT Hub apparaat twin eigenschappen (knooppunt) | Microsoft Docs
description: Het gebruik van Azure IoT Hub apparaat horende apparaten configureren. U de Azure IoT SDK's voor Node.js gebruiken voor het implementeren van een gesimuleerde apparaattoepassing en een service-app die de apparaatconfiguratie van een met behulp van een apparaat-twin wijzigt.
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
ms.openlocfilehash: 771106ce7b00a5231d9929e4b5ea34aefe693597
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-desired-properties-to-configure-devices-node"></a><span data-ttu-id="6b086-104">Gewenste eigenschappen gebruiken voor het configureren van apparaten (knooppunt)</span><span class="sxs-lookup"><span data-stu-id="6b086-104">Use desired properties to configure devices (Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="6b086-105">Aan het einde van deze zelfstudie hebt u twee console Node.js-apps:</span><span class="sxs-lookup"><span data-stu-id="6b086-105">At the end of this tutorial, you will have two Node.js console apps:</span></span>

* <span data-ttu-id="6b086-106">**SimulateDeviceConfiguration.js**, een gesimuleerde apparaattoepassing die wordt gewacht op een gewenste configuratie-update en rapporteert de status van een gesimuleerde configuratie updateproces.</span><span class="sxs-lookup"><span data-stu-id="6b086-106">**SimulateDeviceConfiguration.js**, a simulated device app that waits for a desired configuration update and reports the status of a simulated configuration update process.</span></span>
* <span data-ttu-id="6b086-107">**SetDesiredConfigurationAndQuery.js**, een Node.js back-end-app, die de gewenste configuratie ingesteld op een apparaat en het configuratieproces van de update-query's.</span><span class="sxs-lookup"><span data-stu-id="6b086-107">**SetDesiredConfigurationAndQuery.js**, a Node.js back-end app, which sets the desired configuration on a device and queries the configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="6b086-108">Het artikel [Azure IoT SDK's] [ lnk-hub-sdks] bevat informatie over de Azure IoT SDK's dat u gebruiken kunt om zowel apparaatgegevens als back-end-apps te bouwen.</span><span class="sxs-lookup"><span data-stu-id="6b086-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="6b086-109">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="6b086-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="6b086-110">Node.js versie 0.10.x of hoger.</span><span class="sxs-lookup"><span data-stu-id="6b086-110">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="6b086-111">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="6b086-111">An active Azure account.</span></span> <span data-ttu-id="6b086-112">(Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)</span><span class="sxs-lookup"><span data-stu-id="6b086-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

<span data-ttu-id="6b086-113">Als u hebt gevolgd de [aan de slag met apparaat horende] [ lnk-twin-tutorial] zelfstudie, u hebt al een IoT-hub en een apparaat-id genoemd **myDeviceId**; en u kunt doorgaan met de [de gesimuleerde apparaattoepassing maken] [ lnk-how-to-configure-createapp] sectie.</span><span class="sxs-lookup"><span data-stu-id="6b086-113">If you followed the [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**; and you can skip to the [Create the simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-the-simulated-device-app"></a><span data-ttu-id="6b086-114">De gesimuleerde apparaattoepassing maken</span><span class="sxs-lookup"><span data-stu-id="6b086-114">Create the simulated device app</span></span>
<span data-ttu-id="6b086-115">In deze sectie maakt u een Node.js-consoletoepassing die is verbonden met uw hub als **myDeviceId**, wordt gewacht op een gewenste configuratie-update en vervolgens rapporten updates op het updateproces gesimuleerde configuratie.</span><span class="sxs-lookup"><span data-stu-id="6b086-115">In this section, you create a Node.js console app that connects to your hub as **myDeviceId**, waits for a desired configuration update and then reports updates on the simulated configuration update process.</span></span>

1. <span data-ttu-id="6b086-116">Maak een nieuwe lege map genaamd **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="6b086-116">Create a new empty folder called **simulatedeviceconfiguration**.</span></span> <span data-ttu-id="6b086-117">In de **simulatedeviceconfiguration** map, maak een nieuw package.json-bestand met de volgende opdracht achter de opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="6b086-117">In the **simulatedeviceconfiguration** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="6b086-118">Accepteer alle standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="6b086-118">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="6b086-119">Bij de opdrachtprompt in de **simulatedeviceconfiguration** map, voer de volgende opdracht voor het installeren van de **azure-iot-device**, en **azure-iot-device-mqtt** pakket:</span><span class="sxs-lookup"><span data-stu-id="6b086-119">At your command prompt in the **simulatedeviceconfiguration** folder, run the following command to install the **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="6b086-120">Start een teksteditor en maak een nieuwe **SimulateDeviceConfiguration.js** bestand de **simulatedeviceconfiguration** map.</span><span class="sxs-lookup"><span data-stu-id="6b086-120">Using a text editor, create a new **SimulateDeviceConfiguration.js** file in the **simulatedeviceconfiguration** folder.</span></span>
4. <span data-ttu-id="6b086-121">Voeg de volgende code naar de **SimulateDeviceConfiguration.js** -bestand en vervang de **{verbindingsreeks apparaat}** tijdelijke aanduiding met de apparaat-verbindingsreeks die u hebt gekopieerd tijdens het maken van de **myDeviceId** apparaat-id:</span><span class="sxs-lookup"><span data-stu-id="6b086-121">Add the following code to the **SimulateDeviceConfiguration.js** file, and substitute the **{device connection string}** placeholder with the device connection string you copied when you created the **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="6b086-122">De **Client** object bevat de methoden die zijn vereist voor interactie met horende apparaten van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="6b086-122">The **Client** object exposes all the methods required to interact with device twins from the device.</span></span> <span data-ttu-id="6b086-123">De vorige code nadat het initialiseren van de **Client** object, haalt de apparaat-twin voor **myDeviceId**, en koppelt u een handler voor de update op de gewenste eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="6b086-123">The previous code, after it initializes the **Client** object, retrieves the device twin for **myDeviceId**, and attaches a handler for the update on desired properties.</span></span> <span data-ttu-id="6b086-124">De handler controleert of dat er een wijzigingsaanvraag voor de huidige configuratie door te vergelijken met de configIds is, wordt een methode die de configuratiewijziging begint aanroept.</span><span class="sxs-lookup"><span data-stu-id="6b086-124">The handler verifies that there is an actual configuration change request by comparing the configIds, then invokes a method that starts the configuration change.</span></span>
   
    <span data-ttu-id="6b086-125">Houd er rekening mee dat omwille van de eenvoud de vorige code gebruikmaakt van een vastgelegde standaard voor de eerste configuratie.</span><span class="sxs-lookup"><span data-stu-id="6b086-125">Note that for the sake of simplicity, the previous code uses a hard-coded default for the inital configuration.</span></span> <span data-ttu-id="6b086-126">Een echte app zou waarschijnlijk dat de configuratie van een lokale opslag laden.</span><span class="sxs-lookup"><span data-stu-id="6b086-126">A real app would probably load that configuration from a local storage.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="6b086-127">Gewenste eigenschap wijzigingsgebeurtenissen altijd één keer worden verzonden op het apparaatverbinding, Controleer of er een werkelijke wijziging in de eigenschappen van de gewenste is voordat u een actie uitvoert.</span><span class="sxs-lookup"><span data-stu-id="6b086-127">Desired property change events are always emitted once at device connection, make sure to check that there is an actual change in the desired properties before performing any action.</span></span>
   > 
   > 
5. <span data-ttu-id="6b086-128">Voeg de volgende methoden voordat de `client.open()` aanroepen:</span><span class="sxs-lookup"><span data-stu-id="6b086-128">Add the following methods before the `client.open()` invocation:</span></span>
   
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
   
    <span data-ttu-id="6b086-129">De **initConfigChange** methode gemelde eigenschappen van het lokale apparaat twin-object wordt bijgewerkt met de configuratie-update-aanvraag en stelt de status op **in behandeling**, werkt u vervolgens de twin apparaat van de service.</span><span class="sxs-lookup"><span data-stu-id="6b086-129">The **initConfigChange** method updates reported properties on the local device twin object with the configuration update request and sets the status to **Pending**, then updates the device twin on the service.</span></span> <span data-ttu-id="6b086-130">Nadat het apparaat twin is bijgewerkt, wordt een langdurige proces dat wordt beëindigd bij de uitvoering van gesimuleerd **completeConfigChange**.</span><span class="sxs-lookup"><span data-stu-id="6b086-130">After successfully updating the device twin, it simulates a long running process that terminates in the execution of **completeConfigChange**.</span></span> <span data-ttu-id="6b086-131">Deze methode werkt u het lokale apparaat-twin gemelde eigenschappen van de status is ingesteld op **geslaagd** en verwijderen van de **pendingConfig** object.</span><span class="sxs-lookup"><span data-stu-id="6b086-131">This method updates the local device twin's reported properties setting the status to **Success** and removing the **pendingConfig** object.</span></span> <span data-ttu-id="6b086-132">De apparaat-twin op de service wordt vervolgens bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="6b086-132">It then updates the device twin on the service.</span></span>
   
    <span data-ttu-id="6b086-133">Dat het, voor het opslaan van bandbreedte, gerapporteerd eigenschappen zijn bijgewerkt door te geven alleen de eigenschappen te wijzigen (met de naam **patch** in de bovenstaande code), in plaats van het hele document vervangen.</span><span class="sxs-lookup"><span data-stu-id="6b086-133">Note that, to save bandwidth, reported properties are updated by specifying only the properties to be modified (named **patch** in the above code), instead of replacing the whole document.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="6b086-134">Deze zelfstudie wordt een gedrag voor updates voor gelijktijdige configuratie niet simuleren.</span><span class="sxs-lookup"><span data-stu-id="6b086-134">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="6b086-135">Bepaalde configuratie-update-processen mogelijk wijzigingen van de doelconfiguratie voor terwijl de update wordt uitgevoerd, anderen mogelijk moet u ze in de wachtrij en anderen met een fout opgetreden weigeren kunnen.</span><span class="sxs-lookup"><span data-stu-id="6b086-135">Some configuration update processes might be able to accommodate changes of target configuration while the update is running, others might have to queue them, and others could reject them with an error condition.</span></span> <span data-ttu-id="6b086-136">Zorg ervoor dat rekening houden met het gewenste gedrag voor uw specifieke configuratie-proces en de juiste logica toevoegen voordat u begint de wijziging in de configuratie.</span><span class="sxs-lookup"><span data-stu-id="6b086-136">Make sure to consider the desired behavior for your specific configuration process, and add the appropriate logic before initiating the configuration change.</span></span>
   > 
   > 
6. <span data-ttu-id="6b086-137">Voer de app voor apparaat:</span><span class="sxs-lookup"><span data-stu-id="6b086-137">Run the device app:</span></span>
   
        node SimulateDeviceConfiguration.js
   
    <span data-ttu-id="6b086-138">U ziet het bericht `retrieved device twin`.</span><span class="sxs-lookup"><span data-stu-id="6b086-138">You should see the message `retrieved device twin`.</span></span> <span data-ttu-id="6b086-139">De app actief houden.</span><span class="sxs-lookup"><span data-stu-id="6b086-139">Keep the app running.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="6b086-140">De service-app maken</span><span class="sxs-lookup"><span data-stu-id="6b086-140">Create the service app</span></span>
<span data-ttu-id="6b086-141">In deze sectie maakt u een Node.js-consoletoepassing die updates de *gewenst eigenschappen* op het apparaat twin gekoppeld **myDeviceId** met een nieuwe telemetrie configuration-object.</span><span class="sxs-lookup"><span data-stu-id="6b086-141">In this section, you will create a Node.js console app that updates the *desired properties* on the device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="6b086-142">Vervolgens zoekt de horende apparaat is opgeslagen in de IoT-hub en ziet u het verschil tussen de gewenste en gerapporteerde configuraties van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="6b086-142">It then queries the device twins stored in the IoT hub and shows the difference between the desired and reported configurations of the device.</span></span>

1. <span data-ttu-id="6b086-143">Maak een nieuwe lege map genaamd **setdesiredandqueryapp**.</span><span class="sxs-lookup"><span data-stu-id="6b086-143">Create a new empty folder called **setdesiredandqueryapp**.</span></span> <span data-ttu-id="6b086-144">In de **setdesiredandqueryapp** map, maak een nieuw package.json-bestand met de volgende opdracht achter de opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="6b086-144">In the **setdesiredandqueryapp** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="6b086-145">Accepteer alle standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="6b086-145">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="6b086-146">Bij de opdrachtprompt in de **setdesiredandqueryapp** map, voer de volgende opdracht voor het installeren van de **azure-iothub** pakket:</span><span class="sxs-lookup"><span data-stu-id="6b086-146">At your command prompt in the **setdesiredandqueryapp** folder, run the following command to install the **azure-iothub** package:</span></span>
   
    ```
    npm install azure-iothub node-uuid --save
    ```
3. <span data-ttu-id="6b086-147">Start een teksteditor en maak een nieuwe **SetDesiredAndQuery.js** bestand de **addtagsandqueryapp** map.</span><span class="sxs-lookup"><span data-stu-id="6b086-147">Using a text editor, create a new **SetDesiredAndQuery.js** file in the **addtagsandqueryapp** folder.</span></span>
4. <span data-ttu-id="6b086-148">Voeg de volgende code naar de **SetDesiredAndQuery.js** -bestand en vervang de **{iot hub verbindingsreeks}** aanduiding voor items met de IoT Hub-verbindingsreeks die u tijdens het maken van uw hub hebt gekopieerd:</span><span class="sxs-lookup"><span data-stu-id="6b086-148">Add the following code to the **SetDesiredAndQuery.js** file, and substitute the **{iot hub connection string}** placeholder with the IoT Hub connection string you copied when you created your hub:</span></span>
   
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

    <span data-ttu-id="6b086-149">De **register** object bevat de methoden die zijn vereist voor interactie met horende apparaten van de service.</span><span class="sxs-lookup"><span data-stu-id="6b086-149">The **Registry** object exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="6b086-150">De vorige code nadat het initialiseren van de **register** object, haalt de apparaat-twin voor **myDeviceId**, en de gewenste eigenschappen bijgewerkt met een nieuwe telemetrie configuration-object.</span><span class="sxs-lookup"><span data-stu-id="6b086-150">The previous code, after it initializes the **Registry** object, retrieves the device twin for **myDeviceId**, and updates its desired properties with a new telemetry configuration object.</span></span> <span data-ttu-id="6b086-151">Daarna roept deze de **queryTwins** werken gebeurtenis 10 seconden.</span><span class="sxs-lookup"><span data-stu-id="6b086-151">After that, it calls the **queryTwins** function event 10 seconds.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="6b086-152">Deze toepassing een IoT Hub query elke 10 seconden ter illustratie.</span><span class="sxs-lookup"><span data-stu-id="6b086-152">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="6b086-153">Met query's gebruikersgerichte om rapporten te genereren over verschillende apparaten en niet voor het detecteren van wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="6b086-153">Use queries to generate user-facing reports across many devices, and not to detect changes.</span></span> <span data-ttu-id="6b086-154">Als uw oplossing realtime meldingen over apparaatgebeurtenissen vereist, gebruikt u [twin meldingen][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="6b086-154">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
    > 
    ><span data-ttu-id="6b086-155">.</span><span class="sxs-lookup"><span data-stu-id="6b086-155">.</span></span>

1. <span data-ttu-id="6b086-156">Voeg de volgende code precies vóór de `registry.getDeviceTwin()` aanroepen voor het implementeren van de **queryTwins** functie:</span><span class="sxs-lookup"><span data-stu-id="6b086-156">Add the following code right before the `registry.getDeviceTwin()` invocation to implement the **queryTwins** function:</span></span>
   
        var queryTwins = function() {
            var query = registry.createQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'", 100);
            query.nextAsTwin(function(err, results) {
                if (err) {
                    console.error('Failed to fetch the results: ' + err.message);
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
   
    <span data-ttu-id="6b086-157">De vorige code query's de horende apparaten opgeslagen in de IoT-hub en de gewenste en gerapporteerde telemetrie-configuraties worden afgedrukt.</span><span class="sxs-lookup"><span data-stu-id="6b086-157">The previous code queries the device twins stored in the IoT hub and prints the desired and reported telemetry configurations.</span></span> <span data-ttu-id="6b086-158">Raadpleeg de [IoT Hub-querytaal] [ lnk-query] voor informatie over het uitgebreide om rapporten te genereren in al uw apparaten.</span><span class="sxs-lookup"><span data-stu-id="6b086-158">Refer to the [IoT Hub query language][lnk-query] to learn how to generate rich reports across all your devices.</span></span>
2. <span data-ttu-id="6b086-159">Met **SimulateDeviceConfiguration.js** wordt uitgevoerd, voert u de toepassing met:</span><span class="sxs-lookup"><span data-stu-id="6b086-159">With **SimulateDeviceConfiguration.js** running, run the application with:</span></span>
   
        node SetDesiredAndQuery.js 5m
   
    <span data-ttu-id="6b086-160">Ziet u de configuratie van de gerapporteerde gewijzigd van **geslaagd** naar **in behandeling** naar **geslaagd** opnieuw met de nieuwe actieve verzenden frequentie van vijf minuten in plaats van 24 uur.</span><span class="sxs-lookup"><span data-stu-id="6b086-160">You should see the reported configuration change from **Success** to **Pending** to **Success** again with the new active send frequency of five minutes instead of 24 hours.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="6b086-161">Er is een vertraging van maximaal een minuut tussen het apparaat rapport opnieuw en het queryresultaat.</span><span class="sxs-lookup"><span data-stu-id="6b086-161">There is a delay of up to a minute between the device report operation and the query result.</span></span> <span data-ttu-id="6b086-162">Dit is het inschakelen van de query-infrastructuur om te werken op zeer grote schaal.</span><span class="sxs-lookup"><span data-stu-id="6b086-162">This is to enable the query infrastructure to work at very high scale.</span></span> <span data-ttu-id="6b086-163">Voor het ophalen van consistente weergaven van een enkel apparaat twin gebruiken de **getDeviceTwin** methode in de **register** klasse.</span><span class="sxs-lookup"><span data-stu-id="6b086-163">To retrieve consistent views of a single device twin use the **getDeviceTwin** method in the **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="6b086-164">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6b086-164">Next steps</span></span>
<span data-ttu-id="6b086-165">In deze zelfstudie stelt u een gewenste configuratie als *gewenst eigenschappen* vanuit een back-end-app en een gesimuleerde apparaattoepassing om te detecteren die wijziging en een updateproces van meerdere stappen zijn status als reporting simuleren geschreven *eigenschappen gerapporteerd* aan de apparaat-twin.</span><span class="sxs-lookup"><span data-stu-id="6b086-165">In this tutorial, you set a desired configuration as *desired properties* from a back-end app, and wrote a simulated device app to detect that change and simulate a multi-step update process reporting its status as *reported properties* to the device twin.</span></span>

<span data-ttu-id="6b086-166">Gebruik de volgende bronnen voor meer informatie over hoe:</span><span class="sxs-lookup"><span data-stu-id="6b086-166">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="6b086-167">verzenden van telemetrie vanaf apparaten met de [aan de slag met IoT Hub] [ lnk-iothub-getstarted] zelfstudie</span><span class="sxs-lookup"><span data-stu-id="6b086-167">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="6b086-168">schema of bewerkingen uitvoeren op grote sets van apparaten, Zie de [planning en broadcast taken] [ lnk-schedule-jobs] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="6b086-168">schedule or perform operations on large sets of devices see the [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="6b086-169">beheren van apparaten interactief (zoals het inschakelen van een ventilator van een gebruiker beheerde app), met de [direct methoden gebruiken] [ lnk-methods-tutorial] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="6b086-169">control devices interactively (such as turning on a fan from a user-controlled app), with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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
