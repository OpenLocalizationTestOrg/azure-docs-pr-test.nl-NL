---
title: aaaAzure Iothub operations bewaking | Microsoft Docs
description: Hoe Hallo toouse Azure IoT Hub operations bewaking toomonitor status van bewerkingen voor uw IoT-hub in realtime.
services: iot-hub
documentationcenter: 
author: nberdy
manager: timlt
editor: 
ms.assetid: a299f3a5-b14d-4586-9c3b-44aea14ed013
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.openlocfilehash: a0b233ef2d9bd0827e19fa30fdbdd49b2b61b813
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="iot-hub-operations-monitoring"></a>IoT Hub bewerkingen controleren

IoT Hub operations bewaking kunt u toomonitor Hallo status van bewerkingen voor uw IoT-hub in realtime. IoT Hub houdt gebeurtenissen over verschillende categorieën van bewerkingen. U kunt kiezen voor het verzenden van gebeurtenissen van een of meer categorieën tooan eindpunt van uw iothub voor verwerking. U kunt bewaken Hallo gegevens op fouten of complexe verwerking op basis van gegevenspatronen instellen.

IoT Hub bewaakt zes soorten gebeurtenissen:

* Bewerkingen voor apparaat-id
* De apparaattelemetrie
* Cloud-naar-apparaat-berichten
* Verbindingen
* Uploaden van bestanden
* Berichtroutering

## <a name="how-tooenable-operations-monitoring"></a>Hoe tooenable bewerkingen controleren

1. Een iothub maken. U vindt instructies over het toocreate een IoT-hub in Hallo [aan de slag] [ lnk-get-started] handleiding.

1. Open Hallo-blade van uw IoT-hub. Van daaruit, klikt u op **Operations bewaking**.

    ![Toegangsbewerkingen bewaking van Hallo-portal][1]

1. Selecteer Hallo categorieën die u wenst dat toomonitor en klik op bewaking **opslaan**. Hallo gebeurtenissen zijn beschikbaar voor het lezen van Hallo Event Hub-compatibele eindpunt die worden vermeld in **Bewakingsinstellingen**. Hallo IoT Hub-eindpunt wordt aangeroepen `messages/operationsmonitoringevents`.

    ![Bewerkingen bewaking op uw IoT-hub configureren][2]

> [!NOTE]
> Selecteren **uitgebreid** bewaking voor Hallo **verbindingen** categorie zorgt ervoor dat IoT Hub toogenerate aanvullende diagnostische berichten. Voor alle andere categorieën Hallo **uitgebreid** in elke foutbericht Instellingswijzigingen Hallo hoeveelheid informatie IoT Hub bevat.

## <a name="event-categories-and-how-toouse-them"></a>Gebeurteniscategorieën en hoe toouse ze

Elke categorie houdt bewaking operations een ander type interactie met IoT Hub en elke categorie bewaking is een schema dat bepaalt hoe de structuur van gebeurtenissen in die categorie.

### <a name="device-identity-operations"></a>Bewerkingen voor apparaat-id

identiteit Hallo-bewerkingen apparaatcategorie fouten die zich voordoen wanneer u toocreate probeert houdt, bijwerken of verwijderen van een vermelding in het identiteitenregister van uw IoT-hub. Het bijhouden van deze categorie is nuttig voor het inrichten van scenario's.

```json
{
    "time": "UTC timestamp",
        "operationName": "create",
        "category": "DeviceIdentityOperations",
        "level": "Error",
        "statusCode": 4XX,
        "statusDescription": "MessageDescription",
        "deviceId": "device-ID",
        "durationMs": 1234,
        "userAgent": "userAgent",
        "sharedAccessPolicy": "accessPolicy"
}
```

### <a name="device-telemetry"></a>De apparaattelemetrie

Hallo telemetrie apparaatcategorie houdt fouten die optreden op Hallo IoT-hub en verwante toohello telemetrie pijplijn zijn. Deze categorie bevat fouten die optreden bij het verzenden van telemetriegebeurtenissen (zoals beperking) en telemetrische gebeurtenissen (zoals onbevoegde lezer) ontvangen. Deze categorie kan geen catch-fouten worden veroorzaakt door de code die wordt uitgevoerd op Hallo apparaat zelf.

```json
{
        "messageSizeInBytes": 1234,
        "batching": 0,
        "protocol": "Amqp",
        "authType": "{\"scope\":\"device\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
        "time": "UTC timestamp",
        "operationName": "ingress",
        "category": "DeviceTelemetry",
        "level": "Error",
        "statusCode": 4XX,
        "statusType": 4XX001,
        "statusDescription": "MessageDescription",
        "deviceId": "device-ID",
        "EventProcessedUtcTime": "UTC timestamp",
        "PartitionId": 1,
        "EventEnqueuedUtcTime": "UTC timestamp"
}
```

