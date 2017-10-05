---
title: Azure IoT Hub-bewerkingen controleren | Microsoft Docs
description: Het gebruik van Azure IoT Hub-bewerkingen voor het controleren van de status van bewerkingen voor uw IoT-hub in real-time bewaking.
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
ms.openlocfilehash: b6de5c5df5f9401a41be152bfa06eb994594e83d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="iot-hub-operations-monitoring"></a><span data-ttu-id="10d0c-103">IoT Hub bewerkingen controleren</span><span class="sxs-lookup"><span data-stu-id="10d0c-103">IoT Hub operations monitoring</span></span>

<span data-ttu-id="10d0c-104">IoT Hub operations bewaking kunt u de status van bewerkingen voor uw IoT-hub in realtime controleren.</span><span class="sxs-lookup"><span data-stu-id="10d0c-104">IoT Hub operations monitoring enables you to monitor the status of operations on your IoT hub in real time.</span></span> <span data-ttu-id="10d0c-105">IoT Hub houdt gebeurtenissen over verschillende categorieën van bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="10d0c-105">IoT Hub tracks events across several categories of operations.</span></span> <span data-ttu-id="10d0c-106">U kunt kiezen voor het verzenden van gebeurtenissen uit een of meer categorieën voor een eindpunt van uw iothub voor verwerking.</span><span class="sxs-lookup"><span data-stu-id="10d0c-106">You can opt into sending events from one or more categories to an endpoint of your IoT hub for processing.</span></span> <span data-ttu-id="10d0c-107">U kunt de gegevens op fouten controleren of complexe verwerking op basis van gegevenspatronen instellen.</span><span class="sxs-lookup"><span data-stu-id="10d0c-107">You can monitor the data for errors or set up more complex processing based on data patterns.</span></span>

<span data-ttu-id="10d0c-108">IoT Hub bewaakt zes soorten gebeurtenissen:</span><span class="sxs-lookup"><span data-stu-id="10d0c-108">IoT Hub monitors six categories of events:</span></span>

* <span data-ttu-id="10d0c-109">Bewerkingen voor apparaat-id</span><span class="sxs-lookup"><span data-stu-id="10d0c-109">Device identity operations</span></span>
* <span data-ttu-id="10d0c-110">De apparaattelemetrie</span><span class="sxs-lookup"><span data-stu-id="10d0c-110">Device telemetry</span></span>
* <span data-ttu-id="10d0c-111">Cloud-naar-apparaat-berichten</span><span class="sxs-lookup"><span data-stu-id="10d0c-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="10d0c-112">Verbindingen</span><span class="sxs-lookup"><span data-stu-id="10d0c-112">Connections</span></span>
* <span data-ttu-id="10d0c-113">Uploaden van bestanden</span><span class="sxs-lookup"><span data-stu-id="10d0c-113">File uploads</span></span>
* <span data-ttu-id="10d0c-114">Berichtroutering</span><span class="sxs-lookup"><span data-stu-id="10d0c-114">Message routing</span></span>

## <a name="how-to-enable-operations-monitoring"></a><span data-ttu-id="10d0c-115">Het inschakelen van bewaking bewerkingen</span><span class="sxs-lookup"><span data-stu-id="10d0c-115">How to enable operations monitoring</span></span>

1. <span data-ttu-id="10d0c-116">Een iothub maken.</span><span class="sxs-lookup"><span data-stu-id="10d0c-116">Create an IoT hub.</span></span> <span data-ttu-id="10d0c-117">U vindt instructies over het maken van een IoT-hub in de [aan de slag] [ lnk-get-started] handleiding.</span><span class="sxs-lookup"><span data-stu-id="10d0c-117">You can find instructions on how to create an IoT hub in the [Get Started][lnk-get-started] guide.</span></span>

1. <span data-ttu-id="10d0c-118">Open de blade van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="10d0c-118">Open the blade of your IoT hub.</span></span> <span data-ttu-id="10d0c-119">Van daaruit, klikt u op **Operations bewaking**.</span><span class="sxs-lookup"><span data-stu-id="10d0c-119">From there, click **Operations monitoring**.</span></span>

    ![Toegangsbewerkingen configuratie in de portal van de bewaking][1]

