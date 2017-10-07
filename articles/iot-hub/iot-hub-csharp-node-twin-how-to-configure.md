---
title: aaaUse Azure IoT Hub twin apparaateigenschappen (.NET/knooppunt) | Microsoft Docs
description: Hoe toouse Azure IoT Hub apparaat horende tooconfigure apparaten. U gebruikt hello Azure IoT-apparaat SDK voor Node.js tooimplement een gesimuleerde apparaattoepassing en hello Azure IoT service SDK voor .NET tooimplement een service-app die de apparaatconfiguratie van een met behulp van een apparaat-twin wijzigt.
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 3c627476-f982-43c9-bd17-e0698c5d236d
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: elioda
ms.openlocfilehash: 840a1b2e45f4763131299577583aa89015dcdd1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices"></a><span data-ttu-id="96142-104">Eigenschappen van de gewenste tooconfigure apparaten gebruiken</span><span class="sxs-lookup"><span data-stu-id="96142-104">Use desired properties tooconfigure devices</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="96142-105">Aan het einde van de Hallo van deze zelfstudie hebt u twee console apps:</span><span class="sxs-lookup"><span data-stu-id="96142-105">At hello end of this tutorial, you will have two console apps:</span></span>

* <span data-ttu-id="96142-106">**SimulateDeviceConfiguration.js**, een gesimuleerde apparaattoepassing die wordt gewacht op een gewenste configuratie-update en rapporten Hallo status van een gesimuleerde configuratieproces voor de update.</span><span class="sxs-lookup"><span data-stu-id="96142-106">**SimulateDeviceConfiguration.js**, a simulated device app that waits for a desired configuration update and reports hello status of a simulated configuration update process.</span></span>
* <span data-ttu-id="96142-107">**SetDesiredConfigurationAndQuery**, een .NET back-end-app, die ingesteld Hallo gewenste configuratie op een apparaat en query's Hallo update configuratieproces.</span><span class="sxs-lookup"><span data-stu-id="96142-107">**SetDesiredConfigurationAndQuery**, a .NET back-end app, which sets hello desired configuration on a device and queries hello configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="96142-108">Hallo artikel [Azure IoT SDK's] [ lnk-hub-sdks] bevat informatie over hello Azure IoT SDK's waarmee u toobuild kunt apparaat- en back-end-apps.</span><span class="sxs-lookup"><span data-stu-id="96142-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="96142-109">toocomplete in deze zelfstudie hebt u Hallo volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="96142-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="96142-110">Visual Studio 2015 of Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="96142-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="96142-111">Node.js versie 0.10.x of hoger.</span><span class="sxs-lookup"><span data-stu-id="96142-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="96142-112">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="96142-112">An active Azure account.</span></span> <span data-ttu-id="96142-113">Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.</span><span class="sxs-lookup"><span data-stu-id="96142-113">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

