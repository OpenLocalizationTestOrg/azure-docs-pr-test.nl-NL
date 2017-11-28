---
title: Schalen met Azure IoT Hub | Microsoft Docs
description: Klik hier voor meer informatie over het schalen van uw IoT-hub ter ondersteuning van de verwachte bericht doorvoer. Bevat een overzicht van de ondersteunde doorvoer voor elke laag en opties voor sharding.
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: e7bd4968-db46-46cf-865d-9c944f683832
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2cb263103da05b10c24aab71d81c43eb25987565
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="scale-your-iot-hub-solution"></a><span data-ttu-id="31e7e-104">Schalen van uw IoT hub-oplossing</span><span class="sxs-lookup"><span data-stu-id="31e7e-104">Scale your IoT hub solution</span></span>
<span data-ttu-id="31e7e-105">Azure IoT Hub kan maximaal een miljoen gelijktijdig verbonden apparaten ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="31e7e-105">Azure IoT Hub can support up to a million simultaneously connected devices.</span></span> <span data-ttu-id="31e7e-106">Zie voor meer informatie [IoT Hub prijzen][lnk-pricing].</span><span class="sxs-lookup"><span data-stu-id="31e7e-106">For more information, see [IoT Hub pricing][lnk-pricing].</span></span> <span data-ttu-id="31e7e-107">Elke eenheid IoT-Hub kunt een bepaald aantal dagelijkse berichten.</span><span class="sxs-lookup"><span data-stu-id="31e7e-107">Each IoT Hub unit allows a certain number of daily messages.</span></span>

<span data-ttu-id="31e7e-108">Als u wilt schalen goed uw oplossing, kunt u uw bepaalde gebruik van IoT-Hub.</span><span class="sxs-lookup"><span data-stu-id="31e7e-108">To properly scale your solution, consider your particular use of IoT Hub.</span></span> <span data-ttu-id="31e7e-109">Houd rekening met de vereiste piek-doorvoer voor de volgende categorieën van bewerkingen in het bijzonder:</span><span class="sxs-lookup"><span data-stu-id="31e7e-109">In particular, consider the required peak throughput for the following categories of operations:</span></span>

* <span data-ttu-id="31e7e-110">Apparaat-naar-cloud-berichten</span><span class="sxs-lookup"><span data-stu-id="31e7e-110">Device-to-cloud messages</span></span>
* <span data-ttu-id="31e7e-111">Cloud-naar-apparaat-berichten</span><span class="sxs-lookup"><span data-stu-id="31e7e-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="31e7e-112">Registerbewerkingen voor identiteit</span><span class="sxs-lookup"><span data-stu-id="31e7e-112">Identity registry operations</span></span>

<span data-ttu-id="31e7e-113">Naast deze informatie doorvoer Zie [IoT Hub quota en vertragingen] [ IoT Hub quotas and throttles] en dienovereenkomstig ontwerpen van uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="31e7e-113">In addition to this throughput information, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles] and design your solution accordingly.</span></span>

## <a name="device-to-cloud-and-cloud-to-device-message-throughput"></a><span data-ttu-id="31e7e-114">Apparaat-naar-cloud- en cloud-naar-apparaat bericht doorvoer</span><span class="sxs-lookup"><span data-stu-id="31e7e-114">Device-to-cloud and cloud-to-device message throughput</span></span>
<span data-ttu-id="31e7e-115">De beste manier om het formaat van een IoT Hub-oplossing is om te evalueren van het verkeer op basis van per eenheid.</span><span class="sxs-lookup"><span data-stu-id="31e7e-115">The best way to size an IoT Hub solution is to evaluate the traffic on a per-unit basis.</span></span>

<span data-ttu-id="31e7e-116">Apparaat-naar-cloudberichten Volg deze richtlijnen volgehouden doorvoer.</span><span class="sxs-lookup"><span data-stu-id="31e7e-116">Device-to-cloud messages follow these sustained throughput guidelines.</span></span>