1. <span data-ttu-id="10d0c-121">Selecteer de bewaking categorieën die u wilt bewaken, en klik vervolgens op **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="10d0c-121">Select the monitoring categories you wish to monitor, and then click **Save**.</span></span> <span data-ttu-id="10d0c-122">De gebeurtenissen beschikbaar zijn voor het lezen van het Event Hub-compatibele eindpunt die worden vermeld in **Bewakingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="10d0c-122">The events are available for reading from the Event Hub-compatible endpoint listed in **Monitoring settings**.</span></span> <span data-ttu-id="10d0c-123">Het eindpunt van de IoT Hub heet `messages/operationsmonitoringevents`.</span><span class="sxs-lookup"><span data-stu-id="10d0c-123">The IoT Hub endpoint is called `messages/operationsmonitoringevents`.</span></span>

    ![Bewerkingen bewaking op uw IoT-hub configureren][2]

> [!NOTE]
> <span data-ttu-id="10d0c-125">Selecteren **uitgebreid** bewaking voor de **verbindingen** categorie zorgt ervoor dat de IoT Hub voor het genereren van aanvullende diagnostische berichten.</span><span class="sxs-lookup"><span data-stu-id="10d0c-125">Selecting **Verbose** monitoring for the **Connections** category causes IoT Hub to generate additional diagnostics messages.</span></span> <span data-ttu-id="10d0c-126">Voor alle andere categorieën, de **uitgebreid** in elke foutbericht instellen van de hoeveelheid gegevens IoT Hub bevat.</span><span class="sxs-lookup"><span data-stu-id="10d0c-126">For all other categories, the **Verbose** setting changes the quantity of information IoT Hub includes in each error message.</span></span>

## <a name="event-categories-and-how-to-use-them"></a><span data-ttu-id="10d0c-127">Gebeurteniscategorieën en hoe ze te gebruiken</span><span class="sxs-lookup"><span data-stu-id="10d0c-127">Event categories and how to use them</span></span>

<span data-ttu-id="10d0c-128">Elke categorie houdt bewaking operations een ander type interactie met IoT Hub en elke categorie bewaking is een schema dat bepaalt hoe de structuur van gebeurtenissen in die categorie.</span><span class="sxs-lookup"><span data-stu-id="10d0c-128">Each operations monitoring category tracks a different type of interaction with IoT Hub, and each monitoring category has a schema that defines how events in that category are structured.</span></span>

### <a name="device-identity-operations"></a><span data-ttu-id="10d0c-129">Bewerkingen voor apparaat-id</span><span class="sxs-lookup"><span data-stu-id="10d0c-129">Device identity operations</span></span>

<span data-ttu-id="10d0c-130">De apparaatcategorie identity-bewerkingen bijgehouden fouten die zich voordoen wanneer u probeert te maken, bijwerken of verwijderen van een vermelding in het identiteitenregister van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="10d0c-130">The device identity operations category tracks errors that occur when you attempt to create, update, or delete an entry in your IoT hub's identity registry.</span></span> <span data-ttu-id="10d0c-131">Het bijhouden van deze categorie is nuttig voor het inrichten van scenario's.</span><span class="sxs-lookup"><span data-stu-id="10d0c-131">Tracking this category is useful for provisioning scenarios.</span></span>

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

### <a name="device-telemetry"></a><span data-ttu-id="10d0c-132">De apparaattelemetrie</span><span class="sxs-lookup"><span data-stu-id="10d0c-132">Device telemetry</span></span>

<span data-ttu-id="10d0c-133">De telemetrie apparaatcategorie houdt fouten die optreden bij de IoT-hub en gerelateerd zijn aan de pijplijn telemetrie.</span><span class="sxs-lookup"><span data-stu-id="10d0c-133">The device telemetry category tracks errors that occur at the IoT hub and are related to the telemetry pipeline.</span></span> <span data-ttu-id="10d0c-134">Deze categorie bevat fouten die optreden bij het verzenden van telemetriegebeurtenissen (zoals beperking) en telemetrische gebeurtenissen (zoals onbevoegde lezer) ontvangen.</span><span class="sxs-lookup"><span data-stu-id="10d0c-134">This category includes errors that occur when sending telemetry events (such as throttling) and receiving telemetry events (such as unauthorized reader).</span></span> <span data-ttu-id="10d0c-135">Deze categorie kan geen catch-fouten worden veroorzaakt door de code die wordt uitgevoerd op het apparaat zelf.</span><span class="sxs-lookup"><span data-stu-id="10d0c-135">This category cannot catch errors caused by code running on the device itself.</span></span>

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

### <a name="cloud-to-device-commands"></a><span data-ttu-id="10d0c-136">Cloud-naar-apparaatopdrachten</span><span class="sxs-lookup"><span data-stu-id="10d0c-136">Cloud-to-device commands</span></span>

