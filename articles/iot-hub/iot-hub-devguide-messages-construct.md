---
title: berichtindeling voor aaaUnderstand Azure IoT Hub | Microsoft Docs
description: Handleiding voor ontwikkelaars - descibes Hallo indeling en de verwachte inhoud van IoT Hub berichten.
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
ms.openlocfilehash: 3b1567e47bc32f70c0c252996648c4035ae81243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-read-iot-hub-messages"></a>Maken en IoT Hub berichten lezen

naadloze interoperabiliteit toosupport alle protocollen, IoT-Hub definieert een algemene berichtindeling voor alle apparaten gerichte protocollen. Deze berichtindeling wordt gebruikt voor zowel [apparaat-naar-cloud] [ lnk-d2c] en [cloud-naar-apparaat] [ lnk-c2d] berichten. Een [IoT Hub bericht] [ lnk-messaging] bestaat uit:

* Een set *Systeemeigenschappen*. Eigenschappen die IoT Hub worden geïnterpreteerd of ingesteld. Deze verzameling is een vooraf vastgesteld.
* Een set *toepassingseigenschappen*. Een woordenlijst van eigenschappen van een verbindingsreeks die de toepassing hello kunt definiëren en toegang zonder toodeserialize Hallo berichttekst. IoT Hub wordt nooit wijzigt deze eigenschappen.
* Een ondoorzichtige binaire instantie.

Namen en waarden mag alleen ASCII-alfanumerieke tekens, plus ``{'!', '#', '$', '%, '&', "'", '*', '*', '+', '-', '.', '^', '_', '`', '|', '~'}`` wanneer u:

* Apparaat-naar-cloud-berichten verzenden met de Hallo HTTP-protocol.
* Cloud-naar-apparaat-berichten verzenden.

Voor meer informatie over het tooencode en decoderen van berichten die worden verzonden met behulp van verschillende protocollen, Zie [Azure IoT SDK's][lnk-sdks].

Hallo volgende tabel geeft een lijst Hallo set Systeemeigenschappen in IoT Hub berichten.

| Eigenschap | Beschrijving |
| --- | --- |
| MessageId |Een gebruiker worden ingesteld-id voor het Hallo-bericht gebruikt voor aanvragen / antwoorden patronen. Indeling: Een hoofdlettergevoelige tekenreeks (omhoog too128 tekens lang) van ASCII-7-bits alfanumerieke tekens + `{'-', ':',’.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`. |
| Volgnummer |Een getal (uniek per apparaat wachtrij) toegewezen door de IoT Hub tooeach cloud-naar-apparaat-bericht. |
| te|Een doel dat is opgegeven in [Cloud-naar-apparaat] [ lnk-c2d] berichten. |
| ExpiryTimeUtc |Datum en tijd van de verloopdatum voor het bericht. |
| EnqueuedTime |Datum en tijd Hallo [Cloud-naar-apparaat] [ lnk-c2d] bericht is ontvangen door de IoT Hub. |
| CorrelationId |Een tekenreekseigenschap in een antwoordbericht waarin doorgaans Hallo MessageId van Hallo-aanvraag in aanvragen / antwoorden patronen. |
| Gebruikers-id |Een ID gebruikt toospecify Hallo oorsprong van berichten. Wanneer berichten worden gegenereerd door de IoT Hub, wordt de ingesteld te`{iot hub name}`. |
| ACK |Een bericht generator van feedback. Deze eigenschap wordt gebruikt in de cloud-naar-apparaatberichten toorequest Iothub toogenerate Feedbackberichten als gevolg van Hallo verbruik van het Hallo-bericht door Hallo-apparaat. Mogelijke waarden: **geen** (standaard): geen Feedbackbericht wordt gegenereerd, **positieve**: ontvangen een feedbackbericht als het Hallo-bericht is voltooid, **negatieve**: ontvangen een feedback wordt weergegeven als het Hallo-bericht is verlopen (of levering van het maximum aantal is bereikt) zonder wordt voltooid door het Hallo-apparaat of **volledige**: positieve en negatieve. Zie voor meer informatie [bericht feedback][lnk-feedback]. |
| ConnectionDeviceId |Een ID die is ingesteld door de IoT Hub apparaat-naar-cloud-berichten. Het Hallo bevat **deviceId** van Hallo-apparaat dat het Hallo-bericht verzonden. |
| ConnectionDeviceGenerationId |Een ID die is ingesteld door de IoT Hub apparaat-naar-cloud-berichten. Het Hallo bevat **generationId** (conform [identiteit apparaateigenschappen][lnk-device-properties]) van Hallo-apparaat dat het Hallo-bericht verzonden. |
| ConnectionAuthMethod |Een verificatiemethode is ingesteld door de IoT Hub apparaat-naar-cloud-berichten. Deze eigenschap bevat informatie over Hallo verificatie methode gebruikt tooauthenticate Hallo apparaat Hallo-bericht verzenden. Zie voor meer informatie [anti-adresvervalsing van apparaat toocloud][lnk-antispoofing]. |

## <a name="message-size"></a>Berichtgrootte

IoT Hub meet grootte van het bericht op een manier protocol networkdirect overweegt alleen Hallo werkelijke nettolading. Hallo-grootte in bytes wordt berekend als de som van de volgende Hallo Hallo:

* Hallo hoofdtekst grootte in bytes.
* Hallo-grootte in bytes van alle Hallo waarden van Systeemeigenschappen Hallo-bericht.
* Hallo-grootte in bytes van alle gebruikersnamen en waarden.

Namen en waarden zijn beperkt tooASCII tekens, zodat Hallo lengte van Hallo tekenreeksen gelijk is aan het Hallo-grootte in bytes.

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over limieten voor de berichtgrootte van IoT-Hub [IoT Hub quota's en beperking][lnk-quotas].

toolearn toocreate en lezen Iothub berichten in diverse programmeertalen, Zie hoe Hallo [aan de slag] [ lnk-get-started] zelfstudies.

[lnk-messaging]: iot-hub-devguide-messaging.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-get-started]: iot-hub-get-started.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-feedback]: iot-hub-devguide-messages-c2d.md#message-feedback
[lnk-device-properties]: iot-hub-devguide-identity-registry.md#device-identity-properties
[lnk-antispoofing]: iot-hub-devguide-messages-d2c.md#anti-spoofing-properties
