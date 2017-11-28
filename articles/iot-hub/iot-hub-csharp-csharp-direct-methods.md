---
title: Azure IoT Hub aaaUse directe methoden (.NET/.NET) | Microsoft Docs
description: Hoe Azure IoT Hub toouse directe methoden. U gebruikt hello Azure IoT-device SDK voor .NET tooimplement een gesimuleerde apparaattoepassing met een directe methode en hello Azure IoT service SDK voor .NET tooimplement een service-app die Hallo directe methode aanroept.
services: iot-hub
documentationcenter: 
author: dsk-2015
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: dkshir
ms.openlocfilehash: d4fa093a99558ec6faf294c2583a14a722b9ac03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-netnet"></a><span data-ttu-id="18240-104">Directe methoden (.NET/.NET) gebruiken</span><span class="sxs-lookup"><span data-stu-id="18240-104">Use direct methods (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="18240-105">In deze zelfstudie zijn we continu toodevelop twee .NET-console apps:</span><span class="sxs-lookup"><span data-stu-id="18240-105">In this tutorial, we are going toodevelop two .NET console apps:</span></span>

* <span data-ttu-id="18240-106">**CallMethodOnDevice**, een back-end-app, die een methode wordt aangeroepen in de gesimuleerde apparaattoepassing Hallo en antwoord Hallo weergegeven.</span><span class="sxs-lookup"><span data-stu-id="18240-106">**CallMethodOnDevice**, a back-end app, which calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="18240-107">**SimulateDeviceMethods**, een consoletoepassing die overeenkomt met een apparaat tooyour IoT-hub te koppelen aan de apparaat-id Hallo eerder hebt gemaakt en toohello methode aangeroepen door Hallo cloud reageert.</span><span class="sxs-lookup"><span data-stu-id="18240-107">**SimulateDeviceMethods**, a console app which simulates a device connecting tooyour IoT hub with hello device identity created earlier, and responds toohello method called by hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="18240-108">Hallo artikel [Azure IoT SDK's] [ lnk-hub-sdks] bevat informatie over hello Azure IoT SDK's waarmee u toobuild beide toorun toepassingen op apparaten en de back-end van uw oplossing kunt.</span><span class="sxs-lookup"><span data-stu-id="18240-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="18240-109">toocomplete deze zelfstudie hebt u nodig:</span><span class="sxs-lookup"><span data-stu-id="18240-109">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="18240-110">Visual Studio 2015 of Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="18240-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="18240-111">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="18240-111">An active Azure account.</span></span> <span data-ttu-id="18240-112">(Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)</span><span class="sxs-lookup"><span data-stu-id="18240-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="18240-113">Als u toocreate Hallo apparaat-id via een programma in plaats daarvan wilt, lezen Hallo overeenkomstige sectie in Hallo [verbinding maken met uw gesimuleerde apparaat tooyour iothub met .NET] [ lnk-device-identity-csharp] artikel.</span><span class="sxs-lookup"><span data-stu-id="18240-113">If you want toocreate hello device identity programmatically instead, read hello corresponding section in hello [Connect your simulated device tooyour IoT hub using .NET][lnk-device-identity-csharp] article.</span></span>


## <a name="create-a-simulated-device-app"></a><span data-ttu-id="18240-114">Een gesimuleerde apparaattoepassing maken</span><span class="sxs-lookup"><span data-stu-id="18240-114">Create a simulated device app</span></span>
<span data-ttu-id="18240-115">In deze sectie maakt u een .NET-consoletoepassing die tooa methode met de naam door Hallo oplossing back-end reageert.</span><span class="sxs-lookup"><span data-stu-id="18240-115">In this section, you create a .NET console app that responds tooa method called by hello solution back end.</span></span>

1. <span data-ttu-id="18240-116">Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toohello huidige oplossing met behulp van Hallo **consoletoepassing** projectsjabloon.</span><span class="sxs-lookup"><span data-stu-id="18240-116">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="18240-117">Naam Hallo project **SimulateDeviceMethods**.</span><span class="sxs-lookup"><span data-stu-id="18240-117">Name hello project **SimulateDeviceMethods**.</span></span>
   
    ![Nieuwe Visual C# klassieke Windows-apparaat-app][img-createdeviceapp]
    
1. <span data-ttu-id="18240-119">Klik in Solution Explorer met de rechtermuisknop op Hallo **SimulateDeviceMethods** project en klik vervolgens op **NuGet-pakketten beheren...** .</span><span class="sxs-lookup"><span data-stu-id="18240-119">In Solution Explorer, right-click hello **SimulateDeviceMethods** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="18240-120">In Hallo **NuGet Package Manager** Selecteer **Bladeren** en zoek naar **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="18240-120">In hello **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="18240-121">Selecteer **installeren** tooinstall hello **Microsoft.Azure.Devices.Client** Inpakken en accepteer de gebruiksvoorwaarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="18240-121">Select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="18240-122">Deze procedure downloadt, installeert en voegt u een verwijzing toohello [Azure IoT-device SDK] [ lnk-nuget-client-sdk] NuGet-pakket en de bijbehorende afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="18240-122">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet-Pakketbeheer venster Client-app][img-clientnuget]
1. <span data-ttu-id="18240-124">Voeg de volgende Hallo `using` instructies boven Hallo Hallo **Program.cs** bestand:</span><span class="sxs-lookup"><span data-stu-id="18240-124">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;

1. <span data-ttu-id="18240-125">Hallo na toohello velden toevoegen **programma** klasse.</span><span class="sxs-lookup"><span data-stu-id="18240-125">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="18240-126">Vervang Hallo tijdelijke aanduidingswaarde met de verbindingsreeks van het Hallo-apparaat die u hebt genoteerd in de vorige sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="18240-126">Replace hello placeholder value with hello device connection string that you noted in hello previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. <span data-ttu-id="18240-127">Hallo tooimplement Hallo directe methode volgen op Hallo apparaat toevoegen:</span><span class="sxs-lookup"><span data-stu-id="18240-127">Add hello following tooimplement hello direct method on hello device:</span></span>

        static Task<MethodResponse> WriteLineToConsole(MethodRequest methodRequest, object userContext)
        {
            Console.WriteLine();
            Console.WriteLine("\t{0}", methodRequest.DataAsJson);
            Console.WriteLine("\nReturning response for method {0}", methodRequest.Name);

            string result = "'Input was written toolog.'";
            return Task.FromResult(new MethodResponse(Encoding.UTF8.GetBytes(result), 200));
        }

1. <span data-ttu-id="18240-128">Voeg code toohello na Hallo **Main** methode tooopen Hallo verbinding tooyour IoT hub en geïnitialiseerd Hallo methode listener:</span><span class="sxs-lookup"><span data-stu-id="18240-128">Finally, add hello following code toohello **Main** method tooopen hello connection tooyour IoT hub and initialize hello method listener:</span></span>
   
        try
        {
            Console.WriteLine("Connecting toohub");
            Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);

            // setup callback for "writeLine" method
            Client.SetMethodHandlerAsync("writeLine", WriteLineToConsole, null).Wait();
            Console.WriteLine("Waiting for direct method call\n Press enter tooexit.");
            Console.ReadLine();

            Console.WriteLine("Exiting...");

            // as a good practice, remove hello "writeLine" handler
            Client.SetMethodHandlerAsync("writeLine", null, null).Wait();
            Client.CloseAsync().Wait();
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }
        
