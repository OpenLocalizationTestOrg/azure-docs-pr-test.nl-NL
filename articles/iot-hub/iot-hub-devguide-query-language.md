---
title: aaaUnderstand hello querytaal Azure IoT Hub | Microsoft Docs
description: Handleiding voor ontwikkelaars - beschrijving van de SQL-achtige IoT Hub-querytaal Hallo gebruikt tooretrieve informatie over apparaat horende en taken van uw IoT-hub.
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
ms.openlocfilehash: 01a7c8ffdf44c6c27b834739d02c8fef1dd3d3fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-query-language-for-device-twins-jobs-and-message-routing"></a><span data-ttu-id="5fee0-103">Referentie - querytaal IoT Hub voor apparaat horende, taken en het routeren van berichten</span><span class="sxs-lookup"><span data-stu-id="5fee0-103">Reference - IoT Hub query language for device twins, jobs, and message routing</span></span>

<span data-ttu-id="5fee0-104">IoT Hub biedt een krachtige SQL-achtige taal tooretrieve informatie met betrekking tot [apparaat horende] [ lnk-twins] en [taken][lnk-jobs], en [berichtroutering][lnk-devguide-messaging-routes].</span><span class="sxs-lookup"><span data-stu-id="5fee0-104">IoT Hub provides a powerful SQL-like language tooretrieve information regarding [device twins][lnk-twins] and [jobs][lnk-jobs], and [message routing][lnk-devguide-messaging-routes].</span></span> <span data-ttu-id="5fee0-105">Dit artikel biedt:</span><span class="sxs-lookup"><span data-stu-id="5fee0-105">This article presents:</span></span>

* <span data-ttu-id="5fee0-106">Een inleiding toohello belangrijke functies van Hallo querytaal IoT Hub, en</span><span class="sxs-lookup"><span data-stu-id="5fee0-106">An introduction toohello major features of hello IoT Hub query language, and</span></span>
* <span data-ttu-id="5fee0-107">Hallo gedetailleerde omschrijving van Hallo-taal.</span><span class="sxs-lookup"><span data-stu-id="5fee0-107">hello detailed description of hello language.</span></span>

## <a name="get-started-with-device-twin-queries"></a><span data-ttu-id="5fee0-108">Aan de slag met apparaat twin query 's</span><span class="sxs-lookup"><span data-stu-id="5fee0-108">Get started with device twin queries</span></span>
<span data-ttu-id="5fee0-109">[Apparaat horende] [ lnk-twins] kan willekeurige JSON-objecten bevatten als zowel labels en eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="5fee0-109">[Device twins][lnk-twins] can contain arbitrary JSON objects as both tags and properties.</span></span> <span data-ttu-id="5fee0-110">IoT-Hub kunt u tooquery apparaat horende als een enkele JSON-document met alle apparaten twin informatie.</span><span class="sxs-lookup"><span data-stu-id="5fee0-110">IoT Hub enables you tooquery device twins as a single JSON document containing all device twin information.</span></span>
<span data-ttu-id="5fee0-111">Stel bijvoorbeeld dat uw IoT hub apparaat horende hebben Hallo structuur te volgen:</span><span class="sxs-lookup"><span data-stu-id="5fee0-111">Assume, for instance, that your IoT hub device twins have hello following structure:</span></span>

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

<span data-ttu-id="5fee0-112">IoT-Hub toont Hallo apparaat horende als een documentverzameling aangeroepen **apparaten**.</span><span class="sxs-lookup"><span data-stu-id="5fee0-112">IoT Hub exposes hello device twins as a document collection called **devices**.</span></span>
<span data-ttu-id="5fee0-113">Hallo volgende query haalt dus Hallo hele set horende apparaten:</span><span class="sxs-lookup"><span data-stu-id="5fee0-113">So hello following query retrieves hello whole set of device twins:</span></span>

```sql
SELECT * FROM devices
```

