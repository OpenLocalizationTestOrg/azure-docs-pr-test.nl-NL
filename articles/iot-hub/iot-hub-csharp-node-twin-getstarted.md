---
title: Aan de slag met Azure IoT Hub apparaat horende (.NET/knooppunt) | Microsoft Docs
description: Het gebruik van Azure IoT Hub apparaat horende labels toevoegen en vervolgens met de query voor een IoT Hub. U het apparaat met Azure IoT SDK voor Node.js gebruiken voor het implementeren van de gesimuleerde apparaattoepassing en de Azure IoT service SDK voor .NET voor het implementeren van een service-app die de labels worden toegevoegd en de IoT Hub-query wordt uitgevoerd.
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
ms.openlocfilehash: 07797b9159c9b926e9eb47d8864c63048951931a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-device-twins-netnode"></a><span data-ttu-id="2e1fd-104">Aan de slag met apparaat horende (.NET/knooppunt)</span><span class="sxs-lookup"><span data-stu-id="2e1fd-104">Get started with device twins (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="2e1fd-105">Aan het einde van deze zelfstudie hebt u een .NET- en Node.js-consoletoepassing:</span><span class="sxs-lookup"><span data-stu-id="2e1fd-105">At the end of this tutorial, you will have a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="2e1fd-106">**AddTagsAndQuery.sln**, een .NET back-end-app, die labels toegevoegd en wordt opgevraagd horende apparaten.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-106">**AddTagsAndQuery.sln**, a .NET back-end app, which adds tags and queries device twins.</span></span>
* <span data-ttu-id="2e1fd-107">**TwinSimulatedDevice.js**, een Node.js-app dat een apparaat simuleert dat verbinding met uw IoT-hub aan de apparaat-id eerder hebt gemaakt maakt, en rapporteert de voorwaarde van de verbinding.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-107">**TwinSimulatedDevice.js**, a Node.js app which simulates a device that connects to your IoT hub with the device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="2e1fd-108">Het artikel [Azure IoT SDK's] [ lnk-hub-sdks] bevat informatie over de Azure IoT SDK's dat u gebruiken kunt om zowel apparaatgegevens als back-end-apps te bouwen.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="2e1fd-109">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="2e1fd-109">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="2e1fd-110">Visual Studio 2015 of Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="2e1fd-111">Node.js versie 0.10.x of hoger.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="2e1fd-112">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-112">An active Azure account.</span></span> <span data-ttu-id="2e1fd-113">(Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)</span><span class="sxs-lookup"><span data-stu-id="2e1fd-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-the-service-app"></a><span data-ttu-id="2e1fd-114">De service-app maken</span><span class="sxs-lookup"><span data-stu-id="2e1fd-114">Create the service app</span></span>
<span data-ttu-id="2e1fd-115">In deze sectie maakt u een .NET-consoletoepassing maken (met C#) waarmee de metagegevens van de locatie wordt toegevoegd aan de apparaat-twin gekoppeld **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-115">In this section, you create a .NET console app (using C#) that adds location metadata to the device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="2e1fd-116">Deze vervolgens het apparaat horende opgeslagen in de IoT-hub te selecteren van de apparaten die zich in de Verenigde Staten en de waarden die gerapporteerd van een mobiele verbinding een query.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-116">It then queries the device twins stored in the IoT hub selecting the devices located in the US, and then the ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="2e1fd-117">Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toe aan de huidige oplossing met behulp van de projectsjabloon **Console Application**.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-117">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="2e1fd-118">Noem het project **AddTagsAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-118">Name the project **AddTagsAndQuery**.</span></span>
   
    ![Nieuw Windows Classic Desktop-project in Visual C#][img-createapp]
1. <span data-ttu-id="2e1fd-120">Klik in Solution Explorer met de rechtermuisknop op de **AddTagsAndQuery** project en klik vervolgens op **NuGet-pakketten beheren...** .</span><span class="sxs-lookup"><span data-stu-id="2e1fd-120">In Solution Explorer, right-click the **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="2e1fd-121">In de **NuGet Package Manager** Selecteer **Bladeren** en zoek naar **microsoft.azure.devices**.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-121">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="2e1fd-122">Selecteer **installeren** voor het installeren van de **Microsoft.Azure.Devices** Inpakken en accepteer de gebruiksvoorwaarden.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-122">Select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="2e1fd-123">Met deze procedure worden de [Azure IoT-service-SDK][lnk-nuget-service-sdk], het NuGet-pakket en de bijbehorende afhankelijkheden gedownload en geïnstalleerd. Ook worden verwijzingen hiernaar toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-123">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Sluit het venster Nuget Package Manager.][img-servicenuget]
1. <span data-ttu-id="2e1fd-125">Voeg aan het begin van het bestand **Program.cs** de volgende `using` instructies toe:</span><span class="sxs-lookup"><span data-stu-id="2e1fd-125">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="2e1fd-126">Voeg de volgende velden toe aan de klasse **Program**:</span><span class="sxs-lookup"><span data-stu-id="2e1fd-126">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="2e1fd-127">Vervang de tijdelijke aanduidingswaarde met de IoT Hub-verbindingsreeks voor de hub die u hebt gemaakt in de vorige sectie.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-127">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="2e1fd-128">Voeg de volgende methode toe aan de klasse **Program**:</span><span class="sxs-lookup"><span data-stu-id="2e1fd-128">Add the following method to the **Program** class:</span></span>
   
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
   
    <span data-ttu-id="2e1fd-129">De **RegistryManager** klasse bevat alle methoden die zijn vereist voor interactie met horende apparaten van de service.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-129">The **RegistryManager** class exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="2e1fd-130">De vorige code eerst initialiseert de **registryManager** object en vervolgens haalt de apparaat-twin voor **myDeviceId**, en ten slotte de labels bijgewerkt met informatie over de gewenste locatie.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-130">The previous code first initializes the **registryManager** object, then retrieves the device twin for **myDeviceId**, and finally updates its tags with the desired location information.</span></span>
   
    <span data-ttu-id="2e1fd-131">Na het bijwerken, deze twee query's uitvoert: de eerste selecteert alleen de apparaat-horende apparaten zich in de **Redmond43** plant en de tweede verfijning de query voor het selecteren van alleen de apparaten die ook via het mobiele netwerk zijn verbonden.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-131">After updating, it executes two queries: the first selects only the device twins of devices located in the **Redmond43** plant, and the second refines the query to select only the devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="2e1fd-132">Houd er rekening mee dat de vorige code bij het maken van de **query** object, geeft u een maximum aantal geretourneerde documenten.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-132">Note that the previous code, when it creates the **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="2e1fd-133">De **query** object bevat een **HasMoreResults** Boole-eigenschap die u gebruiken kunt om aan te roepen de **GetNextAsTwinAsync** methoden meerdere keren voor het ophalen van alle resultaten.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-133">The **query** object contains a **HasMoreResults** boolean property that you can use to invoke the **GetNextAsTwinAsync** methods multiple times to retrieve all results.</span></span> <span data-ttu-id="2e1fd-134">Een methode aangeroepen **GetNextAsJson** is beschikbaar voor de resultaten die bijvoorbeeld niet apparaat horende zijn resultaten van query's voor aggregatie.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-134">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="2e1fd-135">Voeg tot slot de volgende regels toe aan de methode **Main**:</span><span class="sxs-lookup"><span data-stu-id="2e1fd-135">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

1. <span data-ttu-id="2e1fd-136">Open in Solution Explorer de **opstartprojecten instellen...**  en zorg ervoor dat de **actie** voor **AddTagsAndQuery** project **Start**.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-136">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="2e1fd-137">De oplossing bouwen.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-137">Build the solution.</span></span>
1. <span data-ttu-id="2e1fd-138">Deze toepassing uitvoeren door met de rechtermuisknop op de **AddTagsAndQuery** project en selecteer **Debug**, gevolgd door **nieuw exemplaar gestart**.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-138">Run this application by right-clicking on the **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="2e1fd-139">U ziet één apparaat in de resultaten van de query wordt gevraagd voor alle apparaten vinden in **Redmond43** en er is geen voor de query die de resultaten beperkt tot apparaten die gebruikmaken van een mobiel netwerk.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-139">You should see one device in the results for the query asking for all devices located in **Redmond43** and none for the query that restricts the results to devices that use a cellular network.</span></span>
   
    ![De resultaten van de query-venster][img-addtagapp]

<span data-ttu-id="2e1fd-141">In de volgende sectie maakt u een apparaat-app die rapporten de informatie over de connectiviteit en het resultaat van de query in de vorige sectie wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-141">In the next section, you create a device app that reports the connectivity information and changes the result of the query in the previous section.</span></span>

## <a name="create-the-device-app"></a><span data-ttu-id="2e1fd-142">De apparaat-app maken</span><span class="sxs-lookup"><span data-stu-id="2e1fd-142">Create the device app</span></span>
<span data-ttu-id="2e1fd-143">In deze sectie maakt u een Node.js-consoletoepassing die is verbonden met uw hub als **myDeviceId**, en werkt vervolgens de gerapporteerde eigenschappen bevatten informatie die is verbonden met een mobiel netwerk.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-143">In this section, you create a Node.js console app that connects to your hub as **myDeviceId**, and then updates its reported properties to contain the information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="2e1fd-144">Maak een nieuwe lege map genaamd **reportconnectivity**.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-144">Create a new empty folder called **reportconnectivity**.</span></span> <span data-ttu-id="2e1fd-145">In de **reportconnectivity** map, maak een nieuw package.json-bestand met de volgende opdracht achter de opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-145">In the **reportconnectivity** folder, create a new package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="2e1fd-146">Accepteer alle standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-146">Accept all the defaults.</span></span>
   
    ```
    npm init
    ```
1. <span data-ttu-id="2e1fd-147">Bij de opdrachtprompt in de **reportconnectivity** map, voer de volgende opdracht voor het installeren van de **azure-iot-device**, en **azure-iot-device-mqtt** pakket:</span><span class="sxs-lookup"><span data-stu-id="2e1fd-147">At your command prompt in the **reportconnectivity** folder, run the following command to install the **azure-iot-device**, and **azure-iot-device-mqtt** package:</span></span>
   
    ```
    npm install azure-iot-device azure-iot-device-mqtt --save
    ```
1. <span data-ttu-id="2e1fd-148">Start een teksteditor en maak een nieuwe **ReportConnectivity.js** bestand de **reportconnectivity** map.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-148">Using a text editor, create a new **ReportConnectivity.js** file in the **reportconnectivity** folder.</span></span>
1. <span data-ttu-id="2e1fd-149">Voeg de volgende code naar de **ReportConnectivity.js** -bestand en vervang de tijdelijke aanduiding voor de verbindingsreeks apparaat met de categorie die u hebt gekopieerd tijdens het maken van de **myDeviceId** apparaat-id:</span><span class="sxs-lookup"><span data-stu-id="2e1fd-149">Add the following code to the **ReportConnectivity.js** file, and substitute the placeholder for device connection string with the one you copied when you created the **myDeviceId** device identity:</span></span>
   
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
   
    <span data-ttu-id="2e1fd-150">De **Client** object bevat de methoden die u nodig hebt om te communiceren met horende apparaten van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-150">The **Client** object exposes all the methods you require to interact with device twins from the device.</span></span> <span data-ttu-id="2e1fd-151">De vorige code nadat het initialiseren van de **Client** object, haalt de apparaat-twin voor **myDeviceId** en de bijbehorende eigenschap gerapporteerde verbindingsgegevens bijgewerkt door de.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-151">The previous code, after it initializes the **Client** object, retrieves the device twin for **myDeviceId** and updates its reported property with the connectivity information.</span></span>
1. <span data-ttu-id="2e1fd-152">De apparaat-app uitvoeren</span><span class="sxs-lookup"><span data-stu-id="2e1fd-152">Run the device app</span></span>
   
        node ReportConnectivity.js
   
    <span data-ttu-id="2e1fd-153">U ziet het bericht `twin state reported`.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-153">You should see the message `twin state reported`.</span></span>
1. <span data-ttu-id="2e1fd-154">Nu dat het apparaat heeft gemeld dat de gegevens over de connectiviteit, moet deze worden weergegeven in beide query's.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-154">Now that the device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="2e1fd-155">Uitvoeren van de .NET **AddTagsAndQuery** app opnieuw uit te voeren de query's.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-155">Run the .NET **AddTagsAndQuery** app to run the queries again.</span></span> <span data-ttu-id="2e1fd-156">Deze tijd **myDeviceId** moet worden weergegeven in beide queryresultaten.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-156">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![][img-addtagapp2]

## <a name="next-steps"></a><span data-ttu-id="2e1fd-157">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2e1fd-157">Next steps</span></span>
<span data-ttu-id="2e1fd-158">In deze handleiding hebt u een nieuwe IoT-hub geconfigureerd in Azure Portal en vervolgens een apparaat-id gemaakt in het id-register van de IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-158">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="2e1fd-159">U metagegevens van apparaten als labels toegevoegd vanuit een back-end-app en een gesimuleerde apparaattoepassing geschreven naar apparaten connectiviteit rapportgegevens in de apparaat-twin.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-159">You added device metadata as tags from a back-end app, and wrote a simulated device app to report device connectivity information in the device twin.</span></span> <span data-ttu-id="2e1fd-160">Ook hebt u geleerd hoe deze gegevens met behulp van de SQL-achtige IoT Hub-querytaal opvragen.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-160">You also learned how to query this information using the SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="2e1fd-161">Gebruik de volgende bronnen voor meer informatie over hoe:</span><span class="sxs-lookup"><span data-stu-id="2e1fd-161">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="2e1fd-162">verzenden van telemetrie vanaf apparaten met de [aan de slag met IoT Hub] [ lnk-iothub-getstarted] zelfstudie</span><span class="sxs-lookup"><span data-stu-id="2e1fd-162">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="2e1fd-163">apparaten configureren met de gewenste eigenschappen van apparaat twin met de [gebruik gewenst eigenschappen voor het configureren van apparaten] [ lnk-twin-how-to-configure] zelfstudie</span><span class="sxs-lookup"><span data-stu-id="2e1fd-163">configure devices using device twin's desired properties with the [Use desired properties to configure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="2e1fd-164">beheren van apparaten interactief (zoals het inschakelen van een ventilator van een gebruiker beheerde app) met de [direct methoden gebruiken] [ lnk-methods-tutorial] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="2e1fd-164">control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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

