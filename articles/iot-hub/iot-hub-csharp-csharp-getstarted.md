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
# <a name="connect-your-device-tooyour-iot-hub-using-net"></a>Verbinding maken met uw apparaat tooyour iothub met .NET

[!INCLUDE [iot-hub-selector-get-started](../../includes/iot-hub-selector-get-started.md)]

Aan het einde van de Hallo van deze zelfstudie hebt u drie console .NET-toepassingen:

* **CreateDeviceIdentity**, die een apparaat-id maakt en gekoppelde beveiliging sleutel tooconnect app op uw apparaat.
* **ReadDeviceToCloudMessages**, weergeven met Hallo telemetrie verzonden door de app op uw apparaat.
* **SimulatedDevice**, die tooyour IoT-hub aan Hallo apparaat-id eerder hebt gemaakt, en verzendt een bericht telemetrie elke seconde met behulp van Hallo MQTT protocol.

U kunt downloaden of kloon van de Visual Studio-oplossing hello, waarin drie Hallo-apps vanuit Github.

```bash
git clone https://github.com/Azure-Samples/iot-hub-dotnet-simulated-device-client-app.git
```

> [!NOTE]
> Zie voor informatie over hello Azure IoT SDK's waarmee u toobuild kunt toorun toepassingen op apparaten en uw back-end oplossing, [Azure IoT SDK's][lnk-hub-sdks].

toocomplete in deze zelfstudie, moet u hello te volgen:

* Visual Studio 2015 of Visual Studio 2017.
* Een actief Azure-account. (Als u geen account hebt, kunt u binnen een paar minuten een [gratis account][lnk-free-trial] maken.)

[!INCLUDE [iot-hub-get-started-create-hub](../../includes/iot-hub-get-started-create-hub.md)]

U hebt nu uw IoT-hub gemaakt en u hebt Hallo-hostnaam en verbindingsreeks van IoT Hub dat u nodig hebt toocomplete Hallo rest van deze handleiding.

<a id="DeviceIdentity_csharp"></a>
[!INCLUDE [iot-hub-get-started-create-device-identity-csharp](../../includes/iot-hub-get-started-create-device-identity-csharp.md)]

<a id="D2C_csharp"></a>
## <a name="receive-device-to-cloud-messages"></a>Apparaat-naar-cloud-berichten ontvangen
In dit gedeelte maakt u een .NET-consoletoepassing die apparaat-naar-cloud-berichten uit IoT Hub kan lezen. Een iothub toont een [Azure Event Hubs][lnk-event-hubs-overview]-compatibel eindpunt tooenable u tooread apparaat-naar-cloud-berichten. tookeep dingen eenvoudige, deze zelfstudie maakt u een basislezer die niet geschikt voor een implementatie met hoge doorvoer. toolearn hoe tooprocess apparaat-naar-cloud-berichten op grote schaal, Zie Hallo [apparaat-naar-cloud-berichten verwerken] [ lnk-process-d2c-tutorial] zelfstudie. Zie voor meer informatie over hoe tooprocess van van Event Hubs berichten Hallo [aan de slag met Event Hubs] [ lnk-eventhubs-tutorial] zelfstudie. (Deze zelfstudie is van toepassing toohello IoT Hub Event Hub-compatibele eindpunten.)

> [!NOTE]
> Hallo Event Hub-compatibele eindpunt voor het lezen van apparaat-naar-cloudberichten altijd gebruikt Hallo AMQP-protocol.

1. Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toohello huidige oplossing met behulp van Hallo **Console-App (.NET Framework)** projectsjabloon. Zorg ervoor dat .NET Framework-versie Hallo 4.5.1 of later. Naam Hallo project **ReadDeviceToCloudMessages**.

    ![Nieuw Windows Classic Desktop-project in Visual C#][10a]

2. Klik in Solution Explorer met de rechtermuisknop op Hallo **ReadDeviceToCloudMessages** project en klik vervolgens op **NuGet-pakketten beheren**.

3. In Hallo **NuGet Package Manager** venster, zoekt u **WindowsAzure.ServiceBus**, selecteer **installeren**, en accepteer de gebruiksvoorwaarden Hallo. Deze procedure downloadt, installeert en voegt u een verwijzing te[Azure Service Bus][lnk-servicebus-nuget], inclusief alle afhankelijkheden ervan. Met dit pakket kan Hallo toepassing tooconnect toohello Event Hub-compatibele eindpunt op uw IoT-hub.

4. Voeg de volgende Hallo `using` instructies boven Hallo Hallo **Program.cs** bestand:

    ```csharp
    using Microsoft.ServiceBus.Messaging;
    using System.Threading;
    ```

5. Hallo na toohello velden toevoegen **programma** klasse. Vervang Hallo tijdelijke aanduidingswaarde met IoT Hub-verbindingsreeks voor Hallo-hub die u hebt gemaakt in de sectie 'Een IoT-hub maken' Hallo Hallo.

    ```csharp
    static string connectionString = "{iothub connection string}";
    static string iotHubD2cEndpoint = "messages/events";
    static EventHubClient eventHubClient;
    ```

6. Hallo na methode toohello toevoegen **programma** klasse:

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

    Deze methode gebruikt een **EventHubReceiver** exemplaar tooreceive berichten van alle Hallo IoT hub apparaat-naar-cloud ontvangstpartities. U geeft een `DateTime.Now` parameter bij het maken van Hallo **EventHubReceiver** object, zodat alleen verzonden nadat deze is gestart berichten worden ontvangen. Dit filter is handig in een testomgeving zodat u Hallo huidige reeks berichten kunt zien. In een productieomgeving moet uw code ervoor zorgen dat alle Hallo-berichten worden verwerkt. Zie voor meer informatie, Hallo zelfstudie [hoe tooprocess IoT Hub apparaat-naar-cloud-berichten][lnk-process-d2c-tutorial].

7. Voeg regels toohello na Hallo **Main** methode:

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

## <a name="create-a-device-app"></a>Een apparaat-app maken

In deze sectie maakt u een .NET consoletoepassing maken die een apparaat simuleert dat apparaat-naar-cloudberichten tooan iothub verzendt.

1. Voeg in Visual Studio een Visual C# Classic Windows Desktop-project toohello huidige oplossing met behulp van Hallo **Console-App (.NET Framework)** projectsjabloon. Zorg ervoor dat .NET Framework-versie Hallo 4.5.1 of later. Naam Hallo project **SimulatedDevice**.

    ![Nieuw Windows Classic Desktop-project in Visual C#][10b]

2. Klik in Solution Explorer met de rechtermuisknop op Hallo **SimulatedDevice** project en klik vervolgens op **NuGet-pakketten beheren**.

3. In Hallo **NuGet Package Manager** Selecteer **Bladeren**, zoeken naar **Microsoft.Azure.Devices.Client**, selecteer **installeren** Hallo tooinstall **Microsoft.Azure.Devices.Client** Inpakken en accepteer de gebruiksvoorwaarden Hallo. Deze procedure downloadt, installeert en voegt u een verwijzing toohello [Azure IoT-device SDK NuGet-pakket] [ lnk-device-nuget] en de bijbehorende afhankelijkheden.

4. Voeg de volgende Hallo `using` instructie bovenaan Hallo Hallo **Program.cs** bestand:

    ```csharp
    using Microsoft.Azure.Devices.Client;
    using Newtonsoft.Json;
    ```

5. Hallo na toohello velden toevoegen **programma** klasse. Vervang `{iot hub hostname}` met Hallo IoT hub-hostnaam u in het gedeelte voor Hallo 'Een IoT-hub maken' hebt opgehaald. Vervang `{device key}` met Hallo apparaatsleutel die u hebt opgehaald in het gedeelte voor Hallo 'Een apparaat-id maken'.

    ```csharp
    static DeviceClient deviceClient;
    static string iotHubUri = "{iot hub hostname}";
    static string deviceKey = "{device key}";
    ```

6. Hallo na methode toohello toevoegen **programma** klasse:

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

    Met deze methode wordt elke seconde een nieuw apparaat-naar-cloud bericht verzonden. Hallo-bericht bevat een JSON-geserialiseerd object, met Hallo apparaat-ID en willekeurige cijfers toosimulate een temperatuursensor en een sensor vochtigheid.

7. Voeg regels toohello na Hallo **Main** methode:

    ```csharp
    Console.WriteLine("Simulated device\n");
    deviceClient = DeviceClient.Create(iotHubUri, new DeviceAuthenticationWithRegistrySymmetricKey ("myFirstDevice", deviceKey), TransportType.Mqtt);

    SendDeviceToCloudMessagesAsync();
    Console.ReadLine();
    ```

    Standaard Hallo **maken** methode in een .NET Framework-app maakt een **DeviceClient** -exemplaar dat gebruikmaakt van Hallo AMQP-protocol toocommunicate met IoT Hub. toouse hello MQTT of HTTP-protocol gebruiken Hallo onderdrukking Hallo **maken** methode waarmee u toospecify Hallo-protocol. UWP en PCL clients Hallo HTTP-protocol standaard gebruikt. Als u Hallo HTTP-protocol gebruikt, moet u ook Hallo toevoegen **Microsoft.AspNet.WebApi.Client** NuGet-pakket tooyour project tooinclude hello **System.Net.Http.Formatting** naamruimte.

Deze zelfstudie leert u Hallo stappen toocreate een IoT Hub apparaat-app. U kunt ook Hallo [Connected Service for Azure IoT Hub] [ lnk-connected-service] Visual Studio-extensie tooadd Hallo benodigde code tooyour app voor het apparaat.

> [!NOTE]
> tookeep dingen eenvoudige, deze zelfstudie wordt niet geïmplementeerd voor een beleid voor opnieuw proberen. In productiecode moet u beleid voor opnieuw proberen (zoals exponentieel uitstel), zoals voorgesteld in de MSDN-artikel Hallo implementeren [afhandeling van tijdelijke fout][lnk-transient-faults].

## <a name="run-hello-apps"></a>Hallo-apps uitvoeren

U bent nu klaar toorun Hallo apps.

1. Klik in Solution Explorer, in Visual Studio, met de rechtermuisknop op uw oplossing en klik vervolgens op **Set StartUp projects**. Selecteer **meerdere opstartprojecten**, en selecteer vervolgens **Start** als actie voor beide Hallo Hallo **ReadDeviceToCloudMessages** en **SimulatedDevice** projecten.

    ![Eigenschappen van opstartprojecten][41]

2. Druk op **F5** toostart beide apps die worden uitgevoerd. console-uitvoer van Hallo Hallo **SimulatedDevice** app Hallo berichten app op uw apparaat tooyour iothub verzendt. console-uitvoer van Hallo Hallo **ReadDeviceToCloudMessages** app toont Hallo-berichten die uw IoT-hub ontvangt.

    ![Console-uitvoer van apps][42]

3. Hallo **gebruik** -tegel in Hallo [Azure-portal] [ lnk-portal] toont Hallo aantal verzonden berichten toohello IoT-hub:

    ![Tegel Usage in Azure Portal][43]

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie maakt u een IoT-hub geconfigureerd in hello Azure-portal en vervolgens een apparaat-id in de id-register Hallo iothub hebt gemaakt. U hebt deze apparaat-id tooenable Hallo apparaat app toosend apparaat-naar-cloudberichten toohello iothub gebruikt. Hebt u ook een app die wordt weergegeven Hallo-berichten dat is ontvangen door de Hallo iothub hebt gemaakt.

toocontinue aan de slag met IoT Hub en tooexplore raadpleegt u andere IoT-scenario's:

* [Verbinding maken met uw apparaat][lnk-connect-device]
* [Aan de slag met apparaatbeheer][lnk-device-management]
* [Aan de slag met IoT Edge][lnk-iot-edge]

toolearn hoe tooextend uw IoT-oplossing en proces apparaat-naar-cloud-berichten op grote schaal, zien Hallo [apparaat-naar-cloud-berichten verwerken] [ lnk-process-d2c-tutorial] zelfstudie.

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