### <a name="cloud-to-device-commands"></a>Cloud-naar-apparaatopdrachten

Hallo cloud-naar-apparaatopdrachten categorie houdt fouten die optreden op Hallo IoT-hub en verwante toohello cloud-naar-apparaat bericht pijplijn zijn. Deze categorie bevat fouten die optreden bij het verzenden van berichten van de cloud-naar-apparaat (zoals niet-geautoriseerde afzender), het ontvangen van berichten van de cloud-naar-apparaat (zoals levering aantal overschreden) en het cloud-naar-apparaat bericht feedback ontvangen (zoals feedback verlopen). Deze categorie onderschept niet fouten van een apparaat dat een bericht cloud-naar-apparaat niet goed verwerkt als cloud-naar-apparaat het Hallo-bericht met succes is afgeleverd.

```json
{
    "messageSizeInBytes": 1234,
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "deliveryAcknowledgement": 0,
    "protocol": "Amqp",
    "time": " UTC timestamp",
    "operationName": "ingress",
    "category": "C2DCommands",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID",
    "EventProcessedUtcTime": "UTC timestamp",
    "PartitionId": 1,
    "EventEnqueuedUtcTime": “UTC timestamp"
}
```

### <a name="connections"></a>Verbindingen

Hallo verbindingen categorie houdt fouten die optreden wanneer apparaten verbinding maken met of Verbreek de verbinding een IoT-hub tussen. Het bijhouden van deze categorie is handig voor het identificeren van niet-geautoriseerde verbindingspogingen en voor het bijhouden van wanneer een verbinding verbroken voor apparaten in de gebieden van slechte connectiviteit wordt.

```json
{
    "durationMs": 1234,
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "protocol": "Amqp",
    "time": " UTC timestamp",
    "operationName": "deviceConnect",
    "category": "Connections",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID"
}
```

### <a name="file-uploads"></a>Uploaden van bestanden

Hallo-bestand uploaden categorie houdt fouten die optreden op Hallo IoT-hub en verwante toofile uploaden functionaliteit zijn. Deze categorie omvat:

* Fouten die bij Hallo SAS URI optreden, zoals wanneer het voordat een apparaat een melding Hallo hub van het uploaden van een voltooide verloopt.
* Kan niet door Hallo apparaat gemelde uploads.
* Fouten die optreden wanneer een bestand niet in de opslag tijdens het maken van message notification IoT Hub gevonden is.

Deze categorie kan geen catch-fouten die rechtstreeks optreden terwijl Hallo-apparaat is een toostorage bestand uploadt.

```json
{
    "authType": "{\"scope\":\"hub\",\"type\":\"sas\",\"issuer\":\"iothub\"}",
    "protocol": "HTTP",
    "time": " UTC timestamp",
    "operationName": "ingress",
    "category": "fileUpload",
    "level": "Error",
    "statusCode": 4XX,
    "statusType": 4XX001,
    "statusDescription": "MessageDescription",
    "deviceId": "device-ID",
    "blobUri": "http//bloburi.com",
    "durationMs": 1234
}
```

### <a name="message-routing"></a>Berichtroutering

categorie routering Hallo-bericht houdt fouten die optreden tijdens bericht route evaluatie- en eindpunt status waargenomen door de IoT Hub. Deze categorie omvat gebeurtenissen zoals wanneer een regel resulteert te 'niet-gedefinieerde', wanneer IoT Hub markeert een eindpunt als onbestelbare en eventuele andere fouten die zijn ontvangen van een eindpunt. Deze categorie omvat geen specifieke fouten over Hallo-berichten zelf (zoals apparaat beperking fouten), die worden gemeld onder Hallo 'apparaattelemetrie' categorie.

```json
{
    "messageSizeInBytes": 1234,
    "time": "UTC timestamp",
    "operationName": "ingress",
    "category": "routes",
    "level": "Error",
    "deviceId": "device-ID",
    "messageId": "ID of message",
    "routeName": "myroute",
    "endpointName": "myendpoint",
    "details": "ExternalEndpointDisabled"
}
```

## <a name="view-events"></a>Evenementen bekijken

U kunt Hallo *iothub explorer* hulpprogramma tooquickly testen uw IoT-hub genereren van gebeurtenissen voor bewaking. Hallo tooinstall hulpprogramma, Zie de instructies Hallo in Hallo [iothub explorer] [ lnk-iothub-explorer] GitHub-opslagplaats.

1. Zorg ervoor dat Hallo **verbindingen** te bewaken categorie is ingesteld**uitgebreid** in Hallo-portal.

1. Voer Hallo volgende opdracht tooread uit Hallo bewaking eindpunt bij een opdrachtprompt:

    ```
    iothub-explorer monitor-ops --login {your iothubowner connection string}
    ```

1. Voer Hallo opdracht toosimulate na een apparaat verzenden van apparaat-naar-cloud-berichten in een andere opdrachtprompt:

    ```
    iothub-explorer simulate-device {your device name} --send "My test message" --login {your iothubowner connection string}
    ```

