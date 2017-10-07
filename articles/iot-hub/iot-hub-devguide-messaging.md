---
title: messaging-aaaUnderstand Azure IoT Hub | Microsoft Docs
description: Handleiding voor ontwikkelaars - apparaat-naar-cloud- en cloud-naar-apparaat met IoT Hub berichten. Bevat informatie over berichtindelingen en ondersteunde communicatieprotocollen.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3fc5f1a3-3711-4611-9897-d4db079b4250
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: a610741e23e243f392f1c042f9ab4a00d42f734f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="device-to-cloud-and-cloud-to-device-messaging-with-iot-hub"></a>Apparaat-naar-cloud- en cloud-naar-apparaat met IoT Hub messaging

Gebruik IoT Hub berichten toocommunicate met uw apparaten met:

* Verzenden van [apparaat-naar-cloud] [ lnk-d2c] berichten van uw apparaten tooyour oplossing back-end.
* Verzenden van [cloud-naar-apparaat] [ lnk-c2d] berichten van Hallo oplossing terug eindigen tooyour apparaten.

Core-eigenschappen van de IoT Hub messaging-functionaliteit zijn Hallo betrouwbaarheid en duurzaamheid van berichten. Deze eigenschappen herstelmogelijkheden toointermittent connectiviteit op Hallo apparaat aan clientzijde inschakelen en tooload bereikt in gebeurtenisverwerking Hallo cloud-zijde. IoT Hub implementeert *ten minste eenmaal* levering wordt gegarandeerd dat voor zowel cloud-naar-apparaat als apparaat-naar-cloud-berichten.

Zie voor een inleiding toohello mogelijkheden van IoT Hub, Hallo artikelen [Azure en Internet der dingen] [ lnk-azure-iot] en [overzicht van de service Azure IoT Hub Hallo] [lnk-iot-hub-overview].

## <a name="when-toouse-iot-hub-messaging"></a>Wanneer toouse Iothub messaging

Apparaat-naar-cloud-berichten voor het verzenden van time series Telemetrie en waarschuwingen uit de app op uw apparaat en cloud-naar-apparaat-berichten voor eenzijdige meldingen tooyour apparaat app gebruiken.

* Raadpleeg te[apparaat-naar-cloud communicatie richtlijnen] [ lnk-d2c-guidance] indien in waarover twijfel bestaat tussen het gebruik van apparaat-naar-cloud-berichten, gemelde eigenschappen of bestand uploaden.
* Raadpleeg te[Cloud-naar-apparaat communicatie richtlijnen] [ lnk-c2d-guidance] indien in waarover twijfel bestaat tussen het gebruik van cloud-naar-apparaat-berichten, gewenste eigenschappen of directe methoden.

## <a name="next-steps"></a>Volgende stappen

* Meer informatie over IoT Hub [apparaat-naar-cloud messaging][lnk-d2c].
* Meer informatie over IoT Hub [cloud-naar-apparaat messaging][lnk-c2d].

[lnk-azure-iot]: iot-hub-what-is-azure-iot.md
[lnk-iot-hub-overview]: iot-hub-what-is-iot-hub.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md