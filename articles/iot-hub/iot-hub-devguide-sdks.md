---
title: De Azure IoT SDK's begrijpen | Microsoft Docs
description: Handleiding voor ontwikkelaars - informatie over en koppelingen naar de verschillende Azure IoT-apparaat en de service SDK's die u gebruiken kunt om apps op apparaten en back-end-apps te ontwikkelen.
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: c5c9a497-bb03-4301-be2d-00edfb7d308f
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bcbf4b9633f58293edb19aeb33dec6602ac4ec8f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="understand-and-use-azure-iot-sdks"></a><span data-ttu-id="b2cdf-103">Begrijpen en gebruiken van Azure IoT SDK 's</span><span class="sxs-lookup"><span data-stu-id="b2cdf-103">Understand and use Azure IoT SDKs</span></span>

<span data-ttu-id="b2cdf-104">Er zijn drie categorieën van de SDK voor het werken met IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="b2cdf-104">There are three categories of SDK for working with IoT Hub:</span></span>

* <span data-ttu-id="b2cdf-105">**Apparaat-SDK's** kunt u voor het bouwen van apps die worden uitgevoerd op uw IoT-apparaten.</span><span class="sxs-lookup"><span data-stu-id="b2cdf-105">**Device SDKs** enable you to build apps that run on your IoT devices.</span></span> <span data-ttu-id="b2cdf-106">Deze apps verzenden van telemetrie naar uw IoT-hub en eventueel berichten ontvangen van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="b2cdf-106">These apps send telemetry to your IoT hub, and optionally receive messages from your IoT hub.</span></span>

* <span data-ttu-id="b2cdf-107">**Service-SDK's** helpen u voor het beheren van uw IoT-hub en, desgewenst berichten verzenden naar uw IoT-apparaten.</span><span class="sxs-lookup"><span data-stu-id="b2cdf-107">**Service SDKs** enable you to manage your IoT hub, and optionally send messages to your IoT devices.</span></span>

* <span data-ttu-id="b2cdf-108">**Azure IoT-rand** kunt u gateways als apparaten die niet een van de ondersteunde protocollen, of wanneer u moet voor het verwerken van berichten op de rand wilt laten maken.</span><span class="sxs-lookup"><span data-stu-id="b2cdf-108">**Azure IoT Edge** enables you to build gateways to enable devices that don't use one of the supported protocols, or when you need to process messages on the edge.</span></span>

<span data-ttu-id="b2cdf-109">SDK's zijn beschikbaar voor de ondersteuning van meerdere programmeertalen.</span><span class="sxs-lookup"><span data-stu-id="b2cdf-109">SDKs are provided to support multiple programming languages.</span></span>

## <a name="azure-iot-device-sdks"></a><span data-ttu-id="b2cdf-110">Apparaat met Azure IoT SDK 's</span><span class="sxs-lookup"><span data-stu-id="b2cdf-110">Azure IoT device SDKs</span></span>

<span data-ttu-id="b2cdf-111">Het apparaat met Microsoft Azure IoT SDK's bevatten code voor gebouw apparaten en toepassingen die verbinding maken met en worden beheerd door de services van Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="b2cdf-111">The Microsoft Azure IoT device SDKs contain code that facilitates building devices and applications that connect to and are managed by Azure IoT Hub services.</span></span>

<span data-ttu-id="b2cdf-112">Het volgende apparaat met Azure IoT SDK's kunnen worden gedownload van GitHub:</span><span class="sxs-lookup"><span data-stu-id="b2cdf-112">The following Azure IoT device SDKs are available to download from GitHub:</span></span>

