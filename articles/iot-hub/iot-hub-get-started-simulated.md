---
title: Gesimuleerde apparaten verbinding laten maken met Azure IoT Hub aan de slag | Microsoft Docs
description: Informatie over het maken van de gesimuleerde IoT-apparaten en verbind ze met Azure IoT Hub. Uw apparaten kunnen verzenden telemetrie naar IoT Hub en Iot-Hub kunt controleren en beheren van uw apparaten.
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
ms.date: 06/02/2017
ms.author: dobett
ms.openlocfilehash: 436b3057509a831837159e814490959a2d7455a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-iot-hub-get-started-with-simulated-devices-tutorials"></a><span data-ttu-id="b06d6-105">Azure IoT-Hub aan de slag met gesimuleerde apparaten zelfstudies</span><span class="sxs-lookup"><span data-stu-id="b06d6-105">Azure IoT Hub get started with simulated devices tutorials</span></span>

<span data-ttu-id="b06d6-106">Deze zelfstudies vindt u Azure IoT Hub en het apparaat-SDK's.</span><span class="sxs-lookup"><span data-stu-id="b06d6-106">These tutorials introduce you to Azure IoT Hub and the device SDKs.</span></span> <span data-ttu-id="b06d6-107">De zelfstudies betrekking hebben op algemene IoT-scenario's om aan te tonen van de mogelijkheden van IoT-Hub.</span><span class="sxs-lookup"><span data-stu-id="b06d6-107">The tutorials cover common IoT scenarios to demonstrate the capabilities of IoT Hub.</span></span> <span data-ttu-id="b06d6-108">De zelfstudies ook te laten zien hoe IoT Hub worden gecombineerd met andere Azure-services en hulpprogramma's voor het bouwen van krachtige IoT-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="b06d6-108">The tutorials also illustrate how to combine IoT Hub with other Azure services and tools to build more powerful IoT solutions.</span></span> <span data-ttu-id="b06d6-109">De zelfstudies die worden vermeld in de volgende tabel beschreven hoe u gesimuleerde IoT-apparaten maken.</span><span class="sxs-lookup"><span data-stu-id="b06d6-109">The tutorials listed in the following table show you how to create simulated IoT devices.</span></span>

| <span data-ttu-id="b06d6-110">Programmeertaal</span><span class="sxs-lookup"><span data-stu-id="b06d6-110">Programming language</span></span> |
|----------------------|
| <span data-ttu-id="b06d6-111">[.NET][Sim_NET]</span><span class="sxs-lookup"><span data-stu-id="b06d6-111">[.NET][Sim_NET]</span></span>      |
| <span data-ttu-id="b06d6-112">[Java][Sim_Jav]</span><span class="sxs-lookup"><span data-stu-id="b06d6-112">[Java][Sim_Jav]</span></span>      |
| <span data-ttu-id="b06d6-113">[Node.js][Sim_Nd]</span><span class="sxs-lookup"><span data-stu-id="b06d6-113">[Node.js][Sim_Nd]</span></span>    |
| <span data-ttu-id="b06d6-114">[Python][Sim_Pyth]</span><span class="sxs-lookup"><span data-stu-id="b06d6-114">[Python][Sim_Pyth]</span></span>   |

<span data-ttu-id="b06d6-115">Bovendien kunt u een gateway aan de rand van de IoT waarmee gesimuleerde apparaten verbinding maken met uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="b06d6-115">In addition, you can use an IoT Edge gateway to enable simulated devices to connect to your IoT hub.</span></span>

| <span data-ttu-id="b06d6-116">Programmeertaal</span><span class="sxs-lookup"><span data-stu-id="b06d6-116">Programming language</span></span> | <span data-ttu-id="b06d6-117">Platform</span><span class="sxs-lookup"><span data-stu-id="b06d6-117">Platform</span></span>           |
|----------------------|------------------- |
| <span data-ttu-id="b06d6-118">C</span><span class="sxs-lookup"><span data-stu-id="b06d6-118">C</span></span>                    | <span data-ttu-id="b06d6-119">[Linux][Sim_Lnx]</span><span class="sxs-lookup"><span data-stu-id="b06d6-119">[Linux][Sim_Lnx]</span></span>   |
| <span data-ttu-id="b06d6-120">C</span><span class="sxs-lookup"><span data-stu-id="b06d6-120">C</span></span>                    | <span data-ttu-id="b06d6-121">[Windows][Sim_Win]</span><span class="sxs-lookup"><span data-stu-id="b06d6-121">[Windows][Sim_Win]</span></span> |

[!INCLUDE [iot-hub-get-started-extended](../../includes/iot-hub-get-started-extended.md)]

[Sim_NET]: iot-hub-csharp-csharp-getstarted.md
[Sim_Jav]: iot-hub-java-java-getstarted.md
[Sim_Nd]: iot-hub-node-node-getstarted.md
[Sim_Pyth]: iot-hub-python-getstarted.md
[Sim_Lnx]: iot-hub-linux-iot-edge-get-started.md
[Sim_Win]: iot-hub-windows-iot-edge-get-started.md
