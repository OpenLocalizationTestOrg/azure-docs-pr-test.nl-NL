---
title: Aan de slag met Azure IoT Hub apparaat horende (.NET/.NET) | Microsoft Docs
description: Het gebruik van Azure IoT Hub apparaat horende labels toevoegen en vervolgens met de query voor een IoT Hub. U het apparaat met Azure IoT SDK voor .NET gebruiken voor het implementeren van de gesimuleerde apparaattoepassing en de Azure IoT service SDK voor .NET voor het implementeren van een service-app die de labels worden toegevoegd en de IoT Hub-query wordt uitgevoerd.
services: iot-hub
documentationcenter: node
author: dsk-2015
manager: timlt
editor: 
ms.assetid: f7e23b6e-bfde-4fba-a6ec-dbb0f0e005f4
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/15/2017
ms.author: dkshir
ms.openlocfilehash: 6073d594117e69676b753a1e3af25fffa3583a2b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-device-twins-netnet"></a><span data-ttu-id="6d63b-104">Aan de slag met apparaat horende (.NET/.NET)</span><span class="sxs-lookup"><span data-stu-id="6d63b-104">Get started with device twins (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="6d63b-105">Aan het einde van deze zelfstudie hebt u deze apps van .NET-console:</span><span class="sxs-lookup"><span data-stu-id="6d63b-105">At the end of this tutorial, you will have these .NET console apps:</span></span>