<span data-ttu-id="96142-114">Als u Hallo gevolgd [aan de slag met apparaat horende] [ lnk-twin-tutorial] zelfstudie, u hebt al een IoT-hub en een apparaat-id genoemd **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="96142-114">If you followed hello [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**.</span></span> <span data-ttu-id="96142-115">In dat geval kunt u overslaan toohello [maken Hallo gesimuleerde apparaattoepassing] [ lnk-how-to-configure-createapp] sectie.</span><span class="sxs-lookup"><span data-stu-id="96142-115">In that case, you can skip toohello [Create hello simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-hello-simulated-device-app"></a><span data-ttu-id="96142-116">Hallo gesimuleerde apparaattoepassing maken</span><span class="sxs-lookup"><span data-stu-id="96142-116">Create hello simulated device app</span></span>
<span data-ttu-id="96142-117">In deze sectie maakt u een Node.js-consoletoepassing die verbinding tooyour hub als maakt **myDeviceId**, wordt gewacht op een gewenste configuratie-update en vervolgens rapporten updates op Hallo gesimuleerde update configuratieproces.</span><span class="sxs-lookup"><span data-stu-id="96142-117">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, waits for a desired configuration update and then reports updates on hello simulated configuration update process.</span></span>

1. <span data-ttu-id="96142-118">Maak een nieuwe lege map genaamd **simulatedeviceconfiguration**.</span><span class="sxs-lookup"><span data-stu-id="96142-118">Create a new empty folder called **simulatedeviceconfiguration**.</span></span> <span data-ttu-id="96142-119">In Hallo **simulatedeviceconfiguration** map, een nieuw package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="96142-119">In hello **simulatedeviceconfiguration** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="96142-120">Accepteer alle Hallo standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="96142-120">Accept all hello defaults.</span></span>
   
    ```
    npm init
    ```
1. <span data-ttu-id="96142-121">Bij de opdrachtprompt in Hallo **simulatedeviceconfiguration** map na de opdracht tooinstall Hallo Hallo **azure-iot-device** en **azure-iot-device-mqtt**pakketten:</span><span class="sxs-lookup"><span data-stu-id="96142-121">At your command prompt in hello **simulatedeviceconfiguration** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. <span data-ttu-id="96142-122">Start een teksteditor en maak een nieuwe **SimulateDeviceConfiguration.js** bestand in Hallo **simulatedeviceconfiguration** map.</span><span class="sxs-lookup"><span data-stu-id="96142-122">Using a text editor, create a new **SimulateDeviceConfiguration.js** file in hello **simulatedeviceconfiguration** folder.</span></span>
1. <span data-ttu-id="96142-123">Hallo na code toohello toevoegen **SimulateDeviceConfiguration.js** -bestand en vervang Hallo **{verbindingsreeks apparaat}** aanduiding voor items met de verbindingsreeks voor Hallo apparaat u hebt gekopieerd wanneer u Hallo gemaakt **myDeviceId** apparaat-id:</span><span class="sxs-lookup"><span data-stu-id="96142-123">Add hello following code toohello **SimulateDeviceConfiguration.js** file, and substitute hello **{device connection string}** placeholder with hello device connection string you copied when you created hello **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="96142-124">Hallo **Client** object beschrijft alle Hallo methoden vereist toointeract met apparaat horende van Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="96142-124">hello **Client** object exposes all hello methods required toointeract with device twins from hello device.</span></span> <span data-ttu-id="96142-125">Deze code initialiseert Hallo **Client** -object is opgehaald Hallo apparaat twin voor **myDeviceId**, en koppelt u een handler voor Hallo update op *gewenst eigenschappen*.</span><span class="sxs-lookup"><span data-stu-id="96142-125">This code initializes hello **Client** object, retrieves hello device twin for **myDeviceId**, and then attaches a handler for hello update on *desired properties*.</span></span> <span data-ttu-id="96142-126">Hallo-handler controleert of dat er een wijzigingsaanvraag voor de huidige configuratie door te vergelijken Hallo configIds is, wordt een methode die de configuratiewijziging Hallo begint roept.</span><span class="sxs-lookup"><span data-stu-id="96142-126">hello handler verifies that there is an actual configuration change request by comparing hello configIds, then invokes a method that starts hello configuration change.</span></span>
   
    <span data-ttu-id="96142-127">Houd er rekening mee dat voor Hallo mogelijk te houden van eenvoud, deze code maakt gebruik van een standaard vastgelegde voor de initiële configuratie Hallo.</span><span class="sxs-lookup"><span data-stu-id="96142-127">Note that for hello sake of simplicity, this code uses a hard-coded default for hello initial configuration.</span></span> <span data-ttu-id="96142-128">Een echte app zou waarschijnlijk dat de configuratie van een lokale opslag laden.</span><span class="sxs-lookup"><span data-stu-id="96142-128">A real app would probably load that configuration from a local storage.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="96142-129">Gewenste eigenschap wijzigingsgebeurtenissen zijn altijd één keer op het apparaatverbinding verzonden.</span><span class="sxs-lookup"><span data-stu-id="96142-129">Desired property change events are always emitted once at device connection.</span></span> <span data-ttu-id="96142-130">Zorg ervoor dat er sprake is van een werkelijke wijziging in Hallo toocheck gewenst eigenschappen voordat u een actie uitvoert.</span><span class="sxs-lookup"><span data-stu-id="96142-130">Make sure toocheck that there is an actual change in hello desired properties before performing any action.</span></span>
   > 
   > 
1. <span data-ttu-id="96142-131">Toevoegen van de volgende methoden voordat Hallo Hallo `client.open()` aanroepen:</span><span class="sxs-lookup"><span data-stu-id="96142-131">Add hello following methods before hello `client.open()` invocation:</span></span>
   
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
   
    <span data-ttu-id="96142-132">Hallo **initConfigChange** methode updates Hallo gerapporteerd eigenschappen op Hallo lokale twin apparaatobject met Hallo configuratie updatestatus aanvraag en sets hello te**in behandeling**, en vervolgens updates Hallo apparaat-twin op Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="96142-132">hello **initConfigChange** method updates hello reported properties on hello local device twin object with hello configuration update request and sets hello status too**Pending**, then updates hello device twin on hello service.</span></span> <span data-ttu-id="96142-133">Nadat Hallo apparaat twin is bijgewerkt, wordt een langdurige proces dat wordt beëindigd bij uitvoering van Hallo gesimuleerd **completeConfigChange**.</span><span class="sxs-lookup"><span data-stu-id="96142-133">After successfully updating hello device twin, it simulates a long running process that terminates in hello execution of **completeConfigChange**.</span></span> <span data-ttu-id="96142-134">Deze methode werkt Hallo gemelde eigenschappen van lokale status hello te stellen**geslaagd** en verwijderen van Hallo **pendingConfig** object.</span><span class="sxs-lookup"><span data-stu-id="96142-134">This method updates hello local reported properties setting hello status too**Success** and removing hello **pendingConfig** object.</span></span> <span data-ttu-id="96142-135">Hallo apparaat twin op Hallo-service wordt vervolgens bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="96142-135">It then updates hello device twin on hello service.</span></span>
   
    <span data-ttu-id="96142-136">Die toosave bandbreedte, gerapporteerd eigenschappen zijn bijgewerkt door te geven alleen Hallo eigenschappen toobe gewijzigd (met de naam **patch** in Hallo bovenstaande code), in plaats van het hele document Hallo vervangen.</span><span class="sxs-lookup"><span data-stu-id="96142-136">Note that, toosave bandwidth, reported properties are updated by specifying only hello properties toobe modified (named **patch** in hello above code), instead of replacing hello whole document.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="96142-137">Deze zelfstudie wordt een gedrag voor updates voor gelijktijdige configuratie niet simuleren.</span><span class="sxs-lookup"><span data-stu-id="96142-137">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="96142-138">Bepaalde configuratie-update-processen mogelijk wijzigingen van de doelconfiguratie kunnen tooaccommodate terwijl Hallo update wordt uitgevoerd, enkele mogelijk tooqueue ze en sommige kan weigeren met een fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="96142-138">Some configuration update processes might be able tooaccommodate changes of target configuration while hello update is running, some might have tooqueue them, and some could reject them with an error condition.</span></span> <span data-ttu-id="96142-139">Zorg ervoor dat tooconsider Hallo gewenste gedrag voor uw specifieke configuratieproces en Hallo juiste logica toevoegen voordat u begint Hallo configuratiewijziging.</span><span class="sxs-lookup"><span data-stu-id="96142-139">Make sure tooconsider hello desired behavior for your specific configuration process, and add hello appropriate logic before initiating hello configuration change.</span></span>
   > 
   > 
1. <span data-ttu-id="96142-140">Hallo apparaattoepassing uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="96142-140">Run hello device app:</span></span>
   
        node SimulateDeviceConfiguration.js
   
    <span data-ttu-id="96142-141">U ziet het Hallo-bericht `retrieved device twin`.</span><span class="sxs-lookup"><span data-stu-id="96142-141">You should see hello message `retrieved device twin`.</span></span> <span data-ttu-id="96142-142">Houd Hallo-app die wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="96142-142">Keep hello app running.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="96142-143">Hallo-service-app maken</span><span class="sxs-lookup"><span data-stu-id="96142-143">Create hello service app</span></span>
<span data-ttu-id="96142-144">In deze sectie maakt u een .NET-consoletoepassing die updates Hallo *gewenst eigenschappen* op Hallo apparaat twin gekoppeld **myDeviceId** met een nieuwe telemetrie configuration-object.</span><span class="sxs-lookup"><span data-stu-id="96142-144">In this section, you will create a .NET console app that updates hello *desired properties* on hello device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="96142-145">Vervolgens vraagt Hallo apparaat horende opgeslagen in Hallo IoT-hub en toont Hallo verschil tussen Hallo gewenst en configuraties van Hallo apparaat gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="96142-145">It then queries hello device twins stored in hello IoT hub and shows hello difference between hello desired and reported configurations of hello device.</span></span>

1. <span data-ttu-id="96142-146">Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toohello huidige oplossing met behulp van Hallo **consoletoepassing** projectsjabloon.</span><span class="sxs-lookup"><span data-stu-id="96142-146">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="96142-147">Naam Hallo project **SetDesiredConfigurationAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="96142-147">Name hello project **SetDesiredConfigurationAndQuery**.</span></span>
   
    ![Nieuw Windows Classic Desktop-project in Visual C#][img-createapp]
1. <span data-ttu-id="96142-149">Klik in Solution Explorer met de rechtermuisknop op Hallo **SetDesiredConfigurationAndQuery** project en klik vervolgens op **NuGet-pakketten beheren...** .</span><span class="sxs-lookup"><span data-stu-id="96142-149">In Solution Explorer, right-click hello **SetDesiredConfigurationAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="96142-150">In Hallo **NuGet Package Manager** Selecteer **Bladeren**, zoeken naar **microsoft.azure.devices**, selecteer **installeren** tooinstall Hallo **Microsoft.Azure.Devices** Inpakken en accepteer de gebruiksvoorwaarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="96142-150">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="96142-151">Deze procedure downloadt, installeert en voegt u een verwijzing toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet-pakket en de bijbehorende afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="96142-151">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Sluit het venster Nuget Package Manager.][img-servicenuget]
1. <span data-ttu-id="96142-153">Voeg de volgende Hallo `using` instructies boven Hallo Hallo **Program.cs** bestand:</span><span class="sxs-lookup"><span data-stu-id="96142-153">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. <span data-ttu-id="96142-154">Hallo na toohello velden toevoegen **programma** klasse.</span><span class="sxs-lookup"><span data-stu-id="96142-154">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="96142-155">Vervang Hallo tijdelijke aanduidingswaarde met IoT Hub-verbindingsreeks voor Hallo-hub die u hebt gemaakt in de vorige sectie Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="96142-155">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="96142-156">Hallo na methode toohello toevoegen **programma** klasse:</span><span class="sxs-lookup"><span data-stu-id="96142-156">Add hello following method toohello **Program** class:</span></span>
   
        static private async Task SetDesiredConfigurationAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch = new {
                    properties = new {
                        desired = new {
                            telemetryConfig = new {
                                configId = Guid.NewGuid().ToString(),
                                sendFrequency = "5m"
                            }
                        }
                    }
                };
   
            await registryManager.UpdateTwinAsync(twin.DeviceId, JsonConvert.SerializeObject(patch), twin.ETag);
            Console.WriteLine("Updated desired configuration");
   
            try
            {
                while (true)
                {
                    var query = registryManager.CreateQuery("SELECT * FROM devices WHERE deviceId = 'myDeviceId'");
                    var results = await query.GetNextAsTwinAsync();
                    foreach (var result in results)
                    {
                        Console.WriteLine("Config report for: {0}", result.DeviceId);
                        Console.WriteLine("Desired telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Desired["telemetryConfig"], Formatting.Indented));
                        Console.WriteLine("Reported telemetryConfig: {0}", JsonConvert.SerializeObject(result.Properties.Reported["telemetryConfig"], Formatting.Indented));
                        Console.WriteLine();
                    }
                    Thread.Sleep(10000);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Exception: {ex.Message}");
            }
        }
   
    <span data-ttu-id="96142-157">Hallo **register** object beschrijft alle Hallo methoden vereist toointeract met apparaat horende van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="96142-157">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="96142-158">Deze code initialiseert Hallo **register** -object is opgehaald Hallo apparaat twin voor **myDeviceId**, en werkt vervolgens de gewenste eigenschappen met een nieuwe telemetrie configuration-object.</span><span class="sxs-lookup"><span data-stu-id="96142-158">This code initializes hello **Registry** object, retrieves hello device twin for **myDeviceId**, and then updates its desired properties with a new telemetry configuration object.</span></span>
    <span data-ttu-id="96142-159">Daarna wordt opgevraagd Hallo apparaat horende opgeslagen in de IoT-hub Hallo elke 10 seconden en afdrukken bestellen Hallo gewenst en telemetrie configuraties gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="96142-159">After that, it queries hello device twins stored in hello IoT hub every 10 seconds, and prints hello desired and reported telemetry configurations.</span></span> <span data-ttu-id="96142-160">Raadpleeg toohello [IoT Hub-querytaal] [ lnk-query] toolearn hoe toogenerate rich op alle apparaten in uw rapporten.</span><span class="sxs-lookup"><span data-stu-id="96142-160">Refer toohello [IoT Hub query language][lnk-query] toolearn how toogenerate rich reports across all your devices.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="96142-161">Deze toepassing een IoT Hub query elke 10 seconden ter illustratie.</span><span class="sxs-lookup"><span data-stu-id="96142-161">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="96142-162">Gebruik een query toogenerate gebruikersgerichte rapporten over veel apparaten, en niet toodetect wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="96142-162">Use queries toogenerate user-facing reports across many devices, and not toodetect changes.</span></span> <span data-ttu-id="96142-163">Als uw oplossing realtime meldingen over apparaatgebeurtenissen vereist, gebruikt u [twin meldingen][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="96142-163">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
   > 
   > 
1. <span data-ttu-id="96142-164">Voeg regels toohello na Hallo **Main** methode:</span><span class="sxs-lookup"><span data-stu-id="96142-164">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery().Wait();
        Console.WriteLine("Press any key tooquit.");
        Console.ReadLine();
1. <span data-ttu-id="96142-165">Open in Solution Explorer hello, Hallo **opstartprojecten instellen...**  en zorg ervoor dat Hallo **actie** voor **SetDesiredConfigurationAndQuery** project **Start**.</span><span class="sxs-lookup"><span data-stu-id="96142-165">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **SetDesiredConfigurationAndQuery** project is **Start**.</span></span> <span data-ttu-id="96142-166">Hallo-oplossing bouwen.</span><span class="sxs-lookup"><span data-stu-id="96142-166">Build hello solution.</span></span>
1. <span data-ttu-id="96142-167">Met **SimulateDeviceConfiguration.js** Hallo .NET-toepassing wordt uitgevoerd, worden uitgevoerd vanuit Visual Studio met **F5** en ziet u Hallo gemelde configuratiewijziging van **geslaagd** te**in behandeling** te**geslaagd** opnieuw met de nieuwe actief Hallo verzenden frequentie van vijf minuten in plaats van 24 uur.</span><span class="sxs-lookup"><span data-stu-id="96142-167">With **SimulateDeviceConfiguration.js** running, run hello .NET application from Visual Studio using **F5** and you should see hello reported configuration change from **Success** too**Pending** too**Success** again with hello new active send frequency of five minutes instead of 24 hours.</span></span>

 ![Apparaten die zijn geconfigureerd][img-deviceconfigured]
   
   > [!IMPORTANT]
   > <span data-ttu-id="96142-169">Er is een vertraging van up tooa minuut tussen Hallo apparaat rapport opnieuw en Hallo queryresultaat.</span><span class="sxs-lookup"><span data-stu-id="96142-169">There is a delay of up tooa minute between hello device report operation and hello query result.</span></span> <span data-ttu-id="96142-170">Dit is tooenable Hallo query infrastructuur toowork op zeer grote schaal.</span><span class="sxs-lookup"><span data-stu-id="96142-170">This is tooenable hello query infrastructure toowork at very high scale.</span></span> <span data-ttu-id="96142-171">tooretrieve consistente weergaven van een enkel apparaat twin gebruiken Hallo **getDeviceTwin** methode in Hallo **register** klasse.</span><span class="sxs-lookup"><span data-stu-id="96142-171">tooretrieve consistent views of a single device twin use hello **getDeviceTwin** method in hello **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="96142-172">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="96142-172">Next steps</span></span>
<span data-ttu-id="96142-173">In deze zelfstudie stelt u een gewenste configuratie als *gewenst eigenschappen* van Hallo oplossing back-end en een apparaat app toodetect die wijzigen en een updateproces van meerdere stappen rapportage van de status ervan via Hallo gerapporteerd simuleren geschreven Eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="96142-173">In this tutorial, you set a desired configuration as *desired properties* from hello solution back end, and wrote a device app toodetect that change and simulate a multi-step update process reporting its status through hello reported properties.</span></span>

<span data-ttu-id="96142-174">Gebruik Hallo resources toolearn hoe volgende aan:</span><span class="sxs-lookup"><span data-stu-id="96142-174">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="96142-175">verzenden van telemetrie vanaf apparaten Hello [aan de slag met IoT Hub] [ lnk-iothub-getstarted] zelfstudie</span><span class="sxs-lookup"><span data-stu-id="96142-175">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="96142-176">plannen of uitvoeren van bewerkingen op grote sets van apparaten Zie Hallo [planning en broadcast taken] [ lnk-schedule-jobs] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="96142-176">schedule or perform operations on large sets of devices see hello [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="96142-177">beheren van apparaten interactief (zoals het inschakelen van een ventilator van een gebruiker beheerde app), met Hallo [direct methoden gebruiken] [ lnk-methods-tutorial] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="96142-177">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-twin-how-to-configure/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-twin-how-to-configure/createnetapp.png
[img-deviceconfigured]: media/iot-hub-csharp-node-twin-how-to-configure/deviceconfigured.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/1.1.0/

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
[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md

[lnk-guid]: https://en.wikipedia.org/wiki/Globally_unique_identifier

[lnk-how-to-configure-createapp]: iot-hub-csharp-node-twin-how-to-configure.md#create-the-simulated-device-app
