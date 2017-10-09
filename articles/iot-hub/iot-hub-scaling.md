---
title: schalen van aaaAzure Iothub | Microsoft Docs
description: Hoe tooscale uw IoT hub toosupport uw verwachte bericht doorvoer. Bevat een overzicht van ondersteunde Hallo doorvoer voor elke laag en opties voor sharding.
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
ms.openlocfilehash: 3b8bf6c44631c65b34b69752d9043c21db24bb01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-your-iot-hub-solution"></a><span data-ttu-id="31f76-104">Schalen van uw IoT hub-oplossing</span><span class="sxs-lookup"><span data-stu-id="31f76-104">Scale your IoT hub solution</span></span>
<span data-ttu-id="31f76-105">Azure IoT Hub kan tooa miljoenen gelijktijdig verbonden apparaten ondersteunen.</span><span class="sxs-lookup"><span data-stu-id="31f76-105">Azure IoT Hub can support up tooa million simultaneously connected devices.</span></span> <span data-ttu-id="31f76-106">Zie voor meer informatie [IoT Hub prijzen][lnk-pricing].</span><span class="sxs-lookup"><span data-stu-id="31f76-106">For more information, see [IoT Hub pricing][lnk-pricing].</span></span> <span data-ttu-id="31f76-107">Elke eenheid IoT-Hub kunt een bepaald aantal dagelijkse berichten.</span><span class="sxs-lookup"><span data-stu-id="31f76-107">Each IoT Hub unit allows a certain number of daily messages.</span></span>

<span data-ttu-id="31f76-108">tooproperly schalen van uw oplossing, kunt u uw specifieke gebruik van IoT-Hub.</span><span class="sxs-lookup"><span data-stu-id="31f76-108">tooproperly scale your solution, consider your particular use of IoT Hub.</span></span> <span data-ttu-id="31f76-109">Houd rekening met Hallo vereist piek doorvoer voor Hallo volgende categorieën van bewerkingen in het bijzonder:</span><span class="sxs-lookup"><span data-stu-id="31f76-109">In particular, consider hello required peak throughput for hello following categories of operations:</span></span>

* <span data-ttu-id="31f76-110">Apparaat-naar-cloud-berichten</span><span class="sxs-lookup"><span data-stu-id="31f76-110">Device-to-cloud messages</span></span>
* <span data-ttu-id="31f76-111">Cloud-naar-apparaat-berichten</span><span class="sxs-lookup"><span data-stu-id="31f76-111">Cloud-to-device messages</span></span>
* <span data-ttu-id="31f76-112">Registerbewerkingen voor identiteit</span><span class="sxs-lookup"><span data-stu-id="31f76-112">Identity registry operations</span></span>

<span data-ttu-id="31f76-113">Bij toevoeging toothis doorvoer informatie, Zie [IoT Hub quota en vertragingen] [ IoT Hub quotas and throttles] en dienovereenkomstig ontwerpen van uw oplossing.</span><span class="sxs-lookup"><span data-stu-id="31f76-113">In addition toothis throughput information, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles] and design your solution accordingly.</span></span>

## <a name="device-to-cloud-and-cloud-to-device-message-throughput"></a><span data-ttu-id="31f76-114">Apparaat-naar-cloud- en cloud-naar-apparaat bericht doorvoer</span><span class="sxs-lookup"><span data-stu-id="31f76-114">Device-to-cloud and cloud-to-device message throughput</span></span>
<span data-ttu-id="31f76-115">Hallo aanbevolen manier toosize een IoT Hub-oplossing is tooevaluate Hallo-verkeer op basis van per eenheid.</span><span class="sxs-lookup"><span data-stu-id="31f76-115">hello best way toosize an IoT Hub solution is tooevaluate hello traffic on a per-unit basis.</span></span>

<span data-ttu-id="31f76-116">Apparaat-naar-cloudberichten Volg deze richtlijnen volgehouden doorvoer.</span><span class="sxs-lookup"><span data-stu-id="31f76-116">Device-to-cloud messages follow these sustained throughput guidelines.</span></span>

