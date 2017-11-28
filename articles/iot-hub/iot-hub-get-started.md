---
title: Azure IoT Hub - aan de slag IoT-apparaten toohello cloud verbinden | Microsoft Docs
description: Meer informatie over hoe tooconnect uw IoT-boards en starter Kit tooAzure IoT Hub. Uw apparaten kunnen verzenden telemetrie tooIoT Hub en IoT-Hub kunt controleren en beheren van uw apparaten.
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
keywords: Azure iot hub-zelfstudie
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: dobett
ms.openlocfilehash: 6dc956308009091532019ff84aec881f042f0104
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-get-started-tutorials"></a><span data-ttu-id="ed1b3-105">Azure IoT Hub get zelfstudies gestart</span><span class="sxs-lookup"><span data-stu-id="ed1b3-105">Azure IoT Hub get started tutorials</span></span>

<span data-ttu-id="ed1b3-106">U kunt Azure IoT Hub en hello Azure IoT SDK's toobuild Internet der dingen (IoT)-oplossingen voor apparaten:</span><span class="sxs-lookup"><span data-stu-id="ed1b3-106">You can use Azure IoT Hub and hello Azure IoT device SDKs toobuild Internet of Things (IoT) solutions:</span></span>

* <span data-ttu-id="ed1b3-107">Azure IoT Hub is een volledig beheerde service in Hallo cloud die veilig verbindt, bewaakt en beheert uw IoT-apparaten.</span><span class="sxs-lookup"><span data-stu-id="ed1b3-107">Azure IoT Hub is a fully managed service in hello cloud that securely connects, monitors, and manages your IoT devices.</span></span> <span data-ttu-id="ed1b3-108">Gebruik hello Azure IoT-apparaat-SDK's tooimplement uw IoT-apparaten.</span><span class="sxs-lookup"><span data-stu-id="ed1b3-108">Use hello Azure IoT Device SDKs tooimplement your IoT devices.</span></span>
* <span data-ttu-id="ed1b3-109">Gebruik een IoT-gateway in complexere IoT-scenario's.</span><span class="sxs-lookup"><span data-stu-id="ed1b3-109">Use an IoT gateway in more complex IoT scenarios.</span></span> <span data-ttu-id="ed1b3-110">Waar moet u wel tooconsider factoren zoals de oudere apparaten, kosten van bandbreedte, beveiliging en privacy-beleid of gegevensverwerking rand weergeven.</span><span class="sxs-lookup"><span data-stu-id="ed1b3-110">For example, where you need tooconsider factors such as legacy devices, bandwidth costs, security and privacy policies, or edge data processing.</span></span> <span data-ttu-id="ed1b3-111">In deze scenario's gebruikt u Azure IoT rand tooimplement een gateway die is verbonden apparaten tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="ed1b3-111">In these scenarios, you use Azure IoT Edge tooimplement a gateway that connects devices tooyour IoT hub.</span></span>

## <a name="what-hello-tutorials-cover"></a><span data-ttu-id="ed1b3-112">Wat Hallo zelfstudies hebben betrekking op</span><span class="sxs-lookup"><span data-stu-id="ed1b3-112">What hello tutorials cover</span></span>

<span data-ttu-id="ed1b3-113">Deze zelfstudies introduceren tooAzure IoT Hub en Hallo apparaat-SDK's.</span><span class="sxs-lookup"><span data-stu-id="ed1b3-113">These tutorials introduce you tooAzure IoT Hub and hello device SDKs.</span></span> <span data-ttu-id="ed1b3-114">Hallo zelfstudies omvatten algemene IoT scenario's toodemonstrate Hallo mogelijkheden van IoT-Hub.</span><span class="sxs-lookup"><span data-stu-id="ed1b3-114">hello tutorials cover common IoT scenarios toodemonstrate hello capabilities of IoT Hub.</span></span> <span data-ttu-id="ed1b3-115">Hallo zelfstudies ook laten zien hoe toocombine IoT Hub met andere Azure-services en hulpprogramma's voor toobuild meer krachtige IoT-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="ed1b3-115">hello tutorials also illustrate how toocombine IoT Hub with other Azure services and tools toobuild more powerful IoT solutions.</span></span> <span data-ttu-id="ed1b3-116">In de zelfstudies hello, kunt u toouse gesimuleerde of echte IoT-apparaten.</span><span class="sxs-lookup"><span data-stu-id="ed1b3-116">In hello tutorials, you can choose toouse either simulated or real IoT devices.</span></span> <span data-ttu-id="ed1b3-117">Bovendien leert u hoe toouse een gateway tooenable apparaten tooconnect tooyour iothub.</span><span class="sxs-lookup"><span data-stu-id="ed1b3-117">In addition, you can learn how toouse a gateway tooenable devices tooconnect tooyour IoT hub.</span></span>

