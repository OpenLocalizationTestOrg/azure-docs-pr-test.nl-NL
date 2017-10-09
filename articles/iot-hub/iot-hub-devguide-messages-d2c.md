---
title: aaaUnderstand Azure IoT Hub apparaat-naar-cloud messaging | Microsoft Docs
description: Handleiding voor ontwikkelaars - hoe toouse apparaat-naar-cloud-berichten met IoT Hub. Bevat informatie over het verzenden van Telemetrie- en niet-telemtry gegevens en het gebruik van toodeliver routeren van berichten.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 07dc8a6be747365c7efbc528ab2762b0d9790758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="send-device-to-cloud-messages-tooiot-hub"></a><span data-ttu-id="8e300-104">Apparaat-naar-cloudberichten tooIoT Hub te verzenden</span><span class="sxs-lookup"><span data-stu-id="8e300-104">Send device-to-cloud messages tooIoT Hub</span></span>

<span data-ttu-id="8e300-105">toosend tijdreeks Telemetrie en waarschuwingen van uw apparaten tooyour back-end oplossing, kunt u de apparaat-naar-cloud-berichten verzenden van uw apparaat tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="8e300-105">toosend time-series telemetry and alerts from your devices tooyour solution back end, send device-to-cloud messages from your device tooyour IoT hub.</span></span> <span data-ttu-id="8e300-106">Zie voor een beschrijving van de andere ondersteund door de IoT Hub apparaat-naar-cloud-opties, [apparaat-naar-cloud communicatie richtlijnen][lnk-d2c-guidance].</span><span class="sxs-lookup"><span data-stu-id="8e300-106">For a discussion of other device-to-cloud options supported by IoT Hub, see [Device-to-cloud communications guidance][lnk-d2c-guidance].</span></span>

