---
title: Inzicht in Azure IoT Hub apparaat-naar-cloud messaging | Microsoft Docs
description: Handleiding voor ontwikkelaars - gebruiken met IoT Hub apparaat-naar-cloud-berichten. Bevat informatie over het verzenden van Telemetrie- en niet-telemtry gegevens, en routering gebruiken om berichten te bezorgen.
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
ms.openlocfilehash: d856e26084ee79386a2e8e0e527804bda86b477b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="send-device-to-cloud-messages-to-iot-hub"></a><span data-ttu-id="464b1-104">Apparaat-naar-cloud-berichten verzenden met IoT Hub</span><span class="sxs-lookup"><span data-stu-id="464b1-104">Send device-to-cloud messages to IoT Hub</span></span>

<span data-ttu-id="464b1-105">Voor het verzenden van telemetrie van de tijdreeks en waarschuwingen van uw apparaten naar de back-end van uw oplossing, apparaat-naar-cloud-berichten van uw apparaat te verzenden naar uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="464b1-105">To send time-series telemetry and alerts from your devices to your solution back end, send device-to-cloud messages from your device to your IoT hub.</span></span> <span data-ttu-id="464b1-106">Zie voor een beschrijving van de andere ondersteund door de IoT Hub apparaat-naar-cloud-opties, [apparaat-naar-cloud communicatie richtlijnen][lnk-d2c-guidance].</span><span class="sxs-lookup"><span data-stu-id="464b1-106">For a discussion of other device-to-cloud options supported by IoT Hub, see [Device-to-cloud communications guidance][lnk-d2c-guidance].</span></span>

