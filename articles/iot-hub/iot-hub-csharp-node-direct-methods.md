---
title: Azure IoT Hub aaaUse directe methoden (.NET/knooppunt) | Microsoft Docs
description: Hoe Azure IoT Hub toouse directe methoden. U gebruikt hello Azure IoT-device SDK voor Node.js tooimplement een gesimuleerde apparaattoepassing met een directe methode en hello Azure IoT service SDK voor .NET tooimplement een service-app die Hallo directe methode aanroept.
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
ms.openlocfilehash: f566f939be840eb308b00ffa4e05c4e5b3fefb39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-direct-methods-netnode"></a><span data-ttu-id="e537a-104">Directe methoden (.NET/knooppunt) gebruiken</span><span class="sxs-lookup"><span data-stu-id="e537a-104">Use direct methods (.NET/Node)</span></span>
[!INCLUDE [iot-hub-selector-c2d-methods](../../includes/iot-hub-selector-c2d-methods.md)]

<span data-ttu-id="e537a-105">In deze zelfstudie gaan we een .NET toodevelop en een Node.js-consoletoepassing:</span><span class="sxs-lookup"><span data-stu-id="e537a-105">In this tutorial, we are going toodevelop a .NET and a Node.js console app:</span></span>

* <span data-ttu-id="e537a-106">**CallMethodOnDevice.sln**, een .NET back-end-app, die een methode wordt aangeroepen in de gesimuleerde apparaattoepassing Hallo en antwoord Hallo weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e537a-106">**CallMethodOnDevice.sln**, a .NET back-end app, which calls a method in hello simulated device app and displays hello response.</span></span>
* <span data-ttu-id="e537a-107">**SimulatedDevice.js**, een Node.js-app, die overeenkomt met een apparaat tooyour IoT-hub te koppelen aan de apparaat-id Hallo eerder hebt gemaakt en toohello methode aangeroepen door Hallo cloud reageert.</span><span class="sxs-lookup"><span data-stu-id="e537a-107">**SimulatedDevice.js**, a Node.js app, which simulates a device connecting tooyour IoT hub with hello device identity created earlier, and responds toohello method called by hello cloud.</span></span>

