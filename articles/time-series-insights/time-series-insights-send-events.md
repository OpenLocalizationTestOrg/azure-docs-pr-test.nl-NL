---
title: Gebeurtenissen verzenden naar een Azure Time Series Insights-omgeving | Microsoft Docs
description: In deze zelfstudie worden de stappen besproken voor het verzenden van gebeurtenissen naar uw Time Series Insights-omgeving
keywords: 
services: tsi
documentationcenter: 
author: venkatgct
manager: jhubbard
editor: 
ms.assetid: 
ms.service: tsi
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/21/2017
ms.author: venkatja
ms.openlocfilehash: b4ef96a045393f28b3cd750068fe82a5a8411afa
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="send-events-to-a-time-series-insights-environment-using-event-hub"></a><span data-ttu-id="ae224-103">Gebeurtenissen verzenden naar een Time Series Insights-omgeving met Event Hub</span><span class="sxs-lookup"><span data-stu-id="ae224-103">Send events to a Time Series Insights environment using event hub</span></span>

<span data-ttu-id="ae224-104">In deze zelfstudie wordt uitgelegd hoe u een Event Hub maakt en configureert, en een voorbeeldtoepassing uitvoert om gebeurtenissen te verzenden.</span><span class="sxs-lookup"><span data-stu-id="ae224-104">This tutorial explains how to create and configure event hub and run a sample application to push events.</span></span> <span data-ttu-id="ae224-105">Als u een bestaande Event Hub hebt die al gebeurtenissen in JSON-indeling bevat, kunt u deze zelfstudie overslaan en uw omgeving bekijken in [Time Series Insights](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ae224-105">If you have an existing event hub with events in JSON format, skip this tutorial and view your environment in [time series insights](https://insights.timeseries.azure.com).</span></span>

## <a name="configure-an-event-hub"></a><span data-ttu-id="ae224-106">Een Event Hub configureren</span><span class="sxs-lookup"><span data-stu-id="ae224-106">Configure an event hub</span></span>
1. <span data-ttu-id="ae224-107">Voor het maken van uw Event Hub volgt u de instructies in de Event Hub-[documentatie](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).</span><span class="sxs-lookup"><span data-stu-id="ae224-107">To create an event hub, follow instructions from the Event Hub [documentation](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).</span></span>

2. <span data-ttu-id="ae224-108">Zorg ervoor dat u een consumergroep maakt die uitsluitend door uw Time Series Insights-gebeurtenisbron wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ae224-108">Make sure you create a consumer group that is used exclusively by your Time Series Insights event source.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="ae224-109">Deze consumergroep mag niet worden gebruikt door een andere service (zoals een Stream Analytics-taak of een andere Time Series Insights-omgeving).</span><span class="sxs-lookup"><span data-stu-id="ae224-109">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment).</span></span> <span data-ttu-id="ae224-110">Als de consumergroep wordt gebruikt door andere services, wordt de leesbewerking negatief beïnvloed voor deze omgeving en de andere services.</span><span class="sxs-lookup"><span data-stu-id="ae224-110">If consumer group is used by other services, read operation is negatively affected for this environment and the other services.</span></span> <span data-ttu-id="ae224-111">Als u $Default als consumergroep selecteert, kan dit leiden tot mogelijk hergebruik door andere lezers.</span><span class="sxs-lookup"><span data-stu-id="ae224-111">If you are using “$Default” as the consumer group, it could lead to potential reuse by other readers.</span></span>

  ![Event Hub-consumergroep selecteren](media/send-events/consumer-group.png)

3. <span data-ttu-id="ae224-113">Maak in de Event Hub 'MySendPolicy'. Dit wordt gebruikt voor het verzenden van gebeurtenissen in het csharp-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="ae224-113">On the event hub, create “MySendPolicy” that is used to send events in the csharp sample.</span></span>

  ![Een beleid voor gedeelde toegang selecteren en klikken op de knop Toevoegen](media/send-events/shared-access-policy.png)  

  ![Een nieuw beleid voor gedeelde toegang toevoegen](media/send-events/shared-access-policy-2.png)  

## <a name="create-time-series-insights-event-source"></a><span data-ttu-id="ae224-116">Een Time Series Insights-gebeurtenisbron maken</span><span class="sxs-lookup"><span data-stu-id="ae224-116">Create Time Series Insights event source</span></span>
1. <span data-ttu-id="ae224-117">Als u nog geen gebeurtenisbron hebt gemaakt, volgt u [deze instructies](time-series-insights-add-event-source.md) om een gebeurtenisbron te maken.</span><span class="sxs-lookup"><span data-stu-id="ae224-117">If you haven't created an event source, follow [these instructions](time-series-insights-add-event-source.md) to create an event source.</span></span>

2. <span data-ttu-id="ae224-118">Geef 'deviceTimestamp' op als de naam van de tijdstempeleigenschap. Deze eigenschap wordt gebruikt als de werkelijke tijdstempel in het csharp-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="ae224-118">Specify “deviceTimestamp” as the timestamp property name – this property is used as the actual timestamp in the csharp sample.</span></span> <span data-ttu-id="ae224-119">De naam van de tijdstempeleigenschap is hoofdlettergevoelig en waarden moeten de indeling __jjjj-MM-ddTUU. FFFFFFFK__ volgen wanneer ze als JSON worden verzonden naar een Event Hub.</span><span class="sxs-lookup"><span data-stu-id="ae224-119">The timestamp property name is case-sensitive and values must follow the format __yyyy-MM-ddTHH:mm:ss.FFFFFFFK__ when sent as JSON to event hub.</span></span> <span data-ttu-id="ae224-120">Als de eigenschap niet aanwezig is in de gebeurtenis, wordt de tijd gebruikt waarop de gebeurtenis in de wachtrij van de Event Hub is geplaatst.</span><span class="sxs-lookup"><span data-stu-id="ae224-120">If the property does not exist in the event, then the event hub enqueued time is used.</span></span>

  ![Gebeurtenisbron maken](media/send-events/event-source-1.png)

## <a name="sample-code-to-push-events"></a><span data-ttu-id="ae224-122">Voorbeeldcode uitvoeren om gebeurtenissen te pushen</span><span class="sxs-lookup"><span data-stu-id="ae224-122">Sample code to push events</span></span>
1. <span data-ttu-id="ae224-123">Ga naar het Event Hub-beleid 'MySendPolicy' en kopieer de verbindingsreeks met de beleidssleutel.</span><span class="sxs-lookup"><span data-stu-id="ae224-123">Go to the event hub policy “MySendPolicy” and copy the connection string with the policy key.</span></span>

  ![MySendPolicy-verbindingsreeks kopiëren](media/send-events/sample-code-connection-string.png)

2. <span data-ttu-id="ae224-125">Voer de volgende code uit, waarmee voor elk van de drie apparaten 600 gebeurtenissen worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="ae224-125">Run the following code that to send 600 events per each of the three devices.</span></span> <span data-ttu-id="ae224-126">Werk `eventHubConnectionString` bij met uw verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="ae224-126">Update `eventHubConnectionString` with your connection string.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Globalization;
using System.IO;
using Microsoft.ServiceBus.Messaging;

namespace Microsoft.Rdx.DataGenerator
{
    internal class Program
    {
        private static void Main(string[] args)
        {
            var from = new DateTime(2017, 4, 20, 15, 0, 0, DateTimeKind.Utc);
            Random r = new Random();
            const int numberOfEvents = 600;

            var deviceIds = new[] { "device1", "device2", "device3" };

            var events = new List<string>();
            for (int i = 0; i < numberOfEvents; ++i)
            {
                for (int device = 0; device < deviceIds.Length; ++device)
                {
                    // Generate event and serialize as JSON object:
                    // { "deviceTimestamp": "utc timestamp", "deviceId": "guid", "value": 123.456 }
                    events.Add(
                        String.Format(
                            CultureInfo.InvariantCulture,
                            @"{{ ""deviceTimestamp"": ""{0}"", ""deviceId"": ""{1}"", ""value"": {2} }}",
                            (from + TimeSpan.FromSeconds(i * 30)).ToString("o"),
                            deviceIds[device],
                            r.NextDouble()));
                }
            }

            // Create event hub connection.
            var eventHubConnectionString = @"Endpoint=sb://...";
            var eventHubClient = EventHubClient.CreateFromConnectionString(eventHubConnectionString);

            using (var ms = new MemoryStream())
            using (var sw = new StreamWriter(ms))
            {
                // Wrap events into JSON array:
                sw.Write("[");
                for (int i = 0; i < events.Count; ++i)
                {
                    if (i > 0)
                    {
                        sw.Write(',');
                    }
                    sw.Write(events[i]);
                }
                sw.Write("]");

                sw.Flush();
                ms.Position = 0;

                // Send JSON to event hub.
                EventData eventData = new EventData(ms);
                eventHubClient.Send(eventData);
            }
        }
    }
}

```
## <a name="supported-json-shapes"></a><span data-ttu-id="ae224-127">Ondersteunde JSON-vormen</span><span class="sxs-lookup"><span data-stu-id="ae224-127">Supported JSON shapes</span></span>
### <a name="sample-1"></a><span data-ttu-id="ae224-128">Voorbeeld 1</span><span class="sxs-lookup"><span data-stu-id="ae224-128">Sample 1</span></span>

#### <a name="input"></a><span data-ttu-id="ae224-129">Invoer</span><span class="sxs-lookup"><span data-stu-id="ae224-129">Input</span></span>

<span data-ttu-id="ae224-130">Een eenvoudig JSON-object.</span><span class="sxs-lookup"><span data-stu-id="ae224-130">A simple JSON object.</span></span>

```json
{
    "id":"device1",
    "timestamp":"2016-01-08T01:08:00Z"
}
```
#### <a name="output---1-event"></a><span data-ttu-id="ae224-131">Uitvoer - 1 gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="ae224-131">Output - 1 event</span></span>

|<span data-ttu-id="ae224-132">id</span><span class="sxs-lookup"><span data-stu-id="ae224-132">id</span></span>|<span data-ttu-id="ae224-133">tijdstempel</span><span class="sxs-lookup"><span data-stu-id="ae224-133">timestamp</span></span>|
|--------|---------------|
|<span data-ttu-id="ae224-134">device1</span><span class="sxs-lookup"><span data-stu-id="ae224-134">device1</span></span>|<span data-ttu-id="ae224-135">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="ae224-135">2016-01-08T01:08:00Z</span></span>|

### <a name="sample-2"></a><span data-ttu-id="ae224-136">Voorbeeld 2</span><span class="sxs-lookup"><span data-stu-id="ae224-136">Sample 2</span></span>

#### <a name="input"></a><span data-ttu-id="ae224-137">Invoer</span><span class="sxs-lookup"><span data-stu-id="ae224-137">Input</span></span>
<span data-ttu-id="ae224-138">Een JSON-matrix met twee JSON-objecten.</span><span class="sxs-lookup"><span data-stu-id="ae224-138">A JSON array with two JSON objects.</span></span> <span data-ttu-id="ae224-139">Elk JSON-object wordt omgezet in een gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="ae224-139">Each JSON object will be converted to an event.</span></span>
```json
[
    {
        "id":"device1",
        "timestamp":"2016-01-08T01:08:00Z"
    },
    {
        "id":"device2",
        "timestamp":"2016-01-17T01:17:00Z"
    }
]
```
#### <a name="output---2-events"></a><span data-ttu-id="ae224-140">Uitvoer - 2 gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="ae224-140">Output - 2 Events</span></span>

|<span data-ttu-id="ae224-141">id</span><span class="sxs-lookup"><span data-stu-id="ae224-141">id</span></span>|<span data-ttu-id="ae224-142">tijdstempel</span><span class="sxs-lookup"><span data-stu-id="ae224-142">timestamp</span></span>|
|--------|---------------|
|<span data-ttu-id="ae224-143">device1</span><span class="sxs-lookup"><span data-stu-id="ae224-143">device1</span></span>|<span data-ttu-id="ae224-144">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="ae224-144">2016-01-08T01:08:00Z</span></span>|
|<span data-ttu-id="ae224-145">device2</span><span class="sxs-lookup"><span data-stu-id="ae224-145">device2</span></span>|<span data-ttu-id="ae224-146">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="ae224-146">2016-01-08T01:17:00Z</span></span>|
### <a name="sample-3"></a><span data-ttu-id="ae224-147">Voorbeeld 3</span><span class="sxs-lookup"><span data-stu-id="ae224-147">Sample 3</span></span>

#### <a name="input"></a><span data-ttu-id="ae224-148">Invoer</span><span class="sxs-lookup"><span data-stu-id="ae224-148">Input</span></span>

<span data-ttu-id="ae224-149">Een JSON-object met een geneste JSON-matrix met twee JSON-objecten.</span><span class="sxs-lookup"><span data-stu-id="ae224-149">A JSON object with a nested JSON array containing two JSON objects.</span></span>
```json
{
    "location":"WestUs",
    "events":[
        {
            "id":"device1",
            "timestamp":"2016-01-08T01:08:00Z"
        },
        {
            "id":"device2",
            "timestamp":"2016-01-17T01:17:00Z"
        }
    ]
}

```
#### <a name="output---2-events"></a><span data-ttu-id="ae224-150">Uitvoer - 2 gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="ae224-150">Output - 2 Events</span></span>
<span data-ttu-id="ae224-151">Houd er rekening mee dat de eigenschap 'location' naar elk van de gebeurtenissen wordt gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="ae224-151">Note that the property "location" is copied over to each of the event.</span></span>

|<span data-ttu-id="ae224-152">location</span><span class="sxs-lookup"><span data-stu-id="ae224-152">location</span></span>|<span data-ttu-id="ae224-153">events.id</span><span class="sxs-lookup"><span data-stu-id="ae224-153">events.id</span></span>|<span data-ttu-id="ae224-154">events.timestamp</span><span class="sxs-lookup"><span data-stu-id="ae224-154">events.timestamp</span></span>|
|--------|---------------|----------------------|
|<span data-ttu-id="ae224-155">WestUs</span><span class="sxs-lookup"><span data-stu-id="ae224-155">WestUs</span></span>|<span data-ttu-id="ae224-156">device1</span><span class="sxs-lookup"><span data-stu-id="ae224-156">device1</span></span>|<span data-ttu-id="ae224-157">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="ae224-157">2016-01-08T01:08:00Z</span></span>|
|<span data-ttu-id="ae224-158">WestUs</span><span class="sxs-lookup"><span data-stu-id="ae224-158">WestUs</span></span>|<span data-ttu-id="ae224-159">device2</span><span class="sxs-lookup"><span data-stu-id="ae224-159">device2</span></span>|<span data-ttu-id="ae224-160">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="ae224-160">2016-01-08T01:17:00Z</span></span>|

### <a name="sample-4"></a><span data-ttu-id="ae224-161">Voorbeeld 4</span><span class="sxs-lookup"><span data-stu-id="ae224-161">Sample 4</span></span>

#### <a name="input"></a><span data-ttu-id="ae224-162">Invoer</span><span class="sxs-lookup"><span data-stu-id="ae224-162">Input</span></span>

<span data-ttu-id="ae224-163">Een JSON-object met een geneste JSON-matrix met twee JSON-objecten.</span><span class="sxs-lookup"><span data-stu-id="ae224-163">A JSON object with a nested JSON array containing two JSON objects.</span></span> <span data-ttu-id="ae224-164">Uit deze invoer blijkt dat de algemene eigenschappen kunnen worden vertegenwoordigd door het complexe JSON-object.</span><span class="sxs-lookup"><span data-stu-id="ae224-164">This input demonstrates that the global properties may be represented by the complex JSON object.</span></span>

```json
{
    "location":"WestUs",
    "manufacturer":{
        "name":"manufacturer1",
        "location":"EastUs"
    },
    "events":[
        {
            "id":"device1",
            "timestamp":"2016-01-08T01:08:00Z",
            "data":{
                "type":"pressure",
                "units":"psi",
                "value":108.09
            }
        },
        {
            "id":"device2",
            "timestamp":"2016-01-17T01:17:00Z",
            "data":{
                "type":"vibration",
                "units":"abs G",
                "value":217.09
            }
        }
    ]
}
```
#### <a name="output---2-events"></a><span data-ttu-id="ae224-165">Uitvoer - 2 gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="ae224-165">Output - 2 Events</span></span>

|<span data-ttu-id="ae224-166">location</span><span class="sxs-lookup"><span data-stu-id="ae224-166">location</span></span>|<span data-ttu-id="ae224-167">manufacturer.name</span><span class="sxs-lookup"><span data-stu-id="ae224-167">manufacturer.name</span></span>|<span data-ttu-id="ae224-168">manufacturer.location</span><span class="sxs-lookup"><span data-stu-id="ae224-168">manufacturer.location</span></span>|<span data-ttu-id="ae224-169">events.id</span><span class="sxs-lookup"><span data-stu-id="ae224-169">events.id</span></span>|<span data-ttu-id="ae224-170">events.timestamp</span><span class="sxs-lookup"><span data-stu-id="ae224-170">events.timestamp</span></span>|<span data-ttu-id="ae224-171">events.data.type</span><span class="sxs-lookup"><span data-stu-id="ae224-171">events.data.type</span></span>|<span data-ttu-id="ae224-172">events.data.units</span><span class="sxs-lookup"><span data-stu-id="ae224-172">events.data.units</span></span>|<span data-ttu-id="ae224-173">events.data.value</span><span class="sxs-lookup"><span data-stu-id="ae224-173">events.data.value</span></span>|
|---|---|---|---|---|---|---|---|
|<span data-ttu-id="ae224-174">WestUs</span><span class="sxs-lookup"><span data-stu-id="ae224-174">WestUs</span></span>|<span data-ttu-id="ae224-175">manufacturer1</span><span class="sxs-lookup"><span data-stu-id="ae224-175">manufacturer1</span></span>|<span data-ttu-id="ae224-176">EastUs</span><span class="sxs-lookup"><span data-stu-id="ae224-176">EastUs</span></span>|<span data-ttu-id="ae224-177">device1</span><span class="sxs-lookup"><span data-stu-id="ae224-177">device1</span></span>|<span data-ttu-id="ae224-178">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="ae224-178">2016-01-08T01:08:00Z</span></span>|<span data-ttu-id="ae224-179">pressure</span><span class="sxs-lookup"><span data-stu-id="ae224-179">pressure</span></span>|<span data-ttu-id="ae224-180">psi</span><span class="sxs-lookup"><span data-stu-id="ae224-180">psi</span></span>|<span data-ttu-id="ae224-181">108.09</span><span class="sxs-lookup"><span data-stu-id="ae224-181">108.09</span></span>|
|<span data-ttu-id="ae224-182">WestUs</span><span class="sxs-lookup"><span data-stu-id="ae224-182">WestUs</span></span>|<span data-ttu-id="ae224-183">manufacturer1</span><span class="sxs-lookup"><span data-stu-id="ae224-183">manufacturer1</span></span>|<span data-ttu-id="ae224-184">EastUs</span><span class="sxs-lookup"><span data-stu-id="ae224-184">EastUs</span></span>|<span data-ttu-id="ae224-185">device2</span><span class="sxs-lookup"><span data-stu-id="ae224-185">device2</span></span>|<span data-ttu-id="ae224-186">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="ae224-186">2016-01-08T01:17:00Z</span></span>|<span data-ttu-id="ae224-187">vibration</span><span class="sxs-lookup"><span data-stu-id="ae224-187">vibration</span></span>|<span data-ttu-id="ae224-188">abs G</span><span class="sxs-lookup"><span data-stu-id="ae224-188">abs G</span></span>|<span data-ttu-id="ae224-189">217.09</span><span class="sxs-lookup"><span data-stu-id="ae224-189">217.09</span></span>|

## <a name="next-steps"></a><span data-ttu-id="ae224-190">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ae224-190">Next steps</span></span>

* <span data-ttu-id="ae224-191">Uw omgeving bekijken in de [Time Series Insights-portal](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="ae224-191">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
