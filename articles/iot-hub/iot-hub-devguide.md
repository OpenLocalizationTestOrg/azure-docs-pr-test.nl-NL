---
title: aaaDeveloper-handleiding voor Azure IoT Hub | Microsoft Docs
description: Hello Azure IoT Hub developer guide bevat discussies van eindpunten, beveiliging, identiteitsregister hello, Apparaatbeheer, direct methoden, apparaat horende, bestandsuploads, taken, Hallo querytaal IoT Hub en messaging.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: d534ff9d-2de5-4995-bb2d-84a02693cb2e
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 2d3f18399e4cef6f9c4850a5caeb170a2d091a35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-developer-guide"></a>Azure IoT Hub developer guide

Azure IoT Hub is een volledig beheerde service waarmee stabiele en veilige tweerichtingscommunicatie tussen miljoenen apparaten inschakelen en een back-end oplossing.

Azure IoT Hub beschikt u over:

* Veilige communicatie met behulp van per apparaat beveiligingsreferenties en toegangscontrole.
* Opties voor meerdere apparaat-naar-cloud- en cloud-naar-apparaat hyperschaal communicatie.
* Waarop opslag van informatie over de status per apparaat en de metagegevens.
* Eenvoudig apparaten connectiviteit met de apparaatbibliotheken voor Hallo meest populaire talen en platforms.

Deze IoT Hub developer guide bevat Hallo artikelen te volgen:

* [Apparaat-naar-cloud communicatie richtlijnen] [ lnk-d2c-guidance] kunt u tussen apparaat-naar-cloud-berichten van apparaat twin gemelde eigenschappen en uploaden bestand kiezen.
* [Cloud-naar-apparaat communicatie richtlijnen] [ lnk-c2d-guidance] kunt u tussen rechtstreekse methoden van apparaat twin gewenste eigenschappen en cloud-naar-apparaat-berichten kiezen.
* [Apparaat-naar-cloud- en cloud-naar-apparaat met IoT Hub berichten] [ devguide-messaging] Hallo messaging worden functies beschreven (apparaat-naar-cloud en cloud-naar-apparaat) die IoT-Hub toont.
  * [Verzenden van apparaat-naar-cloudberichten tooIoT Hub][devguide-messages-d2c].
  * [Apparaat-naar-cloud-berichten lezen uit Hallo ingebouwd eindpunt][devguide-builtin].
  * [Gebruik aangepaste eindpunten en routeringsregels voor apparaat-naar-cloudberichten][devguide-custom].
  * [Verzenden van cloud naar apparaat-berichten uit IoT Hub][devguide-messages-c2d].
  * [Maken en IoT Hub berichten lezen][devguide-format].
