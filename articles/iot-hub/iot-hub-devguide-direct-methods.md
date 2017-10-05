---
title: Directe methoden Azure IoT Hub | Microsoft Docs
description: Handleiding voor ontwikkelaars - rechtstreekse methoden gebruiken om aan te roepen code op uw apparaten vanuit een app service.
services: iot-hub
documentationcenter: .net
author: nberdy
manager: timlt
editor: 
ms.assetid: 9f0535f1-02e6-467a-9fc4-c0950702102d
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: nberdy
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 77e788a32097edbcb1cd4faaa45f35812eabd94a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="understand-and-invoke-direct-methods-from-iot-hub"></a><span data-ttu-id="9ef84-103">Begrijpen en direct methoden uit IoT Hub aanroepen</span><span class="sxs-lookup"><span data-stu-id="9ef84-103">Understand and invoke direct methods from IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="9ef84-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="9ef84-104">Overview</span></span>
<span data-ttu-id="9ef84-105">IoT-Hub kunt u direct methoden op apparaten uit de cloud.</span><span class="sxs-lookup"><span data-stu-id="9ef84-105">IoT Hub gives you ability to invoke direct methods on devices from the cloud.</span></span> <span data-ttu-id="9ef84-106">Rechtstreekse methoden vertegenwoordigen een request-reply interactie met een apparaat dat vergelijkbaar is met een HTTP-aanroep in dat ze slagen of onmiddellijk (na een door de gebruiker opgegeven time mislukken).</span><span class="sxs-lookup"><span data-stu-id="9ef84-106">Direct methods represent a request-reply interaction with a device similar to an HTTP call in that they succeed or fail immediately (after a user-specified timeout).</span></span> <span data-ttu-id="9ef84-107">Dit is nuttig voor scenario's waarin het verloop van directe actie verschillend, afhankelijk van of het apparaat kunnen reageren, zoals het verzenden van een SMS wake-up naar een apparaat als een apparaat is offline (SMS wordt duurder dan een methodeaanroep van) is.</span><span class="sxs-lookup"><span data-stu-id="9ef84-107">This is useful for scenarios where the course of immediate action is different depending on whether the device was able to respond, such as sending an SMS wake-up to a device if a device is offline (SMS being more expensive than a method call).</span></span>

<span data-ttu-id="9ef84-108">Elke methode apparaat gericht op één apparaat.</span><span class="sxs-lookup"><span data-stu-id="9ef84-108">Each device method targets a single device.</span></span> <span data-ttu-id="9ef84-109">[Taken] [ lnk-devguide-jobs] plannen methodeaanroep voor niet-verbonden apparaten en bieden een manier om aan te roepen rechtstreekse methoden op meerdere apparaten.</span><span class="sxs-lookup"><span data-stu-id="9ef84-109">[Jobs][lnk-devguide-jobs] provide a way to invoke direct methods on multiple devices, and schedule method invocation for disconnected devices.</span></span>

<span data-ttu-id="9ef84-110">Iedereen met **service verbinding** machtigingen voor IoT Hub kunnen een methode aangeroepen voor een apparaat.</span><span class="sxs-lookup"><span data-stu-id="9ef84-110">Anyone with **service connect** permissions on IoT Hub may invoke a method on a device.</span></span>

### <a name="when-to-use"></a><span data-ttu-id="9ef84-111">Wanneer gebruikt u dit?</span><span class="sxs-lookup"><span data-stu-id="9ef84-111">When to use</span></span>
<span data-ttu-id="9ef84-112">Methoden voor direct een reactie op aanvragen patroon volgen en zijn bedoeld voor communicatie waarvoor onmiddellijke bevestiging van hun resultaat, meestal interactief beheer van het apparaat, bijvoorbeeld een ventilator inschakelen.</span><span class="sxs-lookup"><span data-stu-id="9ef84-112">Direct methods follow a request-response pattern and are meant for communications that require immediate confirmation of their result, usually interactive control of the device, for example to turn on a fan.</span></span>