1. <span data-ttu-id="18240-129">In Visual Studio Solution Explorer hello, met de rechtermuisknop op uw oplossing en klik op **Opstartprojecten instellen...** . Selecteer **één opstartproject**, en selecteer vervolgens Hallo **SimulateDeviceMethods** -project in het vervolgkeuzemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="18240-129">In hello Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select hello **SimulateDeviceMethods** project in hello dropdown menu.</span></span>        

> [!NOTE]
> <span data-ttu-id="18240-130">tookeep dingen eenvoudige, deze zelfstudie wordt niet geïmplementeerd voor een beleid voor opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="18240-130">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="18240-131">In productiecode moet u beleid voor opnieuw proberen (zoals verbinding opnieuw), zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="18240-131">In production code, you should implement retry policies (such as connection retry), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="18240-132">Een directe methode is aangeroepen voor een apparaat</span><span class="sxs-lookup"><span data-stu-id="18240-132">Call a direct method on a device</span></span>
<span data-ttu-id="18240-133">In deze sectie maakt maken u een .NET-consoletoepassing die een methode wordt aangeroepen in de gesimuleerde apparaattoepassing Hallo en wordt vervolgens weergegeven antwoord Hallo.</span><span class="sxs-lookup"><span data-stu-id="18240-133">In this section, you create a .NET console app that calls a method in hello simulated device app and then displays hello response.</span></span>

