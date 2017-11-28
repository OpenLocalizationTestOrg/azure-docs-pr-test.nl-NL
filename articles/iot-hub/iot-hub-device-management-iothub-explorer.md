---
title: aaaAzure IoT device management met iothub explorer | Microsoft Docs
description: Hallo iothub explorer CLI-hulpprogramma gebruiken voor Azure IoT Hub Apparaatbeheer, met directe Hallo-methoden en Hallo Twin van de eigenschappen van de gewenste opties.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Azure iot-Apparaatbeheer, Apparaatbeheer via azure iot hub, apparaat management iot, Apparaatbeheer via iot hub
ms.assetid: b34f799a-fc14-41b9-bf45-54751163fffe
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/12/2017
ms.author: xshi
ms.openlocfilehash: e0a5e6120db5c4fb12f7f8b605a56e0e4aad9217
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-for-azure-iot-hub-device-management"></a><span data-ttu-id="a3215-104">Iothub-explorer gebruiken voor het beheer van Azure IoT Hub-apparaten</span><span class="sxs-lookup"><span data-stu-id="a3215-104">Use iothub-explorer for Azure IoT Hub device management</span></span>

![End-to-end-diagram](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="a3215-106">[iothub explorer](https://github.com/azure/iothub-explorer) is een CLI-hulpprogramma dat u op een host computer toomanage apparaat-id's in het register van IoT hub uitvoert.</span><span class="sxs-lookup"><span data-stu-id="a3215-106">[iothub-explorer](https://github.com/azure/iothub-explorer) is a CLI tool that you run on a host computer toomanage device identities in your IoT hub registry.</span></span> <span data-ttu-id="a3215-107">Wordt geleverd met opties waarmee u tooperform kunt diverse taken.</span><span class="sxs-lookup"><span data-stu-id="a3215-107">It comes with management options that you can use tooperform various tasks.</span></span>

| <span data-ttu-id="a3215-108">Beheeroptie</span><span class="sxs-lookup"><span data-stu-id="a3215-108">Management option</span></span>          | <span data-ttu-id="a3215-109">Taak</span><span class="sxs-lookup"><span data-stu-id="a3215-109">Task</span></span>                                                                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a3215-110">Directe methoden</span><span class="sxs-lookup"><span data-stu-id="a3215-110">Direct methods</span></span>             | <span data-ttu-id="a3215-111">Een apparaat fungeren zoals starten of stoppen van verzenden van berichten of Hallo-apparaat opnieuw maken.</span><span class="sxs-lookup"><span data-stu-id="a3215-111">Make a device act such as starting or stopping sending messages or rebooting hello device.</span></span>                                        |
| <span data-ttu-id="a3215-112">Eigenschappen van de gewenste Twin</span><span class="sxs-lookup"><span data-stu-id="a3215-112">Twin desired properties</span></span>    | <span data-ttu-id="a3215-113">Een apparaat in een bepaalde status, zoals het instellen van een toogreen LED plaatsen of interval too30 minuten instellen Hallo telemetrie verzenden.</span><span class="sxs-lookup"><span data-stu-id="a3215-113">Put a device into certain states, such as setting an LED toogreen or setting hello telemetry send interval too30 minutes.</span></span>         |
| <span data-ttu-id="a3215-114">Dubbele eigenschappen gerapporteerd</span><span class="sxs-lookup"><span data-stu-id="a3215-114">Twin reported properties</span></span>   | <span data-ttu-id="a3215-115">Ophalen van Hallo gerapporteerde status van een apparaat.</span><span class="sxs-lookup"><span data-stu-id="a3215-115">Get hello reported state of a device.</span></span> <span data-ttu-id="a3215-116">Hallo apparaat rapporteert bijvoorbeeld Hallo die LED nu knippert.</span><span class="sxs-lookup"><span data-stu-id="a3215-116">For example, hello device reports hello LED is blinking now.</span></span>                                    |
| <span data-ttu-id="a3215-117">Labels Twin</span><span class="sxs-lookup"><span data-stu-id="a3215-117">Twin tags</span></span>                  | <span data-ttu-id="a3215-118">Apparaatspecifieke metagegevens opslaan in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="a3215-118">Store device-specific metadata in hello cloud.</span></span> <span data-ttu-id="a3215-119">Bijvoorbeeld, de implementatielocatie van de van een machine snoep Hallo.</span><span class="sxs-lookup"><span data-stu-id="a3215-119">For example, hello deployment location of a vending machine.</span></span>                         |
| <span data-ttu-id="a3215-120">Cloud-naar-apparaat-berichten</span><span class="sxs-lookup"><span data-stu-id="a3215-120">Cloud-to-device messages</span></span>   | <span data-ttu-id="a3215-121">Meldingen tooa apparaat verzenden.</span><span class="sxs-lookup"><span data-stu-id="a3215-121">Send notifications tooa device.</span></span> <span data-ttu-id="a3215-122">Bijvoorbeeld 'het is zeer waarschijnlijk toorain vandaag.</span><span class="sxs-lookup"><span data-stu-id="a3215-122">For example, "It is very likely toorain today.</span></span> <span data-ttu-id="a3215-123">Vergeet niet een overkoepelende toobring."</span><span class="sxs-lookup"><span data-stu-id="a3215-123">Don't forget toobring an umbrella."</span></span>              |
| <span data-ttu-id="a3215-124">Apparaat twin query 's</span><span class="sxs-lookup"><span data-stu-id="a3215-124">Device twin queries</span></span>        | <span data-ttu-id="a3215-125">Query uitvoeren op alle apparaten horende tooretrieve die met een willekeurige voorwaarden, zoals het Hallo-apparaten die gebruikt worden om te identificeren.</span><span class="sxs-lookup"><span data-stu-id="a3215-125">Query all device twins tooretrieve those with arbitrary conditions, such as identifying hello devices that are available for use.</span></span> |

<span data-ttu-id="a3215-126">Zie voor meer gedetailleerde uitleg over Hallo verschillen en richtlijnen over het gebruik van deze opties, [apparaat-naar-cloud communicatie richtlijnen](iot-hub-devguide-d2c-guidance.md) en [Cloud-naar-apparaat communicatie richtlijnen](iot-hub-devguide-c2d-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="a3215-126">For more detailed explanation on hello differences and guidance on using these options, see [Device-to-cloud communication guidance](iot-hub-devguide-d2c-guidance.md) and [Cloud-to-device communication guidance](iot-hub-devguide-c2d-guidance.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a3215-127">Apparaatdubbels zijn JSON-documenten waarin statusinformatie van een apparaat (metagegevens, configuraties en voorwaarden) zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="a3215-127">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="a3215-128">IoT Hub persistente een apparaat twin voor elk apparaat dat tooit verbindt.</span><span class="sxs-lookup"><span data-stu-id="a3215-128">IoT Hub persists a device twin for each device that connects tooit.</span></span> <span data-ttu-id="a3215-129">Zie voor meer informatie over apparaat horende [aan de slag met apparaat horende](iot-hub-node-node-twin-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="a3215-129">For more information about device twins, see [Get started with device twins](iot-hub-node-node-twin-getstarted.md).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="a3215-130">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="a3215-130">What you learn</span></span>

<span data-ttu-id="a3215-131">U leert met iothub-explorer met de verschillende beheeropties op uw ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="a3215-131">You learn using iothub-explorer with various management options on your development machine.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="a3215-132">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="a3215-132">What you do</span></span>

<span data-ttu-id="a3215-133">Voer iothub explorer met verschillende opties.</span><span class="sxs-lookup"><span data-stu-id="a3215-133">Run iothub-explorer with various management options.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a3215-134">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="a3215-134">What you need</span></span>

- <span data-ttu-id="a3215-135">Zelfstudie [instellen van uw apparaat](iot-hub-raspberry-pi-kit-node-get-started.md) voltooid die Hallo volgens de vereisten worden behandeld:</span><span class="sxs-lookup"><span data-stu-id="a3215-135">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="a3215-136">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="a3215-136">An active Azure subscription.</span></span>
  - <span data-ttu-id="a3215-137">Een Azure-IoT-hub in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="a3215-137">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="a3215-138">Een clienttoepassing die berichten tooyour Azure IoT hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="a3215-138">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="a3215-139">Zorg ervoor dat uw apparaat wordt uitgevoerd met de clienttoepassing Hallo tijdens deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="a3215-139">Make sure your device is running with hello client application during this tutorial.</span></span>
- <span data-ttu-id="a3215-140">iothub-explorer [iothub explorer installeren](https://github.com/azure/iothub-explorer) op uw ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="a3215-140">iothub-explorer, [Install iothub-explorer](https://github.com/azure/iothub-explorer) on your development machine.</span></span>

## <a name="connect-tooyour-iot-hub"></a><span data-ttu-id="a3215-141">Verbinding maken met tooyour IoT-hub</span><span class="sxs-lookup"><span data-stu-id="a3215-141">Connect tooyour IoT hub</span></span>

<span data-ttu-id="a3215-142">Sluit tooyour iothub door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="a3215-142">Connect tooyour IoT hub by running hello following command:</span></span>

```bash
iothub-explorer login <your IoT hub connection string>
```

## <a name="use-iothub-explorer-with-direct-methods"></a><span data-ttu-id="a3215-143">Iothub explorer gebruiken met directe methoden</span><span class="sxs-lookup"><span data-stu-id="a3215-143">Use iothub-explorer with direct methods</span></span>

<span data-ttu-id="a3215-144">Hallo aanroepen `start` methode in Hallo apparaat app toosend berichten tooyour IoT-hub door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="a3215-144">Invoke hello `start` method in hello device app toosend messages tooyour IoT hub by running hello following command:</span></span>

```bash
iothub-explorer device-method <your device Id> start
```

<span data-ttu-id="a3215-145">Hallo aanroepen `stop` methode bij het verzenden van Hallo apparaat app toostop tooyour IoT-hub door het uitvoeren van de volgende opdracht Hallo-berichten:</span><span class="sxs-lookup"><span data-stu-id="a3215-145">Invoke hello `stop` method in hello device app toostop sending messages tooyour IoT hub by running hello following command:</span></span>

```bash
iothub-explorer device-method <your device Id> stop
```

## <a name="use-iothub-explorer-with-twins-desired-properties"></a><span data-ttu-id="a3215-146">Gebruik iothub-explorer met de gewenste eigenschappen van twin</span><span class="sxs-lookup"><span data-stu-id="a3215-146">Use iothub-explorer with twin’s desired properties</span></span>

<span data-ttu-id="a3215-147">Instellen van een interval van de gewenste eigenschap 3000 = door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="a3215-147">Set a desired property interval = 3000 by running hello following command:</span></span>

```bash
iothub-explorer update-twin <your device id> {\"properties\":{\"desired\":{\"interval\":3000}}}
```

<span data-ttu-id="a3215-148">Deze eigenschap kan worden gelezen door uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="a3215-148">This property can be read by your device.</span></span>

## <a name="use-iothub-explorer-with-twins-reported-properties"></a><span data-ttu-id="a3215-149">Gebruik iothub-explorer met de dubbele eigenschappen gerapporteerd</span><span class="sxs-lookup"><span data-stu-id="a3215-149">Use iothub-explorer with twin’s reported properties</span></span>

<span data-ttu-id="a3215-150">Ophalen van hello gemelde eigenschappen van Hallo apparaat door te voeren Hallo de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="a3215-150">Get hello reported properties of hello device by running hello following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="a3215-151">Een van de eigenschappen Hallo is $metadata. $lastUpdated waaruit blijkt Hallo laatste keer dat dit apparaat worden verzonden of ontvangen van een bericht.</span><span class="sxs-lookup"><span data-stu-id="a3215-151">One of hello properties is $metadata.$lastUpdated which shows hello last time this device sends or receives a message.</span></span>

## <a name="use-iothub-explorer-with-twins-tags"></a><span data-ttu-id="a3215-152">Gebruik iothub-explorer met de labels van twin</span><span class="sxs-lookup"><span data-stu-id="a3215-152">Use iothub-explorer with twin’s tags</span></span>

<span data-ttu-id="a3215-153">Hallo-labels en eigenschappen van Hallo apparaat weergegeven door het uitvoeren van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="a3215-153">Display hello tags and properties of hello device by running hello following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="a3215-154">Voeg een veld rol = temperatuur en vochtigheid toohello apparaat door te voeren Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="a3215-154">Add a field role = temperature&humidity toohello device by running hello following command:</span></span>

```bash
iothub-explorer update-twin <your device id> "{\"tags\":{\"role\":\"temperature&humidity\"}}"

```

## <a name="use-iothub-explorer-with-cloud-to-device-messages"></a><span data-ttu-id="a3215-155">Gebruik iothub-explorer met de Cloud-naar-apparaat-berichten</span><span class="sxs-lookup"><span data-stu-id="a3215-155">Use iothub-explorer with Cloud-to-device messages</span></span>

<span data-ttu-id="a3215-156">Een apparaat met 'Hallo wereld' bericht toohello door het uitvoeren van de volgende opdracht Hallo verzenden:</span><span class="sxs-lookup"><span data-stu-id="a3215-156">Send a "Hello World" message toohello device by running hello following command:</span></span>

```bash
iothub-explorer send <device-id> "Hello World"
```

<span data-ttu-id="a3215-157">Zie [iothub explorer toosend gebruiken en te ontvangen van berichten tussen het apparaat en IoT Hub](iot-hub-explorer-cloud-device-messaging.md) voor een echte scenario van het gebruik van deze opdracht.</span><span class="sxs-lookup"><span data-stu-id="a3215-157">See [Use iothub-explorer toosend and receive messages between your device and IoT Hub](iot-hub-explorer-cloud-device-messaging.md) for a real scenario of using this command.</span></span>

## <a name="use-iothub-explorer-with-device-twins-queries"></a><span data-ttu-id="a3215-158">Met iothub-Verkenner terwijl het apparaat horende query 's</span><span class="sxs-lookup"><span data-stu-id="a3215-158">Use iothub-explorer with device twins queries</span></span>

<span data-ttu-id="a3215-159">Query uitvoeren op apparaten met een label van de rol 'temperatuur en vochtigheid' door het uitvoeren van de volgende opdracht Hallo =:</span><span class="sxs-lookup"><span data-stu-id="a3215-159">Query devices with a tag of role = 'temperature&humidity' by running hello following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role = 'temperature&humidity'"
```

<span data-ttu-id="a3215-160">Query uitvoeren op alle apparaten, behalve die met een label van de rol 'temperatuur en vochtigheid' door het uitvoeren van de volgende opdracht Hallo =:</span><span class="sxs-lookup"><span data-stu-id="a3215-160">Query all devices except those with a tag of role = 'temperature&humidity' by running hello following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role != 'temperature&humidity'"
```

## <a name="next-steps"></a><span data-ttu-id="a3215-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a3215-161">Next steps</span></span>

<span data-ttu-id="a3215-162">U hebt geleerd hoe toouse iothub-explorer met de verschillende opties.</span><span class="sxs-lookup"><span data-stu-id="a3215-162">You've learned how toouse iothub-explorer with various management options.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
