---
title: aaaUnderstand hello Azure IoT SDK's | Microsoft Docs
description: Handleiding voor ontwikkelaars - informatie over en koppelingen toohello verschillende Azure IoT-apparaat en de service SDK's waarmee u toobuild apparaat-apps en apps van de back-end kunt.
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
ms.openlocfilehash: e319451ca97876666e1c011ee0e1a73d0a0f1ed1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="understand-and-use-azure-iot-sdks"></a><span data-ttu-id="a77c9-103">Begrijpen en gebruiken van Azure IoT SDK 's</span><span class="sxs-lookup"><span data-stu-id="a77c9-103">Understand and use Azure IoT SDKs</span></span>

<span data-ttu-id="a77c9-104">Er zijn drie categorieën van de SDK voor het werken met IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="a77c9-104">There are three categories of SDK for working with IoT Hub:</span></span>

* <span data-ttu-id="a77c9-105">**Apparaat-SDK's** u toobuild-apps die worden uitgevoerd op uw IoT-apparaten inschakelen.</span><span class="sxs-lookup"><span data-stu-id="a77c9-105">**Device SDKs** enable you toobuild apps that run on your IoT devices.</span></span> <span data-ttu-id="a77c9-106">Deze apps verzenden van telemetrie tooyour IoT-hub en eventueel berichten ontvangen van uw IoT-hub.</span><span class="sxs-lookup"><span data-stu-id="a77c9-106">These apps send telemetry tooyour IoT hub, and optionally receive messages from your IoT hub.</span></span>

* <span data-ttu-id="a77c9-107">**Service-SDK's** inschakelen toomanage u uw IoT-hub en eventueel berichten verzenden tooyour IoT-apparaten.</span><span class="sxs-lookup"><span data-stu-id="a77c9-107">**Service SDKs** enable you toomanage your IoT hub, and optionally send messages tooyour IoT devices.</span></span>

* <span data-ttu-id="a77c9-108">**Azure IoT-rand** kunt u toobuild gateways tooenable apparaten die niet gebruikmaken van een van de protocollen hello wordt ondersteund, of wanneer u tooprocess berichten op het Hallo-rand nodig hebt.</span><span class="sxs-lookup"><span data-stu-id="a77c9-108">**Azure IoT Edge** enables you toobuild gateways tooenable devices that don't use one of hello supported protocols, or when you need tooprocess messages on hello edge.</span></span>

<span data-ttu-id="a77c9-109">SDK's zijn opgegeven toosupport meerdere programmeertalen.</span><span class="sxs-lookup"><span data-stu-id="a77c9-109">SDKs are provided toosupport multiple programming languages.</span></span>

## <a name="azure-iot-device-sdks"></a><span data-ttu-id="a77c9-110">Apparaat met Azure IoT SDK 's</span><span class="sxs-lookup"><span data-stu-id="a77c9-110">Azure IoT device SDKs</span></span>

<span data-ttu-id="a77c9-111">Hallo Microsoft Azure IoT-apparaat-SDK's bevatten code voor gebouw apparaten en toepassingen die verbinding tooand maken worden beheerd door Azure IoT Hub-services.</span><span class="sxs-lookup"><span data-stu-id="a77c9-111">hello Microsoft Azure IoT device SDKs contain code that facilitates building devices and applications that connect tooand are managed by Azure IoT Hub services.</span></span>

<span data-ttu-id="a77c9-112">Hallo zijn volgende Azure IoT-apparaat-SDK's beschikbaar toodownload vanuit GitHub:</span><span class="sxs-lookup"><span data-stu-id="a77c9-112">hello following Azure IoT device SDKs are available toodownload from GitHub:</span></span>

