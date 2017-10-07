---
title: aaaUse Azure IoT Hub twin apparaateigenschappen (.NET/.NET) | Microsoft Docs
description: Hoe toouse Azure IoT Hub apparaat horende tooconfigure apparaten. U gebruikt hello Azure IoT-apparaat SDK voor .NET tooimplement een gesimuleerde apparaattoepassing en hello Azure IoT service SDK voor .NET tooimplement een service-app die de apparaatconfiguratie van een met behulp van een apparaat-twin wijzigt.
services: iot-hub
documentationcenter: .net
author: dsk-2015
manager: timlt
editor: 
ms.assetid: 3c627476-f982-43c9-bd17-e0698c5d236d
ms.service: iot-hub
ms.devlang: csharp
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: dkshir
ms.openlocfilehash: 486436d29abfd5158c253adc5abf5935e0e1fdba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-desired-properties-tooconfigure-devices"></a><span data-ttu-id="532d4-104">Eigenschappen van de gewenste tooconfigure apparaten gebruiken</span><span class="sxs-lookup"><span data-stu-id="532d4-104">Use desired properties tooconfigure devices</span></span>
[!INCLUDE [iot-hub-selector-twin-how-to-configure](../../includes/iot-hub-selector-twin-how-to-configure.md)]

<span data-ttu-id="532d4-105">Aan het einde van de Hallo van deze zelfstudie hebt u twee apps voor .NET-console:</span><span class="sxs-lookup"><span data-stu-id="532d4-105">At hello end of this tutorial, you will have two .NET console apps:</span></span>

* <span data-ttu-id="532d4-106">**SimulateDeviceConfiguration**, een gesimuleerde apparaattoepassing die wordt gewacht op een gewenste configuratie-update en rapporten Hallo status van een gesimuleerde configuratieproces voor de update.</span><span class="sxs-lookup"><span data-stu-id="532d4-106">**SimulateDeviceConfiguration**, a simulated device app that waits for a desired configuration update and reports hello status of a simulated configuration update process.</span></span>
* <span data-ttu-id="532d4-107">**SetDesiredConfigurationAndQuery**, een back-end-app, die ingesteld Hallo gewenste configuratie op een apparaat en query's Hallo update configuratieproces.</span><span class="sxs-lookup"><span data-stu-id="532d4-107">**SetDesiredConfigurationAndQuery**, a back-end app, which sets hello desired configuration on a device and queries hello configuration update process.</span></span>