## <a name="set-up-your-device"></a><span data-ttu-id="ed1b3-118">Uw apparaat instellen</span><span class="sxs-lookup"><span data-stu-id="ed1b3-118">Set up your device</span></span>

<span data-ttu-id="ed1b3-119">Verbinding maken met een IoT-apparaat of de gateway tooAzure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ed1b3-119">Connect an IoT device or gateway tooAzure IoT Hub.</span></span> <span data-ttu-id="ed1b3-120">U kunt een fysieke of gesimuleerde apparaat tooget gestart:</span><span class="sxs-lookup"><span data-stu-id="ed1b3-120">You can choose a physical or simulated device tooget started:</span></span>

| <span data-ttu-id="ed1b3-121">IoT-apparaat</span><span class="sxs-lookup"><span data-stu-id="ed1b3-121">IoT device</span></span>                       | <span data-ttu-id="ed1b3-122">Programmeertaal</span><span class="sxs-lookup"><span data-stu-id="ed1b3-122">Programming language</span></span> |
|----------------------------------|----------------------|
| <span data-ttu-id="ed1b3-123">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="ed1b3-123">Raspberry Pi</span></span>                     | <span data-ttu-id="ed1b3-124">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span><span class="sxs-lookup"><span data-stu-id="ed1b3-124">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span></span>  |
| <span data-ttu-id="ed1b3-125">IoT DevKit</span><span class="sxs-lookup"><span data-stu-id="ed1b3-125">IoT DevKit</span></span>                       | <span data-ttu-id="ed1b3-126">[Arduino in VSCode][DevKit]</span><span class="sxs-lookup"><span data-stu-id="ed1b3-126">[Arduino in VSCode][DevKit]</span></span>     |
| <span data-ttu-id="ed1b3-127">Intel Edison</span><span class="sxs-lookup"><span data-stu-id="ed1b3-127">Intel Edison</span></span>                     | <span data-ttu-id="ed1b3-128">[Node.js][Ed_Nd], [C][Ed_C]</span><span class="sxs-lookup"><span data-stu-id="ed1b3-128">[Node.js][Ed_Nd], [C][Ed_C]</span></span>    |
| <span data-ttu-id="ed1b3-129">Adafruit Doezelaar HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="ed1b3-129">Adafruit Feather HUZZAH ESP8266</span></span>  | <span data-ttu-id="ed1b3-130">[Arduino][Hu_Ard]</span><span class="sxs-lookup"><span data-stu-id="ed1b3-130">[Arduino][Hu_Ard]</span></span>              |
| <span data-ttu-id="ed1b3-131">Sparkfun ESP8266 ding Dev</span><span class="sxs-lookup"><span data-stu-id="ed1b3-131">Sparkfun ESP8266 Thing Dev</span></span>       | <span data-ttu-id="ed1b3-132">[Arduino][Th_Ard]</span><span class="sxs-lookup"><span data-stu-id="ed1b3-132">[Arduino][Th_Ard]</span></span>              |
| <span data-ttu-id="ed1b3-133">Adafruit Doezelaar M0</span><span class="sxs-lookup"><span data-stu-id="ed1b3-133">Adafruit Feather M0</span></span>              | <span data-ttu-id="ed1b3-134">[Arduino][M0_Ard]</span><span class="sxs-lookup"><span data-stu-id="ed1b3-134">[Arduino][M0_Ard]</span></span>              |
| <span data-ttu-id="ed1b3-135">Gesimuleerde apparaat op PC</span><span class="sxs-lookup"><span data-stu-id="ed1b3-135">Simulated device on PC</span></span>           | <span data-ttu-id="ed1b3-136">[.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd], [Python][Sim_Pyth]</span><span class="sxs-lookup"><span data-stu-id="ed1b3-136">[.NET][Sim_NET], [Java][Sim_Jav], [Node.js][Sim_Nd], [Python][Sim_Pyth]</span></span> |
| <span data-ttu-id="ed1b3-137">Online apparaatsimulator</span><span class="sxs-lookup"><span data-stu-id="ed1b3-137">Online device simulator</span></span>         | <span data-ttu-id="ed1b3-138">[Raspberry Pi (Node.js)][Ol_Sim]</span><span class="sxs-lookup"><span data-stu-id="ed1b3-138">[Raspberry Pi (Node.js)][Ol_Sim]</span></span> |