<span data-ttu-id="10d0c-137">De categorie cloud-naar-apparaatopdrachten houdt fouten die optreden bij de IoT-hub en gerelateerd zijn aan de pijplijn cloud-naar-apparaat-bericht.</span><span class="sxs-lookup"><span data-stu-id="10d0c-137">The cloud-to-device commands category tracks errors that occur at the IoT hub and are related to the cloud-to-device message pipeline.</span></span> <span data-ttu-id="10d0c-138">Deze categorie bevat fouten die optreden bij het verzenden van berichten van de cloud-naar-apparaat (zoals niet-geautoriseerde afzender), het ontvangen van berichten van de cloud-naar-apparaat (zoals levering aantal overschreden) en het cloud-naar-apparaat bericht feedback ontvangen (zoals feedback verlopen).</span><span class="sxs-lookup"><span data-stu-id="10d0c-138">This category includes errors that occur when sending cloud-to-device messages (such as unauthorized sender), receiving cloud-to-device messages (such as delivery count exceeded), and receiving cloud-to-device message feedback (such as feedback expired).</span></span> <span data-ttu-id="10d0c-139">Deze categorie onderschept fouten van een apparaat dat een bericht cloud-naar-apparaat niet goed verwerkt als de cloud-naar-apparaat-bericht is bezorgd niet.</span><span class="sxs-lookup"><span data-stu-id="10d0c-139">This category does not catch errors from a device that improperly handles a cloud-to-device message if the cloud-to-device message was delivered successfully.</span></span>

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

### <a name="connections"></a><span data-ttu-id="10d0c-140">Verbindingen</span><span class="sxs-lookup"><span data-stu-id="10d0c-140">Connections</span></span>

<span data-ttu-id="10d0c-141">De categorie verbindingen houdt fouten die optreden wanneer apparaten verbinding maken met of Verbreek de verbinding een IoT-hub tussen.</span><span class="sxs-lookup"><span data-stu-id="10d0c-141">The connections category tracks errors that occur when devices connect or disconnect from an IoT hub.</span></span> <span data-ttu-id="10d0c-142">Het bijhouden van deze categorie is handig voor het identificeren van niet-geautoriseerde verbindingspogingen en voor het bijhouden van wanneer een verbinding verbroken voor apparaten in de gebieden van slechte connectiviteit wordt.</span><span class="sxs-lookup"><span data-stu-id="10d0c-142">Tracking this category is useful for identifying unauthorized connection attempts and for tracking when a connection is lost for devices in areas of poor connectivity.</span></span>

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

### <a name="file-uploads"></a><span data-ttu-id="10d0c-143">Uploaden van bestanden</span><span class="sxs-lookup"><span data-stu-id="10d0c-143">File uploads</span></span>

<span data-ttu-id="10d0c-144">Het bestand uploaden categorie houdt fouten die optreden bij de IoT-hub en gerelateerd zijn aan de functionaliteit van het uploaden van bestanden.</span><span class="sxs-lookup"><span data-stu-id="10d0c-144">The file upload category tracks errors that occur at the IoT hub and are related to file upload functionality.</span></span> <span data-ttu-id="10d0c-145">Deze categorie omvat:</span><span class="sxs-lookup"><span data-stu-id="10d0c-145">This category includes:</span></span>

* <span data-ttu-id="10d0c-146">Fouten die bij de SAS-URI optreden, zoals wanneer het voordat een apparaat een melding van de hub van het uploaden van een voltooide verloopt.</span><span class="sxs-lookup"><span data-stu-id="10d0c-146">Errors that occur with the SAS URI, such as when it expires before a device notifies the hub of a completed upload.</span></span>
* <span data-ttu-id="10d0c-147">Kan geen uploads gemeld door het apparaat.</span><span class="sxs-lookup"><span data-stu-id="10d0c-147">Failed uploads reported by the device.</span></span>
* <span data-ttu-id="10d0c-148">Fouten die optreden wanneer een bestand niet in de opslag tijdens het maken van message notification IoT Hub gevonden is.</span><span class="sxs-lookup"><span data-stu-id="10d0c-148">Errors that occur when a file is not found in storage during IoT Hub notification message creation.</span></span>

<span data-ttu-id="10d0c-149">Deze categorie kan geen catch-fouten die rechtstreeks zich tijdens het uploaden van het apparaat is een bestand naar de opslag.</span><span class="sxs-lookup"><span data-stu-id="10d0c-149">This category cannot catch errors that directly occur while the device is uploading a file to storage.</span></span>

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

