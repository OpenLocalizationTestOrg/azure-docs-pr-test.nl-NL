---
title: taken voor aaaUnderstand Azure IoT Hub | Microsoft Docs
description: Handleiding voor ontwikkelaars - taken toorun op meerdere apparaten plannen tooyour IoT-hub verbonden. Taken kunnen bijwerken labels en gewenste eigenschappen en methoden niet aanroepen direct voor meerdere apparaten.
services: iot-hub
documentationcenter: .net
author: juanjperez
manager: timlt
editor: 
ms.assetid: fe78458f-4f14-4358-ac83-4f7bd14ee8da
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/30/2016
ms.author: juanpere
ms.openlocfilehash: 8be134e6c379feae5087df8f562a74505c57afee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="schedule-jobs-on-multiple-devices"></a><span data-ttu-id="4e0e4-104">Taken op meerdere apparaten plannen</span><span class="sxs-lookup"><span data-stu-id="4e0e4-104">Schedule jobs on multiple devices</span></span>
## <a name="overview"></a><span data-ttu-id="4e0e4-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="4e0e4-105">Overview</span></span>
<span data-ttu-id="4e0e4-106">Zoals beschreven door de vorige artikelen, maakt Azure IoT Hub een aantal bouwstenen ([twin apparaateigenschappen en tags] [ lnk-twin-devguide] en [methoden directe] [ lnk-dev-methods]).</span><span class="sxs-lookup"><span data-stu-id="4e0e4-106">As described by previous articles, Azure IoT Hub enables a number of building blocks ([device twin properties and tags][lnk-twin-devguide] and [direct methods][lnk-dev-methods]).</span></span>  <span data-ttu-id="4e0e4-107">Normaal gesproken back-end-apps inschakelen apparaat beheerders en operators tooupdate en communiceren met IoT-apparaten bulksgewijs en op een gepland tijdstip.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-107">Typically, back-end apps enable device administrators and operators tooupdate and interact with IoT devices in bulk and at a scheduled time.</span></span>  <span data-ttu-id="4e0e4-108">Taken inkapselen Hallo uitvoering van twin apparaatupdates en rechtstreekse methoden op basis van een verzameling apparaten op een tijdstip planning.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-108">Jobs encapsulate hello execution of device twin updates and direct methods against a set of devices at a schedule time.</span></span>  <span data-ttu-id="4e0e4-109">Een operator zou bijvoorbeeld een back-end-app die u wilt starten en bijhouden van een taak tooreboot een reeks apparaten bij het bouwen van 43 en floor 3 op een tijdstip dat verstoren toohello bewerkingen van Hallo gebouw niet zou gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-109">For example, an operator would use a back-end app that would initiate and track a job tooreboot a set of devices in building 43 and floor 3 at a time that would not be disruptive toohello operations of hello building.</span></span>

### <a name="when-toouse"></a><span data-ttu-id="4e0e4-110">Wanneer toouse</span><span class="sxs-lookup"><span data-stu-id="4e0e4-110">When toouse</span></span>
<span data-ttu-id="4e0e4-111">Overweeg het gebruik van taken wanneer: van Hallo activiteiten in een set van apparaat na de voortgang van een oplossing voor back-end behoeften tooschedule en bijhouden:</span><span class="sxs-lookup"><span data-stu-id="4e0e4-111">Consider using jobs when: a solution back end needs tooschedule and track progress any of hello following activities on a set of device:</span></span>

* <span data-ttu-id="4e0e4-112">Gewenste eigenschappen bijwerken</span><span class="sxs-lookup"><span data-stu-id="4e0e4-112">Update desired properties</span></span>
* <span data-ttu-id="4e0e4-113">Labels bijwerken</span><span class="sxs-lookup"><span data-stu-id="4e0e4-113">Update tags</span></span>
* <span data-ttu-id="4e0e4-114">Directe methoden aanroepen</span><span class="sxs-lookup"><span data-stu-id="4e0e4-114">Invoke direct methods</span></span>

