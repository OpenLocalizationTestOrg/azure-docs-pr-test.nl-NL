---
title: aaaGet de slag met Azure IoT Hub apparaat horende (.NET/.NET) | Microsoft Docs
description: Hoe toouse Azure IoT Hub apparaat horende tooadd tags en gebruik vervolgens een IoT Hub-query. U hello Azure IoT-device SDK voor .NET tooimplement Hallo gesimuleerde apparaattoepassing en hello Azure IoT service SDK voor .NET tooimplement een service-app die Hallo-labels toegevoegd en Hallo IoT Hub-query wordt uitgevoerd.
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
ms.openlocfilehash: 7fa73ac896c44e79c6522d252cd1515bd6e7bb2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-device-twins-netnet"></a><span data-ttu-id="12eda-104">Aan de slag met apparaat horende (.NET/.NET)</span><span class="sxs-lookup"><span data-stu-id="12eda-104">Get started with device twins (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-twin-get-started](../../includes/iot-hub-selector-twin-get-started.md)]

<span data-ttu-id="12eda-105">Aan het einde van de Hallo van deze zelfstudie hebt u deze apps van .NET-console:</span><span class="sxs-lookup"><span data-stu-id="12eda-105">At hello end of this tutorial, you will have these .NET console apps:</span></span>

* <span data-ttu-id="12eda-106">**CreateDeviceIdentity**, een .NET-app die u maakt een apparaat-id en de bijbehorende sleutel tooconnect app op uw gesimuleerde apparaat.</span><span class="sxs-lookup"><span data-stu-id="12eda-106">**CreateDeviceIdentity**, a .NET app which creates a device identity and associated security key tooconnect your simulated device app.</span></span>
* <span data-ttu-id="12eda-107">**AddTagsAndQuery**, een .NET-back-end-app die labels toegevoegd en wordt opgevraagd horende apparaten.</span><span class="sxs-lookup"><span data-stu-id="12eda-107">**AddTagsAndQuery**, a .NET back-end app which adds tags and queries device twins.</span></span>
* <span data-ttu-id="12eda-108">**ReportConnectivity**, een .NET-apparaattoepassing dat een apparaat simuleert dat tooyour IoT-hub is verbonden met de apparaat-id Hallo eerder hebt gemaakt, en rapporteert de voorwaarde van de verbinding.</span><span class="sxs-lookup"><span data-stu-id="12eda-108">**ReportConnectivity**, a .NET device app which simulates a device that connects tooyour IoT hub with hello device identity created earlier, and reports its connectivity condition.</span></span>

