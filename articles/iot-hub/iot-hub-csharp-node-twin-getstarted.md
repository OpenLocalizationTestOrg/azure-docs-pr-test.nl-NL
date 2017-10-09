---
title: aaaGet de slag met Azure IoT Hub apparaat horende (.NET/knooppunt) | Microsoft Docs
description: Hoe toouse Azure IoT Hub apparaat horende tooadd tags en gebruik vervolgens een IoT Hub-query. U hello Azure IoT-device SDK voor Node.js tooimplement Hallo gesimuleerde apparaattoepassing en hello Azure IoT service SDK voor .NET tooimplement een service-app die Hallo-labels toegevoegd en Hallo IoT Hub-query wordt uitgevoerd.
services: iot-hub
documentationcenter: node
author: fsautomata
manager: timlt
editor: 
ms.assetid: f7e23b6e-bfde-4fba-a6ec-dbb0f0e005f4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: elioda
ms.openlocfilehash: 1cec082ebddc19c9b87998a5fd0159d32b07acd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-netnode"></a><span data-ttu-id="3f194-104">Aan de slag met apparaat horende (.NET/knooppunt)</span><span class="sxs-lookup"><span data-stu-id="3f194-104">Get started with device twins (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="3f194-105">Aan het einde van de Hallo van deze zelfstudie hebt u een .NET- en Node.js-consoletoepassing:</span><span class="sxs-lookup"><span data-stu-id="3f194-105">At hello end of this tutorial, you will have a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="3f194-106">**AddTagsAndQuery.sln**, een .NET back-end-app, die labels toegevoegd en wordt opgevraagd horende apparaten.</span><span class="sxs-lookup"><span data-stu-id="3f194-106">**AddTagsAndQuery.sln**, a .NET back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="3f194-107">**TwinSimulatedDevice.js**, een Node.js-app dat een apparaat simuleert dat tooyour IoT-hub is verbonden met de apparaat-id Hallo eerder hebt gemaakt, en rapporteert de voorwaarde van de verbinding.</span><span class="sxs-lookup"><span data-stu-id="3f194-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects tooyour IoT hub with hello device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="3f194-108">Hallo artikel [Azure IoT SDK's] [ lnk-hub-sdks] bevat informatie over hello Azure IoT SDK's waarmee u toobuild kunt apparaat- en back-end-apps.</span><span class="sxs-lookup"><span data-stu-id="3f194-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="3f194-109">toocomplete in deze zelfstudie hebt u Hallo volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="3f194-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="3f194-110">Visual Studio 2015 of Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="3f194-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="3f194-111">Node.js versie 0.10.x of hoger.</span><span class="sxs-lookup"><span data-stu-id="3f194-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="3f194-112">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="3f194-112">An active Azure account.</span></span> <span data-ttu-id="3f194-113">(Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)</span><span class="sxs-lookup"><span data-stu-id="3f194-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-hello-service-app"></a><span data-ttu-id="3f194-114">Hallo-service-app maken</span><span class="sxs-lookup"><span data-stu-id="3f194-114">Create hello service app</span></span>
<span data-ttu-id="3f194-115">In deze sectie maakt u een .NET-consoletoepassing maken (met C#) die wordt toegevoegd locatie metagegevens toohello apparaat twin die zijn gekoppeld aan **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="3f194-115">In this section, you create a .NET console app (using C#) that adds location metadata toohello device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="3f194-116">Vervolgens query's Hallo apparaat horende opgeslagen ons in IoT-hub Hallo Hallo apparaten zich in Hallo selecteren en vervolgens Hallo die een mobiele verbinding gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="3f194-116">It then queries hello device twins stored in hello IoT hub selecting hello devices located in hello US, and then hello ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="3f194-117">Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toohello huidige oplossing met behulp van Hallo **consoletoepassing** projectsjabloon.</span><span class="sxs-lookup"><span data-stu-id="3f194-117">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="3f194-118">Naam Hallo project **AddTagsAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="3f194-118">Name hello project **AddTagsAndQuery**.</span></span>
   
    ![Nieuw Windows Classic Desktop-project in Visual C#][img-createapp]
1. <span data-ttu-id="3f194-120">Klik in Solution Explorer met de rechtermuisknop op Hallo **AddTagsAndQuery** project en klik vervolgens op **NuGet-pakketten beheren...** .</span><span class="sxs-lookup"><span data-stu-id="3f194-120">In Solution Explorer, right-click hello **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="3f194-121">In Hallo **NuGet Package Manager** Selecteer **Bladeren** en zoek naar **microsoft.azure.devices**.</span><span class="sxs-lookup"><span data-stu-id="3f194-121">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="3f194-122">Selecteer **installeren** tooinstall hello **Microsoft.Azure.Devices** Inpakken en accepteer de gebruiksvoorwaarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="3f194-122">Select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="3f194-123">Deze procedure downloadt, installeert en voegt u een verwijzing toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet-pakket en de bijbehorende afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="3f194-123">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Sluit het venster Nuget Package Manager.][img-servicenuget]
1. <span data-ttu-id="3f194-125">Voeg de volgende Hallo `using` instructies boven Hallo Hallo **Program.cs** bestand:</span><span class="sxs-lookup"><span data-stu-id="3f194-125">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="3f194-126">Hallo na toohello velden toevoegen **programma** klasse.</span><span class="sxs-lookup"><span data-stu-id="3f194-126">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="3f194-127">Vervang Hallo tijdelijke aanduidingswaarde met IoT Hub-verbindingsreeks voor Hallo-hub die u hebt gemaakt in de vorige sectie Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="3f194-127">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="3f194-128">Hallo na methode toohello toevoegen **programma** klasse:</span><span class="sxs-lookup"><span data-stu-id="3f194-128">Add hello following method toohello **Program** class:</span></span>
   
        public static async Task AddTagsAndQuery()
        {
            var twin = await registryManager.GetTwinAsync("myDeviceId");
            var patch =
                @"{
                    tags: {
                        location: {
                            region: 'US',
                            plant: 'Redmond43'
                        }
                    }
                }";
            await registryManager.UpdateTwinAsync(twin.DeviceId, patch, twin.ETag);
   
            var query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43'", 100);
            var twinsInRedmond43 = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43: {0}", string.Join(", ", twinsInRedmond43.Select(t => t.DeviceId)));
   
            query = registryManager.CreateQuery("SELECT * FROM devices WHERE tags.location.plant = 'Redmond43' AND properties.reported.connectivity.type = 'cellular'", 100);
            var twinsInRedmond43UsingCellular = await query.GetNextAsTwinAsync();
            Console.WriteLine("Devices in Redmond43 using cellular network: {0}", string.Join(", ", twinsInRedmond43UsingCellular.Select(t => t.DeviceId)));
        }
   
    <span data-ttu-id="3f194-129">Hallo **RegistryManager** klasse beschrijft alle Hallo methoden vereist toointeract met apparaat horende van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="3f194-129">hello **RegistryManager** class exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="3f194-130">Hallo vorige code initialiseert eerst Hallo **registryManager** object, en vervolgens haalt Hallo apparaat twin voor **myDeviceId**, en ten slotte de labels bijgewerkt met informatie over de locatie van de gewenste Hallo.</span><span class="sxs-lookup"><span data-stu-id="3f194-130">hello previous code first initializes hello **registryManager** object, then retrieves hello device twin for **myDeviceId**, and finally updates its tags with hello desired location information.</span></span>
   
    <span data-ttu-id="3f194-131">Na het bijwerken, deze twee query's uitvoert: Hallo selecteert eerst alleen Hallo apparaat horende apparaten zich in Hallo **Redmond43** installaties en Hallo tweede verfijning Hallo query tooselect alleen Hallo apparaten die ook zijn verbonden via mobiel netwerk.</span><span class="sxs-lookup"><span data-stu-id="3f194-131">After updating, it executes two queries: hello first selects only hello device twins of devices located in hello **Redmond43** plant, and hello second refines hello query tooselect only hello devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="3f194-132">Houd er rekening mee dat vorige code Hallo bij het maken van Hallo **query** object, geeft u een maximum aantal geretourneerde documenten.</span><span class="sxs-lookup"><span data-stu-id="3f194-132">Note that hello previous code, when it creates hello **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="3f194-133">Hallo **query** object bevat een **HasMoreResults** Boole-eigenschap waarmee u tooinvoke hello kunt **GetNextAsTwinAsync** methoden meerdere keren tooretrieve alle resultaten.</span><span class="sxs-lookup"><span data-stu-id="3f194-133">hello **query** object contains a **HasMoreResults** boolean property that you can use tooinvoke hello **GetNextAsTwinAsync** methods multiple times tooretrieve all results.</span></span> <span data-ttu-id="3f194-134">Een methode aangeroepen **GetNextAsJson** is beschikbaar voor de resultaten die bijvoorbeeld niet apparaat horende zijn resultaten van query's voor aggregatie.</span><span class="sxs-lookup"><span data-stu-id="3f194-134">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="3f194-135">Voeg regels toohello na Hallo **Main** methode:</span><span class="sxs-lookup"><span data-stu-id="3f194-135">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. <span data-ttu-id="3f194-136">Open in Solution Explorer hello, Hallo **opstartprojecten instellen...**  en zorg ervoor dat Hallo **actie** voor **AddTagsAndQuery** project **Start**.</span><span class="sxs-lookup"><span data-stu-id="3f194-136">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="3f194-137">Hallo-oplossing bouwen.</span><span class="sxs-lookup"><span data-stu-id="3f194-137">Build hello solution.</span></span>
1. <span data-ttu-id="3f194-138">Deze toepassing uitvoeren door met de rechtermuisknop op Hallo **AddTagsAndQuery** project en selecteer **Debug**, gevolgd door **nieuw exemplaar gestart**.</span><span class="sxs-lookup"><span data-stu-id="3f194-138">Run this application by right-clicking on hello **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="3f194-139">U ziet één apparaat in Hallo resultaten voor Hallo query vragen voor alle apparaten vinden in **Redmond43** en geen voor de Hallo-query die Hallo beperkt resultaten toodevices die gebruikmaken van een mobiel netwerk.</span><span class="sxs-lookup"><span data-stu-id="3f194-139">You should see one device in hello results for hello query asking for all devices located in **Redmond43** and none for hello query that restricts hello results toodevices that use a cellular network.</span></span>
   
    ![De resultaten van de query-venster][img-addtagapp]

<span data-ttu-id="3f194-141">In de volgende sectie Hallo, maakt u een apparaat-app die Hallo connectiviteit informatie rapporteert en wijzigingen resultaat van query in de vorige sectie Hallo HALLO hallo.</span><span class="sxs-lookup"><span data-stu-id="3f194-141">In hello next section, you create a device app that reports hello connectivity information and changes hello result of hello query in hello previous section.</span></span>

## <a name="create-hello-device-app"></a><span data-ttu-id="3f194-142">Hallo apparaattoepassing maken</span><span class="sxs-lookup"><span data-stu-id="3f194-142">Create hello device app</span></span>
<span data-ttu-id="3f194-143">In deze sectie maakt u een Node.js-consoletoepassing die verbinding tooyour hub als maakt **myDeviceId**, en werkt vervolgens de gerapporteerde toocontain Hallo eigenschapsgegevens dat is verbonden met een mobiel netwerk.</span><span class="sxs-lookup"><span data-stu-id="3f194-143">In this section, you create a Node.js console app that connects tooyour hub as **myDeviceId**, and then updates its reported properties toocontain hello information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="3f194-144">Maak een nieuwe lege map genaamd **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="3f194-144">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="3f194-145">In Hallo **reportconnectivity** map, een nieuw package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="3f194-145">In hello **reportconnectivity** folder, create a new package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="3f194-146">Accepteer alle Hallo standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="3f194-146">Accept all hello defaults.</span></span>
   
    ```
    npm init
    ```
1. <span data-ttu-id="3f194-147">Bij de opdrachtprompt in Hallo **reportconnectivity** map na de opdracht tooinstall Hallo Hallo **azure-iot-device**, en **azure-iot-device-mqtt** pakket :</span><span class="sxs-lookup"><span data-stu-id="3f194-147">At your command prompt in hello **reportconnectivity** folder, run hello following command tooinstall hello **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. <span data-ttu-id="3f194-148">Start een teksteditor en maak een nieuwe **ReportConnectivity.js** bestand in Hallo **reportconnectivity** map.</span><span class="sxs-lookup"><span data-stu-id="3f194-148">Using a text editor, create a new **ReportConnectivity.js** file in hello **reportconnectivity** folder.</span></span>
1. <span data-ttu-id="3f194-149">Hallo na code toohello toevoegen **ReportConnectivity.js** -bestand en vervang Hallo tijdelijke aanduiding voor de verbindingsreeks apparaat Hello een u tijdens het maken van Hallo gekopieerd **myDeviceId** apparaat identiteit:</span><span class="sxs-lookup"><span data-stu-id="3f194-149">Add hello following code toohello **ReportConnectivity.js** file, and substitute hello placeholder for device connection string with hello one you copied when you created hello **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="3f194-150">Hallo **Client** object bevat alle Hallo-methoden die u nodig hebt toointeract met apparaat horende van Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="3f194-150">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="3f194-151">vorige code Hallo nadat het Hallo initialiseert **Client** -object is opgehaald Hallo apparaat twin voor **myDeviceId** en de bijbehorende gemelde eigenschap bijgewerkt met informatie over Hallo-connectiviteit.</span><span class="sxs-lookup"><span data-stu-id="3f194-151">hello previous code, after it initializes hello **Client** object, retrieves hello device twin for **myDeviceId** and updates its reported property with hello connectivity information.</span></span>
1. <span data-ttu-id="3f194-152">Hallo apparaat app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="3f194-152">Run hello device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="3f194-153">U ziet het Hallo-bericht `twin state reported`.</span><span class="sxs-lookup"><span data-stu-id="3f194-153">You should see hello message `twin state reported`.</span></span>
1. <span data-ttu-id="3f194-154">Nu dat hello apparaat de connectiviteit informatie gerapporteerd, moet deze worden weergegeven in beide query's.</span><span class="sxs-lookup"><span data-stu-id="3f194-154">Now that hello device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="3f194-155">Voer Hallo .NET **AddTagsAndQuery** app toorun Hallo query opnieuw.</span><span class="sxs-lookup"><span data-stu-id="3f194-155">Run hello .NET **AddTagsAndQuery** app toorun hello queries again.</span></span> <span data-ttu-id="3f194-156">Deze tijd **myDeviceId** moet worden weergegeven in beide queryresultaten.</span><span class="sxs-lookup"><span data-stu-id="3f194-156">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][img-addtagapp2]

## <a name="next-steps"></a><span data-ttu-id="3f194-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3f194-157">Next steps</span></span>
<span data-ttu-id="3f194-158">In deze zelfstudie maakt u een nieuwe iothub geconfigureerd in hello Azure-portal en vervolgens een apparaat-id in de id-register Hallo iothub hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="3f194-158">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="3f194-159">U metagegevens van apparaten als labels toegevoegd vanuit een back-end-app en een gesimuleerd apparaat app tooreport-apparaatgegevens connectiviteit in Hallo apparaat twin geschreven.</span><span class="sxs-lookup"><span data-stu-id="3f194-159">You added device metadata as tags from a back-end app, and wrote a simulated device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="3f194-160">U hebt ook geleerd hoe tooquery deze informatie Hallo IoT-Hub SQL-achtige query language gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3f194-160">You also learned how tooquery this information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="3f194-161">Gebruik Hallo resources toolearn hoe volgende aan:</span><span class="sxs-lookup"><span data-stu-id="3f194-161">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="3f194-162">verzenden van telemetrie vanaf apparaten Hello [aan de slag met IoT Hub] [ lnk-iothub-getstarted] zelfstudie</span><span class="sxs-lookup"><span data-stu-id="3f194-162">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="3f194-163">apparaten configureren met de gewenste eigenschappen van apparaat twin Hello [gebruik gewenst eigenschappen tooconfigure apparaten] [ lnk-twin-how-to-configure] zelfstudie</span><span class="sxs-lookup"><span data-stu-id="3f194-163">configure devices using device twin's desired properties with hello [Use desired properties tooconfigure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="3f194-164">beheren van apparaten interactief (zoals het inschakelen van een ventilator van een gebruiker beheerde app) met Hallo [direct methoden gebruiken] [ lnk-methods-tutorial] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="3f194-164">control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-node-twin-getstarted/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-node-twin-getstarted/createnetapp.png
[img-addtagapp]: media/iot-hub-csharp-node-twin-getstarted/addtagapp.png
[img-addtagapp2]: media/iot-hub-csharp-node-twin-getstarted/addtagapp2.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-node-node-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-how-to-configure]: iot-hub-csharp-node-twin-how-to-configure.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