> [!NOTE]
> <span data-ttu-id="532d4-108">Hallo artikel [Azure IoT SDK's] [ lnk-hub-sdks] bevat informatie over hello Azure IoT SDK's waarmee u toobuild kunt apparaat- en back-end-apps.</span><span class="sxs-lookup"><span data-stu-id="532d4-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both device and back-end apps.</span></span>
> 
> 

<span data-ttu-id="532d4-109">toocomplete in deze zelfstudie hebt u Hallo volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="532d4-109">toocomplete this tutorial you need hello following:</span></span>

* <span data-ttu-id="532d4-110">Visual Studio 2015 of Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="532d4-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="532d4-111">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="532d4-111">An active Azure account.</span></span> <span data-ttu-id="532d4-112">Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.</span><span class="sxs-lookup"><span data-stu-id="532d4-112">If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.</span></span>

<span data-ttu-id="532d4-113">Als u Hallo gevolgd [aan de slag met apparaat horende] [ lnk-twin-tutorial] zelfstudie, u hebt al een IoT-hub en een apparaat-id genoemd **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="532d4-113">If you followed hello [Get started with device twins][lnk-twin-tutorial] tutorial, you already have an IoT hub and a device identity called **myDeviceId**.</span></span> <span data-ttu-id="532d4-114">In dat geval kunt u overslaan toohello [maken Hallo gesimuleerde apparaattoepassing] [ lnk-how-to-configure-createapp] sectie.</span><span class="sxs-lookup"><span data-stu-id="532d4-114">In that case, you can skip toohello [Create hello simulated device app][lnk-how-to-configure-createapp] section.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<a id="#create-the-simulated-device-app"></a>
## <a name="create-hello-simulated-device-app"></a><span data-ttu-id="532d4-115">Hallo gesimuleerde apparaattoepassing maken</span><span class="sxs-lookup"><span data-stu-id="532d4-115">Create hello simulated device app</span></span>
<span data-ttu-id="532d4-116">In deze sectie maakt u een .NET-consoletoepassing die verbinding tooyour hub als maakt **myDeviceId**, wordt gewacht op een gewenste configuratie-update en vervolgens rapporten updates op Hallo gesimuleerde update configuratieproces.</span><span class="sxs-lookup"><span data-stu-id="532d4-116">In this section, you create a .NET console app that connects tooyour hub as **myDeviceId**, waits for a desired configuration update and then reports updates on hello simulated configuration update process.</span></span>

1. <span data-ttu-id="532d4-117">Maak in Visual Studio een nieuw Visual C# Classic Windows Desktop-project met behulp van Hallo **consoletoepassing** projectsjabloon.</span><span class="sxs-lookup"><span data-stu-id="532d4-117">In Visual Studio, create a new Visual C# Windows Classic Desktop project by using hello **Console Application** project template.</span></span> <span data-ttu-id="532d4-118">Naam Hallo project **SimulateDeviceConfiguration**.</span><span class="sxs-lookup"><span data-stu-id="532d4-118">Name hello project **SimulateDeviceConfiguration**.</span></span>
   
    ![Nieuwe Visual C# klassieke Windows-apparaat-app][img-createdeviceapp]

1. <span data-ttu-id="532d4-120">Klik in Solution Explorer met de rechtermuisknop op Hallo **SimulateDeviceConfiguration** project en klik vervolgens op **NuGet-pakketten beheren...** .</span><span class="sxs-lookup"><span data-stu-id="532d4-120">In Solution Explorer, right-click hello **SimulateDeviceConfiguration** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="532d4-121">In Hallo **NuGet Package Manager** Selecteer **Bladeren** en zoek naar **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="532d4-121">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="532d4-122">Selecteer **installeren** tooinstall hello **Microsoft.Azure.Devices.Client** Inpakken en accepteer de gebruiksvoorwaarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="532d4-122">Select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="532d4-123">Deze procedure downloadt, installeert en voegt u een verwijzing toohello [Azure IoT-device SDK] [ lnk-nuget-client-sdk] NuGet-pakket en de bijbehorende afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="532d4-123">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet-Pakketbeheer venster Client-app][img-clientnuget]
1. <span data-ttu-id="532d4-125">Voeg de volgende Hallo `using` instructies boven Hallo Hallo **Program.cs** bestand:</span><span class="sxs-lookup"><span data-stu-id="532d4-125">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;
        using Newtonsoft.Json;

1. <span data-ttu-id="532d4-126">Hallo na toohello velden toevoegen **programma** klasse.</span><span class="sxs-lookup"><span data-stu-id="532d4-126">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="532d4-127">Vervang Hallo tijdelijke aanduidingswaarde met de verbindingsreeks van het Hallo-apparaat die u hebt genoteerd in de vorige sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="532d4-127">Replace hello placeholder value with hello device connection string that you noted in hello previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;
        static TwinCollection reportedProperties = new TwinCollection();

1. <span data-ttu-id="532d4-128">Hallo na methode toohello toevoegen **programma** klasse:</span><span class="sxs-lookup"><span data-stu-id="532d4-128">Add hello following method toohello **Program** class:</span></span>
 
        public static void InitClient()
        {
            try
            {
                Console.WriteLine("Connecting toohub");
                Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }
    <span data-ttu-id="532d4-129">Hallo **Client** object bevat alle Hallo-methoden die u nodig hebt toointeract met apparaat horende van Hallo-apparaat.</span><span class="sxs-lookup"><span data-stu-id="532d4-129">hello **Client** object exposes all hello methods you require toointeract with device twins from hello device.</span></span> <span data-ttu-id="532d4-130">Hallo hierboven weergegeven code initialiseert Hallo **Client** object, en vervolgens haalt Hallo apparaat twin voor **myDeviceId**.</span><span class="sxs-lookup"><span data-stu-id="532d4-130">hello code shown above, initializes hello **Client** object, and then retrieves hello device twin for **myDeviceId**.</span></span>

1. <span data-ttu-id="532d4-131">Hallo na methode toohello toevoegen **programma** klasse.</span><span class="sxs-lookup"><span data-stu-id="532d4-131">Add hello following method toohello **Program** class.</span></span> <span data-ttu-id="532d4-132">Deze methode stelt Hallo Beginwaarden telemetrie op Hallo lokale apparaat en klikt u vervolgens updates apparaat twin Hallo.</span><span class="sxs-lookup"><span data-stu-id="532d4-132">This method sets hello initial values of telemetry on hello local device and then updates hello device twin.</span></span>

        public static async void InitTelemetry()
        {
            try
            {
                Console.WriteLine("Report initial telemetry config:");
                TwinCollection telemetryConfig = new TwinCollection();
                
                telemetryConfig["configId"] = "0";
                telemetryConfig["sendFrequency"] = "24h";
                reportedProperties["telemetryConfig"] = telemetryConfig;
                Console.WriteLine(JsonConvert.SerializeObject(reportedProperties));

                await Client.UpdateReportedPropertiesAsync(reportedProperties);
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

1. <span data-ttu-id="532d4-133">Hallo na methode toohello toevoegen **programma** klasse.</span><span class="sxs-lookup"><span data-stu-id="532d4-133">Add hello following method toohello **Program** class.</span></span> <span data-ttu-id="532d4-134">Dit is een terugbelactie die een wijziging in detecteert *gewenst eigenschappen* in Hallo apparaat twin.</span><span class="sxs-lookup"><span data-stu-id="532d4-134">This is a callback which will detect a change in *desired properties* in hello device twin.</span></span>

        private static async Task OnDesiredPropertyChanged(TwinCollection desiredProperties, object userContext)
        {
            try
            {
                Console.WriteLine("Desired property change:");
                Console.WriteLine(JsonConvert.SerializeObject(desiredProperties));

                var currentTelemetryConfig = reportedProperties["telemetryConfig"];
                var desiredTelemetryConfig = desiredProperties["telemetryConfig"];

                if ((desiredTelemetryConfig != null) && (desiredTelemetryConfig["configId"] != currentTelemetryConfig["configId"]))
                {
                    Console.WriteLine("\nInitiating config change");
                    currentTelemetryConfig["status"] = "Pending";
                    currentTelemetryConfig["pendingConfig"] = desiredTelemetryConfig;

                    await Client.UpdateReportedPropertiesAsync(reportedProperties);

                    CompleteConfigChange();
                }
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

    <span data-ttu-id="532d4-135">Deze methode updates Hallo gerapporteerd eigenschappen op Hallo lokale twin apparaatobject met Hallo configuratie updatestatus aanvraag en sets hello te**in behandeling**, en vervolgens de updates Hallo apparaat twin op Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="532d4-135">This method updates hello reported properties on hello local device twin object with hello configuration update request and sets hello status too**Pending**, then updates hello device twin on hello service.</span></span> <span data-ttu-id="532d4-136">Nadat het Hallo apparaat twin is bijgewerkt, Hallo configuratiewijziging is voltooid door het Hallo-methode aanroepen `CompleteConfigChange` in het volgende punt Hallo beschreven.</span><span class="sxs-lookup"><span data-stu-id="532d4-136">After successfully updating hello device twin, it completes hello config change by calling hello method `CompleteConfigChange` described in hello next point.</span></span>

1. <span data-ttu-id="532d4-137">Hallo na methode toohello toevoegen **programma** klasse.</span><span class="sxs-lookup"><span data-stu-id="532d4-137">Add hello following method toohello **Program** class.</span></span> <span data-ttu-id="532d4-138">Deze methode wordt gesimuleerd apparaat opnieuw instellen en vervolgens updates Hallo eigenschappen van de lokale gerapporteerde status hello te stellen**geslaagd** en verwijdert Hallo **pendingConfig** element.</span><span class="sxs-lookup"><span data-stu-id="532d4-138">This method simulates a device reset, then updates hello local reported properties setting hello status too**Success** and removes hello **pendingConfig** element.</span></span> <span data-ttu-id="532d4-139">Hallo apparaat twin op Hallo-service wordt vervolgens bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="532d4-139">It then updates hello device twin on hello service.</span></span> 

        public static async void CompleteConfigChange()
        {
            try
            {
                var currentTelemetryConfig = reportedProperties["telemetryConfig"];

                Console.WriteLine("\nSimulating device reset");
                await Task.Delay(30000); 

                Console.WriteLine("\nCompleting config change");
                currentTelemetryConfig["configId"] = currentTelemetryConfig["pendingConfig"]["configId"];
                currentTelemetryConfig["sendFrequency"] = currentTelemetryConfig["pendingConfig"]["sendFrequency"];
                currentTelemetryConfig["status"] = "Success";
                currentTelemetryConfig["pendingConfig"] = null;

                await Client.UpdateReportedPropertiesAsync(reportedProperties);
                Console.WriteLine("Config change complete \nPress any key tooexit.");
            }
            catch (AggregateException ex)
            {
                foreach (Exception exception in ex.InnerExceptions)
                {
                    Console.WriteLine();
                    Console.WriteLine("Error in sample: {0}", exception);
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", ex.Message);
            }
        }

1. <span data-ttu-id="532d4-140">Ten slotte toevoegen Hallo volgende regels toohello **Main** methode:</span><span class="sxs-lookup"><span data-stu-id="532d4-140">Finally add hello following lines toohello **Main** method:</span></span>

        try
        {
            InitClient();
            InitTelemetry();

            Console.WriteLine("Wait for desired telemetry...");
            Client.SetDesiredPropertyUpdateCallback(OnDesiredPropertyChanged, null).Wait();
            Console.ReadKey();
        }
        catch (AggregateException ex)
        {
            foreach (Exception exception in ex.InnerExceptions)
            {
                Console.WriteLine();
                Console.WriteLine("Error in sample: {0}", exception);
            }
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }

   > [!NOTE]
   > <span data-ttu-id="532d4-141">Deze zelfstudie wordt een gedrag voor updates voor gelijktijdige configuratie niet simuleren.</span><span class="sxs-lookup"><span data-stu-id="532d4-141">This tutorial does not simulate any behavior for concurrent configuration updates.</span></span> <span data-ttu-id="532d4-142">Bepaalde configuratie-update-processen mogelijk wijzigingen van de doelconfiguratie kunnen tooaccommodate terwijl Hallo update wordt uitgevoerd, enkele mogelijk tooqueue ze en sommige kan weigeren met een fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="532d4-142">Some configuration update processes might be able tooaccommodate changes of target configuration while hello update is running, some might have tooqueue them, and some could reject them with an error condition.</span></span> <span data-ttu-id="532d4-143">Zorg ervoor dat tooconsider Hallo gewenste gedrag voor uw specifieke configuratieproces en Hallo juiste logica toevoegen voordat u begint Hallo configuratiewijziging.</span><span class="sxs-lookup"><span data-stu-id="532d4-143">Make sure tooconsider hello desired behavior for your specific configuration process, and add hello appropriate logic before initiating hello configuration change.</span></span>
   > 
   > 
1. <span data-ttu-id="532d4-144">Hallo-oplossing opzetten en Voer Hallo apparaattoepassing vanuit Visual Studio door te klikken op **F5**.</span><span class="sxs-lookup"><span data-stu-id="532d4-144">Build hello solution and then run hello device app from Visual Studio by clicking **F5**.</span></span> <span data-ttu-id="532d4-145">U ziet op Hallo uitvoer console Hallo-berichten die aangeeft dat uw gesimuleerde apparaat is Hallo apparaat twin ophalen, Hallo telemetrie instellen en wijzigen van de gewenste eigenschap wachten.</span><span class="sxs-lookup"><span data-stu-id="532d4-145">On hello output console, you should see hello messages indicating that your simulated device is retrieving hello device twin, setting up hello telemetry, and waiting for desired property change.</span></span> <span data-ttu-id="532d4-146">Houd Hallo-app die wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="532d4-146">Keep hello app running.</span></span>

## <a name="create-hello-service-app"></a><span data-ttu-id="532d4-147">Hallo-service-app maken</span><span class="sxs-lookup"><span data-stu-id="532d4-147">Create hello service app</span></span>
<span data-ttu-id="532d4-148">In deze sectie maakt u een .NET-consoletoepassing die updates Hallo *gewenst eigenschappen* op Hallo apparaat twin gekoppeld **myDeviceId** met een nieuwe telemetrie configuration-object.</span><span class="sxs-lookup"><span data-stu-id="532d4-148">In this section, you will create a .NET console app that updates hello *desired properties* on hello device twin associated with **myDeviceId** with a new telemetry configuration object.</span></span> <span data-ttu-id="532d4-149">Vervolgens vraagt Hallo apparaat horende opgeslagen in Hallo IoT-hub en toont Hallo verschil tussen Hallo gewenst en configuraties van Hallo apparaat gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="532d4-149">It then queries hello device twins stored in hello IoT hub and shows hello difference between hello desired and reported configurations of hello device.</span></span>

1. <span data-ttu-id="532d4-150">Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toohello huidige oplossing met behulp van Hallo **consoletoepassing** projectsjabloon.</span><span class="sxs-lookup"><span data-stu-id="532d4-150">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="532d4-151">Naam Hallo project **SetDesiredConfigurationAndQuery**.</span><span class="sxs-lookup"><span data-stu-id="532d4-151">Name hello project **SetDesiredConfigurationAndQuery**.</span></span>
   
    ![Nieuw Windows Classic Desktop-project in Visual C#][img-createapp]
1. <span data-ttu-id="532d4-153">Klik in Solution Explorer met de rechtermuisknop op Hallo **SetDesiredConfigurationAndQuery** project en klik vervolgens op **NuGet-pakketten beheren...** .</span><span class="sxs-lookup"><span data-stu-id="532d4-153">In Solution Explorer, right-click hello **SetDesiredConfigurationAndQuery** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="532d4-154">In Hallo **NuGet Package Manager** Selecteer **Bladeren**, zoeken naar **microsoft.azure.devices**, selecteer **installeren** tooinstall Hallo **Microsoft.Azure.Devices** Inpakken en accepteer de gebruiksvoorwaarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="532d4-154">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="532d4-155">Deze procedure downloadt, installeert en voegt u een verwijzing toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet-pakket en de bijbehorende afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="532d4-155">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Sluit het venster Nuget Package Manager.][img-servicenuget]
1. <span data-ttu-id="532d4-157">Voeg de volgende Hallo `using` instructies boven Hallo Hallo **Program.cs** bestand:</span><span class="sxs-lookup"><span data-stu-id="532d4-157">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices;
        using System.Threading;
        using Newtonsoft.Json;
1. <span data-ttu-id="532d4-158">Hallo na toohello velden toevoegen **programma** klasse.</span><span class="sxs-lookup"><span data-stu-id="532d4-158">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="532d4-159">Vervang Hallo tijdelijke aanduidingswaarde met IoT Hub-verbindingsreeks voor Hallo-hub die u hebt gemaakt in de vorige sectie Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="532d4-159">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static RegistryManager registryManager;
        static string connectionString = "{iot hub connection string}";
1. <span data-ttu-id="532d4-160">Hallo na methode toohello toevoegen **programma** klasse:</span><span class="sxs-lookup"><span data-stu-id="532d4-160">Add hello following method toohello **Program** class:</span></span>
   
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
   
    <span data-ttu-id="532d4-161">Hallo **register** object beschrijft alle Hallo methoden vereist toointeract met apparaat horende van Hallo-service.</span><span class="sxs-lookup"><span data-stu-id="532d4-161">hello **Registry** object exposes all hello methods required toointeract with device twins from hello service.</span></span> <span data-ttu-id="532d4-162">Deze code initialiseert Hallo **register** -object is opgehaald Hallo apparaat twin voor **myDeviceId**, en werkt vervolgens de gewenste eigenschappen met een nieuwe telemetrie configuration-object.</span><span class="sxs-lookup"><span data-stu-id="532d4-162">This code initializes hello **Registry** object, retrieves hello device twin for **myDeviceId**, and then updates its desired properties with a new telemetry configuration object.</span></span>
    <span data-ttu-id="532d4-163">Daarna wordt opgevraagd Hallo apparaat horende opgeslagen in de IoT-hub Hallo elke 10 seconden en afdrukken bestellen Hallo gewenst en telemetrie configuraties gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="532d4-163">After that, it queries hello device twins stored in hello IoT hub every 10 seconds, and prints hello desired and reported telemetry configurations.</span></span> <span data-ttu-id="532d4-164">Raadpleeg toohello [IoT Hub-querytaal] [ lnk-query] toolearn hoe toogenerate rich op alle apparaten in uw rapporten.</span><span class="sxs-lookup"><span data-stu-id="532d4-164">Refer toohello [IoT Hub query language][lnk-query] toolearn how toogenerate rich reports across all your devices.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="532d4-165">Deze toepassing een IoT Hub query elke 10 seconden ter illustratie.</span><span class="sxs-lookup"><span data-stu-id="532d4-165">This application queries IoT Hub every 10 seconds for illustrative purposes.</span></span> <span data-ttu-id="532d4-166">Gebruik een query toogenerate gebruikersgerichte rapporten over veel apparaten, en niet toodetect wijzigingen.</span><span class="sxs-lookup"><span data-stu-id="532d4-166">Use queries toogenerate user-facing reports across many devices, and not toodetect changes.</span></span> <span data-ttu-id="532d4-167">Als uw oplossing realtime meldingen over apparaatgebeurtenissen vereist, gebruikt u [twin meldingen][lnk-twin-notifications].</span><span class="sxs-lookup"><span data-stu-id="532d4-167">If your solution requires real-time notifications of device events, use [twin notifications][lnk-twin-notifications].</span></span>
   > 
   > 
1. <span data-ttu-id="532d4-168">Voeg regels toohello na Hallo **Main** methode:</span><span class="sxs-lookup"><span data-stu-id="532d4-168">Finally, add hello following lines toohello **Main** method:</span></span>
   
        registryManager = RegistryManager.CreateFromConnectionString(connectionString);
        SetDesiredConfigurationAndQuery();
        Console.WriteLine("Press any key tooquit.");
        Console.ReadLine();
1. <span data-ttu-id="532d4-169">Open in Solution Explorer hello, Hallo **opstartprojecten instellen...**  en zorg ervoor dat Hallo **actie** voor **SetDesiredConfigurationAndQuery** project **Start**.</span><span class="sxs-lookup"><span data-stu-id="532d4-169">In hello Solution Explorer, open hello **Set StartUp projects...** and make sure hello **Action** for **SetDesiredConfigurationAndQuery** project is **Start**.</span></span> <span data-ttu-id="532d4-170">Hallo-oplossing bouwen.</span><span class="sxs-lookup"><span data-stu-id="532d4-170">Build hello solution.</span></span>
1. <span data-ttu-id="532d4-171">Met **SimulateDeviceConfiguration** apparaat app wordt uitgevoerd, service-app uitvoeren Hallo vanuit Visual Studio met **F5**.</span><span class="sxs-lookup"><span data-stu-id="532d4-171">With **SimulateDeviceConfiguration** device app running, run hello service app from Visual Studio using **F5**.</span></span> <span data-ttu-id="532d4-172">Er is gemeld Hallo-configuratie wijzigen vanuit **in behandeling** te**geslaagd** verzenden met de nieuwe actief Hallo frequentie van vijf minuten in plaats van 24 uur.</span><span class="sxs-lookup"><span data-stu-id="532d4-172">You should see hello reported configuration change from **Pending** too**Success** with hello new active send frequency of five minutes instead of 24 hours.</span></span>

 ![Apparaten die zijn geconfigureerd][img-deviceconfigured]
   
   > [!IMPORTANT]
   > <span data-ttu-id="532d4-174">Er is een vertraging van up tooa minuut tussen Hallo apparaat rapport opnieuw en Hallo queryresultaat.</span><span class="sxs-lookup"><span data-stu-id="532d4-174">There is a delay of up tooa minute between hello device report operation and hello query result.</span></span> <span data-ttu-id="532d4-175">Dit is tooenable Hallo query infrastructuur toowork op zeer grote schaal.</span><span class="sxs-lookup"><span data-stu-id="532d4-175">This is tooenable hello query infrastructure toowork at very high scale.</span></span> <span data-ttu-id="532d4-176">tooretrieve consistente weergaven van een enkel apparaat twin gebruiken Hallo **getDeviceTwin** methode in Hallo **register** klasse.</span><span class="sxs-lookup"><span data-stu-id="532d4-176">tooretrieve consistent views of a single device twin use hello **getDeviceTwin** method in hello **Registry** class.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="532d4-177">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="532d4-177">Next steps</span></span>
<span data-ttu-id="532d4-178">In deze zelfstudie stelt u een gewenste configuratie als *gewenst eigenschappen* van Hallo oplossing back-end en een apparaat app toodetect die wijzigen en een updateproces van meerdere stappen rapportage van de status ervan via Hallo gerapporteerd simuleren geschreven Eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="532d4-178">In this tutorial, you set a desired configuration as *desired properties* from hello solution back end, and wrote a device app toodetect that change and simulate a multi-step update process reporting its status through hello reported properties.</span></span>

<span data-ttu-id="532d4-179">Gebruik Hallo resources toolearn hoe volgende aan:</span><span class="sxs-lookup"><span data-stu-id="532d4-179">Use hello following resources toolearn how to:</span></span>

* <span data-ttu-id="532d4-180">verzenden van telemetrie vanaf apparaten Hello [aan de slag met IoT Hub] [ lnk-iothub-getstarted] zelfstudie</span><span class="sxs-lookup"><span data-stu-id="532d4-180">send telemetry from devices with hello [Get started with IoT Hub][lnk-iothub-getstarted] tutorial,</span></span>
* <span data-ttu-id="532d4-181">plannen of uitvoeren van bewerkingen op grote sets van apparaten Zie Hallo [planning en broadcast taken] [ lnk-schedule-jobs] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="532d4-181">schedule or perform operations on large sets of devices see hello [Schedule and broadcast jobs][lnk-schedule-jobs] tutorial.</span></span>
* <span data-ttu-id="532d4-182">beheren van apparaten interactief (zoals het inschakelen van een ventilator van een gebruiker beheerde app), met Hallo [direct methoden gebruiken] [ lnk-methods-tutorial] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="532d4-182">control devices interactively (such as turning on a fan from a user-controlled app), with hello [Use direct methods][lnk-methods-tutorial] tutorial.</span></span>

<!-- images -->
[img-servicenuget]: media/iot-hub-csharp-csharp-twin-how-to-configure/servicesdknuget.png
[img-createapp]: media/iot-hub-csharp-csharp-twin-how-to-configure/createnetapp.png
[img-deviceconfigured]: media/iot-hub-csharp-csharp-twin-how-to-configure/deviceconfigured.png
[img-createdeviceapp]: media/iot-hub-csharp-csharp-twin-how-to-configure/createdeviceapp.png
[img-clientnuget]: media/iot-hub-csharp-csharp-twin-how-to-configure/devicesdknuget.png
[img-deviceconfigured]: media/iot-hub-csharp-csharp-twin-how-to-configure/deviceconfigured.png


<!-- links -->
[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/1.1.0/

[lnk-query]: iot-hub-devguide-query-language.md
[lnk-twin-notifications]: iot-hub-devguide-device-twins.md#back-end-operations
[lnk-twin-tutorial]: iot-hub-csharp-csharp-twin-getstarted.md
[lnk-schedule-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-iothub-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-how-to-configure-createapp]: iot-hub-csharp-csharp-twin-how-to-configure.md#create-the-simulated-device-app
