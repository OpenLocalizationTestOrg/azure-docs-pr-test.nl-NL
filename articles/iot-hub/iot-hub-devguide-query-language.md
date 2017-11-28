---
title: Inzicht in de taal van de query Azure IoT Hub | Microsoft Docs
description: Handleiding voor ontwikkelaars - beschrijving van de SQL-achtige IoT Hub-querytaal gebruikt voor het ophalen van informatie over apparaat horende taken uit uw IoT-hub.
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 851a9ed3-b69e-422e-8a5d-1d79f91ddf15
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/17
ms.author: elioda
ms.openlocfilehash: a7650104eda58923558892f6f0f6666d16dbce28
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="reference---iot-hub-query-language-for-device-twins-jobs-and-message-routing"></a><span data-ttu-id="1d542-103">Referentie - querytaal IoT Hub voor apparaat horende, taken en het routeren van berichten</span><span class="sxs-lookup"><span data-stu-id="1d542-103">Reference - IoT Hub query language for device twins, jobs, and message routing</span></span>

<span data-ttu-id="1d542-104">IoT Hub biedt een krachtige SQL-achtige taal voor het ophalen van informatie met betrekking tot [apparaat horende] [ lnk-twins] en [taken][lnk-jobs], en [berichtroutering][lnk-devguide-messaging-routes].</span><span class="sxs-lookup"><span data-stu-id="1d542-104">IoT Hub provides a powerful SQL-like language to retrieve information regarding [device twins][lnk-twins] and [jobs][lnk-jobs], and [message routing][lnk-devguide-messaging-routes].</span></span> <span data-ttu-id="1d542-105">Dit artikel biedt:</span><span class="sxs-lookup"><span data-stu-id="1d542-105">This article presents:</span></span>

* <span data-ttu-id="1d542-106">Een inleiding tot de belangrijkste functies van de querytaal IoT Hub en</span><span class="sxs-lookup"><span data-stu-id="1d542-106">An introduction to the major features of the IoT Hub query language, and</span></span>
* <span data-ttu-id="1d542-107">De gedetailleerde beschrijving van de taal.</span><span class="sxs-lookup"><span data-stu-id="1d542-107">The detailed description of the language.</span></span>

## <a name="get-started-with-device-twin-queries"></a><span data-ttu-id="1d542-108">Aan de slag met apparaat twin query 's</span><span class="sxs-lookup"><span data-stu-id="1d542-108">Get started with device twin queries</span></span>
<span data-ttu-id="1d542-109">[Apparaat horende] [ lnk-twins] kan willekeurige JSON-objecten bevatten als zowel labels en eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="1d542-109">[Device twins][lnk-twins] can contain arbitrary JSON objects as both tags and properties.</span></span> <span data-ttu-id="1d542-110">IoT-Hub kunt u query apparaat horende als een enkele JSON-document met alle apparaten twin informatie.</span><span class="sxs-lookup"><span data-stu-id="1d542-110">IoT Hub enables you to query device twins as a single JSON document containing all device twin information.</span></span>
<span data-ttu-id="1d542-111">Stel bijvoorbeeld dat uw IoT hub apparaat horende de volgende structuur hebben:</span><span class="sxs-lookup"><span data-stu-id="1d542-111">Assume, for instance, that your IoT hub device twins have the following structure:</span></span>

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        "location": {
            "region": "US",
            "plant": "Redmond43"
        }
    },
    "properties": {
        "desired": {
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300
            },
            "$metadata": {
            ...
            },
            "$version": 4
        },
        "reported": {
            "connectivity": {
                "type": "cellular"
            },
            "telemetryConfig": {
                "configId": "db00ebf5-eeeb-42be-86a1-458cccb69e57",
                "sendFrequencyInSecs": 300,
                "status": "Success"
            },
            "$metadata": {
            ...
            },
            "$version": 7
        }
    }
}
```

<span data-ttu-id="1d542-112">IoT-Hub toont de horende apparaten als een documentverzameling aangeroepen **apparaten**.</span><span class="sxs-lookup"><span data-stu-id="1d542-112">IoT Hub exposes the device twins as a document collection called **devices**.</span></span>
<span data-ttu-id="1d542-113">De volgende query haalt dus de hele set horende apparaten:</span><span class="sxs-lookup"><span data-stu-id="1d542-113">So the following query retrieves the whole set of device twins:</span></span>

```sql
SELECT * FROM devices
```

> [!NOTE]
> <span data-ttu-id="1d542-114">[Azure IoT SDK's] [ lnk-hub-sdks] ondersteuning voor paginering van veel resultaten.</span><span class="sxs-lookup"><span data-stu-id="1d542-114">[Azure IoT SDKs][lnk-hub-sdks] support paging of large results.</span></span>

<span data-ttu-id="1d542-115">IoT-Hub kunt u voor het ophalen van apparaat horende filteren met willekeurig voorwaarden.</span><span class="sxs-lookup"><span data-stu-id="1d542-115">IoT Hub allows you to retrieve device twins filtering with arbitrary conditions.</span></span> <span data-ttu-id="1d542-116">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="1d542-116">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
```

<span data-ttu-id="1d542-117">haalt de horende apparaten met de **location.region** tag ingesteld op **VS**.</span><span class="sxs-lookup"><span data-stu-id="1d542-117">retrieves the device twins with the **location.region** tag set to **US**.</span></span>
<span data-ttu-id="1d542-118">Booleaanse operators en rekenkundige vergelijkingen worden ondersteund, bijvoorbeeld</span><span class="sxs-lookup"><span data-stu-id="1d542-118">Boolean operators and arithmetic comparisons are supported as well, for example</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
    AND properties.reported.telemetryConfig.sendFrequencyInSecs >= 60
```

<span data-ttu-id="1d542-119">Hiermee haalt u alle apparaten horende zich in de Verenigde Staten geconfigureerd voor het verzenden van telemetrie minder vaak elke minuut.</span><span class="sxs-lookup"><span data-stu-id="1d542-119">retrieves all device twins located in the US configured to send telemetry less often than every minute.</span></span> <span data-ttu-id="1d542-120">Voor uw gemak het is ook mogelijk om te gebruiken matrixconstanten met de **IN** en **NIN** (niet-in) operators.</span><span class="sxs-lookup"><span data-stu-id="1d542-120">As a convenience, it is also possible to use array constants with the **IN** and **NIN** (not in) operators.</span></span> <span data-ttu-id="1d542-121">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="1d542-121">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE properties.reported.connectivity IN ['wired', 'wifi']
```

<span data-ttu-id="1d542-122">alle apparaten horende die gerapporteerd Wi-Fi of bekabelde verbindingen opgehaald.</span><span class="sxs-lookup"><span data-stu-id="1d542-122">retrieves all device twins that reported WiFi or wired connectivity.</span></span> <span data-ttu-id="1d542-123">Vaak is het nodig zijn voor het identificeren van alle apparaat horende die een bepaalde eigenschap bevatten.</span><span class="sxs-lookup"><span data-stu-id="1d542-123">It is often necessary to identify all device twins that contain a specific property.</span></span> <span data-ttu-id="1d542-124">IoT Hub biedt ondersteuning voor de functie `is_defined()` voor dit doel.</span><span class="sxs-lookup"><span data-stu-id="1d542-124">IoT Hub supports the function `is_defined()` for this purpose.</span></span> <span data-ttu-id="1d542-125">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="1d542-125">For instance,</span></span>

```SQL
SELECT * FROM devices
WHERE is_defined(properties.reported.connectivity)
```

<span data-ttu-id="1d542-126">ophalen van alle apparaat horende waarmee de `connectivity` eigenschap gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="1d542-126">retrieved all device twins that define the `connectivity` reported property.</span></span> <span data-ttu-id="1d542-127">Raadpleeg de [WHERE-component] [ lnk-query-where] sectie voor de volledige verwijzing van de filtermogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="1d542-127">Refer to the [WHERE clause][lnk-query-where] section for the full reference of the filtering capabilities.</span></span>