* <span data-ttu-id="b2cdf-113">[Azure IoT-apparaat SDK voor C] [ lnk-c-device-sdk] geschreven in C ANSI (C99) voor brede platformcompatibiliteit en draagbaarheid.</span><span class="sxs-lookup"><span data-stu-id="b2cdf-113">[Azure IoT device SDK for C][lnk-c-device-sdk] written in ANSI C (C99) for portability and broad platform compatibility.</span></span> <span data-ttu-id="b2cdf-114">Er zijn twee apparaat clientbibliotheken voor de laag niveau C **iothub_client** en de **serialisatiefunctie**.</span><span class="sxs-lookup"><span data-stu-id="b2cdf-114">There are two device client libraries for C, the low-level **iothub_client** and the **serializer**.</span></span>
* <span data-ttu-id="b2cdf-115">[Azure IoT-apparaat SDK voor .NET][lnk-dotnet-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="b2cdf-115">[Azure IoT device SDK for .NET][lnk-dotnet-device-sdk]</span></span>
* <span data-ttu-id="b2cdf-116">[Azure IoT-apparaat SDK voor Java][lnk-java-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="b2cdf-116">[Azure IoT device SDK for Java][lnk-java-device-sdk]</span></span>
* <span data-ttu-id="b2cdf-117">[Azure IoT-apparaat SDK voor Node.js][lnk-node-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="b2cdf-117">[Azure IoT device SDK for Node.js][lnk-node-device-sdk]</span></span>
* <span data-ttu-id="b2cdf-118">[Azure IoT-apparaat SDK voor Python][lnk-python-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="b2cdf-118">[Azure IoT device SDK for Python][lnk-python-device-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="b2cdf-119">Zie het Leesmij-bestanden in de GitHub-opslagplaatsen voor informatie over het gebruik van taal en managers pakket platform-specifieke binaire bestanden en afhankelijkheden te installeren op uw ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="b2cdf-119">See the readme files in the GitHub repositories for information about using language and platform-specific package managers to install binaries and dependencies on your development machine.</span></span>
> 
> 

### <a name="os-platform-and-hardware-compatibility"></a><span data-ttu-id="b2cdf-120">Compatibiliteit met besturingssystemen platform en hardware</span><span class="sxs-lookup"><span data-stu-id="b2cdf-120">OS platform and hardware compatibility</span></span>

<span data-ttu-id="b2cdf-121">Zie voor meer informatie over de SDK compatibiliteit met bepaalde hardware-apparaten, de [Azure gecertificeerd voor IoT-apparaat catalogus][lnk-certified].</span><span class="sxs-lookup"><span data-stu-id="b2cdf-121">For more information about SDK compatibility with specific hardware devices, see the [Azure Certified for IoT device catalog][lnk-certified].</span></span>

## <a name="azure-iot-service-sdks"></a><span data-ttu-id="b2cdf-122">Azure IoT service SDK 's</span><span class="sxs-lookup"><span data-stu-id="b2cdf-122">Azure IoT service SDKs</span></span>

<span data-ttu-id="b2cdf-123">De Azure IoT service SDK's bevatten code om het te bevorderen toepassingen maken die communiceren rechtstreeks met IoT Hub voor het beheren van apparaten en beveiliging.</span><span class="sxs-lookup"><span data-stu-id="b2cdf-123">The Azure IoT service SDKs contain code to facilitate building applications that interact directly with IoT Hub to manage devices and security.</span></span>

<span data-ttu-id="b2cdf-124">De volgende Azure IoT service SDK's kunnen worden gedownload van GitHub:</span><span class="sxs-lookup"><span data-stu-id="b2cdf-124">The following Azure IoT service SDKs are available to download from GitHub:</span></span>

* <span data-ttu-id="b2cdf-125">[Azure IoT service SDK voor .NET][lnk-dotnet-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="b2cdf-125">[Azure IoT service SDK for .NET][lnk-dotnet-service-sdk]</span></span>
* <span data-ttu-id="b2cdf-126">[Azure IoT service SDK voor Node.js][lnk-node-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="b2cdf-126">[Azure IoT service SDK for Node.js][lnk-node-service-sdk]</span></span>
* <span data-ttu-id="b2cdf-127">[Azure IoT service SDK voor Java][lnk-java-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="b2cdf-127">[Azure IoT service SDK for Java][lnk-java-service-sdk]</span></span>
* <span data-ttu-id="b2cdf-128">[Azure IoT service SDK voor Python][lnk-python-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="b2cdf-128">[Azure IoT service SDK for Python][lnk-python-service-sdk]</span></span>
* <span data-ttu-id="b2cdf-129">[Azure IoT service SDK voor C][lnk-c-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="b2cdf-129">[Azure IoT service SDK for C][lnk-c-service-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="b2cdf-130">Zie het Leesmij-bestanden in de GitHub-opslagplaatsen voor informatie over het gebruik van taal en managers pakket platform-specifieke binaire bestanden en afhankelijkheden te installeren op uw ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="b2cdf-130">See the readme files in the GitHub repositories for information about using language and platform-specific package managers to install binaries and dependencies on your development machine.</span></span>

## <a name="azure-iot-edge"></a><span data-ttu-id="b2cdf-131">Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="b2cdf-131">Azure IoT Edge</span></span>

<span data-ttu-id="b2cdf-132">Azure IoT-rand bevat de volgende infrastructuur en modules om oplossingen van IoT gateway te maken.</span><span class="sxs-lookup"><span data-stu-id="b2cdf-132">Azure IoT Edge contains the infrastructure and modules to create IoT gateway solutions.</span></span> <span data-ttu-id="b2cdf-133">U kunt IoT rand voor het maken van gateways die zijn afgestemd op een end-to-end-scenario uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="b2cdf-133">You can extend IoT Edge to create gateways tailored to any end-to-end scenario.</span></span>

<span data-ttu-id="b2cdf-134">U kunt downloaden [Azure IoT rand] [ lnk-iot-edge] vanuit GitHub.</span><span class="sxs-lookup"><span data-stu-id="b2cdf-134">You can download [Azure IoT Edge][lnk-iot-edge] from GitHub.</span></span>

## <a name="online-api-reference-documentation"></a><span data-ttu-id="b2cdf-135">Online documentatie voor API-verwijzing</span><span class="sxs-lookup"><span data-stu-id="b2cdf-135">Online API reference documentation</span></span>

<span data-ttu-id="b2cdf-136">De volgende lijst bevat koppelingen naar online API-naslagdocumentatie voor Azure IoT-apparaat, service en bibliotheken van de gateway:</span><span class="sxs-lookup"><span data-stu-id="b2cdf-136">The following list contains links to online API reference documentation for Azure IoT device, service, and gateway libraries:</span></span>

* <span data-ttu-id="b2cdf-137">[Internet der dingen (IoT) .NET][lnk-dotnet-ref]</span><span class="sxs-lookup"><span data-stu-id="b2cdf-137">[Internet of Things (IoT) .NET][lnk-dotnet-ref]</span></span>
* <span data-ttu-id="b2cdf-138">[IoT-Hub REST][lnk-rest-ref]</span><span class="sxs-lookup"><span data-stu-id="b2cdf-138">[IoT Hub REST][lnk-rest-ref]</span></span>
* <span data-ttu-id="b2cdf-139">[Azure IoT-apparaat SDK voor C][lnk-c-ref]</span><span class="sxs-lookup"><span data-stu-id="b2cdf-139">[Azure IoT device SDK for C][lnk-c-ref]</span></span>
* <span data-ttu-id="b2cdf-140">[Azure IoT-apparaat SDK voor Java][lnk-java-ref]</span><span class="sxs-lookup"><span data-stu-id="b2cdf-140">[Azure IoT device SDK for Java][lnk-java-ref]</span></span>
* <span data-ttu-id="b2cdf-141">[Azure IoT service SDK voor Java][lnk-java-service-ref]</span><span class="sxs-lookup"><span data-stu-id="b2cdf-141">[Azure IoT service SDK for Java][lnk-java-service-ref]</span></span>
* <span data-ttu-id="b2cdf-142">[Azure IoT-apparaat SDK voor Node.js][lnk-node-ref]</span><span class="sxs-lookup"><span data-stu-id="b2cdf-142">[Azure IoT device SDK for Node.js][lnk-node-ref]</span></span>
* <span data-ttu-id="b2cdf-143">[Azure IoT service SDK voor Node.js][lnk-node-service-ref]</span><span class="sxs-lookup"><span data-stu-id="b2cdf-143">[Azure IoT service SDK for Node.js][lnk-node-service-ref]</span></span>
* <span data-ttu-id="b2cdf-144">[Azure IoT-rand][lnk-gateway-ref]</span><span class="sxs-lookup"><span data-stu-id="b2cdf-144">[Azure IoT Edge][lnk-gateway-ref]</span></span>

## <a name="next-steps"></a><span data-ttu-id="b2cdf-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b2cdf-145">Next steps</span></span>

<span data-ttu-id="b2cdf-146">Er zijn andere onderwerpen met naslaginformatie in deze handleiding voor ontwikkelaars van IoT-Hub:</span><span class="sxs-lookup"><span data-stu-id="b2cdf-146">Other reference topics in this IoT Hub developer guide include:</span></span>

* <span data-ttu-id="b2cdf-147">[Eindpunten van IoT-Hub][lnk-devguide-endpoints]</span><span class="sxs-lookup"><span data-stu-id="b2cdf-147">[IoT Hub endpoints][lnk-devguide-endpoints]</span></span>
* <span data-ttu-id="b2cdf-148">[IoT Hub-querytaal voor apparaat horende, taken en het routeren van berichten][lnk-devguide-query]</span><span class="sxs-lookup"><span data-stu-id="b2cdf-148">[IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query]</span></span>
* <span data-ttu-id="b2cdf-149">[Quota's en beperking][lnk-devguide-quotas]</span><span class="sxs-lookup"><span data-stu-id="b2cdf-149">[Quotas and throttling][lnk-devguide-quotas]</span></span>
* <span data-ttu-id="b2cdf-150">[IoT Hub MQTT-ondersteuning][lnk-devguide-mqtt]</span><span class="sxs-lookup"><span data-stu-id="b2cdf-150">[IoT Hub MQTT support][lnk-devguide-mqtt]</span></span>

<!-- Links and images -->

[lnk-c-device-sdk]: https://github.com/Azure/azure-iot-sdk-c
[lnk-c-service-sdk]: https://github.com/Azure/azure-iot-sdk-c/tree/master/iothub_service_client
[lnk-dotnet-device-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device
[lnk-java-device-sdk]: https://github.com/Azure/azure-iot-sdk-java/tree/master/device
[lnk-dotnet-service-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/service
[lnk-java-service-sdk]: https://github.com/Azure/azure-iot-sdk-java/tree/master/service
[lnk-node-device-sdk]: https://github.com/Azure/azure-iot-sdk-node/tree/master/device
[lnk-node-service-sdk]: https://github.com/Azure/azure-iot-sdk-node/tree/master/service
[lnk-python-device-sdk]: https://github.com/Azure/azure-iot-sdk-python/tree/master/device
[lnk-python-service-sdk]: https://github.com/Azure/azure-iot-sdk-python/tree/master/service
[lnk-certified]: https://catalog.azureiotsuite.com/
[lnk-iot-edge]: https://github.com/Azure/iot-edge

[lnk-dotnet-ref]: https://docs.microsoft.com/dotnet/api/microsoft.azure.devices
[lnk-c-ref]: https://azure.github.io/azure-iot-sdk-c/index.html
[lnk-java-ref]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.device
[lnk-node-ref]: https://azure.github.io/azure-iot-sdk-node/
[lnk-rest-ref]: https://docs.microsoft.com/rest/api/iothub/
[lnk-java-service-ref]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.service.auth
[lnk-node-service-ref]: https://azure.github.io/azure-iot-sdk-node/
[lnk-gateway-ref]: http://azure.github.io/iot-edge/api_reference/c/html/

[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
