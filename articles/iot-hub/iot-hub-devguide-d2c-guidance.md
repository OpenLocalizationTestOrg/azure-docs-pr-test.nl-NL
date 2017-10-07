---
title: Opties voor aaaAzure IoT Hub apparaat-naar-cloud | Microsoft Docs
description: Handleiding voor ontwikkelaars - richtlijnen voor wanneer toouse apparaat-naar-cloud-berichten, gemelde eigenschappen of bestand uploaden voor cloud-naar-apparaat communicatie.
services: iot-hub
documentationcenter: .net
author: fsautomata
manager: timlt
editor: 
ms.assetid: 979136db-c92d-4288-870c-f305e8777bdd
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: elioda
ms.openlocfilehash: 2caefc4f59e16ad28b0d8cf4b3bb627b4cba803b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="device-to-cloud-communications-guidance"></a>Richtlijnen voor apparaat-naar-cloud-communicatie
Bij het verzenden van informatie van Hallo apparaat app toohello back-end oplossing, toont IoT Hub drie opties:

* [Apparaat-naar-cloudberichten] [ lnk-d2c] voor tijd reeks Telemetrie en waarschuwingen.
* [Eigenschappen gerapporteerd] [ lnk-twins] voor het melden van status apparaatgegevens zoals mogelijkheden beschikbaar, voorwaarden of Hallo status langlopende workflows. Bijvoorbeeld, configuratie en software-updates.
* [Bestand uploaden] [ lnk-fileupload] voor media-bestanden en grote telemetrie batches geüpload door afwisselend verbonden apparaten of toosave bandbreedte gecomprimeerd.

Hier volgt een gedetailleerde vergelijking van Hallo communicatieopties voor verschillende apparaat-naar-cloud.

|  | Apparaat-naar-cloud-berichten | Gerapporteerde eigenschappen | Uploaden van bestanden |
| ---- | ------- | ---------- | ---- |
| Scenario | Telemetrie tijdreeks en waarschuwingen. Bijvoorbeeld, 256 KB sensor gegevensbatches verzonden om de 5 minuten. | Beschikbare mogelijkheden en voorwaarden. Bijvoorbeeld, Hallo huidige apparaat connectiviteitsmodus zoals Mobiel of Wi-Fi. Langlopende werkstromen, zoals configuratie en software-updates synchroniseren. | Media-bestanden. Grote (meestal gecomprimeerde) telemetrie batches. |
| Opslaan en ophalen | Tijdelijk opgeslagen door de IoT Hub too7 dagen. Alleen opeenvolgende lezen. | Opgeslagen door de IoT Hub in Hallo apparaat twin. Ophalen mogelijk met behulp van Hallo [IoT Hub-querytaal][lnk-query]. | Opgeslagen in Azure Storage-account van gebruiker. |
| Grootte | Too256 KB-berichten. | Maximum aantal gemelde eigenschappen grootte is 8 KB. | Maximale bestandsgrootte die wordt ondersteund door Azure Blob Storage. |
| Frequentie | Hoog. Zie voor meer informatie [IoT Hub beperkt][lnk-quotas]. | Normaal. Zie voor meer informatie [IoT Hub beperkt][lnk-quotas]. | Laag. Zie voor meer informatie [IoT Hub beperkt][lnk-quotas]. |
| Protocol | Beschikbaar op alle protocollen. | Momenteel alleen beschikbaar wanneer met behulp van protocollen MQTT. | Beschikbaar zijn wanneer u elk protocol voor, maar vereist HTTP op Hallo-apparaat. |

Het is mogelijk dat een toepassing tooboth verzenden gegevens als een tijdreeks telemetrie of waarschuwing en ook toomake vereist deze beschikbaar zijn in Hallo apparaat twin. In dit scenario kunt u ervoor gekozen Hallo volgende opties:

* Hallo apparaattoepassing verzendt een bericht apparaat-naar-cloud en rapporten van een wijziging van de eigenschap.
* Hallo back-end oplossing kunt Hallo gegevens opslaan in Hallo apparaat twin labels wanneer het Hallo-bericht ontvangt.

Aangezien de apparaat-naar-cloud-berichten inschakelen veel hogere doorvoer dan apparaat twin updates, is het soms wenselijk tooavoid bijwerken Hallo apparaat twin voor elk apparaat-naar-cloud-bericht.


[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-fileupload]: iot-hub-devguide-file-upload.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
