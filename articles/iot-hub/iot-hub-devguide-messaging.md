---
title: Inzicht in Azure IoT Hub messaging | Microsoft Docs
description: Handleiding voor ontwikkelaars - apparaat-naar-cloud- en cloud-naar-apparaat met IoT Hub berichten. Bevat informatie over berichtindelingen en ondersteunde communicatieprotocollen.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3fc5f1a3-3711-4611-9897-d4db079b4250
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: f54398d7ac46bf178d2bb603669b399d25370736
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="device-to-cloud-and-cloud-to-device-messaging-with-iot-hub"></a><span data-ttu-id="3d1c7-104">Apparaat-naar-cloud- en cloud-naar-apparaat met IoT Hub messaging</span><span class="sxs-lookup"><span data-stu-id="3d1c7-104">Device-to-cloud and cloud-to-device messaging with IoT Hub</span></span>

<span data-ttu-id="3d1c7-105">Gebruik IoT Hub messaging om te communiceren met uw apparaten met:</span><span class="sxs-lookup"><span data-stu-id="3d1c7-105">Use IoT Hub messaging to communicate with your devices by:</span></span>

* <span data-ttu-id="3d1c7-106">Verzenden van [apparaat-naar-cloud] [ lnk-d2c] berichten van uw apparaten aan uw oplossing voor back-end.</span><span class="sxs-lookup"><span data-stu-id="3d1c7-106">Sending [device-to-cloud][lnk-d2c] messages from your devices to your solution back end.</span></span>
* <span data-ttu-id="3d1c7-107">Verzenden van [cloud-naar-apparaat] [ lnk-c2d] berichten van de oplossing voor back-end op uw apparaten.</span><span class="sxs-lookup"><span data-stu-id="3d1c7-107">Sending [cloud-to-device][lnk-c2d] messages from the solution back end to your devices.</span></span>

<span data-ttu-id="3d1c7-108">Core-eigenschappen van de IoT Hub messaging-functionaliteit zijn de betrouwbaarheid en duurzaamheid van berichten.</span><span class="sxs-lookup"><span data-stu-id="3d1c7-108">Core properties of IoT Hub messaging functionality are the reliability and durability of messages.</span></span> <span data-ttu-id="3d1c7-109">Deze eigenschappen inschakelen herstelmogelijkheden bij onregelmatige connectiviteit aan de kant van het apparaat en pieken in aan de kant van de cloud voor gebeurtenisverwerking laden.</span><span class="sxs-lookup"><span data-stu-id="3d1c7-109">These properties enable resilience to intermittent connectivity on the device side, and to load spikes in event processing on the cloud side.</span></span> <span data-ttu-id="3d1c7-110">IoT Hub implementeert *ten minste eenmaal* levering wordt gegarandeerd dat voor zowel cloud-naar-apparaat als apparaat-naar-cloud-berichten.</span><span class="sxs-lookup"><span data-stu-id="3d1c7-110">IoT Hub implements *at least once* delivery guarantees for both device-to-cloud and cloud-to-device messaging.</span></span>

<span data-ttu-id="3d1c7-111">Zie de artikelen voor een inleiding tot de mogelijkheden van IoT Hub, [Azure en Internet der dingen] [ lnk-azure-iot] en [overzicht van de service Azure IoT Hub][lnk-iot-hub-overview].</span><span class="sxs-lookup"><span data-stu-id="3d1c7-111">For an introduction to the capabilities of IoT Hub, see the articles [Azure and Internet of Things][lnk-azure-iot] and [Overview of the Azure IoT Hub service][lnk-iot-hub-overview].</span></span>

## <a name="when-to-use-iot-hub-messaging"></a><span data-ttu-id="3d1c7-112">Het gebruik van IoT-Hub messaging</span><span class="sxs-lookup"><span data-stu-id="3d1c7-112">When to use IoT Hub messaging</span></span>

<span data-ttu-id="3d1c7-113">Apparaat-naar-cloud-berichten voor het verzenden van time series Telemetrie en waarschuwingen uit de app op uw apparaat en cloud-naar-apparaat-berichten gebruiken voor eenzijdige meldingen app op uw apparaat.</span><span class="sxs-lookup"><span data-stu-id="3d1c7-113">Use device-to-cloud messages for sending time series telemetry and alerts from your device app, and cloud-to-device messages for one-way notifications to your device app.</span></span>

* <span data-ttu-id="3d1c7-114">Raadpleeg [apparaat-naar-cloud communicatie richtlijnen] [ lnk-d2c-guidance] indien in waarover twijfel bestaat tussen het gebruik van apparaat-naar-cloud-berichten, gemelde eigenschappen of bestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="3d1c7-114">Refer to [Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using device-to-cloud messages, reported properties, or file upload.</span></span>
* <span data-ttu-id="3d1c7-115">Raadpleeg [Cloud-naar-apparaat communicatie richtlijnen] [ lnk-c2d-guidance] indien in waarover twijfel bestaat tussen het gebruik van cloud-naar-apparaat-berichten, gewenste eigenschappen of directe methoden.</span><span class="sxs-lookup"><span data-stu-id="3d1c7-115">Refer to [Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using cloud-to-device messages, desired properties, or direct methods.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d1c7-116">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3d1c7-116">Next steps</span></span>

* <span data-ttu-id="3d1c7-117">Meer informatie over IoT Hub [apparaat-naar-cloud messaging][lnk-d2c].</span><span class="sxs-lookup"><span data-stu-id="3d1c7-117">Learn about IoT Hub [device-to-cloud messaging][lnk-d2c].</span></span>
* <span data-ttu-id="3d1c7-118">Meer informatie over IoT Hub [cloud-naar-apparaat messaging][lnk-c2d].</span><span class="sxs-lookup"><span data-stu-id="3d1c7-118">Learn about IoT Hub [cloud-to-device messaging][lnk-c2d].</span></span>

[lnk-azure-iot]: iot-hub-what-is-azure-iot.md
[lnk-iot-hub-overview]: iot-hub-what-is-iot-hub.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md