<span data-ttu-id="ed1b3-139">Bovendien kunt u een IoT-Edge gateway tooenable apparaten tooconnect tooyour IoT-hub:</span><span class="sxs-lookup"><span data-stu-id="ed1b3-139">In addition, you can use an IoT Edge gateway tooenable devices tooconnect tooyour IoT hub:</span></span>

| <span data-ttu-id="ed1b3-140">Gateway-apparaat</span><span class="sxs-lookup"><span data-stu-id="ed1b3-140">Gateway device</span></span>               | <span data-ttu-id="ed1b3-141">Programmeertaal</span><span class="sxs-lookup"><span data-stu-id="ed1b3-141">Programming language</span></span> | <span data-ttu-id="ed1b3-142">Platform</span><span class="sxs-lookup"><span data-stu-id="ed1b3-142">Platform</span></span>         |
|------------------------------|----------------------|------------------|
| <span data-ttu-id="ed1b3-143">Intel NUC (model DE3815TYKE)</span><span class="sxs-lookup"><span data-stu-id="ed1b3-143">Intel NUC (model DE3815TYKE)</span></span> | <span data-ttu-id="ed1b3-144">C</span><span class="sxs-lookup"><span data-stu-id="ed1b3-144">C</span></span>                    | <span data-ttu-id="ed1b3-145">[De o Linux][NUC_Lnx]</span><span class="sxs-lookup"><span data-stu-id="ed1b3-145">[Wind River Linux][NUC_Lnx]</span></span> |
| <span data-ttu-id="ed1b3-146">Gesimuleerde gateway</span><span class="sxs-lookup"><span data-stu-id="ed1b3-146">Simulated gateway</span></span>            | <span data-ttu-id="ed1b3-147">C</span><span class="sxs-lookup"><span data-stu-id="ed1b3-147">C</span></span>                    | <span data-ttu-id="ed1b3-148">[Linux][Sim_Lnx], [Windows][Sim_Win]</span><span class="sxs-lookup"><span data-stu-id="ed1b3-148">[Linux][Sim_Lnx], [Windows][Sim_Win]</span></span> |

[!INCLUDE [iot-hub-get-started-extended](../../includes/iot-hub-get-started-extended.md)]

[Pi_Nd]: iot-hub-raspberry-pi-kit-node-get-started.md
[Pi_C]: iot-hub-raspberry-pi-kit-c-get-started.md
[Pi_Py]: iot-hub-raspberry-pi-kit-python-get-started.md
[DevKit]: iot-hub-arduino-iot-devkit-az3166-get-started.md
[Ed_Nd]: iot-hub-intel-edison-kit-node-get-started.md
[Ed_C]: iot-hub-intel-edison-kit-c-get-started.md
[Hu_Ard]: iot-hub-arduino-huzzah-esp8266-get-started.md
[Th_Ard]: iot-hub-sparkfun-esp8266-thing-dev-get-started.md
[M0_Ard]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started.md
[Sim_NET]: iot-hub-csharp-csharp-getstarted.md
[Sim_Jav]: iot-hub-java-java-getstarted.md
[Sim_Nd]: iot-hub-node-node-getstarted.md
[Sim_Pyth]: iot-hub-python-getstarted.md
[NUC_Lnx]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
[Sim_Lnx]: iot-hub-linux-iot-edge-get-started.md
[Sim_Win]: iot-hub-windows-iot-edge-get-started.md
[Ol_Sim]: iot-hub-raspberry-pi-web-simulator-get-started.md
