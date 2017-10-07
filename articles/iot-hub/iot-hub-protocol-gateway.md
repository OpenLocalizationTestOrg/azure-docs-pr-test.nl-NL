---
title: IoT-protocolgateway aaaAzure | Microsoft Docs
description: Hoe protocol toouse een Azure-IoT gateway tooextend Iothub mogelijkheden en protocol ondersteuning tooenable apparaten tooconnect tooyour hub met behulp van protocollen niet ondersteund door de IoT Hub.
services: iot-hub
documentationcenter: 
author: kdotchkoff
manager: timlt
editor: 
ms.assetid: 555e59ae-3136-4533-8ba8-f3a3b6acf648
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/11/2017
ms.author: kdotchko
ms.openlocfilehash: 9cfed30149672d8f7e021a9899192105bbcdd400
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# Ondersteuning voor aanvullende protocollen voor IoT Hub
Azure IoT Hub ondersteunt systeemeigen communicatie via Hallo MQTT, AMQP en HTTP-protocollen. In sommige gevallen apparaten of veld gateways mogelijk niet kunnen toouse een van deze standaardprotocollen en protocol aanpassing is vereist. In dergelijke gevallen kunt u een aangepaste gateway. Een aangepaste gateway kunt inschakelen protocol aanpassing voor eindpunten van IoT Hub bridging Hallo verkeer tooand uit IoT Hub. U kunt Hallo [protocolgateway van Azure IOT](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md) als een aangepaste gateway tooenable protocol aanpassing voor IoT Hub.

## Azure IoT-protocol-gateway
Hello Azure IoT-protocol-gateway is een raamwerk voor aanpassing protocol die is ontworpen voor bidirectionele communicatie met IoT Hub met hoge schaalbaarheid. Hallo-protocol-gateway is een Pass Through-onderdeel dat apparaatverbindingen over een specifiek protocol aanvaardt. Het verbinding Hallo-verkeer tooIoT Hub via AMQP 1.0. Hello Azure IoT-protocolgateway is beschikbaar als een open source software project tooprovide flexibiliteit voor het toevoegen van ondersteuning voor verschillende protocollen en protocolversies.

U kunt Hallo protocol-gateway in Azure implementeren in een uiterst schaalbare manier met behulp van Azure Service Fabric, Azure Cloud Services-werkrollen of Windows virtuele Machines. Bovendien kan Hallo protocol-gateway worden geïmplementeerd in on-premises omgevingen zoals veld gateways.

Hello Azure IoT-protocolgateway bevat een MQTT protocol adapter waarmee u toocustomize hello MQTT protocol gedrag indien nodig. Aangezien IoT Hub ingebouwde ondersteuning voor Hallo MQTT v3.1.1 protocol biedt, moet u alleen overwegen Hallo MQTT protocol adapter als protocol aanpassingen of specifieke vereisten voor aanvullende functionaliteit vereist zijn.

Hallo MQTT adapter ook getoond Hallo-programmeermodel voor het bouwen van protocol adapters voor andere protocollen. Bovendien kan hello Azure IoT-protocol-gateway programmeermodel tooplug in aangepaste onderdelen voor speciale verwerking zoals aangepaste verificatie, bericht transformaties, compressie/decompressie of ontsleutelen van verkeer tussen Hallo apparaten en IoT Hub.

Voor flexibiliteit, Hallo protocol-gateway en de implementatie van de protocollen MQTT vindt u in een open source software-project. Hiermee kunt u toocustomize Hallo implementatie indien nodig.

## Volgende stappen
meer informatie over hello Azure IoT-protocolgateway toolearn en hoe toouse en implementeren als onderdeel van uw IoT-oplossing, Zie:

* [Azure IoT-protocol-gateway-opslagplaats op GitHub](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md)
* [Azure IoT gateway protocol ontwikkelaarshandleiding](https://github.com/Azure/azure-iot-protocol-gateway/blob/master/docs/DeveloperGuide.md)

toolearn meer informatie over het plannen van de implementatie van uw IoT Hub, Zie:

* [Vergelijken met Event Hubs][lnk-compare]
* [Schalen, HA en Noodherstel][lnk-scaling]
* [Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide]

[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
