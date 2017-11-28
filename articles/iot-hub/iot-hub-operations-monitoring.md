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
# <a name="iot-hub-operations-monitoring"></a><span data-ttu-id="ce96f-103">IoT Hub bewerkingen controleren</span><span class="sxs-lookup"><span data-stu-id="ce96f-103">IoT Hub operations monitoring</span></span>

<span data-ttu-id="ce96f-104">IoT Hub operations bewaking kunt u toomonitor Hallo status van bewerkingen voor uw IoT-hub in realtime.</span><span class="sxs-lookup"><span data-stu-id="ce96f-104">IoT Hub operations monitoring enables you toomonitor hello status of operations on your IoT hub in real time.</span></span> <span data-ttu-id="ce96f-105">IoT Hub houdt gebeurtenissen over verschillende categorieën van bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="ce96f-105">IoT Hub tracks events across several categories of operations.</span></span> <span data-ttu-id="ce96f-106">U kunt kiezen voor het verzenden van gebeurtenissen van een of meer categorieën tooan eindpunt van uw iothub voor verwerking.</span><span class="sxs-lookup"><span data-stu-id="ce96f-106">You can opt into sending events from one or more categories tooan endpoint of your IoT hub for processing.</span></span> <span data-ttu-id="ce96f-107">U kunt bewaken Hallo gegevens op fouten of complexe verwerking op basis van gegevenspatronen instellen.</span><span class="sxs-lookup"><span data-stu-id="ce96f-107">You can monitor hello data for errors or set up more complex processing based on data patterns.</span></span>

<span data-ttu-id="ce96f-108">IoT Hub bewaakt zes soorten gebeurtenissen:</span><span class="sxs-lookup"><span data-stu-id="ce96f-108">IoT Hub monitors six categories of events:</span></span>

* <span data-ttu-id="ce96f-109">Bewerkingen voor apparaat-id</span><span class="sxs-lookup"><span data-stu-id="ce96f-109">Device identity operations</span></span>
* <span data-ttu-id="ce96f-110">De apparaattelemetrie</span><span class="sxs-lookup"><span data-stu-id="ce96f-110">Device telemetry</span></span>
* <span data-ttu-id="ce96f-111">Cloud-naar-apparaat-berichten</span><span class="sxs-lookup"><span data-stu-id="ce96f-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="ce96f-112">Verbindingen</span><span class="sxs-lookup"><span data-stu-id="ce96f-112">Connections</span></span>
* <span data-ttu-id="ce96f-113">Uploaden van bestanden</span><span class="sxs-lookup"><span data-stu-id="ce96f-113">File uploads</span></span>
* <span data-ttu-id="ce96f-114">Berichtroutering</span><span class="sxs-lookup"><span data-stu-id="ce96f-114">Message routing</span></span>

## <a name="how-tooenable-operations-monitoring"></a><span data-ttu-id="ce96f-115">Hoe tooenable bewerkingen controleren</span><span class="sxs-lookup"><span data-stu-id="ce96f-115">How tooenable operations monitoring</span></span>

1. <span data-ttu-id="ce96f-116">Een iothub maken.</span><span class="sxs-lookup"><span data-stu-id="ce96f-116">Create an IoT hub.</span></span> <span data-ttu-id="ce96f-117">U vindt instructies over het toocreate een IoT-hub in Hallo [aan de slag] [ lnk-get-started] handleiding.</span><span class="sxs-lookup"><span data-stu-id="ce96f-117">You can find instructions on how toocreate an IoT hub in hello [Get Started][lnk-get-started] guide.</span></span>

1. <span data-ttu-id="ce96f-118">Open Hallo-blade van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="ce96f-118">Open hello blade of your IoT hub.</span></span> <span data-ttu-id="ce96f-119">Van daaruit, klikt u op **Operations bewaking**.</span><span class="sxs-lookup"><span data-stu-id="ce96f-119">From there, click **Operations monitoring**.</span></span>

    ![Toegangsbewerkingen bewaking van Hallo-portal][1]

1. <span data-ttu-id="ce96f-121">Selecteer Hallo categorieën die u wenst dat toomonitor en klik op bewaking **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="ce96f-121">Select hello monitoring categories you wish toomonitor, and then click **Save**.</span></span> <span data-ttu-id="ce96f-122">Hallo gebeurtenissen zijn beschikbaar voor het lezen van Hallo Event Hub-compatibele eindpunt die worden vermeld in **Bewakingsinstellingen**.</span><span class="sxs-lookup"><span data-stu-id="ce96f-122">hello events are available for reading from hello Event Hub-compatible endpoint listed in **Monitoring settings**.</span></span> <span data-ttu-id="ce96f-123">Hallo IoT Hub-eindpunt wordt aangeroepen `messages/operationsmonitoringevents`.</span><span class="sxs-lookup"><span data-stu-id="ce96f-123">hello IoT Hub endpoint is called `messages/operationsmonitoringevents`.</span></span>

    ![Bewerkingen bewaking op uw IoT-hub configureren][2]

