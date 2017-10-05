---
title: Azure IoT-Apparaatbeheer met iothub explorer | Microsoft Docs
description: De iothub-explorer CLI-hulpprogramma gebruiken voor Azure IoT Hub Apparaatbeheer, met daarin de rechtstreekse methoden en de Twin eigenschappen van de gewenste opties.
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
ms.openlocfilehash: 5b7a5057bdfb5920fbb5759bed1f5561cfa1d7e0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="use-iothub-explorer-for-azure-iot-hub-device-management"></a><span data-ttu-id="28c54-104">Iothub-explorer gebruiken voor het beheer van Azure IoT Hub-apparaten</span><span class="sxs-lookup"><span data-stu-id="28c54-104">Use iothub-explorer for Azure IoT Hub device management</span></span>

![End-to-end-diagram](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="28c54-106">[iothub explorer](https://github.com/azure/iothub-explorer) is een CLI-hulpprogramma dat u op een host uitvoert computer voor het beheren van apparaat-id's in het register van IoT hub.</span><span class="sxs-lookup"><span data-stu-id="28c54-106">[iothub-explorer](https://github.com/azure/iothub-explorer) is a CLI tool that you run on a host computer to manage device identities in your IoT hub registry.</span></span> <span data-ttu-id="28c54-107">Het wordt geleverd met opties die u kunt verschillende taken uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="28c54-107">It comes with management options that you can use to perform various tasks.</span></span>

| <span data-ttu-id="28c54-108">Beheeroptie</span><span class="sxs-lookup"><span data-stu-id="28c54-108">Management option</span></span>          | <span data-ttu-id="28c54-109">Taak</span><span class="sxs-lookup"><span data-stu-id="28c54-109">Task</span></span>                                                                                                                            |
|----------------------------|---------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="28c54-110">Directe methoden</span><span class="sxs-lookup"><span data-stu-id="28c54-110">Direct methods</span></span>             | <span data-ttu-id="28c54-111">Een apparaat fungeren zoals starten of stoppen van verzenden van berichten of het apparaat opnieuw maken.</span><span class="sxs-lookup"><span data-stu-id="28c54-111">Make a device act such as starting or stopping sending messages or rebooting the device.</span></span>                                        |
| <span data-ttu-id="28c54-112">Eigenschappen van de gewenste Twin</span><span class="sxs-lookup"><span data-stu-id="28c54-112">Twin desired properties</span></span>    | <span data-ttu-id="28c54-113">Een apparaat in een bepaalde status, zoals een LED in groen instellen of het instellen van het interval voor het verzenden van telemetrie tot 30 minuten geplaatst.</span><span class="sxs-lookup"><span data-stu-id="28c54-113">Put a device into certain states, such as setting an LED to green or setting the telemetry send interval to 30 minutes.</span></span>         |
| <span data-ttu-id="28c54-114">Dubbele eigenschappen gerapporteerd</span><span class="sxs-lookup"><span data-stu-id="28c54-114">Twin reported properties</span></span>   | <span data-ttu-id="28c54-115">Ophalen van de gerapporteerde status van een apparaat.</span><span class="sxs-lookup"><span data-stu-id="28c54-115">Get the reported state of a device.</span></span> <span data-ttu-id="28c54-116">Bijvoorbeeld, meldt het apparaat dat de LED nu knippert.</span><span class="sxs-lookup"><span data-stu-id="28c54-116">For example, the device reports the LED is blinking now.</span></span>                                    |
| <span data-ttu-id="28c54-117">Labels Twin</span><span class="sxs-lookup"><span data-stu-id="28c54-117">Twin tags</span></span>                  | <span data-ttu-id="28c54-118">Apparaatspecifieke metagegevens niet opslaan in de cloud.</span><span class="sxs-lookup"><span data-stu-id="28c54-118">Store device-specific metadata in the cloud.</span></span> <span data-ttu-id="28c54-119">Bijvoorbeeld, de implementatielocatie van een snoep-machine.</span><span class="sxs-lookup"><span data-stu-id="28c54-119">For example, the deployment location of a vending machine.</span></span>                         |
| <span data-ttu-id="28c54-120">Cloud-naar-apparaat-berichten</span><span class="sxs-lookup"><span data-stu-id="28c54-120">Cloud-to-device messages</span></span>   | <span data-ttu-id="28c54-121">Meldingen verzenden naar een apparaat.</span><span class="sxs-lookup"><span data-stu-id="28c54-121">Send notifications to a device.</span></span> <span data-ttu-id="28c54-122">Bijvoorbeeld, "het is zeer waarschijnlijk regen vandaag.</span><span class="sxs-lookup"><span data-stu-id="28c54-122">For example, "It is very likely to rain today.</span></span> <span data-ttu-id="28c54-123">Vergeet niet om een overkoepelende."</span><span class="sxs-lookup"><span data-stu-id="28c54-123">Don't forget to bring an umbrella."</span></span>              |
| <span data-ttu-id="28c54-124">Apparaat twin query 's</span><span class="sxs-lookup"><span data-stu-id="28c54-124">Device twin queries</span></span>        | <span data-ttu-id="28c54-125">Query uitvoeren op alle apparaten horende om op te halen die met een willekeurige voorwaarden, zoals de apparaten die gebruikt worden om te identificeren.</span><span class="sxs-lookup"><span data-stu-id="28c54-125">Query all device twins to retrieve those with arbitrary conditions, such as identifying the devices that are available for use.</span></span> |

<span data-ttu-id="28c54-126">Zie voor meer gedetailleerde uitleg over de verschillen en richtlijnen over het gebruik van deze opties, [apparaat-naar-cloud communicatie richtlijnen](iot-hub-devguide-d2c-guidance.md) en [Cloud-naar-apparaat communicatie richtlijnen](iot-hub-devguide-c2d-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="28c54-126">For more detailed explanation on the differences and guidance on using these options, see [Device-to-cloud communication guidance](iot-hub-devguide-d2c-guidance.md) and [Cloud-to-device communication guidance](iot-hub-devguide-c2d-guidance.md).</span></span>

> [!NOTE]
> <span data-ttu-id="28c54-127">Apparaatdubbels zijn JSON-documenten waarin statusinformatie van een apparaat (metagegevens, configuraties en voorwaarden) zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="28c54-127">Device twins are JSON documents that store device state information (metadata, configurations, and conditions).</span></span> <span data-ttu-id="28c54-128">IoT Hub persistente een apparaat twin voor elk apparaat dat verbinding met het maakt.</span><span class="sxs-lookup"><span data-stu-id="28c54-128">IoT Hub persists a device twin for each device that connects to it.</span></span> <span data-ttu-id="28c54-129">Zie voor meer informatie over apparaat horende [aan de slag met apparaat horende](iot-hub-node-node-twin-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="28c54-129">For more information about device twins, see [Get started with device twins](iot-hub-node-node-twin-getstarted.md).</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="28c54-130">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="28c54-130">What you learn</span></span>

<span data-ttu-id="28c54-131">U leert met iothub-explorer met de verschillende beheeropties op uw ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="28c54-131">You learn using iothub-explorer with various management options on your development machine.</span></span>

## <a name="what-you-do"></a><span data-ttu-id="28c54-132">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="28c54-132">What you do</span></span>

<span data-ttu-id="28c54-133">Voer iothub explorer met verschillende opties.</span><span class="sxs-lookup"><span data-stu-id="28c54-133">Run iothub-explorer with various management options.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="28c54-134">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="28c54-134">What you need</span></span>

- <span data-ttu-id="28c54-135">Zelfstudie [instellen van uw apparaat](iot-hub-raspberry-pi-kit-node-get-started.md) voltooid die wordt ingegaan op de volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="28c54-135">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="28c54-136">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="28c54-136">An active Azure subscription.</span></span>
  - <span data-ttu-id="28c54-137">Een Azure-IoT-hub in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="28c54-137">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="28c54-138">Een clienttoepassing dat berichten naar uw Azure-IoT-hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="28c54-138">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="28c54-139">Zorg ervoor dat uw apparaat wordt uitgevoerd met de clienttoepassing tijdens deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="28c54-139">Make sure your device is running with the client application during this tutorial.</span></span>
- <span data-ttu-id="28c54-140">iothub-explorer [iothub explorer installeren](https://github.com/azure/iothub-explorer) op uw ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="28c54-140">iothub-explorer, [Install iothub-explorer](https://github.com/azure/iothub-explorer) on your development machine.</span></span>

## <a name="connect-to-your-iot-hub"></a><span data-ttu-id="28c54-141">Verbinding maken met uw IoT-hub</span><span class="sxs-lookup"><span data-stu-id="28c54-141">Connect to your IoT hub</span></span>

<span data-ttu-id="28c54-142">Verbinding maken met uw IoT-hub met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="28c54-142">Connect to your IoT hub by running the following command:</span></span>

```bash
iothub-explorer login <your IoT hub connection string>
```

## <a name="use-iothub-explorer-with-direct-methods"></a><span data-ttu-id="28c54-143">Iothub explorer gebruiken met directe methoden</span><span class="sxs-lookup"><span data-stu-id="28c54-143">Use iothub-explorer with direct methods</span></span>

<span data-ttu-id="28c54-144">Aanroepen de `start` methode in de app apparaat berichten verzenden naar uw IoT-hub met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="28c54-144">Invoke the `start` method in the device app to send messages to your IoT hub by running the following command:</span></span>

```bash
iothub-explorer device-method <your device Id> start
```

<span data-ttu-id="28c54-145">Aanroepen de `stop` methode in de app apparaat om te stoppen met het verzenden van berichten naar uw IoT-hub met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="28c54-145">Invoke the `stop` method in the device app to stop sending messages to your IoT hub by running the following command:</span></span>

```bash
iothub-explorer device-method <your device Id> stop
```

## <a name="use-iothub-explorer-with-twins-desired-properties"></a><span data-ttu-id="28c54-146">Gebruik iothub-explorer met de gewenste eigenschappen van twin</span><span class="sxs-lookup"><span data-stu-id="28c54-146">Use iothub-explorer with twin’s desired properties</span></span>

<span data-ttu-id="28c54-147">Instellen van een interval van de gewenste eigenschap 3000 = met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="28c54-147">Set a desired property interval = 3000 by running the following command:</span></span>

```bash
iothub-explorer update-twin <your device id> {\"properties\":{\"desired\":{\"interval\":3000}}}
```

<span data-ttu-id="28c54-148">Deze eigenschap kan worden gelezen door uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="28c54-148">This property can be read by your device.</span></span>

## <a name="use-iothub-explorer-with-twins-reported-properties"></a><span data-ttu-id="28c54-149">Gebruik iothub-explorer met de dubbele eigenschappen gerapporteerd</span><span class="sxs-lookup"><span data-stu-id="28c54-149">Use iothub-explorer with twin’s reported properties</span></span>

<span data-ttu-id="28c54-150">Haal de gerapporteerde eigenschappen van het apparaat met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="28c54-150">Get the reported properties of the device by running the following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="28c54-151">Een van de eigenschappen is $metadata. $lastUpdated waarin de laatste keer dat dit apparaat worden verzonden of ontvangen van een bericht.</span><span class="sxs-lookup"><span data-stu-id="28c54-151">One of the properties is $metadata.$lastUpdated which shows the last time this device sends or receives a message.</span></span>

## <a name="use-iothub-explorer-with-twins-tags"></a><span data-ttu-id="28c54-152">Gebruik iothub-explorer met de labels van twin</span><span class="sxs-lookup"><span data-stu-id="28c54-152">Use iothub-explorer with twin’s tags</span></span>

<span data-ttu-id="28c54-153">De labels en eigenschappen van het apparaat weergegeven door met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="28c54-153">Display the tags and properties of the device by running the following command:</span></span>

```bash
iothub-explorer get-twin <your device id>
```

<span data-ttu-id="28c54-154">Voeg een veld rol = temperatuur en vochtigheid aan het apparaat met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="28c54-154">Add a field role = temperature&humidity to the device by running the following command:</span></span>

```bash
iothub-explorer update-twin <your device id> "{\"tags\":{\"role\":\"temperature&humidity\"}}"

```

## <a name="use-iothub-explorer-with-cloud-to-device-messages"></a><span data-ttu-id="28c54-155">Gebruik iothub-explorer met de Cloud-naar-apparaat-berichten</span><span class="sxs-lookup"><span data-stu-id="28c54-155">Use iothub-explorer with Cloud-to-device messages</span></span>

<span data-ttu-id="28c54-156">Een 'Hallo wereld'-bericht verzenden naar het apparaat met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="28c54-156">Send a "Hello World" message to the device by running the following command:</span></span>

```bash
iothub-explorer send <device-id> "Hello World"
```

<span data-ttu-id="28c54-157">Zie [iothub-explorer gebruiken om te verzenden en ontvangen van berichten tussen het apparaat en IoT Hub](iot-hub-explorer-cloud-device-messaging.md) voor een echte scenario van het gebruik van deze opdracht.</span><span class="sxs-lookup"><span data-stu-id="28c54-157">See [Use iothub-explorer to send and receive messages between your device and IoT Hub](iot-hub-explorer-cloud-device-messaging.md) for a real scenario of using this command.</span></span>

## <a name="use-iothub-explorer-with-device-twins-queries"></a><span data-ttu-id="28c54-158">Met iothub-Verkenner terwijl het apparaat horende query 's</span><span class="sxs-lookup"><span data-stu-id="28c54-158">Use iothub-explorer with device twins queries</span></span>

<span data-ttu-id="28c54-159">Query uitvoeren op apparaten met een label van de rol = 'temperatuur en vochtigheid' door de volgende opdracht uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="28c54-159">Query devices with a tag of role = 'temperature&humidity' by running the following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role = 'temperature&humidity'"
```

<span data-ttu-id="28c54-160">Query uitvoeren op alle apparaten, behalve die met een label van de rol = 'temperatuur en vochtigheid' door de volgende opdracht uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="28c54-160">Query all devices except those with a tag of role = 'temperature&humidity' by running the following command:</span></span>

```bash
iothub-explorer query-twin "SELECT * FROM devices WHERE tags.role != 'temperature&humidity'"
```

## <a name="next-steps"></a><span data-ttu-id="28c54-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="28c54-161">Next steps</span></span>

<span data-ttu-id="28c54-162">U hebt geleerd iothub-explorer met de verschillende opties gebruiken.</span><span class="sxs-lookup"><span data-stu-id="28c54-162">You've learned how to use iothub-explorer with various management options.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