<span data-ttu-id="1d542-128">Groepering en aggregaties worden ook ondersteund.</span><span class="sxs-lookup"><span data-stu-id="1d542-128">Grouping and aggregations are also supported.</span></span> <span data-ttu-id="1d542-129">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="1d542-129">For instance,</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="1d542-130">retourneert de telling van de apparaten in de status van elk telemetrie-configuratie.</span><span class="sxs-lookup"><span data-stu-id="1d542-130">returns the count of the devices in each telemetry configuration status.</span></span>

```json
[
    {
        "numberOfDevices": 3,
        "status": "Success"
    },
    {
        "numberOfDevices": 2,
        "status": "Pending"
    },
    {
        "numberOfDevices": 1,
        "status": "Error"
    }
]
```

<span data-ttu-id="1d542-131">Het vorige voorbeeld ziet u een situatie waarin drie apparaten gerapporteerd geslaagde configuratie, twee nog steeds toepassen van de configuratie en een heeft een fout gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="1d542-131">The preceding example illustrates a situation where three devices reported successful configuration, two are still applying the configuration, and one reported an error.</span></span>

### <a name="c-example"></a><span data-ttu-id="1d542-132">C#-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="1d542-132">C# example</span></span>
<span data-ttu-id="1d542-133">De queryfunctionaliteit die wordt blootgelegd door de [C# service SDK] [ lnk-hub-sdks] in de **RegistryManager** klasse.</span><span class="sxs-lookup"><span data-stu-id="1d542-133">The query functionality is exposed by the [C# service SDK][lnk-hub-sdks] in the **RegistryManager** class.</span></span>
<span data-ttu-id="1d542-134">Hier volgt een voorbeeld van een eenvoudige query:</span><span class="sxs-lookup"><span data-stu-id="1d542-134">Here is an example of a simple query:</span></span>

```csharp
var query = registryManager.CreateQuery("SELECT * FROM devices", 100);
while (query.HasMoreResults)
{
    var page = await query.GetNextAsTwinAsync();
    foreach (var twin in page)
    {
        // do work on twin object
    }
}
```

<span data-ttu-id="1d542-135">Opmerking hoe de **query** object is gemaakt met een paginagrootte (maximaal 1000) en vervolgens meerdere pagina's kunnen worden opgehaald door het aanroepen van de **GetNextAsTwinAsync** methoden meerdere keren.</span><span class="sxs-lookup"><span data-stu-id="1d542-135">Note how the **query** object is instantiated with a page size (up to 1000), and then multiple pages can be retrieved by calling the **GetNextAsTwinAsync** methods multiple times.</span></span>
<span data-ttu-id="1d542-136">Opmerking dat het queryobject meerdere bevat **volgende\***, afhankelijk van de deserialisatie-optie die door de query, zoals apparaatobjecten twin of de taak, of gewoon JSON vereist om te worden gebruikt als u projecties.</span><span class="sxs-lookup"><span data-stu-id="1d542-136">Note that the query object exposes multiple **Next\***, depending on the deserialization option required by the query, such as device twin or job objects, or plain JSON to be used when using projections.</span></span>

### <a name="nodejs-example"></a><span data-ttu-id="1d542-137">Node.js-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="1d542-137">Node.js example</span></span>
<span data-ttu-id="1d542-138">De queryfunctionaliteit die wordt blootgelegd door de [Azure IoT service SDK voor Node.js] [ lnk-hub-sdks] in de **register** object.</span><span class="sxs-lookup"><span data-stu-id="1d542-138">The query functionality is exposed by the [Azure IoT service SDK for Node.js][lnk-hub-sdks] in the **Registry** object.</span></span>
<span data-ttu-id="1d542-139">Hier volgt een voorbeeld van een eenvoudige query:</span><span class="sxs-lookup"><span data-stu-id="1d542-139">Here is an example of a simple query:</span></span>

```nodejs
var query = registry.createQuery('SELECT * FROM devices', 100);
var onResults = function(err, results) {
    if (err) {
        console.error('Failed to fetch the results: ' + err.message);
    } else {
        // Do something with the results
        results.forEach(function(twin) {
            console.log(twin.deviceId);
        });

        if (query.hasMoreResults) {
            query.nextAsTwin(onResults);
        }
    }
};
query.nextAsTwin(onResults);
```

<span data-ttu-id="1d542-140">Opmerking hoe de **query** object is gemaakt met een paginagrootte (maximaal 1000) en vervolgens meerdere pagina's kunnen worden opgehaald door het aanroepen van de **nextAsTwin** methoden meerdere keren.</span><span class="sxs-lookup"><span data-stu-id="1d542-140">Note how the **query** object is instantiated with a page size (up to 1000), and then multiple pages can be retrieved by calling the **nextAsTwin** methods multiple times.</span></span>
<span data-ttu-id="1d542-141">Opmerking dat het queryobject meerdere bevat **volgende\***, afhankelijk van de deserialisatie-optie die door de query, zoals apparaatobjecten twin of de taak, of gewoon JSON vereist om te worden gebruikt als u projecties.</span><span class="sxs-lookup"><span data-stu-id="1d542-141">Note that the query object exposes multiple **next\***, depending on the deserialization option required by the query, such as device twin or job objects, or plain JSON to be used when using projections.</span></span>

### <a name="limitations"></a><span data-ttu-id="1d542-142">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="1d542-142">Limitations</span></span>
> [!IMPORTANT]
> <span data-ttu-id="1d542-143">Apparaat horende queryresultaten, kunnen een paar minuten vertraging met betrekking tot de meest recente waarden bevatten.</span><span class="sxs-lookup"><span data-stu-id="1d542-143">Query results can have a few minutes of delay with respect to the latest values in device twins.</span></span> <span data-ttu-id="1d542-144">Als het uitvoeren van query's afzonderlijk apparaat horende door-id, is het altijd beter om de ophalen apparaat twin API, die altijd de meest recente waarden bevat en is beperking hoger limieten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1d542-144">If querying individual device twins by id, it is always preferable to use the retrieve device twin API, which always contains the latest values and has higher throttling limits.</span></span>

<span data-ttu-id="1d542-145">Op dit moment vergelijkingen bijvoorbeeld alleen tussen primitieve typen (geen objecten) worden ondersteund `... WHERE properties.desired.config = properties.reported.config` wordt alleen ondersteund als deze eigenschappen primitieve waarden hebben.</span><span class="sxs-lookup"><span data-stu-id="1d542-145">Currently, comparisons are supported only between primitive types (no objects), for instance `... WHERE properties.desired.config = properties.reported.config` is supported only if those properties have primitive values.</span></span>

## <a name="get-started-with-jobs-queries"></a><span data-ttu-id="1d542-146">Aan de slag met taken query 's</span><span class="sxs-lookup"><span data-stu-id="1d542-146">Get started with jobs queries</span></span>
<span data-ttu-id="1d542-147">[Taken] [ lnk-jobs] bieden een manier om het uitvoeren van bewerkingen op sets van apparaten.</span><span class="sxs-lookup"><span data-stu-id="1d542-147">[Jobs][lnk-jobs] provide a way to execute operations on sets of devices.</span></span> <span data-ttu-id="1d542-148">Elk apparaat twin bevat de informatie van de taken die het onderdeel in een verzameling met de naam is **taken**.</span><span class="sxs-lookup"><span data-stu-id="1d542-148">Each device twin contains the information of the jobs of which it is part in a collection called **jobs**.</span></span>
<span data-ttu-id="1d542-149">Logisch,</span><span class="sxs-lookup"><span data-stu-id="1d542-149">Logically,</span></span>

```json
{
    "deviceId": "myDeviceId",
    "etag": "AAAAAAAAAAc=",
    "tags": {
        ...
    },
    "properties": {
        ...
    },
    "jobs": [
        {
            "deviceId": "myDeviceId",
            "jobId": "myJobId",
            "jobType": "scheduleTwinUpdate",
            "status": "completed",
            "startTimeUtc": "2016-09-29T18:18:52.7418462",
            "endTimeUtc": "2016-09-29T18:20:52.7418462",
            "createdDateTimeUtc": "2016-09-29T18:18:56.7787107Z",
            "lastUpdatedDateTimeUtc": "2016-09-29T18:18:56.8894408Z",
            "outcome": {
                "deviceMethodResponse": null
            }
        },
        ...
    ]
}
```

<span data-ttu-id="1d542-150">Deze verzameling is momenteel als waarop **devices.jobs** querytaal van de IoT-Hub.</span><span class="sxs-lookup"><span data-stu-id="1d542-150">Currently, this collection is queryable as **devices.jobs** in the IoT Hub query language.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1d542-151">De eigenschap taken wordt op dit moment nooit geretourneerd tijdens het opvragen van apparaat horende (dat wil zeggen, query's met ' apparaten').</span><span class="sxs-lookup"><span data-stu-id="1d542-151">Currently, the jobs property is never returned when querying device twins (that is, queries that contains 'FROM devices').</span></span> <span data-ttu-id="1d542-152">Kan alleen worden benaderd rechtstreeks met query's met `FROM devices.jobs`.</span><span class="sxs-lookup"><span data-stu-id="1d542-152">It can only be accessed directly with queries using `FROM devices.jobs`.</span></span>
>
>

<span data-ttu-id="1d542-153">Bijvoorbeeld, als u alle taken (afgelopen en geplande) die invloed hebben op één apparaat, kunt u de volgende query:</span><span class="sxs-lookup"><span data-stu-id="1d542-153">For instance, to get all jobs (past and scheduled) that affect a single device, you can use the following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
```

<span data-ttu-id="1d542-154">Houd er rekening mee hoe deze query bevat de status van de apparaat-specifieke (en mogelijk het antwoord directe methode) van elke taak geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="1d542-154">Note how this query provides the device-specific status (and possibly the direct method response) of each job returned.</span></span>
<span data-ttu-id="1d542-155">Het is ook mogelijk om te filteren met willekeurig Booleaanse voorwaarden op alle eigenschappen van het object in de **devices.jobs** verzameling.</span><span class="sxs-lookup"><span data-stu-id="1d542-155">It is also possible to filter with arbitrary Boolean conditions on all object properties in the **devices.jobs** collection.</span></span>
<span data-ttu-id="1d542-156">Bijvoorbeeld de volgende query:</span><span class="sxs-lookup"><span data-stu-id="1d542-156">For instance, the following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
    AND devices.jobs.jobType = 'scheduleTwinUpdate'
    AND devices.jobs.status = 'completed'
    AND devices.jobs.createdTimeUtc > '2016-09-01'
```

<span data-ttu-id="1d542-157">haalt alle voltooid apparaat twin update taken voor apparaat **myDeviceId** die zijn gemaakt na September 2016.</span><span class="sxs-lookup"><span data-stu-id="1d542-157">retrieves all completed device twin update jobs for device **myDeviceId** that were created after September 2016.</span></span>

<span data-ttu-id="1d542-158">Het is ook mogelijk om op te halen van de resultaten per apparaat van een enkele taak.</span><span class="sxs-lookup"><span data-stu-id="1d542-158">It is also possible to retrieve the per-device outcomes of a single job.</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.jobId = 'myJobId'
```

### <a name="limitations"></a><span data-ttu-id="1d542-159">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="1d542-159">Limitations</span></span>
<span data-ttu-id="1d542-160">Op dit moment wordt een query op **devices.jobs** bieden geen ondersteuning voor:</span><span class="sxs-lookup"><span data-stu-id="1d542-160">Currently, queries on **devices.jobs** do not support:</span></span>

* <span data-ttu-id="1d542-161">Projecties, daarom alleen `SELECT *` is mogelijk.</span><span class="sxs-lookup"><span data-stu-id="1d542-161">Projections, therefore only `SELECT *` is possible.</span></span>
* <span data-ttu-id="1d542-162">De voorwaarden die naar het apparaat twin naast taakeigenschappen verwijzen (Zie de vorige sectie).</span><span class="sxs-lookup"><span data-stu-id="1d542-162">Conditions that refer to the device twin in addition to job properties (see the preceding section).</span></span>
* <span data-ttu-id="1d542-163">Uitvoeren van aggregaties, zoals count, avg, groeperen op.</span><span class="sxs-lookup"><span data-stu-id="1d542-163">Performing aggregations, such as count, avg, group by.</span></span>

## <a name="get-started-with-device-to-cloud-message-routes-query-expressions"></a><span data-ttu-id="1d542-164">Aan de slag met de apparaat-naar-cloud bericht routes query-expressies</span><span class="sxs-lookup"><span data-stu-id="1d542-164">Get started with device-to-cloud message routes query expressions</span></span>

<span data-ttu-id="1d542-165">Met behulp van [apparaat-naar-cloud routes][lnk-devguide-messaging-routes], kunt u IoT Hub apparaat-naar-cloud-berichten naar verschillende eindpunten op basis van expressies geëvalueerd op basis van afzonderlijke berichten verzenden.</span><span class="sxs-lookup"><span data-stu-id="1d542-165">Using [device-to-cloud routes][lnk-devguide-messaging-routes], you can configure IoT Hub to dispatch device-to-cloud messages to different endpoints based on expressions evaluated against individual messages.</span></span>

<span data-ttu-id="1d542-166">De route [voorwaarde] [ lnk-query-expressions] de dezelfde querytaal van IoT Hub gebruikt als voorwaarden in twin en taak query's.</span><span class="sxs-lookup"><span data-stu-id="1d542-166">The route [condition][lnk-query-expressions] uses the same IoT Hub query language as conditions in twin and job queries.</span></span> <span data-ttu-id="1d542-167">Route voorwaarden worden geëvalueerd op het berichtkoppen en de hoofdtekst.</span><span class="sxs-lookup"><span data-stu-id="1d542-167">Route conditions are evaluated on the message headers and body.</span></span> <span data-ttu-id="1d542-168">Uw routering query-expressie is mogelijk alleen berichtkoppen, alleen de hoofdtekst van het bericht of beide headers bericht en berichttekst.</span><span class="sxs-lookup"><span data-stu-id="1d542-168">Your routing query expression may involve only message headers, only the message body, or both message headers and message body.</span></span> <span data-ttu-id="1d542-169">IoT Hub wordt ervan uitgegaan dat een specifiek schema voor de kopteksten en de hoofdtekst van het bericht om te routeren van berichten en de volgende secties wordt beschreven wat is vereist voor de IoT-Hub te routeren correct:</span><span class="sxs-lookup"><span data-stu-id="1d542-169">IoT Hub assumes a specific schema for the headers and message body in order to route messages, and the following sections describe what is required for IoT Hub to properly route:</span></span>

### <a name="routing-on-message-headers"></a><span data-ttu-id="1d542-170">Routering op berichtkoppen</span><span class="sxs-lookup"><span data-stu-id="1d542-170">Routing on message headers</span></span>

<span data-ttu-id="1d542-171">IoT Hub wordt ervan uitgegaan dat de volgende JSON-weergave van berichtkoppen voor het routeren van berichten:</span><span class="sxs-lookup"><span data-stu-id="1d542-171">IoT Hub assumes the following JSON representation of message headers for message routing:</span></span>

```json
{
    "$messageId": "",
    "$enqueuedTime": "",
    "$to": "",
    "$expiryTimeUtc": "",
    "$correlationId": "",
    "$userId": "",
    "$ack": "",
    "$connectionDeviceId": "",
    "$connectionDeviceGenerationId": "",
    "$connectionAuthMethod": "",
    "$content-type": "",
    "$content-encoding": "",

    "userProperty1": "",
    "userProperty2": ""
}
```

<span data-ttu-id="1d542-172">Bericht Systeemeigenschappen worden voorafgegaan door de `'$'` symbool.</span><span class="sxs-lookup"><span data-stu-id="1d542-172">Message system properties are prefixed with the `'$'` symbol.</span></span>
<span data-ttu-id="1d542-173">Eigenschappen van de gebruiker worden altijd geopend met hun naam.</span><span class="sxs-lookup"><span data-stu-id="1d542-173">User properties are always accessed with their name.</span></span> <span data-ttu-id="1d542-174">Als de naam van een eigenschap gebeurt overeenkomen met een systeemeigenschap (zoals `$to`), de eigenschap wordt opgehaald met de `$to` expressie.</span><span class="sxs-lookup"><span data-stu-id="1d542-174">If a user property name happens to coincide with a system property (such as `$to`), the user property will be retrieved with the `$to` expression.</span></span>
<span data-ttu-id="1d542-175">U kunt altijd toegang hebt tot de systeemeigenschap met behulp van haakjes `{}`: u kunt bijvoorbeeld de expressie gebruiken `{$to}` voor toegang tot de systeemeigenschap `to`.</span><span class="sxs-lookup"><span data-stu-id="1d542-175">You can always access the system property using brackets `{}`: for instance, you can use the expression `{$to}` to access the system property `to`.</span></span> <span data-ttu-id="1d542-176">Eigenschapnamen ophalen altijd de bijbehorende systeemeigenschap.</span><span class="sxs-lookup"><span data-stu-id="1d542-176">Bracketed property names always retrieve the corresponding system property.</span></span>

<span data-ttu-id="1d542-177">Houd er rekening mee dat de namen van eigenschappen zijn niet hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="1d542-177">Remember that property names are case insensitive.</span></span>

> [!NOTE]
> <span data-ttu-id="1d542-178">Alle berichteigenschappen zijn tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="1d542-178">All message properties are strings.</span></span> <span data-ttu-id="1d542-179">Eigenschappen, zoals beschreven in de [ontwikkelaarshandleiding][lnk-devguide-messaging-format], zijn momenteel niet beschikbaar voor gebruik in query's.</span><span class="sxs-lookup"><span data-stu-id="1d542-179">System properties, as described in the [developer guide][lnk-devguide-messaging-format], are currently not available to use in queries.</span></span>
>

<span data-ttu-id="1d542-180">Als u bijvoorbeeld een `messageType` eigenschap, kunt u alle telemetrie op één eindpunt en alle waarschuwingen naar een ander eindpunt te routeren.</span><span class="sxs-lookup"><span data-stu-id="1d542-180">For example, if you use a `messageType` property, you might want to route all telemetry to one endpoint, and all alerts to another endpoint.</span></span> <span data-ttu-id="1d542-181">U kunt de volgende expressie voor het routeren van de telemetrie schrijven:</span><span class="sxs-lookup"><span data-stu-id="1d542-181">You can write the following expression to route the telemetry:</span></span>

```sql
messageType = 'telemetry'
```

<span data-ttu-id="1d542-182">En de expressie voor het routeren van de waarschuwing berichten in de volgende:</span><span class="sxs-lookup"><span data-stu-id="1d542-182">And the following expression to route the alert messages:</span></span>

```sql
messageType = 'alert'
```

<span data-ttu-id="1d542-183">Booleaanse expressies en functies worden ook ondersteund.</span><span class="sxs-lookup"><span data-stu-id="1d542-183">Boolean expressions and functions are also supported.</span></span> <span data-ttu-id="1d542-184">Deze functie kunt u bijvoorbeeld onderscheid maken tussen ernst:</span><span class="sxs-lookup"><span data-stu-id="1d542-184">This feature enables you to distinguish between severity level, for example:</span></span>

```sql
messageType = 'alerts' AND as_number(severity) <= 2
```

<span data-ttu-id="1d542-185">Raadpleeg de [expressie en voorwaarden] [ lnk-query-expressions] sectie voor een volledige lijst van ondersteunde operatoren en functies.</span><span class="sxs-lookup"><span data-stu-id="1d542-185">Refer to the [Expression and conditions][lnk-query-expressions] section for the full list of supported operators and functions.</span></span>

### <a name="routing-on-message-bodies"></a><span data-ttu-id="1d542-186">Routering op de berichttekst</span><span class="sxs-lookup"><span data-stu-id="1d542-186">Routing on message bodies</span></span>

<span data-ttu-id="1d542-187">IoT Hub kan alleen worden doorgestuurd op basis van de berichttekst inhoud als de berichttekst correct is gevormd JSON gecodeerd in UTF-8, UTF-16- of UTF-32.</span><span class="sxs-lookup"><span data-stu-id="1d542-187">IoT Hub can only route based on message body contents if the message body is properly formed JSON encoded in either UTF-8, UTF-16, or UTF-32.</span></span> <span data-ttu-id="1d542-188">U moet het inhoudstype van het bericht instellen `application/json` en de inhoudsversleuteling op een van de ondersteunde coderingen UTF in berichtkoppen om toe te staan van IoT Hub voor het routeren van het bericht op basis van de inhoud.</span><span class="sxs-lookup"><span data-stu-id="1d542-188">You must set the content type of the message to `application/json` and the content encoding to one of the supported UTF encodings in the message headers to allow IoT Hub to route the message based on the body contents.</span></span> <span data-ttu-id="1d542-189">Als een van de headers niet is opgegeven, wordt niet IoT Hub proberen om te evalueren van een queryexpressie met betrekking tot de hoofdtekst tegen het bericht.</span><span class="sxs-lookup"><span data-stu-id="1d542-189">If either of the headers is not specified, IoT Hub will not attempt to evaluate any query expression involving the body against the message.</span></span> <span data-ttu-id="1d542-190">Als uw bericht is niet een JSON-bericht, of als het bericht geeft niet het type inhoud en de codering van inhoud, kan u nog steeds berichtroutering gebruiken voor het routeren van het bericht op basis van de berichtkoppen.</span><span class="sxs-lookup"><span data-stu-id="1d542-190">If your message is not a JSON message, or if the message does not specify the content type and content encoding, you may still use message routing to route the message based on the message headers.</span></span>

<span data-ttu-id="1d542-191">U kunt `$body` in de query-expressie voor het routeren van het bericht.</span><span class="sxs-lookup"><span data-stu-id="1d542-191">You can use `$body` in the query expression to route the message.</span></span> <span data-ttu-id="1d542-192">U kunt een eenvoudige hoofdtekst-verwijzing, hoofdtekst matrixverwijzing of meerdere hoofdtekst verwijzingen in de query-expressie.</span><span class="sxs-lookup"><span data-stu-id="1d542-192">You can use a simple body reference, body array reference, or multiple body references in the query expression.</span></span> <span data-ttu-id="1d542-193">Uw query-expressie kunt ook een verwijzing instantie met een verwijzing van de header bericht combineren.</span><span class="sxs-lookup"><span data-stu-id="1d542-193">Your query expression can also combine a body reference with a message header reference.</span></span> <span data-ttu-id="1d542-194">De volgende zijn bijvoorbeeld alle geldige query-expressies:</span><span class="sxs-lookup"><span data-stu-id="1d542-194">For example, the following are all valid query expressions:</span></span>

```sql
$body.message.Weather.Location.State = 'WA'
$body.Weather.HistoricalData[0].Month = 'Feb'
$body.Weather.Temperature = 50 AND $body.message.Weather.IsEnabled
length($body.Weather.Location.State) = 2
$body.Weather.Temperature = 50 AND Status = 'Active'
```

## <a name="basics-of-an-iot-hub-query"></a><span data-ttu-id="1d542-195">Basisprincipes van een IoT Hub-query</span><span class="sxs-lookup"><span data-stu-id="1d542-195">Basics of an IoT Hub query</span></span>
<span data-ttu-id="1d542-196">Elke IoT Hub-query bevat van een geselecteerd en van clausules en door waar u optionele en GROUP BY componenten.</span><span class="sxs-lookup"><span data-stu-id="1d542-196">Every IoT Hub query consists of a SELECT and FROM clauses and by optional WHERE and GROUP BY clauses.</span></span> <span data-ttu-id="1d542-197">Elke query wordt uitgevoerd op een verzameling van JSON-documenten, bijvoorbeeld apparaat horende.</span><span class="sxs-lookup"><span data-stu-id="1d542-197">Every query is run on a collection of JSON documents, for example device twins.</span></span> <span data-ttu-id="1d542-198">De component FROM geeft aan dat de te worden herhaald op documentenverzameling (**apparaten** of **devices.jobs**).</span><span class="sxs-lookup"><span data-stu-id="1d542-198">The FROM clause indicates the document collection to be iterated on (**devices** or **devices.jobs**).</span></span> <span data-ttu-id="1d542-199">Klik wordt in de component WHERE gefilterd.</span><span class="sxs-lookup"><span data-stu-id="1d542-199">Then, the filter in the WHERE clause is applied.</span></span> <span data-ttu-id="1d542-200">Met aggregaties, worden de resultaten van deze stap gegroepeerd als opgegeven in de component GROUP BY en voor elke groep, een rij wordt gegenereerd zoals opgegeven in de component SELECT.</span><span class="sxs-lookup"><span data-stu-id="1d542-200">With aggregations, the results of this step are grouped as specified in the GROUP BY clause and, for each group, a row is generated as specified in the SELECT clause.</span></span>

```sql
SELECT <select_list>
FROM <from_specification>
[WHERE <filter_condition>]
[GROUP BY <group_specification>]
```

## <a name="from-clause"></a><span data-ttu-id="1d542-201">FROM-component</span><span class="sxs-lookup"><span data-stu-id="1d542-201">FROM clause</span></span>
<span data-ttu-id="1d542-202">De **van < from_specification >** component kunt wordt ervan uitgegaan dat slechts twee waarden: **van apparaten**, apparaat-horende query of **van devices.jobs**, query taak per apparaat meer informatie.</span><span class="sxs-lookup"><span data-stu-id="1d542-202">The **FROM <from_specification>** clause can assume only two values: **FROM devices**, to query device twins, or **FROM devices.jobs**, to query job per-device details.</span></span>

## <a name="where-clause"></a><span data-ttu-id="1d542-203">WHERE-component</span><span class="sxs-lookup"><span data-stu-id="1d542-203">WHERE clause</span></span>
<span data-ttu-id="1d542-204">De **waarbij < filter_condition >** component is optioneel.</span><span class="sxs-lookup"><span data-stu-id="1d542-204">The **WHERE <filter_condition>** clause is optional.</span></span> <span data-ttu-id="1d542-205">Hiermee geeft u een of meer voorwaarden dat de JSON-in de verzameling van documenten moeten voldoen om te worden opgenomen als onderdeel van het resultaat.</span><span class="sxs-lookup"><span data-stu-id="1d542-205">It specifies one or more conditions that the JSON documents in the FROM collection must satisfy to be included as part of the result.</span></span> <span data-ttu-id="1d542-206">De opgegeven voorwaarden op "true" moet worden opgenomen in het resultaat moet worden geëvalueerd door elk JSON-document.</span><span class="sxs-lookup"><span data-stu-id="1d542-206">Any JSON document must evaluate the specified conditions to "true" to be included in the result.</span></span>

<span data-ttu-id="1d542-207">De toegestane voorwaarden worden beschreven in de sectie [expressies en voorwaarden][lnk-query-expressions].</span><span class="sxs-lookup"><span data-stu-id="1d542-207">The allowed conditions are described in section [Expressions and conditions][lnk-query-expressions].</span></span>

## <a name="select-clause"></a><span data-ttu-id="1d542-208">SELECT-component</span><span class="sxs-lookup"><span data-stu-id="1d542-208">SELECT clause</span></span>
<span data-ttu-id="1d542-209">De component SELECT (**Selecteer < select_list >**) is verplicht en Hiermee geeft u de waarden die worden opgehaald uit de query.</span><span class="sxs-lookup"><span data-stu-id="1d542-209">The SELECT clause (**SELECT <select_list>**) is mandatory and specifies what values are retrieved from the query.</span></span> <span data-ttu-id="1d542-210">Deze geeft de JSON-waarden moeten worden gebruikt voor het genereren van de nieuwe JSON-objecten.</span><span class="sxs-lookup"><span data-stu-id="1d542-210">It specifies the JSON values to be used to generate new JSON objects.</span></span>
<span data-ttu-id="1d542-211">De Projectiefase genereert voor elk element van de gefilterde (en desgewenst gegroepeerde) subset van de verzameling van een nieuwe JSON-object gemaakt met de opgegeven waarden in de component SELECT.</span><span class="sxs-lookup"><span data-stu-id="1d542-211">For each element of the filtered (and optionally grouped) subset of the FROM collection, the projection phase generates a new JSON object, constructed with the values specified in the SELECT clause.</span></span>

<span data-ttu-id="1d542-212">Hieronder vindt u de grammatica van de component SELECT:</span><span class="sxs-lookup"><span data-stu-id="1d542-212">Following is the grammar of the SELECT clause:</span></span>

```
SELECT [TOP <max number>] <projection list>

<projection_list> ::=
    '*'
    | <projection_element> AS alias [, <projection_element> AS alias]+

<projection_element> :==
    attribute_name
    | <projection_element> '.' attribute_name
    | <aggregate>

<aggregate> :==
    count()
    | avg(<projection_element>)
    | sum(<projection_element>)
    | min(<projection_element>)
    | max(<projection_element>)
```

<span data-ttu-id="1d542-213">waar **%{attribute_name/** verwijst naar een eigenschap van het JSON-document in de verzameling FROM.</span><span class="sxs-lookup"><span data-stu-id="1d542-213">where **attribute_name** refers to any property of the JSON document in the FROM collection.</span></span> <span data-ttu-id="1d542-214">Enkele voorbeelden van SELECT-component kunnen worden gevonden in de [aan de slag met apparaat twin query's] [ lnk-query-getstarted] sectie.</span><span class="sxs-lookup"><span data-stu-id="1d542-214">Some examples of SELECT clauses can be found in the [Getting started with device twin queries][lnk-query-getstarted] section.</span></span>

<span data-ttu-id="1d542-215">Op dit moment selectie componenten anders dan **Selecteer \***  worden alleen ondersteund in cumulatieve query's in horende apparaten.</span><span class="sxs-lookup"><span data-stu-id="1d542-215">Currently, selection clauses different than **SELECT \*** are only supported in aggregate queries on device twins.</span></span>

## <a name="group-by-clause"></a><span data-ttu-id="1d542-216">GROUP BY-component</span><span class="sxs-lookup"><span data-stu-id="1d542-216">GROUP BY clause</span></span>
<span data-ttu-id="1d542-217">De **GROUP BY < group_specification >** component is een optionele stap die kan worden uitgevoerd na het opgegeven in de component WHERE, en voordat de projectie Selecteer in het opgegeven filter.</span><span class="sxs-lookup"><span data-stu-id="1d542-217">The **GROUP BY <group_specification>** clause is an optional step that can be executed after the filter specified in the WHERE clause, and before the projection specified in the SELECT.</span></span> <span data-ttu-id="1d542-218">Deze groepen documenten op basis van de waarde van een kenmerk.</span><span class="sxs-lookup"><span data-stu-id="1d542-218">It groups documents based on the value of an attribute.</span></span> <span data-ttu-id="1d542-219">Deze groepen worden gebruikt voor het genereren van geaggregeerde waarden zoals opgegeven in de component SELECT.</span><span class="sxs-lookup"><span data-stu-id="1d542-219">These groups are used to generate aggregated values as specified in the SELECT clause.</span></span>

<span data-ttu-id="1d542-220">Er is een voorbeeld van een GROUP BY-query:</span><span class="sxs-lookup"><span data-stu-id="1d542-220">An example of a query using GROUP BY is:</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="1d542-221">De formele syntaxis voor de GROUP BY is:</span><span class="sxs-lookup"><span data-stu-id="1d542-221">The formal syntax for GROUP BY is:</span></span>

```
GROUP BY <group_by_element>
<group_by_element> :==
    attribute_name
    | < group_by_element > '.' attribute_name
```

<span data-ttu-id="1d542-222">waar **%{attribute_name/** verwijst naar een eigenschap van het JSON-document in de verzameling FROM.</span><span class="sxs-lookup"><span data-stu-id="1d542-222">where **attribute_name** refers to any property of the JSON document in the FROM collection.</span></span>

<span data-ttu-id="1d542-223">De component GROUP BY wordt momenteel alleen ondersteund bij het opvragen van apparaat horende.</span><span class="sxs-lookup"><span data-stu-id="1d542-223">Currently, the GROUP BY clause is only supported when querying device twins.</span></span>

## <a name="expressions-and-conditions"></a><span data-ttu-id="1d542-224">Expressies en voorwaarden</span><span class="sxs-lookup"><span data-stu-id="1d542-224">Expressions and conditions</span></span>
<span data-ttu-id="1d542-225">Op een hoog niveau een *expressie*:</span><span class="sxs-lookup"><span data-stu-id="1d542-225">At a high level, an *expression*:</span></span>

* <span data-ttu-id="1d542-226">Resulteert in een exemplaar van een JSON-type (zoals Booleaanse waarde, getal, string, matrix of object), en</span><span class="sxs-lookup"><span data-stu-id="1d542-226">Evaluates to an instance of a JSON type (such as Boolean, number, string, array, or object), and</span></span>
* <span data-ttu-id="1d542-227">Wordt gedefinieerd door het bewerken van gegevens die afkomstig zijn van de JSON-document apparaat en de constanten die met ingebouwde operatoren en functies.</span><span class="sxs-lookup"><span data-stu-id="1d542-227">Is defined by manipulating data coming from the device JSON document and constants using built-in operators and functions.</span></span>

<span data-ttu-id="1d542-228">*Voorwaarden* expressies die in een Booleaanse waarde resulteren zijn.</span><span class="sxs-lookup"><span data-stu-id="1d542-228">*Conditions* are expressions that evaluate to a Boolean.</span></span> <span data-ttu-id="1d542-229">Een constante anders dan Booleaanse waarde **true** wordt beschouwd als **false** (inclusief **null**, **niet-gedefinieerde**, een willekeurig exemplaar object of de matrix een willekeurige tekenreeks en duidelijk de Booleaanse waarde **false**).</span><span class="sxs-lookup"><span data-stu-id="1d542-229">Any constant different than Boolean **true** is considered as **false** (including **null**, **undefined**, any object or array instance, any string, and clearly the Boolean **false**).</span></span>

<span data-ttu-id="1d542-230">De syntaxis voor expressies is:</span><span class="sxs-lookup"><span data-stu-id="1d542-230">The syntax for expressions is:</span></span>

```
<expression> ::=
    <constant> |
    attribute_name |
    <function_call> |
    <expression> binary_operator <expression> |
    <create_array_expression> |
    '(' <expression> ')'

<function_call> ::=
    <function_name> '(' expression ')'

<constant> ::=
    <undefined_constant>
    | <null_constant>
    | <number_constant>
    | <string_constant>
    | <array_constant>

<undefined_constant> ::= undefined
<null_constant> ::= null
<number_constant> ::= decimal_literal | hexadecimal_literal
<string_constant> ::= string_literal
<array_constant> ::= '[' <constant> [, <constant>]+ ']'
```

<span data-ttu-id="1d542-231">Waarbij:</span><span class="sxs-lookup"><span data-stu-id="1d542-231">where:</span></span>

| <span data-ttu-id="1d542-232">Symbool</span><span class="sxs-lookup"><span data-stu-id="1d542-232">Symbol</span></span> | <span data-ttu-id="1d542-233">Definitie</span><span class="sxs-lookup"><span data-stu-id="1d542-233">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="1d542-234">%{attribute_name/</span><span class="sxs-lookup"><span data-stu-id="1d542-234">attribute_name</span></span> | <span data-ttu-id="1d542-235">Een eigenschap van het JSON-document in de **FROM** verzameling.</span><span class="sxs-lookup"><span data-stu-id="1d542-235">Any property of the JSON document in the **FROM** collection.</span></span> |
| <span data-ttu-id="1d542-236">binary_operator</span><span class="sxs-lookup"><span data-stu-id="1d542-236">binary_operator</span></span> | <span data-ttu-id="1d542-237">Een binaire operator die worden vermeld in de [Operators](#operators) sectie.</span><span class="sxs-lookup"><span data-stu-id="1d542-237">Any binary operator listed in the [Operators](#operators) section.</span></span> |
| <span data-ttu-id="1d542-238">functie_naam</span><span class="sxs-lookup"><span data-stu-id="1d542-238">function_name</span></span>| <span data-ttu-id="1d542-239">Een functie die worden vermeld in de [functies](#functions) sectie.</span><span class="sxs-lookup"><span data-stu-id="1d542-239">Any function listed in the [Functions](#functions) section.</span></span> |
| <span data-ttu-id="1d542-240">decimal_literal</span><span class="sxs-lookup"><span data-stu-id="1d542-240">decimal_literal</span></span> |<span data-ttu-id="1d542-241">Een float uitgedrukt in decimale notatie.</span><span class="sxs-lookup"><span data-stu-id="1d542-241">A float expressed in decimal notation.</span></span> |
| <span data-ttu-id="1d542-242">hexadecimal_literal</span><span class="sxs-lookup"><span data-stu-id="1d542-242">hexadecimal_literal</span></span> |<span data-ttu-id="1d542-243">Een getal uitgedrukt in de tekenreeks '0 x' gevolgd door een reeks van hexadecimale cijfers.</span><span class="sxs-lookup"><span data-stu-id="1d542-243">A number expressed by the string ‘0x’ followed by a string of hexadecimal digits.</span></span> |
| <span data-ttu-id="1d542-244">string_literal</span><span class="sxs-lookup"><span data-stu-id="1d542-244">string_literal</span></span> |<span data-ttu-id="1d542-245">Letterlijke tekenreeks zijn vertegenwoordigd door een reeks van nul of meer Unicode-tekens of escapereeksen Unicode-tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="1d542-245">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="1d542-246">Letterlijke tekenreeks zijn ingesloten in enkele aanhalingstekens (apostrof: ') of dubbele aanhalingstekens (aanhalingsteken: ').</span><span class="sxs-lookup"><span data-stu-id="1d542-246">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span> <span data-ttu-id="1d542-247">Hiermee heft toegestaan: `\'`, `\"`, `\\`, `\uXXXX` voor Unicode-tekens die zijn gedefinieerd door 4 hexadecimale cijfers.</span><span class="sxs-lookup"><span data-stu-id="1d542-247">Allowed escapes: `\'`, `\"`, `\\`, `\uXXXX` for Unicode characters defined by 4 hexadecimal digits.</span></span> |

### <a name="operators"></a><span data-ttu-id="1d542-248">Operators</span><span class="sxs-lookup"><span data-stu-id="1d542-248">Operators</span></span>
<span data-ttu-id="1d542-249">De volgende operators worden ondersteund:</span><span class="sxs-lookup"><span data-stu-id="1d542-249">The following operators are supported:</span></span>

| <span data-ttu-id="1d542-250">Familie</span><span class="sxs-lookup"><span data-stu-id="1d542-250">Family</span></span> | <span data-ttu-id="1d542-251">Operators</span><span class="sxs-lookup"><span data-stu-id="1d542-251">Operators</span></span> |
| --- | --- |
| <span data-ttu-id="1d542-252">Rekenkundige bewerking</span><span class="sxs-lookup"><span data-stu-id="1d542-252">Arithmetic</span></span> |<span data-ttu-id="1d542-253">+,-,*,/,%</span><span class="sxs-lookup"><span data-stu-id="1d542-253">+,-,*,/,%</span></span> |
| <span data-ttu-id="1d542-254">Logische</span><span class="sxs-lookup"><span data-stu-id="1d542-254">Logical</span></span> |<span data-ttu-id="1d542-255">EN, OF NIET</span><span class="sxs-lookup"><span data-stu-id="1d542-255">AND, OR, NOT</span></span> |
| <span data-ttu-id="1d542-256">Vergelijking</span><span class="sxs-lookup"><span data-stu-id="1d542-256">Comparison</span></span> |<span data-ttu-id="1d542-257">=, !=, <, >, <=, >=, <></span><span class="sxs-lookup"><span data-stu-id="1d542-257">=, !=, <, >, <=, >=, <></span></span> |

### <a name="functions"></a><span data-ttu-id="1d542-258">Functies</span><span class="sxs-lookup"><span data-stu-id="1d542-258">Functions</span></span>
<span data-ttu-id="1d542-259">Tijdens het opvragen van horende en zijn die de enige ondersteunde is functie:</span><span class="sxs-lookup"><span data-stu-id="1d542-259">When querying twins and jobs the only supported function is:</span></span>

| <span data-ttu-id="1d542-260">Functie</span><span class="sxs-lookup"><span data-stu-id="1d542-260">Function</span></span> | <span data-ttu-id="1d542-261">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="1d542-261">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="1d542-262">IS_DEFINED(Property)</span><span class="sxs-lookup"><span data-stu-id="1d542-262">IS_DEFINED(property)</span></span> | <span data-ttu-id="1d542-263">Retourneert een Booleaanse waarde die aangeeft of de eigenschap een waarde is toegewezen (met inbegrip van `null`).</span><span class="sxs-lookup"><span data-stu-id="1d542-263">Returns a Boolean indicating if the property has been assigned a value (including `null`).</span></span> |

<span data-ttu-id="1d542-264">In situaties routes, worden de volgende wiskundige functies ondersteund:</span><span class="sxs-lookup"><span data-stu-id="1d542-264">In routes conditions, the following math functions are supported:</span></span>

| <span data-ttu-id="1d542-265">Functie</span><span class="sxs-lookup"><span data-stu-id="1d542-265">Function</span></span> | <span data-ttu-id="1d542-266">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="1d542-266">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="1d542-267">ABS(x)</span><span class="sxs-lookup"><span data-stu-id="1d542-267">ABS(x)</span></span> | <span data-ttu-id="1d542-268">Retourneert de absolute (positieve) waarde van de opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="1d542-268">Returns the absolute (positive) value of the specified numeric expression.</span></span> |
| <span data-ttu-id="1d542-269">EXP(x)</span><span class="sxs-lookup"><span data-stu-id="1d542-269">EXP(x)</span></span> | <span data-ttu-id="1d542-270">Berekent de exponentiële waarde van de opgegeven numerieke expressie (e ^ x).</span><span class="sxs-lookup"><span data-stu-id="1d542-270">Returns the exponential value of the specified numeric expression (e^x).</span></span> |
| <span data-ttu-id="1d542-271">Power(x,y)</span><span class="sxs-lookup"><span data-stu-id="1d542-271">POWER(x,y)</span></span> | <span data-ttu-id="1d542-272">Retourneert de waarde van de opgegeven expressie voor de opgegeven macht (x ^ y).</span><span class="sxs-lookup"><span data-stu-id="1d542-272">Returns the value of the specified expression to the specified power (x^y).</span></span>|
| <span data-ttu-id="1d542-273">Square(x)</span><span class="sxs-lookup"><span data-stu-id="1d542-273">SQUARE(x)</span></span> | <span data-ttu-id="1d542-274">Retourneert het kwadraat van de numerieke waarde die is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="1d542-274">Returns the square of the specified numeric value.</span></span> |
| <span data-ttu-id="1d542-275">CEILING(x)</span><span class="sxs-lookup"><span data-stu-id="1d542-275">CEILING(x)</span></span> | <span data-ttu-id="1d542-276">Retourneert de kleinste waarde van geheel getal groter dan of gelijk zijn aan de opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="1d542-276">Returns the smallest integer value greater than, or equal to, the specified numeric expression.</span></span> |
| <span data-ttu-id="1d542-277">Floor(x)</span><span class="sxs-lookup"><span data-stu-id="1d542-277">FLOOR(x)</span></span> | <span data-ttu-id="1d542-278">Retourneert het grootste gehele getal kleiner dan of gelijk zijn aan de opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="1d542-278">Returns the largest integer less than or equal to the specified numeric expression.</span></span> |
| <span data-ttu-id="1d542-279">Sign(x)</span><span class="sxs-lookup"><span data-stu-id="1d542-279">SIGN(x)</span></span> | <span data-ttu-id="1d542-280">Retourneert de positief (+ 1), nul (0) of minteken (-1) van de opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="1d542-280">Returns the positive (+1), zero (0), or negative (-1) sign of the specified numeric expression.</span></span>|
| <span data-ttu-id="1d542-281">WORTEL(x)</span><span class="sxs-lookup"><span data-stu-id="1d542-281">SQRT(x)</span></span> | <span data-ttu-id="1d542-282">Retourneert het kwadraat van de numerieke waarde die is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="1d542-282">Returns the square of the specified numeric value.</span></span> |

<span data-ttu-id="1d542-283">In situaties routes, worden het volgende type controleren en de casten functies ondersteund:</span><span class="sxs-lookup"><span data-stu-id="1d542-283">In routes conditions, the following type checking and casting functions are supported:</span></span>

| <span data-ttu-id="1d542-284">Functie</span><span class="sxs-lookup"><span data-stu-id="1d542-284">Function</span></span> | <span data-ttu-id="1d542-285">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="1d542-285">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="1d542-286">AS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="1d542-286">AS_NUMBER</span></span> | <span data-ttu-id="1d542-287">De invoerreeks converteert naar een getal.</span><span class="sxs-lookup"><span data-stu-id="1d542-287">Converts the input string to a number.</span></span> <span data-ttu-id="1d542-288">`noop`Als de invoer is een getal. `Undefined` als tekenreeks geen een getal vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="1d542-288">`noop` if input is a number; `Undefined` if string does not represent a number.</span></span>|
| <span data-ttu-id="1d542-289">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="1d542-289">IS_ARRAY</span></span> | <span data-ttu-id="1d542-290">Retourneert een Booleaanse waarde die aangeeft of het type van de opgegeven expressie een matrix is.</span><span class="sxs-lookup"><span data-stu-id="1d542-290">Returns a Boolean value indicating if the type of the specified expression is an array.</span></span> |
| <span data-ttu-id="1d542-291">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="1d542-291">IS_BOOL</span></span> | <span data-ttu-id="1d542-292">Retourneert een Booleaanse waarde die aangeeft of het type van de opgegeven expressie een Booleaanse waarde is.</span><span class="sxs-lookup"><span data-stu-id="1d542-292">Returns a Boolean value indicating if the type of the specified expression is a Boolean.</span></span> |
| <span data-ttu-id="1d542-293">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="1d542-293">IS_DEFINED</span></span> | <span data-ttu-id="1d542-294">Retourneert een Booleaanse waarde die aangeeft of de eigenschap een waarde is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="1d542-294">Returns a Boolean indicating if the property has been assigned a value.</span></span> |
| <span data-ttu-id="1d542-295">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="1d542-295">IS_NULL</span></span> | <span data-ttu-id="1d542-296">Retourneert een Booleaanse waarde die aangeeft of het type van de opgegeven expressie null is.</span><span class="sxs-lookup"><span data-stu-id="1d542-296">Returns a Boolean value indicating if the type of the specified expression is null.</span></span> |
| <span data-ttu-id="1d542-297">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="1d542-297">IS_NUMBER</span></span> | <span data-ttu-id="1d542-298">Retourneert een Booleaanse waarde die aangeeft of het type van de opgegeven expressie is van een getal.</span><span class="sxs-lookup"><span data-stu-id="1d542-298">Returns a Boolean value indicating if the type of the specified expression is a number.</span></span> |
| <span data-ttu-id="1d542-299">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="1d542-299">IS_OBJECT</span></span> | <span data-ttu-id="1d542-300">Retourneert een Booleaanse waarde die aangeeft of het type van de opgegeven expressie een JSON-object is.</span><span class="sxs-lookup"><span data-stu-id="1d542-300">Returns a Boolean value indicating if the type of the specified expression is a JSON object.</span></span> |
| <span data-ttu-id="1d542-301">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="1d542-301">IS_PRIMITIVE</span></span> | <span data-ttu-id="1d542-302">Retourneert een Booleaanse waarde die aangeeft of het type van de opgegeven expressie is van een primitief (string, Boolean, numerieke of `null`).</span><span class="sxs-lookup"><span data-stu-id="1d542-302">Returns a Boolean value indicating if the type of the specified expression is a primitive (string, Boolean, numeric or `null`).</span></span> |
| <span data-ttu-id="1d542-303">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="1d542-303">IS_STRING</span></span> | <span data-ttu-id="1d542-304">Retourneert een Booleaanse waarde die aangeeft of het type van de opgegeven expressie een tekenreeks is.</span><span class="sxs-lookup"><span data-stu-id="1d542-304">Returns a Boolean value indicating if the type of the specified expression is a string.</span></span> |

<span data-ttu-id="1d542-305">In situaties routes, worden de volgende tekenreeksfuncties ondersteund:</span><span class="sxs-lookup"><span data-stu-id="1d542-305">In routes conditions, the following string functions are supported:</span></span>

| <span data-ttu-id="1d542-306">Functie</span><span class="sxs-lookup"><span data-stu-id="1d542-306">Function</span></span> | <span data-ttu-id="1d542-307">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="1d542-307">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="1d542-308">CONCAT(x,...)</span><span class="sxs-lookup"><span data-stu-id="1d542-308">CONCAT(x, …)</span></span> | <span data-ttu-id="1d542-309">Retourneert een tekenreeks die het resultaat van het samenvoegen van twee of meer tekenreekswaarden.</span><span class="sxs-lookup"><span data-stu-id="1d542-309">Returns a string that is the result of concatenating two or more string values.</span></span> |
| <span data-ttu-id="1d542-310">LENGTH(x)</span><span class="sxs-lookup"><span data-stu-id="1d542-310">LENGTH(x)</span></span> | <span data-ttu-id="1d542-311">Retourneert het aantal tekens van de opgegeven tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="1d542-311">Returns the number of characters of the specified string expression.</span></span>|
| <span data-ttu-id="1d542-312">LOWER(x)</span><span class="sxs-lookup"><span data-stu-id="1d542-312">LOWER(x)</span></span> | <span data-ttu-id="1d542-313">Retourneert een tekenreeksexpressie na hoofdletter gegevens converteren naar kleine letters.</span><span class="sxs-lookup"><span data-stu-id="1d542-313">Returns a string expression after converting uppercase character data to lowercase.</span></span> |
| <span data-ttu-id="1d542-314">UPPER(x)</span><span class="sxs-lookup"><span data-stu-id="1d542-314">UPPER(x)</span></span> | <span data-ttu-id="1d542-315">Retourneert een tekenreeksexpressie na kleine letter gegevens converteren naar hoofdletters.</span><span class="sxs-lookup"><span data-stu-id="1d542-315">Returns a string expression after converting lowercase character data to uppercase.</span></span> |
| <span data-ttu-id="1d542-316">De SUBTEKENREEKS (tekenreeks, start [, lengte])</span><span class="sxs-lookup"><span data-stu-id="1d542-316">SUBSTRING(string, start [, length])</span></span> | <span data-ttu-id="1d542-317">Retourneert deel van een tekenreeksexpressie die beginnen bij de op nul gebaseerde positie opgegeven teken en blijft de opgegeven lengte of het einde van de tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="1d542-317">Returns part of a string expression starting at the specified character zero-based position and continues to the specified length, or to the end of the string.</span></span> |
| <span data-ttu-id="1d542-318">INDEX_OF (tekenreeks, fragment)</span><span class="sxs-lookup"><span data-stu-id="1d542-318">INDEX_OF(string, fragment)</span></span> | <span data-ttu-id="1d542-319">Retourneert de beginpositie van het eerste exemplaar van de tweede tekenreeksexpressie binnen de eerste expressie in de opgegeven tekenreeks is of -1 als de tekenreeks is niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="1d542-319">Returns the starting position of the first occurrence of the second string expression within the first specified string expression, or -1 if the string is not found.</span></span>|
| <span data-ttu-id="1d542-320">STARTS_WITH (x, y)</span><span class="sxs-lookup"><span data-stu-id="1d542-320">STARTS_WITH(x, y)</span></span> | <span data-ttu-id="1d542-321">Retourneert een Boolean die aangeeft of de eerste expressie tekenreeks begint met het tweede.</span><span class="sxs-lookup"><span data-stu-id="1d542-321">Returns a Boolean indicating whether the first string expression starts with the second.</span></span> |
| <span data-ttu-id="1d542-322">ENDS_WITH (x, y)</span><span class="sxs-lookup"><span data-stu-id="1d542-322">ENDS_WITH(x, y)</span></span> | <span data-ttu-id="1d542-323">Retourneert een Boolean die aangeeft of de eerste tekenreeksexpressie eindigt op de tweede.</span><span class="sxs-lookup"><span data-stu-id="1d542-323">Returns a Boolean indicating whether the first string expression ends with the second.</span></span> |
| <span data-ttu-id="1d542-324">CONTAINS(x,y)</span><span class="sxs-lookup"><span data-stu-id="1d542-324">CONTAINS(x,y)</span></span> | <span data-ttu-id="1d542-325">Retourneert een Boolean die aangeeft of de eerste expressie tekenreeks de tweede bevat.</span><span class="sxs-lookup"><span data-stu-id="1d542-325">Returns a Boolean indicating whether the first string expression contains the second.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1d542-326">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1d542-326">Next steps</span></span>
<span data-ttu-id="1d542-327">Meer informatie over het uitvoeren van query's in uw apps met behulp van [Azure IoT SDK's][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="1d542-327">Learn how to execute queries in your apps using [Azure IoT SDKs][lnk-hub-sdks].</span></span>

[lnk-query-where]: iot-hub-devguide-query-language.md#where-clause
[lnk-query-expressions]: iot-hub-devguide-query-language.md#expressions-and-conditions
[lnk-query-getstarted]: iot-hub-devguide-query-language.md#get-started-with-device-twin-queries

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-devguide-messaging-routes]: iot-hub-devguide-messages-read-custom.md
[lnk-devguide-messaging-format]: iot-hub-devguide-messages-construct.md
[lnk-devguide-messaging-routes]: ./iot-hub-devguide-messages-read-custom.md

[lnk-hub-sdks]: iot-hub-devguide-sdks.md
