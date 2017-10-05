---
title: Gebruik Azure IoT Hub direct methoden (.NET/knooppunt) | Microsoft Docs
description: Het gebruik van Azure IoT Hub rechtstreekse methoden. U kunt het apparaat met Azure IoT SDK voor Node.js gebruiken voor het implementeren van een gesimuleerde apparaattoepassing met een directe methode en de service Azure IoT SDK voor .NET voor het implementeren van een service-app die de directe methode aanroept.
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: ab035b8e-bff8-4e12-9536-f31d6b6fe425
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/10/2017
ms.author: nberdy
ms.openlocfilehash: ad705789a153381e21b2ccb05d4e0c17f78671fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-direct-methods-netnode"></a><span data-ttu-id="ff9e8-104">Directe methoden (.NET/knooppunt) gebruiken</span><span class="sxs-lookup"><span data-stu-id="ff9e8-104">Use direct methods (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="ff9e8-105">In deze zelfstudie gaan we een .NET- en Node.js-consoletoepassing ontwikkelen:</span><span class="sxs-lookup"><span data-stu-id="ff9e8-105">In this tutorial, we are going to develop a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="ff9e8-106">**CallMethodOnDevice.sln**, een .NET back-end-app, die een methode wordt aangeroepen in de gesimuleerde apparaattoepassing en het antwoord wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ff9e8-106">**CallMethodOnDevice.sln**, a .NET back-end app, which calls a method in the simulated device app and displays the response.</span></span>
* <span data-ttu-id="ff9e8-107">**SimulatedDevice.js**, een Node.js-app, die overeenkomt met een apparaat verbinding te maken met uw iothub met de identiteit van het apparaat eerder hebt gemaakt en reageert op de methode aangeroepen door de cloud.</span><span class="sxs-lookup"><span data-stu-id="ff9e8-107">**SimulatedDevice.js**, a Node.js app, which simulates a device connecting to your IoT hub with the device identity created earlier, and responds to the method called by the cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="ff9e8-108">Het artikel [Azure IoT-SDK's][lnk-hub-sdks] bevat informatie over de verschillende Azure IoT-SDK's die u kunt gebruiken om beide toepassingen zo te maken dat ze zowel op het apparaat als op de back-end van uw oplossing kunnen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ff9e8-108">The article [Azure IoT SDKs][lnk-hub-sdks] provides information about the Azure IoT SDKs that you can use to build both applications to run on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="ff9e8-109">Voor deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="ff9e8-109">To complete this tutorial, you need:</span></span>

* <span data-ttu-id="ff9e8-110">Visual Studio 2015 of Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="ff9e8-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="ff9e8-111">Node.js versie 0.10.x of hoger.</span><span class="sxs-lookup"><span data-stu-id="ff9e8-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="ff9e8-112">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="ff9e8-112">An active Azure account.</span></span> <span data-ttu-id="ff9e8-113">(Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)</span><span class="sxs-lookup"><span data-stu-id="ff9e8-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="ff9e8-114">Een gesimuleerde apparaattoepassing maken</span><span class="sxs-lookup"><span data-stu-id="ff9e8-114">Create a simulated device app</span></span>
<span data-ttu-id="ff9e8-115">In deze sectie maakt u een Node.js-consoletoepassing dat met een methode aangeroepen door de oplossing voor back-end overeenkomt.</span><span class="sxs-lookup"><span data-stu-id="ff9e8-115">In this section, you create a Node.js console app that responds to a method called by the solution back end.</span></span>

1. <span data-ttu-id="ff9e8-116">Maak een nieuwe lege map met de naam **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="ff9e8-116">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="ff9e8-117">In de map **simulateddevice** maakt u een package.json-bestand door in het opdrachtprompt de volgende opdracht op te geven.</span><span class="sxs-lookup"><span data-stu-id="ff9e8-117">In the **simulateddevice** folder, create a package.json file using the following command at your command prompt.</span></span> <span data-ttu-id="ff9e8-118">Accepteer alle standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="ff9e8-118">Accept all the defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="ff9e8-119">Bij de opdrachtprompt in de **simulateddevice** map, voer de volgende opdracht voor het installeren van de **azure-iot-device** en **azure-iot-device-mqtt** pakketten:</span><span class="sxs-lookup"><span data-stu-id="ff9e8-119">At your command prompt in the **simulateddevice** folder, run the following command to install the **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>
   
    ```
        npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="ff9e8-120">Start een teksteditor en maak een bestand in de **simulateddevice** map en noem deze **SimulatedDevice.js**.</span><span class="sxs-lookup"><span data-stu-id="ff9e8-120">Using a text editor, create a file in the **simulateddevice** folder and name it **SimulatedDevice.js**.</span></span>
4. <span data-ttu-id="ff9e8-121">Voeg de volgende `require` instructies toe aan het begin van het bestand **SimulatedDevice.js**:</span><span class="sxs-lookup"><span data-stu-id="ff9e8-121">Add the following `require` statements at the start of the **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="ff9e8-122">Voeg een **connectionString** variabele en deze gebruiken voor het maken een **DeviceClient** exemplaar.</span><span class="sxs-lookup"><span data-stu-id="ff9e8-122">Add a **connectionString** variable and use it to create a **DeviceClient** instance.</span></span> <span data-ttu-id="ff9e8-123">Vervang **{verbindingsreeks apparaat}** tekenreeks met de apparaatverbinding u hebt gegenereerd tijdens de *maken van een apparaat-id* sectie:</span><span class="sxs-lookup"><span data-stu-id="ff9e8-123">Replace **{device connection string}** with the device connection string you generated in the *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="ff9e8-124">Voeg de volgende functie voor het implementeren van de directe methode op het apparaat toe:</span><span class="sxs-lookup"><span data-stu-id="ff9e8-124">Add the following function to implement the direct method on the device:</span></span>
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written to log.', function(err) {
            if(err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response to method \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. <span data-ttu-id="ff9e8-125">Maak verbinding met uw IoT-hub en de methode-listener initialiseren:</span><span class="sxs-lookup"><span data-stu-id="ff9e8-125">Open the connection to your IoT hub and initialize the method listener:</span></span>
   
    ```
    client.open(function(err) {
        if (err) {
            console.error('could not open IotHub client');
        }  else {
            console.log('client opened');
            client.onDeviceMethod('writeLine', onWriteLine);
        }
    });
    ```
8. <span data-ttu-id="ff9e8-126">Sla het bestand **SimulatedDevice.js** op en sluit het.</span><span class="sxs-lookup"><span data-stu-id="ff9e8-126">Save and close the **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="ff9e8-127">Om de zaken niet nodeloos ingewikkeld te maken, is in deze handleiding geen beleid voor opnieuw proberen geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="ff9e8-127">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="ff9e8-128">In productiecode moet u beleid voor opnieuw proberen (zoals verbinding opnieuw), zoals voorgesteld in het MSDN-artikel implementeren [afhandeling van tijdelijke fout][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="ff9e8-128">In production code, you should implement retry policies (such as connection retry), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="ff9e8-129">Een directe methode is aangeroepen voor een apparaat</span><span class="sxs-lookup"><span data-stu-id="ff9e8-129">Call a direct method on a device</span></span>
<span data-ttu-id="ff9e8-130">In deze sectie maakt u een .NET consoletoepassing maken die een methode wordt aangeroepen in de gesimuleerde apparaattoepassing en wordt vervolgens het antwoord.</span><span class="sxs-lookup"><span data-stu-id="ff9e8-130">In this section, you create a .NET console app that calls a method in the simulated device app and then displays the response.</span></span>

1. <span data-ttu-id="ff9e8-131">Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toe aan de huidige oplossing met behulp van de projectsjabloon **Console Application**.</span><span class="sxs-lookup"><span data-stu-id="ff9e8-131">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution by using the **Console Application** project template.</span></span> <span data-ttu-id="ff9e8-132">Zorg ervoor dat de versie van .NET Framework minimaal 4.5.1 is.</span><span class="sxs-lookup"><span data-stu-id="ff9e8-132">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="ff9e8-133">Noem het project **CallMethodOnDevice**.</span><span class="sxs-lookup"><span data-stu-id="ff9e8-133">Name the project **CallMethodOnDevice**.</span></span>
   
    ![Nieuw Windows Classic Desktop-project in Visual C#][10]
2. <span data-ttu-id="ff9e8-135">Klik in Solution Explorer met de rechtermuisknop op de **CallMethodOnDevice** project en klik vervolgens op **NuGet-pakketten beheren...** .</span><span class="sxs-lookup"><span data-stu-id="ff9e8-135">In Solution Explorer, right-click the **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="ff9e8-136">Klik in de **NuGet Package Manager** op **Browse** en zoek naar **microsoft.azure.devices**. Accepteer de gebruiksvoorwaarden en klik op **Install** om het **Microsoft.Azure.Devices**-pakket te installeren.</span><span class="sxs-lookup"><span data-stu-id="ff9e8-136">In the **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** to install the **Microsoft.Azure.Devices** package, and accept the terms of use.</span></span> <span data-ttu-id="ff9e8-137">Met deze procedure worden de [Azure IoT-service-SDK][lnk-nuget-service-sdk], het NuGet-pakket en de bijbehorende afhankelijkheden gedownload en geïnstalleerd. Ook worden verwijzingen hiernaar toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="ff9e8-137">This procedure downloads, installs, and adds a reference to the [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Sluit het venster Nuget Package Manager.][11]

4. <span data-ttu-id="ff9e8-139">Voeg aan het begin van het bestand **Program.cs** de volgende `using` instructies toe:</span><span class="sxs-lookup"><span data-stu-id="ff9e8-139">Add the following `using` statements at the top of the **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="ff9e8-140">Voeg de volgende velden toe aan de klasse **Program**:</span><span class="sxs-lookup"><span data-stu-id="ff9e8-140">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="ff9e8-141">Vervang de tijdelijke aanduidingswaarde met de IoT Hub-verbindingsreeks voor de hub die u hebt gemaakt in de vorige sectie.</span><span class="sxs-lookup"><span data-stu-id="ff9e8-141">Replace the placeholder value with the IoT Hub connection string for the hub that you created in the previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="ff9e8-142">Voeg de volgende methode toe aan de klasse **Program**:</span><span class="sxs-lookup"><span data-stu-id="ff9e8-142">Add the following method to the **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line to be written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="ff9e8-143">Deze methode wordt aangeroepen voor een directe methode met de naam `writeLine` op de `myDeviceId` apparaat.</span><span class="sxs-lookup"><span data-stu-id="ff9e8-143">This method invokes a direct method with name `writeLine` on the `myDeviceId` device.</span></span> <span data-ttu-id="ff9e8-144">Vervolgens worden de respons van het apparaat in de console geschreven.</span><span class="sxs-lookup"><span data-stu-id="ff9e8-144">Then, it writes the response provided by the device on the console.</span></span> <span data-ttu-id="ff9e8-145">Houd er rekening mee hoe het is mogelijk om op te geven van een time-outwaarde voor het apparaat om te reageren.</span><span class="sxs-lookup"><span data-stu-id="ff9e8-145">Note how it is possible to specify a timeout value for the device to respond.</span></span>
7. <span data-ttu-id="ff9e8-146">Voeg tot slot de volgende regels toe aan de methode **Main**:</span><span class="sxs-lookup"><span data-stu-id="ff9e8-146">Finally, add the following lines to the **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter to exit.");
        Console.ReadLine();

## <a name="run-the-applications"></a><span data-ttu-id="ff9e8-147">De toepassingen uitvoeren</span><span class="sxs-lookup"><span data-stu-id="ff9e8-147">Run the applications</span></span>
<span data-ttu-id="ff9e8-148">U kunt nu de toepassingen gaan uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ff9e8-148">You are now ready to run the applications.</span></span>

1. <span data-ttu-id="ff9e8-149">In de Visual Studio Solution Explorer met de rechtermuisknop op uw oplossing en klik vervolgens op **Opstartprojecten instellen...** .</span><span class="sxs-lookup"><span data-stu-id="ff9e8-149">In the Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**.</span></span> <span data-ttu-id="ff9e8-150">Selecteer **één opstartproject**, en selecteer vervolgens de **CallMethodOnDevice** -project in de vervolgkeuzelijst.</span><span class="sxs-lookup"><span data-stu-id="ff9e8-150">Select **Single startup project**, and then select the **CallMethodOnDevice** project in the dropdown menu.</span></span>

2. <span data-ttu-id="ff9e8-151">Bij een opdrachtprompt in de **simulateddevice** map, voer de volgende opdracht om te beginnen met luisteren voor methodeaanroepen vanuit uw IoT-Hub:</span><span class="sxs-lookup"><span data-stu-id="ff9e8-151">At a command prompt in the **simulateddevice** folder, run the following command to start listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   <span data-ttu-id="ff9e8-152">Wachten op het gesimuleerde apparaat te openen:![][7]</span><span class="sxs-lookup"><span data-stu-id="ff9e8-152">Wait for the simulated device to open:  ![][7]</span></span>
3. <span data-ttu-id="ff9e8-153">Nu dat het apparaat is verbonden en wachten op methode-aanroepen uitgevoerd .NET **CallMethodOnDevice** app de methode in de gesimuleerde apparaattoepassing aan te roepen.</span><span class="sxs-lookup"><span data-stu-id="ff9e8-153">Now that the device is connected and waiting for method invocations, run the .NET **CallMethodOnDevice** app to invoke the method in the simulated device app.</span></span> <span data-ttu-id="ff9e8-154">U ziet de reactie van het apparaat in de console geschreven.</span><span class="sxs-lookup"><span data-stu-id="ff9e8-154">You should see the device response written in the console.</span></span>
   
    ![][8]
4. <span data-ttu-id="ff9e8-155">Het apparaat reageert vervolgens aan de methode door dit bericht afdrukken:</span><span class="sxs-lookup"><span data-stu-id="ff9e8-155">The device then reacts to the method by printing this message:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="ff9e8-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ff9e8-156">Next steps</span></span>
<span data-ttu-id="ff9e8-157">In deze handleiding hebt u een nieuwe IoT-hub geconfigureerd in Azure Portal en vervolgens een apparaat-id gemaakt in het id-register van de IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="ff9e8-157">In this tutorial, you configured a new IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="ff9e8-158">U hebt deze apparaat-id gebruikt om in te schakelen van de gesimuleerde apparaattoepassing om te reageren op de methoden die worden aangeroepen door de cloud.</span><span class="sxs-lookup"><span data-stu-id="ff9e8-158">You used this device identity to enable the simulated device app to react to methods invoked by the cloud.</span></span> <span data-ttu-id="ff9e8-159">Hebt u ook een app roept methoden op het apparaat en de reactie van het apparaat wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ff9e8-159">You also created an app that invokes methods on the device and displays the response from the device.</span></span> 

<span data-ttu-id="ff9e8-160">Als u aan de slag wilt gaan met IoT Hub en andere IoT-scenario's wilt verkennen, leest u deze artikelen:</span><span class="sxs-lookup"><span data-stu-id="ff9e8-160">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="ff9e8-161">[Aan de slag met IoT Hub]</span><span class="sxs-lookup"><span data-stu-id="ff9e8-161">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="ff9e8-162">[Taken plannen op meerdere apparaten][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="ff9e8-162">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="ff9e8-163">Zie voor meer informatie over het uitbreiden van uw IoT-oplossing en schema-methode op meerdere apparaten aanroepen, de [planning en broadcast taken] [ lnk-tutorial-jobs] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="ff9e8-163">To learn how to extend your IoT solution and schedule method calls on multiple devices, see the [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

<!-- Images. -->
[7]: ./media/iot-hub-csharp-node-direct-methods/run-simulated-device.png
[8]: ./media/iot-hub-csharp-node-direct-methods/netserviceapp.png
[9]: ./media/iot-hub-csharp-node-direct-methods/methods-output.png

[10]: ./media/iot-hub-csharp-node-direct-methods/direct-methods-csharp1.png
[11]: ./media/iot-hub-csharp-node-direct-methods/direct-methods-csharp2.png

<!-- Links -->
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx

[lnk-dev-setup]: https://github.com/Azure/azure-iot-sdk-node/blob/master/doc/node-devbox-setup.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/
[lnk-nuget-service-sdk]: https://www.nuget.org/packages/Microsoft.Azure.Devices/

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-tutorial-jobs]: iot-hub-node-node-schedule-jobs.md
[lnk-devguide-methods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[Send Cloud-to-Device messages with IoT Hub]: iot-hub-csharp-csharp-c2d.md
[Process Device-to-Cloud messages]: iot-hub-csharp-csharp-process-d2c.md
<span data-ttu-id="ff9e8-164">[Aan de slag met IoT Hub]: iot-hub-node-node-getstarted.md</span><span class="sxs-lookup"><span data-stu-id="ff9e8-164">[Get started with IoT Hub]: iot-hub-node-node-getstarted.md</span></span>