## <a name="job-lifecycle"></a><span data-ttu-id="4e0e4-115">De levenscyclus van taak</span><span class="sxs-lookup"><span data-stu-id="4e0e4-115">Job lifecycle</span></span>
<span data-ttu-id="4e0e4-116">Taken worden gestart door Hallo back-end oplossing en beheerd door de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-116">Jobs are initiated by hello solution back end and maintained by IoT Hub.</span></span>  <span data-ttu-id="4e0e4-117">U kunt een taak via een URI service gerichte starten (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) en de query voor de voortgang van een taak wordt uitgevoerd via een URI service gerichte (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span><span class="sxs-lookup"><span data-stu-id="4e0e4-117">You can initiate a job through a service-facing URI (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) and query for progress on an executing job through a service-facing URI (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span></span>  <span data-ttu-id="4e0e4-118">Zodra een taak wordt gestart, kunt een query uitvoert voor taken Hallo back-endserver voor apps toorefresh Hallo status van actieve taken.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-118">Once a job is initiated, querying for jobs enables hello back-end app toorefresh hello status of running jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="4e0e4-119">Wanneer u een taak gestart, namen en waarden mogen alleen US-ASCII-afdrukbare alfanumerieke behalve aanwezig in de volgende set Hallo: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-119">When you initiate a job, property names and values can only contain US-ASCII printable alphanumeric, except any in hello following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="4e0e4-120">De onderwerpen waarnaar wordt verwezen:</span><span class="sxs-lookup"><span data-stu-id="4e0e4-120">Reference topics:</span></span>
<span data-ttu-id="4e0e4-121">Hallo volgende verwijzing onderwerpen bieden u meer informatie over het gebruik van taken.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-121">hello following reference topics provide you with more information about using jobs.</span></span>