> [!NOTE]
> <span data-ttu-id="ce96f-125">Selecteren **uitgebreid** bewaking voor Hallo **verbindingen** categorie zorgt ervoor dat IoT Hub toogenerate aanvullende diagnostische berichten.</span><span class="sxs-lookup"><span data-stu-id="ce96f-125">Selecting **Verbose** monitoring for hello **Connections** category causes IoT Hub toogenerate additional diagnostics messages.</span></span> <span data-ttu-id="ce96f-126">Voor alle andere categorieën Hallo **uitgebreid** in elke foutbericht Instellingswijzigingen Hallo hoeveelheid informatie IoT Hub bevat.</span><span class="sxs-lookup"><span data-stu-id="ce96f-126">For all other categories, hello **Verbose** setting changes hello quantity of information IoT Hub includes in each error message.</span></span>

## <a name="event-categories-and-how-toouse-them"></a><span data-ttu-id="ce96f-127">Gebeurteniscategorieën en hoe toouse ze</span><span class="sxs-lookup"><span data-stu-id="ce96f-127">Event categories and how toouse them</span></span>

<span data-ttu-id="ce96f-128">Elke categorie houdt bewaking operations een ander type interactie met IoT Hub en elke categorie bewaking is een schema dat bepaalt hoe de structuur van gebeurtenissen in die categorie.</span><span class="sxs-lookup"><span data-stu-id="ce96f-128">Each operations monitoring category tracks a different type of interaction with IoT Hub, and each monitoring category has a schema that defines how events in that category are structured.</span></span>

### <a name="device-identity-operations"></a><span data-ttu-id="ce96f-129">Bewerkingen voor apparaat-id</span><span class="sxs-lookup"><span data-stu-id="ce96f-129">Device identity operations</span></span>

<span data-ttu-id="ce96f-130">identiteit Hallo-bewerkingen apparaatcategorie fouten die zich voordoen wanneer u toocreate probeert houdt, bijwerken of verwijderen van een vermelding in het identiteitenregister van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="ce96f-130">hello device identity operations category tracks errors that occur when you attempt toocreate, update, or delete an entry in your IoT hub's identity registry.</span></span> <span data-ttu-id="ce96f-131">Het bijhouden van deze categorie is nuttig voor het inrichten van scenario's.</span><span class="sxs-lookup"><span data-stu-id="ce96f-131">Tracking this category is useful for provisioning scenarios.</span></span>

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

### <a name="device-telemetry"></a><span data-ttu-id="ce96f-132">De apparaattelemetrie</span><span class="sxs-lookup"><span data-stu-id="ce96f-132">Device telemetry</span></span>

<span data-ttu-id="ce96f-133">Hallo telemetrie apparaatcategorie houdt fouten die optreden op Hallo IoT-hub en verwante toohello telemetrie pijplijn zijn.</span><span class="sxs-lookup"><span data-stu-id="ce96f-133">hello device telemetry category tracks errors that occur at hello IoT hub and are related toohello telemetry pipeline.</span></span> <span data-ttu-id="ce96f-134">Deze categorie bevat fouten die optreden bij het verzenden van telemetriegebeurtenissen (zoals beperking) en telemetrische gebeurtenissen (zoals onbevoegde lezer) ontvangen.</span><span class="sxs-lookup"><span data-stu-id="ce96f-134">This category includes errors that occur when sending telemetry events (such as throttling) and receiving telemetry events (such as unauthorized reader).</span></span> <span data-ttu-id="ce96f-135">Deze categorie kan geen catch-fouten worden veroorzaakt door de code die wordt uitgevoerd op Hallo apparaat zelf.</span><span class="sxs-lookup"><span data-stu-id="ce96f-135">This category cannot catch errors caused by code running on hello device itself.</span></span>

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

### <a name="cloud-to-device-commands"></a><span data-ttu-id="ce96f-136">Cloud-naar-apparaatopdrachten</span><span class="sxs-lookup"><span data-stu-id="ce96f-136">Cloud-to-device commands</span></span>