| <span data-ttu-id="31e7e-117">Laag</span><span class="sxs-lookup"><span data-stu-id="31e7e-117">Tier</span></span> | <span data-ttu-id="31e7e-118">Volgehouden doorvoer</span><span class="sxs-lookup"><span data-stu-id="31e7e-118">Sustained throughput</span></span> | <span data-ttu-id="31e7e-119">Continue verzendsnelheid</span><span class="sxs-lookup"><span data-stu-id="31e7e-119">Sustained send rate</span></span> |
| --- | --- | --- |
| <span data-ttu-id="31e7e-120">S1</span><span class="sxs-lookup"><span data-stu-id="31e7e-120">S1</span></span> |<span data-ttu-id="31e7e-121">Maximaal 1111 KB per minuut per eenheid</span><span class="sxs-lookup"><span data-stu-id="31e7e-121">Up to 1111 KB/minute per unit</span></span><br/><span data-ttu-id="31e7e-122">(1,5 GB/dag/unit)</span><span class="sxs-lookup"><span data-stu-id="31e7e-122">(1.5 GB/day/unit)</span></span> |<span data-ttu-id="31e7e-123">Gemiddelde van 278 berichten per minuut per eenheid</span><span class="sxs-lookup"><span data-stu-id="31e7e-123">Average of 278 messages/minute per unit</span></span><br/><span data-ttu-id="31e7e-124">(400.000 berichten per dag per eenheid)</span><span class="sxs-lookup"><span data-stu-id="31e7e-124">(400,000 messages/day per unit)</span></span> |
| <span data-ttu-id="31e7e-125">S2</span><span class="sxs-lookup"><span data-stu-id="31e7e-125">S2</span></span> |<span data-ttu-id="31e7e-126">Maximaal 16 MB per minuut per eenheid</span><span class="sxs-lookup"><span data-stu-id="31e7e-126">Up to 16 MB/minute per unit</span></span><br/><span data-ttu-id="31e7e-127">(22.8 GB/dag/unit)</span><span class="sxs-lookup"><span data-stu-id="31e7e-127">(22.8 GB/day/unit)</span></span> |<span data-ttu-id="31e7e-128">Gemiddelde van 4,167 berichten per minuut per eenheid</span><span class="sxs-lookup"><span data-stu-id="31e7e-128">Average of 4,167 messages/minute per unit</span></span><br/><span data-ttu-id="31e7e-129">(6 miljoen berichten per dag per eenheid)</span><span class="sxs-lookup"><span data-stu-id="31e7e-129">(6 million messages/day per unit)</span></span> |
| <span data-ttu-id="31e7e-130">S3</span><span class="sxs-lookup"><span data-stu-id="31e7e-130">S3</span></span> |<span data-ttu-id="31e7e-131">Maximaal 814 MB per minuut per eenheid</span><span class="sxs-lookup"><span data-stu-id="31e7e-131">Up to 814 MB/minute per unit</span></span><br/><span data-ttu-id="31e7e-132">(1144.4 GB/dag/unit)</span><span class="sxs-lookup"><span data-stu-id="31e7e-132">(1144.4 GB/day/unit)</span></span> |<span data-ttu-id="31e7e-133">Gemiddelde van 208,333 berichten per minuut per eenheid</span><span class="sxs-lookup"><span data-stu-id="31e7e-133">Average of 208,333 messages/minute per unit</span></span><br/><span data-ttu-id="31e7e-134">(300 miljoen berichten per dag per eenheid)</span><span class="sxs-lookup"><span data-stu-id="31e7e-134">(300 million messages/day per unit)</span></span> |

## <a name="identity-registry-operation-throughput"></a><span data-ttu-id="31e7e-135">Identiteit register bewerking doorvoer</span><span class="sxs-lookup"><span data-stu-id="31e7e-135">Identity registry operation throughput</span></span>
<span data-ttu-id="31e7e-136">IoT Hub identiteit registerbewerkingen zijn niet moet runtime-bewerkingen, zoals ze voornamelijk zijn gerelateerd aan apparaten inrichten.</span><span class="sxs-lookup"><span data-stu-id="31e7e-136">IoT Hub identity registry operations are not supposed to be run-time operations, as they are mostly related to device provisioning.</span></span>

<span data-ttu-id="31e7e-137">Zie voor specifieke burst prestaties cijfers [IoT Hub quota en vertragingen][IoT Hub quotas and throttles].</span><span class="sxs-lookup"><span data-stu-id="31e7e-137">For specific burst performance numbers, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles].</span></span>

## <a name="sharding"></a><span data-ttu-id="31e7e-138">Sharding</span><span class="sxs-lookup"><span data-stu-id="31e7e-138">Sharding</span></span>
<span data-ttu-id="31e7e-139">Terwijl een enkele IoT-hub naar miljoenen apparaten uitbreiden kunt, vereist soms uw oplossing specifieke prestatiekenmerken die een enkele iothub kan niet worden gegarandeerd.</span><span class="sxs-lookup"><span data-stu-id="31e7e-139">While a single IoT hub can scale to millions of devices, sometimes your solution requires specific performance characteristics that a single IoT hub cannot guarantee.</span></span> <span data-ttu-id="31e7e-140">In dat geval wordt het aanbevolen dat u uw apparaten in meerdere IoT hubs partitioneren.</span><span class="sxs-lookup"><span data-stu-id="31e7e-140">In that case, it is recommended that you partition your devices into multiple IoT hubs.</span></span> <span data-ttu-id="31e7e-141">Meerdere IoT hubs verkeer bursts vloeiend en verkrijgen van de vereiste doorvoer of bewerking tarieven die vereist zijn.</span><span class="sxs-lookup"><span data-stu-id="31e7e-141">Multiple IoT hubs smooth traffic bursts and obtain the required throughput or operation rates that are required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31e7e-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="31e7e-142">Next steps</span></span>
<span data-ttu-id="31e7e-143">Als u wilt de mogelijkheden van IoT Hub verder verkennen, Zie:</span><span class="sxs-lookup"><span data-stu-id="31e7e-143">To further explore the capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="31e7e-144">[Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="31e7e-144">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="31e7e-145">[Een apparaat simuleren met Azure IoT rand][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="31e7e-145">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[IoT Hub quotas and throttles]: iot-hub-devguide-quotas-throttling.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
