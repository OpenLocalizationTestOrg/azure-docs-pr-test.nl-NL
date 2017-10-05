---
title: Azure IoT Hub taken begrijpen | Microsoft Docs
description: Handleiding voor ontwikkelaars - plannen van taken uit te voeren op meerdere apparaten verbonden met uw IoT-hub. Taken kunnen bijwerken labels en gewenste eigenschappen en methoden niet aanroepen direct voor meerdere apparaten.
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
ms.openlocfilehash: abb7f80662650efa8f158f32125ebc5350cb4f62
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="schedule-jobs-on-multiple-devices"></a><span data-ttu-id="f6548-104">Taken op meerdere apparaten plannen</span><span class="sxs-lookup"><span data-stu-id="f6548-104">Schedule jobs on multiple devices</span></span>
## <a name="overview"></a><span data-ttu-id="f6548-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="f6548-105">Overview</span></span>
<span data-ttu-id="f6548-106">Zoals beschreven door de vorige artikelen, maakt Azure IoT Hub een aantal bouwstenen ([twin apparaateigenschappen en tags] [ lnk-twin-devguide] en [methoden directe] [ lnk-dev-methods]).</span><span class="sxs-lookup"><span data-stu-id="f6548-106">As described by previous articles, Azure IoT Hub enables a number of building blocks ([device twin properties and tags][lnk-twin-devguide] and [direct methods][lnk-dev-methods]).</span></span>  <span data-ttu-id="f6548-107">Back-end-apps inschakelen normaal gesproken apparaatbeheerders en operators om te werken en te communiceren met IoT-apparaten bulksgewijs en op een gepland tijdstip.</span><span class="sxs-lookup"><span data-stu-id="f6548-107">Typically, back-end apps enable device administrators and operators to update and interact with IoT devices in bulk and at a scheduled time.</span></span>  <span data-ttu-id="f6548-108">Taken bevatten de uitvoering van twin apparaatupdates en rechtstreekse methoden op basis van een verzameling apparaten op een tijdstip planning.</span><span class="sxs-lookup"><span data-stu-id="f6548-108">Jobs encapsulate the execution of device twin updates and direct methods against a set of devices at a schedule time.</span></span>  <span data-ttu-id="f6548-109">Een operator gebruikt bijvoorbeeld een back-end-app die u wilt starten en bijhouden van een taak opnieuw opstarten van een reeks apparaten bij het bouwen van 43 en floor 3 tegelijk die niet aan de bewerkingen van het gebouw verstoren.</span><span class="sxs-lookup"><span data-stu-id="f6548-109">For example, an operator would use a back-end app that would initiate and track a job to reboot a set of devices in building 43 and floor 3 at a time that would not be disruptive to the operations of the building.</span></span>

### <a name="when-to-use"></a><span data-ttu-id="f6548-110">Wanneer gebruikt u dit?</span><span class="sxs-lookup"><span data-stu-id="f6548-110">When to use</span></span>
<span data-ttu-id="f6548-111">Overweeg het gebruik van taken wanneer: een oplossing voor back-endnetwerk moet plannen en de voortgang volgen van de volgende activiteiten in een set van apparaat:</span><span class="sxs-lookup"><span data-stu-id="f6548-111">Consider using jobs when: a solution back end needs to schedule and track progress any of the following activities on a set of device:</span></span>

* <span data-ttu-id="f6548-112">Gewenste eigenschappen bijwerken</span><span class="sxs-lookup"><span data-stu-id="f6548-112">Update desired properties</span></span>
* <span data-ttu-id="f6548-113">Labels bijwerken</span><span class="sxs-lookup"><span data-stu-id="f6548-113">Update tags</span></span>
* <span data-ttu-id="f6548-114">Directe methoden aanroepen</span><span class="sxs-lookup"><span data-stu-id="f6548-114">Invoke direct methods</span></span>

## <a name="job-lifecycle"></a><span data-ttu-id="f6548-115">De levenscyclus van taak</span><span class="sxs-lookup"><span data-stu-id="f6548-115">Job lifecycle</span></span>
<span data-ttu-id="f6548-116">Taken worden gestart door de back-end van de oplossing en beheerd door de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f6548-116">Jobs are initiated by the solution back end and maintained by IoT Hub.</span></span>  <span data-ttu-id="f6548-117">U kunt een taak via een URI service gerichte starten (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) en de query voor de voortgang van een taak wordt uitgevoerd via een URI service gerichte (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span><span class="sxs-lookup"><span data-stu-id="f6548-117">You can initiate a job through a service-facing URI (`{iot hub}/jobs/v2/{device id}/methods/<jobID>?api-version=2016-11-14`) and query for progress on an executing job through a service-facing URI (`{iot hub}/jobs/v2/<jobId>?api-version=2016-11-14`).</span></span>  <span data-ttu-id="f6548-118">Zodra een taak wordt gestart, kan een query uitvoert voor taken de back-end-app vernieuwen van de status van actieve taken.</span><span class="sxs-lookup"><span data-stu-id="f6548-118">Once a job is initiated, querying for jobs enables the back-end app to refresh the status of running jobs.</span></span>

