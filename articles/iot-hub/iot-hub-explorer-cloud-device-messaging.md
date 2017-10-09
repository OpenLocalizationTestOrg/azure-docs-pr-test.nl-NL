---
title: aaaManage Azure IoT Hub cloud apparaat met iothub explorer messaging | Microsoft Docs
description: Ontdek hoe toouse Hallo iothub explorer CLI-hulpprogramma toomonitor apparaat toocloud (D2C)-berichten en berichten cloud toodevice (C2D) in Azure IoT Hub.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: iothub explorer cloud apparaat messaging, iot hub cloud toodevice cloud toodevice messaging
ms.assetid: 04521658-35d3-4503-ae48-51d6ad3c62cc
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: 741383b5631714cc2fef3309541fd2117aa7824c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-toosend-and-receive-messages-between-your-device-and-iot-hub"></a><span data-ttu-id="5e04f-104">Gebruik iothub explorer toosend en ontvangen van berichten tussen het apparaat en IoT-Hub</span><span class="sxs-lookup"><span data-stu-id="5e04f-104">Use iothub-explorer toosend and receive messages between your device and IoT Hub</span></span>

![End-to-end-diagram](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="5e04f-106">[iothub explorer](https://github.com/azure/iothub-explorer) heeft een aantal opdrachten die IoT Hub beheer vergemakkelijkt.</span><span class="sxs-lookup"><span data-stu-id="5e04f-106">[iothub-explorer](https://github.com/azure/iothub-explorer) has a handful of commands that makes IoT Hub management easier.</span></span> <span data-ttu-id="5e04f-107">Deze zelfstudie is gericht op het toouse iothub explorer toosend en ontvangen van berichten tussen het apparaat en uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="5e04f-107">This tutorial focuses on how toouse iothub-explorer toosend and receive messages between your device and your IoT hub.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="5e04f-108">Wat u leert</span><span class="sxs-lookup"><span data-stu-id="5e04f-108">What you will learn</span></span>

<span data-ttu-id="5e04f-109">U leert hoe toouse iothub explorer toomonitor apparaat-naar-cloud-berichten en berichten die toosend cloud-naar-apparaat.</span><span class="sxs-lookup"><span data-stu-id="5e04f-109">You learn how toouse iothub-explorer toomonitor device-to-cloud messages and toosend cloud-to-device messages.</span></span> <span data-ttu-id="5e04f-110">Apparaat-naar-cloud-berichten kunnen worden sensorgegevens dat uw apparaat verzamelt en vervolgens tooyour IoT-hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="5e04f-110">Device-to-cloud messages could be sensor data that your device collects and then sends tooyour IoT hub.</span></span> <span data-ttu-id="5e04f-111">Cloud-naar-apparaat-berichten kunnen worden opdrachten uw IoT-hub verzendt tooyour apparaat tooblink een LED die is verbonden tooyour apparaat.</span><span class="sxs-lookup"><span data-stu-id="5e04f-111">Cloud-to-device messages could be commands that your IoT hub sends tooyour device tooblink an LED that is connected tooyour device.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="5e04f-112">Wat u doet</span><span class="sxs-lookup"><span data-stu-id="5e04f-112">What you will do</span></span>

- <span data-ttu-id="5e04f-113">Gebruik iothub explorer toomonitor apparaat-naar-cloud-berichten.</span><span class="sxs-lookup"><span data-stu-id="5e04f-113">Use iothub-explorer toomonitor device-to-cloud messages.</span></span>
- <span data-ttu-id="5e04f-114">Gebruik iothub explorer toosend cloud-naar-apparaat-berichten.</span><span class="sxs-lookup"><span data-stu-id="5e04f-114">Use iothub-explorer toosend cloud-to-device messages.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="5e04f-115">Wat u nodig hebt</span><span class="sxs-lookup"><span data-stu-id="5e04f-115">What you need</span></span>

- <span data-ttu-id="5e04f-116">Zelfstudie [instellen van uw apparaat](iot-hub-raspberry-pi-kit-node-get-started.md) voltooid die Hallo volgens de vereisten worden behandeld:</span><span class="sxs-lookup"><span data-stu-id="5e04f-116">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="5e04f-117">Een actief Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="5e04f-117">An active Azure subscription.</span></span>
  - <span data-ttu-id="5e04f-118">Een Azure-IoT-hub in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="5e04f-118">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="5e04f-119">Een clienttoepassing die berichten tooyour Azure IoT hub verzendt.</span><span class="sxs-lookup"><span data-stu-id="5e04f-119">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="5e04f-120">iothub-explorer.</span><span class="sxs-lookup"><span data-stu-id="5e04f-120">iothub-explorer.</span></span> <span data-ttu-id="5e04f-121">([Iothub explorer installeren](https://github.com/azure/iothub-explorer))</span><span class="sxs-lookup"><span data-stu-id="5e04f-121">([Install iothub-explorer](https://github.com/azure/iothub-explorer))</span></span>

## <a name="monitor-device-to-cloud-messages"></a><span data-ttu-id="5e04f-122">Apparaat-naar-cloud-berichten worden gecontroleerd</span><span class="sxs-lookup"><span data-stu-id="5e04f-122">Monitor device-to-cloud messages</span></span>

<span data-ttu-id="5e04f-123">toomonitor berichten die vanaf uw apparaat tooyour IoT-hub worden verzonden als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="5e04f-123">toomonitor messages that are sent from your device tooyour IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="5e04f-124">Open een consolevenster.</span><span class="sxs-lookup"><span data-stu-id="5e04f-124">Open a console window.</span></span>
1. <span data-ttu-id="5e04f-125">Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="5e04f-125">Run hello following command:</span></span>

   ```bash
   iothub-explorer monitor-events <device-id> --login "<IoTHubConnectionString>"
   ```

   > [!Note]
   > <span data-ttu-id="5e04f-126">Ophalen van `<device-id>` en `<IoTHubConnectionString>` uit uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="5e04f-126">Get `<device-id>` and `<IoTHubConnectionString>` from your IoT hub.</span></span> <span data-ttu-id="5e04f-127">Zorg ervoor dat u klaar bent met eerdere Hallo-zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="5e04f-127">Make sure you've finished hello previous tutorial.</span></span> <span data-ttu-id="5e04f-128">Of u kunt proberen toouse `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` hebt u `HostName`, `SharedAccessKeyName` en `SharedAccessKey`.</span><span class="sxs-lookup"><span data-stu-id="5e04f-128">Or you can try toouse `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` if you have `HostName`, `SharedAccessKeyName` and `SharedAccessKey`.</span></span>

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="5e04f-129">Cloud-naar-apparaat-berichten verzenden</span><span class="sxs-lookup"><span data-stu-id="5e04f-129">Send cloud-to-device messages</span></span>

<span data-ttu-id="5e04f-130">toosend een bericht van uw IoT hub tooyour-apparaat als volgt te werk:</span><span class="sxs-lookup"><span data-stu-id="5e04f-130">toosend a message from your IoT hub tooyour device, follow these steps:</span></span>

1. <span data-ttu-id="5e04f-131">Open een consolevenster.</span><span class="sxs-lookup"><span data-stu-id="5e04f-131">Open a console window.</span></span>
1. <span data-ttu-id="5e04f-132">Start een sessie op uw IoT-hub door het Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="5e04f-132">Start a session on your IoT hub by running hello following command:</span></span>

   ```bash
   iothub-explorer login `<IoTHubConnectionString>`
   ```

1. <span data-ttu-id="5e04f-133">Een bericht tooyour apparaat verzenden door te voeren Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="5e04f-133">Send a message tooyour device by running hello following command:</span></span>

   ```bash
   iothub-explorer send <device-id> <message>
   ```

<span data-ttu-id="5e04f-134">Hallo opdracht knippert Hallo LED die is verbonden tooyour apparaat en Hallo-bericht tooyour apparaat verzendt.</span><span class="sxs-lookup"><span data-stu-id="5e04f-134">hello command blinks hello LED that is connected tooyour device and sends hello message tooyour device.</span></span>

> [!Note]
> <span data-ttu-id="5e04f-135">Er is een afzonderlijke ack opdracht back tooyour IoT-hub bij ontvangst van het Hallo-bericht niet nodig voor Hallo apparaat toosend.</span><span class="sxs-lookup"><span data-stu-id="5e04f-135">There is no need for hello device toosend a separate ack command back tooyour IoT hub upon receiving hello message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e04f-136">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5e04f-136">Next steps</span></span>

<span data-ttu-id="5e04f-137">U hebt geleerd hoe toomonitor apparaat-naar-cloud-berichten en berichten tussen uw IoT-apparaat en de Azure IoT Hub cloud naar apparaat verzenden.</span><span class="sxs-lookup"><span data-stu-id="5e04f-137">You’ve learned how toomonitor device-to-cloud messages and send cloud-to-device messages between your IoT device and Azure IoT Hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
