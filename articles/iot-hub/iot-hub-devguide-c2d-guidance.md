---
title: Opties voor aaaAzure IoT Hub cloud-naar-apparaat | Microsoft Docs
description: Handleiding voor ontwikkelaars - richtlijnen voor wanneer toouse directe methoden van apparaat twin gewenste eigenschappen of cloud-naar-apparaat-berichten voor cloud-naar-apparaat communicatie.
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: 1ac90923-1edf-4134-bbd4-77fee9b68d24
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: elioda
ms.openlocfilehash: bb95445054fa2711e34fc1d928c3665e0246c81c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="cloud-to-device-communications-guidance"></a>Cloud-naar-apparaat communicatie richtlijnen
IoT Hub biedt drie opties voor apparaat apps tooexpose functionaliteit tooa back-endserver voor apps:

* [Directe methoden] [ lnk-methods] voor communicatie waarvoor onmiddellijke bevestiging van Hallo resultaat. Rechtstreekse methoden worden vaak gebruikt voor interactief beheer van apparaten zoals het inschakelen van een ventilator.
* [Dubbele eigenschappen van de gewenste] [ lnk-twins] langlopende opdrachten bestemd tooput Hallo apparaat in een bepaalde status gewenst. Bijvoorbeeld, Hallo telemetrie verzenden interval too30 minuten ingesteld.
* [Cloud-naar-apparaatberichten] [ lnk-c2d] voor eenzijdige meldingen toohello apparaat app.

Hier volgt een gedetailleerde vergelijking van Hallo verschillende cloud-naar-apparaat communicatieopties.

|  | Directe methoden | De gewenste eigenschappen van Twin | Cloud-naar-apparaat-berichten |
| ---- | ------- | ---------- | ---- |
| Scenario | Opdrachten waarvoor onmiddellijke bevestiging, zoals het inschakelen van een ventilator nodig. | Langlopende opdrachten bedoeld tooput Hallo apparaat in een bepaalde gewenste status. Bijvoorbeeld, Hallo telemetrie verzenden interval too30 minuten ingesteld. | Eenzijdige meldingen toohello apparaattoepassing. |
| Gegevensstroom | Twee richtingen. Hallo apparaattoepassing kan meteen toohello methode reageren. Hallo back-end oplossing ontvangt Hallo uitkomst contextueel toohello aanvraag. | Eenzijdige. Hallo apparaattoepassing ontvangt een melding bij wijziging van de eigenschap Hallo. | Eenzijdige. Hallo apparaattoepassing ontvangt het Hallo-bericht
| Duurzaamheid | Niet-verbonden apparaten geen contact wordt opgenomen. Hallo back-end oplossing wordt gemeld dat het Hallo-apparaat niet is verbonden. | Eigenschapswaarden blijven in Hallo apparaat twin behouden. Apparaat wordt lezen op de volgende opnieuw verbinding te maken. Eigenschapswaarden zijn opgehaald Hello [IoT Hub-querytaal][lnk-query]. | Berichten worden behouden door de IoT Hub voor too48 uur. |
| Doelen | Met behulp van één apparaat **deviceId**, of meerdere apparaten met behulp van [taken][lnk-jobs]. | Met behulp van één apparaat **deviceId**, of meerdere apparaten met behulp van [taken][lnk-jobs]. | Eén apparaat door **deviceId**. |
| Grootte | Up too8KB aanvragen en antwoorden van 8KB. | Maximum aantal gewenste grootte van de eigenschappen van 8KB. | Too64KB berichten. |
| Frequentie | Hoog. Zie voor meer informatie [IoT Hub beperkt][lnk-quotas]. | Normaal. Zie voor meer informatie [IoT Hub beperkt][lnk-quotas]. | Laag. Zie voor meer informatie [IoT Hub beperkt][lnk-quotas]. |
| Protocol | Momenteel alleen beschikbaar wanneer met behulp van protocollen MQTT. | Momenteel alleen beschikbaar wanneer met behulp van protocollen MQTT. | Beschikbaar op alle protocollen. Apparaat moet controleren als u HTTP gebruikt. |

Meer informatie over hoe toouse methoden, eigenschappen van de gewenste en cloud-naar-apparaat-berichten rechtstreeks in de volgende zelfstudies Hallo:

* [Directe methoden gebruiken][lnk-methods-tutorial], voor rechtstreekse methoden;
* [Eigenschappen van de gewenste tooconfigure apparaten gebruiken][lnk-twin-properties]voor apparaat twin de gewenste eigenschappen; 
* [Cloud-naar-apparaat-berichten verzenden][lnk-c2d-tutorial], voor cloud-naar-apparaat-berichten.

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-jobs]: iot-hub-devguide-jobs.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-methods]: iot-hub-devguide-direct-methods.md
[lnk-methods-tutorial]: iot-hub-node-node-direct-methods.md
[lnk-twin-properties]: iot-hub-node-node-twin-how-to-configure.md
[lnk-c2d-tutorial]: iot-hub-node-node-c2d.md