> [!NOTE]
> <span data-ttu-id="f6548-119">Wanneer u een taak gestart, namen en waarden mogen alleen US-ASCII-afdrukbare alfanumerieke behalve aanwezig in de volgende set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span><span class="sxs-lookup"><span data-stu-id="f6548-119">When you initiate a job, property names and values can only contain US-ASCII printable alphanumeric, except any in the following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

## <a name="reference-topics"></a><span data-ttu-id="f6548-120">De onderwerpen waarnaar wordt verwezen:</span><span class="sxs-lookup"><span data-stu-id="f6548-120">Reference topics:</span></span>
<span data-ttu-id="f6548-121">De volgende onderwerpen met naslaginformatie bieden u meer informatie over het gebruik van taken.</span><span class="sxs-lookup"><span data-stu-id="f6548-121">The following reference topics provide you with more information about using jobs.</span></span>

## <a name="jobs-to-execute-direct-methods"></a><span data-ttu-id="f6548-122">Taken direct methoden uit te voeren</span><span class="sxs-lookup"><span data-stu-id="f6548-122">Jobs to execute direct methods</span></span>
<span data-ttu-id="f6548-123">Hieronder ziet u de details van de HTTP 1.1-aanvraag voor het uitvoeren van een [directe methode] [ lnk-dev-methods] in een set van apparaten met behulp van een taak:</span><span class="sxs-lookup"><span data-stu-id="f6548-123">The following is the HTTP 1.1 request details for executing a [direct method][lnk-dev-methods] on a set of devices using a job:</span></span>

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
<span data-ttu-id="f6548-124">De queryvoorwaarde kan ook worden voor één apparaat-Id of een lijst van apparaat-id's, zoals hieronder wordt weergegeven</span><span class="sxs-lookup"><span data-stu-id="f6548-124">The query condition can also be on a single device Id or on a list of device Ids as shown below</span></span>

<span data-ttu-id="f6548-125">**Voorbeelden**</span><span class="sxs-lookup"><span data-stu-id="f6548-125">**Examples**</span></span>
```
queryCondition = "deviceId = 'MyDevice1'"
queryCondition = "deviceId IN ['MyDevice1','MyDevice2']"
queryCondition = "deviceId IN ['MyDevice1']
```
<span data-ttu-id="f6548-126">[IoT Hub-querytaal] [ lnk-query] worden querytaal IoT-Hub in meer detail behandeld.</span><span class="sxs-lookup"><span data-stu-id="f6548-126">[IoT Hub Query Language][lnk-query] covers IoT Hub query language in additional detail.</span></span>

## <a name="jobs-to-update-device-twin-properties"></a><span data-ttu-id="f6548-127">Taken bijwerken twin apparaateigenschappen</span><span class="sxs-lookup"><span data-stu-id="f6548-127">Jobs to update device twin properties</span></span>
<span data-ttu-id="f6548-128">Hieronder ziet u de details van het HTTP 1.1-aanvraag voor het bijwerken van twin apparaateigenschappen met behulp van een taak:</span><span class="sxs-lookup"><span data-stu-id="f6548-128">The following is the HTTP 1.1 request details for updating device twin properties using a job:</span></span>

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

## <a name="querying-for-progress-on-jobs"></a><span data-ttu-id="f6548-129">Een query uitvoert voor de voortgang van taken</span><span class="sxs-lookup"><span data-stu-id="f6548-129">Querying for progress on jobs</span></span>
<span data-ttu-id="f6548-130">Hieronder ziet u de details van het HTTP 1.1-aanvraag voor [opvragen van taken][lnk-query]:</span><span class="sxs-lookup"><span data-stu-id="f6548-130">The following is the HTTP 1.1 request details for [querying for jobs][lnk-query]:</span></span>

    ```
    GET /jobs/v2/query?api-version=2016-11-14[&jobType=<jobType>][&jobStatus=<jobStatus>][&pageSize=<pageSize>][&continuationToken=<continuationToken>]

    Authorization: <config.sharedAccessSignature>
    Content-Type: application/json; charset=utf-8
    Request-Id: <guid>
    User-Agent: <sdk-name>/<sdk-version>
    ```

<span data-ttu-id="f6548-131">De continuationToken wordt geleverd door het antwoord.</span><span class="sxs-lookup"><span data-stu-id="f6548-131">The continuationToken is provided from the response.</span></span>  