<span data-ttu-id="ce96f-137">Hallo cloud-naar-apparaatopdrachten categorie houdt fouten die optreden op Hallo IoT-hub en verwante toohello cloud-naar-apparaat bericht pijplijn zijn.</span><span class="sxs-lookup"><span data-stu-id="ce96f-137">hello cloud-to-device commands category tracks errors that occur at hello IoT hub and are related toohello cloud-to-device message pipeline.</span></span> <span data-ttu-id="ce96f-138">Deze categorie bevat fouten die optreden bij het verzenden van berichten van de cloud-naar-apparaat (zoals niet-geautoriseerde afzender), het ontvangen van berichten van de cloud-naar-apparaat (zoals levering aantal overschreden) en het cloud-naar-apparaat bericht feedback ontvangen (zoals feedback verlopen).</span><span class="sxs-lookup"><span data-stu-id="ce96f-138">This category includes errors that occur when sending cloud-to-device messages (such as unauthorized sender), receiving cloud-to-device messages (such as delivery count exceeded), and receiving cloud-to-device message feedback (such as feedback expired).</span></span> <span data-ttu-id="ce96f-139">Deze categorie onderschept niet fouten van een apparaat dat een bericht cloud-naar-apparaat niet goed verwerkt als cloud-naar-apparaat het Hallo-bericht met succes is afgeleverd.</span><span class="sxs-lookup"><span data-stu-id="ce96f-139">This category does not catch errors from a device that improperly handles a cloud-to-device message if hello cloud-to-device message was delivered successfully.</span></span>

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

### <a name="connections"></a><span data-ttu-id="ce96f-140">Verbindingen</span><span class="sxs-lookup"><span data-stu-id="ce96f-140">Connections</span></span>

<span data-ttu-id="ce96f-141">Hallo verbindingen categorie houdt fouten die optreden wanneer apparaten verbinding maken met of Verbreek de verbinding een IoT-hub tussen.</span><span class="sxs-lookup"><span data-stu-id="ce96f-141">hello connections category tracks errors that occur when devices connect or disconnect from an IoT hub.</span></span> <span data-ttu-id="ce96f-142">Het bijhouden van deze categorie is handig voor het identificeren van niet-geautoriseerde verbindingspogingen en voor het bijhouden van wanneer een verbinding verbroken voor apparaten in de gebieden van slechte connectiviteit wordt.</span><span class="sxs-lookup"><span data-stu-id="ce96f-142">Tracking this category is useful for identifying unauthorized connection attempts and for tracking when a connection is lost for devices in areas of poor connectivity.</span></span>

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

### <a name="file-uploads"></a><span data-ttu-id="ce96f-143">Uploaden van bestanden</span><span class="sxs-lookup"><span data-stu-id="ce96f-143">File uploads</span></span>

<span data-ttu-id="ce96f-144">Hallo-bestand uploaden categorie houdt fouten die optreden op Hallo IoT-hub en verwante toofile uploaden functionaliteit zijn.</span><span class="sxs-lookup"><span data-stu-id="ce96f-144">hello file upload category tracks errors that occur at hello IoT hub and are related toofile upload functionality.</span></span> <span data-ttu-id="ce96f-145">Deze categorie omvat:</span><span class="sxs-lookup"><span data-stu-id="ce96f-145">This category includes:</span></span>

* <span data-ttu-id="ce96f-146">Fouten die bij Hallo SAS URI optreden, zoals wanneer het voordat een apparaat een melding Hallo hub van het uploaden van een voltooide verloopt.</span><span class="sxs-lookup"><span data-stu-id="ce96f-146">Errors that occur with hello SAS URI, such as when it expires before a device notifies hello hub of a completed upload.</span></span>
* <span data-ttu-id="ce96f-147">Kan niet door Hallo apparaat gemelde uploads.</span><span class="sxs-lookup"><span data-stu-id="ce96f-147">Failed uploads reported by hello device.</span></span>
* <span data-ttu-id="ce96f-148">Fouten die optreden wanneer een bestand niet in de opslag tijdens het maken van message notification IoT Hub gevonden is.</span><span class="sxs-lookup"><span data-stu-id="ce96f-148">Errors that occur when a file is not found in storage during IoT Hub notification message creation.</span></span>

<span data-ttu-id="ce96f-149">Deze categorie kan geen catch-fouten die rechtstreeks optreden terwijl Hallo-apparaat is een toostorage bestand uploadt.</span><span class="sxs-lookup"><span data-stu-id="ce96f-149">This category cannot catch errors that directly occur while hello device is uploading a file toostorage.</span></span>

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