> [!NOTE]
> <span data-ttu-id="5fee0-114">[Azure IoT SDK's] [ lnk-hub-sdks] ondersteuning voor paginering van veel resultaten.</span><span class="sxs-lookup"><span data-stu-id="5fee0-114">[Azure IoT SDKs][lnk-hub-sdks] support paging of large results.</span></span>

<span data-ttu-id="5fee0-115">IoT-Hub kunt u tooretrieve apparaat horende filteren met willekeurig voorwaarden.</span><span class="sxs-lookup"><span data-stu-id="5fee0-115">IoT Hub allows you tooretrieve device twins filtering with arbitrary conditions.</span></span> <span data-ttu-id="5fee0-116">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="5fee0-116">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
```

<span data-ttu-id="5fee0-117">haalt Hallo apparaat horende Hello **location.region** tag te ingesteld**VS**.</span><span class="sxs-lookup"><span data-stu-id="5fee0-117">retrieves hello device twins with hello **location.region** tag set too**US**.</span></span>
<span data-ttu-id="5fee0-118">Booleaanse operators en rekenkundige vergelijkingen worden ondersteund, bijvoorbeeld</span><span class="sxs-lookup"><span data-stu-id="5fee0-118">Boolean operators and arithmetic comparisons are supported as well, for example</span></span>

```sql
SELECT * FROM devices
WHERE tags.location.region = 'US'
    AND properties.reported.telemetryConfig.sendFrequencyInSecs >= 60
```

<span data-ttu-id="5fee0-119">Hiermee haalt u alle apparaten horende zich in Hallo ons geconfigureerd toosend telemetrie minder vaak dan elke minuut.</span><span class="sxs-lookup"><span data-stu-id="5fee0-119">retrieves all device twins located in hello US configured toosend telemetry less often than every minute.</span></span> <span data-ttu-id="5fee0-120">Voor uw gemak is het ook mogelijk toouse matrixconstanten Hello **IN** en **NIN** (niet-in) operators.</span><span class="sxs-lookup"><span data-stu-id="5fee0-120">As a convenience, it is also possible toouse array constants with hello **IN** and **NIN** (not in) operators.</span></span> <span data-ttu-id="5fee0-121">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="5fee0-121">For instance,</span></span>

```sql
SELECT * FROM devices
WHERE properties.reported.connectivity IN ['wired', 'wifi']
```

<span data-ttu-id="5fee0-122">alle apparaten horende die gerapporteerd Wi-Fi of bekabelde verbindingen opgehaald.</span><span class="sxs-lookup"><span data-stu-id="5fee0-122">retrieves all device twins that reported WiFi or wired connectivity.</span></span> <span data-ttu-id="5fee0-123">Het is vaak nodig tooidentify alle apparaat horende die een bepaalde eigenschap bevatten.</span><span class="sxs-lookup"><span data-stu-id="5fee0-123">It is often necessary tooidentify all device twins that contain a specific property.</span></span> <span data-ttu-id="5fee0-124">IoT Hub Hallo-functie ondersteunt `is_defined()` voor dit doel.</span><span class="sxs-lookup"><span data-stu-id="5fee0-124">IoT Hub supports hello function `is_defined()` for this purpose.</span></span> <span data-ttu-id="5fee0-125">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="5fee0-125">For instance,</span></span>

```SQL
SELECT * FROM devices
WHERE is_defined(properties.reported.connectivity)
```

<span data-ttu-id="5fee0-126">alle apparaten horende waarmee Hallo opgehaald `connectivity` eigenschap gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="5fee0-126">retrieved all device twins that define hello `connectivity` reported property.</span></span> <span data-ttu-id="5fee0-127">Raadpleeg toohello [WHERE-component] [ lnk-query-where] sectie voor de volledige verwijzing Hallo Hallo filtermogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="5fee0-127">Refer toohello [WHERE clause][lnk-query-where] section for hello full reference of hello filtering capabilities.</span></span>

<span data-ttu-id="5fee0-128">Groepering en aggregaties worden ook ondersteund.</span><span class="sxs-lookup"><span data-stu-id="5fee0-128">Grouping and aggregations are also supported.</span></span> <span data-ttu-id="5fee0-129">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="5fee0-129">For instance,</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="5fee0-130">retourneert Hallo telling van Hallo apparaten in de status van elk telemetrie-configuratie.</span><span class="sxs-lookup"><span data-stu-id="5fee0-130">returns hello count of hello devices in each telemetry configuration status.</span></span>

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

<span data-ttu-id="5fee0-131">Hallo voorgaande voorbeeld ziet u een situatie waarin drie apparaten gerapporteerd geslaagde configuratie, twee Hallo configuration steeds toepast en een heeft een fout gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="5fee0-131">hello preceding example illustrates a situation where three devices reported successful configuration, two are still applying hello configuration, and one reported an error.</span></span>

### <a name="c-example"></a><span data-ttu-id="5fee0-132">C#-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="5fee0-132">C# example</span></span>
<span data-ttu-id="5fee0-133">Hallo queryfunctionaliteit die wordt blootgelegd door Hallo [C# service SDK] [ lnk-hub-sdks] in Hallo **RegistryManager** klasse.</span><span class="sxs-lookup"><span data-stu-id="5fee0-133">hello query functionality is exposed by hello [C# service SDK][lnk-hub-sdks] in hello **RegistryManager** class.</span></span>
<span data-ttu-id="5fee0-134">Hier volgt een voorbeeld van een eenvoudige query:</span><span class="sxs-lookup"><span data-stu-id="5fee0-134">Here is an example of a simple query:</span></span>

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

<span data-ttu-id="5fee0-135">Opmerking hoe Hallo **query** object is gemaakt met een paginagrootte (omhoog too1000) en vervolgens meerdere pagina's kunnen worden opgehaald door de aanroepende Hallo **GetNextAsTwinAsync** methoden meerdere keren.</span><span class="sxs-lookup"><span data-stu-id="5fee0-135">Note how hello **query** object is instantiated with a page size (up too1000), and then multiple pages can be retrieved by calling hello **GetNextAsTwinAsync** methods multiple times.</span></span>
<span data-ttu-id="5fee0-136">Opmerking die queryobject Hallo beschrijft meerdere **volgende\***, afhankelijk van Hallo deserialisatie optie vereist door de query hello, zoals twin of taak apparaatobjecten, of gewoon JSON toobe gebruikt als u projecties.</span><span class="sxs-lookup"><span data-stu-id="5fee0-136">Note that hello query object exposes multiple **Next\***, depending on hello deserialization option required by hello query, such as device twin or job objects, or plain JSON toobe used when using projections.</span></span>

### <a name="nodejs-example"></a><span data-ttu-id="5fee0-137">Node.js-voorbeeld</span><span class="sxs-lookup"><span data-stu-id="5fee0-137">Node.js example</span></span>
<span data-ttu-id="5fee0-138">Hallo queryfunctionaliteit die wordt blootgelegd door Hallo [Azure IoT service SDK voor Node.js] [ lnk-hub-sdks] in Hallo **register** object.</span><span class="sxs-lookup"><span data-stu-id="5fee0-138">hello query functionality is exposed by hello [Azure IoT service SDK for Node.js][lnk-hub-sdks] in hello **Registry** object.</span></span>
<span data-ttu-id="5fee0-139">Hier volgt een voorbeeld van een eenvoudige query:</span><span class="sxs-lookup"><span data-stu-id="5fee0-139">Here is an example of a simple query:</span></span>

```nodejs
var query = registry.createQuery('SELECT * FROM devices', 100);
var onResults = function(err, results) {
    if (err) {
        console.error('Failed toofetch hello results: ' + err.message);
    } else {
        // Do something with hello results
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

<span data-ttu-id="5fee0-140">Opmerking hoe Hallo **query** object is gemaakt met een paginagrootte (omhoog too1000) en vervolgens meerdere pagina's kunnen worden opgehaald door de aanroepende Hallo **nextAsTwin** methoden meerdere keren.</span><span class="sxs-lookup"><span data-stu-id="5fee0-140">Note how hello **query** object is instantiated with a page size (up too1000), and then multiple pages can be retrieved by calling hello **nextAsTwin** methods multiple times.</span></span>
<span data-ttu-id="5fee0-141">Opmerking die queryobject Hallo beschrijft meerdere **volgende\***, afhankelijk van Hallo deserialisatie optie vereist door de query hello, zoals twin of taak apparaatobjecten, of gewoon JSON toobe gebruikt als u projecties.</span><span class="sxs-lookup"><span data-stu-id="5fee0-141">Note that hello query object exposes multiple **next\***, depending on hello deserialization option required by hello query, such as device twin or job objects, or plain JSON toobe used when using projections.</span></span>

### <a name="limitations"></a><span data-ttu-id="5fee0-142">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="5fee0-142">Limitations</span></span>
> [!IMPORTANT]
> <span data-ttu-id="5fee0-143">Apparaat horende queryresultaten, kunnen een paar minuten vertraging met opzicht toohello meest recente waarden bevatten.</span><span class="sxs-lookup"><span data-stu-id="5fee0-143">Query results can have a few minutes of delay with respect toohello latest values in device twins.</span></span> <span data-ttu-id="5fee0-144">Als het uitvoeren van query's afzonderlijk apparaat horende door-id, het is altijd beter toouse Hallo apparaat twin API, die altijd bevat de meest recente waarden Hallo en hoger beperking limieten ophalen.</span><span class="sxs-lookup"><span data-stu-id="5fee0-144">If querying individual device twins by id, it is always preferable toouse hello retrieve device twin API, which always contains hello latest values and has higher throttling limits.</span></span>

<span data-ttu-id="5fee0-145">Op dit moment vergelijkingen bijvoorbeeld alleen tussen primitieve typen (geen objecten) worden ondersteund `... WHERE properties.desired.config = properties.reported.config` wordt alleen ondersteund als deze eigenschappen primitieve waarden hebben.</span><span class="sxs-lookup"><span data-stu-id="5fee0-145">Currently, comparisons are supported only between primitive types (no objects), for instance `... WHERE properties.desired.config = properties.reported.config` is supported only if those properties have primitive values.</span></span>

## <a name="get-started-with-jobs-queries"></a><span data-ttu-id="5fee0-146">Aan de slag met taken query 's</span><span class="sxs-lookup"><span data-stu-id="5fee0-146">Get started with jobs queries</span></span>
<span data-ttu-id="5fee0-147">[Taken] [ lnk-jobs] bieden een manier tooexecute bewerkingen op sets van apparaten.</span><span class="sxs-lookup"><span data-stu-id="5fee0-147">[Jobs][lnk-jobs] provide a way tooexecute operations on sets of devices.</span></span> <span data-ttu-id="5fee0-148">Elk apparaat twin Hallo informatie bevat van Hallo taken waarvoor onderdeel in een verzameling met de naam is **taken**.</span><span class="sxs-lookup"><span data-stu-id="5fee0-148">Each device twin contains hello information of hello jobs of which it is part in a collection called **jobs**.</span></span>
<span data-ttu-id="5fee0-149">Logisch,</span><span class="sxs-lookup"><span data-stu-id="5fee0-149">Logically,</span></span>

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

<span data-ttu-id="5fee0-150">Deze verzameling is momenteel als waarop **devices.jobs** in Hallo querytaal IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="5fee0-150">Currently, this collection is queryable as **devices.jobs** in hello IoT Hub query language.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5fee0-151">Op dit moment Hallo taken eigenschap nooit geretourneerd tijdens het opvragen van apparaat horende (dat wil zeggen, query's met ' apparaten').</span><span class="sxs-lookup"><span data-stu-id="5fee0-151">Currently, hello jobs property is never returned when querying device twins (that is, queries that contains 'FROM devices').</span></span> <span data-ttu-id="5fee0-152">Kan alleen worden benaderd rechtstreeks met query's met `FROM devices.jobs`.</span><span class="sxs-lookup"><span data-stu-id="5fee0-152">It can only be accessed directly with queries using `FROM devices.jobs`.</span></span>
>
>

<span data-ttu-id="5fee0-153">Bijvoorbeeld: tooget alle taken (afgelopen en geplande) die invloed hebben op één apparaat, kunt u Hallo query te volgen:</span><span class="sxs-lookup"><span data-stu-id="5fee0-153">For instance, tooget all jobs (past and scheduled) that affect a single device, you can use hello following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
```

<span data-ttu-id="5fee0-154">Houd er rekening mee hoe deze query bevat Hallo apparaatspecifieke status (en mogelijk Hallo directe methode antwoord) van elke taak geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="5fee0-154">Note how this query provides hello device-specific status (and possibly hello direct method response) of each job returned.</span></span>
<span data-ttu-id="5fee0-155">Het is ook mogelijk toofilter met willekeurige Booleaanse voorwaarden op alle objecteigenschappen in Hallo **devices.jobs** verzameling.</span><span class="sxs-lookup"><span data-stu-id="5fee0-155">It is also possible toofilter with arbitrary Boolean conditions on all object properties in hello **devices.jobs** collection.</span></span>
<span data-ttu-id="5fee0-156">Bijvoorbeeld: Hallo query te volgen:</span><span class="sxs-lookup"><span data-stu-id="5fee0-156">For instance, hello following query:</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.deviceId = 'myDeviceId'
    AND devices.jobs.jobType = 'scheduleTwinUpdate'
    AND devices.jobs.status = 'completed'
    AND devices.jobs.createdTimeUtc > '2016-09-01'
```

<span data-ttu-id="5fee0-157">haalt alle voltooid apparaat twin update taken voor apparaat **myDeviceId** die zijn gemaakt na September 2016.</span><span class="sxs-lookup"><span data-stu-id="5fee0-157">retrieves all completed device twin update jobs for device **myDeviceId** that were created after September 2016.</span></span>

<span data-ttu-id="5fee0-158">Het is ook mogelijk tooretrieve Hallo per apparaat resultaten van één taak.</span><span class="sxs-lookup"><span data-stu-id="5fee0-158">It is also possible tooretrieve hello per-device outcomes of a single job.</span></span>

```sql
SELECT * FROM devices.jobs
WHERE devices.jobs.jobId = 'myJobId'
```

### <a name="limitations"></a><span data-ttu-id="5fee0-159">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="5fee0-159">Limitations</span></span>
<span data-ttu-id="5fee0-160">Op dit moment wordt een query op **devices.jobs** bieden geen ondersteuning voor:</span><span class="sxs-lookup"><span data-stu-id="5fee0-160">Currently, queries on **devices.jobs** do not support:</span></span>

* <span data-ttu-id="5fee0-161">Projecties, daarom alleen `SELECT *` is mogelijk.</span><span class="sxs-lookup"><span data-stu-id="5fee0-161">Projections, therefore only `SELECT *` is possible.</span></span>
* <span data-ttu-id="5fee0-162">De voorwaarden die betrekking toohello apparaat twin in toevoeging toojob eigenschappen hebben (Zie Hallo voorgaande sectie).</span><span class="sxs-lookup"><span data-stu-id="5fee0-162">Conditions that refer toohello device twin in addition toojob properties (see hello preceding section).</span></span>
* <span data-ttu-id="5fee0-163">Uitvoeren van aggregaties, zoals count, avg, groeperen op.</span><span class="sxs-lookup"><span data-stu-id="5fee0-163">Performing aggregations, such as count, avg, group by.</span></span>

## <a name="get-started-with-device-to-cloud-message-routes-query-expressions"></a><span data-ttu-id="5fee0-164">Aan de slag met de apparaat-naar-cloud bericht routes query-expressies</span><span class="sxs-lookup"><span data-stu-id="5fee0-164">Get started with device-to-cloud message routes query expressions</span></span>

<span data-ttu-id="5fee0-165">Met behulp van [apparaat-naar-cloud routes][lnk-devguide-messaging-routes], kunt u een IoT Hub toodispatch apparaat-naar-cloud-op basis van expressies geëvalueerd op basis van afzonderlijke berichten toodifferent-eindpunten berichten configureren.</span><span class="sxs-lookup"><span data-stu-id="5fee0-165">Using [device-to-cloud routes][lnk-devguide-messaging-routes], you can configure IoT Hub toodispatch device-to-cloud messages toodifferent endpoints based on expressions evaluated against individual messages.</span></span>

<span data-ttu-id="5fee0-166">Hallo route [voorwaarde] [ lnk-query-expressions] gebruikt Hallo dezelfde IoT Hub-querytaal als voorwaarden in twin en taak query's.</span><span class="sxs-lookup"><span data-stu-id="5fee0-166">hello route [condition][lnk-query-expressions] uses hello same IoT Hub query language as conditions in twin and job queries.</span></span> <span data-ttu-id="5fee0-167">Route voorwaarden worden geëvalueerd op Hallo berichtkoppen en hoofdtekst.</span><span class="sxs-lookup"><span data-stu-id="5fee0-167">Route conditions are evaluated on hello message headers and body.</span></span> <span data-ttu-id="5fee0-168">Uw routering query-expressie is mogelijk alleen berichtkoppen alleen Hallo hoofdtekst van het bericht of beide headers bericht en berichttekst.</span><span class="sxs-lookup"><span data-stu-id="5fee0-168">Your routing query expression may involve only message headers, only hello message body, or both message headers and message body.</span></span> <span data-ttu-id="5fee0-169">IoT Hub wordt ervan uitgegaan dat een specifiek schema voor Hallo kopteksten en de berichttekst in, in volgorde tooroute berichten en Hallo volgende secties is beschreven wat er nodig is voor IoT Hub tooproperly route:</span><span class="sxs-lookup"><span data-stu-id="5fee0-169">IoT Hub assumes a specific schema for hello headers and message body in order tooroute messages, and hello following sections describe what is required for IoT Hub tooproperly route:</span></span>

### <a name="routing-on-message-headers"></a><span data-ttu-id="5fee0-170">Routering op berichtkoppen</span><span class="sxs-lookup"><span data-stu-id="5fee0-170">Routing on message headers</span></span>

<span data-ttu-id="5fee0-171">IoT Hub wordt ervan uitgegaan dat de volgende JSON-weergave van berichtkoppen voor berichtroutering Hallo:</span><span class="sxs-lookup"><span data-stu-id="5fee0-171">IoT Hub assumes hello following JSON representation of message headers for message routing:</span></span>

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

<span data-ttu-id="5fee0-172">Bericht Systeemeigenschappen worden voorafgegaan door Hallo `'$'` symbool.</span><span class="sxs-lookup"><span data-stu-id="5fee0-172">Message system properties are prefixed with hello `'$'` symbol.</span></span>
<span data-ttu-id="5fee0-173">Eigenschappen van de gebruiker worden altijd geopend met hun naam.</span><span class="sxs-lookup"><span data-stu-id="5fee0-173">User properties are always accessed with their name.</span></span> <span data-ttu-id="5fee0-174">Als de naam van een eigenschap toocoincide met een systeemeigenschap gebeurt (zoals `$to`), Hallo gebruikerseigenschap wordt opgehaald met de Hallo `$to` expressie.</span><span class="sxs-lookup"><span data-stu-id="5fee0-174">If a user property name happens toocoincide with a system property (such as `$to`), hello user property will be retrieved with hello `$to` expression.</span></span>
<span data-ttu-id="5fee0-175">U kunt altijd toegang hebt tot de eigenschap system Hallo met behulp van haakjes `{}`: u kunt bijvoorbeeld Hallo expressie gebruiken `{$to}` tooaccess Hallo systeemeigenschap `to`.</span><span class="sxs-lookup"><span data-stu-id="5fee0-175">You can always access hello system property using brackets `{}`: for instance, you can use hello expression `{$to}` tooaccess hello system property `to`.</span></span> <span data-ttu-id="5fee0-176">Eigenschapnamen ophalen altijd Hallo overeenkomstige system-eigenschap.</span><span class="sxs-lookup"><span data-stu-id="5fee0-176">Bracketed property names always retrieve hello corresponding system property.</span></span>

<span data-ttu-id="5fee0-177">Houd er rekening mee dat de namen van eigenschappen zijn niet hoofdlettergevoelig.</span><span class="sxs-lookup"><span data-stu-id="5fee0-177">Remember that property names are case insensitive.</span></span>

> [!NOTE]
> <span data-ttu-id="5fee0-178">Alle berichteigenschappen zijn tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="5fee0-178">All message properties are strings.</span></span> <span data-ttu-id="5fee0-179">Eigenschappen, zoals beschreven in Hallo [ontwikkelaarshandleiding][lnk-devguide-messaging-format], zijn momenteel niet beschikbaar toouse in query's.</span><span class="sxs-lookup"><span data-stu-id="5fee0-179">System properties, as described in hello [developer guide][lnk-devguide-messaging-format], are currently not available toouse in queries.</span></span>
>

<span data-ttu-id="5fee0-180">Als u bijvoorbeeld een `messageType` eigenschap, kunt u tooroute alle telemetrie tooone eindpunt en alle waarschuwingen tooanother eindpunt.</span><span class="sxs-lookup"><span data-stu-id="5fee0-180">For example, if you use a `messageType` property, you might want tooroute all telemetry tooone endpoint, and all alerts tooanother endpoint.</span></span> <span data-ttu-id="5fee0-181">U kunt Hallo na expressie tooroute Hallo telemetrie schrijven:</span><span class="sxs-lookup"><span data-stu-id="5fee0-181">You can write hello following expression tooroute hello telemetry:</span></span>

```sql
messageType = 'telemetry'
```

<span data-ttu-id="5fee0-182">En Hallo expressie tooroute Hallo waarschuwingsberichten te volgen:</span><span class="sxs-lookup"><span data-stu-id="5fee0-182">And hello following expression tooroute hello alert messages:</span></span>

```sql
messageType = 'alert'
```

<span data-ttu-id="5fee0-183">Booleaanse expressies en functies worden ook ondersteund.</span><span class="sxs-lookup"><span data-stu-id="5fee0-183">Boolean expressions and functions are also supported.</span></span> <span data-ttu-id="5fee0-184">Met deze functie kunt u toodistinguish tussen ernstniveau worden weergegeven, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="5fee0-184">This feature enables you toodistinguish between severity level, for example:</span></span>

```sql
messageType = 'alerts' AND as_number(severity) <= 2
```

<span data-ttu-id="5fee0-185">Raadpleeg toohello [expressie en voorwaarden] [ lnk-query-expressions] sectie voor Hallo volledige lijst van ondersteunde operatoren en functies.</span><span class="sxs-lookup"><span data-stu-id="5fee0-185">Refer toohello [Expression and conditions][lnk-query-expressions] section for hello full list of supported operators and functions.</span></span>

### <a name="routing-on-message-bodies"></a><span data-ttu-id="5fee0-186">Routering op de berichttekst</span><span class="sxs-lookup"><span data-stu-id="5fee0-186">Routing on message bodies</span></span>

<span data-ttu-id="5fee0-187">IoT Hub kan alleen worden doorgestuurd op basis van de berichttekst inhoud als de berichttekst Hallo correct is gevormd JSON gecodeerd in UTF-8, UTF-16- of UTF-32.</span><span class="sxs-lookup"><span data-stu-id="5fee0-187">IoT Hub can only route based on message body contents if hello message body is properly formed JSON encoded in either UTF-8, UTF-16, or UTF-32.</span></span> <span data-ttu-id="5fee0-188">U moet Hallo-inhoudstype van het Hallo-bericht te instellen`application/json` en Hallo inhoud codering tooone Hallo UTF-coderingen in Hallo-bericht headers tooallow Hallo-bericht van IoT Hub tooroute op basis van de inhoud van Hallo ondersteund.</span><span class="sxs-lookup"><span data-stu-id="5fee0-188">You must set hello content type of hello message too`application/json` and hello content encoding tooone of hello supported UTF encodings in hello message headers tooallow IoT Hub tooroute hello message based on hello body contents.</span></span> <span data-ttu-id="5fee0-189">Als een Hallo headers niet is opgegeven, wordt IoT-Hub niet geprobeerd tooevaluate een query-expressie met betrekking tot Hallo hoofdtekst tegen het Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="5fee0-189">If either of hello headers is not specified, IoT Hub will not attempt tooevaluate any query expression involving hello body against hello message.</span></span> <span data-ttu-id="5fee0-190">Als uw bericht is niet een JSON-bericht, of als het Hallo-bericht geeft geen Hallo inhoudstype en codering van inhoud, mag u nog steeds berichtroutering tooroute op basis van berichtkoppen Hallo Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="5fee0-190">If your message is not a JSON message, or if hello message does not specify hello content type and content encoding, you may still use message routing tooroute hello message based on hello message headers.</span></span>

<span data-ttu-id="5fee0-191">U kunt `$body` in Hallo query-expressie tooroute Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="5fee0-191">You can use `$body` in hello query expression tooroute hello message.</span></span> <span data-ttu-id="5fee0-192">Kunt u de verwijzing naar een eenvoudige hoofdtekst, hoofdtekst matrixverwijzing of meerdere hoofdtekst verwijzingen in Hallo query-expressie.</span><span class="sxs-lookup"><span data-stu-id="5fee0-192">You can use a simple body reference, body array reference, or multiple body references in hello query expression.</span></span> <span data-ttu-id="5fee0-193">Uw query-expressie kunt ook een verwijzing instantie met een verwijzing van de header bericht combineren.</span><span class="sxs-lookup"><span data-stu-id="5fee0-193">Your query expression can also combine a body reference with a message header reference.</span></span> <span data-ttu-id="5fee0-194">Hallo hieronder vindt u bijvoorbeeld alle geldige query-expressies:</span><span class="sxs-lookup"><span data-stu-id="5fee0-194">For example, hello following are all valid query expressions:</span></span>

```sql
$body.message.Weather.Location.State = 'WA'
$body.Weather.HistoricalData[0].Month = 'Feb'
$body.Weather.Temperature = 50 AND $body.message.Weather.IsEnabled
length($body.Weather.Location.State) = 2
$body.Weather.Temperature = 50 AND Status = 'Active'
```

## <a name="basics-of-an-iot-hub-query"></a><span data-ttu-id="5fee0-195">Basisprincipes van een IoT Hub-query</span><span class="sxs-lookup"><span data-stu-id="5fee0-195">Basics of an IoT Hub query</span></span>
<span data-ttu-id="5fee0-196">Elke IoT Hub-query bevat van een geselecteerd en van clausules en door waar u optionele en GROUP BY componenten.</span><span class="sxs-lookup"><span data-stu-id="5fee0-196">Every IoT Hub query consists of a SELECT and FROM clauses and by optional WHERE and GROUP BY clauses.</span></span> <span data-ttu-id="5fee0-197">Elke query wordt uitgevoerd op een verzameling van JSON-documenten, bijvoorbeeld apparaat horende.</span><span class="sxs-lookup"><span data-stu-id="5fee0-197">Every query is run on a collection of JSON documents, for example device twins.</span></span> <span data-ttu-id="5fee0-198">Hallo FROM-component geeft Hallo document verzameling toobe herhaald op (**apparaten** of **devices.jobs**).</span><span class="sxs-lookup"><span data-stu-id="5fee0-198">hello FROM clause indicates hello document collection toobe iterated on (**devices** or **devices.jobs**).</span></span> <span data-ttu-id="5fee0-199">Vervolgens Hallo-filter in Hallo waarin component is toegepast.</span><span class="sxs-lookup"><span data-stu-id="5fee0-199">Then, hello filter in hello WHERE clause is applied.</span></span> <span data-ttu-id="5fee0-200">Met aggregaties, Hallo resultaten van deze stap worden gegroepeerd als opgegeven in de Hallo GROUP BY-component en voor elke groep een rij wordt gegenereerd zoals opgegeven in Hallo SELECT-component.</span><span class="sxs-lookup"><span data-stu-id="5fee0-200">With aggregations, hello results of this step are grouped as specified in hello GROUP BY clause and, for each group, a row is generated as specified in hello SELECT clause.</span></span>

```sql
SELECT <select_list>
FROM <from_specification>
[WHERE <filter_condition>]
[GROUP BY <group_specification>]
```

## <a name="from-clause"></a><span data-ttu-id="5fee0-201">FROM-component</span><span class="sxs-lookup"><span data-stu-id="5fee0-201">FROM clause</span></span>
<span data-ttu-id="5fee0-202">Hallo **van < from_specification >** component kunt wordt ervan uitgegaan dat slechts twee waarden: **van apparaten**, tooquery apparaat horende, of **van devices.jobs**, tooquery taak per-apparaat meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5fee0-202">hello **FROM <from_specification>** clause can assume only two values: **FROM devices**, tooquery device twins, or **FROM devices.jobs**, tooquery job per-device details.</span></span>

## <a name="where-clause"></a><span data-ttu-id="5fee0-203">WHERE-component</span><span class="sxs-lookup"><span data-stu-id="5fee0-203">WHERE clause</span></span>
<span data-ttu-id="5fee0-204">Hallo **waarbij < filter_condition >** component is optioneel.</span><span class="sxs-lookup"><span data-stu-id="5fee0-204">hello **WHERE <filter_condition>** clause is optional.</span></span> <span data-ttu-id="5fee0-205">Hiermee wordt een of meer voorwaarden dat Hallo JSON-documenten in hello FROM verzameling moeten voldoen aan de toobe opgenomen als onderdeel van Hallo resultaat.</span><span class="sxs-lookup"><span data-stu-id="5fee0-205">It specifies one or more conditions that hello JSON documents in hello FROM collection must satisfy toobe included as part of hello result.</span></span> <span data-ttu-id="5fee0-206">Elk JSON-document moet worden geëvalueerd Hallo opgegeven voorwaarden te 'true' toobe in Hallo resultaat opgenomen.</span><span class="sxs-lookup"><span data-stu-id="5fee0-206">Any JSON document must evaluate hello specified conditions too"true" toobe included in hello result.</span></span>

<span data-ttu-id="5fee0-207">Hallo toegestaan voorwaarden worden beschreven in de sectie [expressies en voorwaarden][lnk-query-expressions].</span><span class="sxs-lookup"><span data-stu-id="5fee0-207">hello allowed conditions are described in section [Expressions and conditions][lnk-query-expressions].</span></span>

## <a name="select-clause"></a><span data-ttu-id="5fee0-208">SELECT-component</span><span class="sxs-lookup"><span data-stu-id="5fee0-208">SELECT clause</span></span>
<span data-ttu-id="5fee0-209">Hallo SELECT-component (**Selecteer < select_list >**) is verplicht en Hiermee geeft u de waarden die worden opgehaald uit het Hallo-query.</span><span class="sxs-lookup"><span data-stu-id="5fee0-209">hello SELECT clause (**SELECT <select_list>**) is mandatory and specifies what values are retrieved from hello query.</span></span> <span data-ttu-id="5fee0-210">Hiermee geeft u Hallo JSON waarden toobe toogenerate nieuwe JSON-objecten gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5fee0-210">It specifies hello JSON values toobe used toogenerate new JSON objects.</span></span>
<span data-ttu-id="5fee0-211">Voor elk element van gefilterde (en desgewenst gegroepeerde) subset van hello FROM verzameling Hallo, Hallo Projectiefase wordt een nieuwe JSON-object worden geconstrueerd met Hallo opgegeven waarden in de SELECT-component Hallo gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="5fee0-211">For each element of hello filtered (and optionally grouped) subset of hello FROM collection, hello projection phase generates a new JSON object, constructed with hello values specified in hello SELECT clause.</span></span>

<span data-ttu-id="5fee0-212">Hieronder vindt u Hallo grammatica van Hallo SELECT-component:</span><span class="sxs-lookup"><span data-stu-id="5fee0-212">Following is hello grammar of hello SELECT clause:</span></span>

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

<span data-ttu-id="5fee0-213">waar **%{attribute_name/** tooany-eigenschap van Hallo JSON-document in hello FROM verzameling verwijst.</span><span class="sxs-lookup"><span data-stu-id="5fee0-213">where **attribute_name** refers tooany property of hello JSON document in hello FROM collection.</span></span> <span data-ttu-id="5fee0-214">Enkele voorbeelden van SELECT-component kunnen worden gevonden in Hallo [aan de slag met apparaat twin query's] [ lnk-query-getstarted] sectie.</span><span class="sxs-lookup"><span data-stu-id="5fee0-214">Some examples of SELECT clauses can be found in hello [Getting started with device twin queries][lnk-query-getstarted] section.</span></span>

<span data-ttu-id="5fee0-215">Op dit moment selectie componenten anders dan **Selecteer \***  worden alleen ondersteund in cumulatieve query's in horende apparaten.</span><span class="sxs-lookup"><span data-stu-id="5fee0-215">Currently, selection clauses different than **SELECT \*** are only supported in aggregate queries on device twins.</span></span>

## <a name="group-by-clause"></a><span data-ttu-id="5fee0-216">GROUP BY-component</span><span class="sxs-lookup"><span data-stu-id="5fee0-216">GROUP BY clause</span></span>
<span data-ttu-id="5fee0-217">Hallo **GROUP BY < group_specification >** component is een optionele stap die kan worden uitgevoerd nadat de WHERE-component in Hallo Hallo-filter opgegeven en voordat Hallo projectie opgegeven in Hallo selecteren.</span><span class="sxs-lookup"><span data-stu-id="5fee0-217">hello **GROUP BY <group_specification>** clause is an optional step that can be executed after hello filter specified in hello WHERE clause, and before hello projection specified in hello SELECT.</span></span> <span data-ttu-id="5fee0-218">Deze documenten op basis van de waarde van een kenmerk Hallo gegroepeerd.</span><span class="sxs-lookup"><span data-stu-id="5fee0-218">It groups documents based on hello value of an attribute.</span></span> <span data-ttu-id="5fee0-219">Deze groepen zijn gebruikte toogenerate geaggregeerd waarden zoals opgegeven in de SELECT-component Hallo.</span><span class="sxs-lookup"><span data-stu-id="5fee0-219">These groups are used toogenerate aggregated values as specified in hello SELECT clause.</span></span>

<span data-ttu-id="5fee0-220">Er is een voorbeeld van een GROUP BY-query:</span><span class="sxs-lookup"><span data-stu-id="5fee0-220">An example of a query using GROUP BY is:</span></span>

```sql
SELECT properties.reported.telemetryConfig.status AS status,
    COUNT() AS numberOfDevices
FROM devices
GROUP BY properties.reported.telemetryConfig.status
```

<span data-ttu-id="5fee0-221">Hallo formele syntaxis voor GROUP BY is:</span><span class="sxs-lookup"><span data-stu-id="5fee0-221">hello formal syntax for GROUP BY is:</span></span>

```
GROUP BY <group_by_element>
<group_by_element> :==
    attribute_name
    | < group_by_element > '.' attribute_name
```

<span data-ttu-id="5fee0-222">waar **%{attribute_name/** tooany-eigenschap van Hallo JSON-document in hello FROM verzameling verwijst.</span><span class="sxs-lookup"><span data-stu-id="5fee0-222">where **attribute_name** refers tooany property of hello JSON document in hello FROM collection.</span></span>

<span data-ttu-id="5fee0-223">Op dit moment wordt Hallo GROUP BY-component alleen ondersteund bij het opvragen van horende apparaten.</span><span class="sxs-lookup"><span data-stu-id="5fee0-223">Currently, hello GROUP BY clause is only supported when querying device twins.</span></span>

## <a name="expressions-and-conditions"></a><span data-ttu-id="5fee0-224">Expressies en voorwaarden</span><span class="sxs-lookup"><span data-stu-id="5fee0-224">Expressions and conditions</span></span>
<span data-ttu-id="5fee0-225">Op een hoog niveau een *expressie*:</span><span class="sxs-lookup"><span data-stu-id="5fee0-225">At a high level, an *expression*:</span></span>

* <span data-ttu-id="5fee0-226">Evalueert tooan exemplaar van een JSON-type (zoals Booleaanse waarde, getal, string, matrix of object), en</span><span class="sxs-lookup"><span data-stu-id="5fee0-226">Evaluates tooan instance of a JSON type (such as Boolean, number, string, array, or object), and</span></span>
* <span data-ttu-id="5fee0-227">Wordt gedefinieerd door het bewerken van gegevens die afkomstig zijn van Hallo apparaat JSON-document en constanten met ingebouwde operatoren en functies.</span><span class="sxs-lookup"><span data-stu-id="5fee0-227">Is defined by manipulating data coming from hello device JSON document and constants using built-in operators and functions.</span></span>

<span data-ttu-id="5fee0-228">*Voorwaarden* expressies die tooa Booleaanse waarde evalueren zijn.</span><span class="sxs-lookup"><span data-stu-id="5fee0-228">*Conditions* are expressions that evaluate tooa Boolean.</span></span> <span data-ttu-id="5fee0-229">Een constante anders dan Booleaanse waarde **true** wordt beschouwd als **false** (inclusief **null**, **niet-gedefinieerde**, een willekeurig exemplaar object of de matrix elke tekenreeks en duidelijk Hallo Booleaanse waarde **false**).</span><span class="sxs-lookup"><span data-stu-id="5fee0-229">Any constant different than Boolean **true** is considered as **false** (including **null**, **undefined**, any object or array instance, any string, and clearly hello Boolean **false**).</span></span>

<span data-ttu-id="5fee0-230">Hallo-syntaxis voor expressies is:</span><span class="sxs-lookup"><span data-stu-id="5fee0-230">hello syntax for expressions is:</span></span>

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

<span data-ttu-id="5fee0-231">Waarbij:</span><span class="sxs-lookup"><span data-stu-id="5fee0-231">where:</span></span>

| <span data-ttu-id="5fee0-232">Symbool</span><span class="sxs-lookup"><span data-stu-id="5fee0-232">Symbol</span></span> | <span data-ttu-id="5fee0-233">Definitie</span><span class="sxs-lookup"><span data-stu-id="5fee0-233">Definition</span></span> |
| --- | --- |
| <span data-ttu-id="5fee0-234">%{attribute_name/</span><span class="sxs-lookup"><span data-stu-id="5fee0-234">attribute_name</span></span> | <span data-ttu-id="5fee0-235">Een eigenschap van JSON-document in Hallo Hallo **FROM** verzameling.</span><span class="sxs-lookup"><span data-stu-id="5fee0-235">Any property of hello JSON document in hello **FROM** collection.</span></span> |
| <span data-ttu-id="5fee0-236">binary_operator</span><span class="sxs-lookup"><span data-stu-id="5fee0-236">binary_operator</span></span> | <span data-ttu-id="5fee0-237">Een binaire operator die worden vermeld in Hallo [Operators](#operators) sectie.</span><span class="sxs-lookup"><span data-stu-id="5fee0-237">Any binary operator listed in hello [Operators](#operators) section.</span></span> |
| <span data-ttu-id="5fee0-238">functie_naam</span><span class="sxs-lookup"><span data-stu-id="5fee0-238">function_name</span></span>| <span data-ttu-id="5fee0-239">Een functie die worden vermeld in Hallo [functies](#functions) sectie.</span><span class="sxs-lookup"><span data-stu-id="5fee0-239">Any function listed in hello [Functions](#functions) section.</span></span> |
| <span data-ttu-id="5fee0-240">decimal_literal</span><span class="sxs-lookup"><span data-stu-id="5fee0-240">decimal_literal</span></span> |<span data-ttu-id="5fee0-241">Een float uitgedrukt in decimale notatie.</span><span class="sxs-lookup"><span data-stu-id="5fee0-241">A float expressed in decimal notation.</span></span> |
| <span data-ttu-id="5fee0-242">hexadecimal_literal</span><span class="sxs-lookup"><span data-stu-id="5fee0-242">hexadecimal_literal</span></span> |<span data-ttu-id="5fee0-243">Een getal, uitgedrukt door Hallo tekenreeks '0 x' gevolgd door een reeks van hexadecimale cijfers.</span><span class="sxs-lookup"><span data-stu-id="5fee0-243">A number expressed by hello string ‘0x’ followed by a string of hexadecimal digits.</span></span> |
| <span data-ttu-id="5fee0-244">string_literal</span><span class="sxs-lookup"><span data-stu-id="5fee0-244">string_literal</span></span> |<span data-ttu-id="5fee0-245">Letterlijke tekenreeks zijn vertegenwoordigd door een reeks van nul of meer Unicode-tekens of escapereeksen Unicode-tekenreeksen.</span><span class="sxs-lookup"><span data-stu-id="5fee0-245">String literals are Unicode strings represented by a sequence of zero or more Unicode characters or escape sequences.</span></span> <span data-ttu-id="5fee0-246">Letterlijke tekenreeks zijn ingesloten in enkele aanhalingstekens (apostrof: ') of dubbele aanhalingstekens (aanhalingsteken: ').</span><span class="sxs-lookup"><span data-stu-id="5fee0-246">String literals are enclosed in single quotes (apostrophe: ' ) or double quotes (quotation mark: ").</span></span> <span data-ttu-id="5fee0-247">Hiermee heft toegestaan: `\'`, `\"`, `\\`, `\uXXXX` voor Unicode-tekens die zijn gedefinieerd door 4 hexadecimale cijfers.</span><span class="sxs-lookup"><span data-stu-id="5fee0-247">Allowed escapes: `\'`, `\"`, `\\`, `\uXXXX` for Unicode characters defined by 4 hexadecimal digits.</span></span> |

### <a name="operators"></a><span data-ttu-id="5fee0-248">Operators</span><span class="sxs-lookup"><span data-stu-id="5fee0-248">Operators</span></span>
<span data-ttu-id="5fee0-249">Hallo operators volgende worden ondersteund:</span><span class="sxs-lookup"><span data-stu-id="5fee0-249">hello following operators are supported:</span></span>

| <span data-ttu-id="5fee0-250">Familie</span><span class="sxs-lookup"><span data-stu-id="5fee0-250">Family</span></span> | <span data-ttu-id="5fee0-251">Operators</span><span class="sxs-lookup"><span data-stu-id="5fee0-251">Operators</span></span> |
| --- | --- |
| <span data-ttu-id="5fee0-252">Rekenkundige bewerking</span><span class="sxs-lookup"><span data-stu-id="5fee0-252">Arithmetic</span></span> |<span data-ttu-id="5fee0-253">+,-,*,/,%</span><span class="sxs-lookup"><span data-stu-id="5fee0-253">+,-,*,/,%</span></span> |
| <span data-ttu-id="5fee0-254">Logische</span><span class="sxs-lookup"><span data-stu-id="5fee0-254">Logical</span></span> |<span data-ttu-id="5fee0-255">EN, OF NIET</span><span class="sxs-lookup"><span data-stu-id="5fee0-255">AND, OR, NOT</span></span> |
| <span data-ttu-id="5fee0-256">Vergelijking</span><span class="sxs-lookup"><span data-stu-id="5fee0-256">Comparison</span></span> |<span data-ttu-id="5fee0-257">=, !=, <, >, <=, >=, <></span><span class="sxs-lookup"><span data-stu-id="5fee0-257">=, !=, <, >, <=, >=, <></span></span> |

### <a name="functions"></a><span data-ttu-id="5fee0-258">Functies</span><span class="sxs-lookup"><span data-stu-id="5fee0-258">Functions</span></span>
<span data-ttu-id="5fee0-259">Tijdens het opvragen van horende en taken Hallo alleen ondersteund is functie:</span><span class="sxs-lookup"><span data-stu-id="5fee0-259">When querying twins and jobs hello only supported function is:</span></span>

| <span data-ttu-id="5fee0-260">Functie</span><span class="sxs-lookup"><span data-stu-id="5fee0-260">Function</span></span> | <span data-ttu-id="5fee0-261">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="5fee0-261">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="5fee0-262">IS_DEFINED(Property)</span><span class="sxs-lookup"><span data-stu-id="5fee0-262">IS_DEFINED(property)</span></span> | <span data-ttu-id="5fee0-263">Retourneert een Booleaanse waarde waarmee wordt aangegeven als Hallo eigenschap een waarde is toegewezen (met inbegrip van `null`).</span><span class="sxs-lookup"><span data-stu-id="5fee0-263">Returns a Boolean indicating if hello property has been assigned a value (including `null`).</span></span> |

<span data-ttu-id="5fee0-264">Routes voorwaarden worden Hallo na wiskundige functies ondersteund:</span><span class="sxs-lookup"><span data-stu-id="5fee0-264">In routes conditions, hello following math functions are supported:</span></span>

| <span data-ttu-id="5fee0-265">Functie</span><span class="sxs-lookup"><span data-stu-id="5fee0-265">Function</span></span> | <span data-ttu-id="5fee0-266">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="5fee0-266">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="5fee0-267">ABS(x)</span><span class="sxs-lookup"><span data-stu-id="5fee0-267">ABS(x)</span></span> | <span data-ttu-id="5fee0-268">Retourneert Hallo absolute (positieve) waarde Hallo opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="5fee0-268">Returns hello absolute (positive) value of hello specified numeric expression.</span></span> |
| <span data-ttu-id="5fee0-269">EXP(x)</span><span class="sxs-lookup"><span data-stu-id="5fee0-269">EXP(x)</span></span> | <span data-ttu-id="5fee0-270">Retourneert Hallo exponentiële waarde Hallo opgegeven numerieke expressie (e ^ x).</span><span class="sxs-lookup"><span data-stu-id="5fee0-270">Returns hello exponential value of hello specified numeric expression (e^x).</span></span> |
| <span data-ttu-id="5fee0-271">Power(x,y)</span><span class="sxs-lookup"><span data-stu-id="5fee0-271">POWER(x,y)</span></span> | <span data-ttu-id="5fee0-272">Retourneert de waarde van de opgegeven Hallo Hallo expressie toohello opgegeven power (x ^ y).</span><span class="sxs-lookup"><span data-stu-id="5fee0-272">Returns hello value of hello specified expression toohello specified power (x^y).</span></span>|
| <span data-ttu-id="5fee0-273">Square(x)</span><span class="sxs-lookup"><span data-stu-id="5fee0-273">SQUARE(x)</span></span> | <span data-ttu-id="5fee0-274">Retourneert Hallo vierkante Hallo opgegeven numerieke waarde.</span><span class="sxs-lookup"><span data-stu-id="5fee0-274">Returns hello square of hello specified numeric value.</span></span> |
| <span data-ttu-id="5fee0-275">CEILING(x)</span><span class="sxs-lookup"><span data-stu-id="5fee0-275">CEILING(x)</span></span> | <span data-ttu-id="5fee0-276">Retourneert Hallo kleinste geheel getal groter dan of gelijk zijn aan om Hallo opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="5fee0-276">Returns hello smallest integer value greater than, or equal to, hello specified numeric expression.</span></span> |
| <span data-ttu-id="5fee0-277">Floor(x)</span><span class="sxs-lookup"><span data-stu-id="5fee0-277">FLOOR(x)</span></span> | <span data-ttu-id="5fee0-278">Retourneert de grootste integer Hallo kleiner dan of gelijk toohello numerieke expressie opgegeven.</span><span class="sxs-lookup"><span data-stu-id="5fee0-278">Returns hello largest integer less than or equal toohello specified numeric expression.</span></span> |
| <span data-ttu-id="5fee0-279">Sign(x)</span><span class="sxs-lookup"><span data-stu-id="5fee0-279">SIGN(x)</span></span> | <span data-ttu-id="5fee0-280">Retourneert Hallo positieve (+ 1), nul (0) of minteken (-1) Hallo opgegeven numerieke expressie.</span><span class="sxs-lookup"><span data-stu-id="5fee0-280">Returns hello positive (+1), zero (0), or negative (-1) sign of hello specified numeric expression.</span></span>|
| <span data-ttu-id="5fee0-281">WORTEL(x)</span><span class="sxs-lookup"><span data-stu-id="5fee0-281">SQRT(x)</span></span> | <span data-ttu-id="5fee0-282">Retourneert Hallo vierkante Hallo opgegeven numerieke waarde.</span><span class="sxs-lookup"><span data-stu-id="5fee0-282">Returns hello square of hello specified numeric value.</span></span> |

<span data-ttu-id="5fee0-283">Routes voorwaarden worden Hallo na type controleren en functies die ondersteund:</span><span class="sxs-lookup"><span data-stu-id="5fee0-283">In routes conditions, hello following type checking and casting functions are supported:</span></span>

| <span data-ttu-id="5fee0-284">Functie</span><span class="sxs-lookup"><span data-stu-id="5fee0-284">Function</span></span> | <span data-ttu-id="5fee0-285">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="5fee0-285">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="5fee0-286">AS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="5fee0-286">AS_NUMBER</span></span> | <span data-ttu-id="5fee0-287">Converteert Hallo invoerreeks tooa getal.</span><span class="sxs-lookup"><span data-stu-id="5fee0-287">Converts hello input string tooa number.</span></span> <span data-ttu-id="5fee0-288">`noop`Als de invoer is een getal. `Undefined` als tekenreeks geen een getal vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="5fee0-288">`noop` if input is a number; `Undefined` if string does not represent a number.</span></span>|
| <span data-ttu-id="5fee0-289">IS_ARRAY</span><span class="sxs-lookup"><span data-stu-id="5fee0-289">IS_ARRAY</span></span> | <span data-ttu-id="5fee0-290">Retourneert een Booleaanse waarde die aangeeft als Hallo type Hallo expressie opgegeven is een matrix.</span><span class="sxs-lookup"><span data-stu-id="5fee0-290">Returns a Boolean value indicating if hello type of hello specified expression is an array.</span></span> |
| <span data-ttu-id="5fee0-291">IS_BOOL</span><span class="sxs-lookup"><span data-stu-id="5fee0-291">IS_BOOL</span></span> | <span data-ttu-id="5fee0-292">Retourneert een Booleaanse waarde die aangeeft als Hallo type Hallo expressie opgegeven is een Booleaanse waarde.</span><span class="sxs-lookup"><span data-stu-id="5fee0-292">Returns a Boolean value indicating if hello type of hello specified expression is a Boolean.</span></span> |
| <span data-ttu-id="5fee0-293">IS_DEFINED</span><span class="sxs-lookup"><span data-stu-id="5fee0-293">IS_DEFINED</span></span> | <span data-ttu-id="5fee0-294">Retourneert een Booleaanse waarde die aangeeft of Hallo eigenschap een waarde is toegewezen.</span><span class="sxs-lookup"><span data-stu-id="5fee0-294">Returns a Boolean indicating if hello property has been assigned a value.</span></span> |
| <span data-ttu-id="5fee0-295">IS_NULL</span><span class="sxs-lookup"><span data-stu-id="5fee0-295">IS_NULL</span></span> | <span data-ttu-id="5fee0-296">Retourneert een Booleaanse waarde die aangeeft als Hallo type Hallo expressie opgegeven is null.</span><span class="sxs-lookup"><span data-stu-id="5fee0-296">Returns a Boolean value indicating if hello type of hello specified expression is null.</span></span> |
| <span data-ttu-id="5fee0-297">IS_NUMBER</span><span class="sxs-lookup"><span data-stu-id="5fee0-297">IS_NUMBER</span></span> | <span data-ttu-id="5fee0-298">Retourneert een Booleaanse waarde die aangeeft als Hallo type Hallo expressie opgegeven is een getal.</span><span class="sxs-lookup"><span data-stu-id="5fee0-298">Returns a Boolean value indicating if hello type of hello specified expression is a number.</span></span> |
| <span data-ttu-id="5fee0-299">IS_OBJECT</span><span class="sxs-lookup"><span data-stu-id="5fee0-299">IS_OBJECT</span></span> | <span data-ttu-id="5fee0-300">Retourneert een Booleaanse waarde die aangeeft als Hallo type Hallo expressie opgegeven is een JSON-object.</span><span class="sxs-lookup"><span data-stu-id="5fee0-300">Returns a Boolean value indicating if hello type of hello specified expression is a JSON object.</span></span> |
| <span data-ttu-id="5fee0-301">IS_PRIMITIVE</span><span class="sxs-lookup"><span data-stu-id="5fee0-301">IS_PRIMITIVE</span></span> | <span data-ttu-id="5fee0-302">Retourneert een Booleaanse waarde waarmee wordt aangegeven als Hallo type Hallo opgegeven expressie is een primitief (string, Boolean, numerieke of `null`).</span><span class="sxs-lookup"><span data-stu-id="5fee0-302">Returns a Boolean value indicating if hello type of hello specified expression is a primitive (string, Boolean, numeric or `null`).</span></span> |
| <span data-ttu-id="5fee0-303">IS_STRING</span><span class="sxs-lookup"><span data-stu-id="5fee0-303">IS_STRING</span></span> | <span data-ttu-id="5fee0-304">Retourneert een Booleaanse waarde die aangeeft als Hallo type Hallo expressie opgegeven is een tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="5fee0-304">Returns a Boolean value indicating if hello type of hello specified expression is a string.</span></span> |

<span data-ttu-id="5fee0-305">Routes voorwaarden worden Hallo na tekenreeks-functies ondersteund:</span><span class="sxs-lookup"><span data-stu-id="5fee0-305">In routes conditions, hello following string functions are supported:</span></span>

| <span data-ttu-id="5fee0-306">Functie</span><span class="sxs-lookup"><span data-stu-id="5fee0-306">Function</span></span> | <span data-ttu-id="5fee0-307">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="5fee0-307">Description</span></span> |
| -------- | ----------- |
| <span data-ttu-id="5fee0-308">CONCAT(x,...)</span><span class="sxs-lookup"><span data-stu-id="5fee0-308">CONCAT(x, …)</span></span> | <span data-ttu-id="5fee0-309">Retourneert een tekenreeks die Hallo resultaat is van het samenvoegen van twee of meer tekenreekswaarden.</span><span class="sxs-lookup"><span data-stu-id="5fee0-309">Returns a string that is hello result of concatenating two or more string values.</span></span> |
| <span data-ttu-id="5fee0-310">LENGTH(x)</span><span class="sxs-lookup"><span data-stu-id="5fee0-310">LENGTH(x)</span></span> | <span data-ttu-id="5fee0-311">Retourneert Hallo aantal tekens Hallo opgegeven tekenreeksexpressie.</span><span class="sxs-lookup"><span data-stu-id="5fee0-311">Returns hello number of characters of hello specified string expression.</span></span>|
| <span data-ttu-id="5fee0-312">LOWER(x)</span><span class="sxs-lookup"><span data-stu-id="5fee0-312">LOWER(x)</span></span> | <span data-ttu-id="5fee0-313">Retourneert een tekenreeksexpressie na hoofdletter gegevens toolowercase converteren.</span><span class="sxs-lookup"><span data-stu-id="5fee0-313">Returns a string expression after converting uppercase character data toolowercase.</span></span> |
| <span data-ttu-id="5fee0-314">UPPER(x)</span><span class="sxs-lookup"><span data-stu-id="5fee0-314">UPPER(x)</span></span> | <span data-ttu-id="5fee0-315">Retourneert een tekenreeksexpressie na kleine letter gegevens toouppercase converteren.</span><span class="sxs-lookup"><span data-stu-id="5fee0-315">Returns a string expression after converting lowercase character data toouppercase.</span></span> |
| <span data-ttu-id="5fee0-316">De SUBTEKENREEKS (tekenreeks, start [, lengte])</span><span class="sxs-lookup"><span data-stu-id="5fee0-316">SUBSTRING(string, start [, length])</span></span> | <span data-ttu-id="5fee0-317">Retourneert deel uit van een tekenreeksexpressie die begint bij Hallo opgegeven teken op nul gebaseerde positie en blijft toohello opgegeven lengte of toohello einde van de Hallo-tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="5fee0-317">Returns part of a string expression starting at hello specified character zero-based position and continues toohello specified length, or toohello end of hello string.</span></span> |
| <span data-ttu-id="5fee0-318">INDEX_OF (tekenreeks, fragment)</span><span class="sxs-lookup"><span data-stu-id="5fee0-318">INDEX_OF(string, fragment)</span></span> | <span data-ttu-id="5fee0-319">Retourneert Hallo beginpositie van de eerste instantie Hallo van tweede tekenreeksexpressie Hallo binnen Hallo eerste opgegeven tekenreeksexpressie of -1 als het Hallo-tekenreeks is niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="5fee0-319">Returns hello starting position of hello first occurrence of hello second string expression within hello first specified string expression, or -1 if hello string is not found.</span></span>|
| <span data-ttu-id="5fee0-320">STARTS_WITH (x, y)</span><span class="sxs-lookup"><span data-stu-id="5fee0-320">STARTS_WITH(x, y)</span></span> | <span data-ttu-id="5fee0-321">Retourneert een Booleaanse waarde die aangeeft of de eerste tekenreeksexpressie Hallo op de tweede met de Hallo begint.</span><span class="sxs-lookup"><span data-stu-id="5fee0-321">Returns a Boolean indicating whether hello first string expression starts with hello second.</span></span> |
| <span data-ttu-id="5fee0-322">ENDS_WITH (x, y)</span><span class="sxs-lookup"><span data-stu-id="5fee0-322">ENDS_WITH(x, y)</span></span> | <span data-ttu-id="5fee0-323">Retourneert een Booleaanse waarde die aangeeft of de eerste tekenreeksexpressie Hallo Hallo tweede eindigt.</span><span class="sxs-lookup"><span data-stu-id="5fee0-323">Returns a Boolean indicating whether hello first string expression ends with hello second.</span></span> |
| <span data-ttu-id="5fee0-324">CONTAINS(x,y)</span><span class="sxs-lookup"><span data-stu-id="5fee0-324">CONTAINS(x,y)</span></span> | <span data-ttu-id="5fee0-325">Retourneert een Booleaanse waarde die aangeeft of de eerste tekenreeksexpressie Hallo Hallo op de tweede bevat.</span><span class="sxs-lookup"><span data-stu-id="5fee0-325">Returns a Boolean indicating whether hello first string expression contains hello second.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5fee0-326">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5fee0-326">Next steps</span></span>
<span data-ttu-id="5fee0-327">Meer informatie over hoe tooexecute query's in uw apps met behulp van [Azure IoT SDK's][lnk-hub-sdks].</span><span class="sxs-lookup"><span data-stu-id="5fee0-327">Learn how tooexecute queries in your apps using [Azure IoT SDKs][lnk-hub-sdks].</span></span>

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
