---
title: aaaGet gestart met Azure IoT Hub (.NET) | Microsoft Docs
description: Meer informatie over hoe toosend apparaat-naar-cloud-berichten tooAzure IoT Hub met IoT SDK's voor .NET. Gesimuleerde apparaat en service-apps tooregister uw apparaat maken en berichten uit iothub berichten verzenden.
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
ms.openlocfilehash: 56cf14687411898ea0fa4ebb1782e18b3930809c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="connect-your-device-tooyour-iot-hub-using-net"></a><span data-ttu-id="aa72d-104">Verbinding maken met uw apparaat tooyour iothub met .NET</span><span class="sxs-lookup"><span data-stu-id="aa72d-104">Connect your device tooyour IoT hub using .NET</span></span>

[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

<span data-ttu-id="aa72d-105">Aan het einde van de Hallo van deze zelfstudie hebt u drie console .NET-toepassingen:</span><span class="sxs-lookup"><span data-stu-id="aa72d-105">At hello end of this tutorial, you have three .NET console apps:</span></span>

* <span data-ttu-id="aa72d-106">**CreateDeviceIdentity**, die een apparaat-id maakt en gekoppelde beveiliging sleutel tooconnect app op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="aa72d-106">**CreateDeviceIdentity**, which creates a device identity and associated security key tooconnect your device app.</span></span>
* <span data-ttu-id="aa72d-107">**ReadDeviceToCloudMessages**, weergeven met Hallo telemetrie verzonden door de app op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="aa72d-107">**ReadDeviceToCloudMessages**, which displays hello telemetry sent by your device app.</span></span>
* <span data-ttu-id="aa72d-108">**SimulatedDevice**, die tooyour IoT-hub aan Hallo apparaat-id eerder hebt gemaakt, en verzendt een bericht telemetrie elke seconde met behulp van Hallo MQTT protocol.</span><span class="sxs-lookup"><span data-stu-id="aa72d-108">**SimulatedDevice**, which connects tooyour IoT hub with hello device identity created earlier, and sends a telemetry message every second by using hello MQTT protocol.</span></span>

<span data-ttu-id="aa72d-109">U kunt downloaden of kloon van de Visual Studio-oplossing hello, waarin drie Hallo-apps vanuit Github.</span><span class="sxs-lookup"><span data-stu-id="aa72d-109">You can download or clone hello Visual Studio solution, which contains hello three apps from Github.</span></span>

```bash
git clone https://github.com/Azure-Samples/iot-hub-dotnet-simulated-device-client-app.git
```

> [!NOTE]
> <span data-ttu-id="aa72d-110">Zie voor informatie over hello Azure IoT SDK's waarmee u toobuild kunt toorun toepassingen op apparaten en uw back-end oplossing, [Azure IoT SDK's][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="aa72d-110">For information about hello Azure IoT SDKs that you can use toobuild both applications toorun on devices, and your solution back end, see [Azure IoT SDKs][lnk-hub-sdks].</span></span>

<span data-ttu-id="aa72d-111">toocomplete in deze zelfstudie, moet u hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="aa72d-111">toocomplete this tutorial, you need hello following:</span></span>

* <span data-ttu-id="aa72d-112">Visual Studio 2015 of Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="aa72d-112">Visual Studio 2015 or Visual Studio 2017.</span></span>
* <span data-ttu-id="aa72d-113">Een actief Azure-account.</span><span class="sxs-lookup"><span data-stu-id="aa72d-113">An active Azure account.</span></span> <span data-ttu-id="aa72d-114">(Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)</span><span class="sxs-lookup"><span data-stu-id="aa72d-114">(If you don't have an account, you can create a [free account][lnk-free-trial] in just a couple of minutes.)</span></span>

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

<span data-ttu-id="aa72d-115">U hebt nu uw IoT-hub gemaakt en u hebt Hallo-hostnaam en verbindingsreeks van IoT Hub dat u nodig hebt toocomplete Hallo rest van deze handleiding.</span><span class="sxs-lookup"><span data-stu-id="aa72d-115">You have now created your IoT hub, and you have hello host name and IoT Hub connection string that you need toocomplete hello rest of this tutorial.</span></span>

<a id="DeviceIdentity_csharp"></a>
[!INCLUDE [iot-hub-get-started-create-device-identity-csharp](../../includes/iot-hub-get-started-create-device-identity-csharp.md)]

<a id="D2C_csharp"></a>
## <a name="receive-device-to-cloud-messages"></a><span data-ttu-id="aa72d-116">Apparaat-naar-cloud-berichten ontvangen</span><span class="sxs-lookup"><span data-stu-id="aa72d-116">Receive device-to-cloud messages</span></span>
<span data-ttu-id="aa72d-117">In dit gedeelte maakt u een .NET-consoletoepassing die apparaat-naar-cloud-berichten uit IoT Hub kan lezen.</span><span class="sxs-lookup"><span data-stu-id="aa72d-117">In this section, you create a .NET console app that reads device-to-cloud messages from IoT Hub.</span></span> <span data-ttu-id="aa72d-118">Een iothub toont een [Azure Event Hubs][lnk-event-hubs-overview]-compatibel eindpunt tooenable u tooread apparaat-naar-cloud-berichten.</span><span class="sxs-lookup"><span data-stu-id="aa72d-118">An IoT hub exposes an [Azure Event Hubs][lnk-event-hubs-overview]-compatible endpoint tooenable you tooread device-to-cloud messages.</span></span> <span data-ttu-id="aa72d-119">tookeep dingen eenvoudige, deze zelfstudie maakt u een basislezer die niet geschikt voor een implementatie met hoge doorvoer.</span><span class="sxs-lookup"><span data-stu-id="aa72d-119">tookeep things simple, this tutorial creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="aa72d-120">toolearn hoe tooprocess apparaat-naar-cloud-berichten op grote schaal, Zie Hallo [apparaat-naar-cloud-berichten verwerken] [ lnk-process-d2c-tutorial] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="aa72d-120">toolearn how tooprocess device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span> <span data-ttu-id="aa72d-121">Zie voor meer informatie over hoe tooprocess van van Event Hubs berichten Hallo [aan de slag met Event Hubs] [ lnk-eventhubs-tutorial] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="aa72d-121">For more information about how tooprocess messages from Event Hubs, see hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span> <span data-ttu-id="aa72d-122">(Deze zelfstudie is van toepassing toohello IoT Hub Event Hub-compatibele eindpunten.)</span><span class="sxs-lookup"><span data-stu-id="aa72d-122">(This tutorial is applicable toohello IoT Hub Event Hub-compatible endpoints.)</span></span>

> [!NOTE]
> <span data-ttu-id="aa72d-123">Hallo Event Hub-compatibele eindpunt voor het lezen van apparaat-naar-cloudberichten altijd gebruikt Hallo AMQP-protocol.</span><span class="sxs-lookup"><span data-stu-id="aa72d-123">hello Event Hub-compatible endpoint for reading device-to-cloud messages always uses hello AMQP protocol.</span></span>

1. <span data-ttu-id="aa72d-124">Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toohello huidige oplossing met behulp van Hallo **Console-App (.NET Framework)** projectsjabloon.</span><span class="sxs-lookup"><span data-stu-id="aa72d-124">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution, by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="aa72d-125">Zorg ervoor dat .NET Framework-versie Hallo 4.5.1 of later.</span><span class="sxs-lookup"><span data-stu-id="aa72d-125">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="aa72d-126">Naam Hallo project **ReadDeviceToCloudMessages**.</span><span class="sxs-lookup"><span data-stu-id="aa72d-126">Name hello project **ReadDeviceToCloudMessages**.</span></span>

    ![Nieuw Windows Classic Desktop-project in Visual C#][10a]

2. <span data-ttu-id="aa72d-128">Klik in Solution Explorer met de rechtermuisknop op Hallo **ReadDeviceToCloudMessages** project en klik vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="aa72d-128">In Solution Explorer, right-click hello **ReadDeviceToCloudMessages** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="aa72d-129">In Hallo **NuGet Package Manager** venster, zoekt u **WindowsAzure.ServiceBus**, selecteer **installeren**, en accepteer de gebruiksvoorwaarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="aa72d-129">In hello **NuGet Package Manager** window, search for **WindowsAzure.ServiceBus**, select **Install**, and accept hello terms of use.</span></span> <span data-ttu-id="aa72d-130">Deze procedure downloadt, installeert en voegt u een verwijzing te[Azure Service Bus][lnk-servicebus-nuget], inclusief alle afhankelijkheden ervan.</span><span class="sxs-lookup"><span data-stu-id="aa72d-130">This procedure downloads, installs, and adds a reference too[Azure Service Bus][lnk-servicebus-nuget], with all its dependencies.</span></span> <span data-ttu-id="aa72d-131">Met dit pakket kan Hallo toepassing tooconnect toohello Event Hub-compatibele eindpunt op uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="aa72d-131">This package enables hello application tooconnect toohello Event Hub-compatible endpoint on your IoT hub.</span></span>

4. <span data-ttu-id="aa72d-132">Voeg de volgende Hallo `using` instructies boven Hallo Hallo **Program.cs** bestand:</span><span class="sxs-lookup"><span data-stu-id="aa72d-132">Add hello following `using` statements at hello top of hello **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.ServiceBus.Messaging;
    using System.Threading;
    ```

5. <span data-ttu-id="aa72d-133">Hallo na toohello velden toevoegen **programma** klasse.</span><span class="sxs-lookup"><span data-stu-id="aa72d-133">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="aa72d-134">Vervang Hallo tijdelijke aanduidingswaarde met IoT Hub-verbindingsreeks voor Hallo-hub die u hebt gemaakt in de sectie 'Een IoT-hub maken' Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="aa72d-134">Replace hello placeholder value with hello IoT Hub connection string for hello hub you created in hello "Create an IoT hub" section.</span></span>

    ```csharp
    static string connectionString = "{iothub connection string}";
    static string iotHubD2cEndpoint = "messages/events";
    static EventHubClient eventHubClient;
    ```

6. <span data-ttu-id="aa72d-135">Hallo na methode toohello toevoegen **programma** klasse:</span><span class="sxs-lookup"><span data-stu-id="aa72d-135">Add hello following method toohello **Program** class:</span></span>

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

    <span data-ttu-id="aa72d-136">Deze methode gebruikt een **EventHubReceiver** exemplaar tooreceive berichten van alle Hallo IoT hub apparaat-naar-cloud ontvangstpartities.</span><span class="sxs-lookup"><span data-stu-id="aa72d-136">This method uses an **EventHubReceiver** instance tooreceive messages from all hello IoT hub device-to-cloud receive partitions.</span></span> <span data-ttu-id="aa72d-137">U geeft een `DateTime.Now` parameter bij het maken van Hallo **EventHubReceiver** object, zodat alleen verzonden nadat deze is gestart berichten worden ontvangen.</span><span class="sxs-lookup"><span data-stu-id="aa72d-137">Notice how you pass a `DateTime.Now` parameter when you create hello **EventHubReceiver** object, so that it only receives messages sent after it starts.</span></span> <span data-ttu-id="aa72d-138">Dit filter is handig in een testomgeving zodat u Hallo huidige reeks berichten kunt zien.</span><span class="sxs-lookup"><span data-stu-id="aa72d-138">This filter is useful in a test environment so you can see hello current set of messages.</span></span> <span data-ttu-id="aa72d-139">In een productieomgeving moet uw code ervoor zorgen dat alle Hallo-berichten worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="aa72d-139">In a production environment, your code should make sure that it processes all hello messages.</span></span> <span data-ttu-id="aa72d-140">Zie voor meer informatie, Hallo zelfstudie [hoe tooprocess IoT Hub apparaat-naar-cloud-berichten][lnk-process-d2c-tutorial].</span><span class="sxs-lookup"><span data-stu-id="aa72d-140">For more information, see hello tutorial [How tooprocess IoT Hub device-to-cloud messages][lnk-process-d2c-tutorial].</span></span>

7. <span data-ttu-id="aa72d-141">Voeg regels toohello na Hallo **Main** methode:</span><span class="sxs-lookup"><span data-stu-id="aa72d-141">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Receive messages. Ctrl-C tooexit.\n");
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

## <a name="create-a-device-app"></a><span data-ttu-id="aa72d-142">Een apparaat-app maken</span><span class="sxs-lookup"><span data-stu-id="aa72d-142">Create a device app</span></span>

<span data-ttu-id="aa72d-143">In deze sectie maakt u een .NET consoletoepassing maken die een apparaat simuleert dat apparaat-naar-cloudberichten tooan iothub verzendt.</span><span class="sxs-lookup"><span data-stu-id="aa72d-143">In this section, you create a .NET console app that simulates a device that sends device-to-cloud messages tooan IoT hub.</span></span>

1. <span data-ttu-id="aa72d-144">Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toohello huidige oplossing met behulp van Hallo **Console-App (.NET Framework)** projectsjabloon.</span><span class="sxs-lookup"><span data-stu-id="aa72d-144">In Visual Studio, add a Visual C# Windows Classic Desktop project toohello current solution, by using hello **Console App (.NET Framework)** project template.</span></span> <span data-ttu-id="aa72d-145">Zorg ervoor dat .NET Framework-versie Hallo 4.5.1 of later.</span><span class="sxs-lookup"><span data-stu-id="aa72d-145">Make sure hello .NET Framework version is 4.5.1 or later.</span></span> <span data-ttu-id="aa72d-146">Naam Hallo project **SimulatedDevice**.</span><span class="sxs-lookup"><span data-stu-id="aa72d-146">Name hello project **SimulatedDevice**.</span></span>

    ![Nieuw Windows Classic Desktop-project in Visual C#][10b]

2. <span data-ttu-id="aa72d-148">Klik in Solution Explorer met de rechtermuisknop op Hallo **SimulatedDevice** project en klik vervolgens op **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="aa72d-148">In Solution Explorer, right-click hello **SimulatedDevice** project, and then click **Manage NuGet Packages**.</span></span>

3. <span data-ttu-id="aa72d-149">In Hallo **NuGet Package Manager** Selecteer **Bladeren**, zoeken naar **Microsoft.Azure.Devices.Client**, selecteer **installeren** Hallo tooinstall **Microsoft.Azure.Devices.Client** Inpakken en accepteer de gebruiksvoorwaarden Hallo.</span><span class="sxs-lookup"><span data-stu-id="aa72d-149">In hello **NuGet Package Manager** window, select **Browse**, search for **Microsoft.Azure.Devices.Client**, select **Install** tooinstall hello **Microsoft.Azure.Devices.Client** package, and accept hello terms of use.</span></span> <span data-ttu-id="aa72d-150">Deze procedure downloadt, installeert en voegt u een verwijzing toohello [Azure IoT-device SDK NuGet-pakket] [ lnk-device-nuget] en de bijbehorende afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="aa72d-150">This procedure downloads, installs, and adds a reference toohello [Azure IoT device SDK NuGet package][lnk-device-nuget] and its dependencies.</span></span>

4. <span data-ttu-id="aa72d-151">Voeg de volgende Hallo `using` instructie bovenaan Hallo Hallo **Program.cs** bestand:</span><span class="sxs-lookup"><span data-stu-id="aa72d-151">Add hello following `using` statement at hello top of hello **Program.cs** file:</span></span>

    ```csharp
    using Microsoft.Azure.Devices.Client;
    using Newtonsoft.Json;
    ```

5. <span data-ttu-id="aa72d-152">Hallo na toohello velden toevoegen **programma** klasse.</span><span class="sxs-lookup"><span data-stu-id="aa72d-152">Add hello following fields toohello **Program** class.</span></span> <span data-ttu-id="aa72d-153">Vervang `{iot hub hostname}` met Hallo IoT hub-hostnaam u in het gedeelte voor Hallo 'Een IoT-hub maken' hebt opgehaald.</span><span class="sxs-lookup"><span data-stu-id="aa72d-153">Substitute `{iot hub hostname}` with hello IoT hub host name you retrieved in hello "Create an IoT hub" section.</span></span> <span data-ttu-id="aa72d-154">Vervang `{device key}` met Hallo apparaatsleutel die u hebt opgehaald in het gedeelte voor Hallo 'Een apparaat-id maken'.</span><span class="sxs-lookup"><span data-stu-id="aa72d-154">Substitute `{device key}` with hello device key you retrieved in hello "Create a device identity" section.</span></span>

    ```csharp
    static DeviceClient deviceClient;
    static string iotHubUri = "{iot hub hostname}";
    static string deviceKey = "{device key}";
    ```

6. <span data-ttu-id="aa72d-155">Hallo na methode toohello toevoegen **programma** klasse:</span><span class="sxs-lookup"><span data-stu-id="aa72d-155">Add hello following method toohello **Program** class:</span></span>

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

    <span data-ttu-id="aa72d-156">Met deze methode wordt elke seconde een nieuw apparaat-naar-cloud bericht verzonden.</span><span class="sxs-lookup"><span data-stu-id="aa72d-156">This method sends a new device-to-cloud message every second.</span></span> <span data-ttu-id="aa72d-157">Hallo-bericht bevat een JSON-geserialiseerd object, met Hallo apparaat-ID en willekeurige cijfers toosimulate een temperatuursensor en een sensor vochtigheid.</span><span class="sxs-lookup"><span data-stu-id="aa72d-157">hello message contains a JSON-serialized object, with hello device ID and randomly generated numbers toosimulate a temperature sensor, and a humidity sensor.</span></span>

7. <span data-ttu-id="aa72d-158">Voeg regels toohello na Hallo **Main** methode:</span><span class="sxs-lookup"><span data-stu-id="aa72d-158">Finally, add hello following lines toohello **Main** method:</span></span>

    ```csharp
    Console.WriteLine("Simulated device\n");
    deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey ("myFirstDevice", deviceKey), TransportType.Mqtt);

    SendDeviceToCloudMessagesAsync();
    Console.ReadLine();
    ```

    <span data-ttu-id="aa72d-159">Standaard Hallo **maken** methode in een .NET Framework-app maakt een **DeviceClient** -exemplaar dat gebruikmaakt van Hallo AMQP-protocol toocommunicate met IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="aa72d-159">By default, hello **Create** method in a .NET Framework app creates a **DeviceClient** instance that uses hello AMQP protocol toocommunicate with IoT Hub.</span></span> <span data-ttu-id="aa72d-160">toouse hello MQTT of HTTP-protocol gebruiken Hallo onderdrukking Hallo **maken** methode waarmee u toospecify Hallo-protocol.</span><span class="sxs-lookup"><span data-stu-id="aa72d-160">toouse hello MQTT or HTTP protocol, use hello override of hello **Create** method that enables you toospecify hello protocol.</span></span> <span data-ttu-id="aa72d-161">UWP en PCL clients Hallo HTTP-protocol standaard gebruikt.</span><span class="sxs-lookup"><span data-stu-id="aa72d-161">UWP and PCL clients use hello HTTP protocol by default.</span></span> <span data-ttu-id="aa72d-162">Als u Hallo HTTP-protocol gebruikt, moet u ook Hallo toevoegen **Microsoft.AspNet.WebApi.Client** NuGet-pakket tooyour project tooinclude hello **System.Net.Http.Formatting** naamruimte.</span><span class="sxs-lookup"><span data-stu-id="aa72d-162">If you use hello HTTP protocol, you should also add hello **Microsoft.AspNet.WebApi.Client** NuGet package tooyour project tooinclude hello **System.Net.Http.Formatting** namespace.</span></span>

<span data-ttu-id="aa72d-163">Deze zelfstudie leert u Hallo stappen toocreate een IoT Hub apparaat-app.</span><span class="sxs-lookup"><span data-stu-id="aa72d-163">This tutorial takes you through hello steps toocreate an IoT Hub device app.</span></span> <span data-ttu-id="aa72d-164">U kunt ook Hallo [Connected Service for Azure IoT Hub] [ lnk-connected-service] Visual Studio-extensie tooadd Hallo benodigde code tooyour app voor het apparaat.</span><span class="sxs-lookup"><span data-stu-id="aa72d-164">You can also use hello [Connected Service for Azure IoT Hub][lnk-connected-service] Visual Studio extension tooadd hello necessary code tooyour device app.</span></span>

> [!NOTE]
> <span data-ttu-id="aa72d-165">tookeep dingen eenvoudige, deze zelfstudie wordt niet geïmplementeerd voor een beleid voor opnieuw proberen.</span><span class="sxs-lookup"><span data-stu-id="aa72d-165">tookeep things simple, this tutorial does not implement any retry policy.</span></span> <span data-ttu-id="aa72d-166">In productiecode moet u beleid voor opnieuw proberen (zoals exponentieel uitstel), zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout][lnk-transient-faults].</span><span class="sxs-lookup"><span data-stu-id="aa72d-166">In production code, you should implement retry policies (such as an exponential backoff), as suggested in hello MSDN article [Transient Fault Handling][lnk-transient-faults].</span></span>

## <a name="run-hello-apps"></a><span data-ttu-id="aa72d-167">Hallo-apps uitvoeren</span><span class="sxs-lookup"><span data-stu-id="aa72d-167">Run hello apps</span></span>

<span data-ttu-id="aa72d-168">U bent nu klaar toorun Hallo apps.</span><span class="sxs-lookup"><span data-stu-id="aa72d-168">You are now ready toorun hello apps.</span></span>

1. <span data-ttu-id="aa72d-169">Klik in Solution Explorer, in Visual Studio, met de rechtermuisknop op uw oplossing en klik vervolgens op **Set StartUp projects**.</span><span class="sxs-lookup"><span data-stu-id="aa72d-169">In Visual Studio, in Solution Explorer, right-click your solution, and then click **Set StartUp projects**.</span></span> <span data-ttu-id="aa72d-170">Selecteer **meerdere opstartprojecten**, en selecteer vervolgens **Start** als actie voor beide Hallo Hallo **ReadDeviceToCloudMessages** en **SimulatedDevice** projecten.</span><span class="sxs-lookup"><span data-stu-id="aa72d-170">Select **Multiple startup projects**, and then select **Start** as hello action for both hello **ReadDeviceToCloudMessages** and **SimulatedDevice** projects.</span></span>

    ![Eigenschappen van opstartprojecten][41]

2. <span data-ttu-id="aa72d-172">Druk op **F5** toostart beide apps die worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="aa72d-172">Press **F5** toostart both apps running.</span></span> <span data-ttu-id="aa72d-173">console-uitvoer van Hallo Hallo **SimulatedDevice** app Hallo berichten app op uw apparaat tooyour iothub verzendt.</span><span class="sxs-lookup"><span data-stu-id="aa72d-173">hello console output from hello **SimulatedDevice** app shows hello messages your device app sends tooyour IoT hub.</span></span> <span data-ttu-id="aa72d-174">console-uitvoer van Hallo Hallo **ReadDeviceToCloudMessages** app toont Hallo-berichten die uw IoT-hub ontvangt.</span><span class="sxs-lookup"><span data-stu-id="aa72d-174">hello console output from hello **ReadDeviceToCloudMessages** app shows hello messages that your IoT hub receives.</span></span>

    ![Console-uitvoer van apps][42]

3. <span data-ttu-id="aa72d-176">Hallo **gebruik** -tegel in Hallo [Azure-portal] [ lnk-portal] toont Hallo aantal verzonden berichten toohello IoT-hub:</span><span class="sxs-lookup"><span data-stu-id="aa72d-176">hello **Usage** tile in hello [Azure portal][lnk-portal] shows hello number of messages sent toohello IoT hub:</span></span>

    ![Tegel Usage in Azure Portal][43]

## <a name="next-steps"></a><span data-ttu-id="aa72d-178">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="aa72d-178">Next steps</span></span>

<span data-ttu-id="aa72d-179">In deze zelfstudie maakt u een IoT-hub geconfigureerd in hello Azure-portal en vervolgens een apparaat-id in de id-register Hallo iothub hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="aa72d-179">In this tutorial, you configured an IoT hub in hello Azure portal, and then created a device identity in hello IoT hub's identity registry.</span></span> <span data-ttu-id="aa72d-180">U hebt deze apparaat-id tooenable Hallo apparaat app toosend apparaat-naar-cloudberichten toohello iothub gebruikt.</span><span class="sxs-lookup"><span data-stu-id="aa72d-180">You used this device identity tooenable hello device app toosend device-to-cloud messages toohello IoT hub.</span></span> <span data-ttu-id="aa72d-181">Hebt u ook een app die wordt weergegeven Hallo-berichten dat is ontvangen door de Hallo iothub hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="aa72d-181">You also created an app that displays hello messages received by hello IoT hub.</span></span>

<span data-ttu-id="aa72d-182">toocontinue aan de slag met IoT Hub en tooexplore raadpleegt u andere IoT-scenario's:</span><span class="sxs-lookup"><span data-stu-id="aa72d-182">toocontinue getting started with IoT Hub and tooexplore other IoT scenarios, see:</span></span>

* <span data-ttu-id="aa72d-183">[Verbinding maken met uw apparaat][lnk-connect-device]</span><span class="sxs-lookup"><span data-stu-id="aa72d-183">[Connecting your device][lnk-connect-device]</span></span>
* <span data-ttu-id="aa72d-184">[Aan de slag met apparaatbeheer][lnk-device-management]</span><span class="sxs-lookup"><span data-stu-id="aa72d-184">[Getting started with device management][lnk-device-management]</span></span>
* <span data-ttu-id="aa72d-185">[Aan de slag met IoT Edge][lnk-iot-edge]</span><span class="sxs-lookup"><span data-stu-id="aa72d-185">[Getting started with IoT Edge][lnk-iot-edge]</span></span>

<span data-ttu-id="aa72d-186">toolearn hoe tooextend uw IoT-oplossing en proces apparaat-naar-cloud-berichten op grote schaal, zien Hallo [apparaat-naar-cloud-berichten verwerken] [ lnk-process-d2c-tutorial] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="aa72d-186">toolearn how tooextend your IoT solution and process device-to-cloud messages at scale, see hello [Process device-to-cloud messages][lnk-process-d2c-tutorial] tutorial.</span></span>

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