1. Hallo eerste opdrachtprompt toont bewakingsgebeurtenissen Hallo Hallo gesimuleerde apparaat verbinding maakt tooyour IoT-hub.

## <a name="connect-toohello-monitoring-endpoint"></a>Verbinding maken met eindpunt bewaking toohello

Hallo bewaking eindpunt op uw IoT-hub is een Event Hub-compatibele eindpunt. U kunt een mechanisme die geschikt is voor Event Hubs tooread bewaking berichten van dit eindpunt. Hallo maakt volgende voorbeeld een basislezer die niet geschikt voor een implementatie met hoge doorvoer. Zie voor meer informatie over hoe tooprocess van van Event Hubs berichten Hallo [aan de slag met Event Hubs] [ lnk-eventhubs-tutorial] zelfstudie.

tooconnect toohello bewaking eindpunt, moet u een tekenreeks en Hallo eindpunt verbindingsnaam. Hallo stappen laten zien hoe toofind vereiste waarden in de portal Hallo Hallo:

1. Navigeer in Hallo portal tooyour resource-blade IoT Hub.

1. Kies **Operations bewaking**, en noteer Hallo **Event Hub-compatibele naam** en **Event Hub-compatibele eindpunt** waarden:

    ![Event Hub-compatibele eindpunt waarden][img-endpoints]

1. Kies **gedeeld toegangsbeleid**, en kies vervolgens **service**. Maak een notitie van Hallo **primaire sleutel** waarde:

    ![Gedeelde beleid primaire toegangssleutel voor][img-service-key]

Hallo volgende C# code steekproef wordt genomen vanuit een Visual Studio **Classic Windows Desktop** C#-consoletoepassing. Hallo-project heeft Hallo **WindowsAzure.ServiceBus** NuGet-pakket geïnstalleerd.

* Tijdelijke aanduiding voor tekenreeks van Hallo-verbinding vervangen door een verbindingsreeks die gebruikmaakt van Hallo **Event Hub-compatibele eindpunt** en service **primaire sleutel** waarden die u eerder weergegeven in de volgende Hallo hebt genoteerd. Voorbeeld:

    ```cs
    "Endpoint={your Event Hub-compatible endpoint};SharedAccessKeyName=service;SharedAccessKey={your service primary key value}"
    ```

* Vervang Hallo bewaking van de tijdelijke aanduiding voor de naam van eindpunt Hello **Event Hub-compatibele naam** waarde die u eerder hebt genoteerd.

```cs
class Program
{
    static string connectionString = "{your monitoring endpoint connection string}";
    static string monitoringEndpointName = "{your monitoring endpoint name}";
    static EventHubClient eventHubClient;

    static void Main(string[] args)
    {
        Console.WriteLine("Monitoring. Press Enter key tooexit.\n");

        eventHubClient = EventHubClient.CreateFromConnectionString(connectionString, monitoringEndpointName);
        var d2cPartitions = eventHubClient.GetRuntimeInformation().PartitionIds;
        CancellationTokenSource cts = new CancellationTokenSource();
        var tasks = new List<Task>();

        foreach (string partition in d2cPartitions)
        {
            tasks.Add(ReceiveMessagesFromDeviceAsync(partition, cts.Token));
        }

        Console.ReadLine();
        Console.WriteLine("Exiting...");
        cts.Cancel();
        Task.WaitAll(tasks.ToArray());
    }

    private static async Task ReceiveMessagesFromDeviceAsync(string partition, CancellationToken ct)
    {
        var eventHubReceiver = eventHubClient.GetDefaultConsumerGroup().CreateReceiver(partition, DateTime.UtcNow);
        while (true)
        {
            if (ct.IsCancellationRequested)
            {
                await eventHubReceiver.CloseAsync();
                break;
            }

            EventData eventData = await eventHubReceiver.ReceiveAsync(new TimeSpan(0,0,10));

            if (eventData != null)
            {
                string data = Encoding.UTF8.GetString(eventData.GetBytes());
                Console.WriteLine("Message received. Partition: {0} Data: '{1}'", partition, data);
            }
        }
    }
}
```

## <a name="next-steps"></a>Volgende stappen
toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:

* [Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide]
* [Een apparaat simuleren met Azure IoT rand][lnk-iotedge]

<!-- Links and images -->
[1]: media/iot-hub-operations-monitoring/enable-OM-1.png
[2]: media/iot-hub-operations-monitoring/enable-OM-2.png
[img-endpoints]: media/iot-hub-operations-monitoring/monitoring-endpoint.png
[img-service-key]: media/iot-hub-operations-monitoring/service-key.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[lnk-diagnostic-metrics]: iot-hub-metrics.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-dr]: iot-hub-ha-dr.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer
[lnk-eventhubs-tutorial]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md