> [!NOTE]
> <span data-ttu-id="e537a-108">Hallo artikel [Azure IoT SDK's] [ lnk-hub-sdks] bevat informatie over hello Azure IoT SDK's waarmee u toobuild beide toorun toepassingen op apparaten en de back-end van uw oplossing kunt.</span><span class="sxs-lookup"><span data-stu-id="e537a-108">hello article [Azure IoT SDKs][lnk-hub-sdks] provides information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices and your solution back end.</span></span>
> 
> 

<span data-ttu-id="e537a-109">toocomplete deze zelfstudie hebt u nodig:</span><span class="sxs-lookup"><span data-stu-id="e537a-109">toocomplete this tutorial, you need:</span></span>

* <span data-ttu-id="e537a-110">Visual Studio 2015 of Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="e537a-110">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="e537a-111">Node.js versie 0.10.x of hoger.</span><span class="sxs-lookup"><span data-stu-id="e537a-111">Node.js version 0.10.x or later.</span></span>
* <span data-ttu-id="e537a-112">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="e537a-112">An active Azure account.</span></span> <span data-ttu-id="e537a-113">(Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)</span><span class="sxs-lookup"><span data-stu-id="e537a-113">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

[!INCLUDE [iot-hub-get-started-create-device-identity](../../includes/iot-hub-get-started-create-device-identity.md)]

## <a name="create-a-simulated-device-app"></a><span data-ttu-id="e537a-114">Een gesimuleerde apparaattoepassing maken</span><span class="sxs-lookup"><span data-stu-id="e537a-114">Create a simulated device app</span></span>
<span data-ttu-id="e537a-115">In deze sectie maakt u een Node.js-consoletoepassing die tooa methode aangeroepen door Hallo oplossing terug end reageert.</span><span class="sxs-lookup"><span data-stu-id="e537a-115">In this section, you create a Node.js console app that responds tooa method called by hello solution back end.</span></span>

1. <span data-ttu-id="e537a-116">Maak een nieuwe lege map met de naam **simulateddevice**.</span><span class="sxs-lookup"><span data-stu-id="e537a-116">Create a new empty folder called **simulateddevice**.</span></span> <span data-ttu-id="e537a-117">In Hallo **simulateddevice** map, een package.json-bestand met behulp van de volgende opdracht achter de opdrachtprompt Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="e537a-117">In hello **simulateddevice** folder, create a package.json file using hello following command at your command prompt.</span></span> <span data-ttu-id="e537a-118">Accepteer alle Hallo standaardwaarden:</span><span class="sxs-lookup"><span data-stu-id="e537a-118">Accept all hello defaults:</span></span>
   
    ```
    npm init
    ```
2. <span data-ttu-id="e537a-119">Bij de opdrachtprompt in Hallo **simulateddevice** map na de opdracht tooinstall Hallo Hallo **azure-iot-device** en **azure-iot-device-mqtt** pakketten:</span><span class="sxs-lookup"><span data-stu-id="e537a-119">At your command prompt in hello **simulateddevice** folder, run hello following command tooinstall hello **azure-iot-device** and **azure-iot-device-mqtt** packages:</span></span>
   
    ```
        npm install azure-iot-device azure-iot-device-mqtt --save
    ```
3. <span data-ttu-id="e537a-120">Een bestand met een teksteditor maken in Hallo **simulateddevice** map en noem deze **SimulatedDevice.js**.</span><span class="sxs-lookup"><span data-stu-id="e537a-120">Using a text editor, create a file in hello **simulateddevice** folder and name it **SimulatedDevice.js**.</span></span>
4. <span data-ttu-id="e537a-121">Voeg de volgende Hallo `require` instructies aan Hallo start Hallo **SimulatedDevice.js** bestand:</span><span class="sxs-lookup"><span data-stu-id="e537a-121">Add hello following `require` statements at hello start of hello **SimulatedDevice.js** file:</span></span>
   
    ```
    'use strict';
   
    var Mqtt = require('azure-iot-device-mqtt').Mqtt;
    var DeviceClient = require('azure-iot-device').Client;
    ```
5. <span data-ttu-id="e537a-122">Voeg een **connectionString** variabele en gebruik deze toocreate een **DeviceClient** exemplaar.</span><span class="sxs-lookup"><span data-stu-id="e537a-122">Add a **connectionString** variable and use it toocreate a **DeviceClient** instance.</span></span> <span data-ttu-id="e537a-123">Vervang **{verbindingsreeks apparaat}** met Hallo verbindingsreeks voor apparaat u hebt gegenereerd in Hallo *maken van een apparaat-id* sectie:</span><span class="sxs-lookup"><span data-stu-id="e537a-123">Replace **{device connection string}** with hello device connection string you generated in hello *Create a device identity* section:</span></span>
   
    ```
    var connectionString = '{device connection string}';
    var client = DeviceClient.fromConnectionString(connectionString, Mqtt);
    ```
6. <span data-ttu-id="e537a-124">Hallo functie tooimplement Hallo directe methode volgen op Hallo apparaat toevoegen:</span><span class="sxs-lookup"><span data-stu-id="e537a-124">Add hello following function tooimplement hello direct method on hello device:</span></span>
   
    ```
    function onWriteLine(request, response) {
        console.log(request.payload);
   
        response.send(200, 'Input was written toolog.', function(err) {
            if(err) {
                console.error('An error occurred when sending a method response:\n' + err.toString());
            } else {
                console.log('Response toomethod \'' + request.methodName + '\' sent successfully.' );
            }
        });
    }
    ```
7. <span data-ttu-id="e537a-125">Open Hallo verbinding tooyour IoT-hub en Hallo methode listener initialiseren:</span><span class="sxs-lookup"><span data-stu-id="e537a-125">Open hello connection tooyour IoT hub and initialize hello method listener:</span></span>
   
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
8. <span data-ttu-id="e537a-126">Opslaan en sluiten Hallo **SimulatedDevice.js** bestand.</span><span class="sxs-lookup"><span data-stu-id="e537a-126">Save and close hello **SimulatedDevice.js** file.</span></span>

> [!NOTE]
> <span data-ttu-id="e537a-127">tookeep dingen eenvoudige, deze zelfstudie wordt niet geïmplementeerd voor een beleid voor opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="e537a-127">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="e537a-128">In productiecode moet u beleid voor opnieuw proberen (zoals verbinding opnieuw), zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="e537a-128">In production code, you should implement retry policies (such as connection retry), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>
> 
> 

## <a name="call-a-direct-method-on-a-device"></a><span data-ttu-id="e537a-129">Een directe methode is aangeroepen voor een apparaat</span><span class="sxs-lookup"><span data-stu-id="e537a-129">Call a direct method on a device</span></span>
<span data-ttu-id="e537a-130">In deze sectie maakt maken u een .NET-consoletoepassing die een methode wordt aangeroepen in de gesimuleerde apparaattoepassing Hallo en wordt vervolgens weergegeven antwoord Hallo.</span><span class="sxs-lookup"><span data-stu-id="e537a-130">In this section, you create a .NET console app that calls a method in hello simulated device app and then displays hello response.</span></span>

1. <span data-ttu-id="e537a-131">Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toohello huidige oplossing met behulp van Hallo **consoletoepassing** projectsjabloon.</span><span class="sxs-lookup"><span data-stu-id="e537a-131">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution by using hello **Console Application** project template.</span></span> <span data-ttu-id="e537a-132">Zorg ervoor dat .NET Framework-versie Hallo 4.5.1 of later.</span><span class="sxs-lookup"><span data-stu-id="e537a-132">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="e537a-133">Naam Hallo project **CallMethodOnDevice**.</span><span class="sxs-lookup"><span data-stu-id="e537a-133">Name hello project **CallMethodOnDevice**.</span></span>
   
    ![Nieuw Windows Classic Desktop-project in Visual C#][10]
2. <span data-ttu-id="e537a-135">Klik in Solution Explorer met de rechtermuisknop op Hallo **CallMethodOnDevice** project en klik vervolgens op **NuGet-pakketten beheren...** .</span><span class="sxs-lookup"><span data-stu-id="e537a-135">In Solution Explorer, right-click hello **CallMethodOnDevice** project, and then click **Manage NuGet Packages...**.</span></span>
3. <span data-ttu-id="e537a-136">In Hallo **NuGet Package Manager** Selecteer **Bladeren**, zoeken naar **microsoft.azure.devices**, selecteer **installeren** tooinstall Hallo **Microsoft.Azure.Devices** Inpakken en accepteer de gebruiksvoorwaarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="e537a-136">In hello **NuGet Package Manager** window, select **Browse**, search for **microsoft.azure.devices**, select **Install** tooinstall hello **Microsoft.Azure.Devices** package, and accept hello terms of use.</span></span> <span data-ttu-id="e537a-137">Deze procedure downloadt, installeert en voegt u een verwijzing toohello [Azure IoT service SDK] [ lnk-nuget-service-sdk] NuGet-pakket en de bijbehorende afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="e537a-137">This procedure downloads, installs, and adds a reference toohello [Azure IoT service SDK][lnk-nuget-service-sdk] NuGet package and its dependencies.</span></span>
   
    ![Sluit het venster Nuget Package Manager.][11]

4. <span data-ttu-id="e537a-139">Voeg de volgende Hallo `using` instructies boven Hallo Hallo **Program.cs** bestand:</span><span class="sxs-lookup"><span data-stu-id="e537a-139">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>
   
        using System.Threading.Tasks;
        using Microsoft.Azure.Devices;
5. <span data-ttu-id="e537a-140">Hallo na toohello velden toevoegen **programma** klasse.</span><span class="sxs-lookup"><span data-stu-id="e537a-140">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="e537a-141">Vervang Hallo tijdelijke aanduidingswaarde met IoT Hub-verbindingsreeks voor Hallo-hub die u hebt gemaakt in de vorige sectie Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="e537a-141">Replace hello placeholder value with hello IoT Hub connection string for hello hub that you created in hello previous section.</span></span>
   
        static ServiceClient serviceClient;
        static string connectionString = "{iot hub connection string}";
6. <span data-ttu-id="e537a-142">Hallo na methode toohello toevoegen **programma** klasse:</span><span class="sxs-lookup"><span data-stu-id="e537a-142">Add hello following method toohello **Program** class:</span></span>
   
        private static async Task InvokeMethod()
        {
            var methodInvocation = new CloudToDeviceMethod("writeLine") { ResponseTimeout = TimeSpan.FromSeconds(30) };
            methodInvocation.SetPayloadJson("'a line toobe written'");

            var response = await serviceClient.InvokeDeviceMethodAsync("myDeviceId", methodInvocation);

            Console.WriteLine("Response status: {0}, payload:", response.Status);
            Console.WriteLine(response.GetPayloadAsJson());
        }
   
    <span data-ttu-id="e537a-143">Deze methode wordt aangeroepen voor een directe methode met de naam `writeLine` op Hallo `myDeviceId` apparaat.</span><span class="sxs-lookup"><span data-stu-id="e537a-143">This method invokes a direct method with name `writeLine` on hello `myDeviceId` device.</span></span> <span data-ttu-id="e537a-144">Vervolgens worden Hallo respons van Hallo-apparaat op Hallo console geschreven.</span><span class="sxs-lookup"><span data-stu-id="e537a-144">Then, it writes hello response provided by hello device on hello console.</span></span> <span data-ttu-id="e537a-145">Houd er rekening mee hoe het is mogelijk toospecify een time-outwaarde voor Hallo apparaat toorespond.</span><span class="sxs-lookup"><span data-stu-id="e537a-145">Note how it is possible toospecify a timeout value for hello device toorespond.</span></span>
7. <span data-ttu-id="e537a-146">Voeg regels toohello na Hallo **Main** methode:</span><span class="sxs-lookup"><span data-stu-id="e537a-146">Finally, add hello following lines toohello **Main** method:</span></span>
   
        serviceClient = ServiceClient.CreateFromConnectionString(connectionString);
        InvokeMethod().Wait();
        Console.WriteLine("Press Enter tooexit.");
        Console.ReadLine();

## <a name="run-hello-applications"></a><span data-ttu-id="e537a-147">Hallo-toepassingen uitvoeren</span><span class="sxs-lookup"><span data-stu-id="e537a-147">Run hello applications</span></span>
<span data-ttu-id="e537a-148">U bent nu klaar toorun Hallo toepassingen.</span><span class="sxs-lookup"><span data-stu-id="e537a-148">You are now ready toorun hello applications.</span></span>

1. <span data-ttu-id="e537a-149">In Visual Studio Solution Explorer hello, met de rechtermuisknop op uw oplossing en klik op **Opstartprojecten instellen...** . Selecteer **één opstartproject**, en selecteer vervolgens Hallo **CallMethodOnDevice** -project in het vervolgkeuzemenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="e537a-149">In hello Visual Studio Solution Explorer, right-click your solution, and then click **Set StartUp Projects...**. Select **Single startup project**, and then select hello **CallMethodOnDevice** project in hello dropdown menu.</span></span>

2. <span data-ttu-id="e537a-150">Bij een opdrachtprompt in Hallo **simulateddevice** map Hallo opdracht toostart luisteren naar methodeaanroepen van uw IoT-Hub te volgen:</span><span class="sxs-lookup"><span data-stu-id="e537a-150">At a command prompt in hello **simulateddevice** folder, run hello following command toostart listening for method calls from your IoT Hub:</span></span>
   
    ```
    node SimulatedDevice.js
    ```
   <span data-ttu-id="e537a-151">Wachten op Hallo gesimuleerd apparaat tooopen:![][7]</span><span class="sxs-lookup"><span data-stu-id="e537a-151">Wait for hello simulated device tooopen:  ![][7]</span></span>
3. <span data-ttu-id="e537a-152">Nu dat het Hallo-apparaat is verbonden en Hallo .NET wacht methode aanroepen, voer **CallMethodOnDevice** app tooinvoke Hallo methode in de gesimuleerde apparaattoepassing Hallo.</span><span class="sxs-lookup"><span data-stu-id="e537a-152">Now that hello device is connected and waiting for method invocations, run hello .NET **CallMethodOnDevice** app tooinvoke hello method in hello simulated device app.</span></span> <span data-ttu-id="e537a-153">U ziet Hallo apparaat antwoord is geschreven in Hallo-console.</span><span class="sxs-lookup"><span data-stu-id="e537a-153">You should see hello device response written in hello console.</span></span>
   
    ![][8]
4. <span data-ttu-id="e537a-154">Hallo apparaat reageert vervolgens toohello methode door dit bericht afdrukken:</span><span class="sxs-lookup"><span data-stu-id="e537a-154">hello device then reacts toohello method by printing this message:</span></span>
   
    ![][9]

## <a name="next-steps"></a><span data-ttu-id="e537a-155">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e537a-155">Next steps</span></span>
<span data-ttu-id="e537a-156">In deze zelfstudie maakt u een nieuwe iothub geconfigureerd in hello Azure-portal en vervolgens een apparaat-id in de id-register Hallo iothub hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e537a-156">In this tutorial, you configured a new IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="e537a-157">U hebt deze apparaat-id tooenable Hallo gesimuleerd apparaat app tooreact toomethods aangeroepen door Hallo cloud gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e537a-157">You used this device identity tooenable hello simulated device app tooreact toomethods invoked by hello cloud.</span></span> <span data-ttu-id="e537a-158">Hebt u ook een app die wordt aangeroepen methoden op Hallo apparaat en geeft weer Hallo-antwoord van Hallo-apparaat hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="e537a-158">You also created an app that invokes methods on hello device and displays hello response from hello device.</span></span> 

<span data-ttu-id="e537a-159">toocontinue aan de slag met IoT Hub en tooexplore raadpleegt u andere IoT-scenario's:</span><span class="sxs-lookup"><span data-stu-id="e537a-159">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="e537a-160">[Aan de slag met IoT Hub]</span><span class="sxs-lookup"><span data-stu-id="e537a-160">[Get started with IoT Hub]</span></span>
* <span data-ttu-id="e537a-161">[Taken plannen op meerdere apparaten][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="e537a-161">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="e537a-162">toolearn hoe tooextend uw IoT-oplossing en schema-methode aanroepen op meerdere apparaten, raadpleegt u Hallo [planning en broadcast taken] [ lnk-tutorial-jobs] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="e537a-162">toolearn how tooextend your IoT solution and schedule method calls on multiple devices, see hello [Schedule and broadcast jobs][lnk-tutorial-jobs] tutorial.</span></span>

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
[Aan de slag met IoT Hub]: iot-hub-node-node-getstarted.md