* <span data-ttu-id="a77c9-113">[Azure IoT-apparaat SDK voor C] [ lnk-c-device-sdk] geschreven in C ANSI (C99) voor brede platformcompatibiliteit en draagbaarheid.</span><span class="sxs-lookup"><span data-stu-id="a77c9-113">[Azure IoT device SDK for C][lnk-c-device-sdk] written in ANSI C (C99) for portability and broad platform compatibility.</span></span> <span data-ttu-id="a77c9-114">Er zijn twee apparaat clientbibliotheken voor C hello op laag niveau **iothub_client** en Hallo **serialisatiefunctie**.</span><span class="sxs-lookup"><span data-stu-id="a77c9-114">There are two device client libraries for C, hello low-level **iothub_client** and hello **serializer**.</span></span>
* <span data-ttu-id="a77c9-115">[Azure IoT-apparaat SDK voor .NET][lnk-dotnet-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="a77c9-115">[Azure IoT device SDK for .NET][lnk-dotnet-device-sdk]</span></span>
* <span data-ttu-id="a77c9-116">[Azure IoT-apparaat SDK voor Java][lnk-java-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="a77c9-116">[Azure IoT device SDK for Java][lnk-java-device-sdk]</span></span>
* <span data-ttu-id="a77c9-117">[Azure IoT-apparaat SDK voor Node.js][lnk-node-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="a77c9-117">[Azure IoT device SDK for Node.js][lnk-node-device-sdk]</span></span>
* <span data-ttu-id="a77c9-118">[Azure IoT-apparaat SDK voor Python][lnk-python-device-sdk]</span><span class="sxs-lookup"><span data-stu-id="a77c9-118">[Azure IoT device SDK for Python][lnk-python-device-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="a77c9-119">Zie Hallo Leesmij-bestanden in de GitHub-opslagplaatsen Hallo voor informatie over het gebruik van taal en platform-specifieke pakket managers tooinstall binaire bestanden en afhankelijkheden op uw ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="a77c9-119">See hello readme files in hello GitHub repositories for information about using language and platform-specific package managers tooinstall binaries and dependencies on your development machine.</span></span>
> 
> 

### <a name="os-platform-and-hardware-compatibility"></a><span data-ttu-id="a77c9-120">Compatibiliteit met besturingssystemen platform en hardware</span><span class="sxs-lookup"><span data-stu-id="a77c9-120">OS platform and hardware compatibility</span></span>

<span data-ttu-id="a77c9-121">Zie voor meer informatie over de compatibiliteit van de SDK met de specifieke hardware Hallo [Azure gecertificeerd voor IoT-apparaat catalogus][lnk-certified].</span><span class="sxs-lookup"><span data-stu-id="a77c9-121">For more information about SDK compatibility with specific hardware devices, see hello [Azure Certified for IoT device catalog][lnk-certified].</span></span>

## <a name="azure-iot-service-sdks"></a><span data-ttu-id="a77c9-122">Azure IoT service SDK 's</span><span class="sxs-lookup"><span data-stu-id="a77c9-122">Azure IoT service SDKs</span></span>

<span data-ttu-id="a77c9-123">Hello Azure IoT service SDK's bevatten code toofacilitate bouwen van toepassingen die rechtstreeks met de IoT Hub toomanage apparaten en beveiliging communiceren.</span><span class="sxs-lookup"><span data-stu-id="a77c9-123">hello Azure IoT service SDKs contain code toofacilitate building applications that interact directly with IoT Hub toomanage devices and security.</span></span>

<span data-ttu-id="a77c9-124">Hallo zijn volgende Azure IoT service SDK's beschikbaar toodownload vanuit GitHub:</span><span class="sxs-lookup"><span data-stu-id="a77c9-124">hello following Azure IoT service SDKs are available toodownload from GitHub:</span></span>

* <span data-ttu-id="a77c9-125">[Azure IoT service SDK voor .NET][lnk-dotnet-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="a77c9-125">[Azure IoT service SDK for .NET][lnk-dotnet-service-sdk]</span></span>
* <span data-ttu-id="a77c9-126">[Azure IoT service SDK voor Node.js][lnk-node-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="a77c9-126">[Azure IoT service SDK for Node.js][lnk-node-service-sdk]</span></span>
* <span data-ttu-id="a77c9-127">[Azure IoT service SDK voor Java][lnk-java-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="a77c9-127">[Azure IoT service SDK for Java][lnk-java-service-sdk]</span></span>
* <span data-ttu-id="a77c9-128">[Azure IoT service SDK voor Python][lnk-python-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="a77c9-128">[Azure IoT service SDK for Python][lnk-python-service-sdk]</span></span>
* <span data-ttu-id="a77c9-129">[Azure IoT service SDK voor C][lnk-c-service-sdk]</span><span class="sxs-lookup"><span data-stu-id="a77c9-129">[Azure IoT service SDK for C][lnk-c-service-sdk]</span></span>

> [!NOTE]
> <span data-ttu-id="a77c9-130">Zie Hallo Leesmij-bestanden in de GitHub-opslagplaatsen Hallo voor informatie over het gebruik van taal en platform-specifieke pakket managers tooinstall binaire bestanden en afhankelijkheden op uw ontwikkelcomputer.</span><span class="sxs-lookup"><span data-stu-id="a77c9-130">See hello readme files in hello GitHub repositories for information about using language and platform-specific package managers tooinstall binaries and dependencies on your development machine.</span></span>

## <a name="azure-iot-edge"></a><span data-ttu-id="a77c9-131">Azure IoT Edge</span><span class="sxs-lookup"><span data-stu-id="a77c9-131">Azure IoT Edge</span></span>

<span data-ttu-id="a77c9-132">Azure IoT-rand bevat Hallo-infrastructuur en -modules toocreate IoT gateway-oplossingen.</span><span class="sxs-lookup"><span data-stu-id="a77c9-132">Azure IoT Edge contains hello infrastructure and modules toocreate IoT gateway solutions.</span></span> <span data-ttu-id="a77c9-133">U kunt IoT rand toocreate gateways op maat gemaakte tooany end-to-end scenario uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="a77c9-133">You can extend IoT Edge toocreate gateways tailored tooany end-to-end scenario.</span></span>

<span data-ttu-id="a77c9-134">U kunt downloaden [Azure IoT rand] [ lnk-iot-edge] vanuit GitHub.</span><span class="sxs-lookup"><span data-stu-id="a77c9-134">You can download [Azure IoT Edge][lnk-iot-edge] from GitHub.</span></span>

## <a name="online-api-reference-documentation"></a><span data-ttu-id="a77c9-135">Online documentatie voor API-verwijzing</span><span class="sxs-lookup"><span data-stu-id="a77c9-135">Online API reference documentation</span></span>

<span data-ttu-id="a77c9-136">Hallo bevat volgende lijst koppelingen tooonline API-naslagdocumentatie voor Azure IoT-apparaat, service en bibliotheken van de gateway:</span><span class="sxs-lookup"><span data-stu-id="a77c9-136">hello following list contains links tooonline API reference documentation for Azure IoT device, service, and gateway libraries:</span></span>

* <span data-ttu-id="a77c9-137">[Internet der dingen (IoT) .NET][lnk-dotnet-ref]</span><span class="sxs-lookup"><span data-stu-id="a77c9-137">[Internet of Things (IoT) .NET][lnk-dotnet-ref]</span></span>
* <span data-ttu-id="a77c9-138">[IoT-Hub REST][lnk-rest-ref]</span><span class="sxs-lookup"><span data-stu-id="a77c9-138">[IoT Hub REST][lnk-rest-ref]</span></span>
* <span data-ttu-id="a77c9-139">[Azure IoT-apparaat SDK voor C][lnk-c-ref]</span><span class="sxs-lookup"><span data-stu-id="a77c9-139">[Azure IoT device SDK for C][lnk-c-ref]</span></span>
* <span data-ttu-id="a77c9-140">[Azure IoT-apparaat SDK voor Java][lnk-java-ref]</span><span class="sxs-lookup"><span data-stu-id="a77c9-140">[Azure IoT device SDK for Java][lnk-java-ref]</span></span>
* <span data-ttu-id="a77c9-141">[Azure IoT service SDK voor Java][lnk-java-service-ref]</span><span class="sxs-lookup"><span data-stu-id="a77c9-141">[Azure IoT service SDK for Java][lnk-java-service-ref]</span></span>
* <span data-ttu-id="a77c9-142">[Azure IoT-apparaat SDK voor Node.js][lnk-node-ref]</span><span class="sxs-lookup"><span data-stu-id="a77c9-142">[Azure IoT device SDK for Node.js][lnk-node-ref]</span></span>
* <span data-ttu-id="a77c9-143">[Azure IoT service SDK voor Node.js][lnk-node-service-ref]</span><span class="sxs-lookup"><span data-stu-id="a77c9-143">[Azure IoT service SDK for Node.js][lnk-node-service-ref]</span></span>
* <span data-ttu-id="a77c9-144">[Azure IoT-rand][lnk-gateway-ref]</span><span class="sxs-lookup"><span data-stu-id="a77c9-144">[Azure IoT Edge][lnk-gateway-ref]</span></span>

## <a name="next-steps"></a><span data-ttu-id="a77c9-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="a77c9-145">Next steps</span></span>

<span data-ttu-id="a77c9-146">Er zijn andere onderwerpen met naslaginformatie in deze handleiding voor ontwikkelaars van IoT-Hub:</span><span class="sxs-lookup"><span data-stu-id="a77c9-146">Other reference topics in this IoT Hub developer guide include:</span></span>

* <span data-ttu-id="a77c9-147">[Eindpunten van IoT-Hub][lnk-devguide-endpoints]</span><span class="sxs-lookup"><span data-stu-id="a77c9-147">[IoT Hub endpoints][lnk-devguide-endpoints]</span></span>
* <span data-ttu-id="a77c9-148">[IoT Hub-querytaal voor apparaat horende, taken en het routeren van berichten][lnk-devguide-query]</span><span class="sxs-lookup"><span data-stu-id="a77c9-148">[IoT Hub query language for device twins, jobs, and message routing][lnk-devguide-query]</span></span>
* <span data-ttu-id="a77c9-149">[Quota's en beperking][lnk-devguide-quotas]</span><span class="sxs-lookup"><span data-stu-id="a77c9-149">[Quotas and throttling][lnk-devguide-quotas]</span></span>
* <span data-ttu-id="a77c9-150">[IoT Hub MQTT-ondersteuning][lnk-devguide-mqtt]</span><span class="sxs-lookup"><span data-stu-id="a77c9-150">[IoT Hub MQTT support][lnk-devguide-mqtt]</span></span>

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
