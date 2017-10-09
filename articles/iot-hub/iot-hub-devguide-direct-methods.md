---
title: Azure IoT Hub aaaUnderstand directe methoden | Microsoft Docs
description: Handleiding voor ontwikkelaars - code voor gebruik rechtstreeks methoden tooinvoke op uw apparaten vanuit een app service.
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
ms.openlocfilehash: 0d15d44a0c3e1d1cda1669c1ed011c2f932e3d92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-invoke-direct-methods-from-iot-hub"></a><span data-ttu-id="51aa8-103">Begrijpen en direct methoden uit IoT Hub aanroepen</span><span class="sxs-lookup"><span data-stu-id="51aa8-103">Understand and invoke direct methods from IoT Hub</span></span>
## <a name="overview"></a><span data-ttu-id="51aa8-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="51aa8-104">Overview</span></span>
<span data-ttu-id="51aa8-105">IoT Hub, hebt u mogelijkheid tooinvoke rechtstreekse methoden op apparaten van Hallo cloud.</span><span class="sxs-lookup"><span data-stu-id="51aa8-105">IoT Hub gives you ability tooinvoke direct methods on devices from hello cloud.</span></span> <span data-ttu-id="51aa8-106">Rechtstreekse methoden vertegenwoordigen een request-reply interactie met een apparaat vergelijkbare tooan HTTP aanroepen in dat ze slagen of mislukken onmiddellijk (na een door de gebruiker opgegeven time).</span><span class="sxs-lookup"><span data-stu-id="51aa8-106">Direct methods represent a request-reply interaction with a device similar tooan HTTP call in that they succeed or fail immediately (after a user-specified timeout).</span></span> <span data-ttu-id="51aa8-107">Dit is nuttig voor scenario's waarin Hallo loop van de directe actie verschillend, afhankelijk van of Hallo apparaat kunnen toorespond, zoals een SMS wake-up tooa apparaat verzenden als een apparaat is offline (SMS wordt duurder dan een methodeaanroep van) is.</span><span class="sxs-lookup"><span data-stu-id="51aa8-107">This is useful for scenarios where hello course of immediate action is different depending on whether hello device was able toorespond, such as sending an SMS wake-up tooa device if a device is offline (SMS being more expensive than a method call).</span></span>

<span data-ttu-id="51aa8-108">Elke methode apparaat gericht op één apparaat.</span><span class="sxs-lookup"><span data-stu-id="51aa8-108">Each device method targets a single device.</span></span> <span data-ttu-id="51aa8-109">[Taken] [ lnk-devguide-jobs] plannen methodeaanroep voor niet-verbonden apparaten en bieden een manier tooinvoke rechtstreekse methoden op meerdere apparaten.</span><span class="sxs-lookup"><span data-stu-id="51aa8-109">[Jobs][lnk-devguide-jobs] provide a way tooinvoke direct methods on multiple devices, and schedule method invocation for disconnected devices.</span></span>

<span data-ttu-id="51aa8-110">Iedereen met **service verbinding** machtigingen voor IoT Hub kunnen een methode aangeroepen voor een apparaat.</span><span class="sxs-lookup"><span data-stu-id="51aa8-110">Anyone with **service connect** permissions on IoT Hub may invoke a method on a device.</span></span>

### <a name="when-toouse"></a><span data-ttu-id="51aa8-111">Wanneer toouse</span><span class="sxs-lookup"><span data-stu-id="51aa8-111">When toouse</span></span>
<span data-ttu-id="51aa8-112">Methoden voor direct een reactie op aanvragen patroon volgen en zijn bedoeld voor communicaties die direct bevestiging van hun resultaat, meestal interactieve besturingselement van het Hallo-apparaat, bijvoorbeeld tooturn op een ventilator vereisen.</span><span class="sxs-lookup"><span data-stu-id="51aa8-112">Direct methods follow a request-response pattern and are meant for communications that require immediate confirmation of their result, usually interactive control of hello device, for example tooturn on a fan.</span></span>

