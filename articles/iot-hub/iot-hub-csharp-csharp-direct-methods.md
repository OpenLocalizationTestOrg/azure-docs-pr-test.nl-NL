---
title: Gebruik Azure IoT Hub direct methoden (.NET/.NET) | Microsoft Docs
description: Het gebruik van Azure IoT Hub rechtstreekse methoden. U het apparaat met Azure IoT SDK voor .NET gebruiken voor het implementeren van een gesimuleerde apparaattoepassing met een directe methode en de service Azure IoT SDK voor .NET voor het implementeren van een service-app die de directe methode aanroept.
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
ms.openlocfilehash: 9ce1fbebb6417c10618aa182e3c1d9ddf8132fb6
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/29/2017
---
# <a name="use-direct-methods-netnet"></a><span data-ttu-id="e8886-104">Directe methoden (.NET/.NET) gebruiken</span><span class="sxs-lookup"><span data-stu-id="e8886-104">Use direct methods (.NET/.NET)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="e8886-105">In deze zelfstudie gaan we twee .NET-console-apps ontwikkelen:</span><span class="sxs-lookup"><span data-stu-id="e8886-105">In this tutorial, we are going to develop two .NET console apps:</span></span>

* <span data-ttu-id="e8886-106">**CallMethodOnDevice**, een back-end-app, die een methode wordt aangeroepen in de gesimuleerde apparaattoepassing en het antwoord weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e8886-106">**CallMethodOnDevice**, a back-end app, which calls a method in the simulated device app and displays the response.</span></span>
* <span data-ttu-id="e8886-107">**SimulateDeviceMethods**, een consoletoepassing waarmee een verbinding te maken met uw IoT-hub aan de apparaat-id apparaat simuleert eerder hebt gemaakt en reageert de methode wordt aangeroepen door de cloud.</span><span class="sxs-lookup"><span data-stu-id="e8886-107">**SimulateDeviceMethods**, a console app which simulates a device connecting to your IoT hub with the device identity created earlier, and responds to the method called by the cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="e8886-108">Het artikel [Azure IoT-SDK's][lnk-hub-sdks] bevat informatie over de verschillende Azure IoT-SDK's die u kunt gebruiken om beide toepassingen zo te maken dat ze zowel op het apparaat als op de back-end van uw oplossing kunnen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e8886-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="e8886-109">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="e8886-109">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="e8886-110">Visual Studio 2015 of Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="e8886-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="e8886-111">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="e8886-111">An active Azure account.</span></span> <span data-ttu-id="e8886-112">(Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)</span><span class="sxs-lookup"><span data-stu-id="e8886-112">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity-portal](../../includes/iot-hub-get-started-create-device-identity-portal.md)]

<span data-ttu-id="e8886-113">Als u de apparaat-id in plaats daarvan programmatisch maken wilt, leest u de bijbehorende sectie in het [uw gesimuleerde apparaat verbonden met uw iothub met .NET] [ lnk-device-identity-csharp] artikel.</span><span class="sxs-lookup"><span data-stu-id="e8886-113">If you want to create the device identity programmatically instead, read the corresponding section in the [Connect your simulated device to your IoT hub using .NET][lnk-device-identity-csharp] article.</span></span>


## <a name="create-a-simulated-device-app"></a><span data-ttu-id="e8886-114">Een gesimuleerde apparaattoepassing maken</span><span class="sxs-lookup"><span data-stu-id="e8886-114">Create a simulated device app</span></span>
<span data-ttu-id="e8886-115">In deze sectie maakt u een .NET-consoletoepassing dat met een methode aangeroepen door de oplossing voor back-end overeenkomt.</span><span class="sxs-lookup"><span data-stu-id="e8886-115">In this section, you create a .NET console app that responds to a method called by the solution back end.</span></span>

1. <span data-ttu-id="e8886-116">Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toe aan de huidige oplossing met behulp van de projectsjabloon **Console Application**.</span><span class="sxs-lookup"><span data-stu-id="e8886-116">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="e8886-117">Noem het project **SimulateDeviceMethods**.</span><span class="sxs-lookup"><span data-stu-id="e8886-117">Name the project **SimulateDeviceMethods**.</span></span>
   
    ![Nieuwe Visual C# klassieke Windows-apparaat-app][img-createdeviceapp]
    
1. <span data-ttu-id="e8886-119">Klik in Solution Explorer met de rechtermuisknop op de **SimulateDeviceMethods** project en klik vervolgens op **NuGet-pakketten beheren...** .</span><span class="sxs-lookup"><span data-stu-id="e8886-119">In Solution Explorer, right-click the **SimulateDeviceMethods** project, and then click **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="e8886-120">In de **NuGet Package Manager** Selecteer **Bladeren** en zoek naar **microsoft.azure.devices.client**.</span><span class="sxs-lookup"><span data-stu-id="e8886-120">In the **NuGet Package Manager** window, select **Browse** and search for **microsoft.azure.devices.client**.</span></span> <span data-ttu-id="e8886-121">Selecteer **installeren** voor het installeren van de **Microsoft.Azure.Devices.Client** Inpakken en accepteer de gebruiksvoorwaarden.</span><span class="sxs-lookup"><span data-stu-id="e8886-121">Select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span></span> <span data-ttu-id="e8886-122">Deze procedure downloadt, installeert en voegt u een verwijzing naar de [Azure IoT-device SDK] [ lnk-nuget-client-sdk] NuGet-pakket en de bijbehorende afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="e8886-122">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK][lnk-nuget-client-sdk] NuGet package and its dependencies.</span></span>
   
    ![NuGet-Pakketbeheer venster Client-app][img-clientnuget]
1. <span data-ttu-id="e8886-124">Voeg aan het begin van het bestand **Program.cs** de volgende `using` instructies toe:</span><span class="sxs-lookup"><span data-stu-id="e8886-124">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using Microsoft.Azure.Devices.Client;
        using Microsoft.Azure.Devices.Shared;

1. <span data-ttu-id="e8886-125">Voeg de volgende velden toe aan de klasse **Program**:</span><span class="sxs-lookup"><span data-stu-id="e8886-125">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="e8886-126">Vervang de tijdelijke aanduidingswaarde met de verbindingsreeks voor apparaten die u in de vorige sectie hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="e8886-126">Replace the placeholder value with the device connection string that you noted in the previous section.</span></span>
   
        static string DeviceConnectionString = "HostName=<yourIotHubName>.azure-devices.net;DeviceId=<yourIotDeviceName>;SharedAccessKey=<yourIotDeviceAccessKey>";
        static DeviceClient Client = null;

1. <span data-ttu-id="e8886-127">Voeg de volgende voor het implementeren van de directe methode op het apparaat:</span><span class="sxs-lookup"><span data-stu-id="e8886-127">Add the following to implement the direct method on the device:</span></span>

        static Task<MethodResponse> WriteLineToConsole(MethodRequest methodRequest, object userContext)
        {
            Console.WriteLine();
            Console.WriteLine("\t{0}", methodRequest.DataAsJson);
            Console.WriteLine("\nReturning response for method {0}", methodRequest.Name);

            string result = "'Input was written to log.'";
            return Task.FromResult(new MethodResponse(Encoding.UTF8.GetBytes(result), 200));
        }

1. <span data-ttu-id="e8886-128">Voeg de volgende code naar de **Main** methode voor het openen van de verbinding met uw IoT-hub en de methode-listener initialiseren:</span><span class="sxs-lookup"><span data-stu-id="e8886-128">Finally, add the following code to the **Main** method to open the connection to your IoT hub and initialize the method listener:</span></span>
   
        try
        {
            Console.WriteLine("Connecting to hub");
            Client = DeviceClient.CreateFromConnectionString(DeviceConnectionString, TransportType.Mqtt);

            // setup callback for "writeLine" method
            Client.SetMethodHandlerAsync("writeLine", WriteLineToConsole, null).Wait();
            Console.WriteLine("Waiting for direct method call\n Press enter to exit.");
            Console.ReadLine();

            Console.WriteLine("Exiting...");

            // as a good practice, remove the "writeLine" handler
            Client.SetMethodHandlerAsync("writeLine", null, null).Wait();
            Client.CloseAsync().Wait();
        }
        catch (Exception ex)
        {
            Console.WriteLine();
            Console.WriteLine("Error in sample: {0}", ex.Message);
        }
        
1. <span data-ttu-id="e8886-129">In de Visual Studio Solution Explorer met de rechtermuisknop op uw oplossing en klik vervolgens op **Opstartprojecten instellen...** .</span><span class="sxs-lookup"><span data-stu-id="e8886-129">In the Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**.</span></span> <span data-ttu-id="e8886-130">Selecteer **één opstartproject**, en selecteer vervolgens de **SimulateDeviceMethods** -project in de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="e8886-130">Select **Single startup project**, and then select the **SimulateDeviceMethods** project in the dropdown menu.</span></span>        

> [!NOTE]
> <span data-ttu-id="e8886-131">Om de zaken niet nodeloos ingewikkeld te maken, is in deze handleiding geen beleid voor opnieuw proberen geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="e8886-131">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="e8886-132">In productiecode moet u beleid voor opnieuw proberen (zoals verbinding opnieuw), zoals voorgesteld in het MSDN-artikel implementeren [afhandeling van tijdelijke fout][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="e8886-132">In production code, you should implement retry policies (such as connection retry), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="e8886-133">Een directe methode is aangeroepen voor een apparaat</span><span class="sxs-lookup"><span data-stu-id="e8886-133">Call a direct method on a device</span></span>
<span data-ttu-id="e8886-134">In deze sectie maakt u een .NET consoletoepassing maken die een methode wordt aangeroepen in de gesimuleerde apparaattoepassing en wordt vervolgens het antwoord.</span><span class="sxs-lookup"><span data-stu-id="e8886-134">In this section, you create a .NET console app that calls a method in the simulated device app and then displays the response.</span></span>

1. <span data-ttu-id="e8886-135">Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toe aan de huidige oplossing met behulp van de projectsjabloon **Console Application**.</span><span class="sxs-lookup"><span data-stu-id="e8886-135">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="e8886-136">Zorg ervoor dat de versie van .NET Framework minimaal 4.5.1 is.</span><span class="sxs-lookup"><span data-stu-id="e8886-136">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="e8886-137">Noem het project **CallMethodOnDevice**.</span><span class="sxs-lookup"><span data-stu-id="e8886-137">Name the project **CallMethodOnDevice**.</span></span>
   
    ![Nieuw Windows Classic Desktop-project in Visual C#][img-createserviceapp]
2. <span data-ttu-id="e8886-139">Klik in Solution Explorer met de rechtermuisknop op de **CallMethodOnDevice** project en klik vervolgens op **NuGet-pakketten beheren...** .</span><span class="sxs-lookup"><span data-stu-id="e8886-139">In Solution Explorer, right-click the **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="e8886-140">Klik in de **NuGet Package Manager** op **Browse** en zoek naar **microsoft.azure.devices**. Accepteer de gebruiksvoorwaarden en klik op **Install** om het **Microsoft.Azure.Devices**-pakket te installeren.</span><span class="sxs-lookup"><span data-stu-id="e8886-140">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="e8886-141">Met deze procedure worden de [Azure IoT-service-SDK][lnk-nuget-service-sdk], het NuGet-pakket en de bijbehorende afhankelijkheden gedownload en geïnstalleerd. Ook worden verwijzingen hiernaar toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="e8886-141">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Sluit het venster Nuget Package Manager.][img-servicenuget]

4. <span data-ttu-id="e8886-143">Voeg aan het begin van het bestand **Program.cs** de volgende `using` instructies toe:</span><span class="sxs-lookup"><span data-stu-id="e8886-143">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="e8886-144">Voeg de volgende velden toe aan de klasse **Program**:</span><span class="sxs-lookup"><span data-stu-id="e8886-144">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="e8886-145">Vervang de tijdelijke aanduidingswaarde met de IoT Hub-verbindingsreeks voor de hub die u hebt gemaakt in de vorige sectie.</span><span class="sxs-lookup"><span data-stu-id="e8886-145">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="e8886-146">Voeg de volgende methode toe aan de klasse **Program**:</span><span class="sxs-lookup"><span data-stu-id="e8886-146">Add the following method to the **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line to be written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="e8886-147">Deze methode wordt aangeroepen voor een directe methode met de naam `writeLine` op de `myDeviceId` apparaat.</span><span class="sxs-lookup"><span data-stu-id="e8886-147">This method invokes a direct method with name `writeLine` on the `myDeviceId` device.</span></span> <span data-ttu-id="e8886-148">Vervolgens worden de respons van het apparaat in de console geschreven.</span><span class="sxs-lookup"><span data-stu-id="e8886-148">Then, it writes the response provided by the device on the console.</span></span> <span data-ttu-id="e8886-149">Houd er rekening mee hoe het is mogelijk om op te geven van een time-outwaarde voor het apparaat om te reageren.</span><span class="sxs-lookup"><span data-stu-id="e8886-149">Note how it is possible to specify a timeout value for the device to respond.</span></span>
7. <span data-ttu-id="e8886-150">Voeg tot slot de volgende regels toe aan de methode **Main**:</span><span class="sxs-lookup"><span data-stu-id="e8886-150">Finally, add the following lines to the **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

1. <span data-ttu-id="e8886-151">In de Visual Studio Solution Explorer met de rechtermuisknop op uw oplossing en klik vervolgens op **Opstartprojecten instellen...** .</span><span class="sxs-lookup"><span data-stu-id="e8886-151">In the Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**.</span></span> <span data-ttu-id="e8886-152">Selecteer **één opstartproject**, en selecteer vervolgens de **CallMethodOnDevice** -project in de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="e8886-152">Select **Single startup project**, and then select the **CallMethodOnDevice** project in the dropdown menu.</span></span>

## <a name="run-the-applications"></a><span data-ttu-id="e8886-153">De toepassingen uitvoeren</span><span class="sxs-lookup"><span data-stu-id="e8886-153">Run the applications</span></span>
<span data-ttu-id="e8886-154">U kunt nu de toepassingen gaan uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e8886-154">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="e8886-155">Voer de app voor .NET-apparaat **SimulateDeviceMethods**.</span><span class="sxs-lookup"><span data-stu-id="e8886-155">Run the .NET device app **SimulateDeviceMethods**.</span></span> <span data-ttu-id="e8886-156">Deze zou moeten starten luisteren naar methodeaanroepen van uw IoT-Hub:</span><span class="sxs-lookup"><span data-stu-id="e8886-156">It should start listening for method calls from your IoT Hub:</span></span> 

    ![Apparaat-app uitvoeren][img-deviceapprun]
1. <span data-ttu-id="e8886-158">Nu dat het apparaat is verbonden en wachten op methode-aanroepen uitgevoerd .NET **CallMethodOnDevice** app de methode in de gesimuleerde apparaattoepassing aan te roepen.</span><span class="sxs-lookup"><span data-stu-id="e8886-158">Now that the device is connected and waiting for method invocations, run the .NET **CallMethodOnDevice** app to invoke the method in the simulated device app.</span></span> <span data-ttu-id="e8886-159">U ziet de reactie van het apparaat in de console geschreven.</span><span class="sxs-lookup"><span data-stu-id="e8886-159">You should see the device response written in the console.</span></span>
   
    ![Service-app uitvoeren][img-serviceapprun]
1. <span data-ttu-id="e8886-161">Het apparaat reageert vervolgens aan de methode door dit bericht afdrukken:</span><span class="sxs-lookup"><span data-stu-id="e8886-161">The device then reacts to the method by printing this message:</span></span>
   
    ![Directe methode wordt aangeroepen op het apparaat][img-directmethodinvoked]

## <a name="next-steps"></a><span data-ttu-id="e8886-163">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e8886-163">Next steps</span></span>
<span data-ttu-id="e8886-164">In deze handleiding hebt u een nieuwe IoT-hub geconfigureerd in Azure Portal en vervolgens een apparaat-id gemaakt in het id-register van de IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="e8886-164">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="e8886-165">U hebt deze apparaat-id gebruikt om in te schakelen van de gesimuleerde apparaattoepassing om te reageren op de methoden die worden aangeroepen door de cloud.</span><span class="sxs-lookup"><span data-stu-id="e8886-165">You used this device identity to enable the simulated device app to react to methods invoked by the cloud.</span></span> <span data-ttu-id="e8886-166">Hebt u ook een app roept methoden op het apparaat en de reactie van het apparaat wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e8886-166">You also created an app that invokes methods on the device and displays the response from the device.</span></span> 

<span data-ttu-id="e8886-167">Als u aan de slag wilt gaan met IoT Hub en andere IoT-scenario's wilt verkennen, leest u deze artikelen:</span><span class="sxs-lookup"><span data-stu-id="e8886-167">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="e8886-168">[Aan de slag met IoT Hub]</span><span class="sxs-lookup"><span data-stu-id="e8886-168">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="e8886-169">[Taken plannen op meerdere apparaten][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="e8886-169">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="e8886-170">Zie voor meer informatie over het uitbreiden van uw IoT-oplossing en schema-methode op meerdere apparaten aanroepen, de [planning en broadcast taken] [ lnk-tutorial-jobs] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="e8886-170">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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

<span data-ttu-id="e8886-171">[Aan de slag met IoT Hub]: iot-hub-node-node-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="e8886-171">[Get started with IoT Hub]: iot-hub-node-node-getstarted.md</span></span>
