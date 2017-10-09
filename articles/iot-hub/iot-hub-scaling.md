---
title: schalen van aaaAzure Iothub | Microsoft Docs
description: Hoe tooscale uw IoT hub toosupport uw verwachte bericht doorvoer. Bevat een overzicht van ondersteunde Hallo doorvoer voor elke laag en opties voor sharding.
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: e7bd4968-db46-46cf-865d-9c944f683832
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3b8bf6c44631c65b34b69752d9043c21db24bb01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scale-your-iot-hub-solution"></a>Schalen van uw IoT hub-oplossing
Azure IoT Hub kan tooa miljoenen gelijktijdig verbonden apparaten ondersteunen. Zie voor meer informatie [IoT Hub prijzen][lnk-pricing]. Elke eenheid IoT-Hub kunt een bepaald aantal dagelijkse berichten.

tooproperly schalen van uw oplossing, kunt u uw specifieke gebruik van IoT-Hub. Houd rekening met Hallo vereist piek doorvoer voor Hallo volgende categorieën van bewerkingen in het bijzonder:

* Apparaat-naar-cloud-berichten
* Cloud-naar-apparaat-berichten
* Registerbewerkingen voor identiteit

Bij toevoeging toothis doorvoer informatie, Zie [IoT Hub quota en vertragingen] [ IoT Hub quotas and throttles] en dienovereenkomstig ontwerpen van uw oplossing.

## <a name="device-to-cloud-and-cloud-to-device-message-throughput"></a>Apparaat-naar-cloud- en cloud-naar-apparaat bericht doorvoer
Hallo aanbevolen manier toosize een IoT Hub-oplossing is tooevaluate Hallo-verkeer op basis van per eenheid.

Apparaat-naar-cloudberichten Volg deze richtlijnen volgehouden doorvoer.

| Laag | Volgehouden doorvoer | Continue verzendsnelheid |
| --- | --- | --- |
| S1 |Up too1111 KB per minuut per eenheid<br/>(1,5 GB/dag/unit) |Gemiddelde van 278 berichten per minuut per eenheid<br/>(400.000 berichten per dag per eenheid) |
| S2 |Up too16 MB per minuut per eenheid<br/>(22.8 GB/dag/unit) |Gemiddelde van 4,167 berichten per minuut per eenheid<br/>(6 miljoen berichten per dag per eenheid) |
| S3 |Up too814 MB per minuut per eenheid<br/>(1144.4 GB/dag/unit) |Gemiddelde van 208,333 berichten per minuut per eenheid<br/>(300 miljoen berichten per dag per eenheid) |

## <a name="identity-registry-operation-throughput"></a>Identiteit register bewerking doorvoer
IoT Hub identiteit registerbewerkingen moeten niet toobe runtime-bewerkingen, zoals ze voornamelijk gerelateerde toodevice inrichten zijn.

Zie voor specifieke burst prestaties cijfers [IoT Hub quota en vertragingen][IoT Hub quotas and throttles].

## <a name="sharding"></a>Sharding
Terwijl een enkele IoT-hub toomillions van apparaten schalen kunt, vereist soms uw oplossing specifieke prestatiekenmerken die een enkele iothub kan niet worden gegarandeerd. In dat geval wordt het aanbevolen dat u uw apparaten in meerdere IoT hubs partitioneren. Meerdere IoT hubs verkeer bursts vloeiend en verkrijgen Hallo vereist doorvoer of bewerking tarieven die vereist zijn.

## <a name="next-steps"></a>Volgende stappen
toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:

* [Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide]
* [Een apparaat simuleren met Azure IoT rand][lnk-iotedge]

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[IoT Hub quotas and throttles]: iot-hub-devguide-quotas-throttling.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
