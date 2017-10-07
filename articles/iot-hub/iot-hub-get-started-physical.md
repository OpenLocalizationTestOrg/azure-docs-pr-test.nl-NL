---
title: Verbinding maken met fysieke apparaten tooAzure IoT-Hub aan de slag | Microsoft Docs
description: Meer informatie over hoe tooconnect fysieke apparaten en boards tooAzure IoT Hub. Uw apparaten kunnen verzenden telemetrie tooIoT Hub en IoT-Hub kunt controleren en beheren van uw apparaten.
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
keywords: Azure iot hub-zelfstudie
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: dobett
ms.openlocfilehash: 47ce289c438b2f495d499d724c38ddc4b3307425
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-get-started-with-physical-devices-tutorials"></a><span data-ttu-id="1bb03-105">Azure IoT-Hub aan de slag met zelfstudies voor fysieke apparaten</span><span class="sxs-lookup"><span data-stu-id="1bb03-105">Azure IoT Hub get started with physical devices tutorials</span></span>

<span data-ttu-id="1bb03-106">Deze zelfstudies introduceren tooAzure IoT Hub en Hallo apparaat-SDK's.</span><span class="sxs-lookup"><span data-stu-id="1bb03-106">These tutorials introduce you tooAzure IoT Hub and hello device SDKs.</span></span> <span data-ttu-id="1bb03-107">Hallo zelfstudies omvatten algemene IoT scenario's toodemonstrate Hallo mogelijkheden van IoT-Hub.</span><span class="sxs-lookup"><span data-stu-id="1bb03-107">hello tutorials cover common IoT scenarios toodemonstrate hello capabilities of IoT Hub.</span></span> <span data-ttu-id="1bb03-108">Hallo zelfstudies ook laten zien hoe toocombine IoT Hub met andere Azure-services en hulpprogramma's voor toobuild meer krachtige IoT-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="1bb03-108">hello tutorials also illustrate how toocombine IoT Hub with other Azure services and tools toobuild more powerful IoT solutions.</span></span> <span data-ttu-id="1bb03-109">Hallo zelfstudies die worden vermeld in Hallo na tabel tonen u hoe toocreate fysieke IoT-apparaten.</span><span class="sxs-lookup"><span data-stu-id="1bb03-109">hello tutorials listed in hello following table show you how toocreate physical IoT devices.</span></span>

| <span data-ttu-id="1bb03-110">IoT-apparaat</span><span class="sxs-lookup"><span data-stu-id="1bb03-110">IoT device</span></span>                       | <span data-ttu-id="1bb03-111">Programmeertaal</span><span class="sxs-lookup"><span data-stu-id="1bb03-111">Programming language</span></span> |
|---------------------------------|----------------------|
| <span data-ttu-id="1bb03-112">Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="1bb03-112">Raspberry Pi</span></span>                    | <span data-ttu-id="1bb03-113">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span><span class="sxs-lookup"><span data-stu-id="1bb03-113">[Python][Pi_Py], [Node.js][Pi_Nd], [C][Pi_C]</span></span>  |
| <span data-ttu-id="1bb03-114">IoT DevKit</span><span class="sxs-lookup"><span data-stu-id="1bb03-114">IoT DevKit</span></span>                      | <span data-ttu-id="1bb03-115">[Arduino in VSCode][DevKit]</span><span class="sxs-lookup"><span data-stu-id="1bb03-115">[Arduino in VSCode][DevKit]</span></span>     |
| <span data-ttu-id="1bb03-116">Intel Edison</span><span class="sxs-lookup"><span data-stu-id="1bb03-116">Intel Edison</span></span>                    | <span data-ttu-id="1bb03-117">[Node.js][Ed_Nd], [C][Ed_C]</span><span class="sxs-lookup"><span data-stu-id="1bb03-117">[Node.js][Ed_Nd], [C][Ed_C]</span></span>           |
| <span data-ttu-id="1bb03-118">Adafruit Doezelaar HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="1bb03-118">Adafruit Feather HUZZAH ESP8266</span></span> | <span data-ttu-id="1bb03-119">[Arduino][Hu_Ard]</span><span class="sxs-lookup"><span data-stu-id="1bb03-119">[Arduino][Hu_Ard]</span></span>              |
| <span data-ttu-id="1bb03-120">Sparkfun ESP8266 ding Dev</span><span class="sxs-lookup"><span data-stu-id="1bb03-120">Sparkfun ESP8266 Thing Dev</span></span>      | <span data-ttu-id="1bb03-121">[Arduino][Th_Ard]</span><span class="sxs-lookup"><span data-stu-id="1bb03-121">[Arduino][Th_Ard]</span></span>              |
| <span data-ttu-id="1bb03-122">Adafruit Doezelaar M0</span><span class="sxs-lookup"><span data-stu-id="1bb03-122">Adafruit Feather M0</span></span>             | <span data-ttu-id="1bb03-123">[Arduino][M0_Ard]</span><span class="sxs-lookup"><span data-stu-id="1bb03-123">[Arduino][M0_Ard]</span></span>              |

<span data-ttu-id="1bb03-124">Bovendien kunt u een IoT-Edge gateway tooenable apparaten tooconnect tooyour IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="1bb03-124">In addition, you can use an IoT Edge gateway tooenable devices tooconnect tooyour IoT hub.</span></span>

| <span data-ttu-id="1bb03-125">Gateway-apparaat</span><span class="sxs-lookup"><span data-stu-id="1bb03-125">Gateway device</span></span>               | <span data-ttu-id="1bb03-126">Programmeertaal</span><span class="sxs-lookup"><span data-stu-id="1bb03-126">Programming language</span></span> | <span data-ttu-id="1bb03-127">Platform</span><span class="sxs-lookup"><span data-stu-id="1bb03-127">Platform</span></span>         |
|------------------------------|----------------------|------------------|
| <span data-ttu-id="1bb03-128">Intel NUC (model DE3815TYKE)</span><span class="sxs-lookup"><span data-stu-id="1bb03-128">Intel NUC (model DE3815TYKE)</span></span> | <span data-ttu-id="1bb03-129">C</span><span class="sxs-lookup"><span data-stu-id="1bb03-129">C</span></span>                    | <span data-ttu-id="1bb03-130">[De o Linux][NUC_Lnx]</span><span class="sxs-lookup"><span data-stu-id="1bb03-130">[Wind River Linux][NUC_Lnx]</span></span> |

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
[NUC_Lnx]: iot-hub-gateway-kit-c-lesson1-set-up-nuc.md