* <span data-ttu-id="6d63b-106">**CreateDeviceIdentity**, een .NET-app die u maakt een apparaat-id en de bijbehorende beveiligingssleutel waarmee uw gesimuleerde apparaat app verbinden.</span><span class="sxs-lookup"><span data-stu-id="6d63b-106">**CreateDeviceIdentity**, a .NET app which creates a device identity and associated security key to connect your simulated device app.</span></span>
* <span data-ttu-id="6d63b-107">**AddTagsAndQuery**, een .NET-back-end-app die labels toegevoegd en wordt opgevraagd horende apparaten.</span><span class="sxs-lookup"><span data-stu-id="6d63b-107">**AddTagsAndQuery**, a .NET back-end app which adds tags and queries device twins.</span></span>
* <span data-ttu-id="6d63b-108">**ReportConnectivity**, een .NET-apparaattoepassing dat een apparaat simuleert dat verbinding met uw IoT-hub aan de apparaat-id eerder hebt gemaakt maakt, en rapporteert de voorwaarde van de verbinding.</span><span class="sxs-lookup"><span data-stu-id="6d63b-108">**ReportConnectivity**, a .NET device app which simulates a device that connects to your IoT hub with the device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="6d63b-109">Het artikel [Azure IoT SDK's] [ lnk-hub-sdks] bevat informatie over de Azure IoT SDK's dat u gebruiken kunt om zowel apparaatgegevens als back-end-apps te bouwen.</span><span class="sxs-lookup"><span data-stu-id="6d63b-109">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="6d63b-110">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="6d63b-110">To complete this tutorial you need the following:</span></span>

* <span data-ttu-id="6d63b-111">Visual Studio 2015 of Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="6d63b-111">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="6d63b-112">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="6d63b-112">An active Azure account.</span></span> <span data-ttu-id="6d63b-113">(Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)</span><span class="sxs-lookup"><span data-stu-id="6d63b-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="6d63b-114">Als u de apparaat-id in plaats daarvan programmatisch maken wilt, leest u de bijbehorende sectie in het [uw gesimuleerde apparaat verbonden met uw iothub met .NET] [ lnk-device-identity-csharp] artikel.</span><span class="sxs-lookup"><span data-stu-id="6d63b-114">If you want to create the device identity programmatically instead, read the corresponding section in the [Connect your simulated device to your IoT hub using .NET][lnk-device-identity-csharp] article.</span></span>

## <a name="create-the-service-app"></a><span data-ttu-id="6d63b-115">De service-app maken</span><span class="sxs-lookup"><span data-stu-id="6d63b-115">Create the service app</span></span>
<span data-ttu-id="6d63b-116">In deze sectie maakt u een .NET-consoletoepassing maken (met C#) waarmee de metagegevens van de locatie wordt toegevoegd aan de apparaat-twin gekoppeld **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="6d63b-116">In this section, you create a .NET console app (using C#) that adds location metadata to the device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="6d63b-117">Deze vervolgens het apparaat horende opgeslagen in de IoT-hub te selecteren van de apparaten die zich in de Verenigde Staten en de waarden die gerapporteerd van een mobiele verbinding een query.</span><span class="sxs-lookup"><span data-stu-id="6d63b-117">It then queries the device twins stored in the IoT hub selecting the devices located in the US, and then the ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="6d63b-118">Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toe aan de huidige oplossing met behulp van de projectsjabloon **Console Application**.</span><span class="sxs-lookup"><span data-stu-id="6d63b-118">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="6d63b-119">Noem het project **AddTagsAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="6d63b-119">Name the project **AddTagsAndQuery**.</span></span>
   
    ![Nieuw Windows Classic Desktop-project in Visual C#][img-createapp]
1. <span data-ttu-id="6d63b-121">Klik in Solution Explorer met de rechtermuisknop op de **AddTagsAndQuery** project en klik vervolgens op **NuGet-pakketten beheren...** .</span><span class="sxs-lookup"><span data-stu-id="6d63b-121">In Solution Explorer, right-click the **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="6d63b-122">In de **NuGet Package Manager** Selecteer **Bladeren** en zoek naar **microsoft.azure.devices**.</span><span class="sxs-lookup"><span data-stu-id="6d63b-122">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="6d63b-123">Selecteer **installeren** voor het installeren van de **Microsoft.Azure.Devices** Inpakken en accepteer de gebruiksvoorwaarden.</span><span class="sxs-lookup"><span data-stu-id="6d63b-123">Select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="6d63b-124">Met deze procedure worden de [Azure IoT-service-SDK][lnk-nuget-service-sdk], het NuGet-pakket en de bijbehorende afhankelijkheden gedownload en geïnstalleerd. Ook worden verwijzingen hiernaar toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="6d63b-124">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Sluit het venster Nuget Package Manager.][img-servicenuget]
1. <span data-ttu-id="6d63b-126">Voeg aan het begin van het bestand **Program.cs** de volgende `using` instructies toe:</span><span class="sxs-lookup"><span data-stu-id="6d63b-126">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="6d63b-127">Voeg de volgende velden toe aan de klasse **Program**:</span><span class="sxs-lookup"><span data-stu-id="6d63b-127">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="6d63b-128">Vervang de tijdelijke aanduidingswaarde met de IoT Hub-verbindingsreeks voor de hub die u hebt gemaakt in de vorige sectie.</span><span class="sxs-lookup"><span data-stu-id="6d63b-128">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="6d63b-129">Voeg de volgende methode toe aan de klasse **Program**:</span><span class="sxs-lookup"><span data-stu-id="6d63b-129">Add the following method to the **Program** class:</span></span>
   
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
   
    <span data-ttu-id="6d63b-130">De **RegistryManager** klasse bevat alle methoden die zijn vereist voor interactie met horende apparaten van de service.</span><span class="sxs-lookup"><span data-stu-id="6d63b-130">The **RegistryManager** class exposes all the methods required to interact with device twins from the service.</span></span> <span data-ttu-id="6d63b-131">De vorige code eerst initialiseert de **registryManager** object en vervolgens haalt de apparaat-twin voor **myDeviceId**, en ten slotte de labels bijgewerkt met informatie over de gewenste locatie.</span><span class="sxs-lookup"><span data-stu-id="6d63b-131">The previous code first initializes the **registryManager** object, then retrieves the device twin for **myDeviceId**, and finally updates its tags with the desired location information.</span></span>
   
    <span data-ttu-id="6d63b-132">Na het bijwerken, deze twee query's uitvoert: de eerste selecteert alleen de apparaat-horende apparaten zich in de **Redmond43** plant en de tweede verfijning de query voor het selecteren van alleen de apparaten die ook via het mobiele netwerk zijn verbonden.</span><span class="sxs-lookup"><span data-stu-id="6d63b-132">After updating, it executes two queries: the first selects only the device twins of devices located in the **Redmond43** plant, and the second refines the query to select only the devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="6d63b-133">Houd er rekening mee dat de vorige code bij het maken van de **query** object, geeft u een maximum aantal geretourneerde documenten.</span><span class="sxs-lookup"><span data-stu-id="6d63b-133">Note that the previous code, when it creates the **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="6d63b-134">De **query** object bevat een **HasMoreResults** Boole-eigenschap die u gebruiken kunt om aan te roepen de **GetNextAsTwinAsync** methoden meerdere keren voor het ophalen van alle resultaten.</span><span class="sxs-lookup"><span data-stu-id="6d63b-134">The **query** object contains a **HasMoreResults** boolean property that you can use to invoke the **GetNextAsTwinAsync** methods multiple times to retrieve all results.</span></span> <span data-ttu-id="6d63b-135">Een methode aangeroepen **GetNextAsJson** is beschikbaar voor de resultaten die bijvoorbeeld niet apparaat horende zijn resultaten van query's voor aggregatie.</span><span class="sxs-lookup"><span data-stu-id="6d63b-135">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="6d63b-136">Voeg tot slot de volgende regels toe aan de methode **Main**:</span><span class="sxs-lookup"><span data-stu-id="6d63b-136">Finally, add the following lines to the **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

1. <span data-ttu-id="6d63b-137">Open in Solution Explorer de **opstartprojecten instellen...**  en zorg ervoor dat de **actie** voor **AddTagsAndQuery** project **Start**.</span><span class="sxs-lookup"><span data-stu-id="6d63b-137">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="6d63b-138">De oplossing bouwen.</span><span class="sxs-lookup"><span data-stu-id="6d63b-138">Build the solution.</span></span>
1. <span data-ttu-id="6d63b-139">Deze toepassing uitvoeren door met de rechtermuisknop op de **AddTagsAndQuery** project en selecteer **Debug**, gevolgd door **nieuw exemplaar gestart**.</span><span class="sxs-lookup"><span data-stu-id="6d63b-139">Run this application by right-clicking on the **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="6d63b-140">U ziet één apparaat in de resultaten van de query wordt gevraagd voor alle apparaten vinden in **Redmond43** en er is geen voor de query die de resultaten beperkt tot apparaten die gebruikmaken van een mobiel netwerk.</span><span class="sxs-lookup"><span data-stu-id="6d63b-140">You should see one device in the results for the query asking for all devices located in **Redmond43** and none for the query that restricts the results to devices that use a cellular network.</span></span>
   
    ![De resultaten van de query-venster][img-addtagapp]

<span data-ttu-id="6d63b-142">In de volgende sectie maakt u een apparaat-app die rapporten de informatie over de connectiviteit en het resultaat van de query in de vorige sectie wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="6d63b-142">In the next section, you create a device app that reports the connectivity information and changes the result of the query in the previous section.</span></span>

## <a name="create-the-device-app"></a><span data-ttu-id="6d63b-143">De apparaat-app maken</span><span class="sxs-lookup"><span data-stu-id="6d63b-143">Create the device app</span></span>
<span data-ttu-id="6d63b-144">In deze sectie maakt u een .NET-consoletoepassing die is verbonden met uw hub als **myDeviceId**, en werkt vervolgens de gerapporteerde eigenschappen bevatten informatie die is verbonden met een mobiel netwerk.</span><span class="sxs-lookup"><span data-stu-id="6d63b-144">In this section, you create a .NET console app that connects to your hub as **myDeviceId**, and then updates its reported properties to contain the information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="6d63b-145">Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toe aan de huidige oplossing met behulp van de projectsjabloon **Console Application**.</span><span class="sxs-lookup"><span data-stu-id="6d63b-145">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="6d63b-146">Noem het project **ReportConnectivity**.</span><span class="sxs-lookup"><span data-stu-id="6d63b-146">Name the project **ReportConnectivity**.</span></span>
   
    ![Nieuwe Visual C# klassieke Windows-apparaat-app][img-createdeviceapp]
    
1. <span data-ttu-id="6d63b-148">Klik in Solution Explorer met de rechtermuisknop op de **ReportConnectivity** project en klik vervolgens op **NuGet-pakketten beheren...** .</span><span class="sxs-lookup"><span data-stu-id="6d63b-148">In Solution Explorer, right-click the **ReportConnectivity** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="6d63b-149">In de **NuGet Package Manager** Selecteer **Bladeren** en zoek naar **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="6d63b-149">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="6d63b-150">Selecteer **installeren** voor het installeren van de **Microsoft.Azure.Devices.Client** Inpakken en accepteer de gebruiksvoorwaarden.</span><span class="sxs-lookup"><span data-stu-id="6d63b-150">Select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span></span> <span data-ttu-id="6d63b-151">Deze procedure downloadt, installeert en voegt u een verwijzing naar de [Azure IoT-device SDK] [ lnk-nuget-client-sdk] NuGet-pakket en de bijbehorende afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="6d63b-151">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet-Pakketbeheer venster Client-app][img-clientnuget]
1. <span data-ttu-id="6d63b-153">Voeg aan het begin van het bestand **Program.cs** de volgende `using` instructies toe:</span><span class="sxs-lookup"><span data-stu-id="6d63b-153">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. <span data-ttu-id="6d63b-154">Voeg de volgende velden toe aan de klasse **Program**:</span><span class="sxs-lookup"><span data-stu-id="6d63b-154">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="6d63b-155">Vervang de tijdelijke aanduidingswaarde met de verbindingsreeks voor apparaten die u in de vorige sectie hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="6d63b-155">Replace the placeholder value with the device connection string that you noted in the previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. <span data-ttu-id="6d63b-156">Voeg de volgende methode toe aan de klasse **Program**:</span><span class="sxs-lookup"><span data-stu-id="6d63b-156">Add the following method to the **Program** class:</span></span>

       public static async void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting to hub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
                Console.WriteLine("Retrieving twin");
                await Client.GetTwinAsync();
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

    <span data-ttu-id="6d63b-157">De **Client** object bevat de methoden die u nodig hebt om te communiceren met horende apparaten van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="6d63b-157">The **Client** object exposes all the methods you require to interact with device twins from the device.</span></span> <span data-ttu-id="6d63b-158">De hierboven weergegeven code initialiseert de **Client** object, en vervolgens haalt de apparaat-twin voor **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="6d63b-158">The code shown above, initializes the **Client** object, and then retrieves the device twin for **myDeviceId**.</span></span>

1. <span data-ttu-id="6d63b-159">Voeg de volgende methode toe aan de klasse **Program**:</span><span class="sxs-lookup"><span data-stu-id="6d63b-159">Add the following method to the **Program** class:</span></span>
   
        public static async void ReportConnectivity()
        {
            try
            {
                Console.WriteLine("Sending connectivity data as reported property");
                
                TwinCollection reportedProperties, connectivity;
                reportedProperties = new TwinCollection();
                connectivity = new TwinCollection();
                connectivity["type"] = "cellular";
                reportedProperties["connectivity"] = connectivity;
                await Client.UpdateReportedPropertiesAsync(reportedProperties);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

   <span data-ttu-id="6d63b-160">De bovenstaande updates code **myDeviceId**de eigenschap met de connectiviteit-informatie gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="6d63b-160">The code above updates **myDeviceId**'s reported property with the connectivity information.</span></span>

1. <span data-ttu-id="6d63b-161">Voeg tot slot de volgende regels toe aan de methode **Main**:</span><span class="sxs-lookup"><span data-stu-id="6d63b-161">Finally, add the following lines to the **Main** method:</span></span>
   
       try
       {
            InitClient();
            ReportConnectivity();
       }
       catch (Exception ex)
       {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
       }
       Console.WriteLine("Press Enter to exit.");
       Console.ReadLine();

1. <span data-ttu-id="6d63b-162">Open in Solution Explorer de **opstartprojecten instellen...**  en zorg ervoor dat de **actie** voor **ReportConnectivity** project **Start**.</span><span class="sxs-lookup"><span data-stu-id="6d63b-162">In the Solution Explorer, open the **Set StartUp projects...** and make sure the **Action** for **ReportConnectivity** project is **Start**.</span></span> <span data-ttu-id="6d63b-163">De oplossing bouwen.</span><span class="sxs-lookup"><span data-stu-id="6d63b-163">Build the solution.</span></span>
1. <span data-ttu-id="6d63b-164">Deze toepassing uitvoeren door met de rechtermuisknop op de **ReportConnectivity** project en selecteer **Debug**, gevolgd door **nieuw exemplaar gestart**.</span><span class="sxs-lookup"><span data-stu-id="6d63b-164">Run this application by right-clicking on the **ReportConnectivity** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="6d63b-165">U ziet het ophalen van de informatie twin, en vervolgens verzenden connectiviteit heeft als een *gerapporteerd eigenschap*.</span><span class="sxs-lookup"><span data-stu-id="6d63b-165">You should see it getting the twin information, and then sending connectivity as a *reported property*.</span></span>
   
    ![Apparaat-app verbinding rapport uitvoeren][img-rundeviceapp]
    
    
1. <span data-ttu-id="6d63b-167">Nu dat het apparaat heeft gemeld dat de gegevens over de connectiviteit, moet deze worden weergegeven in beide query's.</span><span class="sxs-lookup"><span data-stu-id="6d63b-167">Now that the device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="6d63b-168">Uitvoeren van de .NET **AddTagsAndQuery** app opnieuw uit te voeren de query's.</span><span class="sxs-lookup"><span data-stu-id="6d63b-168">Run the .NET **AddTagsAndQuery** app to run the queries again.</span></span> <span data-ttu-id="6d63b-169">Deze tijd **myDeviceId** moet worden weergegeven in beide queryresultaten.</span><span class="sxs-lookup"><span data-stu-id="6d63b-169">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![Connectiviteit van apparaten is gerapporteerd][img-tagappsuccess]

## <a name="next-steps"></a><span data-ttu-id="6d63b-171">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6d63b-171">Next steps</span></span>
<span data-ttu-id="6d63b-172">In deze handleiding hebt u een nieuwe IoT-hub geconfigureerd in Azure Portal en vervolgens een apparaat-id gemaakt in het id-register van de IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="6d63b-172">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="6d63b-173">U metagegevens van apparaten als labels toegevoegd vanuit een back-end-app en een gesimuleerde apparaattoepassing geschreven naar apparaten connectiviteit rapportgegevens in de apparaat-twin.</span><span class="sxs-lookup"><span data-stu-id="6d63b-173">You added device metadata as tags from a back-end app, and wrote a simulated device app to report device connectivity information in the device twin.</span></span> <span data-ttu-id="6d63b-174">Ook hebt u geleerd hoe deze gegevens met behulp van de SQL-achtige IoT Hub-querytaal opvragen.</span><span class="sxs-lookup"><span data-stu-id="6d63b-174">You also learned how to query this information using the SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="6d63b-175">Gebruik de volgende bronnen voor meer informatie over hoe:</span><span class="sxs-lookup"><span data-stu-id="6d63b-175">Use the following resources to learn how to:</span></span>

* <span data-ttu-id="6d63b-176">verzenden van telemetrie vanaf apparaten met de [aan de slag met IoT Hub] [ lnk-iothub-getstarted] zelfstudie</span><span class="sxs-lookup"><span data-stu-id="6d63b-176">send telemetry from devices with the [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="6d63b-177">apparaten configureren met de gewenste eigenschappen van apparaat twin met de [gebruik gewenst eigenschappen voor het configureren van apparaten] [ lnk-twin-how-to-configure] zelfstudie</span><span class="sxs-lookup"><span data-stu-id="6d63b-177">configure devices using device twin's desired properties with the [Use desired properties to configure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="6d63b-178">beheren van apparaten interactief (zoals het inschakelen van een ventilator van een gebruiker beheerde app) met de [direct methoden gebruiken] [ lnk-methods-tutorial] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="6d63b-178">control devices interactively (such as turning on a fan from a user-controlled app) with the [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-csharp-twin-getstarted/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-csharp-twin-getstarted/createnetapp.png
[img-addtagapp]: media/iot-hub-csharp-csharp-twin-getstarted/addtagapp.png
[img-createdeviceapp]: media/iot-hub-csharp-csharp-twin-getstarted/createdeviceapp.png
[img-clientnuget]: media/iot-hub-csharp-csharp-twin-getstarted/clientsdknuget.png
[img-rundeviceapp]: media/iot-hub-csharp-csharp-twin-getstarted/rundeviceapp.png
[img-tagappsuccess]: media/iot-hub-csharp-csharp-twin-getstarted/tagappsuccess.png

<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/

[lnk-device-identity-csharp]: iot-hub-csharp-csharp-getstarted.md#DeviceIdentity_csharp
[lnk-d2c]: iot-hub-devguide-messaging.md#device-to-cloud-messages
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-identity]: iot-hub-devguide-identity-registry.md

[lnk-iothub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-how-to-configure]: iot-hub-csharp-node-twin-how-to-configure.md

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

