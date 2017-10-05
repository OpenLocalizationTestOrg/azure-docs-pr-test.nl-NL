---
title: Verbinding maken met een Raspberry Pi Azure IoT Suite | Microsoft Docs
description: Zelfstudies met behulp van Node.js- of C kunt u informatie over het gebruik van de Microsoft Azure IoT Starter Kit voor de frambozen Pi 3 en de oplossing voor externe controle IoT Suite. U kunt een zelfstudie die simuleert telemetrie, of waarmee externe firmware-updates die gebruikmaakt van echte sensoren hebt gekozen.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/26/2017
ms.author: dobett
ms.openlocfilehash: eaa6a21a08bd9068b5335a8167f54c2aa387e0e5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="connect-your-microsoft-azure-iot-raspberry-pi-3-starter-kit-to-the-remote-monitoring-solution"></a><span data-ttu-id="99888-104">Verbinding maken met uw Microsoft Azure IoT frambozen Pi 3 Starter Kit de oplossing voor externe controle</span><span class="sxs-lookup"><span data-stu-id="99888-104">Connect your Microsoft Azure IoT Raspberry Pi 3 Starter Kit to the remote monitoring solution</span></span>

<span data-ttu-id="99888-105">De zelfstudies in deze sectie kunnen u meer informatie over hoe een frambozen Pi 3-apparaat verbindt met de oplossing voor externe controle.</span><span class="sxs-lookup"><span data-stu-id="99888-105">The tutorials in this section help you learn how to connect a Raspberry Pi 3 device to the remote monitoring solution.</span></span> <span data-ttu-id="99888-106">De zelfstudie geschikt is voor de gewenste programmeertaal kiezen en de of u hebt de sensor hardware beschikbaar voor gebruik met uw frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="99888-106">Choose the tutorial appropriate to your preferred programming language and the whether you have the sensor hardware available to use with your Raspberry Pi.</span></span>

## <a name="the-tutorials"></a><span data-ttu-id="99888-107">De zelfstudies</span><span class="sxs-lookup"><span data-stu-id="99888-107">The tutorials</span></span>

| <span data-ttu-id="99888-108">Zelfstudie</span><span class="sxs-lookup"><span data-stu-id="99888-108">Tutorial</span></span> | <span data-ttu-id="99888-109">Opmerkingen</span><span class="sxs-lookup"><span data-stu-id="99888-109">Notes</span></span> | <span data-ttu-id="99888-110">Talen</span><span class="sxs-lookup"><span data-stu-id="99888-110">Languages</span></span> |
| -------- | ----- | --------- |
| <span data-ttu-id="99888-111">Gesimuleerde telemetrie (basis)</span><span class="sxs-lookup"><span data-stu-id="99888-111">Simulated telemetry (Basic)</span></span>| <span data-ttu-id="99888-112">Sensorgegevens simuleert.</span><span class="sxs-lookup"><span data-stu-id="99888-112">Simulates sensor data.</span></span> <span data-ttu-id="99888-113">Maakt gebruik van een zelfstandige frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="99888-113">Uses a standalone Raspberry Pi.</span></span> | <span data-ttu-id="99888-114">[C][lnk-c-simulator], [Node.js][lnk-node-simulator]</span><span class="sxs-lookup"><span data-stu-id="99888-114">[C][lnk-c-simulator], [Node.js][lnk-node-simulator]</span></span> |
| <span data-ttu-id="99888-115">Echte temperatuursensor (tussenliggend)</span><span class="sxs-lookup"><span data-stu-id="99888-115">Real sensor (Intermediate)</span></span> | <span data-ttu-id="99888-116">Maakt gebruik van gegevens uit een sensor BME280 is verbonden met uw frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="99888-116">Uses data from a BME280 sensor connected to your Raspberry Pi.</span></span> | <span data-ttu-id="99888-117">[C][lnk-c-basic], [Node.js][lnk-node-basic]</span><span class="sxs-lookup"><span data-stu-id="99888-117">[C][lnk-c-basic], [Node.js][lnk-node-basic]</span></span> |
| <span data-ttu-id="99888-118">Implementeer firmware-update (Geavanceerd)</span><span class="sxs-lookup"><span data-stu-id="99888-118">Implement firmware update (Advanced)</span></span>| <span data-ttu-id="99888-119">Maakt gebruik van gegevens uit een sensor BME280 is verbonden met uw frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="99888-119">Uses data from a BME280 sensor connected to your Raspberry Pi.</span></span> <span data-ttu-id="99888-120">Hiermee kunt externe firmware-updates op uw frambozen Pi.</span><span class="sxs-lookup"><span data-stu-id="99888-120">Enables remote firmware updates on your Raspberry Pi.</span></span> | <span data-ttu-id="99888-121">[C][lnk-c-advanced], [Node.js][lnk-node-advanced]</span><span class="sxs-lookup"><span data-stu-id="99888-121">[C][lnk-c-advanced], [Node.js][lnk-node-advanced]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="99888-122">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="99888-122">Next steps</span></span>

<span data-ttu-id="99888-123">Ga naar de [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) voor meer voorbeelden en documentatie over Azure IoT.</span><span class="sxs-lookup"><span data-stu-id="99888-123">Visit the [Azure IoT Dev Center](https://azure.microsoft.com/develop/iot/) for more samples and documentation on Azure IoT.</span></span>

[lnk-node-simulator]: iot-suite-raspberry-pi-kit-node-get-started-simulator.md
[lnk-node-basic]: iot-suite-raspberry-pi-kit-node-get-started-basic.md
[lnk-node-advanced]: iot-suite-raspberry-pi-kit-node-get-started-advanced.md
[lnk-c-simulator]: iot-suite-raspberry-pi-kit-c-get-started-simulator.md
[lnk-c-basic]: iot-suite-raspberry-pi-kit-c-get-started-basic.md
[lnk-c-advanced]: iot-suite-raspberry-pi-kit-c-get-started-advanced.md