### <a name="message-routing"></a><span data-ttu-id="ce96f-150">Berichtroutering</span><span class="sxs-lookup"><span data-stu-id="ce96f-150">Message routing</span></span>

<span data-ttu-id="ce96f-151">categorie routering Hallo-bericht houdt fouten die optreden tijdens bericht route evaluatie- en eindpunt status waargenomen door de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ce96f-151">hello message routing category tracks errors that occur during message route evaluation and endpoint health as perceived by IoT Hub.</span></span> <span data-ttu-id="ce96f-152">Deze categorie omvat gebeurtenissen zoals wanneer een regel resulteert te 'niet-gedefinieerde', wanneer IoT Hub markeert een eindpunt als onbestelbare en eventuele andere fouten die zijn ontvangen van een eindpunt.</span><span class="sxs-lookup"><span data-stu-id="ce96f-152">This category includes events such as when a rule evaluates too"undefined", when IoT Hub marks an endpoint as dead, and any other errors received from an endpoint.</span></span> <span data-ttu-id="ce96f-153">Deze categorie omvat geen specifieke fouten over Hallo-berichten zelf (zoals apparaat beperking fouten), die worden gemeld onder Hallo 'apparaattelemetrie' categorie.</span><span class="sxs-lookup"><span data-stu-id="ce96f-153">This category does not include specific errors about hello messages themselves (such as device throttling errors), which are reported under hello "device telemetry" category.</span></span>

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

## <a name="view-events"></a><span data-ttu-id="ce96f-154">Evenementen bekijken</span><span class="sxs-lookup"><span data-stu-id="ce96f-154">View events</span></span>

<span data-ttu-id="ce96f-155">U kunt Hallo *iothub explorer* hulpprogramma tooquickly testen uw IoT-hub genereren van gebeurtenissen voor bewaking.</span><span class="sxs-lookup"><span data-stu-id="ce96f-155">You can use hello *iothub-explorer* tool tooquickly test that your IoT hub is generating monitoring events.</span></span> <span data-ttu-id="ce96f-156">Hallo tooinstall hulpprogramma, Zie de instructies Hallo in Hallo [iothub explorer] [ lnk-iothub-explorer] GitHub-opslagplaats.</span><span class="sxs-lookup"><span data-stu-id="ce96f-156">tooinstall hello tool, see hello instructions in hello [iothub-explorer][lnk-iothub-explorer] GitHub repository.</span></span>

1. <span data-ttu-id="ce96f-157">Zorg ervoor dat Hallo **verbindingen** te bewaken categorie is ingesteld**uitgebreid** in Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="ce96f-157">Make sure hello **Connections** monitoring category is set too**Verbose** in hello portal.</span></span>

