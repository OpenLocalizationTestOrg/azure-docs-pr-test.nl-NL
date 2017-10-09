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
# <a name="understand-and-use-azure-iot-sdks"></a>Begrijpen en gebruiken van Azure IoT SDK 's

Er zijn drie categorieën van de SDK voor het werken met IoT Hub:

* **Apparaat-SDK's** u toobuild-apps die worden uitgevoerd op uw IoT-apparaten inschakelen. Deze apps verzenden van telemetrie tooyour IoT-hub en eventueel berichten ontvangen van uw IoT-hub.

* **Service-SDK's** inschakelen toomanage u uw IoT-hub en eventueel berichten verzenden tooyour IoT-apparaten.

* **Azure IoT-rand** kunt u toobuild gateways tooenable apparaten die niet gebruikmaken van een van de protocollen hello wordt ondersteund, of wanneer u tooprocess berichten op het Hallo-rand nodig hebt.

SDK's zijn opgegeven toosupport meerdere programmeertalen.

## <a name="azure-iot-device-sdks"></a>Apparaat met Azure IoT SDK 's

Hallo Microsoft Azure IoT-apparaat-SDK's bevatten code voor gebouw apparaten en toepassingen die verbinding tooand maken worden beheerd door Azure IoT Hub-services.

Hallo zijn volgende Azure IoT-apparaat-SDK's beschikbaar toodownload vanuit GitHub:

* [Azure IoT-apparaat SDK voor C] [ lnk-c-device-sdk] geschreven in C ANSI (C99) voor brede platformcompatibiliteit en draagbaarheid. Er zijn twee apparaat clientbibliotheken voor C hello op laag niveau **iothub_client** en Hallo **serialisatiefunctie**.
* [Azure IoT-apparaat SDK voor .NET][lnk-dotnet-device-sdk]
* [Azure IoT-apparaat SDK voor Java][lnk-java-device-sdk]
* [Azure IoT-apparaat SDK voor Node.js][lnk-node-device-sdk]
* [Azure IoT-apparaat SDK voor Python][lnk-python-device-sdk]

> [!NOTE]
> Zie Hallo Leesmij-bestanden in de GitHub-opslagplaatsen Hallo voor informatie over het gebruik van taal en platform-specifieke pakket managers tooinstall binaire bestanden en afhankelijkheden op uw ontwikkelcomputer.
> 
> 

### <a name="os-platform-and-hardware-compatibility"></a>Compatibiliteit met besturingssystemen platform en hardware

Zie voor meer informatie over de compatibiliteit van de SDK met de specifieke hardware Hallo [Azure gecertificeerd voor IoT-apparaat catalogus][lnk-certified].

## <a name="azure-iot-service-sdks"></a>Azure IoT service SDK 's

Hello Azure IoT service SDK's bevatten code toofacilitate bouwen van toepassingen die rechtstreeks met de IoT Hub toomanage apparaten en beveiliging communiceren.

Hallo zijn volgende Azure IoT service SDK's beschikbaar toodownload vanuit GitHub:

* [Azure IoT service SDK voor .NET][lnk-dotnet-service-sdk]
* [Azure IoT service SDK voor Node.js][lnk-node-service-sdk]
* [Azure IoT service SDK voor Java][lnk-java-service-sdk]
* [Azure IoT service SDK voor Python][lnk-python-service-sdk]
* [Azure IoT service SDK voor C][lnk-c-service-sdk]

> [!NOTE]
> Zie Hallo Leesmij-bestanden in de GitHub-opslagplaatsen Hallo voor informatie over het gebruik van taal en platform-specifieke pakket managers tooinstall binaire bestanden en afhankelijkheden op uw ontwikkelcomputer.

## <a name="azure-iot-edge"></a>Azure IoT Edge

Azure IoT-rand bevat Hallo-infrastructuur en -modules toocreate IoT gateway-oplossingen. U kunt IoT rand toocreate gateways op maat gemaakte tooany end-to-end scenario uitbreiden.

U kunt downloaden [Azure IoT rand] [ lnk-iot-edge] vanuit GitHub.

## <a name="online-api-reference-documentation"></a>Online documentatie voor API-verwijzing

Hallo bevat volgende lijst koppelingen tooonline API-naslagdocumentatie voor Azure IoT-apparaat, service en bibliotheken van de gateway:

* [Internet der dingen (IoT) .NET][lnk-dotnet-ref]
* [IoT-Hub REST][lnk-rest-ref]
* [Azure IoT-apparaat SDK voor C][lnk-c-ref]
* [Azure IoT-apparaat SDK voor Java][lnk-java-ref]
* [Azure IoT service SDK voor Java][lnk-java-service-ref]
* [Azure IoT-apparaat SDK voor Node.js][lnk-node-ref]
* [Azure IoT service SDK voor Node.js][lnk-node-service-ref]
* [Azure IoT-rand][lnk-gateway-ref]

## <a name="next-steps"></a>Volgende stappen

Er zijn andere onderwerpen met naslaginformatie in deze handleiding voor ontwikkelaars van IoT-Hub:

* [Eindpunten van IoT-Hub][lnk-devguide-endpoints]
* [IoT Hub-querytaal voor apparaat horende, taken en het routeren van berichten][lnk-devguide-query]
* [Quota's en beperking][lnk-devguide-quotas]
* [IoT Hub MQTT-ondersteuning][lnk-devguide-mqtt]

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