| <span data-ttu-id="31f76-117">Laag</span><span class="sxs-lookup"><span data-stu-id="31f76-117">Tier</span></span> | <span data-ttu-id="31f76-118">Volgehouden doorvoer</span><span class="sxs-lookup"><span data-stu-id="31f76-118">Sustained throughput</span></span> | <span data-ttu-id="31f76-119">Continue verzendsnelheid</span><span class="sxs-lookup"><span data-stu-id="31f76-119">Sustained send rate</span></span> |
| --- | --- | --- |
| <span data-ttu-id="31f76-120">S1</span><span class="sxs-lookup"><span data-stu-id="31f76-120">S1</span></span> |<span data-ttu-id="31f76-121">Up too1111 KB per minuut per eenheid</span><span class="sxs-lookup"><span data-stu-id="31f76-121">Up too1111 KB/minute per unit</span></span><br/><span data-ttu-id="31f76-122">(1,5 GB/dag/unit)</span><span class="sxs-lookup"><span data-stu-id="31f76-122">(1.5 GB/day/unit)</span></span> |<span data-ttu-id="31f76-123">Gemiddelde van 278 berichten per minuut per eenheid</span><span class="sxs-lookup"><span data-stu-id="31f76-123">Average of 278 messages/minute per unit</span></span><br/><span data-ttu-id="31f76-124">(400.000 berichten per dag per eenheid)</span><span class="sxs-lookup"><span data-stu-id="31f76-124">(400,000 messages/day per unit)</span></span> |
| <span data-ttu-id="31f76-125">S2</span><span class="sxs-lookup"><span data-stu-id="31f76-125">S2</span></span> |<span data-ttu-id="31f76-126">Up too16 MB per minuut per eenheid</span><span class="sxs-lookup"><span data-stu-id="31f76-126">Up too16 MB/minute per unit</span></span><br/><span data-ttu-id="31f76-127">(22.8 GB/dag/unit)</span><span class="sxs-lookup"><span data-stu-id="31f76-127">(22.8 GB/day/unit)</span></span> |<span data-ttu-id="31f76-128">Gemiddelde van 4,167 berichten per minuut per eenheid</span><span class="sxs-lookup"><span data-stu-id="31f76-128">Average of 4,167 messages/minute per unit</span></span><br/><span data-ttu-id="31f76-129">(6 miljoen berichten per dag per eenheid)</span><span class="sxs-lookup"><span data-stu-id="31f76-129">(6 million messages/day per unit)</span></span> |
| <span data-ttu-id="31f76-130">S3</span><span class="sxs-lookup"><span data-stu-id="31f76-130">S3</span></span> |<span data-ttu-id="31f76-131">Up too814 MB per minuut per eenheid</span><span class="sxs-lookup"><span data-stu-id="31f76-131">Up too814 MB/minute per unit</span></span><br/><span data-ttu-id="31f76-132">(1144.4 GB/dag/unit)</span><span class="sxs-lookup"><span data-stu-id="31f76-132">(1144.4 GB/day/unit)</span></span> |<span data-ttu-id="31f76-133">Gemiddelde van 208,333 berichten per minuut per eenheid</span><span class="sxs-lookup"><span data-stu-id="31f76-133">Average of 208,333 messages/minute per unit</span></span><br/><span data-ttu-id="31f76-134">(300 miljoen berichten per dag per eenheid)</span><span class="sxs-lookup"><span data-stu-id="31f76-134">(300 million messages/day per unit)</span></span> |

## <a name="identity-registry-operation-throughput"></a><span data-ttu-id="31f76-135">Identiteit register bewerking doorvoer</span><span class="sxs-lookup"><span data-stu-id="31f76-135">Identity registry operation throughput</span></span>
<span data-ttu-id="31f76-136">IoT Hub identiteit registerbewerkingen moeten niet toobe runtime-bewerkingen, zoals ze voornamelijk gerelateerde toodevice inrichten zijn.</span><span class="sxs-lookup"><span data-stu-id="31f76-136">IoT Hub identity registry operations are not supposed toobe run-time operations, as they are mostly related toodevice provisioning.</span></span>

<span data-ttu-id="31f76-137">Zie voor specifieke burst prestaties cijfers [IoT Hub quota en vertragingen][IoT Hub quotas and throttles].</span><span class="sxs-lookup"><span data-stu-id="31f76-137">For specific burst performance numbers, see [IoT Hub quotas and throttles][IoT Hub quotas and throttles].</span></span>

## <a name="sharding"></a><span data-ttu-id="31f76-138">Sharding</span><span class="sxs-lookup"><span data-stu-id="31f76-138">Sharding</span></span>
<span data-ttu-id="31f76-139">Terwijl een enkele IoT-hub toomillions van apparaten schalen kunt, vereist soms uw oplossing specifieke prestatiekenmerken die een enkele iothub kan niet worden gegarandeerd.</span><span class="sxs-lookup"><span data-stu-id="31f76-139">While a single IoT hub can scale toomillions of devices, sometimes your solution requires specific performance characteristics that a single IoT hub cannot guarantee.</span></span> <span data-ttu-id="31f76-140">In dat geval wordt het aanbevolen dat u uw apparaten in meerdere IoT hubs partitioneren.</span><span class="sxs-lookup"><span data-stu-id="31f76-140">In that case, it is recommended that you partition your devices into multiple IoT hubs.</span></span> <span data-ttu-id="31f76-141">Meerdere IoT hubs verkeer bursts vloeiend en verkrijgen Hallo vereist doorvoer of bewerking tarieven die vereist zijn.</span><span class="sxs-lookup"><span data-stu-id="31f76-141">Multiple IoT hubs smooth traffic bursts and obtain hello required throughput or operation rates that are required.</span></span>

## <a name="next-steps"></a><span data-ttu-id="31f76-142">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="31f76-142">Next steps</span></span>
<span data-ttu-id="31f76-143">toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:</span><span class="sxs-lookup"><span data-stu-id="31f76-143">toofurther explore hello capabilities of IoT Hub, see:</span></span>

* <span data-ttu-id="31f76-144">[Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide]</span><span class="sxs-lookup"><span data-stu-id="31f76-144">[IoT Hub developer guide][lnk-devguide]</span></span>
* <span data-ttu-id="31f76-145">[Een apparaat simuleren met Azure IoT rand][lnk-iotedge]</span><span class="sxs-lookup"><span data-stu-id="31f76-145">[Simulating a device with Azure IoT Edge][lnk-iotedge]</span></span>

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[IoT Hub quotas and throttles]: iot-hub-devguide-quotas-throttling.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