* [Uploaden van bestanden van een apparaat] [ devguide-upload] wordt beschreven hoe u de bestanden van een apparaat kunt uploaden. Hallo artikel bevat ook informatie over onderwerpen zoals Hallo meldingen Hallo uploadproces kunt verzenden.
* [Apparaat-id's van IoT-Hub beheren] [ devguide-identities] wordt beschreven welke gegevens elk IoT-hub register identiteitsopslag en hoe u toegang tot en wijzigt.
* [Beheren van toegang tooIoT Hub] [ devguide-security] wordt Hallo security model gebruikt toogrant toegang tooIoT Hub functionaliteit beschreven voor apparaten en cloud-onderdelen. Hallo artikel bevat informatie over het gebruik van tokens en X.509-certificaten en details van Hallo machtigingen u verleent.
* [Gebruik Apparaatstatus horende toosynchronize en configuraties] [ devguide-device-twins] beschrijft Hallo *apparaat twin* concept en Hallo functionaliteit, zoals het synchroniseren van een apparaat met het apparaat worden getoond Twin. Hallo artikel bevat informatie over het Hallo-gegevens die zijn opgeslagen in een twin apparaat.
* [Een directe methode aangeroepen voor een apparaat] [ devguide-directmethods] beschrijft Hallo levenscyclus van een directe methode, informatie over hoe tooinvoke methoden op een apparaat vanuit uw back-end-app en ingang Hallo methode op uw apparaat directe.
* [Plannen van taken op meerdere apparaten] [ devguide-jobs] wordt beschreven hoe u taken op meerdere apparaten kunt plannen. Hallo artikel wordt beschreven hoe toosubmit taken die taken uitvoeren als een directe methode, het bijwerken van een apparaat met een apparaat-twin uitvoeren. Ook wordt beschreven hoe tooquery Hallo status van een taak.
* [Verwijzen naar: Kies een communicatieprotocol] [ devguide-protocol] beschrijft Hallo communicatieprotocollen dat IoT Hub voor apparaatcommunicatie ondersteunt en lijsten Hallo poorten die geopend worden moeten.
* [Referentie - IoT-hubeindpunten] [ devguide-endpoints] beschrijft Hallo verschillende eindpunten die elke IoT-hub voor runtime- en beheerbewerkingen toont. Hallo tevens wordt beschreven hoe u kunt extra eindpunten maken in uw IoT-hub en hoe toouse een veld gateway tooenable apparaten connectiviteit tooyour IoT Hub-eindpunten in scenario's voor niet-standaard.
* [Referentie - querytaal IoT Hub voor apparaat horende, taken en berichtroutering] [ devguide-query] die IoT Hub-querytaal waarmee u tooretrieve gegevens van uw hub over uw apparaat horende en taken worden beschreven.
* [Referentie - quota's en beperking] [ devguide-quotas] bevat een overzicht van Hallo quota die zijn ingesteld in Hallo service IoT Hub en Hallo beperking gedrag die u kunt toosee verwachten wanneer u een quotum overschrijdt.
* [Verwijzen naar - prijzen] [ devguide-pricing] biedt algemene informatie over de verschillende SKU's en prijzen voor IoT Hub en meer informatie over hoe verschillende functies van de IoT Hub worden gemeten als Hallo door de IoT Hub berichten.
* [Referentie - apparaat en de service SDK's] [ devguide-sdks] lijsten hello Azure IoT SDK's kunt u toodevelop apparaat en de service-apps die met uw IoT-hub communiceren. Hallo artikel bevat koppelingen tooonline API-documentatie.
* [Referentie - ondersteuning voor IoT Hub MQTT] [ devguide-mqtt] bevat gedetailleerde informatie over hoe IoT Hub Hallo MQTT protocol ondersteunt. Hallo artikel beschrijft Hallo-ondersteuning voor Hallo MQTT protocol ingebouwde toohello Azure IoT SDK's en bevat informatie over het gebruik van Hallo MQTT protocol rechtstreeks.
* [Verklarende woordenlijst] [ devguide-glossary] een lijst met algemene IoT-Hub-termen.

[devguide-messaging]: iot-hub-devguide-messaging.md
[devguide-upload]: iot-hub-devguide-file-upload.md
[devguide-identities]: iot-hub-devguide-identity-registry.md
[devguide-security]: iot-hub-devguide-security.md
[devguide-device-twins]: iot-hub-devguide-device-twins.md
[devguide-directmethods]: iot-hub-devguide-direct-methods.md
[devguide-jobs]: iot-hub-devguide-jobs.md
[devguide-endpoints]: iot-hub-devguide-endpoints.md
[devguide-quotas]: iot-hub-devguide-quotas-throttling.md
[devguide-query]: iot-hub-devguide-query-language.md
[devguide-sdks]: iot-hub-devguide-sdks.md
[devguide-mqtt]: iot-hub-mqtt-support.md
[devguide-glossary]: iot-hub-devguide-glossary.md
[devguide-pricing]: iot-hub-devguide-pricing.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[devguide-messages-d2c]: iot-hub-devguide-messages-d2c.md
[devguide-builtin]: iot-hub-devguide-messages-read-builtin.md
[devguide-custom]: iot-hub-devguide-messages-read-custom.md
[devguide-messages-c2d]: iot-hub-devguide-messages-c2d.md
[devguide-format]: iot-hub-devguide-messages-construct.md
[devguide-protocol]: iot-hub-devguide-protocols.md
