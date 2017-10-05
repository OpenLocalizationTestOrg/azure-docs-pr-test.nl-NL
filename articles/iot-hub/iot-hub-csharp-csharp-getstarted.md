---
title: Aan de slag met Azure IoT Hub (.NET) | Microsoft Docs
description: Informatie over het verzenden van apparaat-naar-cloud-berichten naar Azure IoT Hub met behulp van IoT SDK's voor .NET. U maakt gesimuleerde apparaat- en service-apps om uw apparaat te registreren, berichten te verzenden en berichten uit IoT Hub te lezen.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: f40604ff-8fd6-4969-9e99-8574fbcf036c
ms.service: iot-hub
ms.devlang: dotnet
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 69296eb9ac2a74a97b632d27733a6a06500b4abd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="connect-your-device-to-your-iot-hub-using-net"></a><span data-ttu-id="547c3-104">Uw apparaat verbinding laten maken met uw IoT Hub met .NET</span><span class="sxs-lookup"><span data-stu-id="547c3-104">Connect your device to your IoT hub using .NET</span></span>

[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="547c3-105">Aan het eind van deze zelfstudie beschikt u over drie .NET-consoletoepassingen:</span><span class="sxs-lookup"><span data-stu-id="547c3-105">At the end of this tutorial, you have three .NET console apps:</span></span>

* <span data-ttu-id="547c3-106">**CreateDeviceIdentity**: deze toepassing maakt een apparaat-id en de bijbehorende beveiligingssleutel waarmee uw apparaat-app kan worden verbonden.</span><span class="sxs-lookup"><span data-stu-id="547c3-106">**CreateDeviceIdentity**, which creates a device identity and associated security key to connect your device app.</span></span>
* <span data-ttu-id="547c3-107">**ReadDeviceToCloudMessages**: deze toepassing geeft de telemetrie weer die is verzonden door uw apparaat-app.</span><span class="sxs-lookup"><span data-stu-id="547c3-107">**ReadDeviceToCloudMessages**, which displays the telemetry sent by your device app.</span></span>
* <span data-ttu-id="547c3-108">**SimulatedDevice**: deze toepassing koppelt uw IoT-hub aan de apparaat-id die u eerder hebt gemaakt en verzendt iedere seconde een telemetriebericht via het MQTT-protocol.</span><span class="sxs-lookup"><span data-stu-id="547c3-108">**SimulatedDevice**, which connects to your IoT hub with the device identity created earlier, and sends a telemetry message every second by using the MQTT protocol.</span></span>

<span data-ttu-id="547c3-109">U kunt de Visual Studio-oplossing downloaden of klonen om zo de beschikking te krijgen over de drie apps van Github.</span><span class="sxs-lookup"><span data-stu-id="547c3-109">You can download or clone the Visual Studio solution, which contains the three apps from Github.</span></span>

```bash
git clone https://github.com/Azure-Samples/iot-hub-dotnet-simulated-device-client-app.git
```

> [!NOTE]
> <span data-ttu-id="547c3-110">Raadpleeg het artikel [Azure IoT-SDKs][lnk-hub-sdks] voor meer informatie over de verschillende Azure IoT-SDK's die u kunt gebruiken om beide toepassingen zo te maken dat ze zowel op het apparaat als op de back-end van uw oplossing kunnen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="547c3-110">For information about the Azure IoT SDKs that you can use to build both applications to run on devices, and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="547c3-111">Voor het voltooien van deze zelfstudie hebt u het volgende nodig:</span><span class="sxs-lookup"><span data-stu-id="547c3-111">To complete this tutorial, you need the following:</span></span>

* <span data-ttu-id="547c3-112">Visual Studio 2015 of Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="547c3-112">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="547c3-113">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="547c3-113">An active Azure account.</span></span> <span data-ttu-id="547c3-114">(Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)</span><span class="sxs-lookup"><span data-stu-id="547c3-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="547c3-115">U hebt nu uw IoT Hub gemaakt en u hebt de hostnaam en de IoT Hub-verbindingsreeks die u nodig hebt voor de rest van deze handleiding.</span><span class="sxs-lookup"><span data-stu-id="547c3-115">You have now created your IoT hub, and you have the host name and IoT Hub connection string that you need to complete the rest of this tutorial.</span></span>

<a id="DeviceIdentity_csharp"></a>
[!INCLUDE [iot-hub-get-started-create-device-identity-csharp](../../includes/iot-hub-get-started-create-device-identity-csharp.md)]

<a id="D2C_csharp"></a>
## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="547c3-116">Apparaat-naar-cloud-berichten ontvangen</span><span class="sxs-lookup"><span data-stu-id="547c3-116">Receive device-to-cloud messages</span></span>
<span data-ttu-id="547c3-117">In dit gedeelte maakt u een .NET-consoletoepassing die apparaat-naar-cloud-berichten uit IoT Hub kan lezen.</span><span class="sxs-lookup"><span data-stu-id="547c3-117">In this section, you create a .NET console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="547c3-118">Een IoT-hub toont een [Azure Event Hubs][lnk-event-hubs-overview]-compatibel eindpunt waarmee u apparaat-naar-cloud-berichten kunt lezen.</span><span class="sxs-lookup"><span data-stu-id="547c3-118">An IoT hub exposes an [Azure Event Hubs][lnk-event-hubs-overview]-compatible endpoint to enable you to read device-to-cloud messages.</span></span> <span data-ttu-id="547c3-119">Om de zaken niet nodeloos ingewikkeld te maken, maakt u met deze handleiding een basislezer die niet geschikt is voor hoge doorvoersnelheden.</span><span class="sxs-lookup"><span data-stu-id="547c3-119">To keep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="547c3-120">In de zelfstudie [Apparaat-naar-cloud-berichten verwerken][lnk-process-d2c-tutorial] leert u hoe u op grote schaal apparaat-naar-cloud-berichten kunt verwerken.</span><span class="sxs-lookup"><span data-stu-id="547c3-120">To learn how to process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span> <span data-ttu-id="547c3-121">Zie voor meer informatie over het verwerken van Event Hubs-berichten de zelfstudie [Aan de slag met Event Hubs][lnk-eventhubs-tutorial].</span><span class="sxs-lookup"><span data-stu-id="547c3-121">For more information about how to process messages from Event Hubs, see the [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span> <span data-ttu-id="547c3-122">(Deze zelfstudie is van toepassing op eindpunten die compatibel zijn met event hubs in IoT Hub.)</span><span class="sxs-lookup"><span data-stu-id="547c3-122">(This tutorial is applicable to the IoT Hub Event Hub-compatible endpoints.)</span></span>

> [!NOTE]
> <span data-ttu-id="547c3-123">Het met Event Hub compatibele eindpunt voor het lezen van apparaat-naar-cloud-berichten maakt altijd gebruik van het AMQP-protocol.</span><span class="sxs-lookup"><span data-stu-id="547c3-123">The Event Hub-compatible endpoint for reading device-to-cloud messages always uses the AMQP protocol.</span></span>

1. <span data-ttu-id="547c3-124">Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toe aan de huidige oplossing met behulp van de projectsjabloon **Console App (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="547c3-124">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution, by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="547c3-125">Zorg ervoor dat de versie van .NET Framework minimaal 4.5.1 is.</span><span class="sxs-lookup"><span data-stu-id="547c3-125">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="547c3-126">Noem het project **ReadDeviceToCloudMessages**.</span><span class="sxs-lookup"><span data-stu-id="547c3-126">Name the project **ReadDeviceToCloudMessages**.</span></span>

    ![Nieuw Windows Classic Desktop-project in Visual C#][10a]

2. <span data-ttu-id="547c3-128">Klik in Solution Explorer met de rechtermuisknop op het project **ReadDeviceToCloudMessages** en klik vervolgens op **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="547c3-128">In Solution Explorer, right-click the **ReadDeviceToCloudMessages** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="547c3-129">In het venster **NuGet Package Manager** zoekt u **WindowsAzure.ServiceBus**. Accepteer de gebruikersvoorwaarden en klik op **Install**.</span><span class="sxs-lookup"><span data-stu-id="547c3-129">In the **NuGet Package Manager** window, search for **WindowsAzure.ServiceBus**, select **Install**, and accept the terms of use.</span></span> <span data-ttu-id="547c3-130">Met deze procedure worden [Azure Service Bus][lnk-servicebus-nuget] en de bijbehorende afhankelijkheden gedownload en geïnstalleerd. Ook worden verwijzingen hiernaar toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="547c3-130">This procedure downloads, installs, and adds a reference to [Azure Service Bus][lnk-servicebus-nuget], with all its dependencies.</span></span> <span data-ttu-id="547c3-131">Met dit pakket kan de toepassing verbinding maken met het eindpunt dat compatibel is met event hubs op uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="547c3-131">This package enables the application to connect to the Event Hub-compatible endpoint on your IoT hub.</span></span>

4. <span data-ttu-id="547c3-132">Voeg aan het begin van het bestand **Program.cs** de volgende `using` instructies toe:</span><span class="sxs-lookup"><span data-stu-id="547c3-132">Add the following `using` statements at the top of the **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.ServiceBus.Messaging;
    using System.Threading;
    ```

5. <span data-ttu-id="547c3-133">Voeg de volgende velden toe aan de klasse **Program**:</span><span class="sxs-lookup"><span data-stu-id="547c3-133">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="547c3-134">Vervang de tijdelijke-aanduidingswaarde met de IoT Hub-verbindingsreeks voor de hub die u hebt gemaakt in de sectie Een IoT-hub maken.</span><span class="sxs-lookup"><span data-stu-id="547c3-134">Replace the placeholder value with the IoT Hub connection string for the hub you created in the "Create an IoT hub" section.</span></span>

    ```csharp
    static string connectionString = "{iothub connection string}";
    static string iotHubD2cEndpoint = "messages/events";
    static EventHubClient eventHubClient;
    ```

6. <span data-ttu-id="547c3-135">Voeg de volgende methode toe aan de klasse **Program**:</span><span class="sxs-lookup"><span data-stu-id="547c3-135">Add the following method to the **Program** class:</span></span>

    ```csharp
    private static async Task ReceiveMessagesFromDeviceAsync(string partition, CancellationToken ct)
    {
        var eventHubReceiver = eventHubClient.GetDefaultConsumerGroup().CreateReceiver(partition, DateTime.UtcNow);
        while (true)
        {
            if (ct.IsCancellationRequested) break;
            EventData eventData = await eventHubReceiver.ReceiveAsync();
            if (eventData == null) continue;

            string data = Encoding.UTF8.GetString(eventData.GetBytes());
            Console.WriteLine("Message received. Partition: {0} Data: '{1}'", partition, data);
        }
    }
    ```

    <span data-ttu-id="547c3-136">Deze methode gebruikt een exemplaar van **EventHubReceiver** om berichten te ontvangen van alle apparaat-naar-cloud ontvangstpartities van de IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="547c3-136">This method uses an **EventHubReceiver** instance to receive messages from all the IoT hub device-to-cloud receive partitions.</span></span> <span data-ttu-id="547c3-137">U geeft nu een `DateTime.Now` parameter door bij het maken van het object **EventHubReceiver**, zodat alleen berichten worden ontvangen die zijn verzonden nadat het object is gestart.</span><span class="sxs-lookup"><span data-stu-id="547c3-137">Notice how you pass a `DateTime.Now` parameter when you create the **EventHubReceiver** object, so that it only receives messages sent after it starts.</span></span> <span data-ttu-id="547c3-138">Dit filter is handig in een testomgeving, omdat u zo de huidige reeks berichten kunt zien.</span><span class="sxs-lookup"><span data-stu-id="547c3-138">This filter is useful in a test environment so you can see the current set of messages.</span></span> <span data-ttu-id="547c3-139">In een productieomgeving moet de code ervoor zorgen dat alle berichten worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="547c3-139">In a production environment, your code should make sure that it processes all the messages.</span></span> <span data-ttu-id="547c3-140">Zie voor meer informatie de zelfstudie [IoT Hub-apparaat-naar-cloud-berichten verwerken][lnk-process-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="547c3-140">For more information, see the tutorial [How to process IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial].</span></span>

7. <span data-ttu-id="547c3-141">Voeg tot slot de volgende regels toe aan de methode **Main**:</span><span class="sxs-lookup"><span data-stu-id="547c3-141">Finally, add the following lines to the **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Receive messages. Ctrl-C to exit.\n");
    eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, iotHubD2cEndpoint);

    var d2cPartitions = eventHubClient.GetRuntimeInformation().PartitionIds;

    CancellationTokenSource cts = new CancellationTokenSource();

    System.Console.CancelKeyPress += (s, e) =>
    {
        e.Cancel = true;
        cts.Cancel();
        Console.WriteLine("Exiting...");
    };

    var tasks = new List<Task>();
    foreach (string partition in d2cPartitions)
    {
        tasks.Add(ReceiveMessagesFromDeviceAsync(partition, cts.Token));
    }  
    Task.WaitAll(tasks.ToArray());
    ```

## <a name="create-a-device-app"></a><span data-ttu-id="547c3-142">Een apparaat-app maken</span><span class="sxs-lookup"><span data-stu-id="547c3-142">Create a device app</span></span>

<span data-ttu-id="547c3-143">In deze sectie maakt u een .NET-consoletoepassing die een apparaat simuleert dat apparaat-naar-cloud-berichten naar een IoT Hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="547c3-143">In this section, you create a .NET console app that simulates a device that sends device-to-cloud messages to an IoT hub.</span></span>

1. <span data-ttu-id="547c3-144">Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toe aan de huidige oplossing met behulp van de projectsjabloon **Console App (.NET Framework)**.</span><span class="sxs-lookup"><span data-stu-id="547c3-144">In Visual Studio, add a Visual C# Windows Classic Desktop project to the current solution, by using the **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="547c3-145">Zorg ervoor dat de versie van .NET Framework minimaal 4.5.1 is.</span><span class="sxs-lookup"><span data-stu-id="547c3-145">Make sure the .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="547c3-146">Noem het project **SimulatedDevice**.</span><span class="sxs-lookup"><span data-stu-id="547c3-146">Name the project **SimulatedDevice**.</span></span>

    ![Nieuw Windows Classic Desktop-project in Visual C#][10b]

2. <span data-ttu-id="547c3-148">Klik in Solution Explorer met de rechtermuisknop op het project **SimulatedDevice** en klik vervolgens op **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="547c3-148">In Solution Explorer, right-click the **SimulatedDevice** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="547c3-149">Klik in de **NuGet Package Manager** op **Browse** en zoek naar **Microsoft.Azure.Devices.Client**. Accepteer de gebruiksvoorwaarden en klik op **Install** om het **Microsoft.Azure.Devices.Client**-pakket te installeren.</span><span class="sxs-lookup"><span data-stu-id="547c3-149">In the **NuGet Package Manager** window, select **Browse**, search for **Microsoft.Azure.Devices.Client**, select **Install** to install the **Microsoft.Azure.Devices.Client** package, and accept the terms of use.</span></span> <span data-ttu-id="547c3-150">Met deze procedure worden het [Azure IoT Device SDK NuGet-pakket][lnk-device-nuget] en de bijbehorende afhankelijkheden gedownload en geïnstalleerd. Ook worden verwijzingen hiernaar toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="547c3-150">This procedure downloads, installs, and adds a reference to the [Azure IoT device SDK NuGet package][lnk-device-nuget] and its dependencies.</span></span>

4. <span data-ttu-id="547c3-151">Voeg aan het begin van het bestand **Program.cs** de volgende `using`-instructie toe:</span><span class="sxs-lookup"><span data-stu-id="547c3-151">Add the following `using` statement at the top of the **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices.Client;
    using Newtonsoft.Json;
    ```

5. <span data-ttu-id="547c3-152">Voeg de volgende velden toe aan de klasse **Program**:</span><span class="sxs-lookup"><span data-stu-id="547c3-152">Add the following fields to the **Program** class.</span></span> <span data-ttu-id="547c3-153">Vervang `{iot hub hostname}` met de hostnaam van de IoT-hub die u in de sectie 'Een IoT-hub maken' hebt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="547c3-153">Substitute `{iot hub hostname}` with the IoT hub host name you retrieved in the "Create an IoT hub" section.</span></span> <span data-ttu-id="547c3-154">Vervang `{device key}` door de apparaatsleutel die u in de sectie 'Een apparaatidentiteit maken' hebt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="547c3-154">Substitute `{device key}` with the device key you retrieved in the "Create a device identity" section.</span></span>

    ```csharp
    static DeviceClient deviceClient;
    static string iotHubUri = "{iot hub hostname}";
    static string deviceKey = "{device key}";
    ```

6. <span data-ttu-id="547c3-155">Voeg de volgende methode toe aan de klasse **Program**:</span><span class="sxs-lookup"><span data-stu-id="547c3-155">Add the following method to the **Program** class:</span></span>

    ```csharp
    private static async void SendDeviceToCloudMessagesAsync()
    {
        double minTemperature = 20;
        double minHumidity = 60;
        int messageId = 1;
        Random rand = new Random();

        while (true)
        {
            double currentTemperature = minTemperature + rand.NextDouble() * 15;
            double currentHumidity = minHumidity + rand.NextDouble() * 20;

            var telemetryDataPoint = new
            {
                messageId = messageId++,
                deviceId = "myFirstDevice",
                temperature = currentTemperature,
                humidity = currentHumidity
            };
            var messageString = JsonConvert.SerializeObject(telemetryDataPoint);
            var message = new Message(Encoding.ASCII.GetBytes(messageString));
            message.Properties.Add("temperatureAlert", (currentTemperature > 30) ? "true" : "false");

            await deviceClient.SendEventAsync(message);
            Console.WriteLine("{0} > Sending message: {1}", DateTime.Now, messageString);

            await Task.Delay(1000);
        }
    }
    ```

    <span data-ttu-id="547c3-156">Met deze methode wordt elke seconde een nieuw apparaat-naar-cloud bericht verzonden.</span><span class="sxs-lookup"><span data-stu-id="547c3-156">This method sends a new device-to-cloud message every second.</span></span> <span data-ttu-id="547c3-157">Het bericht bevat een JSON-geserialiseerd object met de apparaat-id en willekeurig gegenereerde nummers om een temperatuursensor te simuleren, en een vochtigheidssensor.</span><span class="sxs-lookup"><span data-stu-id="547c3-157">The message contains a JSON-serialized object, with the device ID and randomly generated numbers to simulate a temperature sensor, and a humidity sensor.</span></span>

7. <span data-ttu-id="547c3-158">Voeg tot slot de volgende regels toe aan de methode **Main**:</span><span class="sxs-lookup"><span data-stu-id="547c3-158">Finally, add the following lines to the **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Simulated device\n");
    deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey ("myFirstDevice", deviceKey), TransportType.Mqtt);

    SendDeviceToCloudMessagesAsync();
    Console.ReadLine();
    ```

    <span data-ttu-id="547c3-159">Met de **Create**-methode in een .NET Framework-app maakt u standaard een **DeviceClient**-exemplaar dat het AMQP-protocol gebruikt om te communiceren met IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="547c3-159">By default, the **Create** method in a .NET Framework app creates a **DeviceClient** instance that uses the AMQP protocol to communicate with IoT Hub.</span></span> <span data-ttu-id="547c3-160">Als u het MQTT- of HTTP-protocol wilt gebruiken, moet u de **Create**-methode overschrijven. Zo kunt u zelf het protocol bepalen.</span><span class="sxs-lookup"><span data-stu-id="547c3-160">To use the MQTT or HTTP protocol, use the override of the **Create** method that enables you to specify the protocol.</span></span> <span data-ttu-id="547c3-161">UWP- en PCL-clients gebruiken standaard het HTTP-protocol.</span><span class="sxs-lookup"><span data-stu-id="547c3-161">UWP and PCL clients use the HTTP protocol by default.</span></span> <span data-ttu-id="547c3-162">Als u het HTTP-protocol gebruikt, dient u ook het NuGet-pakket **Microsoft.AspNet.WebApi.Client** toe te voegen om uw project op te nemen in de naamruimte **System.Net.Http.Formatting**.</span><span class="sxs-lookup"><span data-stu-id="547c3-162">If you use the HTTP protocol, you should also add the **Microsoft.AspNet.WebApi.Client** NuGet package to your project to include the **System.Net.Http.Formatting** namespace.</span></span>

<span data-ttu-id="547c3-163">In deze handleiding doorloopt u de stappen voor het maken van een IoT Hub-apparaat-app.</span><span class="sxs-lookup"><span data-stu-id="547c3-163">This tutorial takes you through the steps to create an IoT Hub device app.</span></span> <span data-ttu-id="547c3-164">U kunt ook de Visual Studio-extensie [Connected Service for Azure IoT Hub][lnk-connected-service] gebruiken om de benodigde code toe te voegen aan de apparaat-app.</span><span class="sxs-lookup"><span data-stu-id="547c3-164">You can also use the [Connected Service for Azure IoT Hub][lnk-connected-service] Visual Studio extension to add the necessary code to your device app.</span></span>

> [!NOTE]
> <span data-ttu-id="547c3-165">Om de zaken niet nodeloos ingewikkeld te maken, is in deze handleiding geen beleid voor opnieuw proberen geïmplementeerd.</span><span class="sxs-lookup"><span data-stu-id="547c3-165">To keep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="547c3-166">Bij de productiecode moet u een beleid voor opnieuw proberen implementeren (zoals exponentieel uitstel), zoals aangegeven in het MSDN-artikel [Transient Fault Handling][lnk-transient-faults] (Afhandeling van tijdelijke fouten).</span><span class="sxs-lookup"><span data-stu-id="547c3-166">In production code, you should implement retry policies (such as an exponential backoff), as suggested in the MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-the-apps"></a><span data-ttu-id="547c3-167">De apps uitvoeren</span><span class="sxs-lookup"><span data-stu-id="547c3-167">Run the apps</span></span>

<span data-ttu-id="547c3-168">U kunt nu de apps uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="547c3-168">You are now ready to run the apps.</span></span>

1. <span data-ttu-id="547c3-169">Klik in Solution Explorer, in Visual Studio, met de rechtermuisknop op uw oplossing en klik vervolgens op **Set StartUp projects**.</span><span class="sxs-lookup"><span data-stu-id="547c3-169">In Visual Studio, in Solution Explorer, right-click your solution, and then click **Set StartUp projects**.</span></span> <span data-ttu-id="547c3-170">Klik op **Multiple startup projects** en klik vervolgens op **Start** als de actie voor beide projecten **ProcessDeviceToCloudMessages** en **SimulatedDevice**.</span><span class="sxs-lookup"><span data-stu-id="547c3-170">Select **Multiple startup projects**, and then select **Start** as the action for both the **ReadDeviceToCloudMessages** and **SimulatedDevice** projects.</span></span>

    ![Eigenschappen van opstartprojecten][41]

2. <span data-ttu-id="547c3-172">Druk op **F5** om beide apps uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="547c3-172">Press **F5** to start both apps running.</span></span> <span data-ttu-id="547c3-173">De console-uitvoer van de **SimulatedDevice**-app toont de berichten die uw apparaat-app verzendt naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="547c3-173">The console output from the **SimulatedDevice** app shows the messages your device app sends to your IoT hub.</span></span> <span data-ttu-id="547c3-174">De console-uitvoer van de **ReadDeviceToCloudMessages**-app toont de berichten die uw IoT-hub ontvangt.</span><span class="sxs-lookup"><span data-stu-id="547c3-174">The console output from the **ReadDeviceToCloudMessages** app shows the messages that your IoT hub receives.</span></span>

    ![Console-uitvoer van apps][42]

3. <span data-ttu-id="547c3-176">De tegel **Gebruik** in [Azure Portal][lnk-portal] toont het aantal berichten dat is verzonden naar de IoT-hub:</span><span class="sxs-lookup"><span data-stu-id="547c3-176">The **Usage** tile in the [Azure portal][lnk-portal] shows the number of messages sent to the IoT hub:</span></span>

    ![Tegel Usage in Azure Portal][43]

## <a name="next-steps"></a><span data-ttu-id="547c3-178">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="547c3-178">Next steps</span></span>

<span data-ttu-id="547c3-179">In deze zelfstudie hebt u een IoT-hub geconfigureerd in Azure Portal en vervolgens een apparaat-id gemaakt in het id-register van de IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="547c3-179">In this tutorial, you configured an IoT hub in the Azure portal, and then created a device identity in the IoT hub's identity registry.</span></span> <span data-ttu-id="547c3-180">U hebt deze apparaat-id gebruikt om de apparaat-app in staat te stellen apparaat-naar-cloud-berichten te verzenden naar de IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="547c3-180">You used this device identity to enable the device app to send device-to-cloud messages to the IoT hub.</span></span> <span data-ttu-id="547c3-181">Ook hebt u een app gemaakt die de berichten weergeeft die worden ontvangen door de IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="547c3-181">You also created an app that displays the messages received by the IoT hub.</span></span>

<span data-ttu-id="547c3-182">Als u aan de slag wilt gaan met IoT Hub en andere IoT-scenario's wilt verkennen, leest u deze artikelen:</span><span class="sxs-lookup"><span data-stu-id="547c3-182">To continue getting started with IoT Hub and to explore other IoT scenarios, see:</span></span>

* <span data-ttu-id="547c3-183">[Verbinding maken met uw apparaat][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="547c3-183">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="547c3-184">[Aan de slag met apparaatbeheer][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="547c3-184">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="547c3-185">[Aan de slag met IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="547c3-185">[Getting started with IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="547c3-186">Raadpleeg de zelfstudie [Apparaat-naar-cloud-berichten verwerken][lnk-process-d2c-tutorial] voor meer informatie over hoe u uw IoT-oplossing uitbreidt en apparaat-naar-cloud-berichten op schaal verwerkt.</span><span class="sxs-lookup"><span data-stu-id="547c3-186">To learn how to extend your IoT solution and process device-to-cloud messages at scale, see the [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

<!-- Images. -->
[41]: ./media/iot-hub-csharp-csharp-getstarted/run-apps1.png
[42]: ./media/iot-hub-csharp-csharp-getstarted/run-apps2.png
[43]: ./media/iot-hub-csharp-csharp-getstarted/usage.png
[10a]: ./media/iot-hub-csharp-csharp-getstarted/create-receive-csharp1.png
[10b]: ./media/iot-hub-csharp-csharp-getstarted/create-device-csharp1.png


<!-- Links -->
[lnk-process-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
[lnk-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-portal]: https://portal.azure.com/

[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-servicebus-nuget]: https://www.nuget.org/packages/WindowsAzure.ServiceBus
[lnk-event-hubs-overview]: ../event-hubs/event-hubs-overview.md

[lnk-device-nuget]: https://www.nuget.org/packages/Microsoft.Azure.Devices.Client/
[lnk-transient-faults]: https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx
[lnk-connected-service]: https://visualstudiogallery.msdn.microsoft.com/e254a3a5-d72e-488e-9bd3-8fee8e0cd1d6
[lnk-device-management]: iot-hub-node-node-device-management-get-started.md
[lnk-iot-edge]: iot-hub-linux-iot-edge-get-started.md
[lnk-connect-device]: https://azure.microsoft.com/develop/iot/