## <a name="jobs-properties"></a><span data-ttu-id="f6548-132">Eigenschappen van taken</span><span class="sxs-lookup"><span data-stu-id="f6548-132">Jobs Properties</span></span>
<span data-ttu-id="f6548-133">Hier volgt een lijst met eigenschappen en bijbehorende beschrijvingen, die kunnen worden gebruikt voor het uitvoeren van query's voor taken of taak resultaten.</span><span class="sxs-lookup"><span data-stu-id="f6548-133">The following is a list of properties and corresponding descriptions, which can be used when querying for jobs or job results.</span></span>

| <span data-ttu-id="f6548-134">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="f6548-134">Property</span></span> | <span data-ttu-id="f6548-135">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f6548-135">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f6548-136">**jobId**</span><span class="sxs-lookup"><span data-stu-id="f6548-136">**jobId**</span></span> |<span data-ttu-id="f6548-137">Aanvraag-ID opgegeven voor de taak.</span><span class="sxs-lookup"><span data-stu-id="f6548-137">Application provided ID for the job.</span></span> |
| <span data-ttu-id="f6548-138">**startTime**</span><span class="sxs-lookup"><span data-stu-id="f6548-138">**startTime**</span></span> |<span data-ttu-id="f6548-139">Toepassing opgegeven begintijd (ISO 8601-) voor de taak.</span><span class="sxs-lookup"><span data-stu-id="f6548-139">Application provided start time (ISO-8601) for the job.</span></span> |
| <span data-ttu-id="f6548-140">**Eindtijd**</span><span class="sxs-lookup"><span data-stu-id="f6548-140">**endTime**</span></span> |<span data-ttu-id="f6548-141">IoT Hub opgegeven datum (ISO 8601-) voor wanneer de taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="f6548-141">IoT Hub provided date (ISO-8601) for when the job completed.</span></span> <span data-ttu-id="f6548-142">Geldig nadat de taak de status 'voltooid' bereikt.</span><span class="sxs-lookup"><span data-stu-id="f6548-142">Valid only after the job reaches the 'completed' state.</span></span> |
| <span data-ttu-id="f6548-143">**type**</span><span class="sxs-lookup"><span data-stu-id="f6548-143">**type**</span></span> |<span data-ttu-id="f6548-144">Typen taken:</span><span class="sxs-lookup"><span data-stu-id="f6548-144">Types of jobs:</span></span> |
| <span data-ttu-id="f6548-145">**scheduledUpdateTwin**: een taak die wordt gebruikt voor het bijwerken van een reeks gewenste eigenschappen of labels.</span><span class="sxs-lookup"><span data-stu-id="f6548-145">**scheduledUpdateTwin**: A job used to update a set of desired properties or tags.</span></span> | |
| <span data-ttu-id="f6548-146">**scheduledDeviceMethod**: een taak gebruikt de methode van een apparaat op een reeks horende apparaten aan te roepen.</span><span class="sxs-lookup"><span data-stu-id="f6548-146">**scheduledDeviceMethod**: A job used to invoke a device method on a set of device twins.</span></span> | |
| <span data-ttu-id="f6548-147">**status**</span><span class="sxs-lookup"><span data-stu-id="f6548-147">**status**</span></span> |<span data-ttu-id="f6548-148">Huidige status van de taak.</span><span class="sxs-lookup"><span data-stu-id="f6548-148">Current state of the job.</span></span> <span data-ttu-id="f6548-149">Mogelijke waarden voor de status van:</span><span class="sxs-lookup"><span data-stu-id="f6548-149">Possible values for status:</span></span> |
| <span data-ttu-id="f6548-150">**in behandeling** : gepland en wacht om te worden opgenomen door de taak service.</span><span class="sxs-lookup"><span data-stu-id="f6548-150">**pending** : Scheduled and waiting to be picked up by the job service.</span></span> | |
| <span data-ttu-id="f6548-151">**geplande** : gepland voor een tijd in de toekomst.</span><span class="sxs-lookup"><span data-stu-id="f6548-151">**scheduled** : Scheduled for a time in the future.</span></span> | |
| <span data-ttu-id="f6548-152">**met** : momenteel actieve taken.</span><span class="sxs-lookup"><span data-stu-id="f6548-152">**running** : Currently active job.</span></span> | |
| <span data-ttu-id="f6548-153">**geannuleerd** : taak is geannuleerd.</span><span class="sxs-lookup"><span data-stu-id="f6548-153">**cancelled** : Job has been cancelled.</span></span> | |
| <span data-ttu-id="f6548-154">**kan geen** : taak is mislukt.</span><span class="sxs-lookup"><span data-stu-id="f6548-154">**failed** : Job failed.</span></span> | |
| <span data-ttu-id="f6548-155">**voltooid** : taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="f6548-155">**completed** : Job has completed.</span></span> | |
| <span data-ttu-id="f6548-156">**deviceJobStatistics**</span><span class="sxs-lookup"><span data-stu-id="f6548-156">**deviceJobStatistics**</span></span> |<span data-ttu-id="f6548-157">Statistieken over van de taak kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f6548-157">Statistics about the job's execution.</span></span> |