<span data-ttu-id="51aa8-113">Raadpleeg te[Cloud-naar-apparaat communicatie richtlijnen] [ lnk-c2d-guidance] als u twijfelt tussen het gebruik van de eigenschappen van de gewenste directe methoden of cloud-naar-apparaat-berichten.</span><span class="sxs-lookup"><span data-stu-id="51aa8-113">Refer too[Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using desired properties, direct methods, or cloud-to-device messages.</span></span>

## <a name="method-lifecycle"></a><span data-ttu-id="51aa8-114">De levenscyclus van de methode</span><span class="sxs-lookup"><span data-stu-id="51aa8-114">Method lifecycle</span></span>
<span data-ttu-id="51aa8-115">Rechtstreekse methoden op Hallo apparaat worden geïmplementeerd en is mogelijk nul of meer invoerwaarden in Hallo methode nettolading toocorrectly instantiëren.</span><span class="sxs-lookup"><span data-stu-id="51aa8-115">Direct methods are implemented on hello device and may require zero or more inputs in hello method payload toocorrectly instantiate.</span></span> <span data-ttu-id="51aa8-116">Aanroepen van een directe methode via een URI service gerichte (`{iot hub}/twins/{device id}/methods/`).</span><span class="sxs-lookup"><span data-stu-id="51aa8-116">You invoke a direct method through a service-facing URI (`{iot hub}/twins/{device id}/methods/`).</span></span> <span data-ttu-id="51aa8-117">Een apparaat ontvangt rechtstreekse methoden door een apparaat-specifieke MQTT onderwerp (`$iothub/methods/POST/{method name}/`).</span><span class="sxs-lookup"><span data-stu-id="51aa8-117">A device receives direct methods through a device-specific MQTT topic (`$iothub/methods/POST/{method name}/`).</span></span> <span data-ttu-id="51aa8-118">We kunnen op extra apparaten aan clientzijde netwerkprotocollen in toekomstige Hallo ondersteuning voor directe methoden.</span><span class="sxs-lookup"><span data-stu-id="51aa8-118">We may support direct methods on additional device-side networking protocols in hello future.</span></span>

> [!NOTE]
> <span data-ttu-id="51aa8-119">Wanneer u een directe methode voor een apparaat aangeroepen, namen en waarden mogen alleen US-ASCII-afdrukbare alfanumerieke behalve aanwezig in de volgende set Hallo: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span><span class="sxs-lookup"><span data-stu-id="51aa8-119">When you invoke a direct method on a device, property names and values can only contain US-ASCII printable alphanumeric, except any in hello following set: ``{'$', '(', ')', '<', '>', '@', ',', ';', ':', '\', '"', '/', '[', ']', '?', '=', '{', '}', SP, HT}``.</span></span>
> 
> 

<span data-ttu-id="51aa8-120">Directe methoden zijn synchrone en een slagen of mislukken na de time-outperiode hello (standaard: 30 seconden, instelbare up too3600 seconden).</span><span class="sxs-lookup"><span data-stu-id="51aa8-120">Direct methods are synchronous and either succeed or fail after hello timeout period (default: 30 seconds, settable up too3600 seconds).</span></span> <span data-ttu-id="51aa8-121">Directe methoden zijn nuttig in interactieve scenario's waar u een apparaat tooact als Hallo-apparaat online en ontvangende opdrachten is, zoals het inschakelen van een licht via een telefoon.</span><span class="sxs-lookup"><span data-stu-id="51aa8-121">Direct methods are useful in interactive scenarios where you want a device tooact if and only if hello device is online and receiving commands, such as turning on a light from a phone.</span></span> <span data-ttu-id="51aa8-122">In deze scenario's gewenste toosee een onmiddellijke slagen of mislukken zodat Hallo cloudservice zo snel mogelijk op Hallo resultaat kan reageren.</span><span class="sxs-lookup"><span data-stu-id="51aa8-122">In these scenarios, you want toosee an immediate success or failure so hello cloud service can act on hello result as soon as possible.</span></span> <span data-ttu-id="51aa8-123">Hallo-apparaat kan sommige berichttekst als gevolg van het Hallo-methode retourneren, maar het is niet vereist voor Hallo methode toodo zodat.</span><span class="sxs-lookup"><span data-stu-id="51aa8-123">hello device may return some message body as a result of hello method, but it isn't required for hello method toodo so.</span></span> <span data-ttu-id="51aa8-124">Er is geen garantie op volgorde of eventuele semantiek gelijktijdigheid van taken op methodeaanroepen.</span><span class="sxs-lookup"><span data-stu-id="51aa8-124">There is no guarantee on ordering or any concurrency semantics on method calls.</span></span>

<span data-ttu-id="51aa8-125">Directe methode zijn HTTP-only van Hallo cloud kant en MQTT alleen-lezen van Hallo apparaat kant.</span><span class="sxs-lookup"><span data-stu-id="51aa8-125">Direct method are HTTP-only from hello cloud side, and MQTT-only from hello device side.</span></span>

<span data-ttu-id="51aa8-126">Hallo-nettolading voor methodeaanvragen en antwoorden is een JSON-document van too8KB.</span><span class="sxs-lookup"><span data-stu-id="51aa8-126">hello payload for method requests and responses is a JSON document up too8KB.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="51aa8-127">De onderwerpen waarnaar wordt verwezen:</span><span class="sxs-lookup"><span data-stu-id="51aa8-127">Reference topics:</span></span>
<span data-ttu-id="51aa8-128">Hallo bieden volgende naslagonderwerpen u meer informatie over het gebruik van rechtstreekse methoden.</span><span class="sxs-lookup"><span data-stu-id="51aa8-128">hello following reference topics provide you with more information about using direct methods.</span></span>

## <a name="invoke-a-direct-method-from-a-back-end-app"></a><span data-ttu-id="51aa8-129">Aanroepen van een directe methode van een back-endserver voor apps</span><span class="sxs-lookup"><span data-stu-id="51aa8-129">Invoke a direct method from a back-end app</span></span>
### <a name="method-invocation"></a><span data-ttu-id="51aa8-130">De methodeaanroep</span><span class="sxs-lookup"><span data-stu-id="51aa8-130">Method invocation</span></span>
<span data-ttu-id="51aa8-131">Directe methode aanroepen op een apparaat zijn HTTP-aanroepen die bestaan uit:</span><span class="sxs-lookup"><span data-stu-id="51aa8-131">Direct method invocations on a device are HTTP calls which comprise:</span></span>

* <span data-ttu-id="51aa8-132">Hallo *URI* specifieke toohello apparaat (`{iot hub}/twins/{device id}/methods/`)</span><span class="sxs-lookup"><span data-stu-id="51aa8-132">hello *URI* specific toohello device (`{iot hub}/twins/{device id}/methods/`)</span></span>
* <span data-ttu-id="51aa8-133">Hallo POST *methode*</span><span class="sxs-lookup"><span data-stu-id="51aa8-133">hello POST *method*</span></span>
* <span data-ttu-id="51aa8-134">*Headers* waarop Hallo autorisatie bevatten, aanvraag-ID, het type inhoud en de codering van inhoud</span><span class="sxs-lookup"><span data-stu-id="51aa8-134">*Headers* which contain hello authorization, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="51aa8-135">Een transparante JSON *hoofdtekst* in Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="51aa8-135">A transparent JSON *body* in hello following format:</span></span>

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

<span data-ttu-id="51aa8-136">Er is een time-out in seconden.</span><span class="sxs-lookup"><span data-stu-id="51aa8-136">Timeout is in seconds.</span></span> <span data-ttu-id="51aa8-137">Als u time-out niet is ingesteld, wordt standaard too30 seconden.</span><span class="sxs-lookup"><span data-stu-id="51aa8-137">If timeout is not set, it defaults too30 seconds.</span></span>

### <a name="response"></a><span data-ttu-id="51aa8-138">Antwoord</span><span class="sxs-lookup"><span data-stu-id="51aa8-138">Response</span></span>
<span data-ttu-id="51aa8-139">Hallo back-end app ontvangt een antwoord dat bestaat uit:</span><span class="sxs-lookup"><span data-stu-id="51aa8-139">hello back-end app receives a response which comprises:</span></span>

* <span data-ttu-id="51aa8-140">*HTTP-statuscode*, die wordt gebruikt voor fouten die afkomstig zijn van Hallo IoT Hub, met inbegrip van een 404-fout voor apparaten die momenteel niet verbonden</span><span class="sxs-lookup"><span data-stu-id="51aa8-140">*HTTP status code*, which is used for errors coming from hello IoT Hub, including a 404 error for devices not currently connected</span></span>
* <span data-ttu-id="51aa8-141">*Headers* waarop Hallo ETag bevatten, aanvraag-ID, het type inhoud en de codering van inhoud</span><span class="sxs-lookup"><span data-stu-id="51aa8-141">*Headers* which contain hello ETag, request ID, content type, and content encoding</span></span>
* <span data-ttu-id="51aa8-142">Een JSON *hoofdtekst* in Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="51aa8-142">A JSON *body* in hello following format:</span></span>

```
{
    "status" : 201,
    "payload" : {...}
}
```

   <span data-ttu-id="51aa8-143">Beide `status` en `body` worden geleverd door het Hallo-apparaat en toorespond gebruikt met de statuscode van Hallo van het apparaat en/of beschrijving.</span><span class="sxs-lookup"><span data-stu-id="51aa8-143">Both `status` and `body` are provided by hello device and used toorespond with hello device's own status code and/or description.</span></span>

## <a name="handle-a-direct-method-on-a-device"></a><span data-ttu-id="51aa8-144">Verwerken van een directe methode op een apparaat</span><span class="sxs-lookup"><span data-stu-id="51aa8-144">Handle a direct method on a device</span></span>
### <a name="method-invocation"></a><span data-ttu-id="51aa8-145">De methodeaanroep</span><span class="sxs-lookup"><span data-stu-id="51aa8-145">Method invocation</span></span>
<span data-ttu-id="51aa8-146">Apparaten ontvangen directe methode-aanvragen op Hallo MQTT onderwerp:`$iothub/methods/POST/{method name}/?$rid={request id}`</span><span class="sxs-lookup"><span data-stu-id="51aa8-146">Devices receive direct method requests on hello MQTT topic: `$iothub/methods/POST/{method name}/?$rid={request id}`</span></span>

<span data-ttu-id="51aa8-147">Hallo hoofdtekst welk apparaat Hallo ontvangt heeft Hallo volgende indeling:</span><span class="sxs-lookup"><span data-stu-id="51aa8-147">hello body which hello device receives is in hello following format:</span></span>

```
{
    "input1": "someInput",
    "input2": "anotherInput"
}
```

<span data-ttu-id="51aa8-148">Methodeaanvragen zijn QoS 0.</span><span class="sxs-lookup"><span data-stu-id="51aa8-148">Method requests are QoS 0.</span></span>

### <a name="response"></a><span data-ttu-id="51aa8-149">Antwoord</span><span class="sxs-lookup"><span data-stu-id="51aa8-149">Response</span></span>
<span data-ttu-id="51aa8-150">Hallo apparaat verzendt reacties te`$iothub/methods/res/{status}/?$rid={request id}`, waarbij:</span><span class="sxs-lookup"><span data-stu-id="51aa8-150">hello device sends responses too`$iothub/methods/res/{status}/?$rid={request id}`, where:</span></span>

* <span data-ttu-id="51aa8-151">Hallo `status` eigenschap Hallo apparaat opgegeven status van de uitvoering van de methode is.</span><span class="sxs-lookup"><span data-stu-id="51aa8-151">hello `status` property is hello device-supplied status of method execution.</span></span>
* <span data-ttu-id="51aa8-152">Hallo `$rid` eigenschap Hallo aanvraag-ID van de methodeaanroep Hallo ontvangen van IoT Hub is.</span><span class="sxs-lookup"><span data-stu-id="51aa8-152">hello `$rid` property is hello request ID from hello method invocation received from IoT Hub.</span></span>

<span data-ttu-id="51aa8-153">Hallo-instantie is ingesteld door Hallo-apparaat en elke status kunt worden.</span><span class="sxs-lookup"><span data-stu-id="51aa8-153">hello body is set by hello device and can be any status.</span></span>

## <a name="additional-reference-material"></a><span data-ttu-id="51aa8-154">Aanvullende referentiemateriaal</span><span class="sxs-lookup"><span data-stu-id="51aa8-154">Additional reference material</span></span>
<span data-ttu-id="51aa8-155">Er zijn andere onderwerpen met naslaginformatie in Hallo Ontwikkelaarshandleiding voor IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="51aa8-155">Other reference topics in hello IoT Hub developer guide include:</span></span>

* <span data-ttu-id="51aa8-156">[IoT-hubeindpunten] [ lnk-endpoints] beschrijft Hallo verschillende eindpunten die elke IoT-hub voor runtime- en beheerbewerkingen toont.</span><span class="sxs-lookup"><span data-stu-id="51aa8-156">[IoT Hub endpoints][lnk-endpoints] describes hello various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="51aa8-157">[Bandbreedtebeperking en quota's] [ lnk-quotas] beschrijft Hallo quota's die van toepassing toohello service IoT Hub en bandbreedteregeling gedrag tooexpect Hallo wanneer u Hallo-service gebruiken.</span><span class="sxs-lookup"><span data-stu-id="51aa8-157">[Throttling and quotas][lnk-quotas] describes hello quotas that apply toohello IoT Hub service and hello throttling behavior tooexpect when you use hello service.</span></span>
* <span data-ttu-id="51aa8-158">[Azure IoT-SDKs voor apparaat en de service] [ lnk-sdks] lijsten Hallo verschillende taal kunt u bij het ontwikkelen van apps voor het apparaat en de service die communiceren met IoT Hub SDK's.</span><span class="sxs-lookup"><span data-stu-id="51aa8-158">[Azure IoT device and service SDKs][lnk-sdks] lists hello various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="51aa8-159">[IoT Hub-querytaal voor apparaat horende, taken en berichtroutering] [ lnk-query] Hallo querytaal IoT-Hub kunt u informatie van de tooretrieve uit IoT Hub over uw apparaat horende en taken worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="51aa8-159">[IoT Hub query language for device twins, jobs, and message routing][lnk-query] describes hello IoT Hub query language you can use tooretrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="51aa8-160">[Ondersteuning voor IoT Hub MQTT] [ lnk-devguide-mqtt] meer informatie over IoT Hub ondersteuning biedt voor Hallo MQTT protocol.</span><span class="sxs-lookup"><span data-stu-id="51aa8-160">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for hello MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="51aa8-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="51aa8-161">Next steps</span></span>
<span data-ttu-id="51aa8-162">Nu hebt u geleerd hoe toouse direct methoden, hebt u mogelijk geïnteresseerd in Hallo IoT Hub developer guide onderwerp te volgen:</span><span class="sxs-lookup"><span data-stu-id="51aa8-162">Now you have learned how toouse direct methods, you may be interested in hello following IoT Hub developer guide topic:</span></span>

* <span data-ttu-id="51aa8-163">[Taken plannen op meerdere apparaten][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="51aa8-163">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="51aa8-164">Als u tootry sommige Hallo concepten die in dit artikel wordt beschreven wilt, kunt u mogelijk geïnteresseerd in Hallo IoT Hub-zelfstudie:</span><span class="sxs-lookup"><span data-stu-id="51aa8-164">If you would like tootry out some of hello concepts described in this article, you may be interested in hello following IoT Hub tutorial:</span></span>

* <span data-ttu-id="51aa8-165">[Directe methoden gebruiken][lnk-methods-tutorial]</span><span class="sxs-lookup"><span data-stu-id="51aa8-165">[Use direct methods][lnk-methods-tutorial]</span></span>

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