## <a name="jobs-tooexecute-direct-methods"></a><span data-ttu-id="4e0e4-122">Taken tooexecute rechtstreekse methoden</span><span class="sxs-lookup"><span data-stu-id="4e0e4-122">Jobs tooexecute direct methods</span></span>
<span data-ttu-id="4e0e4-123">Hallo volgt Hallo HTTP 1.1-gegevens voor de aanvraag voor het uitvoeren van een [directe methode] [ lnk-dev-methods] in een set van apparaten met behulp van een taak:</span><span class="sxs-lookup"><span data-stu-id="4e0e4-123">hello following is hello HTTP 1.1 request details for executing a [direct method][lnk-dev-methods] on a set of devices using a job:</span></span>

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleDirectRequest', 
        cloudToDeviceMethod: {
            methodName: '<methodName>',
            payload: <payload>,                 
            responseTimeoutInSeconds: methodTimeoutInSeconds 
        },
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        
    }
    ```
<span data-ttu-id="4e0e4-124">Hallo queryvoorwaarde kan ook worden voor één apparaat-Id of een lijst van apparaat-id's zoals hieronder wordt weergegeven</span><span class="sxs-lookup"><span data-stu-id="4e0e4-124">hello query condition can also be on a single device Id or on a list of device Ids as shown below</span></span>

<span data-ttu-id="4e0e4-125">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="4e0e4-125">**Examples**</span></span>
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
<span data-ttu-id="4e0e4-126">[IoT Hub-querytaal] [ lnk-query] worden querytaal IoT-Hub in meer detail behandeld.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-126">[IoT Hub Query Language][lnk-query] covers IoT Hub query language in additional detail.</span></span>

## <a name="jobs-tooupdate-device-twin-properties"></a><span data-ttu-id="4e0e4-127">Taken tooupdate apparaateigenschappen twin</span><span class="sxs-lookup"><span data-stu-id="4e0e4-127">Jobs tooupdate device twin properties</span></span>
<span data-ttu-id="4e0e4-128">Hallo volgende is Hallo HTTP 1.1-aanvraagdetails voor het bijwerken van twin apparaateigenschappen met behulp van een taak:</span><span class="sxs-lookup"><span data-stu-id="4e0e4-128">hello following is hello HTTP 1.1 request details for updating device twin properties using a job:</span></span>

    ```
    PUT /jobs/v2/<jobId>?api-version=2016-11-14
    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>

    {
        jobId: '<jobId>',
        type: 'scheduleTwinUpdate', 
        updateTwin: <patch>                 // Valid JSON object
        queryCondition: '<queryOrDevices>', // query condition
        startTime: <jobStartTime>,          // as an ISO-8601 date string
        maxExecutionTimeInSeconds: <maxExecutionTimeInSeconds>        // format TBD
    }
    ```

## <a name="querying-for-progress-on-jobs"></a><span data-ttu-id="4e0e4-129">Een query uitvoert voor de voortgang van taken</span><span class="sxs-lookup"><span data-stu-id="4e0e4-129">Querying for progress on jobs</span></span>
<span data-ttu-id="4e0e4-130">Hallo volgt Hallo details voor HTTP 1.1-aanvraag voor [opvragen van taken][lnk-query]:</span><span class="sxs-lookup"><span data-stu-id="4e0e4-130">hello following is hello HTTP 1.1 request details for [querying for jobs][lnk-query]:</span></span>

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

<span data-ttu-id="4e0e4-131">Hallo continuationToken wordt geleverd door het Hallo-antwoord.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-131">hello continuationToken is provided from hello response.</span></span>  

## <a name="jobs-properties"></a><span data-ttu-id="4e0e4-132">Eigenschappen van taken</span><span class="sxs-lookup"><span data-stu-id="4e0e4-132">Jobs Properties</span></span>
<span data-ttu-id="4e0e4-133">Hallo Hieronder volgt een lijst met eigenschappen en bijbehorende beschrijvingen, die kunnen worden gebruikt voor het uitvoeren van query's voor taken of taak resultaten.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-133">hello following is a list of properties and corresponding descriptions, which can be used when querying for jobs or job results.</span></span>

| <span data-ttu-id="4e0e4-134">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="4e0e4-134">Property</span></span> | <span data-ttu-id="4e0e4-135">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4e0e4-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4e0e4-136">**jobId**</span><span class="sxs-lookup"><span data-stu-id="4e0e4-136">**jobId**</span></span> |<span data-ttu-id="4e0e4-137">Aanvraag-ID opgegeven voor Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-137">Application provided ID for hello job.</span></span> |
| <span data-ttu-id="4e0e4-138">**startTime**</span><span class="sxs-lookup"><span data-stu-id="4e0e4-138">**startTime**</span></span> |<span data-ttu-id="4e0e4-139">Toepassing opgegeven begintijd (ISO 8601-) voor Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-139">Application provided start time (ISO-8601) for hello job.</span></span> |
| <span data-ttu-id="4e0e4-140">**Eindtijd**</span><span class="sxs-lookup"><span data-stu-id="4e0e4-140">**endTime**</span></span> |<span data-ttu-id="4e0e4-141">IoT Hub opgegeven datum (ISO 8601-) als Hallo-taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-141">IoT Hub provided date (ISO-8601) for when hello job completed.</span></span> <span data-ttu-id="4e0e4-142">Geldig nadat de taak Hallo Hallo 'voltooid' status bereikt.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-142">Valid only after hello job reaches hello 'completed' state.</span></span> |
| <span data-ttu-id="4e0e4-143">**type**</span><span class="sxs-lookup"><span data-stu-id="4e0e4-143">**type**</span></span> |<span data-ttu-id="4e0e4-144">Typen taken:</span><span class="sxs-lookup"><span data-stu-id="4e0e4-144">Types of jobs:</span></span> |
| <span data-ttu-id="4e0e4-145">**scheduledUpdateTwin**: een taak gebruikt tooupdate een reeks gewenste eigenschappen of labels.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-145">**scheduledUpdateTwin**: A job used tooupdate a set of desired properties or tags.</span></span> | |
| <span data-ttu-id="4e0e4-146">**scheduledDeviceMethod**: een taak gebruikt tooinvoke een methode van het apparaat van een reeks horende apparaten.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-146">**scheduledDeviceMethod**: A job used tooinvoke a device method on a set of device twins.</span></span> | |
| <span data-ttu-id="4e0e4-147">**status**</span><span class="sxs-lookup"><span data-stu-id="4e0e4-147">**status**</span></span> |<span data-ttu-id="4e0e4-148">Huidige status van het Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-148">Current state of hello job.</span></span> <span data-ttu-id="4e0e4-149">Mogelijke waarden voor de status van:</span><span class="sxs-lookup"><span data-stu-id="4e0e4-149">Possible values for status:</span></span> |
| <span data-ttu-id="4e0e4-150">**in behandeling** : gepland en wachten toobe die zijn opgepikt door Hallo taak service.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-150">**pending** : Scheduled and waiting toobe picked up by hello job service.</span></span> | |
| <span data-ttu-id="4e0e4-151">**geplande** : gepland voor een tijd in toekomstige Hallo.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-151">**scheduled** : Scheduled for a time in hello future.</span></span> | |
| <span data-ttu-id="4e0e4-152">**met** : momenteel actieve taken.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-152">**running** : Currently active job.</span></span> | |
| <span data-ttu-id="4e0e4-153">**geannuleerd** : taak is geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-153">**cancelled** : Job has been cancelled.</span></span> | |
| <span data-ttu-id="4e0e4-154">**kan geen** : taak is mislukt.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-154">**failed** : Job failed.</span></span> | |
| <span data-ttu-id="4e0e4-155">**voltooid** : taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-155">**completed** : Job has completed.</span></span> | |
| <span data-ttu-id="4e0e4-156">**deviceJobStatistics**</span><span class="sxs-lookup"><span data-stu-id="4e0e4-156">**deviceJobStatistics**</span></span> |<span data-ttu-id="4e0e4-157">Statistieken over Hallo taakuitvoering.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-157">Statistics about hello job's execution.</span></span> |

<span data-ttu-id="4e0e4-158">**deviceJobStatistics** eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-158">**deviceJobStatistics** properties.</span></span>

| <span data-ttu-id="4e0e4-159">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="4e0e4-159">Property</span></span> | <span data-ttu-id="4e0e4-160">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="4e0e4-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="4e0e4-161">**deviceJobStatistics.deviceCount**</span><span class="sxs-lookup"><span data-stu-id="4e0e4-161">**deviceJobStatistics.deviceCount**</span></span> |<span data-ttu-id="4e0e4-162">Het aantal apparaten in het Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-162">Number of devices in hello job.</span></span> |
| <span data-ttu-id="4e0e4-163">**deviceJobStatistics.failedCount**</span><span class="sxs-lookup"><span data-stu-id="4e0e4-163">**deviceJobStatistics.failedCount**</span></span> |<span data-ttu-id="4e0e4-164">Het aantal apparaten waarop Hallo-taak is mislukt.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-164">Number of devices where hello job failed.</span></span> |
| <span data-ttu-id="4e0e4-165">**deviceJobStatistics.succeededCount**</span><span class="sxs-lookup"><span data-stu-id="4e0e4-165">**deviceJobStatistics.succeededCount**</span></span> |<span data-ttu-id="4e0e4-166">Het aantal apparaten waarbij Hallo-taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-166">Number of devices where hello job succeeded.</span></span> |
| <span data-ttu-id="4e0e4-167">**deviceJobStatistics.runningCount**</span><span class="sxs-lookup"><span data-stu-id="4e0e4-167">**deviceJobStatistics.runningCount**</span></span> |<span data-ttu-id="4e0e4-168">Het aantal apparaten dat Hallo taak momenteel worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-168">Number of devices that are currently running hello job.</span></span> |
| <span data-ttu-id="4e0e4-169">**deviceJobStatistics.pendingCount**</span><span class="sxs-lookup"><span data-stu-id="4e0e4-169">**deviceJobStatistics.pendingCount**</span></span> |<span data-ttu-id="4e0e4-170">Het aantal apparaten met wachtende toorun Hallo taak.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-170">Number of devices that are pending toorun hello job.</span></span> |

### <a name="additional-reference-material"></a><span data-ttu-id="4e0e4-171">Aanvullende referentiemateriaal</span><span class="sxs-lookup"><span data-stu-id="4e0e4-171">Additional reference material</span></span>
<span data-ttu-id="4e0e4-172">Er zijn andere onderwerpen met naslaginformatie in Hallo Ontwikkelaarshandleiding voor IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="4e0e4-172">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="4e0e4-173">[IoT-hubeindpunten] [ lnk-endpoints] beschrijft Hallo verschillende eindpunten die elke IoT-hub voor runtime- en beheerbewerkingen toont.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-173">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="4e0e4-174">[Bandbreedtebeperking en quota's] [ lnk-quotas] beschrijft Hallo quota's die van toepassing toohello service IoT Hub en bandbreedteregeling gedrag tooexpect Hallo wanneer u Hallo-service gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-174">[Throttling and quotas][lnk-quotas] describes hello quotas that apply toohello IoT Hub service and hello throttling behavior tooexpect when you use hello service.</span></span>
* <span data-ttu-id="4e0e4-175">[Azure IoT-SDKs voor apparaat en de service] [ lnk-sdks] lijsten Hallo verschillende taal SDK's u een gebruiken bij het ontwikkelen van apps voor het apparaat en de service die communiceren met IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-175">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you an use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="4e0e4-176">[IoT Hub-querytaal voor apparaat horende, taken en berichtroutering] [ lnk-query] Hallo querytaal IoT-Hub kunt u informatie van de tooretrieve uit IoT Hub over uw apparaat horende en taken worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-176">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes hello IoT Hub query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="4e0e4-177">[Ondersteuning voor IoT Hub MQTT] [ lnk-devguide-mqtt] meer informatie over IoT Hub ondersteuning biedt voor Hallo MQTT protocol.</span><span class="sxs-lookup"><span data-stu-id="4e0e4-177">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e0e4-178">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4e0e4-178">Next steps</span></span>
<span data-ttu-id="4e0e4-179">Als u tootry sommige Hallo concepten die in dit artikel wordt beschreven wilt, kunt u mogelijk geïnteresseerd in Hallo IoT Hub-zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="4e0e4-179">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorial:</span></span>

* <span data-ttu-id="4e0e4-180">[Planning en broadcast-taken][lnk-jobs-tutorial]</span><span class="sxs-lookup"><span data-stu-id="4e0e4-180">[Schedule and broadcast jobs][lnk-jobs-tutorial]</span></span>

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-jobs-tutorial]: iot-hub-node-node-schedule-jobs.md
[lnk-c2d-methods]: iot-hub-node-node-direct-methods.md
[lnk-dev-methods]: iot-hub-devguide-direct-methods.md
[lnk-get-started-twin]: iot-hub-node-node-twin-getstarted.md
[lnk-twin-devguide]: iot-hub-devguide-device-twins.md