> [!NOTE]
> <span data-ttu-id="12eda-109">Hallo artikel [Azure IoT SDK's] [ lnk-hub-sdks] bevat informatie over hello Azure IoT SDK's waarmee u toobuild kunt apparaat- en back-end-apps.</span><span class="sxs-lookup"><span data-stu-id="12eda-109">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="12eda-110">toocomplete in deze zelfstudie hebt u Hallo volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="12eda-110">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="12eda-111">Visual Studio 2015 of Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="12eda-111">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="12eda-112">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="12eda-112">An active Azure account.</span></span> <span data-ttu-id="12eda-113">(Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)</span><span class="sxs-lookup"><span data-stu-id="12eda-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="12eda-114">Als u toocreate Hallo apparaat-id via een programma in plaats daarvan wilt, lezen Hallo overeenkomstige sectie in Hallo [verbinding maken met uw gesimuleerde apparaat tooyour iothub met .NET] [ lnk-device-identity-csharp] artikel.</span><span class="sxs-lookup"><span data-stu-id="12eda-114">If you want toocreate hello device identity programmatically instead, read hello corresponding section in hello [Connect your simulated device tooyour IoT hub using .NET][lnk-device-identity-csharp] article.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="12eda-115">Hallo-service-app maken</span><span class="sxs-lookup"><span data-stu-id="12eda-115">Create hello service app</span></span>
<span data-ttu-id="12eda-116">In deze sectie maakt u een .NET-consoletoepassing maken (met C#) die wordt toegevoegd locatie metagegevens toohello apparaat twin die zijn gekoppeld aan **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="12eda-116">In this section, you create a .NET console app (using C#) that adds location metadata toohello device twin associated with **myDeviceId**.</span></span> <span data-ttu-id="12eda-117">Vervolgens query's Hallo apparaat horende opgeslagen ons in IoT-hub Hallo Hallo apparaten zich in Hallo selecteren en vervolgens Hallo die een mobiele verbinding gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="12eda-117">It then queries hello device twins stored in hello IoT hub selecting hello devices located in hello US, and then hello ones that reported a cellular connection.</span></span>

1. <span data-ttu-id="12eda-118">Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toohello huidige oplossing met behulp van Hallo **consoletoepassing** projectsjabloon.</span><span class="sxs-lookup"><span data-stu-id="12eda-118">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="12eda-119">Naam Hallo project **AddTagsAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="12eda-119">Name hello project **AddTagsAndQuery**.</span></span>
   
    ![Nieuw Windows Classic Desktop-project in Visual C#][img-createapp]
1. <span data-ttu-id="12eda-121">Klik in Solution Explorer met de rechtermuisknop op Hallo **AddTagsAndQuery** project en klik vervolgens op **NuGet-pakketten beheren...** .</span><span class="sxs-lookup"><span data-stu-id="12eda-121">In Solution Explorer, right-click hello **AddTagsAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="12eda-122">In Hallo **NuGet Package Manager** Selecteer **Bladeren** en zoek naar **microsoft.azure.devices**.</span><span class="sxs-lookup"><span data-stu-id="12eda-122">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices**.</span></span> <span data-ttu-id="12eda-123">Selecteer **installeren** tooinstall hello **Microsoft.Azure.Devices** Inpakken en accepteer de gebruiksvoorwaarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="12eda-123">Select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="12eda-124">Deze procedure downloadt, installeert en voegt u een verwijzing toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet-pakket en de bijbehorende afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="12eda-124">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Sluit het venster Nuget Package Manager.][img-servicenuget]
1. <span data-ttu-id="12eda-126">Voeg de volgende Hallo `using` instructies boven Hallo Hallo **Program.cs** bestand:</span><span class="sxs-lookup"><span data-stu-id="12eda-126">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
1. <span data-ttu-id="12eda-127">Hallo na toohello velden toevoegen **programma** klasse.</span><span class="sxs-lookup"><span data-stu-id="12eda-127">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="12eda-128">Vervang Hallo tijdelijke aanduidingswaarde met IoT Hub-verbindingsreeks voor Hallo-hub die u hebt gemaakt in de vorige sectie Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="12eda-128">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="12eda-129">Hallo na methode toohello toevoegen **programma** klasse:</span><span class="sxs-lookup"><span data-stu-id="12eda-129">Add hello following method toohello **Program** class:</span></span>
   
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
   
    <span data-ttu-id="12eda-130">Hallo **RegistryManager** klasse beschrijft alle Hallo methoden vereist toointeract met apparaat horende van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="12eda-130">hello **RegistryManager** class exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="12eda-131">Hallo vorige code initialiseert eerst Hallo **registryManager** object, en vervolgens haalt Hallo apparaat twin voor **myDeviceId**, en ten slotte de labels bijgewerkt met informatie over de locatie van de gewenste Hallo.</span><span class="sxs-lookup"><span data-stu-id="12eda-131">hello previous code first initializes hello **registryManager** object, then retrieves hello device twin for **myDeviceId**, and finally updates its tags with hello desired location information.</span></span>
   
    <span data-ttu-id="12eda-132">Na het bijwerken, deze twee query's uitvoert: Hallo selecteert eerst alleen Hallo apparaat horende apparaten zich in Hallo **Redmond43** installaties en Hallo tweede verfijning Hallo query tooselect alleen Hallo apparaten die ook zijn verbonden via mobiel netwerk.</span><span class="sxs-lookup"><span data-stu-id="12eda-132">After updating, it executes two queries: hello first selects only hello device twins of devices located in hello **Redmond43** plant, and hello second refines hello query tooselect only hello devices that are also connected through cellular network.</span></span>
   
    <span data-ttu-id="12eda-133">Houd er rekening mee dat vorige code Hallo bij het maken van Hallo **query** object, geeft u een maximum aantal geretourneerde documenten.</span><span class="sxs-lookup"><span data-stu-id="12eda-133">Note that hello previous code, when it creates hello **query** object, specifies a maximum number of returned documents.</span></span> <span data-ttu-id="12eda-134">Hallo **query** object bevat een **HasMoreResults** Boole-eigenschap waarmee u tooinvoke hello kunt **GetNextAsTwinAsync** methoden meerdere keren tooretrieve alle resultaten.</span><span class="sxs-lookup"><span data-stu-id="12eda-134">hello **query** object contains a **HasMoreResults** boolean property that you can use tooinvoke hello **GetNextAsTwinAsync** methods multiple times tooretrieve all results.</span></span> <span data-ttu-id="12eda-135">Een methode aangeroepen **GetNextAsJson** is beschikbaar voor de resultaten die bijvoorbeeld niet apparaat horende zijn resultaten van query's voor aggregatie.</span><span class="sxs-lookup"><span data-stu-id="12eda-135">A method called **GetNextAsJson** is available for results that are not device twins, for example, results of aggregation queries.</span></span>
1. <span data-ttu-id="12eda-136">Voeg regels toohello na Hallo **Main** methode:</span><span class="sxs-lookup"><span data-stu-id="12eda-136">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        AddTagsAndQuery().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. <span data-ttu-id="12eda-137">Open in Solution Explorer hello, Hallo **opstartprojecten instellen...**  en zorg ervoor dat Hallo **actie** voor **AddTagsAndQuery** project **Start**.</span><span class="sxs-lookup"><span data-stu-id="12eda-137">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **AddTagsAndQuery** project is **Start**.</span></span> <span data-ttu-id="12eda-138">Hallo-oplossing bouwen.</span><span class="sxs-lookup"><span data-stu-id="12eda-138">Build hello solution.</span></span>
1. <span data-ttu-id="12eda-139">Deze toepassing uitvoeren door met de rechtermuisknop op Hallo **AddTagsAndQuery** project en selecteer **Debug**, gevolgd door **nieuw exemplaar gestart**.</span><span class="sxs-lookup"><span data-stu-id="12eda-139">Run this application by right-clicking on hello **AddTagsAndQuery** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="12eda-140">U ziet één apparaat in Hallo resultaten voor Hallo query vragen voor alle apparaten vinden in **Redmond43** en geen voor de Hallo-query die Hallo beperkt resultaten toodevices die gebruikmaken van een mobiel netwerk.</span><span class="sxs-lookup"><span data-stu-id="12eda-140">You should see one device in hello results for hello query asking for all devices located in **Redmond43** and none for hello query that restricts hello results toodevices that use a cellular network.</span></span>
   
    ![De resultaten van de query-venster][img-addtagapp]

<span data-ttu-id="12eda-142">In de volgende sectie Hallo, maakt u een apparaat-app die Hallo connectiviteit informatie rapporteert en wijzigingen resultaat van query in de vorige sectie Hallo HALLO hallo.</span><span class="sxs-lookup"><span data-stu-id="12eda-142">In hello next section, you create a device app that reports hello connectivity information and changes hello result of hello query in hello previous section.</span></span>

## <a name="create-hello-device-app"></a><span data-ttu-id="12eda-143">Hallo apparaattoepassing maken</span><span class="sxs-lookup"><span data-stu-id="12eda-143">Create hello device app</span></span>
<span data-ttu-id="12eda-144">In deze sectie maakt u een .NET-consoletoepassing die verbinding tooyour hub als maakt **myDeviceId**, en werkt vervolgens de gerapporteerde toocontain Hallo eigenschapsgegevens dat is verbonden met een mobiel netwerk.</span><span class="sxs-lookup"><span data-stu-id="12eda-144">In this section, you create a .NET console app that connects tooyour hub as **myDeviceId**, and then updates its reported properties toocontain hello information that it is connected using a cellular network.</span></span>

1. <span data-ttu-id="12eda-145">Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toohello huidige oplossing met behulp van Hallo **consoletoepassing** projectsjabloon.</span><span class="sxs-lookup"><span data-stu-id="12eda-145">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="12eda-146">Naam Hallo project **ReportConnectivity**.</span><span class="sxs-lookup"><span data-stu-id="12eda-146">Name hello project **ReportConnectivity**.</span></span>
   
    ![Nieuwe Visual C# klassieke Windows-apparaat-app][img-createdeviceapp]
    
1. <span data-ttu-id="12eda-148">Klik in Solution Explorer met de rechtermuisknop op Hallo **ReportConnectivity** project en klik vervolgens op **NuGet-pakketten beheren...** .</span><span class="sxs-lookup"><span data-stu-id="12eda-148">In Solution Explorer, right-click hello **ReportConnectivity** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="12eda-149">In Hallo **NuGet Package Manager** Selecteer **Bladeren** en zoek naar **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="12eda-149">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="12eda-150">Selecteer **installeren** tooinstall hello **Microsoft.Azure.Devices.Client** Inpakken en accepteer de gebruiksvoorwaarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="12eda-150">Select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="12eda-151">Deze procedure downloadt, installeert en voegt u een verwijzing toohello [Azure IoT-device SDK] [ lnk-nuget-client-sdk] NuGet-pakket en de bijbehorende afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="12eda-151">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet-Pakketbeheer venster Client-app][img-clientnuget]
1. <span data-ttu-id="12eda-153">Voeg de volgende Hallo `using` instructies boven Hallo Hallo **Program.cs** bestand:</span><span class="sxs-lookup"><span data-stu-id="12eda-153">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. <span data-ttu-id="12eda-154">Hallo na toohello velden toevoegen **programma** klasse.</span><span class="sxs-lookup"><span data-stu-id="12eda-154">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="12eda-155">Vervang Hallo tijdelijke aanduidingswaarde met de verbindingsreeks van het Hallo-apparaat die u hebt genoteerd in de vorige sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="12eda-155">Replace hello placeholder value with hello device connection string that you noted in hello previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. <span data-ttu-id="12eda-156">Hallo na methode toohello toevoegen **programma** klasse:</span><span class="sxs-lookup"><span data-stu-id="12eda-156">Add hello following method toohello **Program** class:</span></span>

       public static async void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting toohub");
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

    <span data-ttu-id="12eda-157">Hallo **Client** object bevat alle Hallo-methoden die u nodig hebt toointeract met apparaat horende van Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="12eda-157">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="12eda-158">Hallo hierboven weergegeven code initialiseert Hallo **Client** object, en vervolgens haalt Hallo apparaat twin voor **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="12eda-158">hello code shown above, initializes hello **Client** object, and then retrieves hello device twin for **myDeviceId**.</span></span>

1. <span data-ttu-id="12eda-159">Hallo na methode toohello toevoegen **programma** klasse:</span><span class="sxs-lookup"><span data-stu-id="12eda-159">Add hello following method toohello **Program** class:</span></span>
   
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

   <span data-ttu-id="12eda-160">Hallo bovenstaande updates code **myDeviceId**de eigenschap met de informatie over de connectiviteit van Hallo gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="12eda-160">hello code above updates **myDeviceId**'s reported property with hello connectivity information.</span></span>

1. <span data-ttu-id="12eda-161">Voeg regels toohello na Hallo **Main** methode:</span><span class="sxs-lookup"><span data-stu-id="12eda-161">Finally, add hello following lines toohello **Main** method:</span></span>
   
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
       Console.WriteLine("Press Enter tooexit.");
       Console.ReadLine();

1. <span data-ttu-id="12eda-162">Open in Solution Explorer hello, Hallo **opstartprojecten instellen...**  en zorg ervoor dat Hallo **actie** voor **ReportConnectivity** project **Start**.</span><span class="sxs-lookup"><span data-stu-id="12eda-162">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **ReportConnectivity** project is **Start**.</span></span> <span data-ttu-id="12eda-163">Hallo-oplossing bouwen.</span><span class="sxs-lookup"><span data-stu-id="12eda-163">Build hello solution.</span></span>
1. <span data-ttu-id="12eda-164">Deze toepassing uitvoeren door met de rechtermuisknop op Hallo **ReportConnectivity** project en selecteer **Debug**, gevolgd door **nieuw exemplaar gestart**.</span><span class="sxs-lookup"><span data-stu-id="12eda-164">Run this application by right-clicking on hello **ReportConnectivity** project and selecting **Debug**, followed by **Start new instance**.</span></span> <span data-ttu-id="12eda-165">U ziet het Hallo twin informatie verkrijgen en vervolgens verzenden connectiviteit heeft als een *gerapporteerd eigenschap*.</span><span class="sxs-lookup"><span data-stu-id="12eda-165">You should see it getting hello twin information, and then sending connectivity as a *reported property*.</span></span>
   
    ![Connectiviteit van apparaten app tooreport uitvoeren][img-rundeviceapp]
    
    
1. <span data-ttu-id="12eda-167">Nu dat hello apparaat de connectiviteit informatie gerapporteerd, moet deze worden weergegeven in beide query's.</span><span class="sxs-lookup"><span data-stu-id="12eda-167">Now that hello device reported its connectivity information, it should appear in both queries.</span></span> <span data-ttu-id="12eda-168">Voer Hallo .NET **AddTagsAndQuery** app toorun Hallo query opnieuw.</span><span class="sxs-lookup"><span data-stu-id="12eda-168">Run hello .NET **AddTagsAndQuery** app toorun hello queries again.</span></span> <span data-ttu-id="12eda-169">Deze tijd **myDeviceId** moet worden weergegeven in beide queryresultaten.</span><span class="sxs-lookup"><span data-stu-id="12eda-169">This time **myDeviceId** should appear in both query results.</span></span>
   
    ![Connectiviteit van apparaten is gerapporteerd][img-tagappsuccess]

## <a name="next-steps"></a><span data-ttu-id="12eda-171">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="12eda-171">Next steps</span></span>
<span data-ttu-id="12eda-172">In deze zelfstudie maakt u een nieuwe iothub geconfigureerd in hello Azure-portal en vervolgens een apparaat-id in de id-register Hallo iothub hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="12eda-172">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="12eda-173">U metagegevens van apparaten als labels toegevoegd vanuit een back-end-app en een gesimuleerd apparaat app tooreport-apparaatgegevens connectiviteit in Hallo apparaat twin geschreven.</span><span class="sxs-lookup"><span data-stu-id="12eda-173">You added device metadata as tags from a back-end app, and wrote a simulated device app tooreport device connectivity information in hello device twin.</span></span> <span data-ttu-id="12eda-174">U hebt ook geleerd hoe tooquery deze informatie Hallo IoT-Hub SQL-achtige query language gebruiken.</span><span class="sxs-lookup"><span data-stu-id="12eda-174">You also learned how tooquery this information using hello SQL-like IoT Hub query language.</span></span>

<span data-ttu-id="12eda-175">Gebruik Hallo resources toolearn hoe volgende aan:</span><span class="sxs-lookup"><span data-stu-id="12eda-175">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="12eda-176">verzenden van telemetrie vanaf apparaten Hello [aan de slag met IoT Hub] [ lnk-iothub-getstarted] zelfstudie</span><span class="sxs-lookup"><span data-stu-id="12eda-176">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="12eda-177">apparaten configureren met de gewenste eigenschappen van apparaat twin Hello [gebruik gewenst eigenschappen tooconfigure apparaten] [ lnk-twin-how-to-configure] zelfstudie</span><span class="sxs-lookup"><span data-stu-id="12eda-177">configure devices using device twin's desired properties with hello [Use desired properties tooconfigure devices][lnk-twin-how-to-configure] tutorial,</span></span>
* <span data-ttu-id="12eda-178">beheren van apparaten interactief (zoals het inschakelen van een ventilator van een gebruiker beheerde app) met Hallo [direct methoden gebruiken] [ lnk-methods-tutorial] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="12eda-178">control devices interactively (such as turning on a fan from a user-controlled app) with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

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