<span data-ttu-id="8e300-107">U apparaat-naar-cloud-berichten verzenden via een apparaat gerichte-eindpunt (**/devices/ {deviceId} / berichten/gebeurtenissen**).</span><span class="sxs-lookup"><span data-stu-id="8e300-107">You send device-to-cloud messages through a device-facing endpoint (**/devices/{deviceId}/messages/events**).</span></span> <span data-ttu-id="8e300-108">Routering van regels en vervolgens uw berichten tooone Hallo service gerichte eindpunten op uw IoT-hub te routeren.</span><span class="sxs-lookup"><span data-stu-id="8e300-108">Routing rules then route your messages tooone of hello service-facing endpoints on your IoT hub.</span></span> <span data-ttu-id="8e300-109">Routeringsregels gebruiken Hallo kopteksten en de hoofdtekst van hello apparaat-naar-cloud-berichten die door uw hub toodetermine waar tooroute ze.</span><span class="sxs-lookup"><span data-stu-id="8e300-109">Routing rules use hello headers and body of hello device-to-cloud messages flowing through your hub toodetermine where tooroute them.</span></span> <span data-ttu-id="8e300-110">Berichten zijn standaard gerouteerde toohello ingebouwde gerichte service-eindpunt (**berichten/gebeurtenissen**), die compatibel is met [Event Hubs][lnk-event-hubs].</span><span class="sxs-lookup"><span data-stu-id="8e300-110">By default, messages are routed toohello built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="8e300-111">Daarom kunt u standaard [Event Hubs-integratie en SDK's] [ lnk-compatible-endpoint] tooreceive apparaat-naar-cloud-berichten in uw oplossing voor back-end.</span><span class="sxs-lookup"><span data-stu-id="8e300-111">Therefore, you can use standard [Event Hubs integration and SDKs][lnk-compatible-endpoint] tooreceive device-to-cloud messages in your solution back end.</span></span>

<span data-ttu-id="8e300-112">IoT Hub implementeert apparaat-naar-cloud-berichten met behulp van een streaming messaging-patroon.</span><span class="sxs-lookup"><span data-stu-id="8e300-112">IoT Hub implements device-to-cloud messaging using a streaming messaging pattern.</span></span> <span data-ttu-id="8e300-113">IoT-Hub apparaat-naar-cloudberichten lijken meer op [Event Hubs] [ lnk-event-hubs] *gebeurtenissen* dan [Service Bus] [ lnk-servicebus] *berichten* dat er wordt een groot aantal gebeurtenissen Hallo-service die kan worden gelezen door meerdere lezers te doorlopen.</span><span class="sxs-lookup"><span data-stu-id="8e300-113">IoT Hub's device-to-cloud messages are more like [Event Hubs][lnk-event-hubs] *events* than [Service Bus][lnk-servicebus] *messages* in that there is a high volume of events passing through hello service that can be read by multiple readers.</span></span>

<span data-ttu-id="8e300-114">Apparaat-naar-cloud-berichten met IoT Hub heeft Hallo volgende kenmerken:</span><span class="sxs-lookup"><span data-stu-id="8e300-114">Device-to-cloud messaging with IoT Hub has hello following characteristics:</span></span>

* <span data-ttu-id="8e300-115">Apparaat-naar-cloud-berichten worden duurzame en bewaard in een IoT-hub standaard **berichten/gebeurtenissen** eindpunt voor tooseven dagen.</span><span class="sxs-lookup"><span data-stu-id="8e300-115">Device-to-cloud messages are durable and retained in an IoT hub's default **messages/events** endpoint for up tooseven days.</span></span>
* <span data-ttu-id="8e300-116">Apparaat-naar-cloud-berichten kunnen niet groter zijn dan 256 KB en kunnen worden gegroepeerd in batches toooptimize verzendt.</span><span class="sxs-lookup"><span data-stu-id="8e300-116">Device-to-cloud messages can be at most 256 KB, and can be grouped in batches toooptimize sends.</span></span> <span data-ttu-id="8e300-117">Batches mag hoogstens 256 KB.</span><span class="sxs-lookup"><span data-stu-id="8e300-117">Batches can be at most 256 KB.</span></span>
* <span data-ttu-id="8e300-118">Zoals uitgelegd in Hallo [besturingselement toegang tooIoT Hub] [ lnk-devguide-security] gedeelte, IoT-Hub kunt per apparaat authenticatie en toegangsbeheer.</span><span class="sxs-lookup"><span data-stu-id="8e300-118">As explained in hello [Control access tooIoT Hub][lnk-devguide-security] section, IoT Hub enables per-device authentication and access control.</span></span>
* <span data-ttu-id="8e300-119">IoT-Hub kunt u toocreate too10 aangepaste eindpunten.</span><span class="sxs-lookup"><span data-stu-id="8e300-119">IoT Hub allows you toocreate up too10 custom endpoints.</span></span> <span data-ttu-id="8e300-120">Berichten worden afgeleverd toohello eindpunten op basis van de routes geconfigureerd op uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="8e300-120">Messages are delivered toohello endpoints based on routes configured on your IoT hub.</span></span> <span data-ttu-id="8e300-121">Zie voor meer informatie [routering regels](#routing-rules).</span><span class="sxs-lookup"><span data-stu-id="8e300-121">For more information, see [Routing rules](#routing-rules).</span></span>
* <span data-ttu-id="8e300-122">IoT-Hub kunt miljoenen gelijktijdig verbonden apparaten (Zie [quota's en beperking][lnk-quotas]).</span><span class="sxs-lookup"><span data-stu-id="8e300-122">IoT Hub enables millions of simultaneously connected devices (see [Quotas and throttling][lnk-quotas]).</span></span>
* <span data-ttu-id="8e300-123">IoT Hub is niet toegestaan voor het partitioneren van willekeurige.</span><span class="sxs-lookup"><span data-stu-id="8e300-123">IoT Hub does not allow arbitrary partitioning.</span></span> <span data-ttu-id="8e300-124">Apparaat-naar-cloud-berichten worden gepartitioneerd op basis van hun oorspronkelijke **deviceId**.</span><span class="sxs-lookup"><span data-stu-id="8e300-124">Device-to-cloud messages are partitioned based on their originating **deviceId**.</span></span>

<span data-ttu-id="8e300-125">Zie voor meer informatie over de verschillen tussen Hallo IoT Hub en Event Hubs-services Hallo [vergelijking van Azure IoT Hub en Azure Event Hubs][lnk-comparison].</span><span class="sxs-lookup"><span data-stu-id="8e300-125">For more information about hello differences between hello IoT Hub and Event Hubs services, see [Comparison of Azure IoT Hub and Azure Event Hubs][lnk-comparison].</span></span>

## <a name="send-non-telemetry-traffic"></a><span data-ttu-id="8e300-126">Niet-telemetrie verkeer verzenden</span><span class="sxs-lookup"><span data-stu-id="8e300-126">Send non-telemetry traffic</span></span>

<span data-ttu-id="8e300-127">Vaak bovendien tootelemetry gegevenspunten, apparaten verzenden van berichten en aanvragen die afzonderlijke uitvoering en verwerking in Hallo back-end oplossing vereisen.</span><span class="sxs-lookup"><span data-stu-id="8e300-127">Often, in addition tootelemetry data points, devices send messages and requests that require separate execution and handling in hello solution back end.</span></span> <span data-ttu-id="8e300-128">Bijvoorbeeld, back kritieke waarschuwingen die een specifieke actie in Hallo moeten activeren-end.</span><span class="sxs-lookup"><span data-stu-id="8e300-128">For example, critical alerts that must trigger a specific action in hello back end.</span></span> <span data-ttu-id="8e300-129">U kunt eenvoudig schrijven een [routeringsregel] [ lnk-devguide-custom] toosend deze typen berichten tooan eindpunt dedicated tootheir verwerking op basis van een koptekst op het Hallo-bericht of een waarde in de hoofdtekst van Hallo-bericht.</span><span class="sxs-lookup"><span data-stu-id="8e300-129">You can easily write a [routing rule][lnk-devguide-custom] toosend these types of messages tooan endpoint dedicated tootheir processing based on either a header on hello message or a value in hello message body.</span></span>

<span data-ttu-id="8e300-130">Zie voor meer informatie over Hallo aanbevolen manier tooprocess dit kind van bericht Hallo [zelfstudie: hoe tooprocess IoT Hub apparaat-naar-cloud-berichten] [ lnk-d2c-tutorial] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="8e300-130">For more information about hello best way tooprocess this kind of message, see hello [Tutorial: How tooprocess IoT Hub device-to-cloud messages][lnk-d2c-tutorial] tutorial.</span></span>

## <a name="route-device-to-cloud-messages"></a><span data-ttu-id="8e300-131">Apparaat-naar-cloud-berichten rondsturen</span><span class="sxs-lookup"><span data-stu-id="8e300-131">Route device-to-cloud messages</span></span>

<span data-ttu-id="8e300-132">U hebt twee opties voor routering apparaat-naar-cloudberichten tooyour back-end-apps:</span><span class="sxs-lookup"><span data-stu-id="8e300-132">You have two options for routing device-to-cloud messages tooyour back-end apps:</span></span>

* <span data-ttu-id="8e300-133">Gebruik Hallo ingebouwde [Event Hub-compatibele eindpunt] [ lnk-compatible-endpoint] tooenable back-end apps tooread Hallo apparaat-naar-cloud-berichten ontvangen door Hallo hub.</span><span class="sxs-lookup"><span data-stu-id="8e300-133">Use hello built-in [Event Hub-compatible endpoint][lnk-compatible-endpoint] tooenable back-end apps tooread hello device-to-cloud messages received by hello hub.</span></span> <span data-ttu-id="8e300-134">toolearn over ingebouwde Event Hub-compatibele eindpunt hello, Zie [apparaat-naar-cloud-berichten lezen uit Hallo ingebouwd eindpunt][lnk-devguide-builtin].</span><span class="sxs-lookup"><span data-stu-id="8e300-134">toolearn about hello built-in Event Hub-compatible endpoint, see [Read device-to-cloud messages from hello built-in endpoint][lnk-devguide-builtin].</span></span>
* <span data-ttu-id="8e300-135">Gebruik Routering regels toosend berichten toocustom eindpunten in uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="8e300-135">Use routing rules toosend messages toocustom endpoints in your IoT hub.</span></span> <span data-ttu-id="8e300-136">Aangepaste eindpunten inschakelen voor uw back-end apps tooread apparaat-naar-cloud-berichten met Event Hubs, Service Bus-wachtrijen of Service Bus-onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="8e300-136">Custom endpoints enable your back-end apps tooread device-to-cloud messages using Event Hubs, Service Bus queues, or Service Bus topics.</span></span> <span data-ttu-id="8e300-137">toolearn over Routering en aangepaste eindpunten, Zie [aangepaste eindpunten en routeringsregels gebruikt voor apparaat-naar-cloud-berichten][lnk-devguide-custom].</span><span class="sxs-lookup"><span data-stu-id="8e300-137">toolearn about routing and custom endpoints, see [Use custom endpoints and routing rules for device-to-cloud messages][lnk-devguide-custom].</span></span>

## <a name="anti-spoofing-properties"></a><span data-ttu-id="8e300-138">Eigenschappen anti-adresvervalsing (spoofing)</span><span class="sxs-lookup"><span data-stu-id="8e300-138">Anti-spoofing properties</span></span>

<span data-ttu-id="8e300-139">tooavoid apparaat vervalsing in IoT Hub apparaat-naar-cloud-berichten stempels alle berichten met Hallo volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="8e300-139">tooavoid device spoofing in device-to-cloud messages, IoT Hub stamps all messages with hello following properties:</span></span>

* <span data-ttu-id="8e300-140">**ConnectionDeviceId**</span><span class="sxs-lookup"><span data-stu-id="8e300-140">**ConnectionDeviceId**</span></span>
* <span data-ttu-id="8e300-141">**ConnectionDeviceGenerationId**</span><span class="sxs-lookup"><span data-stu-id="8e300-141">**ConnectionDeviceGenerationId**</span></span>
* <span data-ttu-id="8e300-142">**ConnectionAuthMethod**</span><span class="sxs-lookup"><span data-stu-id="8e300-142">**ConnectionAuthMethod**</span></span>

<span data-ttu-id="8e300-143">Hallo eerst twee bevatten Hallo **deviceId** en **generationId** Hallo die afkomstig zijn apparaat, conform [identiteit apparaateigenschappen][lnk-device-properties].</span><span class="sxs-lookup"><span data-stu-id="8e300-143">hello first two contain hello **deviceId** and **generationId** of hello originating device, as per [Device identity properties][lnk-device-properties].</span></span>

<span data-ttu-id="8e300-144">Hallo **ConnectionAuthMethod** eigenschap bevat een JSON-geserialiseerd object, hello volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="8e300-144">hello **ConnectionAuthMethod** property contains a JSON serialized object, with hello following properties:</span></span>

```json
{
  "scope": "{ hub | device}",
  "type": "{ symkey | sas}",
  "issuer": "iothub"
}
```

## <a name="next-steps"></a><span data-ttu-id="8e300-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8e300-145">Next steps</span></span>

<span data-ttu-id="8e300-146">Voor informatie over het Hallo-SDK's kunt u toosend apparaat-naar-cloud-berichten gebruiken, Zie [Azure IoT SDK's][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="8e300-146">For information about hello SDKs you can use toosend device-to-cloud messages, see [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="8e300-147">Hallo [aan de slag] [ lnk-get-started] zelfstudies ziet u hoe toosend apparaat-naar-cloud-berichten van gesimuleerde en fysieke apparaten.</span><span class="sxs-lookup"><span data-stu-id="8e300-147">hello [Get Started][lnk-get-started] tutorials show you how toosend device-to-cloud messages from both simulated and physical devices.</span></span> <span data-ttu-id="8e300-148">Zie voor meer details Hallo [proces IoT Hub apparaat-naar-cloud-berichten met behulp van routes] [ lnk-d2c-tutorial] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="8e300-148">For more detail, see hello [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

[lnk-devguide-builtin]: iot-hub-devguide-messages-read-builtin.md
[lnk-devguide-custom]: iot-hub-devguide-messages-read-custom.md
[lnk-comparison]: iot-hub-compare-event-hubs.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[lnk-get-started]: iot-hub-get-started.md

[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/
[lnk-servicebus]: http://azure.microsoft.com/documentation/services/service-bus/
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-compatible-endpoint]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-properties]: iot-hub-devguide-identity-registry.md#device-identity-properties
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
