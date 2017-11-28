---
title: aaaSend gebeurtenissen tooAzure Time Series Insights omgeving | Microsoft Docs
description: Deze zelfstudie wordt ingegaan op Hallo stappen toopush gebeurtenissen tooyour Time Series Insights omgeving
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
ms.openlocfilehash: dbccc23f61351a0033cd48c1a02fb3841b45d560
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="send-events-tooa-time-series-insights-environment-using-event-hub"></a><span data-ttu-id="f4460-103">Verzenden van gebeurtenissen tooa Time Series Insights omgeving met event hub</span><span class="sxs-lookup"><span data-stu-id="f4460-103">Send events tooa Time Series Insights environment using event hub</span></span>

<span data-ttu-id="f4460-104">Deze zelfstudie wordt uitgelegd hoe toocreate en event hub configureren en uitvoeren van een toepassing voorbeeld toopush gebeurtenissen.</span><span class="sxs-lookup"><span data-stu-id="f4460-104">This tutorial explains how toocreate and configure event hub and run a sample application toopush events.</span></span> <span data-ttu-id="f4460-105">Als u een bestaande Event Hub hebt die al gebeurtenissen in JSON-indeling bevat, kunt u deze zelfstudie overslaan en uw omgeving bekijken in [Time Series Insights](https://insights.timeseries.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f4460-105">If you have an existing event hub with events in JSON format, skip this tutorial and view your environment in [time series insights](https://insights.timeseries.azure.com).</span></span>

## <a name="configure-an-event-hub"></a><span data-ttu-id="f4460-106">Een Event Hub configureren</span><span class="sxs-lookup"><span data-stu-id="f4460-106">Configure an event hub</span></span>
1. <span data-ttu-id="f4460-107">toocreate een event hub, volg de instructies van Hallo Event Hub [documentatie](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).</span><span class="sxs-lookup"><span data-stu-id="f4460-107">toocreate an event hub, follow instructions from hello Event Hub [documentation](https://docs.microsoft.com/azure/event-hubs/event-hubs-create).</span></span>

2. <span data-ttu-id="f4460-108">Zorg ervoor dat u een consumergroep maakt die uitsluitend door uw Time Series Insights-gebeurtenisbron wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f4460-108">Make sure you create a consumer group that is used exclusively by your Time Series Insights event source.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="f4460-109">Deze consumergroep mag niet worden gebruikt door een andere service (zoals een Stream Analytics-taak of een andere Time Series Insights-omgeving).</span><span class="sxs-lookup"><span data-stu-id="f4460-109">Make sure this consumer group is not used by any other service (such as Stream Analytics job or another Time Series Insights environment).</span></span> <span data-ttu-id="f4460-110">Als consumergroep wordt gebruikt door andere services, bewerking nadelig wordt beïnvloed voor deze omgeving lees- en andere services Hallo.</span><span class="sxs-lookup"><span data-stu-id="f4460-110">If consumer group is used by other services, read operation is negatively affected for this environment and hello other services.</span></span> <span data-ttu-id="f4460-111">Als u '$Default' als consumergroep hello, kan dit ertoe leiden toopotential opnieuw kunnen worden gebruikt door andere lezers.</span><span class="sxs-lookup"><span data-stu-id="f4460-111">If you are using “$Default” as hello consumer group, it could lead toopotential reuse by other readers.</span></span>

  ![Event Hub-consumergroep selecteren](media/send-events/consumer-group.png)

3. <span data-ttu-id="f4460-113">Maak 'MySendPolicy' op Hallo event hub, dat wil gebruikte toosend gebeurtenissen in Hallo csharp voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="f4460-113">On hello event hub, create “MySendPolicy” that is used toosend events in hello csharp sample.</span></span>

  ![Een beleid voor gedeelde toegang selecteren en klikken op de knop Toevoegen](media/send-events/shared-access-policy.png)  

  ![Een nieuw beleid voor gedeelde toegang toevoegen](media/send-events/shared-access-policy-2.png)  

## <a name="create-time-series-insights-event-source"></a><span data-ttu-id="f4460-116">Een Time Series Insights-gebeurtenisbron maken</span><span class="sxs-lookup"><span data-stu-id="f4460-116">Create Time Series Insights event source</span></span>
1. <span data-ttu-id="f4460-117">Als u een gebeurtenisbron nog niet hebt gemaakt, voert u de [deze instructies](time-series-insights-add-event-source.md) toocreate een gebeurtenisbron.</span><span class="sxs-lookup"><span data-stu-id="f4460-117">If you haven't created an event source, follow [these instructions](time-series-insights-add-event-source.md) toocreate an event source.</span></span>

2. <span data-ttu-id="f4460-118">'DeviceTimestamp' opgeven als de naam van de eigenschap timestamp Hallo – deze eigenschap wordt gebruikt als Hallo werkelijke tijdstempel in Hallo csharp voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="f4460-118">Specify “deviceTimestamp” as hello timestamp property name – this property is used as hello actual timestamp in hello csharp sample.</span></span> <span data-ttu-id="f4460-119">Hallo timestamp eigenschapsnaam is hoofdlettergevoelig en waarden moeten volgen op Hallo indeling __jjjj-MM-ddTUU. FFFFFFFK__ wanneer ze worden verzonden als JSON tooevent hub.</span><span class="sxs-lookup"><span data-stu-id="f4460-119">hello timestamp property name is case-sensitive and values must follow hello format __yyyy-MM-ddTHH:mm:ss.FFFFFFFK__ when sent as JSON tooevent hub.</span></span> <span data-ttu-id="f4460-120">Als het Hallo-eigenschap bestaat niet in de gebeurtenis hello, wordt vervolgens hello gebeurtenistijd hub in de wachtrij gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f4460-120">If hello property does not exist in hello event, then hello event hub enqueued time is used.</span></span>

  ![Gebeurtenisbron maken](media/send-events/event-source-1.png)

## <a name="sample-code-toopush-events"></a><span data-ttu-id="f4460-122">Voorbeeld code toopush gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="f4460-122">Sample code toopush events</span></span>
1. <span data-ttu-id="f4460-123">Ga toohello event hub beleid 'MySendPolicy' en kopieer Hallo-verbindingsreeks met Hallo beleidssleutel.</span><span class="sxs-lookup"><span data-stu-id="f4460-123">Go toohello event hub policy “MySendPolicy” and copy hello connection string with hello policy key.</span></span>

  ![MySendPolicy-verbindingsreeks kopiëren](media/send-events/sample-code-connection-string.png)

2. <span data-ttu-id="f4460-125">Hallo na de code die gebeurtenissen toosend 600 per elk Hallo drie apparaten uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="f4460-125">Run hello following code that toosend 600 events per each of hello three devices.</span></span> <span data-ttu-id="f4460-126">Werk `eventHubConnectionString` bij met uw verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="f4460-126">Update `eventHubConnectionString` with your connection string.</span></span>

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

                // Send JSON tooevent hub.
                EventData eventData = new EventData(ms);
                eventHubClient.Send(eventData);
            }
        }
    }
}