<span data-ttu-id="9ef84-113">Raadpleeg [Cloud-naar-apparaat communicatie richtlijnen] [ lnk-c2d-guidance] als u twijfelt tussen het gebruik van de eigenschappen van de gewenste directe methoden of cloud-naar-apparaat-berichten.</span><span class="sxs-lookup"><span data-stu-id="9ef84-113">Refer to [Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="method-lifecycle"></a><span data-ttu-id="9ef84-114">De levenscyclus van de methode</span><span class="sxs-lookup"><span data-stu-id="9ef84-114">Method lifecycle</span></span>
<span data-ttu-id="9ef84-115">Rechtstreekse methoden worden geïmplementeerd op het apparaat en nul of meer van de invoervermeldingen in de nettolading van de methode correct instantiëren vereisen.</span><span class="sxs-lookup"><span data-stu-id="9ef84-115">Direct methods are implemented on the device and may require zero or more inputs in the method payload to correctly instantiate.</span></span> <span data-ttu-id="9ef84-116">Aanroepen van een directe methode via een URI service gerichte (`{iot hub}/twins/{device id}/methods/`).</span><span class="sxs-lookup"><span data-stu-id="9ef84-116">You invoke a direct method through a service-facing URI (`{iot hub}/twins/{device id}/methods/`).</span></span> <span data-ttu-id="9ef84-117">Een apparaat ontvangt rechtstreekse methoden door een apparaat-specifieke MQTT onderwerp (`$iothub/methods/POST/{method name}/`).</span><span class="sxs-lookup"><span data-stu-id="9ef84-117">A device receives direct methods through a device-specific MQTT topic (`$iothub/methods/POST/{method name}/`).</span></span> <span data-ttu-id="9ef84-118">We kunnen rechtstreekse methoden in de toekomst ondersteuning op extra apparaten aan clientzijde-netwerkprotocollen.</span><span class="sxs-lookup"><span data-stu-id="9ef84-118">We may support direct methods on additional device-side networking protocols in the future.</span></span>

> [!NOTE]
> <span data-ttu-id="9ef84-119">Wanneer u een directe methode voor een apparaat aangeroepen, namen en waarden mogen alleen US-ASCII-afdrukbare alfanumerieke behalve aanwezig in de volgende set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span><span class="sxs-lookup"><span data-stu-id="9ef84-119">When you invoke a direct method on a device, property names and values can only contain US-ASCII printable alphanumeric, except any in the following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

<span data-ttu-id="9ef84-120">Directe methoden zijn synchrone en een slagen of mislukken na de time-outperiode (standaard: 30 seconden, worden ingesteld van 3600 seconden).</span><span class="sxs-lookup"><span data-stu-id="9ef84-120">Direct methods are synchronous and either succeed or fail after the timeout period (default: 30 seconds, settable up to 3600 seconds).</span></span> <span data-ttu-id="9ef84-121">Directe methoden zijn nuttig in interactieve scenario's waar u een apparaat om te fungeren als het apparaat online en ontvangende opdrachten is, zoals het inschakelen van een licht via een telefoon.</span><span class="sxs-lookup"><span data-stu-id="9ef84-121">Direct methods are useful in interactive scenarios where you want a device to act if and only if the device is online and receiving commands, such as turning on a light from a phone.</span></span> <span data-ttu-id="9ef84-122">In deze scenario's die u wilt zien van een onmiddellijke slagen of mislukken, dus de cloudservice kan worden uitgevoerd op het resultaat zo snel mogelijk.</span><span class="sxs-lookup"><span data-stu-id="9ef84-122">In these scenarios, you want to see an immediate success or failure so the cloud service can act on the result as soon as possible.</span></span> <span data-ttu-id="9ef84-123">Het apparaat kan sommige berichttekst als gevolg van de methode retourneren, maar het is niet vereist voor de methode om dit te doen.</span><span class="sxs-lookup"><span data-stu-id="9ef84-123">The device may return some message body as a result of the method, but it isn't required for the method to do so.</span></span> <span data-ttu-id="9ef84-124">Er is geen garantie op volgorde of eventuele semantiek gelijktijdigheid van taken op methodeaanroepen.</span><span class="sxs-lookup"><span data-stu-id="9ef84-124">There is no guarantee on ordering or any concurrency semantics on method calls.</span></span>

<span data-ttu-id="9ef84-125">Directe methode zijn HTTP alleen-lezen van de kant van de cloud en MQTT alleen-lezen van de kant van het apparaat.</span><span class="sxs-lookup"><span data-stu-id="9ef84-125">Direct method are HTTP-only from the cloud side, and MQTT-only from the device side.</span></span>

<span data-ttu-id="9ef84-126">De nettolading voor methodeaanvragen en antwoorden is een JSON-document maximaal 8KB.</span><span class="sxs-lookup"><span data-stu-id="9ef84-126">The payload for method requests and responses is a JSON document up to 8KB.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="9ef84-127">De onderwerpen waarnaar wordt verwezen:</span><span class="sxs-lookup"><span data-stu-id="9ef84-127">Reference topics:</span></span>
<span data-ttu-id="9ef84-128">De volgende onderwerpen met naslaginformatie bieden u meer informatie over het gebruik van rechtstreekse methoden.</span><span class="sxs-lookup"><span data-stu-id="9ef84-128">The following reference topics provide you with more information about using direct methods.</span></span>

## <a name="invoke-a-direct-method-from-a-back-end-app"></a><span data-ttu-id="9ef84-129">Aanroepen van een directe methode van een back-endserver voor apps</span><span class="sxs-lookup"><span data-stu-id="9ef84-129">Invoke a direct method from a back-end app</span></span>
### <a name="method-invocation"></a><span data-ttu-id="9ef84-130">De methodeaanroep</span><span class="sxs-lookup"><span data-stu-id="9ef84-130">Method invocation</span></span>
<span data-ttu-id="9ef84-131">Directe methode aanroepen op een apparaat zijn HTTP-aanroepen die bestaan uit:</span><span class="sxs-lookup"><span data-stu-id="9ef84-131">Direct method invocations on a device are HTTP calls which comprise:</span></span>

* <span data-ttu-id="9ef84-132">De *URI* specifiek zijn voor het apparaat (`{iot hub}/twins/{device id}/methods/`)</span><span class="sxs-lookup"><span data-stu-id="9ef84-132">The *URI* specific to the device (`{iot hub}/twins/{device id}/methods/`)</span></span>
* <span data-ttu-id="9ef84-133">De POST *methode*</span><span class="sxs-lookup"><span data-stu-id="9ef84-133">The POST *method*</span></span>
* <span data-ttu-id="9ef84-134">*Headers* waarop de autorisatie bevatten, aanvraag-ID, het type inhoud en de codering van inhoud</span><span class="sxs-lookup"><span data-stu-id="9ef84-134">*Headers* which contain the authorization, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="9ef84-135">Een transparante JSON *hoofdtekst* in de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="9ef84-135">A transparent JSON *body* in the following format:</span></span>

```
{
    "methodName": "reboot",
    "responseTimeoutInSeconds": 200,
    "payload": {
        "input1": "someInput",
        "input2": "anotherInput"
    }
}
```

<span data-ttu-id="9ef84-136">Er is een time-out in seconden.</span><span class="sxs-lookup"><span data-stu-id="9ef84-136">Timeout is in seconds.</span></span> <span data-ttu-id="9ef84-137">Als de time-out voor niet is ingesteld, wordt standaard 30 seconden.</span><span class="sxs-lookup"><span data-stu-id="9ef84-137">If timeout is not set, it defaults to 30 seconds.</span></span>

### <a name="response"></a><span data-ttu-id="9ef84-138">Antwoord</span><span class="sxs-lookup"><span data-stu-id="9ef84-138">Response</span></span>
<span data-ttu-id="9ef84-139">De back-end-app ontvangt een antwoord dat bestaat uit:</span><span class="sxs-lookup"><span data-stu-id="9ef84-139">The back-end app receives a response which comprises:</span></span>

* <span data-ttu-id="9ef84-140">*HTTP-statuscode*, die wordt gebruikt voor fouten die afkomstig zijn van de IoT-Hub, met inbegrip van een 404-fout voor apparaten die momenteel niet verbonden</span><span class="sxs-lookup"><span data-stu-id="9ef84-140">*HTTP status code*, which is used for errors coming from the IoT Hub, including a 404 error for devices not currently connected</span></span>
* <span data-ttu-id="9ef84-141">*Headers* waarop de ETag bevatten, aanvraag-ID, het type inhoud en de codering van inhoud</span><span class="sxs-lookup"><span data-stu-id="9ef84-141">*Headers* which contain the ETag, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="9ef84-142">Een JSON *hoofdtekst* in de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="9ef84-142">A JSON *body* in the following format:</span></span>

```
{
    "status" : 201,
    "payload" : {...}
}
```

   <span data-ttu-id="9ef84-143">Beide `status` en `body` zijn geleverd door het apparaat en gebruikt om met de statuscode van het apparaat en/of beschrijving te reageren.</span><span class="sxs-lookup"><span data-stu-id="9ef84-143">Both `status` and `body` are provided by the device and used to respond with the device's own status code and/or description.</span></span>

## <a name="handle-a-direct-method-on-a-device"></a><span data-ttu-id="9ef84-144">Verwerken van een directe methode op een apparaat</span><span class="sxs-lookup"><span data-stu-id="9ef84-144">Handle a direct method on a device</span></span>
### <a name="method-invocation"></a><span data-ttu-id="9ef84-145">De methodeaanroep</span><span class="sxs-lookup"><span data-stu-id="9ef84-145">Method invocation</span></span>
<span data-ttu-id="9ef84-146">Directe methodeaanvragen in het onderwerp MQTT, ontvangen apparaten:`$iothub/methods/POST/{method name}/?$rid={request id}`</span><span class="sxs-lookup"><span data-stu-id="9ef84-146">Devices receive direct method requests on the MQTT topic: `$iothub/methods/POST/{method name}/?$rid={request id}`</span></span>

<span data-ttu-id="9ef84-147">De instantie die het apparaat ontvangt is in de volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="9ef84-147">The body which the device receives is in the following format:</span></span>

```
{
    "input1": "someInput",
    "input2": "anotherInput"
}
```

<span data-ttu-id="9ef84-148">Methodeaanvragen zijn QoS 0.</span><span class="sxs-lookup"><span data-stu-id="9ef84-148">Method requests are QoS 0.</span></span>

### <a name="response"></a><span data-ttu-id="9ef84-149">Antwoord</span><span class="sxs-lookup"><span data-stu-id="9ef84-149">Response</span></span>
<span data-ttu-id="9ef84-150">Het apparaat verzendt reacties naar `$iothub/methods/res/{status}/?$rid={request id}`, waarbij:</span><span class="sxs-lookup"><span data-stu-id="9ef84-150">The device sends responses to `$iothub/methods/res/{status}/?$rid={request id}`, where:</span></span>

* <span data-ttu-id="9ef84-151">De `status` eigenschap is de status apparaat opgegeven van de methode kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="9ef84-151">The `status` property is the device-supplied status of method execution.</span></span>
* <span data-ttu-id="9ef84-152">De `$rid` eigenschap is de aanvraag-ID van het aanroepen van de methode heeft ontvangen van IoT-Hub.</span><span class="sxs-lookup"><span data-stu-id="9ef84-152">The `$rid` property is the request ID from the method invocation received from IoT Hub.</span></span>

<span data-ttu-id="9ef84-153">De hoofdtekst kan is ingesteld door het apparaat en geen status.</span><span class="sxs-lookup"><span data-stu-id="9ef84-153">The body is set by the device and can be any status.</span></span>

## <a name="additional-reference-material"></a><span data-ttu-id="9ef84-154">Aanvullende referentiemateriaal</span><span class="sxs-lookup"><span data-stu-id="9ef84-154">Additional reference material</span></span>
<span data-ttu-id="9ef84-155">Er zijn andere onderwerpen waarnaar wordt verwezen in de IoT Hub developer guide:</span><span class="sxs-lookup"><span data-stu-id="9ef84-155">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="9ef84-156">[IoT-hubeindpunten] [ lnk-endpoints] beschrijft de verschillende eindpunten die elke IoT-hub voor runtime- en beheerbewerkingen toont.</span><span class="sxs-lookup"><span data-stu-id="9ef84-156">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="9ef84-157">[Bandbreedtebeperking en quota's] [ lnk-quotas] beschrijving van de quota die betrekking hebben op de IoT Hub-service en het gedrag bandbreedteregeling kunt verwachten wanneer u de service gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9ef84-157">[Throttling and quotas][lnk-quotas] describes the quotas that apply to the IoT Hub service and the throttling behavior to expect when you use the service.</span></span>
* <span data-ttu-id="9ef84-158">[Azure IoT-SDKs voor apparaat en de service] [ lnk-sdks] geeft een lijst van de verschillende SDK's kunt u bij het ontwikkelen van apps voor het apparaat en de service die communiceren met IoT Hub-taal.</span><span class="sxs-lookup"><span data-stu-id="9ef84-158">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="9ef84-159">[IoT Hub-querytaal voor apparaat horende, taken en berichtroutering] [ lnk-query] beschrijft de IoT Hub-querytaal kunt u gegevens ophalen uit IoT Hub over uw apparaat horende en taken.</span><span class="sxs-lookup"><span data-stu-id="9ef84-159">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes the IoT Hub query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="9ef84-160">[Ondersteuning voor IoT Hub MQTT] [ lnk-devguide-mqtt] meer informatie over IoT Hub ondersteuning biedt voor het MQTT-protocol.</span><span class="sxs-lookup"><span data-stu-id="9ef84-160">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ef84-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9ef84-161">Next steps</span></span>
<span data-ttu-id="9ef84-162">Nu u hebt geleerd hoe u directe methoden kunt gebruiken, kunt u mogelijk geïnteresseerd in het volgende onderwerp van IoT Hub developer guide:</span><span class="sxs-lookup"><span data-stu-id="9ef84-162">Now you have learned how to use direct methods, you may be interested in the following IoT Hub developer guide topic:</span></span>

* <span data-ttu-id="9ef84-163">[Taken plannen op meerdere apparaten][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="9ef84-163">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="9ef84-164">Als u wilt uitproberen enkele concepten die in dit artikel wordt beschreven, kunt u mogelijk geïnteresseerd in de volgende IoT Hub-zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="9ef84-164">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorial:</span></span>

* <span data-ttu-id="9ef84-165">[Directe methoden gebruiken][lnk-methods-tutorial]</span><span class="sxs-lookup"><span data-stu-id="9ef84-165">[Use direct methods][lnk-methods-tutorial]</span></span>

<!-- links and images -->

[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md

[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-devguide-messages]: iot-hub-devguide-messaging.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