<span data-ttu-id="464b1-107">U apparaat-naar-cloud-berichten verzenden via een apparaat gerichte-eindpunt (**/devices/ {deviceId} / berichten/gebeurtenissen**).</span><span class="sxs-lookup"><span data-stu-id="464b1-107">You send device-to-cloud messages through a device-facing endpoint (**/devices/{deviceId}/messages/events**).</span></span> <span data-ttu-id="464b1-108">Routering van regels en vervolgens uw berichten doorsturen naar een van de service gerichte eindpunten op uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="464b1-108">Routing rules then route your messages to one of the service-facing endpoints on your IoT hub.</span></span> <span data-ttu-id="464b1-109">Routeringsregels gebruiken de kopteksten en de hoofdtekst van de apparaat-naar-cloud-berichten die door uw hub bepalen waar ze doorsturen.</span><span class="sxs-lookup"><span data-stu-id="464b1-109">Routing rules use the headers and body of the device-to-cloud messages flowing through your hub to determine where to route them.</span></span> <span data-ttu-id="464b1-110">Standaard berichten worden doorgestuurd naar het ingebouwde gerichte service-eindpunt (**berichten/gebeurtenissen**), die compatibel is met [Event Hubs][lnk-event-hubs].</span><span class="sxs-lookup"><span data-stu-id="464b1-110">By default, messages are routed to the built-in service-facing endpoint (**messages/events**), that is compatible with [Event Hubs][lnk-event-hubs].</span></span> <span data-ttu-id="464b1-111">Daarom kunt u standaard [Event Hubs-integratie en SDK's] [ lnk-compatible-endpoint] apparaat-naar-cloud-berichten ontvangen in de back-end van uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="464b1-111">Therefore, you can use standard [Event Hubs integration and SDKs][lnk-compatible-endpoint] to receive device-to-cloud messages in your solution back end.</span></span>

<span data-ttu-id="464b1-112">IoT Hub implementeert apparaat-naar-cloud-berichten met behulp van een streaming messaging-patroon.</span><span class="sxs-lookup"><span data-stu-id="464b1-112">IoT Hub implements device-to-cloud messaging using a streaming messaging pattern.</span></span> <span data-ttu-id="464b1-113">IoT-Hub apparaat-naar-cloudberichten lijken meer op [Event Hubs] [ lnk-event-hubs] *gebeurtenissen* dan [Service Bus] [ lnk-servicebus] *berichten* dat er wordt een groot aantal gebeurtenissen dat door de service die kan worden gelezen door meerdere lezers.</span><span class="sxs-lookup"><span data-stu-id="464b1-113">IoT Hub's device-to-cloud messages are more like [Event Hubs][lnk-event-hubs] *events* than [Service Bus][lnk-servicebus] *messages* in that there is a high volume of events passing through the service that can be read by multiple readers.</span></span>

<span data-ttu-id="464b1-114">Apparaat-naar-cloud-berichten met IoT Hub heeft de volgende kenmerken:</span><span class="sxs-lookup"><span data-stu-id="464b1-114">Device-to-cloud messaging with IoT Hub has the following characteristics:</span></span>

* <span data-ttu-id="464b1-115">Apparaat-naar-cloud-berichten worden duurzame en bewaard in een IoT-hub standaard **berichten/gebeurtenissen** eindpunt voor maximaal zeven dagen.</span><span class="sxs-lookup"><span data-stu-id="464b1-115">Device-to-cloud messages are durable and retained in an IoT hub's default **messages/events** endpoint for up to seven days.</span></span>
* <span data-ttu-id="464b1-116">Apparaat-naar-cloud-berichten kunnen niet groter zijn dan 256 KB en kunnen worden gegroepeerd in batches te optimaliseren verzendt.</span><span class="sxs-lookup"><span data-stu-id="464b1-116">Device-to-cloud messages can be at most 256 KB, and can be grouped in batches to optimize sends.</span></span> <span data-ttu-id="464b1-117">Batches mag hoogstens 256 KB.</span><span class="sxs-lookup"><span data-stu-id="464b1-117">Batches can be at most 256 KB.</span></span>
* <span data-ttu-id="464b1-118">Zoals wordt beschreven in de [toegangsbeheer met IoT Hub] [ lnk-devguide-security] gedeelte, IoT-Hub kunt per apparaat authenticatie en toegangsbeheer.</span><span class="sxs-lookup"><span data-stu-id="464b1-118">As explained in the [Control access to IoT Hub][lnk-devguide-security] section, IoT Hub enables per-device authentication and access control.</span></span>
* <span data-ttu-id="464b1-119">IoT-Hub kunt u maximaal 10 aangepaste eindpunten maken.</span><span class="sxs-lookup"><span data-stu-id="464b1-119">IoT Hub allows you to create up to 10 custom endpoints.</span></span> <span data-ttu-id="464b1-120">Berichten worden afgeleverd bij de eindpunten op basis van de routes geconfigureerd op uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="464b1-120">Messages are delivered to the endpoints based on routes configured on your IoT hub.</span></span> <span data-ttu-id="464b1-121">Zie voor meer informatie [routering regels](#routing-rules).</span><span class="sxs-lookup"><span data-stu-id="464b1-121">For more information, see [Routing rules](#routing-rules).</span></span>
* <span data-ttu-id="464b1-122">IoT-Hub kunt miljoenen gelijktijdig verbonden apparaten (Zie [quota's en beperking][lnk-quotas]).</span><span class="sxs-lookup"><span data-stu-id="464b1-122">IoT Hub enables millions of simultaneously connected devices (see [Quotas and throttling][lnk-quotas]).</span></span>
* <span data-ttu-id="464b1-123">IoT Hub is niet toegestaan voor het partitioneren van willekeurige.</span><span class="sxs-lookup"><span data-stu-id="464b1-123">IoT Hub does not allow arbitrary partitioning.</span></span> <span data-ttu-id="464b1-124">Apparaat-naar-cloud-berichten worden gepartitioneerd op basis van hun oorspronkelijke **deviceId**.</span><span class="sxs-lookup"><span data-stu-id="464b1-124">Device-to-cloud messages are partitioned based on their originating **deviceId**.</span></span>

<span data-ttu-id="464b1-125">Zie voor meer informatie over de verschillen tussen de IoT Hub en Event Hubs services [vergelijking van Azure IoT Hub en Azure Event Hubs][lnk-comparison].</span><span class="sxs-lookup"><span data-stu-id="464b1-125">For more information about the differences between the IoT Hub and Event Hubs services, see [Comparison of Azure IoT Hub and Azure Event Hubs][lnk-comparison].</span></span>

## <a name="send-non-telemetry-traffic"></a><span data-ttu-id="464b1-126">Niet-telemetrie verkeer verzenden</span><span class="sxs-lookup"><span data-stu-id="464b1-126">Send non-telemetry traffic</span></span>

<span data-ttu-id="464b1-127">Vaak naast telemetriegegevenspunten verzenden apparaten van berichten en aanvragen die afzonderlijke uitvoering en verwerking in de back-end oplossing vereisen.</span><span class="sxs-lookup"><span data-stu-id="464b1-127">Often, in addition to telemetry data points, devices send messages and requests that require separate execution and handling in the solution back end.</span></span> <span data-ttu-id="464b1-128">Bijvoorbeeld, kritieke waarschuwingen die een specifieke actie in de back-end moeten activeren.</span><span class="sxs-lookup"><span data-stu-id="464b1-128">For example, critical alerts that must trigger a specific action in the back end.</span></span> <span data-ttu-id="464b1-129">U kunt eenvoudig schrijven een [routeringsregel] [ lnk-devguide-custom] deze typen berichten verzenden naar een eindpunt dat is toegewezen aan hun verwerking op basis van de header voor het bericht of een waarde in de berichttekst.</span><span class="sxs-lookup"><span data-stu-id="464b1-129">You can easily write a [routing rule][lnk-devguide-custom] to send these types of messages to an endpoint dedicated to their processing based on either a header on the message or a value in the message body.</span></span>

<span data-ttu-id="464b1-130">Zie voor meer informatie over de beste manier om dit soort bericht te verwerken, de [zelfstudie: IoT Hub apparaat-naar-cloud-berichten verwerken] [ lnk-d2c-tutorial] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="464b1-130">For more information about the best way to process this kind of message, see the [Tutorial: How to process IoT Hub device-to-cloud messages][lnk-d2c-tutorial] tutorial.</span></span>

## <a name="route-device-to-cloud-messages"></a><span data-ttu-id="464b1-131">Apparaat-naar-cloud-berichten rondsturen</span><span class="sxs-lookup"><span data-stu-id="464b1-131">Route device-to-cloud messages</span></span>

<span data-ttu-id="464b1-132">Hebt u twee opties voor het routeren van apparaat-naar-cloud-berichten naar uw back-end-apps:</span><span class="sxs-lookup"><span data-stu-id="464b1-132">You have two options for routing device-to-cloud messages to your back-end apps:</span></span>

* <span data-ttu-id="464b1-133">Gebruik de ingebouwde [Event Hub-compatibele eindpunt] [ lnk-compatible-endpoint] zodat back-end apps Lees de apparaat-naar-cloud-berichten dat is ontvangen door de hub.</span><span class="sxs-lookup"><span data-stu-id="464b1-133">Use the built-in [Event Hub-compatible endpoint][lnk-compatible-endpoint] to enable back-end apps to read the device-to-cloud messages received by the hub.</span></span> <span data-ttu-id="464b1-134">Zie voor meer informatie over de ingebouwde Event Hub-compatibele eindpunt, [apparaat-naar-cloud-berichten lezen van het ingebouwde eindpunt][lnk-devguide-builtin].</span><span class="sxs-lookup"><span data-stu-id="464b1-134">To learn about the built-in Event Hub-compatible endpoint, see [Read device-to-cloud messages from the built-in endpoint][lnk-devguide-builtin].</span></span>
* <span data-ttu-id="464b1-135">Regels voor doorsturen gebruiken om berichten te verzenden naar aangepaste eindpunten in uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="464b1-135">Use routing rules to send messages to custom endpoints in your IoT hub.</span></span> <span data-ttu-id="464b1-136">Aangepaste eindpunten inschakelen voor uw back-end-apps om apparaat-naar-cloud-berichten met Event Hubs, Service Bus-wachtrijen of Service Bus-onderwerpen te lezen.</span><span class="sxs-lookup"><span data-stu-id="464b1-136">Custom endpoints enable your back-end apps to read device-to-cloud messages using Event Hubs, Service Bus queues, or Service Bus topics.</span></span> <span data-ttu-id="464b1-137">Zie voor meer informatie over Routering en aangepaste eindpunten, [aangepaste eindpunten en routeringsregels gebruikt voor apparaat-naar-cloud-berichten][lnk-devguide-custom].</span><span class="sxs-lookup"><span data-stu-id="464b1-137">To learn about routing and custom endpoints, see [Use custom endpoints and routing rules for device-to-cloud messages][lnk-devguide-custom].</span></span>

## <a name="anti-spoofing-properties"></a><span data-ttu-id="464b1-138">Eigenschappen anti-adresvervalsing (spoofing)</span><span class="sxs-lookup"><span data-stu-id="464b1-138">Anti-spoofing properties</span></span>

<span data-ttu-id="464b1-139">Om te voorkomen dat apparaat vervalsing in IoT Hub apparaat-naar-cloud-berichten stempels alle berichten met de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="464b1-139">To avoid device spoofing in device-to-cloud messages, IoT Hub stamps all messages with the following properties:</span></span>

* <span data-ttu-id="464b1-140">**ConnectionDeviceId**</span><span class="sxs-lookup"><span data-stu-id="464b1-140">**ConnectionDeviceId**</span></span>
* <span data-ttu-id="464b1-141">**ConnectionDeviceGenerationId**</span><span class="sxs-lookup"><span data-stu-id="464b1-141">**ConnectionDeviceGenerationId**</span></span>
* <span data-ttu-id="464b1-142">**ConnectionAuthMethod**</span><span class="sxs-lookup"><span data-stu-id="464b1-142">**ConnectionAuthMethod**</span></span>

<span data-ttu-id="464b1-143">De eerste twee bevatten de **deviceId** en **generationId** van het oorspronkelijke apparaat conform [identiteit apparaateigenschappen][lnk-device-properties].</span><span class="sxs-lookup"><span data-stu-id="464b1-143">The first two contain the **deviceId** and **generationId** of the originating device, as per [Device identity properties][lnk-device-properties].</span></span>

<span data-ttu-id="464b1-144">De **ConnectionAuthMethod** eigenschap bevat een JSON-geserialiseerd object, met de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="464b1-144">The **ConnectionAuthMethod** property contains a JSON serialized object, with the following properties:</span></span>

```json
{
  "scope": "{ hub | device}",
  "type": "{ symkey | sas}",
  "issuer": "iothub"
}
```

## <a name="next-steps"></a><span data-ttu-id="464b1-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="464b1-145">Next steps</span></span>

<span data-ttu-id="464b1-146">Zie voor meer informatie over de SDK's die u kunt gebruiken om apparaat-naar-cloud-berichten te verzenden [Azure IoT SDK's][lnk-sdks].</span><span class="sxs-lookup"><span data-stu-id="464b1-146">For information about the SDKs you can use to send device-to-cloud messages, see [Azure IoT SDKs][lnk-sdks].</span></span>

<span data-ttu-id="464b1-147">De [aan de slag] [ lnk-get-started] zelfstudies ziet u het apparaat-naar-cloud-berichten verzenden vanuit gesimuleerde en fysieke apparaten.</span><span class="sxs-lookup"><span data-stu-id="464b1-147">The [Get Started][lnk-get-started] tutorials show you how to send device-to-cloud messages from both simulated and physical devices.</span></span> <span data-ttu-id="464b1-148">Zie voor meer details over de [proces IoT Hub apparaat-naar-cloud-berichten met behulp van routes] [ lnk-d2c-tutorial] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="464b1-148">For more detail, see the [Process IoT Hub device-to-cloud messages using routes][lnk-d2c-tutorial] tutorial.</span></span>

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