### <a name="message-routing"></a><span data-ttu-id="10d0c-150">Berichtroutering</span><span class="sxs-lookup"><span data-stu-id="10d0c-150">Message routing</span></span>

<span data-ttu-id="10d0c-151">De routering categorie bericht houdt fouten die optreden tijdens bericht route evaluatie- en eindpunt status waargenomen door de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="10d0c-151">The message routing category tracks errors that occur during message route evaluation and endpoint health as perceived by IoT Hub.</span></span> <span data-ttu-id="10d0c-152">Deze categorie omvat gebeurtenissen zoals wanneer een regel resulteert in 'niet-gedefinieerde', wanneer IoT Hub markeert een eindpunt als onbestelbare en eventuele andere fouten die zijn ontvangen van een eindpunt.</span><span class="sxs-lookup"><span data-stu-id="10d0c-152">This category includes events such as when a rule evaluates to "undefined", when IoT Hub marks an endpoint as dead, and any other errors received from an endpoint.</span></span> <span data-ttu-id="10d0c-153">Deze categorie omvat geen specifieke fouten over de berichten zelf (zoals apparaat beperking fouten), die worden gemeld onder de categorie 'apparaattelemetrie '.</span><span class="sxs-lookup"><span data-stu-id="10d0c-153">This category does not include specific errors about the messages themselves (such as device throttling errors), which are reported under the "device telemetry" category.</span></span>

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

## <a name="view-events"></a><span data-ttu-id="10d0c-154">Evenementen bekijken</span><span class="sxs-lookup"><span data-stu-id="10d0c-154">View events</span></span>

<span data-ttu-id="10d0c-155">U kunt de *iothub explorer* hulpprogramma voor het snel testen van uw IoT-hub genereren van gebeurtenissen voor bewaking.</span><span class="sxs-lookup"><span data-stu-id="10d0c-155">You can use the *iothub-explorer* tool to quickly test that your IoT hub is generating monitoring events.</span></span> <span data-ttu-id="10d0c-156">Zie de instructies in het installeren van het hulpprogramma de [iothub explorer] [ lnk-iothub-explorer] GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="10d0c-156">To install the tool, see the instructions in the [iothub-explorer][lnk-iothub-explorer] GitHub repository.</span></span>

1. <span data-ttu-id="10d0c-157">Zorg ervoor dat de **verbindingen** categorie bewaking is ingesteld op **uitgebreid** in de portal.</span><span class="sxs-lookup"><span data-stu-id="10d0c-157">Make sure the **Connections** monitoring category is set to **Verbose** in the portal.</span></span>

1. <span data-ttu-id="10d0c-158">Voer de volgende opdracht om te lezen van het controle-eindpunt bij een opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="10d0c-158">At a command-prompt, run the following command to read from the monitoring endpoint:</span></span>

    ```
    iothub-explorer monitor-ops --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="10d0c-159">Voer de volgende opdracht om te simuleren van een apparaat verzenden van apparaat-naar-cloud-berichten in een andere opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="10d0c-159">In another command-prompt, run the following command to simulate a device sending device-to-cloud messages:</span></span>

    ```
    iothub-explorer simulate-device {your device name} --send "My test message" --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="10d0c-160">De eerste opdrachtprompt toont de bewakingsgebeurtenissen het gesimuleerde apparaat verbinding maakt met uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="10d0c-160">The first command-prompt shows the monitoring events as the simulated device connects to your IoT hub.</span></span>

## <a name="connect-to-the-monitoring-endpoint"></a><span data-ttu-id="10d0c-161">Verbinding maken met het controle-eindpunt</span><span class="sxs-lookup"><span data-stu-id="10d0c-161">Connect to the monitoring endpoint</span></span>

