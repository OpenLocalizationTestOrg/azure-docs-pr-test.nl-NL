---
title: aaaAzure oplossingen voor Internet der dingen (IoT Suite) | Microsoft Docs
description: Overzicht van de architectuur van een steekproef IoT-oplossing en hoe deze zich verhoudt toodevices, Hallo service Azure IoT Hub, Azure IoT-apparaat-SDK's, Azure IoT service SDK's en andere Azure-services.
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: a859e379-dca7-42fa-bdf6-1125c86ad140
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 2d934e3f988c530de6a242869c021712d2aa1576
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
[!INCLUDE [iot-azure-and-iot](../../includes/iot-azure-and-iot.md)]

## <a name="next-steps"></a><span data-ttu-id="1bc50-103">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="1bc50-103">Next steps</span></span>

<span data-ttu-id="1bc50-104">Azure IoT Hub is een Azure-service voor beveiligde en betrouwbare bidirectionele communicatie tussen de back-end van uw oplossing en miljoenen apparaten.</span><span class="sxs-lookup"><span data-stu-id="1bc50-104">Azure IoT Hub is an Azure service that enables secure and reliable bi-directional communications between your solution back end and millions of devices.</span></span> <span data-ttu-id="1bc50-105">Hiermee kunt Hallo back-end oplossing voor:</span><span class="sxs-lookup"><span data-stu-id="1bc50-105">It enables hello solution back end to:</span></span>

* <span data-ttu-id="1bc50-106">telemetrie op schaal van uw apparaten te ontvangen;</span><span class="sxs-lookup"><span data-stu-id="1bc50-106">Receive telemetry at scale from your devices.</span></span>
* <span data-ttu-id="1bc50-107">Gegevens van uw apparaten tooa stream-gebeurtenisverwerking routeren.</span><span class="sxs-lookup"><span data-stu-id="1bc50-107">Route data from your devices tooa stream event processor.</span></span>
* <span data-ttu-id="1bc50-108">uploads van bestanden vanaf apparaten te ontvangen;</span><span class="sxs-lookup"><span data-stu-id="1bc50-108">Receive file uploads from devices.</span></span>
* <span data-ttu-id="1bc50-109">Cloud-naar-apparaat-berichten toospecific apparaten verzenden.</span><span class="sxs-lookup"><span data-stu-id="1bc50-109">Send cloud-to-device messages toospecific devices.</span></span>

<span data-ttu-id="1bc50-110">U kunt uw eigen back-end oplossing IoT Hub-tooimplement gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1bc50-110">You can use IoT Hub tooimplement your own solution back end.</span></span> <span data-ttu-id="1bc50-111">IoT-Hub bevat bovendien een identiteit register gebruikt tooprovision apparaten, hun beveiligingsreferenties en hun rechten tooconnect toohello IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="1bc50-111">In addition, IoT Hub includes an identity registry used tooprovision devices, their security credentials, and their rights tooconnect toohello IoT hub.</span></span> <span data-ttu-id="1bc50-112">Zie toolearn meer informatie over IoT Hub [wat is IoT Hub?] [lnk-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="1bc50-112">toolearn more about IoT Hub, see [What is IoT Hub?][lnk-iot-hub].</span></span>

<span data-ttu-id="1bc50-113">toolearn hoe Azure IoT Hub kunt standaarden gebaseerd Apparaatbeheer voor u tooremotely beheren, configureren en bijwerken van uw apparaten, Zie [overzicht van Apparaatbeheer met IoT Hub][lnk-device-management].</span><span class="sxs-lookup"><span data-stu-id="1bc50-113">toolearn how Azure IoT Hub enables standards-based device management for you tooremotely manage, configure, and update your devices, see [Overview of device management with IoT Hub][lnk-device-management].</span></span>

<span data-ttu-id="1bc50-114">tooimplement clienttoepassingen op een groot aantal hardwareplatforms en besturingssystemen, kunt u apparaat-hello Azure IoT SDK's.</span><span class="sxs-lookup"><span data-stu-id="1bc50-114">tooimplement client applications on a wide variety of device hardware platforms and operating systems, you can use hello Azure IoT device SDKs.</span></span> <span data-ttu-id="1bc50-115">Hallo apparaat-SDK's bevatten bibliotheken die vergemakkelijken verzenden telemetrie tooan IoT hub en ontvangst cloud-naar-apparaat-berichten.</span><span class="sxs-lookup"><span data-stu-id="1bc50-115">hello device SDKs include libraries that facilitate sending telemetry tooan IoT hub and receiving cloud-to-device messages.</span></span> <span data-ttu-id="1bc50-116">Wanneer u Hallo apparaat-SDK's gebruikt, kunt u kiezen uit diverse netwerk protocollen toocommunicate met IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="1bc50-116">When you use hello device SDKs, you can choose from several network protocols toocommunicate with IoT Hub.</span></span> <span data-ttu-id="1bc50-117">meer, Zie Hallo toolearn [informatie over apparaat-SKD's][lnk-device-sdks].</span><span class="sxs-lookup"><span data-stu-id="1bc50-117">toolearn more, see hello [information about device SDKs][lnk-device-sdks].</span></span>

<span data-ttu-id="1bc50-118">schrijven van code en enkele voorbeelden uitvoeren gestart tooget Zie Hallo [aan de slag met IoT Hub] [ lnk-getstarted] zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="1bc50-118">tooget started writing some code and running some samples, see hello [Get started with IoT Hub][lnk-getstarted] tutorial.</span></span>

<span data-ttu-id="1bc50-119">Wellicht bent u ook geïnteresseerd in [Azure IoT Suite][lnk-iot-suite]. Dit is een verzameling van vooraf geconfigureerde oplossingen.</span><span class="sxs-lookup"><span data-stu-id="1bc50-119">You may also be interested in [Azure IoT Suite][lnk-iot-suite], which is a collection of preconfigured solutions.</span></span> <span data-ttu-id="1bc50-120">IoT Suite kunt u tooget snel aan de slag en IoT-projecten tooaddress algemene IoT-scenario's--zoals externe controle, beheer van bedrijfsmiddelen en voorspeld onderhoud worden geschaald.</span><span class="sxs-lookup"><span data-stu-id="1bc50-120">IoT Suite enables you tooget started quickly and scale IoT projects tooaddress common IoT scenarios--such as remote monitoring, asset management, and predictive maintenance.</span></span>

[lnk-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-iot-hub]: iot-hub-what-is-iot-hub.md
[lnk-iot-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-iotdev]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-device-management-overview.md