1. <span data-ttu-id="18240-134">Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toohello huidige oplossing met behulp van Hallo **consoletoepassing** projectsjabloon.</span><span class="sxs-lookup"><span data-stu-id="18240-134">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="18240-135">Zorg ervoor dat .NET Framework-versie Hallo 4.5.1 of later.</span><span class="sxs-lookup"><span data-stu-id="18240-135">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="18240-136">Naam Hallo project **CallMethodOnDevice**.</span><span class="sxs-lookup"><span data-stu-id="18240-136">Name hello project **CallMethodOnDevice**.</span></span>
   
    ![Nieuw Windows Classic Desktop-project in Visual C#][img-createserviceapp]
2. <span data-ttu-id="18240-138">Klik in Solution Explorer met de rechtermuisknop op Hallo **CallMethodOnDevice** project en klik vervolgens op **NuGet-pakketten beheren...** .</span><span class="sxs-lookup"><span data-stu-id="18240-138">In Solution Explorer, right-click hello **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="18240-139">In Hallo **NuGet Package Manager** Selecteer **Bladeren**, zoeken naar **microsoft.azure.devices**, selecteer **installeren** tooinstall Hallo **Microsoft.Azure.Devices** Inpakken en accepteer de gebruiksvoorwaarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="18240-139">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="18240-140">Deze procedure downloadt, installeert en voegt u een verwijzing toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet-pakket en de bijbehorende afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="18240-140">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Sluit het venster Nuget Package Manager.][img-servicenuget]

4. <span data-ttu-id="18240-142">Voeg de volgende Hallo `using` instructies boven Hallo Hallo **Program.cs** bestand:</span><span class="sxs-lookup"><span data-stu-id="18240-142">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="18240-143">Hallo na toohello velden toevoegen **programma** klasse.</span><span class="sxs-lookup"><span data-stu-id="18240-143">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="18240-144">Vervang Hallo tijdelijke aanduidingswaarde met IoT Hub-verbindingsreeks voor Hallo-hub die u hebt gemaakt in de vorige sectie Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="18240-144">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="18240-145">Hallo na methode toohello toevoegen **programma** klasse:</span><span class="sxs-lookup"><span data-stu-id="18240-145">Add hello following method toohello **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line toobe written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="18240-146">Deze methode wordt aangeroepen voor een directe methode met de naam `writeLine` op Hallo `myDeviceId` apparaat.</span><span class="sxs-lookup"><span data-stu-id="18240-146">This method invokes a direct method with name `writeLine` on hello `myDeviceId` device.</span></span> <span data-ttu-id="18240-147">Vervolgens worden Hallo respons van Hallo-apparaat op Hallo console geschreven.</span><span class="sxs-lookup"><span data-stu-id="18240-147">Then, it writes hello response provided by hello device on hello console.</span></span> <span data-ttu-id="18240-148">Houd er rekening mee hoe het is mogelijk toospecify een time-outwaarde voor Hallo apparaat toorespond.</span><span class="sxs-lookup"><span data-stu-id="18240-148">Note how it is possible toospecify a timeout value for hello device toorespond.</span></span>
7. <span data-ttu-id="18240-149">Voeg regels toohello na Hallo **Main** methode:</span><span class="sxs-lookup"><span data-stu-id="18240-149">Finally, add hello following lines toohello **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

1. <span data-ttu-id="18240-150">In Visual Studio Solution Explorer hello, met de rechtermuisknop op uw oplossing en klik op **Opstartprojecten instellen...** . Selecteer **één opstartproject**, en selecteer vervolgens Hallo **CallMethodOnDevice** -project in het vervolgkeuzemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="18240-150">In hello Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select hello **CallMethodOnDevice** project in hello dropdown menu.</span></span>