<span data-ttu-id="f6548-158">**deviceJobStatistics** eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="f6548-158">**deviceJobStatistics** properties.</span></span>

| <span data-ttu-id="f6548-159">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="f6548-159">Property</span></span> | <span data-ttu-id="f6548-160">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="f6548-160">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f6548-161">**deviceJobStatistics.deviceCount**</span><span class="sxs-lookup"><span data-stu-id="f6548-161">**deviceJobStatistics.deviceCount**</span></span> |<span data-ttu-id="f6548-162">Het aantal apparaten in de taak.</span><span class="sxs-lookup"><span data-stu-id="f6548-162">Number of devices in the job.</span></span> |
| <span data-ttu-id="f6548-163">**deviceJobStatistics.failedCount**</span><span class="sxs-lookup"><span data-stu-id="f6548-163">**deviceJobStatistics.failedCount**</span></span> |<span data-ttu-id="f6548-164">Het aantal apparaten waarop de taak is mislukt.</span><span class="sxs-lookup"><span data-stu-id="f6548-164">Number of devices where the job failed.</span></span> |
| <span data-ttu-id="f6548-165">**deviceJobStatistics.succeededCount**</span><span class="sxs-lookup"><span data-stu-id="f6548-165">**deviceJobStatistics.succeededCount**</span></span> |<span data-ttu-id="f6548-166">Het aantal apparaten waarop de taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="f6548-166">Number of devices where the job succeeded.</span></span> |
| <span data-ttu-id="f6548-167">**deviceJobStatistics.runningCount**</span><span class="sxs-lookup"><span data-stu-id="f6548-167">**deviceJobStatistics.runningCount**</span></span> |<span data-ttu-id="f6548-168">Het aantal apparaten dat de taak die momenteel worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="f6548-168">Number of devices that are currently running the job.</span></span> |
| <span data-ttu-id="f6548-169">**deviceJobStatistics.pendingCount**</span><span class="sxs-lookup"><span data-stu-id="f6548-169">**deviceJobStatistics.pendingCount**</span></span> |<span data-ttu-id="f6548-170">Het aantal apparaten dat in behandeling zijn de taak uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="f6548-170">Number of devices that are pending to run the job.</span></span> |

### <a name="additional-reference-material"></a><span data-ttu-id="f6548-171">Aanvullende referentiemateriaal</span><span class="sxs-lookup"><span data-stu-id="f6548-171">Additional reference material</span></span>
<span data-ttu-id="f6548-172">Er zijn andere onderwerpen waarnaar wordt verwezen in de IoT Hub developer guide:</span><span class="sxs-lookup"><span data-stu-id="f6548-172">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="f6548-173">[IoT-hubeindpunten] [ lnk-endpoints] beschrijft de verschillende eindpunten die elke IoT-hub voor runtime- en beheerbewerkingen toont.</span><span class="sxs-lookup"><span data-stu-id="f6548-173">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="f6548-174">[Bandbreedtebeperking en quota's] [ lnk-quotas] beschrijving van de quota die betrekking hebben op de IoT Hub-service en het gedrag bandbreedteregeling kunt verwachten wanneer u de service gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f6548-174">[Throttling and quotas][lnk-quotas] describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span></span>
* <span data-ttu-id="f6548-175">[Azure IoT-SDKs voor apparaat en de service] [ lnk-sdks] geeft een lijst van de taal van de verschillende SDK's u een gebruiken bij het ontwikkelen van apps voor het apparaat en de service die communiceren met IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="f6548-175">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you an use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="f6548-176">[IoT Hub-querytaal voor apparaat horende, taken en berichtroutering] [ lnk-query] beschrijft de IoT Hub-querytaal kunt u gegevens ophalen uit IoT Hub over uw apparaat horende en taken.</span><span class="sxs-lookup"><span data-stu-id="f6548-176">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="f6548-177">[Ondersteuning voor IoT Hub MQTT] [ lnk-devguide-mqtt] meer informatie over IoT Hub ondersteuning biedt voor het MQTT-protocol.</span><span class="sxs-lookup"><span data-stu-id="f6548-177">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6548-178">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f6548-178">Next steps</span></span>
<span data-ttu-id="f6548-179">Als u wilt uitproberen enkele concepten die in dit artikel wordt beschreven, kunt u mogelijk geïnteresseerd in de volgende IoT Hub-zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="f6548-179">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="f6548-180">[Planning en broadcast-taken][lnk-jobs-tutorial]</span><span class="sxs-lookup"><span data-stu-id="f6548-180">[Schedule and broadcast jobs][lnk-jobs-tutorial]</span></span>

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