<span data-ttu-id="10d0c-162">Het eindpunt van de controle op uw IoT-hub is een Event Hub-compatibele eindpunt.</span><span class="sxs-lookup"><span data-stu-id="10d0c-162">The monitoring endpoint on your IoT hub is an Event Hub-compatible endpoint.</span></span> <span data-ttu-id="10d0c-163">U kunt een mechanisme dat werkt met Event Hubs bewaking om berichten te lezen van dit eindpunt.</span><span class="sxs-lookup"><span data-stu-id="10d0c-163">You can use any mechanism that works with Event Hubs to read monitoring messages from this endpoint.</span></span> <span data-ttu-id="10d0c-164">Het volgende voorbeeld maakt een basislezer die niet geschikt voor een implementatie met hoge doorvoer.</span><span class="sxs-lookup"><span data-stu-id="10d0c-164">The following sample creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="10d0c-165">Zie voor meer informatie over het verwerken van Event Hubs-berichten de zelfstudie [Aan de slag met Event Hubs][lnk-eventhubs-tutorial].</span><span class="sxs-lookup"><span data-stu-id="10d0c-165">For more information about how to process messages from Event Hubs, see the [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span>

<span data-ttu-id="10d0c-166">Voor verbinding met het controle-eindpunt, moet u een verbindingsreeks en de naam van het eindpunt.</span><span class="sxs-lookup"><span data-stu-id="10d0c-166">To connect to the monitoring endpoint, you need a connection string and the endpoint name.</span></span> <span data-ttu-id="10d0c-167">De volgende stappen ziet u hoe u de vereiste waarden vinden in de portal:</span><span class="sxs-lookup"><span data-stu-id="10d0c-167">The following steps show you how to find the necessary values in the portal:</span></span>

1. <span data-ttu-id="10d0c-168">Navigeer naar de resourceblade van uw IoT-Hub in de portal.</span><span class="sxs-lookup"><span data-stu-id="10d0c-168">In the portal, navigate to your IoT Hub resource blade.</span></span>

1. <span data-ttu-id="10d0c-169">Kies **Operations bewaking**, en noteer de **Event Hub-compatibele naam** en **Event Hub-compatibele eindpunt** waarden:</span><span class="sxs-lookup"><span data-stu-id="10d0c-169">Choose **Operations monitoring**, and make a note of the **Event Hub-compatible name** and **Event Hub-compatible endpoint** values:</span></span>

    ![Event Hub-compatibele eindpunt waarden][img-endpoints]

1. <span data-ttu-id="10d0c-171">Kies **gedeeld toegangsbeleid**, en kies vervolgens **service**.</span><span class="sxs-lookup"><span data-stu-id="10d0c-171">Choose **Shared access policies**, then choose **service**.</span></span> <span data-ttu-id="10d0c-172">Noteer de **primaire sleutel** waarde:</span><span class="sxs-lookup"><span data-stu-id="10d0c-172">Make a note of the **Primary key** value:</span></span>

    ![Gedeelde beleid primaire toegangssleutel voor][img-service-key]

<span data-ttu-id="10d0c-174">De volgende C#-codevoorbeeld is genomen van een Visual Studio **Classic Windows Desktop** C#-consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="10d0c-174">The following C# code sample is taken from a Visual Studio **Windows Classic Desktop** C# console app.</span></span> <span data-ttu-id="10d0c-175">Het project heeft de **WindowsAzure.ServiceBus** NuGet-pakket geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="10d0c-175">The project has the **WindowsAzure.ServiceBus** NuGet package installed.</span></span>

* <span data-ttu-id="10d0c-176">De tijdelijke aanduiding voor tekenreeks verbinding vervangen door een verbindingsreeks die gebruikmaakt van de **Event Hub-compatibele eindpunt** en service **primaire sleutel** waarden die u eerder weergegeven in het volgende voorbeeld is aangegeven:</span><span class="sxs-lookup"><span data-stu-id="10d0c-176">Replace the connection string placeholder with a connection string that uses the **Event Hub-compatible endpoint** and service **Primary key** values you noted previously as shown in the following example:</span></span>

    ```cs
    "Endpoint={your Event Hub-compatible endpoint};SharedAccessKeyName=service;SharedAccessKey={your service primary key value}"
    ```

* <span data-ttu-id="10d0c-177">Vervang de bewaking eindpunt de naam van de tijdelijke aanduiding met de **Event Hub-compatibele naam** waarde die u eerder hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="10d0c-177">Replace the monitoring endpoint name placeholder with the **Event Hub-compatible name** value you noted previously.</span></span>

```cs
class Program
{
    static string connectionString = "{your monitoring endpoint connection string}";
    static string monitoringEndpointName = "{your monitoring endpoint name}";
    static EventHubClient eventHubClient;

    static void Main(string[] args)
    {
        Console.WriteLine("Monitoring. Press Enter key to exit.\n");

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

## <a name="next-steps"></a><span data-ttu-id="10d0c-178">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="10d0c-178">Next steps</span></span>
<span data-ttu-id="10d0c-179">Als u wilt de mogelijkheden van IoT Hub verder verkennen, Zie:</span><span class="sxs-lookup"><span data-stu-id="10d0c-179">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="10d0c-180">[Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="10d0c-180">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="10d0c-181">[Een apparaat simuleren met Azure IoT rand][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="10d0c-181">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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