```
## <a name="supported-json-shapes"></a><span data-ttu-id="f4460-127">Ondersteunde JSON-vormen</span><span class="sxs-lookup"><span data-stu-id="f4460-127">Supported JSON shapes</span></span>
### <a name="sample-1"></a><span data-ttu-id="f4460-128">Voorbeeld 1</span><span class="sxs-lookup"><span data-stu-id="f4460-128">Sample 1</span></span>

#### <a name="input"></a><span data-ttu-id="f4460-129">Invoer</span><span class="sxs-lookup"><span data-stu-id="f4460-129">Input</span></span>

<span data-ttu-id="f4460-130">Een eenvoudig JSON-object.</span><span class="sxs-lookup"><span data-stu-id="f4460-130">A simple JSON object.</span></span>

```json
{
    "id":"device1",
    "timestamp":"2016-01-08T01:08:00Z"
}
```
#### <a name="output---1-event"></a><span data-ttu-id="f4460-131">Uitvoer - 1 gebeurtenis</span><span class="sxs-lookup"><span data-stu-id="f4460-131">Output - 1 event</span></span>

|<span data-ttu-id="f4460-132">id</span><span class="sxs-lookup"><span data-stu-id="f4460-132">id</span></span>|<span data-ttu-id="f4460-133">tijdstempel</span><span class="sxs-lookup"><span data-stu-id="f4460-133">timestamp</span></span>|
|--------|---------------|
|<span data-ttu-id="f4460-134">device1</span><span class="sxs-lookup"><span data-stu-id="f4460-134">device1</span></span>|<span data-ttu-id="f4460-135">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="f4460-135">2016-01-08T01:08:00Z</span></span>|

### <a name="sample-2"></a><span data-ttu-id="f4460-136">Voorbeeld 2</span><span class="sxs-lookup"><span data-stu-id="f4460-136">Sample 2</span></span>

#### <a name="input"></a><span data-ttu-id="f4460-137">Invoer</span><span class="sxs-lookup"><span data-stu-id="f4460-137">Input</span></span>
<span data-ttu-id="f4460-138">Een JSON-matrix met twee JSON-objecten.</span><span class="sxs-lookup"><span data-stu-id="f4460-138">A JSON array with two JSON objects.</span></span> <span data-ttu-id="f4460-139">Elk JSON-object worden geconverteerde tooan gebeurtenis.</span><span class="sxs-lookup"><span data-stu-id="f4460-139">Each JSON object will be converted tooan event.</span></span>
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
#### <a name="output---2-events"></a><span data-ttu-id="f4460-140">Uitvoer - 2 gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="f4460-140">Output - 2 Events</span></span>

|<span data-ttu-id="f4460-141">id</span><span class="sxs-lookup"><span data-stu-id="f4460-141">id</span></span>|<span data-ttu-id="f4460-142">tijdstempel</span><span class="sxs-lookup"><span data-stu-id="f4460-142">timestamp</span></span>|
|--------|---------------|
|<span data-ttu-id="f4460-143">device1</span><span class="sxs-lookup"><span data-stu-id="f4460-143">device1</span></span>|<span data-ttu-id="f4460-144">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="f4460-144">2016-01-08T01:08:00Z</span></span>|
|<span data-ttu-id="f4460-145">device2</span><span class="sxs-lookup"><span data-stu-id="f4460-145">device2</span></span>|<span data-ttu-id="f4460-146">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="f4460-146">2016-01-08T01:17:00Z</span></span>|
### <a name="sample-3"></a><span data-ttu-id="f4460-147">Voorbeeld 3</span><span class="sxs-lookup"><span data-stu-id="f4460-147">Sample 3</span></span>

#### <a name="input"></a><span data-ttu-id="f4460-148">Invoer</span><span class="sxs-lookup"><span data-stu-id="f4460-148">Input</span></span>

<span data-ttu-id="f4460-149">Een JSON-object met een geneste JSON-matrix met twee JSON-objecten.</span><span class="sxs-lookup"><span data-stu-id="f4460-149">A JSON object with a nested JSON array containing two JSON objects.</span></span>
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
#### <a name="output---2-events"></a><span data-ttu-id="f4460-150">Uitvoer - 2 gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="f4460-150">Output - 2 Events</span></span>
<span data-ttu-id="f4460-151">Houd er rekening mee dat Hallo-eigenschap 'locatie' tooeach van Hallo gebeurtenis is gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="f4460-151">Note that hello property "location" is copied over tooeach of hello event.</span></span>

|<span data-ttu-id="f4460-152">location</span><span class="sxs-lookup"><span data-stu-id="f4460-152">location</span></span>|<span data-ttu-id="f4460-153">events.id</span><span class="sxs-lookup"><span data-stu-id="f4460-153">events.id</span></span>|<span data-ttu-id="f4460-154">events.timestamp</span><span class="sxs-lookup"><span data-stu-id="f4460-154">events.timestamp</span></span>|
|--------|---------------|----------------------|
|<span data-ttu-id="f4460-155">WestUs</span><span class="sxs-lookup"><span data-stu-id="f4460-155">WestUs</span></span>|<span data-ttu-id="f4460-156">device1</span><span class="sxs-lookup"><span data-stu-id="f4460-156">device1</span></span>|<span data-ttu-id="f4460-157">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="f4460-157">2016-01-08T01:08:00Z</span></span>|
|<span data-ttu-id="f4460-158">WestUs</span><span class="sxs-lookup"><span data-stu-id="f4460-158">WestUs</span></span>|<span data-ttu-id="f4460-159">device2</span><span class="sxs-lookup"><span data-stu-id="f4460-159">device2</span></span>|<span data-ttu-id="f4460-160">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="f4460-160">2016-01-08T01:17:00Z</span></span>|

### <a name="sample-4"></a><span data-ttu-id="f4460-161">Voorbeeld 4</span><span class="sxs-lookup"><span data-stu-id="f4460-161">Sample 4</span></span>

#### <a name="input"></a><span data-ttu-id="f4460-162">Invoer</span><span class="sxs-lookup"><span data-stu-id="f4460-162">Input</span></span>

<span data-ttu-id="f4460-163">Een JSON-object met een geneste JSON-matrix met twee JSON-objecten.</span><span class="sxs-lookup"><span data-stu-id="f4460-163">A JSON object with a nested JSON array containing two JSON objects.</span></span> <span data-ttu-id="f4460-164">Deze invoer laat zien dat Hallo algemene eigenschappen kunnen worden vertegenwoordigd door Hallo complexe JSON-object.</span><span class="sxs-lookup"><span data-stu-id="f4460-164">This input demonstrates that hello global properties may be represented by hello complex JSON object.</span></span>

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
#### <a name="output---2-events"></a><span data-ttu-id="f4460-165">Uitvoer - 2 gebeurtenissen</span><span class="sxs-lookup"><span data-stu-id="f4460-165">Output - 2 Events</span></span>

|<span data-ttu-id="f4460-166">location</span><span class="sxs-lookup"><span data-stu-id="f4460-166">location</span></span>|<span data-ttu-id="f4460-167">manufacturer.name</span><span class="sxs-lookup"><span data-stu-id="f4460-167">manufacturer.name</span></span>|<span data-ttu-id="f4460-168">manufacturer.location</span><span class="sxs-lookup"><span data-stu-id="f4460-168">manufacturer.location</span></span>|<span data-ttu-id="f4460-169">events.id</span><span class="sxs-lookup"><span data-stu-id="f4460-169">events.id</span></span>|<span data-ttu-id="f4460-170">events.timestamp</span><span class="sxs-lookup"><span data-stu-id="f4460-170">events.timestamp</span></span>|<span data-ttu-id="f4460-171">events.data.type</span><span class="sxs-lookup"><span data-stu-id="f4460-171">events.data.type</span></span>|<span data-ttu-id="f4460-172">events.data.units</span><span class="sxs-lookup"><span data-stu-id="f4460-172">events.data.units</span></span>|<span data-ttu-id="f4460-173">events.data.value</span><span class="sxs-lookup"><span data-stu-id="f4460-173">events.data.value</span></span>|
|---|---|---|---|---|---|---|---|
|<span data-ttu-id="f4460-174">WestUs</span><span class="sxs-lookup"><span data-stu-id="f4460-174">WestUs</span></span>|<span data-ttu-id="f4460-175">manufacturer1</span><span class="sxs-lookup"><span data-stu-id="f4460-175">manufacturer1</span></span>|<span data-ttu-id="f4460-176">EastUs</span><span class="sxs-lookup"><span data-stu-id="f4460-176">EastUs</span></span>|<span data-ttu-id="f4460-177">device1</span><span class="sxs-lookup"><span data-stu-id="f4460-177">device1</span></span>|<span data-ttu-id="f4460-178">2016-01-08T01:08:00Z</span><span class="sxs-lookup"><span data-stu-id="f4460-178">2016-01-08T01:08:00Z</span></span>|<span data-ttu-id="f4460-179">pressure</span><span class="sxs-lookup"><span data-stu-id="f4460-179">pressure</span></span>|<span data-ttu-id="f4460-180">psi</span><span class="sxs-lookup"><span data-stu-id="f4460-180">psi</span></span>|<span data-ttu-id="f4460-181">108.09</span><span class="sxs-lookup"><span data-stu-id="f4460-181">108.09</span></span>|
|<span data-ttu-id="f4460-182">WestUs</span><span class="sxs-lookup"><span data-stu-id="f4460-182">WestUs</span></span>|<span data-ttu-id="f4460-183">manufacturer1</span><span class="sxs-lookup"><span data-stu-id="f4460-183">manufacturer1</span></span>|<span data-ttu-id="f4460-184">EastUs</span><span class="sxs-lookup"><span data-stu-id="f4460-184">EastUs</span></span>|<span data-ttu-id="f4460-185">device2</span><span class="sxs-lookup"><span data-stu-id="f4460-185">device2</span></span>|<span data-ttu-id="f4460-186">2016-01-08T01:17:00Z</span><span class="sxs-lookup"><span data-stu-id="f4460-186">2016-01-08T01:17:00Z</span></span>|<span data-ttu-id="f4460-187">vibration</span><span class="sxs-lookup"><span data-stu-id="f4460-187">vibration</span></span>|<span data-ttu-id="f4460-188">abs G</span><span class="sxs-lookup"><span data-stu-id="f4460-188">abs G</span></span>|<span data-ttu-id="f4460-189">217.09</span><span class="sxs-lookup"><span data-stu-id="f4460-189">217.09</span></span>|

## <a name="next-steps"></a><span data-ttu-id="f4460-190">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f4460-190">Next steps</span></span>

* <span data-ttu-id="f4460-191">Uw omgeving bekijken in de [Time Series Insights-portal](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="f4460-191">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