1. <span data-ttu-id="ce96f-158">Voer Hallo volgende opdracht tooread uit Hallo bewaking eindpunt bij een opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="ce96f-158">At a command-prompt, run hello following command tooread from hello monitoring endpoint:</span></span>

    ```
    iothub-explorer monitor-ops --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="ce96f-159">Voer Hallo opdracht toosimulate na een apparaat verzenden van apparaat-naar-cloud-berichten in een andere opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="ce96f-159">In another command-prompt, run hello following command toosimulate a device sending device-to-cloud messages:</span></span>

    ```
    iothub-explorer simulate-device {your device name} --send "My test message" --login {your iothubowner connection string}
    ```

1. <span data-ttu-id="ce96f-160">Hallo eerste opdrachtprompt toont bewakingsgebeurtenissen Hallo Hallo gesimuleerde apparaat verbinding maakt tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="ce96f-160">hello first command-prompt shows hello monitoring events as hello simulated device connects tooyour IoT hub.</span></span>

## <a name="connect-toohello-monitoring-endpoint"></a><span data-ttu-id="ce96f-161">Verbinding maken met eindpunt bewaking toohello</span><span class="sxs-lookup"><span data-stu-id="ce96f-161">Connect toohello monitoring endpoint</span></span>

<span data-ttu-id="ce96f-162">Hallo bewaking eindpunt op uw IoT-hub is een Event Hub-compatibele eindpunt.</span><span class="sxs-lookup"><span data-stu-id="ce96f-162">hello monitoring endpoint on your IoT hub is an Event Hub-compatible endpoint.</span></span> <span data-ttu-id="ce96f-163">U kunt een mechanisme die geschikt is voor Event Hubs tooread bewaking berichten van dit eindpunt.</span><span class="sxs-lookup"><span data-stu-id="ce96f-163">You can use any mechanism that works with Event Hubs tooread monitoring messages from this endpoint.</span></span> <span data-ttu-id="ce96f-164">Hallo maakt volgende voorbeeld een basislezer die niet geschikt voor een implementatie met hoge doorvoer.</span><span class="sxs-lookup"><span data-stu-id="ce96f-164">hello following sample creates a basic reader that is not suitable for a high throughput deployment.</span></span> <span data-ttu-id="ce96f-165">Zie voor meer informatie over hoe tooprocess van van Event Hubs berichten Hallo [aan de slag met Event Hubs] [ lnk-eventhubs-tutorial] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="ce96f-165">For more information about how tooprocess messages from Event Hubs, see hello [Get Started with Event Hubs][lnk-eventhubs-tutorial] tutorial.</span></span>

<span data-ttu-id="ce96f-166">tooconnect toohello bewaking eindpunt, moet u een tekenreeks en Hallo eindpunt verbindingsnaam.</span><span class="sxs-lookup"><span data-stu-id="ce96f-166">tooconnect toohello monitoring endpoint, you need a connection string and hello endpoint name.</span></span> <span data-ttu-id="ce96f-167">Hallo stappen laten zien hoe toofind vereiste waarden in de portal Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="ce96f-167">hello following steps show you how toofind hello necessary values in hello portal:</span></span>

1. <span data-ttu-id="ce96f-168">Navigeer in Hallo portal tooyour resource-blade IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ce96f-168">In hello portal, navigate tooyour IoT Hub resource blade.</span></span>

1. <span data-ttu-id="ce96f-169">Kies **Operations bewaking**, en noteer Hallo **Event Hub-compatibele naam** en **Event Hub-compatibele eindpunt** waarden:</span><span class="sxs-lookup"><span data-stu-id="ce96f-169">Choose **Operations monitoring**, and make a note of hello **Event Hub-compatible name** and **Event Hub-compatible endpoint** values:</span></span>

    ![Event Hub-compatibele eindpunt waarden][img-endpoints]

1. <span data-ttu-id="ce96f-171">Kies **gedeeld toegangsbeleid**, en kies vervolgens **service**.</span><span class="sxs-lookup"><span data-stu-id="ce96f-171">Choose **Shared access policies**, then choose **service**.</span></span> <span data-ttu-id="ce96f-172">Maak een notitie van Hallo **primaire sleutel** waarde:</span><span class="sxs-lookup"><span data-stu-id="ce96f-172">Make a note of hello **Primary key** value:</span></span>

    ![Gedeelde beleid primaire toegangssleutel voor][img-service-key]

<span data-ttu-id="ce96f-174">Hallo volgende C# code steekproef wordt genomen vanuit een Visual Studio **Classic Windows Desktop** C#-consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="ce96f-174">hello following C# code sample is taken from a Visual Studio **Windows Classic Desktop** C# console app.</span></span> <span data-ttu-id="ce96f-175">Hallo-project heeft Hallo **WindowsAzure.ServiceBus** NuGet-pakket geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ce96f-175">hello project has hello **WindowsAzure.ServiceBus** NuGet package installed.</span></span>

* <span data-ttu-id="ce96f-176">Tijdelijke aanduiding voor tekenreeks van Hallo-verbinding vervangen door een verbindingsreeks die gebruikmaakt van Hallo **Event Hub-compatibele eindpunt** en service **primaire sleutel** waarden die u eerder weergegeven in de volgende Hallo hebt genoteerd. Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ce96f-176">Replace hello connection string placeholder with a connection string that uses hello **Event Hub-compatible endpoint** and service **Primary key** values you noted previously as shown in hello following example:</span></span>

    ```cs
    "Endpoint={your Event Hub-compatible endpoint};SharedAccessKeyName=service;SharedAccessKey={your service primary key value}"
    ```

* <span data-ttu-id="ce96f-177">Vervang Hallo bewaking van de tijdelijke aanduiding voor de naam van eindpunt Hello **Event Hub-compatibele naam** waarde die u eerder hebt genoteerd.</span><span class="sxs-lookup"><span data-stu-id="ce96f-177">Replace hello monitoring endpoint name placeholder with hello **Event Hub-compatible name** value you noted previously.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="ce96f-178">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ce96f-178">Next steps</span></span>
<span data-ttu-id="ce96f-179">toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:</span><span class="sxs-lookup"><span data-stu-id="ce96f-179">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="ce96f-180">[Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="ce96f-180">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="ce96f-181">[Een apparaat simuleren met Azure IoT rand][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="ce96f-181">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

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