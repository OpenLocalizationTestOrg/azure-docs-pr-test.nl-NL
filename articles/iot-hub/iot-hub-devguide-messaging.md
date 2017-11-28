---
title: messaging-aaaUnderstand Azure IoT Hub | Microsoft Docs
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
ms.openlocfilehash: a610741e23e243f392f1c042f9ab4a00d42f734f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="device-to-cloud-and-cloud-to-device-messaging-with-iot-hub"></a><span data-ttu-id="f8e6c-104">Apparaat-naar-cloud- en cloud-naar-apparaat met IoT Hub messaging</span><span class="sxs-lookup"><span data-stu-id="f8e6c-104">Device-to-cloud and cloud-to-device messaging with IoT Hub</span></span>

<span data-ttu-id="f8e6c-105">Gebruik IoT Hub berichten toocommunicate met uw apparaten met:</span><span class="sxs-lookup"><span data-stu-id="f8e6c-105">Use IoT Hub messaging toocommunicate with your devices by:</span></span>

* <span data-ttu-id="f8e6c-106">Verzenden van [apparaat-naar-cloud] [ lnk-d2c] berichten van uw apparaten tooyour oplossing back-end.</span><span class="sxs-lookup"><span data-stu-id="f8e6c-106">Sending [device-to-cloud][lnk-d2c] messages from your devices tooyour solution back end.</span></span>
* <span data-ttu-id="f8e6c-107">Verzenden van [cloud-naar-apparaat] [ lnk-c2d] berichten van Hallo oplossing terug eindigen tooyour apparaten.</span><span class="sxs-lookup"><span data-stu-id="f8e6c-107">Sending [cloud-to-device][lnk-c2d] messages from hello solution back end tooyour devices.</span></span>

<span data-ttu-id="f8e6c-108">Core-eigenschappen van de IoT Hub messaging-functionaliteit zijn Hallo betrouwbaarheid en duurzaamheid van berichten.</span><span class="sxs-lookup"><span data-stu-id="f8e6c-108">Core properties of IoT Hub messaging functionality are hello reliability and durability of messages.</span></span> <span data-ttu-id="f8e6c-109">Deze eigenschappen herstelmogelijkheden toointermittent connectiviteit op Hallo apparaat aan clientzijde inschakelen en tooload bereikt in gebeurtenisverwerking Hallo cloud-zijde.</span><span class="sxs-lookup"><span data-stu-id="f8e6c-109">These properties enable resilience toointermittent connectivity on hello device side, and tooload spikes in event processing on hello cloud side.</span></span> <span data-ttu-id="f8e6c-110">IoT Hub implementeert *ten minste eenmaal* levering wordt gegarandeerd dat voor zowel cloud-naar-apparaat als apparaat-naar-cloud-berichten.</span><span class="sxs-lookup"><span data-stu-id="f8e6c-110">IoT Hub implements *at least once* delivery guarantees for both device-to-cloud and cloud-to-device messaging.</span></span>

<span data-ttu-id="f8e6c-111">Zie voor een inleiding toohello mogelijkheden van IoT Hub, Hallo artikelen [Azure en Internet der dingen] [ lnk-azure-iot] en [overzicht van de service Azure IoT Hub Hallo] [lnk-iot-hub-overview].</span><span class="sxs-lookup"><span data-stu-id="f8e6c-111">For an introduction toohello capabilities of IoT Hub, see hello articles [Azure and Internet of Things][lnk-azure-iot] and [Overview of hello Azure IoT Hub service][lnk-iot-hub-overview].</span></span>

## <a name="when-toouse-iot-hub-messaging"></a><span data-ttu-id="f8e6c-112">Wanneer toouse Iothub messaging</span><span class="sxs-lookup"><span data-stu-id="f8e6c-112">When toouse IoT Hub messaging</span></span>

<span data-ttu-id="f8e6c-113">Apparaat-naar-cloud-berichten voor het verzenden van time series Telemetrie en waarschuwingen uit de app op uw apparaat en cloud-naar-apparaat-berichten voor eenzijdige meldingen tooyour apparaat app gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f8e6c-113">Use device-to-cloud messages for sending time series telemetry and alerts from your device app, and cloud-to-device messages for one-way notifications tooyour device app.</span></span>

* <span data-ttu-id="f8e6c-114">Raadpleeg te[apparaat-naar-cloud communicatie richtlijnen] [ lnk-d2c-guidance] indien in waarover twijfel bestaat tussen het gebruik van apparaat-naar-cloud-berichten, gemelde eigenschappen of bestand uploaden.</span><span class="sxs-lookup"><span data-stu-id="f8e6c-114">Refer too[Device-to-cloud communication guidance][lnk-d2c-guidance] if in doubt between using device-to-cloud messages, reported properties, or file upload.</span></span>
* <span data-ttu-id="f8e6c-115">Raadpleeg te[Cloud-naar-apparaat communicatie richtlijnen] [ lnk-c2d-guidance] indien in waarover twijfel bestaat tussen het gebruik van cloud-naar-apparaat-berichten, gewenste eigenschappen of directe methoden.</span><span class="sxs-lookup"><span data-stu-id="f8e6c-115">Refer too[Cloud-to-device communication guidance][lnk-c2d-guidance] if in doubt between using cloud-to-device messages, desired properties, or direct methods.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f8e6c-116">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f8e6c-116">Next steps</span></span>

* <span data-ttu-id="f8e6c-117">Meer informatie over IoT Hub [apparaat-naar-cloud messaging][lnk-d2c].</span><span class="sxs-lookup"><span data-stu-id="f8e6c-117">Learn about IoT Hub [device-to-cloud messaging][lnk-d2c].</span></span>
* <span data-ttu-id="f8e6c-118">Meer informatie over IoT Hub [cloud-naar-apparaat messaging][lnk-c2d].</span><span class="sxs-lookup"><span data-stu-id="f8e6c-118">Learn about IoT Hub [cloud-to-device messaging][lnk-c2d].</span></span>

[lnk-azure-iot]: iot-hub-what-is-azure-iot.md
[lnk-iot-hub-overview]: iot-hub-what-is-iot-hub.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md