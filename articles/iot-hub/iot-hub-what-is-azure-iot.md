---
title: Azure-oplossingen voor het internet der dingen (IoT-suite) | Microsoft Docs
description: "Overzicht van een voorbeeldoplossing met IoT-architectuur en hoe deze is gekoppeld aan apparaten, de Azure IoT Hub-service, Azure IoT-apparaat-SDK's, Azure IoT-service-SDK’s en andere Azure-services."
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
ms.openlocfilehash: 1d54f090a0e07cd5102cb48cd70a1377845d6654
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
[!INCLUDE [iot-azure-and-iot](../../includes/iot-azure-and-iot.md)]

## <a name="next-steps"></a><span data-ttu-id="d7464-103">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d7464-103">Next steps</span></span>

<span data-ttu-id="d7464-104">Azure IoT Hub is een Azure-service voor beveiligde en betrouwbare bidirectionele communicatie tussen de back-end van uw oplossing en miljoenen apparaten.</span><span class="sxs-lookup"><span data-stu-id="d7464-104">Azure IoT Hub is an Azure service that enables secure and reliable bi-directional communications between your solution back end and millions of devices.</span></span> <span data-ttu-id="d7464-105">U stelt de back-end van de oplossing ermee in staat om:</span><span class="sxs-lookup"><span data-stu-id="d7464-105">It enables the solution back end to:</span></span>

* <span data-ttu-id="d7464-106">telemetrie op schaal van uw apparaten te ontvangen;</span><span class="sxs-lookup"><span data-stu-id="d7464-106">Receive telemetry at scale from your devices.</span></span>
* <span data-ttu-id="d7464-107">gegevens van uw apparaten naar een processor voor streaming-gebeurtenissen te routeren;</span><span class="sxs-lookup"><span data-stu-id="d7464-107">Route data from your devices to a stream event processor.</span></span>
* <span data-ttu-id="d7464-108">uploads van bestanden vanaf apparaten te ontvangen;</span><span class="sxs-lookup"><span data-stu-id="d7464-108">Receive file uploads from devices.</span></span>
* <span data-ttu-id="d7464-109">cloud-naar-apparaatberichten naar specifieke apparaten te verzenden.</span><span class="sxs-lookup"><span data-stu-id="d7464-109">Send cloud-to-device messages to specific devices.</span></span>

<span data-ttu-id="d7464-110">Met IoT-Hub kunt u zelf de back-end van uw oplossing implementeren.</span><span class="sxs-lookup"><span data-stu-id="d7464-110">You can use IoT Hub to implement your own solution back end.</span></span> <span data-ttu-id="d7464-111">IoT Hub bevat bovendien een id-register dat wordt gebruikt voor het inrichten van apparaten, hun beveiligingsreferenties en hun rechten om verbinding maken met de IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="d7464-111">In addition, IoT Hub includes an identity registry used to provision devices, their security credentials, and their rights to connect to the IoT hub.</span></span> <span data-ttu-id="d7464-112">Zie [Wat is IoT Hub?][lnk-iot-hub] voor meer informatie over IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d7464-112">To learn more about IoT Hub, see [What is IoT Hub?][lnk-iot-hub].</span></span>

<span data-ttu-id="d7464-113">Zie [Overzicht van apparaatbeheer met IoT Hub][lnk-device-management] voor meer informatie over hoe Azure IoT Hub op standaarden gebaseerd IoT-apparaatbeheer voor u mogelijk maakt, om zo uw apparaten op afstand te beheren, te configureren en bij te werken.</span><span class="sxs-lookup"><span data-stu-id="d7464-113">To learn how Azure IoT Hub enables standards-based device management for you to remotely manage, configure, and update your devices, see [Overview of device management with IoT Hub][lnk-device-management].</span></span>

<span data-ttu-id="d7464-114">U kunt de Azure IoT Device SDK's gebruiken voor het implementeren van clienttoepassingen op een groot aantal hardwareplatforms en besturingssystemen.</span><span class="sxs-lookup"><span data-stu-id="d7464-114">To implement client applications on a wide variety of device hardware platforms and operating systems, you can use the Azure IoT device SDKs.</span></span> <span data-ttu-id="d7464-115">De apparaat-SDK's bevatten bibliotheken die het eenvoudiger maken om telemetrie te verzenden naar een IoT Hub en om cloud-naar-apparaatberichten te ontvangen.</span><span class="sxs-lookup"><span data-stu-id="d7464-115">The device SDKs include libraries that facilitate sending telemetry to an IoT hub and receiving cloud-to-device messages.</span></span> <span data-ttu-id="d7464-116">Wanneer u de apparaat-SDK's gebruikt, kunt u kiezen uit verschillende netwerkprotocollen om te communiceren met IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="d7464-116">When you use the device SDKs, you can choose from several network protocols to communicate with IoT Hub.</span></span> <span data-ttu-id="d7464-117">Raadpleeg ook de [informatie over apparaat-SDK's][lnk-device-sdks].</span><span class="sxs-lookup"><span data-stu-id="d7464-117">To learn more, see the [information about device SDKs][lnk-device-sdks].</span></span>

<span data-ttu-id="d7464-118">Raadpleeg de zelfstudie [Aan de slag met IoT Hub][lnk-getstarted] als u code wilt leren schrijven en een aantal voorbeelden wilt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d7464-118">To get started writing some code and running some samples, see the [Get started with IoT Hub][lnk-getstarted] tutorial.</span></span>

<span data-ttu-id="d7464-119">Wellicht bent u ook geïnteresseerd in [Azure IoT Suite][lnk-iot-suite]. Dit is een verzameling van vooraf geconfigureerde oplossingen.</span><span class="sxs-lookup"><span data-stu-id="d7464-119">You may also be interested in [Azure IoT Suite][lnk-iot-suite], which is a collection of preconfigured solutions.</span></span> <span data-ttu-id="d7464-120">Met IoT-Suite kunt u snel aan de slag en IoT-projecten schalen om veelvoorkomende problemen met algemene IoT-scenario's op te lossen. Denk bijvoorbeeld aan externe controle, beheer van assets en voorspellend onderhoud.</span><span class="sxs-lookup"><span data-stu-id="d7464-120">IoT Suite enables you to get started quickly and scale IoT projects to address common IoT scenarios--such as remote monitoring, asset management, and predictive maintenance.</span></span>

[lnk-getstarted]: iot-hub-csharp-csharp-getstarted.md
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-iot-hub]: iot-hub-what-is-iot-hub.md
[lnk-iot-suite]: https://azure.microsoft.com/documentation/suites/iot-suite/
[lnk-iotdev]: https://azure.microsoft.com/develop/iot/
[lnk-device-management]: iot-hub-device-management-overview.md