## <a name="run-hello-applications"></a><span data-ttu-id="18240-151">Hallo-toepassingen uitvoeren</span><span class="sxs-lookup"><span data-stu-id="18240-151">Run hello applications</span></span>
<span data-ttu-id="18240-152">U bent nu klaar toorun Hallo toepassingen.</span><span class="sxs-lookup"><span data-stu-id="18240-152">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="18240-153">Uitvoeren van .NET-apparaattoepassing Hallo **SimulateDeviceMethods**.</span><span class="sxs-lookup"><span data-stu-id="18240-153">Run hello .NET device app **SimulateDeviceMethods**.</span></span> <span data-ttu-id="18240-154">Deze zou moeten starten luisteren naar methodeaanroepen van uw IoT-Hub:</span><span class="sxs-lookup"><span data-stu-id="18240-154">It should start listening for method calls from your IoT Hub:</span></span> 

    ![Apparaat-app uitvoeren][img-deviceapprun]
1. <span data-ttu-id="18240-156">Nu dat het Hallo-apparaat is verbonden en Hallo .NET wacht methode aanroepen, voer **CallMethodOnDevice** app tooinvoke Hallo methode in de gesimuleerde apparaattoepassing Hallo.</span><span class="sxs-lookup"><span data-stu-id="18240-156">Now that hello device is connected and waiting for method invocations, run hello .NET **CallMethodOnDevice** app tooinvoke hello method in hello simulated device app.</span></span> <span data-ttu-id="18240-157">U ziet Hallo apparaat antwoord is geschreven in Hallo-console.</span><span class="sxs-lookup"><span data-stu-id="18240-157">You should see hello device response written in hello console.</span></span>
   
    ![Service-app uitvoeren][img-serviceapprun]
1. <span data-ttu-id="18240-159">Hallo apparaat reageert vervolgens toohello methode door dit bericht afdrukken:</span><span class="sxs-lookup"><span data-stu-id="18240-159">hello device then reacts toohello method by printing this message:</span></span>
   
    ![Directe methode aangeroepen op Hallo-apparaat][img-directmethodinvoked]

## <a name="next-steps"></a><span data-ttu-id="18240-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="18240-161">Next steps</span></span>
<span data-ttu-id="18240-162">In deze zelfstudie maakt u een nieuwe iothub geconfigureerd in hello Azure-portal en vervolgens een apparaat-id in de id-register Hallo iothub hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="18240-162">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="18240-163">U hebt deze apparaat-id tooenable Hallo gesimuleerd apparaat app tooreact toomethods aangeroepen door Hallo cloud gebruikt.</span><span class="sxs-lookup"><span data-stu-id="18240-163">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="18240-164">Hebt u ook een app die wordt aangeroepen methoden op Hallo apparaat en geeft weer Hallo-antwoord van Hallo-apparaat hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="18240-164">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span> 

<span data-ttu-id="18240-165">toocontinue aan de slag met IoT Hub en tooexplore raadpleegt u andere IoT-scenario's:</span><span class="sxs-lookup"><span data-stu-id="18240-165">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="18240-166">[Aan de slag met IoT Hub]</span><span class="sxs-lookup"><span data-stu-id="18240-166">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="18240-167">[Taken plannen op meerdere apparaten][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="18240-167">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="18240-168">toolearn hoe tooextend uw IoT-oplossing en schema-methode aanroepen op meerdere apparaten, raadpleegt u Hallo [planning en broadcast taken] [ lnk-tutorial-jobs] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="18240-168">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- Images. -->
[img-createdeviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-device-app.png
[img-clientnuget]: ./media/iot-hub-csharp-csharp-direct-methods/device-app-nuget.png
[img-createserviceapp]: ./media/iot-hub-csharp-csharp-direct-methods/create-service-app.png
[img-servicenuget]: ./media/iot-hub-csharp-csharp-direct-methods/service-app-nuget.png
[img-deviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-device-app.png
[img-serviceapprun]: ./media/iot-hub-csharp-csharp-direct-methods/run-service-app.png
[img-directmethodinvoked]: ./media/iot-hub-csharp-csharp-direct-methods/direct-method-invoked.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-nuget-client-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-device-identity-csharp]: iot-hub-csharp-csharp-getstarted.md#DeviceIdentity_csharp

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md

[Aan de slag met IoT Hub]: iot-hub-node-node-getstarted.md
