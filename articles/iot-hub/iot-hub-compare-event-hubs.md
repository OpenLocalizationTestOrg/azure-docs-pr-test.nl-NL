---
title: aaaCompare Azure IoT Hub tooAzure Event Hubs | Microsoft Docs
description: Een vergelijking van Hallo IoT Hub en Event Hubs Azure-services functionele verschillen en gebruiksvoorbeelden is gemarkeerd. Hallo vergelijking omvat ondersteunde protocollen, Apparaatbeheer, bewaking, en bestanden kunnen uploaden.
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: aeddea62-8302-48e2-9aad-c5a0e5f5abe9
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.openlocfilehash: e5f546b54e29860498d540abfc86a41c4662c0df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="comparison-of-azure-iot-hub-and-azure-event-hubs"></a>Vergelijking van Azure IoT Hub en Azure Event Hubs
Een van de belangrijkste gebruiksvoorbeelden Hallo voor IoT Hub is toogather telemetrie van apparaten. Om deze reden IoT Hub wordt vaak te worden vergeleken[Azure Event Hubs][Azure Event Hubs]. Zoals IoT Hub Event Hubs is een service waarmee gebeurtenissen en telemetriegegevens verzamelen voor gebeurtenisverwerking toohello cloud op grote schaal met weinig latentie en hoge betrouwbaarheid.

Hallo-services hebben echter veel verschillen, die worden beschreven in de volgende tabel Hallo:

| Onderwerp | IoT Hub | Event Hubs |
| --- | --- | --- |
| Communicatiepatronen | Hiermee [apparaat-naar-cloud communicatie] [ lnk-d2c-guidance] (messaging, file uploads en gerapporteerde eigenschappen) en [cloud-naar-apparaat communicatie] [ lnk-c2d-guidance] (direct methoden, gewenste eigenschappen, messaging). |U kunt alleen gebeurtenis Inkomend (meestal beschouwd als voor apparaat-naar-cloud-scenario's). |
| Informatie over de status van apparaat | [Apparaat horende] [ lnk-twins] kunt opslaan en opvragen van informatie over de status van apparaten. | Er is geen informatie over de status van het apparaat kan worden opgeslagen. |
| Ondersteuning voor het protocol van apparaten |Biedt ondersteuning voor protocollen MQTT, MQTT over WebSockets, AMQP, AMQP over WebSockets en HTTP. Bovendien IoT Hub werkt met Hallo [protocolgateway van Azure IOT][lnk-azure-protocol-gateway], een aanpasbare protocol-gateway-implementatie toosupport aangepaste protocollen. |AMQP, AMQP over WebSockets en HTTP ondersteunt. |
| Beveiliging |Biedt per apparaat-id en terughalen toegangsbeheer. Zie Hallo [Beveiligingssectie Hallo Ontwikkelaarshandleiding voor IoT Hub]. |Biedt Event Hubs-wide [gedeeld toegangsbeleid][Event Hubs - security], met intrekken van beperkte ondersteuning voor via [van uitgeversbeleid][Event Hubs publisher policies]. IoT-oplossingen zijn vaak tooimplement een aangepaste oplossing toosupport per apparaat van de vereiste referenties en anti-adresvervalsing metingen. |
| Controle van bewerkingen |Hiermee schakelt u IoT-oplossingen toosubscribe tooa uitgebreide set apparaat identity management en connectiviteit gebeurtenissen, zoals afzonderlijke apparaat verificatiefouten, beperking en uitzonderingen onjuiste notatie. Deze gebeurtenissen kunt u tooquickly connectiviteitsproblemen op niveau van de afzonderlijke apparaten Hallo identificeren. |Beschrijft alleen cumulatieve metrische gegevens. |
| Schalen |Is geoptimaliseerd toosupport miljoenen gelijktijdig verbonden apparaten. |Meters Hallo verbindingen conform [Azure Event Hubs quota][Azure Event Hubs quotas]. Op Hallo daarentegen, Event Hubs kunt u toospecify Hallo partitie voor elk bericht verzonden. |
| Apparaat-SDK 's |Biedt [apparaat-SKD's] [ Azure IoT SDKs] voor een groot aantal verschillende platforms en talen in toevoeging toodirect MQTT, AMQP en HTTP-APIs. |Wordt ondersteund op .NET, Java en C, in aanvulling tooAMQP en HTTP verzenden interfaces. |
| Bestand uploaden |Kunnen IoT-oplossingen tooupload bestanden van apparaten toohello cloud. Bevat een bestand meldingseindpunt voor workflow-integratie en een operationele bewaking categorie voor de ondersteuning voor foutopsporing. | Niet ondersteund. |
| Route berichten toomultiple eindpunten | Up too10 worden aangepaste eindpunten ondersteund. Regels bepalen hoe berichten gerouteerde toocustom eindpunten zijn. Zie voor meer informatie [berichten verzenden en ontvangen met IoT Hub][lnk-devguide-messaging]. | Vereist aanvullende code toobe geschreven en worden gehost voor berichtverzending. |

Kortom, zelfs als alleen gebruiksvoorbeeld Hallo telemetrie voor apparaat-naar-cloud-inkomend biedt IoT Hub een service die is ontworpen voor connectiviteit van IoT-apparaten. Tooexpand hello waardevoorstellen voor deze scenario's met IoT-specifieke functies gaat door. Event Hubs is ontworpen voor gebeurtenis inkomend grootschalige, zowel in de context Hallo van scenario's inter datacenter en intra-datacenter.

Het is niet ongewoon toouse zowel IoT Hub en Event Hubs in Hallo dezelfde oplossing. IoT Hub apparaat-naar-cloud-communicatie Hallo verwerkt en Event Hubs later stadium gebeurtenis inkomend in realtime verwerking engines afgehandeld.

### <a name="next-steps"></a>Volgende stappen
Zie toolearn meer informatie over het plannen van uw implementatie IoT Hub [schalen en HA DR][lnk-scaling].

toofurther verkennen Hallo-mogelijkheden van IoT Hub, Zie:

* [Ontwikkelaarshandleiding voor IoT Hub][lnk-devguide]
* [Een apparaat simuleren met IoT rand][lnk-iotedge]

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[Azure Event Hubs]: ../event-hubs/event-hubs-what-is-event-hubs.md
[Beveiligingssectie Hallo Ontwikkelaarshandleiding voor IoT Hub]: iot-hub-devguide-security.md
[Event Hubs - security]: ../event-hubs/event-hubs-authentication-and-security-model-overview.md
[Event Hubs publisher policies]: ../event-hubs/event-hubs-features.md#event-publishers
[Azure Event Hubs quotas]: ../event-hubs/event-hubs-quotas.md
[Azure IoT SDKs]: https://github.com/Azure/azure-iot-sdks
[lnk-azure-protocol-gateway]: iot-hub-protocol-gateway.md

[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
